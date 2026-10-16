# Project Icarus — pinned public source archive

**Ág: sources/pinned-project-baseline.** Ez nem egy futtatható, összemerge-elt JARVIS build, hanem pontos SHA-kra pinelt Git submodule-okba rendezett, nyilvános forrásgyűjtemény.

| Útvonal | Forrásverzió | Cél |
|---|---|---|
| sources/pygpt | 2d8779a983edc73846a640bbbda1dcc7d513d924 | Core Python/PySide6 engine |
| sources/pygpt-addons | 15759ba00cab37622e0b9f5b302c73fc7aa56a50 | Curated MCP/Skills/extension catalog |
| sources/jarvis-original | e0bd3c5a3a258cc1cf35014ae0a35c7b6b9db87f | Original HUD/Brahma source, P5 target |
| sources/photocraft | b71991e15a3fc01d3c5848464c14c19b6dc8f2b5 | P6 creative image editing |
| sources/lightcraft | 7b47ba7894a2563be32ab75176866b6d743df7a4 | P6 creative lighting/editing |
| sources/filmcraft | 5231852443363f001c3f6b396dd9b1e6461ae2be | P6 video studio |
| sources/fcc-upstream | c5239619be489ff393fff29caf838c8a5a957454 | P3 PUBLIC FCC upstream reference, not linked to private AI-Proxy |

## Lekérés

~~~bash
git clone --branch sources/pinned-project-baseline https://github.com/diablomike20/Jarvis-2.0.git
git -C Jarvis-2.0 submodule update --init --recursive
~~~

## Biztonsági, licenc- és igazolási határok

- A forráskomponensek egymással még nincsenek futásidejűen integrálva; csak teljesen külön, visszakereshető checkoutokként szerepelnek.
- A privát AI-Proxy kódját, tokenjeit, projektbeszélgetés-exportokat, filmes hangmintákat nem mozgattuk ide.
- A PyGPT forrás licence, az AGPL-3.0-only FCC, egyes kreatív szoftverek és külső modellek licencfeltételeit továbbra is ellenőrizni kell, ha később összevonás/terjesztés történik.
- A submodule nem offline archive: checkout hálózati elérését és license notice fájlokat meg kell őrizni.
- Telepíthető PyGPT baseline: integration/pygpt-addons-baseline ág. Részletes dokumentáció: docs/master-spec-20261016 ág.
