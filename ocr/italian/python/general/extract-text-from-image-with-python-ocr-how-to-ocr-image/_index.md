---
category: general
date: 2026-05-31
description: Estrai il testo da un'immagine usando la libreria aocr di Python. Scopri
  come fare OCR su un'immagine, caricare l'immagine per l'OCR e riconoscere caratteri
  speciali in poche righe.
draft: false
keywords:
- extract text from image
- recognize special characters
- convert image to text
- how to ocr image
- load image for ocr
language: it
og_description: Estrai il testo da un'immagine usando la libreria aocr di Python.
  Questa guida mostra come fare OCR su un'immagine, caricare l'immagine per l'OCR
  e riconoscere rapidamente i caratteri speciali.
og_title: Estrai testo da un'immagine con Python OCR – Come fare OCR su un'immagine
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
title: Estrai testo da immagine con Python OCR – Come fare OCR su un'immagine
url: /it/python/general/extract-text-from-image-with-python-ocr-how-to-ocr-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da immagine con Python OCR – Come fare OCR su un'immagine

Hai mai avuto bisogno di **estrarre testo da un'immagine** ma non eri sicuro quale libreria potesse gestire simboli strani come “Ł”, “Ž” o “ß”? Non sei il solo. In molti progetti reali—pensa a ricevute scannerizzate, segnaletica multilingue o documenti storici—la capacità di **riconoscere caratteri speciali** può fare la differenza tra un dataset utilizzabile e un vicolo cieco.

La buona notizia? Con poche righe di Python e il leggero pacchetto **aocr**, puoi convertire qualsiasi immagine in testo ricercabile. Di seguito troverai uno script completo, pronto all'uso, più il *perché* di ogni passaggio così non ti limiterai a copiare‑incollare, ma comprenderai davvero cosa sta succedendo.

## Cosa Copre Questo Tutorial

- Installare e importare la libreria **aocr**  
- Caricare un'immagine per OCR (inclusi i problemi comuni)  
- Eseguire il motore per **convertire l'immagine in testo**  
- Stampare il risultato e gestire l'output dei caratteri speciali  
- Estendere il flusso di base per il supporto multilingua e la gestione degli errori  

Alla fine di questa guida sarai in grado di **estrarre testo da immagine** di qualsiasi lingua e saprai come affinare il processo quando le impostazioni predefinite non bastano.

## Prerequisiti

| Requisito | Perché è importante |
|-----------|----------------------|
| Python 3.8+ | aocr si basa su funzionalità di typing moderne |
| `pip` access | Per installare la libreria |
| Un'immagine di esempio (ad es., `multilingual.png`) | La useremo per mostrare i caratteri speciali |
| Familiarità di base con gli ambienti virtuali (opzionale) | Mantiene le dipendenze ordinate |

Non sono necessari strumenti esterni pesanti come Tesseract—**aocr** include un motore neurale veloce che funziona subito.

---

## Passo 1: Installa la Libreria aocr

Per prima cosa, apri un terminale (o la console del tuo IDE) ed esegui:

```bash
pip install aocr
```

*Pro tip:* Se gestisci più progetti, crea prima un ambiente virtuale:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # macOS/Linux
.\ocr-env\Scripts\activate    # Windows
pip install aocr
```

Questo isola le dipendenze OCR dal resto del sistema—qualcosa che ho scoperto salvare molte seccature in seguito.

---

## Passo 2: Carica l'Immagine per OCR

Ora che il pacchetto è pronto, dobbiamo **caricare l'immagine per OCR**. La classe `OcrEngine` si aspetta un percorso verso un file, quindi assicurati che l'immagine esista e sia leggibile.

```python
import aocr

