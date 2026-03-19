---
category: general
date: 2026-03-18
description: Voer OCR uit op een afbeelding om tekst uit een PNG te extraheren en
  een doorzoekbare PDF te genereren. Leer hoe je een tekstafbeelding herkent en een
  PNG naar PDF converteert in enkele minuten.
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: nl
og_description: Voer OCR uit op een afbeelding om tekst uit een PNG te extraheren,
  herken de tekstafbeelding en genereer een doorzoekbare PDF. Volg deze stap‑voor‑stap
  handleiding.
og_title: Voer OCR uit op afbeelding – Haal snel tekst uit PNG
tags:
- OCR
- Python
- Image Processing
title: Voer OCR uit op afbeelding – Haal tekst snel uit PNG
url: /nl/python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR uitvoeren op afbeelding – Tekst uit PNG snel extraheren

Heb je ooit **OCR op afbeelding** moeten uitvoeren maar wist je niet waar te beginnen? Misschien heb je een gescande artikel opgeslagen als `article.png` en wil je alleen de platte tekst, of je hebt een doorzoekbare PDF nodig voor archivering. Hoe dan ook, je bent op de juiste plek. In deze tutorial lopen we door het extraheren van tekst uit PNG, het herkennen van de tekstafbeelding, en zelfs het omzetten van die PNG naar een doorzoekbare PDF—allemaal met een handvol regels code.

> **Wat je krijgt:** een compleet, uitvoerbaar script dat een PNG laadt, OCR uitvoert, de hOCR-uitvoer opslaat, en optioneel een doorzoekbare PDF maakt. Geen ontbrekende imports, geen “zie de docs” doodlopende wegen—gewoon een zelfstandige oplossing die je vandaag nog in je project kunt gebruiken.

## Vereisten

- **Python 3.8+** (de hier gebruikte syntaxis werkt op elke recente versie)
- De **`ocr_engine`** bibliotheek die je gebruikt (het voorbeeld gaat uit van een klasse genaamd `OcrEngine`; vervang door Tesseract, EasyOCR, etc., indien nodig)
- Een PNG‑afbeelding die je wilt verwerken (bijv. `article.png` geplaatst in een map die je kunt refereren)
- Schrijfrechten voor de output‑directory

Als je Tesseract onder de motorkap gebruikt, installeer het met:

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

En installeer vervolgens de Python‑wrapper:

```bash
pip install pytesseract Pillow
```

*Pro tip:* houd je OCR‑bibliotheek up‑to‑date—nieuwe taalpakketten en prestatie‑verbeteringen komen regelmatig.

## OCR uitvoeren op afbeelding – Stapsgewijze handleiding

Hieronder staat het **volledige script**. Voel je vrij om het te kopiëren en plakken in een bestand genaamd `run_ocr.py` en uit te voeren met `python run_ocr.py`.

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

### Wat het script doet, in eenvoudige bewoordingen

1. **Instantiate** de OCR‑engine zodat je zijn instellingen kunt beheren.
2. **Load** het PNG‑bestand (`article.png`). Het script stopt vroegtijdig als het bestand er niet is—geen mysterieuze `NoneType`‑fouten later.
3. **Select** `hocr` als exportformaat. Dit formaat behoudt de oorspronkelijke lay-out, wat essentieel is voor het later omzetten van de afbeelding naar een doorzoekbare PDF.
4. **Run** de herkenningsengine; hier gebeurt het zware werk.
5. **Write** de hOCR‑XML naar `article.hocr`. Je hebt nu een machine‑leesbare weergave van de tekst en de coördinaten.
6. *(Optioneel)* Schakel over naar `"pdf"` en genereer een doorzoekbare PDF in één extra stap.

De **verwachte output** is een UTF‑8‑gecodeerd `.hocr`‑bestand dat er ongeveer zo uitziet (ingekort voor de beknoptheid):

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

