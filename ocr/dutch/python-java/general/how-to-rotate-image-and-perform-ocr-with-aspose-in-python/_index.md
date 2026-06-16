---
category: general
date: 2026-03-26
description: Leer hoe je een afbeelding kunt roteren en OCR kunt uitvoeren in Python.
  Deze gids laat ook zien hoe je een afbeelding kunt voorbewerken voor OCR en efficiënt
  tekst uit een afbeelding kunt extraheren.
draft: false
keywords:
- how to rotate image
- how to perform ocr
- preprocess image for ocr
- recognize text from image
- how to extract text from image
language: nl
og_description: Hoe je een afbeelding correct draait en vervolgens tekst uit de afbeelding
  herkent met Aspose OCR. Volg deze stapsgewijze tutorial om de afbeelding voor OCR
  voor te bereiden en tekst uit de afbeelding te extraheren.
og_title: Hoe je een afbeelding roteert en OCR uitvoert – Complete Python-gids
tags:
- Aspose
- Python
- Image Processing
- OCR
title: Hoe een afbeelding te roteren en OCR uit te voeren met Aspose in Python
url: /nl/python-java/general/how-to-rotate-image-and-perform-ocr-with-aspose-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een afbeelding roteren en OCR uitvoeren met Aspose in Python

Heb je je ooit afgevraagd **hoe je een afbeelding moet roteren** zodat een OCR‑engine de tekst daadwerkelijk kan lezen? Misschien heb je een formulier gescand dat scheef staat, of heeft een foto 90° met de klok mee gedraaid. In dat geval ziet de tekst er voor het menselijk oog goed uit, maar de OCR‑engine ziet er een puinhoop uit. Het goede nieuws? Het is een fluitje van een cent om de oriëntatie te corrigeren, het gewenste gebied bij te snijden en vervolgens de tekst te extraheren — alles met een paar regels Python en Aspose‑bibliotheken.

In deze tutorial lopen we het volledige proces door: van het laden van een geroteerde TIFF, het corrigeren van de oriëntatie, **afbeelding voorbewerken voor OCR**, en uiteindelijk **tekst herkennen uit afbeelding**. Aan het einde weet je **hoe je OCR uitvoert** op elke afbeelding en kun je **tekst uit afbeelding**‑bestanden met vertrouwen **extraheren**.

## Wat je nodig hebt

- Python 3.8+ (de code werkt met elke recente versie)
- `asposeocrjava` en `asposeimaging` pakketten geïnstalleerd via `pip`
- Een voorbeeldafbeelding die geroteerd moet worden (bijv. `rotated_form.tif`)
- Een beetje nieuwsgierigheid naar beeldverwerking

Geen zware frameworks nodig — alleen de twee Aspose‑pakketten en een beetje Python‑logica.

---

## Stap 1: Installeer Aspose‑pakketten (Hoe OCR uit te voeren)

Voordat we **een afbeelding kunnen roteren** of **tekst uit afbeelding kunnen herkennen**, hebben we de bibliotheken nodig die het zware werk doen.

```bash
pip install asposeocrjava asposeimaging
```

> **Pro tip:** Als je achter een bedrijfsproxy zit, voeg `--proxy http://proxy:port` toe aan het commando. De pakketten zijn pure Python‑wrappers rond de Aspose .NET/Java‑core, dus de installatie is meestal direct.

---

## Stap 2: Laad het bronbestand en roteer het – De kernstap “Hoe een afbeelding roteren”

```python
from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

# Load the original, incorrectly oriented image
source_image = Image.load("YOUR_DIRECTORY/rotated_form.tif")

# Rotate 90° clockwise – this fixes the orientation for OCR
rotated_image = source_image.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)
```

> **Waarom roteren?** De meeste OCR‑engines gaan ervan uit dat tekst van links‑naar‑rechts en van boven‑naar‑onder loopt. Als de bitmap zijwaarts staat, zal de engine ofwel onzin teruggeven of helemaal niets. Roteren brengt het pixelrooster in lijn met de verwachte leesvolgorde, waardoor de nauwkeurigheid drastisch verbetert.

