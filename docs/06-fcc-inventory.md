# 06 — Free Claude Code (ai_proxy_2) komponens- és API-leltár

## Forrásirány, reprodukálhatóság és magánszféra

Korábbi nyilvános fork: https://github.com/Rishurajgautam24/free-claude-code @ a599319dd6d56cf5ea1db7e52eeac0bc80fccb7c. Fejlettebb nyilvános upstream: https://github.com/Alishahryar1/free-claude-code @ c5239619be489ff393fff29caf838c8a5a957454. A felhasználói privát munka nem került át a nyilvános repo-ba. Nem azonosítjuk a régi MIT-forráslicencet az új upstream AGPL-3.0-only licenccel.

Az alábbi 61-bejegyzéses katalógus egy korábbi forrásauditból származik, új upstream-pinen újra ellenőrizendő. A Python 3.14.7 FCC és a PyGPT 3.10–3.13 külön virtualenv/processzt igényel.

## 61 modellszolgáltatói bejegyzés
| # | Provider konfigurációs azonosító | Név |
|---:|---|---|
| 1 | nvidia_nim | NVIDIA NIM |
| 2 | open_router | OpenRouter |
| 3 | groq | Groq |
| 4 | cline_pass | ClinePass |
| 5 | openai | OpenAI linked account |
| 6 | openai_api | OpenAI API |
| 7 | anthropic | Anthropic |
| 8 | github_copilot | GitHub Copilot |
| 9 | xai | xAI Grok |
| 10 | alibaba_cloud | Alibaba Cloud |
| 11 | qwencloud | QwenCloud Token |
| 12 | qwencloud_coding | QwenCloud Coding |
| 13 | together | Together AI |
| 14 | deepinfra | DeepInfra |
| 15 | siliconflow | SiliconFlow |
| 16 | nebius | Nebius |
| 17 | chutes | Chutes |
| 18 | featherless | Featherless |
| 19 | agnes | Agnes AI |
| 20 | zenmux | ZenMux |
| 21 | wandb | W&B |
| 22 | azure_openai | Azure OpenAI |
| 23 | gemini | Google Gemini |
| 24 | vertex | Google Vertex |
| 25 | deepseek | DeepSeek |
| 26 | mistral | Mistral |
| 27 | mistral_codestral | Mistral Codestral |
| 28 | opencode_zen | OpenCode Zen |
| 29 | opencode_go | OpenCode Go |
| 30 | vercel | Vercel AI Gateway |
| 31 | bedrock | Amazon Bedrock |
| 32 | huggingface | HuggingFace |
| 33 | cohere | Cohere |
| 34 | wafer | Wafer |
| 35 | kimi | Kimi |
| 36 | kimi_code | Kimi Code |
| 37 | kilo | Kilo |
| 38 | minimax | MiniMax |
| 39 | cerebras | Cerebras |
| 40 | sambanova | SambaNova |
| 41 | fireworks | Fireworks |
| 42 | novita | Novita |
| 43 | cloudflare | Cloudflare |
| 44 | zai | Z.ai Coding |
| 45 | zai_api | Z.ai API |
| 46 | tokenrouter | TokenRouter |
| 47 | nararoute | NaraRoute |
| 48 | poolside | Poolside |
| 49 | llm7 | LLM7 |
| 50 | scaleway | Scaleway |
| 51 | lightning | Lightning |
| 52 | experiential | Experiential |
| 53 | cheaperinference | CheaperInference |
| 54 | orcarouter | OrcaRouter |
| 55 | atlascloud | Atlas Cloud |
| 56 | xkiro | xKiro |
| 57 | opper | Opper |
| 58 | ollama_cloud | Ollama Cloud |
| 59 | lmstudio | LM Studio |
| 60 | llamacpp | llama.cpp |
| 61 | ollama | Ollama |

61 konfigurációs provider **nem** 61 külön ingyenes modell vagy előfizetés. Custom provider konfiguráció tovább bővítheti.

## 11 coding agent / kliens
| # | Név | Típus |
|---:|---|---|
| 1 | Claude Code | Coding agent/harness |
| 2 | OpenAI Codex | Coding agent/harness |
| 3 | Pi | Coding agent/harness |
| 4 | OpenCode | Coding agent/harness |
| 5 | Cline | Coding agent/harness |
| 6 | Hermes Agent | Coding agent/harness |
| 7 | DeepSeek Harness | Coding agent/harness |
| 8 | Grok Build | Coding agent/harness |
| 9 | Muse Code | Coding agent/harness |
| 10 | Aider | Coding agent/harness |
| 11 | VS Code Chat | VS Code integráció |

## Fő képességblokkok

Anthropic Messages /v1/messages; OpenAI Responses /v1/responses; /v1/messages/count_tokens; model router, alias, fallback, retries, rate limit; SSE streaming; message/tool/thinking konverzió; admin model és kapcsolt fiók beállítások; browser coding sessions /admin/api/code/...; CLI harnessök; Discord/Telegram; helyi Whisper/NVIDIA NIM hangbevitel; diagnosztika, updater, session resume.

## P3 belépési és elfogadási kapu

1. Felhasználható forrás verzió/licenc megválasztva.
2. API szolgáltatás helyben és hitelesítve, soha nem admin a teljes LAN-on.
3. Contract test: /v1/messages, /v1/responses, token count.
4. SSE teszt: chunk, finish_reason, tool arguments, reasoning blokk.
5. Fallback: rate-limit, credential failure, invalid model, offline backend.
6. Agent harness: workspace-scope, approvals, interrupt, resume és result.
7. Native PyGPT audio/image/video adapterek nem vesznek el FCC beházasításkor.
8. End-to-end: PyGPT → FCC → provider / code agent → PyGPT event → felhasználó.

## Security

A vizsgált FCC alapértékekben szerepelt 0.0.0.0 hálózati bind és kikapcsolt auth. Ezeket nem fogadjuk el. Elvárt: 127.0.0.1, auth, least privilege, sandboxed tool processz, admin endpoint és token lekorlátozás. BypassPermissions alapból tiltott.

**Státusz:** dokumentált és kutatott, P3 a célrepóban még NOT_STARTED.
