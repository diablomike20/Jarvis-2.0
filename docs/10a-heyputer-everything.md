# R&D-017 — HeyPuter/everything: 51 forrásbeli alkalmazásmappa és JARVIS-integrációs lehetőségek

**Forrás:** https://github.com/HeyPuter/everything  
**Rögzített commit:** `06802a1e3749202e4db94d39c9ef5ab1a97d0ef1` (main; lekérdezés: 2026-10-16)  
**Státusz:** `HIGH_VALUE_CANDIDATE / PARKED / NOT_INSTALLED / NOT_RUNTIME_TESTED`  
**Kapcsolódó fázis:** P6 (JARVIS-specifikus kreatív / CAD extrák), opcionálisan P2–P4 során csak dokumentált összehasonlítás.  
**Döntési elv:** az eredeti Project Icarus sorrendjét NEM módosítja.

**Darabszám-pontosítás:** a projekt README-je korábban 60 alkalmazást említett, de a 2026-10-16-i pinelt Git-fában az `src/` alatt 51 közvetlen gyerekkönyvtár ellenőrizhető. Az adatokat nem szabad egymás szinonimájaként kezelni; részletes lista: [16c](16c-creative-rnd-heyputer-roadmap.md).

## 1. Bizonyított forrásadatok

A fő repository 2026-10-13-án jött létre; a vizsgált Git-fában 32 364 fájl és az `src/` alatt 51 közvetlen alkalmazáskönyvtár található. A GitHub API ~421 899 KB repository size adatot jelentett (nem egyenlő minden környezetben a checkout méretével). A főgyökér LICENSE **MIT**, de minden alprojekt transzitív dependency licencét és a bundled/remote modellek feltételeit külön kell ellenőrizni. A forrás túlnyomórészt JS/TypeScript + Vite/WebGL/WebAssembly, nem PyGPT-be illeszthető natív Python-plugincsomag.

A README csoportjai: Office, Collaboration, Creative Tools, Engineering, Productivity, Finance, Business, Developer Tools és Games. A teljességi lista a `src/` alatt található: 3d, accounting, api-client, assets, audio-studio, backgammon, building-design, cad, calendar, cap-table, checkers, chess, childcare, circuits, contacts, contracts, crm, documents, email, expense, field-service, fleet, help-desk, hiring, inventory, invoicing, legal, meetings, music-studio, notes, parametric, pdf, photo-studio, pos, presentation, projects, property-management, records, shifts, signatures, solitaire, spreadsheet, sudoku, survey, tasks, teamchat, time-tracking, vector-studio, video-studio, whiteboard, wiki.

A fő README Node >= 22.12-t ír, de a 3D app saját README-je **Node 24 LTS**-t kér. A kiválasztott subappok külön `npm install`, `npm run dev`, `npm test`, `npm run build` ciklussal rendelkeznek. Nem történt e műveletek futtatása, így a valódi build és kompatibilitás még ismeretlen.

## 2. Prioritásos komponensek és forrásbizonyíték

