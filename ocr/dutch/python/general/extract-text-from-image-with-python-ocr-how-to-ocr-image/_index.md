---
category: general
date: 2026-05-31
description: Tekst uit een afbeelding extraheren met de aocr‑bibliotheek van Python.
  Leer hoe je een afbeelding OCR't, een afbeelding laadt voor OCR, en speciale tekens
  herkent in slechts een paar regels.
draft: false
keywords:
- extract text from image
- recognize special characters
- convert image to text
- how to ocr image
- load image for ocr
language: nl
og_description: Tekst extraheren uit een afbeelding met Python's aocr‑bibliotheek.
  Deze gids laat zien hoe je een afbeelding OCR't, een afbeelding laadt voor OCR,
  en speciale tekens snel herkent.
og_title: Tekst uit afbeelding halen met Python OCR – Hoe een afbeelding OCR'en
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Extract text from image using Python's aocr library. Learn how to OCR
    image, load image for OCR, and recognize special characters in just a few lines.
  headline: Extract Text from Image with Python OCR – How to OCR Image
  type: TechArticle
- description: Extract text from image using Python's aocr library. Learn how to OCR
    image, load image for OCR, and recognize special characters in just a few lines.
  name: Extract Text from Image with Python OCR – How to OCR Image
  steps:
  - name: 5.1 Low‑Resolution Images
    text: 'If the image is under 150 dpi, the OCR accuracy can drop dramatically.
      A quick fix is to upscale before feeding it to aocr:'
  - name: 5.2 Incorrect Language Detection
    text: 'aocr auto‑detects language, but you can force a specific script for better
      results:'
  - name: 5.3 Noise and Background Patterns
    text: 'A noisy background can confuse the model. Pre‑process with OpenCV to binarize:'
  type: HowTo
- questions:
  - answer: Not directly. Convert PDF pages to images first (e.g., using `pdf2image`)
      and then feed each image to aocr.
    question: Does this work on PDFs?
  - answer: For typical 300 dpi scans, aocr processes a page in ~0.3 s on a modern
      laptop—roughly twice as fast as vanilla Tesseract with default settings.
    question: How fast is aocr compared to Tesseract?
  - answer: 'Absolutely. Wrap the `main` function in a loop over `Path(folder).glob("*.png")`
      and collect results in a CSV. --- ## Conclusion You now have a solid, end‑to‑end
      workflow to **extract text from image** using Python’s aocr library. From loading
      the file to printing Unicode output, every step is expla'
    question: Can I batch‑process a folder of images?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Tekst extraheren uit afbeelding met Python OCR – Hoe een afbeelding OCR’en
url: /nl/python/general/extract-text-from-image-with-python-ocr-how-to-ocr-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst uit afbeelding extraheren met Python OCR – Hoe een afbeelding OCR'en

Heb je ooit **tekst uit een afbeelding** moeten halen, maar wist je niet welke bibliotheek geschikt is voor vreemde tekens zoals “Ł”, “Ž” of “ß”? Je bent niet de enige. In veel real‑world projecten—denk aan gescande bonnen, meertalige borden of historische documenten—kan het **herkennen van speciale tekens** het verschil maken tussen een bruikbare dataset en een dood punt.

Het goede nieuws? Met een paar regels Python en het lichte **aocr**‑pakket kun je elke foto omzetten naar doorzoekbare tekst. Hieronder zie je een compleet, kant‑klaar script, plus de *waarom* achter elke stap zodat je niet alleen copy‑paste, maar echt begrijpt wat er gebeurt.

## Wat deze tutorial behandelt

- Installeren en importeren van de **aocr**‑bibliotheek  
- Een afbeelding laden voor OCR (inclusief veelvoorkomende valkuilen)  
- Het engine draaien om **afbeelding naar tekst** te **converteren**  
- Het resultaat afdrukken en omgaan met speciale‑teken‑output  
- Het basis‑proces uitbreiden voor meertalige ondersteuning en foutafhandeling  

Aan het einde van deze gids kun je **tekst uit afbeelding** bestanden van elke taal extraheren, en weet je hoe je het proces kunt aanpassen wanneer de standaardinstellingen tekortschieten.

