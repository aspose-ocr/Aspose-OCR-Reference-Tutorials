---
category: general
date: 2026-06-25
description: A kötegelt OCR feldolgozás Pythonban egyszerűen. Tanulja meg, hogyan
  lehet szöveget kinyerni képkötegekből, és sajátítsa el a kötegelt képszöveg‑kivonást
  párhuzamos szálakkal.
draft: false
keywords:
- batch OCR processing
- extract text from image batch
- batch image text extraction
language: hu
og_description: A Pythonban végzett kötegelt OCR feldolgozás lehetővé teszi, hogy
  gyorsan szöveget nyerj ki képkötegekből. Ez az útmutató végigvezet a párhuzamos
  OCR-en, világos kódrészletekkel.
og_title: Kötegelt OCR feldolgozás Pythonban – Teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Batch OCR processing in Python made easy. Learn how to extract text
    from image batch and master batch image text extraction with parallel threads.
  headline: Batch OCR Processing in Python – Complete Programming Guide
  type: TechArticle
- description: Batch OCR processing in Python made easy. Learn how to extract text
    from image batch and master batch image text extraction with parallel threads.
  name: Batch OCR Processing in Python – Complete Programming Guide
  steps:
  - name: Missing or Corrupt Images
    text: If an image can’t be opened, most OCR libraries raise an exception that
      aborts the whole batch. Wrap the call in a `try/except` inside the batch function
      or filter out problematic files beforehand (see the sanity check in Step 1).
  - name: Language & DPI Settings
    text: For multilingual documents, pass a `langs` parameter (e.g., `langs=['en',
      'de']`). If your scans are low‑resolution, consider pre‑processing with `Pillow`
      to upscale to 300 DPI before OCR—this often boosts accuracy.
  - name: Memory Constraints
    text: 'Eight threads can eat RAM, especially with large images. If you hit memory
      errors, lower `max_threads` or process the list in smaller chunks:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Kötegelt OCR feldolgozás Pythonban – Teljes programozási útmutató
url: /hu/python-java/general/batch-ocr-processing-in-python-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kötegelt OCR feldolgozás Pythonban – Teljes programozási útmutató

Valaha szükséged volt **kötegelt OCR feldolgozásra**, de nem tudtad, hogyan futtathatod hatékonyan tucatnyi beolvasott oldalon? Nem vagy egyedül – a fejlesztők gyakran akadnak el, amikor megpróbálnak szöveget kinyerni egy képkötegből anélkül, hogy leterhelnék a CPU-t.  

Ebben az útmutatóban bemutatunk egy egyszerű módszert a **szöveg kinyerésére képkötegből** a Python OCR motorjával, legfeljebb nyolc szálon futtatva a feladatot, és végül megmutatjuk, hány karaktert adott hozzá minden egyes kép. A végére egy újrahasználható szkriptet kapsz, amely **kötegelt képek szövegkivonását** profi módon kezeli.

## Amit ez az oktatóanyag lefed

Áttekintünk három gyakorlati lépést:

1. Készíts egy listát a felismertetni kívánt képfájlokról.  
2. Indítsd el az OCR motort párhuzamosan a `max_threads=8` beállítással.  
3. Járd végig az eredményeket, és nyomtass ki egy tömör összefoglalót.

Nincs külső szolgáltatás, nincs rejtélyes könyvtár – csak tiszta Python és egy tipikus OCR wrapper (például az `ocr` a `easyocr`‑ból vagy egy egyedi wrapper). Ha van Python 3.8+ és telepített OCR csomagod, már készen állsz a másolás‑beillesztésre és a futtatásra.

---

## 1. lépés: Készíts listát a képfájlokról a kötegelt OCR feldolgozáshoz

Az első dolog, amire szükséged van, egy gyűjtemény a képek elérési útjairól. Gondolj rá úgy, mint egy bevásárlólistára az OCR motor számára; minden bejegyzés egy PNG, JPEG vagy TIFF fájlra mutat, amely a kívánt szöveget tartalmazza.

```python
# Step 1: Prepare a list of image files to be recognized
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png",
    "YOUR_DIRECTORY/page4.png",
    "YOUR_DIRECTORY/page5.png"
]

# Quick sanity check – make sure the files exist
import os
missing = [p for p in image_files if not os.path.isfile(p)]
if missing:
    raise FileNotFoundError(f"These files are missing: {missing}")
```

