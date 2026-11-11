---
category: general
date: 2026-07-05
description: Extrahujte tabulku z obrázku pomocí Python OCR. Naučte se, jak extrahovat
  tabulku, převést obrázek na TSV a ovládnout techniky OCR tabulky v Pythonu.
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: cs
og_description: Extrahujte tabulku z obrázku pomocí Python OCR. Tento návod ukazuje,
  jak extrahovat tabulku, převést obrázek na TSV a použít nástroje pro OCR tabulky
  v Pythonu.
og_title: Extrahovat tabulku z obrázku – převést obrázek na TSV v Pythonu
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
title: Extrahovat tabulku z obrázku – převést obrázek na TSV v Pythonu
url: /cs/python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat tabulku z obrázku – Převést obrázek na TSV v Pythonu

Už jste se někdy ptali, jak extrahovat tabulku z obrázku, aniž byste si trhali vlasy? V tomto tutoriálu vás provedeme **jak extrahovat tabulku** z obrázku pomocí knihovny `aocr` a poté tato data převést do přehledného TSV souboru. Žádná magie, jen několik řádků Pythonu a trochu AI‑poháněného post‑processingu.

Pokud jste někdy zkoušeli zkopírovat‑vložit tabulku ze skenované faktury nebo screenshotu a skončili s nepořádkem, oceníte, proč je OCR‑poháněný přístup stojí za to zvládnout. Na konci budete schopni předat libovolný obrázek tabulky do Pythonu a získat čisté hodnoty oddělené tabulátory připravené pro tabulky nebo databáze.

---

## Co budete potřebovat

| Požadavek | Proč je důležitý |
|-------------|----------------|
| Python 3.9+ | Balíček `aocr` cílí na moderní runtime Pythonu. |
| `aocr` library (`pip install aocr`) | Poskytuje OCR engine a AI post‑processor, který použijeme. |
| An image file containing a table (PNG, JPG, etc.) | Zdrojová data, která budeme extrahovat. |
| Optional: a virtual environment | Udržuje závislosti izolované – vysoce doporučeno. |

Mít tyto věci připravené vám ušetří přerušení uprostřed průvodce.

---

## Nainstalujte závislosti

Nejprve si nainstalujeme OCR nástroje. Otevřete terminál a spusťte:

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **Pro tip:** Pokud narazíte na chyby oprávnění, přidejte `--user` k příkazu `pip install` nebo použijte `pipx` pro globální instalaci.

---

## Krok 1 – Inicializace OCR engine

Engine je srdcem procesu. Představte si ho jako „mozek“, který se dívá na každý pixel a rozhoduje, který znak kam patří.

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

Proč vytváříme instanci engine místo volání jediné funkce? Objekt engine nám umožňuje později připojit vlastní post‑processory, což nám dává jemnou kontrolu nad výstupem – nezbytné, když potřebujete **ocr table image python** přesnost.

---

## Krok 2 – Připojení AI post‑processoru

`aocr` přichází s lehkým AI post‑processorem, který čistí surové OCR výsledky a zachovává okraje buněk. Nepotřebuje žádné další argumenty, což udržuje kód přehledný.

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

Pokud tento krok přeskočíte, stále získáte surový text, ale struktura tabulky bude šumivá – představte si tabulku, kde je každá buňka záhadou. Post‑processor provádí těžkou práci s zarovnáním textu do původní mřížky.

---

## Krok 3 – Načtení obrázku tabulky

Obrázek můžete načíst z libovolné cesty, ale pro přehlednost použijeme zástupný adresář. Nahraďte `"YOUR_DIRECTORY/invoice_table.png"` skutečnou cestou k vašemu souboru.

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

> **Poznámka:** `aocr.Image` automaticky detekuje formát obrázku a normalizuje barevné kanály, takže není potřeba předzpracovávat soubor, pokud není výrazně poškozený.

---

## Krok 4 – Provedení strukturovaného OCR

Engine nyní skenuje obrázek a vrací surový objekt tabulky. Tento objekt obsahuje řádky, sloupce a surový text pro každou buňku.

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

Proč použít `recognize_structured` místo obecného volání `recognize`? Strukturovaná varianta se snaží odhadnout hranice řádků/sloupců, což vám dává maticově podobný výsledek, který je mnohem snazší převést na TSV později.

---

## Krok 5 – Vyčištění dat pomocí AI post‑processoru

Spuštění post‑processoru vylepšuje surový výstup: odstraňuje cizí znaky, spojuje rozdělené fragmenty a zajišťuje, že text v každé buňce je správně zarovnán.

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

Pokud se podíváte na `processed_table.table`, uvidíte seznam řádků, kde každý řádek je seznam objektů `Cell`. Každý `Cell` má atribut `.text`, který obsahuje vyčištěný řetězec.

---

## Krok 6 – Export tabulky jako TSV

Poslední krok je převést zpracovaná data do souboru s hodnotami oddělenými tabulátory (TSV) – právě to, co potřebujete, když chcete **convert image to TSV** pro Excel nebo Google Sheets.

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

Spuštění skriptu vypíše každý řádek do konzole (pokud chcete) a zapíše čistý TSV soubor, který můžete otevřít v libovolném tabulkovém programu.

### Rychlé ověření

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

Měli byste vidět pěkně zarovnané sloupce, například:

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

Pokud výstup vypadá rozmazaně, zkontrolujte kvalitu obrázku (ostrost, kontrast) a zvažte úpravu nastavení OCR engine – `engine.set_config(...)` vám umožní nastavit jazykové modely a prahy důvěry.

---

## Řešení běžných okrajových případů

| Situace | Navrhované řešení |
|-----------|-------------------|
| **Skewed image** | Předrotovat pomocí `Pillow` (`Image.rotate`) před předáním do `aocr`. |
| **Low contrast** | Použít ekvalizaci histogramu (`cv2.equalizeHist`) pro zvýšení čitelnosti. |
| **Merged cells** | Post‑process TSV k rozdělení buněk na základě známých oddělovačů nebo použít flag `merge_cells=False`, pokud je k dispozici. |
| **Multi‑page PDFs** | Nejprve převést každou stránku na obrázek (`pdf2image`) a spustit pipeline ve smyčce. |

Tyto úpravy udrží váš **ocr table image python** workflow robustní napříč různorodým zdrojovým materiálem.

---

## Kompletní skript – Jedno‑stop řešení

Níže je kompletní, připravený ke spuštění skript, který spojuje všechny diskutované kroky. Uložte jej jako `extract_table.py` a spusťte `python extract_table.py`.

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


## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich vlastních projektech.

- [Extrahovat text z obrázku pomocí Aspose OCR – Průvodce krok za krokem](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Jak extrahovat tabulku z obrázku pomocí Aspose.OCR pro .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Jak extrahovat text z obrázku přípravou obdélníků v OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}