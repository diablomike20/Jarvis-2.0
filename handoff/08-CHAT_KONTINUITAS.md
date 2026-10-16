# 08 — Beszélgetések és fejlesztőügynökök közti tudásfolytonosság

## Miért van erre szükség?
A felhasználó jelezte: a beszélgetés elérte maximális hosszát; nem szeretné minden új fejlesztőchatet újra betanítani a projekt szerepére. Cél a tartós, ellenőrizhető és átolvasható projektállapot Gitben és gépi regiszterekben, nem a chat hosszúságának megkerülése.

## Forrássorrend és tanulmányozási kötelezettség
1. `PROMPT_UJ_CHAT_KOLLEGANAK.txt`.
2. `handoff/README.md`, 01–09, a docs/00–16c, source lock, research lock, feature registry, tests.
3. A régebbi kapcsolódó beszélgetések és feltöltött Jarvis-AI projektexportok **ha jogosultan elérhetők**. A nyers beszélgetések nem minden fejlesztő környezetében hozzáférhetők, ezért az ügynök ne állítsa „minden chatet elolvastam” tényként, ha a rendszer nem ad hozzáférést.
4. Az éppen dolgozott feladathoz tartozó pontos git ref: `integrations`, `sources`, másik agent branch csak read-only.
5. A releváns modul source code, API és függőség, behavior, CI/log; végül tudás-visszamondás konkrét bizonyítékokkal.

## State Capsule (kötelező minden munkamenet záráskor)
`state/current-status.md` és `state/current-status.json` (tervezett lokális, nem létező fájlok). Mezők:
- snapshot ID, timestamp, GitHub repo, branch, base SHA, head SHA;
- active phase P0–P6, aktuális task, owner;
- elfogadott döntések és ADR-ek, tiltások;
- source pins és megváltozott függőségek;
- mi készült el ténylegesen (build/link/log) vs mi csak tervezett;
- felfüggesztett futások, jóváhagyások, privacy és megoldatlan hibák;
- elfogadási teszt ID PASS/FAIL/BLOCKED/NOT_RUN és bizonyíték;
- következő, legkisebb biztonságos lépés, visszaállítási terv;
- AGENT_HANDOFF prompt és olvasott fájllista.

## Egyidejű ügynökök / ágak
Kódfájlhoz egy gazda, munkához külön branch/worktree, akkor is ha párhuzamos ugyanazt a projektet tanulmányozzák. `main` és más ügynök `feature/` ág nem írható user engedély nélkül. PR review és contract tests a két munka közti integráció kapuja. Ne használj automatikus `git reset --hard` vagy globális Skill overwrite.

## Kétszintű „DeepLearn”
**Első szint: projekt-Domain Learn.** Minden dokumentum átolvasása, korábbi döntések, tiltások, architektúra, API ownership, indítási/tesztelési folyamat.
**Második szint: Source Learn.** Pontos kód/fájl, osztályfüggvény, import callgraph, vízszintes modulhatár, negatív teszt és ellenpélda. Csak ezután írható a konkrét feladat fázis- és tesztterve.

A DeepLearn itt alapos elemzést jelent, **nem modell-súlyok valódi finomhangolását** vagy háttérben zajló, nem naplózott önfejlesztést.

## A tudás frissítésének üteme
Minden észlelt új repo/model/Skill a kutatási backlogba kerül. A felhasználó által jóváhagyott változtatás ADR-be, a külön ág kódjába, feature registrybe és tesztmátrixba. Egy chatben kimondott lelkes ötlet nem automatikus kész feature.

## Publikus vs privát chat adat
Minden nyers conversation export személyes/privát információt tartalmazhat. A publikus repóban kizárólag műszaki kivonat, repo commit és nyilvános forrás legyen. A teljes nyers ChatGPT exportot csak jogosult, privát, ellenőrzött tárba lehet másolni.

## Handoff acceptance
Új chat első válasza a konkrétan átolvasott dokumentumokat sorolja, jelöli a jelenlegi phase-t, 5 kiemelt tiltást, 5 kockázatot és a legközelebbi tesztelhető lépést. Ha valamelyik chat/file nem olvasható, kérje a pontos hozzáférést, és ne találjon ki tartalmat.
