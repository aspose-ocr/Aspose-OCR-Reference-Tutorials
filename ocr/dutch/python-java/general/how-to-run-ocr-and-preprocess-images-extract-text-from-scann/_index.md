---
category: general
date: 2026-04-26
description: Hoe OCR uit te voeren op een gescand formulier, leer hoe je de afbeelding
  voorbewerkt om ruis te verminderen, en haal snel tekst uit de afbeelding.
draft: false
keywords:
- how to run OCR
- how to preprocess image
- extract text from image
- how to extract text
- how to reduce noise
language: nl
og_description: Hoe OCR uit te voeren op gescande documenten, afbeeldingen voor te
  bewerken, ruis te verminderen en efficiënt tekst te extraheren.
og_title: Hoe OCR uit te voeren en afbeeldingen voor te bewerken – Snelle gids
tags:
- OCR
- image processing
- Python
title: Hoe OCR uit te voeren en afbeeldingen voor te bewerken – Tekst extraheren uit
  gescande formulieren
url: /nl/python-java/general/how-to-run-ocr-and-preprocess-images-extract-text-from-scann/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR uit te voeren – Een volledige gids voor het extraheren van tekst uit afbeeldingen

Heb je je ooit afgevraagd **hoe je OCR uitvoert** op een rommelig gescande formulier en schone, doorzoekbare tekst krijgt? Je bent niet de enige. In veel real‑world projecten is de ruwe afbeelding vol met stippen, ongelijke verlichting en andere eigenaardigheden die standaard OCR laten haperen.  

Het goede nieuws? Met slechts een paar regels Python en een slimme preprocessing‑pipeline kun je de herkenningsnauwkeurigheid dramatisch verhogen, **ruis verminderen**, en precies de woorden halen die je nodig hebt. In deze tutorial lopen we elke stap door — van het laden van de afbeelding tot het afdrukken van de uiteindelijke string — zodat je met een kant‑klaar snippet aan de slag kunt voor facturen, bonnen of elk gescand document.

## Wat je gaat bouwen

- Een `OcrEngine`‑instance die communiceert met de onderliggende OCR‑bibliotheek.  
- Een preprocessing‑keten die de afbeelding **binariseert** en een **median blur** toepast om stippen glad te strijken.  
- Een eenvoudige aanroep van `process()` die een object retourneert met de eigenschap `text`, de geëxtraheerde string.  

Aan het einde heb je een zelfstandige script die je op elk afbeeldingsbestand kunt draaien en direct de geëxtraheerde tekst in de console ziet.

## Vereisten

- Python 3.9+ (de hier gebruikte syntaxis komt overeen met de nieuwste stabiele release).  
- Het fictieve `aocr`‑pakket – zie het als een dunne wrapper rond Tesseract of een moderne OCR‑engine. Installeer het met `pip install aocr`.  
- Een gescande afbeelding (`scanned_form.jpg`) geplaatst in een map die je kunt refereren.  

Als je een echte OCR‑bibliotheek zoals `pytesseract` gebruikt, kun je `OcrEngine` vervangen door de juiste klasse — alles blijft verder gelijk.

![](how-to-run-ocr-example.png "voorbeeld van hoe OCR uit te voeren, met een gescand formulier en de geëxtraheerde tekst")

*Alt text: hoe OCR uit te voeren op een gescand document en de geëxtraheerde tekst bekijken.*

---

## Stap 1: Hoe OCR uit te voeren – Initialiseer de Engine