> **Randgeval:** Als je niet zeker weet of de afbeelding 90°, 180° of 270° moet draaien, kun je `source_image.width` vergelijken met `source_image.height` of de `exif`‑oriëntatietags gebruiken. Aspose’s `rotate_flip`‑methode ondersteunt ook `ROTATE_180` en `ROTATE_270_CLOCKWISE`.

> **Afbeeldingsvoorbeeld (optioneel):**  
> ![voorbeeld van hoe afbeelding te roteren](/assets/rotate-demo.png "Hoe een afbeelding roteren – vóór en na rotatie")

---

## Stap 3: Snijd het interessegebied bij – Afbeelding voorbewerken voor OCR

Vaak heb je slechts een klein deel van de pagina nodig — bijvoorbeeld een handtekeningveld of een blok cijfers. Bijsnijden verwijdert ruis en versnelt **hoe OCR uit te voeren**.

```python
# Define the rectangle that encloses the text you care about
# (x=100, y=200, width=800, height=300) – adjust to your form
roi = Rectangle(100, 200, 800, 300)

# Crop the rotated image to that rectangle
roi_image = rotated_image.crop(roi)
```

> **Waarom bijsnijden?** Het verkleinen van de afbeelding beperkt de zoekruimte van de OCR‑engine, waardoor valse positieven afnemen en de verwerkingstijd korter wordt. Het helpt ook als het bronbestand watermerken of andere grafische elementen bevat die de engine kunnen verwarren.

> **Tip:** Als je met meerdere velden werkt, herhaal dan de bijsnijdstap met verschillende rechthoeken en voer OCR afzonderlijk uit op elk deel.

---

## Stap 4: Initialiseert de OCR‑engine – De kern “Hoe OCR uit te voeren”

```python
# Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

> **Onder de motorkap:** Aspose OCR maakt gebruik van een combinatie van Tesseract en eigen beeldanalyse. Het één keer instantiëren van de engine en deze hergebruiken voor meerdere afbeeldingen is efficiënter dan telkens een nieuw object aan te maken.

---

## Stap 5: Voer de bijgesneden afbeelding in en herken de tekst – Hoe tekst uit afbeelding te extraheren

```python
# Set the cropped image as the input for OCR
ocr_engine.set_image(roi_image)

# Run the recognition process
result = ocr_engine.recognize()

# Extract the plain text
extracted_text = result.get_text()
print(extracted_text)
```

### Verwachte uitvoer

Bevat het ROI de zin “Invoice #12345 – Paid”, zie je iets als:

```
Invoice #12345 – Paid
```

Als de OCR moeite heeft, kun je extra spaties of verkeerd gelezen tekens krijgen (bijv. “Invo1ce #I2345 – Pa1d”). Dan komen **afbeelding voorbewerken voor OCR**‑trucs, zoals contrast aanpassen of binarisatie toepassen, in beeld. Aspose biedt extra filters die je vóór stap 5 kunt ketenen, maar de basisstroom werkt voor de meeste schone scans.

---

## Stap 6: Optioneel – Fijn afstellen van de OCR‑instellingen (Geavanceerd “Hoe OCR uit te voeren”)

Als je een hogere nauwkeurigheid nodig hebt voor een specifieke taal of bepaalde tekens wilt negeren, kun je de engine aanpassen:

```python
# Example: Restrict recognition to English alphanumerics only
ocr_engine.get_recognition_settings().set_recognition_language("en")
ocr_engine.get_recognition_settings().set_characters_blacklist("!@#$%^&*()")
```

> **Wanneer te gebruiken:** Gebruik dit wanneer het document veel decoratieve symbolen bevat die je niet nodig hebt. Een blacklist vermindert valse detecties.

---

## Volledig end‑to‑end‑script

Alles bij elkaar, hier is een kant‑en‑klaar script dat **hoe een afbeelding te roteren**, **afbeelding voorbewerken voor OCR**, en uiteindelijk **tekst uit afbeelding te herkennen** combineert:

```python
# -*- coding: utf-8 -*-
"""
Complete example: rotate, crop, and OCR an image with Aspose.
Author: Your Name
Date: 2026-03-26
"""

