---
category: general
date: 2026-06-22
description: Voer OCR uit op een afbeelding met Python in slechts een paar regels.
  Leer hoe je een afbeelding laadt voor OCR, tekst herkent uit een PNG en de OCR-engine
  efficiënt gebruikt.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- load image for OCR
- use OCR engine
language: nl
og_description: Voer snel OCR uit op een afbeelding met Python. Deze tutorial laat
  zien hoe je een afbeelding laadt voor OCR, tekst herkent uit een PNG, en de OCR-engine
  met vertrouwen gebruikt.
og_title: Voer OCR uit op afbeelding in Python – Stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Python in just a few lines. Learn how to
    load image for OCR, recognize text from PNG, and use OCR engine efficiently.
  headline: Perform OCR on Image in Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: OCR uitvoeren op afbeelding in Python – Complete gids
url: /nl/python-java/general/perform-ocr-on-image-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Voer OCR uit op afbeelding in Python – Complete gids

Heb je ooit **perform OCR on image** bestanden moeten verwerken maar zat je vast bij de allereerste regel code? Je bent niet de enige. In deze walkthrough laten we je precies zien hoe je **load image for OCR** kunt doen, een lichte **OCR engine** instelt, en uiteindelijk **recognize text from PNG** met slechts een handvol commando's.

We behandelen alles, van het installeren van de bibliotheek tot het aanpassen van de whitelist zodat alleen cijfers en hoofdletters de scan overleven. Aan het einde heb je een kant‑klaar script dat je in elk project kunt gebruiken—geen mysterie, geen extra poespas.

## Wat je zult leren

- Hoe je **use OCR engine** programmatisch in Python kunt gebruiken.  
- De exacte stappen om **load image for OCR** uit een lokale map te laden.  
- Waarom en hoe je herkenning beperkt tot een aangepaste tekenset.  
- Hoe je **recognize text from PNG** kunt uitvoeren en het resultaat veilig afhandelt.  

**Prerequisites:** Python 3.7+ geïnstalleerd, een terminal waar je vertrouwd mee bent, en een afbeelding (bijv. `serial-number.png`) die je wilt lezen. Geen eerdere OCR-ervaring vereist.

---

## OCR uitvoeren op afbeelding – Initialiseer de OCR-engine

Het eerste dat je moet doen is een instantie van de OCR-engine maken. Beschouw de engine als het brein dat de pixels analyseert en ze omzet in tekens.

```python
import ocr  # Assuming the OCR library is named `ocr`

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Why this matters:* Zonder een engine is er niets om de afbeelding te verwerken. De `OcrEngine`‑klasse bundelt al het zware werk—pre‑processing, segmentatie en karakterclassificatie—in één object dat je kunt hergebruiken.

---

## Afbeelding laden voor OCR – Lever het PNG‑bestand

Nu de engine bestaat, moet je hem de afbeelding geven die je wilt lezen. De bibliotheek verwacht een `ImageStream`‑object, dat je direct vanuit een bestandspad kunt maken.

```python
# Step 2: Load the image to be processed
image_path = "YOUR_DIRECTORY/serial-number.png"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

*Pro tip:* Houd de afbeelding in een hoog‑contrastformaat (zwarte tekst op witte achtergrond) en vermijd compressie‑artefacten; die kunnen de OCR‑algoritme in de war brengen.

---

## Tekens beperken – Whitelist cijfers en hoofdletters

Vaak ben je alleen geïnteresseerd in een subset van tekens—bijvoorbeeld een serienummer dat alleen A‑Z en 0‑9 bevat. Door een whitelist in te stellen, vertel je de engine alles behalve die tekens te negeren, wat de nauwkeurigheid aanzienlijk verbetert.

```python
# Step 3: Restrict recognition to digits and uppercase letters
whitelist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
engine.get_settings().set_whitelist(whitelist)
```

*What’s happening under the hood?* De engine bouwt een filter dat elk glyph dat niet in de whitelist voorkomt, verwijdert vóór de uiteindelijke classificatiefase. Dit is vooral handig wanneer de afbeelding ruis of decoratieve tekst bevat die je niet nodig hebt.

---

## Tekst herkennen uit PNG – Voer het OCR‑proces uit

