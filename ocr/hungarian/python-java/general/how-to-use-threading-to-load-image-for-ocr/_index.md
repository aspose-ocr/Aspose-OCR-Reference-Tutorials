---
category: general
date: 2026-04-26
description: Hogyan használjunk szálakat a kép betöltéséhez OCR-hez Pythonban. Tanulja
  meg az aszinkron OCR feldolgozást visszahívásokkal, háttérszálakkal és képek betöltésével
  néhány lépésben.
draft: false
keywords:
- how to use threading
- load image for OCR
- python threading OCR
- async OCR callback
- background thread image processing
language: hu
og_description: Hogyan használjuk a szálkezelést a kép betöltéséhez OCR-hez Pythonban.
  Ez az útmutató egy teljes, futtatható példát mutat be visszahívásokkal és háttérben
  történő végrehajtással.
og_title: Hogyan használjunk szálkezelést a kép betöltéséhez OCR-hez
tags:
- Python
- Threading
- OCR
- Image Processing
title: Hogyan használjuk a szálkezelést a kép OCR-hez történő betöltéséhez
url: /hu/python-java/general/how-to-use-threading-to-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjunk szálkezelést a kép betöltéséhez OCR-hez

Gondolkodtál már azon, **hogyan használjunk szálkezelést** a kép betöltéséhez OCR-hez anélkül, hogy lefagyna az alkalmazásod? Ez a helyzet bármikor felmerül, akár asztali szkenner, webszolgáltatás vagy egyszerű szkriptet építesz, amely hatalmas képeket dolgoz fel. A jó hír? Néhány Python sor és a megfelelő szálkezelési minta biztosítja, hogy a felhasználói felület gyors maradjon, miközben az OCR motor varázsol.

Ebben az útmutatóban végigvezetünk egy teljes, vég‑től‑végig példán: egy nagy PNG betöltése, OCR indítása egy háttérszálon, és az eredmény kezelése egy visszahívással. A végére nem csak **hogyan használjunk szálkezelést** fogod tudni, hanem azt is, hogy **hogyan töltsünk be képet OCR-hez** tiszta, újrahasználható módon.

## Amire szükséged lesz

