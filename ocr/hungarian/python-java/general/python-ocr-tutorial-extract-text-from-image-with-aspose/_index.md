---
category: general
date: 2026-03-26
description: 'Python OCR oktatóanyag: tanulja meg, hogyan lehet szöveget kinyerni
  képből, betölteni a képet OCR-hez, és felismerni a nyugtán lévő szöveget az Aspose
  OCR használatával néhány lépésben.'
draft: false
keywords:
- python ocr tutorial
- extract text from image
- load image for ocr
- perform ocr in python
- recognize text from receipt
language: hu
og_description: 'Python OCR oktatóanyag: gyorsan megtanulhatod, hogyan vonj ki szöveget
  képből, tölts be képet OCR-hez, és ismerd fel a számla szövegét az Aspise OCR-rel.'
og_title: Python OCR útmutató – Szöveg kinyerése képből
tags:
- OCR
- Aspose
- Python
title: Python OCR útmutató – Szöveg kinyerése képből az Aspose segítségével
url: /hu/python-java/general/python-ocr-tutorial-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR tutorial – Kép szövegének kinyerése Aspose-szal

Valaha is elgondolkodtál azon, hogyan lehet kinyerni a szöveget egy homályos nyugtából vagy egy beolvasott űrlapról anélkül, hogy órákat töltenél egyedi reguláris kifejezések írásával? Nem vagy egyedül. Ebben a **python ocr tutorial** bemutatóban végigvezetünk a kép betöltésén OCR-hez, az OCR végrehajtásán Pythonban, és végül a nyugta fájlok szövegének felismerésén az Aspose OCR könyvtár segítségével.  

A útmutató végére egy kész‑használatra szánt szkriptet kapsz, amely bármely támogatott képformátumot beolvas, kinyeri a szöveges tartalmat, és kiírja a konzolra. Nincs külső szolgáltatás, nincs API kulcs – csak tiszta Python és egy erőteljes OCR motor.  

## Amire szükséged lesz

- Python 3.8 vagy újabb (a kód típusjelöléseket használ, ezért a legújabb interpreter a legjobb)
- `asposeocrjava` csomag telepítve a `pip install aspose-ocr` paranccsal
- Egy minta kép – például a `receipt_noisy.jpg`, amely egy tipikus bolt nyugtát tartalmaz
- (Opcionális) Egy virtuális környezet a függőségek rendezett tartásához

Ha ezek a pontok rendben vannak, ugrhatunk is a kódba.  

## 1. lépés: Aspose OCR osztályok telepítése és importálása

Először is győződj meg róla, hogy az Aspose OCR csomag elérhető. Ezután importáld a szükséges osztályokat.

```python
# Install the package (run once)
# pip install aspose-ocr

# Import the required Aspose OCR modules
import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult
```

**Miért fontos:** Csak a szükséges szimbólumok importálása tisztán tartja a névtér­et, és jelzi az interpreternek, melyik könyvtár részeit használjuk valójában. Emellett rövidíti a későbbi kódsorokat, így a bemutató könnyebben követhető.

> **Pro tipp:** Ha Jupyter notebook-ot használsz, tedd a telepítő sor elé a `!` jelet, hogy cellában fusson.

## 2. lépés: OCR motor létrehozása és Deep‑Learning mód engedélyezése

Az Aspose több motor módot kínál. A legtöbb valós nyugta esetén a deep‑learning modell a legmagasabb pontosságot biztosítja, különösen a zajos beolvasásoknál.

```python
# Initialise the OCR engine
ocr_engine = OcrEngine()

# Switch to deep‑learning mode for better accuracy on complex images
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
```

**Miért deep‑learning?** A hagyományos szabály‑alapú OCR elakadhat alacsony kontrasztú vagy torz karaktereknél. A deep‑learning modell, amely milliók glyph-jein lett betanítva, jobban alkalmazkodik a változatossághoz – pontosan amire szükséged van, amikor *OCR-t végzel Pythonban* telefonkamerával készített nyugtákon.

## 3. lépés: Kép betöltése OCR-hez

Most már ténylegesen **betöltjük a képet OCR-hez**. Az Aspose.Imaging támogatja a PNG, JPEG, BMP, TIFF és további formátumokat, így gyakorlatilag bármely dokumentumképre rámutathatsz.

```python
# Load the image (replace the path with your own file)
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/receipt_noisy.jpg")

# Attach the image to the OCR engine
ocr_engine.set_image(input_image)
```

**Gyakori hibaforrás:** Ha elfelejted beállítani a képet a motoron, `NullReferenceException` keletkezik futásidőben. Mindig hívd meg a `set_image`-t a fájl betöltése után.

## 4. lépés: OCR végrehajtása és szöveg kinyerése

Miután a motor elő van készítve és a kép csatolva van, végre **végrehajthatjuk az OCR-t Pythonban**, és lekérhetjük a szöveges eredményt.

```python
# Run the recognition process
ocr_result: OcrResult = ocr_engine.recognize()

# Extract plain text from the result object
recognized_text = ocr_result.get_text()
```

