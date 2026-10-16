# 16c — Kreatív műhely, fejlesztői labor és HeyPuter Everything (részletes P6/R&D terv)

**Ez a kiegészítő dokumentum kiemelt prioritással integrálja a felhasználó által átadott HeyPuter/Everything elemzést.** A pontos korábbi audit: [10a](10a-heyputer-everything.md). A teljes JARVIS célspecifikáció: [16](16-jarvis20-complete-feature-specification.md).

**Változatok:** HeyPuter/everything @ `06802a1e3749202e4db94d39c9ef5ab1a97d0ef1`, 2026-10-16; PhotoCraft @ `b71991e15a3fc01d3c5848464c14c19b6dc8f2b5`, LightCraft @ `7b47ba7894a2563be32ab75176866b6d743df7a4`, FilmCraft @ `5231852443363f001c3f6b396dd9b1e6461ae2be`. **Nincs e komponensekből kész P6 JARVIS build.**

## 1. Közös kreatív felhasználói élmény — mit kérhet majd JARVIS-tól?

**CR-UX-001:** „Nyisd meg a képet, javítsd az árnyékokat, kezeld rétegekkel, készíts webes exportot.” → PhotoCraft/LightCraft/HeyPuter közül választás képesség, input és telepített állapot alapján; ne egyesítsünk két eltérő szerkesztő motort bizonyítatlanul.

**CR-UX-002:** „Készíts hatásos videóelőzetest felirattal, hangkeveréssel.” → FilmCraft NLE projekt, timeline állapot, klip sorrend, keyframe/titles/sound, export, visszavonás. JARVIS a parancsot közvetíti és eredményt ellenőrzi, nem állítja, hogy egy külső video AI modell automatikusan elérhető.

**CR-UX-003:** „Rajzold meg ezt a műszaki alkatrészt milliméterre, készíts STEP és STL változatot.” → FreeCAD/HeyPuter Parametric (csak bizonyított verzió), sketch és constraints, méretegységek, geometriai ellenőrzés, snapshot, export és roundtrip. Valódi gyártási megfelelés külön mérnöki ellenőrzés.

**CR-UX-004:** „Állíts be három fényt, anyagokat és kamerát a 3D-jeleneten.” → Blender MCP vagy bizonyított 3D scene adapter, csak authorized file paths. Lehet preview/render/export és szükség esetén részletes error report.

**CR-UX-005:** „Rajzolj kapcsolási rajzot a szenzorokkal.” → eredeti JARVIS Circuit HUD + későbbi 2D/Circuits tool; elektromos biztonság és tűrések nem becslések.

## 2. A kreatív alkotórendszerek összehasonlítása

| Engine | Kód és vezérlési felület | Forrásban ismert képességek | Integrációs állapot | Megjegyzés |
|---|---|---|---|---|
| **PhotoCraft** | Rust natív, MCP/CLI/JSON | PSD/PSB, layer/tree, mask, 16 adjustment layers, text, vector, brush, shader/GPU compositor, import/export | P6 OPTIONAL; early alpha | A felhasználó külön kerüljön a full app vagy adaper mellett, dual MIT/Apache-2.0 licence ellenőrizve |
| **LightCraft** | Rust natív, MCP | RAW/photo library, exposure, contrast, tone curves, white balance, color grading, masking, presets, non-destructive exports | P6 OPTIONAL; young | Nem a PhotoCraft duplikációja: előhívás/album vs kompoziting |
| **FilmCraft** | Rust natív agent command bridge | NLE timeline, clips/tracks, cut/insert/overwrite, effects, keyframes, titles, captions, color, audio, export | P6 OPTIONAL; young | Nem generatív filmmodell önmagában; tesztelendő codeckészlet |
| **FreeCAD** | Desktop Python/CAD | Parametrikus műszaki alkatrész, model tree, constraints, STEP/STL, explicit tool operations | P6 OPTIONAL / connector plan | Konkrét verzió és CLI/Python bridge még nincs pinelve |
| **Blender MCP** | MCP+Blender adapter | Scene, mesh, material, lighting, render, inspect, import/export | P6 OPTIONAL | MCP szerver és Blender verzió, jogosultság |
| **HeyPuter Parametric** | TypeScript OpenCascade WASM | sketch/constraint/feature tree, AI agent/host tools, STEP/STL | P6 R&D HIGH_VALUE / EARLY ALPHA | Puter cloud dependencies; no production CAD promise |
| **HeyPuter 3D Studio** | Three.js/WebGL/WASM | 3D jelenet, model/camera/light, asset export GLB/OBJ/STL, AI scripted tool functions | P6 R&D HIGH_VALUE | Nem Blender .blend teljes paritás |
| **HeyPuter 2D CAD** | Browser 2D vector geometry | DXF, PDF/SVG és rajzeszközök | P6 R&D HIGH_VALUE / EARLY ALPHA | Tűrés és roundtrip teszt |
| **HeyPuter Photo Studio** | Browser editor | PSD/PSB, layers/masks, AI edit panel | P6 R&D | Kép limit, Puter account AI módhoz |
| **HeyPuter Video Studio** | Browser editor | Timeline, efektek, WebGL2/MediaPipe/WASM és AI edit | P6 R&D | Codec/browser/cloud teszt |
| **HeyPuter Audio Studio** | Browser multitrack audio | Waveform, DAW-jelleg, WASM DSP | P6 R&D | Nem TTS/voice clone motor |
| **HeyPuter API Client** | Web dev tool | REST/WS, OpenAPI/HAR import, collections/tests | P0-P4 TOOL CANDIDATE | Szenzitív fejléc/token kezelés és origin |

