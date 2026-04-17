---
category: general
date: 2026-03-26
description: Leer hoe je OCR in Python uitvoert en tekst herkent uit afbeeldingsbestanden.
  Deze gids laat zien hoe je tekst uit PNG kunt extraheren en afbeeldingen snel naar
  tekst kunt converteren.
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: nl
og_description: Hoe voer je OCR uit in Python? Volg deze gids om tekst uit een afbeelding
  te herkennen, tekst uit PNG te extraheren en een afbeelding naar tekst te converteren
  met een proeflicentie.
og_title: Hoe OCR in Python uit te voeren – Complete tutorial
tags:
- OCR
- Python
- Image Processing
title: Hoe OCR in Python uit te voeren – Complete stap‑voor‑stap tutorial
url: /nl/python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR uit te voeren in Python – Complete stap‑voor‑stap tutorial  

Heb je je ooit afgevraagd **hoe je OCR kunt uitvoeren** op een foto die je net met je telefoon hebt gemaakt? Je bent niet de enige—ontwikkelaars overal hebben een betrouwbare manier nodig om tekst uit afbeeldingsbestanden te herkennen zonder te worstelen met complexe native bibliotheken.  

In deze tutorial lopen we een praktische voorbeeld door dat laat zien **hoe je OCR kunt uitvoeren**, **tekst uit een afbeelding herkent**, en **tekst uit PNG extraheert** met een lichtgewicht Python-wrapper. Aan het einde kun je **afbeelding naar tekst converteren** in slechts een paar regels code, en je hoeft je geen zorgen te maken over licentieproblemen omdat we de ingebouwde proefmodus gebruiken.

## Wat je zult leren  

* Hoe je een proeflicentie voor de OCR-engine instelt (geen bestands pad nodig).  
* De exacte volgorde van aanroepen naar **recognize text from image** objecten.  
* Manieren om **extract text from PNG** bestanden te gebruiken en veelvoorkomende valkuilen zoals ontbrekende lettertypen te behandelen.  
* Tips voor het schalen van de oplossing wanneer je overschakelt van een proef- naar een productielicentie.  

**Prerequisites** – je hebt Python 3.8+ en het `ocr` pakket nodig (installeren via `pip install ocr`). Geen andere externe tools zijn vereist.

---  

