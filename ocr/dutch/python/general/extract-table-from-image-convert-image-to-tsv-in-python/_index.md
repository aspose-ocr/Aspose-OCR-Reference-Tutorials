---
category: general
date: 2026-07-05
description: Tabel uit afbeelding extraheren met Python OCR. Leer hoe je een tabel
  kunt extraheren, een afbeelding naar TSV kunt converteren en beheers OCR‑tabelafbeelding
  Python‑technieken.
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: nl
og_description: Tabel extraheren uit afbeelding met Python OCR. Deze gids laat zien
  hoe je een tabel kunt extraheren, een afbeelding naar TSV kunt converteren en OCR‑tabelafbeeldings‑Python‑tools
  kunt gebruiken.
og_title: Tabel uit afbeelding extraheren – Afbeelding naar TSV converteren in Python
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  headline: Extract Table from Image – Convert Image to TSV in Python
  type: TechArticle
- description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  name: Extract Table from Image – Convert Image to TSV in Python
  steps:
  - name: Initialise the aocr OCR engine.
    text: Initialise the aocr OCR engine.
  - name: Attach the AI post‑processor.
    text: Attach the AI post‑processor.
  - name: Load a table image.
    text: Load a table image.
  - name: Perform structured OCR.
    text: Perform structured OCR.
  - name: Clean the results.
    text: Clean the results.
  - name: Export the table as a TSV file.
    text: Export the table as a TSV file.
  type: HowTo
tags:
- OCR
- Python
- Table Extraction
title: Tabel extraheren uit afbeelding – Afbeelding omzetten naar TSV in Python
url: /nl/python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tabel uit afbeelding extraheren – Afbeelding naar TSV converteren in Python

Heb je je ooit afgevraagd hoe je een tabel uit een afbeelding kunt halen zonder je haar te trekken? In deze tutorial lopen we stap voor stap door **hoe je tabel**-gegevens uit een afbeelding haalt met de `aocr`-bibliotheek, en die gegevens vervolgens omzet in een nette TSV‑bestand. Geen magie, slechts een paar regels Python en een beetje AI‑aangedreven post‑processing.

Als je ooit hebt geprobeerd een tabel van een gescande factuur of een screenshot te kopiëren‑plakken en eindigde met een warboel, zul je waarderen waarom een OCR‑gedreven aanpak de moeite waard is om te beheersen. Aan het einde kun je elke afbeelding van een tabel in Python laden en schone, door tabs gescheiden waarden krijgen die klaar zijn voor spreadsheets of databases.

---

## Wat je nodig hebt

Voordat we beginnen, zorg dat je het volgende op je machine hebt staan:

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| Python 3.9+ | Het `aocr`‑pakket richt zich op moderne Python‑runtime‑omgevingen. |
| `aocr` library (`pip install aocr`) | Biedt de OCR‑engine en de AI‑post‑processor die we gaan gebruiken. |
| Een afbeeldingsbestand dat een tabel bevat (PNG, JPG, enz.) | De brongegevens die we gaan extraheren. |
| Optioneel: een virtuele omgeving | Houdt afhankelijkheden geïsoleerd — sterk aanbevolen. |

Deze zaken klaar hebben, voorkomt onderbrekingen halverwege de gids.

---

## Installeer de afhankelijkheden

Laten we eerst de OCR‑tools installeren. Open een terminal en voer uit:

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **Pro tip:** Als je permissiefouten krijgt, voeg `--user` toe aan het `pip install`‑commando of gebruik `pipx` voor een globale installatie.

---

## Stap 1 – Initialiseer de OCR‑engine

De engine is het hart van het proces. Beschouw het als het “brein” dat elke pixel bekijkt en beslist welk teken waar hoort.

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

Waarom maken we een engine‑object aan in plaats van een enkele functie aan te roepen? Het engine‑object stelt ons in staat later aangepaste post‑processors toe te voegen, waardoor we fijnmazige controle over de output krijgen — essentieel wanneer je **ocr table image python**‑nauwkeurigheid nodig hebt.

---

## Stap 2 – Voeg de AI‑post‑processor toe

`aocr` wordt geleverd met een lichtgewicht AI‑post‑processor die ruwe OCR‑resultaten opschoont terwijl celranden behouden blijven. Er zijn geen extra argumenten nodig, wat de code overzichtelijk houdt.

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

Als je deze stap overslaat, krijg je nog steeds ruwe tekst, maar de tabelstructuur zal rommelig zijn — denk aan een spreadsheet waarin elke cel een mysterie is. De post‑processor doet het zware werk van het uitlijnen van tekst op het oorspronkelijke raster.

---

## Stap 3 – Laad je tabelafbeelding

Je kunt een afbeelding vanaf elk pad laden, maar voor de duidelijkheid gebruiken we een placeholder‑directory. Vervang `"YOUR_DIRECTORY/invoice_table.png"` door het daadwerkelijke pad naar je bestand.

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

**Opmerking:** `aocr.Image` detecteert automatisch het afbeeldingsformaat en normaliseert kleurkanalen, dus je hoeft het bestand niet voor te bewerken tenzij het ernstig beschadigd is.

