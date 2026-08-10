---
category: general
date: 2026-05-31
description: Vytvořte prohledávatelný PDF ze skenovaných obrázků pomocí Python OCR.
  Naučte se, jak převést PDF se skenovaným obrázkem, převést TIFF na PDF a během několika
  minut přidat OCR textovou vrstvu.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- convert tiff to pdf
- how to run OCR
- add OCR text layer
language: cs
og_description: Vytvořte okamžitě prohledávatelný PDF. Tento průvodce ukazuje, jak
  spustit OCR, převést naskenovaný PDF obrázek a přidat OCR textovou vrstvu pomocí
  jediného Python skriptu.
og_title: Vytvořte prohledávatelný PDF pomocí Pythonu – kompletní tutoriál
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  headline: Create Searchable PDF with Python – Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  name: Create Searchable PDF with Python – Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: 1️⃣ Can I process multi‑page PDFs?
    text: Yes. Use `ocr_engine.load_image("file.pdf")` and then loop over each page
      with `ocr_engine.recognize(pdf_save_options, page_number)`. The library will
      automatically generate a multi‑page searchable PDF.
  - name: 2️⃣ What if my source file is a high‑resolution TIFF (300 dpi+)?
    text: 'Higher DPI yields better OCR accuracy but also larger memory usage. If
      you hit a `MemoryError`, downscale the image first:'
  - name: 3️⃣ How do I change the language of the OCR?
    text: 'Set the `language` property on the engine before loading the image:'
  - name: 4️⃣ What if I need to keep the original image quality?
    text: The `PdfSaveOptions` class has a `compression` property. Set it to `PdfCompression.None`
      to preserve the raster data exactly as it was.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Document Automation
title: Vytvořte prohledávatelný PDF pomocí Pythonu – krok za krokem
url: /cs/python-java/general/create-searchable-pdf-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF pomocí Pythonu – krok za krokem

Už jste se někdy zamýšleli, jak **vytvořit prohledávatelné PDF** ze skenované stránky, aniž byste museli balit desítky nástrojů? Nejste v tom sami. V mnoha kancelářských pracovních postupech se naskenovaný TIFF nebo JPEG uloží na sdílený disk a další osoba musí text ručně kopírovat a vkládat – bolestivé, náchylné k chybám a ztrátě času.  

V tomto tutoriálu projdeme čistým, programovým řešením, které vám umožní **převést skenovaný obrázek PDF**, **převést TIFF do PDF** a **přidat OCR textovou vrstvu** najednou. Na konci budete mít připravený skript, který spustí OCR, vloží skrytý text a vytvoří prohledávatelné PDF, které můžete indexovat, vyhledávat nebo sdílet s jistotou.

## Co budete potřebovat

- Python 3.9+ (jakákoli novější verze funguje)
- balíčky `aspose-ocr` a `aspose-pdf` (instalované pomocí `pip install aspose-ocr aspose-pdf`)
- Naskenovaný obrázek (`.tif`, `.png`, `.jpg` nebo i PDF stránka, která je jen obrázek)
- Mírné množství RAM (OCR engine je nenáročný; i notebook to zvládne)

> **Tip:** Pokud používáte Windows, nejjednodušší způsob, jak získat balíčky, je spustit příkaz v oprávněném PowerShell okně.

```bash
pip install aspose-ocr aspose-pdf
```

Nyní, když jsou předpoklady za sebou, ponořme se do kódu.

## Krok 1: Vytvoření instance OCR engine – *create searchable pdf*

První věc, kterou uděláme, je spuštění OCR engine. Představte si ho jako mozek, který přečte každý pixel a přemění jej na znaky.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine – this is the core of the create searchable pdf process
ocr_engine = OcrEngine()
```

> **Proč je to důležité:** Inicializace engine jen jednou udržuje nízkou spotřebu paměti. Kdybyste volali `OcrEngine()` uvnitř smyčky pro každou stránku, rychle byste vyčerpali zdroje.

## Krok 2: Načtení skenovaného obrázku – *convert tiff to pdf* & *convert scanned image pdf*

Dále nasměrujte engine na soubor, který chcete zpracovat. API přijímá libovolný rastrový obrázek, takže TIFF funguje stejně dobře jako JPEG.

```python
# Load the image you want to OCR. Replace the path with your own file location.
ocr_engine.load_image("YOUR_DIRECTORY/scanned_page.tif")
```

Pokud máte PDF, které obsahuje jen skenovaný obrázek, můžete stále použít `load_image`, protože Aspose automaticky extrahuje první stránku.

## Krok 3: Příprava možností uložení PDF – *add OCR text layer*

Zde konfigurujeme, jak má finální PDF vypadat. Klíčovým příznakem je `create_searchable_pdf`; nastavení na `True` říká knihovně, aby vložila neviditelnou textovou vrstvu, která odráží vizuální obsah.

```python
from aspose.pdf import PdfSaveOptions

pdf_save_options = PdfSaveOptions()
pdf_save_options.create_searchable_pdf = True   # embed OCR text layer
pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"
```

> **Co textová vrstva dělá:** Když otevřete výsledný soubor v Adobe Reader a pokusíte se vybrat text, uvidíte skryté znaky. Vyhledávače je také mohou indexovat – ideální pro soulad nebo archivaci.

## Krok 4: Spuštění OCR a uložení – *how to run OCR* v jediném volání

Nyní se děje magie. Jedno volání metody spustí rozpoznávací engine a zapíše prohledávatelné PDF na disk.

```python
# Run OCR and generate the searchable PDF in one go
ocr_engine.recognize(pdf_save_options)

