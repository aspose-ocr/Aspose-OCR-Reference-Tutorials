---
category: general
date: 2026-06-28
description: Tanulja meg, hogyan ismerjen fel szöveges képet Python OCR segítségével,
  hogyan extraháljon szöveges PNG fájlokat, és hogyan nyomtassa ki a felismert szöveget
  robusztus hiba kezeléssel.
draft: false
keywords:
- recognize text image
- extract text png
- load image ocr
- process image ocr
- print recognized text
language: hu
og_description: Lépésről‑lépésre útmutató a szöveges kép felismeréséhez Pythonban,
  a szöveg PNG formátumban történő kinyeréséhez, és a felismert szöveg biztonságos
  kiírásához.
og_title: Szöveges kép felismerése Python OCR-rel – Teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text image using Python OCR, extract text png
    files, and print recognized text with robust error handling.
  headline: recognize text image with Python OCR – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Szövegkép felismerése Python OCR-rel – Teljes útmutató
url: /hu/python/general/recognize-text-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# szövegkép felismerése Python OCR-rel – Teljes útmutató

Gondolkodtál már azon, hogyan **szövegképet lehet felismerni** egy Python szkriptben anélkül, hogy nehézkes keretrendszert kellene bevetni? Nem vagy egyedül. Sok fejlesztőnek gyors megoldásra van szüksége a *load image OCR* egy képernyőképről, egy beolvasott nyugtáról vagy egy egyszerű PNG‑ről, hogy visszakapja a szöveget.  

Ebben a tutorialban felépítünk egy minimális OCR motorot, csatolunk egy egyedi naplózót, **load image OCR**, futtatjuk a **process image OCR**‑t, és végül **print recognized text**‑et. A végére egy önálló szkriptet kapsz, amely igény szerint **extract text png** fájlokat is képes előállítani.

## Mit fogsz elsajátítani

- Egy teljesen működő Python kódrészlet, amely létrehozza az OCR motort, naplózza minden lépést, és elegánsan kezeli a hibákat.  
- Világos magyarázatok arra, *miért* fontos minden sor – így a kódot könnyen át tudod állítani Tesseract, EasyOCR vagy bármely más háttérmotorra.  
- Tippek a gyakori buktatókhoz (hiányzó betűkészletek, sérült PNG‑k) és azok hibakereséséhez.  

### Előfeltételek

- Python 3.8+ telepítve  
- Egy OCR könyvtár, amely egy `OcrEngine` osztályt biztosít (a példa egy fiktív, de tipikus API‑t használ; cseréld le `pytesseract`‑ra, `easyocr`‑ra stb.).  
- Egy PNG kép, amelyet elemezni szeretnél, `input.png` néven elmentve egy általad irányított mappában.  

> **Pro tipp:** Ha `pytesseract`‑ot használsz, először telepítsd a rendszer‑Tesseract binárisát (`sudo apt install tesseract-ocr` Linuxon), majd futtasd a `pip install pytesseract pillow` parancsot.

---

## ## Szövegkép felismerése: Naplózó beállítása

Egy jó naplózó a háttérhős minden OCR folyamatban. Megmondja, *mikor* indult a motor, *milyen* fájlt nyitott meg, és *miért* lehetett hibás.

```python
# Step 1: Define a simple logger for the OCR engine
def my_logger(level, message):
    """
    level: str – e.g., "INFO", "WARN", "ERROR"
    message: str – human‑readable description of the event
    """
    print(f"[{level}] {message}")
```

*Miért fontos ez:*  
A naplózó leválasztja a diagnosztikai kimenetet az OCR magjától, így egyszerűen átirányítható egy fájlba, egy felügyeleti szolgáltatásba vagy akár egy felhasználói felületre is később.

---

## ## Kép betöltése OCR: A motor PNG‑nek adása

Mielőtt a motor képes lenne **process image OCR**‑ra, szüksége van egy megfelelő képobjektumra. A legtöbb könyvtár elfogad egy Pillow `Image` példányt.

```python
from PIL import Image

# Step 2: Create the OCR engine and attach the logger
ocr_engine = OcrEngine(logging=my_logger)

# Step 3: Load the image to be processed
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Image.from_file(image_path))
my_logger("INFO", f"Loaded image from {image_path}")
```

*Fontos pontok:*  

- **load image ocr** – `Image.from_file` elrejti a PNG dekódolás részleteit.  
- Tartsd az útvonalat konfigurálhatóan; a kódba írt (hard‑coded) útvonal törékennyé teszi a szkriptet.  
- A naplózó hívás megerősíti, hogy a kép sikeresen be lett olvasva, ami akkor hasznos, ha a fájl hiányzik vagy sérült.

---

## ## Process Image OCR: Szöveg felismerése

Most kezdődik a nehéz munka. A motor beolvassa a bitmapet, alkalmazza a neurális hálózatokat vagy heurisztikákat, és egy Unicode karakterláncot ad vissza.

```python
# Step 4: Recognize text from the image
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:
    # Step 5: Handle OCR errors gracefully
    my_logger("ERROR", f"OCR failed with code {e.code}: {e.message}")
    extracted_text = None
```

*Miért csomagoljuk `try/except`‑be:*  
Az OCR összeomolhat alacsony felbontású PNG‑ken, nem támogatott színtereken vagy hiányzó nyelvi adatokon. Az `OcrException` elkapásával csak akkor **print recognized text** hajtasz végre, ha valóban létezik, ezzel elkerülve a felhasználók számára zavaró stack trace‑eket.

---

## ## Print Recognized Text & Extract Text PNG

