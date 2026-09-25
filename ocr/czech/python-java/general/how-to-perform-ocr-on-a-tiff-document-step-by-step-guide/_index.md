---
category: general
date: 2026-01-12
description: Jak provádět OCR rychle a přesně. Naučte se spustit OCR na dokumentu,
  extrahovat text z TIFF, načíst obrázek pro OCR a nastavit jazyk OCR v Pythonu.
draft: false
keywords:
- how to perform ocr
- run ocr on document
- extract text from tiff
- load image for ocr
- set OCR language
language: cs
og_description: Jak provádět OCR v Pythonu. Tento tutoriál vám ukáže, jak spustit
  OCR na dokumentu, extrahovat text z TIFF, načíst obrázek pro OCR a nastavit jazyk
  OCR.
og_title: Jak provést OCR na TIFF dokumentu – kompletní průvodce
tags:
- OCR
- Python
- Image Processing
title: Jak provést OCR na TIFF dokumentu – průvodce krok za krokem
url: /cs/python-java/general/how-to-perform-ocr-on-a-tiff-document-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provést OCR na TIFF dokumentu – kompletní průvodce

Už jste se někdy zamýšleli **jak provést OCR** na naskenovaném TIFF souboru, aniž byste strávili hodiny hledáním správné knihovny? Nejste sami. Mnoho vývojářů narazí na problém, když potřebují extrahovat text z TIFF obrázků, zejména když záleží na výkonu a nastavení jazyka.

V tomto tutoriálu projdeme vše, co potřebujete vědět: od instalace OCR balíčku, načtení obrázku pro OCR, nastavení jazyka OCR, až po **spuštění OCR na dokumentu** a získání čistého textu. Na konci budete mít připravený skript, který můžete vložit do libovolného projektu.

> **Tip:** I když příklad používá obecný modul `ocr`, stejné koncepty platí pro Tesseract, EasyOCR nebo jakýkoli moderní OCR engine, který nabízí Python API.

---

## Co budete potřebovat

- Python 3.8+ (jakákoli aktuální verze)
- OCR knihovnu, která poskytuje třídu `OcrEngine` (ve vzoru je použita fiktivní knihovna `ocr`; nahraďte ji tou skutečnou)
- Vícestránkový TIFF soubor, který chcete zpracovat (budeme ho nazývat `big_document.tif`)
- Počítač s alespoň 4 CPU jádry, pokud plánujete nastavit počet vláken

Žádné externí služby, žádné cloudové klíče — pouze lokální kód, který běží během několika sekund.

---

![jak provést OCR příklad](/images/ocr-example.png "jak provést OCR na TIFF dokumentu")

*Alt text obrázku: jak provést OCR na TIFF dokumentu – náhled extrahovaného textu.*

---

## Krok 1: Instalace a import OCR knihovny

Nejprve si nainstalujte knihovnu. Většina OCR balíčků je na PyPI, takže stačí jednoduchý `pip install`.

```bash
pip install ocr‑engine   # replace with the actual package name, e.g., pytesseract
```

Nyní importujte třídy, které budete potřebovat. Pokud používáte Tesseract, řádek importu bude vypadat jinak, ale zbytek kódu zůstane stejný.

```python
# Step 1: Import the OCR engine and image helper
import ocr                       # fictional package – swap with your real one
from ocr import OcrEngine, Image
```

*Proč je to důležité:* Importování správných symbolů hned na začátku zabraňuje kolizím jmenných prostorů později a činí skript přehlednějším.

---

## Krok 2: Vytvoření a konfigurace OCR enginu (nastavení jazyka OCR)

Konfigurace enginu je místo, kde **nastavíte jazyk OCR** pro přesné rozpoznání. Angličtina je výchozí, ale můžete přepnout na francouzštinu, němčinu nebo dokonce na vícejazykový režim jedním řádkem.

```python
# Step 2: Initialize the engine and set language
ocr_engine = OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # set OCR language to English
ocr_engine.set_thread_count(4)               # limit processing to 4 CPU cores
ocr_engine.set_memory_limit(512 * 1024 * 1024)  # 512 MB internal buffer
```

> **Proč 4 vlákna?** Většina moderních notebooků má alespoň čtyři jádra a omezení počtu vláken zabraňuje tomu, aby OCR proces zabral celý počítač — obzvláště užitečné, když skript běží na sdíleném serveru.

Pokud potřebujete jiný jazyk, stačí nahradit `ocr.Language.ENGLISH` za `ocr.Language.FRENCH`, `ocr.Language.SPANISH` a podobně.

---

## Krok 3: Načtení obrázku pro OCR (Load Image for OCR)

Nyní **načteme obrázek pro OCR**. Metoda `Image.load` načte TIFF soubor do paměti a automaticky zvládne vícestránkové dokumenty.

