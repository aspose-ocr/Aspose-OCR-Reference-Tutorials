---
category: general
date: 2026-04-26
description: Hoe OCR snel en betrouwbaar te maken. Leer tekst uit een afbeelding te
  extraheren, een afbeelding te laden voor OCR, en OCR uit te voeren op een PNG met
  een aangepast woordenboek.
draft: false
keywords:
- how to create OCR
- extract text from image
- extract text scanned document
- load image for OCR
- run OCR on png
language: nl
og_description: Hoe OCR te maken in Python en tekst uit een afbeelding te extraheren.
  Deze gids laat zien hoe je een afbeelding laadt voor OCR, OCR uitvoert op PNG en
  een aangepast woordenboek gebruikt.
og_title: Hoe OCR te maken in Python – Snelle Tekstextractie
tags:
- OCR
- Python
- Image Processing
title: Hoe OCR in Python te maken – Tekst uit afbeelding extraheren
url: /nl/python-java/general/how-to-create-ocr-in-python-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR te maken in Python – Stapsgewijze gids

Heb je je ooit afgevraagd **hoe je OCR kunt maken** die je gescande PDF's, screenshots of handgeschreven notities kan lezen? Je bent niet de enige. In veel real‑world projecten moeten we *tekst uit afbeelding* bestanden extraheren, maar de kant‑en‑klaar engines struikelen vaak over domeinspecifieke woorden.  

In deze tutorial zie je een compleet, uitvoerbaar voorbeeld dat een afbeelding laadt voor OCR, een aangepast woordenboek toepast, en uiteindelijk **OCR uitvoeren op PNG** bestanden. Aan het einde kun je tekst uit elke afbeelding extraheren en de engine aanpassen aan je eigen terminologie.

## Wat deze tutorial behandelt

* Het installeren van het kleine maar krachtige `aocr` pakket (of een andere compatibele bibliotheek).  
* Het configureren van een **aangepast woordenboek** zodat termen zoals `aspocorp` of `licensekey` worden herkend.  
* **Een afbeelding laden voor OCR**, of het nu een PNG, JPEG of een gescande PDF-pagina is.  
* Het uitvoeren van het OCR-proces en het afdrukken van het resultaat.  

Geen externe documentatielinks, alleen een zelfstandige oplossing die je vandaag kunt kopiëren‑plakken en uitvoeren.

### Vereisten

* Python 3.8 of nieuwer (de code gebruikt f‑strings).  
* Basiskennis van de commandoregel – je typt een paar `pip install` commando's.  
* Een afbeeldingsbestand (`technical_doc.png` in het voorbeeld) ergens geplaatst dat je kunt refereren.  

Als je aan deze drie punten voldoet, ben je klaar om te beginnen.  

---

## Stap 1: Installeer de OCR-bibliotheek

Eerst hebben we een OCR-engine nodig die een programmeerbaar configuratie‑object ondersteunt. Het `aocr` pakket is een lichtgewicht wrapper rond een native OCR-engine en werkt goed voor demo's.

```bash
# Install the library (run once)
pip install aocr
```

> **Pro tip:** Als je Windows gebruikt en een compilatiefout krijgt, probeer dan `pip install aocr‑binary` dat kant‑en‑klaar wheels levert.

### Waarom deze bibliotheek installeren?

`aocr` geeft ons directe toegang tot een `config` object waarin we een **aangepast woordenboek** kunnen injecteren. Dat is de geheime saus om de nauwkeurigheid op niche‑vocabularia te verbeteren.

---

## Stap 2: Maak de OCR-engine‑instantie aan & voeg een aangepast woordenboek toe

Nu starten we de engine en vertellen we welke woorden als bekend moeten worden beschouwd.

```python
from aocr import OcrEngine

# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Provide a custom dictionary to improve recognition of domain‑specific terms
ocr_engine.config.custom_dictionary = [
    "aspocorp",      # our company's brand name
    "ocrengine",    # the library name itself
    "licensekey"    # a common field in our contracts
]
```

### Waarom een aangepast woordenboek belangrijk is

Standaard OCR-modellen zijn getraind op generieke corpora. Wanneer het model “aspocorp” ziet, kan het het splitsen in “aspo corp” of letters volledig weglaten. Door een aangepaste lijst te voeden, sturen we de herkenner naar de exacte spelling die we nodig hebben, waardoor de post‑processing inspanning drastisch wordt verminderd.

---

## Stap 3: Laad de afbeelding die je wilt verwerken

Hier laden we **afbeelding voor OCR**. De `Image.load` methode accepteert een pad‑string en bepaalt automatisch het bestandstype.

```python
import aocr

# Step 3: Load the image that contains the text you want to extract
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/technical_doc.png")
```

> **Randgeval:** Als je bron een meer‑pagina PDF is, converteer dan elke pagina eerst naar PNG (bijv. met `pdf2image`) en voer ze één‑voor‑één aan de engine.

### Tips voor betere afbeeldingskwaliteit

