# 07 — Korábbi fejlesztési bizonyítékok, GitHub Actions futások, időrendi állapot

**Figyelem:** a korábbi chatben kapott futási beszámolók nem jelentenek automatikus újraellenőrzött eredményt. Két forrásszint:
**REPORTED_PRIOR_SESSION** — előző beszélgetésben szerepelt; az adott artifact jelenleg nincs újrafuttatva.
**VERIFIED_GITHUB_METADATA** — GitHub branch és repository jelenlegi státusza ténylegesen visszaolvasva.
A korábbi információt úgy őrizzük, hogy későbbi fejlesztő megtalálja, de ne jelölje fals PASS-nak.

## Chronológia

### 2026-10-09 — JARVIS-tól várva
Eredeti JARVIS/Brahma átnevezés és teljes magyar voice; Gemini kötelező függőség kiváltása; PhotoCraft/LightCraft/FilmCraft teljes integráció egy telepítőben, FreeCAD a modulrendszerhez; felhasználó saját használatra szánta.

### 2026-10-09 — JARVIS Universal Source Plugins
Korábbi jelentés szerint PR #4 Universal Source Plugins `manifest.json`, source adapterek, MCP eszközfelderítés, engedélyezéses futtatás: CI és unit ellenőrzés sikeres. Windows integráció és main-beolvasztás nincs bizonyítva az átadásban. Ez egy korábbi JARVIS fejlesztési kezdeményezés, nem az új Project Icarus P2 automatikusan kész része.

### 2026-10-10 — Windows build és telepítő problémák
Korábbi Windows-telepítő futások `google.generativeai` függőségi hibával küzdöttek. A legutóbbi smoke teszt szerint hiányzott `dist\BrahmaEvo\_internal\TTS\vocoder\configs`; exit code 23 és a felhasználói utasítás: **„Do not publish setup.”** Ezt a hibát külön regressziós tesztben őrizni kell.

### 2026-10-11 — Claude Code CLI ág és WinCI
Korábbi jelentés: `feature/jarvis-claude-full-runtime-20261011` és `delivery/jarvis-ai-complete-2026-10-10`; Actions #38014964958, #38152054654. Python syntax/MCP JSON-RPC, Claude CLI 2.1.88 és Windows helper tesztek némelyike sikeresnek lett jelentve. Valódi paid/provider/model + end-to-end GUI+voice tartós siker külön igazolandó.
Komponensek: main.py, agent/executor.py, actions/claude_code_bridge.py, core/claude_runtime.py, Node CLI stream-json + stdio permission prompt, BrahmaMcp.exe / PyAutoGUI / Qt approval. Ne írjuk felül.

### 2026-10-12 — izolált bridge / hangkutatás
Előző beszámoló szerint egy korábbi két-repo integráció 11/11 ellenőrzésen és CI-n ment át, commit jelöltek `87c8935`, `d89181c`, futások #38196097519/#38196256081; további hat Claude feature-csoport csak részleges volt. Pontos SHA/ág újraellenőrzésig REPORTED_PRIOR_SESSION.

Hangprojekt: korábbi Videa Vasember 3 promó 55 sec, két WAV vágás 1.36 sec és 0.88 sec (összesen 2.24 s); magyar STT és jelenetjelölés, a konkrét hang előadó azonossága **nem** bizonyított. Ebből nem áll rendelkezésre teljes magyar hangadatbázis, nem része a nyilvános JARVIS repo-nak.

### 2026-10-16 — Project Icarus forrás- és dokumentációmigráció
- Target repo `diablomike20/Jarvis-2.0`, main README only, base `38d6991faf52eb1c2348773b702a9fb44db6f470`.
- `integration/pygpt-addons-baseline` (HEAD 074b2efb8c4a73aee8d55d8b6bc56a2e69df211c), Git submodules PyGPT @2d8779a... és Addons @15759ba...
- `sources/pinned-project-baseline` (HEAD 1da31bdd7850665d963906dfc8a4d97b2788e94d) hét nyilvános Git-submodule, köztük eredeti JARVIS és 3 Craft.
- `docs/master-spec-20261016` (2026-10-16 olvasott HEAD 935016895c814131e42022e021a034638d3fd603) 00–16c docs, 65 fő feature target, 50 actions, 51 HeyPuter app, feature registry.
- `docs/gods-eye-view-feature-expansion-20261016` párhuzamos dokumentációs branch, ne overwrite.
- `docs/final-handoff-20261016` új önálló dokumentációs / export ág, rögzített kiindulásból.

### 2026-10-16 — Free-Claude-AI és God's Eye View új bejegyzések
A user saját privát `Free-Claude-AI` forrásában Puter.js login hibaminta: file:// és auth-probe. God's Eye View public fork Cesium/MCP a későbbi geo modulhoz. Lásd 03–05.

## Kötelező következtetés
Az előző GitHub Actions zöld állapot sem helyettesíti a Windows EXE, a teljes modell/eszköz, a hang, a GUI és a stabil task workflow e2e tesztjeit. A régi `feature/` ágak tartalmát új kolléga csak read-only, SHA alapon vizsgálhatja a párhuzamos másik agent tulajdonjogának megsértése nélkül.

## Javasolt visszaellenőrzési checklist
- GitHub Actions run és artifact expiry, CI logok; említett commit SHA/ág relevanciája.
- JARVIS/main és Claude branch összehasonlítás (files/CI); nincs véletlen kész állapot öröklés.
- Az eredeti core mind az 50 action számára smoke test/negative test, indító és build.
- A telepítőből hiányzó `TTS/vocoder/configs` kontrollált regresszió.
- Az új PyGPT+FCC ma nem ugyanaz a régi JARVIS Claude branch; nincs automatikus merge.
