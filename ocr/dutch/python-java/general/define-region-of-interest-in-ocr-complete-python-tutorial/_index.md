---
category: general
date: 2026-06-16
description: Definieer het interessegebied in OCR om Spaanse tekst van identiteitskaarten
  te extraheren. Leer hoe je een afbeelding laadt voor OCR en het ROI efficiënt specificeert.
draft: false
keywords:
- define region of interest
- load image for ocr
- how to specify roi
- extract id card text
- extract spanish text image
language: nl
og_description: Definieer de regio van interesse in OCR om Spaanse tekst van identiteitskaarten
  te extraheren. Stapsgewijze handleiding voor het laden van afbeeldingen en het specificeren
  van de ROI.
og_title: Definieer interessegebied in OCR – Complete Python‑tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Define region of interest in OCR to extract Spanish text from ID cards.
    Learn how to load image for OCR and specify ROI efficiently.
  headline: Define region of interest in OCR – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Definieer interessegebied in OCR – Complete Python‑tutorial
url: /nl/python-java/general/define-region-of-interest-in-ocr-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definieer regio van interesse in OCR – Complete Python Tutorial

Heb je je ooit afgevraagd hoe je **define region of interest in OCR** kunt definiëren zodat je alleen het deel van een afbeelding leest dat je echt nodig hebt? In deze tutorial lopen we je precies dat stap voor stap door, en laten we je zien hoe je **load image for OCR** kunt doen en Spaanse tekst van een identiteitskaart kunt extraheren in slechts een paar regels Python.  

Als je ooit naar een ruisvolle scan hebt gekeken en dacht: “Er moet een schonere manier zijn om het naamveld te pakken,” dan ben je hier op de juiste plek. Aan het einde kun je de tekst van de identiteitskaart die je nodig hebt ophalen zonder te struikelen over achtergrondruis.

## Wat je zult leren

- Waarom je **define region of interest** moet doen voordat je OCR uitvoert.  
- De exacte stappen om **load image for OCR** te gebruiken met een populaire Python OCR-wrapper.  
- Hoe je **how to specify ROI** kunt instellen met pixelcoördinaten.  
- Manieren om **extract id card text** betrouwbaar te extraheren, zelfs wanneer de brontaal Spaans is.  
- Tips voor het omgaan met randgevallen zoals gedraaide kaarten of scans met weinig contrast.  

Er is geen eerdere OCR‑ervaring vereist — alleen een werkende Python 3‑omgeving en een JPEG van een identiteitskaart die je wilt testen.

---

![Define region of interest illustration](placeholder.png){alt="Define region of interest example showing a highlighted rectangle on an ID card image"}

## Stap 1: Installeer en importeer de OCR‑bibliotheek

Allereerst heb je een bibliotheek nodig die een `OcrEngine`‑klasse exposeert, vergelijkbaar met de snippet die je eerder zag. Voor deze gids gebruiken we het fictieve `ocr`‑pakket, maar dezelfde concepten gelden voor `pytesseract`, `easyocr`, of elke wrapper die je een taal en een ROI laat instellen.

```bash
pip install ocr   # Replace with the actual package name you use
```

```python
# Import the library and any helper classes
import ocr
from ocr import Rectangle, Image
```

*Pro tip:* Als je `pytesseract` gebruikt, wordt de `Rectangle`‑klasse een eenvoudige tuple `(left, top, width, height)`. De rest van de workflow blijft identiek.

## Stap 2: Laad afbeelding voor OCR

Nu **load image for OCR**. De engine verwacht een `ocr.Image`‑object, dus wijzen we hem naar het bestand dat de identiteitskaart bevat. Zorg ervoor dat het pad absoluut is of relatief ten opzichte van de werkmap van je script.

```python
# Create the OCR engine instance
engine = ocr.OcrEngine()

# Tell the engine which language we’re interested in – Spanish in this case
engine.language = ocr.Language.SPANISH

# Load the source image that contains the text to be recognized
engine.image = Image.load_from_file("YOUR_DIRECTORY/id-card.jpg")
```

Als de afbeelding enorm is, overweeg dan eerst te verkleinen; OCR‑engines werken sneller op afbeeldingen onder 1500 px breed.

## Stap 3: Hoe ROI opgeven (Definieer regio van interesse)

Hier is het hart van de tutorial: **how to specify ROI**. Een regio van interesse is simpelweg een rechthoek die de OCR‑engine vertelt: “Kijk alleen binnen deze pixelgrenzen.” Zie het als een vakje om het naamveld op een identiteitskaart te tekenen.

```python
# Define the region of interest – left, top, width, height (all in pixels)
engine.region_of_interest = Rectangle(
    left=120,   # X‑coordinate of the left edge
    top=80,     # Y‑coordinate of the top edge
    width=340,  # Width of the box
    height=200  # Height of the box
)
```

Waarom die getallen? In onze voorbeeldafbeelding staat de naam ongeveer 120 px vanaf de linkerrand en 80 px vanaf de bovenkant. Pas ze aan zodat ze overeenkomen met de lay-out van de kaarten die jij verwerkt.  

