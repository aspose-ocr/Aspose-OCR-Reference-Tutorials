---
category: general
date: 2026-05-03
description: Samouczek OCR w Pythonie, który pokazuje, jak wczytywać pliki PNG, rozpoznawać
  tekst z obrazu oraz darmowe zasoby AI do przetwarzania OCR wsadowego.
draft: false
keywords:
- python ocr tutorial
- batch ocr processing
- free ai resources
- load png image
- recognize text from image
language: pl
og_description: Samouczek OCR w Pythonie prowadzi Cię przez ładowanie obrazów PNG,
  rozpoznawanie tekstu z obrazu oraz korzystanie z darmowych zasobów AI do przetwarzania
  OCR wsadowego.
og_title: Samouczek OCR w Pythonie – Szybkie przetwarzanie wsadowe OCR z darmowymi
  zasobami AI
tags:
- OCR
- Python
- AI
title: Samouczek OCR w Pythonie – Łatwe przetwarzanie OCR wsadowego
url: /pl/python/general/python-ocr-tutorial-batch-ocr-processing-made-easy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR Tutorial – Batch OCR Processing Made Easy

Kiedykolwiek potrzebowałeś **python ocr tutorial**, który naprawdę pozwala uruchomić OCR na dziesiątkach plików PNG bez wyrywania włosów? Nie jesteś sam. W wielu rzeczywistych projektach musisz **load png image** pliki, przekazać je do silnika, a potem posprzątać zasoby AI, gdy skończysz.  

W tym przewodniku przejdziemy krok po kroku przez kompletny, gotowy do uruchomienia przykład, który pokazuje dokładnie, jak **recognize text from image** plików, przetwarzać je wsadowo i zwolnić pamięć AI. Na koniec będziesz mieć samodzielny skrypt, który możesz wrzucić do dowolnego projektu — bez dodatkowego balastu, tylko najważniejsze elementy.

## What You’ll Need

- Python 3.10 lub nowszy (użyta tutaj składnia opiera się na f‑strings i type hints)  
- Biblioteka OCR, która udostępnia metodę `engine.recognize` – w celach demonstracyjnych przyjmiemy fikcyjny pakiet `aocr`, ale możesz podmienić go na Tesseract, EasyOCR itp.  
- Moduł pomocniczy `ai` pokazany w fragmencie kodu (obsługuje inicjalizację modelu i czyszczenie zasobów)  
- Folder pełen plików PNG, które chcesz przetworzyć  

Jeśli nie masz zainstalowanego `aocr` lub `ai`, możesz je zasymulować przy pomocy stubów – zobacz sekcję „Optional Stubs” pod koniec.

## Step 1: Initialize the AI Engine (Free AI Resources)

Zanim przekażesz jakikolwiek obraz do potoku OCR, podkładowy model musi być gotowy. Inicjalizacja tylko raz oszczędza pamięć i przyspiesza zadania wsadowe.

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
Wywoływanie `ai.initialize` wielokrotnie dla każdego obrazu przydzielałoby pamięć GPU za każdym razem, co w końcu doprowadziłoby do awarii skryptu. Sprawdzając `ai.is_initialized()` zapewniamy jednorazową alokację – to zasada „free AI resources”.

## Step 2: Load PNG Image Files for Batch OCR Processing

Teraz zbieramy wszystkie pliki PNG, które chcemy poddać OCR. Użycie `pathlib` utrzymuje kod niezależny od systemu operacyjnego.

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
Jeśli folder zawiera pliki nie‑PNG (np. JPEG), zostaną one zignorowane, co zapobiega „zadławieniu” `engine.recognize` nieobsługiwanym formatem.

## Step 3: Run OCR on Each Image and Apply Post‑Processing

Gdy silnik jest gotowy, a lista plików przygotowana, możemy przejść po obrazach, wyodrębnić surowy tekst i przekazać go do post‑procesora, który usuwa typowe artefakty OCR (np. niechciane podziały linii).

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
`aocr.Image.load` może wykonywać leniwe dekodowanie, co jest szybsze przy dużych partiach. Utrzymanie kroku ładowania jako osobnego etapu ułatwia także podmianę biblioteki obrazu, jeśli później będziesz potrzebował obsługiwać JPEG lub TIFF.

## Step 4: Clean Up – Free AI Resources After the Batch

Po zakończeniu przetwarzania wsadowego musimy zwolnić model, aby uniknąć wycieków pamięci, szczególnie na maszynach z GPU.

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

Poniżej znajduje się pojedynczy plik, który łączy cztery kroki w spójny przepływ pracy. Zapisz go jako `batch_ocr.py` i uruchom z wiersza poleceń.

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

Uruchomienie skryptu w folderze zawierającym trzy pliki PNG może wypisać:

```
Engine already initialized.
Found 3 PNG image(s) to process.
Processed invoice1.png: 452 characters.
Processed receipt2.png: 317 characters.
Processed flyer3.png: 689 characters.
All results saved to /home/user/ocr_results.txt
AI resources released.
```

Plik `ocr_results.txt` będzie zawierał wyraźny separator dla każdego obrazu, po którym nastąpi wyczyszczony tekst OCR.

## Optional Stubs for aocr & ai (If You Don’t Have Real Packages)

Jeśli chcesz po prostu przetestować przepływ bez wciągania ciężkich bibliotek OCR, możesz stworzyć minimalne moduły mock:

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

Umieść te foldery obok `batch_ocr.py`, a skrypt uruchomi się, wypisując wyniki mock.

## Pro Tips & Common Pitfalls

- **Memory spikes:** Jeśli przetwarzasz tysiące wysokiej rozdzielczości PNG, rozważ ich zmniejszenie przed OCR. `aocr.Image.load` często przyjmuje argument `max_size`.
- **Unicode handling:** Zawsze otwieraj plik wyjściowy z `encoding="utf-8"`; silniki OCR mogą emitować znaki spoza ASCII.
- **Parallelism:** Dla OCR obciążającego CPU możesz opakować `ocr_batch` w `concurrent.futures.ThreadPoolExecutor`. Pamiętaj tylko, aby utrzymać jedną instancję `ai` – uruchamianie wielu wątków, które każdy wywołuje `ai.initialize`, podważa cel „free AI resources”.
- **Error resilience:** Owiń pętlę przetwarzającą poszczególne obrazy w blok `try/except`, aby pojedynczy uszkodzony PNG nie przerwał całego wsadu.

## Conclusion

Masz teraz **python ocr tutorial**, który pokazuje, jak **load png image** pliki, wykonać **batch OCR processing** i odpowiedzialnie zarządzać **free AI resources**. Kompletny, uruchamialny przykład pokazuje dokładnie, jak **recognize text from image** obiektów i posprzątać po sobie, więc możesz go skopiować‑wkleić do własnych projektów bez poszukiwania brakujących elementów.

Gotowy na kolejny krok? Spróbuj podmienić stubowane moduły `aocr` i `ai` na prawdziwe biblioteki, takie jak `pytesseract` i `torchvision`. Możesz także rozbudować skrypt o wyjście w formacie JSON, wysyłanie wyników do bazy danych lub integrację z chmurowym bucketem. Nie ma granic — miłego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}