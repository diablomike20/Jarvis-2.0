# 13 — Kockázat- és nyitott döntésnapló

## Kockázati mátrix

| ID | Súly | Fenyegetés / hibakép | Enyhítés | Kritikus fázis |
|---|---|---|---|---|
| R-001 | CRITICAL | Privát repo tartalom nyilvános targetben | repo public/private előszűrés; publikációs review | P1/P3 |
| R-002 | CRITICAL | FCC unauthenticated bind/admin | 127.0.0.1+random credential+audit | P3 |
| R-003 | CRITICAL | Agent shell bypass approval | permission service, OS sandbox, fail-closed | P3/P4 |
| R-004 | HIGH | PyGPT MainWindow-höz kötött core | külön processz, headless adapter feasibility | P0/P4 |
| R-005 | HIGH | PyQt6→PySide6 inkompatibilitás | korai proof; későbbi screenshot/regression | P0/P5 |
| R-006 | HIGH | Python 3.14 vs <=3.13 ütközés | külön venv/processz, pinelt interpreter | P1/P3 |
| R-007 | HIGH | AGPL/MIT licencek összekeverése | tényleges LICENSE/NOTICE/SBOM audit | P0/P3/P6 |
| R-008 | HIGH | Ellenőrizetlen MCP postinstall kód | immutable source+dependency audit+sandbox | P2 |
| R-009 | HIGH | Dupla memóriarendszer adateltérés | egy memória owner; másolat forrás-id szerint | P4/P6 |
| R-010 | HIGH | Körbe delegáló agent | globális task_id/ownership graph | P4 |
| R-011 | HIGH | SSE retry dupla git/file write | idempotency és side effect ledger | P3/P4 |
| R-012 | HIGH | Git main vagy párhuzamos fejlesztő ág sérül | isolated branch/worktree, no auto merge | ALL |
| R-013 | HIGH | Funkcióvesztés UI csere közben | PARITY GAP ledger, screenshot+feature tests | P5 |
| R-014 | HIGH | Hangmodellhez kevés/hibás jogosultság | rights/voice-data review, no public sample | P6 |
| R-015 | MEDIUM | Nagy IronRAG RAM/CPU erőforrás | külön profiling, capacity gate | P6 |
| R-016 | MEDIUM | Provider nem támogat multimodal toolt | capability matrix, natív fallback | P3 |
| R-017 | MEDIUM | Nem teljes offline source archive | submodule pin + vendored signed backup terv | P1 |
| R-018 | MEDIUM | Hallucinált teszt-eredmények | NOT_RUN alapérték, evidence link kötelező | ALL |
| R-019 | MEDIUM | Windows mikrofoneszköz/Qt driver | Windows integration harness | P5/P6 |
| R-020 | MEDIUM | Model/API díjlimit | cost cap, opt-in, budget telemetry | P3/P4 |
| R-021 | MEDIUM | Túl sok Skill konfliktus | dedup, resolver, célhoz kötött lazy load | P2 |
| R-022 | MEDIUM | Főág védelem valójában nincs beállítva | GitHub admin protected branch review | P1 |

## Még hiányzó tények / döntések

- A PyGPT aktuális master branch valódi Windows-indítása, programverzió/fájl-függőségek és futásidejű health.
- A PyGPT extension katalógus P2 telepítési UI, külső MCP szerver dependency lock és read-only/sandbox állapot.
- FCC: melyik publikálható upstream választott a private source helyett; MIT-AGPL licenc migráció.
- A GUI portnál mi az 1:1 paritás tényleges kép- és állapot-alapú bizonyítéka; nem elég hasonló UI.
- FreeCAD konkrét verzió és API adapter; PhotoCraft/LightCraft/FilmCraft teljes CLI/API contract.
- Beszéd TTS engine, magyar minőségi mérés, hangminták jogosultsági megőrzési mód.
- Publikált célrepo GitHub Settings branch-protection / rulesets tényleges admin beállítása nincs lefuttatva.
- Machine-spec RAM, VRAM, Windows version: a következő end-to-end tesztekhez pontosan szükséges.
- Eredeti Jarvis-Ai bármely fejlesztő ágának befagyasztása és a párhuzamos Claude agent munkájának újraegyeztetése.
- Privát és nagyméretű korábbi projekt TXT / videó / audio biztonságos archívumának helye.

## Elfogadott irány vs mérnöki hipotézis

Elfogadott: PyGPT alapra építkezés; add-onok utána FCC; teljes GUI csak stabil backend után; későbbi extrák; eredeti animáció és funkciómegőrzés; külön docs branch; központi új repo.

Javasolt, nem elfogadott részlet: IPC HTTP/SSE vagy gRPC; supervisor process framework; IronRAG/VoiceStudio/REA/Barehands tényleges telepítése; valós P2 Skill-válogatás; FCC provider routing kötelező mennyisége.

## Figyelési szabály

Minden kockázati státuszhoz konkrét megfigyelés vagy negatív teszt, owner és célfázis rendelhető. Ismeretlen paramétert ne töltsünk ki feltételezéssel.
