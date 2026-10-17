---
category: general
date: 2026-01-12
description: Hoe OCR uit te voeren en een afbeelding snel naar tekst te converteren.
  Leer speciale tekens te herkennen, tekst uit een afbeelding te extraheren en een
  afbeelding te laden voor OCR met een compleet Python‑voorbeeld.
draft: false
keywords:
- how to perform OCR
- convert image to text
- recognize special characters
- extract text from image
- load image for OCR
language: nl
og_description: Hoe OCR uit te voeren in Python, afbeelding naar tekst te converteren
  en speciale tekens te herkennen. Volg deze praktische gids voor het extraheren van
  tekst uit afbeeldingen.
og_title: Hoe OCR in Python uit te voeren – Complete tutorial
tags:
- OCR
- Python
- Image Processing
title: Hoe OCR in Python uit te voeren – Stapsgewijze gids
url: /nl/python/general/how-to-perform-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR uit te voeren in Python – Stapsgewijze gids

Heb je ooit **OCR moeten uitvoeren** op een screenshot die zowel Latijnse als Cyrillische tekens bevat? Je bent niet de enige. In veel projecten—of het nu gaat om het digitaliseren van bonnetjes, het indexeren van meertalige documenten, of het bouwen van een doorzoekbaar archief—**hoe OCR uit te voeren** wordt al snel een brandende vraag.  

In deze tutorial lopen we een compleet, uitvoerbaar voorbeeld door dat laat zien hoe je **afbeelding naar tekst converteert**, **speciale tekens herkent**, en **tekst uit afbeelding haalt** met een eenvoudige Python‑bibliotheek. Aan het einde heb je een kant‑klaar script dat een afbeelding laadt voor OCR, meertalige inhoud verwerkt en het resultaat afdrukt.

## Wat je nodig hebt

Voordat we beginnen, zorg dat je de volgende zaken klaar hebt staan:

- Python 3.8+ geïnstalleerd op je machine.  
- Het `ocr`‑pakket (of een compatibel OCR‑bibliotheek) geïnstalleerd via `pip install ocr`.  
- Een afbeeldingsbestand (`multilingual.png`) dat zowel Latijnse als Cyrillische glyphs bevat.  
- Een eenvoudige teksteditor of IDE—VS Code, PyCharm, of zelfs een simpel Notepad volstaat.  

Als je het `ocr`‑pakket niet hebt, kun je het vervangen door `pytesseract` met een paar kleine aanpassingen; de kernconcepten blijven hetzelfde.

## Stap 1: Installeer en importeer de OCR‑bibliotheek

Eerst maken we de OCR‑engine klaar. We importeren de bibliotheek, maken een engine‑instantie aan en configureren deze voor meertalige ondersteuning.

```python
# Install the library (run this once in your terminal)
# pip install ocr

import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: Enable language packs for Latin and Cyrillic
engine.set_languages(['eng', 'rus'])  # 'eng' = English, 'rus' = Russian
```

**Waarom dit belangrijk is:**  
Het creëren van de engine is de basis—zonder deze kun je later geen **afbeelding laden voor OCR**. Het inschakelen van taalpakketten zorgt ervoor dat de engine tekens zoals “Ŀ”, “Ҕ” en “Ǣ” correct kan identificeren. Als je deze stap overslaat, krijg je onleesbare uitvoer voor niet‑Latijnse scripts.

## Stap 2: Laad de afbeelding met meertalige tekst

Nu wijzen we de engine naar het bestand dat we willen verwerken. Het pad kan absoluut of relatief zijn; zorg er alleen voor dat het naar een leesbare afbeelding wijst.

```python
# Step 2: Load the image containing multilingual text
image_path = "YOUR_DIRECTORY/multilingual.png"  # replace with your actual path
engine.load_image(image_path)
```

> ![how to perform OCR example](/images/ocr-example.png "how to perform OCR on a multilingual image")

**Waarom dit belangrijk is:**  
De `load_image`‑aanroep leest de pixeldata in het geheugen in, zodat deze klaar is voor het OCR‑algoritme. Als de afbeelding groot is, kan de engine deze automatisch verkleinen; je kunt dat later fijn afstellen met `engine.set_max_resolution(3000)` voor scans met hoge resolutie.

## Stap 3: Voer het herkenningsproces uit

Met de engine klaar en de afbeelding geladen, kunnen we eindelijk de tekstinhoud extraheren.

```python
# Step 3: Perform OCR recognition on the loaded image
result = engine.recognize()
```

**Waarom dit belangrijk is:**  
`recognize()` voert het zware neurale netwerk op de achtergrond uit. Het retourneert een object dat de ruwe tekst, vertrouwensscores en zelfs begrenzingskaders bevat als je die nodig hebt voor visuele debugging.

## Stap 4: Geef de herkende tekst weer

Laten we zien wat de engine heeft gevonden. We printen de tekst naar de console, maar je kunt deze ook naar een bestand of database schrijven.

```python
# Step 4: Output the recognized text, which should include characters like “Ŀ”, “Ҕ”, “Ǣ”
print("=== OCR Result ===")
print(result.text)
```