**Miért fontos ez:**  
A lista előre elkészítése lehetővé teszi, hogy az OCR motor valódi kötegelt módban dolgozzon. Emellett egy központi helyet biztosít a fájlok hozzáadásához vagy eltávolításához anélkül, hogy később módosítanod kellene a feldolgozási logikát. A szanitás‑ellenőrzés megakadályozza a „fájl nem található” hibát egy hosszú futás közepén.

---

## 2. lépés: Futtasd az OCR‑t a kötegen párhuzamos szálakkal (Extract Text from Image Batch)

Most átadjuk a listát az OCR motorának. A legtöbb modern OCR wrapper rendelkezik egy `recognize_batch` metódussal, amely elfogad egy `max_threads` argumentumot. Ha ezt `8`‑ra állítod, a könyvtár nyolc munkaszálat indít, ami egy hyper‑threading‑kel rendelkező négymagos CPU‑n jelentősen lerövidítheti a feldolgozási időt.

```python
# Step 2: Run OCR on the batch, allowing up to 8 parallel threads
# Assuming `ocr` is a module that provides OcrEngine with recognize_batch()
import ocr

batch_results = ocr.OcrEngine.recognize_batch(image_files, max_threads=8)

# batch_results is a list of Result objects, each with a .text attribute
```

**Miért segít a párhuzamosság:**  
Az OCR CPU‑igényes; minden képet egy neurális hálózat vagy egy régi motor dolgoz fel. Egymás után futtatni őket fájdalmasan lassú lehet, különösen nagy felbontású beolvasások esetén. A párhuzamos szálak minden magot foglalkoztatnak, így egy 5 perces feladatot 1 percre csökkenthetnek tipikus hardveren.

**Tipp:** Ha az `easyocr`‑t használod, a hívás így néz ki: `reader.readtext(image_path, detail=0)` egy ciklusban. A mi `recognize_batch` absztrakciónk elrejti ezt a komplexitást, de bármikor helyettesítheted saját `ThreadPoolExecutor`‑eddel, ha a könyvtár nem támogat kötegelt módot.

---

## 3. lépés: Járd végig az eredményeket és összegzd a kötegelt képek szövegkivonását

Miután az OCR befejeződött, egy listád lesz az eredményobjektumokról. Párosítsuk össze az eredeti fájlutakat a megfelelő OCR kimenettel, és nyomtassunk egy szép sort minden képhez, amely megmutatja, hány karaktert sikerült felismerni.

```python
# Step 3: Iterate through the results and display character counts
for file_path, result in zip(image_files, batch_results):
    # result.text holds the raw extracted string
    char_count = len(result.text)
    print(f"{file_path} → {char_count} characters recognized")
```

**Ami megjelenik majd:**  

```
YOUR_DIRECTORY/page1.png → 1245 characters recognized
YOUR_DIRECTORY/page2.png → 987 characters recognized
YOUR_DIRECTORY/page3.png → 1103 characters recognized
YOUR_DIRECTORY/page4.png → 1320 characters recognized
YOUR_DIRECTORY/page5.png → 845 characters recognized
```

**Miért hasznos ez a lépés:**  
Egy gyors karakter-számlálás első pillantásra megmutatja, hogy egy kép helyesen lett‑e feldolgozva. Egy váratlanul alacsony szám homályos beolvasásra, rossz nyelvi beállításra vagy sérült fájlra utalhat – olyan problémákra, amelyeket a további elemzés előtt még orvosolhatsz.

---

## Bónusz: Szélsebes esetek és gyakori buktatók kezelése

### Hiányzó vagy sérült képek  
Ha egy képet nem lehet megnyitni, a legtöbb OCR könyvtár kivételt dob, ami leállítja az egész köteget. Csomagold be a hívást egy `try/except` blokkba a köteg‑függvényen belül, vagy előre szűrd ki a problémás fájlokat (lásd az 1. lépés szanitás‑ellenőrzését).

### Nyelv‑ és DPI‑beállítások  
Többnyelvű dokumentumok esetén add meg a `langs` paramétert (pl. `langs=['en', 'de']`). Ha a beolvasások alacsony felbontásúak, fontold meg a `Pillow`‑val való előfeldolgozást, hogy 300 DPI‑ra felméretezd őket – ez gyakran növeli a pontosságot.

