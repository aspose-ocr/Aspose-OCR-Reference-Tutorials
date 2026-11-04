---
category: general
date: 2026-06-25
description: Python OCR‑tutorial die laat zien hoe je tekst uit PNG‑bestanden haalt,
  tekstafbeeldingen leest en afbeeldingstekst herkent met een eenvoudige, licentievrije
  engine.
draft: false
keywords:
- python ocr tutorial
- extract text png
- read text image
- recognize image text
- load image for ocr
language: nl
og_description: De Python OCR‑tutorial leert je hoe je een afbeelding laadt voor OCR,
  tekst uit PNG‑bestanden extraheert en afbeeldings­tekst herkent in slechts een paar
  regels code.
og_title: Python OCR-tutorial – Tekst uit PNG extraheren
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  headline: 'Python OCR Tutorial: Extract Text from PNG Images'
  type: TechArticle
- description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  name: 'Python OCR Tutorial: Extract Text from PNG Images'
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer (the library works with 3.7+ but 3.8+ is recommended).
      - Basic familiarity with pip and virtual environments. - An image file named
      `sample.png` (or any PNG you’d like to test) saved in a folder you can reference.'
  - name: 1. Low Contrast or Dark Backgrounds
    text: '```python # Increase contrast before recognition (optional step) image
      = image.adjust_contrast(1.5) # 1.0 = no change, >1 = higher contrast result
      = engine.recognize(image) ```'
  - name: 2. Skewed Text Lines
    text: '```python # Auto‑deskew the image image = image.deskew() result = engine.recognize(image)
      ```'
  - name: 3. Non‑English Characters
    text: 'If your PNG contains accented letters or non‑Latin scripts, initialise
      the engine with the appropriate language pack:'
  - name: 4. Very Large Images
    text: 'Processing a 4000×3000 PNG can be slow. Downscale it while preserving readability:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Tutorial
title: 'Python OCR-tutorial: Tekst extraheren uit PNG-afbeeldingen'
url: /nl/python-java/general/python-ocr-tutorial-extract-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR Tutorial – Tekst extraheren uit PNG-afbeeldingen

Heb je je ooit afgevraagd hoe **python ocr tutorial** een screenshot van een bon kan omzetten in bewerkbare tekst? Je bent niet de enige. In veel real‑world projecten moeten we snel *read text image* bestanden lezen, en het zelf doen is beter dan elke keer copy‑pasten vanuit een GUI.

In deze gids lopen we een hands‑on voorbeeld door dat **extracts text PNG** bestanden verwerkt, je laat zien hoe je *load image for OCR* kunt doen, en uiteindelijk de *recognize image text* resultaat afdrukt — allemaal met een gratis, alleen‑evaluatie OCR‑engine. Geen licentiesleutels, geen zware afhankelijkheden — alleen plain Python en een paar kleine pakketten.

## Wat je zult leren

- Hoe je de lichte OCR‑bibliotheek installeert en importeert.
- De exacte stappen om **load image for OCR** te doen en veelvoorkomende valkuilen af te handelen.
- Manieren om **read text image** bestanden van verschillende kwaliteit te lezen.
- Tips om de nauwkeurigheid te verbeteren wanneer je **extract text png** bestanden verwerkt.
- Hoe je de herkende string weergeeft en optioneel naar schijf schrijft.

### Vereisten

- Python 3.8 of nieuwer (de bibliotheek werkt met 3.7+, maar 3.8+ wordt aanbevolen).
- Basiskennis van pip en virtuele omgevingen.
- Een afbeeldingsbestand genaamd `sample.png` (of elke PNG die je wilt testen) opgeslagen in een map die je kunt refereren.

Als een van deze onbekend klinkt, pauzeer dan een minuut en stel ze in — geloof me, de opbrengst is het waard.

---

## Python OCR Tutorial – De engine instellen

Allereerst hebben we een OCR‑engine‑object nodig. De bibliotheek die we gebruiken is een kleine wrapper rond een native OCR‑engine die direct uit de doos werkt voor evaluatie. Het vereist geen licentiesleutel, waardoor de *python ocr tutorial* perfect is voor snelle prototypes.

```python
# Step 1: Install the OCR package (run once in your terminal)
# pip install simple-ocr-lib

