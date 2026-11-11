---
category: general
date: 2026-03-18
description: Tekst extraheren uit PNG met Python en Aspose OCR. Leer hoe je een afbeelding
  laadt voor OCR, OCR uitvoert op meerdere bestanden, en batch‑OCR van afbeeldingen
  realiseert met parallelle beeldherkenning.
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: nl
og_description: Tekst extraheren uit PNG met Aspose OCR in Python. Deze tutorial laat
  zien hoe je een afbeelding laadt voor OCR, meerdere bestanden verwerkt met OCR en
  batch‑OCR‑afbeeldingen uitvoert met parallelle beeldherkenning.
og_title: Tekst uit PNG extraheren – Parallelle OCR-gids
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: Tekst extraheren uit PNG – Parallelle OCR-gids voor batchafbeeldingsherkenning
url: /nl/python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst extraheren uit PNG – Parallelle OCR-gids voor batchafbeeldingsherkenning

Heb je ooit **extract text from PNG** bestanden moeten **extraheren**, maar zat je vast op het punt waar één afbeelding eeuwig duurt om te verwerken? Je bent niet de enige. In veel real‑world projecten—denk aan factuurscanners, bondigitalizers of archiveringshulpmiddelen—is snelheid belangrijk, en het verwerken van elke PNG één voor één is gewoon niet voldoende.  

In deze gids lopen we een complete, kant‑klaar oplossing door die **loads image for OCR**, **ocr multiple files** in een **batch OCR images** manier uitvoert, en **parallel image recognition** benut met Python's `threading` module. Aan het einde heb je een script dat tekst uit een willekeurig aantal PNG's haalt in seconden, niet minuten.

## Wat je nodig hebt

- Python 3.8 of nieuwer (de getoonde syntaxis werkt ook op 3.10+).  
- Het Aspose OCR voor Java/​Python pakket (`aspose-ocr`). Je kunt het installeren via `pip`.  
- Een map met een handvol PNG‑bestanden die je wilt verwerken.  
- Een bescheiden hoeveelheid RAM—elke thread houdt een kleine OCR‑engine‑instantie, dus zelfs een laptop kan tientallen workers starten.

Geen externe services, geen cloud‑sleutels, en geen mysterieuze configuratiebestanden. Gewoon pure Python‑code die je kunt copy‑paste en uitvoeren.

## Waarom tekst uit PNG parallel extraheren?

Het verwerken van een PNG is CPU‑gebonden: de OCR‑engine voert een reeks beeld‑analyse‑algoritmen uit die door pixeldata heen gaan. Wanneer je tien, twintig of honderd afbeeldingen hebt, is de totale uitvoeringstijd in feite de som van elke individuele run.  

Door voor elk bestand een thread te starten, laten we het besturingssysteem die CPU‑intensieve taken gelijktijdig plannen. Op een multi‑core machine halveert—of zelfs kwartelt—de wandklok‑tijd vaak. Het compromis is een iets grotere geheugengebruik, maar voor de meeste batch‑taken is de snelheidswinst het zeker waard.

> **Pro tip:** Als je te maken hebt met honderden megabytes aan afbeeldingen, overweeg dan `concurrent.futures.ProcessPoolExecutor` te gebruiken in plaats van `threading`. Processen geven je echte paralleliteit op de GIL‑gebonden CPython interpreter, tegen een iets hogere overhead.

## Stap 1: Installeer Aspose OCR voor Python

Allereerst—laten we de OCR‑bibliotheek op je systeem krijgen.

```bash
pip install aspose-ocr
```

Die enkele regel haalt de nieuwste Aspose OCR‑binaries en de Python‑bindings op. Als je een permissiefout krijgt, probeer dan `--user` toe te voegen of een virtuele omgeving te gebruiken.

## Stap 2: Laad afbeelding voor OCR – de worker‑functie

Nu definiëren we de kernroutine die in elke thread wordt uitgevoerd. Het **loads image for OCR**, voert de herkenning uit, en print een voorbeeld van de geëxtraheerde tekst.

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

Een paar dingen om op te merken:

- **Why a new `OcrEngine` per thread?** De engine bevat interne buffers; het delen van één instantie zou race‑conditions en onsamenhangende output veroorzaken.  
- **Why strip newlines?** Wanneer we naar de console loggen houdt het de regel netjes.  
- **Error handling?** In productie zou je de body omhullen met een `try/except` en misschien naar een bestand loggen—iets wat we later behandelen.

## Stap 3: Lijst de PNG‑bestanden die je wilt verwerken

Je zou de lijst hard‑coderen, maar een flexibelere aanpak is om een map te scannen. Hieronder vermelden we handmatig drie bestanden voor duidelijkheid; vervang de paden door je eigen map.

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

Als je een automatische ontdekking verkiest:

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

Die kleine aanpassing laat je **extract text from PNG** bestanden in bulk uitvoeren zonder elke keer de broncode aan te passen.

## Stap 4: Stel ocr multiple files in met batch OCR images

We maken nu een thread voor elke afbeelding. Dit is het hart van het **batch OCR images** patroon.

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

De list comprehension houdt de code beknopt, en elk `Thread`‑object slaat de doel‑functie en zijn argument (`image_path`) op.  

> **Side note:** Python's `threading` module gebruikt native OS‑threads, dus op een 4‑core laptop zie je meestal tot vier threads echt tegelijk draaien; de rest wordt ingepland zodra cores vrij komen.

## Stap 5: Voer parallelle beeldherkenning uit

Het starten van de workers is eenvoudig: iterate over de lijst en roep `start()` aan. Daarna wachten we tot elke thread klaar is met `join()`.

```python
# Step 5: Start all threads
for thread in thread_list:
    thread.start()

# Step 6: Wait for every thread to finish before exiting
for thread in thread_list:
    thread.join()
```

Wanneer het script klaar is, zie je een reeks regels zoals:

```
[YOUR_DIRECTORY/doc1.png] -> Invoice #12345 Date: 2024-07-01 Total: $...
[YOUR_DIRECTORY/doc2.png] -> Receipt from Store XYZ Items: 3 Subtotal: $...
[YOUR_DIRECTORY/doc3.png] -> ...
```

Die output bevestigt dat elke PNG is verwerkt en de geëxtraheerde tekst beschikbaar is voor verdere verwerking (bijv. opslaan in een database of invoeren in een NLP‑pipeline).

## Stap 6: Verifieer de resultaten en behandel randgevallen

### Controleren op lege resultaten

Soms is een afbeelding te ruisachtig, of slaagt de OCR‑engine er niet in om tekens te detecteren. Een snelle sanity‑check kan je redden van downstream fouten.

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

### Het aantal gelijktijdige threads beperken

Als je dit op een bescheiden VM draait, kan het starten van honderden threads de scheduler overweldigen. Je kunt de gelijktijdigheid beperken met een semaphore:

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### Resultaten opslaan naar een bestand

In plaats van te printen, wil je misschien een CSV met de bestandsnaam en geëxtraheerde tekst:

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

Zorg ervoor dat je de CSV **eenmalig** buiten de thread‑functie opent om race‑conditions te vermijden; de writer van de `csv` module is thread‑safe voor eenvoudige writes.

## Volledig werkend voorbeeld

Alles samenvoegend, hier is een enkel script dat je kunt plaatsen in een bestand genaamd `batch_ocr.py` en uitvoeren:

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