# JARVIS 2.0 — TELJES FUNKCIONÁLIS CÉLSPECIFIKÁCIÓ (MASTER)

**Project Icarus / JARVIS UNIFIED**  
**Specifikáció:** JARVIS-FS-2026-10-16 / v1.1  
**Nyelv:** magyar  
**Forrás:** a felhasználó által rögzített célok, a Jarvis-2.0 dokumentációs ág, valamint forráskódban ellenőrzött JARVIS/Brahma, PyGPT, PyGPT_Addons, Free Claude Code, PhotoCraft, LightCraft, FilmCraft és HeyPuter/Everything.  
**Futásidejű állapot:** nincs kész integrált JARVIS 2.0 build; ez a teljes *tervezett* és *megőrizendő* funkciófelület leírása.  
**Közvetlen kiegészítő dokumentumok:** [16a — JARVIS saját funkciók](16a-jarvis-original-preservation.md) · [16b — PyGPT/FCC/Add-ons](16b-core-ai-addons-capability-matrix.md) · [16c — kreatív és kutatási modulok](16c-creative-rnd-heyputer-roadmap.md) · [04–07 komponensleltár](04-pygpt-inventory.md) · [08 IPC szerződés](08-api-event-contracts.md) · [12 elfogadási tesztek](12-test-matrix.md).

> **Alapelv:** egy funkcionalitás attól, hogy a forrásrepositoriban szerepel, még nem garantáltan beüzemelt. Ez a dokumentum elkülöníti a kötelező célállapotot a kutatási lehetőségektől. A „JARVIS 2.0 tartalmazni fogja” az elfogadott funkciókat jelenti a megfelelő fázis sikeres lezárása *után*; nem állítja, hogy ma mind működik.

## 1. Mi a JARVIS 2.0?

Egy olyan egyesített, Windows-központú, magyar felhasználói élményre tervezett AI-asszisztens és alkotó/fejlesztő munkakörnyezet, amely: (1) megőrzi a meglévő Brahma/JARVIS HUD-ot és használható funkcióit; (2) a PyGPT komplex AI, ügynök, RAG és alkalmazáseszköz-képességeire épít; (3) a PyGPT_Addons szelektíven ellenőrzött MCP-, Skill- és Extension-rendszerét használja; (4) külön folyamatban kapcsolja a Free Claude Code (ai_proxy_2) több-szolgáltatós modellgatewayét és kódolóügynökeit; (5) később hozzáadja a hang- és kreatív műhelymodulokat. Az asszisztenshez természetes nyelven, hanggal vagy GUI-n keresztül lehet feladatokat adni; a rendszer szabályozott jóváhagyással, megfigyelhető állapotban dolgozik.

### 1.1. Mi NEM lesz automatikusan a termék része?

A 61 FCC providerbejegyzés nem 61 élő ingyenes modell; 30 MCP bejegyzés nem 30 azonnal működő csatlakozás; a teljes HeyPuter Everything nem kerül automatikusan be; a többi kutatott agentprojekt nem lesz önálló, egymással versengő főkoordinátor. A GUI-port csak a PyGPT–FCC háttérrendszer működésének igazolása után indul. A „self-evolving” nem jelent jóváhagyás nélküli, bármely fájlt módosító automatikus átírást.

### 1.2. Igazságállapotok

- **COMMITTED_TARGET:** felhasználói cél és megőrzési követelmény; még nem feltétlenül kész.
- **SOURCE_IMPLEMENTED / SOURCE_ADVERTISED:** forrásban létező implementáció / README-ben hirdetett képesség; külön runtime teszt kell.
- **INTEGRATION_PLANNED:** célarchitektúrában szerepel, a PyGPT–FCC/JARVIS kötés még nincs kész.
- **OPTIONAL_P6:** később jóváhagyásra váró szakmodul.
- **PARKED_RND:** kutatási tartalék, **nem** megrendelt késztermék-funkció.
- **NOT_RUN / PASS / FAIL / BLOCKED:** tényleges tesztstátusz, bizonyítékkal.

## 2. Eredeti JARVIS/Brahma élmény és asztali kezelőfelület (P5)

