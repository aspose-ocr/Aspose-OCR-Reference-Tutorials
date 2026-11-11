---
category: general
date: 2026-06-25
description: Szöveg kinyerése képből Python OCR-rel. Tanulja meg, hogyan töltsön be
  képet OCR-hez, hogyan végezzen OCR-t Pythonban, és hogyan konvertálja a nyugtát
  JSON formátumba néhány egyszerű lépésben.
draft: false
keywords:
- extract text from image
- load image for OCR
- perform OCR in Python
- convert receipt to JSON
language: hu
og_description: Képről szöveg kinyerése Python OCR-rel. Ez az útmutató végigvezet
  a kép OCR-hez való betöltésén, a Pythonban történő OCR végrehajtásán, és egy nyugta
  JSON formátumba konvertálásán.
og_title: Kép szövegének kinyerése Pythonban – Teljes OCR útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  headline: Extract Text from Image in Python – Full OCR Guide
  type: TechArticle
- description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  name: Extract Text from Image in Python – Full OCR Guide
  steps:
  - name: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
    text: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
  - name: '**Load an image for OCR** – tell the engine which file to read.'
    text: '**Load an image for OCR** – tell the engine which file to read.'
  - name: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
    text: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
  - name: '**Run the recognition** – actually perform OCR in Python.'
    text: '**Run the recognition** – actually perform OCR in Python.'
  - name: '**Print or store the result** – convert receipt to JSON and see the output.'
    text: '**Print or store the result** – convert receipt to JSON and see the output.'
  - name: Sends the image through a pre‑trained convolutional network.
    text: Sends the image through a pre‑trained convolutional network.
  - name: Decodes the network output into readable characters.
    text: Decodes the network output into readable characters.
  - name: Packages everything into the selected format (JSON in our case).
    text: Packages everything into the selected format (JSON in our case).
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- JSON
title: Kép szövegének kinyerése Pythonban – Teljes OCR útmutató
url: /hu/python/general/extract-text-from-image-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép szövegének kinyerése Pythonban – Teljes OCR útmutató

Valaha szükséged volt **kép szövegének kinyerésére**, de nem tudtad, hol kezdj? Ebben az útmutatóban végigvezetünk, hogyan **tölts be képet OCR-hez**, **végezz OCR-t Pythonban**, és **alakítsd át a nyugtát JSON-re** — mindezt csak néhány sor kóddal.

Ha valaha készítettél nyugta‑olvasó alkalmazást, költség‑követőt, vagy egyszerűen csak automatizálni szeretnéd az adatbevitelét, látni fogod, miért jelent áttörést ennek a folyamatnak a elsajátítása. A végére egy működő szkriptet kapsz, amely beolvassa a nyugta képét, és egy tiszta JSON payload‑ot ad ki, készen a további szolgáltatások számára.

## Mit fogsz megtanulni

1. **Create an OCR engine instance** – az OCR motor példányának létrehozása – a belépési pont minden felismerési feladathoz.  
2. **Load an image for OCR** – kép betöltése OCR-hez – mondd meg a motornak, melyik fájlt olvassa.  
3. **Choose the export format** – export formátum kiválasztása – JSON vagy XML, mi a JSON-t választjuk, mert könnyebb felhasználni.  
4. **Run the recognition** – felismerés futtatása – ténylegesen OCR-t végez Pythonban.  
5. **Print or store the result** – eredmény kiírása vagy tárolása – nyugta átalakítása JSON-re és az output megtekintése.

Előzetes OCR tapasztalat nem szükséges; csak egy alap Python környezet és egy képfájl (nyugta, szórólap, bármi, amire szükséged van).

---

![Diagram a képből történő szövegkivonás folyamata Python OCR-rel](extract-text-from-image-python-ocr.png){alt="Diagram a képből történő szövegkivonás folyamata Python OCR-rel"}

## Kép szövegének kinyerése – Lépésről‑lépésre Python OCR

Az alábbiakban a teljes, azonnal futtatható szkript található. Nyugodtan másold be egy `receipt_ocr.py` nevű fájlba, és futtasd a `python receipt_ocr.py` parancsot.

```python
# receipt_ocr.py

# 1️⃣ Import the aocr package (make sure it's installed via `pip install aocr`)
import aocr

# 2️⃣ Create an OCR engine instance – this object orchestrates the whole process
engine = aocr.OcrEngine()

# 3️⃣ Load the image you want to process.
#    Replace the path with the location of your receipt or any image.
engine.load_image("YOUR_DIRECTORY/receipt.png")

# 4️⃣ Choose the output format. JSON is handy for APIs and downstream services.
engine.export_format = aocr.ExportFormat.JSON

# 5️⃣ Run the recognition and obtain the raw result.
json_result = engine.recognize()

# 6️⃣ Output the raw JSON string – you can also write it to a file if you prefer.
print(json_result)
```

### Miért működik ez

- **Engine instance** – `aocr.OcrEngine()` encapsulates all the heavy lifting (model loading, preprocessing, etc.).  
- **Loading the image** – `engine.load_image()` tells the library exactly which bitmap to analyze; you can feed JPEG, PNG, or even multi‑page PDFs.  
- **Export format** – Setting `engine.export_format` to `aocr.ExportFormat.JSON` makes the result a structured string, perfect for APIs that expect JSON.  
- **Recognition call** – `engine.recognize()` runs the neural net inference behind the scenes; it returns a JSON string that contains detected text blocks, confidence scores, and layout information.  

---

