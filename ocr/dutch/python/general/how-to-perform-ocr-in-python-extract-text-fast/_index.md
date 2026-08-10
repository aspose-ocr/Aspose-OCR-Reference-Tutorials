---
category: general
date: 2026-03-26
description: Leer hoe je OCR in Python kunt uitvoeren en eenvoudig tekst uit een afbeelding
  kunt extraheren, tekst van een scan kunt lezen, of tekst van een factuur kunt extraheren
  met een eenvoudige OcrEngine.
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from scan
- extract text from invoice
- how to use OCR
language: nl
og_description: Hoe OCR uit te voeren in Python? Deze gids laat je zien hoe je tekst
  uit een afbeelding kunt extraheren, tekst uit een scan kunt lezen en tekst uit een
  factuur kunt halen in enkele minuten.
og_title: Hoe OCR in Python uit te voeren – Tekst snel extraheren
tags:
- OCR
- Python
- Image Processing
title: Hoe OCR in Python uit te voeren – Tekst snel extraheren
url: /nl/python/general/how-to-perform-ocr-in-python-extract-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR uit te voeren in Python – Tekst Snel Extracten

Heb je je ooit afgevraagd **hoe je OCR** kunt uitvoeren op een gescande bon of een wazige PDF? Je bent niet de enige. In veel projecten komt de behoefte om **tekst uit een afbeelding** te halen al snel naar voren, en de gebruikelijke “alles handmatig typen” aanpak is simpelweg niet schaalbaar.  

In deze tutorial zie je een compleet, kant‑klaar voorbeeld dat laat zien **hoe je OCR** kunt gebruiken om tekst van een scan te lezen, gegevens van een factuur te halen, en zelfs automatische scheefcorrectie toe te passen – allemaal met slechts een paar regels Python.

## Wat je gaat leren

We lopen stap voor stap door alles wat je moet weten:

* De exacte afhankelijkheden en imports die nodig zijn.
* Hoe je een `OcrEngine`‑instantie maakt en configureert.
* Manieren om **tekst uit afbeelding te extraheren**, **tekst van scan te lezen**, en **tekst van factuur te extraheren** met dezelfde engine.
* Veelvoorkomende valkuilen (verkeerde taal, ontbrekende bestanden, grote afbeeldingen) en hoe je ze kunt vermijden.
* Verwachte output zodat je kunt verifiëren dat de OCR geslaagd is.

Er zijn geen externe documentatielinks nodig – alles staat in één bestand, zodat je de code kunt kopiëren‑plakken en direct resultaten ziet.

## Vereisten

Voordat we beginnen, zorg dat je het volgende hebt:

* Python 3.8+ geïnstalleerd (het `ocr`‑pakket werkt met elke recente versie).
* De `ocr`‑bibliotheek beschikbaar (`pip install ocr‑engine` – vervang door de daadwerkelijke pakketnaam indien anders).
* Een afbeeldingsbestand dat je wilt verwerken – voor de demo gebruiken we `invoice.png` in een map genaamd `YOUR_DIRECTORY`.

Dat is alles. Als je dit al hebt, kun je meteen aan de slag.

## Stap 1: Installeer en importeer de OCR‑module

Allereerst: we hebben de OCR‑bibliotheek nodig. Als je die nog niet geïnstalleerd hebt, voer dan het volgende commando uit in je terminal:

```bash
pip install ocr-engine
```

Importeer nu de module in ons script.

```python
# Step 1: Import the OCR module
import ocr
```

> **Pro tip:** Houd je virtuele omgeving netjes; dit voorkomt versieconflicten wanneer je later andere beeldverwerkings‑pakketten toevoegt.

## Stap 2: Maak en configureer de OCR‑engine

Het aanmaken van de engine is zo simpel als het aanroepen van de constructor, maar de echte kracht zit in de juiste configuratie. We stellen de taal in op Engels en schakelen automatische scheefcorrectie in, wat essentieel is bij gescande facturen die niet perfect uitgelijnd zijn.

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Step 3: Configure the engine – set language and enable automatic skew correction
engine.language = ocr.Language.English   # any supported language, e.g., Spanish, French
engine.auto_skew = True                 # fixes tilted scans automatically
```

Waarom `auto_skew` inschakelen? Veel scanners produceren afbeeldingen die een paar graden scheef staan. Zonder correctie kan de engine tekens missen, waardoor een perfect leesbare factuur verandert in onzin.

## Stap 3: Voer OCR uit op je doelafbeelding

Nu geven we het afbeeldingsbestand aan de engine. De methode `recognize_image` retourneert een object dat de ruwe tekst bevat, evenals eventuele vertrouwensscores (indien de bibliotheek die levert).

```python
# Step 4: Perform OCR on the target image
ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

Werk je met een **tekst‑van‑scan‑scenario**, vervang dan simpelweg het pad door de gescande PDF die je hebt geconverteerd naar PNG of JPEG. Dezelfde aanroep werkt voor elk afbeeldingsformaat dat de onderliggende bibliotheek ondersteunt.

## Stap 4: Inspecteer en gebruik de geëxtraheerde tekst