### Verwachte uitvoer

```
=== OCR Result ===
Hello, world! Ŀ is a Latin‑extended character.
Привет, мир! Ҕ is a Cyrillic character.
Special combo: Ǣ is a ligature.
```

Als je iets vergelijkbaars ziet, gefeliciteerd—je hebt succesvol **afbeelding naar tekst geconverteerd** en **speciale tekens herkend**.

## Veelvoorkomende valkuilen behandelen

Zelfs met een eenvoudige script kun je tegen een paar hobbels aanlopen. Hieronder vind je praktische tips uit eigen ervaring.

### 1. Ontbrekende taalpakketten

Als je vraagtekens (`?`) ziet in plaats van Cyrillische letters, controleer dan of de taalpakketten geïnstalleerd zijn. Voor veel OCR‑engines moet je de bijbehorende `.traineddata`‑bestanden downloaden en in de `tessdata`‑map van de engine plaatsen.

```python
# Example for pytesseract
import pytesseract
pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
# Ensure 'eng' and 'rus' data files exist in tessdata
```

### 2. Lage beeldkwaliteit

Vage of laag‑contrast afbeeldingen geven lage vertrouwensscores. Pre‑process de afbeelding met OpenCV:

```python
import cv2

# Load, convert to grayscale, and apply thresholding
raw = cv2.imread(image_path)
gray = cv2.cvtColor(raw, cv2.COLOR_BGR2GRAY)
_, thresh = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)

# Save a temporary cleaned image and feed it to the OCR engine
cv2.imwrite("cleaned.png", thresh)
engine.load_image("cleaned.png")
```

### 3. Grote bestanden en geheugenverbruik

Het verwerken van een foto van 10 MB kan het geheugen doen pieken. Gebruik `engine.set_max_image_size(2000)` om de resolutie te beperken, of splits de afbeelding in tegels en OCR elke tegel apart.

### 4. Begrenzingskaders vastleggen

Als je wilt markeren waar elk woord verschijnt (handig voor UI‑overlays), krijg je toegang tot `result.boxes`:

```python
for box in result.boxes:
    print(f"Word: {box.text} – Coordinates: {box.x0},{box.y0},{box.x1},{box.y1}")
```

## Volledig script – Eén‑klik uitvoering

Alles samengevoegd, hier is een enkel bestand dat je kunt uitvoeren als `python ocr_demo.py`. Het bevat foutafhandeling, optionele pre‑processing en commentaar voor duidelijkheid.

```python
#!/usr/bin/env python3
"""
Complete OCR demo: load image, recognize multilingual text,
and print results. Works with the generic 'ocr' library.
"""

import os
import sys
import ocr

def main(image_path: str):
    # Verify the image exists
    if not os.path.isfile(image_path):
        sys.exit(f"Error: File not found – {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()
    engine.set_languages(['eng', 'rus'])          # load language packs
    engine.set_max_image_size(2500)               # limit memory usage

    # Load the image
    try:
        engine.load_image(image_path)
    except Exception as e:
        sys.exit(f"Failed to load image: {e}")

    # Perform recognition
    try:
        result = engine.recognize()
    except Exception as e:
        sys.exit(f"OCR failed: {e}")

    # Output the text
    print("\n=== OCR Result ===")
    print(result.text)

    # Optional: display confidence scores
    if hasattr(result, "confidence"):
        avg_conf = sum(result.confidence) / len(result.confidence)
        print(f"\nAverage confidence: {avg_conf:.1%}")

if __name__ == "__main__":
    # Replace with your actual image path or pass as CLI argument
    img = sys.argv[1] if len(sys.argv) > 1 else "YOUR_DIRECTORY/multilingual.png"
    main(img)
```

Voer het uit met:

```bash
python ocr_demo.py path/to/multilingual.png
```

Je zou dezelfde uitvoer moeten zien als eerder getoond, wat bevestigt dat je **tekst uit afbeelding hebt gehaald**.

## Conclusie

We hebben behandeld **hoe OCR uit te voeren** in Python van begin tot eind: de bibliotheek installeren, een afbeelding laden, meertalige inhoud herkennen, en de meest voorkomende randgevallen afhandelen. Door deze gids te volgen kun je nu **afbeelding naar tekst converteren**, **speciale tekens herkennen**, en **tekst uit afbeelding extraheren** in je eigen projecten—geen handmatige transcriptie meer.

Wat nu? Probeer te experimenteren met:

- Het toevoegen van meer taalpakketten (bijv. `spa` voor Spaans).  
- Resultaten exporteren naar JSON voor downstream verwerking.  
- De OCR‑stap integreren in een Flask‑API zodat andere services het kunnen aanroepen.  

Als je tegen vreemde problemen aanloopt, is de community rond de meeste OCR‑bibliotheken actief—zoek naar “ocr library language pack installation” of laat een reactie achter hieronder. Veel programmeerplezier, en geniet van het omzetten van afbeeldingen naar doorzoekbare tekst!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}