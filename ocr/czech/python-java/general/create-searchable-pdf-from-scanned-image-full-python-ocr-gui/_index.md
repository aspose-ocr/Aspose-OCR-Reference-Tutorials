---
category: general
date: 2026-07-05
description: Vytvořte prohledávatelný PDF pomocí Pythonu. Naučte se, jak provést OCR
  naskenovaného PNG, převést naskenovaný obrázkový PDF a během několika minut získat
  prohledávatelný PDF.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: cs
og_description: Rychle vytvořte prohledávatelný PDF. Tento průvodce ukazuje, jak provést
  OCR PNG, převést naskenovaný PDF obrázek a vytvořit prohledávatelný PDF pomocí Pythonu.
og_title: Vytvořte prohledávatelný PDF ze skenovaného obrázku – Python OCR tutoriál
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF with Python. Learn how to OCR a scanned PNG,
    convert scanned image PDF, and get a searchable PDF in minutes.
  headline: Create Searchable PDF from Scanned Image – Full Python OCR Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF
- Automation
title: Vytvořte prohledávatelný PDF ze skenovaného obrázku – Kompletní průvodce OCR
  v Pythonu
url: /cs/python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF ze skenovaného obrázku – Kompletní průvodce OCR v Pythonu

Už jste se někdy zamysleli, jak **vytvořit prohledávatelné PDF** ze skenovaného obrázku, aniž byste museli platit za drahý software? Nejste v tom sami. V mnoha kancelářích přicházejí PDF jako ploché obrázky – těžko prohledatelné, nemožné kopírovat‑vkládat a noční můra při auditech shody. Dobrá zpráva? Několika řádky Pythonu můžete převést tento statický PNG na plně prohledávatelné PDF a proces je snadnější, než si myslíte.

V tomto tutoriálu projdeme kompletním **příkladem rozpoznávání OCR**, který zahrnuje vše od instalace správné knihovny po zápis finálního PDF souboru. Na konci budete přesně vědět, jak **převést skenované PDF obrázky**, jak **programově ocr pdf**, a budete mít znovupoužitelný skript, který můžete vložit do jakéhokoli projektu.

## Co se naučíte

- Nainstalovat a nakonfigurovat Python OCR knihovnu (použijeme `pytesseract` a `pdf2image`).
- Inicializovat OCR engine a nastavit jazyk.
- Načíst skenovaný PNG (nebo jakýkoli obrázek) a spustit na něm OCR.
- Převést výsledek OCR na **prohledávatelné PDF** (byte array) a uložit jej.
- Tipy pro práci s více‑stránkovými dokumenty, různými jazyky a běžnými úskalími.

Předchozí zkušenost s OCR není vyžadována – stačí funkční prostředí Python 3 a trochu zvědavosti.

## Vytvoření prohledávatelného PDF – Přehled

Below is a high‑level flowchart of the steps we’ll implement.  

