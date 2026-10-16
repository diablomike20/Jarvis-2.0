# R&D-018 — God's Eye View / JARVIS GeoSpatial Intelligence Console — mély forrásaudit

**Forrás:** https://github.com/diablomike20/gods-eye-view @ `e2274bbf0ceaeb2e14f8a59d63e77000553c6816` · eredeti: https://github.com/bilawalsidhu/gods-eye-view. 2026-10-16-i fork- és kódvizsgálat. `package.json` verzió: **0.2.1**, Node **24.14+ vagy 26.x**. Git-fa: **1936 fájl/blob, 2052 fa-elem**. Forráskód MIT, de a harmadik fél adatai és vizuális elemei külön licenceket követnek.

**Állapot:** `P6_OPTIONAL / HIGH_VALUE_CANDIDATE / PARKED_RND / NOT_INSTALLED / NOT_RUNTIME_TESTED`. „**Stark Industries approval**” = humoros neve a **külön projektgazdai engedélyezési kapunak**; nem jelent automatikus integrációt vagy valódi vállalati jogosítást.

## 1. Mit tud, és mit NEM?

Nyilvános és külső forrásokból felépített, térinformatikai/OSINT-jellegű *vizualizációs felület*, CesiumJS 3D renderrel, helyi Node köztes API-kkal, külön réteg-adapterekkel, OpenAI Realtime-alapú hangvezérléssel és Model Context Protocol eszközökkel. **Nem élő kémműhold, nem univerzális emberekre irányuló megfigyelés, nem hiteles katonai/vészhelyzeti rendszer.** A repülő/hajó adat késhet, az útforgalmi kisautók mozgása szimulált, a kamerák nézetszöge becsült, a Starlink/műhold pozíció számított, a Falcon 9 replay rekonstruált becslés.

A README *„20 layers and map sources”* címkéje a UI-csoportosításra utal. Az alábbi 23 sor az aktuális README felsorolt nyilvános térképi rétegeit és map stack tételét adja; az alrendszerek száma ettől eltérhet.

## 2. Rétegenkénti leltár — 23 source-dokumentált sor