A `recognize()` metódus egy `OcrResult` objektumot ad vissza, amely nem csak a nyers szöveget, hanem a megbízhatósági pontszámokat, a kereteket és a nyelvi információkat is tartalmazza. Egy gyors **szöveg kinyerése képből** esetén csak a `get_text()`-ra van szükségünk.

## 5. lépés: Felismert szöveg megjelenítése

Nézzük meg, mit olvasott valójában a motor a nyugtáról.

```python
print("Recognized text:\n", recognized_text)
```

A tipikus kimenet így néz ki:

```
Recognized text:
   Store XYZ
   04/26/2026  14:32
   Item A   2.99
   Item B   5.49
   TOTAL    8.48
   THANK YOU!
```

Ha a kimenet torz karaktereket tartalmaz, gondolj a kép előfeldolgozására (pl. kontraszt növelése vagy dőléskorrekció szűrő alkalmazása) mielőtt betöltenéd az OCR motorba. Az Aspose.Imaging teljes képfeljavító eszközkészletet kínál, amelyet láncolhatsz.

## Szélsőséges esetek kezelése és tippek a pontosság javításához

### 1. Nagyon zajos nyugták kezelése
Ha a nyugta erősen elmosódott, érdemes lehet átváltani a `OcrEngineMode.HIGH_SPEED` módra a gyorsabb, bár kevésbé pontos átfutáshoz, majd egy második átfutást futtatni `DEEP_LEARNING` módban a tisztított képen.

```python
ocr_engine.set_engine_mode(OcrEngineMode.HIGH_SPEED)
# ... run first pass, then...
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
# ... run second pass on the same image
```

### 2. Nyelv megadása
Alapértelmezés szerint az Aspose megpróbálja automatikusan felismerni a nyelvet. Angol nyugták esetén rögzítheted a nyelvet:

```python
ocr_engine.set_language("eng")
```

### 3. Memóriakezelés
Sok kép feldolgozásakor egy ciklusban, explicit módon szabadítsd fel az erőforrásokat:

```python
input_image.dispose()
ocr_engine.dispose()
```

### 4. OCR eredmények fájlba mentése
Néha szükség van a kinyert szöveg későbbi elemzéshez való megőrzésére.

```python
with open("receipt_output.txt", "w", encoding="utf-8") as f:
    f.write(recognized_text)
```

## Teljes működő példa

Az alábbiakban a teljes szkript látható, amely mindent összekapcsol. Másold be egy `receipt_ocr.py` nevű fájlba, állítsd be a kép útvonalát, és futtasd a `python receipt_ocr.py` parancsot.

```python
# receipt_ocr.py
# -------------------------------------------------
# Complete Python OCR tutorial using Aspose OCR
# -------------------------------------------------

# 1️⃣ Install the package (run once):
# pip install aspose-ocr

import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult

def main():
    # 2️⃣ Initialise engine in deep‑learning mode
    engine = OcrEngine()
    engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)

    # 3️⃣ Load your receipt image
    image_path = "YOUR_DIRECTORY/receipt_noisy.jpg"   # <-- change this
    img = ocr.Imaging.Image.load(image_path)
    engine.set_image(img)

    # 4️⃣ Recognise text
    result: OcrResult = engine.recognize()
    text = result.get_text()

    # 5️⃣ Output the result
    print("=== Recognized text from receipt ===")
    print(text)

    # Optional: write to a file
    with open("receipt_output.txt", "w", encoding="utf-8") as out_file:
        out_file.write(text)

    # Clean up resources
    img.dispose()
    engine.dispose()

if __name__ == "__main__":
    main()
```

A szkript futtatása meg kell, hogy jelenítse a nyugta tartalmát a konzolon, és létrehozza a `receipt_output.txt` fájlt ugyanazzal az adatával.

![Python OCR tutorial – mintaszámla kimenet](https://example.com/receipt_output.png "python ocr tutorial példa")

*Kép alternatív szövege:* **python ocr tutorial – mintaszámla kimenet**

## Összefoglalás és következő lépések

Most egy **python ocr tutorial**-t vettünk át, amely bemutatja, hogyan **töltsünk be képet OCR-hez**, **végezzünk OCR-t Pythonban**, és végül **ismerjük fel a szöveget nyugta** fájlokból az Aspose használatával. A fő tanulságok:

- Válaszd ki a megfelelő motor módot (deep‑learning a pontosságért)
- Mindig csatold a képet a `recognize()` hívása előtt
- Használd az `OcrResult` objektumot a tiszta szöveg kinyeréséhez, majd tárold vagy dolgozd fel igény szerint

Mi a következő? Gondolj az Aspose Imaging szűrők láncolására az alacsony kontrasztú beolvasások javításához, vagy integráld a szkriptet egy Flask API-ba, hogy nyugtákat tölthess fel egy webes űrlapon keresztül. Emellett érdemes lehet az OCR adatokat CSV-be exportálni a könyvelési automatizáláshoz.

Van kérdésed a többoldalas PDF-ek vagy a nem latin betűk kezelésével kapcsolatban? Hagyj megjegyzést – szívesen segítek!  

**Készen állsz a dokumentumautomatizálás szintjének emelésére?** Szerezd be a kódot, kísérletezz különböző képekkel, és hagyd, hogy az OCR motor végezze a nehéz munkát. Boldog kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}