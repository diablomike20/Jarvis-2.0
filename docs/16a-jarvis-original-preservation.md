# 16a — Eredeti JARVIS / Brahma funkciómegőrzési mátrix

**Forrás:** https://github.com/diablomike20/Jarvis-Ai @ `e0bd3c5a3a258cc1cf35014ae0a35c7b6b9db87f`  
**Fajta:** meglévő modulokból származtatott funkciószerződés; a forrásfájl jelenléte ellenőrzött, a részletes működés és az éles integráció **NOT_RUN**.  
**Szabály:** semmilyen eredeti funkciót nem hagyunk el csendben a P5 GUI-port és a P6 extra munka miatt.

## 1. GUI és főfolyamat

- `main.py`: elsődleges alkalmazás, Qt/Windows event loop, microphone/audio és action importok; jelenleg Google GenAI/Gemini import is látszik — ezt külön migrációs tételként kell kezelni, nem szabad kész modellcserének nevezni.
- `ui.py`: meglévő `BrahmaUI` / PyQt6 Qt widget rendszer, többek között `QWebEngineView`, eredeti theme, parancssáv, HUD és UI eventek. A pontos vizuális határhoz asset + screenshot baseline szükséges.
- `assets/web_background/`: eredeti WebGL/Three.js háttér, megőrzendő (például index.html, shader/OrbitControls). Nem helyettesítendő új animációval.
- `assets/globe/`: 3D HoloGlobe és térkép erőforrások.
- `assets/sounds/`: UI audio cue-k (listening, mission complete, telemetry, deploy).
- `config/`: beállításminták és app settings; valódi kulcsok Gitbe nem kerülhetnek.
- `core/`: voice/hotkey/echo guard/sensorium/identity/state és hasonló működési infrastruktúra — pontosabb osztály-függvény-audit P0-ban.

## 2. Eredeti, tényleges actions/ modul-fájllista és megőrzési terv

A modulok létezését a Git-fában ellenőriztük. A lehetséges funkcionalitás a névből, a JARVIS README-ből és ismert integrációs mintákból következik; minden modul API és teljes működés **ellenőrizendő**.

