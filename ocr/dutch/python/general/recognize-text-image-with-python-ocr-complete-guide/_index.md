---
category: general
date: 2026-06-28
description: Leer hoe je tekstafbeeldingen herkent met Python OCR, tekst‑png‑bestanden
  extraheert en de herkende tekst afdrukt met robuuste foutafhandeling.
draft: false
keywords:
- recognize text image
- extract text png
- load image ocr
- process image ocr
- print recognized text
language: nl
og_description: Stapsgewijze tutorial om een tekstafbeelding te herkennen in Python,
  tekst uit een PNG te extraheren en de herkende tekst veilig af te drukken.
og_title: Herken tekstafbeelding met Python OCR – Complete gids
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
title: Tekstafbeelding herkennen met Python OCR – Complete gids
url: /nl/python/general/recognize-text-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tekstafbeelding herkennen met Python OCR – Complete Gids

Heb je je ooit afgevraagd hoe je **tekstafbeelding** in een Python‑script kunt herkennen zonder een zwaar framework te gebruiken? Je bent niet de enige. Veel ontwikkelaars hebben een snelle manier nodig om *image OCR* te laden van een screenshot, een gescande bon of een eenvoudige PNG en de tekst terug te krijgen.  

In deze tutorial zetten we een minimale OCR‑engine op, koppelen we een aangepaste logger, **load image OCR**, voeren we de **process image OCR** uit, en tenslotte **print recognized text**. Aan het einde heb je een zelfstandige script die ook **extract text png** bestanden on‑demand kan verwerken.

## Wat je mee krijgt

- Een volledig functioneel Python‑fragment dat een OCR‑engine maakt, elke stap logt en fouten elegant afhandelt.  
- Duidelijke uitleg over *waarom* elke regel belangrijk is — zodat je de code kunt aanpassen naar Tesseract, EasyOCR of een andere backend.  
- Tips voor veelvoorkomende valkuilen (ontbrekende fonts, corrupte PNG’s) en hoe je ze kunt debuggen.  

### Vereisten

- Python 3.8+ geïnstalleerd  
- Een OCR‑bibliotheek die een `OcrEngine`‑klasse exposeert (het voorbeeld gebruikt een fictieve maar typische API; vervang deze door `pytesseract`, `easyocr`, etc.).  
- Een PNG‑afbeelding die je wilt analyseren, opgeslagen als `input.png` in een map die je beheert.  

> **Pro tip:** Als je `pytesseract` gebruikt, installeer dan eerst de systeem‑Tesseract‑binary (`sudo apt install tesseract-ocr` op Linux) en daarna `pip install pytesseract pillow`.

---

## ## Recognize Text Image: Logger instellen

Een goede logger is de onbezongen held van elke OCR‑pipeline. Hij vertelt je *wanneer* de engine is gestart, *welk* bestand hij heeft geopend, en *waarom* hij eventueel is mislukt.

```python
# Step 1: Define a simple logger for the OCR engine
def my_logger(level, message):
    """
    level: str – e.g., "INFO", "WARN", "ERROR"
    message: str – human‑readable description of the event
    """
    print(f"[{level}] {message}")
```

*Waarom dit belangrijk is:*  
De logger scheidt diagnostische output van de OCR‑core, waardoor je logs gemakkelijk kunt omleiden naar een bestand, een monitoring‑service of zelfs een UI later.

---

## ## Load Image OCR: De engine een PNG voeren

Voordat de engine **process image OCR** kan uitvoeren, heeft hij een geldig image‑object nodig. De meeste bibliotheken accepteren een Pillow `Image`‑instance.

```python
from PIL import Image

# Step 2: Create the OCR engine and attach the logger
ocr_engine = OcrEngine(logging=my_logger)

# Step 3: Load the image to be processed
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Image.from_file(image_path))
my_logger("INFO", f"Loaded image from {image_path}")
```

*Belangrijke punten:*  

- **load image ocr** – `Image.from_file` verbergt de details van PNG‑decodering.  
- Houd het pad configureerbaar; hard‑coden maakt het script broos.  
- De logger‑aanroep bevestigt dat de afbeelding succesvol is gelezen, wat handig is wanneer het bestand ontbreekt of corrupt is.

