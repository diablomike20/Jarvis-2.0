# 14 — Ténylegesen végrehajtott GitHub-migrációk naplója

**Dátum:** 2026-10-16. **Cél:** https://github.com/diablomike20/Jarvis-2.0. Nyilvános.

## Kezdeti referencia

- Target main: 38d6991faf52eb1c2348773b702a9fb44db6f470
- Kezdő fájl: README.md ("# Jarvis-2.0 / Project Icarus")
- Könyvtárszintű API ellenőrzés: hozzáférés admin:true / push:true.
- A main branch érintetlen maradt.

## Létrehozott ágak

1. docs/master-spec-20261016 a kezdő main SHA-ból.
2. integration/pygpt-addons-baseline a kezdő main SHA-ból.

## Integrációs ág konkrét commit

074b2efb8c4a73aee8d55d8b6bc56a2e69df211c

A branch tartalma: .gitmodules; INTEGRATION.md; README.md; upstream/pygpt submodule pin 2d8779a983edc73846a640bbbda1dcc7d513d924; upstream/pygpt-addons pin 15759ba00cab37622e0b9f5b302c73fc7aa56a50.

Git Gitlink-objektumokat hoztunk létre; a submodule külső forrás pontos HEAD-jét a rekurzív klón letölti. A checkout valódi Windows/Python működése NOT_RUN, ezért az első P2 elfogadási teszt még NEM teljesült.

## Dokumentációs ág commitok

- 56937ac6d114c0207ccc9cb1280c3789fa07e5cf — README, charter, forrás-pin, architektúra, fázisok.
- 85d6a1796299244095d6be45a22391108361e8a6 — PyGPT, Add-ons, FCC, GUI leltár.
- 6b468a53a26717aea47787f7d3ff4e93b455d59e — IPC, security, kutatási backlog, handoff.
- A következő commitban további tesztek, rizikó, ADR, napló és gépi katalógus.

## Ami NEM történt meg

- Nem változott Jarvis-2.0 main és a korábbi JARVIS/PyGPT/Add-ons/FCC upstream.
- Nem történt PyGPT Windows indulás vagy telepítési próba.
- Nem állítottunk be GitHub branch protection ruleset-et.
- Nem került át a privát AI-Proxy forrás; nincs FCC P3 service a célrepóban.
- Nem került át nyers beszélgetés-export, hanganyag, teljesfilm- vagy modellbináris.
- Nem épült meg JARVIS GUI-port, végleges magyar hang, PhotoCraft/LightCraft/FilmCraft/FreeCAD adapter.
- Nem történt automatikus PR merge / push default main ágra.

## Jelentési elv

Forrásbeemelés ≠ működő integráció. Dokumentációs commit ≠ végrehajtott teszt. User által jóváhagyandó nyitott feladatok külön backlog és fáziskapu szerint.
