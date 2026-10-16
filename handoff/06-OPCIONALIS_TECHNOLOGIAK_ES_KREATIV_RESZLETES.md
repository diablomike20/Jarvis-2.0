# 06 — Kiegészítők, alternatív keretrendszerek és prioritás (P6 / R&D)

Az összes kutatási jelölt külön szerepel `docs/10-research-backlog.md`, `docs/10a-heyputer-everything.md`, `docs/16c-creative-rnd-heyputer-roadmap.md` és `catalog/research-reference-lock.v1.json` fájlban. Egyik sem aktív a P2/P3 backendben pusztán attól, hogy tanulmányoztuk.

## Az operációs rendszer és mérnöki modulok
- **FreeCAD:** Python/CAD parametrikus sketch, shape, constraint, 3D model, STEP/STL; Windows FreeCAD környezet/GUI-hívás és sandbox jóváhagyás; változtatás soha approval nélkül.
- **PhotoCraft:** rétegzett képmanipuláció, PSD/PSB, mask, filters, GPU engine; Rust MCP/API-kat auditálni, natív project mentés és roundtrip.
- **LightCraft:** RAW, photo collection, non-destructive tone/color/masks; PhotoCraft-tal nem kell fizikailag összevonni, hanem közös JARVIS tool-választás.
- **FilmCraft:** Rust-alapú NLE timeline, klip/effekt, audio, cím/felirat, export; nem összekeverendő generatív video modellel.
- **Blender MCP:** külön server Blenderben, 3D jelenetparaméterek, mesh/material/render; verzió/permissions/asset license külön.

## REA — Reverse Engineer Anything
morluto/rea MIT, Node/MCP/CLI, 4025 Git forrásfájl korábbi vizsgálatban. Cél: bizonyítékokra épülő statikus/dinamikus app/binary/firmware vizsgálat és rekonstrukciós kötelezettségkövetés. `complete/unknown/truncated` állapotok és `Reconstruction Obligation Ledger` értékesek. Nem automatikus PyQt6→PySide6 konverter és nem korlátlan zárt program visszamásoló rendszer. Sandbox és jogosultság előfeltétel.

## DeerFlow
bytedance/deer-flow LangGraph ügynök-orkestráció, sandbox, DeerMem, subagents, scheduled tasks, project memory. **Ne tegyük második központi orchestratornak PyGPT mellett**. Benchmark/minták P0/P4.

## Superpowers + nagy Skill Tree
obra/superpowers 15 skills; PyGPT_Addons 37 között 13 Superpowers névegyezés. AlphaSaleAidan nagy csomag 348 hirdetett Skill, de csak 214 közvetlen SKILL.md azonosítva adott Git-fában, 132 külső. `install.sh` törölhet és felülírhat globális Skill mappákat. Tanulság: Skill resolver + capability routing + izolált Skill install + version pin.

## Memory Vault, IronRAG és PyGPT
- **Memory Vault:** Obsidian/Markdown priming, profile/jobs/daily logs/boot config, adatok szerkeszthetősége, tervezett personal knowledge.
- **IronRAG:** Rust PostgreSQL/pgvector/Redis, 23 MCP, graph + vector + lexical + code-aware 15 language, bizonyítékok. Infrastrukturális erőforrásigény és licencek külön.
- **PyGPT RAG:** elsődleges meglevő memória/index; a másik kettő nem automatizált konzisztens tri-memória stack. Ownership, per-user ACL, source revision alapvető.
A felhasználó kifejezetten kérte: a VoiceStudio és IronRAG **tartalékban maradjanak**, mert később még szükségesek lehetnek.

## VoiceStudio és hangprofil
AGPL-3.0, Python API+Electron. Beszéd output/openai compat routes, streaming, voice conversion, több TTS. Magyar `hu/hun` dokumentált az OmniVoice nyelvi listában, de a kiválasztott beszélő felismerése/hangminősége/szabályozás runtime teszt.
Korábbi hangkutatásban XTTS-v2 és F5-TTS Hungarian jelölt, egyes modellek nem kereskedelmi license-szel; hangadatok nem kerülnek public repo-ba. Specifikus színészi hang felhasználásának pontos engedélye nem bizonyított a repo szintjén.

## Fullstack Agent összes almodulja
jaredrhod/fullstack-agent (AGPL) négy modulból áll: ai-memory-vault (Markdown memory), backtalk (Claude Agent SDK audio, local Whisper+Kokoro, pause, approval), ai-visualizer (4 böngészős animáció és `.voice_state`/`.voice_waveform` state bus), barehands (MediaPipe + Three.js, kamera, /cmd endpoint, kézmozdulatos 3D board). Barehands P6 HIGH VALUE, de eredeti HUD csere nem.
Jelentős security: `bypassPermissions` nem elfogadható, localhost HTTP endpoint külön auth, AI HTML/gesture véletlen command ellenőrzés.

## HeyPuter/everything
51 ellenőrzött `src/` alkalmazáskönyvtár 2026-10-16 Git fában, köztük `3d`, `parametric`, `cad`, `photo-studio`, `video-studio`, `audio-studio`, `music-studio`, `api-client`, `circuits`, Office/CRM/project utility-k. Gyakran külön Vite/WebAssembly/JS és Puter cloud login. Parametric early-alpha OpenCascade/WASM sketch/STEP/STL lehetőség; nem bizonyított FreeCAD gyártásparitás. P6 tartalék.

## Prompt- és benchmarkgyűjtemények
x1xhlol/system-prompts-and-models-of-ai-tools; asgeirtj/system_prompts_leaks; BeatAPI/awesome-3d-prompts; zlxxlz1026/awesome-gpt-6-astra-casebook; Anil-matcha/awesome-gpt-6-astra — lehet tesztötlet és rendszertervezési referencia, de kétes eredetű promptokat nem emelünk át saját system instrukciónak, és casebook nem működő core komponens.

## gods-eye-view
Külön `03` audit: 3D geospatial MCP/UI integráció P6, nem átépített JARVIS HoloGlobe. A kód MIT, 3rd party dataset feltételek külön. Node >=24.14 (vagy 26), Cesium, Vite, voice AI, track, weather, camera, share scene.

## Mérés alapján engedélyezhető áthelyezés R&D-ből
Projekt prioritását egy *mérhető* hiány (feature GAP, P95 latency, user need) indokolja. Ha van átfedés az eredeti PyGPT engine-nel, benchmark kell. Csak sikeres architektúra, licenc, security, dependency és regression review után aktiválunk.