Voordat de engine iets kan lezen, moeten we een instance maken. Beschouw de `OcrEngine` als het brein dat later de visuele data zal interpreteren.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()
```

> **Waarom dit belangrijk is:** Het instantieren van de engine zet interne modellen op, laadt taalpakketten en bereidt de runtime‑omgeving voor. Het overslaan van deze stap leidt meestal tot een `NoneType`‑fout wanneer je later `process()` aanroept.

---

## Stap 2: Hoe afbeelding voor te verwerken – Laad je gescande formulier

Nu het brein klaar is, voeren we er een afbeelding in. De afbeelding kan elk formaat hebben dat door `aocr.Image` wordt ondersteund.

```python
# Step 2: Load the image you want to recognize
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/scanned_form.jpg")
```

> **Pro tip:** Gebruik absolute paden tijdens ontwikkeling om “bestand niet gevonden” verrassingen te vermijden wanneer het script vanuit een andere werkmap wordt uitgevoerd.

---

## Stap 3: Hoe ruis te verminderen – Binarisatie & Median Blur toepassen

Ruwe scans bevatten vaak losse stippen, ongelijke achtergrond of vage schaduwen. Twee klassieke trucjes — **binarisatie** en **median blur** — maken alles schoon zonder de randen die karakters definiëren op te offeren.

```python
# Step 3: Pre‑process the image to improve recognition accuracy
# • Binarize converts the image to black‑and‑white using a threshold
# • Median blur reduces noise while preserving edges
ocr_engine.image = ocr_engine.image.apply_filters(
    aocr.ImageFilters.binarize(threshold=180),
    aocr.ImageFilters.median_blur(radius=2)
)
```

### Dieper ingaan

- **Binarisatie**: De waarde `threshold=180` vertelt het algoritme: “Alles helderder dan 180 wordt wit; alles anders wordt zwart.” Pas dit getal aan als je scan te donker of te licht is.  
- **Median Blur**: Een radius van `2` betekent dat het filter kijkt naar een 5×5‑pixelvenster en de centrale pixel vervangt door de mediaanwaarde. Dit gladstrijkt geïsoleerde stippen terwijl de strepen van letters intact blijven.

> **Randgeval:** Als je document gekleurde markeringen bevat, kan een eenvoudige binaire drempel ze wissen. Overweeg in dat scenario `aocr.ImageFilters.adaptive_threshold()` te gebruiken — dit past de drempel lokaal aan over de afbeelding.

---

## Stap 4: Hoe tekst te extraheren – Het OCR‑proces uitvoeren

Met een schone afbeelding in de hand laten we de engine eindelijk zijn magie doen.

```python
# Step 4: Run the OCR process on the prepared image
ocr_result = ocr_engine.process()
```

> **Wat er onder de motorkap gebeurt:** De engine draait een neuraal netwerk (of een legacy patroonmatcher) over de pixelmatrix, vertaalt elk herkend glyph naar Unicode‑tekens, en zet ze samen tot regels en alinea’s.

---

## Stap 5: Hoe tekst te extraheren – Het resultaat afdrukken

Het `ocr_result`‑object biedt een handige `text`‑attribuut. Laten we zien wat we hebben gekregen.

```python
# Step 5: Print the extracted text
print(ocr_result.text)
```

### Verwachte uitvoer

Als het gescande formulier bevat:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Zou je iets moeten zien als:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Merk op hoe de preprocessing‑stap losse stippen heeft verwijderd die eerder “Amount” veranderden in “Am0unt”. Dat is de kracht van **hoe ruis te verminderen** vóór OCR.

---

## Veelvoorkomende valkuilen & hoe ze op te lossen

| Symptoom | Waarschijnlijke oorzaak | Snelle oplossing |
|----------|--------------------------|-------------------|
| Vervormde tekens (bijv. “@#%”) | Afbeelding te donker of te licht | Pas de `threshold` in `binarize()` aan; probeer `adaptive_threshold`. |
| Ontbrekende woorden | Ruis nog aanwezig | Verhoog `radius` voor `median_blur` of voeg een `gaussian_blur` filter toe. |
| Verkeerde taal (bijv. Engelse letters worden Chinees) | Verkeerd taalpakket geladen | Geef `language="eng"` mee bij het aanmaken van `OcrEngine()` als de bibliotheek dit ondersteunt. |
| Trage verwerking bij grote bestanden | Hoge resolutie | Verklein de afbeelding eerst: `aocr.ImageFilters.resize(width=1200)` vóór binarisatie. |

---

## Verder gaan – Volgende stappen en gerelateerde onderwerpen

- **Batchverwerking**: Plaats de bovenstaande logica in een lus om tientallen bestanden automatisch te verwerken.  
- **Gestructureerde output**: Gebruik reguliere expressies op `ocr_result.text` om velden zoals datums of bedragen te extraheren.  
- **Alternatieve bibliotheken**: Vervang `aocr` door `pytesseract` — de code verandert alleen bij de engine‑initialisatie.  
- **Hoe afbeelding voor te verwerken voor PDF’s**: Converteer elke PDF‑pagina naar een afbeelding en pas vervolgens dezelfde pipeline toe.  

Deze uitbreidingen laten je de oplossing opschalen van één enkel formulier naar een enterprise‑grade document‑ingestie‑pipeline.

---

## Conclusie

We hebben **hoe OCR uit te voeren** van begin tot eind behandeld, laten zien **hoe afbeelding voor te verwerken** om **ruis te verminderen**, en demonstreren **hoe tekst uit een afbeelding te extraheren** met een schoon, reproduceerbaar script. De belangrijkste les? Een paar eenvoudige filters — binarisatie en median blur — kunnen een ruisvolle scan omzetten in een betrouwbare gegevensbron, waardoor je uren handmatige opschoning bespaart.

Probeer het script met je eigen documenten, pas de drempels aan, en zie de nauwkeurigheid stijgen. Wanneer je er klaar voor bent, verken batchverwerking of integreer de output in een database voor doorzoekbare archieven. Veel programmeerplezier, en moge je OCR altijd spot‑on zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}