---
category: general
date: 2026-06-16
description: Szöveg kinyerése TIFF-fájlokból Python OCR-rel. Tanulja meg, hogyan konvertálja
  a TIFF-et szöveggé lépésről lépésre, könnyedén kezelve a többoldalas dokumentumokat.
draft: false
keywords:
- extract text from tiff
- convert tiff to text
- Python OCR multi‑page TIFF
- OCR language settings
- OCR engine Python
language: hu
og_description: Szöveget nyerj ki TIFF fájlokból Python OCR-rel. Kövesd ezt az útmutatót
  a TIFF szöveggé konvertálásához, a többoldalas beolvasások kezeléséhez, és tiszta
  eredményekhez.
og_title: Szöveg kinyerése TIFF-ből – Teljes Python útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  headline: Extract Text from TIFF – Complete Python Guide
  type: TechArticle
- description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  name: Extract Text from TIFF – Complete Python Guide
  steps:
  - name: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
    text: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
  - name: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
    text: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
  - name: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
    text: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
  - name: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
    text: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Text extraction
title: Szöveg kinyerése TIFF-ből – Teljes Python útmutató
url: /hu/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szöveg kinyerése TIFF‑ből – Teljes Python útmutató

Valaha szükséged volt **szöveg kinyerésére TIFF** képekből, de nem tudtad, hol kezdjed? Nem vagy egyedül – sok fejlesztő szembesül ezzel a problémával, amikor beolvasott archívumokkal vagy régi dokumentumokkal dolgozik. A jó hír? Néhány Python sorral **TIFF‑et szöveggé alakíthatsz** villámgyorsan, még akkor is, ha a fájl tucatnyi oldalt tartalmaz.

Ebben az útmutatóban egy valós példán keresztül vezetünk végig: egy többoldalas TIFF betöltése, az OCR nyelvének francia nyelvre állítása, és a felismert szöveg kinyerése minden egyes oldalról. A végére egy azonnal futtatható szkriptet kapsz, megérted, miért fontos minden lépés, és tudni fogod, hogyan igazítsd más nyelvekhez vagy képformátumokhoz.

## Előfeltételek

- Python 3.8 vagy újabb telepítve.
- Az `ocr` csomag (vagy bármely kompatibilis OCR könyvtár, amely `OcrEngine` osztályt biztosít). Telepítheted a `pip install ocr-lib` paranccsal – cseréld le a ténylegesen használt csomagnévre.
- Egy többoldalas TIFF fájl (pl. `french-scans.tif`), amelyet feldolgozni szeretnél.
- Alapvető ismeretek a Python szkriptek írásához.

Nincs nehéz függőség, nincs külső szolgáltatás – csak tiszta Python és egy OCR motor.

## 1. lépés: Az OCR motor beállítása a **szöveg kinyeréséhez TIFF‑ből**

Először is – szükségünk van egy OCR motor példányra, és meg kell mondanunk, melyik nyelvet használja. Ebben az esetben a forrásanyag francia, ezért ennek megfelelően állítjuk be a nyelvet.

```python
import ocr  # Replace with the actual import if your OCR library uses a different name

# Create the OCR engine
engine = ocr.OcrEngine()

# Tell the engine to look for French characters
engine.language = ocr.Language.FRENCH
```

**Miért fontos ez:**  
A nyelvi beállítás drámaian javítja a pontosságot. A francia karakterek, mint a „é” vagy a „ç”, általános szimbólumként lennének félreolvasva, ha a motor alapértelmezés szerint angolt használna. A francia nyelv kifejezett kiválasztásával a motor a megfelelő karaktertérképet kapja.

> **Pro tipp:** Ha több nyelven dolgozol, a `engine.language` értékét futás közben módosíthatod minden egyes `recognize()` hívás előtt.

## 2. lépés: A többoldalas TIFF betöltése, amelyet **TIFF‑ből szöveggé konvertálunk**

Egy TIFF több keretet (frame‑et) is tartalmazhat – tekints minden keretet egy külön oldalnak. Az OCR könyvtár ezt elrejti számunkra, így egyszerűen csak a fájlra mutatunk.

```python
# Path to your multi‑page TIFF
tiff_path = "YOUR_DIRECTORY/french-scans.tif"

# Load the file; the engine now knows how many pages it contains
engine.load_from_file(tiff_path)
```