## Kép betöltése OCR-hez aocr használatával

Ha azon tűnődsz, hogy a képnek szüksége van-e valamilyen speciális előfeldolgozásra, a rövid válasz **nem** — a `aocr` automatikusan kezeli a legtöbb általános esetet (kontraszt beállítás, kiegyenesítés). Azonban a pontosságot növelheted a következőkkel:

- Biztosítsd, hogy a kép legalább 300 dpi legyen.  
- Vágd le a felesleges kereteket.  
- Konvertáld szürkeárnyalatba a betöltés előtt (opcionális, `engine.load_image()` ezt megteszi helyetted).

```python
# Optional preprocessing example using Pillow
from PIL import Image, ImageOps

original = Image.open("YOUR_DIRECTORY/receipt.png")
# Convert to grayscale and increase contrast
processed = ImageOps.autocontrast(original.convert("L"))
processed.save("processed_receipt.png")
engine.load_image("processed_receipt.png")
```

*Pro tipp:* Ha a nyugta sok zajt tartalmaz, a fenti extra lépés jelentősen javíthatja a **perform OCR in Python** pontosságát.

## Export formátum kiválasztása és nyugta átalakítása JSON-re

Talán azt kérdezed, „Miért ne csak egyszerű szöveget kapnánk?” Mert a JSON megőrzi a hierarchikus struktúrát (sorok, szavak, keretdobozok). Ez sokkal egyszerűbbé teszi a *teljes összeg* vagy *dátum* mezők későbbi leképezését.

```python
engine.export_format = aocr.ExportFormat.JSON   # Switch to XML with aocr.ExportFormat.XML if needed
```

Amikor futtatod a szkriptet, a `json_result` valahogy így fog kinézni (rövidítve a tömörség kedvéért):

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "bbox": [12, 34, 210, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.96,
          "bbox": [15, 400, 190, 420]
        }
      ]
    }
  ]
}
```

Most már van egy **convert receipt to JSON** payload-od, amelyet közvetlenül egy adatbázisba, egy REST végpontra vagy egy gépi tanulási modellbe táplálhatsz.

## Felismerés futtatása és eredmények lekérése

Az utolsó lépés — a tényleges OCR végrehajtása — olyan egyszerű, mint a `recognize()` meghívása. A könyvtár a háttérben:

1. Sends the image through a pre‑trained convolutional network.  
2. Decodes the network output into readable characters.  
3. Packages everything into the selected format (JSON in our case).

```python
json_result = engine.recognize()
print(json_result)   # <-- This prints the JSON string to stdout
```

Ha az outputot nyomtatás helyett tárolni szeretnéd, egyszerűen írd egy fájlba:

```python
with open("receipt_output.json", "w", encoding="utf-8") as f:
    f.write(json_result)
```

*Edge case:* Egyes nyugták nem ASCII karaktereket tartalmaznak (pl. „€”). Győződj meg róla, hogy a fájlt UTF‑8 kódolással nyitod meg, ahogy fent is látható, hogy elkerüld a torz szöveget.

## Teljes működő példa (Minden lépés egy szkriptben)

Mindent összevonva, itt a végső szkript, amelyet vég‑től‑végig futtathatsz:

```python
import aocr
from PIL import Image, ImageOps

# Create engine
engine = aocr.OcrEngine()

# Optional: preprocess image for better accuracy
raw = Image.open("YOUR_DIRECTORY/receipt.png")
processed = ImageOps.autocontrast(raw.convert("L"))
processed.save("processed_receipt.png")

# Load the (processed) image
engine.load_image("processed_receipt.png")

# Choose JSON output
engine.export_format = aocr.ExportFormat.JSON

# Run OCR
json_result = engine.recognize()

# Save result
with open("receipt_output.json", "w", encoding="utf-8") as out_file:
    out_file.write(json_result)

print("OCR complete! JSON saved to receipt_output.json")
```

Futtasd a következővel:

```bash
python receipt_ocr.py
```

Egy megerősítő sort kell látnod, és ugyanabban a mappában egy `receipt_output.json` fájlt, amely a strukturált adatokat tartalmazza.

## Következtetés

Most már tudod, **hogyan nyerj ki szöveget képből** Python használatával, hogyan **tölts be képet OCR-hez**, hogyan **végezz OCR-t Pythonban**, és hogyan **alakítsd át a nyugtát JSON-re** a további felhasználáshoz. Ez az end‑to‑end folyamat könnyű, csak a `aocr` csomagra van szüksége, és bármely automatizálási csővezetékbe beilleszthető.

Mi a következő? Próbáld megcserélni az export formátumot XML-re, kísérletezz különböző képelőfeldolgozási technikákkal, vagy építs egy apró Flask API-t, amely fogad egy feltöltött nyugtát, és azonnal visszaadja a JSON payload-ot. A lehetőségek határtalanok, ha már elsajátítottad az alapokat.

Van kérdésed vagy elakadtál? Írj egy megjegyzést alább, és jó kódolást!

## Mit érdemes még megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat, és alternatív megvalósítási megközelítéseket fedezhess fel saját projektjeidben.

- [Kép szövegének kinyerése Aspose OCR-rel – Lépésről‑lépésre útmutató](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Kép szövegének kinyerése – OCR optimalizálás Aspose.OCR-rel .NET-hez](/ocr/english/net/ocr-optimization/)
- [Hogyan nyerj ki táblázatot képből Aspose.OCR használatával .NET-hez](/ocr/english/net/text-recognition/recognize-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}