---
category: general
date: 2026-03-28
description: Naučte se rychle OCR PDF pomocí Pythonu. Tento průvodce vám ukáže, jak
  extrahovat text z PDF, rozpoznat text v PDF a převést naskenované PDF na text pomocí
  Aspose OCR.
draft: false
keywords:
- how to ocr pdf
- ocr pdf with python
- extract text from pdf
- recognize text from pdf
- convert scanned pdf to text
language: cs
og_description: Naučte se, jak OCR PDF pomocí Pythonu. Extrahujte text z PDF, rozpoznávejte
  text z PDF a během několika minut převádějte naskenované PDF na text.
og_title: Jak provést OCR PDF v Pythonu – Kompletní průvodce
tags:
- PDF
- OCR
- Python
- Aspose
title: Jak provést OCR PDF v Pythonu – krok za krokem průvodce
url: /cs/python-java/general/how-to-ocr-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak OCR PDF v Pythonu – krok za krokem průvodce

Už jste se někdy zamýšleli **jak OCR PDF** funguje, když je soubor jen obrázkem stránky? Nejste v tom sami. V tomto tutoriálu projdeme přesně kroky k OCR PDF souborům, extrahování textu z PDF a převodu naskenovaného PDF na prohledávatelný text – vše pomocí čistého Python kódu.

Probereme vše od instalace knihovny Aspose OCR až po získání rozpoznaného textu z každé stránky. Na konci budete schopni **OCR PDF s Pythonem**, **extrahovat text z PDF** a **převést naskenované PDF na text** bez zbytečného hledání v různých dokumentacích. Žádné zbytečnosti, jen praktický, spustitelný příklad, který můžete zkopírovat‑vložit.

## Co budete potřebovat

* Python 3.8+ (nejnovější stabilní verze funguje nejlépe)  
* Licence Aspose OCR for Python nebo klíč pro bezplatnou zkušební verzi – můžete jej získat na webu Aspose.  
* Naskenované PDF, které chcete zpracovat (budeme ho nazývat `input.pdf`).  

Pokud už to máte, skvělé – pojďme na to. Pokud ne, instalace balíčku je hračka a ukážeme vám, jak na to.

## Jak OCR PDF – nastavení prostředí

První věc, kterou musíte udělat, je získat modul Aspose OCR na svůj počítač. Balíček se jmenuje `aspose-ocr` a můžete jej nainstalovat pomocí pip:

```bash
pip install aspose-ocr
```

> **Tip:** Použijte virtuální prostředí (`python -m venv venv`), aby vaše závislosti zůstaly přehledné.

Jakmile je balíček nainstalován, můžete jej importovat a spustit OCR engine. To je základ pro každý **ocr pdf with python** workflow, který později vytvoříte.

## OCR PDF s Pythonem – import Aspose OCR

Nyní, když je knihovna k dispozici, přidejme ji do našeho skriptu. Také nastavíme engine, aby pracoval v *direct PDF mode*, což říká Aspose, aby četl PDF bajty přímo ze souboru místo převodu každé stránky na obrázek.

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr

# Step 2: Create an OCR engine instance and enable direct PDF processing
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
```

Proč použít `PdfMode.DIRECT`? Protože přeskočí další krok rasterizace, což proces zrychlí a zachová původní rozložení – zvláště užitečné, když potřebujete **recognize text from PDF** přesně.

## Rozpoznání textu z PDF – spuštění engine

S připraveným enginem nasměrujte na svůj naskenovaný soubor. Metoda `recognize_from_pdf` udělá veškerou těžkou práci: projde každou stránku, spustí OCR algoritmus a vrátí objekt `OcrResult`, který obsahuje kolekci objektů `Page`.

```python
# Step 3: Define the path to the PDF you want to process
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# Step 4: Perform OCR on the PDF and obtain the result object
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)
```

Zajímá vás, jestli to funguje i s šifrovanými PDF – ano, stačí před voláním `recognize_from_pdf` nastavit heslo pomocí `ocr_engine.password = "secret"`. To je okrajový případ, který mnoho tutoriálů opomíjí, ale v reálných pipelinech se hodí.

## Extrahování textu z PDF – přístup k výsledkům stránek

Seznam `ocr_result.pages` obsahuje jeden záznam na stránku. Každý objekt `Page` má atribut `.text`, který obsahuje čistý textový výstup naskenované stránky. Projděte jej a vytiskněte výsledky, abyste viděli, co bylo skutečně extrahováno.

```python
# Step 5: Iterate through each page and display the recognized text
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)
```

Spuštěním skriptu získáte výstup podobný tomuto:

```
PDF OCR complete. Text per page:
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Tento výstup dokazuje, že jste úspěšně **extract text from PDF** a **recognize text from PDF** pomocí Aspose OCR. Nyní můžete řetězce poslat do databáze, vyhledávacího indexu nebo jakékoliv další NLP pipeline.

