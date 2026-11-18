---
category: general
date: 2026-03-26
description: Come estrarre il testo da un PDF usando l'OCR. Impara a caricare il PDF
  come immagine, riconoscere il testo del PDF ed estrarre il testo dal PDF con un
  semplice esempio in Python.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize pdf text
- load pdf as image
- how to use OCR
language: it
og_description: Come estrarre il testo da PDF usando l'OCR. Questa guida ti mostra
  come caricare un PDF come immagine, riconoscere il testo del PDF ed estrarre il
  testo dal PDF in Python.
og_title: Come estrarre il testo PDF con OCR – Tutorial completo
tags:
- OCR
- Python
- PDF processing
title: Come estrarre il testo PDF con OCR – Guida completa passo passo
url: /it/python-java/general/how-to-extract-pdf-text-with-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come Estrarre Testo da PDF con OCR – Guida Completa Passo‑Passo

Ti sei mai chiesto **come estrarre PDF** che in realtà sono solo immagini scansionate? Non sei solo: molti sviluppatori si trovano di fronte a questo ostacolo quando hanno bisogno di contenuti ricercabili ma dispongono solo di PDF costituiti da immagini. La buona notizia? Poche righe di codice e una solida libreria OCR possono trasformare quei PDF‑immagine in testo semplice in un attimo.  

In questo tutorial vedremo **come usare OCR** per caricare un PDF come immagine, riconoscere il testo del PDF e infine **estrarre testo da PDF** di qualsiasi lunghezza. Alla fine avrai uno script eseguibile, una spiegazione chiara di ogni passaggio e alcuni consigli per evitare le solite insidie.

## Cosa Ti Serve

- Python 3.9 o superiore (il codice funziona anche su 3.10+)  
- Il pacchetto Python `ocr` (o qualsiasi libreria OCR compatibile che esponga `OcrEngine`, `OcrEngineMode` e `Imaging.Image`)  
- Un PDF multipagina da elaborare (per la demo lo chiameremo `multi_page.pdf`)  
- Familiarità di base con gli ambienti virtuali (opzionale ma consigliata)

> **Pro tip:** Se sei su Windows, considera di usare Anaconda Prompt; su macOS/Linux, un semplice `python -m venv venv && source venv/bin/activate` fa al caso tuo.

## Passo 1: Installa la Libreria OCR

Per prima cosa, scarica il pacchetto OCR da PyPI. L’esempio qui sotto usa un pacchetto fittizio `ocr` che rispecchia l’API mostrata nello snippet di codice, ma la maggior parte delle librerie reali (come `pytesseract` + `pdf2image`) segue lo stesso schema.

```bash
pip install ocr
```

Se usi un motore diverso, sostituisci `ocr` con il nome appropriato (ad esempio `pip install pytesseract pdf2image`).

## Passo 2: Inizializza il Motore OCR

Creare un’istanza del motore è la base di **come estrarre PDF** testo. Pensa al motore come al cervello che interpreterà i pixel di ogni pagina PDF.

```python
import ocr

# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Set the engine to the default mode (fast enough for most PDFs)
ocr_engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)
```

> **Perché è importante:** `set_engine_mode` ti permette di bilanciare velocità e precisione. `DEFAULT` è una scelta equilibrata; se ti serve maggiore accuratezza, passa a `HIGH_ACCURACY` (se la libreria lo supporta).

## Passo 3: Carica il PDF come Oggetto Immagine

OCR funziona su immagini, non su contenitori PDF, quindi dobbiamo prima convertire il PDF in una rappresentazione immagine. Il metodo `Imaging.Image.load` gestisce automaticamente i PDF multipagina.

```python
# Step 3: Load the multi‑page PDF as an image object
pdf_path = "YOUR_DIRECTORY/multi_page.pdf"
pdf_image = ocr.Imaging.Image.load(pdf_path)
```

> **Caso limite:** Alcune librerie accettano solo un’immagine a pagina. In quel caso, dovresti iterare su ogni pagina usando `pdf2image.convert_from_path`. La nostra chiamata `load` astrae tutto ciò, rendendo **load pdf as image** una singola riga.

## Passo 4: Riconosci il Testo su Tutte le Pagine

Ora arriva il cuore di **recognize PDF text**. Il motore scansiona ogni pagina, restituendo una lista di oggetti risultato—uno per pagina.

```python
# Step 4: Recognize text on all pages of the PDF
page_results = ocr_engine.recognize_multi_page(pdf_image)
```

Ogni `page_result` contiene metodi come `get_text()` (testo semplice) e `get_confidence()` (metrica di qualità opzionale).  

> **Suggerimento:** Se ti serve solo la prima pagina, chiama `recognize(pdf_image[0])` invece dell’aiutante multipagina.

## Passo 5: Itera sui Risultati e Stampa il Testo Estratto