| ID | Képesség | Mit ad a forrás szerint? | Kulcs / feltétel | JARVIS runtime |
|---|---|---|---|---|
| GEV-L01 | 🗺️ Map Stack | Esri satellite imagery, Google Photorealistic 3D, OSM, plus additional ion-hosted stacks | 🟢 Esri satellite + OSM · 🟡 ion-hosted Google 3D + world terrain · 🔴 direct Google + place search | NOT_RUN |
| GEV-L02 | ✈️ Live Flights | 11,000+ live aircraft + route history | 🟢 (🟡 optional for more polling credits) | NOT_RUN |
| GEV-L03 | 🎖️ Military Flights | ADS-B military traffic in amber, emergency broadcasts in red | 🟢 | NOT_RUN |
| GEV-L04 | 📡 GNSS Integrity | Regional navigation accuracy scores; anomalies do not confirm interference | 🟢 | NOT_RUN |
| GEV-L05 | 🔥 Fire Perimeters | Incident boundaries and reported containment | 🟢 | NOT_RUN |
| GEV-L06 | 🚢 Live Vessels | Thousands of ships worldwide | 🟡 | NOT_RUN |
| GEV-L07 | 🛰️ Satellites | 838-object catalog, color-coded by class with a live legend — the **DENSE** chip drops in the whole Starlink shell | 🟢 | NOT_RUN |
| GEV-L08 | 🌍 Earthquakes | Global seismic activity, last 24h | 🟢 | NOT_RUN |
| GEV-L09 | ◍ Air quality | Live AQHI on the published 1–10+ health-risk scale, with a Weather-panel card showing the band legend and the highest readings in view. **Canada only** — ECCC is the first registered provider | 🟢 | NOT_RUN |
| GEV-L10 | 🚗 Traffic | Simulated vehicles on OSM roads. With TomTom, live flow speeds drive the simulation and congestion colors below ~8 km; individual vehicle positions are not live observations | 🟢 simulation · 🟡 live flow speeds | NOT_RUN |
| GEV-L11 | 📹 CCTV Mesh | ~4,000 public cameras (shared cap) projected _into_ the 3D space — Austin · Texas (TxDOT) · California (Caltrans) · London (TfL) · Ontario (511) · Finland (Fintraffic) · British Columbia (DriveBC) · Estonia (Tallinn, Tarktee) · Delaware (DelDOT live video) · New South Wales (Live Traffic NSW) · Calgary · Norway (Statens vegvesen) · Toronto · King County (WA) · Washington (WSDOT) · Catalonia (Servei Català de Trànsit), plus opt-in New York City (NYC DOT TMC, needs your own NYC DOT agreement) and opt-in Lithuania (Via Lietuva / Eismoinfo, photo licence unconfirmed). Positions are published; poses are estimated priors **you calibrate by dragging a gizmo on the camera itself** | 🟢 | NOT_RUN |
| GEV-L12 | 📷 Mapped ALPR Cameras | License-plate-reader camera locations tagged by OpenStreetMap contributors, loaded one city-sized view at a time, with **SHOW NEAREST**. Locations and tags only: no plate data, no video | 🟢 | NOT_RUN |
| GEV-L13 | 📷 Street Level | Street-level photos behind one panel, one chip per provider: coverage on the streets, image cones, an embedded viewer and **FOLLOW**. Mapillary, Google Street View, KartaView and Panoramax | 🟢 KartaView, Panoramax · 🟡 Mapillary token · 🔴 Google Maps key | NOT_RUN |
| GEV-L14 | 📻 Radio | Geolocated world radio with an **analog tuner** — drag the needle across up to 750 stations and the globe flies to each broadcaster | 🟢 | NOT_RUN |
| GEV-L15 | 🚌 Transit | Live buses, trams, metros, trains and ferries with delayed playback between reports, selected-vehicle trails, and mode-coloured DETECT labels — Boston, Austin, Minneapolis, Helsinki, the Netherlands, Norway, South East Queensland, and nine in Ontario: Toronto (surface vehicles; the subway publishes no positions), Mississauga, Hamilton, Durham Region, York Region, Guelph, Burlington, Barrie and Kingston | 🟢 | NOT_RUN |
| GEV-L16 | 🚲 Bikeshare | Live station availability | 🟢 | NOT_RUN |
| GEV-L17 | 🧭 Directions | Click A and B on the globe for a street-following drive, walk or cycle route draped on the terrain with turn-by-turn steps — then FLY the camera along it. No key, no geocoder, no mic | 🟢 | NOT_RUN |
| GEV-L18 | 🔥 Active Fires | Live NASA FIRMS detections, trailing 24h | 🟡 | NOT_RUN |
| GEV-L19 | 🚀 Space Missions | Rolling 30-day launches with payload, stage, and recovery detail | 🟢 (🟡 optional token raises the allowance) | NOT_RUN |
| GEV-L20 | 🎖️ Mapped Installations | Viewport-bounded military-site context from community mapping — incomplete by nature, and labeled that way | 🟢 | NOT_RUN |
| GEV-L21 | 🌬️ Wind | Animated 10 m forecast wind with an optional speed, temperature or pressure color field and a reading at map center | 🟢 | NOT_RUN |
| GEV-L22 | 🌦️ Observed Weather | Rain radar (contiguous US), Satellite clouds (GOES regional or global infrared, Clouds only or Full image) and Lightning density (Americas and Pacific) on one history timeline | 🟢 | NOT_RUN |
| GEV-L23 | 🌀 Cyclones | Advisory positions, forecast tracks and uncertainty cones for the Atlantic and eastern/central North Pacific | 🟢 | NOT_RUN |

A listán felüli kiegészítések: Street Level multi-provider (Mapillary, Google Street View, KartaView, Panoramax), `Recent Imagery` (Landsat/Sentinel és VIIRS fallback), Local Receivers (WebUSB és saját ADS-B decoder), bundled statikus infrastruktúra (adatközpontok, gátak, tenger alatti kábelek). A REA és HeyPuter ettől teljesen külön alrendszerek.

## 3. Egyéb alkalmazásfunkciók és megőrzendő működés

