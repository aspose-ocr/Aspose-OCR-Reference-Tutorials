---
category: general
date: 2026-03-26
description: Jak extrahovat text z PDF pomocí OCR. Naučte se načíst PDF jako obrázek,
  rozpoznat text v PDF a extrahovat text z PDF pomocí jednoduchého příkladu v Pythonu.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize pdf text
- load pdf as image
- how to use OCR
language: cs
og_description: Jak extrahovat text z PDF pomocí OCR. Tento návod vám ukáže, jak načíst
  PDF jako obrázek, rozpoznat text v PDF a extrahovat text z PDF v Pythonu.
og_title: Jak extrahovat text z PDF pomocí OCR – kompletní návod
tags:
- OCR
- Python
- PDF processing
title: Jak extrahovat text z PDF pomocí OCR – Kompletní krok za krokem průvodce
url: /cs/python-java/general/how-to-extract-pdf-text-with-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak extrahovat text z PDF pomocí OCR – Kompletní krok‑za‑krokem průvodce

Už jste se někdy zamýšleli **jak extrahovat PDF** soubory, které jsou ve skutečnosti jen naskenované obrázky? Nejste sami – mnoho vývojářů narazí na tuto překážku, když potřebují prohledávat obsah, ale mají jen PDF obsahující obrázky. Dobrá zpráva? Několik řádků kódu a solidní OCR knihovna dokážou proměnit tyto obrázkové PDF na čistý text během chvilky.  

V tomto tutoriálu si projdeme **jak použít OCR** k načtení PDF jako obrázku, rozpoznání textu v PDF a nakonec **extrahování textu z PDF** dokumentů libovolné délky. Na konci budete mít spustitelný skript, jasné vysvětlení každého kroku a několik tipů, jak se vyhnout běžným úskalím.

## Co budete potřebovat

- Python 3.9 nebo novější (kód funguje i na 3.10+)  
- Python balíček `ocr` (nebo jakákoli kompatibilní OCR knihovna, která poskytuje `OcrEngine`, `OcrEngineMode` a `Imaging.Image`)  
- Vícestránkový PDF, který chcete zpracovat (pro ukázku ho budeme nazývat `multi_page.pdf`)  
- Základní znalost virtuálních prostředí (volitelné, ale doporučené)

> **Pro tip:** Pokud používáte Windows, zvažte Anaconda Prompt; na macOS/Linux stačí jednoduchý `python -m venv venv && source venv/bin/activate`.

## Krok 1: Instalace OCR knihovny

Nejprve si stáhněte OCR balíček z PyPI. Níže uvedený příklad používá fiktivní balíček `ocr`, který odráží API ukázané ve výňatku kódu, ale většina reálných knihoven (např. `pytesseract` + `pdf2image`) funguje podle stejného vzoru.

```bash
pip install ocr
```

Pokud používáte jiný engine, nahraďte `ocr` odpovídajícím názvem (např. `pip install pytesseract pdf2image`).

## Krok 2: Inicializace OCR enginu

Vytvoření instance enginu je základem **jak extrahovat PDF** text. Představte si engine jako mozek, který bude interpretovat pixely na každé stránce PDF.

```python
import ocr

# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Set the engine to the default mode (fast enough for most PDFs)
ocr_engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)
```

> **Proč je to důležité:** `set_engine_mode` vám umožní vyměnit rychlost za přesnost. `DEFAULT` je vyvážená volba; pokud potřebujete vyšší přesnost, přepněte na `HIGH_ACCURACY` (pokud knihovna tuto možnost podporuje).

## Krok 3: Načtení PDF jako objektu obrázku

OCR pracuje s obrázky, ne s PDF kontejnery, takže nejprve musíme PDF převést na obrazovou reprezentaci. Metoda `Imaging.Image.load` automaticky zpracuje vícestránkové PDF.

```python
# Step 3: Load the multi‑page PDF as an image object
pdf_path = "YOUR_DIRECTORY/multi_page.pdf"
pdf_image = ocr.Imaging.Image.load(pdf_path)
```

> **Hraniční případ:** Některé knihovny akceptují jen jednostránkový obrázek. V takovém případě byste procházeli každou stránku pomocí `pdf2image.convert_from_path`. Naše volání `load` to abstrahuje, takže **load pdf as image** je jednorázový příkaz.

## Krok 4: Rozpoznání textu na všech stránkách

Nyní přichází jádro **recognize PDF text**. Engine prohledá každou stránku a vrátí seznam objektů výsledků – jeden pro každou stránku.

```python
# Step 4: Recognize text on all pages of the PDF
page_results = ocr_engine.recognize_multi_page(pdf_image)
```

Každý `page_result` obsahuje metody jako `get_text()` (čistý text) a `get_confidence()` (volitelná metrika kvality).  

> **Tip:** Pokud potřebujete jen první stránku, zavolejte `recognize(pdf_image[0])` místo pomocníka pro vícestránkové PDF.

