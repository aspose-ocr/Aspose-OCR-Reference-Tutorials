---
category: general
date: 2026-06-06
description: Voer OCR uit op een afbeelding met Python en bekijk de vertrouwensscores.
  Leer hoe je woorden met een lage vertrouwensscore filtert, drempels instelt en randgevallen
  afhandelt.
draft: false
keywords:
- run OCR on image
- Python OCR tutorial
- OCR confidence threshold
- low‑confidence word detection
- image text extraction
language: nl
og_description: Voer OCR uit op een afbeelding in Python, controleer de vertrouwensniveaus
  en filter woorden met een lage vertrouwensscore. Deze tutorial leidt je stap voor
  stap door een volledig, uitvoerbaar voorbeeld.
og_title: OCR uitvoeren op afbeelding met Python – volledige gids
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  headline: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  name: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: Install and Import the OCR Engine
    text: First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box
      for many languages and gives you a confidence score per word.
  - name: Run OCR on the Image
    text: Now we actually **run OCR on image**. The `recognize_image` method from
      the original example is replaced with EasyOCR’s `readtext` call, which returns
      a list of `(bbox, text, confidence)` tuples.
  - name: Summarize Overall Confidence
    text: 'Unlike the earlier snippet that printed a single `confidence` attribute,
      EasyOCR gives a confidence per word. To get an overall sense, we’ll average
      them:'
  - name: List Low‑Confidence Words
    text: Now comes the part that directly answers the “list words whose confidence
      is below the desired threshold” requirement. We’ll set a **OCR confidence threshold**
      of 0.80 (80 %) by default, but you can adjust it.
  - name: Edge Cases & Variations
    text: 1. **Batch Processing** – If you need to **run OCR on image** files in bulk,
      wrap the above logic in a loop that iterates over a directory. 2. **Multiple
      Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine
      will detect both. 3. **Alternative Engines** – Want to try **pyte
  type: HowTo
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`)
      and then feed the PNG/JPEG into the script.
    question: Does this work with PDFs?
  - answer: 'Try image preprocessing: increase contrast, remove background noise,
      or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths`
      parameter you can tweak.'
    question: My confidence numbers are all low—what can I do?
  - answer: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter`
      where each row contains `text`, `confidence`, and bounding‑box coordinates.
    question: Can I export the results to CSV?
  - answer: 'EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed.
      Verify with `torch.cuda.is_available()` before running the script. --- ## Conclusion
      We’ve just **run OCR on image** using Python, inspected the overall confidence,
      and isolated any low‑confidence words that need a {{< /b'
    question: Is there a GPU‑accelerated version?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Voer OCR uit op een afbeelding met Python – Complete stap‑voor‑stap gids
url: /nl/python-java/general/run-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR uitvoeren op afbeelding met Python – Complete stap‑voor‑stap gids

Heb je ooit **OCR uitvoeren op afbeelding** bestanden nodig gehad, maar wist je niet hoe je er betrouwbare tekst uit kon halen? Je bent niet de enige—veel ontwikkelaars stuiten op hetzelfde probleem wanneer de geëxtraheerde woorden er wankel uitzien en de vertrouwensscore een mysterie is.

In deze gids duiken we direct in een werkende oplossing: je ziet hoe je **OCR uitvoeren op afbeelding** doet, de algehele vertrouwensscore leest, en eventuele woorden met een lage vertrouwensscore eruit haalt die handmatige controle nodig hebben. Aan het einde heb je een herbruikbaar script, begrijp je waarom elke regel belangrijk is, en weet je hoe je de vertrouwensdrempel voor je eigen projecten kunt aanpassen.

## Wat deze tutorial behandelt

We lopen de volledige workflow door—van het laden van een afbeelding tot het afdrukken van een nette rapportage van woorden die onder een vertrouwenspercentage van 80 % vielen. Onderweg bespreken we:

* Kiezen van een solide OCR-engine (we gebruiken **EasyOCR**, een populaire Python OCR-bibliotheek)  
* Interpreteren van het `confidence`‑attribuut dat elk OCR-resultaat retourneert  
* Filteren van woorden met een aangepaste **OCR confidence threshold**  
* Het script uitbreiden voor batchverwerking of alternatieve engines zoals **pytesseract**  

Ervaring met OCR is niet vereist, alleen een basiskennis van Python en een werkende omgeving (Python 3.9+ aanbevolen).  

Klaar om vage screenshots om te zetten in schone, doorzoekbare tekst? Laten we beginnen.

---

## ## Hoe OCR uitvoeren op afbeelding met Python

Het hart van de tutorial is een drie‑stappen‑fragment dat de code die je al zag weerspiegelt. Hieronder splitsen we elke regel, leggen we het waarom uit, en geven we je een volledig, kant‑en‑klaar script.

### Stap 1: Installeer en importeer de OCR-engine

Zorg er eerst voor dat de OCR-bibliotheek beschikbaar is. **EasyOCR** werkt direct uit de doos voor veel talen en geeft je een vertrouwensscore per woord.

```bash
pip install easyocr
```

```python
import easyocr  # The engine that will run OCR on image files
import os
```

*Waarom EasyOCR?* Het bevat een deep‑learning model dat getraind is op diverse datasets, waardoor je doorgaans hogere vertrouwenswaarden krijgt dan met de oudere Tesseract-engine, vooral bij afbeeldingen van gemengde kwaliteit.

> **Pro tip:** Als je in een beperkte omgeving werkt (bijv. een kleine Docker‑container), kan `pytesseract` lichter zijn, maar verlies je een deel van de moderne nauwkeurigheid die EasyOCR biedt.

### Stap 2: Voer OCR uit op de afbeelding

Nu voeren we daadwerkelijk **OCR uitvoeren op afbeelding** uit. De `recognize_image`‑methode uit het oorspronkelijke voorbeeld wordt vervangen door EasyOCR’s `readtext`‑aanroep, die een lijst van `(bbox, text, confidence)`‑tuples retourneert.

```python
# Initialize the OCR reader for English (you can add more languages as needed)
reader = easyocr.Reader(['en'])

