---
category: general
date: 2026-06-25
description: Hogyan használjunk OCR-t Pythonban – tanulja meg, hogyan töltsön be képet
  OCR-hez, hogyan ismerje fel a szöveget egy területen, és hogyan vonja ki gyorsan
  a terület szövegét.
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: hu
og_description: Hogyan használjunk OCR-t Pythonban – lépésről lépésre útmutató egy
  kép betöltéséhez, szöveg felismeréséhez egy meghatározott területen, és a számla
  számának kinyeréséhez.
og_title: 'Hogyan használjuk az OCR Python-t: Kép betöltése és a régió szövegének
  kinyerése'
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 'Hogyan használjuk az OCR-t Pythonban: Kép betöltése és a régió szövegének
  kinyerése'
url: /hu/python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjuk az OCR-t Pythonban: Kép betöltése és a régió szövegének kinyerése

**How to use OCR in Python** egyszerűbb, mint gondolnád. Volt már, hogy egy beolvasott számlát néztél, és azon tűnődtél, hogyan lehet csak a számlaszámot kinyerni anélkül, hogy az egész oldalt feldolgoznád? Nem vagy egyedül – sok fejlesztő találkozik ezzel a problémával, amikor először kísérletezik az optikai karakterfelismeréssel. Ebben az útmutatóban végigvezetünk a kép betöltésén OCR-hez, egy téglalap definiálásán, a szöveg felismerésén abban a régióban, és végül a régió szövegének kinyerésén. A végére egy kész‑futtatható szkriptet kapsz, amely izolálja a szükséges szövegrészt.

> *Pro tip:* Ha PDF-ekkel dolgozol, először minden oldalt alakíts képpé – a legtöbb OCR könyvtár a PNG/JPEG formátumot kezeli a legjobban.

## Amire szükséged lesz

- Python 3.8+ (az ajánlott a legújabb stabil kiadás)  
- Olyan OCR könyvtár, amely egy `OcrEngine` osztályt biztosít (pl. **ocr** a `pip install ocr-lib`‑ből)  
- Egy minta kép – itt a `invoice.png` fájlt használjuk, amelyet egy általad irányított mappában helyezel el  
- Alapvető ismeretek a téglalapokról (x, y, szélesség, magasság)  

Nincs nehéz függőség, nincs GPU szükség – csak egyszerű CPU munka, ami hordozhatóvá teszi.

---

## Hogyan használjuk az OCR-t: Motor inicializálása (1. lépés)

Mielőtt bármilyen szöveget olvasni tudnánk, szükségünk van egy OCR motor példányra. Gondolj rá úgy, mint egy agyra, amely a képpontmintákat elemzi.

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Miért fontos:* A motor inicializálása betölti a nyelvi modelleket és beállítja az alapértelmezett konfigurációkat. Ennek a lépésnek a kihagyása kivételt dob, amint meghívod a `recognize_region`‑t.

## Kép betöltése OCR-hez (2. lépés)

Miután a motor készen áll, egy képet adunk neki. A könyvtár `Image.load` metódusa kezeli a gyakori formátumokat és normalizálja a bitmapet.

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

Ha a fájl nem található, a Python `FileNotFoundError`‑t dob. Győződj meg róla, hogy az útvonal abszolút vagy a szkript munkakönyvtárához relatív.  

*Különleges eset:* Néhány OCR motor szürkeárnyalatos képet vár. Ha pontatlanságot észlelsz, először konvertáld a képet:

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

## Szöveg felismerése a régióban (3. lépés)

A régió definiálása azt jelenti, hogy megmondod a motor számára, *hol* keressen. A `Rectangle` lebegőpontos értékeket használ al-pixel pontossághoz, ami hasznos lehet nagy felbontású beolvasásoknál.

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – a téglalap bal‑felső sarka (pixelben)  
- **width, height** – a doboz mérete  

Kíváncsi lehetsz, hogyan találod meg ezeket a számokat. Egy gyors módszer, ha megnyitod a képet bármely szerkesztőben (pl. GIMP vagy Paint.NET), és a kijelölő eszközzel leolvasod a koordinátákat.  

