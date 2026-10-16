# 11 — Fejlesztőügynök és új chat átadási protokoll

## A projektgazda kifejezett munkamódja

Minden új fejlesztőchat/ügynöknek az itt dokumentált projekt döntéseivel kell kezdenie. A cél az újratanítás kiküszöbölése: nincs felszínes README-átfutás; alapos forráskódtanulmányozás, függőségek, alternatív utak, korlátok és felelősségi határok.

## Kötelező belépővizsgálat

1. Olvasd a docs ág README és 00–16c fejezeteket; KÜLÖNÖSEN a 16-os Master funkcióspecifikációt, 16a/16b/16c mellékleteket és catalog/feature-registry.v1.json fájlt.
2. Olvasd az integration branch INTEGRATION.md és a .gitmodules adatokat; ellenőrizd az aktuális HEAD-et.
3. Vesd össze a Source Register pinelt SHA-jait a tényleges checkouttal.
4. Olvasd a feladathoz szükséges forrásfájlokat a PyGPT/Addon/FCC/JARVIS repo pontos commitján; ne hivatkozz hozzáférés nélküli állományra.
5. Jegyezd fel a képesség tulajdonosát, a GUI/IPC/process/venv határt, a már kész teszteket és ismert blokkolókat.
6. Tanulmányozd és adaptáld a releváns részeket; ne készíts meg nem mért új implementációt.
7. A végén jelentkezz: mit tanulmányoztál, mi igazolt, mi csak becsült és melyik teszt hiányzik.

## Munkamegosztás

- Minden feladatnak 1 owner, 1 branch és lehetőség szerint dedikált worktree.
- Két agent nem írja ugyanazt a fájlt jóváhagyott koordináció nélkül.
- A párhuzamos Claude/egyéb fejlesztő munkáját ne bontsd, ne merge-öld, ne cherry-pickeld önkényesen.
- main/master/reference soha nem módosul explicit felhasználói döntés nélkül.
- Forrás vendor submodule hash pin; upgrade külön változtatási tétel.
- A PR vagy commit önmagában nem kódparitás bizonyíték.

## Kötelező feladatbrief

~~~text
PROJECT: Jarvis-2.0 / Project Icarus
REPO: https://github.com/diablomike20/Jarvis-2.0
BRANCH: <dedikált ág, main soha>
BASE_SHA: <konkrét>
GOAL: <mérhető cél>
SCOPE: <engedélyezett fájlok és alrendszerek>
DO_NOT_TOUCH: <védett fájlok/repo/branch>
DEPENDENCIES: <pinelt upstream és IPC sémák>
TESTS: <működő parancsok és elvárt bizonyíték>
ACCEPTANCE: <számozott kritérium>
REPORT: <repo SHA, modified files, tests, result, blockers>
~~~

## Státuszjelentés

Ne állíts PASS-t vélelmezésből. Jelentés: módosított fájlok listája, diff stat, branch, base/head, futtatott teszt parancs+exit code+log, megmaradt GAP, licenc/security, user input requiring approval, rollback. A bizonyíthatatlan állapot NOT_RUN/UNKNOWN.

## Tudás folytonossága

A dokumentációs ág a projekt „source of truth” az elfogadott specifikációknak; a kód és teszt eredményének igazsága a megfelelő commitban és tesztlogban él. Ha döntés változik, ADR módosítás új commitban, dátummal és tulajdonossal. A chatben elhangzott új ötlet nem automatikus követelmény.

## Tiltások

- Ne generálj hamis adatot, screenshotot, dummy adatot valósként.
- Ne telepíts át ellenőrizetlen Skills/MCP csomagot globálisan.
- Ne publikálj privát forrás-/hang-/beszélgetés-adatot.
- Ne cseréld le eredeti JARVIS HUD-ot Orb vagy más UI-val felhatalmazás nélkül.
- Ne ígérj készen lévő Windows installert tényleges artifact nélkül.
- Ne állítsd, hogy a P3 FCC/P5 HUD integráció már kész csak mert a docs vagy submodule commit megvan.

## Rövid bootprompt (másolható)

„Te a Project Icarus / JARVIS UNIFIED fejlesztőügynöke vagy. Előbb mélyen tanulmányozd a docs/master-spec-20261016 ág README, 00–16c dokumentumait és a catalog/feature-registry.v1.json fájlt, az integration/pygpt-addons-baseline forrásainak rögzített SHA-it és az aktuális, számodra kijelölt munkaterületet. Ne kapkodj, forráskódból és működési bizonyítékokból dolgozz. A funkciómegőrzés, a JARVIS eredeti HUD, az ágak izolációja, a secrets/voice adatvédelem kötelező. Munkát csak a megadott branch/scope szerint módosíts; a main/master ágakat és más ügynök munkáját ne érintsd. A végén konkrét fájl-, commit-, teszt- és blocker-jelentést adj. Ne állíts teszteletlen funkciót késznek.”
