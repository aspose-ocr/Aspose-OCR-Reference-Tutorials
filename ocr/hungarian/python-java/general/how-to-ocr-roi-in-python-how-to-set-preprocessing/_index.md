---
category: general
date: 2026-03-28
description: Hogyan OCR-elj ROI-t Pythonban – Tanulja meg, hogyan állíthatja be az
  előfeldolgozási beállításokat a pontos szövegkinyeréshez a képek meghatározott területeiről.
draft: false
keywords:
- how to OCR ROI
- how to set preprocessing
- Aspose OCR Python
- ROI extraction
- image preprocessing OCR
language: hu
og_description: Hogyan OCR-eljünk ROI-t Pythonban – Ez az útmutató bemutatja, hogyan
  állítsuk be az előfeldolgozást a meghatározott képrészletekből származó megbízható
  szövegkinyeréshez.
og_title: Hogyan OCR-eljünk ROI-t Pythonban – Hogyan állítsuk be az előfeldolgozást
tags:
- OCR
- Python
- Aspose
title: Hogyan OCR-eljünk ROI-t Pythonban – Hogyan állítsuk be az előfeldolgozást
url: /hu/python-java/general/how-to-ocr-roi-in-python-how-to-set-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan OCR-eljünk ROI-t Pythonban – Hogyan állítsuk be az előfeldolgozást

Gondolkodtál már **hogyan OCR-eljünk ROI-t** egy zajos számla képen anélkül, hogy az egész oldalt a memóriába töltenéd? Nem vagy egyedül. Sok valós projektben csak néhány mezőre van szükség – ügyfél neve, cím, összegzések – így az egész dokumentum beolvasása túlzás.  

A jó hír? Az Aspose OCR segítségével pontosan megmondhatod a motor számára, **hol keressen**, sőt még meg is kérheted, hogy először tisztítsa meg a képet. Ebben az útmutatóban végigvezetünk **hogyan állítsuk be az előfeldolgozási** beállításokat, hogyan definiáljunk érdeklődési területeket (ROI‑kat), és hogyan nyerjünk ki tiszta szöveget néhány Python sorral.

A végére egy kész‑futásra alkalmas szkriptet kapsz, amely konkrét blokkokat nyer ki bármely számlából, blokknyugtából vagy űrlapból. Nem kell extra eszköz, csak az Aspose OCR és egy kis Python logika.

---

## Amire szükséged lesz

- **Python 3.8+** (a kód bármely friss verzión működik)  
- **Aspose OCR for Python via .NET** – telepítsd a `pip install aspose-ocr` paranccsal  
- Egy minta kép (pl. `invoice.png`) egy olyan mappában, amelyre hivatkozhatsz  
- Alapvető ismeretek a Python függvényekről és az objektum‑orientált szintaxisról  

Ha már megvannak ezek, nagyszerű – ugorjunk egyenesen a kódra.

---

![Hogyan OCR-eljünk ROI diagram](ocr-roi.png "Hogyan OCR-eljünk ROI példa")

*Alt szöveg: Hogyan OCR-eljünk ROI diagram, amely ROI dobozokat mutat egy számla képen*

---

## 1. lépés – Az OCR motor inicializálása (Hogyan OCR-eljünk ROI)

