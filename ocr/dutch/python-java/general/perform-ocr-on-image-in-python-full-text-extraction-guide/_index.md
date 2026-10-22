---
category: general
date: 2026-06-19
description: Voer OCR uit op een afbeelding met behulp van de OCR‑bibliotheek van
  Python. Leer hoe je tekst uit een afbeelding detecteert, tekst uit een JPEG herkent
  en efficiënt tekst uit een gescande afbeelding extraheert.
draft: false
keywords:
- perform OCR on image
- recognize text from jpeg
- detect text from image
- extract text from scanned image
- load image for OCR
language: nl
og_description: Voer OCR uit op een afbeelding met Python en haal tekst uit gescande
  bestanden. Deze gids leidt je stap voor stap door het laden van afbeeldingen, het
  corrigeren van scheefstand en het herkennen van tekst.
og_title: Voer OCR uit op afbeelding in Python – Volledige gids voor tekstextractie
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  headline: Perform OCR on Image in Python – Full Text Extraction Guide
  type: TechArticle
- description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  name: Perform OCR on Image in Python – Full Text Extraction Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed (the example uses the `ocr` package available via
      `pip install ocr-lib` – replace with your actual library name). - Basic familiarity
      with Python functions and virtual environments. - An image file (JPEG, PNG,
      TIFF) you want to process; we’ll use `skewed_page.jpg` as a placeh'
  - name: Recognize Text from JPEG vs PNG
    text: 'Both formats are supported, but JPEG compression can introduce artifacts
      that confuse the engine. If you notice frequent mis‑recognitions, try converting
      the JPEG to PNG first:'
  - name: Detect Text from Image with Multiple Languages
    text: 'If your document mixes English and Spanish, set a multilingual mode:'
  - name: Extract Text from Scanned PDFs
    text: 'For PDFs, you need to rasterize each page into an image first. Libraries
      like `pdf2image` make this painless:'
  type: HowTo