Laten we de ruwe OCR‑output afdrukken. In een echte factuur‑verwerkingspipeline zou je deze string waarschijnlijk parseren, regelitems, totalen en datums extraheren, maar voor nu bevestigt een snelle blik dat de OCR geslaagd is.

```python
# Step 5: Display the raw extracted text
print("Raw OCR text:\n", ocr_result.text)
```

**Verwachte output (ingekort voor beknoptheid):**

```
Raw OCR text:
 Invoice #12345
 Date: 2026‑03‑01
 Bill To: Acme Corp.
 Item          Qty   Price   Total
 ------------------------------------------------
 Widget A      10    5.00    50.00
 Widget B      5     12.00   60.00
 ------------------------------------------------
 Subtotal:                     110.00
 Tax (5%):                     5.50
 Grand Total:                  115.50
```

Als de output er rommelig uitziet, controleer dan of de afbeelding scherp is en of `engine.language` overeenkomt met de taal van het document.

## Stap 5: Veelvoorkomende randgevallen afhandelen

### Grote afbeeldingen

Het verwerken van een scan van 5000 × 5000 pixel kan veel geheugen verbruiken. Een snelle manier om dit te beperken is de afbeelding te verkleinen voordat je ze naar de engine stuurt:

```python
from PIL import Image

def load_and_resize(path, max_dim=2000):
    img = Image.open(path)
    img.thumbnail((max_dim, max_dim), Image.ANTIALIAS)
    return img

scaled_image = load_and_resize("YOUR_DIRECTORY/invoice.png")
ocr_result = engine.recognize_image(scaled_image)
```

### Meerdere talen

Als je **tekst uit afbeelding** moet extraheren die zowel Engels als Spaans bevat, kun je een lijst van talen instellen:

```python
engine.language = [ocr.Language.English, ocr.Language.Spanish]
```

De engine probeert dan tekens uit beide sets te herkennen.

### Foutafhandeling

Ga nooit ervan uit dat het bestand bestaat. Plaats de aanroep in een try‑except‑blok om een vriendelijke melding te geven:

```python
try:
    ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
    print("OCR succeeded!")
except FileNotFoundError:
    print("Error: The image file was not found. Check the path and try again.")
except ocr.OcrError as e:
    print(f"OCR failed with error: {e}")
```

## Visuele referentie

Hieronder zie je een screenshot van de voorbeeldfactuur die we in de demo hebben gebruikt. Let op de lichte kanteling – precies wat `auto_skew` corrigeert.

![how to perform OCR on an invoice](/images/ocr-example.png)

*Alt text:* how to perform OCR on an invoice image showing automatic skew correction.

## Volledig, uitvoerbaar voorbeeld

Alles bij elkaar genomen, hier is één script dat je vanaf de commandoregel kunt uitvoeren. Het behandelt installatie, configuratie, foutafhandeling en een eenvoudige post‑processing stap die de geëxtraheerde tekst naar een bestand `output.txt` schrijft.

```python
# full_ocr_demo.py
# -------------------------------------------------
# Demonstrates how to perform OCR, extract text from image,
# read text from scan, and extract text from invoice.
# -------------------------------------------------

import ocr
from pathlib import Path

def main(image_path: str, output_path: str = "output.txt"):
    # Create and configure the engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.auto_skew = True

    # Verify the image exists
    if not Path(image_path).is_file():
        print(f"❌  Image not found: {image_path}")
        return

    # Run OCR
    try:
        result = engine.recognize_image(image_path)
    except ocr.OcrError as err:
        print(f"❌  OCR failed: {err}")
        return

    # Output the raw text
    print("✅  OCR completed. Raw text:")
    print(result.text)

    # Save to a text file for later processing
    Path(output_path).write_text(result.text, encoding="utf-8")
    print(f"💾  Text saved to {output_path}")

if __name__ == "__main__":
    # Replace with your actual file location
    main("YOUR_DIRECTORY/invoice.png")
```

Het uitvoeren van `python full_ocr_demo.py` zal de geëxtraheerde tekst naar de console printen en opslaan in `output.txt`. Vanaf daar kun je reguliere expressies, CSV‑schrijvers of andere logica toepassen die je nodig hebt voor **tekst‑van‑factuur‑automatisering**.

## Conclusie

Je hebt nu een solide, end‑to‑end oplossing voor **hoe OCR uit te voeren** in Python. Door een `OcrEngine` te maken, taal en scheefcorrectie te configureren, en een paar praktische randgevallen af te handelen, kun je betrouwbaar **tekst uit afbeelding** extraheren, **tekst van scan** lezen, en **tekst van factuur** halen zonder door verspreide documentatie te hoeven zoeken.

Wat nu? Probeer een batch bestanden in een lus te verwerken, experimenteer met verschillende talen, of koppel de output aan een PDF‑generatie‑bibliotheek om doorzoekbare PDF’s te maken. De mogelijkheden zijn eindeloos, en de code die je net zag is een stevige springplank.

Heb je vragen over een specifiek bestandsformaat of hulp nodig bij het afstemmen van vertrouwensdrempels? Laat een reactie achter – ik help je graag je OCR‑pipeline te finetunen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}