**Fontos:** PhotoCraft/LightCraft/FilmCraft natív Rust alkalmazásai külön folyamatot vagy szolgáltatást kérnek; a HeyPuter/Everything főként JS/TS/Vite/WebAssembly és webes UI. A PyGPT Python/PySide6 környezetébe ezeket szó szerinti package importként nem lehet egységesen beolvasztani.

## 3. HeyPuter/Everything — forráskódon ellenőrzött tények

- Nyilvános repo: https://github.com/HeyPuter/everything.
- A pinelt main Git-fában **32 364 blob (fájl)** és **51 közvetlen `src/` alatti top-level alkalmazásmappa** szerepel. A README és a korábbi audit „60 alkalmazás” marketing-/README-adatát elkülönítjük, mivel a közvetlenül megszámolt fa 51 könyvtárat mutat; lehetnek további más helyeken található vagy logikai appok, de ez nincs jelenleg bizonyítva.
- A gyökérrepo MIT-licencű, az alprojekt és transzitív dependencies licence külön feladat.
- Sok külön frontend-app Vite/JS/TS/WebGL/WASM-függőségű. A README Node >=22.12-t, a 3D alprojekt Node 24-et dokumentál. Nem egyetlen kész Windowsos executable.
- A `src/parametric` és `src/cad` README-ben early alpha státusz látható. Nem vállalható ipari CAD megbízhatóság teszt nélkül.
- A `src/3d/src/assistant/agent.ts` és `src/parametric/src/assistant/agent.ts` modell/tool-response ciklusai értékesek egy későbbi Python/MCP adapter alapjául, **de nem kész MCP endpointok**.
- Puter.js fiók/SDK és cloud AI kapcsolatok, valamint költség/adatáramlás lehetséges; ezek nem „ingyen, offline, korlátlan AI” bizonyítékok.

## 4. A pinelt HeyPuter source `src/` alatti mind a 51 közvetlen appkönyvtár

