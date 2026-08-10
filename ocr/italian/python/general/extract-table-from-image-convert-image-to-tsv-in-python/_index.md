---
category: general
date: 2026-07-05
description: Estrai la tabella da un'immagine usando OCR in Python. Impara come estrarre
  la tabella, convertire l'immagine in TSV e padroneggiare le tecniche OCR per tabelle
  in Python.
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: it
og_description: Estrai una tabella da un'immagine con OCR in Python. Questa guida
  mostra come estrarre la tabella, convertire l'immagine in TSV e utilizzare gli strumenti
  Python per OCR di tabelle da immagini.
og_title: Estrai tabella da immagine – Converti immagine in TSV con Python
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  headline: Extract Table from Image – Convert Image to TSV in Python
  type: TechArticle
- description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  name: Extract Table from Image – Convert Image to TSV in Python
  steps:
  - name: Initialise the aocr OCR engine.
    text: Initialise the aocr OCR engine.
  - name: Attach the AI post‑processor.
    text: Attach the AI post‑processor.
  - name: Load a table image.
    text: Load a table image.
  - name: Perform structured OCR.
    text: Perform structured OCR.
  - name: Clean the results.
    text: Clean the results.
  - name: Export the table as a TSV file.
    text: Export the table as a TSV file.
  type: HowTo
tags:
- OCR
- Python
- Table Extraction
title: Estrai tabella da immagine – Converti immagine in TSV con Python
url: /it/python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrarre una tabella da un'immagine – Convertire immagine in TSV in Python

Ti sei mai chiesto come estrarre una tabella da un'immagine senza impazzire? In questo tutorial vedremo **come estrarre i dati della tabella** da un'immagine usando la libreria `aocr`, per poi trasformare quei dati in un file TSV ordinato. Nessuna magia, solo poche righe di Python e un po' di post‑processing alimentato dall'AI.

Se hai mai provato a copiare‑incollare una tabella da una fattura scannerizzata o da uno screenshot e ti sei ritrovato con un caos incomprensibile, apprezzerai perché un approccio basato su OCR è così importante da padroneggiare. Alla fine, potrai fornire qualsiasi immagine di una tabella a Python e ottenere valori separati da tabulazione puliti, pronti per fogli di calcolo o database.

---

## Cosa ti servirà

Prima di immergerci, assicurati di avere quanto segue sulla tua macchina:

| Requisito | Perché è importante |
|-----------|----------------------|
| Python 3.9+ | Il pacchetto `aocr` è destinato a runtime Python moderni. |
| `aocr` library (`pip install aocr`) | Fornisce il motore OCR e il post‑processore AI che utilizzeremo. |
| Un file immagine contenente una tabella (PNG, JPG, ecc.) | I dati sorgente che estrarremo. |
| Opzionale: un ambiente virtuale | Mantiene le dipendenze isolate — altamente consigliato. |

Avere tutto pronto ti evita interruzioni a metà della guida.

---

## Installa le dipendenze

Per prima cosa, installiamo gli strumenti OCR. Apri un terminale ed esegui:

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **Consiglio:** Se incontri errori di permessi, aggiungi `--user` al comando `pip install` o usa `pipx` per un'installazione globale.

---

## Passo 1 – Inizializzare il motore OCR

Il motore è il cuore del processo. Pensalo come il “cervello” che osserva ogni pixel e decide a quale carattere appartiene.

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

Perché istanziamo un motore invece di chiamare una singola funzione? L'oggetto motore ci permette di collegare post‑processori personalizzati in seguito, offrendoci un controllo fine sull'output — essenziale quando ti serve **ocr table image python** precisione.

---

## Passo 2 – Collegare il post‑processore AI

`aocr` include un leggero post‑processore AI che pulisce i risultati OCR grezzi preservando i bordi delle celle. Non sono richiesti argomenti aggiuntivi, il che mantiene il codice ordinato.

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

Se salti questo passo, otterrai comunque testo grezzo, ma la struttura della tabella sarà rumorosa — pensa a un foglio di calcolo in cui ogni cella è un mistero. Il post‑processore si occupa del lavoro pesante di allineare il testo alla griglia originale.

---

## Passo 3 – Caricare l'immagine della tabella

Puoi caricare un'immagine da qualsiasi percorso, ma per chiarezza faremo riferimento a una directory segnaposto. Sostituisci `"YOUR_DIRECTORY/invoice_table.png"` con il percorso reale del tuo file.

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

> **Nota:** `aocr.Image` rileva automaticamente il formato dell'immagine e normalizza i canali colore, quindi non è necessario pre‑processare il file a meno che non sia gravemente degradato.

---

