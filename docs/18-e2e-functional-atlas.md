# 18 — Teljes JARVIS 2.0 végponttól végpontig funkciószerződés (34 felhasználói forgatókönyv)

**Project Icarus / forrásalapú specifikáció; NEM elkészült integráció.** Ez a MASTER [16](16-jarvis20-complete-feature-specification.md) kiegészítése, nem helyettesítője. A részletes eredeti JARVIS/PyGPT/FCC/Addon/HeyPuter leltár: [16a](16a-jarvis-original-preservation.md), [16b](16b-core-ai-addons-capability-matrix.md), [16c](16c-creative-rnd-heyputer-roadmap.md); God's Eye View: [17](17-gods-eye-view-geospatial-audit.md).

## Fogalmak

- **SOURCE_IMPLEMENTED / SOURCE_ADVERTISED** = másik repo kódja vagy dokumentációja tartalmaz képességet.
- **COMMITTED_TARGET** = tervezett integrált JARVIS alapfunkció; nem most éles.
- **PARKED_RND / P6_OPTIONAL** = még nem végleges funkcióigény, nem aktivált.
- **PASS** = futásidejű bizonyíték, commit, környezet és log; ha nincs, NOT_RUN.

## 1. A teljes képesség-architektúra

```text
JARVIS / Brahma original HUD           magyar voice, kamera, Windows-felügyelet
          |
    JARVIS Supervisor + Approval Service
          |
     PyGPT 2.9.1 (Agents V2, tools, plugins, memory/RAG)
      |                 |                     |
      |             PyGPT_Addons          Native provider/media
      |          30 MCP + 37 Skills           adapters
      |
 FCC / ai_proxy_2 (61 provider recipe; 11 coding clients)
      |
 [Coding sessions, streaming, tool calls, model fallback]

P6_OPTIONAL: VoiceStudio, IronRAG, REA, Barehands, FreeCAD,
             PhotoCraft, LightCraft, FilmCraft, HeyPuter Everything,
             God's Eye View Cesium Globe
```

A diagram logikai; a valós 1:1 működési tesztek még nem futottak le. A fő PyGPT/FCC motorokat és P6 parkoltatott külső eszközöket ne tekintsük egyszerre telepítettnek.

## 2. Forráskód által alátámasztott összes fő domén

| Domén | Eredeti forrás | Leltár és szint |
|---|---|---|
| Original JARVIS GUI és 50 actions-modul | diablomike20/Jarvis-Ai | 16a: egyedi Qt/Windows, audio, smart home, document, 3D globe |
| Asszisztens runtime | diablomike20/PyGPT | 40 plugin mappa, 16 desktop tool, 18 provider family |
| RAG és betöltés | PyGPT | 30 loader, 8 vector store implementáció |
| Multimodal hang | PyGPT | 7 STT és 6 TTS adapter |
| MCP/Skill bővítmények | diablomike20/PyGPT_Addons | 2 addon, 30 connector, 37 Skill, 11 demo minta |
| Modellgateway és coding agent | Alishahryar1/free-claude-code | 61 provider catalog entry, 11 kliens |
| Photo, RAW és NLE | PhotoCraft/LightCraft/FilmCraft | Rust native/agent funkciók, P6 |
| Parametrikus CAD, médiaappok | HeyPuter/everything | 51 külön ellenőrzött src/ appmappa, R&D |
| Forenzika | morluto/rea | MCP evidence/reconstruction, P6 R&D |
| Projektgraf memória | IronRAG | knowledge graph, 23 MCP, 15 nyelv ingest, P6 R&D |
| Hangklónozás | VoiceStudio | helyi TTS/STT/MCP, magyar candidate, P6 |
| Kamerás gesztus | Barehands | MediaPipe/Three.js, P6 |
| Geo + 3D világrétegek | God's Eye View | 23 README réteg/tétel, 40 MCP tool, Scene Director, P6 |

## 3. Teljes felhasználói folyamatok (F-001–F-034)

Minden sor célviselkedés, nem gyártott runtime-eredmény. A „Kimenet” ellenőrzendő elfogadási kritérium, nem GARANTÁLT kész funkció.

