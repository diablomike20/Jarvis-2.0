# 14 — Ténylegesen végrehajtott GitHub-migrációk naplója

**Dátum:** 2026-10-16. **Cél:** https://github.com/diablomike20/Jarvis-2.0. Nyilvános.

## Kezdeti referencia

- Target main: 38d6991faf52eb1c2348773b702a9fb44db6f470
- Kezdő fájl: README.md ("# Jarvis-2.0 / Project Icarus")
- Könyvtárszintű API ellenőrzés: hozzáférés admin:true / push:true.
- A main branch érintetlen maradt.

## Létrehozott ágak

1. docs/master-spec-20261016 a kezdő main SHA-ból.
2. integration/pygpt-addons-baseline a kezdő main SHA-ból.

## Integrációs ág konkrét commit

074b2efb8c4a73aee8d55d8b6bc56a2e69df211c

A branch tartalma: .gitmodules; INTEGRATION.md; README.md; upstream/pygpt submodule pin 2d8779a983edc73846a640bbbda1dcc7d513d924; upstream/pygpt-addons pin 15759ba00cab37622e0b9f5b302c73fc7aa56a50.

Git Gitlink-objektumokat hoztunk létre; a submodule külső forrás pontos HEAD-jét a rekurzív klón letölti. A checkout valódi Windows/Python működése NOT_RUN, ezért az első P2 elfogadási teszt még NEM teljesült.

## Dokumentációs ág commitok

- 56937ac6d114c0207ccc9cb1280c3789fa07e5cf — README, charter, forrás-pin, architektúra, fázisok.
- 85d6a1796299244095d6be45a22391108361e8a6 — PyGPT, Add-ons, FCC, GUI leltár.
- 6b468a53a26717aea47787f7d3ff4e93b455d59e — IPC, security, kutatási backlog, handoff.
- 4df078ed320351beb18d0b98dcbab4c602723f4f — 74 tervezett acceptance teszt, 22 kockázati tétel, ADR, napló, gépi JSON nyilvántartások.

## Ami NEM történt meg

- Nem változott Jarvis-2.0 main és a korábbi JARVIS/PyGPT/Add-ons/FCC upstream.
- Nem történt PyGPT Windows indulás vagy telepítési próba.
- Nem állítottunk be GitHub branch protection ruleset-et.
- Nem került át a privát AI-Proxy forrás; nincs FCC P3 service a célrepóban.
- Nem került át nyers beszélgetés-export, hanganyag, teljesfilm- vagy modellbináris.
- Nem épült meg JARVIS GUI-port, végleges magyar hang, PhotoCraft/LightCraft/FilmCraft/FreeCAD adapter.
- Nem történt automatikus PR merge / push default main ágra.

## Jelentési elv

Forrásbeemelés ≠ működő integráció. Dokumentációs commit ≠ végrehajtott teszt. User által jóváhagyandó nyitott feladatok külön backlog és fáziskapu szerint.

## Forrásgyűjtemény ág

- sources/pinned-project-baseline ágat a változatlan main bázisból hoztuk létre.
- Commit 1da31bdd7850665d963906dfc8a4d97b2788e94d: .gitmodules, README.md, sources-manifest.json és 7 public Git submodule.
- Minden submodule pontosan a 01-source-register.md táblázat commitjára mutat; az eltérő jogi/telepítési feltételek miatt nem történt automatikus build.
- A GitHub faobjektumok sikeresen létrejöttek. Rekurzív klónozás tesztje továbbra is NOT_RUN.

## 2026-10-16 — HeyPuter/everything forrásaudit

- Változtatás kizárólag a dokumentációs ágon, a main változatlan.
- Rögzített upstream SHA: `06802a1e3749202e4db94d39c9ef5ab1a97d0ef1`; a 60 app és a 32 364 Git-fájl forrásfában megfigyelt.
- `docs/10a-heyputer-everything.md` részletes vizsgálat; kutatási backlog és referencia-lock frissítve.
- Nincs submodule/beépítés a CORE-ba, nincs npm install/build, nincs Puter-login, nincs külső adatküldés.

## 2026-10-16 — Teljes JARVIS 2.0 funkcióspecifikáció

A felhasználó kérésére új, részletes, magyar nyelvű funkcionális célleltár került a külön dokumentációs ágra:

- `docs/16-jarvis20-complete-feature-specification.md` — 16 fejezet és 65 kóddal azonosított célfunkció; a HeyPuter/Everything anyaga elkülönítve.
- `docs/16a-jarvis-original-preservation.md` — 50 ellenőrzött JARVIS actions/ fájl, funkciómegőrzési követelmények.
- `docs/16b-core-ai-addons-capability-matrix.md` — 40 PyGPT plugin könyvtár, 16 tool, PyGPT/FCC/Addons tulajdonosi mátrix.
- `docs/16c-creative-rnd-heyputer-roadmap.md` — 51 tényleges HeyPuter src app, opcionális P6 CAD/creative integráció.
- `catalog/feature-registry.v1.json` — géppel olvasható 65 feature + 157 forrás-katalógusrekord; minden runtime teszt NOT_RUN.
- `README.md` és `docs/11-agent-handoff.md` frissítve az új chat/fejlesztői handoffhoz.

A HeyPuter régebbi 60-app állítását külön jelöltük a ténylegesen számolt 51 forráskönyvtártól. Nem történt Windows build, futásidejű integráció, a main ág és az eredeti forrásrepo nem módosult. A privát AI-Proxy, filmes referenciahangok és nyers korábbi beszélgetés-exportok továbbra sincsenek nyilvános GitHubba feltöltve.

## 2026-10-16 — v1.1 scope-korrekció

A teljes funkcióspecifikáció és a gépi célfunkció-regiszter egy, a Project Icarushoz nem tartozó személyes témára felvett kutatási tétellel rövidebb lett. Az aktuális célfunkciók száma: **64** (a korábbi v1.0-ban 65 volt). A 157 forrásleltár-rekord és az eredeti PyGPT/FCC/P6 célok változatlanok. Az archivált átadási szöveg is kizárólag projekt-releváns tartalmat őriz. A teljes integrált JARVIS runtime továbbra sem készült el.
