---
category: general
date: 2026-06-22
description: Szerezz meg határolódoboz-koordinátákat képekből Python segítségével.
  Tanuld meg, hogyan lehet szöveget kinyerni képből Pythonban az Aspose OCR-rel és
  JSON-parszolással percek alatt.
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: hu
og_description: Szerezze meg a körülhatároló doboz koordinátáit képekből Python használatával.
  Ez az útmutató bemutatja, hogyan lehet szöveget kinyerni képből Pythonban az Aspose
  OCR-rel, és hogyan lehet feldolgozni az elrendezési adatokat.
og_title: Keret koordináták lekérése OCR-ből Pythonban – Teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  headline: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  type: TechArticle
- description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  name: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - An active Aspose.OCR for Python
      license or a free trial (the library works without a license but adds a watermark).
      - `pip install aspose-ocr` (the package name on PyPI). - A sample image called
      `invoice.png` placed in a folder you can reference.'
  - name: 1. Convert Bounding Boxes to Simple Rectangles
    text: 'If your downstream tool expects `(x, y, width, height)` instead of eight
      points, add a helper:'
  - name: 2. Handle Multi‑Page PDFs
    text: 'Aspose OCR can accept PDF streams. Replace the image loading line with:'
  - name: 3. Visualize Bounding Boxes
    text: 'If you want to see the boxes drawn on the original image, use Pillow:'
  type: HowTo
- questions:
  - answer: For large documents, consider streaming the JSON or processing page‑by‑page
      to keep memory usage low.
    question: What if the JSON is huge?
  - answer: Low contrast or handwritten text often trips OCR engines. Pre‑process
      the image (increase contrast, binarize) before feeding it to Aspose.
    question: Why are some words missing?
  - answer: Yes—set `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`
      to receive a `"characters"` array with its own `boundingBox`.
    question: Can I get character‑level coordinates?
  - answer: Absolutely. (0, 0) is the top‑left corner of the image.
    question: Is the coordinate system zero‑based?
  type: FAQPage
tags:
- OCR
- Python
- JSON
- Image Processing
title: Bounding box koordináták lekérése OCR‑ből Pythonban – Teljes útmutató
url: /hu/python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szerezze meg a határoló keret koordinátáit OCR-rel Pythonban – Teljes útmutató

Valaha szüksége volt **határoló keret koordináták** lekérésére minden egyes szóhoz egy beolvasott számlán, de nem tudta, hol kezdje? Ön nem egyedül van. Sok automatizálási projektben meg kell határozni a szöveget egy képen, hogy kiemeljük, elhomályosítsuk vagy továbbadjuk az elemzéseknek. A jó hír? Néhány Python sorral és az Aspose.OCR-rel egyszerre kinyerheti a szöveget **és** a pontos pozícióját.

Ebben az útmutatóban egy gyakorlati példán keresztül mutatjuk be, hogyan **vonhat ki szöveget képből Python‑stílusban**, majd hogyan merülhet el a JSON elrendezési adatokban a határoló keretek kinyeréséhez. Nincs felesleges részlet, csak egy működő szkript, magyarázatok arra, hogy miért fontos minden lépés, és tippek a gyakori buktatók elkerüléséhez.

---

## Amit építeni fog

A guide végére egy kész, futtatható Python szkriptet kap, amely:

1. Betölti a képet (pl. egy számla PNG) az Aspose OCR-be.  
2. Beállítja a motorot, hogy JSON elrendezési információt adjon vissza.  
3. A JSON-t Python szótárba alakítja.  
4. Végigiterál minden felismert szón, kiírva a szöveget **és** a határoló keret koordinátáit.

Emellett megmutatjuk, hogyan lehet a kódot többoldalas PDF-ekhez, különböző képformátumokhoz és egyedi koordináta rendszerekhez igazítani.

### Előfeltételek