![příklad jak OCR PDF](placeholder-image.png "příklad jak OCR PDF")

*Text alternativního obrázku:* **příklad jak OCR PDF** – ukazuje výstup konzole s rozpoznaným textem pro každou stránku.

## Převod naskenovaného PDF na text – uložení výstupu

Většina vývojářů nechce jen vidět text v konzoli; potřebují trvalý soubor. Níže je malý pomocník, který zapíše text každé stránky do samostatného `.txt` souboru, čímž efektivně **convert scanned PDF to text** ve složce nazvané `output`.

```python
import os

output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

Po dokončení skriptu budete mít uklizený adresář:

```
output_text/
│─ page_1.txt
│─ page_2.txt
└─ …
```

Nyní jste plně **convert scanned PDF to text** a můžete tyto soubory předat jakémukoliv dalšímu procesu – vyhledávání, analytice nebo i jednoduchému `grep`.

## Časté otázky a okrajové případy

**Co když moje PDF obsahuje obrázky smíšené se skutečným textem?**  
Aspose OCR se pokusí rozpoznat vše, ale můžete proces urychlit vypnutím OCR pro stránky, které již obsahují vybratelný text. Nastavte `ocr_engine.auto_detect_page_orientation = True` a poté zavolejte `ocr_engine.recognize_from_pdf(..., detect_text=False)` pro stránky, o nichž víte, že jsou v pořádku.

**Mohu řídit jazykový model?**  
Určitě. Nastavte `ocr_engine.language = aocr.Language.English` (nebo jakýkoli podporovaný jazyk) před voláním `recognize_from_pdf`. To zvyšuje přesnost u dokumentů v jiných jazycích než angličtině.

**Jak zacházet s velmi velkými PDF (100 + stránek)?**  
Zpracovávejte je po částech. Metoda `recognize_from_pdf` přijímá argument `page_range`, např. `ocr_engine.recognize_from_pdf(path, page_range=(1, 20))`. Procházejte rozsahy v cyklu, aby se udržela nízká spotřeba paměti.

## Kompletní funkční příklad

Spojením všech částí získáte jediný skript, který můžete uložit do souboru `ocr_pdf.py` a spustit:

```python
import os
import aspose.ocr as aocr

# -------------------------------------------------
# 1️⃣  Initialize the OCR engine (direct PDF mode)
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
# Optional: set language for better accuracy
ocr_engine.language = aocr.Language.English

# -------------------------------------------------
# 2️⃣  Path to the scanned PDF you want to process
# -------------------------------------------------
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# -------------------------------------------------
# 3️⃣  Run OCR – this is where we actually recognize text from PDF
# -------------------------------------------------
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)

# -------------------------------------------------
# 4️⃣  Print the extracted text (shows how to extract text from PDF)
# -------------------------------------------------
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)

# -------------------------------------------------
# 5️⃣  Save each page as a .txt file (convert scanned PDF to text)
# -------------------------------------------------
output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

Spusťte jej pomocí:

```bash
python ocr_pdf.py
```

Měli byste vidět výstup v konzoli, který potvrzuje text každé stránky a umístění uložených `.txt` souborů.

## Závěr

Probrali jsme **how to OCR PDF** pomocí Pythonu, ukázali čistý způsob **ocr pdf with python**, ukázali jsme, jak **extract text from PDF**, vysvětlili mechaniku **recognize text from PDF** a nakonec poskytli připravený úryvek, který **convert scanned PDF to text**. Celý proces je zabalen

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}