---
category: general
date: 2026-07-05
description: Voer OCR uit op een afbeelding met Python. Leer hoe je een afbeelding
  naar tekst converteert met Python, een afbeelding laadt voor OCR en Cyrillische
  tekst uit een afbeelding haalt in enkele minuten.
draft: false
keywords:
- perform OCR on image
- convert image to text python
- load image for OCR
- extract Cyrillic text from image
- recognize Cyrillic text
language: nl
og_description: Voer OCR uit op een afbeelding in Python. Deze gids laat zien hoe
  je een afbeelding naar tekst converteert met Python, een afbeelding laadt voor OCR
  en snel Cyrillische tekst uit een afbeelding haalt.
og_title: Voer OCR uit op een afbeelding met Python – Volledige tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image using Python. Learn how to convert image to text
    python, load image for OCR and extract Cyrillic text from image in minutes.
  headline: Perform OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- Cyrillic
title: Voer OCR uit op afbeelding met Python – Complete stapsgewijze gids
url: /nl/python/general/perform-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Perform OCR on Image with Python – Complete Step‑by‑Step Guide

Heb je je ooit afgevraagd hoe je **perform OCR on image** bestanden kunt verwerken zonder ze aan een externe dienst over te dragen? Je bent niet de enige. In veel projecten—paspoortscanners, kassabon‑digitizers of archiveringshulpmiddelen—het verkrijgen van ruwe tekst uit een foto is de eerste hindernis.  

In deze tutorial lopen we een praktisch voorbeeld door dat **converts image to text python** stijl, laat zien hoe je **load image for OCR** kunt doen, en uiteindelijk **extract Cyrillic text from image** met de open‑source `aocr` bibliotheek. Aan het einde kun je **recognize Cyrillic text** in elke afbeelding die je erop loslaat.

> **What you’ll walk away with:** een kant‑klaar script, duidelijke uitleg van elke stap, en tips voor het omgaan met veelvoorkomende valkuilen (zoals vage scans of onverwachte lettertypen). Geen externe API's, alleen pure Python.

---

## Prerequisites

Before we dive in, make sure you have:

- Python 3.8 of nieuwer geïnstalleerd.
- Een terminal of opdrachtprompt waar je je prettig bij voelt.
- Het `aocr` pakket (installeerbaar via `pip install aocr`).
- Een afbeeldingsbestand dat Cyrillische tekens bevat (bijv. een gescande Russische paspoort).  

If any of these sound unfamiliar, don’t panic—each bullet point will be covered briefly as we go.

---

## Step 1: Perform OCR on Image – Setting Up the Environment

The first thing we need is a clean Python environment where the OCR library lives. Using a virtual environment isolates dependencies and prevents version clashes.

```bash
# Create a virtual environment (optional but recommended)
python -m venv ocr-env
# Activate it (Windows)
ocr-env\Scripts\activate
# Activate it (macOS/Linux)
source ocr-env/bin/activate

# Install the aocr library
pip install aocr
```

**Waarom?**  
A dedicated environment ensures that the `aocr` package and its native binaries don’t interfere with other projects. It also makes reproducibility a breeze—someone else can clone your repo and run the same `pip install -r requirements.txt` command.

> **Pro tip:** Freeze je afhankelijkheden met `pip freeze > requirements.txt` zodat je altijd precies weet welke versies er zijn gebruikt.

---

## Step 2: Load Image for OCR – Importing and Preparing the File

Now that the library is ready, we need to **load image for OCR**. The `aocr.Image.from_file` method handles most common formats (PNG, JPEG, TIFF). Here’s how you do it:

```python
import aocr

# Path to the Cyrillic image – replace with your actual file location
image_path = "YOUR_DIRECTORY/rus_passport.png"

# Load the image into an aocr.Image object
cyrillic_image = aocr.Image.from_file(image_path)
```

**Wat gebeurt er hier?**  
`aocr.Image.from_file` reads the binary data, decodes it, and stores it in an object that the OCR engine can understand. If the file can’t be found, Python will raise a `FileNotFoundError`, which you can catch later if you need graceful error handling.

> **Randgeval:** Some scanners output multi‑page TIFFs. In that scenario, you’d need to split the pages first—`aocr` provides `Image.from_tiff_pages()` for that.

---

## Step 3: Configure the OCR Engine – Forcing Cyrillic Recognition

By default, many OCR engines try to guess the language, which can lead to garbled output for non‑Latin scripts. To **recognize Cyrillic text** reliably, we explicitly set the language to “cyrillic”.

```python
# Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Force the engine to use the Cyrillic recognizer
ocr_engine.language = "cyrillic"
```

**Waarom de taal forceren?**  
Cyrillic characters share visual similarities with Latin letters (e.g., “A” vs “А”). Telling the engine to expect Cyrillic reduces mis‑recognition dramatically, especially on low‑resolution scans.

---

## Step 4: Perform OCR on Image – Running the Recognition

