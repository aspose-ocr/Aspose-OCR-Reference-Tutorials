---
category: general
date: 2026-06-25
description: Extrahujte text z obrázků pomocí knihovny Python aocr – naučte se dávkové
  OCR, nastavte režim rozpoznávání na tištěný a přidejte AI postprocesor.
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: cs
og_description: Extrahujte text z obrázků pomocí knihovny aocr pro Python. Tento tutoriál
  ukazuje dávkové OCR, režim rozpoznávání tištěného textu a volitelný AI postprocesor.
og_title: Extrahujte text z obrázků v Pythonu – Kompletní průvodce aocr batch
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: Extrahovat text z obrázků v Pythonu pomocí aocr OCR Batch
url: /cs/python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z obrázků v Pythonu pomocí aocr OCR Batch

Už jste někdy potřebovali **extrahovat text z obrázků**, ale zahltil vás spousta drobných kroků? Nejste v tom sami. Ať už digitalizujete naskenované formuláře, získáváte data z účtenek nebo budujete prohledávatelný archiv, získání spolehlivých OCR výsledků ve velkém měřítku může připomínat výstup na strmý kopec.

Dobrá zpráva? S **knihovnou aocr** můžete během několika řádků nastavit kompletní **Python OCR batch**. V tomto průvodci si ukážeme, jak vytvořit OCR batch, načíst všechny podporované obrázky ze složky, zvolit správný **recognition mode printed** a dokonce připojit **AI postprocessor** pro extra zvýšení přesnosti. Na konci budete mít připravený skript, který extrahuje text z obrázků a ukáže vám, kolik textu bylo zachyceno u každého souboru.

## Co se naučíte

- Jak nainstalovat a importovat balíček `aocr`.
- Nastavení `OcrBatch` pro automatické zpracování tisíců souborů.
- Výběr optimálního režimu rozpoznávání pro tištěné dokumenty.
- (Volitelné) Připojení AI post‑processoru pro vyčištění šumných výsledků.
- Zobrazení cesty ke každému souboru spolu s délkou jeho extrahovaného textu.
- Tipy pro řešení okrajových případů, jako jsou nepodporované formáty nebo prázdné stránky.

### Předpoklady

- Python 3.8 nebo novější nainstalovaný na vašem počítači.  
- Základní znalost Python skriptování (smyčky, importy, atd.).  
- Přístup ke složce s naskenovanými obrázky (PNG, JPG, TIFF, atd.).  

Pokud máte vše připravené, pojďme na to — žádné externí služby nejsou potřeba.

## Krok 1: Instalace knihovny aocr

Nejprve základ. Balíček `aocr` není součástí standardní knihovny, takže jej musíte stáhnout z PyPI.

```bash
pip install aocr
```

> **Tip:** Použijte virtuální prostředí (`python -m venv .venv`) pro izolaci závislostí.  

Po instalaci můžete importovat hlavní třídy.

```python
# core imports
import aocr
```

## Krok 2: Vytvoření instance OCR Batch

`OcrBatch` je „pracovní kůň“, který prochází váš adresář a sleduje každý soubor s obrázkem. Představte si ho jako dopravní pás, který posílá obrázky do OCR motoru.

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

V tuto chvíli je batch prázdný, ale naplníme jej v dalším kroku.

## Krok 3: Přidání všech podporovaných obrázků ze složky (rekurzivně)

Pravděpodobně máte vnořenou strukturu složek — možná jednu podsložku na klienta nebo na měsíc. Metoda `add_folder` projde strom za vás a načte každý obrázek, který umí přečíst.

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

Nahraďte `"YOUR_DIRECTORY/scanned_forms/"` skutečnou cestou ve vašem systému. Po tomto volání `ocr_batch.file_paths` obsahuje seznam absolutních názvů souborů a batch přesně ví, kolik položek bude zpracovávat.

## Krok 4: Výběr režimu rozpoznávání pro tištěný text

Engine `aocr` podporuje několik režimů (handwritten, printed, mixed). Protože pracujeme s čistými tištěnými formuláři, nastavíme režim odpovídajícím způsobem. Tento malý příznak může dramaticky zlepšit přesnost, protože motor přeskočí těžkopádné heuristiky potřebné pro kurzívní písmo.

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **Proč je to důležité:** Tištěný text má konzistentní základní linku a tvary znaků, což umožňuje OCR modelu použít užší slovníky znaků. Pokud necháte režim na „auto“, můžete získat extra šum u nízkokvalitních skenů.

