---
category: general
date: 2026-06-22
description: Ottieni le coordinate del bounding box dalle immagini usando Python.
  Impara come estrarre il testo da un'immagine con Python, Aspose OCR e il parsing
  JSON in pochi minuti.
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: it
og_description: Ottieni le coordinate della bounding box dalle immagini usando Python.
  Questa guida mostra come estrarre il testo da un'immagine con Python usando Aspose
  OCR e analizzare i dati di layout.
og_title: Ottieni le coordinate della bounding box dall'OCR in Python – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  headline: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  type: TechArticle
- description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  name: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - An active Aspose.OCR for Python
      license or a free trial (the library works without a license but adds a watermark).
      - `pip install aspose-ocr` (the package name on PyPI). - A sample image called
      `invoice.png` placed in a folder you can reference.'
  - name: 1. Convert Bounding Boxes to Simple Rectangles
    text: 'If your downstream tool expects `(x, y, width, height)` instead of eight
      points, add a helper:'
  - name: 2. Handle Multi‑Page PDFs
    text: 'Aspose OCR can accept PDF streams. Replace the image loading line with:'
  - name: 3. Visualize Bounding Boxes
    text: 'If you want to see the boxes drawn on the original image, use Pillow:'
  type: HowTo
- questions:
  - answer: For large documents, consider streaming the JSON or processing page‑by‑page
      to keep memory usage low.
    question: What if the JSON is huge?
  - answer: Low contrast or handwritten text often trips OCR engines. Pre‑process
      the image (increase contrast, binarize) before feeding it to Aspose.
    question: Why are some words missing?
  - answer: Yes—set `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`
      to receive a `"characters"` array with its own `boundingBox`.
    question: Can I get character‑level coordinates?
  - answer: Absolutely. (0, 0) is the top‑left corner of the image.
    question: Is the coordinate system zero‑based?
  type: FAQPage
tags:
- OCR
- Python
- JSON
- Image Processing
title: Ottieni le coordinate del rettangolo di delimitazione dall'OCR in Python –
  Guida completa
url: /it/python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ottieni le coordinate della Bounding Box da OCR in Python – Guida completa

Ti è mai capitato di dover **ottenere le coordinate della bounding box** per ogni parola in una fattura scansionata, ma non sapevi da dove cominciare? Non sei l'unico. In molti progetti di automazione, è necessario individuare il testo su un'immagine per evidenziarlo, censurarlo o inviarlo a analisi successive. La buona notizia? Con poche righe di Python e Aspose.OCR puoi estrarre sia il testo **e** la sua posizione esatta in un solo passaggio.

In questo tutorial percorreremo un esempio pratico che ti mostra come **estrarre testo da un'immagine in stile Python**, per poi approfondire i dati di layout JSON e recuperare le bounding box. Niente superfluo, solo uno script funzionante, spiegazioni sul perché di ogni passaggio e consigli per evitare gli errori più comuni.

---

## Cosa Costruirai

Al termine di questa guida avrai uno script Python pronto all'uso che:

1. Carica un'immagine (ad esempio, un PNG di fattura) in Aspose OCR.
2. Configura il motore per emettere le informazioni di layout in JSON.
3. Analizza il JSON in un dizionario Python.
4. Itera su ogni parola riconosciuta, stampando il suo testo **e** le coordinate della sua bounding box.

Vedrai anche come adattare il codice per PDF multi‑pagina, diversi formati immagine e sistemi di coordinate personalizzati.

### Prerequisiti

- Python 3.8+ installato sulla tua macchina.  
- Una licenza attiva di Aspose.OCR per Python o una prova gratuita (la libreria funziona senza licenza ma aggiunge una filigrana).  
- `pip install aspose-ocr` (il nome del pacchetto su PyPI).  
- Un'immagine di esempio chiamata `invoice.png` posizionata in una cartella a cui puoi fare riferimento.

È tutto—nessun framework ingombrante, nessun servizio esterno. Immergiamoci.

## Passo 1: Installa e Importa le Librerie Necessarie

Per prima cosa, assicurati che il pacchetto Aspose OCR e il modulo integrato `json` siano disponibili. Il modulo `json` è incluso in Python, quindi dobbiamo solo installare Aspose.

```bash
pip install aspose-ocr
```

Ora importali nel tuo script:

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **Perché è importante:** Importare `aspose.ocr` ti dà accesso al motore OCR ad alte prestazioni, mentre `json` ti consente di trasformare la stringa di layout grezza in un dizionario Python nativo per una facile traversata.

## Passo 2: Crea il Motore OCR e Carica la Tua Immagine

Il motore è il cuore del processo. Lo istanzi, poi lo indirizzi verso l'immagine che desideri analizzare.

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **Consiglio professionale:** Sostituisci `"YOUR_DIRECTORY/invoice.png"` con un percorso assoluto o relativo che punti al tuo file reale. Se il file non viene trovato, Aspose solleverà un `FileNotFoundError`, quindi ricontrolla l'ortografia.

## Passo 3: Configura il Motore per Restituire Dati di Layout JSON

Aspose OCR può restituire testo semplice, JSON solo OCR, o un JSON di layout completo che include le coordinate per parole, linee e persino singoli caratteri. Per **ottenere le coordinate della bounding box**, ci serve il JSON di layout.

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **Perché JSON?** JSON è indipendente dal linguaggio, leggibile dall'uomo e si mappa facilmente a dizionari Python. Il JSON di layout contiene un array `"words"` dove ogni voce contiene il testo e un array `boundingBox` di otto numeri (i quattro punti d'angolo).