With the image loaded and the engine tuned, we finally **perform OCR on image**. The `recognize` method returns an `OcrResult` object containing the extracted text and confidence scores.

```python
# Run the OCR process
ocr_result = ocr_engine.recognize(cyrillic_image)

# Print the raw text
print("Cyrillic text:")
print(ocr_result.text)
```

**Wat geeft `ocr_result` je?**  
- `text`: de platte tekenreeks van herkende tekens.  
- `confidence`: een float (0‑1) die de algehele zekerheid aangeeft.  
- `lines`: een lijst van lijnobjecten als je fijnmazige controle nodig hebt.

> **Veelgestelde vraag:** *Wat als de tekst ondersteboven staat?*  
> `aocr` kan afbeeldingen automatisch roteren; stel gewoon `ocr_engine.auto_rotate = True` in voordat je `recognize` aanroept.

---

## Step 5: Convert Image to Text Python – Post‑Processing the Output

The raw string may contain stray whitespace or line‑break artifacts. To **convert image to text python** style, we’ll clean it up with a few simple steps:

```python
import re

# Remove extra whitespace and normalize line breaks
clean_text = re.sub(r'\s+', ' ', ocr_result.text).strip()

print("\nCleaned Cyrillic text:")
print(clean_text)
```

**Waarom zou je het doen?**  
Cleaned output is easier to feed into downstream pipelines—whether you’re storing it in a database, feeding it to a translation API, or running regex searches for passport numbers.

---

## Step 6: Extract Cyrillic Text from Image – Putting It All Together

Let’s bundle everything into a single, reusable function. This makes **extract Cyrillic text from image** a one‑liner in your own projects.

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Loads an image, forces Cyrillic OCR, and returns cleaned text.
    """
    # Load image
    img = aocr.Image.from_file(image_path)

    # Configure OCR engine for Cyrillic
    engine = aocr.OcrEngine()
    engine.language = "cyrillic"

    # Recognize text
    result = engine.recognize(img)

    # Clean up the output
    cleaned = re.sub(r'\s+', ' ', result.text).strip()
    return cleaned

# Example usage
if __name__ == "__main__":
    path = "YOUR_DIRECTORY/rus_passport.png"
    print("Extracted text:", extract_cyrillic_text(path))
```

**Resultaat dat je zou moeten zien (voorbeeld):**

```
Extracted text: ПАСПОРТ РФ № 1234567890 ИМЯ ФАМИЛИЯ ДАТА РОЖДЕНИЯ 01.01.1990
```

If the image is crisp and the font matches the OCR model, you’ll get near‑perfect transcription.

---

## troubleshooting & Tips

| Probleem | Waarschijnlijke oorzaak | Oplossing |
|----------|--------------------------|-----------|
| Vervormde tekens | Verkeerde taalinstelling | Ensure `ocr_engine.language = "cyrillic"` |
| Lege output | Afbeelding te donker of lage resolutie | Preprocess with `opencv` to increase contrast |
| Verkeerde oriëntatie | Afbeelding gedraaid 90° | Set `ocr_engine.auto_rotate = True` |
| Trage prestaties | Grote afbeelding ( >5 MP ) | Resize with `aocr.Image.resize(width=1024)` before recognition |

---

![perform OCR op afbeelding voorbeeld](ocr_example.png "perform OCR op afbeelding voorbeeld")

*Alt‑tekst: “perform OCR on image voorbeeld dat Python‑code toont die Cyrillische tekst uit een paspoortscan extraheert.”*

---

## Conclusie

We’ve just **performed OCR on image** files using pure Python, learned how to **load image for OCR**, forced the engine to **recognize Cyrillic text**, and finally **extracted Cyrillic text from image** with a tidy helper function. The whole pipeline—from installing `aocr` to cleaning up the result—fits into a few dozen lines of code and can be dropped into any project that needs to **convert image to text python** style.

---

## Wat is het volgende?

- **Batchverwerking:** Loop over een map met scans en sla resultaten op in SQLite.  
- **Taaldetectie:** Combineer `langdetect` met `aocr` om automatisch te schakelen tussen Cyrillisch en Latijns.  
- **Geavanceerde preprocessing:** Gebruik `opencv` om afbeeldingen recht te zetten, te ontruisen of te binariseren voor hogere nauwkeurigheid.  
- **Integreren met FastAPI:** Maak de `extract_cyrillic_text` functie beschikbaar als een REST‑endpoint voor webapps.  

Feel free to experiment—swap the language to “latin” for English passports, or try a different OCR backend altogether. The concepts stay the same, and the code is flexible enough to adapt.

Happy coding, and may your images always be legible!

## Wat moet je hierna leren?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Tekst extraheren uit afbeelding met Aspose OCR – Stapsgewijze gids](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Afbeelding omzetten naar tekst – OCR uitvoeren op afbeelding vanaf URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Afbeeldingstekst extraheren C# met taalkeuze via Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}