| App | Valódi forrásban dokumentált felület | JARVIS relevancia | Érettségi korlát |
|---|---|---|---|
| `src/parametric` | OpenCascade WASM + feature tree/sketch solver, STEP/STL, agent + tools + host, Puter AI Claude | AI-vezérelt, szerkeszthető parametrikus 3D; összehasonlítandó FreeCAD/Blender úttal | README: early alpha, nem production |
| `src/3d` | Three.js/WebGL2, WebAssembly, `bpy`-style JS/Pyodide API, agent/tools, GLB/FBX/OBJ/STL/USD | 3D kreatív modul és kontrollált scene-script adapter | Nem teljes Blender; .blend import korlátozott, export nincs |
| `src/cad` | 2D rajzoló motor, geometriavezérlés, DXF, PDF/SVG export | 2D műszaki rajz és precíz fájlinteroperabilitás | README: early alpha |
| `src/photo-studio` | PSD/PSB, rétegek, maszkok, lokális WASM image engine, AI edit panel | PhotoCraft alternatíva vagy specializált eszköz | 8192 px/oldal, 24 MP limit; AI Puter account |
| `src/video-studio` | Timeline, effektek, WebGL2/MediaPipe/WASM, AI edit | FilmCraft funkció-összehasonlítás és videóeszközök | Böngésző codec/encode függőség; AI Puter |
| `src/audio-studio` | Mintapontos waveform, multitrack, AudioWorklet + Rust WASM DSP | Hangminta-előkészítés a későbbi JARVIS beszédprojekthez | Beszédszintetizátort/voice clonert nem helyettesít |
| `src/api-client` | HTTP/WS kérések, collections, JS tesztek, OpenAPI és HAR, helyi/browser vagy Puter-relay | PyGPT↔FCC API szerződések kézi tesztelésének alapja | README: alpha; credential/proxy/security review |
| `src/documents`, `src/spreadsheet`, `src/pdf` | Webes DOCX/XLSX/PDF feladatok; spreadsheet AI-asszisztens | Opcionális interaktív munkafelület PyGPT dokumentum toolok mellé | Teljes Office paritás nem bizonyított |

Forráshelyek:
- `src/parametric/README.md`, `src/parametric/src/assistant/agent.ts`, `tools.ts`, `host.ts`, `src/kernel/`, `package.json`.
- `src/3d/README.md`, `src/3d/ARCHITECTURE.md`, `src/3d/src/assistant/agent.ts`, `puter.ts`, `tools.ts`, `THIRD_PARTY_NOTICES.md`.
- `src/cad/README.md`, `src/photo-studio/README.md`, `src/video-studio/README.md`, `src/audio-studio/README.md`, `src/api-client/README.md`.

## 3. A legérdekesebb technikai eredmény: belső AI-tool API

A parametrikus CAD és a 3D app `src/assistant/agent.ts` fájlja modell-válasz / tool call / tool result ciklust kezel. Az `agent.ts` úgy van megírva, hogy a chatfüggvény, eszközök és snapshot a hívótól jönnek; ezért scripted modellel is tesztelhető. A parametrikus `tools.ts` egy modellre alkalmazható műveletet újraépítés és hibás feature esetén visszavonás után jelent. A host interfész `host.ts` a geometria és a UI közötti határt absztrahálja; Node-kernel tesztimplementáció is szerepel a leírásban.

**Tervezési következtetés (PROPOSED, nincs implementálva):** a host/tool sémák köré készíthető lokális, sandboxolt adapter, amelyen át PyGPT agent/FCC coding agent hívhatja a webes CAD/3D műveleteket. Ehhez eredmény- és állapotszerializáció, undo/snapshot, sandbox, auth, session_id, license és UI embed (Qt WebEngine vagy saját böngésző) kell. A Puter alkalmazások belső tool rétege **nem** kész, nyilvános MCP-szerver vagy Python SDK a JARVIS számára.

## 4. Puter függőségek: nincs „korlátlan ingyen AI” bizonyíték

- A 3D `src/assistant/puter.ts` a `https://js.puter.com/v2/` kliens SDK-t tölti és Puter bejelentkezést kezel.
- A Parametric AI-eszközei Puter AI/Claude modelleket hívnak. A Photo Studio README kimondja, hogy az AI szerkesztéshez Puter fiók kell, és a képgenerálási/editing outputnak külön korlátai vannak.
- A CAD normál rajzolási funkciói account nélkül is működhetnek, Puter cloudhoz fiók kell.
- A dokumentált helyi böngészős mód **nem azonos** minden AI-művelet ingyenes, offline működésével.
- A Puter szolgáltatói hitelesítés, fogyasztási korlát, költség és adatátadás feltételei külön teszt/ellenőrzés tárgyai; nem irányítunk át a Puter felé felhasználói projektadatot automatikusan.
- A 3D bizonyos funkcióinál runtime Pyodide külső CDN, a CAD/parametric pedig külső WASM/dependency licencekre épül.

