---
category: general
date: 2026-06-25
description: Provádějte OCR na PDF pomocí Pythonu – naučte se, jak načíst PDF pro
  OCR, extrahovat text z PDF stránek a efektivně zobrazit rozpoznaný text.
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF pages
- load PDF for OCR
- how to OCR large PDF
- preview recognized text
language: cs
og_description: Proveďte OCR na PDF v Pythonu. Tento návod ukazuje, jak načíst PDF
  pro OCR, extrahovat text z PDF stránek a rychle si prohlédnout rozpoznaný text.
og_title: Provádějte OCR v PDF pomocí Pythonu – krok za krokem tutoriál
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  headline: Perform OCR on PDF with Python – Complete Guide
  type: TechArticle
- description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  name: Perform OCR on PDF with Python – Complete Guide
  steps:
  - name: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
    text: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
  - name: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
    text: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
  - name: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
    text: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
  - name: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
    text: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Proveďte OCR v PDF pomocí Pythonu – Kompletní průvodce
url: /cs/python/general/perform-ocr-on-pdf-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Perform OCR on PDF with Python – Complete Guide

Už jste někdy potřebovali **perform OCR on PDF** soubory, ale nebyli jste si jisti, kde začít? Možná máte hromadu naskenovaných smluv, nebo jediné objemné příručky, která odmítá spolupracovat s vaším běžným extraktorem textu. Stručně řečeno, chcete **load PDF for OCR**, vytáhnout text a získat rychlý náhled — a to vše, aniž byste přetížili paměť vašeho počítače.

No, jste na správném místě. V tomto tutoriálu projdeme plně funkční Python skript, který **extracts text from PDF pages**, ukáže vám, jak **preview recognized text**, a dokonce se vypořádá s klasickým problémem **how to OCR large PDF** souborů efektivně.

Na konci budete mít připravený program k spuštění, jasné pochopení každého konfiguračního parametru a několik tipů, jak se vyhnout běžným úskalím, která nováčky často potkají.

---

## Co se naučíte

- Jak **load PDF for OCR** pomocí knihovny `aocr`.
- Přesné kroky k **perform OCR on PDF** stránkám po jedné.
- Způsoby, jak **extract text from PDF pages** při zachování kontrolované spotřeby paměti.
- Jak **preview recognized text** pro ověření výsledků.
- Strategie pro zpracování **large PDFs** bez vyčerpání RAM.

> **Tip:** Tento průvodce předpokládá, že máte nainstalovaný Python 3.9+ a základní znalost virtuálních prostředí. Pokud jste v Pythonu noví, nejprve si nastavte virtualenv — věřte mi, ušetří vám to pozdější problémy.

## Požadavky

| Požadavek | Proč je důležitý |
|-------------|----------------|
| `aocr` Python package (or any compatible OCR engine) | Poskytuje třídu `OcrEngine` používanou v celém skriptu. |
| `pip` and a virtual environment | Udržuje závislosti oddělené od systémového Pythonu. |
| Sufficient disk space for temporary image extracts | Některé OCR enginy zapisují obrázky stránek na disk před zpracováním. |
| Optional: `tqdm` for progress bars | Zlepšuje UX při práci s **how to OCR large PDF** úlohami. |

Nainstalujte nezbytné pomocí:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate
pip install aocr tqdm
```

Pokud je váš PDF chráněn heslem, budete muset heslo zadat později — viz sekce „Edge Cases“.

## Krok 1: Perform OCR on PDF – Nastavení enginu

Nejprve potřebujeme instanci OCR enginu. Představte si ji jako mozek, který přečte obrázek každé stránky a vypíše prostý text.

```python
import aocr                     # The OCR library
from tqdm import tqdm           # Optional, for a nice progress bar

def create_engine():
    """
    Initialise the OcrEngine with sensible defaults.
    Returns the configured engine ready for processing.
    """
    engine = aocr.OcrEngine()
    # Limit memory usage – crucial when tackling how to OCR large PDF files
    engine.max_memory_mb = 200               # 200 MB cap, adjust if needed
    # Choose a recognition mode that matches your source material
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine
```

**Proč nastavit `max_memory_mb`?**  
OCR enginy často ukládají obrázky stránek do RAM. Omezováním paměti zabráníte zhroucení skriptu při 500‑stránkové smlouvě.

## Krok 2: Load PDF for OCR a nastavení konfigurace

Nyní skutečně **load PDF for OCR**. Cesta může být absolutní nebo relativní; jen se ujistěte, že soubor existuje.

```python
def load_pdf(engine, pdf_path):
    """
    Loads the PDF into the OCR engine.
    Raises FileNotFoundError if the file does not exist.
    """
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages ready.")
    except Exception as e:
        raise RuntimeError(f"Failed to load PDF: {e}")
```

Pokud je PDF šifrovaný, `engine.load_pdf` obvykle vyvolá výjimku. V takovém případě můžete zavolat `engine.load_pdf(pdf_path, password="secret")` — více o tom později.

## Krok 3: Extract Text from PDF Pages – Hlavní smyčka

Zde **perform OCR on PDF** stránku po stránce. Také **preview recognized text** pro prvních několik stovek znaků, abyste mohli ověřit, že vše funguje.

```python
def ocr_pages(engine, preview_len=200):
    """
    Iterates over each page, runs OCR, and yields the recognized text.
    Also prints a short preview for each page.
    """
    for page_index in tqdm(range(engine.page_count), desc="Processing pages"):
        # Select the current page – essential for multi‑page PDFs
        engine.select_page(page_index)

        # Perform the actual OCR
        page_text = engine.recognize()

        # Preview the first `preview_len` characters (helps with debugging)
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))

        yield page_text
