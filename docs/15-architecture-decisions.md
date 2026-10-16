# 15 — Architecture Decision Records / projektirányok

Ezek a rekordok elválasztják a **felhasználó által kért stratégiai döntést** a még kipróbálatlan technikai javaslattól.

## ADR-001 — JARVIS UNIFIED központi GitHub projekt

- Állapot: ACCEPTED.
- Döntés: diablomike20/Jarvis-2.0, Project Icarus.
- Következmény: a korábbi repo forrás-kópia, nem automatikusan átírandó.
- Kontroll: main változatlan, egyedi feature branch.

## ADR-002 — PyGPT legyen a projekt alapmotorja

- Állapot: ACCEPTED DIRECTION, IMPLEMENTATION PENDING.
- Indok: PyGPT széles asszisztens-képességei és Add-ons mechanizmusa.
- Megvalósítás: pinned Git submodule a P2 ágon, tényleges processz/test hátra van.

## ADR-003 — PyGPT_Addons előbb, mint FCC

- Állapot: ACCEPTED ORDER, SELECTION PENDING.
- 2 Add-on + 30 MCP + 37 Skill = katalóguslehetőség, nem automatikus aktiválás.
- Kontroll: dedup, pin, trust audit, valódi smoke.

## ADR-004 — FCC mint szeparált modell/coding gateway

- Állapot: ACCEPTED DIRECTION / PROPOSED IMPLEMENTATION.
- Külön Python processz, auth, natív PyGPT provider bypass/fallback multimodal.
- A privát code/AGPL forrás kiválasztása még blokkoló.

## ADR-005 — Az eredeti JARVIS HUD és működés megőrzése

- Állapot: ACCEPTED.
- Az eredeti animáció marad; nincs automatikus 3D Orb redraw.
- GUI PyQt6→PySide6 port csak P4 után, P0 izolált feasibility spike megengedett.

## ADR-006 — Extrák később

- Állapot: ACCEPTED.
- JARVIS hungarian voice; PhotoCraft/LightCraft/FilmCraft/FreeCAD; REA/IronRAG/VoiceStudio/Barehands csak megfelelő időben.
- Security/logging/approval/rollback nem „extra”, a kezdetektől alapkövetelmény.

## ADR-007 — Multi-agent munkahatárok

- Állapot: ACCEPTED SAFETY PRINCIPLE, TOOLING PROPOSED.
- Egy feladatgazda; diszjunkt branch és worktree; megőrzött eredeti forrás.
- Ne módosítsd a párhuzamos Claude fejlesztő munkáját.

## ADR-008 — Dokumentáció legyen külön branch

- Állapot: ACCEPTED és IMPLEMENTED.
- Branch: docs/master-spec-20261016.
- Kötelező: verziózott, beolvasandó onboarding és bizonyítékregiszter.

## ADR-009 — Submodule alapú kezdeti forrásbeemelés

- Állapot: IMPLEMENTED FOR PYGPT + ADDONS.
- Előny: eredeti git-história és pinelt SHA; verzióváltás diffelhető.
- Hátrány: klónozáshoz hálózati elérés; ez nem offline forrásarchívum.
- Későbbi vendoring/összevonás döntésre vár.

## ADR-010 — IronRAG, VoiceStudio és Memory Vault

- Állapot: PARKED, NONE INSTALLED.
- IronRAG műszaki dokumentum RAG, Memory Vault Markdown/Obsidian; nem egymás kizárólagos helyettesítői.
- VoiceStudio lehetséges helyi magyar TTS/voice clone.
- Későbbi implementáció előtt funkcionális benchmark/licenc/hardver teszt.

## ADR-011 — Feladatszintű API/IPC envelope

- Állapot: PROPOSED (08 részletezi).
- Szigorú task_id, session_id, causation, approval, retry és cancel.
- A wire format a P3 előtti contract teszt során véglegesítendő.

## ADR-012 — A nagy kutatási backlog ne bontsa meg az első fázisokat

- Állapot: ACCEPTED PRINCIPLE.
- Új GitHub-felfedezések R&D-be kerülnek, nincs automatikus telepítés.
- Az új eszköz csak külön benchmark/előfeltétel után válik kötelező fázisrésztvevővé.

## ADR dokumentálásának szabálya

Státuszváltás csak dátummal, indoklással, érintett fájl/commit/teszt hivatkozással; a USER döntést külön jelölni kell a mérnöki feltételezéstől. Dokumentáció frissítése nem helyettesíti a kódváltoztatást.

## ADR-013 — Publikus források külön gyűjteményága

- Állapot: IMPLEMENTED.
- Branch: sources/pinned-project-baseline, commit 1da31bdd7850665d963906dfc8a4d97b2788e94d.
- 7 eredeti publikus forrás külön Git submodule-ban, nincs modul/runtime összemosás.
- A privát/érzékeny fájlok nem kerülnek automatikusan publikálásra.