Mielőtt megmondhatnánk a motornak, *hol* keressen, szükségünk van egy OCR processzor példányra. Ez az objektum tartalmazza az összes konfigurációt és végrehajtja a felismerési lépést.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the engine – this is the entry point for all OCR work
ocr_engine = aocr.OcrEngine()
```

*Miért fontos*: Az `OcrEngine` osztály elrejti a nehéz feladatokat (betűtípus‑detektálás, elrendezés‑elemzés, stb.). Egyetlen motor létrehozásával elkerülöd a nehéz erőforrások újra‑inicializálását minden egyes képhez, ami a teljesítményt gyorsabbá teszi.

---

## 2. lépés – A forráskép betöltése (Hogyan OCR-eljünk ROI)

Az Aspose Storage egyszerűvé teszi a képek betöltését. Mutasd meg a fájl útvonalát, és kapsz egy `Image` objektumot, amely készen áll a feldolgozásra.

```python
# Replace YOUR_DIRECTORY with the actual path where invoice.png lives
source_image = storage.Image.load("YOUR_DIRECTORY/invoice.png")
```

*Tippek*: Ha stream‑ekkel dolgozol (pl. web‑API‑n keresztül feltöltött képek), egy `BytesIO` objektumot adhatunk át az `Image.load`‑nak a fájlútvonal helyett.

---

## 3. lépés – Az érdeklődési területek (ROI‑k) definiálása

Most válaszolunk a központi kérdésre **hogyan OCR-eljünk ROI-t**: megmondjuk a motornak, melyik pontos téglalapok tartalmazzák a számunkra fontos adatokat. Minden ROI a bal‑felső sarok (`x`, `y`) és a méret (`width`, `height`) alapján van definiálva.

```python
from aspose.ocr import Roi

# Each tuple is (x, y, width, height) in pixels
regions_of_interest = [
    Roi(50, 120, 400, 60),   # Customer name block
    Roi(50, 200, 400, 80)    # Address block
]
```

*Miért használjunk ROI‑kat?*  
- **Sebesség** – A motor kihagyja a kép irreleváns részeit.  
- **Pontosság** – Egy kis területre fókuszálva a zaj máshol nem zavarja a felismerőt.  
- **Rugalmasság** – Tetszőleges számú ROI‑t hozzáadhatsz; a motor a listában megadott sorrendben adja vissza az eredményeket.

---

## 4. lépés – Hogyan állítsuk be az előfeldolgozást a jobb OCR‑pontosságért

A szkennerek vagy telefonok által közvetlenül előállított képek gyakran torzulnak, alacsony kontrasztúak vagy egyenetlen megvilágításúak. Az Aspose OCR egy `PreprocessingOptions` objektumot kínál, amely lehetővé teszi a gyakori javítások engedélyezését a felismerés előtt.

```python
from aspose.ocr import PreprocessingOptions

preprocessing_options = PreprocessingOptions()
preprocessing_options.deskew = True          # Auto‑rotate tilted text
preprocessing_options.binarize = True        # Convert to black‑white for clarity
preprocessing_options.contrast = 1.5         # Boost contrast (1.0 = no change)
```

*Hogyan segít*:  
- **Deskew** eltávolítja a dőlést, ami a karakterformákat homályossá teszi.  
- **Binarize** csökkenti a színes zajt, egy tiszta bináris képet ad a OCR motor számára.  
- **Contrast** erősíti a gyenge vonalakat, ami különösen hasznos a kifakult nyugták esetén.

Kísérletezhetsz ezekkel a flag‑ekkel – kapcsold ki az egyiket, és nézd meg, változik-e a kimenet. Ez a **hogyan állítsuk be az előfeldolgozást** hatékony megközelítése.

---

## 5. lépés – OCR végrehajtása csak a definiált ROI‑kban

Miután megvan a motor, a kép, a ROI‑k és az előfeldolgozás, itt az ideje meghívni a `recognize` metódust. A metódus egy `OcrResult` objektumot ad vissza, amely egy `regions` gyűjteményt tartalmaz – minden elem a megadott ROI sorrendjével egyezik.

```python
ocr_result = ocr_engine.recognize(
    source_image,
    rois=regions_of_interest,
    preprocessing=preprocessing_options
)
```

*A háttérben*: A motor minden ROI‑t kivág, alkalmazza az előfeldolgozási csővezetéket, és futtatja a felismerési modellt a megtisztított részleten. Mivel listát adtunk át, az eredmény ugyanabban a sorrendben marad, ami megkönnyíti a további feldolgozást.

---

## 6. lépés – A kinyert szöveg olvasása és felhasználása (Hogyan OCR-eljünk ROI)

Végül iteráljunk a `regions` listán, és nyomtassuk ki – vagy tároljuk – a felismert karakterláncokat. A `Region` objektum egy `text` tulajdonságot biztosít, amely a Unicode eredményt tartalmazza.

```python
for idx, region in enumerate(ocr_result.regions, start=1):
    print(f"Region {idx} text:")
    print(region.text)
    print("-" * 40)
