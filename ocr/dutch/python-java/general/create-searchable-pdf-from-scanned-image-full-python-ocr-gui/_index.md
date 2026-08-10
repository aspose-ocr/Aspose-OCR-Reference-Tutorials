---
category: general
date: 2026-07-05
description: Maak een doorzoekbare PDF met Python. Leer hoe je een gescande PNG kunt
  OCR’en, een gescande afbeelding‑PDF kunt converteren en binnen enkele minuten een
  doorzoekbare PDF krijgt.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: nl
og_description: Maak snel doorzoekbare PDF's. Deze gids laat zien hoe je een PNG OCR't,
  een gescande afbeeldings‑PDF converteert en een doorzoekbare PDF maakt met Python.
og_title: Maak doorzoekbare PDF van gescande afbeelding – Python OCR‑tutorial
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
title: Maak doorzoekbare PDF van gescande afbeelding – Volledige Python OCR-gids
url: /nl/python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak doorzoekbare PDF van gescande afbeelding – Volledige Python OCR‑gids

Heb je je ooit afgevraagd hoe je **doorzoekbare PDF** kunt maken van een gescande foto zonder dure software te betalen? Je bent niet de enige. In veel kantoren komen PDF’s binnen als platte afbeeldingen—moeilijk doorzoekbaar, onmogelijk te kopiëren‑plakken, en een nachtmerrie voor compliance‑audits. Het goede nieuws? Met een paar regels Python kun je die statische PNG omzetten in een volledig doorzoekbare PDF, en het proces is makkelijker dan je misschien denkt.

In deze tutorial lopen we een compleet **OCR‑herkenningsvoorbeeld** door, van het installeren van de juiste bibliotheek tot het schrijven van het uiteindelijke PDF‑bestand. Aan het einde weet je precies hoe je **gescande afbeelding‑PDF**‑bestanden kunt **converteren**, hoe je **ocr pdf** programmatically kunt uitvoeren, en heb je een herbruikbaar script dat je in elk project kunt gebruiken.

## Wat je zult leren

- Installeer en configureer een Python‑OCR‑bibliotheek (we gebruiken `pytesseract` en `pdf2image`).
- Initialiseert de OCR‑engine en stel de taal in.
- Laad een gescande PNG (of een andere afbeelding) en voer OCR uit.
- Converteer het OCR‑resultaat naar een **doorzoekbare PDF** (byte‑array) en sla deze op.
- Tips voor het verwerken van meer‑pagina‑documenten, verschillende talen en veelvoorkomende valkuilen.

Geen voorafgaande ervaring met OCR vereist—alleen een werkende Python 3‑omgeving en een beetje nieuwsgierigheid.

---

## Doorzoekbare PDF maken – Overzicht

Hieronder staat een high‑level stroomdiagram van de stappen die we gaan implementeren.  