from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

def ocr_rotated_image(
    input_path: str,
    output_path: str = None,
    crop_rect: Rectangle = Rectangle(100, 200, 800, 300)
) -> str:
    """
    Loads an image, rotates it 90° clockwise, crops the region of interest,
    runs OCR, and returns the extracted text.

    Parameters
    ----------
    input_path : str
        Path to the original (possibly rotated) image file.
    output_path : str, optional
        If provided, saves the processed (rotated + cropped) image for inspection.
    crop_rect : Rectangle, optional
        Rectangle defining the ROI. Adjust to match your document layout.

    Returns
    -------
    str
        The plain text extracted from the ROI.
    """
    # Load and rotate
    src = Image.load(input_path)
    rotated = src.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)

    # Crop to region of interest
    roi = rotated.crop(crop_rect)

    # Optionally save the processed image for debugging
    if output_path:
        roi.save(output_path)

    # OCR
    engine = OcrEngine()
    engine.set_image(roi)
    result = engine.recognize()
    return result.get_text()

if __name__ == "__main__":
    text = ocr_rotated_image(
        "YOUR_DIRECTORY/rotated_form.tif",
        output_path="processed_roi.png"
    )
    print("=== Extracted Text ===")
    print(text)
```

Het uitvoeren van dit script print de herkende tekst naar de console en slaat een visueel overzicht van de verwerkte ROI op als `processed_roi.png`. Je kunt die PNG openen om te verifiëren dat rotatie en bijsnijden naar verwachting hebben gewerkt.

---

## Veelgestelde vragen & valkuilen

| Vraag | Antwoord |
|----------|--------|
| **Wat als de afbeelding al rechtop staat?** | De rotatiestap is idempotent — een correct georiënteerde afbeelding 90° roteren zou deze uiteraard kapot maken, dus controleer `source_image.width` versus `height` of gebruik EXIF‑oriëntatiedata voordat je `rotate_flip` aanroept. |
| **Mijn OCR‑output bevat extra regeleinden.** | Gebruik `result.get_text().replace("\n", " ").strip()` om op te schonen, of schakel `ocr_engine.get_recognition_settings().set_remove_line_breaks(True)` in. |
| **Kan ik PDF‑bestanden direct verwerken?** | Ja — Aspose Imaging kan PDF‑pagina’s laden als afbeeldingen (`Image.load("file.pdf")`), waarna je dezelfde rotatie‑ en OCR‑stappen volgt. |
| **Is er een manier om veel bestanden in één keer te verwerken?** | Plaats `ocr_rotated_image` in een lus over een map, of gebruik Python’s `concurrent.futures` om parallel te verwerken. |
| **Hoe ga ik om met andere talen dan Engels?** | Stel de herkenningstaal in via `ocr_engine.get_recognition_settings().set_recognition_language("fr")` voor Frans, enzovoort. |

---

## Conclusie

We hebben behandeld **hoe je een afbeelding correct roteert**, **afbeelding voorbewerkt voor OCR** door bij te snijden, en uiteindelijk **hoe je OCR uitvoert** om **tekst uit afbeelding** te **herkennen** en **extraheren** met Aspose’s Python‑bibliotheken. Het volledige script toont een praktisch, productie‑klaar workflow die je in elke automatiseringspipeline kunt opnemen.

Wil je verder gaan, probeer dan te experimenteren met:

- **Beeldverbetering** (contrast, binarisatie) vóór OCR
- **Meerdere ROI‑extracties** voor formulieren met verschillende velden
- **Batchverwerking** van volledige mappen gescande documenten
- **Integratie** met downstream‑systemen (bijv. geëxtraheerde data in een database)

Voel je vrij om de code aan te passen aan jouw eigen use‑case, en happy coding! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}