| ID | Modul | Megőrzendő képességterület | Jövőbeli szerződés / kockázat |
|---|---|---|---|
| JAR-ACT-001 | `attention_monitor.py` | Mikrofon/figyelem és interakciós események | Hangos interakció, interruption, jóváhagyási UI; működés ellenőrizendő |
| JAR-ACT-002 | `auto_heal_engine.py` | Önjavítás és hibakövetés | Traceback diagnózis, izolált patch, test, rollback; néma módosítás tiltott |
| JAR-ACT-003 | `background_monitor.py` | Háttérfigyelési feladatok | CPU, folyamat, értesítés, teljesítmény; állapot és rate-limit |
| JAR-ACT-004 | `brahma_connect.py` | Android companion-kapcsolat | Mobileszköz/értesítés/hívás bridge, engedély és hálózati security |
| JAR-ACT-005 | `brahma_dev_agent.py` | Fejlesztési agent | Forrásvizsgálat, teszt, worktree, review; nem felülírandó |
| JAR-ACT-006 | `browser_control.py` | Böngésző automatizálás | Navigáció, elemzés, interakció; site trust boundary és prompt-injection |
| JAR-ACT-007 | `calendar_scheduler.py` | Naptári feladatok | Esemény/ütemezés, állandó tárolás, időzóna, consent |
| JAR-ACT-008 | `call_assistant.py` | Telefonhívás-asszisztens | Hívásátvétel/átirat/összefoglaló — külső companion és valódi hívásteszt szükséges |
| JAR-ACT-009 | `calorie_counter.py` | Kalória/fitnesz elemzés | Felhasználó által adott adatok feldolgozása; nem orvosi döntéshozatal |
| JAR-ACT-010 | `circuit_assembler.py` | Elektronikai kapcsolási asszisztens | Alkatrész/pinout/feszültség, SVG bekötés, Arduino minták; biztonsági ellenőrzés |
| JAR-ACT-011 | `claude_code_bridge.py` | Meglévő coding-agent híd | Dev agent delegálás; P3 FCC adapterrel ütközésmentesítés |
| JAR-ACT-012 | `clipboard_processor.py` | Vágólap kezelése | Elemzés, formázás, fordítás; privát clipboard külön opt-in |
| JAR-ACT-013 | `code_helper.py` | Kódsegéd | Magyarázat, javítás, generálás; tests/diff/approval |
| JAR-ACT-014 | `computer_control.py` | Rendszerinterakciók | Bemenet/alkalmazásvezérlés; OS hozzáférés és allowlist |
| JAR-ACT-015 | `computer_settings.py` | Windows beállítások | Hangerő, fényerő, hálózat; platform capability és rollback |
| JAR-ACT-016 | `daily_briefing.py` | Napi információs összefoglaló | Naptár/időjárás/feladat összegzés; forrás és időzítés |
| JAR-ACT-017 | `desktop.py` | Windows Desktop műveletek | Ablakok, indítás, fókusz, OS interakció; tilos néma destructive action |
| JAR-ACT-018 | `desktop_organizer_mcp.py` | Desktop Organizer MCP | Fájl- és mappaszervezés; preview/undo nélkül nincs alap engedély |
| JAR-ACT-019 | `dev_agent.py` | Korábbi fejlesztő agent | Meglévő viselkedés audit, duplikáció a brahma_dev_agenttel |
| JAR-ACT-020 | `docx_tools.py` | Word dokumentumok | Létrehozás/szerkesztés/export, stílus, tesztdokumentum |
| JAR-ACT-021 | `file_controller.py` | Általános fájlvezérlés | Fájlolvasás, másolás, írás, átnevezés; traversal védelem |
| JAR-ACT-022 | `file_processor.py` | Fájlfeldolgozás | Tartalom/konverzió/parse; támogatott típusokat fel kell térképezni |
| JAR-ACT-023 | `flight_finder.py` | Repülőútvonalak/keresés | Valódi adatok, időzóna, útvonalak, hiteles provider |
| JAR-ACT-024 | `game_updater.py` | Játékfrissítés | Folyamat, letöltések, platform API, írás és megerősítés |
| JAR-ACT-025 | `geospatial_globe.py` | Holografikus Föld, radar, térkép | 3D/2D megjelenítés és geo API-k |
| JAR-ACT-026 | `google_workspace_mcp.py` | Google Workspace MCP | Dokumentum/naptár/Drive/levelek, OAuth scope |
| JAR-ACT-027 | `instagram_chat.py` | Instagram beszélgetés | Üzenetek, hitelesítés, külső küldés confirmation |
| JAR-ACT-028 | `instagram_mcp.py` | Instagram MCP | API integráció, rate limit, tokenvédett |
| JAR-ACT-029 | `meeting_assistant.py` | Meeting assistant | Átirat, összegzés, action item; felek tájékoztatása és consent |
| JAR-ACT-030 | `mobile_autopilot.py` | Mobilautomatizálás | Android action policy, sandbox, hozzáférés |
| JAR-ACT-031 | `office_builder.py` | PPTX/XLSX készítő | Sablon, dokumentum, grafikon, artifact ellenőrzés |
| JAR-ACT-032 | `office_generator.py` | Office generátor | Word/PPT/Excel többútvonalas generálás; deduplikáció |
| JAR-ACT-033 | `open_app.py` | Alkalmazásindító | Programok és fájltársítások, csak allowlisttel |
| JAR-ACT-034 | `pdf_tools.py` | PDF műveletek | Készítés, export, kinyerés, strukturált vizsgálat |
| JAR-ACT-035 | `playwright_mcp_client.py` | Playwright MCP kliens | Webautomatizálás, accessibility snapshot, API bridge |
| JAR-ACT-036 | `ppt_template_workflow.py` | PPT-sablon munkafolyamat | Branded slide decks, sablonok, export |
| JAR-ACT-037 | `proactive.py` | Proaktív asszisztens | Eseményfigyelés/ajánlat, nem önkényes végrehajtás |
| JAR-ACT-038 | `pushup_counter.py` | Mozgás/fitness számítás | Kamera alapú mozgáskövetés, opt-in |
| JAR-ACT-039 | `reminder.py` | Emlékeztetők | Személyes/ismétlődő, értesítés, cancel |
| JAR-ACT-040 | `screen_processor.py` | Képernyőelemzés | Vizuális kontextus, privát tartalom kezelése |
| JAR-ACT-041 | `send_message.py` | Üzenetküldés | Címzett, tartalom, külső rendszer, explicit approval |
| JAR-ACT-042 | `spotify_controller.py` | Spotify vezérlés | Zene keresés, lejátszás, várólista, hangerő, átadás |
| JAR-ACT-043 | `system_diagnostics_mcp.py` | Rendszerdiagnosztikai MCP | CPU/RAM/processz és egyéb telemetria, typed errors |
| JAR-ACT-044 | `system_manager.py` | OS processz-/rendszermenedzsment | Csak engedélyezett változtatás; kill/reset kontroll |
| JAR-ACT-045 | `test_action.py` | Akció tesztpélda | Szerződés/reference, nem kötelező business feature |
| JAR-ACT-046 | `unlock_device.py` | Eszköz feloldási művelet | Privilegizált, külön threat model és approval |
| JAR-ACT-047 | `upload_video.py` | Videó feltöltés | Externál adatátadás, fájlvédelem, publikálás approval |
| JAR-ACT-048 | `weather_report.py` | Időjárás | Valós provider, előrejelzés és frissesség |
| JAR-ACT-049 | `web_search.py` | Webkeresés | Forrás, hivatkozás, provider, prompt-injection |
| JAR-ACT-050 | `youtube_video.py` | YouTube/Video műveletek | Videókeresés/feldolgozás, jogosultság és külső API |

