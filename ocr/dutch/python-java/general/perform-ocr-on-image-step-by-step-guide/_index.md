---
category: general
date: 2026-03-18
description: Voer OCR uit op een afbeelding om snel tekst uit de afbeelding te extraheren.
  Leer hoe je een afbeelding laadt voor OCR, een OCR‑engine maakt en de OCR‑nauwkeurigheid
  verbetert met taalopties.
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: nl
og_description: Voer OCR uit op een afbeelding met deze gedetailleerde gids. Leer
  hoe je een afbeelding laadt voor OCR, een OCR‑engine maakt en de OCR‑nauwkeurigheid
  verbetert voor betrouwbare tekstextractie.
og_title: Voer OCR uit op afbeelding – Complete programmeertutorial
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Voer OCR uit op afbeelding – Stapsgewijze handleiding
url: /nl/python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR op afbeelding uitvoeren – Complete programmeertutorial

Heb je ooit **OCR op afbeelding uitvoeren** moeten, maar wist je niet welke bibliotheek je moet kiezen of hoe je betrouwbare resultaten krijgt? Je bent niet de enige. In deze gids lopen we alles door wat je nodig hebt om **tekst uit afbeelding te extraheren**, van het laden van de afbeelding tot het aanpassen van taalopties zodat je **OCR‑nauwkeurigheid kunt verbeteren** bij elke stap.

We behandelen hoe je **load image for OCR**, hoe je **create OCR engine** en waarom elke instelling belangrijk is. Aan het einde heb je een kant‑klaar script dat de herkende tekst afdrukt, en begrijp je het “waarom” achter elke regel—geen vage “zie de docs” shortcuts. Laten we beginnen.

## Wat je nodig hebt

- Python 3.8+ (de code gebruikt f‑strings en type‑hints)
- Het hypothetische `ocr_lib`‑pakket – installeer met `pip install ocr_lib`
- Een afbeeldingsbestand met duidelijke, afgedrukte tekst (bijv. `lab_report.png`)
- Een eenvoudige teksteditor of IDE (VS Code, PyCharm, wat je maar wilt)

Als je die al hebt, geweldig—je bent klaar. Zo niet, download Python van python.org en voer het pip‑commando uit; het duurt maar een minuut.

![perform OCR on image – voorbeeldoutput met geëxtraheerde tekst](/images/ocr-example.png)

*Alt‑tekst: perform OCR on image – voorbeeldoutput met geëxtraheerde tekst.*

## Stap 1: OCR‑engine maken – Hoe **create OCR engine** in Python

Voordat er herkenning kan plaatsvinden, heeft de bibliotheek een engine‑object nodig dat configuratie en runtime‑status bevat. Beschouw de engine als het brein achter de operatie.

```python
# step_1_create_engine.py
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    """
    Initialize and return a fresh OcrEngine instance.
    Creating the engine once and reusing it is more efficient than
    instantiating it inside a loop.
    """
    engine = OcrEngine()
    return engine
```

**Waarom dit belangrijk is:** Het vroeg instantiëren van de engine laat je later taalopties toevoegen, en het cachet ook interne modellen voor snellere opeenvolgende aanroepen.

## Stap 2: Afbeelding laden voor OCR – De juiste manier om **load image for OCR**

Nu we een engine hebben, moeten we het iets geven om te lezen. De `setImageFromFile`‑methode accepteert een bestandsysteem‑pad; het pad kan absoluut of relatief zijn ten opzichte van de werkmap van het script.

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**Pro‑tip:** Gebruik een absoluut pad of `os.path.join` om “file not found” verrassingen te vermijden wanneer het script vanuit een andere map wordt uitgevoerd.

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## Stap 3: OCR‑nauwkeurigheid verbeteren – Aanpassen van **language options** om **improve OCR accuracy**

Out‑of‑the‑box OCR werkt, maar domeinspecifieke vocabularia (zoals laboratoriumjargon) laten het vaak haperen. Door een aangepast woordenboek en een blacklist te gebruiken, verminder je mis‑herkenningen zoals het verwarren van “0” met “O”.

```python
# step_3_language_options.py
def configure_language(engine: OcrEngine) -> None:
    """
    Set up language options to help the engine recognize domain‑specific terms
    and ignore characters that are frequently misread.
    """
    language_opts = LanguageOptions()
    # Add terms that appear often in laboratory reports
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    # Blacklist characters that cause confusion
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)
```

