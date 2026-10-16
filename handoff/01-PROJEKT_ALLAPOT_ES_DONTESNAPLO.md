# 01 — Projekt jelenlegi állapota, döntések és őrzendő korlátok

## Identitás
Project Icarus / Jarvis-2.0 / JARVIS UNIFIED. Központi publikus GitHub: https://github.com/diablomike20/Jarvis-2.0. Eredeti forrás: https://github.com/diablomike20/Jarvis-Ai. Nem azonos a korábbi Brahma/Orb felületi kísérletekkel; az eredeti, a felhasználónak tetsző HUD megőrzendő.

## Felhasználó kifejezetten elfogadott stratégiája
1. Központi repository, sok külön fejlesztői branch rendben van.
2. PyGPT legyen az első technikai gerinc, eredeti funkcióit megtartjuk.
3. Ehhez a saját PyGPT_Addons katalógus ellenőrzött MCP/Skills/Add-on integrációja.
4. Később a Free Claude Code / `ai_proxy_2` gateway, kiválasztott coding agentek és model routing.
5. A GUI átültetésével TILOS kezdeni; PyGPT + FCC backend P4 stabilizálás után PyQt6 → PySide6 HUD port P5.
6. Creative/audio/FreeCAD/3D/RE/camera/extra funkciók csak a stabil mag után (P6), kivéve kicsi izolált megvalósíthatósági próbák.
7. Egyszeri teljes személyes Windows-telepítés a végén, nem külön letöltendő Craft motorok felhasználói oldalról; terjesztésnél licenc/hardver/binary size tradeoff külön.
8. A jelenlegi HUD vizuális élményét nem dobjuk el. Nincs új Orb, nem csinálunk párhuzamos GUI-t a felhasználó által elfogadott jelenlegi helyett.
9. Gemini eltávolításának eredeti célja megőrzendő, de a PyGPT Google provider megléte önmagában nem ugyanaz, mint a korábbi Brahma kötelező Gemini runtime. A részletes cél: ne legyen egyetlen providerhez láncolva.
10. Más fejlesztő által szerkesztett repo/branch nem módosítható ellenőrizetlenül.

## Rögzített műszaki tények
- PyGPT PySide6/Qt, Python >=3.10,<3.14; JARVIS PyQt6. Az upstream FCC legutóbb ellenőrzött új vonala Python 3.14.7. Ez külön folyamatokat igényel.
- PyGPT core nem teljesen headless; core/window/controller függőség. P4–P5 adaptert bizonyítani kell.
- PyGPT 40 plugin mappa (39 funkcionális + base), 16 app tool, 18 LLM adapter, 30 loader, 7 STT, 6 TTS.
- PyGPT_Addons 2 Add-on + 30 MCP + 37 Skills + 11 tutorial.
- FCC új upstream ~61 provider-konfigurációs bejegyzés és 11 coding harness/kliens.
- Jarvis-Ai forrás actions/ mappában 50 ellenőrzött modul, kódmegjelenés nem feltétlen teljes funkcionális bizonyíték.
- HeyPuter/everything 51 közvetlen src alkalmazásmappa; P6 kutatási tartalék.
- God's Eye View külön geospatial UI/MCP jelölt, P6 kutatás, eredeti JARVIS globe-ot nem cseréljük le automatikusan.
- A `Free-Claude-AI` privát forrás, Puter.js browser UI; nem azonos FCC ai_proxy_2 gateway-jel; bejelentkezési hiba külön audit.

## Dokumentációs ágak a projektben
- `main`: kiinduló állapot, változatlan, egy README.
- `docs/master-spec-20261016`: korábbi 00–16c műszaki specifikáció és gépi katalógus.
- `docs/gods-eye-view-feature-expansion-20261016`: már létező kísérleti dokumentációs ág (másik párhuzamos munkamenet); ne írjuk felül.
- `integration/pygpt-addons-baseline`: PyGPT + Add-ons SHA-pinelt gitlink.
- `sources/pinned-project-baseline`: hét publikus forrás submodule.
- `docs/final-handoff-20261016`: ez a csomag, a `docs/master-spec` adott HEAD-jéből elágazva.

## Mit tudunk bizonyítani és mi még hiányzik
GitHub create-branch/commit/tag nélküli forrás-linkek és doc feltöltés megtörtént; a Pinelt PyGPT és Addons Git submodule referenciák rögzítve vannak. Nem igazolt: rekurzív checkout egy tiszta Windows gépen, PyGPT boot és addon működés, FCC processzen át tool/function/sse, JARVIS natív PySide6 GUI, valódi magyar hang, teljes Craft egytelepítős végleges csomag.

## Kritikus múltbeli tapasztalat: build ≠ kész Windows termék
Korábbi JARVIS Windows telepítő munkamenetek hibája: `google.generativeai` import és `TTS/vocoder/configs` csomagolási hiány; utóbbi korábbi smoke teszt exit=23. Ezt nem szabad kijavítottnak állítani pusztán új GitHub Actions siker alapján. A CI commit- és logtörténetet a következő dokumentum részletezi.

## Mi a következő, mérhető fejlesztői belépő?
P0: reprodukálható repo checkout/submodules + Windows dependency lock, source/secret scan és auditable GUI inventory. P1: main védelmi policy/ruleset ellenőrzése. P2: PyGPT natív indulás, 1 Skill, 1 MCP, 1 Extension valós hívással. P3: kiválasztott FCC service és adapter csak engedélyezett, izolált alapból.

## Működési és kommunikációs etikett
Nincs „elkészült” a semmiből; nincs valós helyettesítése dummy adatnak; nincs önkényes release. A felhasználó nem akar újra és újra betanítani új chatet. A dokumentáció és a machine-readable task registry a projekt közös emlékezete.
