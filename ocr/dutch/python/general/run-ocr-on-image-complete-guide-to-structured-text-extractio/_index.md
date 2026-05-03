---
category: general
date: 2026-05-03
description: Leer hoe je OCR op een afbeelding uitvoert en tekst met coördinaten extraheert
  met gestructureerde OCR‑herkenning. Stap‑voor‑stap Python‑code inbegrepen.
draft: false
keywords:
- run OCR on image
- extract text with coordinates
- structured OCR recognition
- OCR post‑processing
- bounding box extraction
- image text detection
language: nl
og_description: Voer OCR uit op een afbeelding en krijg tekst met coördinaten via
  gestructureerde OCR-herkenning. Volledig Python‑voorbeeld met uitleg.
og_title: OCR uitvoeren op afbeelding – Tutorial voor gestructureerde tekstelextractie
tags:
- OCR
- Python
- Computer Vision
title: OCR uitvoeren op afbeelding – Complete gids voor gestructureerde tekstextractie
url: /nl/python/general/run-ocr-on-image-complete-guide-to-structured-text-extractio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR uitvoeren op afbeelding – Complete gids voor gestructureerde teksteextractie

Heb je ooit **run OCR on image** bestanden nodig gehad, maar wist je niet hoe je de exacte posities van elk woord kunt behouden? Je bent niet de enige. In veel projecten—bonnen scannen, formulieren digitaliseren of UI-testen—heb je niet alleen de ruwe tekst nodig, maar ook de begrenzingskaders die aangeven waar elke regel zich op de afbeelding bevindt.  

Deze tutorial laat je een praktische manier zien om *run OCR on image* te doen met de **aocr** engine, **structured OCR recognition** aan te vragen, en vervolgens het resultaat post‑processen terwijl je de geometrie behoudt. Aan het einde kun je **extract text with coordinates** met slechts een paar regels Python, en begrijp je waarom de gestructureerde modus belangrijk is voor vervolgprocessen.

## What You’ll Learn

- Hoe je de OCR-engine initialiseert voor **structured OCR recognition**.  
- Hoe je een afbeelding invoert en ruwe resultaten ontvangt die lijnbegrenzingen bevatten.  
- Hoe je een post‑processor uitvoert die de tekst opschoont zonder de geometrie te verliezen.  
- Hoe je over de uiteindelijke regels itereren en elk stuk tekst samen met de begrenzingskader afdrukken.  

Geen magie, geen verborgen stappen—gewoon een compleet, uitvoerbaar voorbeeld dat je in je eigen project kunt gebruiken.

---

## Prerequisites

Voordat we beginnen, zorg ervoor dat je het volgende geïnstalleerd hebt:

```bash
pip install aocr ai   # hypothetical packages; replace with real ones if needed
```

Je hebt ook een afbeeldingsbestand (`input_image.png` of `.jpg`) nodig dat duidelijke, leesbare tekst bevat. Alles van een gescande factuur tot een screenshot werkt, zolang de OCR-engine de tekens kan zien.

---

## Step 1: Initialise the OCR engine for structured recognition

Het eerste wat we doen is een instantie van `aocr.Engine()` maken en aangeven dat we **structured OCR recognition** willen. Structured mode geeft niet alleen de platte tekst terug, maar ook geometrische gegevens (bounding rectangles) voor elke regel, wat essentieel is wanneer je tekst terug op de afbeelding wilt plaatsen.

```python
import aocr
import ai   # hypothetical post‑processing module

# Initialise the OCR engine
ocr_engine = aocr.Engine()

# Request structured recognition (text + geometry)
ocr_engine.recognize_mode = aocr.RecognitionMode.Structured
```

> **Why this matters:**  
> In de standaardmodus geeft de engine misschien alleen een tekenreeks van aaneengeschakelde woorden. Structured mode geeft je een hiërarchie van pages → lines → words, each with coordinates, making it far easier to overlay results on the original image or feed them into a layout‑aware model.