print("PDF saved as searchable PDF.")
```

Metoda `recognize` vrací objekt stavu, který můžete zkontrolovat na chyby, ale pro většinu jednoduchých scénářů je výše uvedené volání dostačující.

### Očekávaný výstup

Spuštění skriptu vypíše:

```
PDF saved as searchable PDF.
```

Pokud otevřete `scanned_page_searchable.pdf`, všimnete si, že můžete vybrat text, zkopírovat ho a dokonce provést hledání `Ctrl+F`. To je znak workflow **create searchable pdf**.

## Kompletní funkční skript

Níže je kompletní, připravený ke spuštění skript. Stačí nahradit zástupné cesty skutečnými umístěními souborů.

```python
# ------------------------------------------------------------
# create_searchable_pdf.py – Convert scanned image to searchable PDF
# ------------------------------------------------------------

from aspose.ocr import OcrEngine
from aspose.pdf import PdfSaveOptions

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load image (TIFF, JPEG, PNG, or scanned PDF page)
    image_path = "YOUR_DIRECTORY/scanned_page.tif"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure PDF output – embed OCR text layer
    pdf_save_options = PdfSaveOptions()
    pdf_save_options.create_searchable_pdf = True
    pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"

    # 4️⃣ Run OCR and write searchable PDF
    ocr_engine.recognize(pdf_save_options)

    print("PDF saved as searchable PDF.")

if __name__ == "__main__":
    main()
```

Uložte tento soubor jako `create_searchable_pdf.py` a spusťte:

```bash
python create_searchable_pdf.py
```

## Často kladené otázky a okrajové případy

### 1️⃣ Můžu zpracovávat vícestránkové PDF?

Ano. Použijte `ocr_engine.load_image("file.pdf")` a poté projděte každou stránku pomocí `ocr_engine.recognize(pdf_save_options, page_number)`. Knihovna automaticky vygeneruje vícestránkové prohledávatelné PDF.

### 2️⃣ Co když je můj zdrojový soubor vysoké rozlišení TIFF (300 dpi+)?

Vyšší DPI poskytuje lepší přesnost OCR, ale také vyšší spotřebu paměti. Pokud narazíte na `MemoryError`, nejprve zmenšete velikost obrázku:

```python
from PIL import Image
img = Image.open(image_path)
img = img.resize((int(img.width * 0.5), int(img.height * 0.5)), Image.ANTIALIAS)
img.save("temp.tif")
ocr_engine.load_image("temp.tif")
```

### 3️⃣ Jak změním jazyk OCR?

Nastavte vlastnost `language` na engine před načtením obrázku:

```python
ocr_engine.language = "fra"   # French
```

Úplný seznam podporovaných jazykových kódů najdete v dokumentaci Aspose.

### 4️⃣ Co když potřebuji zachovat původní kvalitu obrázku?

Třída `PdfSaveOptions` má vlastnost `compression`. Nastavte ji na `PdfCompression.None`, aby se rasterová data zachovala přesně tak, jak byla.

```python
pdf_save_options.compression = "None"
```

## Tipy pro nasazení v produkčním prostředí

- **Dávkové zpracování:** Zabalte hlavní logiku do funkce, která přijímá seznam cest k souborům. Každý úspěch/neúspěch zaznamenejte do CSV pro auditní stopy.
- **Paralelizace:** Použijte `concurrent.futures.ThreadPoolExecutor` k běhu OCR na více jádrech. Pamatujte, že každý vláken potřebuje svou vlastní instanci `OcrEngine`.
- **Bezpečnost:** Pokud pracujete s citlivými dokumenty, spusťte skript v sandboxovaném prostředí a po zpracování okamžitě odstraňte dočasné soubory.

## Závěr

Nyní víte, jak **vytvořit prohledávatelné PDF** soubory ze skenovaných obrázků pomocí stručného Python skriptu. Inicializací OCR engine, načtením TIFF (nebo libovolného rastrového souboru), konfigurací `PdfSaveOptions` pro **add OCR text layer** a nakonec voláním `recognize` se celý pipeline **convert scanned image pdf** a **convert TIFF to PDF** promění v jediný, opakovatelný příkaz.

Další kroky? Zkuste propojit tento skript s monitorovacím nástrojem, aby se jakýkoli nový sken přetáhlý do složky automaticky stal prohledávatelným. Nebo experimentujte s různými jazyky OCR pro podporu vícejazykových archivů. Možnosti jsou neomezené, když spojíte OCR s generováním PDF.

Máte další otázky ohledně **how to run OCR** v jiných jazycích nebo rámcích? Zanechte komentář níže a šťastné programování! 

![Diagram showing the flow from scanned image → OCR engine → searchable PDF (create searchable pdf)](searchable-pdf-flow.png "Create searchable pdf flow diagram")


## Co byste se měli naučit dál?

- [Jak provést OCR PDF v .NET s Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Převod obrázků do PDF C# – Uložení vícestránkového OCR výsledku](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Jak provést OCR textu z obrázku s jazykem pomocí Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}