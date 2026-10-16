# 16b — PyGPT / Free Claude Code / PyGPT_Addons — teljes capability-összefésülési mátrix

**Kapcsolódó dokumentumok:** [Master funkcióspec](16-jarvis20-complete-feature-specification.md), [PyGPT név szerinti leltár](04-pygpt-inventory.md), [Add-ons katalógus](05-addons-inventory.md), [FCC providerlista](06-fcc-inventory.md), [IPC/API contract](08-api-event-contracts.md).

Ez az integrációs munkaszerződés a védett PyGPT-funkciók, az FCC hozzáadott értéke és az egységes felületi viselkedés között. SOURCE_VERIFIED = az adott nevű modul/adaptersor létezik; USER_VISIBLE_DONE = csak futó GUI+API bizonyítás után.

## 1. PyGPT eredeti 40 plugin könyvtárának funkciótérképe

| ID | PyGPT plugin | Értelmezett funkcióterület | Integrációs követelmény |
|---|---|---|---|
| PY-PLUG-001 | `agent` | Agent plugin / orchestration | Feladat és worker kapcsolódási pont; Agents V2-vel kapcsolat auditálandó |
| PY-PLUG-002 | `audio_input` | Hangbemenet | Mikrofon/STT plugin UI és a provider adapterek közötti kapcsolat |
| PY-PLUG-003 | `audio_output` | Hangkimenet | Szintézis, beszédvezérlés, lejátszó és UI események |
| PY-PLUG-004 | `base` | Plugin keretrendszer | Közös API, lifecycle, metadata; nem külön business feature |
| PY-PLUG-005 | `bitbucket` | Bitbucket | Repo/fejlesztői rendszer, credential igénnyel |
| PY-PLUG-006 | `canvas_web` | HTML Canvas | Interaktív HTML-kimenet, render és sandbox |
| PY-PLUG-007 | `cmd_api` | API parancsok | Validált külső HTTP/API műveletek |
| PY-PLUG-008 | `cmd_code_interpreter` | Kódfuttató parancsok | Python/egyéb kód sandboxban |
| PY-PLUG-009 | `cmd_custom` | Egyedi parancsok | Felhasználói eszközregiszter |
| PY-PLUG-010 | `cmd_files` | Fájl parancsok | Olvasás, írás, attribútum; scope |
| PY-PLUG-011 | `cmd_history` | History parancsok | Beszélgetés visszakeresése |
| PY-PLUG-012 | `cmd_mouse_control` | Egérműveletek | OS mouse interakció jóváhagyással |
| PY-PLUG-013 | `cmd_serial` | Soros port | Hardverkapcsolat, eszközbiztonság |
| PY-PLUG-014 | `cmd_system` | OS parancs | Shell/Process műveletek korlátozottan |
| PY-PLUG-015 | `cmd_web` | Web parancsok | Keresés/letöltés/navigáció forrásellenőrzéssel |
| PY-PLUG-016 | `crontab` | Ütemezés | Ismétlődő munka, cron/timer |
| PY-PLUG-017 | `experts` | Szakértők | Szakértői prompt/agent feladatmegosztás |
| PY-PLUG-018 | `extra_prompt` | Prompt-kiegészítők | Feladatprofil és szöveges kontextus |
| PY-PLUG-019 | `facebook` | Facebook-integráció | Külső közösségi API |
| PY-PLUG-020 | `filesystem` | Fájlrendszer | Érzékeny műveletek, access policy |
| PY-PLUG-021 | `github` | GitHub | Repo, issue, PR, actions, csak szűk scope |
| PY-PLUG-022 | `google` | Google | Kapcsolódó szolgáltatások és OAuth |
| PY-PLUG-023 | `idx_llama_index` | LlamaIndex/RAG | Index, retriever, embedding |
| PY-PLUG-024 | `jev` | JEV | Speciális szolgáltató; dokumentáció/API ellenőrzendő |
| PY-PLUG-025 | `mailer` | Mail | Küldés/fogadás; külső műveleti approval |
| PY-PLUG-026 | `mcp` | Model Context Protocol | Külső tool registry, MCP transport |
| PY-PLUG-027 | `memory` | Memória | Conversation és retrieval |
| PY-PLUG-028 | `openai_dalle` | Képgenerálás | DALL-E kompatibilis szolgáltató |
| PY-PLUG-029 | `openai_vision` | Vision | Képek elemzése multimodális modellekkel |
| PY-PLUG-030 | `osm` | OpenStreetMap | Térképes adatok, helykeresés |
| PY-PLUG-031 | `real_time` | Realtime | Valós idejű interakció és folyam |
| PY-PLUG-032 | `server` | Szerver | Kiszolgálóadapterek, API/feladatok |
| PY-PLUG-033 | `slack` | Slack | Üzenetek, csatornák, engedély |
| PY-PLUG-034 | `telegram` | Telegram | Chat-bot üzenetek |
| PY-PLUG-035 | `tuya` | Tuya okosotthon | Eszközkezelés, felhasználói jóváhagyás |
| PY-PLUG-036 | `twelvelabs` | Twelve Labs | Videó keresés/elemzés |
| PY-PLUG-037 | `twitter` | X/Twitter | Külső API és posztok |
| PY-PLUG-038 | `voice_control` | Hangvezérlés | Parancsérzékelés |
| PY-PLUG-039 | `wikipedia` | Wikipédia | Tudáskeresés és forrás |
| PY-PLUG-040 | `wolfram` | Wolfram | Matematikai/tudományos lekérdezés |