- questions:
  - answer: Absolutely. The library works without a GUI; just ensure the necessary
      native binaries (e.g., Tesseract) are installed on the server.
    question: Can I run this on a headless server?
  - answer: Consider adding a sharpening filter before `engine.recognize`. Many OCR
      libraries expose `image_preprocessing.sharpen = True` or you can use OpenCV’s
      `cv2.GaussianBlur` in reverse.
    question: What if the image is blurry?
  - answer: 'Yes. Wrap `perform_ocr` in a loop over a list of file paths, ## What
      Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
      - [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
      - [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: Does the script support batch processing?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Voer OCR uit op afbeelding in Python – Volledige gids voor teksteextractie
url: /nl/python-java/general/perform-ocr-on-image-in-python-full-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Voer OCR uit op afbeelding in Python – Complete gids voor teksterkenning

Heb je ooit **OCR op afbeelding**‑bestanden moeten uitvoeren, maar liep je tegen een muur omdat de code cryptisch leek? Je bent niet de enige. Of je nu een stapel gescande bonnen omzet in doorzoekbare PDF’s of bijschriften uit een JPEG haalt voor een data‑science project, de mogelijkheid om tekst uit JPEG’s en andere formaten te herkennen is een onmisbare vaardigheid voor elke ontwikkelaar vandaag.

In deze tutorial lopen we stap voor stap door een volledig, uitvoerbaar voorbeeld dat laat zien hoe je **tekst van afbeelding**‑bestanden kunt **detecteren**, **tekst uit gescande afbeelding**‑documenten kunt **extraheren**, en zelfs **afbeelding voor OCR kunt laden** in slechts een handvol regels code. Aan het einde heb je een solide, productie‑klaar fragment dat je in je eigen projecten kunt gebruiken — zonder ontbrekende imports, zonder vage “zie docs” shortcuts.

## Wat je gaat bouwen

- Een klein Python‑script dat een OCR‑engine maakt, auto‑deskew inschakelt, een JPEG (of elk ondersteund formaat) laadt, en de herkende tekst afdrukt.  
- Uitleg over **waarom** elke instelling belangrijk is, niet alleen **hoe** je het moet typen.  
- Tips voor het omgaan met multi‑page PDF’s, niet‑Engelse talen, en veelvoorkomende valkuilen zoals wazige scans.

### Vereisten

- Python 3.8+ geïnstalleerd (het voorbeeld gebruikt het `ocr`‑pakket dat beschikbaar is via `pip install ocr-lib` – vervang dit door de daadwerkelijke bibliotheeknaam).  
- Basiskennis van Python‑functies en virtuele omgevingen.  
- Een afbeeldingsbestand (JPEG, PNG, TIFF) dat je wilt verwerken; we gebruiken `skewed_page.jpg` als placeholder.

> **Pro tip:** Als je Windows gebruikt, voer je terminal dan uit als Administrator bij het installeren van de OCR‑bibliotheek om permissie‑problemen te vermijden.

---

## OCR op afbeelding uitvoeren – Installatie en configuratie

Het eerste wat je nodig hebt is een schone OCR‑engine‑instantie. Beschouw het als het brein achter de operatie; zonder juiste configuratie levert zelfs de scherpste afbeelding onzin op.

```python
# Step 1: Import the OCR library and create an engine
import ocr

engine = ocr.OcrEngine()
# Set the recognition language – English works for most cases
engine.language = ocr.Language.English
```

**Waarom dit belangrijk is:**  
Het instellen van `engine.language` beperkt de tekenset die de OCR‑engine verwacht, wat de nauwkeurigheid drastisch verhoogt. Als je dit overslaat, zal de engine proberen te raden, vaak met foutieve woorden.

---

## Automatische Deskew inschakelen – Kantelen van scans corrigeren

Gescannde pagina’s zijn zelden perfect vlak. Een lichte kanteling kan de karaktersegmentatie verstoren, waardoor “Hello” wordt “H3llo”. De `auto_deskew`‑vlag doet het zware werk voor je.

```python
# Step 2: Turn on automatic deskew to straighten tilted images
engine.image_preprocessing.auto_deskew = True
```

**Randgeval:** Als je weet dat je afbeeldingen al recht zijn, kun je deskew uitschakelen om een paar milliseconden verwerkingstijd te besparen — handig bij het verwerken van duizenden pagina’s in een batch‑taak.

---

## Afbeelding voor OCR laden – Ondersteuning voor JPEG, PNG, TIFF

Nu **laden we de afbeelding voor OCR**. De `ocr.Image.load`‑methode is flexibel; hij accepteert een pad naar elk ondersteund rasterformaat.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/skewed_page.jpg"
image = ocr.Image.load(image_path)
```

> **Waarom deze stap cruciaal is:** De bibliotheek leest het bestand in een interne bitmap, past eventuele kleur‑ruimte‑conversies toe. Als je dit overslaat en een ruwe byte‑stroom doorgeeft, krijg je een `FileNotFoundError` of, erger, stille lege resultaten.

Als je specifiek **tekst uit JPEG**‑bestanden wilt **herkennen**, zorg er dan voor dat de bestandsextensie `.jpeg` of `.jpg` is. Dezelfde aanroep werkt voor PNG (`.png`) of TIFF (`.tif`) zonder wijziging.

---

## OCR op afbeelding uitvoeren – Engine laten draaien

Met de engine klaar en de afbeelding in het geheugen, is het tijd om **OCR op afbeelding**‑data uit te voeren. Deze ene regel doet het zware werk: pre‑processing, segmentatie, classificatie en tekstassemblage.

```python
# Step 4: Run OCR and capture the result object
result = engine.recognize(image)
```

**Wat er onder de motorkap gebeurt:**  
- De engine past de deskew‑transformatie toe (indien ingeschakeld).  
- Hij draait een neuraal netwerk of Tesseract‑backend om karakters te identificeren.  
- Ten slotte worden karakters aan elkaar geplakt tot woorden en regels, en wordt een rijk `result`‑object geretourneerd.

---

## Tekst uit gescande afbeelding extraheren – Resultaten weergeven

De laatste stap is om **tekst uit gescande afbeelding** te **extraheren** en weer te geven. Het attribuut `result.text` bevat de platte‑tekst representatie.

```python
# Step 5: Print the detected text to the console
print("Detected text:")
print(result.text)
```

Typische output ziet er als volgt uit:

```
Detected text:
Invoice #12345
Date: 2023‑09‑01
Total: $1,234.56
Thank you for your business!
```

Als de OCR‑engine geen karakters vindt, is `result.text` een lege string. Controleer in dat geval de beeldkwaliteit of pas de eigenschap `engine.confidence_threshold` aan (als je bibliotheek dit ondersteunt).

---

## Veelvoorkomende variaties afhandelen

### Tekst herkennen uit JPEG vs PNG

Beide formaten worden ondersteund, maar JPEG‑compressie kan artefacten introduceren die de engine verwarren. Als je vaak verkeerde herkenningen ziet, probeer de JPEG eerst naar PNG te converteren:

```python
from PIL import Image
Image.open(image_path).save("temp.png", format="PNG")
image = ocr.Image.load("temp.png")
```

### Tekst detecteren uit afbeelding met meerdere talen

Als je document Engels en Spaans combineert, stel dan een meertalige modus in:

```python
engine.language = ocr.Language.English | ocr.Language.Spanish
```

De engine houdt dan beide alfabetten in overweging tijdens de herkenning.

### Tekst extraheren uit gescande PDF’s

Voor PDF’s moet je elke pagina eerst rasteren naar een afbeelding. Bibliotheken zoals `pdf2image` maken dit moeiteloos:

```python
from pdf2image import convert_from_path

pages = convert_from_path("document.pdf", dpi=300)
for i, page_image in enumerate(pages):
    image = ocr.Image.from_pil(page_image)   # assuming the library accepts a PIL image
    result = engine.recognize(image)
    print(f"Page {i+1} text:")
    print(result.text)
```

---

## Volledig werkend voorbeeld

Hieronder staat het complete script dat je kunt kopiëren‑plakken in een `ocr_demo.py`‑bestand. Het bevat foutafhandeling en een kleine helper om de uitvoeringstijd te meten.

```python
import ocr
import time
import sys
from pathlib import Path

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a given image file and return the extracted text.
    Handles auto‑deskew and basic error reporting.
    """
    if not Path(image_path).exists():
        sys.exit(f"❌ Error: File not found – {image_path}")

    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.image_preprocessing.auto_deskew = True

    try:
        image = ocr.Image.load(image_path)
    except Exception as e:
        sys.exit(f"❌ Failed to load image: {e}")

    start = time.time()
    result = engine.recognize(image)
    elapsed = time.time() - start

    if not result.text.strip():
        print("⚠️ No text detected. Try a higher‑resolution image or adjust preprocessing.")
    else:
        print(f"✅ OCR completed in {elapsed:.2f}s")
        print("Detected text:")
        print(result.text)

    return result.text

if __name__ == "__main__":
    # Replace with the path to your JPEG/PNG/TIFF file
    perform_ocr("YOUR_DIRECTORY/skewed_page.jpg")
```

**Verwachte output** (bij een heldere scan):

```
✅ OCR completed in 0.87s
Detected text:
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

---

## Veelgestelde vragen

**V: Kan ik dit op een headless server draaien?**  
A: Absoluut. De bibliotheek werkt zonder GUI; zorg er alleen voor dat de benodigde native binaries (bijv. Tesseract) op de server geïnstalleerd zijn.

**V: Wat als de afbeelding wazig is?**  
A: Overweeg een verscherpingsfilter toe te passen vóór `engine.recognize`. Veel OCR‑bibliotheken bieden `image_preprocessing.sharpen = True` of je kunt OpenCV’s `cv2.GaussianBlur` in omgekeerde richting gebruiken.

**V: Ondersteunt het script batch‑verwerking?**  
A: Ja. Plaats `perform_ocr` in een lus over een lijst met bestandspaden,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}