---
category: general
date: 2026-03-18
description: Hoe OCR te gebruiken om tekst uit afbeeldingen te extraheren – een snelle
  gids voor het herkennen van tekst uit PNG‑bestanden en het laden van afbeeldingen
  voor OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- how to extract text
- load image for OCR
language: nl
og_description: Hoe OCR te gebruiken om tekst uit afbeeldingen te extraheren – leer
  tekst te herkennen vanuit PNG, laad afbeelding voor OCR, en extraheer tekst met
  een eenvoudig Python‑script.
og_title: 'Hoe OCR te gebruiken: Tekst uit afbeeldingen extraheren in Python'
tags:
- OCR
- Python
- Image Processing
title: 'Hoe OCR te gebruiken: Tekst extraheren uit afbeeldingen in Python'
url: /nl/python-java/general/how-to-use-ocr-extract-text-from-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR te gebruiken: Tekst extraheren uit afbeeldingen in Python

Heb je je ooit afgevraagd **hoe je OCR kunt gebruiken** wanneer je een rommelige screenshot of een gescande bon hebt? Je bent niet de enige—ontwikkelaars moeten voortdurend leesbare tekst uit afbeeldingen halen, vooral PNG's die afkomstig zijn van mobiele apps of webuploads. In deze tutorial lopen we een volledig, uitvoerbaar voorbeeld door dat laat zien hoe je **tekst uit afbeelding** kunt **extraheren**, **tekst uit PNG** kunt **herkennen**, en zelfs **een afbeelding voor OCR kunt laden** met slechts een paar regels Python.

We behandelen alles, van het installeren van de juiste bibliotheek tot het omgaan met meertalige documenten, zodat je aan het einde precies weet *hoe je tekst kunt extraheren* uit elke afbeelding die je aan de engine geeft. Geen vage verwijzingen, alleen een duidelijke, stap‑voor‑stap oplossing die je kunt kopiëren‑plakken en uitvoeren.

## Wat je leert

In de komende secties gaan we:

1. Een lichtgewicht OCR‑engine opzetten (geen zware afhankelijkheden nodig).  
2. Een afbeeldingsbestand laden—specifiek een PNG—naar de engine.  
3. Automatische taaldetectie inschakelen zodat de engine meertalige inhoud kan verwerken.  
4. Het herkenningsproces uitvoeren en het platte‑tekstresultaat ophalen.  
5. De workflow aanpassen voor randgevallen zoals ontbrekende bestanden of niet‑ondersteunde formaten.

Als je vertrouwd bent met basis‑Python, ben je klaar. Geen eerdere OCR‑ervaring vereist, hoewel een snelle blik op de documentatie van de bibliotheek nooit kwaad kan.

---

![Hoe OCR te gebruiken op een PNG‑afbeelding](placeholder.png "Hoe OCR te gebruiken op een PNG‑afbeelding – stapsgewijze gids")

## Hoe OCR te gebruiken – Afbeelding laden en tekst herkennen {#how-to-use-ocr}

### Stap 1: Installeer de OCR‑bibliotheek

Allereerst heb je een Python‑pakket nodig dat een `OcrEngine`‑klasse levert. Voor deze tutorial gebruiken we het fictieve maar illustratieve **SimpleOCR**‑pakket, dat je kunt installeren via pip:

```bash
pip install simple-ocr
```

> **Pro tip:** Als je in een virtuele omgeving werkt (sterk aanbevolen), activeer deze dan voordat je het install‑commando uitvoert. Dit houdt de afhankelijkheden van je project netjes.

### Stap 2: Importeer de engine en maak een instantie

Het aanmaken van de engine is net zo eenvoudig als het aanroepen van de constructor. Beschouw de engine als het “brein” dat later de afbeelding die je erin stopt zal verwerken.

```python
# Step 2: Import and instantiate the OCR engine
from simple_ocr import OcrEngine

# Create a fresh engine instance – this allocates internal buffers
engine = OcrEngine()
```