## Passo 4 – Eseguire OCR strutturato

Ora il motore scansiona l'immagine e restituisce un oggetto tabella grezzo. Questo oggetto contiene righe, colonne e il testo grezzo per ogni cella.

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

Perché usare `recognize_structured` invece di una chiamata generica `recognize`? La variante strutturata tenta di inferire i confini di righe/colonne, fornendoti un risultato simile a una matrice molto più facile da convertire in TSV in seguito.

---

## Passo 5 – Pulire i dati con il post‑processore AI

Eseguire il post‑processore affina l'output grezzo: rimuove caratteri erranti, unisce frammenti divisi e garantisce che il testo di ogni cella sia correttamente allineato.

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

Se ispezioni `processed_table.table`, vedrai una lista di righe, ciascuna riga è una lista di oggetti `Cell`. Ogni `Cell` ha un attributo `.text` che contiene la stringa pulita.

---

## Passo 6 – Esportare la tabella come TSV

L'ultimo passo è trasformare i dati elaborati in un file di valori separati da tabulazione (TSV) — esattamente ciò di cui hai bisogno quando vuoi **convert image to TSV** per Excel o Google Sheets.

```python
import csv

# Define the output TSV path
tsv_path = "extracted_table.tsv"

# Open the file and write rows as tab‑separated values
with open(tsv_path, "w", newline="", encoding="utf-8") as tsv_file:
    writer = csv.writer(tsv_file, delimiter="\t")
    for row in processed_table.table:
        # Extract text from each cell and write the row
        writer.writerow([cell.text for cell in row])

print(f"✅ Table successfully saved to {tsv_path}")
```

Eseguire lo script stampa ogni riga nella console (se lo preferisci) e scrive un file TSV pulito che puoi aprire in qualsiasi programma di fogli di calcolo.

### Verifica rapida

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

Dovresti vedere colonne allineate ordinatamente, ad esempio:

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

Se l'output appare confuso, ricontrolla la qualità dell'immagine (nitidezza, contrasto) e considera di regolare le impostazioni del motore OCR — `engine.set_config(...)` ti permette di modificare i modelli linguistici e le soglie di confidenza.

---

## Gestire casi limite comuni

| Situazione | Correzione suggerita |
|------------|----------------------|
| **Immagine inclinata** | Pre‑ruotare usando `Pillow` (`Image.rotate`) prima di passarla a `aocr`. |
| **Basso contrasto** | Applicare l'equalizzazione dell'istogramma (`cv2.equalizeHist`) per migliorare la leggibilità. |
| **Celle unite** | Post‑processare il TSV per dividere le celle basandosi su delimitatori noti o usare il flag `merge_cells=False` se disponibile. |
| **PDF multi‑pagina** | Convertire prima ogni pagina in un'immagine (`pdf2image`) ed eseguire la pipeline in un ciclo. |

Queste ottimizzazioni mantengono il tuo flusso di lavoro **ocr table image python** robusto su materiale sorgente vario.

---

## Script completo – Soluzione tutto‑in‑uno

Di seguito trovi lo script completo, pronto all'uso, che racchiude tutti i passaggi discussi. Salvalo come `extract_table.py` ed esegui `python extract_table.py`.

```python
#!/usr/bin/env python3
"""
Extract Table from Image – Convert Image to TSV (Python)

This script demonstrates how to:
1. Initialise the aocr OCR engine.
2. Attach the AI post‑processor.
3. Load a table image.
4. Perform structured OCR.
5. Clean the results.
6. Export the table as a TSV file.

Author: Your Name
Date: 2026-07-05
"""

import aocr
import csv
import sys
from pathlib import Path

def main(image_path: str, output_tsv: str = "extracted_table.tsv"):
    # Step 1 – Initialise engine
    engine = aocr.OcrEngine()

    # Step 2 – Attach AI post‑processor
    engine.set_post_processor(ai.run_postprocessor, None)

    # Step 3 – Load image
    if not Path(image_path).is_file():
        sys.exit(f"❌ Image not found: {image_path}")
    image = aocr.Image.from_file(image_path)

    # Step 4 – Structured OCR
    raw_table = engine.recognize_structured(image)

    # Step 5 – Clean with post‑processor
    processed_table = engine.run_postprocessor(raw_table)

    # Step 6 – Write TSV
    with open(output_tsv, "w", newline="", encoding="utf-8") as tsv_file:
        writer = csv.writer(tsv_file, delimiter="\


## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑a‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrarre testo da immagine con Aspose OCR – Guida passo‑a‑passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Come estrarre una tabella da immagine usando Aspose.OCR per .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Come estrarre testo da immagine preparando rettangoli in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}