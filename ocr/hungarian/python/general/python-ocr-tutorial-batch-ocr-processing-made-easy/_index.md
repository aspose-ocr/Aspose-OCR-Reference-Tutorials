---
category: general
date: 2026-05-03
description: Python OCR oktató, amely bemutatja, hogyan lehet PNG képfájlokat betölteni,
  szöveget felismerni a képről, és ingyenes AI erőforrásokat használni kötegelt OCR
  feldolgozáshoz.
draft: false
keywords:
- python ocr tutorial
- batch ocr processing
- free ai resources
- load png image
- recognize text from image
language: hu
og_description: A Python OCR oktatóanyag végigvezet a PNG képek betöltésén, a képről
  történő szövegfelismerésen és az ingyenes AI erőforrások kezelésén a kötegelt OCR
  feldolgozáshoz.
og_title: Python OCR oktatóanyag – Gyors kötegelt OCR ingyenes AI erőforrásokkal
tags:
- OCR
- Python
- AI
title: Python OCR útmutató – Kötegelt OCR feldolgozás egyszerűen
url: /hu/python/general/python-ocr-tutorial-batch-ocr-processing-made-easy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR Bemutató – Kötetes OCR Feldolgozás Egyszerűen

Valaha is szükséged volt egy **python ocr tutorial**-ra, ami tényleg lehetővé teszi, hogy tucatnyi PNG fájlon futtass OCR-t anélkül, hogy a hajadba foglálkossz? Nem vagy egyedül. Sok valós projektben **load png image** fájlokat kell betölteni, egy motorba táplálni, majd a munka befejezésekor felszabadítani az AI erőforrásokat.

Ebben az útmutatóban egy komplett, azonnal futtatható példán keresztül mutatjuk be, hogyan **recognize text from image** fájlokból, hogyan dolgozzuk fel őket kötegben, és hogyan szabadítsuk fel a háttérben lévő AI memóriát. A végére egy önálló szkriptet kapsz, amelyet bármelyik projektbe beilleszthetsz – felesleges kiegészítők nélkül, csak a lényeg.

## Amit Szükséged Van

- Python 3.10 vagy újabb (a használt szintaxis f‑stringeket és típusjelöléseket igényel)  
- Egy OCR könyvtár, amely rendelkezik `engine.recognize` metódussal – a bemutatóhoz egy fiktív `aocr` csomagot feltételezünk, de helyettesítheted Tesseracttal, EasyOCR‑ral stb.  
- A kódrészletben látható `ai` segédmodul (kezeli a modell inicializálását és az erőforrások tisztítását)  
- Egy mappa tele PNG fájlokkal, amelyeket feldolgozni szeretnél  

Ha nincs `aocr` vagy `ai` telepítve, helyettesítheted őket stubokkal – lásd a „Optional Stubs” szekciót a végén.

## 1. lépés: Az AI Motor Inicializálása (Free AI Resources)

Mielőtt bármilyen képet betáplálnál az OCR csővezetékbe, a háttérben lévő modellnek készen kell állnia. Az egyszeri inicializálás memóriát takarít meg és felgyorsítja a kötegelt feladatokat.

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

**Miért fontos:**  
Ha minden képnél újra és újra meghívod az `ai.initialize`‑t, a GPU memória folyamatosan újra lefoglalódik, ami végül összeomlasztja a szkriptet. Az `ai.is_initialized()` ellenőrzésével biztosítjuk az egyszeri lefoglalást – ez a „free AI resources” elv.

## 2. lépés: PNG Képfájlok Betöltése a Kötetes OCR Feldolgozáshoz

Most összegyűjtjük az összes PNG fájlt, amelyet OCR‑en szeretnénk futtatni. A `pathlib` használata platform‑független kódot eredményez.

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

**Szélső eset:**  
Ha a mappában nem‑PNG fájlok (pl. JPEG‑ek) is vannak, azok figyelmen kívül maradnak, így az `engine.recognize` nem akad el egy nem támogatott formátumnál.