**Fő tulajdonos:** JARVIS HUD és integrációs shell. **Forrás:** diablomike20/Jarvis-Ai main.py, ui.py, actions/, core/, assets/; a README által hirdetett funkciók nem mind vannak külön kipróbálva.

**GUI-JAR-001 — 1:1 filmes futurisztikus HUD.** A meglévő PyQt6 grafika, arculat, animációk, kártyák, színséma, gombok, inputok, áttűnések, hangokra reagáló vizuális elemek, popupok, ablakviselkedés és saját erőforrások megőrzése PySide6 átállás után. Nem újratervezett, idegen 3D gömböt készítünk. Determinisztikus screenshot/frame és interakció-paritási teszt.

**GUI-JAR-002 — Hangállapotok és FFT/visualizer.** A command bar hangenergiát, 9-sávos spektrumot és állapotjelző színeket hordozhat. A forrás README szerint a Gold/standby-listening, Cyan/capturing, Purple/reasoning, Green/tool-running és Red/muted állapotok szerepelnek. Az átültetett UI ugyanazon központi állapotgépet tükrözze; hullámforma nem hamis dekoráció.

**GUI-JAR-003 — Feladat-végrehajtási kártyák.** Kinyitható lépések, állapotok, paraméterek, naplókontextus, futásidő, eredmények és jóváhagyások; a JARVIS saját „Visual Chain-of-Thought Execution Tracker” README-jében szereplő panelrendszer megtartandó mint futásidejű, felhasználónak szánt *műveleti napló*, nem rejtett modellgondolatok megjelenítése.

**GUI-JAR-004 — 3D HoloGlobe és térkép.** Meglévő globe/Leaflet/Three.js assets, légi útvonalak, radar és közeli helyek integrációs megőrzése; valós adatforrás/API szükséges, offline és hiányzó kulcs esetén typed degraded state.

**GUI-JAR-005 — Integrációs beállításközpont.** Modellek, API-kulcsok, Spotify, időjárás, intelligens otthon, telefon, munkaeszközök, hang, adatvédelem, profilok és csatlakozási teszt, de a credentialeket titokkezelő tárolja.

**GUI-JAR-006 — Többablakos Windows élmény.** Ablakátlátszóság, mindig felül/overlay, nagy DPI, több monitor, billentyűzetes/mikrofonos navigáció és visszatöltött állapot. A PyGPT eredeti Expert GUI-ja átmenetileg külön kiegészítő felületként megmaradhat.

## 3. Interakció, magyar nyelv, látás és hang (P2 → P5 → P6)

**VOICE-001 — Magyar nyelvű szövegértés:** üzenetváltás, parancsfelismerés, visszakérdezés, magyar lokalizációs szövegek; eltérő LLM szolgáltató választásakor a nyelv nem változhat véletlenül.

**VOICE-002 — STT:** PyGPT Whisper API/helyi Whisper, Google és más audio bemeneti adapterek kezelése; mikrofonlista, push-to-talk/ébresztési lehetőség, beszédszünet felismerés, hibás eszköz és háttérzaj kezelése.

**VOICE-003 — TTS:** PyGPT hangkimeneti adapterek (ElevenLabs, Google GenAI TTS, Google TTS, Azure TTS, OpenAI TTS, xAI TTS) és később a saját magyar JARVIS-hang, külön motor/adapterként, streaminggel és megszakítással.

**VOICE-004 — Egyedi magyar hangkarakter:** a felhasználó által kívánt hang személyazonosságának, hangfelvétel- és modellsúly-jogosultságának vizsgálata; a referenciahang nem kerül public Gitbe. VoiceStudio és F5-TTS magyar modell mint opcionális beszédmotor-jelöltek, hangminőség, késleltetés és GPU teszt után.

**VOICE-005 — Beszéd vezérelt jóváhagyás és barge-in:** az asszisztens hangosan jelezhet engedélykérést, de veszélyes fájl-, kód-, fizetési vagy adatküldési művelethez explicit, ellenőrzött user approval kell. A felhasználó megszakíthatja a beszédet vagy egy feladatot.

**VISION-001 — Multimodális kép/monitor/kamera:** képernyőképek, dokumentumfotók, vizuális hibák, interfészek és hardveres alkatrészek elemzése, kizárólag engedéllyel és megfelelő modell- vagy vision-adapterrel. Kamera nélküli működés degradált módja szükséges.