## Krok 5: Procházení výsledků a výstup extrahovaného textu

Nakonec projdeme výsledky a vytiskneme text každé stránky. Tím dokončujeme workflow **extract text from PDF**.

```python
# Step 5: Print extracted text page by page
for index, page_result in enumerate(page_results):
    print(f"--- Page {index + 1} ---")
    print(page_result.get_text())
    # Optional: show confidence score
    # print(f"Confidence: {page_result.get_confidence():.2f}%")
```

### Očekávaný výstup

Pokud `multi_page.pdf` obsahuje tři stránky se slovy „Hello“, „World“ a „Python“, uvidíte:

```
--- Page 1 ---
Hello
--- Page 2 ---
World
--- Page 3 ---
Python
```

A to je vše – váš PDF je nyní plně prohledávatelný a text je připravený pro další zpracování (indexování, sentiment analýzu, cokoliv).

## Krok 6: Řešení běžných úskalí

| Problém | Proč se vyskytuje | Rychlé řešení |
|---------|-------------------|---------------|
| **Prázdný výstup** | Stránky PDF jsou naskenovány s nízkým DPI, znaky jsou nečitelné. | Zvětšete obrázek před OCR: `pdf_image = pdf_image.resize(300)` (300 DPI je dobrý kompromis). |
| **Špatné znaky** | Ne‑latinské abecedy vyžadují jazykové balíčky. | Načtěte odpovídající jazykový model: `ocr_engine.load_language('spa')` pro španělštinu apod. |
| **Vyčerpání paměti u velkých PDF** | Načítání všech stránek najednou spotřebuje RAM. | Zpracovávejte stránky po částech: `for img in pdf_image.split(batch=10): …` (pseudo‑kód). |
| **Pomalý výkon** | Použití `DEFAULT` u masivního dokumentu může být pomalé. | Přepněte na `FAST` režim nebo spusťte OCR paralelně pomocí `concurrent.futures`. |

## Bonus: Uložení extrahovaného textu do souboru

Většina reálných pipeline potřebuje text uložit. Zde je malý pomocník, který vše zapíše do `output.txt`.

```python
output_path = "YOUR_DIRECTORY/output.txt"

with open(output_path, "w", encoding="utf-8") as f:
    for idx, result in enumerate(page_results):
        f.write(f"--- Page {idx + 1} ---\n")
        f.write(result.get_text() + "\n\n")
print(f"All text saved to {output_path}")
```

Nyní můžete `output.txt` předat vyhledávači, databázi nebo jakémukoli NLP modelu.

## Sestavení všeho dohromady – kompletní skript

Níže je kompletní, připravený ke spuštění program. Zkopírujte, upravte cesty k souborům a můžete jít.

```python
# -*- coding: utf-8 -*-
"""
How to extract PDF text with OCR – end‑to‑end example.

Prerequisites:
    pip install ocr
"""

import ocr

def extract_text_from_pdf(pdf_path: str):
    """
    Load a PDF, run OCR on every page, and return a list of strings.
    """
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)

    # Load PDF as image (multi‑page support)
    pdf_image = ocr.Imaging.Image.load(pdf_path)

    # Recognize text on all pages
    results = engine.recognize_multi_page(pdf_image)

    # Collect plain text
    texts = [res.get_text() for res in results]
    return texts

def main():
    pdf_file = "YOUR_DIRECTORY/multi_page.pdf"
    texts = extract_text_from_pdf(pdf_file)

    # Print and optionally save
    for i, txt in enumerate(texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()

    # Save to file
    out_path = "YOUR_DIRECTORY/extracted_text.txt"
    with open(out_path, "w", encoding="utf-8") as out_f:
        for i, txt in enumerate(texts, start=1):
            out_f.write(f"--- Page {i} ---\n{txt}\n\n")
    print(f"Extracted text stored in {out_path}")

if __name__ == "__main__":
    main()
```

Spusťte:

```bash
python extract_pdf_ocr.py
```

Měli byste vidět obsah každé stránky vytištěný do konzole a potvrzení, že soubor `extracted_text.txt` byl vytvořen.

## Závěr

Probrali jsme **jak extrahovat PDF** text z dokumentů obsahujících jen obrázky pomocí OCR enginu, od instalace knihovny po zpracování vícestránkových výsledků a uložení výstupu. Nyní umíte **jak použít OCR**, **jak načíst PDF jako obrázek** a **jak spolehlivě rozpoznat text v PDF**.  

Další kroky? Vyzkoušejte přepnutí výchozího režimu enginu na nastavení vysoké přesnosti, experimentujte s jazykovými balíčky pro vícejazyčné PDF nebo připojte extrahovaný text do full‑textového vyhledávače jako Elasticsearch. Možnosti jsou neomezené, jakmile ovládnete základy extrahování textu z PDF souborů.

---

![how to extract pdf example](images/ocr_flowchart.png){alt="diagram pracovního postupu jak extrahovat PDF"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}