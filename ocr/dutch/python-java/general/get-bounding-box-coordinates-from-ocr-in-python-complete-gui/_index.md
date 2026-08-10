---
category: general
date: 2026-06-22
description: Haal de coördinaten van de begrenzingskader uit afbeeldingen met Python.
  Leer in enkele minuten hoe je tekst uit een afbeelding kunt extraheren met Python,
  Aspose OCR en JSON-parsing.
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: nl
og_description: Haal de coördinaten van de begrenzingsvak uit afbeeldingen met Python.
  Deze gids laat zien hoe je tekst uit een afbeelding kunt extraheren met Python en
  Aspose OCR en lay-outgegevens kunt parseren.
og_title: Haal Bounding Box‑coördinaten op uit OCR in Python – Volledige tutorial
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
title: Haal Bounding Box‑coördinaten op uit OCR in Python – Complete gids
url: /nl/python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bounding Box‑coördinaten ophalen met OCR in Python – Complete gids

Heb je ooit **bounding box‑coördinaten** moeten krijgen voor elk woord in een gescande factuur, maar wist je niet waar je moest beginnen? Je bent niet de enige. In veel automatiseringsprojecten moet je tekst op een afbeelding lokaliseren om te markeren, te redigeren of in downstream‑analyses te gebruiken. Het goede nieuws? Met een paar regels Python en Aspose.OCR kun je zowel de tekst **als** de exacte positie in één keer ophalen.

In deze tutorial lopen we een hands‑on voorbeeld door dat laat zien hoe je **tekst uit een afbeelding in Python‑stijl** kunt extraheren, en vervolgens duiken we in de JSON‑lay-outgegevens om die bounding boxes te halen. Geen poespas, alleen een werkend script, uitleg waarom elke stap belangrijk is, en tips om veelvoorkomende valkuilen te vermijden.

---

## Wat je gaat bouwen

Aan het einde van deze gids heb je een kant‑en‑klaar Python‑script dat:

1. Een afbeelding (bijv. een factuur‑PNG) laadt in Aspose OCR.  
2. De engine configureert om JSON‑lay‑outinformatie uit te geven.  
3. De JSON omzet naar een Python‑dictionary.  
4. Over elk herkend woord iterereert en zowel de tekst **als** de bounding box‑coördinaten afdrukt.

Je ziet ook hoe je de code kunt aanpassen voor multi‑page PDF’s, verschillende afbeeldingsformaten en aangepaste coördinatensystemen.

### Voorwaarden

- Python 3.8+ geïnstalleerd op je machine.  
- Een actieve Aspose.OCR for Python‑licentie of een gratis proefversie (de bibliotheek werkt zonder licentie maar voegt een watermerk toe).  
- `pip install aspose-ocr` (de pakketnaam op PyPI).  
- Een voorbeeldafbeelding genaamd `invoice.png` geplaatst in een map die je kunt refereren.

Dat is alles—geen zware frameworks, geen externe services. Laten we duiken.

---

## Stap 1: Installeer en importeer de vereiste bibliotheken

Eerst moet je ervoor zorgen dat het Aspose OCR‑pakket en de ingebouwde `json`‑module beschikbaar zijn. De `json`‑module wordt meegeleverd met Python, dus we hoeven alleen Aspose te installeren.

```bash
pip install aspose-ocr
```

Importeer ze nu in je script:

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **Waarom dit belangrijk is:** Het importeren van `aspose.ocr` geeft je toegang tot de high‑performance OCR‑engine, terwijl `json` je in staat stelt de ruwe lay‑out‑string om te zetten naar een native Python‑dictionary voor eenvoudige traversering.

---

## Stap 2: Maak de OCR‑engine en laad je afbeelding

De engine is het hart van het proces. Je maakt een instantie, en wijst vervolgens de afbeelding toe die je wilt scannen.

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **Pro tip:** Vervang `"YOUR_DIRECTORY/invoice.png"` door een absoluut of relatief pad dat naar je daadwerkelijke bestand wijst. Als het bestand niet wordt gevonden, zal Aspose een `FileNotFoundError` genereren, dus controleer de spelling zorgvuldig.

---

## Stap 3: Configureer de engine om JSON‑lay‑outgegevens uit te geven

