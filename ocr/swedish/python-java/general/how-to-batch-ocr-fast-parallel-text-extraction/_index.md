---
category: general
date: 2026-03-26
description: hur man batchar OCR effektivt med Python—lär dig extrahera text från
  bilder och PDF OCR‑konvertering med parallell bearbetning
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: sv
og_description: hur man batchar OCR effektivt—steg‑för‑steg guide för att extrahera
  text från bilder, PDF‑OCR‑konvertering och batch‑OCR‑behandling med Python.
og_title: 'hur man batchar OCR: snabb parallell textutvinning'
tags:
- OCR
- Python
- Parallel Computing
title: 'hur man batchar OCR: snabb parallell textutvinning'
url: /sv/python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hur man batch OCR: snabb parallell textutvinning

Har du någonsin funderat på **hur man batch OCR** när du har dussintals skannade sidor, skärmbilder och PDF-filer liggande omkring? Du är inte ensam—de flesta utvecklare stöter på samma problem: att bearbeta varje fil en efter en blir en smärtsam flaskhals.  

Den goda nyheten är att du kan starta ett fåtal arbets‑trådar, mata dem med alla dina filer och låta OCR‑motorn tugga igenom batchen parallellt. I den här handledningen går vi igenom ett komplett, färdigt‑att‑köra exempel som visar **extract text from images**, utför **pdf ocr conversion**, och utnyttjar **parallel ocr processing** för hastighet.

> **Vad du får med dig**  
> * Ett fullt fungerande Python‑script som bearbetar en blandad lista av PNG-, TIFF-, PDF- och JPG‑filer i ett svep.  
> * Förståelse för varför en trådpool snabbar upp I/O‑bundna OCR‑uppgifter.  
> * Tips för att hantera fel, stora PDF‑filer och anpassade trådräkningar.  

## Förutsättningar

| Krav | Orsak |
|------|-------|
| Python 3.8+ | Modern syntax & `concurrent.futures` |
| `ocr` library (or any compatible OCR wrapper) | Provides `OcrBatchProcessor` and result objects |
| Ett fåtal exempel‑filer (PNG, TIFF, PDF, JPG) | För att se **extract text from images** i aktion |
| Grundläggande kunskap om trådar (valfritt) | Hjälpsamt men inte obligatoriskt |

Om du ännu inte har installerat `ocr`‑paketet, kör:

```bash
pip install ocr-lib   # replace with the actual package name
```

## Steg 1: Importera hjälpfunktioner och skapa batch‑processorn

Det första vi behöver är en plats att samla alla OCR‑jobb. Klassen `OcrBatchProcessor` gör exakt det—den köar arbetsuppgifter och ger dig tillbaka en lista med `Future`‑objekt.

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*Varför detta är viktigt*: Att importera `as_completed` låter oss reagera på varje färdig jobb omedelbart, istället för att vänta på den långsammaste filen. Detta är kärnan i **batch ocr processing**.

## Steg 2: Justera arbets‑poolen för parallell körning

Som standard kan processorn använda en enda tråd, vilket undergräver syftet med batchning. Vi begär uttryckligen fyra arbetare—känn dig fri att öka detta tal till antalet CPU‑kärnor du har.

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*Proffstips*: För I/O‑bundna uppgifter som OCR får du ofta avtagande avkastning efter `CPU cores * 2`. Testa några värden och välj den optimala balansen.

## Steg 3: Köa varje fil du vill OCR:a

Här lägger vi till en blandad samling av bild‑ och PDF‑filer. Metoden `add` registrerar bara sökvägen; själva arbetet startar inte förrän vi skickar in batchen.

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

Om du behöver bearbeta en hel mapp, klarar en snabb `glob`‑loop av jobbet:

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## Steg 4: Skicka iväg jobben och samla futures

Genom att anropa `submit_all` ger du processorn grönt ljus. Den returnerar en lista med `Future`‑objekt—tänk på dem som platshållare för resultat som kommer senare.

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