```

**Pro tip:** Ukazatel postupu `tqdm` vám dává vizuální vodítko, což je zvláště užitečné při práci s **how to OCR large PDF** dokumenty, které zpracování trvá minuty.

## Krok 4: Sestavení všeho dohromady – připravený skript

Níže je kompletní spustitelný příklad. Uložte jej jako `pdf_ocr.py` a spusťte pomocí `python pdf_ocr.py path/to/your/file.pdf`.

```python
#!/usr/bin/env python3
"""
Complete script to perform OCR on PDF, extract text from PDF pages,
and preview recognized text. Works for both small and large PDFs.
"""

import sys
import aocr
from tqdm import tqdm

def create_engine():
    engine = aocr.OcrEngine()
    engine.max_memory_mb = 200
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine

def load_pdf(engine, pdf_path):
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages.")
    except Exception as exc:
        raise RuntimeError(f"Unable to load PDF: {exc}")

def ocr_pages(engine, preview_len=200):
    for page_index in tqdm(range(engine.page_count), desc="OCR progress"):
        engine.select_page(page_index)
        page_text = engine.recognize()
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))
        yield page_text

def main(pdf_path):
    engine = create_engine()
    load_pdf(engine, pdf_path)

    all_text = []
    for txt in ocr_pages(engine):
        all_text.append(txt)

    # Optional: write the combined output to a .txt file
    out_path = pdf_path.rsplit(".", 1)[0] + "_ocr.txt"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write("\n\n".join(all_text))
    print(f"\n✅ OCR complete. Full text saved to: {out_path}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python pdf_ocr.py <path_to_pdf>")
        sys.exit(1)
    pdf_file = sys.argv[1]
    main(pdf_file)
```

### Očekávaný výstup (úryvek)

```
✅ Loaded 'large_contract.pdf' – 342 pages.

--- Page 1 Preview ---
Contract Agreement between Party A and Party B ... 

--- Page 2 Preview ---
Recitals: Whereas, the parties desire to ...

...
✅ OCR complete. Full text saved to: large_contract_ocr.txt
```

Uvidíte krátký náhled pro každou stránku, následovaný konečným potvrzením, že spojený textový soubor byl zapsán.

## Okrajové případy a praktické tipy

| Situace | Co dělat |
|-----------|------------|
| **Encrypted PDF** | Pass the password: `engine.load_pdf(pdf_path, password="mySecret")`. |
| **Very large PDF (> 1000 pages)** | Opatrně zvyšte `max_memory_mb`, nebo zpracovávejte po částech (např. 200 stránek najednou). |
| **Mixed content (printed + handwritten)** | Přepněte `engine.recognition_mode` na `aocr.RecognitionMode.MIXED`, pokud knihovna podporuje tuto možnost. |
| **Missing fonts or poor scan quality** | Před voláním `recognize()` předzpracujte stránky pomocí knihovny pro vylepšení obrazu (např. Pillow). |
| **Out‑of‑memory crashes** | Snižte `preview_len` nebo zapisujte text každé stránky přímo na disk místo toho, abyste jej uchovávali všechny v seznamu. |

## Jak efektivně OCR velké PDF – Pokročilé strategie

Při řešení **how to OCR large PDF** se rychlost a stabilita stávají kritickými. Zde je několik triků, které můžete do skriptu přidat:

1. **Parallelize per page** – Použijte `concurrent.futures.ThreadPoolExecutor`, pokud je OCR engine thread‑safe.
2. **Cache intermediate images** – Některé enginy umožňují ukládat rasterizované stránky na SSD, což dramaticky snižuje zatížení CPU při opakovaném běhu.
3. **Batch write output** – Místo přidávání do Python seznamu otevřete výstupní soubor jednou a zapisujte text každé stránky, jakmile je připraven.
4. **Adjust DPI** – Snížení DPI během rasterizace snižuje paměť, ale může ovlivnit přesnost; najděte optimální hodnotu (obvykle 200‑300 DPI).

Níže je rychlý úryvek ukazující, jak můžete paralelizovat krok OCR (volitelné, odkomentujte pro použití):

```python
# from concurrent.futures import ThreadPoolExecutor

# def ocr_page(engine, idx):
#     engine.select_page(idx)
#     return engine.recognize()

# with ThreadPoolExecutor(max_workers=4) as executor:
#     results = list(tqdm(executor.map(lambda i: ocr_page(engine, i),
#                                    range(engine.page_count)),
#                     total=engine.page_count,
#                     desc="Parallel OCR"))
```

Pamatujte: paralelizmus může zvýšit využití CPU, takže během dlouhých běhů sledujte teplotu systému.

## Často kladené otázky

**Q: Můžu použít tento skript s jinými OCR knihovnami jako Tesseract?**  
A: Absolutely. Replace the `aocr` calls with `pytesseract.image_to

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak OCR PDF v .NET s Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Jak provést extrakci textu z obrazu ze streamu pomocí Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Jak extrahovat text z obrázku z URL pomocí Aspose.OCR pro Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}