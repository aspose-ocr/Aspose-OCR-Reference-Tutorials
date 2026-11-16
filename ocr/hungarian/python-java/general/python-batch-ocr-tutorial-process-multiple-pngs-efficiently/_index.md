---
category: general
date: 2026-06-22
description: Python kötegelt OCR útmutató, amely megmutatja, hogyan futtathatunk több
  szálú OCR-t egy PNG képeket tartalmazó mappán a Tesseract és a pathlib használatával.
  Tanulj meg gyors kötegelt képoszlopolvasást Pythonban.
draft: false
keywords:
- python batch ocr tutorial
- multithreaded OCR in Python
- tesseract OCR batch processing
- pathlib image handling
- OCR thread count optimization
language: hu
og_description: A Python kötegelt OCR oktatóanyag végigvezet egy teljes, futtatható
  szkripten, amely több szál használatával Tesseracttal sok PNG-t dolgoz fel.
og_title: Python kötegelt OCR útmutató – Gyors többmagos OCR PNG képekhez
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  headline: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  type: TechArticle
- description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  name: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  steps:
  - name: '**Collects** every PNG with **pathlib image handling**.'
    text: '**Collects** every PNG with **pathlib image handling**.'
  - name: '**Spins up** a **multithreaded OCR in Python** worker pool.'
    text: '**Spins up** a **multithreaded OCR in Python** worker pool.'
  - name: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
    text: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
  - name: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
    text: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
  type: HowTo
tags:
- OCR
- Python
- Batch Processing
title: 'Python kötegelt OCR útmutató: Több PNG hatékony feldolgozása'
url: /hu/python-java/general/python-batch-ocr-tutorial-process-multiple-pngs-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# python batch ocr tutorial – Gyors többmagos OCR PNG képekhez

Ever wondered how to **python batch ocr tutorial** your way through hundreds of PNG screenshots without watching your CPU melt? You're not the only one. Whether you're digitizing scanned forms, extracting text from receipts, or building a searchable archive, a solid batch OCR pipeline saves you hours.

In this guide we’ll spin up a tiny yet powerful script that gathers every `*.png` in a folder, hands them off to Tesseract via a multithreaded processor, and drops the plain‑text results into a tidy output directory. No mystery libraries—just `pathlib`, `concurrent.futures`, and the ever‑reliable `pytesseract`. By the end you’ll have a **python batch ocr tutorial** you can copy‑paste into any project.

## Mit fogsz megtanulni

- How to collect image files with **pathlib image handling**  
- Setting up a **multithreaded OCR in Python** worker pool  
- Tweaking **OCR thread count optimization** for your CPU cores  
- Saving each result with a clear naming scheme for later search  
- Running the whole thing as a single, self‑contained script  

## Előfeltételek (Amire először szükséged van)

| Requirement | Why It Matters |
|-------------|----------------|
| Python 3.9+ | Modern szintaxis (`pathlib`, f‑strings) |
| Tesseract 5.x installed and accessible in `PATH` | `pytesseract` mögötti OCR motor |
| `pytesseract` (`pip install pytesseract`) | Python wrapper for Tesseract |
| `Pillow` (`pip install pillow`) | Image loading for Tesseract |
| A folder of PNG files you want to process | Our **tesseract OCR batch processing** target |

> **Pro tip:** Ha Windows-t használsz, add hozzá a `C:\Program Files\Tesseract-OCR`-t a rendszer `PATH`-jához, hogy a `pytesseract` automatikusan megtalálja a végrehajtható fájlt.

---

## 1. lépés – Minden PNG kép összegyűjtése (pathlib használatával)

First things first: we need a list of every image we plan to run OCR on. `pathlib` makes this a one‑liner and keeps the code OS‑agnostic.

```python
import pathlib

# Adjust the path to point at your source folder
source_dir = pathlib.Path("YOUR_DIRECTORY/batch_images")
image_files = list(source_dir.glob("*.png"))

print(f"Found {len(image_files)} PNG files to process.")
```

*Why `pathlib`?* It abstracts away Windows backslashes vs. Unix slashes, letting the same script run everywhere. This is the cornerstone of **pathlib image handling** in our tutorial.

---

## 2. lépés – Egyszerű Batch OCR Processzor osztály definiálása

Below is a lightweight wrapper that hides the threading boilerplate. It mirrors the pseudo‑code you saw earlier but is fully functional.

```python
import concurrent.futures
import pytesseract
from PIL import Image
import os

class BatchOcrProcessor:
    """Encapsulates multithreaded OCR logic."""

    def __init__(self):
        self.thread_count = os.cpu_count() or 4  # sensible default
        self.output_folder = pathlib.Path("ocr_results")
        self.output_folder.mkdir(parents=True, exist_ok=True)

    def set_thread_count(self, count: int):
        """Adjust the number of worker threads (OCR thread count optimization)."""
        if count < 1:
            raise ValueError("Thread count must be at least 1")
        self.thread_count = count
        print(f"Thread pool size set to {self.thread_count}")

    def set_output_folder(self, folder: str):
        """Where each OCR result will be saved (tesseract OCR batch processing)."""
        self.output_folder = pathlib.Path(folder)
        self.output_folder.mkdir(parents=True, exist_ok=True)
        print(f"Output folder set to {self.output_folder}")

    def _process_single(self, image_path: pathlib.Path):
        """Run OCR on a single image and write the text file."""
        try:
            img = Image.open(image_path)
            text = pytesseract.image_to_string(img)
            out_file = self.output_folder / f"{image_path.stem}.txt"
            out_file.write_text(text, encoding="utf-8")
            return f"✅ {image_path.name} → {out_file.name}"
        except Exception as exc:
            return f"❌ {image_path.name} failed: {exc}"

    def process(self, image_paths):
        """Run OCR on the entire batch using a thread pool."""
        print("🚀 Starting batch OCR...")
        with concurrent.futures.ThreadPoolExecutor(max_workers=self.thread_count) as executor:
            results = list(executor.map(self._process_single, image_paths))
        for line in results:
            print(line)
        print("🏁 Batch OCR completed.")
```

