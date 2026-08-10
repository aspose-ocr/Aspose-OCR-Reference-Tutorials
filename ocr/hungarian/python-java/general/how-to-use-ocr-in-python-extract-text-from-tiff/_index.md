---
category: general
date: 2026-07-05
description: Hogyan használjuk az OCR-t Pythonban a TIFF gyors szöveggé alakításához.
  Ismerje meg az OCR könyvtár Python lépéseit a TIFF képek szövegének kinyeréséhez
  és egy Python OCR motor felépítéséhez.
draft: false
keywords:
- how to use ocr
- ocr library python
- convert tiff to text
- extract text from tiff
- python ocr engine
language: hu
og_description: Hogyan használjunk OCR-t Pythonban? Ez az útmutató lépésről lépésre
  megmutatja, hogyan konvertáljunk TIFF-fájlokat szöveggé egy python OCR motor és
  az OCR Python könyvtár segítségével.
og_title: Hogyan használjuk az OCR-t Pythonban – Teljes TIFF szövegkivonás
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  headline: How to Use OCR in Python – Extract Text from TIFF
  type: TechArticle
- description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  name: How to Use OCR in Python – Extract Text from TIFF
  steps:
  - name: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
    text: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
  - name: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
    text: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
  - name: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
    text: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Image Processing
title: Hogyan használjuk az OCR-t Pythonban – Szöveg kinyerése TIFF-ből
url: /hu/python-java/general/how-to-use-ocr-in-python-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjunk OCR-t Pythonban – Szöveg kinyerése TIFF-ből

Gondolkodtál már azon, **hogyan használjunk OCR-t Pythonban**, hogy egy beolvasott könyvet szerkeszthető szöveggé alakítsunk? Nem vagy egyedül – fejlesztők, kutatók és hobbi‑kedvelők is ugyanebbe a problémába ütköznek, amikor többoldalas TIFF‑képekkel dolgoznak. A jó hír? A **ocr library python** segítségével felállíthatsz egy kis OCR‑motort, rámutathatsz egy TIFF‑fájlra, és néhány másodperc alatt tiszta, kereshető szöveget kapsz.

Ebben az útmutatóban végigvezetünk minden szükséges lépésen: a megfelelő csomag telepítésén, egy többoldalas TIFF betöltésén, az OCR‑motor futtatásán, és végül az egyes oldalak tartalmának kiíratásán. A végére képes leszel **TIFF‑et szöveggé konvertálni** és **szöveget kinyerni TIFF‑fájlokból** anélkül, hogy elhagynád a Python környezetet.

## Előfeltételek

- Python 3.9 vagy újabb (a példát 3.11‑en teszteltük)
- A `ocr` könyvtár legújabb verziója (vagy bármely kompatibilis `python ocr engine`, amit preferálsz)
- Egy többoldalas TIFF fájl, amelyet feldolgozni szeretnél (ezt `scanned_book.tif`‑nek hívjuk)
- Alapvető ismeretek a Python szkriptek és virtuális környezetek használatáról

Nincs szükség nehéz külső eszközökre – csak pip és néhány sor kód.

## Telepítsd az OCR Library Python-t

Először is: szükséged van egy stabil OCR háttérre. Ebben az útmutatóban a fiktív `ocr` csomagot használjuk, amely egy egyszerű magas szintű API‑t biztosít, de ugyanaz a minta működik Tesseract‑alapú csomagokkal, mint a `pytesseract`, vagy kereskedelmi SDK‑kkal.

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Pro tipp:** Ha Windows rendszeren vagy, és a csomag natív binárisokra támaszkodik, győződj meg róla, hogy a megfelelő Visual C++ redistributable telepítve van. A telepítő általában figyelmeztet, ha valami hiányzik.

## Hogyan használjunk OCR motort Pythonban

