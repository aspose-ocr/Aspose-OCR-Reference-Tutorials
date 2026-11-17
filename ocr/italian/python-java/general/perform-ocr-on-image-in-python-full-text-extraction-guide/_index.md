---
category: general
date: 2026-06-19
description: Esegui OCR su un'immagine usando la libreria OCR di Python. Scopri come
  rilevare il testo da un'immagine, riconoscere il testo da un JPEG e estrarre il
  testo da un'immagine scansionata in modo efficiente.
draft: false
keywords:
- perform OCR on image
- recognize text from jpeg
- detect text from image
- extract text from scanned image
- load image for OCR
language: it
og_description: Esegui OCR su un'immagine con Python ed estrai il testo da file scansionati.
  Questa guida ti accompagna passo passo nel caricamento delle immagini, nella correzione
  dell'inclinazione e nel riconoscimento del testo.
og_title: Esegui OCR su un'immagine in Python – Guida completa all'estrazione del
  testo
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  headline: Perform OCR on Image in Python – Full Text Extraction Guide
  type: TechArticle
- description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  name: Perform OCR on Image in Python – Full Text Extraction Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed (the example uses the `ocr` package available via
      `pip install ocr-lib` – replace with your actual library name). - Basic familiarity
      with Python functions and virtual environments. - An image file (JPEG, PNG,
      TIFF) you want to process; we’ll use `skewed_page.jpg` as a placeh'
  - name: Recognize Text from JPEG vs PNG
    text: 'Both formats are supported, but JPEG compression can introduce artifacts
      that confuse the engine. If you notice frequent mis‑recognitions, try converting
      the JPEG to PNG first:'
  - name: Detect Text from Image with Multiple Languages
    text: 'If your document mixes English and Spanish, set a multilingual mode:'
  - name: Extract Text from Scanned PDFs
    text: 'For PDFs, you need to rasterize each page into an image first. Libraries
      like `pdf2image` make this painless:'
  type: HowTo
