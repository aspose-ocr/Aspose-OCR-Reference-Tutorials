---
category: general
date: 2026-04-26
description: hoe OCR uit afbeeldingen te extraheren met Python – een Python OCR‑voorbeeld
  dat laat zien hoe je een afbeelding laadt voor OCR en tekst van een bon extraheert.
draft: false
keywords:
- how to extract ocr
- python ocr example
- extract text from receipt
- load image for ocr
- how to use OCR
language: nl
og_description: Hoe OCR uit afbeeldingen te extraheren met Python. Leer een Python
  OCR‑voorbeeld, laad een afbeelding voor OCR, en extraheer tekst van een bon in enkele
  minuten.
og_title: hoe OCR te extraheren in Python – Complete gids
tags:
- OCR
- Python
- Image Processing
title: Hoe OCR in Python te extraheren – Stapsgewijze tutorial
url: /nl/python-java/general/how-to-extract-ocr-in-python-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hoe ocr te extraheren in Python – Complete gids

Heb je je ooit afgevraagd **hoe je ocr kunt extraheren** van een wazige bon of een gescande factuur? Je bent niet de enige—ontwikkelaars lopen constant tegen muren aan wanneer ze schone, machinaal‑leesbare tekst uit afbeeldingen nodig hebben. Het goede nieuws? Met slechts een paar regels Python kun je een foto van een bon omzetten in hoog‑vertrouwelijke, doorzoekbare tekst.

In deze tutorial lopen we een **python ocr voorbeeld** door dat laat zien **hoe je een afbeelding laadt voor ocr**, de engine uitvoert, en alleen de tekens behoudt die een vertrouwensdrempel van 85 % halen. Aan het einde kun je **tekst uit bon**‑afbeeldingen extraheren zonder door documentatie te hoeven speuren of API‑parameters te raden.

## Wat je nodig hebt

- Python 3.9 of nieuwer (de syntax die we gebruiken werkt op 3.8+)
- Het `aocr`‑pakket (of een andere OCR‑bibliotheek die een `OcrEngine`‑klasse biedt). Installeer het met:

```bash
pip install aocr
```

- Een voorbeeld‑bonafbeelding (`receipt.png`) geplaatst in een map die je kunt refereren.
- Een teksteditor of IDE—VS Code, PyCharm, of zelfs een eenvoudige notebook volstaat.

Dat is alles. Geen zware frameworks, geen externe services, alleen pure Python.

![High‑confidence OCR result – how to extract ocr from a receipt](/images/ocr-high-confidence.png)

*Afbeeldings‑alt‑tekst: hoe ocr te extraheren uit een bon met Python OCR*

## Stap 1 – Maak de OCR‑engine‑instantie (hoe ocr te extraheren)

Het eerste wat we doen is een OCR‑engine opstarten. Beschouw het als het brein dat de pixels voor ons leest.

```python
# Step 1: Initialize the OCR engine
from aocr import OcrEngine

ocr_engine = OcrEngine()
```

**Waarom?** Het instantieren van `OcrEngine` geeft je een vers configuratie‑object. Later kun je taalmodellen, DPI‑instellingen of pre‑processing stappen aanpassen—allemaal zonder de kernverwerkingslus aan te raken.

## Stap 2 – Laad de afbeelding voor OCR

Vervolgens wijzen we de engine op de afbeelding die we willen analyseren. Hier komt het **load image for ocr**‑keyword van pas.

```python
# Step 2: Load the receipt image
image_path = "YOUR_DIRECTORY/receipt.png"
ocr_engine.image = OcrEngine.Image.load(image_path)
```

> **Pro tip:** Als je afbeelding zich in een andere map bevindt, gebruik dan `os.path.join` om een platform‑onafhankelijk pad te bouwen.

**Waarom de afbeelding op deze manier laden?** De helper `Image.load` leest het bestand in een formaat dat de engine begrijpt, en behandelt gangbare formaten (PNG, JPEG, TIFF) automatisch. Deze stap overslaan of ruwe bytes doorgeven zou een `ValueError` veroorzaken.

## Stap 3 – Voer het OCR‑proces uit

Nu voeren we daadwerkelijk de OCR uit. De `process`‑methode retourneert een rijk resultaatobject met herkende symbolen, vertrouwensscores en begrenzings‑boxen.

```python
# Step 3: Execute OCR and capture the result
ocr_result = ocr_engine.process()
```

**Wat bevat `ocr_result`?** In de meeste bibliotheken omvat het:

- `text`: de ruwe aaneengeschakelde string.
- `symbol_confidences`: een lijst van `(char, confidence)`‑tuples.
- `boxes`: coördinaten voor elk teken (handig voor visuele debugging).

Toegang hebben tot per‑teken‑vertrouwen is essentieel voor de volgende stap.

## Stap 4 – Houd alleen hoog‑vertrouwelijke symbolen (≥ 85 %)

Een bon heeft vaak vlekken, vage afdruk of achtergrondruis. Door lage‑vertrouwelijke symbolen te filteren, verbeteren we de downstream‑parsing drastisch.

```python
# Step 4: Filter out low‑confidence characters
high_confidence_text = ''.join(
    char for char, confidence in ocr_result.symbol_confidences
    if confidence >= 0.85
)
```