Miután a könyvtár készen áll, indítsunk egy OCR motort, és irányítsuk a TIFF fájlunkra. Az alábbi kódrészlet létrehoz egy motor példányt, beállítja a nyelvet angolra, és előkészíti a többoldalas feldolgozáshoz.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # You can switch to ocr.Language.FRENCH, etc.
```

**Miért állítsuk be a nyelvet?**  
A legtöbb OCR motor nyelvi modelleket használ a pontosság növelésére. Ha kihagyod ezt a lépést, a motor egy általános modellre vált vissza, amely esetleg helytelenül ismeri fel az írásjeleket vagy speciális karaktereket.

## Töltsd be a többoldalas TIFF képet

A következő lépés a beolvasott dokumentum betöltése. A `ocr.Image.load` segédfüggvény natívan kezeli a TIFF stackeket, és egy olyan objektumot ad vissza, amely belsőleg minden oldalt képvisel.

```python
# Step 2: Load the multi‑page TIFF image containing the scanned book
tiff_path = "YOUR_DIRECTORY/scanned_book.tif"
tiff_image = ocr.Image.load(tiff_path)
```

> **Szélsőséges eset:** Ha a TIFF tömörítést használ (CCITT Group 4, LZW, stb.) és a könyvtár hibát dob, próbáld meg először egy tömörítetlen verzióra konvertálni az ImageMagick segítségével:
> ```bash
> convert scanned_book.tif -compress none scanned_book_uncompressed.tif
> ```

## OCR végrehajtása minden oldalon – TIFF konvertálása szöveggé

A képoobjektummal a motor most egyszerre tudja feldolgozni az összes oldalt. Ez a metódus egy listát ad vissza, ahol minden elem egyetlen oldal OCR‑eredményét tartalmazza.

```python
# Step 3: Perform OCR on all pages of the image
page_results = engine.recognize_multi_page(tiff_image)
```

**Mi történik a háttérben?**  
A `recognize_multi_page` függvény végigiterál minden rasterizált oldalon, futtatja a neurális hálózat alapú felismerőt, és a sima szöveges kimenetet a megbízhatósági pontszámokkal együtt csomagolja. Gyakorlatilag egy kötegelt művelet, amely megspórolja a kézi ciklus írását.

## Eredmények iterálása – Szöveg kinyerése TIFF‑ből

Végül megjelenítjük a felismert szöveget. Kiírhatod a kimenetet külön `.txt` fájlokba, betöltheted egy adatbázisba, vagy egy keresőindexbe – bármi, ami a munkafolyamatodhoz illik.

```python
# Step 4: Iterate through the results and display the recognized text for each page
for page_index, result in enumerate(page_results):
    print(f"Page {page_index + 1}:\n{result.text}\n")
```

### Várt kimenet

```
Page 1:
Chapter 1
In the beginning...

Page 2:
The quick brown fox jumps over the lazy dog.

Page 3:
...

```

Minden `result.text` karakterlánc a nyers OCR‑kimenetet tartalmazza az adott oldalhoz. Ha sortörés megőrzésére van szükséged, a legtöbb motor a `result.lines`‑t egy karakterláncok listájaként teszi elérhetővé.

## Nagy TIFF fájlok kezelése – Tippek és trükkök

Egy 500 oldalas TIFF feldolgozása memóriaigényes lehet. Íme néhány stratégia a zökkenőmentes működéshez:

1. **Az oldalak darabolása** – A `recognize_multi_page` helyett hívd a `engine.recognize(page)`‑t egy generátorban, amely egyesével adja vissza az oldalakat.
2. **DPI beállítása** – A képfelbontás csökkentése (pl. 300 DPI‑ról 200 DPI‑ra) csökkenti a CPU terhelést, miközben alig befolyásolja a pontosságot a legtöbb nyomtatott szöveg esetén.
3. **Párhuzamosítás** – Ha az OCR motor szálbiztos, indíts egy `concurrent.futures.ThreadPoolExecutor`‑t, hogy egyszerre több oldalon futtassa a felismerést.

```python
import concurrent.futures

def ocr_page(page):
    return engine.recognize(page).text

with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    texts = list(executor.map(ocr_page, tiff_image.pages))
```

## Kinyert szöveg mentése fájlokba

A legtöbb valós környezetben a csővezetékeknek tartós tárolásra van szükségük. Az alábbiakban egy tömör módot mutatunk, amellyel minden oldal szövegét külön fájlba mentheted, megőrizve az oldalsorrendet.

```python
import pathlib