Waarom maken we elke keer een nieuwe instantie? Isolatie. Een verse engine garandeert dat er geen resterende status van een vorige run de huidige herkenning beïnvloedt, wat cruciaal is wanneer je veel bestanden in één batch verwerkt.

### Stap 3: Laad de afbeelding die je wilt verwerken

Nu **laden we de afbeelding voor OCR**. De `setImageFromFile`‑methode accepteert een pad naar elke rasterafbeelding; we wijzen hem naar een PNG genaamd `mixed_doc.png`.

```python
# Step 3: Load the PNG image you want to read
image_path = "YOUR_DIRECTORY/mixed_doc.png"
engine.setImageFromFile(image_path)
```

Als het bestand niet wordt gevonden, gooit `SimpleOCR` een duidelijke `FileNotFoundError`. Je kunt deze opvangen om een vriendelijke foutmelding te geven:

```python
try:
    engine.setImageFromFile(image_path)
except FileNotFoundError:
    print(f"❗️ Unable to locate '{image_path}'. Check the path and try again.")
    raise
```

### Stap 4: Schakel automatische taaldetectie in

De meeste moderne OCR‑engines worden geleverd met taalpakketten. Door `"multilingual"` door te geven, vertellen we de engine de tekst te sniffen en automatisch het juiste taalmodel te kiezen. Dit is vooral handig wanneer je PNG een mix van Engels en Spaans bevat, bijvoorbeeld.

```python
# Step 4: Turn on auto‑language detection (covers all installed packs)
engine.setLanguage("multilingual")
```

Als je de taal van tevoren kent, kun je `"multilingual"` vervangen door een specifieke locale zoals `"eng"` of `"spa"` om de verwerking te versnellen.

### Stap 5: Voer het herkenningsproces uit

Hier gebeurt het zware werk. `recognize()` scant de afbeelding, past segmentatie toe, draait het neurale netwerk en bouwt intern een tekstbuffer op.

```python
# Step 5: Execute OCR – this may take a moment for large images
engine.recognize()
```

Achter de schermen voert de engine uit:

- **Pre‑processing** (kantelen corrigeren, binarisatie)  
- **Lay‑outanalyse** (detecteren van kolommen, tabellen)  
- **Karakterclassificatie** (met een deep‑learning‑model)  

Al dit werk wordt geabstraheerd, waardoor je slechts één regel nodig hebt.

### Stap 6: Haal de herkende tekst op en print deze

Tot slot halen we het resultaatsobject op en extraheren we de platte string. Dit is het moment waarop je daadwerkelijk **tekst uit afbeelding** **extrahert**.

```python
# Step 6: Get the OCR result and display the plain text
result = engine.getResult()
text = result.getText()
print("📝 Recognized Text:\n")
print(text)
```

**Verwachte output** (afgekapt voor beknoptheid):

```
📝 Recognized Text:

Invoice #12345
Date: 2026‑03‑15
Total: $89.99
Thank you for your purchase!
```

Als de afbeelding geen herkenbare tekens bevat, is `text` een lege string. Je kunt hiertegen beschermen:

```python
if not text.strip():
    print("⚠️ No text detected – try a higher‑resolution image or adjust preprocessing.")
```

---

## Tekst extraheren uit afbeelding – Veelvoorkomende randgevallen afhandelen

### Meerdere talen in één bestand

Wanneer een document meerdere talen mixt, doet de instelling `"multilingual"` meestal het juiste. Als je echter verkeerde herkenningen ziet, kun je handmatig een fallback‑lijst opgeven:

```python
engine.setLanguage(["eng", "spa", "fra"])  # English, Spanish, French
```

### Niet‑PNG‑formaten

Hoewel onze focus ligt op **tekst herkennen uit PNG**, accepteert `SimpleOCR` ook JPEG, BMP en TIFF. Verander simpelweg de bestandsextensie in `setImageFromFile`. Voor TIFF‑stapels moet je mogelijk een specifieke pagina selecteren:

