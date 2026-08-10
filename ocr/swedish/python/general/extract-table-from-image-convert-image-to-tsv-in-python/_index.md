---
category: general
date: 2026-07-05
description: Extrahera tabell från bild med Python OCR. Lär dig hur du extraherar
  tabell, konverterar bild till TSV och behärskar OCR‑tabell‑bild‑Python‑tekniker.
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: sv
og_description: Extrahera tabell från bild med Python OCR. Den här guiden visar hur
  du extraherar en tabell, konverterar bilden till TSV och använder OCR‑tabell‑bild‑Python‑verktyg.
og_title: Extrahera tabell från bild – Konvertera bild till TSV i Python
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
title: Extrahera tabell från bild – Konvertera bild till TSV i Python
url: /sv/python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera tabell från bild – Konvertera bild till TSV i Python

Har du någonsin undrat hur man extraherar en tabell från en bild utan att rycka upp håret? I den här handledningen går vi igenom **hur man extraherar tabell**-data från en bild med hjälp av `aocr`-biblioteket, och sedan omvandlar vi den datan till en prydlig TSV-fil. Ingen magi, bara några rader Python och lite AI‑driven efterbehandling.

Om du någonsin har försökt kopiera‑klistra in en tabell från en skannad faktura eller en skärmdump och slutade med en rörig röra, kommer du att uppskatta varför ett OCR‑drivet tillvägagångssätt är värt att behärska. I slutet kommer du att kunna mata in vilken bild av en tabell som helst i Python och få rena, tab‑separerade värden redo för kalkylblad eller databaser.

---

## Vad du behöver

Innan vi dyker ner, se till att du har följande på din maskin:

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.9+ | `aocr`‑paketet riktar sig mot moderna Python‑miljöer. |
| `aocr`-bibliotek (`pip install aocr`) | Tillhandahåller OCR‑motorn och AI‑efterbehandlingen vi kommer att använda. |
| En bildfil som innehåller en tabell (PNG, JPG, etc.) | Källdata som vi ska extrahera. |
| Valfritt: en virtuell miljö | Håller beroenden isolerade — starkt rekommenderat. |

Att ha dessa redo sparar dig från avbrott halvvägs genom guiden.

---

## Installera beroenden

Först, låt oss installera OCR‑verktygen. Öppna en terminal och kör:

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **Proffstips:** Om du får behörighetsfel, lägg till `--user` till `pip install`‑kommandot eller använd `pipx` för en global installation.

---

## Steg 1 – Initiera OCR‑motorn

Motorn är hjärtat i processen. Tänk på den som “hjärnan” som tittar på varje pixel och bestämmer vilken tecken som hör var.

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

Varför instansierar vi en motor istället för att anropa en enda funktion? Motor‑objektet låter oss fästa anpassade efterbehandlare senare, vilket ger oss fin‑granulär kontroll över resultatet — nödvändigt när du behöver **ocr table image python**‑noggrannhet.

---

## Steg 2 – Fäst AI‑efterbehandlare

`aocr` levereras med en lättviktig AI‑efterbehandlare som rensar råa OCR‑resultat samtidigt som den bevarar cellgränser. Inga extra argument krävs, vilket håller koden prydlig.

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

Om du hoppar över detta steg får du fortfarande råtext, men tabellstrukturen blir brusig — tänk på ett kalkylblad där varje cell är ett mysterium. Efterbehandlare gör det tunga arbetet med att justera texten till dess ursprungliga rutnät.

---

## Steg 3 – Ladda din tabellbild

Du kan ladda en bild från vilken sökväg som helst, men för tydlighetens skull refererar vi till en platshållarkatalog. Ersätt `"YOUR_DIRECTORY/invoice_table.png"` med den faktiska sökvägen till din fil.

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

> **Obs:** `aocr.Image` upptäcker automatiskt bildformatet och normaliserar färgkanaler, så du behöver inte förbehandla filen såvida den inte är kraftigt fördärvad.

---

## Steg 4 – Utför strukturerad OCR

Nu skannar motorn bilden och returnerar ett rått tabellobjekt. Detta objekt innehåller rader, kolumner och den råa texten för varje cell.

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

Varför använda `recognize_structured` istället för ett generiskt `recognize`‑anrop? Den strukturerade varianten försöker härleda rad‑/kolumngränser, vilket ger dig ett matris‑likt resultat som är mycket enklare att konvertera till TSV senare.

---

## Steg 5 – Rensa data med AI‑efterbehandlare

Att köra efterbehandlare förfinar den råa utskriften: den tar bort lösa tecken, slår ihop delade fragment och säkerställer att varje cells text är korrekt justerad.

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

Om du inspekterar `processed_table.table` kommer du att se en lista av rader, där varje rad är en lista av `Cell`‑objekt. Varje `Cell` har ett `.text`‑attribut som innehåller den rensade strängen.

---

## Steg 6 – Exportera tabellen som TSV

Det sista steget är att omvandla den bearbetade datan till en tab‑separerad värdefil (TSV) — precis vad du behöver när du vill **convert image to TSV** för Excel eller Google Sheets.

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

Att köra skriptet skriver ut varje rad till konsolen (om du föredrar) och skapar en ren TSV‑fil som du kan öppna i vilket kalkylprogram som helst.

### Snabb verifiering

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

Du bör se prydligt justerade kolumner, som:

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

Om utskriften ser rörig ut, dubbelkolla bildkvaliteten (skärpa, kontrast) och överväg att justera OCR‑motorns inställningar — `engine.set_config(...)` låter dig justera språkmodeller och förtroendetrösklar.

---

## Hantera vanliga kantfall

| Situation | Suggested Fix |
|-----------|---------------|
| **Sned bild** | Förrotera med `Pillow` (`Image.rotate`) innan du matar in den till `aocr`. |
| **Låg kontrast** | Applicera histogramutjämning (`cv2.equalizeHist`) för att förbättra läsbarheten. |
| **Sammanfogade celler** | Efterbehandla TSV‑filen för att dela celler baserat på kända avgränsare eller använd flaggan `merge_cells=False` om den finns. |
| **Fler‑sidiga PDF‑filer** | Konvertera varje sida till en bild först (`pdf2image`) och kör pipeline i en loop. |

Dessa justeringar håller ditt **ocr table image python**‑arbetsflöde robust över varierat källmaterial.

---

## Fullt skript – All‑i‑ett‑lösning

Nedan är det kompletta, färdiga skriptet som samlar alla steg som diskuterats. Spara det som `extract_table.py` och kör `python extract_table.py`.

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


## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Extrahera text från bild med Aspose OCR – Steg‑för‑steg‑guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Hur man extraherar tabell från bild med Aspose.OCR för .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Hur man extraherar text från bild genom att förbereda rektanglar i OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}