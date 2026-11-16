---
category: general
date: 2026-05-31
description: Tanulja meg, hogyan használja az OCR érdeklődési területet a kép betöltéséhez
  OCR-hez, és szöveget nyerjen ki egy téglalapból – tökéletes a számla összegének
  felismeréséhez.
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: hu
og_description: Mesteri OCR érdeklődési terület a kép betöltéséhez, a szöveg kinyerése
  a téglalapból és a számla szövegének felismerése egyetlen oktatóanyagban.
og_title: OCR érdeklődési terület – lépésről lépésre Python útmutató
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  headline: OCR Region of Interest – Extract Text from Rectangle in Python
  type: TechArticle
- description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  name: OCR Region of Interest – Extract Text from Rectangle in Python
  steps:
  - name: Loads an invoice image from disk.
    text: Loads an invoice image from disk.
  - name: Marks a rectangular ROI where the total amount lives.
    text: Marks a rectangular ROI where the total amount lives.
  - name: Runs OCR only inside that ROI.
    text: Runs OCR only inside that ROI.
  - name: Prints the cleaned‑up amount string.
    text: Prints the cleaned‑up amount string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR érdeklődési terület – Szöveg kinyerése téglalapból Pythonban
url: /hu/python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR érdeklődési terület – Szöveg kinyerése téglalapból Pythonban

Gondolkodtál már azon, hogyan **ocr region of interest** egy beolvasott számla adott részén anélkül, hogy az egész oldalt betáplálnád a motorba? Nem vagy az első, aki egy homályos nyugtán ülve azt kérdezi: „Hogyan nyerjem ki az összeget, ami valahol a jobb alsó sarokban van?” A jó hír, hogy megmondhatod az OCR könyvtárnak, pontosan hol keressen, ezzel drámaian növelve a sebességet és a pontosságot.

Ebben az útmutatóban egy teljes, futtatható példán keresztül mutatjuk be, hogyan **load image for OCR**, hogyan definiálj egy **region of interest**, majd hogyan **extract text from rectangle**, végül hogyan **recognize text from invoice**, és válaszolj a klasszikus „hogyan nyerjük ki az összeget” kérdésre. Nincs homályos hivatkozás – csak konkrét kód, világos magyarázatok és néhány profi tipp, amiről jó lenne, ha korábban tudtad volna.

---

## Mit fogsz építeni

A tutorial végére egy apró Python szkriptet kapsz, amely:

1. Betölti a számla képet a lemezről.  
2. Megjelöli azt a téglalap alakú ROI-t, ahol a végösszeg található.  
3. Az OCR‑t csak ezen a ROI‑n futtatja.  
4. Kiírja a megtisztított összeg karakterláncot.  

Mindez bármelyik ROI‑t támogató OCR könyvtárral működik – itt egy fiktív, de reprezentatív `SimpleOCR` csomagot használunk, amely a Tesseract vagy EasyOCR népszerű eszközeit idézi. Nyugodtan cseréld le; a koncepciók változatlanok.

---

## Előfeltételek

- Python 3.8+ telepítve (`python --version`‑nek ≥3.8‑at kell mutatnia).  
- Pip‑el telepíthető OCR csomag (pl. `pip install simpleocr`).  
- Egy számla kép (PNG vagy JPEG), amely egy mappában van, ahonnan hivatkozhatsz.  
- Alapvető ismeretek Python függvényekről és osztályokról (semmi bonyolult).

Ha már megvannak ezek, nagyszerű – vágjunk bele. Ha nem, először szerezd be a képet; a további lépések függetlenek a fájl tényleges tartalmától.

---

## 1. lépés: Load Image for OCR

Az első dolog, amire bármely OCR munkafolyamatnak szüksége van, egy bitmap, amiből olvasni tud. A legtöbb könyvtár egyszerű `load_image` metódust kínál, amely egy fájl útvonalat fogad. Így néz ki a `SimpleOCR` motorunkkal:

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Pro tip:** Használj abszolút útvonalakat vagy `os.path.join`‑t, hogy elkerüld a „file not found” meglepetéseket, amikor a szkriptet más munkakönyvtárból futtatod.

---

## 2. lépés: Define OCR Region of Interest

Ahelyett, hogy a motor az egész oldalt átvizsgálná, pontosan megmondjuk, hol helyezkedik el az összeg. Ez a **ocr region of interest** lépés, és ez a kulcs a megbízható kinyeréshez, különösen, ha a dokumentum zajos fejléceket vagy lábléceket tartalmaz.

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

Miért ezek a számok? Az `x` és `y` pixel eltolások a bal‑felső sarokhoz képest, míg a `width` és `height` a doboz méretét írják le. Ha bizonytalan vagy, nyisd meg a képet bármely szerkesztőben, aktiváld a vonalzót, és jegyezd fel a koordinátákat. Sok IDE is lehetővé teszi, hogy a kurzor pozícióját mutassa, miközben lebegsz.

---

## 3. lépés: Extract Text from Rectangle

Most, hogy a ROI be van állítva, megkérjük a motort, hogy **recognize text from invoice**, de csak a most hozzáadott téglalapra korlátozva. A hívás egy eredményobjektust ad vissza, amely általában a nyers karakterláncot, a biztonsági pontszámokat és néha a határoló dobozokat tartalmazza.

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

A háttérben a `recognize()` minden ROI‑t bejár, kivágja a szeletet, lefuttatja az OCR modellt, és összefűzi az eredményeket. Ezért egy szorosan definiált **extract text from rectangle** terület akár másodperceket is spórolhat a kötegelt feladatok feldolgozásában.

