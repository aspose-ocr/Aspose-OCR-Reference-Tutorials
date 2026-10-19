---
category: general
date: 2026-03-18
description: Extrahujte text z PNG pomocí Pythonu a Aspose OCR. Naučte se, jak načíst
  obrázek pro OCR, spustit OCR na více souborech a dosáhnout dávkového OCR obrázků
  s paralelním rozpoznáváním obrazu.
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: cs
og_description: Extrahujte text z PNG pomocí Aspose OCR v Pythonu. Tento tutoriál
  ukazuje, jak načíst obrázek pro OCR, zpracovat OCR více souborů a spustit dávkové
  OCR obrázků pomocí paralelního rozpoznávání obrazu.
og_title: Extrahovat text z PNG – Průvodce paralelním OCR
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: Extrahovat text z PNG – Průvodce paralelním OCR pro hromadné rozpoznávání obrázků
url: /cs/python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z PNG – Průvodce paralelním OCR pro hromadné rozpoznávání obrázků

Už jste někdy potřebovali **extrahovat text z PNG** souborů, ale uvízli jste v bodě, kdy zpracování jednoho obrázku trvá věčnost? Nejste v tom sami. V mnoha reálných projektech—například skenery faktur, digitalizátory účtenek nebo archivní nástroje—je rychlost důležitá a zpracování každého PNG po jednom prostě nestačí.  

V tomto průvodci projdeme kompletní, připravené řešení, které **načte obrázek pro OCR**, spustí **ocr multiple files** ve **batch OCR images** režimu a využije **parallel image recognition** pomocí modulu `threading` v Pythonu. Na konci budete mít skript, který získá text z libovolného počtu PNG během sekund, ne minut.

## Co budete potřebovat

- Python 3.8 nebo novější (ukázaná syntaxe funguje také na 3.10+).  
- Balíček Aspose OCR pro Java/​Python (`aspose-ocr`). Můžete jej nainstalovat pomocí `pip`.  
- Složka s několika PNG soubory, které chcete zpracovat.  
- Přiměřené množství RAM—každé vlákno drží malou instanci OCR enginu, takže i notebook může spustit desítky pracovníků.

Žádné externí služby, žádné cloudové klíče a žádné tajemné konfigurační soubory. Pouze čistý Python kód, který můžete zkopírovat‑vložit a spustit.

## Proč extrahovat text z PNG paralelně?

Zpracování PNG je náročné na CPU: OCR engine provádí sérii algoritmů analýzy obrazu, které procházejí pixelová data. Když máte deset, dvacet nebo stovku obrázků, celková doba běhu je v podstatě součtem jednotlivých běhů.  

Vytvořením vlákna pro každý soubor necháme operační systém naplánovat tyto CPU‑intenzivní úlohy souběžně. Na vícejádrovém počítači to často zkrátí (dokonce čtvrtí) reálný čas. Nevýhodou je mírně vyšší spotřeba paměti, ale pro většinu hromadných úloh je zisk na rychlosti rozhodně stojí za to.

> **Tip:** Pokud pracujete se stovkami megabajtů obrázků, zvažte použití `concurrent.futures.ProcessPoolExecutor` místo `threading`. Procesy poskytují skutečný paralelismus na GIL‑vázaném interpreteru CPython, za cenu mírně vyššího režie.

## Krok 1: Instalace Aspose OCR pro Python

Nejprve—dostaňme OCR knihovnu na váš systém.

```bash
pip install aspose-ocr
```

Tento jediný řádek stáhne nejnovější binárky Aspose OCR a jeho Pythonové vazby. Pokud narazíte na chybu oprávnění, zkuste přidat `--user` nebo použít virtuální prostředí.

## Krok 2: Načtení obrázku pro OCR – pracovní funkce

Nyní definujeme hlavní rutinu, která bude spuštěna v každém vlákně. **Načte obrázek pro OCR**, spustí rozpoznání a vytiskne náhled extrahovaného textu.

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

Několik věcí, na které je dobré si dát pozor:

- **Proč nový `OcrEngine` pro každé vlákno?** Engine drží interní buffery; sdílení jedné instance by způsobilo závodní podmínky a poškozený výstup.  
- **Proč odstraňovat koncové znaky řádků?** Když logujeme do konzole, udržuje to řádek úhledný.  
- **Zpracování chyb?** V produkci byste obalili tělo do `try/except` a možná logovali do souboru—něco, co později pokryjeme.

## Krok 3: Seznam PNG souborů, které chcete zpracovat

Můžete seznam zakódovat přímo, ale flexibilnější přístup je prohledat adresář. Níže ručně uvádíme tři soubory pro přehlednost; nahraďte cesty svou vlastní složkou.

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

Pokud dáváte přednost automatickému vyhledávání:

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

Tento malý úprava vám umožní **extrahovat text z PNG** souborů hromadně, aniž byste pokaždé zasahovali do zdrojového kódu.

## Krok 4: Nastavení ocr multiple files s batch OCR images

Nyní vytvoříme vlákno pro každý obrázek. Toto je jádro vzoru **batch OCR images**.

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

List comprehension udržuje kód stručný a každý objekt `Thread` ukládá cílovou funkci a její argument (`image_path`).  

> **Poznámka:** Modul `threading` v Pythonu používá nativní OS vlákna, takže na 4‑jádrovém notebooku obvykle uvidíte až čtyři vlákna běžící současně; zbytek bude naplánován, jakmile se jádra uvolní.

## Krok 5: Spuštění paralelního rozpoznávání obrázků

Spuštění pracovníků je jednoduché: projděte seznam a zavolejte `start()`. Poté počkáme, až každý thread skončí pomocí `join()`.

```python
# Step 5: Start all threads
for thread in thread_list:
    thread.start()

# Step 6: Wait for every thread to finish before exiting
for thread in thread_list:
    thread.join()
```

Když skript skončí, uvidíte řadu řádků jako:

```
[YOUR_DIRECTORY/doc1.png] -> Invoice #12345 Date: 2024-07-01 Total: $...
[YOUR_DIRECTORY/doc2.png] -> Receipt from Store XYZ Items: 3 Subtotal: $...
[YOUR_DIRECTORY/doc3.png] -> ...
```

Tento výstup potvrzuje, že každý PNG byl zpracován a extrahovaný text je k dispozici pro další zpracování (např. uložení do databáze nebo předání do NLP pipeline).

## Krok 6: Ověření výsledků a ošetření okrajových případů

### Kontrola prázdných výsledků

Někdy je obrázek příliš šumivý, nebo OCR engine nedetekuje žádné znaky. Rychlá kontrola může ušetřit problémy v dalších krocích.

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

### Omezení počtu souběžných vláken

Pokud to spouštíte na skromném VM, vytvoření stovek vláken může přetížit plánovač. Můžete omezit souběžnost pomocí semaforu:

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### Ukládání výsledků do souboru

Místo tisknutí můžete chtít CSV se jménem souboru a extrahovaným textem:

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

Ujistěte se, že CSV otevřete **jednou** mimo funkci vlákna, aby nedošlo ke konfliktům; zapisovač modulu `csv` je pro jednoduché zápisy vlákny‑bezpečný.

## Kompletní funkční příklad

Spojením všeho dohromady, zde je jediný skript, který můžete vložit do souboru s názvem `batch_ocr.py` a spustit:

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