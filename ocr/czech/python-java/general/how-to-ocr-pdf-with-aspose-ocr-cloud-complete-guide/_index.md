---
category: general
date: 2026-06-06
description: Jak provést OCR PDF pomocí Aspose OCR Cloud. Naučte se extrahovat text
  z PDF, převést stránku PDF na PNG a uložit obrázky stránek PDF v Pythonu.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf page png
- extract plain text pdf
- save pdf page images
language: cs
og_description: Jak provést OCR PDF pomocí Aspose OCR Cloud. Tento průvodce ukazuje,
  jak extrahovat prostý text z PDF, převést stránku PDF na PNG a uložit obrázky stránek
  PDF.
og_title: Jak provést OCR PDF pomocí Aspose OCR Cloud – krok za krokem
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Aspose OCR Cloud. Learn to extract text from PDF,
    convert PDF page PNG, and save PDF page images in Python.
  headline: How to OCR PDF with Aspose OCR Cloud – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Jak provést OCR PDF pomocí Aspose OCR Cloud – Kompletní průvodce
url: /cs/python-java/general/how-to-ocr-pdf-with-aspose-ocr-cloud-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provést OCR PDF pomocí Aspose OCR Cloud – Kompletní průvodce

Už jste se někdy ptali, **jak provést OCR PDF** soubory bez boje s těžkými desktopovými nástroji? Nejste sami – mnoho vývojářů narazí na tuto překážku, když potřebují rychlý, programový způsob, jak získat text ze skenovaných dokumentů. Dobrá zpráva? S Aspose OCR Cloud můžete **extrahovat text z PDF**, převést každou stránku na PNG a dokonce **uložit obrázky stránek PDF** pro pozdější použití, vše z přehledného Python skriptu.

V tomto tutoriálu projdeme vše, co potřebujete vědět: od instalace SDK, licencování enginu a rozpoznávání vícestránkových PDF, po extrahování prostého textu, převod stránek na PNG a ukládání těchto obrázků na disk. Na konci budete mít znovupoužitelný úryvek, který můžete vložit do jakéhokoli projektu, který potřebuje funkce **jak provést OCR PDF**.

## Co budete potřebovat

- **Python 3.8+** (kód funguje také na 3.10 a novějších)  
- Účet Aspose OCR Cloud – získáte soubor s licencí pro zkušební verzi (`Aspose.OCR.lic`)  
- Balíček `asposeocrcloud` (`pip install asposeocrcloud`)  
- Naskenovaný, vícestránkový PDF, který chcete zpracovat  

To je vše. Žádné další binární soubory, žádné nativní závislosti, jen čistý Python.

## Jak provést OCR PDF – Nastavení a licence

Než můžete volat jakékoli OCR metody, musíte SDK říct, kdo jste. Aspose používá lehký licenční soubor, který umístíte na místo přístupné vašemu skriptu.

```python
# Step 1: Import the OCR package and apply your license (optional but recommended)
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply the license – replace the path with your actual .lic file location
License().set_license("Aspose.OCR.lic")
```

*Tip:* Pokud krok s licencí přeskočíte, SDK bude i nadále fungovat, ale do výstupních obrázků vloží malou vodoznak. Není to ideální pro produkci.

## Krok 2: Instalace Aspose OCR Cloud Python SDK

Otevřete terminál a spusťte:

```bash
pip install asposeocrcloud
```

Balíček stáhne všechny potřebné závislosti (requests, pillow, atd.), takže nemusíte hledat nic dalšího.

## Krok 3: Vytvoření OCR enginu a výběr jazyka

Engine je srdcem operace. Můžete specifikovat libovolný jazyk podporovaný Aspose; angličtina funguje ve většině případů.

```python
# Step 3: Create an OCR engine and set the recognition language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)
```

Proč nastavit jazyk? Protože OCR engine používá jazykově specifické slovníky ke zlepšení přesnosti. Pokud zpracováváte francouzské PDF, stačí vyměnit `ENGLISH` za `FRENCH`.

## Krok 4: Odkaz na váš vícestránkový PDF

Poskytněte engine úplnou cestu k souboru, který chcete zpracovat. Relativní cesty jsou v pořádku, pokud jsou vyhodnoceny z pracovního adresáře skriptu.

```python
# Step 4: Specify the path to the multi‑page PDF you want to process
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"
```

Ujistěte se, že soubor je čitelný; jinak uvidíte `FileNotFoundError`.

## Krok 5: Spuštění OCR – Získáte seznam výsledků

Volání `recognize_pdf` vrací seznam, kde každý prvek odpovídá jedné stránce zdrojového PDF.

```python
# Step 5: Run OCR on the PDF – a list of OcrResult objects is returned (one per page)
results = engine.recognize_pdf(pdf_path)
```

Každý `OcrResult` obsahuje dvě užitečné vlastnosti:

* `text` – prostý textový výstup stránky (skvělé pro **extrahovat prostý text pdf**)
* `image` – objekt Pillow `Image` vykreslené stránky (ideální pro **převést pdf stránku png**)

## Krok 6: Extrahování textu z PDF a převod stránek na PNG

Nyní projdeme výsledky, vytiskneme extrahovaný text a uložíme PNG verzi každé stránky.

```python
# Step 6: Iterate through each page, output the extracted text and optionally save the page image
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    # Extract plain text for this page
    print(res.text)                     # <-- this is the "extract plain text pdf" part
    # Convert the page to PNG and save it
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # <-- this does the "convert pdf page png"
```

### Očekávaný výstup v konzoli

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Také najdete `page_1.png`, `page_2.png`, … v adresáři `YOUR_DIRECTORY`. Jedná se o rasterizované obrázky stránek, které můžete použít v následných pipelinech pro zpracování obrazu.

## Krok 7: Uložení obrázků stránek PDF (volitelné zpracování po dokončení)

Pokud potřebujete jen obrázky a ne text, můžete přeskočit řádek `print(res.text)`. Naopak, pokud chcete uložit text do samostatných souborů `.txt`, stačí přidat malý zápis:

```python
# Optional: Save each page's text to a .txt file
for i, res in enumerate(results, start=1):
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)
```

Toto malé doplnění ukazuje, jak snadné je **uložit obrázky stránek PDF** a zároveň zachovat extrahovaný obsah.

## Kompletní funkční příklad

Spojením všeho dohromady, zde je kompletní skript, který můžete zkopírovat a vložit do `ocr_pdf.py`:

```python
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply your license – optional but removes watermarks
License().set_license("Aspose.OCR.lic")

# Initialize the OCR engine and set language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)

# Path to the source PDF
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"

# Run OCR – get a list of results (one per page)
results = engine.recognize_pdf(pdf_path)

# Process each page
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(res.text)  # extract plain text PDF
    # Save the rendered page as PNG
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # convert PDF page PNG
    # Optional: also save the text to a .txt file
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)  # save PDF page images + text
```

Spusťte jej pomocí:

```bash
python ocr_pdf.py
```

Měli byste vidět výpis v konzoli textu každé stránky a sérii PNG souborů


## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak provést OCR PDF v .NET s Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Rozpoznat text PDF – OCR operace s Aspose.OCR pro Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Převést obrázky na PDF C# – Uložit vícestránkový OCR výsledek](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}