---
category: general
date: 2026-03-26
description: Herken snel tekst uit een afbeelding door te leren hoe je een afbeelding
  laadt voor OCR en gegevens uit een specifiek gebied extraheert. Volg deze praktische
  gids.
draft: false
keywords:
- recognize text from image
- load image for ocr
- OCR region of interest
- extract text from ROI
- Python OCR library
- image preprocessing for OCR
language: nl
og_description: Herken tekst uit een afbeelding in Python door een afbeelding te laden
  voor OCR, een interessegebied te definiëren en schone tekst te extraheren. Leer
  de volledige workflow.
og_title: herken tekst uit afbeelding – Complete Python OCR Walkthrough
tags:
- OCR
- Python
- Image Processing
title: tekst herkennen uit afbeelding – Stapsgewijze Python OCR‑handleiding
url: /nl/python-java/general/recognize-text-from-image-step-by-step-python-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tekst herkennen van afbeelding – Complete Python OCR Walkthrough

Heb je ooit **tekst herkennen van afbeelding** moeten doen, maar wist je niet waar te beginnen? Misschien heb je een gescande formulier, een bonnetje of een screenshot en wil je alleen de woorden binnen een bepaald vakje. Het goede nieuws is dat je met een paar regels Python de afbeelding kunt laden voor OCR, je kunt richten op één regio, en de exacte tekst kunt ophalen die je nodig hebt — geen handmatig kopiëren meer.

In deze tutorial lopen we het volledige proces door: de afbeelding laden, een regio van interesse (ROI) definiëren, de OCR‑engine uitvoeren en het resultaat afdrukken. Aan het einde kun je dit fragment in elk project embedden dat tekst moet extraheren uit een specifiek deel van een afbeelding. Geen zware beeldverwerkings‑pipelines, alleen schone, leesbare code die vandaag werkt.

## Prerequisites

- Python 3.8+ geïnstalleerd  
- Het `ocr`‑pakket (of een andere compatibele OCR‑bibliotheek) – installeer met `pip install ocr-lib` (vervang door de daadwerkelijke pakketnaam die je gebruikt)  
- Een PNG/JPEG‑afbeelding die het formulier bevat dat je wilt lezen  
- Basiskennis van Python‑functies en -klassen  

Als je hier al vertrouwd mee bent, prima — je kunt verder gaan. Zo niet, pak dan een snelle koffie en zorg dat de bovenstaande items klaarstaan; de latere stappen gaan ervan uit dat ze beschikbaar zijn.

## Step 1: Create an OCR Engine Instance – “recognize text from image” Core

Het eerste wat we nodig hebben is een object dat weet hoe het met de OCR‑engine moet communiceren. Beschouw het als het brein dat later **tekst herkennen van afbeelding** data zal verwerken.

```python
import ocr  # Import the OCR library

# Initialize the engine
ocr_engine = ocr.OcrEngine()
```

> **Why this matters:** Initializing the engine once lets you reuse settings (like language packs) across multiple images, which improves performance and keeps the code tidy.

## Step 2: Load Image for OCR – Bringing the Picture Into Memory

Nu **load image for OCR** we daadwerkelijk. De bibliotheek biedt een handige statische methode die het bestand leest en een object teruggeeft dat de engine kan begrijpen.

```python
# Load the source image (replace the path with your own)
image_path = "YOUR_DIRECTORY/form.png"
ocr_engine.set_image(ocr.Imaging.Image.load(image_path))
```

> **Pro tip:** Als je afbeelding groot is, overweeg dan om deze te verkleinen vóór het laden. Kleinere afbeeldingen versnellen OCR zonder de nauwkeurigheid voor de meeste gedrukte tekst te verliezen.

## Step 3: Define the OCR Region of Interest (ROI)

Vaak heb je niet de hele pagina nodig — alleen een specifiek vakje waar de gebruiker gegevens heeft ingevuld. Het definiëren van een **OCR region of interest** vertelt de engine om de rest te negeren, wat ruis vermindert en de verwerking versnelt.

```python
# Define ROI: (left, top, width, height) in pixels
region_of_interest = ocr.Rectangle(120, 340, 560, 90)

# Register the ROI with the engine
ocr_engine.add_region_of_interest(region_of_interest)
```