**Waarom 85 %?** Empirisch gezien biedt een drempel rond 0.85 een goede balans tussen recall en precisie voor de meeste gedrukte bonnen. Als je ontbrekende cijfers ziet, verlaag dan de drempel; als je onzinnige tekst krijgt, verhoog hem.

## Stap 5 – Output de hoog‑vertrouwelijke geëxtraheerde tekst

Tot slot printen (of slaan we) we de opgeschoonde string op. Dit is de kern van onze **extract text from receipt**‑workflow.

```python
# Step 5: Show the cleaned result
print("High‑confidence text:", high_confidence_text)
```

Typische output ziet er als volgt uit:

```
High‑confidence text: Store XYZ
Date: 2024‑04‑22
Total: $23.45
```

Je kunt deze string nu doorgeven aan een CSV‑schrijver, een database, of elke downstream‑analytics‑pipeline.

## Volledig, kant‑klaar script

Hieronder staat de complete code‑snippet die je kunt kopiëren‑plakken in `ocr_receipt.py` en direct kunt uitvoeren.

```python
# ocr_receipt.py
# A complete python ocr example that extracts high‑confidence text from a receipt.

from aocr import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the image you want to analyze
    image_path = "YOUR_DIRECTORY/receipt.png"
    ocr_engine.image = OcrEngine.Image.load(image_path)

    # 3️⃣ Run the OCR process
    ocr_result = ocr_engine.process()

    # 4️⃣ Keep only symbols with confidence ≥ 85%
    high_confidence_text = ''.join(
        char for char, confidence in ocr_result.symbol_confidences
        if confidence >= 0.85
    )

    # 5️⃣ Output the result
    print("High‑confidence text:", high_confidence_text)

if __name__ == "__main__":
    main()
```

Sla het bestand op, zorg dat `receipt.png` bestaat, en voer uit:

```bash
python ocr_receipt.py
```

Je zou de opgeschoonde bontekst in de console moeten zien verschijnen.

## Randgevallen & Wat‑als‑scenario's

| Situatie | Aanbevolen oplossing |
|-----------|----------------------|
| **Zeer lage vertrouwensscores overal** | Pre‑process de afbeelding: verhoog contrast, converteer naar grijswaarden, of pas een denoising‑filter toe (`cv2.GaussianBlur`). |
| **Niet‑Latijnse tekens** | Geef een taalmodel door aan `OcrEngine` (bijv. `ocr_engine.language = "spa"` voor Spaans). |
| **Meerdere bonnen in één afbeelding** | Voer OCR uit op de volledige afbeelding, splits vervolgens het resultaat met reguliere expressies die `\n\n+` (dubbele regeleinden) detecteren. |
| **De ruwe OCR‑tekst ook nodig** | Houd `ocr_result.text` naast de gefilterde versie voor debugging. |

Deze variaties zorgen ervoor dat je **how to use OCR**‑kennis verder reikt dan het eenvoudigste geval.

## Veelvoorkomende valkuilen (en hoe ze te vermijden)

- **Vergeten de bibliotheek te installeren** – `pip install aocr` moet slagen voordat je importeert.
- **Het verkeerde pad‑scheidingsteken gebruiken** op Windows (`\` vs `/`). Gebruik `os.path.join`.
- **De vertrouwensdrempel hard‑coderen** zonder te testen – voer altijd een snelle visuele controle uit op een paar bonnen eerst.
- **Unicode‑normalisatie negeren** – sommige bonnen bevatten speciale streepjes; voer `unicodedata.normalize('NFKC', text)` uit als je de output wilt opslaan.

## Volgende stappen – Verder gaan dan de basis

Nu je weet **hoe ocr te extraheren** uit één bon, kun je:

1. **Batch‑verwerking van een map bonnen** – loop over alle PNG/JPG‑bestanden en schrijf elk resultaat naar een CSV.
2. **Integreren met een database** – sla `high_confidence_text` op in SQLite voor snelle opzoekingen.
3. **Natuurlijke‑taal‑parsing toepassen** – gebruik regex of `dateutil` om data, totalen en btw‑bedragen te halen.
4. **Experimenteren met alternatieve bibliotheken** – `pytesseract`, `easyocr`, of cloud‑services (Google Vision, Azure OCR) als je meertalige ondersteuning of hogere nauwkeurigheid nodig hebt.

Elk van deze onderwerpen verwerkt vanzelf onze secundaire zoekwoorden: *python ocr example*, *extract text from receipt*, *load image for ocr*, en *how to use OCR*.

## Conclusie

We hebben zojuist een volledige **python ocr example** doorlopen die laat zien **hoe ocr te extraheren** uit een bonafbeelding, lage‑vertrouwelijke symbolen filtert, en schone resultaten oplevert. De stappen zijn simpel, de code is zelf‑voorzienend, en de aanpak is flexibel genoeg om zich aan te passen aan grotere projecten.

Probeer het met je eigen bonnen, pas de vertrouwensdrempel aan, en schaal vervolgens op naar batch‑verwerking. Als je tegen eigenaardigheden aanloopt—zoals een vaag logo of een ongewoon lettertype—onthoud dan de bovenstaande randgevallen‑tips. Veel programmeerplezier, en moge je OCR‑pijplijnen altijd accuraat zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}