| ID | Funkció | Leírás |
|---|---|---|
| GEV-S01 | **Cockpit / Contact Roster** | Kiválasztott repülő követése, megjelenítés tereppel és kontaktlistával; szimulált kamera, nem valódi fedélzeti kamera. |
| GEV-S02 | **HUD és optikai stílusok** | Normal, CRT, NVG, FLIR/thermal jellegű shader, noir/snow, detection overlay és dashboard. Megjelenítő effekt, nem hőmérsékletmérés. |
| GEV-S03 | **Hangos jelenetvezérlés** | OpenAI Realtime, kontextus, kamera- és layer parancsok, annotáció, query, javítás; magyar JARVIS hang nem kész. |
| GEV-S04 | **Scene Director** | Időzített kameraállások, shotok, rétegek, stílusok, rendezés, import/export; v5 JSON, migráció a régi séma verziókból. |
| GEV-S05 | **Megosztható nézetek** | Kamerahelyzet, műhold-/repülőkövetés, stílus, annotáció és rétegállapot URL/nézet formában. |
| GEV-S06 | **MCP Apps panel** | show_in_gods_eye_view, külön megjelenítőpanel támogatott klienseken; PyGPT MCP Apps UI-kompatibilitás tesztelendő. |
| GEV-S07 | **Lokalizált keresés és útvonal** | Koordináták, beépített helynevek, Google/Photon/Nominatim és OSRM útvonal, 3D kamera-flythrough. |
| GEV-S08 | **Local SDR receiver** | WebUSB RTL-SDR, 1090MHz dekódolás, külső dump1090/978 aircraft.json; saját eszköz szükséges. |
| GEV-S09 | **Friss műholdfotók** | Landsat/Sentinel-2 és VIIRS forrásból legújabb elérhető kép, nem élő optikai adat. |
| GEV-S10 | **Infrastruktúra** | Bundled datacenter, dam, submarine cables; TeleGeography NC adatlicenc külön. |
| GEV-S11 | **Földrajzi annotáció** | Vonal, polygon, pin, nyilak, címkék, route marks, megosztható projektnézet. |
| GEV-S12 | **Távoli adatfogadás** | Forrásoldali adapterek, local-first caching/proxy, korlátozott és visszavonható requests. |
| GEV-S13 | **App lifecycle** | createApplication(scene,controls,data,tools), start/destroy, abort, cleanup, unavailable state. |
| GEV-S14 | **UI tulajdonosi határok** | Kamera ownership, cockpit, panels, styles, view state, stale callback tiltása. |
| GEV-S15 | **Biztonsági keret** | localhost, explicit CSP/embed allowlist, credential proxy, SSRF védelem; nem production hardening. |
| GEV-S16 | **Kísérleti fiókos hang-auth** | Codex OAuth használat lehetőség, de az OpenAI Realtime-alapú third-party szerződés nincs biztosítva. |

### A JARVIS 2.0 felhasználói élménye (célállapot, még nincs implementálva)

„JARVIS, nyisd meg a Geo Console-t, mutasd a földrengések és ciklonok térképét, majd készíts belőle egy kameramozgásos bemutatót.” A PyGPT csak az engedélyezett térképes MCP eszközöket és nézetparancsokat hívja; a külön Node alkalmazás renderel; a JARVIS HUD a feladat állapotát mutatja. Térképi állapot akkor sikeres, ha a vezérlő valódi visszaigazolást kap.

„JARVIS, mutasd ezt a várost felülnézetből 3D-ben, csapadékradarral.” A 3D minőség a Cesium/Google kulcsoktól és szolgáltatói feltételektől függ; ingyenes Esri/OSM esetén más szintű alapréteg jön.

## 4. A `docs/TOOLS.md` alapján igazolt 40 MCP-eszköz

Az alábbi eszközlista **nem azonos** a README külön említett „30 voice tool”-jával. Utóbbi az alkalmazás hangos vezérlési munkamenetének saját eszközkészletére vonatkozik, amely querykat és UI-akciókat is tartalmaz. Az MCP-katalógus 40 sora közé tartozik a kizárólag panelbeli `panel_request` is.