Aspose OCR kan platte tekst, alleen‑OCR‑JSON of een volledige lay‑out‑JSON teruggeven die coördinaten voor woorden, regels en zelfs individuele tekens bevat. Voor **bounding box‑coördinaten ophalen** hebben we de lay‑out‑JSON nodig.

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **Waarom JSON?** JSON is taal‑agnostisch, mens‑leesbaar, en mappt netjes naar Python‑dictionaries. De lay‑out‑JSON bevat een `"words"`‑array waarin elk item de tekst en een `boundingBox`‑array van acht getallen (de vier hoekpunten) bevat.

---

## Stap 4: Voer herkenning uit en haal de ruwe JSON‑string op

Nu voeren we de OCR daadwerkelijk uit. De `recognize()`‑methode retourneert een `OcrResult`‑object, waaruit we de JSON‑string kunnen extraheren.

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

Als je `layout_json` afdrukt, zie je iets als:

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

> **Edge case:** Sommige afbeeldingen kunnen lege `"words"`‑arrays opleveren als de OCR‑engine geen tekst kan detecteren. Controleer in dat geval de beeldkwaliteit (contrast, resolutie) voordat je verder gaat.

---

## Stap 5: Parse de JSON naar een Python‑dictionary

Werken met native Python‑structuren is veel eenvoudiger dan met strings knoeien. Gebruik de functie `json.loads()` om de string te converteren.

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

Nu is `layout_data["words"]` een lijst van dictionaries, elk representerend een woord en zijn bounding box.

---

## Stap 6: Iterate over woorden en **Bounding Box‑coördinaten ophalen**

Hier is de kern van onze tutorial: door elk woord loopen, de tekst extraheren en de coördinaten afdrukken. Dit is precies de plek waar we **bounding box‑coördinaten ophalen**.

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**Voorbeeldoutput** (jouw getallen zullen verschillen op basis van de afbeelding):

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **Waarom het acht‑puntformaat?** De vier hoeken (linksboven, rechtsboven, rechtsonder, linksonder) stellen je in staat een polygoon rond het woord te tekenen, zelfs als de tekst scheef staat. Als je alleen een eenvoudige rechthoek nodig hebt, kun je `x_min = min(x1, x2, x3, x4)`, `y_min = min(y1, y2, y3, y4)`, `width = max(x…) - x_min` en `height = max(y…) - y_min` berekenen.

---

## Optionele verbeteringen

### 1. Bounding boxes omzetten naar eenvoudige rechthoeken

Als je downstream‑tool `(x, y, width, height)` verwacht in plaats van acht punten, voeg dan een helper toe:

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

### 2. Multi‑page PDF’s verwerken

Aspose OCR kan PDF‑streams accepteren. Vervang de regel voor het laden van de afbeelding door:

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

Itereer `set_page_number` voor elke pagina en verzamel de coördinaten per pagina.

### 3. Bounding boxes visualiseren

Wil je de vakken op de originele afbeelding zien, gebruik dan Pillow:

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

Nu zie je rode omtrekken rond elk herkend woord—perfect voor debugging of UI‑overlays.

---

## Veelgestelde vragen & valkuilen

- **Wat als de JSON enorm is?** Voor grote documenten kun je overwegen de JSON te streamen of pagina‑voor‑pagina te verwerken om het geheugenverbruik laag te houden.  
- **Waarom ontbreken sommige woorden?** Laag contrast of handgeschreven tekst brengt OCR‑engines vaak in de problemen. Pre‑process het beeld (verhoog contrast, binariseer) voordat je het naar Aspose stuurt.  
- **Kan ik coördinaten op teken‑niveau krijgen?** Ja—stel `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)` in om een `"characters"`‑array met eigen `boundingBox` te ontvangen.  
- **Is het coördinatensysteem nul‑gebaseerd?** Absoluut. (0, 0) is de linkerbovenhoek van de afbeelding.

---

## Volledig script – Klaar om te kopiëren & uit te voeren

Hieronder vind je het complete, uitvoerbare voorbeeld dat alle stappen combineert. Sla het op als `extract_bboxes.py` en voer `python extract_bboxes.py` uit.

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


## Wat moet je hierna leren?


De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}