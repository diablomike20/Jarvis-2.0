# 02 — JARVIS 2.0 funkciók rendszertérképe és részletes elvárások

A *kötelező* funkciócélok 65 ID-s master leírása: `docs/16-jarvis20-complete-feature-specification.md`. Az 50 eredeti action fájl és integrációs követelményei: `docs/16a`; PyGPT/FCC/Addons részletek: `docs/16b`; kreatív/CAD: `docs/16c`. Ez a dokumentum az alrendszerek használható végtermék-viselkedését és a különálló tesztkövetelményt rögzíti.

## A. Felhasználói élmény és operációs shell
- Eredeti futurisztikus Brahma/JARVIS PyQt6 HUD 1:1, erőforrások/animációk/függőségek/adaptív layout.
- Eredeti 3D HoloGlobe, környezeti nézet, külön interakciós sávok; nincs új kényszerű orb.
- Hang/figyelem állapotszínek, valódi FFT és jelérték, idle/listening/capturing/thinking/tool_running/speaking/error/muted.
- Kártyás feladatlépések, áttekinthető műveleti naplók; nincs belső, nem hozzáférhető modellgondolat mutatása.
- Settings képernyő modellekhez, credential hivatkozásokhoz, pluginokhoz, permission policyhoz, STT/TTS eszközökhöz.
- Ablak pozíció/hotkey/multi monitor/HiDPI/Qt WebEngine/shell, crash recovery.
**Elfogadás:** determinisztikus kép- és state diff, interakciók, menüfeladatok, hosszú futások, Qt thread leállítás és Windows tesztek.

## B. Beszélgetés és kognitív folyamat
- Magyar beszélgetés, angol és többnyelvű bemenetek; a nyelv megőrzése modellváltás után is.
- Több beszélgetés, profile, context compaction, file/image attachments, história és session recovery.
- Chat; Completion; Agents Chat; Orchestrator; Swarm; Experts; Custom Agent; Autonomous Mode; Research; Realtime; Computer Use.
- Többügynökös task-plan, tool request, human approval, trace, retry és cancellation.
- Személyre szóló, de nem kontroll nélkül írható személyiségbeállítás, engedélyezési csatorna.
**Elfogadás:** egyetlen task owner; önhivatkozó delegálás nem keletkezik; prompt injection és hibás provider esetén fail-closed.

## C. AI modellökoszisztéma
- PyGPT natív adapter-családok érintetlenül; 18 provider kódkönyvtár.
- FCC 61 provider katalógus és 11 coding kliens, nem 61 korlátlan ingyenes modell.
- Forrás-/verziószintű capability discovery: text, tool calling, structured output, streaming, reasoning, image, audio, video, code, token budget.
- Szabályozható lokális/vállalati/cloud model routing, cost cap, privacy boundary, auto fallback.
- Offline vagy nincs credential: csak a ténylegesen támogatott helyi modellek; nincs hamis „mindig ingyen Claude”.
**Elfogadás:** model list, request/stream/tool, usage/cost, timeout/rate-limit, provider protocol errors, unsupported capability native passthrough.

## D. Eszköztár és kapcsolódások
- Megőrzött PyGPT 40 plugin könyvtár, 16 natív tool.
- MCP 30 ismert konfiguráció, Skills 37 bejegyzés, 2 demo Add-on és 11 minta; mindegyikhez kiválasztás/installer/eng. teszt.
- Windows desktop, egér/keyboard, terminál, fájlok, böngésző, naptár, e-mail, Github, Google, chat, knowledge, kép, audio/video.
- Saját eredeti 50 actions modul (külön ID és ellenőrzési tétel), már létező `claude_code_bridge.py` nem írható felül automatikusan.
- Minden pluginban capability meta, caller auth, tool sandbox, argumentum validáció, side effects, audit és timeout.
**Elfogadás:** legalább egy valós read-only MCP, egy Skill és egy trusted demo plugin használata; kritikus parancs negatív approval teszt.

## E. Memória, hosszú távú tudás, projektadat
- PyGPT convo/history/RAG index, 30 loader, 8 vector tároló adapter.
- Világos role: felhasználói/csevegési memória, projekt dokumentum-korpusz, agent session scratch.
- Memory Vault (Markdown) és IronRAG (tudásgráf) a jelenlegi központi rendszerben PARKED, nem telepített.
- Projektről jelenlegi log, ADR, forráshivatkozás, feature ID és hiteles tesztállapot mind ellenőrizhető.
- Dokumentum törlés, indexverzió és ACL, megismételhető restore, nem összevissza automatikus memória-szinkron.
**Elfogadás:** 2 munkaterület adatizolációja, visszakereshetőség, adatfrissítés, törlés/restore, exact citation.

## F. Magyar és egyedi hang
- Bemenet: PyGPT 7 STT adapter, helyi Whisper alternatíva, audio device, push-to-talk, későbbi ébresztőszó.
- Kimenet: PyGPT 6 TTS adapter és később saját magyar JARVIS-hang/adaptált VoiceStudio vagy F5-TTS motor.
- Beszédmodell emberi hangjának engedélyezése/szerzői jog eltérhet a filmhangsávhoz kapott jogtól; nyers hang soha public repo.
- Streaming, barge-in, voice state, p50/p95 késleltetés, normalizált hangerő, fallback.
**Elfogadás:** magyar mondatkészlet, fonetikai tesztek, felismerési hibák, megszakítási latency, hardverprofil és license audit.

## G. Kreatív és mérnöki műhely
- PhotoCraft: réteg, maszk, PSD, beállítások, export, undo/redo, agent tool bridge.
- LightCraft: RAW fotóelőhívás, nem destruktív color/tone, preset, katalogizálás.
- FilmCraft: videós timeline, klip vágás/effekt/felirat/hang/export; nem azonos szövegből videót generáló modellel.
- FreeCAD: paraméteres sketches, constraints, 3D CAD, assembly/export STEP/STL és visszaolvasás.
- Blender MCP, HeyPuter 3D/Parametric/CAD/Photo/Video Studio külön R&D, nem automatikus P6 aktiválás.
**Elfogadás:** menthető natív projekt, byte-szintű export roundtrip, unit konverzió, fájljogosultság, render/cancel és crash recovery.

## H. Fejlesztői labor, monitoring és önfejlesztés
- Kód segéd/fejlesztőügynök: izolált Git worktree, TDD, unit/integration, review és csak jóváhagyott commit.
- Self-heal engine: read-only diagnózis → javasolt patch → diff → approval → kontrollált test → rollback; nincs titkos főágmódosítás.
- REA (bináris/firmware/app evidence) forráskutatás és P6 külön MCP, nem automatikus teljes dekompilálás.
- Runtime health, rate limit, diag log, telemetry opt-in, alerts, backup restore.
**Elfogadás:** no-op, failure injected, tool cancel, diff, security rollback, provenance.

## I. Geospatial és helyzetkép — új opció
- Eredeti HoloGlobe védett, God's Eye View átemelési döntés később.
- Globe/tiles/aircraft/ships/satellites/earthquakes/weather/radar/fires, public cameras, analyst voice, geospatial MCP.
- Friss adat és demonstráció/szimuláció külön címkézendő; privacy/dataset és API termék feltételek külön.
**Elfogadás:** állapot és provenance, fallback, snapshot/recording, adatfrissítési timestamp, offline és kulcs nélküli degradáció.

## Kötelező mérési fegyelem
Személyes/privát adat nem használható public acceptance fixture-ként. A történetben szereplő korábbi CI siker **nem** egyenlő a tervezett unified app végtermék működésével. Egyetlen funkció sem maradhat rejtett GAP nélkül.