**Éles eset figyelmeztetés:**  
Ha a fájl útvonala hibás vagy a TIFF sérült, a `load_from_file` metódus kivételt dob. Éles környezetben tedd egy `try/except` blokkba:

```python
try:
    engine.load_from_file(tiff_path)
except Exception as e:
    print(f"Failed to load TIFF: {e}")
    raise
```

## 3. lépés: OCR futtatása a teljes dokumentumon – a **szöveg kinyerése TIFF‑ből** központi része

Most hagyjuk, hogy a motor elvégezze a varázslatát. A `recognize()` hívás egy lépésben feldolgozza az összes oldalt, és egy gazdag eredményobjektust ad vissza.

```python
# Perform OCR on all pages at once
multi_result = engine.recognize()
```

**Mi történik a háttérben?**  
A motor minden egyes keretet bejár, előfeldolgozást alkalmaz (kiegyenesítés, binarizálás), lefuttatja a neurális hálót, és összegzi a kimenetet. Mivel csak egyszer hívtuk meg a `recognize()`‑t, a könyvtár megoszthatja az erőforrásokat az oldalak között, ami gyorsabb, mint a kézi ciklus.

## 4. lépés: A felismert szöveg kinyerése a JSON eredményből – **TIFF‑ből szöveggé konvertálás** oldalanként

Az eredményobjektum JSON‑ként sorosítható. Ebben a JSON‑ban egy `pages` tömböt találsz, amelynek minden eleme egy `text` mezőt tartalmaz.

```python
# Convert the result to a Python dict (JSON-like)
result_dict = multi_result.to_json()

# Extract the list of pages
pages = result_dict["pages"]
```

Most már egy tiszta Python listánk van, ahol minden elem egy oldal OCR‑kimenetét tartalmazza.

## 5. lépés: A szöveg kiírása vagy mentése minden oldalra – a **szöveg kinyerése TIFF‑ből** végső lépése

Iteráljunk végig az oldalakon, és jelenítsük meg a kinyert szöveget. Ha szeretnéd, minden oldalt külön `.txt` fájlba is írhatunk.

```python
for i, page in enumerate(pages, start=1):
    print(f"--- Page {i} ---")
    print(page["text"])
    print()  # Blank line for readability
```

### Várható kimenet (példa)

```
--- Page 1 ---
Bonjour, ceci est un exemple de texte extrait d'une image TIFF.

--- Page 2 ---
Le deuxième page contient davantage d'informations en français.
```

Ha az OCR sikeres, minden oldalra egy tiszta francia mondatblokkot látsz. Ha torz karaktereket észlelsz, ellenőrizd a nyelvi beállítást, vagy fontold meg a kép felbontásának növelését az OCR előtt.

## Gyakori hibák kezelése, amikor **TIFF‑t szöveggé konvertálsz**

| Probléma | Miért fordul elő | Gyors megoldás |
|----------|------------------|----------------|
| **Üres `pages` tömb** | A TIFF nem lett megfelelően betöltve, vagy nulla kerete van. | Ellenőrizd a fájl útvonalát, és győződj meg róla, hogy a TIFF nem egy egyoldalas PNG, amely TIFF‑nek álcázott. |
| **Rossz karakterek** | Nyelvi eltérés vagy alacsony képminőség. | Állítsd be a megfelelő `engine.language` értéket, és előfeldolgozd a képet (pl. növeld a DPI‑t). |
| **Memória túlterhelés nagy TIFF‑eknél** | Az összes oldal egyidejű betöltése RAM‑ot fogyaszt. | Feldolgozás darabokban: tölts be egy keretet, ismerd fel, majd dobja el, mielőtt a következőre lépnél. |
| **Unicode hibák nyomtatáskor** | A konzol kódolása nem támogatja a diakritikus karaktereket. | Használd a `print(page["text"].encode('utf-8').decode('utf-8'))` parancsot, vagy állítsd be a terminált UTF‑8-ra. |

## A szkript kibővítése: a **szöveg kinyerése TIFF‑ből** kötegelt feldolgozáshoz

Miután szilárd alapot szereztél, fontold meg a következő lépéseket:

