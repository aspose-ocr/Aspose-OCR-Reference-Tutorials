---
category: general
date: 2026-03-26
description: Hoe batch‑OCR efficiënt te gebruiken met Python—leer tekst uit afbeeldingen
  en PDF’s te extraheren en OCR‑conversie met parallelle verwerking.
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: nl
og_description: hoe batch‑ocr efficiënt uit te voeren — stapsgewijze gids voor het
  extraheren van tekst uit afbeeldingen, pdf‑ocr‑conversie en batch‑ocr‑verwerking
  met Python.
og_title: 'hoe batch-OCR: snelle parallelle teksteextractie'
tags:
- OCR
- Python
- Parallel Computing
title: 'Hoe batch-OCR: snelle parallelle tekstelextractie'
url: /nl/python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hoe batch-ocr uit te voeren: snelle parallelle tekstextractie

Heb je je ooit afgevraagd **hoe batch-ocr** werkt wanneer je tientallen gescande pagina's, screenshots en PDF's rondliegen? Je bent niet de enige—de meeste ontwikkelaars lopen tegen dezelfde muur aan: elk bestand één voor één verwerken wordt een pijnlijke bottleneck.  

Het goede nieuws is dat je een handvol werkthread‑s kunt opstarten, ze al je bestanden kunt voeren, en kunt zien hoe de OCR‑engine de batch parallel verwerkt. In deze tutorial lopen we een compleet, kant‑klaar voorbeeld door dat **tekst uit afbeeldingen extraheren**, **pdf-ocr-conversie** uitvoeren, en **parallelle ocr-verwerking** benut voor snelheid.

> **Wat je zult meenemen**  
> * Een volledig functioneel Python‑script dat een gemengde lijst van PNG-, TIFF-, PDF- en JPG‑bestanden in één keer verwerkt.  
> * Begrip van waarom een thread‑pool I/O‑gebonden OCR‑taken versnelt.  
> * Tips voor het omgaan met fouten, grote PDF's en aangepaste thread‑aantallen.  

## Vereisten

Voordat we beginnen, zorg dat je het volgende hebt:

| Vereiste | Reden |
|----------|-------|
| Python 3.8+ | Moderne syntaxis & `concurrent.futures` |
| `ocr` library (or any compatible OCR wrapper) | Provides `OcrBatchProcessor` and result objects |
| A handful of sample files (PNG, TIFF, PDF, JPG) | To see the **extract text from images** in action |
| Basic familiarity with threads (optional) | Helpful but not mandatory |

Als je het `ocr`‑pakket nog niet hebt geïnstalleerd, voer dan uit:

```bash
pip install ocr-lib   # replace with the actual package name
```

Nu de omgeving klaar is, laten we het probleem opsplitsen.

## Stap 1: Helpers importeren en de batch‑processor instantiëren

Het eerste wat we nodig hebben is een plek om alle OCR‑taken te verzamelen. De `OcrBatchProcessor`‑klasse doet precies dat—het zet werkitems in een wachtrij en geeft je een lijst met `Future`‑objecten terug.

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*Waarom dit belangrijk is*: Het importeren van `as_completed` stelt ons in staat om direct op elke voltooide taak te reageren, in plaats van te wachten op het langzaamste bestand. Dit is de kern van **batch ocr processing**.

## Stap 2: Het worker‑pool afstemmen voor parallelle uitvoering

Standaard kan de processor één thread gebruiken, wat het doel van batchen ondermijnt. We vragen expliciet om vier workers—voel je vrij dit aantal te verhogen tot het aantal CPU‑cores dat je hebt.

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*Pro tip*: Voor I/O‑gebonden taken zoals OCR krijg je vaak afnemende meeropbrengsten na `CPU cores * 2`. Test een paar waarden en kies het optimale punt.

## Stap 3: Elk bestand dat je wilt OCR‑en in de wachtrij plaatsen

Hier voegen we een gemengde set van afbeelding‑ en PDF‑bestanden toe. De `add`‑methode registreert simpelweg het pad; het daadwerkelijke werk start pas wanneer we de batch indienen.

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

Als je een hele map moet verwerken, doet een snelle `glob`‑lus het werk:

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## Stap 4: De taken starten en futures verzamelen

Het aanroepen van `submit_all` geeft de processor groen licht. Het retourneert een lijst met `Future`‑objecten—beschouw ze als plaatsaanduidingen voor resultaten die later verschijnen.

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

Op dit punt is de OCR‑engine bezig op de achtergrond, elke thread knabbelt aan een bestand.

## Stap 5: Resultaten ophalen zodra ze klaar zijn

Met `as_completed` itereren we over futures in de volgorde waarin ze klaar zijn, niet in de volgorde waarin we ze hebben ingediend. Dit houdt ons script responsief, vooral wanneer sommige PDF's langer duren dan eenvoudige PNG's.

```python
# Step 5 – retrieve each result as it completes
for future in as_completed(ocr_futures):
    try:
        ocr_result = future.result()          # May raise if the job failed
        print("Batch result:\n", ocr_result.get_text())
    except Exception as exc:
        # Graceful error handling – you can log or retry here
        print(f"An OCR job failed: {exc}")
```

**Verwachte output** (afgekapt voor beknoptheid):

