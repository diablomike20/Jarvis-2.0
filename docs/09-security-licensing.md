# 09 — Threat model, licencek, titkos adatok és munkakörnyezeti védelem

**Állapot:** megvalósítási követelmény, nem biztonsági tanúsítvány.

## Miért kritikus?

A projekt egyszerre adhat fájlhozzáférést, rendszerparancsot, kódolóügynököket, böngészőt, MCP-t, GitHubot, hangos jóváhagyást, privát személyes memóriát és fizetős modelleket egyetlen felülethez. Egy rossz tool-specifikáció vagy prompt injection egyszerre sok hozzáférést veszélyeztet.

## Fenyegetési felületek

| Felület | Lehetséges probléma | Minimum védelem |
|---|---|---|
| FCC HTTP gateway | LAN elérés, nem hitelesített admin | 127.0.0.1, random auth, per-scope authz |
| MCP npx/uvx/Docker | supply-chain, latest package | pin, audit, isolated runtime |
| GitHub/FS plugin | nem szándékos push, overwrite, delete | workspace allowlist, human approval, diff |
| Agent shell/code interpreter | host károsítás, titok exfil | sandbox + account isolation |
| Browser/web retrieval | untrusted prompt injection | content trust boundary, output validation |
| Tool callback | felülírt user approval, fake session | signed short-lived approval + no bypass |
| SSE/event broker | stale task result, unauthorized events | actor signature, sequence, correlation |
| Memory/RAG | személyes adatszivárgás, adatkeveredés | tenant/workspace scoping, encryption |
| Voice | téves vagy távoli hangos jóváhagyás | confirmation exact action, separate user gesture kritikus műveletnél |
| Backup/logs | API key, hangminta, privát útvonal | scrub, encryption, retention control |
| Add-on | arbitrary in-process Qt/Python execution | manual review és restricted install |
| Repo main | több agent véletlen merge konfliktusa | branch ownership, no default writes |

## Minimum biztonsági profil

- Az összes belső szolgáltatás localhost-only, explicit authentikáció, nincs alapértelmezett statikus token.
- A Python app és az FCC külön venv/processz, lehetőség szerint külön OS user/ACL.
- Eszközök read-only alapeset, minden write külön scope és approval.
- Nem kezelt /root, teljes home vagy Desktop wildcards alapértelmezett file accessként.
- Tool inputok típusosan validálva, env token nem kerül sem promptba, sem naplóba.
- Insecure permissive PyGPT és FCC alapbeállításokat launch preflight blokkolja.
- Plugin és skill telepítő script nem módosíthat globális ~/.claude vagy ~/.agents skill fákat explicit jóváhagyás nélkül.
- Test data kizárólag dummy credential, izolált repo és szintetikus dokumentum.

## Licenc- és attribúciómátrix

- PyGPT eredeti upstream MIT jelzés; a felhasználói repo API SPDX NOASSERTION: pontos LICENSE/NOTICE vizsgálat kell.
- PyGPT_Addons MIT katalógus; egyes külső bővítmények eltérő licencekkel.
- Free Claude Code korábbi fork MIT; új upstream AGPL-3.0-only: nem egyszerűen csereszabatos.
- VoiceStudio AGPL-3.0, egyes TTS modellek önálló nem kereskedelmi vagy egyéb korlátozott licenccel.
- IronRAG és REA MIT jelzés; külső eszközök (Ghidra, Hopper, IDA stb.) külön feltételek.
- Fullstack Agent, Backtalk, AI Visualizer és Barehands AGPL-3.0-or-later; AI Memory Vault CC BY-SA-4.0.
- Kódrészlet közvetlen összevonására lehet más licenchatás, mint protokollon át külön folyamatból való használatra. Külön jogi audit szükséges terjesztésnél/szolgáltatásnál.

## Public/Private boundary

A Jarvis-2.0 jelenleg nyilvános. Nem írható bele:
- privát AI-Proxy teljes forrása vagy konfigurációja előzetes tartalomfelülvizsgálat nélkül,
- nyers korábbi teljes ChatGPT-beszélgetés vagy személyes profil,
- jogosultsági kulcs, hozzáférési token, .env, cookie, session,
- jogosultságilag nem ellenőrzött JARVIS-hang referencia, filmhangsáv vagy felvétel,
- licencileg nem tisztázott vagy nagyméretű bináris letöltés.

A migráció során a technikai **összefoglalók** kerültek nyilvános ágra; a nyers projekt TXT-export nem. Egy privát forrásról még annak pontos branch/commit adata sem szükséges nyilvános indexbe.

## Release kapu

Security checklist PASS, license manifest és SBOM, dependency/vulnerability scan, api auth negative tests, sandbox breakout attempts, rollback és secret-scan. A sikeres Git commit önmagában nem PASS.
