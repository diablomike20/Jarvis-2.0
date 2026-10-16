# Jarvis-2.0 — Project Icarus / JARVIS UNIFIED

> **Dokumentációs ág, 2026-10-16.** Ez az ág a részletes műszaki dokumentáció forrása. Nem futtatható JARVIS-kiadás. A valóságot és a célállapotot tudatosan külön kezeljük.

## Tartalomjegyzék

| Dokumentum | Téma |
|---|---|
| [00 — Projektalapok](docs/00-project-charter.md) | Cél, szabályok, nem célok, elfogadás |
| [01 — Forrás- és licencnyilvántartás](docs/01-source-register.md) | Publikus projektek, pinelt SHA-k, eredet |
| [02 — Célarchitektúra](docs/02-architecture.md) | Komponensek, processzek, API-k, tulajdonosi határok |
| [03 — Megvalósítás és mérföldkövek](docs/03-phases-and-gates.md) | P0–P6, fáziskapuk és bizonyítási követelmények |
| [04 — PyGPT leltár](docs/04-pygpt-inventory.md) | Pluginok, toolok, provider-adapterek, hang/RAG |
| [05 — Add-ons katalógus](docs/05-addons-inventory.md) | 2 Add-on, 30 MCP, 37 Skill, 11 minta |
| [06 — Free Claude Code](docs/06-fcc-inventory.md) | 61 provider, 11 kliens, gateway, routing, kockázatok |
| [07 — JARVIS GUI](docs/07-gui-compatibility.md) | Eredeti HUD, PyQt6 → PySide6, mérhető paritás |
| [08 — IPC/API szerződés](docs/08-api-event-contracts.md) | Javasolt wire format, események, idempotencia |
| [09 — Biztonság / licencek](docs/09-security-licensing.md) | Fenyegetési modell, privát adatok, ágankénti műveletek |
| [10 — Kutatási backlog](docs/10-research-backlog.md) | REA, DeerFlow, VoiceStudio, IronRAG és új találatok |
| [11 — Agent handoff](docs/11-agent-handoff.md) | Több chat/ügynök együttműködés és DeepLearn-protokoll |
| [12 — Tesztmátrix](docs/12-test-matrix.md) | Regreszszió, integráció, kompatibilitás, evidencia |
| [13 — Nyitott döntések](docs/13-risks-and-open-questions.md) | Bizonytalanságok, blokkolók, döntésnapló |
| [14 — Napló és bizonyítékok](docs/14-migration-log.md) | Tényleges GitHub-műveletek, kész/nem kész |
| [15 — ADR](docs/15-architecture-decisions.md) | Elfogadott irányok vs. javaslatok |

## Forráskód beköltözése

- [integration/pygpt-addons-baseline](https://github.com/diablomike20/Jarvis-2.0/tree/integration/pygpt-addons-baseline): PyGPT és PyGPT_Addons Git submodule-ok, konkrét SHA-kra pinelve.
- A Free Claude Code integrációja későbbi külön P3 munkacsomag; a meglévő privát kódot nem publikáljuk engedély és tartalmi ellenőrzés nélkül.
- A JARVIS eredeti HUD-ja egyelőre változatlanul a forrásrepojában található.

## Bizonyítottsági jelölések

- **VERIFIED_SOURCE:** GitHub-fájlban vagy repo metaadatban konkrétan ellenőrzött tény.
- **REPORTED_PREVIOUSLY:** korábbi projektanyagban szereplő állítás; az aktuális környezetben nincs újrafuttatva.
- **PROPOSED:** mérnöki javaslat, még nem jóváhagyott/implementált.
- **UNVERIFIED_RUNTIME:** létező kód vagy dokumentáció, de futásidejű teszt nincs.
- **BLOCKED:** feltétel hiányzik (hozzáférés, adatvédelmi döntés, hardver, kompatibilitás).
- **PASS / FAIL / NOT_RUN:** tényleges teszt eredménye; csak megismételhető evidenciával adható PASS.

## Szigorú védelmi korlátok

Egyetlen másik forrás-repository main/master ágát sem változtatjuk. A Project Icarus főága sem változott. Minden fejlesztés szigorúan külön ágon, lehetőség szerint külön worktree-ben. A nyilvános repo nem tárolhat API-kulcsot, privát forráskódot, személyes beszélgetésarchívumot vagy kontrollálatlan hangmintát.

**Ez a dokumentáció munkapéldány, nem az elkészült rendszer bizonyítéka.**