- Python 3.8+ telepítve a gépén.  
- Aktív Aspose.OCR for Python licenc vagy ingyenes próba (a könyvtár licenc nélkül is működik, de vízjelet ad hozzá).  
- `pip install aspose-ocr` (a csomag neve a PyPI-n).  
- Egy `invoice.png` nevű mintakép, amelyet egy elérhető mappában helyez el.

Ennyi—nincs nehéz keretrendszer, nincs külső szolgáltatás. Merüljünk bele.

---

## 1. lépés: A szükséges könyvtárak telepítése és importálása

Először győződjön meg róla, hogy az Aspose OCR csomag és a beépített `json` modul elérhető. A `json` modul a Python része, így csak az Aspose telepítésére van szükség.

```bash
pip install aspose-ocr
```

Most importálja őket a szkriptben:

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **Miért fontos:** Az `aspose.ocr` importálása hozzáférést biztosít a nagy teljesítményű OCR motorhoz, míg a `json` lehetővé teszi, hogy a nyers elrendezési karakterláncot natív Python szótárrá alakítsa a könnyű bejárás érdekében.

## 2. lépés: OCR motor létrehozása és a kép betöltése

A motor a folyamat központja. Létrehozza, majd a beolvasni kívánt képre irányítja.

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **Pro tipp:** Cserélje le a `"YOUR_DIRECTORY/invoice.png"`-t egy abszolút vagy relatív útra, amely az Ön tényleges fájljára mutat. Ha a fájl nem található, az Aspose `FileNotFoundError`-t dob, ezért ellenőrizze a helyesírást.

## 3. lépés: A motor beállítása JSON elrendezési adatok kiadására

Az Aspose OCR visszaadhat egyszerű szöveget, csak OCR‑JSON-t vagy egy teljes elrendezési JSON-t, amely tartalmazza a szavak, sorok és akár az egyes karakterek koordinátáit. A **határoló keret koordináták** lekéréséhez a layout JSON‑ra van szükség.

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **Miért JSON?** A JSON nyelvfüggetlen, ember által olvasható, és tisztán leképezhető Python szótárakra. A layout JSON egy `"words"` tömböt tartalmaz, ahol minden bejegyzés a szöveget és egy `boundingBox` nyolc számot (a négy sarokpontot) tárolja.

## 4. lépés: Felismerés futtatása és a nyers JSON karakterlánc lekérése

Most ténylegesen futtatjuk az OCR‑t. A `recognize()` metódus egy `OcrResult` objektumot ad vissza, amelyből kinyerhetjük a JSON karakterláncot.

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

Ha kiírja a `layout_json`‑t, valami ilyesmit fog látni:

```json
{
  "words": [
    {
      "text": "Invoice",
      "boundingBox": [12, 34, 112, 34, 112, 58, 12, 58]
    },
    {
      "text": "#12345",
      "boundingBox": [130, 34, 210, 34, 210, 58, 130, 58]
    }
    // ... more words ...
  ]
}
```

> **Szélsőséges eset:** Néhány kép üres `"words"` tömböt eredményezhet, ha az OCR motor nem tud szöveget detektálni. Ebben az esetben ellenőrizze a kép minőségét (kontraszt, felbontás), mielőtt folytatná.

## 5. lépés: A JSON átalakítása Python szótárrá

A natív Python struktúrákkal való munka sokkal egyszerűbb, mint a karakterláncok manipulálása. Használja a `json.loads()` függvényt a karakterlánc átalakításához.

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

Most a `layout_data["words"]` egy szótárak listája, ahol minden elem egy szót és annak határoló keretét reprezentálja.

## 6. lépés: Szavak iterálása és **határoló keret koordináták** lekérése

