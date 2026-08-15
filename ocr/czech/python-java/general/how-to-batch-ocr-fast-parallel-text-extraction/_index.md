---
category: general
date: 2026-03-26
description: Jak efektivně provádět dávkové OCR pomocí Pythonu – naučte se extrahovat
  text z obrázků a PDF pomocí OCR konverze s paralelním zpracováním.
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: cs
og_description: Jak efektivně provádět hromadné OCR – krok za krokem průvodce extrakcí
  textu z obrázků, konverzí PDF pomocí OCR a hromadným zpracováním OCR v Pythonu.
og_title: 'jak dávkovat OCR: rychlé paralelní získávání textu'
tags:
- OCR
- Python
- Parallel Computing
title: 'Jak provádět dávkové OCR: rychlé paralelní získávání textu'
url: /cs/python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak provádět hromadný OCR: rychlé paralelní získávání textu

Už jste se někdy zamýšleli **jak provádět hromadný OCR**, když máte kolem sebe desítky naskenovaných stránek, snímků obrazovky a PDF? Nejste v tom sami — většina vývojářů narazí na stejný problém: zpracování každého souboru po jednom se stává bolestivým úzkým místem.  

Dobrá zpráva je, že můžete spustit několik pracovních vláken, nasytit je všemi soubory a sledovat, jak OCR engine projíždí dávku paralelně. V tomto tutoriálu projdeme kompletním, připraveným příkladem, který ukazuje **extrakci textu z obrázků**, provádí **pdf OCR konverzi** a využívá **paralelní OCR zpracování** pro rychlost.

> **Co si odnesete**  
> * Plně funkční Python skript, který najednou zpracuje smíšený seznam souborů PNG, TIFF, PDF a JPG.  
> * Porozumění tomu, proč thread pool urychluje I/O‑vázané OCR úlohy.  
> * Tipy pro zacházení s chybami, velkými PDF a vlastními počty vláken.  

## Požadavky

Než se ponoříme, ujistěte se, že máte:

| Požadavek | Důvod |
|-------------|--------|
| Python 3.8+ | Moderní syntaxe & `concurrent.futures` |
| `ocr` knihovna (nebo jakýkoli kompatibilní OCR wrapper) | Poskytuje `OcrBatchProcessor` a objekty výsledků |
| Několik ukázkových souborů (PNG, TIFF, PDF, JPG) | Pro zobrazení **extrakce textu z obrázků** v akci |
| Základní znalost vláken (volitelné) | Užitečné, ale ne povinné |

Pokud jste ještě nenainstalovali balíček `ocr`, spusťte:

```bash
pip install ocr-lib   # replace with the actual package name
```

Nyní, když je prostředí připravené, rozdělíme problém na části.

## Krok 1: Naimportujte pomocné funkce a vytvořte batch procesor

První věc, kterou potřebujeme, je místo, kde budeme shromažďovat všechny OCR úlohy. Třída `OcrBatchProcessor` dělá právě to — zařadí pracovní položky do fronty a vrátí vám seznam objektů `Future`.

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*Proč je to důležité*: Importování `as_completed` nám umožňuje okamžitě reagovat na každou dokončenou úlohu, místo čekání na nejpomalejší soubor. To je jádro **hromadného OCR zpracování**.

## Krok 2: Nastavte pool pracovníků pro paralelní vykonání

Ve výchozím nastavení může procesor používat jedno vlákno, což by účel dávkování zrušilo. Výslovně požádáme o čtyři pracovníky — klidně můžete zvýšit toto číslo na počet vašich CPU jader.

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*Tip*: Pro I/O‑vázané úlohy jako OCR často po `CPU cores * 2` dochází k úbytku přínosu. Otestujte několik hodnot a najděte optimální bod.

## Krok 3: Zařaďte každý soubor, který chcete OCRovat

Zde přidáme smíšený balík obrázkových i PDF souborů. Metoda `add` jen zaznamená cestu; skutečná práce začne až po odeslání dávky.

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

Pokud potřebujete zpracovat celý adresář, stačí rychlý `glob` cyklus:

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## Krok 4: Spusťte úlohy a sbírejte futures