# Path to the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "mixed_quality.png")

# Perform OCR – this is the step where we run OCR on image
ocr_results = reader.readtext(image_path, detail=1, paragraph=False)
```

Elke invoer in `ocr_results` ziet er als volgt uit:

```python
[
    ((x1, y1, x2, y2, x3, y3, x4, y4), "Detected text", 0.92),
    ...
]
```

Het derde element (`0.92` in het voorbeeld) is de vertrouwensscore, variërend van 0 tot 1.

### Stap 3: Samenvatting van de algehele vertrouwensscore

In tegenstelling tot het eerdere fragment dat één `confidence`‑attribuut afdrukte, geeft EasyOCR een vertrouwensscore per woord. Om een algemeen beeld te krijgen, nemen we hun gemiddelde:

```python
# Extract just the confidence numbers
confidences = [item[2] for item in ocr_results]

# Compute the mean confidence (overall confidence)
overall_confidence = sum(confidences) / len(confidences) if confidences else 0

print(f"Overall confidence: {overall_confidence:.2%}")
```

*Waarom gemiddeld?* Het geeft je een snelle gezondheidscheck—als de algehele vertrouwensscore onder, bijvoorbeeld, 70 % valt, moet je waarschijnlijk de afbeelding verbeteren (betere verlichting, voorbewerking, enz.).

### Stap 4: Lijst met woorden met lage vertrouwensscore

Nu volgt het deel dat direct antwoord geeft op de vereiste “lijst woorden waarvan de vertrouwensscore onder de gewenste drempel ligt”. We stellen standaard een **OCR confidence threshold** van 0.80 (80 %) in, maar je kunt deze aanpassen.

```python
# Define the confidence threshold – tweak as needed
THRESHOLD = 0.80

print("\nLow‑confidence words:")
low_confidence_found = False
for bbox, text, conf in ocr_results:
    if conf < THRESHOLD:
        low_confidence_found = True
        print(f"  • '{text}' ({conf:.2%})")
if not low_confidence_found:
    print("  All words meet the confidence threshold.")
```

De lus drukt elk woord af dat niet door de drempel kwam, samen met zijn percentage vertrouwensscore. Dit is de exacte analogie van de oorspronkelijke `for recognized_word in recognition_result.words`‑lus, maar werkt nu met het outputformaat van EasyOCR.

## ## Begrijpen van OCR‑vertrouwensscores

Vertrouwen is geen magisch getal; het is de schatting van het model hoe zeker het is van een bepaalde transcriptie. Hier zijn een paar zaken om in gedachten te houden:

| Situatie | Typische vertrouwensscore | Wat te doen |
|-----------|-------------------|------------|
| Duidelijke, hoge‑resolutie scan | 0.95 – 1.00 | Geen extra werk nodig |
| Lichte onscherpte of ongelijke verlichting | 0.80 – 0.94 | Overweeg lichte voorbewerking (contrastverhoging) |
| Zware ruis, gedraaide tekst | < 0.70 | Pas beeldvoorbewerking toe (ontkanten, ruisverwijdering) of schakel over naar een andere OCR-engine |

> **Let op:** Sommige talen (bijv. cursieve handschrift) leveren van nature lagere scores op. Pas de drempel dienovereenkomstig aan.

### Randgevallen & Variaties

1. **Batchverwerking** – Als je **OCR uitvoeren op afbeelding** bestanden in bulk moet uitvoeren, wikkel dan de bovenstaande logica in een lus die over een map iterereert.  
2. **Meerdere talen** – Geef een lijst zoals `['en', 'fr']` door aan `easyocr.Reader` en de engine detecteert beide.  
3. **Alternatieve engines** – Wil je **pytesseract** proberen? Vervang het lezer‑blok door:

   ```python
   import pytesseract
   from PIL import Image

   img = Image.open(image_path)
   raw_text = pytesseract.image_to_string(img, output_type=pytesseract.Output.DICT)
   # raw_text['text'] contains the full string,
   # raw_text['conf'] holds per‑character confidence.
   ```

   Je moet dan per‑karakter vertrouwensscores aggregeren tot per‑woord waarden—een beetje extra werk maar haalbaar.  
4. **Voorbewerkings‑trucs** – Het toepassen van OpenCV-filters (`cv2.threshold`, `cv2.GaussianBlur`) kan de vertrouwensscore voor ruisende scans verhogen.  

## ## Volledig, kant‑klaar script

Hieronder staat het volledige Python‑bestand dat je in je project kunt plaatsen. Sla het op als `ocr_report.py` en voer `python ocr_report.py` uit. Zorg ervoor dat het afbeeldingspad naar een bestaand bestand wijst.

```python
#!/usr/bin/env python3
"""
run_ocr_on_image.py

A self‑contained script that:
  1. Runs OCR on an image using EasyOCR.
  2. Prints the overall confidence.
  3. Lists any words whose confidence falls below a configurable threshold.

Author: Your Name
Date: 2026‑06‑06
"""

