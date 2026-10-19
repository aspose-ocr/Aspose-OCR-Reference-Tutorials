---
category: general
date: 2026-01-12
description: Extrahujte text z PDF pomocí OCR enginu v Pythonu – naučte se, jak číst
  PDF pomocí OCR, načíst obrázek pro OCR a získat strukturované výsledky.
draft: false
keywords:
- extract text from pdf
- read pdf with ocr
- load image for ocr
- use ocr engine python
language: cs
og_description: Extrahujte text z PDF pomocí OCR enginu v Pythonu. Tento tutoriál
  ukazuje, jak číst PDF pomocí OCR, načíst obrázek pro OCR a použít OCR engine v Pythonu
  pro spolehlivé výsledky.
og_title: Extrahování textu z PDF pomocí OCR enginu v Pythonu – Kompletní průvodce
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Extrahování textu z PDF pomocí OCR enginu v Pythonu – krok za krokem
url: /cs/python/general/extract-text-from-pdf-with-ocr-engine-python-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat text z PDF pomocí OCR Engine Python – Kompletní tutoriál

Už jste někdy potřebovali **extrahovat text z PDF**, ale soubor je jen naskenovaný obrázek? Nejste v tom sami. V mnoha reálných projektech PDF, které obdržíte, neobsahuje žádný vybratelný text, takže jedinou cestou vpřed je **číst PDF s OCR**.  

V tomto průvodci projdeme praktickým, end‑to‑end řešením, které přesně ukazuje, jak **načíst obrázek pro OCR**, spustit **OCR engine Python** a získat strukturovaný text, který můžete předat do následných pipeline. Žádné vágní odkazy, jen kompletní, spustitelný příklad, který můžete dnes zkopírovat a vložit.

## Co se naučíte

- Jak nainstalovat a importovat potřebnou Python OCR knihovnu.  
- Přesné kroky k **načtení obrázku pro OCR** z PDF souboru.  
- Jak zavolat metodu `recognize_structured()` engine a iterovat přes bloky, řádky a slova.  
- Tipy pro práci s výsledky s nízkou důvěrou a PDF s více stránkami.  

Na konci tohoto tutoriálu budete mít skript, který spolehlivě **extrahuje text z PDF** dokumentů, ať už obsahují jednu stránku nebo sto.

---

![Diagram ukazující zpracování PDF OCR engine a výstup strukturovaného textu.](images/ocr_flow.png "diagram extrahování textu z pdf")

*Text obrázku: diagram extrahování textu z pdf ilustrující kroky zpracování OCR.*

## Požadavky

- Python 3.9 nebo novější (kód používá f‑stringy a typové nápovědy).  
- Balíček OCR instalovatelný přes pip, který poskytuje třídu `OcrEngine` (například fiktivní knihovna `pyocr`).  
- PDF soubor, který chcete zpracovat, uložený lokálně (např. `form.pdf`).  

Pokud vám chybí OCR knihovna, nainstalujte ji pomocí:

```bash
pip install pyocr   # replace with the actual package name you use
```

---

## Krok 1: Extrahovat text z PDF – Nastavení OCR engine

Než budeme moci **číst PDF s OCR**, potřebujeme instanci engine. Představte si engine jako mozek, který se dívá na každý pixel a rozhoduje, jaký znak představuje.

```python
# Step 1: Import the OCR module and create an engine instance
import ocr  # or `import pyocr as ocr` depending on the package

# Create the OCR engine – this may load language models under the hood
ocr_engine = ocr.OcrEngine()
```

> **Proč je to důležité:** Inicializace engine jednou vám umožní znovu použít načtené jazykové balíčky napříč více soubory, čímž šetříte čas i paměť.

---

## Krok 2: Načíst obrázek pro OCR – Příprava PDF

PDF není surový obrázek, takže knihovna obvykle poskytuje pomocnou funkci pro převod první stránky (nebo všech stránek) na obrázek, který OCR engine dokáže zpracovat.

```python
# Step 2: Load the PDF page(s) you want to process
# The `load_image` method accepts many formats – PDF, PNG, JPEG, etc.
pdf_path = "YOUR_DIRECTORY/form.pdf"
ocr_engine.load_image(pdf_path)
```

> **Tip:** Pokud má vaše PDF více stránek, mnoho OCR knihoven vám umožní předat `page=2` nebo iterovat přes `engine.load_image(pdf_path, page=n)`. U velkých dokumentů zvažte zpracování stránek po dávkách, aby nedocházelo k výkyvům paměti.

---

## Krok 3: Použít OCR Engine Python – Rozpoznávání strukturovaného textu

Nyní se děje těžká práce. Volání `recognize_structured()` vrací hierarchii bloků → řádků → slov, z nichž každý je anotován jazykem, důvěrou a ohraničujícími boxy.

```python
# Step 3: Perform structured text recognition
structured_result = ocr_engine.recognize_structured()
```

