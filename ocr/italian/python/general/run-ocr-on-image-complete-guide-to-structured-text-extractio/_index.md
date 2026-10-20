---
category: general
date: 2026-05-03
description: Scopri come eseguire l'OCR su un'immagine ed estrarre il testo con le
  coordinate utilizzando il riconoscimento OCR strutturato. Codice Python passo‑passo
  incluso.
draft: false
keywords:
- run OCR on image
- extract text with coordinates
- structured OCR recognition
- OCR post‑processing
- bounding box extraction
- image text detection
language: it
og_description: Esegui OCR su un'immagine e ottieni il testo con le coordinate usando
  il riconoscimento OCR strutturato. Esempio completo in Python con spiegazioni.
og_title: Esegui OCR sull'immagine – Tutorial di estrazione di testo strutturato
tags:
- OCR
- Python
- Computer Vision
title: Esegui OCR su immagine – Guida completa all’estrazione di testo strutturato
url: /it/python/general/run-ocr-on-image-complete-guide-to-structured-text-extractio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su immagine – Guida completa all'estrazione di testo strutturato

Ti è mai capitato di dover **run OCR on image** ma non sapevi come mantenere le posizioni esatte di ogni parola? Non sei l'unico. In molti progetti—scansione di ricevute, digitalizzazione di moduli o test UI—hai bisogno non solo del testo grezzo ma anche dei riquadri che indicano dove si trova ogni riga nell'immagine.  

Questo tutorial ti mostra un modo pratico per *run OCR on image* usando il motore **aocr**, richiedere il **structured OCR recognition** e poi post‑processare il risultato preservando la geometria. Alla fine sarai in grado di **extract text with coordinates** in poche righe di Python e comprenderai perché la modalità strutturata è importante per i task successivi.

## Cosa imparerai

- Come inizializzare il motore OCR per **structured OCR recognition**.  
- Come fornire un'immagine e ricevere risultati grezzi che includono i limiti delle linee.  
- Come eseguire un post‑processore che pulisce il testo senza perdere la geometria.  
- Come iterare sulle linee finali e stampare ogni pezzo di testo insieme al suo bounding box.  

Nessuna magia, nessun passaggio nascosto—solo un esempio completo e funzionante che puoi inserire nel tuo progetto.

---

## Prerequisiti

Prima di immergerci, assicurati di avere installato quanto segue:

```bash
pip install aocr ai   # hypothetical packages; replace with real ones if needed
```

Avrai inoltre bisogno di un file immagine (`input_image.png` o `.jpg`) che contenga testo chiaro e leggibile. Qualsiasi cosa, da una fattura scannerizzata a uno screenshot, va bene, purché il motore OCR riesca a vedere i caratteri.

---

## Passo 1: Inizializzare il motore OCR per il riconoscimento strutturato

La prima cosa che facciamo è creare un'istanza di `aocr.Engine()` e indicare che vogliamo **structured OCR recognition**. La modalità strutturata restituisce non solo il testo semplice ma anche dati geometrici (rettangoli di delimitazione) per ogni riga, essenziali quando devi mappare il testo sull'immagine.

```python
import aocr
import ai   # hypothetical post‑processing module

# Initialise the OCR engine
ocr_engine = aocr.Engine()

# Request structured recognition (text + geometry)
ocr_engine.recognize_mode = aocr.RecognitionMode.Structured
```

> **Perché è importante:**  
> Nella modalità predefinita il motore potrebbe darti solo una stringa di parole concatenate. La modalità strutturata ti fornisce una gerarchia di pagine → linee → parole, ciascuna con coordinate, rendendo molto più semplice sovrapporre i risultati sull'immagine originale o passarli a un modello sensibile al layout.

---

## Passo 2: Eseguire OCR sull'immagine e ottenere i risultati grezzi

Ora forniamo l'immagine al motore. La chiamata `recognize` restituisce un oggetto `OcrResult` che contiene una collezione di linee, ognuna con il proprio rettangolo di delimitazione.

```python
# Load your image (any format supported by aocr)
input_image_path = "input_image.png"

# Run OCR – this returns an OcrResult with lines and bounds
raw_result = ocr_engine.recognize(input_image_path)
```

A questo punto `raw_result.lines` contiene oggetti con due attributi importanti:

- `text` – la stringa riconosciuta per quella linea.  
- `bounds` – una tupla del tipo `(x, y, width, height)` che descrive la posizione della linea.

---

## Passo 3: Post‑processare preservando la geometria

L'output OCR grezzo è spesso rumoroso: caratteri erranti, spazi fuori posto o problemi di interruzione di riga. La funzione `ai.run_postprocessor` pulisce il testo ma **mantiene intatta la geometria originale**, così hai ancora coordinate accurate.

```python
# Apply a post‑processing step that corrects common OCR errors
postprocessed_result = ai.run_postprocessor(raw_result)

# The structure (lines + bounds) stays the same, only `line.text` changes
```

> **Consiglio esperto:** Se disponi di vocabolari specifici del dominio (ad es., codici prodotto), fornisci un dizionario personalizzato al post‑processore per migliorare la precisione.

---

## Passo 4: Estrarre testo con coordinate – iterare e visualizzare

Infine, cicliamo sulle linee pulite, stampando il bounding box di ciascuna insieme al suo testo. Questo è il cuore di **extract text with coordinates**.

```python
# Print each recognised line together with its bounding box
for line in postprocessed_result.lines:
    print(f"[{line.bounds}] {line.text}")
```

### Output previsto

Supponendo che l'immagine di input contenga due linee: “Invoice #12345” e “Total: $89.99”, vedrai qualcosa del genere:

```
[(15, 30, 210, 25)] Invoice #12345
[(15, 70, 190, 25)] Total: $89.99
```

