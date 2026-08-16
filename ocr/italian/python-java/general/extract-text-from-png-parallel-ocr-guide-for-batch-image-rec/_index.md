---
category: general
date: 2026-03-18
description: Estrai il testo da PNG con Python e Aspose OCR. Impara come caricare
  l'immagine per l'OCR, eseguire l'OCR su più file e realizzare l'OCR batch di immagini
  con riconoscimento parallelo.
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: it
og_description: Estrai testo da PNG con Aspose OCR in Python. Questo tutorial mostra
  come caricare l'immagine per l'OCR, elaborare più file OCR e eseguire OCR batch
  di immagini utilizzando il riconoscimento di immagini in parallelo.
og_title: Estrai testo da PNG – Guida OCR parallela
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: Estrai testo da PNG – Guida OCR parallela per il riconoscimento di immagini
  in batch
url: /it/python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da PNG – Guida OCR Parallela per Riconoscimento di Immagini in Batch

Hai mai avuto bisogno di **estrarre testo da PNG** ma ti sei bloccato al punto in cui un'immagine singola impiega un'eternità per essere elaborata? Non sei solo. In molti progetti reali—pensa a scanner di fatture, digitalizzatori di ricevute o strumenti di archiviazione—la velocità è importante, e processare ogni PNG uno‑per‑uno semplicemente non è sufficiente.  

In questa guida percorreremo una soluzione completa, pronta‑all'uso, che **carica l'immagine per OCR**, esegue **ocr multiple files** in modalità **batch OCR images**, e sfrutta il **riconoscimento di immagini parallelo** con il modulo `threading` di Python. Alla fine avrai uno script che estrae testo da un numero qualsiasi di PNG in pochi secondi, non minuti.

## Cosa ti serve

- Python 3.8 o più recente (la sintassi mostrata funziona anche su 3.10+).  
- Il pacchetto Aspose OCR per Java/​Python (`aspose-ocr`). Puoi installarlo tramite `pip`.  
- Una cartella con una manciata di file PNG che desideri elaborare.  
- Una quantità modesta di RAM—ogni thread mantiene una piccola istanza del motore OCR, quindi anche un laptop può avviare decine di worker.  

Nessun servizio esterno, nessuna chiave cloud e nessun file di configurazione misterioso. Solo puro codice Python che puoi copiare‑incollare ed eseguire.

## Perché estrarre testo da PNG in parallelo?

Elaborare un PNG è legato alla CPU: il motore OCR esegue una serie di algoritmi di analisi dell'immagine che elaborano i dati dei pixel. Quando hai dieci, venti o cento immagini, il tempo totale di esecuzione è essenzialmente la somma di ciascuna esecuzione individuale.  

Creando un thread per ogni file, lasciamo al sistema operativo di programmare questi compiti intensivi per CPU in modo concorrente. Su una macchina multicore questo spesso dimezza—o addirittura quadruplica—il tempo reale. Il compromesso è un consumo di memoria leggermente più alto, ma per la maggior parte dei lavori batch il guadagno in velocità ne vale la pena.  

> **Consiglio pro:** Se stai gestendo centinaia di megabyte di immagini, considera l'uso di `concurrent.futures.ProcessPoolExecutor` invece di `threading`. I processi ti offrono un vero parallelismo sull'interprete CPython vincolato dal GIL, a costo di un po' più overhead.

## Passo 1: Installa Aspose OCR per Python

First things first—let’s get the OCR library onto your system.

```bash
pip install aspose-ocr
```

Quella singola riga scarica gli ultimi binari di Aspose OCR e i relativi binding Python. Se incontri un errore di permessi, prova ad aggiungere `--user` o a usare un ambiente virtuale.

## Passo 2: Carica immagine per OCR – la funzione worker

Now we define the core routine that will be executed in each thread. It **loads image for OCR**, runs the recognition, and prints a preview of the extracted text.

```python
import threading
from asposeocrjava import OcrEngine, OcrResult

def ocr_task(image_path: str):
    """
    Loads a PNG, runs OCR, and prints the first 100 characters of the result.
    Each thread creates its own OcrEngine instance to avoid state clashes.
    """
    # Initialise a fresh engine – this is cheap and thread‑safe.
    engine = OcrEngine()
    # Load image for OCR
    engine.setImageFromFile(image_path)

    # Perform the recognition – this is the CPU‑intensive part.
    result: OcrResult = engine.recognize()

    # Show a preview of the recognized text (first 100 characters)
    preview = result.getText()[:100].replace("\n", " ")
    print(f"[{image_path}] -> {preview}...")
```

Alcune cose da notare:

- **Perché un nuovo `OcrEngine` per thread?** Il motore mantiene buffer interni; condividere un'unica istanza causerebbe condizioni di gara e output confuso.  
- **Perché rimuovere le nuove linee?** Quando registriamo sulla console mantiene la linea ordinata.  
- **Gestione degli errori?** In produzione avresti avvolto il corpo in un `try/except` e magari registrato su un file—qualcosa che tratteremo più avanti.

