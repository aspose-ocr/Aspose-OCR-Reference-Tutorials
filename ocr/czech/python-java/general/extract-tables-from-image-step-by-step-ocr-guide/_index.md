---
category: general
date: 2026-03-26
description: Extrahujte tabulky z obrázku a převádějte obrázek na tabulku pomocí Python
  OCR. Naučte se, jak načíst obrázek pro OCR, číst tabulky a extrahovat data tabulky.
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: cs
og_description: Extrahujte tabulky z obrázku pomocí Python OCR. Tento průvodce ukazuje,
  jak načíst obrázek pro OCR, přečíst tabulky a převést je do tabulky.
og_title: Extrahovat tabulky z obrázku – kompletní OCR tutoriál
tags:
- OCR
- Python
- Data Extraction
title: Extrahování tabulek z obrázku – krok za krokem průvodce OCR
url: /cs/python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování tabulek z obrázku – kompletní OCR tutoriál

Už jste někdy potřebovali **extrahovat tabulky z obrázku**, ale nevedeli ste, kde začať? Nie ste sami. Mnoho vývojárov narazí na problém, keď PDF alebo snímka obsahuje tabuľkové údaje, ktoré musia byť premenené na editovateľné riadky a stĺpce. Dobrá správa? Niekoľko riadkov Python kódu v kombinácii so spoľahlivým OCR motorom dokáže premeniť ten obrázok na použiteľný tabuľkový zošit za pár sekúnd.

V tomto tutoriáli prejdeme načítaním obrázku pre OCR, spustením rozpoznávacieho enginu a vyťahovaním každej tabuľky riadok po riadku. Na konci budete schopní **previesť obrázok na tabuľkový zošit** a zároveň uvidíte, ako **ocr čítať tabuľky** a **ocr extrahovať dáta z tabuľky** pre ďalšie spracovanie. Žiadna skrytá mágia, len jasný, spustiteľný kód, ktorý môžete dnes vložiť do svojho projektu.

---

## Čo budete potrebovať

Predtým, než sa pustíme do práce, uistite sa, že máte nasledujúce veci po ruke:

- **Python 3.9+** – najnovšia stabilná verzia funguje najlepšie.  
- Knižnicu **`ocr`** (alebo akúkoľvek kompatibilnú OCR SDK, ktorá poskytuje `OcrEngine`, `Image` a metódy súvisiace s tabuľkami). Nainštalujte ju pomocou `pip install ocr‑sdk` (nahradiť skutočným názvom balíka).  
- Súbor s obrázkom (`.png`, `.jpg`, atď.), ktorý obsahuje jasne vytlačenú tabuľku.  
- Voliteľne: **pandas**, ak chcete rovno zapísať extrahované dáta do CSV alebo Excel súboru (`pip install pandas`).

Máte všetko? Skvelé – poďme na to.

---

## Krok 1: Importujte OCR SDK a pripravte svoje prostredie

Najprv musíme načítať OCR triedy do nášho skriptu a nastaviť malý pomocník, ktorý neskôr premení surové tabuľkové dáta na DataFrame.

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**Prečo je to dôležité:** Importovanie `ocr` nám poskytuje prístup k `OcrEngine`, `Imaging.Image` a objektom tabuliek, cez ktoré budeme iterovať. `pandas` nie je povinný pre samotnú extrakciu, ale uľahčuje časť **previesť obrázok na tabuľkový zošit**.

---

## Krok 2: Načítajte obrázok, ktorý chcete spracovať

Teraz skutočne **načítame obrázok pre OCR**. SDK očakáva objekt `Image`, takže obalíme cestu k súboru pomocou pomocnej metódy `Image.load()`.

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

**Tip:** Ukladajte svoje obrázky do samostatného priečinka (`assets/` alebo `data/`) a používajte relatívne cesty. Tak zostane skript prenosný medzi rôznymi počítačmi.

---

## Krok 3: Spustite proces rozpoznávania

Po pripojení obrázka môžeme konečne povedať enginu, aby **ocr čítal tabuľky**. Volanie `recognize()` vráti objekt výsledku, ktorý obsahuje všetko, čo engine objavil – textové bloky, riadky a najmä tabuľky.

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**Prečo to kontrolujeme:** Niektoré obrázky môžu byť šumové alebo majú slabé okraje tabuliek, čo spôsobí, že engine ich prehliadne. Zaznamenanie varovania vám poskytne skorú spätnú väzbu bez prerušenia skriptu.