Volání `submit_all` dává procesoru zelenou. Vrátí seznam objektů `Future` — považujte je za zástupce výsledků, které se objeví později.

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

V tomto okamžiku OCR engine pracuje na pozadí, každé vlákno sežere jeden soubor.

## Krok 5: Odebírejte výsledky hned, jakmile jsou hotové

Pomocí `as_completed` iterujeme přes futures v pořadí, v jakém končí, nikoli v pořadí, v jakém jsme je odeslali. To udržuje skript responzivní, zejména když některé PDF trvají déle než jednoduché PNG.

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

**Očekávaný výstup** (zkrácený pro stručnost):

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

Každý blok odpovídá čistému textovému zobrazení původního souboru. Pokud provádíte **pdf OCR konverzi**, text bude obsahovat vše, co OCR engine dokázal rozpoznat na každé stránce.

## Řešení okrajových případů a častých úskalí

| Situace | Na co si dát pozor | Rychlé řešení |
|-----------|-------------------|-----------|
| Poškozený obrázek | `future.result()` vyvolá `OSError` | Zabalte do `try/except` (viz kód výše) |
| Velmi velké PDF (> 100 MB) | Tlak na paměť, pomalejší vlákna | Mírně zvýšte `thread_count` nebo PDF rozdělte na kapitoly |
| Dokumenty ve smíšených jazycích | Výchozí OCR model může špatně detekovat | Předávejte nápovědy jazyka `OcrBatchProcessor`, pokud knihovna podporuje |
| Potřeba zachovat rozložení | Pouhé `get_text()` ztrácí sloupce | Použijte `ocr_result.get_hocr()` nebo podobnou metodu citlivou na rozložení |

### Tip: Vlastní počet vláken podle typu souboru

Pokud víte, že většina vašeho zatížení jsou PDF, můžete pro ně alokovat více vláken a pro malé PNG méně. Některé knihovny umožňují předat `priority` na úrovni úlohy; jinak můžete vytvořit dva samostatné batch — jeden pro obrázky, druhý pro PDF — a spustit je souběžně.

## Vizualizace (volitelné)

![diagram pracovního postupu hromadného OCR](https://example.com/ocr-workflow.png "diagram pracovního postupu hromadného OCR")

*Diagram ukazuje tok od objevení souborů → vytvoření dávky → paralelní vykonání → agregaci výsledků.*

## Kompletní skript, který můžete zkopírovat‑vložit

Níže je celý program, připravený k uložení do souboru `.py`. Obsahuje všechny výše uvedené úryvky a malého pomocníka, který automaticky objeví podporované soubory v adresáři.

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

Uložte jej jako `batch_ocr.py`, nasměrujte na složku s vašimi skeny a sledujte, jak se konzole zaplní extrahovaným textem.  

### Proč to funguje

* **Thread pool** – OCR většinou čeká na disk I/O a volání externího engine, takže více vláken udržuje CPU v činnosti.  
* **`as_completed`** – Dostáváte výsledky hned, jak jsou připravené, což je ideální pro UI zpětnou vazbu nebo streamovací pipeline.  
* **Izolace chyb** – Jeden špatný soubor nesrazí celou dávku; blok `try/except` izoluje selhání.

## Závěr

Stručně řečeno, nyní víte **jak provádět hromadný OCR** pomocí Pythonu `concurrent.futures` a OCR knihovny, která podporuje dávkové zpracování. Nastavením rozumného thread poolu, zařazením všech podporovaných souborů a odebíráním výsledků, jakmile jsou hotové, dosáhnete rychlého **paralelního OCR zpracování** bez ztráty spolehlivosti.  

Odtud můžete:

* Připojit výstup k vyhledávacímu indexu pro rychlé vyhledávání dokumentů.  
* Rozšířit skript tak, aby zapisoval každý výsledek do souboru `.txt` vedle originálu.  
* Nahradit vestavěný thread pool `asyncio`, pokud vaše OCR knihovna nabízí asynchronní API.  

Experimentujte dál — vyzkoušejte Tesseract, Azure Cognitive Services nebo Google Vision a uvidíte, že stejný vzor funguje všude. Šťastné OCR‑ování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}