Ha a felismerés sikeres, megjelenítjük az eredményt, és opcionálisan egy `.txt` fájlba írjuk, amely tükrözi az eredeti PNG nevét.

```python
if extracted_text:
    # Step 6: Print the recognized text
    print("Recognized text:", extracted_text)
    my_logger("INFO", "Printed recognized text to console")

    # Optional: Save extracted text for later use
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
```

*Ami megkapod:*  

- **print recognized text** – azonnali vizuális visszajelzés a terminálban.  
- Egy mellékelt `.txt` fájl, amely hatékonyan **extract text png** a további feldolgozáshoz (keresőindexelés, adatbevitel stb.).

---

## ## Gyakori szélsőséges esetek és megoldások

| Helyzet | Tünet | Megoldás |
|-----------|---------|-----|
| PNG csak szürkeárnyalatos | OCR üres stringet ad vissza | Konvertáld RGB‑re (`Image.convert("RGB")`) mielőtt a motorba adod. |
| A nyelv nem támogatott | `OcrException` kóddal `LANG_NOT_FOUND` | Telepítsd a nyelvi csomagot (pl. `tesseract‑lang‑fra` a francia nyelvhez) és állítsd be `ocr_engine.language = "fra"`. |
| Nagyon nagy kép (> 5 MB) | Lassú felismerés vagy memóriahiba | Kicsinyítsd le `image.thumbnail((2000, 2000))` használatával a `set_image` előtt. |
| Váratlan karakterek | Torlasz kimenet | Győződj meg róla, hogy a kép valóban PNG; egyes fájlok PNG‑nek látszanak, de valójában JPEG‑ek. Használd az `Image.verify()`‑t az ellenőrzéshez. |

---

## ## Teljes működő példa (másolás-beillesztés kész)

```python
# -*- coding: utf-8 -*-
"""
Complete script to recognize text image using a generic OCR engine.
Replace OcrEngine, OcrException with the concrete classes from your library.
"""

from PIL import Image

# ----------------------------------------------------------------------
# 1️⃣  Logger definition
# ----------------------------------------------------------------------
def my_logger(level: str, message: str) -> None:
    """Simple console logger."""
    print(f"[{level}] {message}")

# ----------------------------------------------------------------------
# 2️⃣  Engine creation & image loading
# ----------------------------------------------------------------------
ocr_engine = OcrEngine(logging=my_logger)   # <- adapt to your library

image_path = "YOUR_DIRECTORY/input.png"
try:
    img = Image.open(image_path)
    img.verify()                     # sanity check the PNG
    img = Image.open(image_path)     # reopen after verify
    ocr_engine.set_image(img)
    my_logger("INFO", f"Loaded image from {image_path}")
except Exception as load_err:
    my_logger("ERROR", f"Failed to load image: {load_err}")
    raise SystemExit(1)

# ----------------------------------------------------------------------
# 3️⃣  Text recognition
# ----------------------------------------------------------------------
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:            # replace with actual exception class
    my_logger("ERROR", f"OCR failed ({e.code}): {e.message}")
    extracted_text = None

# ----------------------------------------------------------------------
# 4️⃣  Output handling
# ----------------------------------------------------------------------
if extracted_text:
    print("Recognized text:", extracted_text)          # ✅ print recognized text
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
else:
    my_logger("WARN", "No text extracted; check image quality.")
```

**Várható konzol kimenet (sikeres út):**

```
[INFO] Loaded image from YOUR_DIRECTORY/input.png
[INFO] OCR succeeded
Recognized text: Invoice #12345
Total Amount: $1,250.00
Date: 2026‑06‑01
[INFO] Saved extracted text to YOUR_DIRECTORY/input.txt
```

Ha valami rosszul megy, egy egyértelmű `[ERROR]` sort látsz a okkal, köszönhetően az egyedi naplózónak.

---

## ## Következő lépések és kapcsolódó témák

- **extract text png** tömegekből: csomagold a szkriptet egy `for` ciklusba, amely bejár egy könyvtárfát.  
- **process image ocr** előfeldolgozással (kiegyenesítés, kontraszt növelés) az OpenCV‑vel, mielőtt a motorba adod.  
- Válts felhő alapú OCR szolgáltatásra (Google Vision, Azure Read) az `OcrEngine` implementáció cseréjével – a körülötte lévő kód változatlan marad.  
- Tanuld meg, hogyan **print recognized text** PDF‑ekbe írni a `reportlab` segítségével az automatikus jelentéskészítéshez.  

---

## Következtetés

Most egy kompakt, termelés‑kész módszert mutattunk be a **recognize text image** Pythonban, a PNG betöltésétől a **print recognized text**‑ig és az eredmény mentéséig. Egy apró naplózó beillesztésével, a kivételek kezelésével és az eredmény opcionális mentésével a szkript készen áll a gyors kísérletekre és a nagyobb folyamatokba való integrációra.

Próbáld ki a saját képernyőképeiddel, kísérletezz a kép előfeldolgozással, és hamarosan bármely PNG‑ből ki tudsz nyerni szöveget. Van kérdésed? Hagyj egy megjegyzést – jó OCR‑ozást!  

![szövegkép felismerés példája](placeholder.png)


## Mit tanulj meg legközelebb?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljesen működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Szöveg kinyerése képből Aspose OCR‑rel – Lépésről‑lépésre útmutató](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Kép szövegkivonás végrehajtása streamből Aspose OCR használatával](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Kép konvertálása szöveggé – OCR végrehajtása URL‑ről származó képen](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}