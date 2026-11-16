---
category: general
date: 2026-03-18
description: Végezzen OCR-t a képen, hogy gyorsan kinyerje a szöveget a képből. Tanulja
  meg, hogyan töltsön be képet OCR-hez, hogyan hozza létre az OCR-motort, és hogyan
  javíthatja az OCR pontosságát nyelvi beállításokkal.
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: hu
og_description: Végezzen OCR-t a képen ezzel a részletes útmutatóval. Tanulja meg,
  hogyan töltsön be képet OCR-hez, hozza létre az OCR-motort, és javítsa az OCR pontosságát
  a megbízható szövegkinyerés érdekében.
og_title: OCR végrehajtása képen – Teljes programozási útmutató
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: OCR végrehajtása képen – Lépésről lépésre útmutató
url: /hu/python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR végrehajtása képen – Teljes programozási útmutató

Valaha szükséged volt **perform OCR on image**-ra, de nem tudtad, melyik könyvtárat válaszd, vagy hogyan érj el megbízható eredményeket? Nem vagy egyedül. Ebben az útmutatóban végigvezetünk mindenen, amire szükséged van a **extract text from image** elvégzéséhez, a kép betöltésétől a nyelvi beállítások finomhangolásáig, hogy minden lépésben **improve OCR accuracy**-t érj el.

Bemutatjuk, hogyan **load image for OCR**, hogyan **create OCR engine**, és miért fontos minden beállítás. A végére egy kész‑futásra kész szkriptet kapsz, amely kiírja a felismert szöveget, és megérted az egyes sorok „miértjét” – nincs homályos „lásd a dokumentációt” megoldás. Merüljünk el.

## Amire szükséged lesz

- Python 3.8+ (a kód f‑stringeket és típusjelöléseket használ)
- A hipotetikus `ocr_lib` csomag – telepítsd a `pip install ocr_lib` paranccsal
- Egy kép fájl, amely tiszta, nyomtatott szöveget tartalmaz (pl. `lab_report.png`)
- Egy egyszerű szövegszerkesztő vagy IDE (VS Code, PyCharm, vagy amit csak kedvelsz)

Ha már megvannak ezek, nagyszerű – készen állsz. Ha nem, töltsd le a Pythont a python.org oldalról, és futtasd a pip parancsot; ez csak egy percet vesz igénybe.

![perform OCR on image example](/images/ocr-example.png)

*Alt szöveg: perform OCR on image – mintakimenet, amely a kinyert szöveget mutatja.*

## 1. lépés: Create OCR Engine – Hogyan **create OCR engine** Pythonban

Mielőtt bármilyen felismerés megtörténhet, a könyvtárnak szüksége van egy motor objektumra, amely a konfigurációt és a futási állapotot tárolja. Gondolj a motorra, mint a művelet agyára.

```python
# step_1_create_engine.py
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    """
    Initialize and return a fresh OcrEngine instance.
    Creating the engine once and reusing it is more efficient than
    instantiating it inside a loop.
    """
    engine = OcrEngine()
    return engine
```

**Miért fontos ez:** A motor korai példányosítása lehetővé teszi, hogy később nyelvi beállításokat csatolj, és belső modelleket cache-el a gyorsabb későbbi hívásokhoz.

## 2. lépés: Load Image for OCR – A helyes módja a **load image for OCR**-nak

Most, hogy van egy motorunk, valamit kell adnunk neki olvasásra. A `setImageFromFile` metódus egy fájlrendszer‑útvonalat fogad; az útvonal lehet abszolút vagy relatív a szkript munkakönyvtárához képest.

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**Pro tipp:** Használj abszolút útvonalat vagy `os.path.join`-t, hogy elkerüld a „file not found” meglepetéseket, amikor a szkript másik mappából fut.

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## 3. lépés: Improve OCR Accuracy – **language options** finomhangolása a **improve OCR accuracy** érdekében

Azonnali OCR működik, de a szakterületi szókincs (például laboratóriumi zsargon) gyakran megzavarja. Egy egyedi szótár és egy feketelista használatával csökkentheted a félreolvasásokat, mint például a „0” és az „O” összekeverése.

```python
# step_3_language_options.py
def configure_language(engine: OcrEngine) -> None:
    """
    Set up language options to help the engine recognize domain‑specific terms
    and ignore characters that are frequently misread.
    """
    language_opts = LanguageOptions()
    # Add terms that appear often in laboratory reports
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    # Blacklist characters that cause confusion
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)
```

