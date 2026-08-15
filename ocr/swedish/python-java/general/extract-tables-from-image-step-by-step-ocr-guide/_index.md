---
category: general
date: 2026-03-26
description: Extrahera tabeller från bild och konvertera bilden till ett kalkylblad
  med Python OCR. Lär dig hur du laddar bilden för OCR, läser tabeller och extraherar
  tabelldata.
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: sv
og_description: Extrahera tabeller från bild med Python OCR. Den här guiden visar
  hur du laddar bilden för OCR, läser tabeller och konverterar dem till ett kalkylblad.
og_title: Extrahera tabeller från bild – Komplett OCR-handledning
tags:
- OCR
- Python
- Data Extraction
title: Extrahera tabeller från bild – Steg‑för‑steg OCR‑guide
url: /sv/python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera tabeller från bild – Komplett OCR‑handledning

Har du någonsin behövt **extrahera tabeller från en bild** men inte vetat var du ska börja? Du är inte ensam. Många utvecklare fastnar när en PDF eller skärmdump innehåller tabulär data som måste bli redigerbara rader och kolumner. Den goda nyheten? Några rader Python‑kod, i kombination med en kraftfull OCR‑motor, kan förvandla den bilden till ett användbart kalkylblad på några sekunder.

I den här handledningen går vi igenom hur du laddar en bild för OCR, kör igenkänningsmotorn och drar ut varje tabell rad för rad. När du är klar kan du **konvertera bild till kalkylblad**, och du får också se hur du **ocr read tables** och **ocr extract table data** för vidare bearbetning. Ingen gömd magi, bara tydlig, körbar kod som du kan klistra in i ditt projekt redan idag.

---

## Vad du behöver

Innan vi dyker ner, se till att du har följande tillgängligt:

- **Python 3.9+** – den senaste stabila versionen fungerar bäst.  
- **`ocr`**‑biblioteket (eller något kompatibelt OCR‑SDK som exponerar `OcrEngine`, `Image` och tabell‑relaterade metoder). Installera det med `pip install ocr‑sdk` (byt ut mot det faktiska paketnamnet).  
- En bildfil (`.png`, `.jpg`, osv.) som innehåller en tydligt utskriven tabell.  
- Valfritt: **pandas** om du vill skriva den extraherade datan direkt till en CSV‑ eller Excel‑fil (`pip install pandas`).

Har du allt? Toppen—låt oss börja.

---

## Steg 1: Importera OCR‑SDK och förbered din miljö

Först och främst: vi måste importera OCR‑klasserna till vårt skript och sätta upp en liten hjälpfunktion som senare omvandlar råtabell‑data till en DataFrame.

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**Varför detta är viktigt:** Att importera `ocr` ger oss tillgång till `OcrEngine`, `Imaging.Image` och tabell‑objekten vi ska iterera över. `pandas` krävs inte för själva extraktionen, men det gör delen **konvertera bild till kalkylblad** trivial.

---

## Steg 2: Ladda bilden du vill bearbeta

Nu **laddar vi bilden för OCR**. SDK:n förväntar sig ett `Image`‑objekt, så vi omsluter vår filsökväg med hjälpmetoden `Image.load()`.

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

**Proffstips:** Håll dina bildfiler i en dedikerad mapp (`assets/` eller `data/`) och använd relativa sökvägar. På så sätt blir skriptet portabelt mellan olika maskiner.

---

## Steg 3: Kör igenkänningsprocessen

När bilden är bifogad kan vi äntligen be motorn att **ocr read tables**. Anropet `recognize()` returnerar ett resultatobjekt som innehåller allt motorn upptäckt—textblock, rader och, viktigast för oss, tabeller.

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**Varför vi kontrollerar:** Vissa bilder kan vara brusiga eller ha svaga tabellramar, vilket får motorn att missa dem. Att logga en varning ger dig tidig återkoppling utan att skriptet kraschar.

---

## Steg 4: Extrahera varje tabsells rader och celler

Här sker den riktiga magin. Vi itererar över varje upptäckt tabell, drar ut varje rad och sedan varje cells text. List‑comprehension‑delen gör koden kompakt, men vi förklarar ändå flödet.

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

**Vad händer?**  

- `enumerate(..., start=1)` ger oss ett vänligt tabellnummer för loggning.  
- `row_obj.get_cells()` returnerar varje cell‑objekt; `cell.get_text()` hämtar den OCR‑avkodade strängen.  
- Vi sparar raderna i `rows_data` och skickar dem till `pandas.DataFrame` som automatiskt justerar kolumnerna.  
- `print`‑blocket speglar **essential output** som visas i originalexemplet, så du kan verifiera resultaten direkt.

**Hantering av kantfall:** Om en rad har ett annat antal celler än de andra fyller `pandas` i saknade platser med `NaN`. Du kan senare rensa DataFrame med `df.fillna('')` om du föredrar tomma strängar.

---

## Steg 5: Spara de extraherade tabellerna till ett kalkylblad

Nu när vi har en lista med DataFrames är det en barnlek att göra om dem till en Excel‑arbetsbok (eller CSV‑filer). Detta uppfyller målet **konvertera bild till kalkylblad**.

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**Varför Excel?** De flesta affärsanvändare föredrar `.xlsx`. Om du hellre vill ha CSV, ersätt loopen med `df.to_csv(f"table_{idx}.csv", index=False)`.

---

## Komplett, kör‑klar skript

Sätter vi ihop allt får vi följande program som du kan kopiera‑klistra in och köra.

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

**Förväntad konsolutskrift** (för en enkel 2×3‑tabell):

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

Och du hittar `extracted_tables.xlsx` i skriptets mapp, varje tabell på ett eget blad.

---

## Vanliga frågor & tips

| Fråga | Svar |
|----------|--------|
| **Kan jag använda ett annat OCR‑bibliotek?** | Absolut. Mönstret är detsamma: ladda bild → igenkänn → iterera över `get_tables()`. Byt bara ut importen och objektnamnen. |
| **Vad händer om min bild är brusig?** | Förbehandla med OpenCV (tröskling, deskew) innan du skickar den till OCR‑motorn. Brusreducering förbättrar ofta **ocr extract table data**‑noggrannheten. |
| **Behöver jag installera `openpyxl`?** | Ja, `pandas` använder det under huven för Excel‑utmatning. Installera med `pip install openpyxl`. |
| **Hur hanterar jag sammanslagna celler?** | Vissa SDK:er exponerar `cell.is_merged()`; du kan då upptäcka och sprida värdet över det sammanslagna området manuellt. |
| **Finns det ett sätt att extrahera bara specifika tabeller?** | Filtrera med `table_obj.get_confidence()` eller genom att kontrollera rubrik‑nyckelord innan du bearbetar. |

---

## Avslutning

Du har nu en komplett, end‑to‑end‑lösning för **extrahera tabeller från bild**, konvertera resultatet till ett prydligt kalkylblad och även hantera flera tabeller i en enda bild. Skriptet visar hur du **load image for OCR**, **ocr read tables** och **ocr extract table data** samtidigt som det är flexibelt nog för verkliga variationer.

Vad blir nästa steg? Prova att låta OCR‑motorn bearbeta en PDF‑sida renderad som bild, eller experimentera med olika språk och typsnitt. Du kan också skicka DataFrames direkt till en databas eller ett rapportverktyg—din fantasi sätter gränsen.

Om du tyckte att den här guiden var hjälpsam, dela gärna den, ge ett stjärnmärke till repot som hostar SDK:n, eller lämna en kommentar med dina egna knep. Lycka till med kodandet, och må dina tabeller alltid bli perfekt parsade!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}