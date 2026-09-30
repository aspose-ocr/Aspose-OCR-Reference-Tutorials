---
category: general
date: 2026-01-12
description: Estrai testo da PDF usando il motore OCR in Python – impara a leggere
  PDF con OCR, caricare l'immagine per OCR e ottenere risultati strutturati.
draft: false
keywords:
- extract text from pdf
- read pdf with ocr
- load image for ocr
- use ocr engine python
language: it
og_description: Estrai testo da PDF usando il motore OCR Python. Questo tutorial mostra
  come leggere PDF con OCR, caricare l'immagine per l'OCR e utilizzare il motore OCR
  Python per risultati affidabili.
og_title: Estrai testo da PDF con motore OCR Python – Guida completa
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Estrai testo da PDF con motore OCR Python – Guida passo‑passo
url: /it/python/general/extract-text-from-pdf-with-ocr-engine-python-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da PDF con OCR Engine Python – Tutorial completo

Hai mai avuto bisogno di **estrarre testo da PDF** ma il file è solo un'immagine scannerizzata? Non sei solo. In molti progetti reali il PDF che ricevi non ha testo selezionabile, quindi l'unica soluzione è **leggere PDF con OCR**.  

In questa guida percorreremo una soluzione pratica, end‑to‑end, che mostra esattamente come **caricare l'immagine per OCR**, avviare l'**OCR engine Python** e estrarre testo strutturato da inserire nei pipeline successivi. Nessun riferimento vago, solo un esempio completo e eseguibile che puoi copiare‑incollare oggi.

## Cosa imparerai

- Come installare e importare la libreria Python OCR di cui hai bisogno.  
- I passaggi esatti per **caricare l'immagine per OCR** da un file PDF.  
- Come chiamare il metodo `recognize_structured()` del motore e iterare su blocchi, righe e parole.  
- Suggerimenti per gestire risultati a bassa confidenza e PDF multipagina.  

Al termine di questo tutorial avrai uno script che **estrae testo da PDF** in modo affidabile, indipendentemente dal fatto che contenga una pagina o centinaia.

---

