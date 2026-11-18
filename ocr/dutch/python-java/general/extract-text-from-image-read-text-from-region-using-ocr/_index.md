---
category: general
date: 2026-07-05
description: Tekst uit afbeelding halen met Python OCR. Leer hoe je een afbeelding
  laadt voor OCR, tekst uit een regio leest en tekst uit een factuur extraheert met
  een paar regels code.
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: nl
og_description: Haal tekst uit een afbeelding met Python OCR. Deze gids laat zien
  hoe je een afbeelding laadt voor OCR, tekst uit een regio leest en snel tekst uit
  een factuur extraheert.
og_title: Tekst uit afbeelding extraheren – Tekst uit regio lezen met OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Tekst extraheren uit afbeelding – Tekst lezen uit een gebied met OCR
url: /nl/python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst uit afbeelding extraheren – Tekst lezen uit regio met OCR

Heb je ooit **tekst uit afbeelding extraheren** moeten, maar alleen een specifiek deel is relevant—zoals het totaalbedrag op een factuur? Je bent niet de enige. In veel praktijkprojecten zul je merken dat je **tekst uit regio lezen** moet in plaats van de hele afbeelding te analyseren. Gelukkig kun je met een paar regels Python een afbeelding laden voor OCR, een region of interest (ROI) definiëren, en precies de tekens die je nodig hebt extraheren.

In deze tutorial lopen we een compleet, uitvoerbaar voorbeeld door dat laat zien hoe je **afbeelding voor OCR laadt**, een ROI instelt, en uiteindelijk **tekst uit factuur extraheren**. Aan het einde heb je een kant‑klaar fragment dat werkt met elke populaire OCR‑bibliotheek die region‑gebaseerde herkenning ondersteunt.

---

## Wat je nodig hebt

- Python 3.8+ (de code werkt ook op 3.10)  
- Een OCR‑pakket dat een `OcrEngine`‑klasse exposeert (voor de demo gebruiken we een fictieve `ocr`‑module; vervang deze door `pytesseract`, `easyocr`, of een andere bibliotheek die ROI‑ondersteuning biedt)  
- Een voorbeeldafbeelding—bijv. `invoice.png`—die duidelijke, gedrukte tekst bevat  
- Basiskennis van Python‑functies en -klassen (geen deep‑learning‑achtergrond vereist)

Als je deze al hebt, prima—laten we beginnen. Zo niet, download dan de nieuwste Python van python.org en installeer het OCR‑pakket via `pip install your-ocr-lib`.

![Voorbeeld van tekst uit afbeelding extraheren](extract-text-from-image.png "Tekst uit afbeelding – region‑gebaseerde OCR‑demo")

*De afbeelding hierboven illustreert de regio (rode rechthoek) die we zullen targeten om **tekst uit afbeelding te extraheren**.*

---

## Stap 1: Installeer en importeer de OCR‑bibliotheek

Zorg er eerst voor dat de OCR‑bibliotheek beschikbaar is in je omgeving. Het import‑patroon hieronder werkt voor de meeste pakketten die een high‑level `OcrEngine`‑klasse exposeeren.

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **Pro tip:** Als je `pytesseract` gebruikt, moet je de Tesseract‑binary apart installeren en `pytesseract.pytesseract.tesseract_cmd` naar het pad ervan instellen.

---

## Stap 2: Maak de OCR‑engine aan en stel de taal in

Het aanmaken van de engine is eenvoudig, maar het specificeren van de taal verbetert de nauwkeurigheid aanzienlijk, vooral voor facturen die cijfers en Engelse woorden bevatten.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

Waarom doen we dit? De OCR‑engine gebruikt taalkundige modellen om tekens te voorspellen; door aan te geven dat Engels verwacht wordt, worden valse positieven zoals het verwarren van “0” met “O” verminderd.

---

## Stap 3: Laad afbeelding voor OCR

Nu **laden we daadwerkelijk de afbeelding voor OCR**. De meeste bibliotheken accepteren een bestands‑pad of een Pillow‑afbeeldingsobject. Hier gebruiken we de ingebouwde loader van de bibliotheek voor de eenvoud.

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