## 5. Kockázatok / jogi és biztonsági ellenőrzés

- **Érettség:** repository néhány napos a vizsgálat napján; egyes appok explicit early alpha/alpha. Tömeges feature-lista nem egyenlő tesztelt professzionális minőséggel.
- **Függőségek:** Node 22.12+, 3D Node 24, TypeScript/Vite, browser WebGL2/WASM; a PyGPT Python/Qt függőségei külön folyamatot/iframe-integrációt kívánnak.
- **Licencek:** MIT a gyökérben; OpenCascade kernel LGPL-2.1 a Parametric modulban, Pyodide MPL-2.0 és más harmadik fél licencek a 3D-ben; az NOTICE és build-license audit kötelező.
- **Fájlbiztonság:** a browser IndexedDB és Puter cloud közti adatmenetek és OAuth/auth ellenőrzendők; különösen CAD-projekt, hangminta, privát JARVIS dokumentum.
- **AI-kódfuttatás:** 3D scripts és tool-driven CAD műveletek csak projekt-copy/undo/approval/permission kontroll mellett.
- **Dev endpoint:** több subapp Vite `--host 0.0.0.0` fejlesztői bindot használ; ha helyben futtatjuk, explicit loopback/host firewall szükséges.
- **Adatvesztés:** korai alfa projektnél ne küldjünk kizárólagos eredeti tervdokumentumot; biztonsági másolat szükséges.

## 6. JARVIS beillesztési terv (nem aktivált)

1. `R&D/PARKED`: a repository pinelt SHA-val katalogizálva; nem teljes 32k fájlos submodule az első CORE-ba.
2. P6-ban prioritási shortlist: Parametric + 3D, majd CAD + Photo/Video Studio, API Client külön fejlesztői tesztsegédként.
3. Per-app sandbox izolált forrás checkout, Node-pinek, tests + build, no live customer data.
4. Minimal adapter PoC: egy read-only geometria/scene state query, majd egy explicit jóváhagyott módosítás snapshot-visszaállítással.
5. Compare existing PhotoCraft, LightCraft, FilmCraft, FreeCAD and PyGPT native tools; nincs felesleges párhuzamos modul.
6. Integrálás csak bizonyított P6 előny és licenc/security/Windows teszt után, explicit projektgazdai döntéssel.

## 7. Előre definiált vizsgálati tesztek (mind NOT_RUN)

| ID | Próba | Elfogadás |
|---|---|---|
| PUTER-001 | Pinelt source checkout + per-app npm ci | Exact lockfile és változatok |
| PUTER-002 | Parametric Vitest + build + e2e | Reproducible, exit=0 |
| PUTER-003 | 3D Vitest + build + Playwright | Reproducible, exit=0 |
| PUTER-004 | CAD DXF import/export roundtrip | Szerkeszthető geometria, tűrés |
| PUTER-005 | Parametric STEP/STL roundtrip | Geometria és egységek |
| PUTER-006 | Parametric assistant tool calls | read, mutation, rollback, tool schema |
| PUTER-007 | Browser/API integration Qt WebEngine | Session, origin, auth, no leaked credentials |
| PUTER-008 | Puter account / AI dependency isolation | Offline-only és sign-in útvonal feltérképezve |
| PUTER-009 | Security/third party licences | Root MIT + per-app notices, SBOM |
| PUTER-010 | Existing Jarvis creative stack comparison | Nincs igazolatlan feature-duplicáció |

## Záró döntés

**Nagy potenciál a jövőbeli kreatív/CAD „toolbox” számára; NEM a PyGPT és FCC helyettesítője.** Ezt a repót a teljes forráskód megvizsgálása és elfogadása előtt nem adjuk a P1/P2/P3 telepítendő komponenseihez, és nem változtatjuk meg a JARVIS original HUD tervét.

_Evidence: GitHub README + forrásfájlok és manifestek a fent pinelt commiton; a tényleges runtime nem lett elindítva._
