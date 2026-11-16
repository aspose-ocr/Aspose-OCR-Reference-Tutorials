---
category: general
date: 2026-03-18
description: Leer hoe je tekst uit afbeeldingen kunt extraheren en gescande afbeeldingstekst
  kunt omzetten naar bewerkbare strings met Aspose OCR in Python. Stapsgewijze code
  inbegrepen.
draft: false
keywords:
- extract text from images
- convert scanned images text
- Aspose OCR Python
- batch OCR processing
- image to text conversion
language: nl
og_description: Haal tekst uit afbeeldingen met Aspose OCR in Python. Deze tutorial
  laat zien hoe je tekst van gescande afbeeldingen kunt converteren met slechts een
  paar regels code.
og_title: Tekst extraheren uit afbeeldingen met Aspose OCR – Python‑gids
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Tekst extraheren uit afbeeldingen met Aspose OCR – Python‑gids
url: /nl/python-java/general/extract-text-from-images-with-aspose-ocr-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit afbeeldingen met Aspose OCR – Python-gids

Heb je ooit **tekst uit afbeeldingen moeten extraheren** maar wist je niet waar je moest beginnen? Je bent niet de enige—ontwikkelaars krijgen voortdurend de last van het omzetten van gescande PDF's, ruisende screenshots of gefotografeerde bonnetjes naar doorzoekbare, bewerkbare strings.  

Het goede nieuws? Met Aspose OCR voor Python kun je **gescande afbeeldings‑tekst** in bulk **converteren**, zonder je IDE te verlaten. In deze tutorial lopen we een compleet, kant‑klaar voorbeeld door dat precies laat zien hoe je het doet, waarom elke stap belangrijk is en waar je op moet letten.

## Wat je zult leren

- De Aspose OCR‑bibliotheek instellen in een Python‑omgeving.  
- Een lijst met afbeeldingsbestanden voorbereiden (PNG, JPG, TIFF, enz.).  
- Batch‑OCR uitvoeren met één methode‑aanroep.  
- De geëxtraheerde tekst voor elk bestand ophalen en weergeven.  
- Veelvoorkomende valkuilen behandelen, zoals niet‑ondersteunde formaten en geheugenverbruik bij grote bestanden.  

Aan het einde heb je een herbruikbaar script dat **tekst uit afbeeldingen** op aanvraag kan **extraheren**—perfect voor het automatiseren van gegevensinvoer, het indexeren van documenten, of het voeden van downstream NLP‑pijplijnen.

---

![Voorbeeld van tekst extraheren uit afbeeldingen](/images/ocr-extract-text.png "tekst uit afbeeldingen extraheren")

*Afbeeldings‑alt‑tekst: “tekst uit afbeeldingen extraheren met Aspose OCR in Python”*

## Vereisten

- Python 3.8 of nieuwer (de code gebruikt f‑strings).  
- Een geldige Aspose OCR voor Python‑licentie of een gratis proef‑sleutel.  
- De afbeeldingen die je wilt verwerken, lokaal opgeslagen (een willekeurige mix van PNG, JPG of TIFF).  

Als je al een virtuele omgeving hebt, prima—zo niet, maak er een met:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate
```

Nu ben je klaar om de SDK te installeren.

## Stap 1: Installeer de Aspose OCR SDK

Aspose distribueert zijn OCR‑engine via PyPI, dus één `pip`‑opdracht doet het werk:

```bash
pip install aspose-ocr
```

> **Pro tip:** Pin de versie (bijv. `aspose-ocr==22.12`) om later onverwachte breaking changes te voorkomen.

## Stap 2: Importeer de OCR‑engine‑klasse

De kernklasse waarmee je werkt is `OcrEngine`. Importeer deze bovenaan je script:

```python
# Step 2: Import the OCR engine class
from asposeocr import OcrEngine
```

> *Waarom dit belangrijk is:* Alleen importeren wat je nodig hebt houdt de opstarttijd laag, vooral wanneer je het script later in een grotere applicatie integreert.

## Stap 3: Definieer de te verwerken afbeeldingsbestanden

Maak een Python‑list met de volledige paden naar elke afbeelding die je wilt scannen. Vervang `YOUR_DIRECTORY` door het daadwerkelijke mappad.

```python
# Step 3: Define the image files to be processed
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.jpg",
    "YOUR_DIRECTORY/page3.tif"
]
```

> **Randgeval:** Als je honderden bestanden hebt, overweeg dan om deze lijst programmatisch te genereren met `glob.glob('*.png')` om handmatige bewerkingen te vermijden.

## Stap 4: Voer OCR uit op alle afbeeldingen tegelijk

Aspose OCR biedt een handige `processMultiple`‑methode die een lijst van `OcrResult`‑objecten retourneert—één voor elk invoerbestand.

```python
# Step 4: Run OCR on all images at once
ocr_engine = OcrEngine()               # instantiate the engine
ocr_results = ocr_engine.processMultiple(image_files)
```

> *Waarom batchverwerking?* Het afzonderlijk verzenden van elke afbeelding veroorzaakt extra overhead (initialiseren van de engine, laden van native libraries). De batch‑aanroep vermindert CPU‑belasting en versnelt de algehele taak.

### Fouten netjes afhandelen

Als een afbeelding niet gelezen kan worden (beschadigd bestand, niet‑ondersteund formaat), zal `processMultiple` een uitzondering gooien. Plaats de aanroep in een `try/except`‑blok om het script levend te houden:

```python
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as e:
    print(f"⚠️ OCR failed: {e}")
    ocr_results = []   # fallback to empty list