# Step 2: Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Step 2b: Point to your image file (adjust the path as needed)
image_path = r"YOUR_DIRECTORY/multilingual.png"
ocr_engine.load_image(image_path)
```

> **Perché è importante:**  
> - `load_image` esegue un rapido controllo di coerenza (esistenza del file, formato supportato).  
> - Usare una stringa grezza (`r"..."`) evita bug accidentali di caratteri di escape nei percorsi Windows.  
> - Se l'immagine è molto grande, aocr la ridimensionerà automaticamente per mantenere un uso della memoria ragionevole.  

Se ricevi un `FileNotFoundError`, ricontrolla il percorso e assicurati che l'estensione del file sia una tra PNG, JPEG o BMP.

---

## Passo 3: Esegui OCR – Converti l'Immagine in Testo

Con l'immagine in memoria, la chiamata successiva **riconosce i caratteri speciali** e produce una stringa Unicode.

```python
# Step 3: Run the OCR engine
recognized_text = ocr_engine.recognize()
```

Dietro le quinte, aocr esegue una rete convoluzionale‑ricorrente leggera addestrata su dataset multilingue. Ecco perché vedrai correttamente caratteri cirillici, latino‑esteso e persino alcuni glifi poco comuni.

---

## Passo 4: Visualizza il Testo Estratto

Infine, stampiamo il risultato. L'output includerà ogni carattere che il motore è riuscito a decifrare, compresi i fastidiosi diacritici.

```python
# Step 4: Show what we extracted
print("=== OCR RESULT ===")
print(recognized_text)
```

**Esempio di output** (il risultato reale dipenderà dal contenuto dell'immagine):

```
=== OCR RESULT ===
Łąka žužuҖß – multilingual test string
```

*Esempio di immagine:*  
![Esempio di output di estrazione testo da immagine](https://example.com/ocr-output.png "Esempio di output di estrazione testo da immagine")

> **Nota:** La chiamata `print` utilizza la codifica UTF‑8 per impostazione predefinita in Python moderno, quindi dovresti vedere correttamente i caratteri speciali nella maggior parte dei terminali. Se l'output appare corrotto, imposta la console su UTF‑8 o scrivi la stringa su un file con `encoding='utf-8'`.

---

## Passo 5: Gestione dei Casi Limite e Problemi Comuni

### 5.1 Immagini a Bassa Risoluzione

Se l'immagine è inferiore a 150 dpi, l'accuratezza OCR può calare drasticamente. Una soluzione rapida è ingrandire l'immagine prima di passarla a aocr:

```python
from PIL import Image

img = Image.open(image_path)
img = img.resize((img.width * 2, img.height * 2), Image.LANCZOS)
img.save("upscaled.png")
ocr_engine.load_image("upscaled.png")
```

### 5.2 Rilevamento Errato della Lingua

aocr rileva automaticamente la lingua, ma puoi forzare uno script specifico per risultati migliori:

```python
ocr_engine.set_language("rus")   # forces Cyrillic detection
```

I codici lingua supportati includono `eng`, `deu`, `fra`, `rus`, `spa`, ecc.

### 5.3 Rumore e Pattern di Sfondo

Uno sfondo rumoroso può confondere il modello. Pre‑processa con OpenCV per binarizzare:

```python
import cv2

raw = cv2.imread(image_path, cv2.IMREAD_GRAYSCALE)
_, thresh = cv2.threshold(raw, 127, 255, cv2.THRESH_BINARY | cv2.THRESH_OTSU)
cv2.imwrite("clean.png", thresh)
ocr_engine.load_image("clean.png")
```

---

## Script Completo – Soluzione One‑Click

Di seguito trovi l'**esempio completo e eseguibile** che unisce tutti i pezzi. Salvalo come `ocr_demo.py` ed esegui `python ocr_demo.py`.

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

Eseguilo così:

```bash
python ocr_demo.py YOUR_DIRECTORY/multilingual.png
```

Dovresti vedere i caratteri estratti stampati nella console, confermando che hai **estratto testo da immagine** e **riconosciuto caratteri speciali** con successo.

---

## Domande Frequenti

**D: Questo funziona sui PDF?**  
R: Non direttamente. Converti prima le pagine PDF in immagini (ad es., usando `pdf2image`) e poi passa ogni immagine a aocr.

**D: Quanto è veloce aocr rispetto a Tesseract?**  
R: Per scansioni tipiche a 300 dpi, aocr elabora una pagina in ~0.3 s su un laptop moderno—circa il doppio più veloce rispetto a Tesseract vanilla con impostazioni predefinite.

**D: Posso elaborare in batch una cartella di immagini?**  
R: Assolutamente. Avvolgi la funzione `main` in un ciclo su `Path(folder).glob("*.png")` e raccogli i risultati in un CSV.

---

## Conclusione

Ora disponi di un flusso di lavoro solido, end‑to‑end, per **estrarre testo da immagine** usando la libreria aocr di Python. Dal caricamento del file alla stampa dell'output Unicode, ogni passaggio è spiegato così da poterlo adattare ai tuoi progetti—che tu stia costruendo un servizio di scansione ricevute o un archivio documenti multilingue.

Successivamente, considera di approfondire questi argomenti correlati:

- **convert image to text** per PDF (usa `pdf2image` + OCR)  
- **recognize special characters** in note scritte a mano (sperimenta con `ocr_engine.set_dpi(600)`)  
- **load image for OCR** in una API web (Flask + aocr)  

Provalo, modifica le impostazioni della lingua e guarda i tuoi dati diventare immediatamente ricercabili. Hai domande o un caso d'uso interessante? Lascia un commento qui sotto—buona programmazione!

## Cosa Dovresti Imparare Dopo?

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}