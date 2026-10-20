---
category: general
date: 2026-05-03
description: Python OCR tutoriál, který ukazuje, jak načíst PNG soubory obrázků, rozpoznat
  text z obrázku a využít bezplatné AI zdroje pro dávkové zpracování OCR.
draft: false
keywords:
- python ocr tutorial
- batch ocr processing
- free ai resources
- load png image
- recognize text from image
language: cs
og_description: Python OCR tutoriál vás provede načítáním PNG obrázků, rozpoznáváním
  textu z obrázku a využíváním bezplatných AI zdrojů pro hromadné zpracování OCR.
og_title: Python OCR návod – Rychlý hromadný OCR s volnými AI zdroji
tags:
- OCR
- Python
- AI
title: Python OCR tutoriál – Hromadné zpracování OCR snadno
url: /cs/python/general/python-ocr-tutorial-batch-ocr-processing-made-easy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR tutoriál – Snadné zpracování OCR po dávkách

Už jste někdy potřebovali **python ocr tutorial**, který vám skutečně umožní spustit OCR na desítkách PNG souborů, aniž byste si trhali vlasy? Nejste sami. V mnoha reálných projektech musíte **load png image** soubory, předat je enginu a pak po dokončení uvolnit AI zdroje.

V tomto průvodci projdeme kompletním, připraveným příkladem, který ukazuje přesně, jak **recognize text from image** soubory, zpracovat je po dávkách a uvolnit podkladovou AI paměť. Na konci budete mít samostatný skript, který můžete vložit do libovolného projektu – žádné zbytečnosti, jen podstata.

## Co budete potřebovat

- Python 3.10 nebo novější (syntaxe zde používá f‑stringy a typové nápovědy)  
- OCR knihovnu, která poskytuje metodu `engine.recognize` – pro demonstraci předpokládáme fiktivní balíček `aocr`, ale můžete nahradit Tesseract, EasyOCR atd.  
- Modul `ai` z ukázky kódu (spravuje inicializaci modelu a úklid zdrojů)  
- Složku plnou PNG souborů, které chcete zpracovat  

Pokud nemáte nainstalované `aocr` nebo `ai`, můžete je napodobit pomocí stubů – viz sekce „Optional Stubs“ na konci.

## Krok 1: Inicializace AI enginu (Free AI Resources)

Než pošlete jakýkoli obrázek do OCR pipeline, podkladový model musí být připraven. Jednorázová inicializace šetří paměť a zrychluje dávkové úlohy.

```python
# step_1_initialize.py
import ai                # hypothetical helper that wraps the AI model
import aocr               # OCR library

def init_engine(config_path: str = "config.yaml"):
    """
    Initialize the AI engine if it hasn't been set up yet.
    This uses free AI resources – the engine will be released later.
    """
    if not ai.is_initialized():
        ai.initialize(config_path)   # auto‑initialize with the provided configuration
    else:
        print("Engine already initialized.")
```

**Proč je to důležité:**  
Volání `ai.initialize` opakovaně pro každý obrázek by alokovalo GPU paměť znovu a znovu, což nakonec skript zhavaruje. Kontrolou `ai.is_initialized()` garantujeme jedinou alokaci – to je princip „free AI resources“.

## Krok 2: Načtení PNG souborů pro dávkové OCR zpracování

Nyní shromáždíme všechny PNG soubory, které chceme spustit přes OCR. Použití `pathlib` udržuje kód nezávislý na OS.

```python
# step_2_load_images.py
from pathlib import Path
from typing import List

def collect_png_paths(directory: str) -> List[Path]:
    """
    Scan `directory` and return a list of Path objects pointing to PNG files.
    """
    base_path = Path(directory)
    if not base_path.is_dir():
        raise NotADirectoryError(f"'{directory}' is not a valid folder.")
    
    png_files = sorted(base_path.glob("*.png"))
    if not png_files:
        raise FileNotFoundError("No PNG images found in the specified directory.")
    
    print(f"Found {len(png_files)} PNG image(s) to process.")
    return png_files
```

**Hraniční případ:**  
Pokud složka obsahuje soubory, které nejsou PNG (např. JPEG), budou ignorovány, čímž zabráníme tomu, aby `engine.recognize` selhal na nepodporovaném formátu.

## Krok 3: Spuštění OCR na každém obrázku a aplikace post‑processingu

S připraveným enginem a seznamem souborů můžeme iterovat přes obrázky, získat surový text a předat ho post‑processoru, který vyčistí běžné OCR artefakty (jako jsou zbytečné zalomení řádků).

```python
# step_3_ocr_batch.py
import aocr
import ai
from pathlib import Path
from typing import List

def ocr_batch(image_paths: List[Path]) -> List[str]:
    """
    Perform OCR on each PNG image and return a list of cleaned strings.
    """
    results = []
    for image_path in image_paths:
        # Load the image – aocr.Image.load abstracts away Pillow/OpenCV details
        img = aocr.Image.load(str(image_path))
        
        # Recognize raw text
        raw_text = engine.recognize(img)
        
        # Refine the raw OCR output using the AI post‑processor
        cleaned_text = ai.run_postprocessor(raw_text)
        results.append(cleaned_text)
        
        print(f"Processed {image_path.name}: {len(cleaned_text)} characters extracted.")
    
    return results
```

**Proč oddělujeme načítání od rozpoznání:**  
`aocr.Image.load` může provádět líné dekódování, což je rychlejší pro velké dávky. Explicitní krok načítání také usnadňuje výměnu za jinou knihovnu, pokud později potřebujete zpracovávat JPEG nebo TIFF soubory.

## Krok 4: Úklid – uvolnění AI zdrojů po dokončení dávky