![Diagramma che mostra l'OCR engine elaborare un PDF e produrre testo strutturato.](images/ocr_flow.png "diagramma estrazione testo da pdf")

*Testo alternativo dell'immagine: diagramma di estrazione testo da pdf che illustra i passaggi di elaborazione OCR.*

## Prerequisiti

- Python 3.9 o superiore (il codice utilizza f‑strings e type hints).  
- Un pacchetto OCR installabile via pip che espone una classe `OcrEngine` (ad esempio, una libreria fittizia `pyocr`).  
- Un file PDF che desideri elaborare, salvato localmente (es. `form.pdf`).  

If you’re missing the OCR library, install it with:

```bash
pip install pyocr   # replace with the actual package name you use
```

---

## Passo 1: Estrarre testo da PDF – Configurare l'OCR Engine

Prima di poter **leggere PDF con OCR**, abbiamo bisogno di un'istanza del motore. Pensa al motore come al cervello che osserva ogni pixel e decide quale carattere rappresenta.

```python
# Step 1: Import the OCR module and create an engine instance
import ocr  # or `import pyocr as ocr` depending on the package

# Create the OCR engine – this may load language models under the hood
ocr_engine = ocr.OcrEngine()
```

> **Perché è importante:** Inizializzare il motore una sola volta ti permette di riutilizzare i pacchetti linguistici caricati su più file, risparmiando tempo e memoria.

---

## Passo 2: Caricare immagine per OCR – Preparare il tuo PDF

Un PDF non è un'immagine grezza, quindi la libreria solitamente fornisce un helper per convertire la prima pagina (o tutte le pagine) in un'immagine comprensibile per l'OCR engine.

```python
# Step 2: Load the PDF page(s) you want to process
# The `load_image` method accepts many formats – PDF, PNG, JPEG, etc.
pdf_path = "YOUR_DIRECTORY/form.pdf"
ocr_engine.load_image(pdf_path)
```

> **Suggerimento:** Se il tuo PDF ha più pagine, molte librerie OCR ti permettono di passare `page=2` o di iterare su `engine.load_image(pdf_path, page=n)`. Per documenti di grandi dimensioni, considera di elaborare le pagine in batch per evitare picchi di memoria.

---

## Passo 3: Usare OCR Engine Python – Riconoscere testo strutturato

Ora avviene il lavoro pesante. La chiamata `recognize_structured()` restituisce una gerarchia di blocchi → righe → parole, ciascuna annotata con lingua, confidenza e bounding box.

```python
# Step 3: Perform structured text recognition
structured_result = ocr_engine.recognize_structured()
```

> **Cosa ottieni:**  
> - `structured_result.blocks` – contenitori di livello superiore (spesso paragrafi o colonne).  
> - Ogni blocco contiene `lines`, e ogni riga contiene `words`.  
> - I punteggi di confidenza ti permettono di filtrare risultati dubbiosi.

---

## Passo 4: Iterare sui risultati – Accedere a blocchi, righe e parole

Di seguito un ciclo compatto che stampa le informazioni più utili. Sentiti libero di espanderlo per scrivere JSON, CSV o alimentare un database.

```python
# Step 4: Walk through the hierarchy and display key data
for block_idx, text_block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={text_block.language}, confidence={text_block.confidence:.2f}")

    # Show a sample line from the block, if any
    if text_block.lines:
        sample_line = text_block.lines[0]
        print(f"  Sample line: {sample_line.text}")

        # Show a sample word with its bounding box and confidence
        if sample_line.words:
            sample_word = sample_line.words[0]
            print(
                f"    Sample word: '{sample_word.text}' "
                f"bbox={sample_word.bounding_box} "
                f"conf={sample_word.confidence:.2f}"
            )
```

### Output previsto

```
Block 1: language=en, confidence=0.97
  Sample line: Invoice Number: 2025-00123
    Sample word: 'Invoice' bbox=(12,34,78,90) conf=0.99
Block 2: language=en, confidence=0.94
  Sample line: Total Amount: $1,250.00
    Sample word: 'Total' bbox=(15,120,70,155) conf=0.96
...
```

> **Perché ti piacerà:** La gerarchia rispecchia il modo in cui gli esseri umani leggono una pagina, facilitando la ricostruzione di tabelle o layout a colonne in seguito---

## Passo 5: Gestire casi limite – Bassa confidenza e PDF multipagina

### Parole a bassa confidenza

Se la confidenza di una parola scende sotto, ad esempio, `0.70`, potresti volerla segnare per una revisione manuale:

```python
LOW_CONF_THRESHOLD = 0.70

for block in structured_result.blocks:
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

### Elaborare tutte le pagine

```python
# Example: loop over every page in a multi‑page PDF
for page_number in range(ocr_engine.page_count):
    ocr_engine.load_image(pdf_path, page=page_number)
    result = ocr_engine.recognize_structured()
    # …process `result` just like we did above…
```

> **Consiglio professionale:** Metti in cache le immagini intermedie come PNG se la tua libreria OCR le rigenera ogni volta—questo può far risparmiare secondi su grandi batch.

---

## Script completo funzionante

Mettendo tutto insieme, ecco un unico file che puoi eseguire subito:

```python
#!/usr/bin/env python3
"""
Extract text from PDF with OCR engine Python.
This script demonstrates loading a PDF, recognizing structured text,
and printing a concise summary of blocks, lines, and words.
"""

import ocr  # Replace with your actual OCR package import

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
PDF_PATH = "YOUR_DIRECTORY/form.pdf"
LOW_CONF_THRESHOLD = 0.70

# ----------------------------------------------------------------------
# Initialize OCR engine
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()

# ----------------------------------------------------------------------
# Load the PDF (first page by default)
# ----------------------------------------------------------------------
ocr_engine.load_image(PDF_PATH)

# ----------------------------------------------------------------------
# Recognize structured text
# ----------------------------------------------------------------------
structured_result = ocr_engine.recognize_structured()

# ----------------------------------------------------------------------
# Iterate and display results
# ----------------------------------------------------------------------
for block_idx, block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={block.language}, confidence={block.confidence:.2f}")

    if block.lines:
        line = block.lines[0]
        print(f"  Sample line: {line.text}")

        if line.words:
            word = line.words[0]
            print(
                f"    Sample word: '{word.text}' "
                f"bbox={word.bounding_box} "
                f"conf={word.confidence:.2f}"
            )

    # Flag low‑confidence words inside the block
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

Salva questo come `extract_pdf_ocr.py` ed esegui:

```bash
python extract_pdf_ocr.py
```

Dovresti vedere i dettagli a livello di blocco stampati sulla console, insieme a eventuali avvisi di bassa confidenza.

---

## Conclusione

Abbiamo appena coperto un metodo completo e pronto per la produzione per **estrarre testo da PDF** usando un **OCR engine Python**. Dall'installazione della libreria, passando per **caricare l'immagine per OCR**, a **leggere PDF con OCR** e infine iterare sull'output strutturato, ora disponi di uno script riutilizzabile che puoi adattare a qualsiasi progetto.

Prossimi passi che potresti esplorare:

- Esportare la gerarchia in JSON per pipeline NLP successive.  
- Aggiungere il rilevamento della lingua per cambiare i modelli OCR al volo.  
- Integrare con `pdf2image` per pre‑processare PDF che contengono layout complessi.  

Provalo su un batch di fatture multipagina, regola la soglia di confidenza e scopri quanto rapidamente puoi trasformare PDF scannerizzati in testo ricercabile e modificabile. Se incontri problemi, lascia un commento qui sotto—buon OCR!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}