Ahol „értelmezett” szerepel, az a fájlnév és a plugin jellegének műszaki kategóriája; nem bizonyított, hogy a plugin minden felsorolt műveletét az adott refben kipróbáltuk. Például egy Facebook adapter jelenléte nem jelent API-bejelentkezést.

## 2. Az eredeti 16 PyGPT app tool és az egységes UI követelmények

| ID | Tool | GUI / API feladat |
|---|---|---|
| PY-TOOL-001 | `agent_builder` | Agent-profilok és konfigurációs felület |
| PY-TOOL-002 | `agent_workflow` | Agent-munkafolyamat és futásállapot |
| PY-TOOL-003 | `audio_transcriber` | Hangátírás, fájlfeldolgozás |
| PY-TOOL-004 | `calendar` | Események és időpontok |
| PY-TOOL-005 | `code_interpreter` | Védett kódfuttatás és kimenet |
| PY-TOOL-006 | `files` | Fájlok böngészése és kezelése |
| PY-TOOL-007 | `html_canvas` | HTML/JS megjelenítés |
| PY-TOOL-008 | `image_viewer` | Képnézegetés, részletezés |
| PY-TOOL-009 | `indexer` | Dokumentum/RAG indexelés |
| PY-TOOL-010 | `media_player` | Hang- és videólejátszás |
| PY-TOOL-011 | `notepad` | Jegyzetkezelés |
| PY-TOOL-012 | `painter` | Képi rajzolás |
| PY-TOOL-013 | `terminal` | Terminal pane kontrollált parancsokkal |
| PY-TOOL-014 | `text_editor` | Forrás- és szövegszerkesztő |
| PY-TOOL-015 | `translator` | Nyelvi fordítás |
| PY-TOOL-016 | `web_browser` | Webes nézet és navigáció |

**P5 GUI szabály:** a PyGPT app toolok nem tűnhetnek el attól, hogy JARVIS saját HUD-ját portoljuk. Minden toolhoz szükséges: menü/launcher, adatállapot, sikerminta, hiba, progress, kilépés/cleanup, approval.

## 3. Alrendszer-határok és duplikáció

