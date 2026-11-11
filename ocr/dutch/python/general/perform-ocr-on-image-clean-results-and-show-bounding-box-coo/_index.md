---
category: general
date: 2026-03-28
description: Voer OCR uit op een afbeelding en verkrijg schone tekst met de coördinaten
  van de begrenzingskaders. Leer hoe je OCR kunt extraheren, OCR kunt opschonen en
  de resultaten stap voor stap kunt weergeven.
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: nl
og_description: Voer OCR uit op een afbeelding, maak de output schoon en toon de coördinaten
  van de begrenzingskaders in een beknopte tutorial.
og_title: Voer OCR uit op afbeelding – Schone resultaten en begrenzingskaders
tags:
- OCR
- Computer Vision
- Python
title: Voer OCR uit op afbeelding – schone resultaten en toon de coördinaten van het
  begrenzingsvak
url: /nl/python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR uitvoeren op afbeelding – schone resultaten en coördinaten van begrenzende vakken tonen

Heb je ooit **OCR op afbeelding** moeten uitvoeren, maar kreeg je rommelige tekst en wist je niet waar elk woord zich op de foto bevond? Je bent niet de enige. In veel projecten—factuurdigitalisatie, kassabon‑scannen of eenvoudige tekste‑extractie—is het verkrijgen van ruwe OCR‑output slechts de eerste hindernis. Het goede nieuws? Je kunt die output opschonen en direct de coördinaten van de begrenzende vakken van elke regio zien, zonder een hoop boilerplate‑code te schrijven.

In deze gids lopen we stap voor stap door **hoe OCR te extraheren**, een **hoe OCR op te schonen** post‑processor uit te voeren, en uiteindelijk **de coördinaten van begrenzende vakken** voor elke opgeschoonde regio weer te geven. Aan het einde heb je één enkel, uitvoerbaar script dat een onscherpe foto omzet in nette, gestructureerde tekst klaar voor verdere verwerking.

## Wat je nodig hebt

- Python 3.9+ (de syntaxis hieronder werkt op 3.8 en nieuwer)
- Een OCR‑engine die `recognize(..., return_structured=True)` ondersteunt – bijvoorbeeld een fictieve `engine`‑bibliotheek die in het voorbeeld wordt gebruikt. Vervang deze door Tesseract, EasyOCR of een andere SDK die regiogegevens retourneert.
- Basiskennis van Python‑functies en loops
- Een afbeeldingsbestand dat je wilt scannen (PNG, JPG, enz.)

> **Pro tip:** Als je Tesseract gebruikt, geeft de functie `pytesseract.image_to_data` al begrenzende vakken terug. Je kunt het resultaat in een kleine adapter wikkelen die de `engine.recognize`‑API nabootst zoals hieronder getoond.

---

![perform OCR on image example](image-placeholder.png "perform OCR on image example")

*Alt‑tekst: diagram dat laat zien hoe OCR op een afbeelding wordt uitgevoerd en hoe de coördinaten van begrenzende vakken worden gevisualiseerd*

## Stap 1 – OCR uitvoeren op afbeelding en gestructureerde regio’s ophalen

Het eerste wat je moet doen, is de OCR‑engine vragen om niet alleen platte tekst, maar een gestructureerde lijst van tekstreeksen terug te geven. Deze lijst bevat de ruwe string en de rechthoek die deze omsluit.

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**Waarom dit belangrijk is:**  
Wanneer je alleen om platte tekst vraagt, verlies je de ruimtelijke context. Gestructureerde data stelt je later in staat om **coördinaten van begrenzende vakken** weer te geven, tekst uit te lijnen met tabellen, of precieze locaties aan een downstream‑model te leveren.

## Stap 2 – Hoe OCR‑output op te schonen met een post‑processor

OCR‑engines zijn goed in het herkennen van tekens, maar laten vaak overbodige spaties, regeleinde‑artefacten of foutief herkende symbolen achter. Een post‑processor normaliseert de tekst, corrigeert veelvoorkomende OCR‑fouten en verwijdert onnodige witruimte.

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