## Passo 3: Elenca i file PNG da elaborare

You could hard‑code the list, but a more flexible approach is to scan a directory. Below we manually list three files for clarity; replace the paths with your own folder.

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

Se preferisci un rilevamento automatico:

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

Questa piccola modifica ti consente di **estrarre testo da PNG** in blocco senza modificare il codice sorgente ogni volta.

## Passo 4: Configura ocr multiple files con batch OCR images

We now create a thread for every image. This is the heart of the **batch OCR images** pattern.

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

La list comprehension mantiene il codice conciso, e ogni oggetto `Thread` conserva la funzione target e il suo argomento (`image_path`).  

> **Nota a margine:** Il modulo `threading` di Python usa thread nativi del sistema operativo, quindi su un laptop a 4 core vedrai tipicamente fino a quattro thread realmente in esecuzione contemporaneamente; gli altri saranno programmati man mano che i core si liberano.

## Passo 5: Esegui riconoscimento di immagini parallelo

Launching the workers is straightforward: iterate over the list and call `start()`. After that we wait for every thread to finish using `join()`.

```python
# Step 5: Start all threads
for thread in thread_list:
    thread.start()

# Step 6: Wait for every thread to finish before exiting
for thread in thread_list:
    thread.join()
```

When the script finishes, you’ll see a series of lines like:

```
[YOUR_DIRECTORY/doc1.png] -> Invoice #12345 Date: 2024-07-01 Total: $...
[YOUR_DIRECTORY/doc2.png] -> Receipt from Store XYZ Items: 3 Subtotal: $...
[YOUR_DIRECTORY/doc3.png] -> ...
```

Quell'output conferma che ogni PNG è stato elaborato e il testo estratto è disponibile per ulteriori elaborazioni (ad esempio, salvarlo in un database o inserirlo in una pipeline NLP).

## Passo 6: Verifica i risultati e gestisci i casi limite

### Controllo dei risultati vuoti

Sometimes an image is too noisy, or the OCR engine fails to detect any characters. A quick sanity check can save you from downstream errors.

```python
def ocr_task(image_path: str):
    engine = OcrEngine()
    engine.setImageFromFile(image_path)

    result: OcrResult = engine.recognize()
    text = result.getText().strip()

    if not text:
        print(f"[{image_path}] -> No text detected.")
    else:
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")
```

### Limitare il numero di thread concorrenti

If you run this on a modest VM, spawning hundreds of threads might overwhelm the scheduler. You can cap concurrency with a semaphore:

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### Salvare i risultati su file

Instead of printing, you might want a CSV with the filename and extracted text:

```python
import csv
output_path = "ocr_results.csv"

with open(output_path, "w", newline="", encoding="utf-8") as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(["filename", "extracted_text"])

    def ocr_task(image_path: str):
        engine = OcrEngine()
        engine.setImageFromFile(image_path)
        text = engine.recognize().getText().strip()
        writer.writerow([image_path, text])
```

Assicurati di aprire il CSV **una sola volta** al di fuori della funzione thread per evitare condizioni di gara; il writer del modulo `csv` è thread‑safe per scritture semplici.

## Esempio completo funzionante

Putting everything together, here’s a single script you can drop into a file called `batch_ocr.py` and run:

```python
import threading
import pathlib
import csv
from asposeocrjava import OcrEngine, OcrResult

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_DIR = pathlib.Path("YOUR_DIRECTORY")   # <-- change this
OUTPUT_CSV = "ocr_results.csv"
MAX_WORKERS = 8                               # adjust based on your CPU

# ----------------------------------------------------------------------
# Helper: OCR worker
# ----------------------------------------------------------------------
sema = threading.Semaphore(MAX_WORKERS)

def ocr_task(image_path: str, writer):
    """
    Extract text from a single PNG using Aspose OCR.
    This function is designed to run inside a thread.
    """
    with sema:                     # limit concurrent threads
        engine = OcrEngine()
        engine.setImageFromFile(image_path)

        result: OcrResult = engine.recognize()
        text = result.getText().strip()

        # Write to CSV (thread‑safe because writer is shared)
        writer.writerow([image_path, text])

        # Also print a short preview for quick debugging
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")

# ----------------------------------------------------------------------
# Main routine
# ----------------------------------------------------------------------
def main():
    # Discover all PNG files
    image_files = sorted(str(p) for p in IMAGE_DIR.glob("*.png"))
    if not image_files:
        print("No PNG files found in", IMAGE_DIR)
        return

    # Open CSV once, share the writer with all threads
    with open(OUTPUT_CSV, "w", newline="", encoding="utf-8") as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(["filename", "extracted_text"])

        # Create a thread for each image
        threads = [
            threading.Thread(target=ocr_task, args=(path, writer))
            for path in image_files

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}