| AI-képesség | PyGPT felelősség | FCC/Addon felelősség | Konfliktus elkerülése |
|---|---|---|---|
| Task planning | Agents V2 orchestrator | FCC csak delegált coding agent | Egyetlen globális task owner |
| Modelválasztás | Native API + tool/capability szükséglet | 61 provider opció / alias/fallback | Capability + cost matrix |
| Tool invoking | PyGPT plugin/MCP és agent flow | FCC tool-call protokoll + harness | Egyszeri idempotent operation |
| Session | PyGPT conversation/task ID | FCC coding session ID | 1:N mapping és trace ID |
| Memória | PyGPT index/chat memory | FCC saját session cache | No duplicate memory writer |
| STT/TTS | PyGPT audio provider | FCC opcionális voice input | JARVIS voice bus |
| UI | PyGPT Expert GUI (átmenetileg) | FCC admin UI külön | P5 után JARVIS HUD elsődleges |
| Repo edit | PyGPT policy/approval | Coding agent isolated worktree | write-once owner + review |
| Rich media | PyGPT native image/video/audio | FCC csak capability esetén | Native fallback, nincs capability loss |
| Addons | PyGPT Extension/Skills/MCP | FCC harness saját tool config | Central allowlist, nem rejtett globális telepítés |
| Dokumentumok | PyGPT Files/Indexer/office | FCC kódolóügynök segíthet | Single artifact source of truth |
| Scheduler | PyGPT cron / JARVIS reminder | FCC csak meghívásra | Nincs három párhuzamos ütemező |

## 4. Platformszintű AI/provider kapcsolatok

| Rendszer | Forrásban szereplő opciók | Feladat |
|---|---|---|
| pygpt/native | Anthropic, Azure OpenAI, Custom, DeepSeek, EdenAI, Forge, Google, Hugging Face, JEV, LiteLLM, Local, Mistral, Ollama, OpenRouter, OpenAI, Perplexity, Voyage, xAI | Native adapterek megőrzése |
| fcc/router | 61 provider-katalógus + custom | Model routing + stream + fallback |
| fcc/code | Claude Code, Codex, Pi, OpenCode, Cline, Hermes, DeepSeek Harness, Grok Build, Muse Code, Aider, VS Code Chat | Coding agent bridge |
| ext/skills | 37 registry Skill | Lazy resolve, dedup, approval |
| ext/mcp | 30 registry MCP | Run isolation, pinned deps |
| ext/addon | 2 extension demo / 11 példa | Nem productionként aktivált |

## 5. Tudás és betöltés részletezése

A PyGPT 30 dokumentum/web loader-könyvtár:
`file_csv`, `file_docx`, `file_epub`, `file_excel`, `file_html`, `file_image_vision`, `file_ipynb`, `file_json`, `file_markdown`, `file_pdf`, `file_video_audio`, `file_xml`, `hub`, `web_bitbucket`, `web_chatgpt_retrieval`, `web_database`, `web_github_issues`, `web_github_repo`, `web_google_calendar`, `web_google_docs`, `web_google_drive`, `web_google_gmail`, `web_google_keep`, `web_google_sheets`, `web_microsoft_onedrive`, `web_page`, `web_rss`, `web_sitemap`, `web_twitter`, `web_yt`.

Vektortár adapterek: `chroma.py`, `ctx_attachment.py`, `elasticsearch.py`, `pinecode.py`, `qdrant.py`, `redis.py`, `simple.py`, `temp.py`. A `pinecode` a forrásbeli fájlnév; nem állítjuk automatikusan, hogy minden változat teljes Pinecone SDK kompatibilitással működik. Külső adatbázisok valódi használatához külön service, authentikáció, index/schema és backup kell.

Bemenő hang: `bing_speech_recognition`, `google_cloud_speech_recognition`, `google_genai`, `google_speech_recognition`, `openai_whisper`, `openai_whisper_local`, `xai_grok_voice`.

Kimenő hang: `eleven_labs`, `google_genai_tts`, `google_tts`, `ms_azure_tts`, `openai_tts`, `xai_tts`. A kívánt magyar hanghoz külön hangmodell/adapter/rights és minőségmérés kell.

## 6. A harminc MCP connector szerepe