**A kulcsfontosságú döntések magyarázata**

- **ThreadPoolExecutor** valódi többmagos feldolgozást biztosít I/O‑központú feladatokhoz, mint a fájlok olvasása és a külső Tesseract bináris meghívása.  
- A `set_thread_count` metódusban kísérletezhetsz a **OCR thread count optimization**-nal; több szál gyakran gyorsabb áteresztőképességet jelent, amíg a CPU magjaid el nem telnek.  
- Minden kép egy `.txt` fájlt hoz létre, amely az eredeti PNG nevéből származik – tökéletes a későbbi indexeléshez vagy kereséshez.

---

## 3. lépés – Összekapcsolás

Now we instantiate the processor, tweak the thread count, point it at our output folder, and finally hand it the list of images.

```python
if __name__ == "__main__":
    # 1️⃣ Gather PNGs (already done above)
    # 2️⃣ Create processor instance
    ocr_processor = BatchOcrProcessor()

    # 3️⃣ Configure thread pool – feel free to change 8 → your core count
    ocr_processor.set_thread_count(8)   # multithreaded OCR in Python

    # 4️⃣ Choose where results land
    ocr_processor.set_output_folder("YOUR_DIRECTORY/ocr_results")

    # 5️⃣ Run the batch – this call blocks until everything is done
    ocr_processor.process(image_files)

    # 6️⃣ All done – a friendly console message
    print("✅ All images processed. Check the ocr_results folder.")
```

Running the script will produce output similar to:

```
Found 42 PNG files to process.
Thread pool size set to 8
Output folder set to YOUR_DIRECTORY/ocr_results
🚀 Starting batch OCR...
✅ invoice_001.png → invoice_001.txt
✅ receipt_2023-04-15.png → receipt_2023-04-15.txt
...
🏁 Batch OCR completed.
✅ All images processed. Check the ocr_results folder.
```

Each `.txt` contains the raw OCR output. Open any file and you’ll see the extracted text ready for indexing, sentiment analysis, or whatever comes next.

---

## 4. lépés – Gyakori hibák és hogyan kerüld el őket

| Tünet | Valószínű ok | Javítás |
|-------|--------------|---------|
| Üres `.txt` fájlok | A Tesseract nem találja a nyelvi adatokat vagy a kép túl sötét | Telepíts nyelvi csomagokat (`tesseract-ocr-eng`) és előfeldolgozd a képeket (növeld a kontrasztot). |
| `UnicodeDecodeError` a eredmények olvasásakor | A kimenet nem‑UTF‑8 karaktereket tartalmaz | Írj fájlokat `encoding="utf-8"`-vel (már a kódban) vagy használj `errors="ignore"`-t gyors megoldásként. |
| CPU csúcsok, nincs sebességnövekedés | A szálak száma meghaladja a fizikai magok számát | Csökkentsd a `set_thread_count` értékét `os.cpu_count()`-ra vagy alacsonyabbra. |
| `FileNotFoundError` kép megnyitásakor | Az útvonal nem‑ASCII karaktereket tartalmaz Windows-on | Használd a stringet `r` előtaggal vagy közvetlenül `pathlib` objektumokat (ahogy mi is). |

---

## 5. lépés – A tutorial bővítése (következő lépések)

- **Képelőfeldolgozás hozzáadása** OpenCV-vel (`cv2`) az OCR pontosság javításához (pl. kiegyenesítés, küszöbölés).  
- **Párhuzamosítás gépek között** `multiprocessing` vagy egyszerű feladatközön, mint a RabbitMQ használatával nagy terhelés esetén.  
- **Integrálás keresőmotorral** (Elasticsearch), hogy a kinyert szöveg valós időben kereshető legyen.  
- **Tesseract helyettesítése felhő OCR API-val** (Google Vision, Azure Computer Vision), ha kézírásos szövegnél nagyobb pontosságra van szükség.

All of these ideas build on the foundation you now have: a clean, **python batch ocr tutorial** that works out of the box.

---

## Összegzés

You’ve just built a complete **python batch ocr tutorial** that:

1. **Gyűjti** az összes PNG-t **pathlib image handling** segítségével.  
2. **Elindít** egy **multithreaded OCR in Python** munkavállaló pool-t.  
3. **Optimalizálja** a szálak számát a hardveredhez (**OCR thread count optimization**).  
4. **Elmenti** minden eredményt egy dedikált mappába (**tesseract OCR batch processing**).  

The script is ready to drop into any pipeline, whether you’re processing receipts, legal documents, or a mountain of screenshots. Play with the thread count, throw in image pre‑processing, or hook the output into a database—your choice.

Got questions? Feel free to comment below, and happy coding!

![Munkafolyamat-diagram a python batch ocr tutorial több PNG fájl párhuzamos feldolgozásáról](/images/python-batch-ocr-workflow.png){.center width=600 alt="python batch ocr tutorial munkafolyamata"}

---

## Mit érdemes még megtanulni?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Aspose OCR Tutorial – Optikai karakterfelismerés](/ocr/english/)
- [Hogyan batch OCR képeket listával az Aspose.OCR .NET-ben](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Képszöveg kinyerése C#-ban nyelvválasztással az Aspose.OCR használatával](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}