| ID | Felhasználói funkció | Példa kérés | Végrehajtó | Ellenőrzött célkimenet | Hibahatár / jogosultság | Fázis |
|---|---|---|---|---|---|---|
| F-001 | Magyar beszélgetés | Felhasználó hangban vagy szövegben magyarul kérdez | JARVIS audio/input → PyGPT Chat → kiválasztott LLM | Érthető magyar válasz + megjelenített állapot | STT/TTS és remote LLM nélkül typed fallback | P2/P5/P6 |
| F-002 | Beszédfeldolgozás megszakítása | Felhasználó közbevág vagy leállít | JARVIS Voice Supervisor; PyGPT audio backend | Beszéd és feladat megfelelően megszakad, nem marad aktív mic | Áramlási állapot és child cancellation | P5/P6 |
| F-003 | Személyes kontextus használata | Mi lett a múlt heti fejlesztési döntés? | PyGPT chat context/memory, projektjegyzetek | Forrással, dátummal megjelölt visszaidézés | Forráshiánynál ne találjon ki emléket | P2/P4 |
| F-004 | Nagy forráskód összefoglalása | Mutasd a modulok kapcsolatait | PyGPT indexing/RAG + loaders; később IronRAG opcionális | Fájlokra hivatkozó architektúratérkép | Belső projekt több tenant esetén strict scoping | P2/P6 |
| F-005 | Kutatás és forrásellenőrzés | Ellenőrizd a legújabb verzió dokumentációját | PyGPT Research/Web + MCP Context7/GitHub | Dátum, URL, forráserősség, hiányok | Offline/kulcshiánynál blokk | P2 |
| F-006 | Komplex fejlesztés delegálása | Javítsd ezt a tesztet, de főágat ne módosíts | PyGPT Agent Orchestrator → FCC coding harness → Git worktree | Diff, tesztlog, jóváhagyható PR javaslat | No direct main write; fail close/rollback | P3/P4 |
| F-007 | AI modell automatikus választása | Legolcsóbb kompatibilis modellt használd | PyGPT Capability Router → FCC provider catalog | Model ID, költség, adatvédelmi routing | Nem támogatott multimodális kérés natív PyGPT-re | P3/P4 |
| F-008 | Valós idejű modellválasz | Írj, miközben dolgozol | PyGPT UI/events → FCC SSE adapter | Érkező tokenek, tool eredmények, status | Hibás chunk/disconnect nem ír kétszer | P3/P4 |
| F-009 | Több agent szétosztása | Kutatás és implementáció párhuzamosan | PyGPT Agents V2, Superpowers jóváhagyott Skills | Szerepek, egy owner, elkülönített munkahely | Körbe-delegálás és konfliktus blokkolt | P2/P4 |
| F-010 | MCP eszköz beállítása | Kapcsolódj a GitHubhoz olvasásra | PyGPT MCP katalogizálás/permissions | Tool list, auth scope, read-only query | Token nélkül BLOCKED_BY_AUTH | P2 |
| F-011 | Önálló képesség fejlesztése | Ehhez még nincs modul; készíts javaslatot | JARVIS Project Ultron + FCC coding + sandbox | Új modul izolált diff és teszteredmény | Auto-register csak policy után, nem önkényesen | P4/P6 |
| F-012 | Automatikus önjavítás | Hibás funkciót azonosít | JARVIS Auto-Heal koncepció + diagnosztika | Hibaelemzés és javasolt patch, teszt | Nem futtathat korlátlan tetszőleges javítást | P5/P6 |
| F-013 | Windows ablakvezérlés | Rendezd el a munkám ablakait | Eredeti JARVIS actions + Qt/Windows supervisor | Átlátható és visszavonható ablakállapot | Rendszerszintű műveletek approval | P5 |
| F-014 | Képernyőkép értelmezése | Mondd el, mi látható ebben az ablakban | JARVIS screen capture + PyGPT vision provider | Szöveges értelmezés, nem személyazonosítás | Screen consent, remote data privacy | P5 |
| F-015 | Dokumentum előállítás | Készíts önéletrajzot DOCX-ben | PyGPT docx/PDF tooling + eredeti JARVIS document actions | Valós ellenőrizhető DOCX/PDF és letölthetőség | Fájlírás jóváhagyás és versioning | P2/P5 |
| F-016 | Táblázat és prezentáció | Készíts diagramot és PPT-t | PyGPT xlsx/pptx skill, Python interpreter | Számítható képletek, ábra, mentett fájl | Nincs dummy kép vagy hallucinált feltöltés | P2 |
| F-017 | Időzített feladat | Holnap ellenőrizd ezt | PyGPT cron/planner vagy JARVIS scheduler owner | Persistens task, pontos ütem, visszamondás | Nincs dupla időzítő; explicit consent | P2/P4 |
| F-018 | Otthon és IoT | Kapcsold fel a saját lámpát | JARVIS smart home, PyGPT Tuya plugin/adapter | Eszközállapot visszaellenőrizve | Csak explicit párosított eszköz | P5/P6 |
| F-019 | Android társalkalmazás | Küldj értesítést a telefonomra | Brahma Connect/Android bridge | Consent alapján átadott felhasználói értesítés | Nincs rejtett üzenetolvasás/adatátvitel | P5/P6 |
| F-020 | Zenelejátszás | Indíts egy lejátszási listát | Eredeti Spotify MCP / PyGPT integrations | Megfelelő eszközön induló lejátszás | Auth és zene licenc korlátok | P5 |
| F-021 | Képszerkesztés PSD-vel | Szerkeszd ezt a réteget és maszkot | PhotoCraft Rust MCP/CLI, PyGPT tool wrapper | Szerkeszthető PSD / PNG, undo | Nem egyezik késznek minden alpha funkció | P6 |
| F-022 | RAW-fotók fejlesztése | Javíts színt és kontrasztot egy sorozaton | LightCraft Rust MCP | RAW fejlesztési projekt és képexport | A tételes funkcionalitás verziófüggő | P6 |
| F-023 | Videó vágása | Állíts össze klipet felirattal | FilmCraft native Rust agent/MCP | Mentett timeline, audio, render | Codec/hardver támogatást mérni kell | P6 |
| F-024 | CAD parametrikus terv | Készíts módosítható alkatrészt | FreeCAD céladapter vagy HeyPuter parametric R&D | Méretre pontos szerkeszthető modell, export | Nem elég csinos render; geometria ellenőrzés | P6 |
| F-025 | Összetett műszaki visszafejtés | Ellenőrizd a program megfigyelhető viselkedését | REA analysis lab opcionális | Forrásbizonyíték és Reconstruction Ledger | Jogosultság és izolált bináris teszt | P6 |
| F-026 | Helyi magyar TTS | JARVIS válaszoljon saját hangon | PyGPT audio_output + VoiceStudio/F5 TTS kandidátus | Hangmintával mért magyar természetesség | Hangjog, VRAM, modelllicenc review | P6 |
| F-027 | Kézvezérelt HUD | Mozgasd az objektumot kézzel | Barehands kamera/MediaPipe/Three.js opcionális | Kézmozgásból kontrollált UI input | Csak kamera permission; nincs biometrikus profil | P6 |
| F-028 | 3D világ térképe | Mutasd Budapestet műholdas 3D-ben | God's Eye View standalone Cesium és PyGPT MCP | Térképréteg tényleges állapottal, source attribúció | Célszabály: Stark Industries gate; ingyenes 2D fallback | P6_OPTIONAL |
| F-029 | Földrengés és időjárás | Mutasd a közelmúlt földrengéseit és szél-előrejelzést | God's Eye View public USGS/GFS/ECMWF adatok | Időbélyegzett geovizualizáció forrásokkal | Előrejelzés/megfigyelés külön és nem vészhelyzeti döntés | P6_OPTIONAL |
| F-030 | Filmes geojelenet | Készíts narrált földgömb animációt | God's Eye View Scene Director és PyGPT elbeszélés | Visszajátszható v5 scene file | Kép/data licencek, videó készítés külön teszt | P6_OPTIONAL |
| F-031 | Geo nézet hívása chatből | Nyisd meg a térképet erre a helyre | PyGPT MCP show_in_gods_eye_view vagy URL | ACK-kal ellenőrzött, megnyitott globe | MCP Apps UI kompatibilitás nincs még bizonyítva | P6_OPTIONAL |
| F-032 | Nyilvános kamera és infra | Mutasd a nyilvános közúti kamerákat egy régióban | GEV public camera layers, read-only policy | Forrás és kamera státusz, térképi környezet | Nincs privát kamera, nem személyfigyelés | P6_OPTIONAL |
| F-033 | Projekttudás mélyítése | Mely API kapcsolódik ehhez a modulhoz? | IronRAG későbbi code-aware RAG | Typed graph/citation a kódra visszamutatva | Csak ha PyGPT RAG-nál benchmark jobb | P6_OPTIONAL |
| F-034 | Munka átadása új agentnek | Folytasd a fejlesztést új chatben | Dokumentációs ág source register, handoff, test registry | Reprodukálható kontextus és branch-boundary | Nincs hamis memory vagy ellenőrizetlen PASS | P0_ALL |

