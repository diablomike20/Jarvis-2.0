# 12 — Elfogadási tesztmátrix és regressziós terv

**Állapot:** tesztSPEC, egyetlen alábbi tesztet sem igazoltunk automatikusan PASS-nak. A P1 GitHub létrehozási műveleteinek tényeit a migrációs napló külön tartalmazza; ettől a teljes checkout test még NOT_RUN.

## Státusz és kötelező bizonyíték

NOT_RUN, PASS, FAIL, BLOCKED, SKIPPED_APPROVED. PASS esetén szükséges: test ID, branch, head SHA, Python/OS, futtatott parancs, exit code, napló vagy screenshot/hash, futtató/megismételhetőség, legutóbbi dátum. A változó provider hozzáférés BLOCKED_BY_CREDENTIAL, nem hamis PASS.

## 74 követelmény

| ID | Fázis | Követelmény | Alapstátusz |
|---|---|---|---|
| BASE-001 | P0 | Base source commits match locked SHAs | NOT_RUN |
| BASE-002 | P0 | Target main unchanged from initial SHA | NOT_RUN |
| BASE-003 | P0 | License and dependency manifest traced for all shipped components | NOT_RUN |
| BASE-004 | P0 | Original JARVIS HUD screenshot/video baseline recorded | NOT_RUN |
| BASE-005 | P0 | Isolated PySide6 Qt feasibility prototype passes | NOT_RUN |
| REPO-001 | P1 | Document branch created and readable | NOT_RUN |
| REPO-002 | P1 | Integration branch isolated from main | NOT_RUN |
| REPO-003 | P1 | Submodules point to immutable commits | NOT_RUN |
| REPO-004 | P1 | Recursive clone succeeds and source HEADs match | NOT_RUN |
| REPO-005 | P1 | Full source rehydrate/recovery procedure documented | NOT_RUN |
| PY-001 | P2 | PyGPT Windows Python env created from lock | NOT_RUN |
| PY-002 | P2 | PyGPT Qt GUI launches and exits cleanly | NOT_RUN |
| PY-003 | P2 | PyGPT chat sends and receives model answer | NOT_RUN |
| PY-004 | P2 | PyGPT baseline plugins registry loads | NOT_RUN |
| PY-005 | P2 | 16 built-in app tools discoverable | NOT_RUN |
| PY-006 | P2 | One trusted Add-on installed from immutable ref | NOT_RUN |
| PY-007 | P2 | One Skill selected and executed | NOT_RUN |
| PY-008 | P2 | One local, harmless MCP works end-to-end | NOT_RUN |
| PY-009 | P2 | Nonexistent MCP fails closed and is classified | NOT_RUN |
| PY-010 | P2 | Risky system tool is denied by permission policy | NOT_RUN |
| PY-011 | P2 | RAG sample document round-trip and citation verified | NOT_RUN |
| PY-012 | P2 | Invalid provider key produces typed failure | NOT_RUN |
| PY-013 | P2 | PyGPT agents v2 task lifecycle trace | NOT_RUN |
| PY-014 | P2 | No function loss after Add-on installation | NOT_RUN |
| FCC-001 | P3 | FCC separate Python 3.14.7 process runs | NOT_RUN |
| FCC-002 | P3 | Localhost-only listener verified | NOT_RUN |
| FCC-003 | P3 | Admin endpoint requires auth | NOT_RUN |
| FCC-004 | P3 | Default static tokens absent | NOT_RUN |
| FCC-005 | P3 | Messages API happy path | NOT_RUN |
| FCC-006 | P3 | Responses API happy path | NOT_RUN |
| FCC-007 | P3 | Token count API checks | NOT_RUN |
| FCC-008 | P3 | Streaming chunks arrive in order | NOT_RUN |
| FCC-009 | P3 | Tool call JSON schema/args survive protocol translation | NOT_RUN |
| FCC-010 | P3 | Reasoning block/finish reason survives mapping | NOT_RUN |
| FCC-011 | P3 | Invalid model fails with typed error | NOT_RUN |
| FCC-012 | P3 | Rate limit and backoff tests | NOT_RUN |
| FCC-013 | P3 | Model fallback respects privacy/cost policy | NOT_RUN |
| FCC-014 | P3 | Permission deny stops coding tool | NOT_RUN |
| FCC-015 | P3 | Cancellation terminates child process | NOT_RUN |
| FCC-016 | P3 | Code session in isolated Git worktree | NOT_RUN |
| FCC-017 | P3 | Secrets excluded from logs | NOT_RUN |
| FCC-018 | P3 | PyGPT native provider unaffected | NOT_RUN |
| E2E-001 | P4 | PyGPT orchestrator delegates to FCC exactly once | NOT_RUN |
| E2E-002 | P4 | No circular task delegation | NOT_RUN |
| E2E-003 | P4 | No duplicate writes after SSE disconnect/retry | NOT_RUN |
| E2E-004 | P4 | Task cancel idempotent | NOT_RUN |
| E2E-005 | P4 | Stale responses cannot overwrite new state | NOT_RUN |
| E2E-006 | P4 | Mixed native/remote routing works | NOT_RUN |
| E2E-007 | P4 | Crash/restart replays accurate task status | NOT_RUN |
| E2E-008 | P4 | Approval expires and denies | NOT_RUN |
| E2E-009 | P4 | Memory persists and is workspace isolated | NOT_RUN |
| E2E-010 | P4 | Rollback to stable baseline succeeds | NOT_RUN |
| UI-001 | P5 | Original JARVIS animation asset hashes matched | NOT_RUN |
| UI-002 | P5 | Frame screenshot baseline comparison | NOT_RUN |
| UI-003 | P5 | DPI scaling and multi-monitor parity | NOT_RUN |
| UI-004 | P5 | Window transparency/topmost parity | NOT_RUN |
| UI-005 | P5 | QThread shutdown race absent | NOT_RUN |
| UI-006 | P5 | QWebEngine IPC and origin validation | NOT_RUN |
| UI-007 | P5 | Mic listening states map to animation | NOT_RUN |
| UI-008 | P5 | TTS waveform maps to animation | NOT_RUN |
| UI-009 | P5 | Interrupt during speech is synchronous | NOT_RUN |
| UI-010 | P5 | Tool approval overlay deny/approve work | NOT_RUN |
| UI-011 | P5 | Every required PyGPT feature reachable from HUD | NOT_RUN |
| UI-012 | P5 | Expert GUI fallback if retained | NOT_RUN |
| EX-001 | P6 | Hungarian TTS pronunciation quality measured | NOT_RUN |
| EX-002 | P6 | Voice model rights and provenance cleared | NOT_RUN |
| EX-003 | P6 | PhotoCraft feature contract tested | NOT_RUN |
| EX-004 | P6 | LightCraft feature contract tested | NOT_RUN |
| EX-005 | P6 | FilmCraft feature contract tested | NOT_RUN |
| EX-006 | P6 | FreeCAD adapter param and export tests | NOT_RUN |
| EX-007 | P6 | Optional IronRAG benchmark over PyGPT RAG | NOT_RUN |
| EX-008 | P6 | Optional REA isolation/evidence tests | NOT_RUN |
| EX-009 | P6 | Optional Barehands gesture false-positive tests | NOT_RUN |
| EX-010 | P6 | Windows packaging, reinstall and rollback | NOT_RUN |

## Minőségi kapuk

- P2 a PY-001–014 releváns PASS nélkül nem fogadható el; külső credentialt igénylő betöltő/csatlakozó lehet dokumentált BLOCKED, ha opcionális.
- P3 FCC-001–018 teszt és legalább egy valódi integrált feladat.
- P4 E2E-001–010 negatív tesztekkel; crash/retry/approval különösen.
- P5 UI-001–012, original JARVIS animáció megőrzés.
- P6 csak a bekapcsolt extrák EX-tesztje kötelező; el nem fogadott kutatási jelölt marad PARKED.
- Minden buildjelezéshez security és source-license scan, nem csak funkcionális happy path.

## Tesztfolyam tervezete

1. Frozen source baseline + workspace snapshot.
2. Smoke tests for Qt/provider/plugins.
3. Unit tests a bridge mappingra.
4. Contract tests local HTTP/SSE event stream.
5. Integration tests külön processz és hibaállapot.
6. Regression tests PyGPT alapképességek, JARVIS eredeti GUI később.
7. Restore baseline + tests after rollback.
8. Human explicit acceptance signed decision and release note.

Machine-readable tesztek: catalog/acceptance-tests.v1.json. A teszt futtatását végző eszközre még nincs elkészült harness.
