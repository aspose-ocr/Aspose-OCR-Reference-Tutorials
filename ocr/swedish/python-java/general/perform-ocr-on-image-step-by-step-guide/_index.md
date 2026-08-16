---
category: general
date: 2026-03-18
description: Utför OCR på en bild för att snabbt extrahera text från bilden. Lär dig
  hur du laddar bilden för OCR, skapar OCR-motorn och förbättrar OCR‑noggrannheten
  med språkalternativ.
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: sv
og_description: Utför OCR på bild med den här detaljerade guiden. Lär dig att ladda
  bild för OCR, skapa OCR-motor och förbättra OCR‑noggrannheten för pålitlig textutvinning.
og_title: Utför OCR på bild – Komplett programmeringshandledning
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Utför OCR på bild – Steg‑för‑steg guide
url: /sv/python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utför OCR på bild – Komplett programmeringshandledning

Har du någonsin behövt **perform OCR on image** men varit osäker på vilket bibliotek du ska välja eller hur du får pålitliga resultat? Du är inte ensam. I den här guiden går vi igenom allt du behöver för att **extract text from image**, från att ladda bilden till att justera språkalternativ så att du kan **improve OCR accuracy** i varje steg.

Vi kommer att gå igenom hur man **load image for OCR**, hur man **create OCR engine**, och varför varje inställning är viktig. I slutet har du ett färdigt skript som skriver ut den igenkända texten, och du förstår “varför” bakom varje rad—inga vaga “see the docs”-genvägar. Låt oss dyka ner.

## Vad du behöver

- Python 3.8+ (koden använder f‑strings och typindikeringar)
- Det hypotetiska paketet `ocr_lib` – installera med `pip install ocr_lib`
- En bildfil som innehåller tydlig, tryckt text (t.ex. `lab_report.png`)
- En enkel textredigerare eller IDE (VS Code, PyCharm, vad du föredrar)

Om du redan har dem, bra—du är klar. Om inte, hämta Python från python.org och kör pip‑kommandot; det tar bara en minut.

![perform OCR on image – exempel på utdata som visar extraherad text](/images/ocr-example.png)

*Alt text: perform OCR on image – exempel på utdata som visar extraherad text.*

## Steg 1: Skapa OCR‑motor – Hur man **create OCR engine** i Python

Innan någon igenkänning kan ske behöver biblioteket ett motorobjekt som innehåller konfiguration och körningsstatus. Tänk på motorn som hjärnan bakom operationen.

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

**Why this matters:** Att instansiera motorn tidigt låter dig fästa språkalternativ senare, och den cachar också interna modeller för snabbare efterföljande anrop.

## Steg 2: Ladda bild för OCR – Det korrekta sättet att **load image for OCR**

Nu när vi har en motor måste vi ge den något att läsa. Metoden `setImageFromFile` accepterar en filsökväg; sökvägen kan vara absolut eller relativ till skriptets arbetskatalog.

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**Pro tip:** Använd en absolut sökväg eller `os.path.join` för att undvika “file not found”-överraskningar när skriptet körs från en annan mapp.

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## Steg 3: Förbättra OCR‑noggrannhet – Justera **language options** för att **improve OCR accuracy**

Standard‑OCR fungerar, men domänspecifika vokabulärer (som laboratoriejargon) får den ofta att snubbla. Genom att mata in en anpassad ordlista och en svartlista minskar du feligenkänningar som att förväxla “0” med “O”.

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

**Why this helps:** Ordlistan talar om för OCR‑modellen att “HPLC” är ett giltigt token, vilket förhindrar att ordet bryts upp i nonsens. Svartlistan instruerar modellen att behandla tvetydiga symboler som brus, vilket direkt **improves OCR accuracy**.

## Steg 4: Utför OCR på bild – Det centrala **perform OCR on image**‑anropet

Med motorn förberedd och bilden bifogad är det dags att faktiskt känna igen texten. Detta steg returnerar ett `OcrResult`‑objekt som du kan fråga efter råtext, förtroendesiffror eller avgränsningsrutor.

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

Om bilden är suddig kommer du att se lägre förtroendesiffror i resultatet. Det är en signal att förbehandla bilden (t.ex. öka kontrasten) innan du matar den till motorn.

## Steg 5: Extrahera text från bild – Hämta den slutliga strängen

Till sist ber vi `OcrResult` om dess textrepresentation. Metoden `getText()` returnerar en ren textsträng som är klar för vidare bearbetning (spara till en fil, mata in i en databas, osv.).

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

**Expected output:** Om vi antar att `lab_report.png` innehåller ett enkelt bord, kan du se något i stil med:

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

Det är delen **extract text from image** klar.

## Fullt fungerande exempel – Sätt ihop allt

Nedan är ett enda skript som syr ihop delarna från de föregående sektionerna. Du kan kopiera‑klistra in det i `run_ocr.py` och köra `python run_ocr.py`.

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

### Snabb verifieringschecklista

| ✅ | Punkt |
|---|------|
| ✔️ | Engine är skapad (`create OCR engine`) |
| ✔️ | Bild är laddad (`load image for OCR`) |
| ✔️ | Språkalternativ är inställda (`improve OCR accuracy`) |
| ✔️ | OCR utförs (`perform OCR on image`) |
| ✔️ | Text extraheras (`extract text from image`) |

Kör skriptet och titta på konsolen. Om du ser “OCR Output”-blocket med ditt rapports innehåll har du lyckats **perform OCR on image**.

## Vanliga fallgropar & hur du undviker dem

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| **Blurry input** | OCR‑modellen kan inte skilja tecken | Förbehandla med OpenCV: `cv2.GaussianBlur` eller öka DPI |
| **Wrong language** | Standardspråket kan vara satt till något annat än engelska | Anropa `engine.setLanguage("eng")` före `recognize()` |
| **Missing dictionary terms** | Domänspecifika ord blir förvrängda | Lägg till dem via `setDictionary` som visas i Steg 3 |
| **Blacklisted characters cause

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}