---

## Krok 4: Extrahujte riadky a bunky každej tabuľky

Tu sa deje skutočná mágia. Prejdeme každú detegovanú tabuľku, vytiahneme každý riadok a potom text každej bunky. Vnútorný list comprehension robí kód stručným, ale aj tak vysvetlíme tok.

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

**Čo sa deje?**  

- `enumerate(..., start=1)` nám dá priateľské číslo tabuľky pre logovanie.  
- `row_obj.get_cells()` vráti každú bunku; `cell.get_text()` získa OCR‑dekódovaný reťazec.  
- Riadky ukladáme do `rows_data` a potom ich odovzdáme `pandas.DataFrame`, ktorý automaticky zarovná stĺpce.  
- Blok `print` odráža **základný výstup** z pôvodného úryvku, takže môžete okamžite overiť výsledky.

**Riešenie okrajových prípadov:** Ak má riadok iný počet buniek než ostatné, `pandas` doplní chýbajúce miesta hodnotou `NaN`. Neskôr môžete DataFrame vyčistiť pomocou `df.fillna('')`, ak uprednostňujete prázdne reťazce.

---

## Krok 5: Uložte extrahované tabuľky do tabuľkového zošita

Keď už máme zoznam DataFrames, premeniť ich na Excelový zošit (alebo CSV súbory) je hračka. Tým splníme cieľ **previesť obrázok na tabuľkový zošit**.

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**Prečo Excel?** Väčšina obchodných používateľov uprednostňuje `.xlsx`. Ak radšej chcete CSV, nahraďte slučku `df.to_excel(...)` príkazom `df.to_csv(f"table_{idx}.csv", index=False)`.

---

## Kompletný, pripravený na spustenie skript

Zložíme všetko dohromady – tu je kompletný program, ktorý môžete skopírovať a spustiť.

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

**Očakávaný výstup v konzole** (pri jednoduchej 2×3 tabuľke):

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

A v priečinku skriptu nájdete súbor `extracted_tables.xlsx`, každú tabuľku na samostatnom hárku.

---

## Často kladené otázky a tipy

| Otázka | Odpoveď |
|----------|--------|
| **Môžem použiť inú OCR knižnicu?** | Áno. Vzor zostáva rovnaký: načítať obrázok → rozpoznať → iterovať cez `get_tables()`. Stačí vymeniť import a názvy objektov. |
| **Čo ak je môj obrázok šumový?** | Predspracujte ho pomocou OpenCV (thresholding, deskew) pred odovzdaním OCR enginu. Redukcia šumu často zvyšuje presnosť **ocr extrahovať dáta z tabuľky**. |
| **Musím nainštalovať `openpyxl`?** | Áno, `pandas` ho používa pod kapotou pre výstup do Excelu. Nainštalujte pomocou `pip install openpyxl`. |
| **Ako riešiť zlúčené bunky?** | Niektoré SDK poskytujú `cell.is_merged()`; môžete detekovať a manuálne rozšíriť hodnotu cez zlúčený rozsah. |
| **Existuje spôsob, ako extrahovať len konkrétne tabuľky?** | Filtrovať podľa `table_obj.get_confidence()` alebo podľa kontrolných kľúčových slov v hlavičke pred spracovaním. |

---

## Záver

Teraz máte kompletné riešenie od začiatku do konca pre **extrahovanie tabuliek z obrázku**, konverziu výsledku do prehľadného tabuľkového zošita a aj podporu viacerých tabuliek v jednej snímke. Skript ukazuje, ako **načítať obrázok pre OCR**, **ocr čítať tabuľky** a **ocr extrahovať dáta z tabuľky**, pričom zostáva dostatočne flexibilný pre reálne scenáre.

Čo ďalej? Skúste OCR engine použiť na PDF stránku prevedenú na obrázok, alebo experimentujte s rôznymi jazykmi a fontami. Môžete tiež priamo posielať DataFrames do databázy alebo reportovacieho nástroja – vaša predstavivosť je jediným limitom.

Ak sa vám tento návod hodil, pokojne ho zdieľajte, dajte hviezdičku repozitáru, ktorý SDK hostuje, alebo napíšte komentár s vlastnými trikmi. Šťastné kódovanie a nech sú vaše tabuľky vždy dokonale parsované!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}