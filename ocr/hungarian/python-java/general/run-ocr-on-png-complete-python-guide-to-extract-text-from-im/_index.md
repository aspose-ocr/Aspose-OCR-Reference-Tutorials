---
category: general
date: 2026-01-12
description: Futtass OCR-t PNG fájlokon gyorsan Python segítségével. Tanuld meg, hogyan
  nyerhetsz ki szöveget képből és számlából, valamint hogyan tölthetsz be képet OCR-hez
  az Aspose.OCR használatával.
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: hu
og_description: Futtass OCR-t PNG-n azonnal. Ez az útmutató megmutatja, hogyan lehet
  szöveget kinyerni képből és számlából, betölteni a képet OCR-hez, és az eredményeket
  JSON és CSV formátumban menteni.
og_title: OCR futtatása PNG-n – Teljes Python oktató
tags:
- OCR
- Python
- Image Processing
title: OCR futtatása PNG-n – Teljes Python útmutató a képek szövegének kinyeréséhez
url: /hu/python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR futtatása PNG-n – Teljes Python útmutató a képek szövegének kinyeréséhez

Valaha szükséged volt **OCR futtatására PNG** fájlokon, de nem tudtad, melyik könyvtár adna tiszta, strukturált eredményeket? Nem vagy egyedül. Sok valós projektben—gondolj számlázási automatizálásra vagy nyugták beolvasására—a első lépés a **szöveg kinyerése a képből** fájlokból, és a PNG egy gyakori formátum, mert veszteségmentes minőséget őriz.

Ebben az útmutatóban egy gyakorlati példán keresztül mutatjuk be az Aspose.OCR Python csomagot. A végére tudni fogod, hogyan **tölts be képet OCR-hez**, hogyan nyerd ki a szöveg minden sorát, hogyan alakítsd az adatot egy rendezett JSON objektummá, és még CSV-be is exportáld a további feldolgozáshoz. Felesleges szócséplés nélkül, csak egy gyakorlati, azonnal futtatható megoldás.

## Amit megtanulsz

- Hogyan telepítsd és importáld az Aspose.OCR könyvtárat.  
- A pontos lépések a **OCR futtatásához PNG-n** és az eredményobjektum kezeléséhez.  
- Módszerek a **szöveg kinyerésére számlákból** és a kimenet formázása JSON vagy CSV formátumban.  
- Tippek alacsony kontrasztú képek, többnyelvű dokumentumok és a megbízhatósági pontszámok kezeléséhez.  
- Egy teljes, másolás‑beillesztéses kódminta, amelyet már ma futtathatsz.  

> **Előfeltétel:** Python 3.8+ és alapvető ismeretek a pip‑ről. Ha még soha nem használtad az Aspose‑t, ne aggódj—ez az útmutató mindent lefed, amire a kezdéshez szükséged van.

## 1. lépés – Aspose.OCR telepítése és a környezet előkészítése

Mielőtt **OCR‑t futtathatnánk PNG-n**, a könyvtárnak telepítve kell lennie a rendszereden.

```bash
pip install aspose-ocr
```

> **Pro tipp:** Használj virtuális környezetet (`python -m venv venv`), hogy a függőségek izoláltak legyenek. Megakadályozza a verzióütközéseket, ha több projektet kezelsz egyszerre.

A telepítés után importáld a szükséges modulokat:

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

Itt importáljuk a `asposeocr`‑t a nehéz feladatokhoz, valamint a beépített `json` könyvtárat a későbbi sorosításhoz.

## 2. lépés – OCR motor létrehozása és a nyelv beállítása

Az OCR motor a fő komponens, amely ténylegesen olvassa a pixeleket. A legtöbb angol nyelvű számla esetén az angol nyelvi csomagra lesz szükséged:

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Miért fontos:** A nyelv megadása szűkíti a karakterkészletet, ami növeli a pontosságot és felgyorsítja a feldolgozást. Ha többnyelvű számlákat kell kezelned, egyszerűen cseréld le a `ocr.Language.ENGLISH`‑t a megfelelő enumra.

## 3. lépés – Kép betöltése OCR-hez

Most **betöltjük a képet OCR-hez**. A `Image.load` metódus fájlútvonalat fogad, és működik PNG, JPEG, BMP és más formátumokkal is.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **Különleges eset:** Ha a PNG szokatlanul nagy (5 MB felett), fontold meg először a méretezését, hogy a memóriahasználat ésszerű maradjon. A Pillow ezt egyetlen sorban meg tudja tenni:

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

## 4. lépés – OCR futtatása PNG-n és az eredmény rögzítése

Miután a motor készen áll és a kép betöltődött, itt az ideje **OCR futtatásának PNG-n**, és a strukturált eredmény lekérésének.

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

