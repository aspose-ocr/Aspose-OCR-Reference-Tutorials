---
category: general
date: 2026-03-26
description: Riconosci rapidamente il testo da un'immagine imparando come caricare
  l'immagine per l'OCR ed estrarre i dati da una regione specifica. Segui questa guida
  pratica.
draft: false
keywords:
- recognize text from image
- load image for ocr
- OCR region of interest
- extract text from ROI
- Python OCR library
- image preprocessing for OCR
language: it
og_description: Riconosci il testo da un'immagine in Python caricando un'immagine
  per OCR, definendo una regione di interesse e estraendo testo pulito. Scopri l'intero
  flusso di lavoro.
og_title: Riconoscere il testo da un'immagine – Guida completa a OCR in Python
tags:
- OCR
- Python
- Image Processing
title: Riconoscere il testo da un'immagine – Tutorial Python OCR passo passo
url: /it/python-java/general/recognize-text-from-image-step-by-step-python-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# riconoscere testo da immagine – Guida completa OCR in Python

Ti è mai capitato di dover **riconoscere testo da immagine** ma non sapevi da dove cominciare? Forse hai un modulo scansionato, una ricevuta o uno screenshot e vuoi semplicemente le parole all'interno di una casella specifica. La buona notizia è che con poche righe di Python puoi **caricare immagine per OCR**, concentrarti su una singola regione e estrarre il testo esatto di cui hai bisogno—senza dover copiare manualmente.

In questo tutorial percorreremo l'intero processo: caricamento dell'immagine, definizione di una regione di interesse (ROI), esecuzione del motore OCR e stampa del risultato. Alla fine potrai incorporare questo snippet in qualsiasi progetto che deve estrarre testo da una parte specifica di un'immagine. Nessun pipeline di elaborazione immagini pesante, solo codice pulito e leggibile che funziona oggi.

## Prerequisites

- Python 3.8+ installato  
- Il pacchetto `ocr` (o qualsiasi libreria OCR compatibile) – installa con `pip install ocr-lib` (sostituisci con il nome reale del pacchetto che usi)  
- Un'immagine PNG/JPEG che contiene il modulo che desideri leggere  
- Familiarità di base con funzioni e classi Python  

Se sei già a tuo agio con questi, ottimo—puoi saltare avanti. Altrimenti, prendi un caffè veloce e assicurati che gli elementi sopra siano pronti; i passaggi successivi presumono che siano a posto.

## Step 1: Crea un'istanza del motore OCR – Core “riconoscere testo da immagine”

The first thing we need is an object that knows how to talk to the OCR engine. Think of it as the brain that will later **riconoscere testo da immagine** data.

```python
import ocr  # Import the OCR library

# Initialize the engine
ocr_engine = ocr.OcrEngine()
```

> **Why this matters:** Initializing the engine once lets you reuse settings (like language packs) across multiple images, which improves performance and keeps the code tidy.

## Step 2: **Caricare immagine per OCR** – Portare l'immagine in memoria

Now we actually **caricare immagine per OCR**. The library provides a convenient static method that reads the file and returns an object the engine can understand.

```python
# Load the source image (replace the path with your own)
image_path = "YOUR_DIRECTORY/form.png"
ocr_engine.set_image(ocr.Imaging.Image.load(image_path))
```

> **Pro tip:** If your image is large, consider resizing it before loading. Smaller images speed up OCR without sacrificing accuracy for most printed text.

## Step 3: Definisci la **regione di interesse OCR** (ROI)

Often you don’t need the whole page—just a specific box where the user filled in data. Defining a **OCR region of interest** tells the engine to ignore everything else, which reduces noise and speeds up processing.

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

## Step 4: Esegui il processo OCR – Il momento della verità

With everything set up, we finally **riconoscere testo da immagine** inside the defined ROI.

```python
# Execute OCR on the specified region
ocr_result = ocr_engine.recognize()
```

If the engine supports multiple regions, `ocr_result` will contain a list; in our single‑ROI case it’s a simple object with a `get_text()` method.

## Step 5: Estrai e stampa il testo – Ottenere l'output finale

Now we pull the plain string out of the result object and display it. This is where you can plug the output into a database, a CSV file, or any downstream logic.

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

If the OCR engine returns extra whitespace or line breaks, you can clean it with `.strip()` or a regular expression.

## Gestione dei casi limite comuni

| Situazione                              | Cosa fare                                                               |
|----------------------------------------|--------------------------------------------------------------------------|
| **Immagine a bassa risoluzione**               | Upscale with `Pillow` (`Image.resize`) before loading.                  |
| **Testo inclinato o ruotato**             | Apply a rotation correction (`ocr.Imaging.Image.rotate`).               |
| **Lingue multiple**                | Set the language pack on the engine: `ocr_engine.set_language('eng+spa')`. |
| **Nessuna ROI definita**                     | Skip `add_region_of_interest`; the engine will process the whole image. |
| **Caratteri inaspettati (es., virgole)** | Post‑process the string: `extracted_text.replace(',', '')`.            |

These tips keep your **caricare immagine per OCR** pipeline robust even when the source material isn’t perfect.

## Esempio completo funzionante – Copia, incolla, esegui

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

## Conclusione

You now have a clear, end‑to‑end method to **riconoscere testo da immagine** by first **caricare immagine per OCR**, define a precise **OCR region of interest**, and finally extract clean text. The approach works with any Python OCR library that follows the pattern shown above, and you can easily extend it to handle multiple ROIs, different languages, or pre‑processing steps.

Next, you might explore:

- **pre‑elaborazione immagine per OCR** (thresholding, denoising) to boost accuracy on noisy scans.  
- Using the **estrarre testo da ROI** result to populate a pandas DataFrame for bulk data analysis.  
- Switching to a cloud‑based OCR service (Google Vision, Azure Computer Vision) when you need higher reliability at scale.

Give it a spin, tweak the rectangle coordinates to match your own forms, and watch the automation take over. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}