## 4. Intelligens beszélgetés és multimodális AI-platform (PyGPT, P2)

**AI-001 — Chat és kontextus:** több munkamenet, történet, címkék, témák, üzenetek, fájlcsatolmányok, összefoglalás, profilok, promptok; átlátható model- és tokenköltség.

**AI-002 — Agents/Chat, Agents/Orchestrator, Agents/Swarm, Experts:** ügynökök munkamegosztása, delegálás, részfeladatok, worker-állapot, eredménygyűjtés, kontrollált párhuzamosság, soha nem önállóan versengő kettős task-owner.

**AI-003 — Custom Agents / Autonomous Mode / Research:** feladatprofilok, kutatás, eszközhasználat, több lépés, célkövetés, idő- és költségkeretek, hibából visszatérés; nem korlátlan önjáró internet- vagy géphozzáférés.

**AI-004 — Realtime/Audio, Computer Use, Image, Video, Completion:** az eredeti PyGPT módok kód- és featureparitása; a konkrét szolgáltató/API képes legyen az adott típusra, különben natív fallback vagy megmagyarázott hiány.

**AI-005 — Modellkapcsolatok:** legalább a PyGPT forrásbeli 18 adaptercsalád opcióinak megőrzése: Anthropic, Azure OpenAI, Custom, DeepSeek, Eden AI, Forge, Google, Hugging Face, JEV, LiteLLM, Local, Mistral, Ollama, OpenRouter, OpenAI, Perplexity, Voyage, xAI.

## 5. Bővítmény- és eszközrendszer (P2)

**EXT-001 — PyGPT saját plugin-registry:** az eredeti `src/pygpt_net/plugin` 39 funkcionális könyvtára és `base` infrastruktúrája regressziómentesen maradjon; részletes, név szerinti táblák a [04](04-pygpt-inventory.md) dokumentumban.

**EXT-002 — PyGPT 16 app tool:** Agent Builder, Agent Workflow, Audio Transcriber, Calendar, Code Interpreter, Files, HTML Canvas, Image Viewer, Indexer, Media Player, Notepad, Painter, Terminal, Text Editor, Translator, Web Browser. Mindet menün vagy JARVIS-eszközelérési útvonalon is nyilván kell tartani.

**EXT-003 — PyGPT Add-ons katalógus:** 2 külső Extension demo, 30 MCP connector recept, 37 Skills és 11 mintafejlesztési csomag; mindegyiknél forrás hash, licencek, veszélyességi szint, jogosultság, eszközkapabilitás, telepítés/aktiválás és teszt.

**EXT-004 — MCP:** feladat szerint csatlakozó registry, alap read-only, filesystem és GitHub műveletekhez szűkített munkaterület; böngészős, dokumentum-, adatbázis-, Blender, Qdrant, stb. csatlakozók csak a szükségeseket indítva.

**EXT-005 — Skill Resolver:** nem tölt be több száz ismétlődő Skill-t automatikusan. A 37 Add-ons Skill és a Superpowers/Skill Tree átfedések deduplikálása, prioritás, verzió és validáció.

**EXT-006 — Saját pluginfejlesztés / „Project Ultron”:** hiányzó képesség felismerése, saját eszközjavaslat, verziózott forrás és tesztek generálása, izolált sandbox, biztonsági és minőségi ellenőrzés, felhasználói jóváhagyás, rollback; nem korlátlan live patch.

## 6. Modellgateway, Free Claude Code és fejlesztőügynökök (P3)

**FCC-001 — Ai_proxy_2:** elkülönített, hitelesített localhost-gateway a PyGPT mellett, Python-környezet ütközésének elkerülésével; a nyilvános Free Claude Code upstream és a privát anyagok nem másolhatók össze ellenőrzés nélkül.

**FCC-002 — Provider Router:** a Free Claude Code korábban 61 konfigurációs providerbejegyzést és custom provider opciót tartalmazott; ezeket konfigurációs lehetőségként, nem garantált ingyenes hozzáférésként tartjuk nyilván. A pontos lista a [06](06-fcc-inventory.md) dokumentumban.