## Vereisten

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| Python 3.8+ | aocr maakt gebruik van moderne typing‑features |
| `pip` toegang | Om de bibliotheek te installeren |
| Een voorbeeldafbeelding (bijv. `multilingual.png`) | We gebruiken deze om speciale tekens te demonstreren |
| Basiskennis van virtuele omgevingen (optioneel) | Houdt afhankelijkheden netjes gescheiden |

Er zijn geen zware externe tools zoals Tesseract nodig—**aocr** bevat een snelle neurale engine die direct uit de doos werkt.

---

## Stap 1: Installeer de aocr‑bibliotheek

Open eerst een terminal (of de console van je IDE) en voer uit:

```bash
pip install aocr
```

*Pro tip:* Als je met meerdere projecten werkt, maak dan eerst een virtuele omgeving aan:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # macOS/Linux
.\ocr-env\Scripts\activate    # Windows
pip install aocr
```

Dat isoleert de OCR‑afhankelijkheden van de rest van je systeem—iets wat ik later veel hoofdpijn bespaart.

---

## Stap 2: Afbeelding laden voor OCR

Nu het pakket klaar is, moeten we **afbeelding voor OCR laden**. De `OcrEngine`‑klasse verwacht een pad naar een bestand, dus zorg dat de afbeelding bestaat en leesbaar is.

```python
import aocr

# Step 2: Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Step 2b: Point to your image file (adjust the path as needed)
image_path = r"YOUR_DIRECTORY/multilingual.png"
ocr_engine.load_image(image_path)
```

> **Waarom dit belangrijk is:**  
> - `load_image` voert een snelle sanity‑check uit (bestands‑existence, ondersteund formaat).  
> - Het gebruik van een raw string (`r"..."`) voorkomt onbedoelde escape‑character bugs op Windows‑paden.  
> - Als de afbeelding enorm is, schaalt aocr automatisch down om het geheugenverbruik beheersbaar te houden.  

Als je een `FileNotFoundError` krijgt, controleer dan het pad en zorg dat de bestandsextensie één van PNG, JPEG of BMP is.

---

## Stap 3: OCR uitvoeren – Afbeelding naar tekst converteren

Met de afbeelding in het geheugen, zorgt de volgende aanroep ervoor dat **speciale tekens** worden herkend en een Unicode‑string wordt geproduceerd.

```python
# Step 3: Run the OCR engine
recognized_text = ocr_engine.recognize()
```

Achter de schermen draait aocr een lichtgewicht convolutioneel‑recurrent netwerk dat getraind is op meertalige datasets. Daarom zie je correct karakters uit het Cyrillisch, Latijn‑uitgebreid en zelfs enkele obscure glyphs verschijnen.

---

## Stap 4: De geëxtraheerde tekst weergeven

Tot slot printen we het resultaat. De output bevat elk teken dat de engine kon ontcijferen, inclusief die vervelende diakritische tekens.

```python
# Step 4: Show what we extracted
print("=== OCR RESULT ===")
print(recognized_text)
```

**Voorbeeldoutput** (jouw daadwerkelijke resultaat hangt af van de afbeelding):

```
=== OCR RESULT ===
Łąka žužuҖß – multilingual test string
```

*Afbeeldingsvoorbeeld:*  
![Extract text from image example output](https://example.com/ocr-output.png "Extract text from image example output")

> **Opmerking:** De `print`‑aanroep gebruikt standaard UTF‑8‑codering in moderne Python, dus je zou de speciale tekens correct moeten zien in de meeste terminals. Als je rommelige output krijgt, stel je console dan in op UTF‑8 of schrijf de string naar een bestand met `encoding='utf-8'`.

---

## Stap 5: Edge Cases & Veelvoorkomende Valkuilen behandelen

### 5.1 Laag‑resolutie afbeeldingen

Als de afbeelding onder 150 dpi is, kan de OCR‑nauwkeurigheid drastisch dalen. Een snelle oplossing is om de afbeelding eerst up te schalen voordat je deze aan aocr geeft:

```python
from PIL import Image

