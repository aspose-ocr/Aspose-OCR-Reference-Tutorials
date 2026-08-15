---
category: general
date: 2026-03-26
description: Maak een ROI-polygon om OCR uit te voeren op het geselecteerde gebied.
  Leer hoe je meerdere regio's definieert, registreert en tekst extraheert met een
  Python OCR‑engine.
draft: false
keywords:
- create roi polygon
- ocr on selected area
- region of interest
- ocr engine
- python ocr example
language: nl
og_description: Maak een ROI-polygon en voer OCR uit op het geselecteerde gebied met
  een Python‑engine. Volledige code, uitleg en tips inbegrepen.
og_title: Maak ROI-polygon – Snelle OCR op geselecteerd gebied
tags:
- OCR
- Python
- Image Processing
title: ROI-polygon maken – Stapsgewijze handleiding voor OCR op geselecteerd gebied
url: /nl/python-java/general/create-roi-polygon-step-by-step-guide-for-ocr-on-selected-ar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ROI-polygon maken – Volledige tutorial voor OCR op geselecteerd gebied

Heb je ooit **create ROI polygon** moeten **maken** zodat je OCR kunt uitvoeren op alleen het deel van een afbeelding dat relevant is? Misschien scan je bonnen en zijn alleen de totalen belangrijk, of heb je een formulier waarbij alleen het handtekeningveld gelezen moet worden. In die gevallen bespaart **ocr on selected area** tijd en verhoogt het de nauwkeurigheid.  

In deze gids lopen we alles door wat je nodig hebt: van het definiëren van twee polygonen, het registreren ervan bij een OCR‑engine, tot het ophalen van de herkende tekst in één nette aanroep. Aan het einde heb je een kant‑klaar script en een solide begrip van waarom focussen op regio’s van belang belangrijk is.

## Wat je zult leren

- Hoe je **create ROI polygon**‑objecten maakt met een typische OCR‑bibliotheek.
- Het verschil tussen het definiëren van één regio versus meerdere.
- Hoe je die regio’s registreert bij de engine zodat `ocr on selected area` wordt uitgevoerd.
- Verwachte output en hoe je veelvoorkomende valkuilen oplost (bijv. overlappende ROI’s, lege resultaten).

### Vereisten

- Python 3.8+ geïnstalleerd.
- Een OCR‑bibliotheek die `Polygon`, `Point` en `add_region_of_interest` methoden exposeert (het voorbeeld gebruikt een fictieve `ocr`‑module; vervang dit door je eigen SDK, zoals Tesseract‑Python wrappers of EasyOCR).
- Een voorbeeld‑afbeeldingsbestand (`sample.png`) dat tekst bevat binnen de hieronder getoonde coördinaten.

> **Pro tip:** Als je een echte bibliotheek gebruikt, zorg er dan voor dat de afbeelding wordt geladen in dezelfde coördinatenruimte (origine links‑boven, X neemt rechts toe, Y neemt naar beneden toe).  

---  

## Stap 1: Importeer de OCR‑module en laad je afbeelding  

Eerst importeer je het OCR‑pakket en lees je de afbeelding die je wilt verwerken.  

```python
import ocr  # Replace with your actual OCR library import
from pathlib import Path

# Load the image – adjust the path as needed
image_path = Path("sample.png")
ocr_engine = ocr.Engine(image_path)
```

*Waarom dit belangrijk is:* De engine heeft de afbeeldingsdata nodig voordat je een **ROI polygon** kunt toevoegen. Sommige bibliotheken laten je de afbeelding later doorgeven, maar vroegtijdig initialiseren houdt de workflow overzichtelijk.

## Stap 2: Definieer de eerste ROI‑polygon  

Nu maken we de eerste regio van belang. Beschouw het als het tekenen van een rechthoek rond een tabelkop.  

```python
# Step 2: Define the first ROI polygon
first_roi = ocr.Polygon([
    ocr.Point(50, 20),   # top‑left
    ocr.Point(200, 20),  # top‑right
    ocr.Point(200, 80),  # bottom‑right
    ocr.Point(50, 80)    # bottom‑left
])
```

*Uitleg:*  
- `ocr.Point(x, y)` gebruikt pixelcoördinaten.  
- De lijst met punten is met de klok mee geordend, wat de meeste engines verwachten.  
- Je kunt zoveel punten toevoegen als je wilt om onregelmatige vormen te maken; een rechthoek is slechts een speciaal geval.

## Stap 3: Definieer extra ROI‑polygonen (optioneel)  

Je hoeft niet bij één te stoppen. Hier is een tweede polygon die een handtekeningveld lager op de pagina vastlegt.  

```python
# Step 3: Define the second ROI polygon
second_roi = ocr.Polygon([
    ocr.Point(300, 150),
    ocr.Point(480, 150),
    ocr.Point(480, 210),
    ocr.Point(300, 210)
])
```

*Waarom meer toevoegen?* Het uitvoeren van **ocr on selected area** voor meerdere zones laat je verschillende stukjes data in één doorloop extraheren, wat veel sneller is dan elke uitsnede afzonderlijk bijsnijden en verwerken.

## Stap 4: Registreer de ROI’s bij de OCR‑engine  

Met de polygonen klaar, vertel je de engine welke gebieden geïnspecteerd moeten worden.  

```python
# Step 4: Register the ROIs
ocr_engine.add_region_of_interest(first_roi)
ocr_engine.add_region_of_interest(second_roi)
```

