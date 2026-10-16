# 03 — diablomike20/gods-eye-view — célzott forrásaudit és JARVIS moduljavaslat

**Repo:** https://github.com/diablomike20/gods-eye-view; publikus fork, eredeti: https://github.com/bilawalsidhu/gods-eye-view.
**Vizsgált alap:** GitHub main 2026-10-16, package.json v0.2.1, 2052 Git-fabejegyzés.
**Státusz:** dokumentált forráskód, nincs JARVIS-ba bekötve, runtime NOT_RUN.

## Valódi technológia
- Webalkalmazás, ESM/TypeScript/JavaScript és Cesium; Node engine `>=24.14.0 <25 || >=26 <27`; Vite fejlesztő/builder; Puppeteer/regressziós eszközök.
- `npm run dev`, `npm run build`, `npm test`, `npm run build:panel`, `npm run mcp`, `npm run check:boundaries` a forrásban definiált parancsok; futtatás most nem történt.
- Kifejezett `./application`, `./sources/*`, `./ui/*`, `./server/providers/*` package exportok; portable modul és render/fetch logika szétválasztás.
- MCP stdio bridge: `server/mcp/stdio.js`, a lokális webalkalmazás HTTP API-ját használja. Ez integrációhoz jobb első cél, mint a teljes vizualizáció PySide6 portja.
- MCP Apps UI: `show_in_gods_eye_view`, `ui://gods-eye-view/globe` embedded interaktív nézet; host támogatása szükséges.

## Forrás által hirdetett és részben megvalósított képességek
1. 3D fotorealisztikus Föld/Cesium/terrain, térképréteg, saját GL/GLSL stílusok: CRT, NVG, FLIR/thermal, Noir, Snow.
2. Élő/periodikusan frissülő repülőgép AIS/ADS-B jellegű jelek, hajók, műholdak, földrengések, tűzesetek.
3. Radar/időjárás/hőmérséklet/szél/NOAA GFS/ECMWF és vihar/figyelmeztetés rétegek. A forrás dokumentálja, hogy nem minden réteg globális vagy közel valós idejű.
4. Public camera/CCTV, open data geospatial infrastructure, datacenters, dams, roads, antenna, street level.
5. Voice-operated analyst toolset, views, entity track, nearby contacts, cockpit/trails, annotations/whiteboard, share links, scene director és formátumok.
6. Satellite passes, closest/nearby, source freshness, fallback, nem támogatott esetekből kihagyott rekordok és pontatlanságok.
7. A screenshot/scene/movie funkciók demo és elemző eszközök; forrásadatok attribúciója kötelező.

## Tisztességes helyzetjelzés
- A README szerint több réteg és pozíció valós nyilvános adatból származik, de **a közúti forgalom aggregált alapadatokon szimulált**; CCTV és rakéta trajektóriák hozzávetőlegesek. Nem kezelhető minden ikon hiteles élő telemetriaként.
- Ingyenes keyless alapműködés lehetséges (pl. Esri imagery/OSM fallback), de Google Maps/Cesium ion külön kulcs és kvóta/licenc.
- A project `LICENSE` és `DATA_SOURCES.md` kimondja: kód MIT, de a bundelt nem kereskedelmi TeleGeography és külön 3D modell/OSM/CC BY-NC-SA, külső imagery/tiles **NEM** automatikusan MIT.
- Publikus repó nem egyenlő szabadon korlátlan üzemi felhasználhatósággal.
- Sűrű városok street traffic, feeds availability, satellite visibility approximations stb. ismert `docs/KNOWN-ISSUES.md` kockázatok.

## JARVIS architektúra-besorolás
**JAVASLAT:** `P6 R&D HIGH_VALUE`, eredeti HoloGlobe megtartása. Felhasználó külön engedélye nélkül nem csinálunk teljes HUD csereprojektet. Első körben geospatial MCP adaptert, később külön WebEngine panelt vagy embed/MCP Apps UI-t tesztelünk, külön Node processz.

## Javasolt contract
- `geospatial.search(query, bbox, provider, max_results)`
- `geospatial.get_layers()`; `geospatial.layer.update(layer, enabled)`
- `geospatial.track(entity_ref, time_window)`
- `geospatial.camera.focus(lat,long,height,pitch,heading)`
- `geospatial.ask(text, source_snapshot_id)`
- `geospatial.scene.export(format)`
Ezek JARVIS absztrakciós *tervek*, nem meglévő God's Eye View API garantált nevei. A tényleges MCP catalogból illeszteni szükséges.

## Tesztek (mind NOT_RUN)
- Node 24 build és lint/unit baseline, külön install hardening.
- MCP tool list / stdio handshake / lokális /api proxy és timeout.
- QWebEngine, Cesium worker CSP/origin kontroll, multi-monitor GPU memory stress.
- 3 jelölt feed frissessége/provenance és azonosító recheck; fallback-esetben explicit flag.
- Public/private adat, API key és dataset legal compliance.
- GUI és 3D globe integráció nem írhatja felül az eredeti JARVIS HUD minőségét.

## Forrásbizonyíték
https://github.com/diablomike20/gods-eye-view/blob/main/package.json
https://github.com/diablomike20/gods-eye-view/blob/main/docs/MCP_SETUP.md
https://github.com/diablomike20/gods-eye-view/blob/main/docs/TOOLS.md
https://github.com/diablomike20/gods-eye-view/blob/main/docs/KNOWN-ISSUES.md
https://github.com/diablomike20/gods-eye-view/blob/main/DATA_SOURCES.md