- questions:
  - answer: Absolutely. The library works without a GUI; just ensure the necessary
      native binaries (e.g., Tesseract) are installed on the server.
    question: Can I run this on a headless server?
  - answer: Consider adding a sharpening filter before `engine.recognize`. Many OCR
      libraries expose `image_preprocessing.sharpen = True` or you can use OpenCV’s
      `cv2.GaussianBlur` in reverse.
    question: What if the image is blurry?
  - answer: 'Yes. Wrap `perform_ocr` in a loop over a list of file paths, ## What
      Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
      - [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
      - [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: Does the script support batch processing?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Esegui OCR su un'immagine in Python – Guida completa all'estrazione del testo
url: /it/python-java/general/perform-ocr-on-image-in-python-full-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine in Python – Guida Completa all'Estrazione del Testo

Ti è mai capitato di dover **perform OCR on image** su file immagine ma di scontrarti con un muro perché il codice sembrava criptico? Non sei l'unico. Che tu stia trasformando una pila di ricevute scannerizzate in PDF ricercabili o estraendo didascalie da un JPEG per un progetto di data‑science, la capacità di riconoscere testo da JPEG e altri formati è una competenza indispensabile per qualsiasi sviluppatore oggi.

In questo tutorial passeremo in rassegna un esempio completo e eseguibile che ti mostra come **detect text from image** file, **extract text from scanned image** documenti, e persino **load image for OCR** in poche righe. Alla fine avrai uno snippet solido, pronto per la produzione, che potrai inserire nei tuoi progetti—senza import mancanti, senza vaghi shortcut “see docs”.

## Cosa Costruirai

- Un piccolo script Python che crea un motore OCR, abilita l'auto‑deskew, carica un JPEG (o qualsiasi formato supportato) e stampa il testo riconosciuto.
- Spiegazioni del **why** di ogni impostazione, non solo del **how** da digitare.
- Suggerimenti per gestire PDF multi‑pagina, lingue non inglesi e problemi comuni come scansioni sfocate.

### Prerequisiti

- Python 3.8+ installato (l'esempio utilizza il pacchetto `ocr` disponibile tramite `pip install ocr-lib` – sostituisci con il nome della tua libreria reale).
- Familiarità di base con le funzioni Python e gli ambienti virtuali.
- Un file immagine (JPEG, PNG, TIFF) che desideri elaborare; useremo `skewed_page.jpg` come segnaposto.

> **Pro tip:** Se sei su Windows, esegui il terminale come Amministratore quando installi la libreria OCR per evitare problemi di permessi.

---

## Esegui OCR su Immagine – Configurazione e Setup

La prima cosa di cui hai bisogno è un'istanza pulita del motore OCR. Pensala come il cervello dell'operazione; senza una configurazione adeguata, anche l'immagine più nitida restituirà nonsense.

```python
# Step 1: Import the OCR library and create an engine
import ocr

engine = ocr.OcrEngine()
# Set the recognition language – English works for most cases
engine.language = ocr.Language.English
```

**Why this matters:**  
Impostare `engine.language` restringe il set di caratteri che il motore OCR si aspetta, aumentando drasticamente l'accuratezza. Se lo salti, il motore proverà a indovinare, spesso leggendo male parole semplici.

## Abilita Deskew Automatico – Correggi Scansioni Inclinate

Le pagine scannerizzate raramente sono perfettamente piatte. Una leggera inclinazione può compromettere la segmentazione dei caratteri, trasformando “Hello” in “H3llo”. Il flag `auto_deskew` fa il lavoro pesante per te.

```python
# Step 2: Turn on automatic deskew to straighten tilted images
engine.image_preprocessing.auto_deskew = True
```

**Edge case:** Se sai che le tue immagini sono già dritte, disabilitare il deskew può risparmiare qualche millisecondo di tempo di elaborazione—utile quando si gestiscono migliaia di pagine in un lavoro batch.

## Carica Immagine per OCR – Supporto JPEG, PNG, TIFF

Ora carichiamo effettivamente **load image for OCR**. Il metodo `ocr.Image.load` è flessibile; accetta un percorso a qualsiasi formato raster supportato.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/skewed_page.jpg"
image = ocr.Image.load(image_path)
```

> **Why this step is crucial:** La libreria legge il file in un bitmap interno, applicando eventuali conversioni di spazio colore necessarie. Saltare questo passaggio e passare un flusso di byte grezzo genererebbe un `FileNotFoundError` o, peggio, produrrebbe silenziosamente risultati vuoti.

Se hai bisogno di **recognize text from JPEG** file specificamente, assicurati semplicemente che l'estensione del file sia `.jpeg` o `.jpg`. La stessa chiamata funziona per PNG (`.png`) o TIFF (`.tif`) senza modifiche.

## Esegui OCR su Immagine – Esecuzione del Motore

Con il motore pronto e l'immagine in memoria, è il momento di **perform OCR on image** sui dati. Questa singola riga fa il lavoro pesante: pre‑processing, segmentazione, classificazione e assemblaggio del testo.

```python
# Step 4: Run OCR and capture the result object
result = engine.recognize(image)
```

**What happens under the hood?**  
- Il motore applica la trasformazione deskew (se abilitata).  
- Esegue una rete neurale o il backend Tesseract per identificare i caratteri.  
- Infine, unisce i caratteri in parole e linee, restituendo un ricco oggetto `result`.

## Estrai Testo da Immagine Scannerizzata – Visualizza i Risultati

L'ultimo passaggio è **extract text from scanned image** e visualizzarlo. L'attributo `result.text` contiene la rappresentazione plain‑text.

```python
# Step 5: Print the detected text to the console
print("Detected text:")
print(result.text)
```

Un output tipico appare così:

```
Detected text:
Invoice #12345
Date: 2023‑09‑01
Total: $1,234.56
Thank you for your business!
```

Se il motore OCR non riesce a trovare alcun carattere, `result.text` sarà una stringa vuota. In tal caso, ricontrolla la qualità dell'immagine o considera di regolare la proprietà `engine.confidence_threshold` (se la tua libreria la supporta).

## Gestione delle Varianti Comuni

### Riconosci Testo da JPEG vs PNG

Entrambi i formati sono supportati, ma la compressione JPEG può introdurre artefatti che confondono il motore. Se noti frequenti errori di riconoscimento, prova a convertire prima il JPEG in PNG:

```python
from PIL import Image
Image.open(image_path).save("temp.png", format="PNG")
image = ocr.Image.load("temp.png")
```

### Rileva Testo da Immagine con più Lingue

Se il tuo documento mescola inglese e spagnolo, imposta una modalità multilingue:

```python
engine.language = ocr.Language.English | ocr.Language.Spanish
```

Il motore considererà allora entrambi gli alfabeti durante il riconoscimento.

### Estrai Testo da PDF Scannerizzati

Per i PDF, è necessario rasterizzare prima ogni pagina in un'immagine. Librerie come `pdf2image` rendono questo semplice:

```python
from pdf2image import convert_from_path

pages = convert_from_path("document.pdf", dpi=300)
for i, page_image in enumerate(pages):
    image = ocr.Image.from_pil(page_image)   # assuming the library accepts a PIL image
    result = engine.recognize(image)
    print(f"Page {i+1} text:")
    print(result.text)
```

## Esempio Completo Funzionante

Di seguito trovi lo script completo che puoi copiare‑incollare in un file `ocr_demo.py`. Include la gestione degli errori e un piccolo helper per misurare il tempo di esecuzione.

```python
import ocr
import time
import sys
from pathlib import Path

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a given image file and return the extracted text.
    Handles auto‑deskew and basic error reporting.
    """
    if not Path(image_path).exists():
        sys.exit(f"❌ Error: File not found – {image_path}")

    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.image_preprocessing.auto_deskew = True

    try:
        image = ocr.Image.load(image_path)
    except Exception as e:
        sys.exit(f"❌ Failed to load image: {e}")

    start = time.time()
    result = engine.recognize(image)
    elapsed = time.time() - start

    if not result.text.strip():
        print("⚠️ No text detected. Try a higher‑resolution image or adjust preprocessing.")
    else:
        print(f"✅ OCR completed in {elapsed:.2f}s")
        print("Detected text:")
        print(result.text)

    return result.text

if __name__ == "__main__":
    # Replace with the path to your JPEG/PNG/TIFF file
    perform_ocr("YOUR_DIRECTORY/skewed_page.jpg")
```

**Expected output** (supponendo una scansione chiara):

```
✅ OCR completed in 0.87s
Detected text:
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

## Domande Frequenti

**Q: Posso eseguirlo su un server headless?**  
A: Assolutamente. La libreria funziona senza GUI; basta assicurarsi che i binari nativi necessari (ad esempio, Tesseract) siano installati sul server.

**Q: E se l'immagine è sfocata?**  
A: Considera di aggiungere un filtro di nitidezza prima di `engine.recognize`. Molte librerie OCR espongono `image_preprocessing.sharpen = True` oppure puoi usare `cv2.GaussianBlur` di OpenCV in modo inverso.

**Q: Lo script supporta l'elaborazione batch?**  
A: Sì. Avvolgi `perform_ocr` in un ciclo su una lista di percorsi file,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}