*Miért ne OCR-ölnéd az egész oldalt?* A terület korlátozása csökkenti a zajt, felgyorsítja a feldolgozást, és drámaian javítja a pontosságot kis mezők, például számlaszámok esetén.

## Hogyan nyerjük ki a régió szövegét (4. lépés)

Miután a régió be van állítva, kérd meg a motort, hogy csak azt a szeletet ismerje fel. Az eredményobjektum tartalmazza a nyers szöveget és a megbízhatósági pontszámokat.

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

Ha az OCR motor több nyelvet támogat, megadhatsz egy opcionális nyelvkódot:

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*Gyakori hibaforrás:* Néhány motor szólistát ad vissza egyetlen karakterlánc helyett. Ilyen esetben fűzd össze őket:

```python
text = " ".join(region_result.words)
```

## A kinyert számlaszám kiírása (5. lépés)

Végül írd ki – vagy tárold – a kinyert szöveget. A karakterláncot tovább is feldolgozhatod, hogy eltávolítsd a felesleges szóközöket vagy nem numerikus karaktereket.

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

A szkript futtatása egy helyesen beállított téglalappal valami ilyesmit kell, hogy eredményezzen:

```
Invoice number: 20231578
```

Ha szemét karaktereket kapsz, ellenőrizd újra a téglalap koordinátáit, vagy fontold meg a kép felbontásának növelését.

## Teljes működő példa

Összeállítva mindent, itt egy önálló szkript, amelyet másolhatsz és futtathatsz:

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

Mentsd a fájlt `extract_invoice.py` néven, cseréld le a `YOUR_DIRECTORY`‑t a tényleges mappára, majd futtasd:

```bash
python extract_invoice.py
```

A konzolon meg kell jelennie a számlaszámnak.

## Gyakran Ismételt Kérdések

**Q: Mi van, ha a számlaszám egy díszes betűtípussal van nyomtatva?**  
A: A legtöbb modern OCR motor széles betűtípus-skálát kezel, de a pontosságot növelheted egy egyedi nyelvi modell betanításával vagy a kép előfeldolgozásával (pl. küszöb szűrő alkalmazásával).

**Q: Kinyerhetek több mezőt egyszerre?**  
A: Természetesen. Definiálj egy listát `Rectangle` objektumokból – egyet mezőnként –, és iterálj rajtuk, minden eredményt egy szótárban tárolva.

**Q: Működik ez többoldalas PDF-ekkel?**  
A: Először minden oldalt konvertálj képpé (például a `pdf2image` vagy hasonló használatával), majd alkalmazd ugyanazt a régió‑alapú kinyerést oldalanként.

## Összegzés

Ebben az útmutatóban bemutattuk, **hogyan használjuk az OCR-t** Pythonban egy kép betöltéséhez, egy adott régióban a szöveg felismeréséhez és a régió szövegének kinyeréséhez – tökéletes számlaszámok, rendelési azonosítók vagy bármilyen kis adatdarab beolvasott dokumentumokból való kinyeréséhez. Az érdeklődési terület izolálásával gyorsaságot, pontosságot és kevesebb utófeldolgozási nehézséget nyersz.

Készen állsz a következő lépésre? Próbáld meg kiterjeszteni a szkriptet, hogy **kép betöltése OCR-hez** egy kötegelt számlák mappájából történjen, vagy kísérletezz a **szöveg felismerése a régióban** különböző mezőkkel, például dátumokkal és összegekkel. Ugyanaz a minta érvényes – csak módosítsd a téglalap koordinátáit.

Ha bármilyen problémába ütköztél, vagy van ötleted a fejlesztésre, hagyj egy megjegyzést alább. Boldog kódolást, és legyen az OCR folyamatod mindig pontos!

## Mit érdemes legközelebb megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Szöveg kinyerése képből Aspose OCR-rel – Lépésről‑lépésre útmutató](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Hogyan nyerjünk ki szöveget képből téglalapok előkészítésével OCR-ben](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Hogyan használjuk az AspOCR-t: Kép előfeldolgozása OCR szűrőkkel .NET-hez](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}