```python
# Step 3: Load the TIFF image you want to process
image_path = "YOUR_DIRECTORY/big_document.tif"
image = Image.load(image_path)   # load image for OCR
```

*Hraniční případ:* Pokud je soubor obrovský, můžete narazit na nedostatek RAM. V takovém případě zvažte načítání jedné stránky najednou pomocí `Image.load_page(page_number)` (pokud knihovna tuto funkci podporuje).

---

## Krok 4: Spuštění OCR na dokumentu

S připraveným enginem a načteným obrázkem je čas **spustit OCR na dokumentu**. Metoda `process` provede těžkou práci a vrátí objekt výsledku.

```python
# Step 4: Execute OCR
ocr_result = ocr_engine.process(image)
```

Za scénou engine rozdělí obrázek na textové bloky, spustí rozpoznávací model a výsledky spojí dohromady. Volání je blokující, což znamená, že skript čeká, dokud není celý TIFF zpracován — ideální pro dávkové úlohy.

---

## Krok 5: Extrakce textu z TIFF a ověření výstupu

Nakonec **extrahujeme text z TIFF** přístupem k atributu `text` výsledku. Vytiskneme prvních 200 znaků jako rychlou kontrolu.

```python
# Step 5: Show a preview of the recognized text
preview = ocr_result.text[:200]   # first 200 characters
print("Preview of OCR output:\n", preview)
```

**Očekávaný výstup (příklad):**

```
Preview of OCR output:
 In the United States, the Constitution guarantees the ...
```

Pokud potřebujete celý text, jednoduše použijte `ocr_result.text`. Pro další zpracování můžete výstup zapsat do souboru `.txt`:

```python
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(ocr_result.text)
```

---

## Kompletní funkční příklad

Sestavíme vše dohromady v připraveném skriptu. Nahraďte placeholder název balíčku tím, který jste skutečně nainstalovali.

```python
# -*- coding: utf-8 -*-
"""
How to Perform OCR on a TIFF Document – Complete Example
"""

# Install the OCR library first:
# pip install ocr-engine   # adjust to your actual package

import ocr
from ocr import OcrEngine, Image

def main():
    # 1️⃣ Initialize and configure the engine
    engine = OcrEngine()
    engine.language = ocr.Language.ENGLISH
    engine.set_thread_count(4)
    engine.set_memory_limit(512 * 1024 * 1024)

    # 2️⃣ Load the TIFF image
    img_path = "YOUR_DIRECTORY/big_document.tif"
    img = Image.load(img_path)

    # 3️⃣ Run OCR on the loaded image
    result = engine.process(img)

    # 4️⃣ Show a short preview and save the full text
    print("First 200 chars of OCR output:")
    print(result.text[:200])

    with open("extracted_text.txt", "w", encoding="utf-8") as out_file:
        out_file.write(result.text)

    print("\n✅ Extraction complete – see 'extracted_text.txt' for full output.")

if __name__ == "__main__":
    main()
```

Skript spustíte pomocí:

```bash
python ocr_tiff_example.py
```

Měli byste vidět náhled vytištěný do konzole a soubor s názvem `extracted_text.txt`, který obsahuje kompletní transkripci.

---

## Často kladené otázky a hraniční případy

- **Co když TIFF obsahuje více stránek?**  
  Většina OCR engineů zachází s každou stránkou jako s odděleným obrázkem. `ocr_result.text` bude obsahovat nový řádek mezi stránkami. Pokud potřebujete zpracovávat po stránkách, iterujte pomocí `Image.load_page(page_number)`.

- **Mohu místo TIFF zpracovat PNG nebo JPEG?**  
  Ano. Metoda `Image.load` obvykle přijímá libovolný formát podporovaný Pillow nebo podkladovou knihovnou. Stačí změnit příponu souboru.

- **Můj text je poškozený — mám změnit jazyk?**  
  Ano. Krok **nastavení jazyka OCR** je klíčový pro dokumenty v jiných jazycích. Ujistěte se, že je nainstalován jazykový balíček (např. `tesseract‑lang‑fra` pro francouzštinu).

- **Došla mi paměť?**  
  Snižte `set_memory_limit` nebo zpracovávejte stránky po jedné. Některé enginy také umožňují před rozpoznáním zmenšit rozlišení obrázku.

---

## Závěr

A máte to — stručný, plně funkční návod, **jak provést OCR** na TIFF souboru pomocí Pythonu. Probrali jsme vše od instalace knihovny, konfigurace enginu (včetně **nastavení jazyka OCR**), **načtení obrázku pro OCR**, **spuštění OCR na dokumentu** a nakonec **extrakci textu z TIFF**.  

Neváhejte experimentovat: upravte počet vláken, změňte jazyk nebo výstup OCR nasměrujte do pipeline pro zpracování přirozeného jazyka. Možnosti jsou neomezené, jakmile zvládnete základy.

Máte další otázky? Zanechte komentář níže a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}