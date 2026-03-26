---
category: general
date: 2026-03-26
description: Hoe PDF-tekst te extraheren met OCR. Leer hoe je een PDF als afbeelding
  laadt, PDF-tekst herkent en tekst uit een PDF extraheert met een eenvoudig Python‑voorbeeld.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize pdf text
- load pdf as image
- how to use OCR
language: nl
og_description: Hoe PDF-tekst te extraheren met OCR. Deze gids laat zien hoe je een
  PDF als afbeelding laadt, PDF-tekst herkent en tekst uit een PDF haalt in Python.
og_title: Hoe PDF-tekst te extraheren met OCR – Volledige tutorial
tags:
- OCR
- Python
- PDF processing
title: Hoe PDF-tekst te extraheren met OCR – Complete stap‑voor‑stap gids
url: /nl/python-java/general/how-to-extract-pdf-text-with-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe PDF‑tekst te extraheren met OCR – Complete stapsgewijze gids

Heb je je ooit afgevraagd **hoe je PDF‑bestanden** kunt extraheren die eigenlijk alleen gescande afbeeldingen zijn? Je bent niet de enige—veel ontwikkelaars lopen tegen dit probleem aan wanneer ze doorzoekbare inhoud nodig hebben maar alleen image‑only PDF’s hebben. Het goede nieuws? Een paar regels code en een degelijke OCR‑bibliotheek kunnen die foto‑PDF’s in een handomdraai omzetten naar platte tekst.  

In deze tutorial lopen we **uit hoe je OCR** gebruikt om een PDF als afbeelding te laden, PDF‑tekst te herkennen, en uiteindelijk **tekst uit PDF**‑documenten van elke lengte te **extraheren**. Aan het einde heb je een uitvoerbaar script, een duidelijke uitleg van elke stap, en een reeks tips om de gebruikelijke valkuilen te vermijden.

## Wat je nodig hebt

- Python 3.9 of nieuwer (de code werkt ook op 3.10+)  
- Het `ocr` Python‑pakket (of een compatibele OCR‑bibliotheek die `OcrEngine`, `OcrEngineMode` en `Imaging.Image` exposeert)  
- Een meer‑pagina‑PDF die je wilt verwerken (voor de demo noemen we het `multi_page.pdf`)  
- Basiskennis van virtuele omgevingen (optioneel maar aanbevolen)

> **Pro tip:** Als je Windows gebruikt, overweeg dan de Anaconda Prompt; op macOS/Linux werkt een eenvoudige `python -m venv venv && source venv/bin/activate` prima.

## Stap 1: Installeer de OCR‑bibliotheek

Eerst haal je het OCR‑pakket op van PyPI. Het voorbeeld hieronder gebruikt een fictief `ocr`‑pakket dat de API uit de code‑snippet nabootst, maar de meeste echte bibliotheken (zoals `pytesseract` + `pdf2image`) volgen hetzelfde patroon.

```bash
pip install ocr
```

Gebruik je een andere engine, vervang dan `ocr` door de juiste naam (bijv. `pip install pytesseract pdf2image`).

## Stap 2: Initialise­er de OCR‑engine

Een engine‑instantie maken is de basis van **hoe je PDF‑tekst kunt extraheren**. Beschouw de engine als het brein dat de pixels binnen elke PDF‑pagina interpreteert.

```python
import ocr

# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Set the engine to the default mode (fast enough for most PDFs)
ocr_engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)
```

> **Waarom dit belangrijk is:** `set_engine_mode` laat je snelheid ruilen voor nauwkeurigheid. `DEFAULT` is een evenwichtige keuze; als je hogere precisie nodig hebt, schakel dan over naar `HIGH_ACCURACY` (indien de bibliotheek dit ondersteunt).

## Stap 3: Laad de PDF als een Image‑object

OCR werkt op afbeeldingen, niet op PDF‑containers, dus we moeten de PDF eerst omzetten naar een afbeelding. De methode `Imaging.Image.load` verwerkt multi‑page PDF’s automatisch.

```python
# Step 3: Load the multi‑page PDF as an image object
pdf_path = "YOUR_DIRECTORY/multi_page.pdf"
pdf_image = ocr.Imaging.Image.load(pdf_path)
```

> **Randgeval:** Sommige bibliotheken accepteren alleen een één‑pagina afbeelding. In dat scenario zou je door elke pagina itereren met `pdf2image.convert_from_path`. Onze `load`‑aanroep abstraheert dat weg, waardoor **load pdf as image** een één‑regelige opdracht wordt.

## Stap 4: Herken tekst op alle pagina’s

Nu volgt de kern van **recognize PDF text**. De engine scant elke pagina en geeft een lijst met result‑objecten terug—één per pagina.

```python
# Step 4: Recognize text on all pages of the PDF
page_results = ocr_engine.recognize_multi_page(pdf_image)
```

Elk `page_result` bevat methoden zoals `get_text()` (platte tekst) en `get_confidence()` (optionele kwaliteitsmeting).  

> **Tip:** Als je alleen de eerste pagina nodig hebt, roep dan `recognize(pdf_image[0])` aan in plaats van de multi‑page helper.