* Houd de resolutie minimaal 300 dpi.  
* Zorg dat de afbeelding rechtop staat; roteer met `Pillow` indien nodig.  
* Converteer gekleurde scans naar grijswaarden om ruis te verminderen.

---

## Stap 4: Voer het OCR-proces uit op het PNG‑bestand

Met de engine geconfigureerd en de afbeelding geladen, voeren we eindelijk **OCR uitvoeren op PNG**.

```python
# Step 4: Run the OCR process
ocr_result = ocr_engine.process()
```

De `process()`‑aanroep retourneert een object dat de herkende tekst, vertrouwensscores en begrenzingskaders voor elk woord bevat.

---

## Stap 5: Output de herkende tekst

De eenvoudigste manier om te zien wat de engine heeft gevonden, is het afdrukken van het `text` attribuut.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### Verwachte output

Als `technical_doc.png` de zin *“The Aspocorp licensekey expires on 2025‑12‑31.”* bevat, zou de console moeten weergeven:

```
The Aspocorp licensekey expires on 2025-12-31.
```

Merk op hoe het aangepaste woordenboek de merknaam intact hield—iets wat een standaard OCR mogelijk had vervormd.

---

## Volledig werkend voorbeeld (Kopiëren‑Plakken klaar)

Hieronder staat het volledige script, klaar om op te slaan als `run_ocr.py`. Vervang gewoon het placeholder‑pad door de locatie van je afbeelding.

```python
# run_ocr.py
# -------------------------------------------------
# Complete example showing how to create OCR,
# load an image, apply a custom dictionary,
# and extract text from a PNG file.
# -------------------------------------------------

from aocr import OcrEngine
import aocr

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Add domain‑specific words
    ocr_engine.config.custom_dictionary = [
        "aspocorp",
        "ocrengine",
        "licensekey"
    ]

    # 3️⃣ Load the image you want to process
    #    (Make sure the path points to a real file)
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    ocr_engine.image = aocr.Image.load(image_path)

    # 4️⃣ Run the OCR engine
    ocr_result = ocr_engine.process()

    # 5️⃣ Print the extracted text
    print("=== Extracted Text ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

Run it from the terminal:

```bash
python run_ocr.py
```

Je zou de geëxtraheerde tekst in de console moeten zien verschijnen, precies zoals getoond in het eerdere voorbeeld.

---

## Veelgestelde vragen (FAQ)

| Vraag | Antwoord |
|----------|--------|
| **Kan ik tekst extraheren uit een gescande PDF?** | Ja. Converteer eerst elke pagina naar PNG (of TIFF), en voer vervolgens de afbeeldingen aan hetzelfde script. |
| **Wat als mijn afbeelding een JPEG is in plaats van PNG?** | De `Image.load` methode ondersteunt JPEG, BMP, TIFF en PNG direct. Verander gewoon de bestandsextensie. |
| **Hoe verbeter ik de nauwkeurigheid bij scans met weinig contrast?** | Pre‑process met `Pillow` – verhoog het contrast, pas binarisatie toe, of gebruik `opencv` om scheefstand te corrigeren. |
| **Is er een manier om vertrouwensscores voor elk woord te krijgen?** | `ocr_result` bevat `words` – elk woord heeft een `confidence` attribuut dat je kunt itereren. |
| **Kan ik dit draaien op een headless server?** | Absoluut. `aocr` heeft geen GUI‑afhankelijkheden, waardoor het perfect is voor CI‑pipelines. |

---

## Volgende stappen & gerelateerde onderwerpen

Nu je weet **hoe je OCR kunt maken** en **tekst uit afbeelding** bestanden kunt extraheren, overweeg dan om te verkennen:

* **Pre‑processing technieken** – `load image for OCR` is slechts de eerste stap; gebruik `opencv` om te denoisen of te verscherpen.  
* **Batchverwerking** – loop over een map met PNG's om een doorzoekbaar archief te genereren.  
* **Meertalige ondersteuning** – voeg taalpakketten toe aan de engine als je Franse of Duitse documenten moet lezen.  
* **Integratie met Elasticsearch** – index de geëxtraheerde tekst voor full‑text zoeken over gescande assets.  

Elk van deze uitbreidingen bouwt voort op het kernpatroon dat we net hebben behandeld, dus je zult de overgang moeiteloos vinden.

---

## Samenvatting

In een handvol minuten hebben we beantwoord **hoe je OCR kunt maken** die betrouwbaar **tekst uit afbeelding** bestanden extraheert, vooral PNG's, en we hebben je laten zien hoe je **afbeelding voor OCR laadt**, een **aangepast woordenboek** toepast, en **OCR uitvoert op PNG** zonder externe services.  

Probeer het script, pas het woordenboek aan om je eigen jargon te matchen, en je hebt een solide basis voor elk document‑digitaliseringsproject.  

Als je tegen problemen aanloopt, laat dan een reactie achter—ik help graag. En vergeet niet je succesverhalen te delen; de community leert het beste van real‑world voorbeelden.  

**Klaar om je papierwerk te automatiseren?** Pak de code, pas deze aan, en begin vandaag nog met het omzetten van pixels naar doorzoekbare tekst!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}