**FCC-003 — Protocol Gateway:** Anthropic `/v1/messages`, OpenAI Responses `/v1/responses`, count_tokens, streaming SSE, tool call, JSON, gondolkodási/usage adatok protokollkonverziója.

**FCC-004 — Automatikus modellrouting, fallback és költségkeret:** kéréshez megfelelő chat/coding/tool/vision/realtime modell kiválasztása a felhasználó adatvédelmi, helyi/offline és költségszabályai szerint; fallback csak kompatibilis modellre, hiba és quota állapot megjelenítésével.

**FCC-005 — Coding-agent bridge:** Claude Code, Codex, Pi, OpenCode, Cline, Hermes, DeepSeek Harness, Grok Build, Muse Code, Aider és VS Code Chat; azokból csak élesben hitelesített, támogatott kombináció legyen indítható.

**FCC-006 — Kódolási munkamenet:** tervezés, branch/worktree, fájl-olvasás, tesztek, verziódiff, jóváhagyott módosítás, review, eredmény és handoff. Beépített JARVIS `actions/claude_code_bridge.py` és `brahma_dev_agent.py` működése védett; nem felülírandó vakon.

## 7. Hosszú távú memória, projektismeret és RAG (P2/P4)

**MEM-001 — Beszélgetési memória:** felhasználói preferenciák és jóváhagyott kontextus, beszélgetéstörténet, projektkontekstus, session/agent szerepkör elkülönítés, törlés és hozzáférés-szabályozás.

**MEM-002 — Dokumentumindexelés:** PyGPT 30 loader csomagja (Office, PDF, HTML, CSV/JSON/XML, GitHub, Google, Gmail, YouTube, web, adatbázisok). Beolvasott fájl, hivatkozás és frissítés metaadatokkal.

**MEM-003 — Vektor- és RAG-tárolás:** Chroma, Qdrant, Redis, Elasticsearch, egyszerű/ideiglenes/attachment-tárolók és a forrásbeli Pinecone-kapcsolat; válasz legyen visszakereshető és bizonyítható.

**MEM-004 — Projektfolytonosság több AI-chat között:** dokumentációs ág, rögzített forrásverziók, elfogadott döntések, feladatgazda, tesztereredmények, architektúra, új agent kötelező mély onboarding. Az eredeti projektadatok személyes részét nem publikáljuk.

**MEM-005 — Opcionális tudástár-szint:** IronRAG (típusos tudásgráf, 23 MCP eszköz, forrásbizonyíték), AI Memory Vault (Markdown/Obsidian jegyzettár); R&D/PARKED, nem helyettesítik automatikusan a PyGPT memóriáját.

## 8. Windows asztali vezérlés, automatizálás és produktivitás (JARVIS + PyGPT)

**WIN-001 — Alkalmazások és folyamatok:** program megnyitás/bezárás, állapot, erőforrások, ablakelrendezés, CPU/RAM/akkumulátor, Wi-Fi/hangerő/fényerő a működő saját forrásadapterek feltételei szerint. Magas jogosultságú módosítás előtt approval.

**WIN-002 — Bemeneti/UI-automatizálás:** egér, billentyűzet, képernyő, böngésző, Playwright/Chrome eszközök, clipboard figyelés/feldolgozás. Külső oldalak és fájlok tartalma nem adhat utasítást az ügynöknek.

**WIN-003 — Fájlok:** keresés, mappák, másolás/átnevezés, szervezés, tartalomfeldolgozás, transzkripció, indexelés, előnézet, backup/undo. Törlés és felülírás engedélyköteles.

**WIN-004 — Dokumentumok:** professzionális Word, Excel, PowerPoint, PDF; létrehozás, szerkesztés, adatok, képletek, grafikonok, vizuális preview, hivatkozások és hiteles fájlkimenet.

**WIN-005 — Ütemezés, emlékeztető, naptár:** naptárak és események, ismétlődő feladatok, napi összefoglalók, scheduled jobs és proaktív jelzések; külső üzenetküldés jóváhagyással.

**WIN-006 — Kommunikáció és szolgáltatások:** e-mail, Slack, Telegram, Discord, Spotify, Google Workspace, GitHub, Wikipédia/Wolfram, térkép és internetkeresés a meglévő pluginok/csatlakozók és fiókjogosultságok szerint.

