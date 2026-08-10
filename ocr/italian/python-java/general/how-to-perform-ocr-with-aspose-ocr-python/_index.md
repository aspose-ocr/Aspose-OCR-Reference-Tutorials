---
category: general
date: 2026-06-25
description: Come eseguire l'OCR con Aspose OCR Python – impara a caricare l'OCR dell'immagine,
  elaborare l'OCR dell'immagine ed estrarre i risultati JSON in pochi minuti.
draft: false
keywords:
- how to perform OCR
- aspose OCR python
- load image OCR
- process image OCR
language: it
og_description: Come eseguire l'OCR con Aspose OCR Python. Segui questa guida per
  caricare l'OCR dell'immagine, elaborare l'OCR dell'immagine e analizzare l'output
  JSON senza sforzo.
og_title: Come eseguire l'OCR con Aspose OCR Python
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to perform OCR with Aspose OCR Python – learn to load image OCR,
    process image OCR, and extract JSON results in minutes.
  headline: How to Perform OCR with Aspose OCR Python
  type: TechArticle
- description: How to perform OCR with Aspose OCR Python – learn to load image OCR,
    process image OCR, and extract JSON results in minutes.
  name: How to Perform OCR with Aspose OCR Python
  steps:
  - name: Creating an OCR engine instance.
    text: Creating an OCR engine instance.
  - name: Loading an image for OCR.
    text: Loading an image for OCR.
  - name: Processing the image OCR.
    text: Processing the image OCR.
  - name: Converting the result to JSON.
    text: Converting the result to JSON.
  - name: Parsing and printing useful information.
    text: Parsing and printing useful information.
  - name: '**File format matters** – While TIFF works great for scanned documents,
      PNG is often better for screenshots, and JPEG for photographs.'
    text: '**File format matters** – While TIFF works great for scanned documents,
      PNG is often better for screenshots, and JPEG for photographs.'
  - name: '**Resolution** – Aspose OCR performs best with 300 dpi or higher. If you
      see low confidence scores, consider up‑sampling the image before loading.'
    text: '**Resolution** – Aspose OCR performs best with 300 dpi or higher. If you
      see low confidence scores, consider up‑sampling the image before loading.'
  - name: '**Multi‑page files** – If your TIFF contains several pages, `image = ocr.Image.load(path)`
      will give you a stack; you can iterate with `for page in image.pages:` and call
      `engine.recognize(page)` for each.'
    text: '**Multi‑page files** – If your TIFF contains several pages, `image = ocr.Image.load(path)`
      will give you a stack; you can iterate with `for page in image.pages:` and call
      `engine.recognize(page)` for each.'
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: Come eseguire l'OCR con Aspose OCR Python
url: /it/python-java/general/how-to-perform-ocr-with-aspose-ocr-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR con Aspose OCR Python

Ti sei mai chiesto **come eseguire OCR** su una ricevuta, fattura o qualsiasi documento scansionato usando Python? Non sei l'unico. In molti progetti reali, estrarre testo dalle immagini è il primo passo verso l'automazione, l'analisi o l'archiviazione.  

La buona notizia? Con **Aspose OCR Python** puoi caricare l'OCR dell'immagine, elaborare l'OCR dell'immagine e ottenere un payload JSON ordinato in poche righe di codice. Di seguito vedrai uno script completo, pronto all'uso, più la motivazione dietro ogni passaggio così comprenderai davvero *perché* il codice appare così.

## Cosa copre questo tutorial

- Configurare il motore Aspose OCR in Python  
- **Load image OCR** correttamente, gestendo formati comuni come TIFF, PNG e JPEG  
- **Process image OCR** e convertire il risultato in JSON  
- Analizzare il JSON per recuperare informazioni utili (parole, punteggi di confidenza, ecc.)  
- Suggerimenti per il troubleshooting, la gestione dei casi limite e idee per i prossimi passi  

Non è necessaria alcuna esperienza pregressa con Aspose; basta un ambiente Python 3 funzionante e un file immagine che desideri leggere.

## Prerequisiti