## Krok 5: (Volitelné) Připojení AI post‑processoru

Pokud vaše skeny trpí rozmazáním, nízkým kontrastem nebo neobvyklými fonty, AI post‑processor může vyčistit surový OCR výstup před tím, než jej předáte dalším systémům. Metoda `set_ai_postprocessor` očekává objekt, který implementuje rozhraní `process(text: str) -> str`.

Níže je minimální příklad s fiktivní třídou `SimpleCleaner`. Ve skutečnosti můžete zapojit HuggingFace transformer, vlastní jazykový model nebo dokonce pravidlový kontrolor pravopisu.

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

Pokud tento krok přeskočíte, batch jednoduše vrátí surové OCR řetězce.

## Krok 6: Spuštění OCR na celém batchi a sběr výsledků

Nyní začíná těžká část. Metoda `run` projde každý soubor, spustí OCR engine, pošle výstup přes volitelný AI post‑processor a vrátí seznam řetězců — jeden na obrázek.

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

Protože metoda vrací obyčejný Python seznam, můžete s ním zacházet jako s libovolnou kolekcí — uložit jej, zapsat do CSV nebo vložit do databáze.

## Krok 7: Zobrazení cesty ke každému souboru spolu s délkou extrahovaného textu

Rychlá kontrola je vytisknout, kolik znaků bylo extrahováno z každého souboru. Pokud je stránka prázdná nebo OCR selhalo, uvidíte délku `0`.

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

Typický výstup vypadá takto:

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

Vidět `0` okamžitě ukazuje, které soubory potřebují další kontrolu (možná jsou poškozené nebo nejsou vůbec obrázkem).

## Řešení běžných okrajových případů

### 1. Nepodporované typy souborů

`aocr` tiše přeskočí soubory, které nedokáže dekódovat. Pokud máte podezření, že ve složce jsou PDF nebo BMP, odfiltrujte je předem:

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. Velké batchi a spotřeba paměti

Zpracování tisíců vysokého rozlišení skenů může výrazně navýšit paměťovou náročnost. Omezte to zpracováním po částech:

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. Prázdné nebo nízkokontrastní stránky

Pokud stránka obsahuje méně než 10 znaků, můžete ji označit k ruční revizi:

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## Kompletní funkční příklad

Spojením všech částí získáte skript, který můžete zkopírovat a spustit okamžitě. Uložte jej jako `batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**Očekávaný výstup** (zkrácený pro stručnost):

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

Spusťte jej pomocí:

```bash
python batch_ocr.py
```

Pokud je vše nastaveno správně, uvidíte řádek pro každý obrázek, který uvádí počet znaků extrahovaného textu.

## Často kladené otázky

**Q: Funguje to i s PDF?**  
A: Ne přímo. `aocr` pracuje jen s rastrovými obrázky. PDF nejprve převeďte na PNG/TIFF (např. pomocí `pdf2image`).

**Q: Můžu změnit režim rozpoznávání na ručně psaný?**  
A: Samozřejmě — stačí nahradit `aocr.RecognitionMode.PRINTED` za `aocr.RecognitionMode.HANDWRITTEN`. Očekávejte pomalejší běh, ale lepší výsledky u kurzívního textu.

**Q: Co když potřebuji vícejazykovou podporu?**  
A: Knihovna obsahuje jazykové balíčky. Nainstalujte požadovaný jazykový modul (`pip install aocr-lang-fr` pro francouzštinu atd.) a nastavte `ocr_batch.language = "fr"` před spuštěním.

## Další kroky a související témata

- **Paralelní zpracování:** Zabalte provádění batche do `concurrent.futures.ThreadPoolExecutor` pro využití více CPU jader.  
- **Ukládání výsledků:** Zapište `ocr_results` do CSV nebo SQLite databáze pro následnou analytiku.  
- **Integrace s cloudovým AI:** Vyměňte `SimpleCleaner` za transformer model z HuggingFace pro špičkovou korekci pravopisu.  
- **Doladění aocr:** Pokud máte vlastní sadu fontů, prozkoumejte `aocr.Trainer` pro zlepšení přesnosti v režimu printed.

---

To je vše — nyní máte solidní základ


## Co byste se měli naučit dál?


Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}