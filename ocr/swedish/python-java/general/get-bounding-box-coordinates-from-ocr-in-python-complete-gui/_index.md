---
category: general
date: 2026-06-22
description: Hämta koordinater för omgivningsrutor från bilder med Python. Lär dig
  hur du extraherar text från bild med Python med Aspose OCR och JSON‑parsning på
  några minuter.
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: sv
og_description: Hämta koordinater för begränsningsrutor från bilder med Python. Denna
  guide visar hur du extraherar text från en bild med Python och Aspose OCR samt parsar
  layoutdata.
og_title: Få koordinater för avgränsningsruta från OCR i Python – Fullständig handledning
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
title: Hämta koordinater för avgränsningsruta från OCR i Python – Komplett guide
url: /sv/python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hämta koordinater för avgränsningsruta från OCR i Python – Komplett guide

Har du någonsin behövt **hämta koordinater för avgränsningsruta** för varje ord i en skannad faktura, men varit osäker på var du ska börja? Du är inte ensam. I många automationsprojekt måste du lokalisera text på en bild för att markera, maskera eller föra in i efterföljande analyser. De goda nyheterna? Med några rader Python och Aspose.OCR kan du hämta både texten **och** dess exakta position i ett enda pass.

I den här handledningen går vi igenom ett praktiskt exempel som visar dig hur du **extraherar text från bild i Python‑stil**, och sedan dyker ner i JSON‑layoutdata för att hämta ut dessa avgränsningsrutor. Inga onödiga detaljer, bara ett fungerande skript, förklaringar till varför varje steg är viktigt och tips för att undvika vanliga fallgropar.

---

## Vad du kommer att bygga

Vid slutet av den här guiden har du ett färdigt Python‑skript som:

1. Laddar en bild (t.ex. en faktura‑PNG) i Aspose OCR.
2. Konfigurerar motorn för att generera JSON‑layoutinformation.
3. Analyserar JSON‑data till en Python‑ordbok.
4. Itererar över varje igenkännt ord och skriver ut dess text **och** dess avgränsningsrutekordinater.

Du kommer också att se hur du anpassar koden för flersidiga PDF‑filer, olika bildformat och anpassade koordinatsystem.

### Förutsättningar

- Python 3.8+ installerat på din maskin.  
- En aktiv Aspose.OCR för Python‑licens eller en gratis provperiod (biblioteket fungerar utan licens men lägger till ett vattenmärke).  
- `pip install aspose-ocr` (paketnamnet på PyPI).  
- En exempelbild kallad `invoice.png` placerad i en mapp du kan referera till.

Det är allt—inga tunga ramverk, inga externa tjänster. Låt oss dyka in.

---

## Steg 1: Installera och importera de nödvändiga biblioteken

Först, se till att Aspose OCR‑paketet och den inbyggda `json`‑modulen är tillgängliga. `json`‑modulen följer med Python, så vi behöver bara installera Aspose.

```bash
pip install aspose-ocr
```

Importera dem nu i ditt skript:

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **Varför detta är viktigt:** Att importera `aspose.ocr` ger dig tillgång till den högpresterande OCR‑motorn, medan `json` låter dig omvandla den råa layoutsträngen till en inbyggd Python‑ordbok för enkel traversering.

---

## Steg 2: Skapa OCR‑motorn och ladda din bild

Motorn är hjärtat i processen. Du instansierar den och pekar den sedan på bilden du vill skanna.

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **Proffstips:** Ersätt `"YOUR_DIRECTORY/invoice.png"` med en absolut eller relativ sökväg som pekar på din faktiska fil. Om filen inte hittas kommer Aspose att kasta ett `FileNotFoundError`, så dubbelkolla stavningen.

---

## Steg 3: Konfigurera motorn för att skriva ut JSON‑layoutdata

Aspose OCR kan returnera ren text, OCR‑endast JSON eller ett fullständigt layout‑JSON som inkluderar koordinater för ord, rader och till och med enskilda tecken. För **hämta koordinater för avgränsningsruta** behöver vi layout‑JSON‑filen.

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **Varför JSON?** JSON är språkoberoende, människoläsbart och mappar rent på Python‑ordböcker. Layout‑JSON‑filen innehåller en `"words"`‑array där varje post innehåller texten och en `boundingBox`‑array med åtta tal (de fyra hörnpunkterna).

---

## Steg 4: Kör igenkänning och hämta den råa JSON‑strängen

Nu kör vi faktiskt OCR. Metoden `recognize()` returnerar ett `OcrResult`‑objekt, från vilket vi kan extrahera JSON‑strängen.

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

Om du skriver ut `layout_json` kommer du att se något liknande:

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

> **Edge case:** Vissa bilder kan producera tomma `"words"`‑arrayer om OCR‑motorn inte kan upptäcka någon text. I så fall, verifiera bildkvaliteten (kontrast, upplösning) innan du fortsätter.

---

## Steg 5: Analysera JSON‑data till en Python‑ordbok

Att arbeta med inbyggda Python‑strukturer är mycket enklare än att manipulera strängar. Använd funktionen `json.loads()` för att konvertera strängen.

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

Nu är `layout_data["words"]` en lista med ordböcker, där varje objekt representerar ett ord och dess avgränsningsruta.

---

## Steg 6: Iterera över ord och **hämta koordinater för avgränsningsruta**

Här är kärnan i vår handledning: loopa igenom varje ord, extrahera texten och skriva ut koordinaterna. Detta är exakt den plats där vi **hämta koordinater för avgränsningsruta**.

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**Exempelutdata** (dina siffror kommer att skilja sig beroende på bilden):

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **Varför det åttonspunktsformatet?** De fyra hörnen (övre vänster, övre höger, nedre höger, nedre vänster) låter dig rita en polygon runt ordet, även om texten är snedvriden. Om du bara behöver en enkel rektangel kan du beräkna `x_min = min(x1, x2, x3, x4)`, `y_min = min(y1, y2, y3, y4)`, `width = max(x…) - x_min` och `height = max(y…) - y_min`.

---

## Valfria förbättringar

### 1. Konvertera avgränsningsrutor till enkla rektanglar

Om ditt nedströmsverktyg förväntar sig `(x, y, width, height)` istället för åtta punkter, lägg till en hjälpfunktion:

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

### 2. Hantera flersidiga PDF‑filer

Aspose OCR kan ta emot PDF‑strömmar. Ersätt rad‑en för bildladdning med:

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

Iterera `set_page_number` för varje sida och samla koordinater per sida.

### 3. Visualisera avgränsningsrutor

Om du vill se rutorna ritade på originalbilden, använd Pillow:

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

Nu ser du röda konturer runt varje igenkännt ord—perfekt för felsökning eller UI‑överlägg.

---

## Vanliga frågor & fallgropar

- **Vad händer om JSON‑filen är enorm?** För stora dokument, överväg att strömma JSON‑data eller bearbeta sida‑för‑sida för att hålla minnesanvändningen låg.  
- **Varför saknas vissa ord?** Låg kontrast eller handskriven text får ofta OCR‑motorer att misslyckas. Förbehandla bilden (öka kontrast, binarisera) innan du skickar den till Aspose.  
- **Kan jag få tecken‑nivåkoordinater?** Ja—sätt `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)` för att få en `"characters"`‑array med egna `boundingBox`.  
- **Är koordinatsystemet nollbaserat?** Absolut. (0, 0) är bildens övre vänstra hörn.

---

## Fullt skript – redo att kopiera och köra

Nedan är det kompletta, körbara exemplet som kombinerar alla steg. Spara det som `extract_bboxes.py` och kör `python extract_bboxes.py`.

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


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}