![Maak doorzoekbare PDF workflow diagram](https://example.com/flowchart.png "Maak doorzoekbare PDF workflow diagram")

*Alt‑tekst: Maak doorzoekbare PDF workflow diagram dat engine‑initialisatie, afbeelding‑laden, OCR‑herkenning, PDF‑conversie en bestands‑schrijven toont.*

---

## Stap 1: Initialiseert de OCR‑engine (how to ocr pdf)

Waarom moeten we überhaupt iets initialiseren? De OCR‑engine is het brein dat pixelpatronen interpreteert als tekens. Door een engine‑instantie te maken en expliciet de taal in te stellen, vertellen we de bibliotheek welk alfabet verwacht moet worden, wat de nauwkeurigheid drastisch verbetert.

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

**Pro‑tip:** Als je documenten in meerdere talen moet OCR‑en, installeer dan de bijbehorende taalpakketten voor Tesseract en geef een lijst door zoals `"eng+spa"` aan `ocr_language`.

---

## Stap 2: Laad de gescande afbeelding (convert scanned image pdf)

Het volgende puzzelstukje is het inladen van de afbeeldingsdata in Python. Of je nu een enkele PNG of een multi‑page TIFF hebt, de `PIL.Image`‑klasse kan deze openen. Als je start vanuit een PDF die al gescande afbeeldingen bevat, zal `pdf2image` elke pagina naar een afbeelding converteren.

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**Waarom dit belangrijk is:** Het laden van de afbeelding als een Pillow‑object geeft ons toegang tot de ruwe pixeldata, die de OCR‑engine nodig heeft. Deze stap overslaan en ruwe bytes direct doorgeven leidt tot fouten.

---

## Stap 3: Voer OCR‑herkenning uit op de afbeelding (ocr recognition example)

Nu het leuke deel—de engine de tekst laten lezen. `pytesseract.image_to_pdf_or_hocr` retourneert een PDF‑byte‑stream die al een onzichtbare tekstlaag bevat, precies wat we nodig hebben voor een **doorzoekbare PDF**.

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**Randgeval:** Als je afbeelding weinig contrast heeft, overweeg dan een eenvoudige drempel toe te passen vóór OCR:

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

Deze kleine voorverwerking kan de nauwkeurigheid dramatisch verhogen.

---

## Stap 4: Schrijf de PDF‑bytes naar een bestand (convert png searchable pdf)

De OCR‑bibliotheek geeft ons een byte‑array—denk aan de ruwe inhoud van een PDF‑bestand. Alles wat we nu hoeven te doen is die bytes naar schijf schrijven.

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**Wat je zult zien:** Open het resulterende bestand in een PDF‑viewer en zoek naar een woord waarvan je weet dat het in de originele afbeelding staat. Het resultaat moet direct naar de juiste locatie springen, wat bewijst dat de onzichtbare tekstlaag werkt.

---

## Stap 5: Uitbreiden naar meer‑pagina‑documenten (convert scanned image pdf)

Werkelijke contracten beslaan vaak meerdere pagina’s. Om **gescande afbeelding‑pdf**‑bestanden met meerdere pagina’s te **converteren**, loop je door elke pagina, OCR‑t deze en concateneert de resulterende PDF’s.

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

**Waarom samenvoegen?** Elke aanroep van `image_to_pdf_or_hocr` produceert een zelfstandige PDF. Door ze te mergen behoudt het einddocument de oorspronkelijke paginavolgorde.

---

## Veelvoorkomende valkuilen & hoe ze op te lossen

| Symptoom | Waarschijnlijke oorzaak | Oplossing |
|----------|--------------------------|-----------|
| Geen doorzoekbare tekst na het openen van de PDF | Tesseract vindt geen tekens (lege output) | Controleer de beeldkwaliteit, verhoog DPI, of pas voorverwerking toe (contrast, binarisatie). |
| Vervormde tekens (bijv. �) | Verkeerd taalpakket of ontbrekende lettertypen | Installeer de juiste taaldataset (`tesseract‑lang‑eng`) en zorg dat `ocr_language` overeenkomt. |
| PDF‑bestand is enorm (>10 MB voor één pagina) | Gebruik van lossless PNG als bron; OCR voegt een full‑resolution afbeelding toe | Schaal de afbeelding naar beneden vóór OCR (`image.thumbnail((1240, 1754))` voor A4). |
| Script crasht op Windows met “tesseract.exe not found” | Tesseract‑binary niet in PATH | Voeg `pytesseract.pytesseract.tesseract_cmd = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"` toe (pad aanpassen). |

---

## Volledig, kant‑klaar script

Alles samengevoegd, hier is één bestand dat je kunt kopiëren‑plakken en uitvoeren:

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

Sla dit op als `create_searchable_pdf.py`, vervang de placeholders door echte paden, en voer uit:

```bash
python create_searchable_pdf.py
```

Je zou een

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementaties in je eigen projecten te verkennen.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}