![Diagram pracovního postupu pro vytvoření prohledávatelného PDF](https://example.com/flowchart.png "Diagram pracovního postupu pro vytvoření prohledávatelného PDF")

*Alt text: Diagram pracovního postupu pro vytvoření prohledávatelného PDF ukazující inicializaci engine, načtení obrázku, rozpoznání OCR, konverzi do PDF a zápis souboru.*

## Krok 1: Inicializace OCR engine (how to ocr pdf)

Proč vůbec potřebujeme něco inicializovat? OCR engine je mozek, který interpretuje pixelové vzory jako znaky. Vytvořením instance engine a explicitním nastavením jazyka říkáme knihovně, jakou abecedu má očekávat, což dramaticky zvyšuje přesnost.

```python
import pytesseract
from pdf2image import convert_from_path
from PIL import Image
import io

# Ensure Tesseract is on your PATH or provide the executable location
pytesseract.pytesseract.tesseract_cmd = r"/usr/local/bin/tesseract"  # adjust as needed

# Define the language – ENGLISH is the default, but you can add more (e.g., 'fra' for French)
ocr_language = "eng"
```

**Pro tip:** Pokud potřebujete OCR dokumenty ve více jazycích, nainstalujte odpovídající jazykové balíčky pro Tesseract a předávejte seznam jako `"eng+spa"` do `ocr_language`.

## Krok 2: Načtení skenovaného obrázku (convert scanned image pdf)

Dalším dílem skládačky je získání obrazových dat do Pythonu. Ať už máte jediný PNG nebo více‑stránkový TIFF, třída `PIL.Image` jej dokáže otevřít. Pokud začínáte z PDF, které již obsahuje skenované obrázky, `pdf2image` převede každou stránku na obrázek pro nás.

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**Proč je to důležité:** Načtení obrázku jako objektu Pillow nám poskytuje přístup k jeho surovým pixelovým datům, která OCR engine potřebuje. Přeskočení tohoto kroku a předání surových bajtů přímo by způsobilo chyby.

## Krok 3: Provedení OCR rozpoznání na obrázku (ocr recognition example)

Nyní ta zábavná část – nechat engine přečíst text. `pytesseract.image_to_pdf_or_hocr` vrací PDF byte stream, který již obsahuje neviditelnou textovou vrstvu, což je přesně to, co potřebujeme pro **prohledávatelné PDF**.

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**Hraniční případ:** Pokud je váš obrázek nízkokontrastní, zvažte aplikaci jednoduchého prahu před OCR:

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

Tento malý krok předzpracování může dramaticky zvýšit přesnost.

## Krok 4: Zapsání PDF bajtů do souboru (convert png searchable pdf)

OCR knihovna nám předá byte array – představte si to jako surový obsah PDF souboru. Vše, co nyní musíme udělat, je zapsat tyto bajty na disk.

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**Co uvidíte:** Otevřete výsledný soubor v libovolném PDF prohlížeči a zkuste vyhledat slovo, o kterém víte, že se v originálním obrázku vyskytuje. Zvýraznění by mělo skočit přímo na místo, což dokazuje, že neviditelná textová vrstva funguje.

## Krok 5: Rozšíření na více‑stránkové dokumenty (convert scanned image pdf)

Reálné smlouvy často zahrnují více stránek. Pro **convert scanned image pdf** soubory, které obsahují několik stránek, projděte každou stránku, proveďte OCR a spojte výsledné PDF.

```python
def ocr_image_to_pdf(image_obj, lang="eng"):
    """Helper that returns PDF bytes for a single image."""
    return pytesseract.image_to_pdf_or_hocr(image_obj, lang=lang, extension='pdf')

def merge_pdfs(pdf_bytes_list):
    """Combine multiple PDF byte streams into one."""
    from PyPDF2 import PdfMerger
    merger = PdfMerger()
    for i, pdf_bytes in enumerate(pdf_bytes_list):
        merger.append(io.BytesIO(pdf_bytes))
    output = io.BytesIO()
    merger.write(output)
    merger.close()
    return output.getvalue()

# Example: convert a multi‑page scanned PDF to searchable PDF
pages = convert_from_path("YOUR_DIRECTORY/scanned_contract.pdf", dpi=300)
pdf_parts = [ocr_image_to_pdf(p, lang=ocr_language) for p in pages]
final_pdf = merge_pdfs(pdf_parts)

with open("YOUR_DIRECTORY/contract_searchable.pdf", "wb") as f:
    f.write(final_pdf)

print("✅ Multi‑page searchable PDF created.")
```

**Proč sloučit?** Každé volání `image_to_pdf_or_hocr` vytvoří samostatné PDF. Sloučením zajistíte, že finální dokument zachová původní pořadí stránek.

## Běžná úskalí a jak je opravit

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Žádný text není prohledatelný po otevření PDF | Tesseract nenašel žádné znaky (prázdný výstup) | Zkontrolujte kvalitu obrázku, zvyšte DPI nebo aplikujte předzpracování (kontrast, binarizace). |
| poškozené znaky (např. �) | Špatný jazykový balíček nebo chybějící fonty | Nainstalujte správná jazyková data (`tesseract‑lang‑eng`) a ujistěte se, že `ocr_language` odpovídá. |
| Velikost PDF souboru je obrovská (>10 MB pro jednostránkový obrázek) | Použití bezztrátového PNG jako zdroje; OCR přidává obrázek v plném rozlišení | Zmenšete obrázek před OCR (`image.thumbnail((1240, 1754))` pro A4). |
| Skript spadne ve Windows s chybou “tesseract.exe not found” | Binární soubor Tesseract není v PATH | Přidejte `pytesseract.pytesseract.tesseract_cmd = r\"C:\\Program Files\\Tesseract-OCR\\tesseract.exe\"` (upravit cestu). |

## Kompletní, připravený ke spuštění skript

Spojením všeho dohromady, zde je jediný soubor, který můžete zkopírovat a spustit:

```python
#!/usr/bin/env python3
"""
create_searchable_pdf.py
A complete example that converts a scanned PNG (or PDF) into a searchable PDF using Tesseract OCR.
"""

import io
import sys
from pathlib import Path

import pytesseract
from pdf2image import convert_from_path
from PIL import Image
from PyPDF2 import PdfMerger

# -------------------- Configuration --------------------
# Adjust these paths for your environment
TESSERACT_CMD = r"/usr/local/bin/tesseract"   # macOS/Linux
# TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"  # Windows
OCR_LANGUAGE = "eng"                         # Add '+spa' for Spanish, etc.
INPUT_PATH = Path("YOUR_DIRECTORY/scanned_agreement.png")
OUTPUT_PATH = Path("YOUR_DIRECTORY/agreement_searchable.pdf")
# -------------------------------------------------------

# Point pytesseract at the executable
pytesseract.pytesseract.tesseract_cmd = TESSERACT_CMD

def load_image(path: Path) -> Image.Image:
    """Load an image from disk; supports PNG, JPG, TIFF."""
    if not path.is_file():
        sys.exit(f"❌ File not found: {path}")
    return Image.open(path)

def ocr_to_pdf_bytes(img: Image.Image, lang: str = OCR_LANGUAGE) -> bytes:
    """Run OCR on a Pillow image and return PDF bytes with hidden text."""
    return pytesseract.image_to_pdf_or_hocr(img, lang=lang, extension='pdf')

def write_pdf(data: bytes, dest: Path):
    """Write PDF byte stream to a file."""
    dest.parent.mkdir(parents=True, exist_ok=True)
    with open(dest, "wb") as f:
        f.write(data)
    print(f"✅ Searchable PDF saved to {dest}")

def main():
    # Load the scanned image
    image = load_image(INPUT_PATH)

    # Optional: improve contrast for low‑quality scans
    # image = image.convert('L').point(lambda x: 0 if x < 128 else 255, '1')

    # OCR → PDF bytes
    pdf_bytes = ocr_to_pdf_bytes(image)

    # Save the result
    write_pdf(pdf_bytes, OUTPUT_PATH)

if __name__ == "__main__":
    main()
```

Uložte to jako `create_searchable_pdf.py`, nahraďte zástupné symboly skutečnými cestami a spusťte:

```bash
python create_searchable_pdf.py
```

Měli byste vidět

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Jak OCR PDF v .NET s Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Převod obrázků do PDF C# – Uložení více‑stránkového OCR výsledku](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [OCR rozpoznávání PDF dokumentů v Aspose.OCR pro Java](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}