Vid den här tidpunkten är OCR‑motorn upptagen i bakgrunden, varje tråd tuggar på en fil.

## Steg 5: Hämta resultat så snart de är klara

Genom att använda `as_completed` itererar vi över futures i den ordning de blir klara, inte i den ordning vi skickade dem. Detta håller vårt skript responsivt, särskilt när vissa PDF‑filer tar längre tid än enkla PNG‑filer.

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

**Förväntad output** (avkortad för korthet):

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

Varje block motsvarar den rena textrepresentationen av den ursprungliga filen. Om du gör **pdf ocr conversion**, kommer texten att innehålla allt som OCR‑motorn kunde avkoda från varje sida.

## Hantera kantfall & vanliga fallgropar

| Situation | Vad att hålla utkik efter | Snabb fix |
|-----------|---------------------------|-----------|
| En korrupt bild | `future.result()` kastar `OSError` | Omge med `try/except` (se koden ovan) |
| Mycket stora PDF‑filer ( > 100 MB ) | Minnesbelastning, långsammare trådar | Öka `thread_count` måttligt eller dela upp PDF‑filen i kapitel först |
| Dokument med blandade språk | Standard‑OCR‑modellen kan felidentifiera | Skicka språk‑tips till `OcrBatchProcessor` om biblioteket stödjer det |
| Behöver bevara layout | Vanlig `get_text()` förlorar kolumner | Använd `ocr_result.get_hocr()` eller liknande layout‑medveten metod |

### Proffstips: Anpassad trådräknare baserat på filtyp

Om du vet att det mesta av din arbetsbelastning är PDF‑filer, kan du tilldela fler trådar för dem och färre för små PNG‑filer. Vissa bibliotek låter dig skicka en per‑jobb `priority`; annars kan du skapa två separata batcher—en för bilder, en för PDF‑filer—och köra dem samtidigt.

## Visuell översikt (valfritt)

![diagram över batch OCR arbetsflöde](https://example.com/ocr-workflow.png "batch OCR arbetsflöde")

*Diagrammet illustrerar flödet från filupptäckt → batch‑skapande → parallell körning → resultat‑aggregering.*

## Fullt skript du kan kopiera‑klistra in

Nedan är hela programmet, redo att släppas in i en `.py`‑fil. Det inkluderar alla kodsnuttar ovan, plus en liten hjälpfunktion som automatiskt upptäcker stödjade filer i en katalog.

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

Spara detta som `batch_ocr.py`, peka på en mapp som innehåller dina skanningar, och se konsolen fyllas med extraherad text.  

### Varför detta fungerar

* **Thread pool** – OCR är mestadels väntande på disk‑I/O och externa motor‑anrop, så flera trådar håller CPU:n upptagen.  
* **`as_completed`** – Du får resultat så snart de är klara, vilket är idealiskt för UI‑feedback eller strömmande pipelines.  
* **Error isolation** – En dålig fil kommer inte att sänka hela batchen; `try/except`‑blocket isolerar fel.

## Slutsats

Kort sagt, du vet nu **hur man batch OCR** med Python’s `concurrent.futures` tillsammans med ett OCR‑bibliotek som stödjer batch‑bearbetning. Genom att konfigurera en modest trådpool, köa varje stödjad fil och hämta resultat när de är klara, får du snabb **parallel ocr processing** utan att offra pålitlighet.  

Från och med nu kan du:

* Koppla outputen till ett sökindex för snabb dokumenthämtning.  
* Utöka skriptet för att skriva varje resultat till en `.txt`‑fil bredvid originalet.  
* Ersätt den inbyggda trådpoolen med `asyncio` om ditt OCR‑bibliotek erbjuder async‑API:er.  

Fortsätt experimentera—byt ut mot Tesseract, Azure Cognitive Services eller Google Vision, så ser du att samma mönster gäller. Lycka till med OCR‑andet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}