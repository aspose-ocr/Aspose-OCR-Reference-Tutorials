---
category: general
date: 2026-03-26
description: Tabellen uit een afbeelding extraheren en de afbeelding omzetten naar
  een spreadsheet met Python OCR. Leer hoe je een afbeelding laadt voor OCR, tabellen
  leest en tabelgegevens extraheert.
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: nl
og_description: Tabellen extraheren uit afbeelding met Python OCR. Deze gids laat
  zien hoe je een afbeelding laadt voor OCR, tabellen leest en ze converteert naar
  een spreadsheet.
og_title: Tabellen uit afbeelding extraheren – Complete OCR-handleiding
tags:
- OCR
- Python
- Data Extraction
title: Tabellen uit afbeelding extraheren – Stapsgewijze OCR-gids
url: /nl/python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tabellen uit afbeelding extraheren – Complete OCR Tutorial

Heb je ooit **tabellen uit afbeelding moeten extraheren** maar wist je niet waar te beginnen? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer een PDF of screenshot tabulaire gegevens bevat die omgezet moeten worden naar bewerkbare rijen en kolommen. Het goede nieuws? Een paar regels Python‑code, gecombineerd met een robuuste OCR‑engine, kunnen die afbeelding in enkele seconden omzetten naar een bruikbare spreadsheet.

In deze tutorial lopen we stap voor stap door het laden van een afbeelding voor OCR, het uitvoeren van de herkenningsengine en het extraheren van elke tabel rij voor rij. Aan het einde kun je **convert image to spreadsheet** omzetten, en zie je ook hoe je **ocr read tables** en **ocr extract table data** kunt gebruiken voor verdere verwerking. Geen verborgen magie, alleen duidelijke, uitvoerbare code die je vandaag nog in je project kunt gebruiken.

---

## Wat je nodig hebt

- **Python 3.9+** – de nieuwste stabiele release werkt het beste.
- De **`ocr`** bibliotheek (of een compatibele OCR‑SDK die `OcrEngine`, `Image` en tabel‑gerelateerde methoden exposeert). Installeer deze met `pip install ocr‑sdk` (vervang door de daadwerkelijke pakketnaam).
- Een afbeeldingsbestand (`.png`, `.jpg`, etc.) dat een duidelijk afgedrukte tabel bevat.  
- Optioneel: **pandas** als je de geëxtraheerde gegevens direct naar een CSV‑ of Excel‑bestand wilt schrijven (`pip install pandas`).

Heb je alles? Geweldig—laten we beginnen.

---

## Stap 1: Importeer de OCR‑SDK en bereid je omgeving voor

Allereerst moeten we de OCR‑klassen in ons script importeren en een kleine helper opzetten die later de ruwe tabelgegevens omzet naar een DataFrame.

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**Waarom dit belangrijk is:** Het importeren van `ocr` geeft ons toegang tot `OcrEngine`, `Imaging.Image` en de tabelobjecten waar we over zullen itereren. `pandas` is niet vereist voor extractie, maar maakt het deel **convert image to spreadsheet** triviaal.

---

## Stap 2: Laad de afbeelding die je wilt verwerken

Nu **laden we de afbeelding voor OCR**. De SDK verwacht een `Image`‑object, dus we wikkelen ons bestandspad in de hulpmethode `Image.load()`.

```python
# Step 2 – Load the image that contains a table
image_path = Path("YOUR_DIRECTORY/table_image.png")

# Verify the file exists early to avoid cryptic SDK errors
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Attach the image to the engine
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))
```

**Pro tip:** Bewaar je afbeeldingsbestanden in een speciale map (`assets/` of `data/`) en gebruik relatieve paden. Zo blijft het script draagbaar tussen verschillende machines.

---

## Stap 3: Voer het herkenningsproces uit

Met de afbeelding gekoppeld, kunnen we de engine eindelijk laten **ocr read tables**. De `recognize()`‑aanroep retourneert een result object dat alles bevat wat de engine heeft ontdekt—tekstblokken, lijnen en, het belangrijkste voor ons, tabellen.

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**Waarom we controleren:** Sommige afbeeldingen kunnen ruisig zijn of de tabelranden zijn vaag, waardoor de engine ze mist. Het loggen van een waarschuwing geeft je vroegtijdige feedback zonder het script te laten falen.

---

## Stap 4: Extraheer de rijen en cellen van elke tabel

Hier gebeurt de echte magie. We itereren over elke gedetecteerde tabel, halen elke rij op, en vervolgens de tekst van elke cel. De interne list comprehension maakt de code beknopt, maar we leggen de stroom toch uit.