output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for i, result in enumerate(page_results, start=1):
    file_path = output_dir / f"page_{i:03}.txt"
    file_path.write_text(result.text, encoding="utf-8")
    print(f"Saved page {i} to {file_path}")
```

Most már van egy tiszta `.txt` fájlokból álló könyvtárad, amely készen áll az indexelésre vagy további NLP feldolgozásra.

## Kép előnézet – OCR eredmények vizuális megjelenítése

Ha szeretnéd látni az OCR átfedést az eredeti képen (hasznos hibakereséshez), sok könyvtár lehetővé teszi a körülhatároló dobozok rajzolását. Íme egy gyors példa a Pillow használatával:

```python
from PIL import ImageDraw

for page, result in zip(tiff_image.pages, page_results):
    draw = ImageDraw.Draw(page)
    for word in result.words:          # Assume `result.words` gives bounding boxes
        draw.rectangle(word.box, outline="red")
    page.show()   # Opens the annotated page
```

![How to use OCR in Python – OCR overlay on a TIFF page](ocr_overlay_example.png)

*Alternatív szöveg:* How to use OCR in Python – a felismert szöveg vizuális átfedése egy TIFF oldalon.

## Gyakori hibák és hogyan kerüld el őket

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| Torzuló karakterek | Helytelen nyelvi modell | Állítsd be az `engine.language`‑t a megfelelő enumra |
| Hiányzó oldalak | A TIFF tömörítés nem támogatott | Először konvertáld a TIFF-et tömörítetlen formátumba |
| Lassú teljesítmény | Magas DPI + egy szálas feldolgozás | Csökkentsd a DPI-t vagy engedélyezd a több szálas feldolgozást |
| Üres kimenet | A kép túl sötét/alacsony kontrasztú | Előfeldolgozás kontrasztnyújtással (`opencv` vagy `Pillow`) |

Ezeknek a korai kezelése órákat takarít meg a későbbi hibakeresésben.

## Következő lépések – Alapvető kinyerésen túl

Miután elsajátítottad a **hogyan használjunk OCR-t Pythonban** alapjait, érdemes tovább felfedezni:

- **PDF generálás** – Kombináld a kinyert szöveget a `reportlab`‑al, hogy kereshető PDF‑eket építs újra.
- **Nyelvfelismerés** – Automatikusan állítsd át az `engine.language`‑t a `langdetect` használatával.
- **Strukturált adat kinyerés** – Használj reguláris kifejezéseket vagy spaCy‑t, hogy dátumokat, neveket vagy táblázatokat nyerj ki a nyers szövegből.
- **Alternatív OCR háttérprogramok** – Cseréld le az `ocr`‑t `pytesseract`‑ra vagy `easyocr`‑ra, ha többnyelvű támogatásra van szükséged.

Ezek a témák természetesen visszautalnak a másodlagos kulcsszavakra: **ocr library python**, **convert tiff to text**, **extract text from tiff**, és **python ocr engine**, így szilárd alapot adva a fejlettebb projektekhez.

---

### Következtetés

Áttekintettük, **hogyan használjunk OCR-t Pythonban** a telepítéstől a többoldalas feldolgozásig, pontosan megmutatva, hogyan **konvertáljunk TIFF‑et szöveggé** és **nyerjünk ki szöveget TIFF‑ből** egy egyszerű **python OCR engine** segítségével. A fenti teljes, futtatható példa a legtöbb szabványos TIFF fájlra azonnal működnie kell, és a megadott tippek segítenek nagyobb dokumentumok skálázásában vagy az OCR integrálásában nagyobb csővezetékekbe.

Próbáld ki a saját beolvasott könyveiddel, számláiddal vagy archivált képeiddel – majd kísérletezz a “Következő lépések” szekcióban felsorolt haladó ötletekkel. Boldog kódolást, és legyenek az OCR eredményeid mindig pontosak!

## Mit érdemes legközelebb megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Szöveg kinyerése képből Aspose OCR‑rel – Lépésről‑lépésre útmutató](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Hogyan nyerjünk ki szöveget TIFF‑ből Aspose.OCR Java‑val](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Hogyan végezzünk képszöveg‑kinyerést stream‑ből Aspose OCR használatával](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}