Met de engine klaar en de afbeelding geladen, kun je eindelijk **perform OCR on image**. De `recognize()`‑aanroep voert de volledige pijplijn uit en retourneert een result‑object.

```python
# Step 4: Perform OCR on the image
result = engine.recognize()
```

Als je nieuwsgierig bent naar de prestaties, voltooit de methode doorgaans binnen enkele honderden milliseconden voor een 300 × 200 px PNG op een moderne laptop.

---

## Output en verificatie – Haal de herkende tekst op

De laatste stap is om de platte tekst uit het result‑object te extraheren. Alles wat niet overeenkomt met de whitelist wordt automatisch verwijderd, zodat je een schone string krijgt die klaar is voor verdere verwerking.

```python
# Step 5: Output the recognized text (characters outside the whitelist are ignored)
recognized_text = result.get_text()
print(recognized_text)
```

*Typical output:* `AB12C3D4E5` (ervan uitgaande dat de afbeelding dat exacte serienummer bevatte).  

Als de output leeg of onsamenhangend is, controleer dan de beeldkwaliteit en de whitelist; een veelvoorkomende valkuil is per ongeluk benodigde tekens weglaten.

---

## Randgevallen & Veelvoorkomende valkuilen

| Situation | What to Check | Suggested Fix |
|-----------|---------------|---------------|
| **File not found** | Padtypefout of ontbrekend bestand | Gebruik `os.path.abspath` om het volledige pad te verifiëren voordat je `set_image` aanroept. |
| **Low contrast image** | Tekst gaat op in de achtergrond | Pas een eenvoudige drempel toe (`Pillow` of `OpenCV`) voordat je de afbeelding aan de engine levert. |
| **Unexpected characters** | Whitelist te restrictief | Voeg de ontbrekende tekens toe aan de whitelist‑string. |
| **Large images** | Trage herkenning | Verklein de afbeelding tot maximaal 1024 px breedte; OCR‑kwaliteit blijft meestal hoog. |

---

## Volledig script – Klaar om uit te voeren

Hieronder staat het volledige, zelfstandige script dat alle onderdelen samenvoegt. Sla het op als `ocr_demo.py`, vervang `YOUR_DIRECTORY` door de daadwerkelijke map, en voer `python ocr_demo.py` uit.

```python
import ocr
import os

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a PNG image and return the recognized text.
    Only uppercase letters and digits are allowed.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Load the PNG image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # Whitelist: A-Z and 0-9
    engine.get_settings().set_whitelist("ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

    # Run recognition
    result = engine.recognize()

    # Return clean text
    return result.get_text()

if __name__ == "__main__":
    # Adjust the path to point to your PNG file
    png_path = "YOUR_DIRECTORY/serial-number.png"
    try:
        text = perform_ocr(png_path)
        print("Recognized text:", text)
    except Exception as e:
        print("Error during OCR:", e)
```

*Verwachte console‑output* (wanneer de PNG `SN12345` bevat):

```
Recognized text: SN12345
```

---

## Conclusie

Je weet nu precies hoe je **perform OCR on image** bestanden in Python kunt verwerken, van **load image for OCR** tot **recognize text from PNG** en uiteindelijk een schoon resultaat extraheren met een aanpasbare **OCR engine**. De aanpak is eenvoudig, uitbreidbaar en werkt direct uit de doos voor de meeste scans in serienummer‑stijl.

Wat nu? Probeer de whitelist te vervangen door kleine letters, experimenteer met verschillende afbeeldingsformaten (JPEG, BMP), of integreer het script in een batch‑verwerkingspipeline. Hetzelfde patroon—engine → afbeelding → instellingen → herkennen → output—geldt voor vrijwel elke OCR‑taak die je tegenkomt.

Heb je vragen of een eigenzinnige afbeelding die niet wil meewerken? Laat een reactie achter hieronder, en happy coding! 

![Diagram dat de stappen toont om OCR uit te voeren op afbeelding met Python](https://example.com/ocr-flow.png "Diagram dat laat zien hoe OCR uit te voeren op afbeelding met een Python OCR-engine")


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Afbeelding omzetten naar tekst – OCR uitvoeren op afbeelding vanaf URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Hoe AspOCR te gebruiken: afbeelding voorbewerken met OCR-filters voor .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Hoe tekst uit afbeelding te extraheren door rechthoeken voor te bereiden in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}