- Python 3.9+ (a szintaxis, amit használunk, minden újabb verzión működik)
- `pillow` a képek kezeléséhez (`pip install pillow`)
- `pytesseract` mint egy vékony wrapper a Tesseract OCR körül (`pip install pytesseract`)
- Tesseract OCR motor telepítve a gépedre (letöltés innen [tesseract‑ocr.org](https://github.com/tesseract-ocr/tesseract))
- Egy nagy képfájl, amelyet feldolgozni szeretnél (`large_image.png` ebben az útmutatóban)

Nincs szükség extra keretrendszerekre, nincs async/await—csak a klasszikus `threading` és egy visszahívás.

## 1. lépés: A Threading modul importálása (szükséges a háttérben való végrehajtáshoz)

Az első dolog, amit teszünk, hogy betöltjük a `threading` modult. Ez biztosítja a `Thread` osztályt, amely lehetővé teszi, hogy bármelyik függvényt külön operációs rendszer szálban futtassuk.

```python
import threading
```

*Miért fontos ez*: Ha az OCR-t a fő szálon futtatod, a programod (különösen egy GUI) lefagy, amíg az OCR be nem fejeződik. A munka háttérszálra delegálásával a fő szál szabad marad a felhasználói felület frissítésére, a felhasználói bemenet kezelésére vagy más feladatok indítására.

## 2. lépés: Visszahívás definiálása, amely az OCR befejezésekor meghívódik

A visszahívás egyszerűen egy függvény, amelyet egy másik kódrészlet hív meg, amikor befejeződött. Itt a felismert szöveget fogjuk kiírni, de tárolhatod, elküldheted a hálózaton, vagy frissíthetsz egy UI elemet.

```python
def ocr_done(result_text: str) -> None:
    """Called when the OCR thread finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)   # Display the recognized text
```

*Pro tipp*: Tartsd a visszahívást könnyűnek. A nehéz feldolgozás a visszahíváson belül aláássa a szálkezelés célját, mivel még mindig blokkolja azt a szálat, amely meghívta (gyakran a fő szálat).

## 3. lépés: A feldolgozni kívánt kép betöltése

A kép betöltése külön kérdés az OCR-től, de mégis az egész munkafolyamat része. A Pillow használata ezt egyszerűvé teszi.

```python
from PIL import Image

def load_image(path: str) -> Image.Image:
    """Loads an image from disk and returns a Pillow Image object."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img
    except Exception as exc:
        raise RuntimeError(f"Failed to load image: {exc}") from exc
```

*Miért csináljuk itt*: Ha a kép hatalmas, a fő szálon történő betöltés már most is akadozást okozhat. Sok valós alkalmazásban a betöltést is egy szálra helyezik, de a tisztaság kedvéért szinkronban tartjuk.

## 4. lépés: Kis OCR motor wrapper létrehozása

Az eredeti kódrészlet a `engine.process_async`-t használta. Egy apró osztállyal fogjuk utánzani, amely belsőleg elindít egy szálat, és a megadott visszahívást hívja meg, amikor befejeződött.

```python
import pytesseract

class SimpleOcrEngine:
    """A minimal OCR engine that runs pytesseract in a background thread."""

    def __init__(self, image: Image.Image):
        self.image = image

    def _run_ocr(self, callback):
        """Internal method executed in the worker thread."""
        try:
            # pytesseract returns the recognized text as a plain string
            text = pytesseract.image_to_string(self.image)
            callback(text)
        except Exception as exc:
            callback(f"OCR failed: {exc}")

    def process_async(self, callback):
        """Public method to start OCR on a new thread."""
        worker = threading.Thread(target=self._run_ocr, args=(callback,))
        worker.daemon = True          # Daemon so it won’t block program exit
        worker.start()
        print("OCR thread started…")
```

*Magyarázat*:  
- `_run_ocr` végzi a nehéz munkát.  
- `process_async` létrehoz egy `Thread` objektumot, daemonként jelöli (így az interpreter kiléphet, még ha a szál még fut is), és elindítja.  
- A visszahívás vagy az OCR szöveget, vagy egy hibaüzenetet kap.

## 5. lépés: Minden összekapcsolása és egyéb feladatok végzése az OCR futása közben

Most összehangoljuk az egész folyamatot: betöltjük a képet, példányosítjuk a motort, elindítjuk az aszinkron OCR-t, és a fő szálat más feladattal foglaljuk le (itt csak egy üzenetet írunk ki).

```python
if __name__ == "__main__":
    # 1️⃣ Load the image you want to OCR
    img_path = "YOUR_DIRECTORY/large_image.png"
    image = load_image(img_path)

    # 2️⃣ Create the OCR engine instance
    engine = SimpleOcrEngine(image)

    # 3️⃣ Start OCR on a background thread, passing our callback
    engine.process_async(callback=ocr_done)

    # 4️⃣ Do other work while OCR runs (simulated with a loop)
    for i in range(5):
        print(f"Main thread doing other work… ({i+1}/5)")
        # In a real app you might update a progress bar, handle UI events, etc.
        threading.Event().wait(0.5)  # Sleep 0.5 s without blocking the OS thread

    # Give the OCR thread a moment to finish before the script exits
    threading.Event().wait(2)
    print("Script finished.")
```

**Várható kimenet (rövidítve a tömörség kedvéért):**

```
Image 'YOUR_DIRECTORY/large_image.png' loaded – size: (3840, 2160)
OCR thread started…
Main thread doing other work… (1/5)
Main thread doing other work… (2/5)
...
--- Async OCR finished ---
The quick brown fox jumps over the lazy dog.
Script finished.
```

Ha az OCR hibát jelez, a visszahívás egy hibaüzenetet fog kiírni a szöveg helyett.

---

## Miért működik ez a megközelítés jobban, mint egy egyszerű ciklus

- **Válaszidő**: A fő szál soha nem blokkolódik az OCR hívásnál, amely nagy képek esetén több másodpercet is igénybe vehet.
- **Skálázhatóság**: Több `SimpleOcrEngine` példányt is indíthatsz, mindegyik saját szálon, hogy egy képkészletet párhuzamosan dolgozzon fel.
- **Felelősségek szétválasztása**: A betöltés, a feldolgozás és az eredménykezelés tisztán el vannak választva, így a kód könnyebben tesztelhető és karbantartható.

## Gyakori buktatók és hogyan kerüld el őket

| Buktató | Mi történik | Megoldás |
|---------|--------------|-----|
| Elfelejteni a szál *daemon* jelölését | A szkript lefagy, miután a fő munka befejeződött, mert az OCR szál még él. | Állítsd be `worker.daemon = True` **vagy** `join()` a szálat a kilépés előtt. |
| Globális változó használata az eredményhez zárak nélkül | Versenyhelyzetek adatkorruptiót okozhatnak, ha több szál egyszerre ír. | Add át az eredményt egy visszahíváson keresztül (ahogy mi is tesszük), vagy használj szálbiztos tárolókat, például `queue.Queue`. |
| Masszív kép betöltése a fő szálon | A UI lefagy, mielőtt a háttér OCR elindulna. | A kép betöltését is helyezd szálra, vagy használj lusta betöltési technikákat. |
| Kivételek kezelésének hiánya a munkás szálban | A nem kezelt kivételek csendben leállítják a szálat, és nem kapsz eredményt. | Tekerd be az OCR logikát `try/except`-be, és továbbítsd a hibát a visszahívásnak. |

## Ennek a mintának a kiterjesztése

- **Folyamatjelentés**: Használj megosztott `queue.Queue`-t, hogy az OCR szál köztes százalékos előrehaladást küldjön a fő szálnak.
- **Szálkészlet**: Készletfeldolgozáshoz cseréld le az egyes `Thread` objektumokat egy `concurrent.futures.ThreadPoolExecutor`-ra.
- **GUI integráció**: Tkinter vagy PyQt alkalmazásban ütemezd a visszahívást `after()` (Tkinter) vagy `QTimer.singleShot` (Qt) segítségével, hogy a UI frissítések a fő szálon történjenek.

## Teljes működő példa (másolás‑beillesztés kész)

```python
import threading
from PIL import Image
import pytesseract

def ocr_done(result_text: str) -> None:
    """Callback invoked when OCR finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)

def load_image(path: str) -> Image.Image:
    """Load an image and report its size."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}