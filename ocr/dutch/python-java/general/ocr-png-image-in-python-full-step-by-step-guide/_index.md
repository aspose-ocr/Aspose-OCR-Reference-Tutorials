---
category: general
date: 2026-06-06
description: OCR PNG-afbeelding met Python – leer hoe je tekst uit een afbeelding
  kunt extraheren, een Python OCR‑voorbeeld kunt uitvoeren en zelfs gemakkelijk oude
  Griekse tekst kunt lezen.
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: nl
og_description: OCR PNG-afbeelding in Python uitgelegd. Deze gids laat zien hoe je
  tekst uit een afbeelding kunt extraheren, een Python OCR-voorbeeld kunt uitvoeren
  en gemakkelijk Oudgrieks kunt lezen.
og_title: OCR PNG-afbeelding in Python – Complete tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR PNG‑afbeelding in Python – Volledige stap‑voor‑stap gids
url: /nl/python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR PNG‑afbeelding in Python – Volledige stapsgewijze handleiding

Heb je je ooit afgevraagd hoe je **OCR PNG‑afbeeldingen** rechtstreeks vanuit een Python‑script kunt uitvoeren? Misschien heb je een map vol met gescande oude manuscripten en moet je **tekst uit afbeelding**‑bestanden halen zonder alles handmatig te typen. Het goede nieuws is dat je geen doctoraat in computer‑vision nodig hebt—slechts een paar regels code en de juiste bibliotheek, en je leest oude Grieks in enkele seconden.

In deze tutorial lopen we een **python OCR‑voorbeeld** door dat tekst herkent uit een PNG, de taal instelt op Grieks polytonisch, en het resultaat afdrukt. Aan het einde weet je precies hoe je **afbeeldingstekst herkent**, veelvoorkomende valkuilen aanpakt, en het script aanpast voor andere talen of afbeeldingsformaten.

## Wat je zult leren

- Een Python‑OCR‑bibliotheek installeren en configureren (pytesseract + Tesseract OCR)
- Een OCR‑engine‑instantie maken en een PNG‑bestand laden
- De herkenningstaal instellen op Grieks polytonisch zodat je **oud Grieks kunt lezen**
- De herkende tekst weergeven en typische problemen oplossen
- Het script uitbreiden om meerdere PNG’s in batch te verwerken of over te schakelen naar een andere taal

### Vereisten

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| Python 3.8+ | Moderne syntax en type‑hints |
| `pytesseract`‑package | Dunne wrapper rond de Tesseract‑engine |
| Tesseract OCR‑binaries (≥ 5.0) | De daadwerkelijke engine die het zware werk doet |
| Griekse taaldata (`grc.traineddata`) | Nodig om **oud Grieks correct te lezen** |
| Een PNG‑afbeelding die je wilt analyseren (bijv. `ancient_greek.png`) | Ons doel voor de **ocr png image**‑demo |

Je kunt de Python‑kant installeren met:

```bash
pip install pytesseract Pillow
```

En op Ubuntu/macOS voeg je de engine zelf toe:

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

Vergeet niet de Grieks‑polytonische trainingsdata te downloaden:

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

*(Pad kan verschillen; pas `TESSDATA_PREFIX` indien nodig aan.)*

---

## OCR PNG‑afbeelding: maak de engine‑instantie

Het eerste wat we nodig hebben is een object dat met Tesseract communiceert. In `pytesseract` wordt de engine benaderd via module‑niveau functies, maar voor de duidelijkheid wikkelen we het in een kleine klasse. Dit spiegelt het “engine”‑concept dat je in het oorspronkelijke fragment zag.

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**Waarom wikkelen?**  
- Houdt de publieke API identiek aan het fragment waarmee je begon, waardoor migratie moeiteloos verloopt.  
- Maakt het mogelijk om later logging of foutafhandeling toe te voegen zonder de hoofdlogica aan te passen.  
- Demonstreert goede OOP‑praktijken—iets waar senior developers waardering voor hebben.

---

## Tekst uit afbeelding halen: stel de taal in op Grieks polytonisch

Nu we een engine hebben, moeten we aangeven welke taal we verwachten. Grieks polytonisch gebruikt diakritische tekens die niet gedekt worden door de standaard “greek” data, dus wijzen we Tesseract naar het `grc`‑trainedfile.

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

Wil je ooit **tekst uit afbeelding**‑bestanden in een andere taal extraheren, vervang dan `"grc"` door `"eng"` voor Engels, `"fra"` voor Frans, enzovoort. dezelfde regel werkt voor elke geïnstalleerde taal.