**WIN-007 — Okosotthon és mobil:** Tuya, Home Assistant, telefonos Companion/Android, értesítések, hívásasszisztens; a README-ben szereplő funkciók kód- és hardver-függők, csak kipróbálva sorolhatók kész állapotba.

**WIN-008 — Hardveres és műszaki asszisztens:** circuit_assembler, elektronikai alkatrész felismerése, pinout, feszültség-felhívások, rajzolt kábelezés, Arduino/ESP32 jellegű példakód; valódi elektromos bekötéshez külön emberi ellenőrzés.

**WIN-009 — GIS, média és további saját akciók:** HoloGlobe, flight_finder, weather, radar, YouTube, sport/fitnesz mérés, gaming, piac/árfolyam információs modulok és a Jarvis actions/ könyvtár további meglévő elemei. Külső API és pontosság külön tesztelendő.

## 9. Biztonság, autonómia és önfejlesztés (minden fázisban)

**SAFE-001 — Granuláris jogosultság:** olvasás, írás, törlés, programindítás, shell, hálózati adatküldés, fizetős modell, credential-hozzáférés, Git push/merge eltérő jogosultságokkal.

**SAFE-002 — Emberi megerősítés és audit:** pontos parancs/diff és célhely megmutatása, egyszeri jóváhagyás, visszautasítás, időkorlát; hangos jóváhagyás nem lehet könnyen hamisítható kritikus műveleteknél.

**SAFE-003 — Izolált agent execution:** sandbox, Git worktree, változásnapló, saját task tulajdon, race condition ellenőrzés, kill/cancel és rollbacks.

**SAFE-004 — Proaktív hibakeresés és auto-heal:** a meglévő `auto_heal_engine.py` és hasonló kódok nem hajthatnak végre néma, teszteletlen core átírást. Diagnózis → javításjavaslat → izolált teszt → review → alkalmazás → rollback.

**SAFE-005 — Öntanuló/önfejlesztő funkció kerete:** tapasztalat- és workflow-jegyzettár, új Skill indokoltsági vizsgálat, működési tesztek; nem önálló modell-súlyátírás vagy garancia korlátlan önfejlődésre.

**SAFE-006 — Megfigyelhetőség:** változatok, audit log, trace_id, hibakód, retry/fallback, model API költség, erőforrás-használat, health check és crash recovery. Hamis siker, hamis telemetria és hamis eszközadat tiltott.

## 10. Kreatív műhely és CAD (P6, jóváhagyástól és tesztektől függően)

**CREATE-001 — PhotoCraft:** natív Rust képalkotás/szerkesztés, PSD/PSB, rétegek, maszkok, ecsetek, adjustment layers, szövegek, vektorok, non-destructive szerkesztés, agent/CLI/JSON/MCP. A forrás korai alfaként jelzi státuszát, nem garancia Photoshop-paritásra.

**CREATE-002 — LightCraft:** fotókönyvtár/RAW fejlesztés, nem-destruktív fény és szín, fehéregyensúly, tónusgörbe, maszkok, color grading, presetek, export, AI/MCP vezérlés. Forrás Rust; külön processz/adapter.

**CREATE-003 — FilmCraft:** többsávos NLE timeline, vágás, effektek, kulcsképkockák, feliratok, hangkeverés, színkorrekció, render/export, AI parancsok. Forrás Rust, fiatal projekt, kodek/Windows/GPU teszt kötelező.

**CREATE-004 — FreeCAD:** parametrikus modellezés, CAD szerkesztés és export, JARVIS által jóváhagyható parancsok/adapterszintű integráció; konkrét API és automatizálási mélység még tervezendő.

**CREATE-005 — Blender/3D:** a PyGPT Add-ons Blender MCP és esetleges más 3D backend; scene létrehozás, objektummódosítás, anyagok, render, export, csak támogatott end-to-end tesztekkel.