| # | App könyvtár | Feladat / potenciál | JARVIS R&D-prioritás |
|---:|---|---|---|
| 1 | `src/3d` | Three.js scene/model / AI tool host | HIGH_VALUE |
| 2 | `src/accounting` | Könyvelési munkafolyamat | PARKED |
| 3 | `src/api-client` | HTTP/WebSocket/OpenAPI/HAR szerződésteszt | MEDIUM |
| 4 | `src/assets` | Eszköz/asset menedzsment | PARKED |
| 5 | `src/audio-studio` | Többsávos hullámforma, AudioWorklet/WASM | HIGH_VALUE |
| 6 | `src/backgammon` | Játék | PARKED |
| 7 | `src/building-design` | Épület/építészeti szerkesztő | PARKED |
| 8 | `src/cad` | 2D rajz, DXF/PDF/SVG, early alpha | HIGH_VALUE |
| 9 | `src/calendar` | Naptári UI | PARKED |
| 10 | `src/cap-table` | Tőkestruktúra | PARKED |
| 11 | `src/checkers` | Játék | PARKED |
| 12 | `src/chess` | Játék | PARKED |
| 13 | `src/childcare` | Gyermekellátási üzleti app | PARKED |
| 14 | `src/circuits` | Áramkörök szerkesztése | MEDIUM |
| 15 | `src/contacts` | Kontaktkezelés | PARKED |
| 16 | `src/contracts` | Szerződéskezelés | PARKED |
| 17 | `src/crm` | Ügyfélkezelés | PARKED |
| 18 | `src/documents` | Word-jellegű dokumentumszerkesztő | MEDIUM |
| 19 | `src/email` | Levelezési UI | PARKED |
| 20 | `src/expense` | Kiadásnyilvántartás | PARKED |
| 21 | `src/field-service` | Helyszíni munkák | PARKED |
| 22 | `src/fleet` | Flottakezelés | PARKED |
| 23 | `src/help-desk` | Ügyfélszolgálat | PARKED |
| 24 | `src/hiring` | Toborzás | PARKED |
| 25 | `src/inventory` | Készletkezelés | PARKED |
| 26 | `src/invoicing` | Számlázás | PARKED |
| 27 | `src/legal` | Jogi dokumentum munkafolyamat | PARKED |
| 28 | `src/meetings` | Meeting/notes UI | PARKED |
| 29 | `src/music-studio` | Zenekészítési/DAW jelölt | MEDIUM |
| 30 | `src/notes` | Jegyzetalkalmazás | PARKED |
| 31 | `src/parametric` | OpenCascade WASM, sketch/feature tree, STEP/STL, tool host, early alpha | HIGHEST |
| 32 | `src/pdf` | PDF-szerkesztési UI | MEDIUM |
| 33 | `src/photo-studio` | Réteges PSD és böngészős képszerkesztés | HIGH_VALUE |
| 34 | `src/pos` | Értékesítési pont app | PARKED |
| 35 | `src/presentation` | Prezentációs UI | MEDIUM |
| 36 | `src/projects` | Projektkezelés | PARKED |
| 37 | `src/property-management` | Ingatlanüzemeltetés | PARKED |
| 38 | `src/records` | Adatnyilvántartás | PARKED |
| 39 | `src/shifts` | Műszakbeosztás | PARKED |
| 40 | `src/signatures` | Digitális aláírási app | PARKED |
| 41 | `src/solitaire` | Játék | PARKED |
| 42 | `src/spreadsheet` | Táblázatkezelés | MEDIUM |
| 43 | `src/sudoku` | Játék | PARKED |
| 44 | `src/survey` | Kérdőívek | PARKED |
| 45 | `src/tasks` | Feladatkezelő | PARKED |
| 46 | `src/teamchat` | Csoportüzenet UI | PARKED |
| 47 | `src/time-tracking` | Munkaidő-mérés | PARKED |
| 48 | `src/vector-studio` | Vektorgrafika és vektorszerkesztés | MEDIUM |
| 49 | `src/video-studio` | Webes timeline és videószerkesztés | HIGH_VALUE |
| 50 | `src/whiteboard` | Interaktív vászon | PARKED |
| 51 | `src/wiki` | Tudás- és tartalomszerkesztés | PARKED |

A táblázat nem azt jelenti, hogy minden alkalmazás implementációja teljes vagy működik. A PARKED elemeket nem adjuk hozzá a telepítőhöz. A legtöbb CRM/játék/business app jelenleg nem releváns a JARVIS 2.0 első mérföldköveiben.

## 5. Speciális HeyPuter alkalmazások P6 részletes vizsgálata

### Parametric AI CAD — legmagasabb R&D-prioritás

OpenCascade WASM-geometriamag, parametrikus sketch és constraints, feature-tree, STEP/STL export, agent/host/tool réteg. A JARVIS illesztő az alábbi szerződéssel működne: `open_project`, `inspect_document`, `inspect_feature_tree`, `propose_operation`, `preview_diff`, `commit_operation`, `undo`, `export_step`, `export_stl`. Ezek **tervezett JARVIS adapter API-nevek**, nem állítjuk, hogy ma a HeyPuter azonos nevű endpointot ad.

Védőkorlát: nem sértheti az eredeti fájlt; mutáció előtt snapshot, egységek/tűrések ellenőrzése, geometriai roundtrip és elérhetetlen feature esetén rollback. Az AI-szöveges mód bekapcsolásához külön Puter cloud vagy saját modelladapter és auth vizsgálat.

### 3D Studio — scene agent

WebGL/Three.js és kiegészítő WebAssembly/Pyodide, scene/object/light/material/camera, AI tool ciklus. A JARVIS adapter view-only query → kiválasztott object edit → undo → export. Nem garantált natív Blender projekt .blend paritás, független art pipeline jelölt.

### CAD 2D

Geometriai rajzolás, DXF roundtrip, PDF/SVG export; ugyanazon mm/inch koordinátarendszer, line/arc/polyline és szerkesztési pontosság teszt szükséges. A forrás early alpha figyelmeztetését megtartjuk.