Po dokončení dávky musíme model uvolnit, aby nedocházelo k únikům paměti, zejména na strojích s GPU.

```python
# step_4_cleanup.py
import ai

def release_resources():
    """
    Free any allocated AI resources. Safe to call multiple times.
    """
    if ai.is_initialized():
        ai.free_resources()
        print("AI resources have been released.")
    else:
        print("No AI resources were allocated.")
```

## Spojení všeho dohromady – kompletní skript

Níže je jeden soubor, který propojí čtyři kroky do koherentního workflow. Uložte jej jako `batch_ocr.py` a spusťte z příkazové řádky.

```python
# batch_ocr.py
"""
Python OCR tutorial – end‑to‑end batch OCR processing.
Loads PNG images, runs OCR, post‑processes results, and frees AI resources.
"""

import sys
from pathlib import Path
import ai
import aocr

# ----------------------------------------------------------------------
# Helper functions (copied from the steps above)
# ----------------------------------------------------------------------
def init_engine(cfg: str = "config.yaml"):
    if not ai.is_initialized():
        ai.initialize(cfg)
    else:
        print("Engine already initialized.")

def collect_png_paths(directory: str):
    base_path = Path(directory)
    if not base_path.is_dir():
        raise NotADirectoryError(f"'{directory}' is not a valid folder.")
    png_files = sorted(base_path.glob("*.png"))
    if not png_files:
        raise FileNotFoundError("No PNG images found in the specified directory.")
    print(f"Found {len(png_files)} PNG image(s) to process.")
    return png_files

def ocr_batch(image_paths):
    results = []
    for image_path in image_paths:
        img = aocr.Image.load(str(image_path))
        raw_text = engine.recognize(img)
        cleaned_text = ai.run_postprocessor(raw_text)
        results.append(cleaned_text)
        print(f"Processed {image_path.name}: {len(cleaned_text)} characters.")
    return results

def release_resources():
    if ai.is_initialized():
        ai.free_resources()
        print("AI resources released.")
    else:
        print("No resources to release.")

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-png>")
        sys.exit(1)

    image_dir = sys.argv[1]

    try:
        init_engine()
        png_paths = collect_png_paths(image_dir)
        texts = ocr_batch(png_paths)

        # Optional: write results to a single text file
        output_file = Path("ocr_results.txt")
        with output_file.open("w", encoding="utf-8") as f:
            for path, txt in zip(png_paths, texts):
                f.write(f"--- {path.name} ---\n")
                f.write(txt + "\n\n")
        print(f"All results saved to {output_file.resolve()}")
    finally:
        release_resources()
```

### Očekávaný výstup

Spuštění skriptu nad složkou obsahující tři PNG může vypsat:

```
Engine already initialized.
Found 3 PNG image(s) to process.
Processed invoice1.png: 452 characters.
Processed receipt2.png: 317 characters.
Processed flyer3.png: 689 characters.
All results saved to /home/user/ocr_results.txt
AI resources released.
```

Soubor `ocr_results.txt` bude obsahovat jasný oddělovač pro každý obrázek následovaný vyčištěným OCR textem.

## Volitelné stuby pro aocr & ai (pokud nemáte skutečné balíčky)

Pokud chcete jen otestovat tok bez těžkých OCR knihoven, můžete vytvořit minimální mock moduly:

```python
# aocr/__init__.py
class Image:
    @staticmethod
    def load(path):
        return f"ImageObject({path})"

def dummy_recognize(image):
    return "Raw OCR output for " + str(image)

engine = type("Engine", (), {"recognize": dummy_recognize})()
```

```python
# ai/__init__.py
_state = {"initialized": False}

def is_initialized():
    return _state["initialized"]

def initialize(cfg):
    print(f"Initializing AI engine with {cfg}")
    _state["initialized"] = True

def run_postprocessor(text):
    # Very naive cleanup: strip extra spaces
    return " ".join(text.split())

def free_resources():
    print("Freeing AI resources")
    _state["initialized"] = False
```

Umístěte tyto složky vedle `batch_ocr.py` a skript poběží, vypisujíc mock výsledky.

## Pro tipy & časté úskalí

- **Špičky paměti:** Pokud zpracováváte tisíce vysokého rozlišení PNG, zvažte jejich zmenšení před OCR. `aocr.Image.load` často přijímá argument `max_size`.
- **Zpracování Unicode:** Vždy otevírejte výstupní soubor s `encoding="utf-8"`; OCR enginy mohou generovat ne‑ASCII znaky.
- **Paralelizace:** Pro CPU‑bound OCR můžete obalit `ocr_batch` do `concurrent.futures.ThreadPoolExecutor`. Jen nezapomeňte udržet jedinou instanci `ai` – spouštění mnoha vláken, které každé volají `ai.initialize`, podkopává cíl „free AI resources“.
- **Odolnost vůči chybám:** Zabalte smyčku přes obrázky do `try/except`, aby jeden poškozený PNG neukončil celou dávku.

## Závěr

Nyní máte **python ocr tutorial**, který demonstruje, jak **load png image** soubory, provést **batch OCR processing** a zodpovědně spravovat **free AI resources**. Kompletní, spustitelný příklad ukazuje přesně, jak **recognize text from image** objekty a následně úklid, takže jej můžete zkopírovat do vlastních projektů bez hledání chybějících částí.

Jste připraveni na další krok? Vyzkoušejte výměnu stubovaných modulů `aocr` a `ai` za skutečné knihovny jako `pytesseract` a `torchvision`. Můžete také rozšířit skript o výstup do JSON, odesílání výsledků do databáze nebo integraci s cloudovým úložištěm. Možnosti jsou neomezené – šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}