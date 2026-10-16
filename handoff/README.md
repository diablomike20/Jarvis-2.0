# JARVIS 2.0 / PROJECT ICARUS — teljes projektátadási csomag

**Kiadás:** HANDOFF-20261016-A; 2026-10-16; HU.
**Integrált alkalmazás készsége:** NINCS igazolt JARVIS 2.0 end-to-end build.
**GitHub source-of-truth:** `docs/master-spec-20261016` kiinduló commit `935016895c814131e42022e021a034638d3fd603`; ezen az ágon külön handoff kiegészítésként szerepel.
**Public/private határ:** minden fájl tisztított műszaki adatokat tartalmaz; nem tartalmaz tokeneket, hangfelvételeket és teljes nyers privát chat-exportokat.

## Olvasási sorrend — kötelező új fejlesztőchatnek

1. Ez a `handoff/README.md`.
2. A `PROMPT_UJ_CHAT_KOLLEGANAK.txt` — teljes bootprompt, ne kapkodj, DeepLearn tanulmányozás.
3. `handoff/01-PROJEKT_ALLAPOT_ES_DONTESNAPLO.md` — rögzített és még tervezett.
4. `docs/16-jarvis20-complete-feature-specification.md` és a `docs/16a, 16b, 16c` teljes tervezett képességprofil; `catalog/feature-registry.v1.json`.
5. `docs/00–15` külön: charter, licenc, architektúra, fázisok, PyGPT, Add-ons, FCC, GUI, IPC, security, backlog, agent handoff, teszt, kockázat, ADR.
6. `handoff/02-...06` új, bővített részletek és kutatási jelöltek.
7. `handoff/07-BIZONYITEK_ESETEK_ES_CI.md` — régi build, branches és ismert hibák.
8. `handoff/08-CHAT_KONTINUITAS.md` + `JAVASLAT_A_CHATEK_KOZOTTI_FOLYTONOSSAGRA.txt`.
9. `handoff/09-GITHUB_FORRASKATASZTER.md` — pontos források, verziók.
10. `UTOLSO_VALASZ_ES_FREE_CLAUDE_AUDIT.txt` — előző válasz dokumentált, befejezett vizsgálata.

## Fogalmak

- **CÉL / COMMITTED_TARGET:** a felhasználó által kívánt végső vagy fázisfüggő funkció, még nem biztos hogy implementált.
- **SOURCE_PRESENT:** ismert Git-fájlban létező kód / konfiguráció.
- **RUNTIME_PASS:** megismételhető telepítési/funkcionális teszt, pontos commit és log mellett.
- **NOT_RUN:** végrehajtás nincs igazolva, nem jelent PASS-t.
- **PARKED_RND:** tartalék, nem kötelező integráció; nem automatikus architekturális változás.
- **PRIVATE_EXCLUDED:** publikus feltöltésből szándékosan kizárt személyes, titkos, licencileg kérdéses anyag.

## Nem veszhet el

Az eredeti Brahma/JARVIS GUI; semmilyen automatikus 3D Orb újraértelmezés; eredeti action/tool képességek, PyGPT pluginok, app eszközök és natív provider funkciók; integrációs állapot és projekt-történet; forrás- és licencattribúció. A hang és Craft modulok majd P6.

## Nyitott első feladat

P0/P1/P2 tényleges Windows rekurzív checkout és PyGPT indítás, Add-ons rendszer ellenőrzése; P3 FCC csak utána. A dokumentáció nem bizonyít futó rendszert.

**Ez a csomag nem helyettesíti a forráskódot: forráshely és pin szerepel, és a tényleges implementációnak a submodule-okból kell dolgoznia.**

## Új kiegészítés: God's Eye View bekerült a forrásgyűjteménybe

2026-10-16: a `sources/pinned-project-baseline` ágon már **8** Git-submodule található, köztük `sources/gods-eye-view` a `e2274bbf0ceaeb2e14f8a59d63e77000553c6816` SHA-n. Teljes technikai megjegyzés: [handoff/03](03-GODS_EYE_VIEW_TECHNIKAI_AUDIT.md). P6/R&D, nem aktív core.