### Photo Studio és Video Studio

PSD/PSB és layered szerkesztés, valamint timeline/effects/video AI panel. A belső Puter AI funkciók autentikációt igényelhetnek; a local UI szerkesztés és cloud AI külön capabilities. Nem tévesztjük össze a PhotoCraft/FilmCraft natív alkalmazással.

### Audio Studio, Music Studio, Vector Studio

Ezek a JARVIS hanganyag-előkészítés, zeneszerkesztés, vektorgrafika későbbi kreatív eszközei lehetnek; az Audio Studio nem jelent automatikusan magyar TTS vagy hangklón képességet. A referenciahang/adatok publikus repo-ba nem kerülhetnek.

### API Client

Hasznos lehet a PyGPT/FCC `/v1/messages`, `/v1/responses`, SSE és websocket contract kézi teszteléséhez. A helyi böngészős auth és a külső CORS/proxy között külön választás kell; API-kulcs browser storage-ba automatán ne kerüljön.

## 6. Miért nem cseréljük le a FreeCAD/PhotoCraft/FilmCraft tervet?

- Eltérő mélység: a PyGPT és a JARVIS vezérlő, a Rust/Web appok szakosodott editorok.
- Dokumentált alfaverziók: a HeyPuter CAD- és kreatív eszközök bizonyos területeken nem stabilak.
- Deduplikáció: egy felhasználói művelethez csak egy kanonikus projektfájl és egy tulajdonos szerkesztő.
- Licenc és csomagméret: nem ésszerű 32 364 forrásfájlt a JARVIS CORE-ba belemásolni csak néhány 3D tool reményében.
- A lehetséges Puter cloud login külön biztonsági vizsgálat tárgya, nem free-model garancia.

## 7. REA / IronRAG / VoiceStudio / Barehands kapcsolatok

- **REA:** natív binárisok, Electron/browser és firmware vizsgálat, bizonyíték- és kötelezettség-ledger; P0/P5 analitikai segédeszköz, megfelelő sandbox/jogosultság mellett. Nem automatikus decompiler-to-PySide6.
- **IronRAG:** nagy projektforrások kód-aware tudásgráf és grounded search; külön Docker/Postgres/Redis, mérés után; alapból PARKED.
- **VoiceStudio:** helyi beszédplatform és OpenAI-compatible speech API, potenciális magyar hang; P6 és modelljog; alapból PARKED.
- **AI Memory Vault:** Markdown/Obsidian személyes jegyzettár (nem ugyanaz mint IronRAG), és nem kell automatikusan egyszerre két memória.
- **Barehands:** webcam/MediaPipe/Three.js 3D hand tracking; későbbi használható UX extra, nem cseréli le a saját eredeti HUD-t.
- **DeerFlow:** másik agent orchestrator; PyGPT Agents V2 mellett nem válik második globális planneré.

## 8. HeyPuter tesztlista — mind NOT_RUN

| ID | Vizsgálat | Sikerfeltétel |
|---|---|---|
| PUTER-001 | A pinelt source checkout és per-app install | verziók és függőségek rögzítve |
| PUTER-002 | Parametric build, unit és E2E | kimenet hash és test log |
| PUTER-003 | 3D build, Playwright és eseményteszt | determinisztikus scene/test |
| PUTER-004 | CAD DXF be/ki roundtrip | geometria/tűrés megőrzése |
| PUTER-005 | STEP/STL import/export | dimenziók, hibák, geometriai egyezés |
| PUTER-006 | AI tool call és rollback | read, approved mutate, undo |
| PUTER-007 | Qt WebEngine megjelenítés és auth | UI, origin, session elkülönül |
| PUTER-008 | Puter fiók és offline működés szétválasztása | hitelesítési és költséghatárok |
| PUTER-009 | License and dependency scan | MIT/LGPL/MPL és összes NOTICE rendezve |
| PUTER-010 | FreeCAD/PhotoCraft/FilmCraft összevetés | duplikáció döntési jegyzék |

## 9. Döntés

**HeyPuter Everything: HIGH_VALUE_CANDIDATE / PARKED.** A Project Icarus P0→P6 sorrendje változatlan, nincs új kötelező 60 app telepítés. A legnagyobb kutatási érték a `parametric`, `3d`, `cad`, `photo-studio`, `video-studio`, `audio-studio` és `api-client` területen található. Kötelező test/licenc/performance mérés és explicit user jóváhagyás minden runtime aktiválás előtt.