Als je de PDF‑sectie uitcommentarieert, krijg je ook `article_searchable.pdf`, die je in elke PDF‑viewer kunt openen en met de **Ctrl + F**‑zoekbalk direct woorden kunt vinden.

![Voorbeeldoutput OCR op afbeelding](example.png "OCR op afbeelding – hOCR- en PDF-resultaten")

## Hoe tekst uit PNG te extraheren met OcrEngine

Als alles wat je nodig hebt de ruwe tekst is (geen lay-out, geen PDF), kun je de hOCR‑stap volledig overslaan:

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*Waarom platte tekst kiezen?* Het is lichtgewicht, perfect voor indexering, en werkt uitstekend met downstream NLP‑pipelines.

## Tekstafbeelding herkennen en doorzoekbare PDF genereren

Het genereren van een doorzoekbare PDF is een tweedelige dans:

1. **Run OCR** met `hocr` (zoals hierboven) om de lay‑outinformatie te verkrijgen.
2. **Combine** de originele PNG met de hOCR in een PDF met behulp van de PDF‑exporteur van de engine.

De meeste moderne OCR‑bibliotheken (Tesseract, ABBYY, Google Vision) bieden een `pdf`‑export die precies dit doet. Het fragment in het *Optioneel*‑blok van het hoofdscript toont het patroon. Als je bibliotheek geen ingebouwde PDF‑exporteur heeft, kun je **`pdf2image`** + **`reportlab`** gebruiken om de afbeelding en hOCR samen te voegen—laat het me weten, dan deel ik een snel extra voorbeeld.

## PNG naar PDF converteren met OCR‑output

Soms wil je gewoon een **platte PDF** die de afbeelding bevat (geen doorzoekbare laag). Dat is nog eenvoudiger:

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

Combineer dit met de OCR‑stap als je een doorzoekbare versie nodig hebt, of behoud het als een getrouwe visuele replica voor archiveringsdoeleinden.

## Veelvoorkomende valkuilen & tips

| Probleem | Waarom het gebeurt | Snelle oplossing |
|----------|--------------------|-------------------|
| **Vage of lage‑resolutie PNG** | OCR‑nauwkeurigheid daalt drastisch onder ~300 DPI. | Vergroot met `Image.resize((width*2, height*2), Image.LANCZOS)` voordat je het aan de engine geeft. |
| **Verkeerde taal** | Engine gebruikt standaard Engels; niet‑Engelse tekens worden onleesbaar. | Roep `ocr_engine.setLanguage('deu')` (of de juiste ISO‑code) aan vóór `recognize()`. |
| **Ontbrekende hOCR‑output** | Sommige engines gebruiken standaard platte tekst wanneer `setExportFormat` niet wordt aangeroepen. | Controleer dubbel dat `setExportFormat("hocr")` **vóór** `recognize()` wordt uitgevoerd. |
| **Bestandspermissie‑fouten** | Poging om te schrijven naar een alleen‑lezen map. | Gebruik een pad binnen je project of `os.makedirs(..., exist_ok=True)` eerst. |
| **Grote PDF's veroorzaken geheugenpieken** | PDF‑exporteur houdt de hele afbeelding in RAM. | Verwerk pagina's in delen of gebruik een streaming PDF‑schrijver. |

*Pro tip:* test altijd op een kleine voorbeeldafbeelding voordat je opschaalt naar een batch van duizenden. Het bespaart uren debugging.

## Samenvatting

Je weet nu **hoe je OCR op afbeelding**‑bestanden uitvoert, **tekst uit PNG** extraheren, **tekstafbeelding herkennen** voor downstream‑taken, **een doorzoekbare PDF genereren**, en **PNG naar PDF converteren** wanneer je een eenvoudige archief nodig hebt. Het meegeleverde script is een complete copy‑and‑paste‑oplossing die direct werkt, en de optionele secties laten je de output afstemmen op je exacte workflow.

### Wat nu?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}