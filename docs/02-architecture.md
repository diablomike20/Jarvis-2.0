# 02 — Célarchitektúra és belső határok

**Állapot: PROPOSED; az integráció még nem futtatott.**

## Miért a PyGPT a gerinc?

A PyGPT már tartalmaz chat/agents felületet, Agents V2 koordinációt, RAG, plugin, MCP/Skills/Extension mechanizmusokat, multimodális adaptereket, fájlokat és beépített eszközöket. Az eredeti JARVIS/Brahma GUI a felhasználói élményt adja. FCC a modellszolgáltató gateway és külön coding-agent futás. Az architektúra célja a különböző szerepek és erőforrások ütközésének megelőzése.

## Logikai felépítés

~~~text
[ JARVIS HUD / PyQt6 -> később PySide6 port ]
      | user input, state subscription, voice, confirmations
      v
[ JARVIS Supervisor / Permission Service / Event Broker ]
      | versioned IPC; local authenticated API; task IDs
      v
[ PyGPT Qt runtime + Agents V2 + MCP + Skills + RAG ]
      |                     |                   |
      | native providers    | skill tools       | persistent knowledge
      v                     v                   v
[ LLM native API ]    [Addon sandbox]     [PyGPT database/indexes]
      |
      +---- optional FCC adapter ---> [ai_proxy_2 / FCC Python 3.14.7]
                                          | 61 provider catalog entries
                                          | 11 coding clients/harnesses
                                          v
                                    [model/agent backends]
                 optional P6: REA, VoiceStudio, IronRAG, creative modules
~~~

A rajz logikai, NEM jelenleg működő implementáció.

## Folyamat- és Python-határok

- JARVIS main.py/ui.py: jelenlegi PyQt6, GUI-orientált saját runtime.
- PyGPT: Python >=3.10 és <3.14; PySide6/Qt; maga a core jelentős része MainWindow/controller függőségű.
- FCC új upstream: Python ==3.14.7; külön virtualenv/processz kötelező.
- A PyQt6 és PySide6 Qt-binding ugyanazon processzben való erőltetése helyett GUI-port próba, illetve időszakos IPC híd.
- Plugin install és model/voice natív függőségek külön környezetekbe kerüljenek, függőségek SHA/pin kontrollja mellett.
- Az FCC helyben csak 127.0.0.1-en, explicit hitelesítéssel működjön; upstream default hálózat/hitelesítés nem elfogadott.

## Felelősségek és kizárólagos tulajdonjog

| Erőforrás/feladat | Egyetlen író / gazda | Más rendszerek |
|---|---|---|
| Global task state | JARVIS task registry/supervisor | Olvasás és események |
| AI feladat-delegálás | PyGPT Orchestrator | FCC coding agent feladatdelegált |
| Coding session state | FCC saját managed session | PyGPT/JARVIS lekérdezés |
| Chat/task domain memória | PyGPT | JARVIS adapterrel kérdez |
| Projekt dokumentum-tudástár | PyGPT RAG elsőként | IronRAG P6 opcionális, mérés után |
| GUI állapot | JARVIS UI store | Backend események |
| Jóváhagyások | JARVIS Permission Service | Minden agent megáll és kér |
| Központi naplók | JARVIS Supervisor/observability | Források trace ID-t küldenek |
| Source checkout | Branch/worktree felelős | Többi agent csak diff/review |
| Secrets | OS keychain/env/secret-store | Tokenérték nincs logban/docban |

## Feladatéletciklus (terv)

CREATED → ACCEPTED → PLANNED → RUNNING → WAITING_APPROVAL / WAITING_TOOL / RETRYING → SUCCEEDED / FAILED / CANCELLED. Engedélyezett átmeneteket független teszt rögzíti. CANCELLED után nem maradhat felügyelet nélküli child-process vagy írás.

Az orchestration manager legyen egy. A PyGPT egyik agentje delegálhat FCC coding sessiont, de FCC nem hozhat létre új, önálló központi JARVIS taskot azonos idempotency key nélkül.

## Provider-routing (terv)

1. Kérés jellege felismerve (chat/tool/media/coding/realtime).
2. Kiválasztjuk a natív PyGPT adaptert vagy FCC API útvonalat.
3. Capability matrix ellenőrzi: function calls, SSE, JSON schema, reasoning, images, audio, video, long context, rate limits.
4. Ha egy capability nem támogatott FCC-n, a natív útvonal marad.
5. Retry csak idempotens, adatmentes vagy deduplikálható műveleten automatikus; írási művelet újraküldése jóváhagyás nélkül TILOS.
6. Fallback a felhasználói privacy/billing szabályok megőrzésével.

## Memória

Ne induljon három konkurrens memory loop. PyGPT legyen elsődleges beszélgetési/munkamenet-memória. Később Memory Vault lehet szerkeszthető Markdown-tár, IronRAG műszaki dokumentum-RAG; saját forrásazonosító, revízió, törlés/szinkron felügyelet szükséges. Alkalmazás-memória és indexes dokumentum kétszeres automatikus tanítása kerülendő.

## JARVIS HUD

Az eredeti HUD kinézete, animációi, létező működése kötelezően védendő. PyQt6→PySide6 átálláshoz explicit kompatibilitási térkép: Qt signals/slots, QThread, QWebEngine, Windows natív szint, audio, érintett importok. A teljes GUI munka csak P4 ACCEPT után; P0-ban izolált technikai próbát lehet készíteni.

## Szerződéselv

Közvetítő API-k nem írhatnak belső Qt-objektumokra a másik processzből. Minden parancshoz request_id, task_id, session_id, actor_id, capability, approval token, deadline, schema_version, trace_id, idempotency key; minden eredményhez pontos státusz és audit evidence. Lásd 08.
