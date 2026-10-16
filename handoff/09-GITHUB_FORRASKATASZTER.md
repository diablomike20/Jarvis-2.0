# 09 — GitHub forrás- és ágkataszter, használható elérési utak

## A Project Icarus 2026-10-16-i állapota
**Cél:** https://github.com/diablomike20/Jarvis-2.0, publikus main base: `38d6991faf52eb1c2348773b702a9fb44db6f470`.
Dokumentáció: https://github.com/diablomike20/Jarvis-2.0/tree/docs/master-spec-20261016
Integrációs baseline: https://github.com/diablomike20/Jarvis-2.0/tree/integration/pygpt-addons-baseline
Source baseline: https://github.com/diablomike20/Jarvis-2.0/tree/sources/pinned-project-baseline
Handoff: https://github.com/diablomike20/Jarvis-2.0/tree/docs/final-handoff-20261016

## Pontos források
| Modul | Repository | Referencia commit |
|---|---|---|
| Eredeti JARVIS/Brahma | diablomike20/Jarvis-Ai | e0bd3c5a3a258cc1cf35014ae0a35c7b6b9db87f |
| PyGPT | diablomike20/PyGPT | 2d8779a983edc73846a640bbbda1dcc7d513d924 |
| PyGPT_Addons | diablomike20/PyGPT_Addons | 15759ba00cab37622e0b9f5b302c73fc7aa56a50 |
| Nyilvános új FCC upstream | Alishahryar1/free-claude-code | c5239619be489ff393fff29caf838c8a5a957454 |
| Korábbi FCC fork | Rishurajgautam24/free-claude-code | a599319dd6d56cf5ea1db7e52eeac0bc80fccb7c |
| PhotoCraft | diablomike20/photocraft | b71991e15a3fc01d3c5848464c14c19b6dc8f2b5 |
| LightCraft | diablomike20/lightcraft | 7b47ba7894a2563be32ab75176866b6d743df7a4 |
| FilmCraft | diablomike20/filmcraft | 5231852443363f001c3f6b396dd9b1e6461ae2be |
| God's Eye View | diablomike20/gods-eye-view | e2274bbf0ceaeb2e14f8a59d63e77000553c6816 |
| HeyPuter Everything | HeyPuter/everything | 06802a1e3749202e4db94d39c9ef5ab1a97d0ef1 |
| REA | morluto/rea | 1bd5c5c87e81b27bfb16140f71ffa03563e58477 |
| VoiceStudio | debpalash/VoiceStudio | 28d18023436229830debe8e65faf3eba4426f31b |
| IronRAG | mlimarenko/IronRAG | ad8f846aba5a4dd888eae8cf5033f5beb5c8d634 |
| Superpowers | obra/superpowers | bb92a77741419a4ab5f06e711a283343f1ada0c3 |
| DeerFlow | bytedance/deer-flow | 2464566942ace4ffe71d347fde3dd9868e2ecd5d |
| AI Memory Vault | jaredrhod/ai-memory-vault | 659bba9c8b351c937dd393b3042801d1ff1b502c |
| Fullstack Agent | jaredrhod/fullstack-agent | 5bb159f47dbd6fa8f108651d0532a43aef16346b |

**Privát forrás:** diablomike20/AI-Proxy és diablomike20/Free-Claude-AI külön, nem másolható a publikus Jarvis-2.0-ba. A privát anyagokhoz nem számolunk automatikus fejlesztő hozzáféréssel.

## Funkcionális dokumentáció értelemszerűen
A `docs/00–16c` már ténylegesen GitHubra töltött, bő komponens- és funkcióleltár. A `handoff/` kiegészítés nem duplázza meg azt mechanikusan: pontos utalások, új auditok és közös tanulmányozási protokoll.

## Branch-szabály
Branch létrehozása nem „telepítés”. Submodule pontos Git objektumhivatkozás, nem automatikusan működő szolgáltatás. A privát/AGPL felhasználás kizárja a kontrollálatlan széles monolitikus repo-beolvasztást. Forrásupgrade csak új SHA/diff/test/ADR után.

## Gépi nyilvántartás
`catalog/feature-registry.v1.json`, `catalog/acceptance-tests.v1.json`, `catalog/public-source-lock.v1.json`, `catalog/research-reference-lock.v1.json`; jövőben külön `catalog/decisions.v1.json` és `state/current-status.json` is hasznos. Bármely ügynök ellenőrizze az aktuális HEAD-et, mert a fenti SHA-k 2026-10-16 snapshotok.

## 2026-10-16 igazolt nyolcadik public source

A `sources/pinned-project-baseline` branch HEAD: `a728b50752b0360166f01b922a839083f83dcedf`. Tartalmazza a `sources/gods-eye-view` gitlinket, amely a `e2274bbf0ceaeb2e14f8a59d63e77000553c6816` commitra mutat. A nyolc alárendelt forrás közül ez az opcionális P6 3D térinformatikai/MCP jelölt, **nem működő PyGPT funkcióként lett hozzáadva**.
