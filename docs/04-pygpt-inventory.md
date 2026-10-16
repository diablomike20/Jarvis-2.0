# 04 — PyGPT komponensleltár, 1:1 funkcióparitási alap

**Pinelt forrás:** https://github.com/diablomike20/PyGPT/tree/2d8779a983edc73846a640bbbda1dcc7d513d924

Forráskód-könyvtárak alapján. A könyvtár léte **nem bizonyít telepített, bekapcsolt vagy működő funkciót**. Minden alábbi runtime státusza: NOT_RUN.

## Rendszermódok és fő képességek
Chat; Agents/Chat; Agents/Orchestrator; Agents/Swarm; Custom Agents; Autonomous Mode; Experts; Research; Realtime/Audio; Computer Use; Image; Video; Completion. Agent V2 runtime, munkafolyamat, worker, delegálás; MCP, Skills, Extension, RAG és app eszközök.

## Pluginok — 40 könyvtár, ebből 39 funkcionális és base
Forrás: src/pygpt_net/plugin
| # | Plugin | Státusz |
|---:|---|---|
| 1 | agent | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 2 | audio_input | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 3 | audio_output | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 4 | base | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 5 | bitbucket | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 6 | canvas_web | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 7 | cmd_api | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 8 | cmd_code_interpreter | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 9 | cmd_custom | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 10 | cmd_files | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 11 | cmd_history | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 12 | cmd_mouse_control | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 13 | cmd_serial | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 14 | cmd_system | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 15 | cmd_web | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 16 | crontab | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 17 | experts | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 18 | extra_prompt | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 19 | facebook | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 20 | filesystem | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 21 | github | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 22 | google | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 23 | idx_llama_index | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 24 | jev | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 25 | mailer | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 26 | mcp | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 27 | memory | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 28 | openai_dalle | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 29 | openai_vision | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 30 | osm | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 31 | real_time | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 32 | server | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 33 | slack | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 34 | telegram | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 35 | tuya | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 36 | twelvelabs | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 37 | twitter | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 38 | voice_control | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 39 | wikipedia | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 40 | wolfram | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |

Magas jogosultságot igénylők: cmd_system, cmd_files, cmd_mouse_control, cmd_serial, cmd_code_interpreter, filesystem, crontab, network-connected toolok. Minden ilyen műveletet a központi jóváhagyásnak kell elbírálnia.

## Toolok — 16 külön alkalmazáseszköz
Forrás: src/pygpt_net/tools
| # | Eszköz | Státusz |
|---:|---|---|
| 1 | agent_builder | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 2 | agent_workflow | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 3 | audio_transcriber | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 4 | calendar | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 5 | code_interpreter | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 6 | files | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 7 | html_canvas | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 8 | image_viewer | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 9 | indexer | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 10 | media_player | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 11 | notepad | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 12 | painter | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 13 | terminal | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 14 | text_editor | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 15 | translator | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 16 | web_browser | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |

## AI-adaptercsaládok — 18
Forrás: src/pygpt_net/provider/llms
| # | Provider | Státusz |
|---:|---|---|
| 1 | anthropic | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 2 | azure_openai | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 3 | custom | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 4 | deepseek | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 5 | edenai | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 6 | forge | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 7 | google | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 8 | hugging_face | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 9 | jev | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 10 | litellm | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 11 | local | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 12 | mistral | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 13 | ollama | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 14 | open_router | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 15 | openai | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 16 | perplexity | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 17 | voyage | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 18 | x_ai | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |

Provider jelenléte nem egyenlő API-kulcs, szolgáltatói előfizetés vagy összes multimodális capability meglétével.

## Betöltők — 30
Forrás: src/pygpt_net/provider/loaders
| # | Loader | Státusz |
|---:|---|---|
| 1 | file_csv | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 2 | file_docx | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 3 | file_epub | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 4 | file_excel | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 5 | file_html | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 6 | file_image_vision | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 7 | file_ipynb | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 8 | file_json | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 9 | file_markdown | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 10 | file_pdf | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 11 | file_video_audio | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 12 | file_xml | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 13 | hub | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 14 | web_bitbucket | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 15 | web_chatgpt_retrieval | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 16 | web_database | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 17 | web_github_issues | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 18 | web_github_repo | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 19 | web_google_calendar | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 20 | web_google_docs | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 21 | web_google_drive | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 22 | web_google_gmail | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 23 | web_google_keep | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 24 | web_google_sheets | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 25 | web_microsoft_onedrive | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 26 | web_page | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 27 | web_rss | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 28 | web_sitemap | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 29 | web_twitter | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 30 | web_yt | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |

## Vektortárolás — 8
Forrás: src/pygpt_net/provider/vector_stores
| # | Vektortár | Státusz |
|---:|---|---|
| 1 | chroma | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 2 | ctx_attachment | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 3 | elasticsearch | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 4 | pinecode | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 5 | qdrant | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 6 | redis | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 7 | simple | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 8 | temp | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |

## Beszéd-bemenet — 7
| # | STT adapter | Státusz |
|---:|---|---|
| 1 | bing_speech_recognition | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 2 | google_cloud_speech_recognition | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 3 | google_genai | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 4 | google_speech_recognition | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 5 | openai_whisper | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 6 | openai_whisper_local | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 7 | xai_grok_voice | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |

## Beszéd-kimenet — 6
| # | TTS adapter | Státusz |
|---:|---|---|
| 1 | eleven_labs | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 2 | google_genai_tts | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 3 | google_tts | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 4 | ms_azure_tts | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 5 | openai_tts | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |
| 6 | xai_tts | SOURCE_VERIFIED / NOT_RUNTIME_TESTED |

## Architektúrát érintő konkrét források

- src/pygpt_net/app_core.py — Core(window), nem kész headless API.
- src/pygpt_net/core/agents_v2/runtime.py — agent lifecycle és munkamenet.
- src/pygpt_net/core/extensions/extensions.py és controller/extensions — addon telepítése/Qt GUI.
- src/pygpt_net/core/security/security.py — hozzáférés és prompt-injection kontrollok.
- src/pygpt_net/ui és controller — Qt MainWindow alkatrészek.
- src/pygpt_net/plugin, tools, provider — fenti katalógus.

A hiányzó kulcs vagy külső környezet nem PyGPT regresszió; BLOCKED_BY_CONFIG állapot. A valódi 1:1 megőrzéshez funkciónként menü/API, bemenet, kimenet, hibák, jogosultság és Windows teszt kell.