**CREATE-006 — HeyPuter/Everything alkalmazás- és CAD-tartalék:** nem azonos a beépített PhotoCraft/FreeCAD csomaggal. A *kutatási* prioritás: Parametric (OpenCascade WASM + AI tool bridge), 3D Studio (Three.js, agent/tool), CAD 2D/DXF, Photo Studio, Video Studio, Audio Studio, Vector/Music Studio, API Client, dokumentumok/táblázat/PDF. Forrásban **32 364 blob-fájl, 51 közvetlen src alkalmazásmappa** (2026-10-16 vizsgálat), a README „60 alkalmazás” állítása ettől külön; néhány CAD modul early alpha. Puter login/cloud és AI költségfüggőség, külső JS/WASM/Node és licenc audit nélkül nem azonnali modul. [Teljes HeyPuter audit](10a-heyputer-everything.md), [kreatív melléklet](16c-creative-rnd-heyputer-roadmap.md).

## 11. Haladó fejlesztői labor és kutatási tartalék

**LAB-001 — REA (Reverse Engineer Anything):** MCP/CLI, firmware/PE/ELF/Electron/web/Android/runtime elemzés, Ghidra/Hopper/IDA/Binwalk adapterek, evidence ledger, reconstruction obligation/readiness. Először fejlesztői diagnosztikai és paritás-ellenőrző jelölt, nem általános GUI-fordító.

**LAB-002 — Superpowers és kódminőség:** brainstorming, terveket írni, TDD, teszt, code review, worktree, párhuzamos delegálás, verifikáció. A Superpowers Skillek nagy része már PyGPT Addonsban van, ezért deduplikált registry.

**LAB-003 — DeerFlow, Skill Tree, prompt-/modellek/esettárak:** benchmark- és kutatási alapanyag. Nem új kötelező central AI processz. A több száz Skill darabszám nem azonos a minőséggel.

**LAB-004 — VoiceStudio/IronRAG/Memory Vault/Barehands:** P6 jelöltek, nem automatikus buildkövetelmény; beszéd API, strukturált tudásgráf, Markdown személyes jegyzettár, kamera+gesztusvezérelt 3D HUD. Részletes állapot a [10](10-research-backlog.md) dokumentumban.


## 12. Mitől lesz egységes és nem három külön program?

**UNIFIED-001 — Egyetlen központi feladatállapot:** PyGPT orchestrator vezeti az AI feladatot, FCC kezeli a saját coding sessiont, GUI megjelenít; nincs körbe-delegálás.

**UNIFIED-002 — Feladat→kapabilitás automatikus útválasztás:** szöveg, hang, kép, kód, rendszer, dokumentum, 3D alapján a rendelkezésre álló (és engedélyezett) tool kiválasztása; megfelelő provider adapter kiválasztása.

**UNIFIED-003 — Tool operation gate:** minden side effect jogosultság, pontos argumentum, idempotency key, napló és visszaállítás mentén.

**UNIFIED-004 — Multimodális napló és projektdokumentum:** ha egy agent Wordöt ír, az artifact-ként és PDF/preview formában visszajut a GUI-ra; videó/model/forráskód ugyanezzel a feladat-azonosítóval visszakereshető.

**UNIFIED-005 — Hibabiztos folyamatok:** PyGPT/FCC eltérő Python és Qt környezetben, felügyelt indítás, health, cancel, restart, adatvédelmi szegmentáció. Egyik szolgáltatás kiesése nem okozhat észrevétlen hamis sikerüzenetet.

## 13. Használati forgatókönyvek — konkrét célviselkedés

**SCN-01:** „JARVIS, nézd meg a repo hibáját.” → forrás-baseline, branch/worktree, agent tervezés, read-only elemzés, diff, jóváhagyott javítás, unit/integrációs teszt, review, PR csak döntésre, felületi és hangos státusz.

**SCN-02:** „Elemezd ezt a PDF-et, írj belőle Word-dokumentumot és Excel-kalkulációt.” → fájltípus és adatforrás, index/loader, ellenőrzés, többformátumú artifact, preview és letöltés.

**SCN-03:** „Nyisd meg a böngészőt, keresd meg az adatot, emlékeztess holnap.” → engedélyezett browser tool, információ és hivatkozás, scheduler, tartós feladat; weboldalból érkező prompt-injection ne adjon új system parancsot.