> **Why focus on ROI?**  
> - **Speed:** The engine scans fewer pixels.  
> - **Accuracy:** Background graphics outside the ROI can confuse character recognition.  
> - **Simplicity:** You get a clean string that corresponds exactly to the field you care about.

## Step 4: Run the OCR Process – The Moment of Truth

Met alles ingesteld, **recognize text from image** we eindelijk binnen de gedefinieerde ROI.

```python
# Execute OCR on the specified region
ocr_result = ocr_engine.recognize()
```

Als de engine meerdere regio's ondersteunt, zal `ocr_result` een lijst bevatten; in ons enkel‑ROI‑geval is het een eenvoudig object met een `get_text()`‑methode.

## Step 5: Extract and Print the Text – Getting the Final Output

Nu halen we de platte string uit het resultaatobject en tonen deze. Hier kun je de output naar een database, een CSV‑bestand of andere downstream‑logica sturen.

```python
# Retrieve the recognized text
extracted_text = ocr_result.get_text()

# Show the result
print("Text inside ROI:\n", extracted_text)
```

**Expected output** (example for a filled‑in name field):

```
Text inside ROI:
 John Doe
```

Als de OCR‑engine extra witruimte of regeleinden teruggeeft, kun je deze opschonen met `.strip()` of een reguliere expressie.

## Handling Common Edge Cases

| Situation                              | What to Do                                                               |
|----------------------------------------|--------------------------------------------------------------------------|
| **Low‑resolution image**               | Upscale with `Pillow` (`Image.resize`) before loading.                  |
| **Skewed or rotated text**             | Apply a rotation correction (`ocr.Imaging.Image.rotate`).               |
| **Multiple languages**                | Set the language pack on the engine: `ocr_engine.set_language('eng+spa')`. |
| **No ROI defined**                     | Skip `add_region_of_interest`; the engine will process the whole image. |
| **Unexpected characters (e.g., commas)** | Post‑process the string: `extracted_text.replace(',', '')`.            |

These tips keep your **load image for OCR** pipeline robust even when the source material isn’t perfect.

## Full Working Example – Copy, Paste, Run

Below is the complete script you can drop into a `.py` file and execute. It includes all imports, error handling, and a tiny helper that verifies the image exists.

```python
import os
import ocr

def recognize_text_from_image(image_path: str,
                              roi: tuple = (120, 340, 560, 90)):
    """
    Recognize text from a specific region of an image.

    Parameters
    ----------
    image_path : str
        Full path to the image file.
    roi : tuple
        (left, top, width, height) defining the region of interest.

    Returns
    -------
    str
        The extracted text, stripped of surrounding whitespace.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Step 1 – create engine
    engine = ocr.OcrEngine()

    # Step 2 – load image for OCR
    engine.set_image(ocr.Imaging.Image.load(image_path))

    # Step 3 – define ROI
    left, top, width, height = roi
    engine.add_region_of_interest(ocr.Rectangle(left, top, width, height))

    # Step 4 – run OCR
    result = engine.recognize()

    # Step 5 – extract text
    text = result.get_text().strip()
    return text


if __name__ == "__main__":
    # Adjust the path to point at your form image
    img_path = "YOUR_DIRECTORY/form.png"

    try:
        roi_text = recognize_text_from_image(img_path)
        print("Text inside ROI:\n", roi_text)
    except Exception as e:
        print("OCR failed:", e)
```

Running this script prints the cleaned string from the ROI, giving you a ready‑to‑use piece of data.

## Conclusion

You now have a clear, end‑to‑end method to **recognize text from image** by first **load image for OCR**, define a precise **OCR region of interest**, and finally extract clean text. The approach works with any Python OCR library that follows the pattern shown above, and you can easily extend it to handle multiple ROIs, different languages, or pre‑processing steps.

Next, you might explore:

- **image preprocessing for OCR** (thresholding, denoising) to boost accuracy on noisy scans.  
- Using the **extract text from ROI** result to populate a pandas DataFrame for bulk data analysis.  
- Switching to a cloud‑based OCR service (Google Vision, Azure Computer Vision) when you need higher reliability at scale.

Give it a spin, tweak the rectangle coordinates to match your own forms, and watch the automation take over. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}