import os
import easyocr

# --------------------------- Configuration --------------------------- #
IMAGE_DIR = "YOUR_DIRECTORY"          # <-- Change to your folder
IMAGE_NAME = "mixed_quality.png"      # <-- Change to your file name
THRESHOLD = 0.80                       # Confidence threshold (0‑1)

# --------------------------- Helper Functions ----------------------- #
def load_image_path():
    """Construct the absolute path to the target image."""
    return os.path.join(IMAGE_DIR, IMAGE_NAME)

def run_ocr(image_path):
    """Run OCR on the image and return detailed results."""
    reader = easyocr.Reader(['en'])
    return reader.readtext(image_path, detail=1, paragraph=False)

def compute_overall_confidence(results):
    """Return the mean confidence across all detected words."""
    if not results:
        return 0.0
    confidences = [item[2] for item in results]
    return sum(confidences) / len(confidences)

def report_low_confidence_words(results, threshold):
    """Print words whose confidence is below the given threshold."""
    low_conf = [(text, conf) for _, text, conf in results if conf < threshold]
    if not low_conf:
        print("All words meet the confidence threshold.")
    else:
        for text, conf in low_conf:
            print(f"Low‑confidence word: '{text}' ({conf:.2%})")

# --------------------------- Main Execution ------------------------ #
def main():
    image_path = load_image_path()
    if not os.path.isfile(image_path):
        print(f"❌ Image not found: {image_path}")
        return

    # Step 1: Run OCR on image
    ocr_results = run_ocr(image_path)

    # Step 2: Show overall confidence
    overall = compute_overall_confidence(ocr_results)
    print(f"Overall confidence: {overall:.2%}")

    # Step 3: List low‑confidence words
    print("\n--- Low‑confidence words (threshold: {0:.0%}) ---".format(THRESHOLD))
    report_low_confidence_words(ocr_results, THRESHOLD)

if __name__ == "__main__":
    main()
```

**Verwachte output** (je cijfers zullen variëren):

```
Overall confidence: 78.45%

--- Low‑confidence words (threshold: 80%) ---
Low‑confidence word: 'recgnition' (62.13%)
Low‑confidence word: 'imgae' (57.90%)
```

Als elk woord de 80 % drempel haalt, zie je in plaats daarvan het vriendelijke bericht “All words meet the confidence threshold.”.

## ## Veelgestelde vragen (FAQ)

**Q: Werkt dit met PDF’s?**  
A: Niet direct. Converteer elke PDF‑pagina eerst naar een afbeelding (bijv. met `pdf2image`) en voer vervolgens de PNG/JPEG in het script.

**Q: Mijn vertrouwenscijfers zijn allemaal laag—wat kan ik doen?**  
A: Probeer beeldvoorbewerking: verhoog het contrast, verwijder achtergrondruis, of roteer de afbeelding naar een horizontale basislijn. EasyOCR accepteert ook een `contrast_ths`‑parameter die je kunt aanpassen.

**Q: Kan ik de resultaten exporteren naar CSV?**  
A: Zeker. Na de low‑confidence‑lus schrijf je `ocr_results` naar een `csv.DictWriter` waarbij elke rij `text`, `confidence` en de coördinaten van de begrenzings‑box bevat.

**Q: Is er een GPU‑versnelde versie?**  
A: EasyOCR gebruikt automatisch CUDA als er een compatibele GPU en PyTorch geïnstalleerd zijn. Controleer met `torch.cuda.is_available()` voordat je het script uitvoert.

## Conclusie

We hebben net **OCR uitvoeren op afbeelding** gedaan met Python, de algehele vertrouwensscore geïnspecteerd, en eventuele woorden met lage vertrouwensscore geïsoleerd die een

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe drempelwaarde in OCR‑beeldherkenning instellen](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Hoe Aspose OCR gebruiken voor JSON‑resultaat in beeldherkenning](/ocr/english/net/text-recognition/get-result-as-json/)
- [Tekst extraheren uit afbeelding – OCR‑optimalisatie met Aspose.OCR voor .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}