### Memória‑korlátok  
Nyolc szál jelentős RAM‑használatot igényelhet, különösen nagy képek esetén. Ha memóriahibát kapsz, csökkentsd a `max_threads` értékét, vagy dolgozd fel a listát kisebb darabokban:

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(image_files, 3):  # process three images at a time
    results = ocr.OcrEngine.recognize_batch(chunk, max_threads=3)
    # handle results...
```

---

## Teljes működő szkript

Mindent összevonva, itt egy komplett, azonnal futtatható példa. Cseréld le a `"YOUR_DIRECTORY"`‑t arra az útra, ahol a PNG fájljaid vannak, és győződj meg róla, hogy az `ocr` modul telepítve van.

```python
#!/usr/bin/env python3
"""
Batch OCR Processing Script
Extracts text from an image batch using parallel threads and prints character counts.
"""

import os
import ocr  # Replace with your OCR library import, e.g., from easyocr import Reader

# -------------------------------------------------
# Step 1: Define the list of image files
# -------------------------------------------------
image_dir = "YOUR_DIRECTORY"
image_files = [
    os.path.join(image_dir, f"page{i}.png") for i in range(1, 6)
]

# Verify that all files exist
missing = [p for p in image_files if not os.path.isfile(p)]
if missing:
    raise FileNotFoundError(f"Missing image files: {missing}")

# -------------------------------------------------
# Step 2: Run OCR in parallel (max 8 threads)
# -------------------------------------------------
# The OcrEngine is a placeholder – adapt to your library's API
batch_results = ocr.OcrEngine.recognize_batch(image_files, max_threads=8)

# -------------------------------------------------
# Step 3: Report how many characters each image yielded
# -------------------------------------------------
for file_path, result in zip(image_files, batch_results):
    char_count = len(result.text)
    print(f"{file_path} → {char_count} characters recognized")
```

**Várható kimenet** (a számaid ettől eltérnek majd):

```
YOUR_DIRECTORY/page1.png → 1245 characters recognized
YOUR_DIRECTORY/page2.png → 987 characters recognized
YOUR_DIRECTORY/page3.png → 1103 characters recognized
YOUR_DIRECTORY/page4.png → 1320 characters recognized
YOUR_DIRECTORY/page5.png → 845 characters recognized
```

Futtasd a szkriptet a `python batch_ocr.py` paranccsal, és figyeld, ahogy a terminál tömör statisztikákkal töltődik fel.

---

## Vizuális áttekintés

![Kötegelt OCR feldolgozási folyamatábra](image-placeholder.png "Ábra, amely bemutatja a kötegelt OCR feldolgozási lépéseket")

*Image alt text:* *Kötegelt OCR feldolgozási folyamatábra, amely a fájllista létrehozását, a párhuzamos OCR végrehajtást és az eredmények összegzését mutatja.*

---

## Összegzés

Most már van egy szilárd alapod a **kötegelt OCR feldolgozáshoz** Pythonban. Egy tiszta képlista előkészítésével, a **szöveg kinyerése képkötegből** párhuzamos szálakkal, és az eredmények összegzésével egy unalmas, manuális feladatot gyors, újrahasználható pipeline‑ná alakíthatsz.  

Innen tovább:

- Mentsd el minden `result.text`‑et egy `.txt` fájlba a további NLP‑hez.  
- Kombináld a karakter‑számokat a biztonsági pontszámokkal, hogy kiszűrd a gyenge minőségű oldalakat.  
- Integráld a szkriptet egy nagyobb dokumentum‑befogadó munkafolyamatba, például egy keresőindex feltöltéséhez.

Akár archívumokat digitalizálsz, számlabeolvasó alkalmazást építesz, vagy nyelvi modellhez készítesz tréning adatot, az itt bemutatott koncepciók könnyedén skálázhatók több száz vagy ezer fájlra is minimális módosítással.

Van kérdésed a nyelvi beállításokkal, a képek előfeldolgozásával vagy a felhőben való telepítéssel kapcsolatban? Hagyj megjegyzést, vagy nézd meg a kapcsolódó oktatóanyagokat a *Python képek előfeldolgozása* és az *aszinkron OCR asyncio‑val* témakörökben. Boldog kódolást!

## Mit érdemes legközelebb megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy könnyedén elsajátíthasd a további API‑funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Szöveg kinyerése képből Aspose OCR-rel – Lépésről‑lépésre útmutató](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Hogyan kötegeld az OCR képeket listával az Aspose.OCR .NET-ben](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Szöveg kinyerése képből – OCR optimalizálás Aspose.OCR .NET-ben](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}