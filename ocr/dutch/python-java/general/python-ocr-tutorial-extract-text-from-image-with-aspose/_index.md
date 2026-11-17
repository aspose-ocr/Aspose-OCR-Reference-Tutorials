---
category: general
date: 2026-03-26
description: 'Python OCR‑tutorial: leer hoe je tekst uit een afbeelding kunt extraheren,
  een afbeelding kunt laden voor OCR en tekst van een bon kunt herkennen met Aspose
  OCR in slechts een paar stappen.'
draft: false
keywords:
- python ocr tutorial
- extract text from image
- load image for ocr
- perform ocr in python
- recognize text from receipt
language: nl
og_description: 'Python OCR-tutorial: leer snel tekst uit een afbeelding te extraheren,
  laad een afbeelding voor OCR en herken tekst van een bon met Aspise OCR.'
og_title: Python OCR‑tutorial – Tekst uit afbeelding halen
tags:
- OCR
- Aspose
- Python
title: Python OCR-tutorial – Tekst uit afbeelding extraheren met Aspose
url: /nl/python-java/general/python-ocr-tutorial-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR‑tutorial – Tekst extraheren uit afbeelding met Aspose

Heb je je ooit afgevraagd hoe je de tekst uit een wazige bon of een gescande formulier kunt halen zonder uren te besteden aan eigen regexes? Je bent niet de enige. In deze **python ocr tutorial** lopen we stap voor stap door het laden van een afbeelding voor OCR, het uitvoeren van OCR in Python, en tenslotte het herkennen van tekst uit bonbestanden met de Aspose OCR‑bibliotheek.  

Aan het einde van deze gids heb je een kant‑klaar script dat elk ondersteund afbeeldingsformaat kan lezen, de tekstinhoud extraheert en deze naar de console print. Geen externe services, geen API‑sleutels — alleen pure Python en een krachtige OCR‑engine.  

## Wat je nodig hebt

- Python 3.8 of nieuwer (de code maakt gebruik van type‑hints, dus een recente interpreter is het beste)
- `asposeocrjava`‑pakket geïnstalleerd via `pip install aspose-ocr`
- Een voorbeeldafbeelding — bijvoorbeeld `receipt_noisy.jpg` die een typische kassabon bevat
- (Optioneel) Een virtuele omgeving om afhankelijkheden netjes te houden

Als je deze punten hebt afgevinkt, kunnen we direct naar de code springen.  

## Stap 1: Installeer en importeer Aspose OCR‑klassen

Zorg er eerst voor dat het Aspose OCR‑pakket beschikbaar is. Importeer vervolgens de klassen die we nodig hebben.

```python
# Install the package (run once)
# pip install aspose-ocr

# Import the required Aspose OCR modules
import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult
```

**Waarom dit belangrijk is:** Alleen de noodzakelijke symbolen importeren houdt de namespace schoon en geeft de interpreter duidelijk aan welke delen van de bibliotheek we daadwerkelijk gebruiken. Het verkort ook latere code‑regels, waardoor de tutorial makkelijker te volgen is.

> **Pro tip:** Als je een Jupyter‑notebook gebruikt, plaats dan een `!` vóór de installatieregel om deze in‑cell uit te voeren.

## Stap 2: Maak de OCR‑engine en schakel Deep‑Learning‑modus in

Aspose biedt verschillende engine‑modi. Voor de meeste reële kassabonnen levert het deep‑learning‑model de hoogste nauwkeurigheid, vooral bij ruisende scans.

```python
# Initialise the OCR engine
ocr_engine = OcrEngine()

# Switch to deep‑learning mode for better accuracy on complex images
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
```

**Waarom deep‑learning?** Traditionele regel‑gebaseerde OCR kan moeite hebben met tekens met weinig contrast of vervormde karakters. Het deep‑learning‑model, getraind op miljoenen glyphs, past zich beter aan variaties aan — precies wat je nodig hebt wanneer je *perform OCR in Python* op bonnen die met een telefooncamera zijn genomen.

## Stap 3: Laad afbeelding voor OCR

Nu **laden we de afbeelding voor OCR**. Aspose.Imaging ondersteunt PNG, JPEG, BMP, TIFF en meer, zodat je vrijwel elke foto van een document kunt gebruiken.

```python
# Load the image (replace the path with your own file)
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/receipt_noisy.jpg")

# Attach the image to the OCR engine
ocr_engine.set_image(input_image)
```

**Veelvoorkomende valkuil:** Als je de afbeelding niet op de engine zet, krijg je een `NullReferenceException` tijdens runtime. Roep altijd `set_image` aan nadat je het bestand hebt geladen.

## Stap 4: Voer OCR uit en extraheer tekst

Met de engine klaar en de afbeelding gekoppeld, kunnen we eindelijk **perform OCR in Python** en het tekstresultaat ophalen.

```python
# Run the recognition process
ocr_result: OcrResult = ocr_engine.recognize()

# Extract plain text from the result object
recognized_text = ocr_result.get_text()
```