## Stap 5: Iterate door de resultaten en output de geëxtraheerde tekst

Ten slotte lopen we over de resultaten en printen we de tekst van elke pagina. Hiermee is de **extract text from PDF**‑workflow voltooid.

```python
# Step 5: Print extracted text page by page
for index, page_result in enumerate(page_results):
    print(f"--- Page {index + 1} ---")
    print(page_result.get_text())
    # Optional: show confidence score
    # print(f"Confidence: {page_result.get_confidence():.2f}%")
```

### Verwachte output

Als `multi_page.pdf` drie pagina’s bevat met de woorden “Hello”, “World” en “Python”, zie je:

```
--- Page 1 ---
Hello
--- Page 2 ---
World
--- Page 3 ---
Python
```

Dat is alles—je PDF is nu volledig doorzoekbaar en de tekst is klaar voor verdere verwerking (indexering, sentiment‑analyse, wat je maar wilt).

## Stap 6: Veelvoorkomende valkuilen behandelen

| Probleem | Waarom het gebeurt | Snelle oplossing |
|----------|-------------------|------------------|
| **Lege output** | PDF‑pagina’s zijn gescand met lage DPI, waardoor tekens onherkenbaar zijn. | Schaal de afbeelding op vóór OCR: `pdf_image = pdf_image.resize(300)` (300 DPI is een goede balans). |
| **Onzin‑tekens** | Niet‑Latijnse alfabetten hebben taal‑pakketten nodig. | Laad het juiste taalmodel: `ocr_engine.load_language('spa')` voor Spaans, enz. |
| **Geheugen‑explosie bij enorme PDF’s** | Alle pagina’s tegelijk laden verbruikt veel RAM. | Verwerk pagina’s in batches: `for img in pdf_image.split(batch=10): …` (pseudo‑code). |
| **Trage prestaties** | `DEFAULT` gebruiken op een massief document kan traag zijn. | Schakel over naar `FAST`‑modus of voer OCR parallel uit met `concurrent.futures`. |

## Bonus: De geëxtraheerde tekst opslaan in een bestand

De meeste real‑world pipelines hebben de tekst nodig in een bestand. Hier is een kleine helper die alles naar `output.txt` schrijft.

```python
output_path = "YOUR_DIRECTORY/output.txt"

with open(output_path, "w", encoding="utf-8") as f:
    for idx, result in enumerate(page_results):
        f.write(f"--- Page {idx + 1} ---\n")
        f.write(result.get_text() + "\n\n")
print(f"All text saved to {output_path}")
```

Nu kun je `output.txt` voeden aan een zoekmachine, een database, of elk NLP‑model.

## Alles bij elkaar – Volledig script

Hieronder staat het complete, kant‑klaar script. Kopieer‑plak, pas de bestands‑paden aan, en je bent klaar om te gaan.

```python
# -*- coding: utf-8 -*-
"""
How to extract PDF text with OCR – end‑to‑end example.

Prerequisites:
    pip install ocr
"""

import ocr

def extract_text_from_pdf(pdf_path: str):
    """
    Load a PDF, run OCR on every page, and return a list of strings.
    """
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)

    # Load PDF as image (multi‑page support)
    pdf_image = ocr.Imaging.Image.load(pdf_path)

    # Recognize text on all pages
    results = engine.recognize_multi_page(pdf_image)

    # Collect plain text
    texts = [res.get_text() for res in results]
    return texts

def main():
    pdf_file = "YOUR_DIRECTORY/multi_page.pdf"
    texts = extract_text_from_pdf(pdf_file)

    # Print and optionally save
    for i, txt in enumerate(texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()

    # Save to file
    out_path = "YOUR_DIRECTORY/extracted_text.txt"
    with open(out_path, "w", encoding="utf-8") as out_f:
        for i, txt in enumerate(texts, start=1):
            out_f.write(f"--- Page {i} ---\n{txt}\n\n")
    print(f"Extracted text stored in {out_path}")

if __name__ == "__main__":
    main()
```

Voer het uit:

```bash
python extract_pdf_ocr.py
```

Je zou de inhoud van elke pagina in de console moeten zien, gevolgd door een bevestiging dat het bestand `extracted_text.txt` is aangemaakt.

## Conclusie

We hebben behandeld **hoe je PDF‑tekst** kunt extraheren uit alleen‑afbeelding‑documenten met een OCR‑engine, van het installeren van de bibliotheek tot het verwerken van multi‑page resultaten en het opslaan van de output. Je weet nu **hoe je OCR gebruikt**, hoe je **PDF als afbeelding laadt**, en hoe je **PDF‑tekst betrouwbaar herkent**.  

Volgende stappen? Probeer de standaard engine‑modus te vervangen door een high‑accuracy instelling, experimenteer met taal‑pakketten voor meertalige PDF’s, of pipe de geëxtraheerde tekst naar een full‑text zoekindex zoals Elasticsearch. De mogelijkheden zijn eindeloos zodra je de basis van het extraheren van tekst uit PDF‑bestanden onder de knie hebt.

---

![how to extract pdf example](images/ocr_flowchart.png){alt="how to extract pdf workflow diagram"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}