| ID | MCP név | Forrás | Mit adhat vissza? | Státusz |
|---|---|---|---|---|
| GEV-T01 | `get_earthquakes` | `earthquakes` | USGS M2.5+ events in the last 24 hours, strongest first | NOT_RUN |
| GEV-T02 | `get_active_fires` | `fires` | NASA FIRMS detections in an area, highest radiative power first | NOT_RUN |
| GEV-T03 | `get_recent_launches` | `launches` | Launch Library 2 launches in the last 30 days, newest first | NOT_RUN |
| GEV-T04 | `aircraft_in_area` | `aircraft` | Aircraft in an area, nearest first; `military: true` reads the `military` feed | NOT_RUN |
| GEV-T05 | `find_aircraft` | `aircraft` | Aircraft anywhere by callsign, ICAO address or registration | NOT_RUN |
| GEV-T06 | `get_aircraft_track` | `aircraft` | Recent positions of one aircraft, thinned to 200 points | NOT_RUN |
| GEV-T07 | `get_aircraft_info` | `aircraft` | Aircraft type and registration, and flight route, from adsbdb | NOT_RUN |
| GEV-T08 | `vessels_in_area` | `vessels` | Ships reported by AIS in an area, nearest first, optionally by type | NOT_RUN |
| GEV-T09 | `find_vessel` | `vessels` | Ships anywhere by MMSI, IMO number or name | NOT_RUN |
| GEV-T10 | `get_vessel_track` | `vessels` | Recent positions of one ship, thinned to 200 points | NOT_RUN |
| GEV-T11 | `next_satellite_pass` | `satellites` | Next pass over a place or point (default the ISS), with naked-eye visibility | NOT_RUN |
| GEV-T12 | `satellites_overhead` | `satellites` | Satellites in a CelesTrak group above a place or point now, highest first | NOT_RUN |
| GEV-T13 | `find_cctv_cameras` | `cctv` | Public cameras in an area, nearest first | NOT_RUN |
| GEV-T14 | `get_cctv_snapshot` | `cctv` | The current image from one camera, returned as image content | NOT_RUN |
| GEV-T15 | `find_alpr_cameras` | `alpr` | OpenStreetMap-mapped license plate readers in a US/Canadian area up to 3° | NOT_RUN |
| GEV-T16 | `find_radio_stations` | `radio` | Radio Browser stations by area and/or search terms, with stream URLs | NOT_RUN |
| GEV-T17 | `search_places` | `placeSearch` | Points of interest matching a query within an area (Google Places) | NOT_RUN |
| GEV-T18 | `places_nearby` | `placeSearch` | Notable places around a place or point (Google Places) | NOT_RUN |
| GEV-T19 | `plan_route` | `routing` | Walking, driving or cycling route over OpenStreetMap, with a simplified path | NOT_RUN |
| GEV-T20 | `get_bike_share` | `bikeshare` | Live GBFS stations in an area, with bikes and docks available | NOT_RUN |
| GEV-T21 | `get_transit_vehicles` | `transit` | Live GTFS-Realtime vehicle positions in an area, optionally one route | NOT_RUN |
| GEV-T22 | `get_traffic_flow` | `traffic` | TomTom flow in a city-sized area: speed vs free flow, congested and closed road | NOT_RUN |
| GEV-T23 | `get_weather` | `weather` | Current conditions at a place or point | NOT_RUN |
| GEV-T24 | `get_weather_map` | `weatherMaps` | The latest NOAA radar, satellite or lightning map image over an area | NOT_RUN |
| GEV-T25 | `get_wind` | `wind` | GFS or IFS model wind 10 m above ground at a location | NOT_RUN |
| GEV-T26 | `get_recent_imagery` | `imagery` | The most recent clear Landsat/Sentinel-2 image of an area (VIIRS fallback) | NOT_RUN |
| GEV-T27 | `find_submarine_cables` | `cables` | TeleGeography cables and landing points by area or name (CC BY-NC-SA 3.0) | NOT_RUN |
| GEV-T28 | `find_infrastructure` | `infrastructure` | OpenStreetMap datacenters or dams in an area, nearest first (ODbL) | NOT_RUN |
| GEV-T29 | `get_bhote_koshi_flood` | `events` | The 2026 Bhote Koshi flood: evidence trail in story order, flood path and imagery dates (CC BY-NC 4.0) | NOT_RUN |
| GEV-T30 | `get_regional_brief` | `regional` | What and where a location is, its weather and recent headlines | NOT_RUN |
| GEV-T31 | `get_cyclones` | `cyclones` | Active NHC/CPHC tropical cyclones, optionally in an area | NOT_RUN |
| GEV-T32 | `get_fire_perimeters` | `perimeters` | Mapped WFIGS wildfire perimeters in an area, largest first | NOT_RUN |
| GEV-T33 | `get_terrain_height` | `terrain` | Ground, geoid and ellipsoid heights at up to 20 points | NOT_RUN |
| GEV-T34 | `find_military_installations` | `installations` | OpenStreetMap military sites in an area of at most 10° per side | NOT_RUN |
| GEV-T35 | `get_map_features` | `features` | Administrative areas, named places or monuments at a location (needs Overpass) | NOT_RUN |
| GEV-T36 | `situation_brief` | `weather` | Weather, earthquakes, fires, aircraft, ships and cyclones for an area, by section | NOT_RUN |
| GEV-T37 | `military_awareness` | `military` | Military and other aircraft, ships and military installations within 250 km of a point, by section | NOT_RUN |
| GEV-T38 | `get_hud_caption` | `weather`, `summary` | The app's heads-up display caption for an area | NOT_RUN |
| GEV-T39 | `show_in_gods_eye_view` | `app` | A view in God's Eye View: the live panel in clients with MCP Apps, and a link everywhere; takes another answer's view or an area or camera, layers, style, map, marks and something to follow | NOT_RUN |
| GEV-T40 | `panel_request` | `app` | Panel only: loads a path from the app's server for the God's Eye View panel | NOT_RUN |