# Step 2: Import the library and create an engine instance
import ocr

# No license needed for evaluation mode – the engine is ready to go
engine = ocr.OcrEngine()
```

**Waarom dit belangrijk is:** Het creëren van de engine isoleert de OCR‑runtime van de rest van je code, waardoor je deze kunt hergebruiken voor meerdere afbeeldingen zonder elke keer zware bronnen opnieuw te initialiseren.

---

## Afbeelding laden voor OCR – Een PNG‑bestand lezen

Nu de engine bestaat, moeten we *load image for OCR*. De `Image.load`‑methode van de bibliotheek accepteert een pad en decodeert automatisch PNG, JPEG, BMP en enkele andere formaten.

```python
# Step 3: Load the PNG you want to process
image_path = "YOUR_DIRECTORY/sample.png"   # replace with your actual path
image = ocr.Image.load(image_path)
```

> **Pro tip:** Als je PNG een alfakanaal bevat, zal de bibliotheek dit automatisch verwijderen. Voor de beste resultaten bij *read text image* taken, houd de afbeelding in grijstinten — dit vermindert ruis en versnelt de herkenning.

---

## Afbeeldingstekst herkennen – De OCR‑engine draaien

Met het afbeeldingobject klaar, kunnen we eindelijk **recognize image text**. Dit is de kern van de *python ocr tutorial* en vereist slechts één regel code.

```python
# Step 4: Perform OCR on the loaded image
result = engine.recognize(image)
```

**Wat er onder de motorkap gebeurt:** De engine voert een reeks preprocessing‑filters uit (kantelcorrectie, binarisatie) voordat de bitmap wordt gevoed aan een neuraal netwerk getraind op miljoenen tekens. Daarom krijg je vaak verrassend nauwkeurige output, zelfs bij low‑resolution PNG's.

---

## De geëxtraheerde tekst weergeven en opslaan

Het resultaat hebben is geweldig, maar je wilt het waarschijnlijk zien of ergens opslaan. Het `result`‑object biedt een `text`‑attribuut dat de platte‑string output bevat.

```python
# Step 5: Print the recognized text to the console
print("Eval-mode result:", result.text)

# Optional: Save the text to a .txt file for later use
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**Verwachte output** (ervan uitgaande dat `sample.png` “Hello, OCR!” bevat):

```
Eval-mode result: Hello, OCR!
```

Als je rommel krijgt in plaats van leesbare tekens, bekijk dan de volgende sectie voor veelvoorkomende oplossingen.

---

## Veelvoorkomende problemen behandelen bij het extraheren van tekst PNG

Zelfs de beste OCR‑engines struikelen over bepaalde afbeeldingen. Hieronder staan typische obstakels en hoe je ze kunt overwinnen.

### 1. Laag contrast of donkere achtergronden

```python
# Increase contrast before recognition (optional step)
image = image.adjust_contrast(1.5)   # 1.0 = no change, >1 = higher contrast
result = engine.recognize(image)
```

### 2. Scheve tekstregels

```python
# Auto‑deskew the image
image = image.deskew()
result = engine.recognize(image)
```

### 3. Niet‑Engelse tekens

Als je PNG accenten of niet‑Latijnse scripts bevat, initialiseert je de engine met het juiste taalpakket:

```python
engine = ocr.OcrEngine(languages=["eng", "spa"])   # English + Spanish
```

### 4. Zeer grote afbeeldingen

Het verwerken van een 4000×3000 PNG kan traag zijn. Schaal het omlaag terwijl je de leesbaarheid behoudt:

```python
image = image.resize(width=1024)   # keep aspect ratio
result = engine.recognize(image)
```

Deze aanpassingen maken deel uit van een robuuste *python ocr tutorial* die werkt buiten het happy‑path scenario.

---

## Volledig script – Eén‑bestand oplossing

Hieronder staat het volledige, kant‑klaar script dat alle besproken stappen en optionele verbeteringen bevat. Kopieer‑en‑plak het in `ocr_extract.py` en voer `python ocr_extract.py` uit.

```python
# ocr_extract.py
# Complete Python OCR tutorial – extract text from PNG images

import ocr
import sys
import os

def main(image_path):
    # Verify the file exists
    if not os.path.isfile(image_path):
        print(f"Error: File not found → {image_path}")
        sys.exit(1)

    # 1️⃣ Create the OCR engine (evaluation mode, no license needed)
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image – this is the "load image for OCR" step
    image = ocr.Image.load(image_path)

    # Optional preprocessing for better accuracy
    # Uncomment any of the following lines as needed:
    # image = image.adjust_contrast(1.5)   # boost contrast
    # image = image.deskew()               # correct skew
    # image = image.resize(width=1024)     # downscale large images

    # 3️⃣ Recognize the text
    result = engine.recognize(image)

    # 4️⃣ Output the result
    print("Eval-mode result:", result.text)

    # 5️⃣ Save to a .txt file (useful for batch processing)
    txt_path = os.path.splitext(image_path)[0] + "_extracted.txt"
    with open(txt_path, "w", encoding="utf-8") as out_file:
        out_file.write(result.text)
    print(f"Extracted text saved to {txt_path}")

if __name__ == "__main__":
    # Pass the image path as a command‑line argument, e.g.:
    # python ocr_extract.py ./samples/sample.png
    if len(sys.argv) < 2:
        print("Usage: python ocr_extract.py <path_to_png>")
        sys.exit(1)
    main(sys.argv[1])
```

**Uitvoeren:**  
```bash
python ocr_extract.py ./sample.png
```

Je zou de herkende string moeten zien afgedrukt en een bestand `sample_extracted.txt` aangemaakt naast de afbeelding.

---

## Visueel overzicht

![Python OCR tutorial – afbeelding laden voor OCR en tekst extraheren uit PNG](/images/python-ocr-flow.png)

*Alt‑tekst:* *Python OCR tutorial diagram dat de stroom toont van het laden van een afbeelding voor OCR tot het extraheren van tekst PNG.*

Het diagram illustreert de lineaire voortgang van **load image for OCR** → **recognize image text** → **extract text PNG** en benadrukt waar je preprocessing‑stappen kunt invoegen.

---

## Conclusie

We hebben zojuist een **python ocr tutorial** afgerond die laat zien hoe je *load image for OCR*, *recognize image text* en uiteindelijk **extract text png** bestanden kunt verwerken met slechts een handvol Python‑commando's. Het script is volledig functioneel, behandelt veelvoorkomende randgevallen, en kan worden uitgebreid voor batchverwerking of meertalige ondersteuning.

Klaar voor de volgende uitdaging? Probeer de engine PDFs die naar afbeeldingen zijn geconverteerd te voeren, experimenteer met verschillende taalpakketten, of integreer de OCR‑stap in een Flask‑API zodat je webapp geüploade screenshots direct kan lezen. De mogelijkheden voor *read text image* automatisering zijn praktisch eindeloos.

Heb je vragen of een lastig beeld dat je niet kunt kraken? Laat een reactie achter hieronder, en laten we samen problemen oplossen. Happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Tekst extraheren uit afbeelding met Aspose OCR – Stapsgewijze gids](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Tekst extraheren uit afbeelding – OCR‑optimalisatie met Aspose.OCR voor .NET](/ocr/english/net/ocr-optimization/)
- [Hoe afbeeldingstekst OCR‑en met taal met behulp van Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}