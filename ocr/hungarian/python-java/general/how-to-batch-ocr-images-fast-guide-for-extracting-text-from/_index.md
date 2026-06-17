---
category: general
date: 2026-01-12
description: Hogyan végezzünk gyors kötegelt OCR-t képeken, és nyerjünk ki szöveget
  JPEG fájlokból Pythonban. Tanulja meg lépésről‑lépésre a kötegelt feldolgozást egy
  teljesen futtatható példával.
draft: false
keywords:
- how to batch OCR images
- extract text from JPEG files
language: hu
og_description: Hogyan végezzünk kötegelt OCR-t képeken, és nyerjünk ki szöveget JPEG
  fájlokból. Ez az útmutató végigvezet egy teljes, azonnal futtatható Python megoldáson.
og_title: Hogyan végezzünk kötegelt OCR-t képeken – Gyors Python bemutató
tags:
- OCR
- Python
- image processing
title: Képek tömeges OCR-olása – Gyors útmutató a JPEG-fájlok szövegének kinyeréséhez
url: /hu/python-java/general/how-to-batch-ocr-images-fast-guide-for-extracting-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk kötegelt OCR-t képeken – Gyors útmutató a JPEG fájlokból szöveg kinyeréséhez

Gondolkodtál már azon, **hogyan végezzünk kötegelt OCR-t képeken** anélkül, hogy minden fájlhoz külön szkriptet írnál? Nem vagy egyedül. Sok projektben – számlák beolvasása, archívum digitalizálása vagy tartalommoderálás – egyszerre tucatnyi vagy akár több száz JPEG fájlból kell szöveget kinyerni. A jó hír, hogy mindezt néhány Python sorral megteheted, és kapsz egy újrahasználható motort, amelyet bármely folyamatba beilleszthetsz.

Ebben az útmutatóban pontosan megmutatjuk, **hogyan végezzünk kötegelt OCR-t képeken**, majd végigvezetünk a JPEG fájlokból történő szövegkivonáson, a szélsőséges esetek kezelésén és a kimenet ellenőrzésén. A végére egy önálló szkriptet kapsz, amelyet bármely képmappán futtathatsz, és megérted, miért fontos a kötegelt feldolgozás a teljesítmény és a karbantarthatóság szempontjából.

## Amit megtanulsz

- Egy egyszerű OCR motor beállítása és angol nyelvre konfigurálása.
- Az összes JPEG fájl összegyűjtése egy könyvtárból a `pathlib` segítségével.
- Az OCR motor egyszeri meghívása a teljes köteg feldolgozásához.
- A felismert szöveg előnézetének megjelenítése minden egyes képhez.
- Tippek nagy kötegek, különböző nyelvek és gyakori buktatók kezeléséhez.

**Előfeltételek**: Python 3.8+, az `ocr` könyvtár (vagy bármely kompatibilis wrapper), valamint egy JPEG képeket tartalmazó mappa, amelyet elemezni szeretnél. Külső szolgáltatások nem szükségesek – minden helyben fut.

---

## 1. lépés: Az OCR motor inicializálása – A „Hogyan végezzünk kötegelt OCR-t képeken” magja

Mielőtt **kötegelt OCR-t képeken** tudnánk végezni, szükségünk van egy motorra, amely tudja olvasni a szöveget. A legtöbb könyvtárban létrehozunk egy motorobjektumot, opcionálisan beállítjuk a nyelvet, majd minden fájlhoz újra felhasználjuk.

```python
import ocr
import pathlib

# Create the OCR engine and set it to English (the most common case)
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

*Miért fontos*: A motor egyszeri inicializálása elkerüli a nyelvi modellek többszöri betöltésének terheit. Emellett egyetlen helyen módosíthatod a beállításokat (pl. DPI, karakterfehérlista), amelyek a teljes kötegben érvényesek lesznek.

> **Pro tipp**: Ha többnyelvű dokumentumokat szeretnél feldolgozni, cseréld a `ocr.Language.ENGLISH` értéket `ocr.Language.MULTI`‑ra, vagy tölts be több nyelvi csomagot a köteg indítása előtt.

---

## 2. lépés: Az összes JPEG fájl összegyűjtése – A „Szöveg kinyerése JPEG fájlokból” rész

Most, hogy a motor készen áll, meg kell mondanunk, mely képeken dolgozzon. A `pathlib` használata platform‑függetlenné és tömöré teszi a kódot.

```python
# Replace YOUR_DIRECTORY with the path that holds your JPEG files
image_dir = pathlib.Path("YOUR_DIRECTORY/")
image_paths = list(image_dir.glob("*.jpg"))  # only JPEG files, case‑sensitive
```

*Miért fontos*: A fájllista előzetes összegyűjtésével egyetlen hívással átadhatjuk a teljes gyűjteményt az OCR motorának – pont ez a **hogyan végezzünk kötegelt OCR-t képeken** lényege. Ha almappákat is tartalmaz a struktúra, a `glob("**/*.jpg")` kifejezést módosíthatod rekurzív keresésre.

> **Szélsőséges eset**: Ha a képek vegyes kiterjesztésekkel (`.jpeg`, `.JPG`) rendelkeznek, bővítsd a glob mintát: `image_dir.rglob("*.[jJ][pP][eE]?g")`.

---

## 3. lépés: A teljes köteg feldolgozása egy hívással – A kötegelt OCR valódi ereje

A legtöbb modern OCR könyvtár biztosít egy `process_batch` (vagy hasonló nevű) metódust, amely egy iterálható fájlútvonal-listát fogad. Ez a **hogyan végezzünk kötegelt OCR-t képeken** hatékony megvalósításának szíve.

```python
# Process every JPEG file in a single batch operation
ocr_results = ocr_engine.process_batch(image_paths)
```

*Miért fontos*: Egyetlen köteg hívás csökkenti a Python‑‑C átmenetek számát, a nyelvi modellt memóriában tartja, és gyakran lehetővé teszi a belső párhuzamosítást. Az eredmény egy objektumlista – mindegyik tartalmazza a felismert szöveget és a megbízhatósági pontszámokat.

> **Teljesítményjegyzet**: Nagyon nagy kötegek (ezrek képek) esetén érdemes a listát kisebb darabokra (pl. 200 fájl) bontani, hogy elkerüld a túlzott memóriahasználatot.

---

## 4. lépés: A kinyert szöveg előnézetének megjelenítése – Gyors ellenőrzés

Miután a köteg befejeződött, hasznos megnézni az egyes eredmények első néhány karakterét. Ez segít megerősíteni, hogy az OCR valóban szöveget nyert ki a JPEG fájlokból.

```python
for image_path, ocr_result in zip(image_paths, ocr_results):
    # Show the image name and the first 100 characters of its recognised text
    preview = ocr_result.text[:100].replace("\n", " ").strip()
    print(f"{image_path.name}: {preview}...")
