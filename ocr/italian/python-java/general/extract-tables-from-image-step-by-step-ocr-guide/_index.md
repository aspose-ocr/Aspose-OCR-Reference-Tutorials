---
category: general
date: 2026-03-26
description: Estrai tabelle da un'immagine e converti l'immagine in un foglio di calcolo
  usando OCR Python. Scopri come caricare l'immagine per l'OCR, leggere le tabelle
  ed estrarre i dati della tabella.
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: it
og_description: Estrai tabelle da un'immagine con OCR in Python. Questa guida mostra
  come caricare l'immagine per l'OCR, leggere le tabelle e convertirle in un foglio
  di calcolo.
og_title: Estrai tabelle da immagine – Tutorial completo di OCR
tags:
- OCR
- Python
- Data Extraction
title: Estrai tabelle da immagine – Guida OCR passo passo
url: /it/python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai tabelle da immagine – Tutorial OCR completo

Ti è mai capitato di dover **estrarre tabelle da immagine** ma non sapevi da dove cominciare? Non sei il solo. Molti sviluppatori si trovano di fronte a un muro quando un PDF o uno screenshot contiene dati tabulari che devono diventare righe e colonne modificabili. La buona notizia? Poche righe di codice Python, abbinate a un motore OCR solido, possono trasformare quell’immagine in un foglio di calcolo utilizzabile in pochi secondi.

In questo tutorial vedremo come caricare un’immagine per l’OCR, eseguire il motore di riconoscimento e estrarre ogni tabella riga per riga. Alla fine sarai in grado di **convertire immagine in foglio di calcolo**, e vedrai anche come **ocr read tables** e **ocr extract table data** per l’elaborazione successiva. Nessuna magia nascosta, solo codice chiaro e funzionante che puoi inserire subito nel tuo progetto.

---

## Cosa ti servirà

Prima di immergerci, assicurati di avere a disposizione quanto segue:

- **Python 3.9+** – la versione stabile più recente funziona al meglio.  
- La libreria **`ocr`** (o qualsiasi SDK OCR compatibile che esponga `OcrEngine`, `Image` e i metodi relativi alle tabelle). Installala con `pip install ocr‑sdk` (sostituisci con il nome reale del pacchetto).  
- Un file immagine (`.png`, `.jpg`, ecc.) che contenga una tabella stampata in modo chiaro.  
- Facoltativo: **pandas** se vuoi scrivere i dati estratti direttamente in un file CSV o Excel (`pip install pandas`).

Hai tutto? Ottimo—iniziamo.

---

## Passo 1: Importa l'SDK OCR e prepara il tuo ambiente

Prima di tutto: dobbiamo importare le classi OCR nel nostro script e impostare un piccolo helper che in seguito trasformerà i dati grezzi della tabella in un DataFrame.

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**Perché è importante:** L’importazione di `ocr` ci dà accesso a `OcrEngine`, `Imaging.Image` e agli oggetti tabella che itereremo. `pandas` non è obbligatorio per l’estrazione, ma rende la parte “convertire immagine in foglio di calcolo” davvero banale.

---

## Passo 2: Carica l'immagine da elaborare

Ora **carichiamo l’immagine per l'OCR**. L'SDK si aspetta un oggetto `Image`, quindi avvolgeremo il percorso del file con il metodo di supporto `Image.load()`.

```python
# Step 2 – Load the image that contains a table
image_path = Path("YOUR_DIRECTORY/table_image.png")

# Verify the file exists early to avoid cryptic SDK errors
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Attach the image to the engine
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))
```

**Consiglio:** Tieni i file immagine in una cartella dedicata (`assets/` o `data/`) e usa percorsi relativi. In questo modo lo script rimane portabile su diverse macchine.

---

## Passo 3: Esegui il processo di riconoscimento

Con l’immagine collegata, possiamo finalmente dire al motore di **ocr read tables**. La chiamata `recognize()` restituisce un oggetto risultato che contiene tutto ciò che il motore ha scoperto—blocchi di testo, linee e, soprattutto per noi, tabelle.

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**Perché lo controlliamo:** Alcune immagini possono essere rumorose o i bordi della tabella poco evidenti, facendo sì che il motore li salti. Registrare un avviso ti fornisce un feedback precoce senza interrompere lo script.

---

## Passo 4: Estrai le righe e le celle di ogni tabella

Qui avviene la vera magia. Itereremo su ogni tabella rilevata, estrarremo ogni riga e poi il testo di ciascuna cella. La comprensione di lista interna rende il codice conciso, ma spiegheremo comunque il flusso.

