---
category: general
date: 2026-06-22
description: Naučte se, jak provádět OCR PDF souborů v Pythonu, extrahovat text z
  PDF a převádět PDF na text pomocí streamového přístupu. Jednoduché kroky pro zpracování
  naskenovaných PDF.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- load pdf from stream
- process scanned pdf
language: cs
og_description: Jak provést OCR PDF souborů v Pythonu? Postupujte podle tohoto návodu,
  abyste extrahovali text z PDF, převedli PDF na text a zpracovali naskenované PDF
  pomocí streamu.
og_title: Jak provést OCR PDF v Pythonu – krok za krokem průvodce
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  headline: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  type: TechArticle
- description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  name: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  steps:
  - name: Expected Output
    text: 'If `multipage.pdf` contains three scanned pages, you’ll see something like:'
  - name: 1. PDFs with Mixed Image and Text Layers
    text: 'Some PDFs already contain a hidden text layer (e.g., exported from Word).
      If you want the OCR engine to **ignore existing text** and re‑process the image,
      set:'
  - name: 2. Large Files Exceeding Memory Limits
    text: 'When working with gigabyte‑size PDFs, consider processing in chunks:'
  - name: 3. Language and Font Support
    text: 'If your scanned documents are in French or contain special characters,
      tell the engine which language model to use:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Jak provést OCR PDF v Pythonu – Kompletní průvodce extrakcí textu z PDF
url: /cs/python-java/general/how-to-ocr-pdf-in-python-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provést OCR PDF v Pythonu – Kompletní průvodce extrakcí textu z PDF

Už jste se někdy zamýšleli, **jak provést OCR PDF** soubory, aniž byste se potýkali s těžkopádnými desktopovými nástroji? Nejste v tom sami. V mnoha reálných projektech—například automatizace faktur nebo digitalizace archivních skenů—potřebujete spolehlivý způsob, jak převést naskenovaný PDF do prohledávatelného, editovatelného textu.

V tomto tutoriálu projdeme čistým, end‑to‑end příkladem, který **extrahuje text z PDF** stránek pomocí lehkého Python OCR enginu. Na konci přesně vědět, jak **převést PDF na text**, jak **načíst PDF ze streamu** a jak **zpracovat naskenovaný PDF** efektivně. Žádná magie, jen obyčejný Python kód, který můžete dnes vložit do svého projektu.

## Co se naučíte

- Nainstalovat a nakonfigurovat Python OCR knihovnu, která rozumí PDF vstupu.  
- Povolit režim rozpoznávání PDF a nastavit výstupní formát na prostý text.  
- Načíst více‑stránkový PDF ze souborového streamu (klasický vzor “load pdf from stream”).  
- Spustit OCR na všech stránkách a získat textový obsah.  
- Vytisknout nebo uložit výsledky pro následné zpracování.

**Požadavky**  
- Python 3.8+ nainstalovaný na vašem počítači.  
- Základní znalost pip a virtuálních prostředí.  
- Naskenovaný PDF soubor (nazvaný `multipage.pdf` v příkladu) umístěný v známém adresáři.

Pokud vám některý z nich není známý, nebojte se—každý krok je vysvětlen jednoduchým jazykem a poskytneme vám přesné příkazy, které potřebujete.

---

## Krok 1: Instalace OCR enginu (how to OCR PDF)

Nejprve—potřebujete OCR engine, který dokáže zpracovat PDF vstup. Pro tento návod použijeme hypotetický balíček `ocr` (API odráží populární komerční SDK, ale stejný vzor funguje s Tesseract‑OCR, ABBYY nebo Google Vision, pokud jsou správně zabaleny).

```bash
# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Tip:** Pokud používáte Windows a narazíte na chyby oprávnění, zkuste místo toho `pip install --user ocr`.

Jakmile je balíček nainstalován, můžete jej importovat ve svém skriptu a vytvořit instanci enginu—toto je jádro **how to OCR PDF**.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

Objekt `OcrEngine` obsahuje všechna nastavení, která později upravíme, jako jazyk, DPI a—co je klíčové—režim PDF.

## Krok 2: Povolení rozpoznávání PDF a výběr výstupu (extract text from PDF)

Ve výchozím nastavení mnoho OCR SDK předpokládá, že jim předáváte obrázky. Aby engine považoval příchozí stream za PDF, povolíme příznak rozpoznávání PDF a požádáme o výstup v prostém textu.

```python
# Step 2: Turn on PDF mode and request plain text results
settings = engine.get_settings()
settings.set_recognize_pdf(True)                     # tells the engine to parse PDF containers
settings.set_output_format(ocr.OutputFormat.TEXT)   # we want raw text, not XML or PDF
```

Proč se obtěžovat specifikací výstupního formátu? Protože některé enginy mohou vracet PDF s skrytými textovými vrstvami, prohledávatelné PDF nebo JSON s ohraničujícími boxy. Pro většinu datových extrakčních pipeline je **extract text from PDF** jako prosté řetězce nejčistší následný formát.

## Krok 3: Načtení PDF ze souborového streamu (load PDF from stream)

Načítání PDF ze streamu je paměťově úsporný vzor—vyhnete se načtení celého souboru do RAM najednou. To je zvláště užitečné při práci s velkými více‑stránkovými dokumenty.

```python
# Step 3: Load the multi‑page PDF from a file stream
pdf_path = "YOUR_DIRECTORY/multipage.pdf"
pdf_stream = ocr.ImageStream.from_file(pdf_path)   # wraps the file handle in an OCR‑friendly object
engine.set_image(pdf_stream)
```

> **Co když je soubor na S3 nebo jiném cloudovém bucketu?**  
> Jednoduše nahraďte `from_file` metodou, která přijímá byte buffer (např. `ImageStream.from_bytes(s3_object.read())`). Zbytek pipeline zůstane stejný.

## Krok 4: Spuštění OCR na všech stránkách (process scanned PDF)

Nyní začíná těžká část. Engine projde každou stránku, spustí rozpoznávací engine a vrátí seznam objektů stránek—každý z nich poskytuje svůj textový obsah.

```python
# Step 4: Perform OCR on all pages of the PDF
pages = engine.recognize_pdf()
```

V pozadí OCR knihovna dekomprimuje každou PDF stránku, rasterizuje ji s nastaveným DPI a předá bitmapu svému neuronovému modelu. Výsledek? Kolekce objektů `Page` připravených k extrakci.

## Krok 5: Získání a zobrazení rozpoznaného textu (convert PDF to text)

Nakonec projdeme vrácené stránky a vytiskneme rozpoznaný text. To je okamžik, kdy **convert PDF to text** skutečně nastává.

```python
# Step 5: Iterate through the recognized pages and display their text
for index, page in enumerate(pages):
    print(f"--- Page {index + 1} ---")
    print(page.get_text())