**Waarom dit helpt:** Het woordenboek vertelt het OCR‑model dat “HPLC” een geldig token is, waardoor het woord niet in onzin wordt opgesplitst. De blacklist vertelt het model om ambiguë symbolen als ruis te behandelen, wat direct **improves OCR accuracy**.

## Stap 4: OCR op afbeelding uitvoeren – De kern **perform OCR on image** aanroep

Met de engine klaar en de afbeelding gekoppeld, is het tijd om de tekst daadwerkelijk te herkennen. Deze stap retourneert een `OcrResult`‑object dat je kunt raadplegen voor ruwe tekst, vertrouwensscores of begrenzingskaders.

```python
# step_4_recognize.py
def recognize_text(engine: OcrEngine) -> OcrResult:
    """
    Run the OCR process. This may take a few seconds depending on image size.
    Returns an OcrResult that contains the extracted string and metadata.
    """
    result = engine.recognize()
    return result
```

Als de afbeelding onscherp is, zie je lagere vertrouwenscijfers in het resultaat. Dat is een signaal om de afbeelding voor te bewerken (bijv. contrast verhogen) voordat je deze aan de engine geeft.

## Stap 5: Tekst uit afbeelding extraheren – De uiteindelijke string ophalen

Ten slotte vragen we de `OcrResult` om zijn tekstuele weergave. De `getText()`‑methode retourneert een platte‑tekst string die klaar is voor verdere verwerking (opslaan in een bestand, invoeren in een database, enz.).

```python
# step_5_output.py
def print_result(result: OcrResult) -> None:
    """
    Output the recognized text to the console.
    You could also write it to a file with open('output.txt', 'w') …
    """
    extracted = result.getText()
    print("=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===")
```

**Verwachte output:** Als `lab_report.png` een eenvoudige tabel bevat, zie je mogelijk iets als:

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

Dat is het **extract text from image**‑deel voltooid.

## Volledig werkend voorbeeld – Alles samenvoegen

Hieronder staat een enkel script dat de onderdelen uit de vorige secties samenvoegt. Je kunt het kopiëren‑plakken in `run_ocr.py` en uitvoeren met `python run_ocr.py`.

```python
# run_ocr.py
import os
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    engine = OcrEngine()
    return engine

def load_image(engine: OcrEngine, image_path: str) -> None:
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")
    engine.setImageFromFile(image_path)

def configure_language(engine: OcrEngine) -> None:
    language_opts = LanguageOptions()
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)

def recognize_text(engine: OcrEngine) -> OcrResult:
    return engine.recognize()

def print_result(result: OcrResult) -> None:
    extracted = result.getText()
    print("\n=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===\n")

def main() -> None:
    # 1️⃣ Create the OCR engine
    ocr_engine = build_engine()

    # 2️⃣ Load the image you want to process
    image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
    load_image(ocr_engine, image_file)

    # 3️⃣ Apply language tweaks to **improve OCR accuracy**
    configure_language(ocr_engine)

    # 4️⃣ **Perform OCR on image** – this is the heavy lifting
    ocr_result = recognize_text(ocr_engine)

    # 5️⃣ **Extract text from image** and show it
    print_result(ocr_result)

if __name__ == "__main__":
    main()
```

### Snelle verificatie‑checklist

| ✅ | Item |
|---|------|
| ✔️ | Engine is aangemaakt (`create OCR engine`) |
| ✔️ | Afbeelding is geladen (`load image for OCR`) |
| ✔️ | Taalopties zijn ingesteld (`improve OCR accuracy`) |
| ✔️ | OCR is uitgevoerd (`perform OCR on image`) |
| ✔️ | Tekst is geëxtraheerd (`extract text from image`) |

Voer het script uit en bekijk de console. Als je het “OCR Output”‑blok met de inhoud van je rapport ziet, heb je succesvol **performed OCR on image** voltooid.

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Vage invoer** | Het OCR‑model kan de tekens niet onderscheiden | Voorbewerken met OpenCV: `cv2.GaussianBlur` of DPI verhogen |
| **Verkeerde taal** | Standaardtaal kan ingesteld zijn op iets anders dan Engels | Call `engine.setLanguage("eng")` before `recognize()` |
| **Ontbrekende woordenboek‑termen** | Domeinspecifieke woorden worden onleesbaar | Add them via `setDictionary` as shown in Step 3 |
| **Blacklisted characters cause

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}