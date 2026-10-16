# 04 — A Free-Claude-AI privát repository biztonsági és működési auditja

**Vizsgált repo:** diablomike20/Free-Claude-AI — PRIVÁT. Nem kerül forrásként a nyilvános Jarvis-2.0 repo-ba.
**Vizsgált belső fájlok:** README.md, `unlimited claude/Claude.html`, `unlimited claude/run_server.bat`, LICENSE. 
**Bizonyítottság:** statikus kódelemzés; nincs böngészős bejelentkezés-felvétel, nem rendelkezünk user Puter account audit loggal vagy hálózatcapture-rel. Ebből nem jelenthető ki kategorikusan a biztonság.

## Első megállapítás
Az alkalmazás egy önálló böngészős Puter.js Claude chat UI, nem ugyanaz, mint a fejlettebb Free Claude Code Python `ai_proxy_2` gateway. Nem tárolt új Anthropic API kulcsot, és nem látszik custom jelszó-POST a vizsgált HTML-ben; külső SDK `https://js.puter.com/v2/` látható. Ez nem bizonyítja teljeskörűen, hogy egy bejelentkezési session teljesen biztonságos volt.

## Konkrétan ellenőrzött gyengeségek

### FC-001 — Hibás file:// támogatási állítás
HTML `updateProtocolNotice()` (kb. 821–830. sor) zölddel jelöli a közvetlen fájlról megnyitást: `File mode: Authentication should work perfectly here!`.
**Hivatalos Puter ellenpélda:** https://docs.puter.com/supported-platforms/ és https://docs.puter.com/Auth/signIn/ szerint a file:// `unsupported_origin` — valódi `http://localhost` vagy regisztrált origin kell. Ez tényleges dokumentációs/kód hiba, nem a felhasználó hibája.

### FC-002 — Kézi auth nem auth-függvénnyel történik
`handleManualAuth()` (HTML kb. 837–916. sor): `puter.ai.chat("test",{model:'claude-sonnet-4'})` próbakérés. Valójában működő modell, jogosultság, kvóta és hálózati készség is kell; egy failure az auth hibaüzenettel összemosódhat.
**Javaslat:** felhasználói click eseményben `await puter.auth.signIn()`, majd `puter.auth.isSignedIn()` és `puter.auth.getUser()`, külön `model_check`.

### FC-003 — Modelllista és hibadiagnózis elavulhat
Beégetett: claude-sonnet-4, claude-opus-4, claude-3-7-sonnet (kb. 799–808), nincs listModels/capability discovery. Rossz modell 404/permission/usage-limit esetén is `Authentication failed` felirat jelenhet meg.
**Javaslat:** dinamikus `puter.ai.listModels()` és 4xx/5xx typed error mapping, új/elfogyott modell külön kategória.

### FC-004 — Félrevezető kvóta/ingyenesség
README: `100% Free Access`, Puter ingyenes tier. Hivatalos szolgáltatás **User-Pays**: egy account ingyenes kerettel indul, de modellhasználat metered, túlkeret fizetős is lehet. Hivatalos dokumentáció: https://docs.puter.com/user-pays-model/ és https://docs.puter.com/rate-limits-and-quotas/.
**Javaslat:** aktuális allowance és usage kijelzés, explicit cost cap, modellár és alternatíva; ingyenesség nem garantált.

### FC-005 — Szerver bind és túlzott alapport
`run_server.bat`: `python -m http.server 8000`, amely platformfüggően minden hálózati interfészre köthet. Biztonságosabb: `python -m http.server 8000 --bind 127.0.0.1`; a `localhost` böngészőcím önmagában nem védi a szervert a LAN-tól.

### FC-006 — Nem sandboxolt HTML preview
`createArtifactCanvas()` HTML render funkcióban `window.open(URL.createObjectURL(new Blob([code], {type:'text/html'})))` (kb. 1235–1240. sor). Ez nem megbízható AI-generált HTML-t nyit meg különablakban, sandbox/CSP nélkül. Futtatható script vagy hálózati kérés lehet. Először sandboxos, szigorú CSP-jű iframe és biztonságos originkezelés szükséges.

### FC-007 — Chat história megőrzés és browser scope
A README `localStorage` historyt ígér, de a forrásban vizsgált `recentConversations` tömb csak az adott oldal-élettartam alatt él; a kódrészletek alapján tartós localStorage perzisztencia nem igazolt. Nem szabad biztosan megmaradónak nevezni.

### FC-008 — Az auth hibascript a felhasználót hibáztatja
A login hiba guide automatikusan extension/cookie/browser profilt okolja, miközben a fenti hibák és a szolgáltatói modell-/kvótaválaszok saját kódhibát is okozhatnak. Valódi exception.name/code, origin, console/network ellenőrzés kell.

## A phishing kérdésre alapozott válasz
A megvizsgált statikus HTML-ben egy ismert Puter SDK script látható, saját hitelesítő űrlap-végpont vagy explicit idegen jelszógyűjtő fetch nincs azonosítva. **Ez nem bizonyítja 100%-osan a legitimitást**, mert a Puter SDK és a tényleges böngésző hálózati forgalma runtime környezetfüggő. Ha a jelszót ténylegesen `puter.com` által ellenőrzött hitelesítési oldalon adta meg és a sessiont tiszta böngészőben látjuk, kisebb az adathalászat valószínűsége. Ha idegen domain vagy beágyazott jelszómező volt, azonnali fiókvédelem indokolt.

## Felhasználói hibaelhárítási sorrend
1. Ne kattints újra ismeretlen loginra; nézd meg a hitelesítő popup pontos domainjét és az URL-t.
2. Ne `file://` nyisd meg. Futass lokálisan `python -m http.server 8000 --bind 127.0.0.1`, és `http://localhost:8000/Claude.html` a megfelelő mappából.
3. Először direkt a `puter.com` hivatalos oldalán ellenőrizd a fiókba való belépést; ha valószínűleg kitettél jelszót, változtass jelszót és aktív sessionöket jelentkezz ki.
4. DevTools console és Network: `unsupported_origin`, popup blocked, 401/403 auth, 402 usage, 404 unsupported model, CSP/CORS hibák elkülönítése. Ne ossz meg token/cookie képernyőképet.
5. A programban kézi auth fix: `puter.auth.signIn()`; ezután dinamikus modelllista; a `puter.ai.chat` csak sikeres auth/availability ellenőrzés után.
6. Védett HTML preview; storage/permission policy és secrets scan szükséges.

## Összegzés a Project Icarushoz
A programból ötletek átvehetők (könnyű JS chat, model selection UI, artifact cards), de NEM FCC replacement, nem bizonyított ingyenes modell gateway, és a jelenlegi változatában NEM ajánlott központi JARVIS auth megoldásnak. Állapot: PRIVATE_REFERENCE, LOGIN_BUG_SOURCE_FOUND, RUNTIME_NOT_TESTED.
