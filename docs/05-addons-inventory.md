# 05 — PyGPT_Addons katalógus és aktiválási szabályzat

**Forrás:** https://github.com/diablomike20/PyGPT_Addons/tree/15759ba00cab37622e0b9f5b302c73fc7aa56a50
**Állapot:** 2 Add-on + 30 MCP + 37 Skill = 69 katalóguselem; továbbá 11 átfedő oktató minta. **NEM mind telepített.**

## Két Add-on
| ID | Típus | Trusted jelző | Forrás |
|---|---|---|---|
| example_plugin | plugin | true | https://github.com/szczyglis-dev/py-gpt-addons/tree/v1.1.0/examples/plugins/example_plugin |
| example-extension-dark | theme | false | https://github.com/szczyglis-dev/py-gpt-addons/tree/v1.1.0/examples/themes/example-extension-dark |

A katalógus immutable refre és SHA-256-ra hivatkozik; checksum nem kódaláírás vagy sandbox.

## Harminc MCP
| # | Név | Telepítés |
|---:|---|---|
| 1 | context7 | NOT_INSTALLED, review szükséges |
| 2 | deepwiki | NOT_INSTALLED, review szükséges |
| 3 | github | NOT_INSTALLED, review szükséges |
| 4 | playwright | NOT_INSTALLED, review szükséges |
| 5 | chrome-devtools | NOT_INSTALLED, review szükséges |
| 6 | microsoft-learn | NOT_INSTALLED, review szükséges |
| 7 | markitdown | NOT_INSTALLED, review szükséges |
| 8 | blender | NOT_INSTALLED, review szükséges |
| 9 | memory | NOT_INSTALLED, review szükséges |
| 10 | fetch | NOT_INSTALLED, review szükséges |
| 11 | sequential-thinking | NOT_INSTALLED, review szükséges |
| 12 | openclaw | NOT_INSTALLED, review szükséges |
| 13 | filesystem | NOT_INSTALLED, review szükséges |
| 14 | time | NOT_INSTALLED, review szükséges |
| 15 | mcp-docs | NOT_INSTALLED, review szükséges |
| 16 | docker-mcp-gateway | NOT_INSTALLED, review szükséges |
| 17 | redis | NOT_INSTALLED, review szükséges |
| 18 | mongodb | NOT_INSTALLED, review szükséges |
| 19 | elasticsearch | NOT_INSTALLED, review szükséges |
| 20 | brave-search | NOT_INSTALLED, review szükséges |
| 21 | supabase | NOT_INSTALLED, review szükséges |
| 22 | supabase-local | NOT_INSTALLED, review szükséges |
| 23 | neon | NOT_INSTALLED, review szükséges |
| 24 | linear | NOT_INSTALLED, review szükséges |
| 25 | sentry | NOT_INSTALLED, review szükséges |
| 26 | cloudflare-docs | NOT_INSTALLED, review szükséges |
| 27 | qdrant | NOT_INSTALLED, review szükséges |
| 28 | grafana | NOT_INSTALLED, review szükséges |
| 29 | kubernetes | NOT_INSTALLED, review szükséges |
| 30 | atlassian | NOT_INSTALLED, review szükséges |

Külön források, jogosultságok és futtatókörnyezetek: npx/uvx/Docker, API-kulcsok és hálózat. GitHub/FileSystem/MCP/Playwright/Qdrant alapból nem kaphat korlátlan írási jogot.

## Harminchét Skill
| # | Név | Telepítés |
|---:|---|---|
| 1 | skill-creator | CATALOGUED, NOT_INSTALLED |
| 2 | systematic-debugging | CATALOGUED, NOT_INSTALLED |
| 3 | test-driven-development | CATALOGUED, NOT_INSTALLED |
| 4 | requesting-code-review | CATALOGUED, NOT_INSTALLED |
| 5 | writing-plans | CATALOGUED, NOT_INSTALLED |
| 6 | frontend-design | CATALOGUED, NOT_INSTALLED |
| 7 | vercel-react-best-practices | CATALOGUED, NOT_INSTALLED |
| 8 | vercel-composition-patterns | CATALOGUED, NOT_INSTALLED |
| 9 | webapp-testing | CATALOGUED, NOT_INSTALLED |
| 10 | mcp-builder | CATALOGUED, NOT_INSTALLED |
| 11 | agents-sdk | CATALOGUED, NOT_INSTALLED |
| 12 | docx | CATALOGUED, NOT_INSTALLED |
| 13 | pdf | CATALOGUED, NOT_INSTALLED |
| 14 | xlsx | CATALOGUED, NOT_INSTALLED |
| 15 | pptx | CATALOGUED, NOT_INSTALLED |
| 16 | brainstorming | CATALOGUED, NOT_INSTALLED |
| 17 | executing-plans | CATALOGUED, NOT_INSTALLED |
| 18 | subagent-driven-development | CATALOGUED, NOT_INSTALLED |
| 19 | dispatching-parallel-agents | CATALOGUED, NOT_INSTALLED |
| 20 | receiving-code-review | CATALOGUED, NOT_INSTALLED |
| 21 | verification-before-completion | CATALOGUED, NOT_INSTALLED |
| 22 | using-git-worktrees | CATALOGUED, NOT_INSTALLED |
| 23 | finishing-a-development-branch | CATALOGUED, NOT_INSTALLED |
| 24 | writing-skills | CATALOGUED, NOT_INSTALLED |
| 25 | vercel-react-view-transitions | CATALOGUED, NOT_INSTALLED |
| 26 | vercel-react-native-skills | CATALOGUED, NOT_INSTALLED |
| 27 | web-design-guidelines | CATALOGUED, NOT_INSTALLED |
| 28 | vercel-optimize | CATALOGUED, NOT_INSTALLED |
| 29 | deploy-to-vercel | CATALOGUED, NOT_INSTALLED |
| 30 | stripe-best-practices | CATALOGUED, NOT_INSTALLED |
| 31 | postgres-best-practices | CATALOGUED, NOT_INSTALLED |
| 32 | neon | CATALOGUED, NOT_INSTALLED |
| 33 | neon-postgres | CATALOGUED, NOT_INSTALLED |
| 34 | workers-best-practices | CATALOGUED, NOT_INSTALLED |
| 35 | durable-objects | CATALOGUED, NOT_INSTALLED |
| 36 | wrangler | CATALOGUED, NOT_INSTALLED |
| 37 | web-perf | CATALOGUED, NOT_INSTALLED |

## 11 mintaprojekt

examples/plugins/example_plugin; tools/example_tool; llms/example_llm; vector_stores/example_vector_store; loaders/example_loader; audio_input/example_audio_input; audio_output/example_audio_output; web/example_web; agents/example_agent; themes/example-extension-dark; locale/example-locale.

A minták nem production kész termékek. Az audio_output példában nincs kész magyar hangszintézis.

## Szabályok

- Első futtatás előtt immutable commit/release, függőségek, licencek és telepítőszkriptek auditja.
- Csak az adott feladathoz szükséges toolok engedélyezése, read-only alapállapot.
- Külső token csak hitelesített secrets store-ban; logba és gitbe nem.
- Skill deduplikáció: Superpowers 15-ből 13, nagy Skill Tree helyi anyagaiból 18 névegyezés a PyGPT katalógussal.
- Katalógus = dokumentált lehetőség, instantiation = konfiguráció, PASS = tényleges teszt.
- Aktiválási kategóriák javaslatként: CORE, ON_DEMAND, PARKED; végleges lista későbbi döntés.