```

### Očekávaný výstup

Pokud `multipage.pdf` obsahuje tři naskenované stránky, uvidíte něco jako:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

--- Page 2 ---
Item Description   Qty   Price
Widget A           10    $50.00
Widget B            5    $30.00
...

--- Page 3 ---
Thank you for your business!
```

Všimněte si čistého oddělení mezi stránkami—užitečné, pokud potřebujete uložit text každé stránky do databáze nebo jej předat následnému NLP modelu.

## Řešení běžných okrajových případů

### 1. PDF s kombinovanými obrazovými a textovými vrstvami
Některé PDF již obsahují skrytou textovou vrstvu (např. exportované z Wordu). Pokud chcete, aby OCR engine **ignoroval existující text** a znovu zpracoval obrázek, nastavte:

```python
settings.set_force_ocr(True)   # forces rasterization and OCR even if text exists
```

### 2. Velké soubory překračující limity paměti
Při práci s PDF o velikosti gigabajtů zvažte zpracování po částech:

```python
for page_number in range(1, engine.get_page_count() + 1):
    single_page_stream = engine.get_page_stream(page_number)
    engine.set_image(single_page_stream)
    page = engine.recognize_pdf()[0]   # only one page at a time
    print(f"--- Page {page_number} ---")
    print(page.get_text())
```

### 3. Podpora jazyků a fontů
Pokud jsou vaše naskenované dokumenty ve francouzštině nebo obsahují speciální znaky, řekněte engine, který jazykový model použít:

```python
settings.set_language("fr")   # or "en", "de", etc.
```

## Kompletní skript – připravený ke spuštění

Níže je kompletní, spustitelný příklad, který spojuje všechny části dohromady. Uložte jej jako `ocr_pdf.py` a spusťte `python ocr_pdf.py`.

```python
import ocr

def main():
    # Initialize engine
    engine = ocr.OcrEngine()

    # Configure for PDF recognition and plain‑text output
    settings = engine.get_settings()
    settings.set_recognize_pdf(True)
    settings.set_output_format(ocr.OutputFormat.TEXT)

    # Optional: force OCR even if PDF already has text
    # settings.set_force_ocr(True)

    # Load PDF from a stream
    pdf_path = "YOUR_DIRECTORY/multipage.pdf"
    pdf_stream = ocr.ImageStream.from_file(pdf_path)
    engine.set_image(pdf_stream)

    # Perform OCR on every page
    pages = engine.recognize_pdf()

    # Output the results
    for idx, page in enumerate(pages):
        print(f"--- Page {idx + 1} ---")
        print(page.get_text())

if __name__ == "__main__":
    main()
```

**Spuštění skriptu** vytiskne text každé stránky do konzole, přesně tak, jak je uvedeno v sekci “Expected Output”. Odtud můžete výstup přesměrovat do souboru:

```bash
python ocr_pdf.py > extracted_text.txt
```

## Závěr

Právě jsme prošli **how to OCR PDF** soubory v Pythonu od začátku do konce. Nakonfigurováním enginu, načtením dokumentu přes stream a iterací přes každou rozpoznanou stránku můžete **extract text from PDF**, **convert PDF to text** a **process scanned PDF** pomocí jen několika řádků. Přístup škáluje od malých dvoustránkových faktur po obrovské archivní soubory se stovkami stránek.

Co dál? Zkuste předat extrahované řetězce do vyhledávacího indexu, sumarizátoru jazykového modelu nebo datové validační pipeline. Můžete také experimentovat s výstupními formáty jako JSON, abyste zachovali poziční metadata pro pokročilou analýzu dokumentů.

Máte otázky ohledně zpracování šifrovaných PDF nebo integrace s cloudovým úložištěm? Zanechte komentář níže—šťastné kódování! 

![Diagram ukazující workflow OCR PDF – how to OCR PDF, load PDF from stream, recognize pages, and extract text](ocr-pdf-workflow.png "diagram workflow OCR PDF")


## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak provést OCR PDF v .NET s Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Jak extrahovat text z obrázku pomocí Aspose.OCR pro .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Jak extrahovat text ze ZIP archivů pomocí Aspose.OCR pro .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}