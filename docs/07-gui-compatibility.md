# 07 — Eredeti JARVIS/Brahma GUI funkcionális és vizuális paritás

## Kötelező követelmények

Az eredeti JARVIS animáció, stílus, ablakkezelés, interakció és létező funkciók maradjanak meg. Ne legyen automatikus új 3D Orb vagy önkényes újratervezés. A teljes GUI-átállás P5: csak az elfogadott PyGPT+FCC stabil backend után.

## Igazolt forráskülönbség

- Forrás JARVIS: main.py és ui.py PyQt6 használattal, meglévő Brahma háttérlogikával.
- PyGPT: PySide6/Qt, Core és controller gyakran Qt MainWindow függőségű.
- Portolás nem puszta importcsere: Signal/Slot, QThread, QWebEngine, Windows natív ablakzászlók, DPI, átlátszóság, timer, GPU, mikrofon és callback-sorrend.

## Vizsgálati modulok és elfogadási tesztek

| Szegmens | Mérendő / bizonyítandó |
|---|---|
| Indító UI, ablak | hide/show, close/restart, multi-monitor, DPI, always-on-top |
| Eredeti animáció | determinisztikus állapot, frame/screenshot, FPS, időzítési regresszió |
| Érintés/egér/keyboard | hitbox, shortcut, kezelőelemek, navigáció |
| Font/kép/ikon | original asset path, checksum, szerzői jog, megjelenítési azonosság |
| Qt binding | signals, slots, ownership, PyQt→PySide eltérések |
| Qt worker | UI thread és background worker, cancel, megakadástesztek |
| WebEngine | JS bridge, hozzáférési határ, origin, üzenet szerializálás |
| STT / mikrofon | eszközváltás, hiányzó device, push-to-talk |
| TTS / animation sync | idle/listen/think/speak, audio waveform és interrupt |
| PyGPT funkciók elérése | eredeti eszközök, menüpontok és feature-kimenetek |
| Jóváhagyás | mutáció és tool, explicit user approve/deny/timeout |
| Recovery | ablakállapot és folyamatos task állapot crash után |

## P0 és P5 elválasztása

P0: kizárólag izolált minimális PySide6 GUI feasibility teszt — az eredeti HUD-ba nem írunk. P2/P3/P4: PyGPT natív GUI megmarad, és nem akadály a backend stabilizálásában. P5: original JARVIS HUD port, szükség esetén PyGPT Expert GUI fallbackkel.

## Elfogadás

Nem elég a képernyőkép hasonlósága; vizuális, funkcionális, állapot- és negatív teszt. Eltérés GAP-registerben, ownerrel és elfogadási döntéssel. **Még nincs GUI-port elvégezve a célrepóban.**
