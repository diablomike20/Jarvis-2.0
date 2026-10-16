# 00 — Project Icarus / JARVIS UNIFIED — projektalapok

**Dátum:** 2026-10-16. **Állapot:** felhasználói stratégiai irány rögzítve; részletes kivitelezési pontok PROPOSED.

## Mi épül?

Egységes Windows-központú asszisztensplatform, amely megtartja a jelenlegi JARVIS/Brahma eredeti futurisztikus GUI-ját és funkcióit, miközben a PyGPT általános AI-asszisztens- és ügynökrendszerét a PyGPT Add-ons gyűjteménnyel, később a Free Claude Code (ai_proxy_2) szolgáltatói/modell- és coding-agent képességeivel összehozza. Magyar nyelv és saját JARVIS-hang későbbi prioritás.

A jövőbeni modulok: PhotoCraft, LightCraft, FilmCraft, FreeCAD; kutatási opciók: REA, VoiceStudio, IronRAG, AI Memory Vault, Barehands és további felmért projektek.

## A felhasználó sorrendje — kötelezően megőrzendő

1. Központi Jarvis-2.0 repository.
2. PyGPT + szükséges és átvizsgált PyGPT_Addons.
3. Free Claude Code / ai_proxy_2 szelektív szolgáltatás- és agent-integráció.
4. A backend házasításának bizonyítása után eredeti JARVIS/Brahma GUI portolása a PyGPT Qt/Python környezetéhez.
5. Csak a stabil mag után JARVIS-specifikus extrák és polish.
6. Minden szakaszban részletes, visszakereshető dokumentáció és egyértelmű felelősség.

## Funkciómegőrzési szabályok

- Egy eredeti funkció sem törölhető pusztán kényelmi vagy architekturális okból. Ha egy funkció egy ideig nem érhető el az egységes HUD-ból, az explicit GAP-regiszterben szerepel, tervvel és felelőssel.
- A GUI eredeti stílusa/animációja védett; automatikus, külön 3D Orb redesign nincs.
- Az eredeti PyGPT GUI az átmeneti szakaszban opcionális szakértői felületként megmaradhat; az egységes HUD céljának időpontja P5.
- A PyGPT natív provider/vision/audio/image/video integrációit nem szabad automatikusan FCC-n átvezetni, ha az API nem támogatja teljesen a képességet.
- Az együttélő eszközök ne írják felül egymás konfigurációját, memóriáját és feladatgazdáját.

## Nem célok az első körben

- Teljes JARVIS GUI átírása P2 előtt.
- Egyetlen Python-környezet minden natív függőséggel.
- Az összes 30 MCP-szerver API-kulcs nélküli, azonnali engedélyezése.
- Külső Skills-ek kontroll nélküli globális telepítése.
- Az AI önálló, korlátlan repo-írása, deployja, fájltörlése vagy fizetős API-hívása.
- Privát modellek, hangminták, jogvédett filmes tartalom publikálása a nyilvános repositoryba.

## Tulajdonosi modell

- Felhasználó / projektgazda: irányok, változtatási jogosultság, végső döntés, prioritás.
- JARVIS Supervisor: folyamatok életciklusa, naplózás, egészség, jogosultsági kapuk.
- PyGPT: általános agent-feladatirányítás, memória/RAG, eszközbővítmények.
- Free Claude Code: modelleredmény-közvetítés, fallback és coding agent munkamenetek; csak saját hatáskörben.
- GUI: állapotmegjelenítés, mikrofon, jóváhagyás, felhasználói események.
- Skill resolver / registry: célhoz illeszkedő eszköz/Skill kiválasztása ütközésmentesen.

## Kész állapot definíciója

A készség nem commitméret és nem a README állításainak száma. Kész az, ami dokumentált követelmény szerint fut, mérhető, visszaállítható, naplózott, regressziós teszttel igazolt, és nem tesz tönkre korábbi elfogadott képességet.

## Időbecslés értelmezése

Korábbi beszélgetésben: P1/P2 egyszerű forrásbeemelés + kiválasztott alapbővítmények optimistán 1–3 nap, Windows-validálással 3–7 munkanap. Ez becslés, nem elvégzett teszt és nem SLA. A P3/P4 széles funkcióparitása jóval hosszabb lehet.
