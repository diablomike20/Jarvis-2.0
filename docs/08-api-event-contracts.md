# 08 — JARVIS UNIFIED API / IPC / eseményszerződés (PROPOSED)

**Ez normatív terv, nem meglévő implementáció.** Nincs még PyGPT–FCC és GUI–PyGPT protokoll implementálva a célrepóban. A szerződés célja a folyamatfüggőségek és duplikált eszközhívások ellenőrzése.

## Transport és processzek

Első körben localhost HTTP/JSON + Server-Sent Events az eseményekhez; a PyGPT belső Qt API-k nem kerülnek közvetlenül publikálásra. Lehetséges későbbi named-pipe Windows vagy gRPC, de ezek külön döntést és bizonyítékot igényelnek. A provider API transport (FCC: /v1/messages, /v1/responses) nem azonos a JARVIS belső task API-jával.

Minden esemény eredete explicit: USER, JARVIS_GUI, JARVIS_SUPERVISOR, PYGPT_AGENT, FCC_GATEWAY, FCC_CODING_AGENT, EXTENSION.

## Ajánlott envelope v1

~~~json
{
  "schema_version": "1.0.0",
  "event_id": "uuid-v4",
  "correlation_id": "uuid-v4",
  "causation_id": "uuid-v4-or-null",
  "task_id": "uuid-v4",
  "session_id": "uuid-v4",
  "actor_id": "pygpt:agent:planner",
  "event_type": "task.progress",
  "created_at": "2026-10-16T00:00:00Z",
  "sequence": 12,
  "payload": { "stage": "testing", "percent": null },
  "trace_id": "opaque-trace-id",
  "idempotency_key": "scope-task-command-v1"
}
~~~

Egyazon task_id alatt növekvő sequence, monoton vagy deduplikálható event_id. Időbélyeg UTC, a GUI a felhasználói időzónában formázhat. Az eseményeket a receiver soha nem fogadhatja el jogosultságellenőrzés nélkül.

## Task állapotgép

CREATED → ACCEPTED → PLANNED → RUNNING → WAITING_TOOL / WAITING_APPROVAL / RETRYING → RUNNING → SUCCEEDED / FAILED / CANCELLED. Egy tasknak egyszerre pontosan egy aktív fő státusza lehet. A végállapotok terminálisak; out-of-order esemény nem élesztheti fel a befejezett munkát.

- task.created: cél, constraints, workspace_ref, request_id, user approval policy.
- task.accepted: owner, capability route, budget.
- task.progress: állapot/phase, log referencia, nem hamis %-érték.
- task.tool.requested: tool_id, args digest, read/write classification.
- task.approval.requested: human-readable action, exact machine command for detail, TTL.
- task.approval.decided: signed decision / approved action digest / expiry.
- task.tool.result: output ref, exit code, side-effect summary.
- task.cancel.requested / task.cancelled: child process termination, tool stop ack.
- task.failed: typed error, retryable flag, recovery note, no secret-bearing stacktrace.
- task.succeeded: result, evidence links, tests and artifacts.

## Jóváhagyás

Az agent **nem adhat önmagának** approval tokent. Approval csak UI felhasználói interakcióból vagy előzetesen jóváhagyott explicit policyból származhat. A token egyszeri, parancs digestre, workspace-re, actorra, taskra, TTL-re korlátozott. Változott argumentumoknál új jóváhagyás kell. High-risk: shell, file write/delete, Git push/merge, API admin, email, internet-küldés, model spend, native process injection.

## Idempotencia és retry

- Mutáció nélkül: bounded automatic retry lehetséges rate-limitnél vagy timeouts esetén.
- Külső mutáció: egyező request_id/idempotency_key hiányában NEM automatikusan újraküldhető.
- Félbeszakadt stream: event_id + sequence alapján resume vagy explicit fail, nem duplán végrehajtott parancs.
- Agent vagy provider model fallback nem változtathatja csendben a privacy/cost/jogosultsági szabályokat.
- Slow/stale UI response: task generation és correlation ellenőrzés, késői eredmények nem írhatják felül az újat.

## Hibaosztályok (javasolt)

INVALID_ARGUMENT; CAPABILITY_UNSUPPORTED; AUTH_REQUIRED; FORBIDDEN; APPROVAL_REQUIRED; APPROVAL_EXPIRED; PROVIDER_UNAVAILABLE; RATE_LIMITED; TIMEOUT; CANCELLED; CONFLICT; STALE_RESPONSE; UPSTREAM_PROTOCOL_ERROR; PARTIAL_RESULT; UNVERIFIED_RESULT; SANDBOX_DENIED; LICENSE_BLOCKED; INTERNAL.

## Health / supervison

- /internal/health/live — folyamat él.
- /internal/health/ready — függőségek és adapter konfiguráció rendben.
- /internal/capabilities — route, provider feature-gate, enabled status.
- /internal/tasks/{task_id} — csak saját authorized task.
- /internal/events?task_id=... — SSE stream, event replay boundary.
- /internal/approvals/{approval_id} — explicit UI döntés.
- /internal/logs/{trace_id} — redaktált diagnosztika.

Ezek nem meglevő végpontok, hanem javasolt JARVIS köztes API.

## FCC compat layer contract

PyGPT request → capability checks → FCC provider/managed agent → SSE translation → PyGPT result. Tool-calling JSON, message role, thinking blokk, multi-modal attachment, content-usage, rate limits és stop_reason pontosan fordítandó. A szabály nem garantál minden FCC modellnél full multimodal kompatibilitást: az unsupported native PyGPT útvonalon maradhat.

## Producer–consumer minőségbiztosítás

Schema version mismatch → explicit reject; unknown event types → typed warning; max size, bounded queue, cancellation, replay window, backpressure, auth, secrets redaction, process crash/restart replay és task ownership. Szükséges: JSON schema fájlok és contract tesztek implementációkor.
