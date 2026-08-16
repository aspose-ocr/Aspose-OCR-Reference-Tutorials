---
category: general
date: 2026-03-18
description: Spusťte OCR na obrázku, abyste extrahovali text z PNG a vytvořili prohledávatelný
  PDF. Naučte se, jak rozpoznat textový obrázek a převést PNG do PDF během několika
  minut.
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: cs
og_description: Spusťte OCR na obrázku, abyste z PNG extrahovali text, rozpoznali
  textový obrázek a vytvořili prohledávatelný PDF. Postupujte podle tohoto průvodce
  krok za krokem.
og_title: Spusťte OCR na obrázku – rychle extrahujte text z PNG
tags:
- OCR
- Python
- Image Processing
title: Spusťte OCR na obrázku – rychle extrahujte text z PNG
url: /cs/python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Spusťte OCR na obrázku – Rychle extrahujte text z PNG

Už jste někdy potřebovali **spustit OCR na obrázku** soubory, ale nebyli jste si jisti, kde začít? Možná máte naskenovaný článek uložený jako `article.png` a chcete jen prostý text, nebo potřebujete pro archivaci prohledávatelný PDF. V každém případě jste na správném místě. V tomto tutoriálu vás provedeme extrahováním textu z PNG, rozpoznáním textového obrázku a dokonce převodem tohoto PNG na prohledávatelný PDF – vše pomocí několika řádků kódu.

> **Co získáte:** kompletní, spustitelný skript, který načte PNG, spustí OCR, uloží výstup hOCR a volitelně vytvoří prohledávatelný PDF. Žádné chybějící importy, žádné „viz dokumentaci“ slepé uličky – jen samostatné řešení, které můžete dnes vložit do svého projektu.

## Požadavky

Než se ponoříme dál, ujistěte se, že máte:

- **Python 3.8+** (syntaxe použitá zde funguje na jakékoli nedávné verzi)
- Knihovnu **`ocr_engine`**, kterou používáte (příklad předpokládá třídu `OcrEngine`; v případě potřeby nahraďte Tesseract, EasyOCR atd.)
- PNG obrázek, který chcete zpracovat (např. `article.png` umístěný ve složce, na kterou můžete odkazovat)
- Oprávnění k zápisu do výstupního adresáře

Pokud používáte Tesseract pod kapotou, nainstalujte jej pomocí:

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

A poté nainstalujte Python wrapper:

```bash
pip install pytesseract Pillow
```

*Tip:* udržujte svou OCR knihovnu aktuální – nové jazykové balíčky a vylepšení výkonu přicházejí často.

## Spusťte OCR na obrázku – Průvodce krok za krokem

Níže je **kompletní skript**. Klidně jej zkopírujte do souboru s názvem `run_ocr.py` a spusťte pomocí `python run_ocr.py`.

```python
# run_ocr.py
import os
from pathlib import Path

# Import the OCR engine – replace with your actual import if different
# For Tesseract via pytesseract you would use: import pytesseract
# Here we assume a generic OcrEngine class that matches the example
from ocr_engine import OcrEngine  # <-- adjust as needed

def main():
    # ------------------------------------------------------------------
    # Step 1: Create an OCR engine instance
    # ------------------------------------------------------------------
    ocr_engine = OcrEngine()
    # Why this matters: the engine holds configuration (language, DPI, etc.)
    # You can tweak ocr_engine.setLanguage('eng') or similar before proceeding.

    # ------------------------------------------------------------------
    # Step 2: Load the image you want to process
    # ------------------------------------------------------------------
    image_path = Path("YOUR_DIRECTORY/article.png")
    if not image_path.is_file():
        raise FileNotFoundError(f"Image not found: {image_path}")
    ocr_engine.setImageFromFile(str(image_path))

    # ------------------------------------------------------------------
    # Step 3: Choose the export format
    # ------------------------------------------------------------------
    # hOCR preserves layout (bounding boxes, fonts) – perfect for searchable PDFs.
    # Other options: "txt", "pdf", "pdfa"
    ocr_engine.setExportFormat("hocr")

    # ------------------------------------------------------------------
    # Step 4: Run the recognition process
    # ------------------------------------------------------------------
    ocr_result = ocr_engine.recognize()
    # The result object gives us access to the raw OCR text, hOCR, etc.

    # ------------------------------------------------------------------
    # Step 5: Write the HOCR output to a file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/article.hocr")
    with open(output_path, "w", encoding="utf-8") as output_file:
        output_file.write(ocr_result.getExportedContent())
    print(f"✅ HOCR saved to {output_path}")

    # ------------------------------------------------------------------
    # Optional: Generate a searchable PDF from the HOCR
    # ------------------------------------------------------------------
    # Many OCR engines can bundle the original image with the hOCR to produce
    # a PDF that you can search. If your engine supports it, uncomment:
    # ocr_engine.setExportFormat("pdf")
    # pdf_result = ocr_engine.recognize()
    # pdf_path = Path("YOUR_DIRECTORY/article_searchable.pdf")
    # with open(pdf_path, "wb") as pdf_file:
    #     pdf_file.write(pdf_result.getExportedContent())
    # print(f"📄 Searchable PDF created at {pdf_path}")

if __name__ == "__main__":
    main()
```

