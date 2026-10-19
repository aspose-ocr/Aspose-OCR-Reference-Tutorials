---
category: general
date: 2026-03-18
description: Extrahera text från PNG med Python och Aspose OCR. Lär dig hur du laddar
  en bild för OCR, kör OCR på flera filer och utför batch-OCR på bilder med parallell
  bildigenkänning.
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: sv
og_description: Extrahera text från PNG med Aspose OCR i Python. Denna handledning
  visar hur du laddar en bild för OCR, bearbetar OCR för flera filer och kör batch‑OCR
  på bilder med parallell bildigenkänning.
og_title: Extrahera text från PNG – Parallell OCR-guide
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: Extrahera text från PNG – Parallell OCR‑guide för batchbildigenkänning
url: /sv/python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från PNG – Parallell OCR-guide för batchbildigenkänning

Har du någonsin behövt **extrahera text från PNG**‑filer men känt dig fast när en enda bild tar evigheter att bearbeta? Du är inte ensam. I många verkliga projekt—tänk fakturaskannrar, kvitto‑digitaliserare eller arkiveringsverktyg—är hastighet viktigt, och att bearbeta varje PNG en‑och‑en räcker helt enkelt inte.  

I den här guiden går vi igenom en komplett, färdig‑att‑köra lösning som **loads image for OCR**, kör **ocr multiple files** i ett **batch OCR images**‑sätt, och utnyttjar **parallel image recognition** med Python‑modulen `threading`. När du är klar har du ett skript som hämtar text från ett godtyckligt antal PNG‑filer på sekunder, inte minuter.

## Vad du behöver

- Python 3.8 eller nyare (syntaxen som visas fungerar även på 3.10+).  
- Aspose OCR för Java/​Python‑paketet (`aspose-ocr`). Du kan installera det via `pip`.  
- En mapp med ett antal PNG‑filer som du vill bearbeta.  
- En måttlig mängd RAM—varje tråd håller en liten OCR‑motorinstans, så även en laptop kan starta dussintals arbetare.

Inga externa tjänster, inga molnnycklar och inga mystiska konfigurationsfiler. Bara ren Python‑kod som du kan kopiera‑klistra och köra.

## Varför extrahera text från PNG parallellt?

Att bearbeta en PNG är CPU‑intensivt: OCR‑motorn kör en serie bildanalysalgoritmer som tuggar igenom pixeldata. När du har tio, tjugo eller hundra bilder är den totala körtiden i princip summan av varje enskild körning.  

Genom att skapa en tråd för varje fil låter vi operativsystemet schemalägga dessa CPU‑tunga jobb samtidigt. På en multi‑core‑maskin halverar—eller till och med kvartar—det ofta den faktiska klocktiden. Nackdelen är ett något högre minnesavtryck, men för de flesta batchjobb är hastighetsvinsten väl värd det.

> **Pro tip:** Om du hanterar hundratals megabyte med bilder, överväg att använda `concurrent.futures.ProcessPoolExecutor` istället för `threading`. Processer ger dig sann parallellism på den GIL‑bundna CPython‑tolken, på bekostnad av lite mer overhead.

## Steg 1: Installera Aspose OCR för Python

Först och främst—låt oss få OCR‑biblioteket på ditt system.

```bash
pip install aspose-ocr
```

Den enda raden hämtar de senaste Aspose OCR‑binärerna och dess Python‑bindningar. Om du får ett behörighetsfel, prova att lägga till `--user` eller använda en virtuell miljö.

## Steg 2: Load image for OCR – arbetsfunktion

Nu definierar vi kärnrutinen som kommer att köras i varje tråd. Den **loads image for OCR**, kör igenkänning och skriver ut en förhandsgranskning av den extraherade texten.

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

Några saker att notera:

- **Why a new `OcrEngine` per thread?** Motorn har interna buffertar; att dela en instans skulle orsaka race‑conditions och förvrängd output.  
- **Why strip newlines?** När vi loggar till konsolen håller det raden prydlig.  
- **Error handling?** I produktion skulle du omsluta kroppen med ett `try/except` och kanske logga till en fil—något vi kommer att gå igenom senare.

## Steg 3: Lista PNG‑filerna du vill bearbeta

Du skulle kunna hårdkoda listan, men ett mer flexibelt tillvägagångssätt är att skanna en katalog. Nedan listar vi manuellt tre filer för tydlighet; ersätt sökvägarna med din egen mapp.

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

Om du föredrar en automatisk upptäckt:

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

Den lilla justeringen låter dig **extract text from PNG**‑filer i bulk utan att röra källkoden varje gång.

## Steg 4: Ställ in ocr multiple files med batch OCR images

Vi skapar nu en tråd för varje bild. Detta är kärnan i **batch OCR images**‑mönstret.

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

List‑comprehension håller koden koncis, och varje `Thread`‑objekt lagrar mål‑funktionen och dess argument (`image_path`).  

> **Side note:** Python‑modulen `threading` använder inhemska OS‑trådar, så på en 4‑core‑laptop ser du vanligtvis upp till fyra trådar som verkligen körs samtidigt; resten schemaläggs när kärnor blir lediga.

## Steg 5: Kör parallell bildigenkänning

Att starta arbetarna är enkelt: iterera över listan och anropa `start()`. Därefter väntar vi på att varje tråd ska avslutas med `join()`.

```python
# Step 5: Start all threads
for thread in thread_list:
    thread.start()

# Step 6: Wait for every thread to finish before exiting
for thread in thread_list:
    thread.join()
```

När skriptet är klart kommer du att se en rad med rader som:

```
[YOUR_DIRECTORY/doc1.png] -> Invoice #12345 Date: 2024-07-01 Total: $...
[YOUR_DIRECTORY/doc2.png] -> Receipt from Store XYZ Items: 3 Subtotal: $...
[YOUR_DIRECTORY/doc3.png] -> ...
```

Den utskriften bekräftar att varje PNG har bearbetats och den extraherade texten är tillgänglig för vidare hantering (t.ex. sparas i en databas eller matas in i en NLP‑pipeline).

## Steg 6: Verifiera resultaten och hantera kantfall

### Kontroll av tomma resultat

Ibland är en bild för brusig, eller så misslyckas OCR‑motorn med att upptäcka några tecken. En snabb kontroll kan rädda dig från fel längre ner i kedjan.

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

### Begränsa antalet samtidiga trådar

Om du kör detta på en modest VM kan det att skapa hundratals trådar överväga schemaläggaren. Du kan begränsa samtidigheten med en semaphore:

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### Spara resultat till en fil

Istället för att skriva ut kan du vilja ha en CSV med filnamnet och den extraherade texten:

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

Se till att öppna CSV‑filen **en gång** utanför trådfunktionen för att undvika race‑conditions; `csv`‑modulens writer är trådsäker för enkla skrivningar.

## Fullt fungerande exempel

När vi sätter ihop allt, här är ett enda skript som du kan lägga i en fil kallad `batch_ocr.py` och köra:

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