> **Co získáte:**  
> - `structured_result.blocks` – kontejnery nejvyšší úrovně (často odstavce nebo sloupce).  
> - Každý blok obsahuje `lines` a každý řádek obsahuje `words`.  
> - Skóre důvěry vám umožní filtrovat pochybná výsledky.

---

## Krok 4: Iterovat přes výsledky – Přístup k blokům, řádkům a slovům

Níže je kompaktní smyčka, která vypisuje nejvíce užitečné informace. Klidně ji rozšiřte pro zápis do JSON, CSV nebo napájení databáze.

```python
# Step 4: Walk through the hierarchy and display key data
for block_idx, text_block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={text_block.language}, confidence={text_block.confidence:.2f}")

    # Show a sample line from the block, if any
    if text_block.lines:
        sample_line = text_block.lines[0]
        print(f"  Sample line: {sample_line.text}")

        # Show a sample word with its bounding box and confidence
        if sample_line.words:
            sample_word = sample_line.words[0]
            print(
                f"    Sample word: '{sample_word.text}' "
                f"bbox={sample_word.bounding_box} "
                f"conf={sample_word.confidence:.2f}"
            )
```

### Očekávaný výstup

```
Block 1: language=en, confidence=0.97
  Sample line: Invoice Number: 2025-00123
    Sample word: 'Invoice' bbox=(12,34,78,90) conf=0.99
Block 2: language=en, confidence=0.94
  Sample line: Total Amount: $1,250.00
    Sample word: 'Total' bbox=(15,120,70,155) conf=0.96
...
```

> **Proč se vám to bude líbit:** Hierarchie odráží způsob, jakým lidé čtou stránku, což usnadňuje pozdější rekonstrukci tabulek nebo sloupcových rozvržení.

---

## Krok 5: Řešení okrajových případů – Nízká důvěra a PDF s více stránkami

### Slova s nízkou důvěrou

Pokud důvěra slova klesne pod, řekněme, `0.70`, možná jej budete chtít označit k ruční kontrole:

```python
LOW_CONF_THRESHOLD = 0.70

for block in structured_result.blocks:
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

### Zpracování všech stránek

```python
# Example: loop over every page in a multi‑page PDF
for page_number in range(ocr_engine.page_count):
    ocr_engine.load_image(pdf_path, page=page_number)
    result = ocr_engine.recognize_structured()
    # …process `result` just like we did above…
```

> **Pro tip:** Ukládejte mezilehlé obrázky jako PNG, pokud vaše OCR knihovna každou dobu znovu renderuje – může to u velkých dávek ušetřit sekundy.

---

## Kompletní funkční skript

Spojením všeho dohromady, zde je jeden soubor, který můžete okamžitě spustit:

```python
#!/usr/bin/env python3
"""
Extract text from PDF with OCR engine Python.
This script demonstrates loading a PDF, recognizing structured text,
and printing a concise summary of blocks, lines, and words.
"""

import ocr  # Replace with your actual OCR package import

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
PDF_PATH = "YOUR_DIRECTORY/form.pdf"
LOW_CONF_THRESHOLD = 0.70

# ----------------------------------------------------------------------
# Initialize OCR engine
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()

# ----------------------------------------------------------------------
# Load the PDF (first page by default)
# ----------------------------------------------------------------------
ocr_engine.load_image(PDF_PATH)

# ----------------------------------------------------------------------
# Recognize structured text
# ----------------------------------------------------------------------
structured_result = ocr_engine.recognize_structured()

# ----------------------------------------------------------------------
# Iterate and display results
# ----------------------------------------------------------------------
for block_idx, block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={block.language}, confidence={block.confidence:.2f}")

    if block.lines:
        line = block.lines[0]
        print(f"  Sample line: {line.text}")

        if line.words:
            word = line.words[0]
            print(
                f"    Sample word: '{word.text}' "
                f"bbox={word.bounding_box} "
                f"conf={word.confidence:.2f}"
            )

    # Flag low‑confidence words inside the block
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

Save this as `extract_pdf_ocr.py` and run:

```bash
python extract_pdf_ocr.py
```

Měli byste vidět podrobnosti na úrovni bloků vytištěné do konzole, spolu s případnými varováními o nízké důvěře.

---

## Závěr

Právě jsme prošli kompletním, připraveným na produkci způsobem, jak **extrahovat text z PDF** pomocí **OCR engine Python**. Od instalace knihovny, přes **načtení obrázku pro OCR**, až po **čtení PDF s OCR** a nakonec iteraci přes strukturovaný výstup, nyní máte znovupoužitelný skript, který můžete přizpůsobit jakémukoli projektu.

Další kroky, které můžete prozkoumat:

- Export hierarchie do JSON pro následné NLP pipeline.  
- Přidání detekce jazyka pro dynamické přepínání OCR modelů.  
- Integrace s `pdf2image` pro předzpracování PDF, které obsahují složité rozvržení.  

Vyzkoušejte to na dávce faktur s více stránkami, upravte práh důvěry a uvidíte, jak rychle můžete převést naskenované PDF na prohledávatelný, editovatelný text. Pokud narazíte na problémy, zanechte komentář níže – šťastné OCRování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}