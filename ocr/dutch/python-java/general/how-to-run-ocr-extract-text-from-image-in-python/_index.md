---
category: general
date: 2026-03-26
description: Hoe OCR uit te voeren op een PNG‑bestand en tekst uit een afbeelding
  te extraheren met een aangepast woordenboek voor verbeterde OCR‑nauwkeurigheid.
  Leer hoe je een afbeelding snel voor OCR laadt.
draft: false
keywords:
- how to run OCR
- extract text from image
- recognize text from png
- improve OCR accuracy
- load image for OCR
language: nl
og_description: Hoe OCR uit te voeren op een PNG‑bestand en tekst uit een afbeelding
  te extraheren met een aangepast woordenboek voor verbeterde OCR‑nauwkeurigheid.
  Stapsgewijze handleiding.
og_title: Hoe OCR uit te voeren – Tekst uit afbeelding extraheren in Python
tags:
- OCR
- Python
- Image Processing
title: Hoe OCR uit te voeren – Tekst uit een afbeelding halen in Python
url: /nl/python-java/general/how-to-run-ocr-extract-text-from-image-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR uit te voeren – Tekst extraheren uit afbeelding in Python

Heb je je ooit afgevraagd **hoe je OCR kunt uitvoeren** op een gescande factuur of een screenshot en schone, doorzoekbare tekst te krijgen? Je bent niet de enige. In veel projecten is de bottleneck simpelweg het laden van de afbeelding voor OCR en vervolgens de engine overtuigen om domeinspecifieke woorden te begrijpen.  

In deze tutorial lopen we een compleet, kant‑klaar voorbeeld door dat **tekst uit afbeelding** bestanden extraheert, je laat zien hoe je **tekst uit PNG** assets herkent, en zelfs trucjes demonstreert om **OCR‑nauwkeurigheid te verbeteren** met aangepaste woordenboeken en speciale tekens. Aan het einde heb je een zelfstandige script die je in elke Python‑codebase kunt plaatsen.

## Wat je nodig hebt

- Python 3.8+ (de code gebruikt type hints maar werkt op eerdere 3.x‑versies)
- De `ocr`‑bibliotheek die wordt meegeleverd met de OCR‑engine die je target (installeer via `pip install ocr‑engine` – vervang door de daadwerkelijke pakketnaam)
- Een afbeeldingsbestand (`input.png`) dat je wilt verwerken
- Optioneel: een platte‑tekst‑bestand (`invoice_terms.txt`) met domeinspecifieke woorden, één per regel

Geen zware externe afhankelijkheden, geen cloud‑API‑sleutels, alleen een lokale OCR‑engine.

---

## Stap 1: Installeer en importeer de OCR‑bibliotheek

Zorg er eerst voor dat het OCR‑pakket geïnstalleerd is. Als je het hypothetische `ocr-engine`‑pakket gebruikt, voer dan uit:

```bash
pip install ocr-engine
```

Importeer nu de klassen die je nodig hebt:

```python
# Step 1: Import the OCR SDK
import ocr
from ocr import Imaging
```

> **Pro tip:** Als je in een virtuele omgeving werkt, activeer deze dan vóór het installeren om je globale Python schoon te houden.

## Stap 2: Maak een OCR‑engine‑instantie

Het maken van een engine‑object is het startpunt voor elke OCR‑taak. Beschouw het als het inschakelen van de scanner‑hardware in software.

```python
# Step 2: Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
```

Waarom dit belangrijk is: de engine bevat configuratie zoals taal‑pakketten, herkenningsmodi en eventuele aangepaste bronnen die je later toevoegt. Zonder deze kun je niet **image for OCR laden** of de herkennings‑pipeline uitvoeren.

## Stap 3: Laad de afbeelding die je wilt herkennen

Hier **laden we de afbeelding voor OCR** daadwerkelijk. De methode `Imaging.Image.load()` leest het bestand en zet het om naar het interne bitmap‑formaat dat de engine verwacht.

```python
# Step 3: Load the PNG image you want to process
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Imaging.Image.load(image_path))
```

Als je een JPEG of TIFF hebt, werkt dezelfde methode — wijzig alleen de extensie. De engine detecteert het formaat automatisch.

> **Randgeval:** Zeer grote afbeeldingen (meer dan 5 MP) kunnen geheugenpieken veroorzaken. Overweeg te down‑scalen met Pillow voordat je laadt als je prestatie‑problemen ondervindt.

## Stap 4: Lever een aangepast woordenboek om de nauwkeurigheid te verhogen

De meeste OCR‑engines worden geleverd met generieke taalmodellen. Voor facturen, bonnetjes of juridische documenten zie je vaak gemiste woorden. Het leveren van een aangepaste woordenlijst vertelt de engine “deze termen zijn legitiem, behandel ze als correct”.

```python
# Step 4: Attach a custom dictionary (one word per line)
custom_dict_path = "YOUR_DIRECTORY/invoice_terms.txt"
ocr_engine.set_custom_dictionary(custom_dict_path)
```

Typische invoer kan zijn:

```
VAT
InvoiceNumber
Øre
ß
Ħ
```

Het toevoegen hiervan verbetert de **improve OCR accuracy**‑metric dramatisch — vooral voor niet‑ASCII‑symbolen.

