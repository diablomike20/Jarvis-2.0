# 05 — Modellrouter, Free Claude Code, Puter és no-cost-ai tényalapú összehasonlítása

## Három eltérő fogalom — nem felcserélhető
1. **PyGPT natív provider:** az alkalmazás saját adaptere; hang/kép/videó funkcióra jobban optimalizálható.
2. **FCC ai_proxy_2:** Anthropic/OpenAI Responses kompatibilis gateway, model alias, fallback, coding-agent harness, multi-provider konfiguráció. P3 még nincs integrálva.
3. **Puter.js Free-Claude-AI:** böngészős frontend `puter.ai.chat()` hívással, `puter.com` authentikációval. Nem egységes Python backend és nem helyettesíti az FCC managed CLI/SDK képesítését.

## Puter ár és hozzáférés
A Puter hivatalos szabálya `User-Pays`: minden felhasználó saját ingyenes allowance kerettel indul, és a használat ahhoz a fiókhoz számlázódik; kimerülés után a használat limitált vagy fizetős lehet. A szolgáltató reklámszövegében a fejlesztő infrastruktúrája „free”, de ez nem azonos minden felhasználó korlátlan ingyenes Claude API-jával.
- https://docs.puter.com/user-pays-model/
- https://docs.puter.com/rate-limits-and-quotas/
- https://docs.puter.com/Auth/signIn/
- https://docs.puter.com/supported-platforms/

## zebbern/no-cost-ai
**Forrás:** https://github.com/zebbern/no-cost-ai, MIT, README az elsődleges tartalom, nem futó proxy. A lista >80 ingyenes/belépős/kódoló/média hivatkozást hirdet; köztük webes chat, API/free tier, IDE, video/voice. A repositoryban szereplő „Unlimited” és korábbi modellekre vonatkozó becslések nem garantált aktuális kvóták, nincsenek automatikusan validálva.
JARVIS relevancia: provider-kutatási backlog, költség- és szolgáltatói elérhetőségi tesztlista, NEM kötelező futó komponens.
Kockázat: nem minden listázott weboldal ad legitim programozható API-t, egyes nem hivatalos proxyk security/ToS kérdést vetnek fel.

## FCC választási protokoll
A feladat útvonala: explicit capability → biztonsági/adatvédelmi policy → model/provider cache → cost/credit availability → request/send → stream/tool mapping → result/citation/evidence. Ingyenességi becslést külön `observed_at`, `quota_source`, `verified_for_account`, `requires_signup`, `billing_risk` metaadatokkal tárolunk.

### Modellválasztási követelmény
- Nem hazudunk Claude hozzáférést, ha csak nem támogatott alias van a katalógusban.
- Programozás esetén valódi tool-use/model támogatás és coding agent harness kompatibilitás kell, nem csak chat HTML.
- Magyar STT/TTS és realtime audio külön capability, nem minden LLM gateway biztosítja.
- Tool side effects után fallback modell nem ismételhet meg írási műveletet idempotency/approval nélkül.
- Minden fizetős providerhez explicit user cost cap és fiók-onboarding.
- A Puter browser origin account cookiejait nem exportáljuk automatikusan backendbe.

## FCC ági és licencbeli kétértelműség
A privát `AI-Proxy` (ha használatban van) és a korábbi MIT forrás nem automatikusan a legújabb AGPL-3.0 upstream. Pontos commit/compat API teszt és licencek szükségesek; public JARVIS-ba user private code nem kerül.

## További implementációs backlog
P3: Authenticated provider adapter, live cost-discovery/quotas, current model listing, local test fixture, typed failure, circuit breaker, session cancellation.
P6 optional: Puter webmodul csak szigorú origin/sandbox és világos billing policy mellett.

**Állapot:** statikus forráskutatás, e dokumentum nem aktuális szolgáltatói árajánlat vagy provider-telepítés.