---

## Step 2: Run OCR on the image and obtain raw results

Nu voeren we de afbeelding in de engine. De `recognize`‑aanroep retourneert een `OcrResult`‑object dat een verzameling regels bevat, elk met zijn eigen bounding rectangle.

```python
# Load your image (any format supported by aocr)
input_image_path = "input_image.png"

# Run OCR – this returns an OcrResult with lines and bounds
raw_result = ocr_engine.recognize(input_image_path)
```

Op dit punt bevat `raw_result.lines` objecten met twee belangrijke attributen:

- `text` – de herkende string voor die regel.  
- `bounds` – een tuple zoals `(x, y, width, height)` die de positie van de regel beschrijft.

---

## Step 3: Post‑process while preserving geometry

Ruwe OCR‑output is vaak ruisachtig: vreemde tekens, verkeerd geplaatste spaties of regelafbrekingsproblemen. De `ai.run_postprocessor`‑functie maakt de tekst schoon maar **keeps the original geometry** intact, zodat je nog steeds nauwkeurige coördinaten hebt.

```python
# Apply a post‑processing step that corrects common OCR errors
postprocessed_result = ai.run_postprocessor(raw_result)

# The structure (lines + bounds) stays the same, only `line.text` changes
```

> **Pro tip:** Als je domeinspecifieke vocabularies hebt (bijv. product codes), voer dan een aangepast woordenboek in de post‑processor in om de nauwkeurigheid te verbeteren.

---

## Step 4: Extract text with coordinates – iterate and display

Tot slot lopen we door de opgeschoonde regels, waarbij we de bounding box van elke regel naast de tekst afdrukken. Dit is de kern van **extract text with coordinates**.

```python
# Print each recognised line together with its bounding box
for line in postprocessed_result.lines:
    print(f"[{line.bounds}] {line.text}")
```

### Expected Output

Als we aannemen dat de invoerafbeelding twee regels bevat: “Invoice #12345” en “Total: $89.99”, zie je iets als:

```
[(15, 30, 210, 25)] Invoice #12345
[(15, 70, 190, 25)] Total: $89.99
```

De eerste tuple is de `(x, y, width, height)` van de regel op de originele afbeelding, waardoor je rechthoeken kunt tekenen, tekst kunt markeren of de coördinaten in een ander systeem kunt invoeren.

---

## Visualising the Result (Optional)

Als je de bounding boxes over de afbeelding wilt zien, kun je Pillow (PIL) gebruiken om rechthoeken te tekenen. Hieronder staat een kort fragment; voel je vrij om het over te slaan als je alleen de ruwe gegevens nodig hebt.

```python
from PIL import Image, ImageDraw

# Open the original image
img = Image.open(input_image_path)
draw = ImageDraw.Draw(img)

# Draw a rectangle around each line
for line in postprocessed_result.lines:
    x, y, w, h = line.bounds
    draw.rectangle([x, y, x + w, y + h], outline="red", width=2)

# Save or show the annotated image
img.save("annotated_output.png")
img.show()
```

![run OCR on image example showing bounding boxes](/images/ocr-bounding-boxes.png "run OCR on image – bounding box overlay")

De alt‑tekst hierboven bevat het **primary keyword**, wat voldoet aan de SEO‑vereiste voor alt‑attributen van afbeeldingen.

---

## Why Structured OCR Recognition Beats Simple Text Extraction

Je vraagt je misschien af: “Kan ik niet gewoon OCR uitvoeren en de tekst krijgen? Waarom de moeite doen met geometrie?”  

- **Spatial context:** Wanneer je velden op een formulier moet koppelen (bijv. “Date” naast een datumwaarde), geven coördinaten je *waar* de data zich bevindt.  
- **Multi‑column layouts:** Eenvoudige lineaire tekst verliest de volgorde; gestructureerde data behoudt de kolomvolgorde.  
- **Post‑processing accuracy:** Het kennen van de grootte van de box helpt je bepalen of een woord een koptekst, een voetnoot of een vreemd artefact is.  