---

## ## Process Image OCR: De tekst herkennen

Nu begint het zware werk. De engine scant de bitmap, past zijn neurale netwerken of heuristieken toe, en levert een Unicode‑string op.

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

*Waarom we het in `try/except` wikkelen:*  
OCR kan falen bij lage‑resolutie PNG’s, niet‑ondersteunde kleurmodi of ontbrekende taaldatasets. Het vangen van `OcrException` laat je **print recognized text** alleen uitvoeren wanneer er daadwerkelijk tekst is, en voorkomt cryptische stack‑traces voor eindgebruikers.

---

## ## Print Recognized Text & Extract Text PNG

Als de herkenning geslaagd is, tonen we het resultaat en schrijven we optioneel een `.txt`‑bestand dat de oorspronkelijke PNG‑naam weerspiegelt.

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

*Wat je krijgt:*  

- **print recognized text** – directe visuele feedback in de terminal.  
- Een naast‑elkaar `.txt`‑bestand dat effectief **extract text png** voor downstream verwerking (zoekindexering, gegevensinvoer, etc.).

---

## ## Veelvoorkomende randgevallen & hoe ze aan te pakken

| Situatie | Symptom | Oplossing |
|-----------|---------|-----|
| PNG is alleen grijswaarden | OCR geeft lege string terug | Converteer naar RGB (`Image.convert("RGB")`) voordat je de engine voedt. |
| Taal niet ondersteund | `OcrException` met code `LANG_NOT_FOUND` | Installeer het taalpakket (bijv. `tesseract‑lang‑fra` voor Frans) en stel `ocr_engine.language = "fra"` in. |
| Zeer grote afbeelding ( > 5 MB ) | Trage herkenning of geheugenfout | Schaal down met `image.thumbnail((2000, 2000))` vóór `set_image`. |
| Onverwachte tekens | Vervormde output | Zorg dat het bestand echt een PNG is; sommige bestanden doen zich voor als PNG maar zijn JPEG’s. Gebruik `Image.verify()` om te valideren. |

---

## ## Volledig werkend voorbeeld (Klaar om te kopiëren)

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

**Verwachte console‑output (happy path):**

```
[INFO] Loaded image from YOUR_DIRECTORY/input.png
[INFO] OCR succeeded
Recognized text: Invoice #12345
Total Amount: $1,250.00
Date: 2026‑06‑01
[INFO] Saved extracted text to YOUR_DIRECTORY/input.txt
```

Als er iets misgaat, zie je een duidelijke `[ERROR]`‑regel met de reden, dankzij de aangepaste logger.

---

## ## Volgende stappen & gerelateerde onderwerpen

- **extract text png** uit batches: wikkel het script in een `for`‑loop die een mapboom doorloopt.  
- **process image ocr** met pre‑processing (deskew, contrastverhoging) via OpenCV voordat je de engine voedt.  
- Schakel over naar een cloud‑OCR‑service (Google Vision, Azure Read) door de `OcrEngine`‑implementatie te vervangen — je omliggende code blijft hetzelfde.  
- Leer hoe je **print recognized text** in PDF’s kunt plaatsen met `reportlab` voor geautomatiseerde rapportgeneratie.  

---

## Conclusie

We hebben zojuist een compacte, productie‑klare manier doorlopen om **tekstafbeelding** te herkennen in Python, van het laden van de PNG tot **print recognized text** en het opslaan van het resultaat. Door een kleine logger toe te voegen, uitzonderingen af te handelen en optioneel de output te persisteren, is het script klaar voor zowel snelle experimenten als integratie in grotere pipelines.

Probeer het met je eigen screenshots, experimenteer met beeld‑pre‑processing, en je zult al snel tekst uit elke PNG kunnen extraheren die je tegenkomt. Vragen? Laat een reactie achter — happy OCRing!  

![recognize text image example](placeholder.png)


## Wat moet je hierna leren?


De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementaties in je eigen projecten te verkennen.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}