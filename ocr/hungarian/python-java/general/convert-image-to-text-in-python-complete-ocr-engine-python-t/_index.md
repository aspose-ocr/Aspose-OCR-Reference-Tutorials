---
category: general
date: 2026-07-05
description: Kép konvertálása szöveggé Python OCR-rel – egy lépésről‑lépésre Python
  OCR példa, amely bemutatja, hogyan lehet szöveget kinyerni a képből és felismerni
  a szöveget jpg-ből.
draft: false
keywords:
- convert image to text
- extract text from image
- python ocr example
- ocr engine python
- recognize text from jpg
language: hu
og_description: Képet szöveggé alakít Python OCR segítségével. Kövesd ezt a Python
  OCR példát, hogy percek alatt szöveget nyerj ki a képből, és felismerd a jpg-ben
  lévő szöveget.
og_title: Kép szöveggé alakítása Pythonban – Teljes OCR motor útmutató
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert image to text with Python OCR – a step‑by‑step python ocr example
    that shows how to extract text from image and recognize text from jpg.
  headline: Convert Image to Text in Python – Complete OCR Engine Python Tutorial
  type: TechArticle
tags:
- ocr
- python
- image-processing
- text-extraction
title: Kép szöveggé konvertálása Pythonban – Teljes OCR motor Python oktató.
url: /hu/python-java/general/convert-image-to-text-in-python-complete-ocr-engine-python-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép szöveggé konvertálása Pythonban – Teljes OCR motor Python oktatóanyag

Valaha is szükséged volt **képet szöveggé konvertálni**, de nem tudtad, melyik könyvtárra bízhatsz? Nem vagy egyedül – sok fejlesztő szembesül ezzel a problémával, amikor először próbál karaktereket kinyerni egy beolvasott nyugtából vagy egy táblára készült fényképből. A jó hír? A Python OCR ökoszisztémája szinte fájdalommentessé teszi a feladatot.

Ebben a **python ocr example**‑ben egy valós helyzetet dolgozunk fel: van egy JPEG fájlod, amely cirill betűket tartalmaz, és megbízhatóan szeretnéd **képből szöveget kinyerni**. A végére megtanulod, hogyan **ismerd fel a szöveget jpg‑ből**, miért fontos minden egyes lépés, és hogyan adaptálhatod a kódot más nyelvek vagy képtípusok esetén.

## Amire szükséged lesz

Mielőtt belevágnánk, győződj meg róla, hogy a következők rendelkezésedre állnak:

* Python 3.8+ telepítve (a legújabb stabil kiadás a legjobb).
* Működő internetkapcsolat az OCR csomag telepítéséhez.
* Egy képfájl (pl. `cyrillic_sample.jpg`), amely a kinyerni kívánt szöveget tartalmazza.
* Opcionálisan, de hasznos: egy virtuális környezet a függőségek rendezett kezelése érdekében.

Nincsenek nehéz operációs rendszer‑szintű függőségek, nincs rejtett build eszköz – csak néhány pip parancs és néhány sor kód.

## 1. lépés: Telepítsd az OCR motor Python csomagját

Az első dolog, amit meg kell tenned, hogy beszerezz egy OCR motort, amely jól működik Pythonban. Ehhez a bemutatóhoz a fiktív `ocr` csomagot használjuk, mivel API‑ja sok valós könyvtárra (például `pytesseract` vagy `easyocr`) emlékeztet. Telepítsd a következővel:

```bash
pip install ocr
```

> **Miért fontos ez a lépés:** A csomag telepítése letölti a natív binárisokat és a nyelvi adatfájlokat, amelyek ténylegesen elvégzik a nehéz munkát. Ha kihagyod, már a `import ocr` sor futtatásakor `ImportError` jön elő.

## 2. lépés: Modulok importálása és a környezet beállítása

Miután a könyvtár a gépeden van, importáld a szükséges részeket. Emellett konfigurálunk egy naplózást, hogy lásd, mit csinál a motor a háttérben – ez hasznos, amikor később **képből szöveget nyersz ki** olyan fájlokból, amelyek nem tökéletesen tiszták.

```python
import ocr
import logging

# Enable debug output (optional but recommended for first runs)
logging.basicConfig(level=logging.INFO)
```

> **Pro tipp:** Ha Jupyter notebookban dolgozol, állítsd be a `logging.getLogger().setLevel(logging.DEBUG)`‑t, hogy még részletesebb információkat kapj.

## 3. lépés: OCR motor példány létrehozása

Az motor létrehozása a **ocr engine python** munkafolyamatának sarokköve. Olyan, mintha felkapcsolnád a lámpákat egy sötét szobában; nélküle a további lépések semmit sem látnak.

```python
# Step 3: Instantiate the OCR engine
ocr_engine = ocr.OcrEngine()
```

> **Miért kulcsfontosságú ez a lépés:** Az `OcrEngine` objektum tárolja a konfigurációt, például a nyelvi csomagokat, előfeldolgozási beállításokat és a hardveres gyorsítási flag‑eket. Bármelyik módosítása később hatással lesz az összes további felismerésre.

## 4. lépés: A megfelelő nyelv kiválasztása – Cirill támogatás

Ha cirill szöveggel dolgozol (vagy bármilyen nem latin írással), meg kell mondanod a motornak, melyik nyelvi modellt töltse be. Ellenkező esetben torz kimenetet vagy akár üres stringet kapsz.