Az azonosító szerinti repülő/hajó lekérdezés, publikus kamera, katonai jellegű információ és rendszámolvasó kamerák helyadata **érzékenynek minősítendő**, külön approval és célkorlátozás; nem tervezünk személykereső, profilozó vagy illetéktelen követési funkciót.

## 5. Konkrét belső fájlok és komponensszerződések

- `src/main.js`, `src/standalone/application.js`: böngészőoldali kiindulás és alkalmazáskompozíció.
- `docs/APPLICATION.md`: `createApplication` függvény, `createScene` → `createControls` → `createData` → `createTools` sorrend; `start()/destroy()`, abort, cleanup; **egy standalone app/page**.
- `src/ui/`, `docs/UI-OWNERSHIP.md`: render, kamera, cockpit, panel, megjelenítés és állapot; nincs tetszőleges új több-ablakos komponens csatolási garancia.
- `src/layers/`, `server/providers/`: geoadat/layer és proxy szétválasztás.
- `src/tools/`, `src/tools/queries/`, `src/tools/mcp/`, `server/mcp/stdio.js`: hordozható eszközkontraktus, MCP stdio és streamable HTTP, Node adapter.
- `docs/TOOLS.md`: MCP `tools/list`/`tools/call`, terület argumentum, `show_in_gods_eye_view` és a panel.
- `src/app/embed.js`: `?embed=1` csak globe; `gev:ready`, `gev:view`, `gev:view-applied` postMessage.
- `docs/VOICE-OWNERSHIP.md`: OpenAI Realtime lifecycle, 500ms space PTT, tool cancellation, barge-in, hang/rádió handoff, cost metrics.
- `src/director/`, `src/scenes/`, `docs/SCENE-DOCUMENT.md`: scene playback, JSON v5, shot timing, import/export és validáció.
- `docs/MCP_SETUP.md`: Node stdio MCP és `/mcp` HTTP, helyi port.
- `SECURITY.md`, `DATA_SOURCES.md`, `THIRD_PARTY_NOTICES.md`, `LICENSE`: kötelező források jogi/technikai ellenőrzéshez.

## 6. A javasolt JARVIS architektúra (PROPOSED, nem kész)