**SCN-04:** „A képen ez melyik mikrokontroller? Hová kötsem a szenzort?” → képfeldolgozás, alkatrészdetektálás, pinout SVG overlay, dokumentált feszültségkorlát, emberi hardware ellenőrzés.

**SCN-05:** „Készíts termékfotó-retust és klipszerkesztést.” → PhotoCraft / LightCraft / FilmCraft későbbi adapterrel, projekt-kopián, preview, export, visszavonás, licenc és erőforráskapu.

**SCN-06:** „Tervezd meg ezt az alkatrészt pontos méretekkel.” → P6 FreeCAD vagy igazolt HeyPuter Parametric adapter, geometriai lekérdezés, sketch/feature tree, tűrések, STEP/STL kontroll, jóváhagyott változtatás, mentés.

**SCN-07:** „Magyarul beszélj, közben mutasd a gondolkodási/feladatállapotot.” → STT, agent, TTS, FFT HUD, visszakérdezés, interrupt, folyamatjelző kártyák. Tényleges belső chain-of-thought nem jeleníthető meg; csak felhasználói aktivitás/progress.

**SCN-08:** „Vizsgáld meg ezt a régi szoftvert és bizonyítsd a port viselkedésazonosságát.” → opcionális REA evidence, licencek/jogosultság, összehasonlító tesztek, coverage unknown/partial állapotok, nincs meg nem érdemelt PASS.

## 14. Fázissorrend — nem bővíthető meg észrevétlenül

| Fázis | Kötelező kimenet | Mire NEM állíthatjuk, hogy már kész |
|---|---|---|
| P0 | baseline, audit, megvalósíthatósági próbák | teljes PyGPT/FCC rendszer |
| P1 | új repo, docs ág, elkülönített források | kész alkalmazás |
| P2 | PyGPT + kiválasztott, ténylegesen tesztelt Add-ons | 30 MCP/37 Skill mind aktív |
| P3 | FCC proxy/coding adapter, streaming/tool/fallback | minden modell automatikusan ingyen |
| P4 | stabil közös task/permission/memory, rollback | befejezett JARVIS HUD |
| P5 | eredeti JARVIS GUI paritása és teljes kezelhetőség | tetszőleges új UI |
| P6 | ténylegesen elfogadott kreatív, hang, REA/3D extrák | minden kutatási találat telepített |

## 15. A késztermék bizonyításának minimuma

Külön követelményenként: feature_id, tulajdonos, forrás SHA, runtime, teszt input/output, negatív teszt, jogosultság, GUI megjelenítés, fallback, export, log, képernyőkép/artefakt, teljes regresszió és felhasználói átvétel. A „van róla README” csak SOURCE_ADVERTISED. A 74 eredeti teszt és 10 HeyPuter teszt jelenleg terv, nem lefutott teszt.

## 16. Források és pontosítások

- [Jarvis-Ai — az eredeti, létező modulok és HUD](https://github.com/diablomike20/Jarvis-Ai)
- [PyGPT](https://github.com/diablomike20/PyGPT)
- [PyGPT_Addons](https://github.com/diablomike20/PyGPT_Addons)
- [Free Claude Code upstream](https://github.com/Alishahryar1/free-claude-code)
- [PhotoCraft](https://github.com/diablomike20/photocraft), [LightCraft](https://github.com/diablomike20/lightcraft), [FilmCraft](https://github.com/diablomike20/filmcraft)
- [HeyPuter/everything](https://github.com/HeyPuter/everything)
- [REA](https://github.com/morluto/rea), [VoiceStudio](https://github.com/debpalash/VoiceStudio), [IronRAG](https://github.com/mlimarenko/IronRAG), [AI Memory Vault](https://github.com/jaredrhod/ai-memory-vault)
- [Dokumentációs forrásnyilvántartás](01-source-register.md) és [kutatási backlog](10-research-backlog.md).
- A forrásból ellenőrzött számok és a README kijelentések közötti eltérést (*Everything 51 src könyvtár vs 60 meghirdetett app*) dokumentáljuk, nem tüntetjük el.

**Jelenlegi végeredmény:** ez egy részletes, implementálásra előkészített célspecifikáció, és nem a JARVIS 2.0 már működő változatának leírása. A felhasználó által elfogadott sorrend és a parkoltatott opcionális technológiák határa változatlan.
