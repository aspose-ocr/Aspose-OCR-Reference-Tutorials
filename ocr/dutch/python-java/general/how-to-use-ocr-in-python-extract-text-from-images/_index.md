---
category: general
date: 2026-06-16
description: Hoe OCR in Python te gebruiken om tekst uit afbeeldingsbestanden zoals
  PNG te extraheren. Leer stap‑voor‑stap de conversie van afbeelding naar tekst met
  Aspose OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- read text from png
- convert image to text
- ocr image to text python
language: nl
og_description: Hoe OCR in Python te gebruiken om tekst uit afbeeldingen te extraheren.
  Deze gids leidt je door het converteren van PNG‑bestanden naar doorzoekbare tekst
  met Aspose OCR.
og_title: Hoe OCR in Python te gebruiken – Tekst uit afbeeldingen extraheren
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to use OCR in Python to extract text from image files like PNG.
    Learn step‑by‑step conversion of image to text with Aspose OCR.
  headline: How to Use OCR in Python – Extract Text from Images
  type: TechArticle
- description: How to use OCR in Python to extract text from image files like PNG.
    Learn step‑by‑step conversion of image to text with Aspose OCR.
  name: How to Use OCR in Python – Extract Text from Images
  steps:
  - name: Expected Output
    text: '``` Detected language: English Recognized text: Hello, world! This is a
      multi‑language test. こんにちは世界 ```'
  - name: 1. License Not Found
    text: If you see an error like `License file not found`, double‑check the path
      you passed to `set_license`. Using a raw string (`r"..."`) helps avoid escape‑character
      mishaps on Windows.
  - name: 2. Blank Output
    text: 'A blank `ocr_result.text` usually means the image is too noisy or the text
      is too faint. Try increasing the image contrast:'
  - name: 3. Wrong Language Detection
    text: 'If the auto‑detect picks the wrong language, you can force a specific one:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Aspose
title: Hoe OCR in Python te gebruiken – Tekst uit afbeeldingen extraheren
url: /nl/python-java/general/how-to-use-ocr-in-python-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR te gebruiken in Python – Tekst extraheren uit afbeeldingen

Heb je je ooit afgevraagd **hoe je OCR** in een Python‑project kunt gebruiken? Je bent niet de enige. Of je nu een kassabon‑scanner bouwt, een documentarchiver, of gewoon nieuwsgierig bent naar het omzetten van een screenshot naar bewerkbare tekst, de mogelijkheid om **tekst uit afbeelding te extraheren** is een game‑changer.

In deze tutorial lopen we het volledige proces door — van het installeren van de Aspose OCR‑bibliotheek tot het lezen van tekst uit een PNG‑bestand — zodat je **afbeelding naar tekst kunt converteren** met slechts een paar regels code. Aan het einde weet je precies hoe je **tekst uit PNG kunt lezen** en zelfs automatisch meertalige inhoud kunt verwerken.

> **Pro tip:** de automatische taaldetectie van Aspose OCR betekent dat je de taal niet van tevoren hoeft te raden — perfect voor apps die de wereld rondreizen.

## Wat je nodig hebt

- Python 3.8+ (de nieuwste stabiele release is prima)
- Een geldig Aspose OCR‑licentiebestand (`Aspose.OCR.lic`). De gratis proefversie werkt voor testen, maar een juiste licentie verwijdert evaluatielimieten.
- Het Aspose OCR‑pakket geïnstalleerd via `pip`:

```bash
pip install aspose-ocr
```

- Een afbeeldingsbestand dat je wilt verwerken — laten we `sample-multi-lang.png` als demo gebruiken.

Het hebben van deze vereisten zorgt voor een soepele workflow en voorkomt later “module not found”-verrassingen.

![Hoe OCR te gebruiken in Python workflow](https://example.com/ocr-workflow.png "Hoe OCR te gebruiken in Python – stap‑voor‑stap illustratie")

*Afbeeldingsalttekst: Diagram dat laat zien hoe je OCR in Python gebruikt om tekst uit een afbeelding te extraheren.*

## Stap 1: Pas je Aspose OCR‑licentie toe (eenmalig per applicatie vereist)

Het eerste wat elk serieus OCR‑project doet, is een licentie laden. Zonder deze zal Aspose een waarschuwing geven en het aantal pagina's dat je kunt verwerken beperken.

```python
# Import the license class
from aspose.ocr import License