## Stap 5: Voeg speciale tekens toe die niet in de standaardset zitten

Als je domein symbolen gebruikt zoals het Euro‑teken (€) of de Scandinavische Ø, kun je ze expliciet toevoegen:

```python
# Step 5: Register additional characters
ocr_engine.add_custom_characters("ØßĦ")
```

De engine zal die glyphs nu als geldig behandelen tijdens de herkenningsfase, waardoor de kans op “rommel” output afneemt.

## Stap 6: Voer het OCR‑proces uit en haal de tekst op

Roep tenslotte de recognizer aan en haal het platte‑tekstresultaat op. De `recognize()`‑aanroep retourneert een rijk object; we hebben alleen de ruwe string nodig voor de meeste use‑cases.

```python
# Step 6: Execute OCR and print the result
result = ocr_engine.recognize()
print("=== Recognized Text ===")
print(result.get_text())
```

**Verwachte output** (afgekapt voor beknoptheid):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total: €1,250.00
VAT: 25%
...
```

Als de output er rommelig uitziet, controleer dan dubbel of je aangepaste woordenboek en speciale tekens correct geladen zijn.

---

## Visueel overzicht

![diagram hoe OCR uit te voeren](ocr-workflow.png){alt="diagram hoe OCR uit te voeren"}

Het diagram hierboven illustreert de stroom van het laden van een afbeelding tot het verkrijgen van schone tekst, en benadrukt waar je aangepaste woordenboeken en tekensets kunt injecteren.

---

## Veelgestelde vragen & valkuilen

### Werkt dit met multi‑page PDF’s?

Ja — converteer elke pagina gewoon naar een PNG (met `pdf2image` of iets dergelijks) en voer ze opeenvolgend in dezelfde `ocr_engine`‑instantie. De engine verwerkt elke afbeelding onafhankelijk, zodat je een lijst van strings krijgt die je kunt samenvoegen.

### Wat als de afbeelding gedraaid is?

De meeste moderne OCR‑engines detecteren de oriëntatie automatisch, maar je kunt een rotatie forceren met:

```python
ocr_engine.set_image(Imaging.Image.load(image_path).rotate(90))
```

### Hoe om te gaan met andere talen dan Engels?

Vervang het taalmodel voordat je de afbeelding laadt:

```python
ocr_engine.set_language("de")  # German
```

Zorg ervoor dat het bijbehorende taalpakket geïnstalleerd is.

---

## Volledig script – Klaar om te kopiëren & plakken

Hieronder staat het volledige programma, klaar om te draaien nadat je de placeholder‑paden hebt vervangen.

```python
#!/usr/bin/env python3
"""
How to Run OCR – Complete example that extracts text from a PNG,
uses a custom dictionary, and adds special characters for better accuracy.
"""

# Install the OCR package first:
# pip install ocr-engine

import ocr
from ocr import Imaging

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = ocr.OcrEngine()

    # 2️⃣ Load the image you want to recognize
    image_path = "YOUR_DIRECTORY/input.png"      # <-- change this
    ocr_engine.set_image(Imaging.Image.load(image_path))

    # 3️⃣ Provide a custom dictionary (optional but recommended)
    dict_path = "YOUR_DIRECTORY/invoice_terms.txt"   # one word per line
    ocr_engine.set_custom_dictionary(dict_path)

    # 4️⃣ Add any special characters not covered by the default set
    ocr_engine.add_custom_characters("ØßĦ")   # e.g., currency symbols

    # 5️⃣ Run the OCR process
    result = ocr_engine.recognize()

    # 6️⃣ Output the recognized text
    print("=== Recognized Text ===")
    print(result.get_text())

if __name__ == "__main__":
    main()
```

Voer het uit met:

```bash
python run_ocr.py
```

Je zou de geëxtraheerde tekst in de console moeten zien verschijnen. Vanaf daar kun je het naar een bestand schrijven, in een database voeren, of doorgeven aan downstream NLP‑pipelines.

---

## Samenvatting & volgende stappen

We hebben behandeld **hoe je OCR uitvoert** op een PNG, hoe je **tekst uit afbeelding** extraheert, en praktische manieren getoond om **tekst uit PNG te herkennen** terwijl we **OCR‑nauwkeurigheid verbeteren** met woordenboeken en aangepaste tekens.  

Vervolgens, overweeg:

- **Batchverwerking:** Loop over een map met afbeeldingen.
- **Post‑processing:** Gebruik regex om factuurnummers of datums te extraheren.
- **Integratie:** Koppel het script aan een Flask‑API voor OCR‑diensten op aanvraag.

Als je nieuwsgierig bent naar meer geavanceerde onderwerpen, bekijk dan tutorials over **load image for OCR** met OpenCV‑preprocessing, of duik in deep‑learning‑gebaseerde OCR‑modellen zoals Tesseract 4+ met LSTM‑lagen.

---

### Blijf experimenteren!

Probeer `invoice_terms.txt` te vervangen door een lijst met medische terminologie, voeg Griekse tekens toe, of voer de engine een foto met lage resolutie aan om te zien hoe ver de nauwkeurigheid kan reiken. Hoe meer je knutselt, hoe beter je de afwegingen tussen preprocessing, aangepaste vocabularia en engine‑instellingen begrijpt.

Happy coding, and may your OCR results be ever crisp!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}