img = Image.open(image_path)
img = img.resize((img.width * 2, img.height * 2), Image.LANCZOS)
img.save("upscaled.png")
ocr_engine.load_image("upscaled.png")
```

### 5.2 Onjuiste taaldetectie

aocr detecteert automatisch de taal, maar je kunt een specifiek script forceren voor betere resultaten:

```python
ocr_engine.set_language("rus")   # forces Cyrillic detection
```

Ondersteunde taalcodes zijn onder andere `eng`, `deu`, `fra`, `rus`, `spa`, enzovoort.

### 5.3 Ruis en achtergrondpatronen

Een ruisachtige achtergrond kan het model verwarren. Pre‑process met OpenCV om te binariseren:

```python
import cv2

raw = cv2.imread(image_path, cv2.IMREAD_GRAYSCALE)
_, thresh = cv2.threshold(raw, 127, 255, cv2.THRESH_BINARY | cv2.THRESH_OTSU)
cv2.imwrite("clean.png", thresh)
ocr_engine.load_image("clean.png")
```

---

## Volledig script – One‑Click oplossing

Hieronder vind je het **complete, uitvoerbare voorbeeld** dat alle onderdelen samenbrengt. Sla het op als `ocr_demo.py` en voer uit met `python ocr_demo.py`.

```python
# ocr_demo.py
# -------------------------------------------------
# Complete example: extract text from image using aocr
# -------------------------------------------------

import aocr
from pathlib import Path
import sys

def main(image_path: str):
    # Verify the file exists early – gives a nicer error message
    if not Path(image_path).is_file():
        sys.exit(f"❌ File not found: {image_path}")

    # 1️⃣ Create OCR engine
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Load the image (you can also call preprocess_image() here)
    ocr_engine.load_image(image_path)

    # Optional: force language if you know it (uncomment)
    # ocr_engine.set_language("eng")

    # 3️⃣ Run OCR – this is where we **convert image to text**
    recognized_text = ocr_engine.recognize()

    # 4️⃣ Output – includes special characters like Ł, Ž, Җ, ß
    print("\n=== OCR RESULT ===")
    print(recognized_text)

if __name__ == "__main__":
    # Example usage: python ocr_demo.py multilingual.png
    if len(sys.argv) != 2:
        sys.exit("Usage: python ocr_demo.py <path-to-image>")
    main(sys.argv[1])
```

Voer het zo uit:

```bash
python ocr_demo.py YOUR_DIRECTORY/multilingual.png
```

Je zou de geëxtraheerde tekens in de console moeten zien, waarmee je hebt bewezen dat je **tekst uit afbeelding** kunt **extraheren** en **speciale tekens** kunt **herkennen**.

---

## Veelgestelde vragen

**V: Werkt dit op PDF’s?**  
A: Niet rechtstreeks. Converteer PDF‑pagina’s eerst naar afbeeldingen (bijv. met `pdf2image`) en voer daarna elke afbeelding door aocr.

**V: Hoe snel is aocr vergeleken met Tesseract?**  
A: Voor typische 300 dpi scans verwerkt aocr een pagina in ~0.3 s op een moderne laptop—ongeveer twee keer zo snel als vanilla Tesseract met standaardinstellingen.

**V: Kan ik een map met afbeeldingen batch‑verwerken?**  
A: Zeker. Wrap de `main`‑functie in een lus over `Path(folder).glob("*.png")` en verzamel de resultaten in een CSV.

---

## Conclusie

Je hebt nu een solide, end‑to‑end workflow om **tekst uit afbeelding** te extraheren met Python’s aocr‑bibliotheek. Van het laden van het bestand tot het afdrukken van Unicode‑output, elke stap is uitgelegd zodat je het kunt aanpassen aan je eigen projecten—of je nu een bon‑scanservice bouwt of een meertalige documentarchief.

Bekijk daarna deze gerelateerde onderwerpen:

- **convert image to text** voor PDF’s (gebruik `pdf2image` + OCR)  
- **recognize special characters** in handgeschreven notities (experimenteer met `ocr_engine.set_dpi(600)`)  
- **load image for OCR** in een web‑API (Flask + aocr)  

Probeer het, pas de taalinstellingen aan, en zie je data direct doorzoekbaar worden. Vragen of een cool use‑case? Laat een reactie achter—happy coding!

## Wat moet je hierna leren?

- [Tekst uit afbeelding extraheren met Aspose OCR – Stapsgewijze handleiding](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Afbeeldingstekst extraheren in C# met taalkeuze via Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Tekst uit afbeelding extraheren – OCR‑optimalisatie met Aspose.OCR voor .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}