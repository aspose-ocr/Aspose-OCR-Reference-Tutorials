---
category: general
date: 2026-01-12
description: Tekst extraheren uit PDF met OCR-engine Python – leer hoe je PDF leest
  met OCR, afbeelding laadt voor OCR en gestructureerde resultaten krijgt.
draft: false
keywords:
- extract text from pdf
- read pdf with ocr
- load image for ocr
- use ocr engine python
language: nl
og_description: Tekst extraheren uit PDF met OCR‑engine Python. Deze tutorial laat
  zien hoe je PDF leest met OCR, een afbeelding laadt voor OCR, en de OCR‑engine Python
  gebruikt voor betrouwbare resultaten.
og_title: Tekst extraheren uit PDF met OCR-engine Python – Complete gids
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Tekst extraheren uit PDF met OCR‑engine Python – Stapsgewijze handleiding
url: /nl/python/general/extract-text-from-pdf-with-ocr-engine-python-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit PDF met OCR Engine Python – Volledige tutorial

Heb je ooit **tekst uit PDF moeten extraheren** maar is het bestand slechts een gescande afbeelding? Je bent niet de enige. In veel real‑world projecten heeft de PDF die je ontvangt geen selecteerbare tekst, dus de enige manier is om **PDF met OCR te lezen**.  

In deze gids lopen we een praktische, end‑to‑end oplossing door die precies laat zien hoe je **image for OCR laadt**, de **OCR engine Python** opstart, en gestructureerde tekst haalt die je kunt invoeren in downstream pipelines. Geen vage verwijzingen, alleen een compleet, uitvoerbaar voorbeeld dat je vandaag nog kunt copy‑pasten.

## Wat je zult leren

- Hoe je de benodigde Python OCR-bibliotheek installeert en importeert.  
- De exacte stappen om **image for OCR te laden** vanuit een PDF‑bestand.  
- Hoe je de `recognize_structured()`‑methode van de engine aanroept en over blocks, lines en words itereren.  
- Tips voor het omgaan met low‑confidence resultaten en multi‑page PDF’s.  

Aan het einde van deze tutorial heb je een script dat betrouwbaar **tekst uit PDF** documenten extraheert, ongeacht of ze één pagina of honderd pagina's bevatten.

---

![Diagram dat de OCR-engine toont die een PDF verwerkt en gestructureerde tekst output.](images/ocr_flow.png "tekst uit pdf diagram")

*Afbeeldingsalttekst: tekst uit pdf diagram dat OCR-verwerkingsstappen illustreert.*

## Vereisten

- Python 3.9 of nieuwer (de code gebruikt f‑strings en type hints).  
- Een via pip installeerbaar OCR‑pakket dat een `OcrEngine`‑klasse exposeert (bijvoorbeeld een fictieve `pyocr`‑bibliotheek).  
- Een PDF‑bestand dat je wilt verwerken, lokaal opgeslagen (bijv. `form.pdf`).  

Als je de OCR‑bibliotheek mist, installeer deze met:

```bash
pip install pyocr   # replace with the actual package name you use
```

---

## Stap 1: Tekst extraheren uit PDF – OCR‑engine instellen

Voordat we **PDF met OCR kunnen lezen**, hebben we een engine‑instance nodig. Beschouw de engine als het brein dat naar elke pixel kijkt en bepaalt welk teken het vertegenwoordigt.

```python
# Step 1: Import the OCR module and create an engine instance
import ocr  # or `import pyocr as ocr` depending on the package

# Create the OCR engine – this may load language models under the hood
ocr_engine = ocr.OcrEngine()
```

> **Waarom dit belangrijk is:** De engine één keer initialiseren laat je toe om geladen taalpakketten te hergebruiken over meerdere bestanden, waardoor zowel tijd als geheugen bespaard wordt.

---

## Stap 2: Image for OCR laden – Je PDF voorbereiden