```python
# Step 4: Set language to Cyrillic (enables Cyrillic block support)
ocr_engine.language = ocr.Language.CYRILLIC
```

> **Szélsőséges eset:** Egyes motorok külön igénylik a nyelvi adatok letöltését. Ha `LanguageDataNotFound` hibát látsz, futtasd a `ocr.download_language('CYRILLIC')` parancsot, mielőtt beállítod a nyelvet.

## 5. lépés: Töltsd be a képet, amelyből szöveget szeretnél konvertálni

Itt kezdődik ténylegesen a **képet szöveggé konvertálás** folyamata. Az OCR motor egy `Image` objektummal dolgozik, nem közvetlenül egy fájlúttal, ezért először be kell csomagolni a JPEG‑et.

```python
# Step 5: Load the image containing the text
cyrillic_image = ocr.Image.load("YOUR_DIRECTORY/cyrillic_sample.jpg")
```

> **Miért számít:** A kép betöltése lehetővé teszi a motor számára, hogy megvizsgálja a méreteket, a színmélységet és a DPI‑t. Ezek a tulajdonságok befolyásolják, mennyire jól tudja a motor **szöveget felismerni jpg‑ből**.

## 6. lépés: Szöveg felismerése – A Python OCR példa magja

Most végre megkérjük a motort, hogy azt tegye, amire készült: pixeleket karakterekké alakítson. A `recognize` metódus egy eredményobjektust ad vissza, amely tartalmazza a kinyert szöveget, a biztonsági pontszámokat és a határoló dobozokat.

```python
# Step 6: Run OCR and capture the result
ocr_result = ocr_engine.recognize(cyrillic_image)
```

> **Mit kapsz vissza:** `ocr_result.text` egy egyszerű Python string, amely megőrzi a sortöréseket. Ha szó‑szintű pozíciókra van szükséged, nézd meg az `ocr_result.boxes`‑t.

## 7. lépés: A felismert szöveg kiírása – Ellenőrizd a **képet szöveggé konvertálás** sikerét

A legegyszerűbb módja annak, hogy lásd, sikerült‑e **képet szöveggé konvertálni**, a eredmény kiírása. Egy valódi alkalmazásban valószínűleg adatbázisba vagy szövegfájlba írnád.

```python
# Step 7: Print the extracted text
print("=== OCR OUTPUT ===")
print(ocr_result.text)
```

### Várt kimenet

Feltételezve, hogy a `cyrillic_sample.jpg` a „Привет, мир!” kifejezést tartalmazza, a konzolon a következő jelenik meg:

```
=== OCR OUTPUT ===
Привет, мир!
```

Ha a kimenet üres vagy értelmetlen, ellenőrizd a nyelvi beállítást és a kép minőségét. Elmosódott képek vagy alacsony kontraszt gyakran rossz **képből szöveget nyer** eredményeket okoznak.

## Gyakori hibák kezelése

| Probléma | Miért fordul elő | Gyors megoldás |
|----------|------------------|----------------|
| **Üres string** | A nyelvi modell nincs betöltve vagy a kép túl sötét | Győződj meg róla, hogy `ocr_engine.language` megfelel a betűtípusnak; növeld a kép kontrasztját az `ocr.Image.adjust_contrast()`‑el |
| **Hibás karakterek** | Rossz nyelv vagy vegyes írásrendszerek | Állítsd be `ocr_engine.language = ocr.Language.MULTI`‑t vagy futtass két átfutást (Latin, majd Cirill) |
| **Lassú teljesítmény nagy kötegek esetén** | A motor sorban dolgozza fel a képeket | Engedélyezd a több szálas feldolgozást: `ocr_engine.set_threads(4)` |
| **Memóriaszivárgás** | A kép erőforrásai nincsenek felszabadítva | Hívd meg a `cyrillic_image.close()`‑t a felismerés után |

> **Pro tipp:** Tömeges feldolgozásnál tedd a felismerési ciklust egy `try/except` blokkba, hogy elkapd az esetleges `ocr.EngineError` kivételeket anélkül, hogy az egész feladat leállna.

## A példa kibővítése – JPEG‑től PDF‑ekig, Cirill‑tól többnyelvűig

Az a minta, amelyet a **képet szöveggé konvertálás** során követtünk, bármilyen raszteres formátumra alkalmazható: PNG, BMP, TIFF, sőt beolvasott PDF‑ekre is (előbb a lapot képpé kell konvertálni). Ha több nyelvet tartalmazó **képből szöveget nyersz ki**, átadhatsz egy listát:

```python
ocr_engine.language = [ocr.Language.CYRILLIC, ocr.Language.ENGLISH]
```

És ha nagy felbontású okostelefonos fotókkal dolgozol, érdemes egy előfeldolgozó lépést beiktatni:

```python
# Denoise and binarize for better OCR accuracy
clean_image = cyrillic_image.filter(ocr.Filter.GAUSSIAN_BLUR, radius=1)
clean_image = clean_image.binarize(threshold=127)
ocr_result = ocr_engine.recognize(clean_image)
```

Ezek a finomhangolások gyakran egy közepes **python ocr example**‑t produkció‑szintű kóddá változtatnak.

## Teljes működő szkript

Az alábbiakban a kész, futtatható szkriptet találod, amely egyesíti az összes lépést. Mentsd `convert_image_to_text.py` néven, majd futtasd a `python convert_image_to_text.py` paranccsal.



## Mit érdemes még tanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}