## Passo 4: Esegui il Riconoscimento e Ottieni la Stringa JSON Grezza

Ora eseguiamo effettivamente l'OCR. Il metodo `recognize()` restituisce un oggetto `OcrResult`, dal quale possiamo estrarre la stringa JSON.

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

Se stampi `layout_json` vedrai qualcosa del genere:

```json
{
  "words": [
    {
      "text": "Invoice",
      "boundingBox": [12, 34, 112, 34, 112, 58, 12, 58]
    },
    {
      "text": "#12345",
      "boundingBox": [130, 34, 210, 34, 210, 58, 130, 58]
    }
    // ... more words ...
  ]
}
```

> **Caso limite:** Alcune immagini possono produrre array `"words"` vuoti se il motore OCR non riesce a rilevare alcun testo. In tal caso, verifica la qualità dell'immagine (contrasto, risoluzione) prima di procedere.

## Passo 5: Analizza il JSON in un Dizionario Python

Lavorare con strutture Python native è molto più semplice che manipolare stringhe. Usa la funzione `json.loads()` per convertire la stringa.

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

Ora `layout_data["words"]` è una lista di dizionari, ciascuno rappresentante una parola e la sua bounding box.

## Passo 6: Itera sulle Parole e **Ottieni le Coordinate della Bounding Box**

Ecco il cuore del nostro tutorial: iterare su ogni parola, estrarre il testo e stampare le coordinate. Questo è il punto esatto in cui **otteniamo le coordinate della bounding box**.

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**Output di esempio** (i tuoi numeri differiranno in base all'immagine):

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **Perché il formato a otto punti?** I quattro angoli (alto‑sinistra, alto‑destra, basso‑destra, basso‑sinistra) ti permettono di disegnare un poligono attorno alla parola, anche se il testo è inclinato. Se ti serve solo un rettangolo semplice, puoi calcolare `x_min = min(x1, x2, x3, x4)`, `y_min = min(y1, y2, y3, y4)`, `width = max(x…) - x_min`, e `height = max(y…) - y_min`.

## Miglioramenti Opzionali

### 1. Converti le Bounding Box in Rettangoli Semplici

Se il tuo strumento a valle si aspetta `(x, y, width, height)` invece di otto punti, aggiungi una funzione di supporto:

```python
def box_to_rect(box):
    xs = box[0::2]  # extract x coordinates
    ys = box[1::2]  # extract y coordinates
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min, x_max - x_min, y_max - y_min)

for word in layout_data["words"]:
    rect = box_to_rect(word["boundingBox"])
    print(f"'{word['text']}' rectangle {rect}")
```

### 2. Gestisci PDF Multi‑Pagina

Aspose OCR può accettare flussi PDF. Sostituisci la riga di caricamento dell'immagine con:

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

Itera `set_page_number` per ogni pagina, raccogliendo le coordinate per pagina.

### 3. Visualizza le Bounding Box

Se vuoi vedere le box disegnate sull'immagine originale, usa Pillow:

```python
from PIL import Image, ImageDraw

img = Image.open("YOUR_DIRECTORY/invoice.png")
draw = ImageDraw.Draw(img)

for word in layout_data["words"]:
    box = word["boundingBox"]
    # Pillow expects a list of tuples [(x1,y1), (x2,y2), ...]
    polygon = [(box[i], box[i+1]) for i in range(0, len(box), 2)]
    draw.line(polygon + [polygon[0]], fill="red", width=2)

img.show()
```

Ora vedrai contorni rossi attorno a ogni parola riconosciuta—perfetto per il debug o per sovrapposizioni UI.

## Domande Frequenti & Problemi Comuni

- **E se il JSON è enorme?** Per documenti di grandi dimensioni, considera lo streaming del JSON o l'elaborazione pagina per pagina per mantenere basso l'uso di memoria.
- **Perché alcune parole mancano?** Basso contrasto o testo scritto a mano spesso ostacolano i motori OCR. Pre‑elabora l'immagine (aumenta il contrasto, binarizza) prima di inviarla ad Aspose.
- **Posso ottenere coordinate a livello di carattere?** Sì—imposta `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)` per ricevere un array `"characters"` con il proprio `boundingBox`.
- **Il sistema di coordinate è basato su zero?** Assolutamente. (0, 0) è l'angolo in alto a sinistra dell'immagine.

## Script Completo – Pronto da Copiare & Eseguire

Di seguito trovi l'esempio completo e eseguibile che combina tutti i passaggi. Salvalo come `extract_bboxes.py` ed esegui `python extract_bboxes.py`.

```python
import aspose.ocr as ocr
import json

# -------------------------
# 1️⃣ Initialize OCR engine
# -------------------------
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))

# -------------------------------------------------
# 2️⃣ Ask for JSON layout output (contains bounding boxes)
# -------------------------------------------------
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)

# -------------------------
# 3️⃣ Run recognition
# -------------------------
result = engine.recognize()
layout_json = result.get_json()

# -------------------------
# 4️⃣ Parse JSON
# -------------------------
layout_data = json.loads(layout_json)

# -------------------------
# 5️⃣ Helper to turn 8‑point box into rectangle (optional)
# -------------------------
def box_to_rect(box):
    xs = box[0::2]
    ys = box[1::2]
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}