## 4. Minden funkcióra közös szerződés

1. `input_schema`: felhasználói nyelvi utasítás + tartalmi típus + csatolmány + ismert korlát.
2. `capability_lookup`: a model/provider/plugin/Skills/MCP választás a tényleges aktivált catalog és provider capability alapján történik.
3. `task_owner`: csak egy globális task owner; coding session másodlagos ownerként szerződéssel.
4. `approval`: shell, file edit, outbound message, privileged Windows/IoT, drága API, geokamera stb. jóváhagyás kapun át.
5. `execution`: tipizált tool call és response, task/session/correlation/trace ID-vel.
6. `streaming`: indítás, időközi állapot és részleges eredmény külön jelölve; tool nem duplázhat írást retry miatt.
7. `result`: konkrét programállapot, hivatkozás, fájl, log, modellinput/kimenet metaadat; nem elég „elkészült”.
8. `degradation`: missing API key, nem támogatott modell, offline provider, blocked licence, hiányzó hardver — őszinte típusos státusz.
9. `rollback`: munka és fájl módosításai rekonstruálhatóak; risk-szinthez igazodó snapshot.
10. `tests`: unit, contract, integration, acceptance és negatív esetek a fáziskapuk alapján.

## 5. Fázisonkénti valós állapot

| Fázis | Funkciók | Egyelőre igazolt | Következő kapu |
|---|---|---|---|
| P0/P1 | Források rögzítése, dokumentáció és ágak | GitHub ágak + dokumentumok/szubrendszer SHA-k | Windows checkout és test |
| P2 | PyGPT + szűrt Add-ons | Pinelt Git submodule integrációs ágon | Élő PyGPT start, Plugin/Skill/MCP E2E |
| P3 | FCC ai_proxy_2 | Kutatott publikusan elérhető upstream | Local auth + /v1/messages/stream/tool/coding |
| P4 | Backend-házasítás | Architekturális specifikáció | Több agent közös E2E hiba/fallback |
| P5 | Original JARVIS HUD | Forrás és preservation leltár | Paritás, Qt/Windows tesztek |
| P6 | Kreatív, helyi TTS, geo/CAD/RAG/reverse | Source/reference backlog | Modulonként külön jóváhagyás, licencek és proof |

**Szabály:** Semmilyen P6 parkolt rendszer, különösen God's Eye View, nem gyorsítható automatikusan P2/P3-ba csak attól, hogy integrálható MCP-n keresztül.

## 6. Következő mérnöki feladat: capability-to-code proof

A 34 elfogadási történetet csak az eredeti 65 master célfunkcióval és a 157 korábbi inventory rekorddal **egyirányúan cross-reference-eljük**. A feladatgazdák ne gyártsanak eltérő, párhuzamos globális termékdefiníciókat. Az egyes P2/P3/P5 forráshelyeket osztály/funkció és tesztazonosító szintig kell bontani a megvalósításkor. Itt még egyetlen sor sem kapott PASS státuszt.

Források: [16 MASTER](16-jarvis20-complete-feature-specification.md) · [16a original](16a-jarvis-original-preservation.md) · [16b core](16b-core-ai-addons-capability-matrix.md) · [16c creative](16c-creative-rnd-heyputer-roadmap.md) · [17 God's Eye View](17-gods-eye-view-geospatial-audit.md) · [04–07 inventárium](04-pygpt-inventory.md).