```

*Miért fontos*: Egy rövid előnézet lehetővé teszi, hogy azonnal észrevegyél nyilvánvaló hibákat (pl. üres kimenet, torz karakterek) anélkül, hogy minden fájlt megnyitnál. Ha rendszeres problémákat látsz, módosíthatod a motor beállításait és újra futtathatod a köteget.

> **Gyakori buktató**: Elfelejteni a sortörés karakterek eltávolítását rendezetlen előnézetet eredményezhet. A `replace("\n", " ")` sor ezt megtisztítja.

---

## Teljes működő példa – Az összes lépés egyben

Az alábbiakban a teljes szkriptet találod, amelyet egyszerűen másolj‑be, állítsd be a könyvtár útvonalát, és futtasd. Bemutatja a **hogyan végezzünk kötegelt OCR-t képeken** teljes munkafolyamatát az elejétől a végéig.

```python
import ocr
import pathlib

def batch_ocr_jpeg(folder: str):
    """
    Process all JPEG files in `folder` and print a 100‑character preview
    of the recognised text for each image.
    """
    # Step 1 – Initialise OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – Gather JPEG paths
    img_dir = pathlib.Path(folder)
    jpeg_paths = list(img_dir.glob("*.jpg"))  # add more patterns if needed

    if not jpeg_paths:
        print("No JPEG files found in the specified directory.")
        return

    # Step 3 – Batch process
    results = engine.process_batch(jpeg_paths)

    # Step 4 – Display previews
    for path, res in zip(jpeg_paths, results):
        preview = res.text[:100].replace("\n", " ").strip()
        print(f"{path.name}: {preview}...")

if __name__ == "__main__":
    # Replace with the path containing your JPEG images
    batch_ocr_jpeg("YOUR_DIRECTORY/")
```

**Várt kimenet** (példa):

```
invoice_001.jpg: Invoice #001  Date: 2024-03-15  Total: $1,245.00  Bill To: Acme Corp...
receipt_202.jpg: Receipt 202  Store: QuickMart  Total: $45.67  Date: 03/12/2024...
...
```

Ha az előnézet értelmes szöveget mutat, sikeresen **kinyerted a szöveget a JPEG fájlokból** egy kötegelt megközelítéssel.

---

## Nagy kötegek és haladó forgatókönyvek kezelése

### Nagy munkaterhek darabolása
Ezrek képek esetén a memória szűk keresztmetszet lehet. Oszd a listát kisebb darabokra:

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(jpeg_paths, 200):  # 200 files per batch
    results = engine.process_batch(chunk)
    # process results as shown earlier
```

### Nyelvek váltása
Ha a dokumentumaid francia vagy spanyol nyelvűek, a köteg előtt változtasd meg a nyelvet:

```python
engine.language = ocr.Language.FRENCH  # or ocr.Language.SPANISH
```

### Eredmények mentése lemezre
A kiírás helyett érdemes lehet minden OCR eredményt egy `.txt` fájlba írni:

```python
output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for path, res in zip(jpeg_paths, results):
    txt_path = output_dir / f"{path.stem}.txt"
    txt_path.write_text(res.text, encoding="utf-8")
```

---

## Összegzés

Most már tudod, **hogyan végezzünk kötegelt OCR-t képeken** és megbízhatóan **kinyerheted a szöveget a JPEG fájlokból** egy kompakt Python szkript segítségével. A motor egyszeri inicializálásával, az összes JPEG útvonal összegyűjtésével, egyetlen kötegben történő feldolgozásával és a kimenet előnézetével egyszerre érhetsz el sebességet és egyszerűséget. Innen tovább bővítheted a munkafolyamatot – hozzáadhatsz többnyelvű támogatást, tárolhatod az eredményeket adatbázisban, vagy integrálhatod a szkriptet egy nagyobb dokumentum‑feldolgozó csővezetékbe.

Készen állsz a következő lépésre? Próbáld ki a `ocr` könyvtár helyett a Tesseract‑ot, kísérletezz különböző képelőfeldolgozási technikákkal (küszöbölés, átméretezés), vagy add a kinyert szöveget egy természetes nyelvfeldolgozó modellnek automatikus kategorizálás céljából. A lehetőségek végtelenek, és most már egy szilárd alapod van a továbblépéshez.

Boldog kódolást, és legyenek a OCR kötegeid mindig hibamentesek!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}