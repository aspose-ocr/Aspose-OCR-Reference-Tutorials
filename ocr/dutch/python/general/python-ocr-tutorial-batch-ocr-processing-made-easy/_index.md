---
category: general
date: 2026-05-03
description: Python OCR-tutorial die laat zien hoe je PNG‑afbeeldingsbestanden laadt,
  tekst uit een afbeelding herkent en gratis AI‑bronnen voor batch‑OCR‑verwerking
  biedt.
draft: false
keywords:
- python ocr tutorial
- batch ocr processing
- free ai resources
- load png image
- recognize text from image
language: nl
og_description: Python OCR‑tutorial leidt je door het laden van PNG‑afbeeldingen,
  het herkennen van tekst uit een afbeelding en het omgaan met gratis AI‑bronnen voor
  batch‑OCR‑verwerking.
og_title: Python OCR-tutorial – Snelle batch-OCR met gratis AI-bronnen
tags:
- OCR
- Python
- AI
title: Python OCR-tutorial – Batch-OCR-verwerking eenvoudig gemaakt
url: /nl/python/general/python-ocr-tutorial-batch-ocr-processing-made-easy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR Tutorial – Batch OCR Processing Made Easy

Heb je ooit een **python ocr tutorial** nodig gehad die je echt in staat stelt om OCR uit te voeren op tientallen PNG‑bestanden zonder je haar uit te trekken? Je bent niet de enige. In veel real‑world projecten moet je **load png image**‑bestanden laden, ze aan een engine voeren, en daarna de AI‑bronnen opruimen wanneer je klaar bent.  

In deze gids lopen we stap voor stap door een compleet, kant‑klaar voorbeeld dat precies laat zien hoe je **recognize text from image**‑bestanden herkent, ze in batch verwerkt, en het onderliggende AI‑geheugen vrijmaakt. Aan het einde heb je een zelfstandige script die je in elk project kunt plaatsen — geen extra poespas, alleen de essentie.

## What You’ll Need

- Python 3.10 of nieuwer (de gebruikte syntax maakt gebruik van f‑strings en type hints)  
- Een OCR‑bibliotheek die een `engine.recognize`‑methode exposeert – voor demonstratiedoeleinden gaan we uit van een fictief `aocr`‑pakket, maar je kunt Tesseract, EasyOCR, enz. gebruiken  
- De `ai`‑helpermodule die in het code‑fragment wordt getoond (deze verzorgt modelinitialisatie en resource‑cleanup)  
- Een map vol PNG‑bestanden die je wilt verwerken  

Als je `aocr` of `ai` niet geïnstalleerd hebt, kun je ze nabootsen met stubs – zie de sectie “Optional Stubs” onderaan.

## Step 1: Initialize the AI Engine (Free AI Resources)

Voordat je een afbeelding in de OCR‑pipeline stopt, moet het onderliggende model klaar zijn. Eénmalig initialiseren bespaart geheugen en versnelt batch‑taken.

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

**Why this matters:**  
Het herhaaldelijk aanroepen van `ai.initialize` voor elke afbeelding zou steeds GPU‑geheugen toewijzen, wat uiteindelijk het script laat crashen. Door `ai.is_initialized()` te controleren garanderen we één enkele allocatie – dat is het “free AI resources”‑principe.

## Step 2: Load PNG Image Files for Batch OCR Processing

Nu verzamelen we alle PNG‑bestanden die we door OCR willen laten gaan. Met `pathlib` blijft de code OS‑agnostisch.

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

**Edge case:**  
Als de map niet‑PNG‑bestanden bevat (bijv. JPEG’s) worden die genegeerd, zodat `engine.recognize` niet vastloopt op een niet‑ondersteund formaat.

## Step 3: Run OCR on Each Image and Apply Post‑Processing

Met de engine klaar en de bestandenlijst voorbereid, kunnen we over de afbeeldingen itereren, ruwe tekst extraheren, en deze door een post‑processor laten gaan die veelvoorkomende OCR‑artefacten (zoals vreemde regeleinden) opruimt.

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

**Why we separate loading from recognition:**  
`aocr.Image.load` kan lazy decoding uitvoeren, wat sneller is voor grote batches. Het expliciet houden van de laadstap maakt het bovendien eenvoudig om een andere afbeeldingsbibliotheek te gebruiken als je later JPEG‑ of TIFF‑bestanden moet verwerken.

## Step 4: Clean Up – Free AI Resources After the Batch

Zodra de batch klaar is, moeten we het model vrijgeven om geheugenlekken te voorkomen, vooral op GPU‑machines.

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

## Putting It All Together – The Complete Script

Hieronder vind je één enkel bestand dat de vier stappen samenvoegt tot een samenhangende workflow. Sla het op als `batch_ocr.py` en voer het uit vanaf de commandoregel.

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

### Expected Output

Het uitvoeren van het script tegen een map met drie PNG‑bestanden kan bijvoorbeeld het volgende afdrukken:

```
Engine already initialized.
Found 3 PNG image(s) to process.
Processed invoice1.png: 452 characters.
Processed receipt2.png: 317 characters.
Processed flyer3.png: 689 characters.
All results saved to /home/user/ocr_results.txt
AI resources released.
```

Het bestand `ocr_results.txt` zal een duidelijke scheiding bevatten voor elke afbeelding, gevolgd door de opgeschoonde OCR‑tekst.

## Optional Stubs for aocr & ai (If You Don’t Have Real Packages)

Als je alleen de flow wilt testen zonder zware OCR‑bibliotheken te gebruiken, kun je minimale mock‑modules maken:

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

Plaats deze mappen naast `batch_ocr.py` en het script zal draaien, waarbij mock‑resultaten worden afgedrukt.

## Pro Tips & Common Pitfalls

- **Memory spikes:** Als je duizenden hoge‑resolutie PNG‑s verwerkt, overweeg dan om ze vóór OCR te verkleinen. `aocr.Image.load` accepteert vaak een `max_size`‑argument.  
- **Unicode handling:** Open altijd het output‑bestand met `encoding="utf-8"`; OCR‑engines kunnen niet‑ASCII‑tekens produceren.  
- **Parallelism:** Voor CPU‑gebonden OCR kun je `ocr_batch` wikkelen in een `concurrent.futures.ThreadPoolExecutor`. Zorg er wel voor dat er slechts één `ai`‑instantie bestaat – het spawnen van veel threads die elk `ai.initialize` aanroepen ondermijnt het “free AI resources”‑doel.  
- **Error resilience:** Plaats de per‑afbeelding‑lus in een `try/except`‑blok zodat één corrupte PNG niet de hele batch stopt.

## Conclusion

Je hebt nu een **python ocr tutorial** die laat zien hoe je **load png image**‑bestanden verwerkt, **batch OCR processing** uitvoert, en verantwoord **free AI resources** beheert. Het complete, uitvoerbare voorbeeld toont precies hoe je **recognize text from image**‑objecten herkent en daarna opruimt, zodat je het kunt kopiëren‑plakken in je eigen projecten zonder te zoeken naar ontbrekende onderdelen.

Klaar voor de volgende stap? Probeer de gestubde `aocr`‑ en `ai`‑modules te vervangen door echte bibliotheken zoals `pytesseract` en `torchvision`. Je kunt het script ook uitbreiden om JSON uit te voeren, resultaten naar een database te pushen, of te integreren met een cloud‑storage bucket. De mogelijkheden zijn eindeloos — happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}