Az `ocr_result` objektum `OcrRegion` elemek gyűjteményét tartalmazza, mindegyik a felismert szöveget és egy megbízhatósági pontszámot (0‑100) tartalmazza. Itt kapod meg a részletes adatokat, amelyek a **szöveg kinyeréséhez számlák sorából** szükségesek.

## 5. lépés – Az eredmény konvertálása JSON-re és szép kiírása

A legtöbb downstream rendszer szereti a JSON-t, ezért az OCR kimenetet egy szépen formázott karakterlánccá alakítjuk.

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### Minta kimenet

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

Vedd észre, hogy minden sor tartalmaz egy megbízhatósági mutatót – tökéletes az alacsony bizalomú bejegyzések kiszűrésére, ha automatikusan **szöveget szeretnél kinyerni számlákból**.

## 6. lépés – OCR adatok mentése CSV-be (egy sor szöveg + megbízhatóság per sor)

A CSV ideális táblázatokhoz vagy gyors adatimportokhoz. Az Aspose egy egy soros megoldást kínál, hogy mindent egy CSV fájlba írjon.

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

A generált CSV így fog kinézni:

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

Most már megnyithatod Excelben, Google Sheets‑ben, vagy betáplálhatod egy adatbázisba.

## Bónusz – Alacsony megbízhatóságú szöveg és többoldalas PDF-ek kezelése

### Szűrés megbízhatóság alapján

Ha csak magas biztonságú sorokat szeretnél, szűrd le a JSON‑t, mielőtt kiírnád:

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### Többoldalas dokumentumok

Az Aspose.OCR automatikusan létrehoz egy új `page` bejegyzést minden egyes oldalhoz egy többoldalas PNG vagy PDF esetén. Iterálj a `ocr_data["pages"]`‑en, hogy mindet feldolgozd – extra kód nélkül.

## Teljes működő példa

Az alábbi **teljes szkript**, amelyet másolhatsz, beilleszthetsz és azonnal futtathatsz. Cseréld le a `YOUR_DIRECTORY`‑t arra a mappára, amely a PNG fájlodat tartalmazza.

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

Futtasd a szkriptet a `python run_ocr.py` paranccsal, és a konzolon láthatod a JSON kiírást, a lemezre mentett CSV fájlt, valamint a magas megbízhatóságú bejegyzések szűrt listáját.

## Gyakran ismételt kérdések

**K: Használhatom ezt beolvasott nyugta szövegének kinyerésére a számla helyett?**  
V: Teljesen. Ugyanaz a munkafolyamat érvényes – csak állítsd be az `image_path`‑t a nyugta PNG-jére. Ha a nyugta más nyelvet használ, cseréld le a `engine.language`‑t ennek megfelelően.

**K: Mi van, ha a PNG elfordított szöveget tartalmaz?**  
V: Az Aspose.OCR automatikusan felismeri a tájolást, de makacs esetekben manuálisan elfordíthatod a képet a Pillow‑lal, mielőtt a motorba adod.

**K: Szükségem van fizetős licencre az Aspose.OCR-hez?**  
V: A könyvtár ingyenes értékelő módot kínál, amely a kimeneten vízjelet helyez el. Gyártási környezetben licencre lesz szükséged, amelyet az Aspose weboldaláról szerezhetsz be.

## Összegzés

Minden szükséges lépést áttekintettünk, hogy **OCR‑t futtass PNG fájlokon** Python használatával: az SDK telepítése, a kép betöltése, a strukturált szöveg kinyerése, és az eredmény mentése JSON vagy CSV formátumban. Akár egyszerű szkripthez **szöveget szeretnél kinyerni a képből**, akár automatizált könyvelési folyamatban **szöveget kell kinyerni számlákból**, a fenti lépések egy stabil, gyártásra kész alapot biztosítanak.

A következőket érdemes még felfedezni:

- A CSV kimenet integrálása adatbázissal a tömeges számlatároláshoz.  
- Utófeldolgozás hozzáadása reguláris kifejezésekkel, hogy dátumokat, összegeket vagy adóazonosítókat nyerj ki.  
- A `ocr_engine.recognize_barcode` funkció használata, ha a számláid QR kódot tartalmaznak.

Próbáld ki, állítsd be a megbízhatósági küszöböket, és nézd, ahogy a dokumentumfeldolgozási munkafolyamatod könnyedé válik. Van még kérdésed vagy egy izgalmas felhasználási eseted? Írj egy megjegyzést alább – jó OCR‑zést!  

![OCR futtatása PNG példája](run-ocr-on-png.png "OCR futtatása PNG – vizuális példa az OCR eredményére")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}