Infine, cicliamo sui risultati, stampando il testo di ogni pagina. Questo completa il flusso di lavoro **extract text from PDF**.

```python
# Step 5: Print extracted text page by page
for index, page_result in enumerate(page_results):
    print(f"--- Page {index + 1} ---")
    print(page_result.get_text())
    # Optional: show confidence score
    # print(f"Confidence: {page_result.get_confidence():.2f}%")
```

### Output Atteso

Se `multi_page.pdf` contiene tre pagine con le parole “Hello”, “World” e “Python”, vedrai:

```
--- Page 1 ---
Hello
--- Page 2 ---
World
--- Page 3 ---
Python
```

Questo è tutto—il tuo PDF è ora completamente ricercabile e il testo è pronto per l’elaborazione successiva (indicizzazione, analisi del sentiment, ecc.).

## Passo 6: Gestire le Insidie più Comuni

| Problema | Perché Accade | Soluzione Rapida |
|----------|----------------|------------------|
| **Output vuoto** | Le pagine PDF sono scansionate a bassa DPI, rendendo i caratteri indistinguibili. | Ingrandisci l’immagine prima dell’OCR: `pdf_image = pdf_image.resize(300)` (300 DPI è un buon compromesso). |
| **Caratteri spazzatura** | Gli alfabeti non latini richiedono pacchetti linguistici. | Carica il modello linguistico appropriato: `ocr_engine.load_language('spa')` per lo spagnolo, ecc. |
| **Esaurimento memoria su PDF enormi** | Caricare tutte le pagine contemporaneamente consuma RAM. | Elabora le pagine a blocchi: `for img in pdf_image.split(batch=10): …` (pseudo‑codice). |
| **Prestazioni lente** | Usare `DEFAULT` su un documento massiccio può risultare lento. | Passa a modalità `FAST` o esegui l’OCR in parallelo con `concurrent.futures`. |

## Bonus: Salvare il Testo Estratto in un File

La maggior parte delle pipeline reali necessita di persistere il testo. Ecco un piccolo helper che scrive tutto in `output.txt`.

```python
output_path = "YOUR_DIRECTORY/output.txt"

with open(output_path, "w", encoding="utf-8") as f:
    for idx, result in enumerate(page_results):
        f.write(f"--- Page {idx + 1} ---\n")
        f.write(result.get_text() + "\n\n")
print(f"All text saved to {output_path}")
```

Ora puoi alimentare `output.txt` a un motore di ricerca, a un database o a qualsiasi modello NLP.

## Mettere Tutto Insieme – Script Completo

Di seguito trovi il programma completo, pronto per l’esecuzione. Copialo, adatta i percorsi dei file e sei a posto.

```python
# -*- coding: utf-8 -*-
"""
How to extract PDF text with OCR – end‑to‑end example.

Prerequisites:
    pip install ocr
"""

import ocr

def extract_text_from_pdf(pdf_path: str):
    """
    Load a PDF, run OCR on every page, and return a list of strings.
    """
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)

    # Load PDF as image (multi‑page support)
    pdf_image = ocr.Imaging.Image.load(pdf_path)

    # Recognize text on all pages
    results = engine.recognize_multi_page(pdf_image)

    # Collect plain text
    texts = [res.get_text() for res in results]
    return texts

def main():
    pdf_file = "YOUR_DIRECTORY/multi_page.pdf"
    texts = extract_text_from_pdf(pdf_file)

    # Print and optionally save
    for i, txt in enumerate(texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()

    # Save to file
    out_path = "YOUR_DIRECTORY/extracted_text.txt"
    with open(out_path, "w", encoding="utf-8") as out_f:
        for i, txt in enumerate(texts, start=1):
            out_f.write(f"--- Page {i} ---\n{txt}\n\n")
    print(f"Extracted text stored in {out_path}")

if __name__ == "__main__":
    main()
```

Eseguilo:

```bash
python extract_pdf_ocr.py
```

Dovresti vedere il contenuto di ogni pagina stampato sulla console, seguito da una conferma che il file `extracted_text.txt` è stato creato.

## Conclusione

Abbiamo coperto **come estrarre PDF** testo da documenti composti solo da immagini usando un motore OCR, dall’installazione della libreria alla gestione dei risultati multipagina e al salvataggio dell’output. Ora sai **come usare OCR**, come **caricare PDF come immagine** e come **riconoscere PDF text** in modo affidabile.  

Passi successivi? Prova a cambiare la modalità predefinita del motore con un’impostazione ad alta precisione, sperimenta i pacchetti linguistici per PDF multilingue, o indirizza il testo estratto a un indice di ricerca full‑text come Elasticsearch. Il cielo è il limite una volta che hai padroneggiato le basi dell’estrazione di testo da file PDF.

---

![how to extract pdf example](images/ocr_flowchart.png){alt="how to extract pdf workflow diagram"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}