| Requisito | Perché è importante |
|-------------|----------------|
| Python 3.8+ | Le wheel di Aspose OCR sono destinate a interpreti moderni |
| `aspose-ocr` package (`pip install aspose-ocr`) | La libreria core che esegue il lavoro pesante |
| Un'immagine di esempio (ad es. `receipt.tif`) | Ci serve qualcosa da fornire al motore |
| Conoscenza di base di `json` | Parseremo l'output OCR in un dict Python |

> **Consiglio professionale:** Se sei su Windows, esegui il prompt dei comandi come Amministratore quando installi il pacchetto per evitare problemi di permessi.

---

## Come eseguire OCR con Aspose OCR Python

Di seguito trovi lo **script completo** che puoi copiare‑incollare in un file chiamato `ocr_demo.py`. Contiene tutto — dagli import all'output finale — così puoi eseguirlo subito.

```python
#!/usr/bin/env python3
"""
How to Perform OCR with Aspose OCR Python

This script demonstrates:
1. Creating an OCR engine instance.
2. Loading an image for OCR.
3. Processing the image OCR.
4. Converting the result to JSON.
5. Parsing and printing useful information.
"""

import json
import aspose.ocr as ocr
import os
import sys

# ----------------------------------------------------------------------
# Step 1: Create an OCR engine instance
# ----------------------------------------------------------------------
# The engine holds configuration (language, recognition mode, etc.).
# For most cases the defaults work fine, but you can tweak them later.
engine = ocr.OcrEngine()

# ----------------------------------------------------------------------
# Step 2: Load image OCR
# ----------------------------------------------------------------------
# Aspose can read many formats; here we use a TIFF because receipts often
# come as multi‑page scans. Adjust the path to point at your own file.
image_path = os.path.join("YOUR_DIRECTORY", "receipt.tif")
if not os.path.isfile(image_path):
    sys.stderr.write(f"❌ Image not found: {image_path}\n")
    sys.exit(1)

# The Image.load method decodes the file into an in‑memory object.
image = ocr.Image.load(image_path)

# ----------------------------------------------------------------------
# Step 3: Process image OCR
# ----------------------------------------------------------------------
# The recognize() call runs the OCR engine on the supplied image.
# It returns an OcrResult object that we can later serialize.
result = engine.recognize(image)

# ----------------------------------------------------------------------
# Step 4: Convert the recognition result to JSON
# ----------------------------------------------------------------------
# Aspose gives us a handy to_json() method; we then feed the string
# into Python's json module for a native dict.
json_payload = result.to_json()
parsed = json.loads(json_payload)

# ----------------------------------------------------------------------
# Step 5: Inspect the parsed data
# ----------------------------------------------------------------------
# The structure contains keys like "words", "lines", and "pages".
# We'll print a few samples to prove it works.
print("\n🔎 JSON keys:", list(parsed.keys()))
if parsed.get("words"):
    print("First word entry:", parsed["words"][0])
else:
    print("⚠️ No words detected – check image quality or language settings.")
```

### Output previsto