```python
# Step 4 – Iterate over detected tables and collect data
all_tables = []   # Will hold a list of pandas DataFrames

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")

    rows_data = []   # Temporary storage for this table's rows

    for row_obj in table_obj.get_rows():
        # Extract text from each cell in the current row
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    # Convert the raw list of rows into a DataFrame
    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    # Print a human‑readable version to the console
    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))
```

**Wat gebeurt er?**  

- `enumerate(..., start=1)` geeft ons een vriendelijke tabelnummer voor logging.  
- `row_obj.get_cells()` retourneert elk cel‑object; `cell.get_text()` haalt de OCR‑gedecodeerde string op.  
- We slaan rijen op in `rows_data`, en geven ze vervolgens door aan `pandas.DataFrame` die automatisch de kolommen uitlijnt.  
- Het `print`‑blok spiegelt de **essential output** die in het originele fragment wordt getoond, zodat je de resultaten direct kunt verifiëren.

**Afhandeling van randgevallen:** Als een rij een ander aantal cellen heeft dan de andere, vult `pandas` de ontbrekende plekken met `NaN`. Je kunt later de DataFrame opschonen met `df.fillna('')` als je lege strings verkiest.

---

## Stap 5: Sla de geëxtraheerde tabellen op in een spreadsheet

Nu we een lijst met DataFrames hebben, is het omzetten naar een Excel‑werkboek (of CSV‑bestanden) een fluitje van een cent. Dit vervult het doel “convert image to spreadsheet”.

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**Waarom Excel?** De meeste zakelijke gebruikers geven de voorkeur aan `.xlsx`. Als je CSV verkiest, vervang je de lus door `df.to_csv(f"table_{idx}.csv", index=False)`.

---

## Volledig, kant‑klaar script

Alles bij elkaar genomen, hier is het volledige programma dat je kunt kopiëren‑plakken en uitvoeren.

```python
import ocr
from pathlib import Path
import pandas as pd
import logging

logging.basicConfig(level=logging.INFO)

# ---------- Configuration ----------
image_path = Path("YOUR_DIRECTORY/table_image.png")
output_path = Path("extracted_tables.xlsx")
# ----------------------------------

# Verify image exists
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Initialize OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))

# Run recognition
ocr_result = ocr_engine.recognize()

if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
    exit(0)

all_tables = []

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")
    rows_data = []

    for row_obj in table_obj.get_rows():
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))

# Save to Excel
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        df.to_excel(writer, sheet_name=f"Table_{idx}", index=False)

logging.info(f"All tables saved to {output_path}")
```

**Verwachte console‑output** (ervan uitgaande dat er een eenvoudige 2×3 tabel is):

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

En je vindt `extracted_tables.xlsx` in de map van het script, elke tabel op een eigen blad.

---

## Veelgestelde vragen & tips

| Vraag | Antwoord |
|----------|--------|
| **Kan ik een andere OCR‑bibliotheek gebruiken?** | Absoluut. Het patroon blijft hetzelfde: afbeelding laden → herkennen → itereren over `get_tables()`. Vervang alleen de import‑ en objectnamen. |
| **Wat als mijn afbeelding ruisig is?** | Pre‑process met OpenCV (thresholding, deskew) voordat je het aan de OCR‑engine geeft. Ruisreductie verbetert vaak de nauwkeurigheid van **ocr extract table data**. |
| **Moet ik `openpyxl` installeren?** | Ja, `pandas` gebruikt het onder de motorkap voor Excel‑output. Installeer met `pip install openpyxl`. |
| **Hoe ga ik om met samengevoegde cellen?** | Sommige SDK's bieden `cell.is_merged()`; je kunt de waarde handmatig over het samengevoegde bereik verspreiden. |
| **Is er een manier om alleen specifieke tabellen te extraheren?** | Filter op `table_obj.get_confidence()` of controleer op header‑trefwoorden voordat je verwerkt. |

---

## Afronding

Je hebt nu een complete, end‑to‑end oplossing voor **extract tables from image**, die het resultaat omzet naar een nette spreadsheet, en zelfs meerdere tabellen in één afbeelding kan verwerken. Het script toont hoe je **load image for OCR**, **ocr read tables**, en **ocr extract table data** uitvoert, terwijl het flexibel genoeg blijft voor real‑world variaties.

Wat nu? Probeer de OCR‑engine een PDF‑pagina te geven die als afbeelding is gerenderd, of experimenteer met verschillende talen en lettertypen. Je kunt de DataFrames ook direct naar een database of rapportagetool sturen—je verbeelding is de enige limiet.

Als je deze gids nuttig vond, deel hem gerust, geef een ster aan de repository die de SDK host, of laat een commentaar achter met je eigen tips. Veel plezier met coderen, en moge je tabellen altijd perfect worden geparseerd!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}