![hoe OCR uit te voeren voorbeeld](https://example.com/ocr-demo.png "hoe OCR uit te voeren in Python – herkende tekst weergegeven")  

*Afbeeldingsalttekst: hoe OCR uit te voeren in Python – voorbeeldoutput*  

## Stap 1 – Activeer een proeflicentie (geen bestands pad nodig)  

Voordat de engine iets kan lezen, heeft hij een geldige licentie nodig. De proefmodus is perfect voor experimenten en kleine projecten.

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*Waarom dit belangrijk is:* Het licentie‑object vertelt de OCR‑bibliotheek dat je in een sandbox werkt. Als je deze stap overslaat, zal de engine een `LicenseError` genereren op het moment dat je `recognize()` aanroept.  

**Pro tip:** Wanneer je overstapt op een betaalde licentie, vervang je de twee bovenstaande regels door `ocr.License("path/to/your/license.key").apply()`.

## Stap 2 – Maak de OCR Engine‑instantie  

Nu de proeflicentie actief is, instantieren we de hoofd‑engine. Beschouw het als de “hersenen” die naar de afbeelding kijkt en beslist welke tekens waar staan.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*Waarom dit belangrijk is:* De `OcrEngine` bevat configuratie zoals taalpakketten en DPI‑instellingen. Je kunt die later aanpassen, maar de standaard werkt voor de meeste alleen‑Engelse PNG's.

## Stap 3 – Laad de PNG die je wilt verwerken  

Hier is waar we **recognize text from image**. De `ocr.Imaging.Image.load()`‑methode ondersteunt PNG, JPEG, BMP en enkele andere formaten.

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*Randgeval:* Als je PNG een geïndexeerd palet gebruikt (veelvoorkomend bij screenshots), zal de loader deze automatisch omzetten naar een 24‑bit RGB‑buffer. Die conversie kan een kleine prestatie‑impact hebben, maar garandeert nauwkeurige OCR‑resultaten.

## Stap 4 – Voer de OCR uit en haal de tekst op  

Ten slotte vragen we de engine om zijn werk te doen en vervolgens het platte‑tekst resultaat op te halen.

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**Verwachte output** (voorbeeld voor een eenvoudige afbeelding met “Hello World”):

```
Hello World
```

Als de afbeelding meerdere regels bevat, behoudt de output de regeleinden, waardoor het eenvoudig is om downstream processen zoals CSV‑parsers of NLP‑pijplijnen te voeden.

## Optioneel: Fijn afstellen voor betere nauwkeurigheid  

* **Language packs:** `ocr_engine.set_language("eng")` (standaard) of `"fra"` voor Frans.  
* **DPI scaling:** `ocr_engine.set_dpi(300)` kan resultaten verbeteren bij lage‑resolutie scans.  
* **Pre‑processing:** Het toepassen van een binaire drempel (`ocr.Imaging.Image.threshold()`) vóór `set_image` levert vaak schonere tekst op bij ruisende achtergronden.  

Deze aanpassingen zijn nuttig wanneer je van een snelle demo naar een productie‑klare **ocr tutorial python** gaat die honderden bestanden per dag verwerkt.

## Volledig script – Klaar om te kopiëren & plakken  

Hieronder staat het volledige, uitvoerbare script dat alle bovenstaande stappen combineert. Sla het op als `run_ocr.py` en vervang `YOUR_DIRECTORY/sample1.png` door het pad naar je eigen PNG.

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

Voer het uit vanaf de commandoregel:

```bash
python run_ocr.py
```

Je zou de geëxtraheerde tekst in de console moeten zien verschijnen. Als je een lege string krijgt, controleer dan dubbel of de afbeelding daadwerkelijk duidelijke, hoog‑contrast tekst bevat en of de proeflicentie zonder fouten is toegepast.

## Veelgestelde vragen & valkuilen  

* **“Werkt dit met JPEG?”** – Absoluut. De `load()`‑methode detecteert automatisch het formaat, dus je kunt PNG vervangen door JPEG zonder code‑aanpassingen.  
* **“Wat als de afbeelding gedraaid is?”** – De engine kan automatisch de oriëntatie detecteren, maar voor de beste resultaten kun je vooraf roteren met `input_image.rotate(90)` vóór `set_image`.  
* **“Kan ik meerdere afbeeldingen in een lus verwerken?”** – Ja. Verplaats gewoon het laden en de `recognize()`‑aanroepen naar binnen een `for`‑lus; dezelfde `ocr_engine`‑instantie kan hergebruikt worden, wat een kleine hoeveelheid overhead bespaart.  

## Volgende stappen – Van demo naar productie  

Nu je weet **hoe je OCR kunt uitvoeren**, overweeg deze vervolgonderwerpen:

* **Batchverwerking** – Combineer dit script met `os.listdir()` om **extract text from PNG** bestanden in bulk te verwerken.  
* **Integreren met PDF** – Gebruik `pdf2image` om PDF‑pagina's naar PNG te converteren, en voer ze vervolgens in dezelfde pipeline in.  
* **Post‑processing** – Pas regex of fuzzy matching toe om veelvoorkomende OCR‑foutherkenningen op te schonen (bijv. “0” vs “O”).  

Elk van deze bouwt voort op het kernidee van **convert image to text** en vergroot de bruikbaarheid van je OCR‑workflow.

---  

### TL;DR  

We hebben alles behandeld wat je moet weten om **how to perform OCR** in Python: activeer een proeflicentie, maak een engine, laad een PNG, voer de herkenning uit, en print het resultaat. Met slechts een handvol regels kun je **recognize text from image**, **extract text from PNG**, en **convert image to text** voor elke downstream‑applicatie.  

Probeer het, pas de DPI‑ of taalinstellingen aan, en laat de engine het zware werk doen. Veel plezier met coderen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}