# Create a License object and point it to your .lic file
ocr_license = License()
ocr_license.set_license(r"C:\Path\To\Your\Aspose.OCR.lic")
```

> **Waarom dit belangrijk is:** Het vooraf laden van de licentie zorgt ervoor dat de **ocr image to text python**‑engine op volle snelheid en zonder watermerken draait. Beschouw het als het ontgrendelen van de premium‑functies voordat je met de conversie begint.

## Stap 2: Maak een OCR‑engine aan en schakel automatische taaldetectie in

Nu maken we de kernengine aan. Het inschakelen van `language_auto_detect` is cruciaal wanneer je niet weet of de afbeelding Engels, Spaans, Chinees of een mix van talen bevat.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine
ocr_engine = OcrEngine()

# Turn on auto‑language detection – it works for over 60 languages
ocr_engine.language_auto_detect = True
```

Als je *wel* de taal van tevoren kent, kun je `ocr_engine.language = "English"` instellen (of een andere ondersteunde ISO‑code) om het een beetje te versnellen. Maar voor een algemene “tekst uit PNG lezen”‑utility is auto‑detectie de veiligste keuze.

## Stap 3: Laad de afbeelding die je wilt verwerken

Aspose OCR werkt met verschillende formaten — PNG, JPEG, BMP, TIFF, je noemt het. Laten we een PNG‑bestand laden dat meerdere talen bevat.

```python
from aspose.ocr import Image

# Load the image from disk (replace with your actual path)
ocr_image = Image.load_from_file(r"C:\Path\To\sample-multi-lang.png")

# Assign the image to the engine
ocr_engine.image = ocr_image
```

> **Randgeval:** Als de afbeelding enorm is (meer dan een paar megabytes), wil je deze eerst verkleinen om de prestaties te verbeteren. Aspose biedt `ocr_image.resize(width, height)` hiervoor aan.

## Stap 4: Voer OCR‑herkenning uit

Met alles aangesloten is de daadwerkelijke tekste­xtractie één enkele methode‑aanroep. Het result‑object geeft zowel de herkende tekst als de gedetecteerde taal.

```python
# Run the recognition process
ocr_result = ocr_engine.recognize()
```

Achter de schermen draait Aspose geavanceerde neurale netwerken en patroon‑herkenningsalgoritmen om elke pixelcluster om te zetten in tekens. Het zware werk gebeurt volledig in native code, zodat je **snelle, nauwkeurige OCR** krijgt, zelfs op bescheiden hardware.

## Stap 5: Toon de gedetecteerde taal en de herkende tekst

Laten we tenslotte afdrukken wat we hebben. De eigenschap `detected_language` vertelt je welke taal Aspose heeft geraden, en `text` bevat de volledige transcriptie.

```python
print("Detected language:", ocr_result.detected_language)
print("Recognized text:\n", ocr_result.text)
```

### Verwachte output

```
Detected language: English
Recognized text:
 Hello, world!
 This is a multi‑language test.
 こんにちは世界
```

Als je het script uitvoert op een afbeelding die zowel Engels als Japans bevat, zie je dat de taal automatisch wisselt — dankzij de auto‑detectiefunctie die we eerder hebben ingeschakeld.

## Veelvoorkomende valkuilen behandelen

### 1. Licentie niet gevonden

Als je een fout ziet zoals `License file not found`, controleer dan het pad dat je aan `set_license` hebt doorgegeven. Het gebruik van een raw string (`r"..."`) helpt escape‑karakterproblemen op Windows te vermijden.

### 2. Lege uitvoer

Een lege `ocr_result.text` betekent meestal dat de afbeelding te ruisig is of de tekst te vaag. Probeer het contrast van de afbeelding te verhogen:

```python
ocr_image = Image.load_from_file("sample.png")
ocr_image = ocr_image.adjust_contrast(1.5)  # Boost contrast by 50%
ocr_engine.image = ocr_image
```

### 3. Verkeerde taaldetectie

Als de auto‑detectie de verkeerde taal kiest, kun je een specifieke taal forceren:

```python
ocr_engine.language = "Japanese"  # ISO code or language name
```

## Voorbeeld uitbreiden: batchverwerking van meerdere PNG‑bestanden

Vaak wil je **afbeelding naar tekst converteren** voor een hele map, niet alleen een enkel bestand. Hier is een snelle lus die elke PNG in een map verwerkt:

```python
import os
from pathlib import Path

input_folder = Path(r"C:\Images")
output_folder = Path(r"C:\OCR_Output")
output_folder.mkdir(exist_ok=True)

for png_path in input_folder.glob("*.png"):
    # Load and assign image
    ocr_image = Image.load_from_file(str(png_path))
    ocr_engine.image = ocr_image

    # Recognize
    result = ocr_engine.recognize()

    # Write result to a .txt file with the same base name
    txt_path = output_folder / (png_path.stem + ".txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(f"Detected language: {result.detected_language}\n")
        f.write(result.text)

    print(f"Processed {png_path.name} → {txt_path.name}")
```

Deze code laat een praktische manier zien om **tekst uit afbeelding**‑bestanden in bulk te **extraheren**, een veelvoorkomende eis voor documentdigitaliserings‑pijplijnen.

## Volledig werkend script

Alles samengevoegd, hier is een enkel bestand dat je van begin tot eind kunt uitvoeren:

```python
# ocr_demo.py
import os
from aspose.ocr import License, OcrEngine, Image

# -------------------------------------------------
# 1️⃣ Apply license (replace with your own path)
# -------------------------------------------------
license_path = r"C:\Path\To\Aspose.OCR.lic"
ocr_license = License()
ocr_license.set_license(license_path)

# -------------------------------------------------
# 2️⃣ Create engine and enable auto‑detect
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.language_auto_detect = True

# -------------------------------------------------
# 3️⃣ Load image (change to your PNG file)
# -------------------------------------------------
image_path = r"C:\Path\To\sample-multi-lang.png"
ocr_image = Image.load_from_file(image_path)
ocr_engine.image = ocr_image

# -------------------------------------------------
# 4️⃣ Recognize and output results
# -------------------------------------------------
ocr_result = ocr_engine.recognize()
print("Detected language:", ocr_result.detected_language)
print("Recognized text:\n", ocr_result.text)
```

Sla dit op als `ocr_demo.py`, voer `python ocr_demo.py` uit, en je ziet de taal en tekst op de console afgedrukt.

## Conclusie

We hebben **hoe je OCR** in Python van begin tot eind behandeld, en laten zien hoe je **tekst uit afbeelding** kunt **extraheren**, **tekst uit PNG** kunt **lezen**, en over het algemeen **afbeelding naar tekst kunt converteren** met de krachtige engine van Aspose. Door een licentie te laden, automatische taaldetectie in te schakelen en een afbeelding aan de `OcrEngine` te voeren, krijg je in seconden schone, doorzoekbare tekst.

Wat nu? Probeer Aspose te vervangen door een open‑source alternatief zoals Tesseract om de nauwkeurigheid te vergelijken, experimenteer met PDF‑invoer, of integreer de OCR‑stap in een Flask‑API voor realtime afbeeldingsverwerking. De mogelijkheden zijn eindeloos als je de basis van **ocr image to text python** onder de knie hebt.

Heb je vragen over het omgaan met lastige lettertypen, het schalen van prestaties, of licenties? Laat een reactie achter hieronder, en happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Tekst uit afbeelding extraheren met Aspose OCR – Stapsgewijze gids](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Tekst uit afbeelding extraheren – OCR‑optimalisatie met Aspose.OCR voor .NET](/ocr/english/net/ocr-optimization/)
- [Afbeeldingstekst extraheren C# met taalkeuze met behulp van Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}