Als je je eigen opschoonroutine bouwt, overweeg dan:

- Het verwijderen van niet‑ASCII‑tekens (`re.sub(r'[^\x00-\x7F]+',' ', text)`)
- Het samenvoegen van meerdere spaties tot één enkele spatie
- Het toepassen van een spell‑checker zoals `pyspellchecker` voor duidelijke typefouten

**Waarom je hier om zou moeten geven:**  
Een nette string maakt zoeken, indexeren en downstream‑NLP‑pijplijnen veel betrouwbaarder. Met andere woorden, **hoe OCR op te schonen** is vaak het verschil tussen een bruikbare dataset en een hoofdpijnervaring.

## Stap 3 – Coördinaten van begrenzende vakken voor elke opgeschoonde regio weergeven

Nu de tekst netjes is, itereren we over elke regio, printen we de rechthoek en de opgeschoonde string. Dit is het moment waarop we eindelijk **coördinaten van begrenzende vakken** weergeven.

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**Voorbeeldoutput**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

Je kunt die coördinaten nu doorgeven aan een tekenbibliotheek (bijv. OpenCV) om vakken over de originele afbeelding te leggen, of ze opslaan in een database voor latere queries.

## Volledig, kant‑klaar script

Hieronder staat het complete programma dat alle drie de stappen samenbrengt. Vervang de placeholder `engine`‑aanroepen door je eigen OCR‑SDK.

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### Hoe uit te voeren

```bash
python perform_ocr.py sample_invoice.jpg
```

Je zou een lijst met begrenzende vakken gekoppeld aan opgeschoonde tekst moeten zien, precies zoals de voorbeeldoutput hierboven.

## Veelgestelde vragen & randgevallen

| Vraag | Antwoord |
|----------|--------|
| **Wat als de OCR‑engine `return_structured` niet ondersteunt?** | Schrijf een dunne wrapper die de ruwe output van de engine (meestal een lijst van woorden met coördinaten) omzet naar objecten met de attributen `text` en `bounding_box`. |
| **Kan ik vertrouwensscores krijgen?** | Veel SDK’s bieden een vertrouwensmetric per regio. Voeg deze toe aan de print‑statement: `print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")`. |
| **Hoe ga ik om met gedraaide tekst?** | Pre‑process de afbeelding met OpenCV’s `cv2.minAreaRect` om de scheefstand te corrigeren voordat je `recognize` aanroept. |
| **Wat als ik de output in JSON nodig heb?** | Serialiseer `processed_result.regions` met `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)`. |
| **Is er een manier om de vakken te visualiseren?** | Gebruik OpenCV: `cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)` binnen de loop, daarna `cv2.imwrite("annotated.jpg", img)`. |

## Afsluiten

Je hebt zojuist geleerd **hoe OCR op afbeelding** uit te voeren, de ruwe output op te schonen, en **coördinaten van begrenzende vakken** voor elke regio weer te geven. De drie‑stappen‑flow — herkennen → post‑processen → itereren — is een herbruikbaar patroon dat je in elk Python‑project kunt gebruiken dat betrouwbare tekste‑extractie nodig heeft.

### Wat is het volgende?

- **Verken verschillende OCR‑back‑ends** (Tesseract, EasyOCR, Google Vision) en vergelijk de nauwkeurigheid.
- **Integreer met een database** om regiogegevens op te slaan voor doorzoekbare archieven.
- **Voeg taaldetectie toe** om elke regio door de juiste spell‑checker te laten lopen.
- **Leg vakken over de originele afbeelding** voor visuele verificatie (zie het OpenCV‑fragment hierboven).

Als je tegen eigenaardigheden aanloopt, onthoud dan dat de grootste winst voortkomt uit een solide post‑processing stap; een schone string is veel makkelijker mee te werken dan een ruwe dump van tekens.

Happy coding, and may your OCR pipelines be ever tidy!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}