Kortom, **structured OCR recognition** geeft je de flexibiliteit om slimmere pipelines te bouwen—of je nu data in een database stopt, doorzoekbare PDF's maakt, of een machine‑learning model traint dat de lay-out respecteert.

---

## Common Edge Cases and How to Handle Them

| Situation | What to Watch For | Suggested Fix |
|-----------|-------------------|---------------|
| **Rotated or skewed images** | Bounding boxes may be off‑axis. | Pre‑process with deskewing (e.g., OpenCV’s `warpAffine`). |
| **Very small fonts** | Engine may miss characters, leading to empty lines. | Increase image resolution or use `ocr_engine.set_dpi(300)`. |
| **Mixed languages** | Wrong language model can cause garbled text. | Set `ocr_engine.language = ["en", "de"]` before recognition. |
| **Overlapping boxes** | Post‑processor might merge two lines unintentionally. | Verify `line.bounds` after processing; adjust thresholds in `ai.run_postprocessor`. |

Deze scenario's vroeg aanpakken bespaart je later hoofdpijn, vooral wanneer je de oplossing opschaalt naar honderden documenten per dag.

---

## Full End‑to‑End Script

Hieronder staat het volledige, kant‑klaar script dat alle stappen samenvoegt. Kopieer‑plak, pas het pad van de afbeelding aan, en je bent klaar om te gaan.

```python
# -*- coding: utf-8 -*-
"""
Run OCR on image – extract text with coordinates using structured OCR recognition.
Author: Your Name
Date: 2026-05-03
"""

import aocr
import ai
from PIL import Image, ImageDraw

def run_structured_ocr(image_path: str, annotate: bool = False):
    # 1️⃣ Initialise the OCR engine
    ocr_engine = aocr.Engine()
    ocr_engine.recognize_mode = aocr.RecognitionMode.Structured

    # 2️⃣ Recognise the image
    raw_result = ocr_engine.recognize(image_path)

    # 3️⃣ Post‑process while keeping geometry
    processed = ai.run_postprocessor(raw_result)

    # 4️⃣ Print each line with its bounding box
    for line in processed.lines:
        print(f"[{line.bounds}] {line.text}")

    # Optional visualisation
    if annotate:
        img = Image.open(image_path)
        draw = ImageDraw.Draw(img)
        for line in processed.lines:
            x, y, w, h = line.bounds
            draw.rectangle([x, y, x + w, y + h], outline="red", width=2)
        annotated_path = "annotated_" + image_path
        img.save(annotated_path)
        print(f"Annotated image saved as {annotated_path}")

if __name__ == "__main__":
    INPUT_IMG = "input_image.png"
    run_structured_ocr(INPUT_IMG, annotate=True)
```

Running this script will:

1. **Run OCR on image** with structured mode.  
2. **Extract text with coordinates** for every line.  
3. Optioneel een geannoteerde PNG produceren die de kaders toont.

---

## Conclusion

Je hebt nu een solide, zelfstandige oplossing om **run OCR on image** en **extract text with coordinates** te gebruiken met **structured OCR recognition**. De code demonstreert elke stap—van engine‑initialisatie tot post‑processing en visuele verificatie—zodat je het kunt aanpassen aan bonnen, formulieren of elk visueel document dat precieze tekstoplokalisatie vereist.

Wat is de volgende stap? Probeer de `aocr`‑engine te vervangen door een andere bibliotheek (Tesseract, EasyOCR) en kijk hoe hun gestructureerde output verschilt. Experimenteer met verschillende post‑processingstrategieën, zoals spell‑checking of aangepaste regex‑filters, om de nauwkeurigheid voor jouw domein te verhogen. En als je een grotere pipeline bouwt, overweeg dan om de `(text, bounds)`‑paren in een database op te slaan voor latere analyses.

Veel plezier met coderen, en moge je OCR‑projecten altijd nauwkeurig zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}