```

## Stap 5: Geef de geëxtraheerde tekst voor elk bestand weer

Itereer over de resultaten, koppel elk `OcrResult` aan de oorspronkelijke bestandsnaam. De `getText()`‑methode retourneert de herkende string.

```python
# Step 5: Output the extracted text for each file
for index, result in enumerate(ocr_results, start=1):
    file_path = image_files[index - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")   # add a blank line for readability
```

### Verwachte output

Het uitvoeren van het volledige script op drie eenvoudige screenshots kan iets opleveren als:

```
--- Text from file YOUR_DIRECTORY/page1.png ---
Invoice #12345
Date: 2024‑07‑01
Total: $256.78

--- Text from file YOUR_DIRECTORY/page2.jpg ---
Welcome to the Annual Report
Prepared by: Finance Dept.

--- Text from file YOUR_DIRECTORY/page3.tif ---
© 2025 Acme Corp. All rights reserved.
```

Als een afbeelding geen herkenbare tekens bevat, zie je een lege string—er breekt niets, en je kunt beslissen of je dat bestand wilt markeren voor handmatige controle.

## Bonus: OCR‑nauwkeurigheid fijn afstellen

Aspose OCR biedt verschillende optionele instellingen waarmee je kunt experimenteren:

| Instelling | Wat het doet | Wanneer te gebruiken |
|------------|--------------|----------------------|
| `ocr_engine.setLanguage('eng')` | Dwingt het Engelse taalmodel af (vermindert false positives). | Meestal Engelse documenten. |
| `ocr_engine.setResolution(300)` | Verbetert de nauwkeurigheid bij scans met lage dpi. | Scans onder 200 dpi. |
| `ocr_engine.setPageSegMode('single_block')` | Behandelt de hele afbeelding als één tekstblok. | Eenvoudige bonnetjes of ID‑kaarten. |

Je kunt deze regels direct na het aanmaken van `ocr_engine` toevoegen:

```python
ocr_engine.setLanguage('eng')
ocr_engine.setResolution(300)
ocr_engine.setPageSegMode('single_block')
```

## Veelvoorkomende valkuilen & hoe ze te vermijden

1. **Grote TIFF‑stapels** – Een multi‑page TIFF kan gigabytes RAM verbruiken wanneer deze in één keer wordt geladen. Splits het bestand in enkel‑pagina afbeeldingen voordat je ze aan `processMultiple` doorgeeft.  
2. **Niet‑Latijnse scripts** – Als je **tekst uit afbeeldingen** moet extraheren die Cyrillisch, Arabisch of Chinees bevatten, wijzig dan de taalcode overeenkomstig (`'rus'`, `'ara'`, `'chi_sim'`).  
3. **Spaties in bestandspaden** – Windows‑paden met spaties kunnen een `FileNotFoundError` veroorzaken. Plaats elk pad in een raw‑string (`r"C:\My Folder\image.png"`) of gebruik `os.path.abspath`.  

Deze problemen van tevoren aanpakken bespaart je later cryptische runtime‑fouten.

---

## Volledig werkend voorbeeld

Hieronder staat het volledige script dat je kunt kopiëren‑plakken in een bestand genaamd `batch_ocr.py`. Het bevat alle best‑practice‑aanpassingen die hierboven zijn besproken.

```python
# batch_ocr.py
# -------------------------------------------------
# Complete example: extract text from images using Aspose OCR (Python)
# -------------------------------------------------

from asposeocr import OcrEngine
import os

# -------------------------------------------------
# Configuration – adjust these values for your environment
# -------------------------------------------------
IMAGE_DIR = "YOUR_DIRECTORY"   # <-- replace with your folder path
SUPPORTED_EXT = (".png", ".jpg", ".jpeg", ".tif", ".tiff")

# Build a list of image file paths automatically
image_files = [
    os.path.join(IMAGE_DIR, f)
    for f in os.listdir(IMAGE_DIR)
    if f.lower().endswith(SUPPORTED_EXT)
]

if not image_files:
    print("⚠️ No supported image files found in the specified directory.")
    exit(1)

# -------------------------------------------------
# Initialize OCR engine with optional tweaks
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.setLanguage('eng')          # English language model
ocr_engine.setResolution(300)          # Boost low‑dpi accuracy
ocr_engine.setPageSegMode('single_block')  # Treat whole image as one block

# -------------------------------------------------
# Run batch OCR and handle potential errors
# -------------------------------------------------
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as exc:
    print(f"❌ OCR processing failed: {exc}")
    ocr_results = []

# -------------------------------------------------
# Display extracted text
# -------------------------------------------------
for idx, result in enumerate(ocr_results, start=1):
    file_path = image_files[idx - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")
```

Sla op, activeer je virtuele omgeving, en voer uit:

```bash
python batch_ocr.py
```

Je zou de geëxtraheerde strings in de console moeten zien afgedrukt, klaar voor verdere verwerking (bijv. opslaan in een database of voeden van een natural‑language‑model).

---

## Conclusie

In deze gids hebben we laten zien hoe je **tekst uit afbeeldingen** kunt **extraheren** met Aspose OCR voor Python, waarbij we alles behandelen van installatie tot batchverwerking en foutafhandeling. Het script is compact, volledig functioneel en gemakkelijk uit te breiden—of je nu **gescande afbeeldings‑tekst** wilt **converteren** naar CSV‑bestanden, een zoekindex wilt voeden, of simpelweg gegevensinvoer wilt automatiseren.

Klaar voor de volgende stap? Overweeg om deze OCR‑pipeline te combineren met een PDF‑merger om doorzoekbare PDF's te maken, of koppel het aan een cloud‑opslag‑trigger zodat elke geüploade scan direct wordt verwerkt. De mogelijkheden zijn eindeloos, en je hebt nu een solide basis om op voort te bouwen.

Heb je vragen of ideeën voor verbetering? Laat een reactie achter hieronder, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}