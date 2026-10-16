# 19 — Ingyenes AI-szolgáltatók és alternatív belépési modellek: ellenőrzési jegyzék

**Állapot:** `RESEARCH_REFERENCE`; nem új kötelező P2/P3 alrendszer, nem hitelesített ingyenes hozzáférési garancia. A JARVIS elsődleges modellroutingja továbbra is a PyGPT natív provider adapter és később a Free Claude Code / ai_proxy_2.

## zebbern/no-cost-ai

**Forrás:** https://github.com/zebbern/no-cost-ai · MIT. A README egy *dinamikusan változó linkgyűjtemény*, nem integrációs motor, nem API proxy és nem egységes authentikációs szolgáltatás.

Az átvizsgált index a regisztráció nélküli, illetve regisztrációhoz kötött chat, média, hang, IDE és API szolgáltatókat kategorizálja, és láthatóan már elavult modellek/korlátok is szerepelnek benne. Az olyan állításokat, mint „unlimited”, „free” vagy „free premium model”, **nem** tekinthetjük szerződéses, korlátlan hozzáférésnek; egyes ismeretlen közvetítők hozzáférés- és adatvédelmi kockázatot jelentenek.

Javasolt felhasználás: alternatív provider jelöltek *felfedezésére*. Minden jelölt előtt: hivatalos tulajdonos, hitelesítési út, saját domain, API TOS, modellnév, támogatott endpoint, adatkezelés, rate limit, teljes költség, elérhető free tier, georegion és főként kódolóügynök-kompatibilitás ellenőrzése. Ismeretlen „free Claude” proxyt alapból nem kapcsolunk JARVIS tokenjeihez vagy saját memóriájához.

## Puter.js-alapú Claude-stílusú HTML-frontendek

A forráskód alapján van olyan korábban tárgyalt, önhostolt webes frontend, amely nem maga az FCC gateway, hanem Puter.js által biztosított felhasználói session és AI API hívásra épít. Az előző vizsgálatban a releváns belépési mechanizmus egy kliensoldali `js.puter.com/v2/` script, `puter.ai.chat(...)`, valamint egy localhost Python statikus szerver volt. **A különböző GitHub-projektek és privát repo neve/azonosítója ebben a nyilvános dokumentumban nem kerül részletezésre.**

Egy Puter autentikációs popup megléte nem önmagában adathalászat-bizonyíték. Biztonsági ellenőrzés nélkül ugyanakkor nem mondható, hogy minden meghívott oldal biztonságos. Ha a login idegen domainre, nem várt jelszókérésre, böngészőkiegészítőre vagy OAuth scope-ra vezet, nincs engedély a jóváhagyására. Hibaforrás lehet popup/third-party cookie tiltás, browser profile, SDK változás, távoli account provider állapot és modellnév elavulása.

### Felhasználóoldali biztonsági eljárás

1. Csak hivatalos, külön ellenőrzött szolgáltatói login-domainen adj meg hitelesítő adatot.
2. Ne gépelj GitHub/Claude/OpenAI-jelszót egy egyedi, ismeretlen „Claude” HTML űrlapba.
3. Ha jelszót adtál meg nem várt oldalon: hivatalos oldalon jelszócsere, MFA, aktív sessionök és kapcsolt app/token engedélyek ellenőrzése.
4. API kulcsokat ne helyezz third-party böngészős frontendbe, amíg az nem auditált; ha kiadtad, rotáld.
5. A szolgáltató free tierjét ne keverd össze a Claude saját API számlázásával, illetve a Free Claude Code proxy funkcióval.

## JARVIS integrációs döntés

- no-cost-ai: `PARKED_RND / RESOURCE_INDEX`
- Puter.js HTML frontend: `NOT_CORE_ENGINE / NO_AUTO_LOGIN / SECURITY_REVIEW_REQUIRED`
- FCC: `P3_COMMITTED_DIRECTION`, külön, hitelesített helyi szolgáltatás, natív PyGPT fallbackkel.
- Project Icarus publikus repositoryba privát account adat, OAuth cache, token, cookie és forrásfájl nem kerülhet.

A fentiek forrás- és funkcióalapú megfigyelések, nem valós szolgáltatóoldali auth-/phishing-forensics tesztek.