```python
# Step 4 – Iterate over detected tables and collect data
all_tables = []   # Will hold a list of pandas DataFrames

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")

    rows_data = []   # Temporary storage for this table's rows

    for row_obj in table_obj.get_rows():
        # Extract text from each cell in the current row
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    # Convert the raw list of rows into a DataFrame
    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    # Print a human‑readable version to the console
    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))
```

**Cosa sta succedendo?**  

- `enumerate(..., start=1)` fornisce un numero di tabella amichevole per il logging.  
- `row_obj.get_cells()` restituisce ogni oggetto cella; `cell.get_text()` recupera la stringa decodificata dall'OCR.  
- Salviamo le righe in `rows_data`, poi le passiamo a `pandas.DataFrame` che allinea automaticamente le colonne.  
- Il blocco `print` rispecchia l'**output essenziale** mostrato nello snippet originale, così puoi verificare i risultati subito.

**Gestione dei casi limite:** Se una riga ha un numero di celle diverso dalle altre, `pandas` riempirà gli spazi mancanti con `NaN`. Puoi poi pulire il DataFrame con `df.fillna('')` se preferisci stringhe vuote.

---

## Passo 5: Salva le tabelle estratte in un foglio di calcolo

Ora che abbiamo una lista di DataFrame, trasformarli in un workbook Excel (o file CSV) è un gioco da ragazzi. Questo soddisfa l’obiettivo “convertire immagine in foglio di calcolo”.

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**Perché Excel?** La maggior parte degli utenti business ama il formato `.xlsx`. Se preferisci CSV, sostituisci il ciclo con `df.to_csv(f"table_{idx}.csv", index=False)`.

---

## Script completo, pronto da eseguire

Mettiamo tutto insieme: ecco il programma completo che puoi copiare‑incollare ed eseguire.

```python
import ocr
from pathlib import Path
import pandas as pd
import logging

logging.basicConfig(level=logging.INFO)

# ---------- Configuration ----------
image_path = Path("YOUR_DIRECTORY/table_image.png")
output_path = Path("extracted_tables.xlsx")
# ----------------------------------

# Verify image exists
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Initialize OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))

# Run recognition
ocr_result = ocr_engine.recognize()

if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
    exit(0)

all_tables = []

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")
    rows_data = []

    for row_obj in table_obj.get_rows():
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))

# Save to Excel
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        df.to_excel(writer, sheet_name=f"Table_{idx}", index=False)

logging.info(f"All tables saved to {output_path}")
```

**Output console previsto** (supponendo una semplice tabella 2×3):

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

Troverai `extracted_tables.xlsx` nella cartella dello script, ogni tabella su un foglio separato.

---

## Domande frequenti e consigli

| Domanda | Risposta |
|----------|--------|
| **Posso usare una libreria OCR diversa?** | Assolutamente. Il modello rimane lo stesso: carica immagine → riconosci → iterare su `get_tables()`. Basta sostituire import e nomi degli oggetti. |
| **E se la mia immagine è rumorosa?** | Pre‑processa con OpenCV (soglia, deskew) prima di passarla al motore OCR. La riduzione del rumore migliora spesso la precisione di **ocr extract table data**. |
| **Devo installare `openpyxl`?** | Sì, `pandas` lo utilizza in background per l'output Excel. Installa con `pip install openpyxl`. |
| **Come gestisco le celle unite?** | Alcuni SDK espongono `cell.is_merged()`; puoi rilevarle e propagare il valore nell’intervallo unito manualmente. |
| **C'è un modo per estrarre solo tabelle specifiche?** | Filtra per `table_obj.get_confidence()` o controlla parole chiave nell'intestazione prima di elaborare. |

---

## Conclusioni

Ora disponi di una soluzione completa, end‑to‑end, per **estrarre tabelle da immagine**, convertire il risultato in un foglio di calcolo ordinato e gestire anche più tabelle in un’unica immagine. Lo script dimostra come **load image for OCR**, **ocr read tables** e **ocr extract table data**, rimanendo sufficientemente flessibile per le variazioni del mondo reale.

Qual è il prossimo passo? Prova a fornire al motore OCR una pagina PDF renderizzata come immagine, o sperimenta con lingue e font diversi. Potresti anche inviare direttamente i DataFrame a un database o a uno strumento di reporting—la tua immaginazione è il limite.

Se questa guida ti è stata utile, sentiti libero di condividerla, mettere una stella al repository che ospita l'SDK, o lasciare un commento con i tuoi trucchi. Buon coding, e che le tue tabelle siano sempre perfettamente analizzate!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}