*Belangrijk:* Sommige SDK’s vereisen dat je een `clear_regions()`‑methode aanroept voordat je nieuwe toevoegt als je de engine voor een andere afbeelding hergebruikt.

## Stap 5: Voer OCR uit en haal de tekst op  

Tot slot start je de herkenning. De engine kijkt alleen binnen de polygonen die we zojuist hebben toegevoegd.  

```python
# Step 5: Perform OCR on the defined regions
recognized_text = ocr_engine.recognize().get_text()
print("=== Recognized Text ===")
print(recognized_text)
```

**Verwachte output** (ervan uitgaande dat `sample.png` de woorden “Invoice Total: $123.45” bevat in de eerste ROI en “Signature: John Doe” in de tweede):

```
=== Recognized Text ===
Invoice Total: $123.45
Signature: John Doe
```

Als de output leeg is, controleer dan of de coördinaten daadwerkelijk tekst kruisen en of de afbeeldingsresolutie overeenkomt met het coördinatensysteem.

## Randgevallen & Veelvoorkomende valkuilen  

| Situatie                               | Waar op letten                               | Oplossing / Work‑around                              |
|----------------------------------------|----------------------------------------------|------------------------------------------------------|
| **Overlapende ROI's**                  | Tekst kan twee keer worden geretourneerd.    | Houd polygonen gescheiden of verwijder dubbele uitvoer. |
| **ROI buiten afbeeldingsgrenzen**      | Engine kan een fout veroorzaken of niets retourneren. | Beperk coördinaten tot `0 ≤ x < breedte`, `0 ≤ y < hoogte`. |
| **Zeer kleine ROI**                    | OCR‑nauwkeurigheid daalt door onvoldoende pixels. | Vergroot de polygon een paar pixels of schaal de afbeelding eerst op. |
| **Niet‑rechthoekige vorm**             | Sommige engines ondersteunen alleen convexe polygonen. | Splits complexe vormen op in meerdere convexe ROI's. |
| **Veranderende afbeeldingsgrootte**    | Hard‑gecodeerde coördinaten worden ongeldig. | Bereken ROI‑coördinaten relatief aan de afbeeldingsafmetingen (bijv. percentages). |

## Volledig werkend voorbeeld  

Hieronder staat het volledige script dat je kunt kopiëren‑plakken en uitvoeren (vervang `ocr` door je eigen bibliotheek).  

```python
import ocr                      # <- your OCR library
from pathlib import Path

# -------------------------------------------------
# Configuration
# -------------------------------------------------
IMAGE_PATH = Path("sample.png")

# -------------------------------------------------
# Initialize OCR engine with the image
# -------------------------------------------------
engine = ocr.Engine(IMAGE_PATH)

# -------------------------------------------------
# Define ROI polygons
# -------------------------------------------------
first_roi = ocr.Polygon([
    ocr.Point(50, 20), ocr.Point(200, 20),
    ocr.Point(200, 80), ocr.Point(50, 80)
])

second_roi = ocr.Polygon([
    ocr.Point(300, 150), ocr.Point(480, 150),
    ocr.Point(480, 210), ocr.Point(300, 210)
])

# -------------------------------------------------
# Register ROIs
# -------------------------------------------------
engine.add_region_of_interest(first_roi)
engine.add_region_of_interest(second_roi)

# -------------------------------------------------
# Run OCR on the selected areas
# -------------------------------------------------
result = engine.recognize().get_text()

print("=== Recognized Text ===")
print(result)
```

Voer het uit met `python ocr_roi_example.py` en je zou de geëxtraheerde strings uit de twee gedefinieerde zones moeten zien.

## Volgende stappen  

- **Dynamische ROI‑generatie:** In plaats van hard‑gecodeerde coördinaten, gebruik beeldverwerking (bijv. OpenCV contourdetectie) om automatisch tabellen of velden te lokaliseren.  
- **Post‑processing:** Verwijder witruimte, pas regex‑patronen toe, of converteer getallen naar juiste datatypes.  
- **Batchverwerking:** Loop over een map met afbeeldingen, hergebruik dezelfde ROI‑definities als de lay‑out consistent is.  

Als je nieuwsgierig bent naar **ocr on selected area** voor complexere documenten—denk aan meer‑pagina‑PDF’s of gescande formulieren—kijk dan naar bibliotheken die pagina‑gewijze ROI‑registratie ondersteunen.  

---  

### Visueel overzicht  

![Diagram die twee ROI-polygonen op een voorbeeldafbeelding toont](roi_diagram.png){alt="voorbeeld van ROI-polygon maken dat twee geselecteerde gebieden toont"}

---  

## Conclusie  

We hebben zojuist **create ROI polygon**‑objecten gemaakt, ze geregistreerd bij een OCR‑engine, en `ocr on selected area` uitgevoerd in een schoon, reproduceerbaar script. Door de engine te beperken tot de zones die je interesseren, verkort je de verwerkingstijd, verbeter je de nauwkeurigheid, en maak je de verdere gegevensafhandeling veel eenvoudiger.  

Probeer het met je eigen afbeeldingen—pas de coördinaten aan, voeg meer polygonen toe, of koppel de output aan een database. De mogelijkheden zijn eindeloos zodra je regio‑gebaseerde OCR onder de knie hebt.  

Heb je vragen of wil je een cool gebruiksvoorbeeld delen? Laat een reactie achter hieronder, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}