De `recognize()`‑methode retourneert een `OcrResult`‑object dat niet alleen ruwe tekst bevat, maar ook confidence‑scores, bounding boxes en taal‑informatie. Voor een snelle **extract text from image**‑use‑case hebben we alleen `get_text()` nodig.

## Stap 5: Toon de herkende tekst

Laten we zien wat de engine daadwerkelijk van de bon heeft gelezen.

```python
print("Recognized text:\n", recognized_text)
```

Typische output ziet er als volgt uit:

```
Recognized text:
   Store XYZ
   04/26/2026  14:32
   Item A   2.99
   Item B   5.49
   TOTAL    8.48
   THANK YOU!
```

Als de output onleesbare tekens bevat, overweeg dan de afbeelding vooraf te bewerken (bijvoorbeeld het contrast verhogen of een deskew‑filter toepassen) voordat je deze in de OCR‑engine laadt. Aspose.Imaging biedt een volledige reeks beeld‑verbeterings‑tools die je kunt combineren.

## Edge‑cases afhandelen & Tips voor betere nauwkeurigheid

### 1. Omgaan met extreem ruisende bonnen
Als de bon sterk vervaagd is, kun je overschakelen naar de `OcrEngineMode.HIGH_SPEED`‑modus voor een snellere, zij het minder nauwkeurige, pass, en vervolgens een tweede pass in `DEEP_LEARNING` uitvoeren op de opgeschoonde afbeelding.

```python
ocr_engine.set_engine_mode(OcrEngineMode.HIGH_SPEED)
# ... run first pass, then...
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
# ... run second pass on the same image
```

### 2. Taal specificeren
Standaard probeert Aspose de taal automatisch te detecteren. Voor Engelstalige bonnen kun je dit vastzetten:

```python
ocr_engine.set_language("eng")
```

### 3. Geheugenbeheer
Wanneer je veel afbeeldingen in een lus verwerkt, geef je bronnen expliciet vrij:

```python
input_image.dispose()
ocr_engine.dispose()
```

### 4. OCR‑resultaten opslaan naar een bestand
Soms moet de geëxtraheerde tekst bewaard worden voor latere analyse.

```python
with open("receipt_output.txt", "w", encoding="utf-8") as f:
    f.write(recognized_text)
```

## Volledig werkend voorbeeld

Hieronder vind je het complete script dat alles samenbrengt. Kopieer‑en plak het in een bestand met de naam `receipt_ocr.py`, pas het afbeeldingspad aan, en voer `python receipt_ocr.py` uit.

```python
# receipt_ocr.py
# -------------------------------------------------
# Complete Python OCR tutorial using Aspose OCR
# -------------------------------------------------

# 1️⃣ Install the package (run once):
# pip install aspose-ocr

import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult

def main():
    # 2️⃣ Initialise engine in deep‑learning mode
    engine = OcrEngine()
    engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)

    # 3️⃣ Load your receipt image
    image_path = "YOUR_DIRECTORY/receipt_noisy.jpg"   # <-- change this
    img = ocr.Imaging.Image.load(image_path)
    engine.set_image(img)

    # 4️⃣ Recognise text
    result: OcrResult = engine.recognize()
    text = result.get_text()

    # 5️⃣ Output the result
    print("=== Recognized text from receipt ===")
    print(text)

    # Optional: write to a file
    with open("receipt_output.txt", "w", encoding="utf-8") as out_file:
        out_file.write(text)

    # Clean up resources
    img.dispose()
    engine.dispose()

if __name__ == "__main__":
    main()
```

Het uitvoeren van het script moet de inhoud van de bon in je console tonen en tevens `receipt_output.txt` aanmaken met dezelfde gegevens.

![Python OCR tutorial – sample receipt output](https://example.com/receipt_output.png "voorbeeld van python ocr tutorial")

*Afbeeldings‑alt‑tekst:* **Python OCR‑tutorial – voorbeeld van kassabonoutput**

## Samenvatting & Volgende stappen

We hebben net een **python ocr tutorial** doorlopen die laat zien hoe je **load image for OCR**, **perform OCR in Python**, en uiteindelijk **recognize text from receipt**‑bestanden gebruikt met Aspose. De belangrijkste punten zijn:

- Kies de juiste engine‑modus (deep‑learning voor nauwkeurigheid)
- Koppel altijd de afbeelding voordat je `recognize()` aanroept
- Gebruik het `OcrResult`‑object om schone tekst te halen, en sla deze vervolgens op of verwerk hem verder

Wat nu? Overweeg om Aspose Imaging‑filters te combineren om scans met weinig contrast te verbeteren, of integreer het script in een Flask‑API zodat je bonnen via een webformulier kunt uploaden. Je kunt ook de OCR‑data exporteren naar CSV voor automatisering van de boekhouding.

Vragen over het verwerken van meer‑pagina‑PDF’s of niet‑Latijnse scripts? Laat een reactie achter — ik help graag!  

**Klaar om je documentautomatisering naar een hoger niveau te tillen?** Pak de code, experimenteer met verschillende afbeeldingen, en laat de OCR‑engine het zware werk doen. Veel programmeerplezier!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}