## 3. További saját mappák, adatok és vizuális elemek

- `features/` — dinamikus eszközök és saját fejlesztések. A kódforrásban például **check_current_stock_prices**, **circuit_schematic**, **crypto_live_price**, **flights_specific_area**, **internet_speed_test**, **live_cricket_scores**, **make_stickman_dance_when**, **market_analysis**, **show_gif** szerepel. Ezekből a `show_gif` külön manifest/skill/test_cases struktúrát is tartalmaz. Nem ígérünk automatikusan valós vagy megbízható tőzsdei adatot csak a fájlnév alapján.
- `actions/spotify_mcp_server/` — külön TypeScript Spotify MCP implementáció, önálló package-lock és tesztek; összehangolandó a PyGPT külső MCP registryvel és a saját `spotify_controller.py`-vel.
- `config/models/hand_landmarker.task` — a forrásban kézlandmark modellfájl szerepel; **ez nem bizonyítja** a Barehands teljes térbeli UI-ját. A meglévő JARVIS kézmozdulat-implementációját külön kell megvizsgálni.
- `core/user_paths`, `memory/`, `workspace_store`, `smart_home`, `sound_manager` (a `main.py`/`ui.py` importjai alapján) — fokozatosan részletezendő, az adat- és állapottulajdonosság megőrzésével.

## 4. Az eredeti README által megnevezett felhasználói képességek

| README funkciócsoport | Megőrzési követelmény | Kötelező ellenőrzés |
|---|---|---|
| Holographic Hardware Assembler & Circuit HUD | Kamera/képernyő/hang alapú elektronikafelismerés, diagram, biztonsági jelzés, Arduino vázlat | Alkatrész/pinout teszt, hibás/hiányos kép, feszültség-korlát |
| Project Ultron — Self-Evolving Skill Crucible | Saját Skill létrehozás és hot-reload, izolált ellenőrzéssel | Sandbox, rollback, tiltott import/parancs, explicit jóváhagyás |
| Proactive Auto-Heal | Diagnózis és karbantartási javaslat, biztonságos repair flow | Crash injekció, diff, test, rollback |
| FFT Waveform / HUD state glow | 9 sávos audio visszajelzés, listening/reasoning/action/muted | Audio minta, frame diff, állapotváltozás |
| Execution tracker | Felhasználói műveleti szakaszok, státusz/idő, inspect panels | Replay, hibák, typed tool JSON |
| HoloGlobe / mapping | 3D Earth, 2D routes, radar, POI | Valós adatforrás és térképszolgáltató, no fake ETA |
| Spotify MCP | Search, playback, queue, volume, device | OAuth, no account és offline hibák |
| API Setup Hub | Provider/külső szolgáltató config, connection test | Titoktárolás, auth, failure state |
| Native audio / vision | Voice, mikrofon, kamera, képernyő | Win10/11, device permission, fallback |
| Windows desktop | Apps, windows, processes, network/display | Éles OS módosítás előtti approval |
| Office Document Architect | DOCX/XLSX/PPTX/PDF | Valós kimenőfájl, preview, képletek és PDF |
| Brahma Connect | Android, notifications, call proxy | Android companion/OS hozzáférés és consent |
| Smart Home Hub | Tuya/Home Assistant | Tokenerőforrás, eszközelfogadás, hálózat |
| Memory & Identity | Preference, project, custom instructions | User-permission, export/delete, régi adat migráció |

## 5. Későbbi portolás funkciószintű elve

Minden `actions/*.py` szerződést így rögzítünk: `action_id`, Python import/entrypoint, argumentum JSON schema, visszatérési szerkezet, sync/async/felhasználói beavatkozás, secrets/permissions, elvárt side effect, rollback, futtatási bizonyíték és GUI-binding. Ha azonos PyGPT-plugin is létezik, egyik implementációt sem töröljük alapból: előbb egy benchmark és paritási összehasonlítás, majd dokumentált tulajdonosi döntés.

## 6. Pozitív és negatív tesztminta

Pozitív: egy támogatott input a meglévő JARVIS-ban eredményt ad, a P5 port pedig ugyanazt az állapotot és kimenetet hozza. Negatív: nincs API kulcs, nincs mikrofon, visszavont file-jogosultság, rossz szintaxis, eltűnő szolgáltató, későn beérkező async válasz, egymással versengő job, user cancel, hibás Windows DPI. A hibáknak megkülönböztethetőnek és visszakereshetőnek kell lenniük.

**Státusz:** preservation inventory, nem lezárt runtime audit. A további fájlszintű forenzikus kibontás a P0/P5 feladata.