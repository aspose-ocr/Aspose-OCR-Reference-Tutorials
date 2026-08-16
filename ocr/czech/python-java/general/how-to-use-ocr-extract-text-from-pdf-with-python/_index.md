---
category: general
date: 2026-04-26
description: jak používat OCR na naskenovaných PDF, extrahovat text z PDF, spustit
  OCR na PDF a převést naskenované PDF na prohledávatelné soubory během několika kroků
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: cs
og_description: 'jak používat OCR v Pythonu: naučte se, jak extrahovat text z PDF,
  spustit OCR na PDF a převést naskenované PDF na prohledávatelné dokumenty.'
og_title: Jak používat OCR – Rychlý průvodce extrakcí textu z PDF
tags:
- OCR
- Python
- PDF
- Text Extraction
title: jak použít OCR – extrahovat text z PDF pomocí Pythonu
url: /cs/python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak použít OCR – Extrahovat text z PDF pomocí Pythonu

Už jste se někdy zamysleli **jak použít OCR** k vytažení textu ze skenovaného kontraktu, účtenky nebo e-knihy? Nejste v tom sami. V mnoha reálných projektech je PDF, které obdržíte, jen obrázek a bez OCR nemůžete jeho obsah vyhledávat, indexovat ani analyzovat.  

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který ukazuje **jak použít OCR**, jak **extrahovat text z PDF** a proč byste mohli chtít **převést skenované PDF** soubory na prohledávatelné dokumenty. Také se podíváme na jemné umění **načítání PDF jako obrázku**, aby OCR engine viděl každou stránku jasně.

> **Rychlý náhled:** Na konci budete mít skript, který načte více‑stránkové PDF, spustí OCR na každé stránce a vytiskne rozpoznaný text – bez nutnosti externích služeb.

## Co budete potřebovat

- Python 3.9+ (jakákoli recentní verze funguje)
- `aocr` package (nebo jakákoli kompatibilní OCR knihovna, která poskytuje `OcrEngine` a `Image.load`)
- Skenovaný PDF soubor, který chcete zpracovat (např. `contract.pdf`)
- Přiměřené množství RAM (≈ 200 MB na 100‑stránkové PDF je obvykle v pořádku)

Pokud jste ještě nenainstalovali OCR knihovnu, spusťte:

```bash
pip install aocr
```

> **Tip:** Použijte virtuální prostředí, aby vaše závislosti byly přehledné.

## Krok 1: Načíst PDF jako obrázek – První část skládačky

Než může proběhnout jakékoli OCR, musí být PDF reprezentováno jako obrázek. Zde přichází do hry sekundární klíčové slovo **load pdf as image**.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*Proč je to důležité:* `aocr.Image.load` interně rasterizuje každou stránku PDF do bitmapy, kterou OCR engine dokáže pochopit. Pokud tento krok přeskočíte a předáte surové PDF, engine vyhodí chybu, protože očekává pixelová data, nikoli vektorová.

> **Poznámka:** Cesta může být absolutní nebo relativní. Ujistěte se, že soubor je čitelný; jinak narazíte na `FileNotFoundError`.

## Krok 2: Spustit OCR na PDF – Převod pixelů na znaky

Nyní, když PDF existuje jako obrázek, můžeme konečně **spustit OCR na PDF**. Následující úryvek zpracuje každou stránku najednou:

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*Co se děje pod kapotou?* `process_all_pages` prochází rasterizované stránky, aplikuje OCR model a vrací seznam objektů výsledků – jeden na stránku. Každý výsledek obsahuje rozpoznaný text, skóre důvěry a ohraničující rámečky (pokud je budete později potřebovat).

## Krok 3: Extrahovat text z PDF – Vytahování řetězců

S výsledky OCR v ruce se extrahování čistého textu stává triviálním. Projdeme stránky a vytiskneme výstup, čímž demonstrujeme sekundární klíčové slovo **extract text from pdf**.

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**Očekávaný výstup** (zkrácený pro stručnost):

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

Pokud potřebujete text v jediném řetězci, stačí jej spojit:

```python
full_text = "\n".join(r.text for r in page_results)
```

Nyní jste úspěšně **extrahovali text z PDF** pomocí OCR.

## Krok 4: Převést skenované PDF – Udělat jej prohledávatelným

Mnoho nástrojů v následném zpracování (např. Elasticsearch nebo SharePoint) očekává prohledávatelné PDF místo čistého textového výpisu. Můžete vložit výstup OCR zpět do původního PDF, čímž efektivně **convert scanned PDF** na prohledávatelnou verzi.

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*Proč to dělat?* Prohledávatelné PDF zachovává původní rozložení a obrázky a zároveň umožňuje výběr textu a indexaci – výhra pro lidi i stroje.

## Časté úskalí a okrajové případy

### Vícestránková PDF větší než paměť

Pokud má vaše PDF stovky stránek, načtení všeho najednou může vyčerpat RAM. Knihovna `aocr` podporuje líné načítání:

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

Pak zpracovávejte stránky po jedné:

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### Špatná kvalita skenů

Přesnost OCR dramaticky klesá u rozmazaných nebo nízkokontrastních skenů. Před předáním obrázku engine zvažte předzpracování:

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### Podpora jazyků

Ve výchozím nastavení engine předpokládá angličtinu. Pro **run OCR on PDF** v jiném jazyce nastavte kód jazyka:

```python
ocr_engine.language = "spa"  # Spanish
```

Ujistěte se, že odpovídající jazykový model je nainstalován.

## Kompletní funkční příklad

Spojením všeho dohromady získáte samostatný skript, který můžete vložit do souboru nazvaného `ocr_pdf.py` a spustit okamžitě:

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

Spusťte jej takto:

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

Uvidíte text vytištěný do konzole a pokud jste zadali `-o`, objeví se prohledávatelné PDF vedle původního souboru.

## Tipy a osvědčené postupy

- **Batch processing:** Při zpracování desítek PDF obalte výše uvedenou logiku smyčkou a zaznamenávejte úspěch/selhání každého souboru.
- **Confidence filtering:** Každý `page_result` obsahuje metriku důvěry. Odstraňte nebo označte stránky s nízkou důvěrou pro ruční revizi.
- **Parallelism:** Pokud má váš CPU více jader, zvažte použití `concurrent.futures` k paralelnímu zpracování stránek – jen dbejte na využití paměti.
- **Version lock:** API `aocr` se může vyvíjet. Uzamkněte verzi v `requirements.txt` (např. `aocr==2.3.1`), abyste se vyhnuli nekompatibilním změnám.

## Závěr

Prošli jsme **jak použít OCR** k **extrahování textu z PDF**, **spuštění OCR na PDF**, **načítání PDF jako obrázku** a dokonce **convert scanned PDF** do prohledávatelného formátu. Kód je kompletní, vysvětlení pokrývají jak *co*, tak *proč*, a nyní máte znovupoužitelný vzor pro jakýkoli projekt pracující s PDF založenými na obrázcích.

Co dál? Zkuste předat extrahovaný text do pipeline pro zpracování přirozeného jazyka, indexovat prohledávatelná PDF pomocí Elasticsearch, nebo experimentovat s různými OCR backendy jako Tesseract či Azure Computer Vision. Možnosti jsou neomezené a nástroje máte přímo po ruce.

Šťastné programování a ať jsou vaše PDF vždy prohledávatelná! 

![příklad jak použít OCR](/images/ocr_workflow.png "jak použít OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}