1. **Kötegelt konverzió** – Csomagold az egész folyamatot egy `def ocr_tiff(path):` függvénybe, és iterálj egy TIFF fájlok könyvtárán.
2. **Kimenet fájlokba** – A nyomtatás helyett írd minden oldal szövegét `page_{i}.txt` fájlba, vagy fűzd össze egyetlen dokumentummá.
3. **Alternatív OCR motorok** – Ha nagyobb pontosságra van szükséged, cseréld le az `ocr.OcrEngine()`-t Tesseract‑ra (`pytesseract`) vagy Azure Cognitive Services‑re – csak tartsd meg a “szöveg kinyerése TIFF‑ből” logikát.
4. **Utófeldolgozás** – Futtass helyesírás-ellenőrzést, nyelvfelismerést vagy regex‑tisztítást a nyers OCR kimenet megtisztításához.

## Teljes, azonnal futtatható szkript

Az alábbiakban a teljes kód található, készen áll a másolásra és beillesztésre. Alapvető hibakezelést és opcionális mentést tartalmaz minden oldal szövegének külön fájlokba.

```python
import ocr  # Adjust import based on your OCR library
import os

def extract_text_from_tiff(tiff_path: str, output_dir: str = None) -> list:
    """
    Loads a multi‑page TIFF, runs OCR, and returns a list of strings,
    one per page. Optionally saves each page to a .txt file.
    """
    # Initialize engine and set language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.FRENCH

    # Load the TIFF file
    try:
        engine.load_from_file(tiff_path)
    except Exception as e:
        raise RuntimeError(f"Unable to load {tiff_path}: {e}")

    # Run OCR on all pages
    multi_result = engine.recognize()

    # Parse JSON result
    pages = multi_result.to_json()["pages"]
    texts = [page["text"] for page in pages]

    # If an output directory is provided, write each page to a file
    if output_dir:
        os.makedirs(output_dir, exist_ok=True)
        for i, text in enumerate(texts, start=1):
            file_path = os.path.join(output_dir, f"page_{i}.txt")
            with open(file_path, "w", encoding="utf-8") as f:
                f.write(text)

    return texts

if __name__ == "__main__":
    # Example usage – replace with your actual TIFF path
    tiff_file = "YOUR_DIRECTORY/french-scans.tif"
    # Optional: where to store per‑page text files
    out_folder = "extracted_pages"

    page_texts = extract_text_from_tiff(tiff_file, out_folder)

    for i, txt in enumerate(page_texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()
```

Futtasd ezt a szkriptet, állítsd be a `tiff_file` változót a dokumentumodra, és figyeld, ahogy a konzol tiszta francia mondatokkal töltődik fel. Ha megadtad az `out_folder`‑t, akkor egy sor `page_#.txt` fájlt is találsz, amelyek készen állnak a további feldolgozásra.

## Összegzés

Most **kinyertük a szöveget TIFF** fájlokból egy egyszerű Python OCR munkafolyamat segítségével, és már tudod, hogyan **konvertálj TIFF‑et szöveggé** megbízhatóan. A motor a megfelelő nyelvvel történő inicializálásától az egyes oldalak JSON‑eredményének bejárásáig minden lépést a „miért” magyarázatával ismertettünk, így a mintát könnyen alkalmazhatod más nyelvekre, képformátumokra vagy nagyobb kötegelt feladatokra.

Mi a következő? Próbáld ki az OCR háttércserét Tesseract‑ra, kísérletezz különböző nyelvi csomagokkal, vagy integráld a kimenetet egy kereshető adatbázisba. A lehetőségek határtalanok, ha megbízhatóan tudod a beolvasott képeket kereshető szöveggé alakítani.

Nyugodtan hagyj megjegyzést, ha elakadsz vagy ötleteid vannak a további fejlesztésekhez. Boldog kódolást!

## Mit érdemes legközelebb megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat, és alternatív megvalósítási megközelítéseket fedezhess fel saját projektjeidben.

- [Szöveg kinyerése képből Aspose OCR‑rel – Lépésről‑lépésre útmutató](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Szöveg kinyerése képekből OCR művelettel mappákon](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Kép konvertálása szöveggé – OCR végrehajtása URL‑ről származó képen](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}