```python
engine.setImageFromFile("scanned.tif", page=0)  # first page only
```

### Grote bestanden en geheugenverbruik

Als je gigapixel‑scans verwerkt, overweeg dan om te verkleinen vóór OCR:

```python
from PIL import Image

with Image.open(image_path) as img:
    img.thumbnail((2000, 2000))  # keep aspect ratio, max 2000px
    img.save("temp_resized.png")
engine.setImageFromFile("temp_resized.png")
```

Verkleinen vermindert de geheugenbelasting terwijl voldoende detail behouden blijft voor nauwkeurige herkenning.

### Foutopsporing bij mislukte loads

Soms ziet een afbeelding er voor het oog goed uit, maar is intern corrupt. Schakel uitgebreide logging in om te zien wat de engine ziet:

```python
engine.enableDebug(True)   # prints internal steps to stdout
engine.recognize()
```

---

## Volledig, kant‑klaar script

Hieronder staat het volledige programma dat alle onderdelen samenbrengt. Kopieer het naar een bestand genaamd `ocr_demo.py`, pas de placeholder `YOUR_DIRECTORY` aan, en voer `python ocr_demo.py` uit.

```python
# ocr_demo.py
# Full example showing how to use OCR to extract text from a PNG image.
# Requires: pip install simple-ocr pillow

from simple_ocr import OcrEngine
import os
from PIL import Image

def main():
    # 1️⃣ Create the OCR engine
    engine = OcrEngine()

    # 2️⃣ Define the image path – change this to your actual file location
    image_path = os.path.join("YOUR_DIRECTORY", "mixed_doc.png")

    # 3️⃣ Load the image (with a safety net for missing files)
    try:
        engine.setImageFromFile(image_path)
    except FileNotFoundError:
        print(f"❗️ Cannot find image at '{image_path}'. Exiting.")
        return

    # Optional: resize large images to keep memory usage low
    # (uncomment if you deal with huge scans)
    # with Image.open(image_path) as img:
    #     img.thumbnail((2000, 2000))
    #     resized_path = "temp_resized.png"
    #     img.save(resized_path)
    #     engine.setImageFromFile(resized_path)

    # 4️⃣ Enable automatic language detection (covers all installed packs)
    engine.setLanguage("multilingual")

    # 5️⃣ Run the OCR engine
    engine.recognize()

    # 6️⃣ Retrieve and print the recognized text
    result = engine.getResult()
    text = result.getText()

    if text.strip():
        print("\n📝 Recognized Text:\n")
        print(text)
    else:
        print("⚠️ No recognizable text found. Try a clearer image or adjust preprocessing.")

if __name__ == "__main__":
    main()
```

Het uitvoeren van dit script zou de platte‑tekstversie moeten weergeven van wat er in `mixed_doc.png` staat. Voel je vrij om het bestand te vervangen door een andere afbeelding—**hoe je tekst extrahert** werkt op dezelfde manier.

---

## Conclusie

We hebben zojuist **hoe OCR te gebruiken** in Python doorlopen om **tekst uit afbeelding**‑bestanden te **extraheren**, met speciale aandacht voor **tekst herkennen uit PNG**‑assets en de praktische stappen om **een afbeelding voor OCR te laden**. Het bovenstaande fragment is een zelfstandige oplossing: installeer het pakket, voer een bestand in, schakel meertalige detectie in, start de engine en haal het resultaat op.

Vanaf hier kun je:

- Het script integreren in een webservice die gebruikersuploads accepteert.  
- Een map met PDF‑bestanden die naar PNG's zijn geconverteerd batch‑verwerken.  
- Post‑processing toevoegen (bijv. regex‑opschoning, spell‑checking) om de nauwkeurigheid te verbeteren.

Onthoud dat de kwaliteit van OCR afhankelijk is van de helderheid van de afbeelding, de juiste taalpakketten en soms een beetje pre‑processing—dus experimenteer

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}