---

## 4. lépés: How to Extract Amount – Clean the Output

Az OCR nem tökéletes; gyakran kapsz felesleges szóközöket, sortöréseket vagy akár félreolvasott karaktereket (pl. „S” vs „5”). Egy gyors `strip()` és egy apró regex általában megoldja a pénzügyi értékek esetén.

```python
# Step 4: Clean and display the recognized amount
import re

raw_amount = ocr_result.text.strip()
# Simple regex to keep digits, commas, periods, and optional currency symbols
clean_amount = re.search(r'[\d,.]+', raw_amount)
if clean_amount:
    print("Amount:", clean_amount.group())
else:
    print("Could not locate a numeric amount in the ROI.")
```

> **Miért fontos:** Ha az összeget adatbázisba vagy fizetési átjáróba szeretnéd továbbadni, előre meghatározott formátumra van szükség. A whitespace eltávolítása és a nem numerikus karakterek szűrése megakadályozza a downstream hibákat.

---

## 5. lépés: Recognize Text from Invoice – Full Script

Mindent összevetve, itt a teljes, azonnal futtatható szkript. Mentsd el `extract_amount.py` néven, és futtasd `python extract_amount.py`‑vel.

```python
# extract_amount.py
import re
from simpleocr import OcrEngine, Rectangle

def main():
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load the invoice image (adjust the path)
    ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

    # Define ROI where the amount is located
    amount_region = Rectangle(120, 340, 200, 40)
    ocr_engine.add_roi(amount_region)

    # Run OCR on the ROI
    ocr_result = ocr_engine.recognize()

    # Clean and print the amount
    raw_amount = ocr_result.text.strip()
    match = re.search(r'[\d,.]+', raw_amount)
    if match:
        print("Amount:", match.group())
    else:
        print("Could not locate a numeric amount in the ROI.")

if __name__ == "__main__":
    main()
```

### Várható kimenet

```
Amount: 1,245.67
```

Ha a ROI nincs megfelelően igazítva, előfordulhat, hogy `Amount: 1245.6S`‑t látsz – vegyük észre a felesleges „S” karaktert. Állítsd be a téglalap koordinátáit, és futtasd újra, amíg a kimenet tisztának tűnik.

---

## Gyakori hibák és széljegyek

| Probléma | Miért fordul elő | Javítás |
|----------|------------------|---------|
| **ROI túl kicsi** | Az összeg szövege levágódik, részleges felismeréshez vezet. | Növeld a `width`/`height` értékeket ~10‑20 %-kal, és teszteld újra. |
| **Helytelen DPI** | Alacsony felbontású szkennelés (≤150 dpi) csökkenti az OCR pontosságát. | Resample-eld a képet 300 dpi-re a betöltés előtt, vagy kérj magasabb DPI‑t a szkennertől. |
| **Több pénznem** | A regex az első numerikus csoportot veszi, ami lehet egy számlaszám. | Finomítsd a regexet, hogy a számjegyek előtt keresse a pénznem szimbólumokat (`$`, `€`, `£`). |
| **Forgatott számlák** | Az OCR motorok felálló szöveget várnak; a forgatott oldalak hibásak. | Alkalmazz forgatási korrekciót (`ocr_engine.rotate(90)`) a ROI hozzáadása előtt. |
| **Zaj a háttérben** | Árnyékok vagy bélyegek összezavarják a modellt. | Előfeldolgozás egyszerű küszöböléssel (`cv2.threshold`) vagy zajszűrő szűrővel. |

Ezeknek a széljegyeknek a korai kezelése órákat takaríthat meg a későbbi hibakeresésben.

---

## Pro tippek valós projektekhez

- **Kötegelt feldolgozás:** Egy mappában lévő számlákon iterálj, dinamikusan számold ki a ROI‑t (pl. sablonfelismerés alapján), és az eredményeket CSV‑ben tárold.  
- **Sablon egyezés:** Ha több számla elrendezést kezelsz, tarts egy JSON térképet `template_id → ROI koordináták` formátumban. Válts ROI‑t egy gyors elrendezés‑osztályozó alapján.  
- **Párhuzamos végrehajtás:** Használd a `concurrent.futures.ThreadPoolExecutor`‑t, hogy több OCR példányt futtass egyszerre – nagyszerű nagy mennyiségű back‑office csővezetékekhez.  
- **Biztonsági szűrés:** A legtöbb OCR eredmény tartalmaz biztonsági pontszámot. Dobd el a 85 % alatti eredményeket, és jelöld őket manuális felülvizsgálatra.

---

## Összegzés

Mindent lefedtünk, ami ahhoz kell, hogy **ocr region of interest**, **load image for OCR**, **extract text from rectangle**, és végül **recognize text from invoice** segítségével megválaszold a klasszikus **how to extract amount** kérdést. A szkript kompakt, mégis elég rugalmas ahhoz, hogy különböző dokumentumformátumokhoz, nyelvekhez és OCR back‑ekhez igazodjon.

Miután elsajátítottad az alapokat, gondolkodj a munkafolyamat bővítésén: adj hozzá vonalkód‑olvasást, integráld egy PDF parserrel, vagy küldd el a kinyert összeget egy könyvelő API‑nak. A lehetőségek végtelenek, és egy jól definiált ROI‑val mindig gyorsabb, tisztább eredményeket kapsz.

Ha elakadsz, írj egy megjegyzést alul – jó OCR‑ozást!

![ocr region of interest example](https://example.com/ocr_roi_example.png "ocr region of interest example")


## Mit tanulj meg legközelebb?

- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}