Quando esegui `python ocr_demo.py` (supponendo che l'immagine esista e sia leggibile), dovresti vedere qualcosa di simile a:

```
🔎 JSON keys: ['pages', 'lines', 'words', 'language', 'confidence']
First word entry: {'text': 'Total', 'confidence': 0.98, 'rectangle': {...}}
```

Il contenuto esatto varia a seconda dell'immagine di origine, ma la presenza dell'array `"words"` conferma che **process image OCR** è riuscito.

---

## Caricare l'OCR dell'immagine – Suggerimenti e problemi comuni

1. **Il formato del file è importante** – Sebbene TIFF funzioni benissimo per documenti scansionati, PNG è spesso migliore per screenshot e JPEG per fotografie.  
2. **Risoluzione** – Aspose OCR funziona al meglio con 300 dpi o più. Se vedi punteggi di confidenza bassi, considera l'up‑sampling dell'immagine prima del caricamento.  
3. **File multi‑pagina** – Se il tuo TIFF contiene più pagine, `image = ocr.Image.load(path)` ti restituirà uno stack; puoi iterare con `for page in image.pages:` e chiamare `engine.recognize(page)` per ciascuna.

> **Perché questo passaggio è cruciale:** Caricare correttamente l'immagine garantisce che il motore OCR riceva dati pixel puliti. Un formato corrotto o non supportato farà sì che `engine.recognize` lanci un'eccezione, interrompendo la tua pipeline.

---

## Elaborare l'OCR dell'immagine – Opzioni avanzate

Aspose OCR espone diverse proprietà sull'oggetto `OcrEngine`:

| Proprietà | Caso d'uso |
|----------|----------|
| `engine.language = ocr.Language.English` | Forza l'inglese quando l'immagine contiene script misti |
| `engine.recognition_mode = ocr.RecognitionMode.TextDetection` | Più veloce, ma meno preciso; utile per anteprime rapide |
| `engine.auto_rotate = True` | Corregge automaticamente le pagine ruotate (utile per le ricevute) |

Puoi impostare questi prima del passo 3 per perfezionare la fase di **process image OCR**. Ad esempio:

```python
engine.language = ocr.Language.English
engine.auto_rotate = True
```

---

## Comprendere l'output di Aspose OCR Python

Il payload JSON segue uno schema prevedibile:

- **pages** – Elenco di oggetti pagina, ciascuno con dimensioni e informazioni di rotazione.  
- **lines** – Parole raggruppate che condividono la stessa linea di base. Utile per ricostruire i paragrafi.  
- **words** – Oggetti parola individuali contenenti `text`, `confidence` e un `rectangle` con le coordinate.  
- **language** – Codice della lingua rilevata (ad es. "en").  
- **confidence** – Confidenza complessiva per l'intero documento.

Conoscere questa struttura ti permette di estrarre esattamente ciò di cui hai bisogno. Ad esempio, per estrarre tutte le parole con confidenza < 0.9 (possibili errori OCR), potresti aggiungere:

```python
low_confidence = [w for w in parsed["words"] if w["confidence"] < 0.9]
print("Potentially mis‑read words:", low_confidence)
```

---

## Casi limite e come gestirli

| Situazione | Gestione suggerita |
|-----------|--------------------|
| **Empty result** (no words) | Verifica la qualità dell'immagine, assicurati che la lingua corretta sia impostata e, se necessario, aumenta i DPI. |
| **Multi‑page PDFs** | Converti le pagine PDF in immagini prima (ad es. usando `pdf2image`) quindi fornisci ogni pagina al motore OCR. |
| **Non‑Latin scripts** | Installa pacchetti linguistici aggiuntivi tramite `engine.add_language(ocr.Language.ChineseSimplified)`. |
| **Large files** | Elabora a blocchi; riutilizza la stessa istanza di `OcrEngine` per evitare un'eccessiva allocazione di memoria. |

---

## Esempio completo funzionante (tutti i passaggi combinati)

Di seguito trovi una versione compatta che puoi inserire in un notebook Jupyter o in uno script. Include la gestione degli errori, impostazioni opzionali e stampa un riepilogo ordinato.

```python
import json, os, sys, aspose.ocr as ocr

def perform_ocr(image_path: str):
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Create engine and tweak settings (optional)
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English   # ensures English detection
    engine.auto_rotate = True                # correct rotated scans

    # Load and recognize
    image = ocr.Image.load(image_path)
    result = engine.recognize(image)

    # Convert to JSON and parse
    parsed = json.loads(result.to_json())
    return parsed

if __name__ == "__main__":
    img = os.path.join("YOUR_DIRECTORY", "receipt.tif")
    try:
        data = perform_ocr(img)
        print("\n🔎 JSON keys:", list(data.keys()))
        print("First word:", data["words"][0] if data.get("words") else "No words")
    except Exception as exc:
        sys.stderr.write(f"❗ OCR failed: {exc}\n")
```

Eseguendo questo otterrai lo stesso output conciso di prima,

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrai testo da immagine con Aspose OCR – Guida passo‑passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Come usare Aspose OCR per risultato JSON nel riconoscimento immagini](/ocr/english/net/text-recognition/get-result-as-json/)
- [Come eseguire l'estrazione di testo da immagine da stream usando Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}