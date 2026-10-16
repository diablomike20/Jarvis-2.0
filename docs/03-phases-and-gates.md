# 03 — Megvalósítási fázisok, fáziskapuk és haladás

A sorrend felhasználói stratégiai döntés. A részletes ellenőrző pontok mérnöki PROPOSED kritériumok. Nincs automatikus továbblépés teszt nélkül.

## P0 — Snapshot, előzetes audit, megvalósíthatóság

- Git commitok, licencek, Függőségek, fájllisták rögzítve.
- PyGPT install/Windows start kockázatok, Qt-coupling, launcher, portok, OS változat.
- Eredeti JARVIS animációk és GUI-baseline eltárolása; PySide6 minimális izolált vizsgálata.
- Hozzáférés, titkos adatok és upstream változásvédelem.
- Kimenet: forráslock, dependency lock, risk register és tesztterv.
- Gate: minden kötelező forrás megvan; nincs blokkoló, tisztázatlan publikus adatveszély.

## P1 — Új repository / szervezet

- Új Jarvis-2.0 repo, főág, elkülönített docs és integrációs ág.
- Protected main kezelési szabály, még ha GitHub branch-protection tényleges admin-beállítása nincs is ellenőrizve.
- Ágak felelősök szerint; az ág nem egyenlő build státusszal.
- Source manifest és dokumentációs index, jelenlegi forrás SHA.
- Gate: repo létezik és célzott ágon tartalom visszaolvasható.

## P2 — PyGPT + kiválasztott Add-ons

- PyGPT submodule/reprodukálható checkout; Windows támogatott Python.
- PyGPT GUI indul, alap chat teszt.
- Add-ons katalógus hash és telepítő ellenőrzése; minimum egy Skill és egy egyszerű MCP valódi lekérdezése.
- Meglévő 39 funkcionális plugin és 16 tool baseline felmérése; semmi ne tűnjön el rejtetten.
- A 30 MCP és 37 Skill bejegyzést kategorizálni: CORE, ON_DEMAND, PARKED.
- Külső kulcsot, Docker/Node binárist és telepítő-hozzáférést igénylő komponens BLOCKED_FOR_CONFIG státuszt kapjon, ne FAIL-t és ne PASS-t.
- Gate: PyGPT indul, plugin/Skill/MCP csatorna tesztből hívható, naplózás; eredeti PyGPT funkciók regressziós smoke-okkal vizsgálva.

## P3 — Free Claude Code / ai_proxy_2

- Az integráció csak átvizsgált, publikálható forrásból és külön folyamatban indul.
- Python 3.14.7 elkülönített env és pinelt FCC baseline.
- /v1/messages, /v1/responses, SSE streaming, tool calls, /v1/messages/count_tokens.
- Model catalog, code session kezelés, cancel, quota/rate/fallback.
- Központi jogosultságszolgáltatás, localhost auth, audit.
- Nem támogatott multimodális útvonalat natív PyGPT adapterre terelünk, nem vesszük el.
- Gate: kérések/hiba/fallback tool+SSE teszt és egy izolált coding feladat teljes végrehajtása.

## P4 — Házasítás és stabilizálás

- P2/P3 közös feladatorkesztrációja, nincs körbe-delegálás vagy versengő session tulajdon.
- Idempotens retry, cancel/timeout, partial failure, stale response, kill child.
- Emlékezet, modellezés, MCP és file/tool audit.
- Visszaállítási teszt, snapshot; Windows end-to-end próba.
- Gate: feladatok PASS/FAIL evidenciákkal, nincs kritikus nyitott regresszió.

## P5 — JARVIS/Brahma GUI port

- A mag stabil működése után GUI-forrás kiemelése.
- PyQt6→PySide6 port képességenként, nem széles körű vak importcsere.
- Original look, animation, color, timing, hitbox, window/transparency, microfon/event loop.
- Screenshot/video/frame összehasonlítás, keyboard/accessibility smoke.
- Szükséges PyGPT backend képességek elérhetőek UI-ból, opcionális PyGPT expert GUI preserved.
- Gate: vizuális/funkcionális paritás igazolva; eredeti HUD nem változik önkényesen.

## P6 — JARVIS specifikus extrák / evolution

- Magyar JARVIS hang (TTS/STT jogosultság + mért minőség + interrupt).
- PhotoCraft, LightCraft, FilmCraft, FreeCAD külön adapterek, teljes lehetőség-regiszter.
- REA, VoiceStudio, IronRAG, Barehands csak külön bizonyított haszon után.
- Release/update/rollback, diagnosztika, Windows csomagolás csak amikor kész.
- Gate: integrációs regressziók, licenc-/adat- és hardware audit, átvételi tesztek.

## Állapotjelentés szerkezete

| Mező | Értelmezés |
|---|---|
| Phase | P0–P6 |
| Scope | pontos modul/fájl/branch |
| Baseline SHA | induló referencia |
| Head SHA | elkészült ágvég |
| Feature inventory | expected / implemented / tested / blocked |
| Evidence | parancs, exit code, log, hash, screenshot |
| Regression | korábban elfogadott tesztek |
| Remaining risk | P0 / P1 / P2 severity |
| Gate | NOT_RUN / PASS / FAIL / BLOCKED |
| Next owner | következő feladatgazda |

Ne szerepeljen kész százalék egyenértékű tesztlefedettségként, ha a nevező (elfogadási feltételek száma) nincs meghatározva.