- **Fejlesztés és dokumentáció:** context7, deepwiki, github, playwright, chrome-devtools, microsoft-learn, mcp-docs, sequential-thinking.
- **Fájl és formátum:** filesystem, fetch, markitdown, time, memory.
- **Kreatív / 3D:** blender (külön Blender backend/addon kell).
- **Helyi infrastruktúra:** openclaw, docker-mcp-gateway, redis, mongodb, elasticsearch, qdrant, grafana, kubernetes.
- **Online keresés és felhős rendszerek:** brave-search, supabase, supabase-local, neon, linear, sentry, cloudflare-docs, atlassian.

Ez csak a 30 elem funkciócsoportosítása. A tényleges parancsokat, npx/uvx/Docker függőségeket, licenceket és titkokat az eredeti `mcp.json` alapján külön aktiválási döntésben rögzítjük.

## 7. A harminchét Skill szerepe

- **Fejlesztési fegyelem:** skill-creator, systematic-debugging, test-driven-development, requesting-code-review, receiving-code-review, verification-before-completion, writing-plans, executing-plans, finishing-a-development-branch, using-git-worktrees.
- **Ügynökmunka:** agents-sdk, mcp-builder, brainstorming, subagent-driven-development, dispatching-parallel-agents, writing-skills.
- **Felület:** frontend-design, webapp-testing, web-design-guidelines, vercel-react-best-practices, vercel-composition-patterns, vercel-react-view-transitions, vercel-react-native-skills, vercel-optimize, deploy-to-vercel, web-perf.
- **Dokumentumok:** docx, pdf, xlsx, pptx.
- **Backend/szolgáltatók:** stripe-best-practices, postgres-best-practices, neon, neon-postgres, workers-best-practices, durable-objects, wrangler.

A fenti csoportosítás a 37 tényleges Skill nevet tartalmazza; nem egy önállóan működő 37-es agentflotta.

## 8. Funkcionális tesztek és mérhető kimenetek

| Kód | Esemény | Elvárt válasz |
|---|---|---|
| AI-CAP-001 | Egyszerű chat→LLM | helyes provider, stream, task log |
| AI-CAP-002 | Adott modelben nincs tool calling | typed UNSUPPORTED vagy explicit natív váltás |
| AI-CAP-003 | Két agent ugyanazon fájlba írna | conflict és feladat-ownership |
| AI-CAP-004 | GitHub MCP érvénytelen token | AUTH_REQUIRED; nincs nyilvános titok |
| AI-CAP-005 | Code interpreter veszélyes művelet | denied / confirmation és sandbox |
| AI-CAP-006 | Addon forrás SHA mismatch | reject, nem importálódik |
| AI-CAP-007 | 1M token hangzó modell fallback | reális context limit check, nincs csendes csonkolás |
| AI-CAP-008 | Képes chat/vision provider nélkül | error/fallback, multimodal adatvesztés nélkül |
| AI-CAP-009 | Input TTS beszéd megszakítva | nem marad phantom-speaking event |
| AI-CAP-010 | MCP timeout | bounded retry, cancel, audit trace |
| AI-CAP-011 | Web/prompt injection eszközeredményben | untrusted tartalom nem lesz system utasítás |
| AI-CAP-012 | PyGPT eredeti GUI és JARVIS HUD | ugyanazon task/service állapotok, nincs versengő writer |

## 9. Pontos szolgáltatószintű acceptance séma

Minden addon/provider/agent rekordhoz: `id`, `source_repository`, `commit_sha`, `license`, `capabilities`, `requires_credentials`, `requires_network`, `risk_class`, `enabled`, `settings_owner`, `runtime_health`, `test_ids`, `known_gaps`. A `provider_catalog.py` megléte nem jelent élő API-kapcsolatot vagy jogszerű ingyenes hozzáférést.

## 10. Állapot

A dokumentum a meglévő források és tervezett adapterhatárok alapján készült. A 40 PyGPT könyvtár, 16 eszköz, 30 MCP, 37 Skill és az FCC 61 providerbejegyzése **leltározott**, nem mind telepített és tesztelt. P2/P3/P4 csak a [fáziskapuk](03-phases-and-gates.md) tényleges teljesítése után minősíthető késznek.