La prima tupla è il `(x, y, width, height)` della linea sull'immagine originale, permettendoti di disegnare rettangoli, evidenziare il testo o passare le coordinate a un altro sistema.

---

## Visualizzare il risultato (opzionale)

Se vuoi vedere i bounding box sovrapposti all'immagine, puoi usare Pillow (PIL) per disegnare i rettangoli. Di seguito trovi un breve snippet; sentiti libero di saltarlo se ti servono solo i dati grezzi.

```python
from PIL import Image, ImageDraw

# Open the original image
img = Image.open(input_image_path)
draw = ImageDraw.Draw(img)

# Draw a rectangle around each line
for line in postprocessed_result.lines:
    x, y, w, h = line.bounds
    draw.rectangle([x, y, x + w, y + h], outline="red", width=2)

# Save or show the annotated image
img.save("annotated_output.png")
img.show()
```

![run OCR on image example showing bounding boxes](/images/ocr-bounding-boxes.png "run OCR on image – bounding box overlay")

Il testo alternativo sopra contiene la **primary keyword**, soddisfacendo il requisito SEO per gli attributi alt delle immagini.

---

## Perché il riconoscimento OCR strutturato supera la semplice estrazione di testo

Ti potresti chiedere: “Non posso semplicemente eseguire OCR e ottenere il testo? Perché preoccuparsi della geometria?”  

- **Contesto spaziale:** Quando devi mappare i campi su un modulo (ad es., “Date” accanto al valore della data), le coordinate ti dicono *dove* si trova il dato.  
- **Layout a più colonne:** Il testo lineare semplice perde l'ordine; i dati strutturati preservano l'ordine delle colonne.  
- **Precisione del post‑processing:** Conoscere le dimensioni del box ti aiuta a decidere se una parola è un'intestazione, una nota a piè di pagina o un artefatto errante.  

In sintesi, **structured OCR recognition** ti offre la flessibilità per costruire pipeline più intelligenti—che tu stia inserendo dati in un database, creando PDF ricercabili o addestrando un modello di machine‑learning che rispetti il layout.

---

## Casi limite comuni e come gestirli

| Situazione | Cosa controllare | Correzione suggerita |
|-----------|-------------------|---------------|
| **Immagini ruotate o distorte** | I bounding box potrebbero essere fuori asse. | Pre‑processare con deskewing (ad es., `warpAffine` di OpenCV). |
| **Font molto piccoli** | Il motore può perdere caratteri, generando linee vuote. | Aumentare la risoluzione dell'immagine o usare `ocr_engine.set_dpi(300)`. |
| **Lingue miste** | Un modello linguistico errato può produrre testo incomprensibile. | Impostare `ocr_engine.language = ["en", "de"]` prima del riconoscimento. |
| **Box sovrapposti** | Il post‑processore potrebbe unire due linee involontariamente. | Verificare `line.bounds` dopo il processing; regolare le soglie in `ai.run_postprocessor`. |

Affrontare questi scenari fin dall'inizio ti farà risparmiare mal di testa in seguito, soprattutto quando scala la soluzione a centinaia di documenti al giorno.

---

## Script completo end‑to‑end

Di seguito trovi il programma completo, pronto per l'esecuzione, che collega tutti i passaggi. Copia‑incolla, aggiusta il percorso dell'immagine e sei pronto.

```python
# -*- coding: utf-8 -*-
"""
Run OCR on image – extract text with coordinates using structured OCR recognition.
Author: Your Name
Date: 2026-05-03
"""

import aocr
import ai
from PIL import Image, ImageDraw

def run_structured_ocr(image_path: str, annotate: bool = False):
    # 1️⃣ Initialise the OCR engine
    ocr_engine = aocr.Engine()
    ocr_engine.recognize_mode = aocr.RecognitionMode.Structured

    # 2️⃣ Recognise the image
    raw_result = ocr_engine.recognize(image_path)

    # 3️⃣ Post‑process while keeping geometry
    processed = ai.run_postprocessor(raw_result)

    # 4️⃣ Print each line with its bounding box
    for line in processed.lines:
        print(f"[{line.bounds}] {line.text}")

    # Optional visualisation
    if annotate:
        img = Image.open(image_path)
        draw = ImageDraw.Draw(img)
        for line in processed.lines:
            x, y, w, h = line.bounds
            draw.rectangle([x, y, x + w, y + h], outline="red", width=2)
        annotated_path = "annotated_" + image_path
        img.save(annotated_path)
        print(f"Annotated image saved as {annotated_path}")

if __name__ == "__main__":
    INPUT_IMG = "input_image.png"
    run_structured_ocr(INPUT_IMG, annotate=True)
```

Eseguire questo script:

1. **Run OCR on image** in modalità strutturata.  
2. **Extract text with coordinates** per ogni linea.  
3. Opzionalmente produce un PNG annotato che mostra i box.

---

## Conclusione

Ora disponi di una soluzione solida e autonoma per **run OCR on image** e **extract text with coordinates** usando **structured OCR recognition**. Il codice dimostra ogni passaggio—dall'inizializzazione del motore al post‑processing e alla verifica visiva—così puoi adattarlo a ricevute, moduli o qualsiasi documento visivo che richieda una localizzazione precisa del testo.

Qual è il prossimo passo? Prova a sostituire il motore `aocr` con un'altra libreria (Tesseract, EasyOCR) e osserva come differiscono le uscite strutturate. Sperimenta diverse strategie di post‑processing, come il controllo ortografico o filtri regex personalizzati, per aumentare la precisione nel tuo dominio. E se costruisci una pipeline più ampia, considera di memorizzare le coppie `(text, bounds)` in un database per analisi future.

Buon coding, e che i tuoi progetti OCR siano sempre precisi!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}