```text
Felhasználó → JARVIS HUD (eredeti UI, P5 után)
                      ↓ feladat / engedély
               PyGPT Agents V2 (P2)
                      ↓ megengedett MCP / geo nézet
               GeoSpatial adapter / supervisor
                      ↓ localhost, authenticated, rate-limited
               God's Eye View (Node/Cesium)
                      ↓ scene, camera, layer, source states
                QWebEngine vagy külön böngésző
```

**Nem portolnám át az egész CesiumJS programot PySide6-ra.** A Qt WebEngine eleve webes réteghez illeszkedik; megőriznénk a teljes JS/render komponenst, és csak IPC-t/MCP-t illesztenénk.

Három egymástól független beépítési szint:
1. `npm run mcp` → stdio bridge; kezdetben read-only, szigorúan allowlisted queries.
2. `http://127.0.0.1:4173/mcp` → a dokumentáció szerint csak loopback/azonos host Origin, proxyból tiltva, nem önmagában komplett auth.
3. `?embed=1` Qt WebEngine → csak `GEV_EMBED_FRAME_ANCESTORS` explicit CSP engedéllyel; `gev:ready` → `gev:view` → `gev:view-applied` valós ACK. A default frame tiltás `X-Frame-Options:DENY` / CSP `frame-ancestors none`.

Az `show_in_gods_eye_view` MCP Apps panel kliensoldali UI támogatása **külön kompatibilitási tesztet** igényel: nem bizonyított, hogy PyGPT minden szükséges MCP Apps erőforrást megjelenít.

Egyetlen geo vizualizációs task gazdája legyen a PyGPT+JARVIS felügyelet, a GEV ne váljon versengő globális AI-orchestratorrá. JARVIS eredeti HoloGlobe-ja védett. Ha egy réteg nem támogatott/nincs kulcs: `CAPABILITY_UNAVAILABLE`, nem „kész”.

## 7. API-k, adatminőség, pénz, licencek

- Keyless alap Esri + OSM és több publikusan elérhető feed, de provider kvóta és országfüggés fennáll.
- Opciók: Cesium ion, Google Maps, OpenAI Realtime, AISStream, NASA FIRMS, TomTom, Mapillary; opcionális magasabb kvótához OpenSky és Launch Library 2.
- Browser-visible kulcsok: Cesium ion, Google Maps, Mapillary. A `SECURITY.md` szerint domain/API restriction kötelező; backend titok: OpenAI/AISStream/OpenSky OAuth.
- OpenAI API-alapú beszéd mérés/költség; a README $5 hard cap a saját API-key voice session logikára vonatkozik, **nem** általános Google/Cesium számlázási plafon.
- ChatGPT/Codex OAuth-on keresztüli Realtime kísérleti — a projekt maga sem állít biztos harmadik feles szerződést; JARVIS-ban ez nem alap-útvonal.
- TeleGeography tenger alatti kábeladat: CC BY-NC-SA 3.0, nem automatikusan redisztribuálható kereskedelmi módban; Bhote Koshi eseményképek CC BY-NC 4.0; Google/Cesium, városkamerák, fotók és README demóanyagok saját jogokkal. Forrás-MIT csak a programkódra érvényes.
- Ha az adat stale, estimated, simulated, missing vagy third-party fallback, a GUI mutassa. Vészhelyzeti/navigációs/taktikai döntésekhez nem hitelesített.

## 8. Biztonság és a Stark Industries Approval Gate

- Kizárólag nyilvános és jogszerűen elérhető adatok. Tiltott JARVIS-funkció: név szerinti személykeresés/arcazonosítás, privát kamerák felkutatása, valaki folyamatos követése/összevont profilja, célzott fizikai veszélyeztetés.
- Megosztott LAN-ból a kulccsal működő proxyszolgáltatásokat elérhetik; ezért a GEV nem kerül automatikusan `0.0.0.0` címen üzembe.
- Az MCP `panel_request` kulcsa a forrás szerint panel-routing guard, **nem hitelesítés**. Az engedélyezési keret a JARVIS gateway feladata.
- API-kulcsok public gitbe nem kerülhetnek; `.env` csak védett fájl, storage/keychain előnyben.
- Előbb forrás-/dependency-/DATA_SOURCES licenc-audit, izolált Node futás, allowlist, CSP és security negatív teszt; csak ezután külön owner engedély.