## 3. lépés: OCR Futása Minden Képen és Utófeldolgozás Alkalmazása

Miután a motor készen áll és a fájllista elkészült, végigiterálhatunk a képeken, kinyerhetjük a nyers szöveget, és átadhatjuk egy utófeldolgozónak, amely megtisztítja a gyakori OCR hibákat (például felesleges sortöréseket).

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

**Miért választjuk szét a betöltést a felismeréstől:**  
Az `aocr.Image.load` esetleg lazy dekódolást végez, ami nagy kötegek esetén gyorsabb. A betöltési lépés explicit megadása egyszerűvé teszi egy másik képkönyvtárra való átállást, ha később JPEG‑et vagy TIFF‑et kell kezelni.

## 4. lépés: Tisztítás – AI Erőforrások Felszabadítása a Köteg Után

A köteg befejezése után fel kell szabadítanunk a modellt, hogy elkerüljük a memória‑szivárgásokat, különösen GPU‑val rendelkező gépeken.

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

## Az Egész Egyben – A Teljes Szkript

Az alábbi egyetlen fájl összefűzi a négy lépést egy koherens munkafolyamatba. Mentsd `batch_ocr.py` néven, és futtasd a parancssorból.

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

### Várható Kimenet

A szkript futtatása egy három PNG‑t tartalmazó mappán például a következőt írhatja ki:

```
Engine already initialized.
Found 3 PNG image(s) to process.
Processed invoice1.png: 452 characters.
Processed receipt2.png: 317 characters.
Processed flyer3.png: 689 characters.
All results saved to /home/user/ocr_results.txt
AI resources released.
```

Az `ocr_results.txt` fájl minden képnél egy egyértelmű elválasztót és a megtisztított OCR‑szöveget tartalmazza.

## Optional Stubs aocr & ai számára (Ha Nincsenek Valódi Csomagok)

Ha csak a folyamatot szeretnéd tesztelni anélkül, hogy nehéz OCR könyvtárakat telepítenél, létrehozhatsz minimális mock modulokat:

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

Helyezd ezeket a mappákat a `batch_ocr.py` mellé, és a szkript mock eredményeket fog nyomtatni.

## Pro Tippek & Gyakori Hibák

- **Memória‑csúcsok:** Ha több ezer nagy felbontású PNG‑t dolgozol fel, fontold meg a képek átméretezését OCR előtt. Az `aocr.Image.load` gyakran elfogad egy `max_size` paramétert.  
- **Unicode kezelés:** Mindig nyisd meg a kimeneti fájlt `encoding="utf-8"`‑vel; az OCR motorok nem‑ASCII karaktereket is kiadhatnak.  
- **Párhuzamosság:** CPU‑korlátú OCR esetén a `ocr_batch`‑ot be lehet csomagolni egy `concurrent.futures.ThreadPoolExecutor`‑be. Ne feledd, hogy egyetlen `ai` példányt kell használni – ha sok szál mindegyikben meghívja az `ai.initialize`‑t, az ellentétes a „free AI resources” céllal.  
- **Hibamentesség:** Tekerj egy `try/except` blokkba a képenkénti ciklust, hogy egyetlen sérült PNG ne állítsa le az egész köteget.

## Összegzés

Most már rendelkezel egy **python ocr tutorial**‑ral, amely bemutatja, hogyan **load png image** fájlokat, hogyan végezz **batch OCR processing**‑t, és hogyan kezeld felelősen a **free AI resources**‑t. A komplett, futtatható példa pontosan megmutatja, hogyan **recognize text from image** objektumokból, majd tisztítja fel a memóriát, így egyszerűen beillesztheted saját projektjeidbe hiányzó részek keresése nélkül.

Készen állsz a következő lépésre? Próbáld ki a stub‑olt `aocr` és `ai` modulok helyettesítését valódi könyvtárakkal, például `pytesseract`‑tal és `torchvision`‑nal. Bővítheted a szkriptet JSON‑kimenettel, adatbázisba írással vagy felhő‑tároló bucketbe való integrálással. A lehetőségek végtelenek – jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}