*Randgeval:* Als de kaart 90° gedraaid is, verwissel `width` en `height` en pas `left`/`top` dienovereenkomstig aan, of roteer de afbeelding vooraf met Pillow voordat je deze aan de engine geeft.

## Stap 4: Voer OCR uit binnen de ROI

Met de ROI gedefinieerd negeert de engine alles buiten het rechthoekige gebied. Dit versnelt de verwerking en vermindert vals-positieve resultaten veroorzaakt door achtergrondgrafieken.

```python
# Run OCR only inside the defined ROI
roi_result = engine.recognize()
```

De `recognize()`‑aanroep retourneert een object dat de herkende tekst, vertrouwensscores en begrenzingskaders voor elk woord bevat.

## Stap 5: Exporteer identiteitskaart‑tekst (en verifieer Spaanse output)

Tot slot **extract id card text** uit het ROI‑resultaat en printen we het. Omdat we eerder de taal op Spaans hebben ingesteld, zal de OCR‑engine taalspecifieke woordenboeken toepassen, wat de nauwkeurigheid verbetert voor tekens met accenten zoals “ñ” of “á”.

```python
# Output the recognized text from the ROI
print("ROI text:", roi_result.text)
```

### Verwachte output

```
ROI text: JUAN PÉREZ GARCÍA
```

Als je onleesbare tekens ziet, controleer dan of de afbeelding daadwerkelijk Spaans is en of de taalbestanden van de OCR‑bibliotheek geïnstalleerd zijn.

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Symptoom | Waarschijnlijke oorzaak | Oplossing |
|----------|--------------------------|-----------|
| Lege string geretourneerd | ROI snijdt geen tekst | Controleer de coördinaten met een afbeeldingsviewer; gebruik `engine.debug_draw_roi()` indien beschikbaar. |
| Veel rommelige tekens | Verkeerd taalpakket | Installeer het Spaanse taalbestand opnieuw of schakel over naar `ocr.Language.AUTO`. |
| Lage vertrouwensscores | Afbeelding is wazig of heeft weinig contrast | Preprocess met OpenCV – pas `cv2.GaussianBlur` en `cv2.threshold` toe. |
| OCR draait over de hele afbeelding ondanks ROI | Oudere bibliotheekversie | Upgrade naar de nieuwste `ocr`‑package; oudere versies negeerden ROI. |

## Uitbreiding: Meerdere ROI’s

Soms moet je meer dan één veld ophalen (bijv. naam en ID‑nummer). Het patroon blijft hetzelfde: wijzig `engine.region_of_interest` en roep opnieuw `recognize()` aan.

```python
# ROI for the ID number (different coordinates)
engine.region_of_interest = Rectangle(120, 300, 340, 80)
id_result = engine.recognize()
print("ID Number:", id_result.text)
```

Je kunt ook een lijst met rechthoeken batch‑verwerken als de bibliotheek dat ondersteunt, wat een extra ronde naar de OCR‑engine bespaart.

## Volledig werkend script

Alles bij elkaar, hier is een kant‑klaar script dat **defines region of interest**, **loads image for OCR**, en **extracts Spanish text** van een identiteitskaart.

```python
import ocr
from ocr import Rectangle, Image

def extract_name_from_id(image_path):
    """
    Loads an image, defines a ROI around the name field,
    runs OCR in Spanish, and returns the recognized text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.SPANISH
    engine.image = Image.load_from_file(image_path)

    # Adjust these numbers to match your card layout
    engine.region_of_interest = Rectangle(left=120, top=80, width=340, height=200)

    result = engine.recognize()
    return result.text.strip()

if __name__ == "__main__":
    name = extract_name_from_id("YOUR_DIRECTORY/id-card.jpg")
    print("Extracted Name:", name)
```

Voer het script uit en je zou de naam in de console moeten zien verschijnen. Pas de rechthoekwaarden aan om andere velden te targeten, en je hebt een herbruikbare utility voor elk document van het type identiteitskaart.

## Volgende stappen

- **Batchverwerking:** Loop door een map met identiteitskaarten en sla elke geëxtraheerde naam op in een CSV‑bestand.  
- **Taaldetectie:** Laat de gebruiker de taal dynamisch kiezen; `ocr.Language.AUTO` kan handig zijn.  
- **Nabewerking:** Pas regex‑patronen toe om veelvoorkomende OCR‑fouten te corrigeren (bijv. vervang “0” door “O” wanneer het in namen voorkomt).  

Door te leren hoe je **define region of interest** kunt gebruiken, heb je een krachtige manier ontgrendeld om **extract id card text** snel en nauwkeurig te doen, vooral bij documenten in het Spaans.

---

### TL;DR

We hebben je laten zien hoe je **define region of interest in OCR**, **load image for OCR**, en **how to specify ROI** kunt gebruiken om **extract spanish text image** van een identiteitskaart te halen. Het volledige voorbeeld draait in minder dan een minuut en kan met een paar coördinatiewijzigingen op elke lay-out worden aangepast. Probeer het, pas de rechthoek aan, en zie hoe OCR zich richt als een laser.

Happy coding!


## Wat moet je hierna leren?


De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementaties in je eigen projecten te verkennen.

- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}