## 9. 30 elfogadási próba (mind NOT_RUN)

| ID | Ellenőrzés |
|---|---|
| GEO-001 | Rögzített Git SHA, Node/npm/lockfile és MIT/3rd party attribution |
| GEO-002 | Izolált `npm ci`, `npm run doctor`, `npm test`, `npm run build` |
| GEO-003 | Windows process indítás/leállítás és recovery |
| GEO-004 | localhost-only szolgáltatás/negative LAN request |
| GEO-005 | MCP stdio initialize/tools/list/one query |
| GEO-006 | HTTP `/mcp` origin és forwarded request tiltások |
| GEO-007 | MCP Apps panel (valós PyGPT klienssel) |
| GEO-008 | Embedded Qt WebEngine originkezelés és CSP |
| GEO-009 | `gev:ready` → `gev:view-applied` egyszeri ACK |
| GEO-010 | Eredeti JARVIS HUD nem változik |
| GEO-011 | Esri keyless + OSM fallback |
| GEO-012 | Opcionális Google/Cesium kulcs tiltott állapot |
| GEO-013 | Repülő telemetria időkésés és freshness címke |
| GEO-014 | Satellites TLE/SGP4 predicted vs observed |
| GEO-015 | Közúti szimulált jármű helyes jelölése |
| GEO-016 | Kamera estimated pose/live-fallback címkék |
| GEO-017 | Radar/viharforrás időablak és regionális hiány |
| GEO-018 | Scene Director v5 export/import roundtrip |
| GEO-019 | Invalid scene verzió elutasítás, állapotvesztés nélkül |
| GEO-020 | Tool query limit, cancellation, stale result |
| GEO-021 | Saját mikrofon és GEV voice nem verseng |
| GEO-022 | Backpressure/frame rate GPU-stressz alatt |
| GEO-023 | OpenAI API és Google/Cesium billing/quotas |
| GEO-024 | Read-only MCP és érzékeny tool deny alapból |
| GEO-025 | Nincs named-person query / person tracking |
| GEO-026 | Harmadik fél data- és média-licencek nyilvántartása |
| GEO-027 | Nem került titok a kliensbundle-ba vagy Gitbe |
| GEO-028 | Nincs eszköz/osztályozásból operatív fenyegetéskövetkeztetés |
| GEO-029 | Health, diagnostics, rollback és eredeti core regresszió |
| GEO-030 | Projektgazdai aktiválási engedély dokumentálva |

**Kimenet:** `PARKED / HIGH_VALUE_CANDIDATE`. A PyGPT→FCC→stabilizálás→eredeti JARVIS HUD→saját extrák sorrendet nem módosítja. A geotérbeli konzol a P6 opcionális modulok közé kerül, nem a központi AI-motor helyére.

### Elsődleges forráshivatkozások

[README](https://github.com/diablomike20/gods-eye-view/blob/e2274bbf0ceaeb2e14f8a59d63e77000553c6816/README.md) · [TOOLS](https://github.com/diablomike20/gods-eye-view/blob/e2274bbf0ceaeb2e14f8a59d63e77000553c6816/docs/TOOLS.md) · [APPLICATION](https://github.com/diablomike20/gods-eye-view/blob/e2274bbf0ceaeb2e14f8a59d63e77000553c6816/docs/APPLICATION.md) · [MCP_SETUP](https://github.com/diablomike20/gods-eye-view/blob/e2274bbf0ceaeb2e14f8a59d63e77000553c6816/docs/MCP_SETUP.md) · [SECURITY](https://github.com/diablomike20/gods-eye-view/blob/e2274bbf0ceaeb2e14f8a59d63e77000553c6816/SECURITY.md) · [DATA_SOURCES](https://github.com/diablomike20/gods-eye-view/blob/e2274bbf0ceaeb2e14f8a59d63e77000553c6816/DATA_SOURCES.md) · [SCENE-DOCUMENT](https://github.com/diablomike20/gods-eye-view/blob/e2274bbf0ceaeb2e14f8a59d63e77000553c6816/docs/SCENE-DOCUMENT.md).

*Ez forrásalapú tervezés és audit. Runtime evidence: NOT_RUN. No source repo modified.*