---

## Stap 4 – Voer gestructureerde OCR uit

Nu scant de engine de afbeelding en retourneert een ruwe tabel‑object. Dit object bevat rijen, kolommen en de ruwe tekst voor elke cel.

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

Waarom `recognize_structured` gebruiken in plaats van een generieke `recognize`‑aanroep? De gestructureerde variant probeert rij‑/kolomborders af te leiden, waardoor je een matrix‑achtig resultaat krijgt dat later veel makkelijker naar TSV te converteren is.

---

## Stap 5 – Reinig de gegevens met de AI‑post‑processor

Het uitvoeren van de post‑processor verfijnt de ruwe output: het verwijdert vreemde tekens, voegt gesplitste fragmenten samen en zorgt ervoor dat de tekst van elke cel correct uitgelijnd is.

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

Als je `processed_table.table` inspecteert, zie je een lijst van rijen, waarbij elke rij een lijst van `Cell`‑objecten is. Elke `Cell` heeft een `.text`‑attribuut dat de opgeschoonde string bevat.

---

## Stap 6 – Exporteer de tabel als TSV

De laatste stap is om de verwerkte gegevens om te zetten in een tab‑gescheiden waarden (TSV)‑bestand — precies wat je nodig hebt wanneer je een afbeelding naar TSV wilt **converteren** voor Excel of Google Sheets.

```python
import csv

# Define the output TSV path
tsv_path = "extracted_table.tsv"

# Open the file and write rows as tab‑separated values
with open(tsv_path, "w", newline="", encoding="utf-8") as tsv_file:
    writer = csv.writer(tsv_file, delimiter="\t")
    for row in processed_table.table:
        # Extract text from each cell and write the row
        writer.writerow([cell.text for cell in row])

print(f"✅ Table successfully saved to {tsv_path}")
```

Het uitvoeren van het script print elke rij naar de console (indien gewenst) en schrijft een schoon TSV‑bestand dat je in elk spreadsheet‑programma kunt openen.

### Snelle verificatie

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

Je zou netjes uitgelijnde kolommen moeten zien, zoals:

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

Als de output er rommelig uitziet, controleer dan de beeldkwaliteit (scherpte, contrast) en overweeg de instellingen van de OCR‑engine aan te passen — `engine.set_config(...)` laat je taalmodellen en vertrouwensdrempels aanpassen.

---

## Veelvoorkomende randgevallen afhandelen

| Situatie | Aanbevolen oplossing |
|----------|----------------------|
| **Scheef beeld** | Voor‑rotatie met `Pillow` (`Image.rotate`) voordat je het aan `aocr` doorgeeft. |
| **Lage contrast** | Pas histogram‑equalisatie toe (`cv2.equalizeHist`) om de leesbaarheid te verbeteren. |
| **Samengevoegde cellen** | Post‑process het TSV om cellen te splitsen op basis van bekende scheidingstekens of gebruik de `merge_cells=False`‑vlag indien beschikbaar. |
| **Meerdere‑pagina PDF's** | Converteer eerst elke pagina naar een afbeelding (`pdf2image`) en voer de pipeline in een lus uit. |

Deze tweaks houden je **ocr table image python**‑workflow robuust over verschillende bronmaterialen.

---

## Volledig script – Alles‑in‑één‑oplossing

Hieronder staat het volledige, kant‑klaar script dat elke besproken stap bundelt. Sla het op als `extract_table.py` en voer `python extract_table.py` uit.

```python
#!/usr/bin/env python3
"""
Extract Table from Image – Convert Image to TSV (Python)

This script demonstrates how to:
1. Initialise the aocr OCR engine.
2. Attach the AI post‑processor.
3. Load a table image.
4. Perform structured OCR.
5. Clean the results.
6. Export the table as a TSV file.

Author: Your Name
Date: 2026-07-05
"""

import aocr
import csv
import sys
from pathlib import Path

def main(image_path: str, output_tsv: str = "extracted_table.tsv"):
    # Step 1 – Initialise engine
    engine = aocr.OcrEngine()

    # Step 2 – Attach AI post‑processor
    engine.set_post_processor(ai.run_postprocessor, None)

    # Step 3 – Load image
    if not Path(image_path).is_file():
        sys.exit(f"❌ Image not found: {image_path}")
    image = aocr.Image.from_file(image_path)

    # Step 4 – Structured OCR
    raw_table = engine.recognize_structured(image)

    # Step 5 – Clean with post‑processor
    processed_table = engine.run_postprocessor(raw_table)

    # Step 6 – Write TSV
    with open(output_tsv, "w", newline="", encoding="utf-8") as tsv_file:
        writer = csv.writer(tsv_file, delimiter="\


## Wat kun je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Tekst extraheren uit afbeelding met Aspose OCR – Stapsgewijze gids](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Hoe een tabel uit een afbeelding te extraheren met Aspose.OCR voor .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Hoe tekst uit afbeelding te extraheren door rechthoeken voor te bereiden in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}