---

## Afbeeldingstekst herkennen: voer de OCR uit op een PNG

Met de taal ingesteld voeren we de PNG in de engine. Het oorspronkelijke voorbeeld gebruikte een hard‑coded pad; we maken het iets flexibeler door `Path`‑objecten te gebruiken.

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**Tips & randgevallen**

- **Bestand niet gevonden** – wikkel de aanroep in een `try/except FileNotFoundError` om een vriendelijke melding te geven.  
- **Lage resolutie PNG** – overweeg pre‑processing (bijv. resizing, binarisatie) met Pillow vóór OCR.  
- **Niet‑Griekse tekst** – Tesseract zal nog steeds proberen te decoderen, maar de nauwkeurigheid daalt sterk. Zorg altijd voor een passende taal.

---

## De herkende tekst weergeven

Tot slot drukken we het resultaat af. In een echt project schrijf je misschien naar een database, een CSV, of voed je het in een vertaal‑pipeline.

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

Wanneer je het script uitvoert tegen een duidelijke scan van een oude Griekse inscriptie, zou je iets moeten zien als:

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

Als de output er rommelig uitziet, controleer dan of het **greek.traineddata**‑bestand in de juiste map staat en of de PNG niet te ruisachtig is.

---

## Volledig werkend voorbeeld (alle stappen in één script)

Hieronder staat het complete, kant‑klaar script. Sla het op als `ocr_greek.py` en voer `python ocr_greek.py` uit.

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**Verwachte output** (ingekort voor de duidelijkheid):

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

Zie je de juiste Griekse tekens, gefeliciteerd—je hebt met succes een **ocr png image**‑operatie in Python uitgevoerd!

---

## Veelgestelde vragen & pro‑tips

### Hoe verbeter ik de nauwkeurigheid bij een ruisachtige PNG?

- Converteer de afbeelding naar grijswaarden: `img = img.convert('L')`  
- Pas een binaire drempel toe: `img = img.point(lambda x: 0 if x < 128 else 255, '1')`  
- Schaal op met `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`

Deze stappen veranderen vaak een **recognize image text**‑nachtmerrie in een schoon resultaat.

### Kan ik een hele map met PNG’s verwerken?

Zeker. Wikkel de `recognize_image`‑aanroep in een `for`‑loop over `Path.glob("*.png")`. Sla elk resultaat op in een dictionary of schrijf naar een CSV voor latere analyse.

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### Wat als ik alleen cijfers wil extraheren?

Geef een aangepaste **config**‑string mee aan `image_to_string`:

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

Zo kun je **tekst uit afbeelding**‑bestanden die tabellen, serienummers of tijdstempels bevatten, extraheren.

### Is er een manier om vertrouwensscores te krijgen?

Ja—gebruik `pytesseract.image_to_data` dat een TSV met confidence per woord teruggeeft. Je kunt tokens met een lage confidence filteren voordat je de uiteindelijke string samenstelt.

---

## De tutorial uitbreiden

Nu je de basis onder de knie hebt, kun je de volgende gerelateerde onderwerpen verkennen:

- **Batch‑OCR met multiprocessing** – versnel grote corpora van PNG’s.  
- **Hybride OCR + NLP‑pipelines** – vertaal automatisch het geëxtraheerde oude Grieks naar modern Engels.  
- **Alternatieve engines** – probeer `easyocr` of `opencv`‑gebaseerde methoden voor specifieke use‑cases.  
- **Cloud‑OCR‑diensten** – Google Vision, Azure Computer Vision, of AWS Textract voor serverless scaling.

Elk van deze bouwt voort op het kern‑**python ocr example** dat we net behandeld hebben, zodat je je comfortabel voelt om dieper te duiken.

---

## Conclusie

We hebben een simpel fragment omgevormd tot een robuuste **ocr png image**‑workflow in Python. Door een `OcrEngine` te maken, de taal in te stellen op Grieks polytonisch, een PNG te voeren en het resultaat af te drukken, weet je nu hoe je **tekst uit afbeelding**‑bestanden kunt **herkennen**, **afbeeldingstekst** kunt lezen, en zelfs **oud Grieks** kunt ontcijferen.

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementaties in je eigen projecten te verkennen.

- [Tekst extraheren uit afbeelding met Aspose OCR – Stapsgewijze handleiding](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Hoe drempelwaarde instellen in OCR‑afbeeldingsherkenning](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Tekst herkennen in afbeelding met Aspose OCR voor meerdere talen](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}