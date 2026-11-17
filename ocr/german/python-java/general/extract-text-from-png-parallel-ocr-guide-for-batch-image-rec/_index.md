---
category: general
date: 2026-03-18
description: Extrahiere Text aus PNG mit Python und Aspose OCR. Erfahre, wie du ein
  Bild für OCR lädst, OCR für mehrere Dateien ausführst und Batch‑OCR von Bildern
  mit paralleler Bilderkennung erreichst.
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: de
og_description: Extrahiere Text aus PNG mit Aspose OCR in Python. Dieses Tutorial
  zeigt, wie man ein Bild für OCR lädt, mehrere Dateien verarbeitet und Batch‑OCR‑Bilder
  mit paralleler Bilderkennung ausführt.
og_title: Text aus PNG extrahieren – Parallel‑OCR‑Leitfaden
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: Text aus PNG extrahieren – Parallel‑OCR‑Leitfaden für die Batch‑Bilderkennung
url: /de/python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus PNG extrahieren – Parallel‑OCR‑Leitfaden für Batch‑Bild­erkennung

Haben Sie schon einmal **Text aus PNG**‑Dateien extrahieren mussten, aber sind an dem Punkt hängen geblieben, an dem ein einzelnes Bild ewig braucht? Sie sind nicht allein. In vielen realen Projekten – denken Sie an Rechnungsscanner, Belegdigitalisierer oder Archivierungs‑Tools – ist Geschwindigkeit entscheidend, und das sequentielle Verarbeiten jedes PNGs reicht einfach nicht.

In diesem Leitfaden gehen wir Schritt für Schritt durch eine komplette, sofort einsatzbereite Lösung, die **loads image for OCR** ausführt, **ocr multiple files** in einer **batch OCR images**‑Weise verarbeitet und **parallel image recognition** mit Pythons `threading`‑Modul nutzt. Am Ende haben Sie ein Skript, das Text aus beliebig vielen PNGs in Sekunden statt Minuten extrahiert.

## What You’ll Need

- Python 3.8 oder neuer (die gezeigte Syntax funktioniert auch unter 3.10+).  
- Das Aspose OCR für Java/​Python‑Paket (`aspose-ocr`). Sie können es über `pip` installieren.  
- Ein Ordner mit einer Handvoll PNG‑Dateien, die Sie verarbeiten möchten.  
- Ein moderater Arbeitsspeicher – jeder Thread hält eine kleine OCR‑Engine‑Instanz, sodass selbst ein Laptop Dutzende Worker starten kann.

Keine externen Dienste, keine Cloud‑Keys und keine mysteriösen Konfigurationsdateien. Nur reiner Python‑Code, den Sie copy‑paste‑en und ausführen können.

## Why extract text from PNG in parallel?

Die Verarbeitung eines PNGs ist CPU‑bound: Die OCR‑Engine führt eine Reihe von Bild‑Analyse‑Algorithmen aus, die Pixeldaten durchkauen. Haben Sie zehn, zwanzig oder hundert Bilder, ist die Gesamtlaufzeit im Wesentlichen die Summe der einzelnen Durchläufe.

Indem wir für jede Datei einen Thread starten, lassen wir das Betriebssystem diese CPU‑intensiven Jobs gleichzeitig planen. Auf einer Mehrkern‑Maschine halbiert – oder sogar viertelt – sich dadurch häufig die Echtzeit. Der Nachteil ist ein etwas größerer Speicherverbrauch, aber für **most batch jobs** ist der Geschwindigkeitsgewinn mehr als gerechtfertigt.

> **Pro tip:** Wenn Sie mit Hunderten von Megabyte Bildmaterial arbeiten, sollten Sie `concurrent.futures.ProcessPoolExecutor` anstelle von `threading` verwenden. Prozesse bieten echten Parallelismus im GIL‑gebundenen CPython‑Interpreter, allerdings zu **einem etwas höheren** Overhead.

## Step 1: Install Aspose OCR for Python

First things first – let’s get the OCR library onto **your** system.

```bash
pip install aspose-ocr
```

Diese einzelne Zeile holt die neuesten Aspose OCR‑Binärdateien und die zugehörigen Python‑Bindings. Wenn Sie einen Berechtigungsfehler erhalten, versuchen Sie es mit `--user` oder nutzen Sie eine virtuelle Umgebung.

## Step 2: Load image for OCR – the worker function

Now we define the core routine that will be executed in each thread. It **loads image for OCR**, runs the recognition, and prints a preview **of the extracted text**.

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

Ein paar Dinge, die Sie beachten sollten:

- **Warum ein neuer `OcrEngine` pro Thread?** Die Engine hält interne Puffer; das Teilen einer Instanz würde zu Race‑Conditions und verzerrten Ausgaben führen.  
- **Warum Zeilenumbrüche entfernen?** Beim Loggen in die Konsole bleibt die Zeile so übersichtlich.  
- **Fehlerbehandlung?** In der Produktion würden Sie den Körper in ein `try/except` packen und vielleicht in eine Datei loggen – etwas, das wir später behandeln werden.

## Step 3: List the PNG files you want to process

You could hard‑code the list, but a more flexible approach is to scan a directory. Below we manually list three files for clarity; replace the paths with your own folder.

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

If you prefer an automatic discovery:

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

That small tweak lets you **extract text from PNG** files in bulk without touching the source code each time.

## Step 4: Set up ocr multiple files with batch OCR images

We now create a thread for every image. This is the heart of the **batch OCR images** pattern.

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

The list comprehension keeps the code concise, and each `Thread` object stores the target function and its argument (`image_path`).  

> **Side note:** Python’s `threading` module uses native OS threads, so on a 4‑core laptop you’ll typically see up to four threads truly running at once; the rest will be scheduled as cores become free.

## Step 5: Run parallel image recognition

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

That output confirms each PNG was processed and the extracted text is available for further handling (e.g., saving to a database or feeding into a NLP pipeline).

## Step 6: Verify the results and handle edge cases

### Checking for empty results

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

### Limiting the number of concurrent threads

If you run this on a modest VM, spawning hundreds of threads might overwhelm the scheduler. You can cap concurrency with a semaphore:

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### Saving results to a file

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

Make sure to open the CSV **once** outside the thread function to avoid race conditions; the `csv` module’s writer is thread‑safe for simple writes.

## Full Working Example

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