```
Batch result:
 The quick brown fox jumps over the lazy dog.
...
Batch result:
 Invoice #12345
 Date: 2026-03-01
 Total: $1,234.56
...
```

Elk blok correspondeert met de platte‑tekst weergave van het originele bestand. Als je **pdf ocr conversion** uitvoert, zal de tekst alles bevatten wat de OCR‑engine van elke pagina kon ontcijferen.

## Omgaan met randgevallen & veelvoorkomende valkuilen

| Situatie | Waar op te letten | Snelle oplossing |
|----------|-------------------|-------------------|
| Een corrupt beeld | `future.result()` werpt `OSError` | Wrap in `try/except` (see code above) |
| Zeer grote PDF's ( > 100 MB ) | Geheugendruk, tragere threads | Increase `thread_count` modestly or split PDF into chapters first |
| Documenten met gemengde talen | Default OCR model may mis‑detect | Pass language hints to `OcrBatchProcessor` if the library supports it |
| Noodzaak om lay‑out te behouden | Plain `get_text()` verliest kolommen | Use `ocr_result.get_hocr()` or similar layout‑aware method |

### Pro tip: Aangepast thread‑aantal op basis van bestandstype

Als je weet dat het grootste deel van je werklast PDF's zijn, kun je meer threads toewijzen aan die en minder aan kleine PNG's. Sommige bibliotheken laten je een per‑job `priority` doorgeven; anders kun je twee aparte batches maken—een voor afbeeldingen, een voor PDF's—en ze gelijktijdig uitvoeren.

## Visueel overzicht (optioneel)

![workflow diagram batch ocr](https://example.com/ocr-workflow.png "workflow batch ocr")

*Het diagram illustreert de stroom van bestandsdetectie → batch‑creatie → parallelle uitvoering → resultaatsaggregatie.*

## Volledig script dat je kunt copy‑pasten

Hieronder staat het volledige programma, klaar om in een `.py`‑bestand te plaatsen. Het bevat alle bovenstaande fragmenten, plus een kleine helper die automatisch ondersteunde bestanden in een map ontdekt.

```python
#!/usr/bin/env python3
"""
How to Batch OCR – Complete Example
-----------------------------------
This script demonstrates parallel OCR processing of mixed image and PDF files.
It shows how to extract text from images, perform pdf ocr conversion, and
handle errors gracefully.
"""

from concurrent.futures import as_completed
import pathlib, fnmatch, sys
import ocr  # replace with your actual OCR library import

def discover_files(root_dir):
    """Yield paths of supported OCR files under *root_dir*."""
    for path in pathlib.Path(root_dir).rglob("*"):
        if fnmatch.fnmatch(path.suffix.lower(), ".png") \
           or fnmatch.fnmatch(path.suffix.lower(), ".tif") \
           or fnmatch.fnmatch(path.suffix.lower(), ".pdf") \
           or fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
            yield str(path)

def main(directory, workers=4):
    # 1️⃣ Initialise batch processor
    ocr_batch = ocr.OcrBatchProcessor()
    ocr_batch.set_thread_count(workers)

    # 2️⃣ Queue every discovered file
    for file_path in discover_files(directory):
        ocr_batch.add(file_path)

    # 3️⃣ Submit all jobs
    futures = ocr_batch.submit_all()

    # 4️⃣ Process results as they arrive
    for fut in as_completed(futures):
        try:
            result = fut.result()
            print("=== OCR RESULT ===")
            print(result.get_text())
            print("\n---\n")
        except Exception as e:
            print(f"[ERROR] OCR failed for a job: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-files>")
        sys.exit(1)
    main(sys.argv[1])
```

Sla dit op als `batch_ocr.py`, wijs het op een map met je scans, en zie de console vullen met geëxtraheerde tekst.  

### Waarom dit werkt

* **Thread pool** – OCR wacht voornamelijk op schijf‑I/O en externe engine‑calls, dus meerdere threads houden de CPU bezig.  
* **`as_completed`** – Je krijgt resultaten zodra ze klaar zijn, wat ideaal is voor UI‑feedback of streaming‑pijplijnen.  
* **Error isolation** – Eén slecht bestand zal de hele batch niet laten falen; het `try/except`‑blok isoleert fouten.

## Conclusie

Kort samengevat, je weet nu **hoe batch-ocr** te gebruiken met Python’s `concurrent.futures` samen met een OCR‑bibliotheek die batchverwerking ondersteunt. Door een bescheiden thread‑pool te configureren, elk ondersteund bestand in de wachtrij te plaatsen, en resultaten op te halen zodra ze klaar zijn, behaal je snelle **parallel ocr processing** zonder betrouwbaarheid op te offeren.  

Vanaf hier kun je:

* De output koppelen aan een zoekindex voor snelle document‑retrieval.  
* Het script uitbreiden om elk resultaat naar een `.txt`‑bestand naast het origineel te schrijven.  
* De ingebouwde thread‑pool vervangen door `asyncio` als je OCR‑bibliotheek async‑API's biedt.  

Blijf experimenteren—verwissel Tesseract, Azure Cognitive Services, of Google Vision, en je zult zien dat hetzelfde patroon werkt. Veel plezier met OCR‑en!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}