**Miért segít ez:** A szótár azt mondja az OCR modellnek, hogy a „HPLC” egy érvényes token, megakadályozva, hogy a szót értelmetlen darabokra bontsa. A feketelista azt mondja a modellnek, hogy a kétértelmű szimbólumokat zajként kezelje, ami közvetlenül **improves OCR accuracy**.

## 4. lépés: Perform OCR on Image – A központi **perform OCR on image** hívás

A motor előkészítve és a kép csatolva, itt az ideje a szöveg tényleges felismerésének. Ez a lépés egy `OcrResult` objektumot ad vissza, amelyet lekérdezhetsz nyers szövegért, bizalmi pontszámokért vagy határoló dobozokért.

```python
# step_4_recognize.py
def recognize_text(engine: OcrEngine) -> OcrResult:
    """
    Run the OCR process. This may take a few seconds depending on image size.
    Returns an OcrResult that contains the extracted string and metadata.
    """
    result = engine.recognize()
    return result
```

Ha a kép homályos, alacsonyabb bizalmi számokat látsz az eredményben. Ez jelzés arra, hogy előfeldolgozd a képet (például növeld a kontrasztot), mielőtt a motorhoz adnád.

## 5. lépés: Extract Text from Image – A végső karakterlánc kinyerése

Végül a `OcrResult`-t kérjük a szöveges reprezentációjáért. A `getText()` metódus egy egyszerű szöveges karakterláncot ad vissza, amely készen áll a további feldolgozásra (fájlba mentés, adatbázisba betöltés, stb.).

```python
# step_5_output.py
def print_result(result: OcrResult) -> None:
    """
    Output the recognized text to the console.
    You could also write it to a file with open('output.txt', 'w') …
    """
    extracted = result.getText()
    print("=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===")
```

**Várt kimenet:** Feltételezve, hogy a `lab_report.png` egy egyszerű táblázatot tartalmaz, valami ilyesmit láthatsz:

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

Ez a **extract text from image** rész befejeződött.

## Teljes működő példa – Összeállítás egyben

Az alábbi egyetlen szkript, amely összefűzi az előző szakaszok elemeit. Másold be a `run_ocr.py` fájlba, és futtasd a `python run_ocr.py` parancsot.

```python
# run_ocr.py
import os
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    engine = OcrEngine()
    return engine

def load_image(engine: OcrEngine, image_path: str) -> None:
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")
    engine.setImageFromFile(image_path)

def configure_language(engine: OcrEngine) -> None:
    language_opts = LanguageOptions()
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)

def recognize_text(engine: OcrEngine) -> OcrResult:
    return engine.recognize()

def print_result(result: OcrResult) -> None:
    extracted = result.getText()
    print("\n=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===\n")

def main() -> None:
    # 1️⃣ Create the OCR engine
    ocr_engine = build_engine()

    # 2️⃣ Load the image you want to process
    image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
    load_image(ocr_engine, image_file)

    # 3️⃣ Apply language tweaks to **improve OCR accuracy**
    configure_language(ocr_engine)

    # 4️⃣ **Perform OCR on image** – this is the heavy lifting
    ocr_result = recognize_text(ocr_engine)

    # 5️⃣ **Extract text from image** and show it
    print_result(ocr_result)

if __name__ == "__main__":
    main()
```

### Gyors ellenőrző lista

| ✅ | Elem |
|---|------|
| ✔️ | Motor létrehozva (`create OCR engine`) |
| ✔️ | Kép betöltve (`load image for OCR`) |
| ✔️ | Nyelvi beállítások beállítva (`improve OCR accuracy`) |
| ✔️ | OCR végrehajtva (`perform OCR on image`) |
| ✔️ | Szöveg kinyerve (`extract text from image`) |

Futtasd a szkriptet, és figyeld a konzolt. Ha látod a „OCR Output” blokkot a jelentésed tartalmával, sikeresen **performed OCR on image**-t hajtottál végre.

## Gyakori hibák és elkerülésük módjai

| Probléma | Miért fordul elő | Javítás |
|-------|----------------|-----|
| **Blurry input** | Az OCR modell nem tudja megkülönböztetni a karaktereket | Előfeldolgozás OpenCV-vel: `cv2.GaussianBlur` vagy DPI növelése |
| **Wrong language** | Az alapértelmezett nyelv lehet, hogy nem angol | Hívd meg `engine.setLanguage("eng")`-t a `recognize()` előtt |
| **Missing dictionary terms** | A szakterületi szavak összezavarodnak | Add hozzá őket a `setDictionary` segítségével, ahogy a 3. lépésben látható |
| **Blacklisted characters cause** |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}