# JARVIS UNIFIED — PyGPT + Add-ons source integration (P1/P2)

**Állapot: forrásbeemelési baseline; NEM futásidejű integráció.**

A két eredeti, nyilvános forrásprojektet Git submodule-ként rögzítjük. Ezzel a pontos commitok visszaállíthatók, a szerzői előzmény és licencek nem vesznek el. A modulok nem automatikusan telepített, konfigurált vagy tesztelt PyGPT bővítmények.

## Rögzített forrásverziók

- `upstream/pygpt`: https://github.com/diablomike20/PyGPT @ `2d8779a983edc73846a640bbbda1dcc7d513d924` (master)
- `upstream/pygpt-addons`: https://github.com/diablomike20/PyGPT_Addons @ `15759ba00cab37622e0b9f5b302c73fc7aa56a50` (master)

## Lekérés és ellenőrzés

```bash
git clone --branch integration/pygpt-addons-baseline https://github.com/diablomike20/Jarvis-2.0.git
git -C Jarvis-2.0 submodule update --init --recursive
git -C Jarvis-2.0/upstream/pygpt rev-parse HEAD
git -C Jarvis-2.0/upstream/pygpt-addons rev-parse HEAD
```

## Szigorú határok

1. `main` és az eredeti upstream repók NEM módosíthatók véletlenül.
2. A PyGPT a P2 elsődleges motor; az Add-ons katalógus csak ellenőrzött, szelektív telepítéssel aktiválható.
3. A Free Claude Code / ai_proxy_2 még nincs bevonva; P3 külön jóváhagyási/tesztelési fázis.
4. Privát forráskód, token, API-kulcs, hangminta, személyes adat **nem** publikálható ebbe a nyilvános repóba.
5. A későbbi GUI-port és JARVIS-specifikus bővítmények csak P5/P6-ban következnek.
6. Git submodule nem egyenlő eredeti forráskód másolásával: a checkout a forrásrepo elérhetőségétől függ. Offline archiváláshoz külön licenc- és adatvédelmi audittal rögzített forráscsomag szükséges.

## Első körös elfogadási feltételek

- Mindkét submodule létezik, URL és commit SHA megfelelő.
- Rekurzív klónozás működik.
- PyGPT környezet létrehozása és Windows-indítása külön mérhető.
- Bővítmény-telepítés, Skill/MCP és regressziós tesztek nincsenek késznek jelölve, amíg nem futottak.

Részletes projektterv: `docs/master-spec-20261016` ág.