```

**Várható kimenet (példa)**:

```
Region 1 text:
John Doe
----------------------------------------
Region 2 text:
123 Maple Street
Springfield, IL 62704
----------------------------------------
```

Ha a szöveg összezavarodottnak tűnik, nézd át újra a **hogyan állítsuk be az előfeldolgozást** részt: esetleg növeld a `contrast`‑et vagy tiltsd le a `binarize`‑t színes logók esetén.

---

## Gyakori hibák és profi tippek

| Probléma | Miért fordul elő | Javítás (Hogyan állítsuk be az előfeldolgozást) |
|----------|------------------|----------------------------------------------|
| Dőlt szöveg értelmetlen karakterekkel | `deskew` letiltva vagy a kép túl erősen elfordított | Engedélyezd a `preprocessing_options.deskew = True` |
| Számok pontokká vagy szórt jelekké alakulnak | Alacsony kontraszt vagy túl agresszív binarizálás | Csökkentsd a `contrast`‑et (pl. `1.2`) vagy állítsd `binarize = False` |
| ROI koordináták néhány pixellel eltolódnak | Különböző DPI vagy szkenner skálázás | Használj eszközt (pl. Paint.NET) a pontos pixelpozíciók méréséhez, vagy adj hozzá egy kis margót (`+5` pixel) minden ROI‑hoz |
| Egy régió üres eredményt ad | ROI kívül esik a kép határain | Ellenőrizd a kép méreteit: `source_image.width`, `source_image.height` |

---

## A megoldás bővítése (Hogyan OCR-eljünk ROI‑t különböző szituációkban)

- **Dinamikus ROI‑k**: Ha a számláid változó elrendezésűek, először futtathatsz egy gyors teljesoldalas OCR‑t a kulcsszavak („Customer:”, „Address:”) megtalálásához, majd a ROI‑kat futásidőben számolod ki.  
- **Kötegelt feldolgozás**: Csomagold be a fenti lépéseket egy függvénybe, és iterálj egy mappában lévő képek felett. Ne felejtsd el újra‑használni ugyanazt az `ocr_engine` példányt a memóriahasználat alacsonyan tartásához.  
- **Exportálás JSON‑ba**: A nyomtatás helyett építs egy szótárat, és írd ki a `json.dumps`‑szel; ez egyszerűvé teszi a downstream integrációt (pl. ERP rendszerbe való betáplálás).

```python
import json

def extract_invoice_fields(image_path):
    img = storage.Image.load(image_path)
    result = ocr_engine.recognize(
        img,
        rois=regions_of_interest,
        preprocessing=preprocessing_options
    )
    data = {f"field_{i+1}": r.text.strip() for i, r in enumerate(result.regions)}
    return data

print(json.dumps(extract_invoice_fields("invoice.png"), indent=2))
```

---

## Összegzés

Most már van egy teljes, futtatható példád, amely megmutatja, **hogyan OCR-eljünk ROI-t** Pythonban, miközben elsajátítod a **hogyan állítsuk be az előfeldolgozást** a legoptimálisabb pontosságért. Azáltal, hogy a motort csak a számodra fontos téglalapokra korlátozod, és előre megtisztítod a képet, gyorsabb és tisztább eredményeket kapsz – tökéletes számla‑automatizáláshoz, űrlap‑digitalizáláshoz vagy bármely olyan szituációhoz, ahol csak az oldal egy szelete érdekel.

Készen állsz a következő lépésre? Próbáld ki a ROI koordináták módosítását egy másik dokumentumtípushoz, vagy kísérletezz további előfeldolgozási flag‑ekkel, mint a `sharpen` vagy a `noise_reduction`. Az Aspose OCR rugalmassága lehetővé teszi, hogy a csővezetékedet gyakorlatilag bármilyen képminőséghez igazítsd.

Ha elakadsz, ellenőrizd a konzol kimenetét üres régiókért, és nézd át újra az előfeldolgozási beállításokat. Boldog kódolást, és legyen a OCR‑od mindig pontos!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}