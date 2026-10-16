# 01 — Forráskód, eredet, commitok és elválasztás

Minden SHA az ellenőrzés pillanatában lekért ágfej. Reprodukálható buildhez ezeket kell használni, **nem mozgó main/master hivatkozásokat**.

## Alapkomponensek

| Szerep | Repository | Ág | Rögzített commit | Forrásfajta |
|---|---|---|---|---|
| Cél | diablomike20/Jarvis-2.0 | main | 38d6991faf52eb1c2348773b702a9fb44db6f470 | Public, Project Icarus |
| Forrás JARVIS | diablomike20/Jarvis-Ai | main | e0bd3c5a3a258cc1cf35014ae0a35c7b6b9db87f | Public, eredeti HUD/alkalmazás |
| PyGPT alapmotor | diablomike20/PyGPT | master | 2d8779a983edc73846a640bbbda1dcc7d513d924 | Public, felhasználói másolat |
| PyGPT bővítmények | diablomike20/PyGPT_Addons | master | 15759ba00cab37622e0b9f5b302c73fc7aa56a50 | Public, addon-katalógus |
| FCC upstream | Alishahryar1/free-claude-code | main | c5239619be489ff393fff29caf838c8a5a957454 | Public upstream, AGPL-változat |
| FCC korábbi fork | Rishurajgautam24/free-claude-code | main | a599319dd6d56cf5ea1db7e52eeac0bc80fccb7c | Public referencia, régebbi MIT fork |
| PhotoCraft | diablomike20/photocraft | main | b71991e15a3fc01d3c5848464c14c19b6dc8f2b5 | P6 public forrás |
| LightCraft | diablomike20/lightcraft | main | 7b47ba7894a2563be32ab75176866b6d743df7a4 | P6 public forrás |
| FilmCraft | diablomike20/filmcraft | main | 5231852443363f001c3f6b396dd9b1e6461ae2be | P6 public forrás |

Az összes tároló GitHub URL-je: https://github.com/ + a fenti owner/repo mező. FreeCAD megadott, pontosan rögzített célforkja még nincs; PROPOSED csak standard illesztési réteg.

**Privát forrás:** külön AI-Proxy repository létezése megfigyelt, de az automatikus publikus másolás TILOS. A privát repo aktuális commitja és tartalma nem kerül bele a publikus lockfile-ba; P3 előtt külön dönteni kell, mit szabad feltárni. A privát és publikus FCC forkok azonos vagy eltérő commitja NEM ad felhatalmazást a privát konfigurációk publikálására.

## Kutatási referenciák (nem telepítve)

| Projekt | Pinelt commit |
|---|---|
| morluto/rea | 1bd5c5c87e81b27bfb16140f71ffa03563e58477 |
| debpalash/VoiceStudio | 28d18023436229830debe8e65faf3eba4426f31b |
| mlimarenko/IronRAG | ad8f846aba5a4dd888eae8cf5033f5beb5c8d634 |
| bytedance/deer-flow | 2464566942ace4ffe71d347fde3dd9868e2ecd5d |
| obra/superpowers | bb92a77741419a4ab5f06e711a283343f1ada0c3 |
| AlphaSaleAidan/opus-5-5-x-gpt-skill-tree | d95cc14f11dff819f4e7ae8d1b9f5a22eeb58fe8 |
| jaredrhod/fullstack-agent | 5bb159f47dbd6fa8f108651d0532a43aef16346b |
| jaredrhod/ai-memory-vault | 659bba9c8b351c937dd393b3042801d1ff1b502c |
| jaredrhod/backtalk | 84b3a6cd321060cabb74aad6ebe794621cf99bd3 |
| jaredrhod/ai-visualizer | 6921e1d4b06bdd4a34c5264882d5257c4d5f70fd |
| jaredrhod/barehands | eb23bed2d772f9d5a24de26fb92f46c3c76d69cf |
| x1xhlol/system-prompts-and-models-of-ai-tools | 162db92f54d717d8ebd12292e155aeef32bb4b3c |
| asgeirtj/system_prompts_leaks | 3c4deaae9bbd6259e3d972f3bdb208ef6fd942f9 |
| BeatAPI/awesome-3d-prompts | ac37217b7b723fbe38095503e06e3b818fbb1a85 |
| zlxxlz1026/awesome-gpt-6-astra-casebook | ada87b35d4adfedef21816cd2969d0ff88a9427e |
| Anil-matcha/awesome-gpt-6-astra | 22b75e2b1a900fb9ee9932f753d1bc46e4c9fd16 |

## Licenc-megőrzési szabály

A PyGPT eredeti upstream MIT-ként lett korábban ellenőrizve; a felhasználói repo GitHub metadata licence NOASSERTION, ezért a tényleges fájllicenc és minden komponens SPDS/NOTICE auditja szükséges. Az új FCC upstream AGPL-3.0-only; a régi FCC fork MIT; e két kódbázis nem tekinthető jogilag felcserélhetőnek. VoiceStudio és a jaredrhod fullstack/backtalk/visualizer/barehands AGPL-3.0; Memory Vault CC-BY-SA-4.0; IronRAG/REA MIT-ként jelzett. Külső modell- és adatlicencek ettől függetlenül vizsgálandók.

## Git forrásmegjelenítés

Az integrációs ágon PyGPT és Add-ons **Git submodule**, nem másolt Git-történet vagy squash. Ez a forráskód pontos commitját elérhetővé teszi GitHubról és --recurse-submodules checkouttal; offline és teljes forrásarchiválást nem helyettesít. Más projektet nem emeltünk még futtatásra.

## Projektanyagok és magánszféra

A feltöltött JARVIS-beszélgetés-exportokban és hanganyagokban lehet személyes információ, nem publikus projektadat vagy jogilag korlátozott audiotartalom. A nyilvános repositoryba csak tisztított műszaki dokumentációt írunk; teljes nyers beszélgetés-exportok és hangminták csak külön, ellenőrzött privát tárolásba kerülhetnek. Az ilyen állományokat itt dokumentált, de nem teljesített migrációs tételnek tekintjük.

## Tényleges külön forrásgyűjtemény-ág

**sources/pinned-project-baseline** @ 1da31bdd7850665d963906dfc8a4d97b2788e94d — 7 nyilvános Git submodule: PyGPT, PyGPT_Addons, original JARVIS, PhotoCraft, LightCraft, FilmCraft, FCC upstream. A branch saját .gitmodules és sources-manifest.json fájlt tartalmaz. Ezzel a később sorra kerülő programrészek forrása a Jarvis-2.0 keretében visszakereshető, de NINCS futtatva vagy összeolvasztva. A kutatási 16 repó továbbra is pinelt külső referencia, nem kötelező checkout. A privát AI-Proxy nem itt van.

## 2026-10-16 frissítés — God's Eye View

A `diablomike20/gods-eye-view` public fork `main` referencia `e2274bbf0ceaeb2e14f8a59d63e77000553c6816`; a `Jarvis-2.0` `sources/pinned-project-baseline` commitja `a728b50752b0360166f01b922a839083f83dcedf` már ezt a nyolcadik submodule-t is tartalmazza. A live feed/dataset/model license külön audit, nem teljes MIT adatcsomag. Forrás: https://github.com/diablomike20/gods-eye-view, audit: `handoff/03-GODS_EYE_VIEW_TECHNIKAI_AUDIT.md`.