Itt a tutorialunk lényege: minden szó végigiterálása, a szöveg kinyerése és a koordináták kiírása. Ez az a pont, ahol **határoló keret koordinátákat** kapunk.

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**Minta kimenet** (a számok a képtől függően változnak):

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **Miért a nyolc pontos formátum?** A négy sarok (bal‑felső, jobb‑felső, jobb‑alsó, bal‑alsó) lehetővé teszi, hogy polygonként körvonalazzuk a szót, még ha a szöveg ferde is. Ha csak egyszerű téglalapra van szükség, kiszámíthatja a `x_min = min(x1, x2, x3, x4)`, `y_min = min(y1, y2, y3, y4)`, `width = max(x…) - x_min`, és `height = max(y…) - y_min` értékeket.

## Opcionális fejlesztések

### 1. Határoló keretek egyszerű téglalapokká konvertálása

Ha a downstream eszköze `(x, y, width, height)` formátumot vár a nyolc pont helyett, adjon hozzá egy segédfüggvényt:

```python
def box_to_rect(box):
    xs = box[0::2]  # extract x coordinates
    ys = box[1::2]  # extract y coordinates
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min, x_max - x_min, y_max - y_min)

for word in layout_data["words"]:
    rect = box_to_rect(word["boundingBox"])
    print(f"'{word['text']}' rectangle {rect}")
```

### 2. Többoldalas PDF-ek kezelése

Az Aspose OCR elfogad PDF stream‑eket. Cserélje le a kép betöltésére szolgáló sort a következőre:

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

Iterálja a `set_page_number`‑t minden oldalra, és gyűjtse a koordinátákat oldalanként.

### 3. Határoló keretek megjelenítése

Ha szeretné látni a kereteket az eredeti képen, használja a Pillow‑t:

```python
from PIL import Image, ImageDraw

img = Image.open("YOUR_DIRECTORY/invoice.png")
draw = ImageDraw.Draw(img)

for word in layout_data["words"]:
    box = word["boundingBox"]
    # Pillow expects a list of tuples [(x1,y1), (x2,y2), ...]
    polygon = [(box[i], box[i+1]) for i in range(0, len(box), 2)]
    draw.line(polygon + [polygon[0]], fill="red", width=2)

img.show()
```

Most piros körvonalakat fog látni minden felismert szó körül – tökéletes hibakereséshez vagy UI rétegekhez.

## Gyakori kérdések és buktatók

- **Mi van, ha a JSON hatalmas?** Nagy dokumentumok esetén fontolja meg a JSON streamelését vagy az oldalankénti feldolgozást a memóriahasználat alacsonyan tartása érdekében.  
- **Miért hiányoznak egyes szavak?** Alacsony kontraszt vagy kézírás gyakran megzavarja az OCR motorokat. Előfeldolgozza a képet (növelje a kontrasztot, binarizálja), mielőtt az Aspose‑nek adná.  
- **Kaphatok karakter‑szintű koordinátákat?** Igen – állítsa be a `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`‑t, hogy egy `"characters"` tömböt kapjon saját `boundingBox`‑szel.  
- **Nulla‑alapú a koordináta rendszer?** Teljesen. (0, 0) a kép bal‑felső sarka.

## Teljes szkript – Kész a másolásra és futtatásra

Az alábbiakban a teljes, futtatható példát találja, amely minden lépést egyesít. Mentse `extract_bboxes.py` néven, és futtassa `python extract_bboxes.py` paranccsal.

```python
import aspose.ocr as ocr
import json

# -------------------------
# 1️⃣ Initialize OCR engine
# -------------------------
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))

# -------------------------------------------------
# 2️⃣ Ask for JSON layout output (contains bounding boxes)
# -------------------------------------------------
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)

# -------------------------
# 3️⃣ Run recognition
# -------------------------
result = engine.recognize()
layout_json = result.get_json()

# -------------------------
# 4️⃣ Parse JSON
# -------------------------
layout_data = json.loads(layout_json)

# -------------------------
# 5️⃣ Helper to turn 8‑point box into rectangle (optional)
# -------------------------
def box_to_rect(box):
    xs = box[0::2]
    ys = box[1::2]
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min


## Mit érdemes következőként tanulni?


Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}