Een PDF is geen ruwe afbeelding, dus biedt de bibliotheek meestal een helper om de eerste pagina (of alle pagina's) om te zetten naar een afbeelding die de OCR‑engine kan begrijpen.

```python
# Step 2: Load the PDF page(s) you want to process
# The `load_image` method accepts many formats – PDF, PNG, JPEG, etc.
pdf_path = "YOUR_DIRECTORY/form.pdf"
ocr_engine.load_image(pdf_path)
```

> **Tip:** Als je PDF meerdere pagina's heeft, laten veel OCR‑bibliotheken je `page=2` doorgeven of een lus over `engine.load_image(pdf_path, page=n)`. Voor grote documenten, overweeg om pagina's in batches te verwerken om geheugenpieken te vermijden.

---

## Stap 3: OCR Engine Python gebruiken – Gestructureerde tekst herkennen

Nu gebeurt het zware werk. De `recognize_structured()`‑aanroep retourneert een hiërarchie van blocks → lines → words, elk geannoteerd met taal, confidence en bounding boxes.

```python
# Step 3: Perform structured text recognition
structured_result = ocr_engine.recognize_structured()
```

> **Wat je krijgt:**  
> - `structured_result.blocks` – containers op top‑niveau (vaak alinea's of kolommen).  
> - Elk block bevat `lines`, en elke line bevat `words`.  
> - Confidence‑scores laten je dubieuze resultaten filteren.

---

## Stap 4: Over resultaten itereren – Blocks, lines en words benaderen

Hieronder staat een compacte lus die de meest bruikbare informatie afdrukt. Voel je vrij om deze uit te breiden om JSON, CSV te schrijven, of een database te voeden.

```python
# Step 4: Walk through the hierarchy and display key data
for block_idx, text_block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={text_block.language}, confidence={text_block.confidence:.2f}")

    # Show a sample line from the block, if any
    if text_block.lines:
        sample_line = text_block.lines[0]
        print(f"  Sample line: {sample_line.text}")

        # Show a sample word with its bounding box and confidence
        if sample_line.words:
            sample_word = sample_line.words[0]
            print(
                f"    Sample word: '{sample_word.text}' "
                f"bbox={sample_word.bounding_box} "
                f"conf={sample_word.confidence:.2f}"
            )
```

### Verwachte output

```
Block 1: language=en, confidence=0.97
  Sample line: Invoice Number: 2025-00123
    Sample word: 'Invoice' bbox=(12,34,78,90) conf=0.99
Block 2: language=en, confidence=0.94
  Sample line: Total Amount: $1,250.00
    Sample word: 'Total' bbox=(15,120,70,155) conf=0.96
...
```

> **Waarom je dit geweldig zult vinden:** De hiërarchie spiegelt hoe mensen een pagina lezen, waardoor het later eenvoudig is om tabellen of kolomlay-outs te reconstrueren.

---

## Stap 5: Randgevallen afhandelen – Low Confidence & multi‑page PDF’s

### Low‑confidence woorden

Als de confidence van een woord onder, bijvoorbeeld, `0.70` daalt, wil je het misschien markeren voor handmatige controle:

```python
LOW_CONF_THRESHOLD = 0.70

for block in structured_result.blocks:
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

### Alle pagina's verwerken

```python
# Example: loop over every page in a multi‑page PDF
for page_number in range(ocr_engine.page_count):
    ocr_engine.load_image(pdf_path, page=page_number)
    result = ocr_engine.recognize_structured()
    # …process `result` just like we did above…
```

> **Pro tip:** Cache tussenliggende afbeeldingen als PNG’s als je OCR‑bibliotheek ze elke keer opnieuw rendert—dat kan seconden besparen bij grote batches.

---

## Volledig werkend script

Alles samenvoegend, hier is een enkel bestand dat je direct kunt uitvoeren:

```python
#!/usr/bin/env python3
"""
Extract text from PDF with OCR engine Python.
This script demonstrates loading a PDF, recognizing structured text,
and printing a concise summary of blocks, lines, and words.
"""

import ocr  # Replace with your actual OCR package import

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
PDF_PATH = "YOUR_DIRECTORY/form.pdf"
LOW_CONF_THRESHOLD = 0.70

# ----------------------------------------------------------------------
# Initialize OCR engine
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()

# ----------------------------------------------------------------------
# Load the PDF (first page by default)
# ----------------------------------------------------------------------
ocr_engine.load_image(PDF_PATH)

# ----------------------------------------------------------------------
# Recognize structured text
# ----------------------------------------------------------------------
structured_result = ocr_engine.recognize_structured()

# ----------------------------------------------------------------------
# Iterate and display results
# ----------------------------------------------------------------------
for block_idx, block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={block.language}, confidence={block.confidence:.2f}")

    if block.lines:
        line = block.lines[0]
        print(f"  Sample line: {line.text}")

        if line.words:
            word = line.words[0]
            print(
                f"    Sample word: '{word.text}' "
                f"bbox={word.bounding_box} "
                f"conf={word.confidence:.2f}"
            )

    # Flag low‑confidence words inside the block
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

Save this as `extract_pdf_ocr.py` and run:

```bash
python extract_pdf_ocr.py
```

Je zou block‑level details in de console moeten zien afgedrukt, samen met eventuele low‑confidence waarschuwingen.

---

## Conclusie

We hebben zojuist een complete, productie‑klare manier behandeld om **tekst uit PDF** te **extraheren** met een **OCR engine Python**. Beginnend met het installeren van de bibliotheek, via **image for OCR laden**, tot **PDF met OCR lezen** en uiteindelijk itereren over de gestructureerde output, heb je nu een herbruikbaar script dat je kunt aanpassen aan elk project.

Volgende stappen die je kunt verkennen:

- De hiërarchie exporteren naar JSON voor downstream NLP‑pipelines.  
- Taaldetectie toevoegen om OCR‑modellen dynamisch te wisselen.  
- Integreren met `pdf2image` om PDF’s met complexe lay-outs vooraf te verwerken.  

Probeer het op een batch met multi‑page facturen, pas de confidence‑drempel aan, en zie hoe snel je gescande PDF’s kunt omzetten naar doorzoekbare, bewerkbare tekst. Als je tegen problemen aanloopt, laat dan een reactie achter—happy OCRing!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}