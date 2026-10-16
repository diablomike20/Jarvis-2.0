# 10 — Kutatási tartalék és opcionális technológiák

**Alapelv:** új GitHub-felfedezés automatikusan R&D/PARKED. Nem módosíthat P2/P3/P4 végrehajtási sorrendet külön döntés és elfogadási kísérlet nélkül.

## Követendő jelölések

CORE_SOURCE = jelenlegi stratégiai motor; HIGH_VALUE_CANDIDATE = nagy potenciál, még nincs integrálva; R&D_REFERENCE = kutatási dokumentum; PARKED = későbbi vizsgálat; REJECT_FOR_NOW = nem érdemes új futó motorként.

| Forrás | Mire való | Várható plusz JARVIS-ban | Ajánlott státusz |
|---|---|---|---|
| morluto/rea | MCP/CLI visszafejtés, bináris, firmware, Electron, web, rekonstruálás, evidence | P0/P5 technikai megfelelés és inverse-analysis | HIGH_VALUE_CANDIDATE |
| debpalash/VoiceStudio | helyi STT/TTS/voice cloning, OpenAI compat API, stream/MCP | magyar hang P6 | HIGH_VALUE_CANDIDATE / PARKED |
| mlimarenko/IronRAG | Rust, PostgreSQL/pgvector, tudásgráf, 23 MCP | nagy projekt dokumentum-RAG, bizonyíték | HIGH_VALUE_CANDIDATE / PARKED |
| bytedance/deer-flow | LangGraph agent platform, sandbox, memory, session goals | advanced orchestration referenciamodell | R&D_REFERENCE; ne duplikálja PyGPT planner |
| obra/superpowers | AI fejlesztési folyamatok, 15 Skill | tudományosabb proof/plan/test discipline | R&D_REFERENCE / válogatott módszertan |
| AlphaSaleAidan/opus-5-5-x-gpt-skill-tree | Skill/engine router, 348 hirdetett elem | capability-selection és agent munkamegosztás | R&D_REFERENCE, nem globális installer |
| x1xhlol/system-prompts-and-models-of-ai-tools | prompt/tool spec-gyűjtemény | összehasonlító design | R&D_REFERENCE, forrás-hitelesség kérdés |
| asgeirtj/system_prompts_leaks | nagy promptarchívum | kutatás, tool contract tervezés | R&D_REFERENCE, forrás-hitelesség kérdés |
| BeatAPI/awesome-3d-prompts | 3D prompt/case-könyvtár | Blender/FreeCAD benchmark ötletek | PARKED |
| zlxxlz1026/awesome-gpt-6-astra-casebook | modell/ügynök esettanulmányok | model eval feladatok | PARKED |
| Anil-matcha/awesome-gpt-6-astra | workflow/model API példák | provider capability eval | PARKED |
| jaredrhod/fullstack-agent | Claude Code memória/hang/face/hands wizard | UX-minták, nem core agent motor | PARKED |
| jaredrhod/ai-memory-vault | Obsidian Markdown személyes memória | personal context, napi jegyzetek | PARKED — IronRAG nem helyettesíti |
| jaredrhod/backtalk | local Whisper/Kokoro, voice approval, interrupt | streaming és approval minták | PARKED |
| jaredrhod/ai-visualizer | Canvas/JS state bus és 4 arc | animációs protokoll; eredeti HUD marad | PARKED |
| jaredrhod/barehands | MediaPipe+Three.js kamera/gesztus/3D board | térbeli JARVIS HUD opcionális extra | HIGH_VALUE_CANDIDATE / P6 |

## REA — külön megfigyelések

- Nagy eszközrendszer MCP és CLI felülettel, külső analyzerekkel (pl. Ghidra, Hopper, IDA, JADX, Binwalk).
- Evidence, complete/unknown/truncated státuszok, Reconstruction Obligation Ledger és readiness tesztrendszer.
- Nem általános automatikus PyQt6→PySide6 fordító.
- Ismeretlen bináris elemzése csak izolált környezetben és jogosult forrásból.
- P0/P5-nél célzott, mérhető haszon; kezdetben nincs kötelező REA szolgáltatás.

## VoiceStudio — külön megfigyelések

- OmniVoice nyelvi katalógusában Hungarian/hu/hun szerepel.
- API és streaming integrációs pont jobb, mint a teljes Electron GUI átvétele.
- Magyar hangminőség, latencia, GPU/memória, modell/licenc és voice-rights külön próba.
- A csomag egyes többnyelvűnek mondott motorjai nem támogatják a magyart (pl. IndexTTS 2.5 dokumentált öt nyelvű listája).
- A hangprojektről személyes nyers mintát a publikus repo nem tartalmaz.

## IronRAG — külön megfigyelések

- Typed knowledge graph, vector/lexical/technical retrieval, bizonyíték chunkok, MCP, Rust és Docker stack.
- 8 provider katalógus, 23 MCP-eszköz, 15 nyelvű code-aware ingest a dokumentáció szerint.
- Normál kapacitásterv kb. 16 GiB RAM körüli hostot jelöl; mérés szükséges.
- PyGPT beszélgetésmemóriáját ne cseréljük le bizonyítás nélkül; lehet külön technikai corpus owner.

## Fullstack Agent — külön megfigyelések

- Memory Vault: Claude/Obsidian Markdown memória, nem azonos IronRAG-rel.
- Backtalk: Claude Agent SDK-val erősen összekötött, PyGPT-be nem vihető át egyszerűen.
- AI Visualizer: localhost Python + JS, .voice_state/.voice_waveform állapotbusz, megváltoztatható agnosztikus adapterrel.
- Barehands: localhost /cmd és /state, kamera MediaPipe+Three.js, alternatív 3D UI; jelenlegi GUI redesignnak NEM jelölt.
- Wizard meglevő fájlokat mozgat/több repo-t klónoz, ezért globális installer futtatás nélkül review.

## Piacérzékeny és licencfüggő elemek

No auto install; licencek, végpontok, modellek és terjesztési feltételek friss ellenőrzése minden aktiválás előtt. README kimeneti teljesítmény állítás nem felhasználói PASS.

## Mérési javaslat

REA: 5 ismert jó kód/működés ellenőrzési feladat vs manual baseline.
VoiceStudio: WER/STT, természetesség, latency p50/p95, VRAM, magyar kiejtés.
IronRAG: Recall@K, citation correctness, chunk relevancia, RAM/CPU, import/restart.
DeerFlow: többlépéses feladatteljesítés PyGPT Agents V2-vel szemben, ütközésmentesen.
Barehands: gesture precision, false positives, CPU/GPU, Windows kamera permission.