Zorg ervoor dat het pad naar de juiste map wijst; een veelgemaakte fout is het vergeten van het relatieve pad wanneer het script vanuit een andere werkmap wordt uitgevoerd.

---

## Stap 4: Definieer de Region of Interest (ROI)

Het definiëren van de ROI is de kern van **tekst uit regio lezen**. Beschouw het als het tekenen van een rechthoek rond het deel van de factuur dat het totaalbedrag bevat.

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left` en `top` vertegenwoordigen de X‑ en Y‑coördinaten van de linkerbovenhoek van de rechthoek.  
- `width` en `height` bepalen de grootte van de doos.  
- Je kunt experimenteren met verschillende waarden met een afbeeldingsviewer die pixelcoördinaten toont.

> **Waarom ROI belangrijk is:** OCR uitvoeren op de hele pagina verspilt CPU‑cycli en introduceert vaak ruis van niet‑relevante tekst, tabellen of grafische elementen. Door je te richten op een regio krijg je schonere resultaten en snellere verwerking.

---

## Stap 5: Voer OCR uit op de gespecificeerde regio

Met alles ingesteld, **extraheren we eindelijk tekst uit afbeelding**—maar alleen binnen de ROI die we hebben gedefinieerd.

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

De `recognize`‑methode retourneert een object dat doorgaans de ruwe string, vertrouwensscores, en soms begrenzings‑boxen voor elk woord bevat. Voor ons doel hebben we alleen de platte tekst nodig.

---

## Stap 6: Output de geëxtraheerde tekst

Laten we het resultaat afdrukken en zien wat we hebben. Deze stap demonstreert **tekst uit factuur extraheren** in een real‑world scenario.

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### Verwachte output

```
Text inside ROI:
Total Amount: $1,245.67
```

Als je factuur een andere lay-out heeft, zie je welke tekst er binnen de rechthoek staat—mogelijk een factuurnummer, datum, of PO‑referentie.

---

## Stap 7: Verpak alles in een herbruikbare functie (optioneel)

Om de oplossing herbruikbaar te maken voor meerdere facturen, kapsel je de logica in een functie. Dit illustreert ook **ocr op regio** als een generieke utility.

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

Je kunt nu de functie aanroepen met elke factuur:

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

---

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| **Lege output** | ROI dekt eigenlijk geen tekst (verkeerde coördinaten). | Controleer pixelwaarden met een afbeeldingeditor; voeg een visuele debug‑overlay toe. |
| **Onzinnige tekens** | Lage beeldresolutie of slecht contrast. | Pre‑process het beeld: converteer naar grijswaarden, pas drempelwaarde toe (`cv2.threshold`). |
| **Verkeerde taal** | Engine gebruikt standaard een taal zonder het benodigde teken‑set. | Stel expliciet `ocr_engine.language` in op `ENGLISH` of de juiste locale. |
| **Prestatie‑vertraging** | OCR herhaaldelijk uitvoeren op grote afbeeldingen. | Verklein de afbeelding vóór het laden, of verwerk alleen de ROI door eerst bij te snijden. |

---

## Voorbeeld uitbreiden: Meerdere ROI’s

Soms bevat een factuur meerdere velden die je nodig hebt—zoals **tekst uit factuur extraheren** voor zowel het totaalbedrag als de factuurdatum. Je kunt over een lijst van rechthoeken itereren:

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

Dit patroon houdt je code overzichtelijk en maakt het eenvoudig om later meer regio’s toe te voegen.

---

## Conclusie

We hebben zojuist een volledige end‑to‑end workflow behandeld om **tekst uit afbeelding te extraheren** met Python OCR, gericht op een specifieke regio. Door **afbeelding voor OCR te laden**, een **region of interest** te definiëren, en de engine aan te roepen, kun je betrouwbaar **tekst uit regio lezen**—perfect om totalen van facturen, data van bonnetjes, of andere gelokaliseerde gegevens te halen.  

Voel je vrij om te experimenteren

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Tekst uit afbeelding extraheren met Aspose OCR – Stapsgewijze gids](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Tekst uit afbeelding extraheren – OCR‑optimalisatie met Aspose.OCR voor .NET](/ocr/english/net/ocr-optimization/)
- [Hoe tekst uit afbeelding extraheren door rechthoeken voor te bereiden in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}