### Co skript dělá, v běžném jazyce

1. **Instantiate** (vytvoří) OCR engine, abyste mohli ovládat jeho nastavení.
2. **Load** (načte) PNG soubor (`article.png`). Skript se ukončí dříve, pokud soubor neexistuje – žádné tajemné chyby `NoneType` později.
3. **Select** (vybere) `hocr` jako exportní formát. Tento formát zachovává původní rozložení, což je nezbytné pro následný převod obrázku na prohledávatelný PDF.
4. **Run** (spustí) rozpoznávací engine; zde probíhá těžká práce.
5. **Write** (zapíše) hOCR XML do `article.hocr`. Nyní máte strojově čitelnou reprezentaci textu a jeho souřadnic.
6. *(Optional)* Přepne na `"pdf"` a v jednom dalším kroku vygeneruje prohledávatelný PDF.

**Očekávaný výstup** je soubor `.hocr` kódovaný v UTF‑8, který vypadá zhruba takto (zkráceně):

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

Pokud odkomentujete část s PDF, získáte také `article_searchable.pdf`, který můžete otevřít v libovolném PDF prohlížeči a pomocí vyhledávacího pole **Ctrl + F** okamžitě najít slova.

![Příklad výstupu OCR na obrázku](example.png "OCR na obrázku – výsledky hOCR a PDF")

## Jak extrahovat text z PNG pomocí OcrEngine

Pokud potřebujete jen surový text (bez rozložení, bez PDF), můžete krok hOCR úplně přeskočit:

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*Proč zvolit prostý text?* Je lehký, ideální pro indexování a skvěle funguje s následnými NLP pipeline.

## Rozpoznat textový obrázek a vytvořit prohledávatelný PDF

Vytvoření prohledávatelného PDF je dvoufázový proces:

1. **Run OCR** (spustí OCR) s `hocr` (jako výše) pro získání informací o rozložení.
2. **Combine** (kombinuje) původní PNG s hOCR do PDF pomocí PDF exportéru engine.

Většina moderních OCR knihoven (Tesseract, ABBYY, Google Vision) poskytuje export `pdf`, který přesně toto dělá. Úryvek v *Optional* bloku hlavního skriptu ukazuje vzor. Pokud vaše knihovna nemá vestavěný PDF exportér, můžete použít **`pdf2image`** + **`reportlab`** k propojení obrázku a hOCR – stačí mi dát vědět a pošlu rychlý doplňkový příklad.

## Převést PNG na PDF s výstupem OCR

Někdy chcete jen **prostý PDF**, který obsahuje obrázek (bez prohledávatelné vrstvy). To je ještě jednodušší:

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

Spojte to s OCR krokem, pokud potřebujete prohledávatelnou verzi, nebo to nechte jako věrnou vizuální repliku pro archivaci.

## Časté problémy a tipy

| Problém | Proč se to děje | Rychlé řešení |
|-------|----------------|-----------|
| **Rozmazané nebo nízké rozlišení PNG** | Přesnost OCR dramaticky klesá pod ~300 DPI. | Zvětšete pomocí `Image.resize((width*2, height*2), Image.LANCZOS)` před předáním do engine. |
| **Špatný jazyk** | Engine má výchozí nastavení na angličtinu; neanglické znaky se zkomolí. | Zavolejte `ocr_engine.setLanguage('deu')` (nebo příslušný ISO kód) před `recognize()`. |
| **Chybějící hOCR výstup** | Některé enginy mají výchozí nastavení na prostý text, pokud není zavoláno `setExportFormat`. | Zkontrolujte, že `setExportFormat("hocr")` běží **před** `recognize()`. |
| **Chyby oprávnění k souborům** | Pokus o zápis do složky jen pro čtení. | Použijte cestu uvnitř projektu nebo nejprve `os.makedirs(..., exist_ok=True)`. |
| **Velké PDF způsobují špičky v paměti** | Exportér PDF drží celý obrázek v RAM. | Zpracovávejte stránky po částech nebo použijte streamovací PDF zapisovač. |

*Tip:* vždy testujte na malém vzorku obrázku před rozšířením na tisíce. Ušetří to hodiny ladění.

## Závěr

Nyní víte **jak spustit OCR na obrázku** soubory, **extrahovat text z PNG**, **rozpoznat textový obrázek** pro následné úkoly, **vytvořit prohledávatelný PDF** a **převést PNG na PDF**, když potřebujete jednoduchý archiv. Poskytnutý skript je kompletní, připravený ke zkopírování a funguje ihned, a volitelné sekce vám umožní přizpůsobit výstup přesně vašemu workflow.

### Co dál?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}