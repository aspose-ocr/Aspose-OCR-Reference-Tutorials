---
category: general
date: 2026-06-19
description: Végezzen OCR-t képen a Python OCR könyvtárával. Tanulja meg, hogyan lehet
  szöveget észlelni a képen, szöveget felismerni JPEG-ből, és hatékonyan kinyerni
  a szöveget a beolvasott képről.
draft: false
keywords:
- perform OCR on image
- recognize text from jpeg
- detect text from image
- extract text from scanned image
- load image for OCR
language: hu
og_description: Végezzen OCR-t képen Python segítségével, és nyerjen ki szöveget beolvasott
  fájlokból. Ez az útmutató lépésről lépésre végigvezet a képek betöltésén, kiegyenesítésén
  és a szöveg felismerésén.
og_title: OCR végrehajtása képen Pythonban – Teljes szövegkinyerési útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  headline: Perform OCR on Image in Python – Full Text Extraction Guide
  type: TechArticle
- description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  name: Perform OCR on Image in Python – Full Text Extraction Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed (the example uses the `ocr` package available via
      `pip install ocr-lib` – replace with your actual library name). - Basic familiarity
      with Python functions and virtual environments. - An image file (JPEG, PNG,
      TIFF) you want to process; we’ll use `skewed_page.jpg` as a placeh'
  - name: Recognize Text from JPEG vs PNG
    text: 'Both formats are supported, but JPEG compression can introduce artifacts
      that confuse the engine. If you notice frequent mis‑recognitions, try converting
      the JPEG to PNG first:'
  - name: Detect Text from Image with Multiple Languages
    text: 'If your document mixes English and Spanish, set a multilingual mode:'
  - name: Extract Text from Scanned PDFs
    text: 'For PDFs, you need to rasterize each page into an image first. Libraries
      like `pdf2image` make this painless:'
  type: HowTo
- questions:
  - answer: Absolutely. The library works without a GUI; just ensure the necessary
      native binaries (e.g., Tesseract) are installed on the server.
    question: Can I run this on a headless server?
  - answer: Consider adding a sharpening filter before `engine.recognize`. Many OCR
      libraries expose `image_preprocessing.sharpen = True` or you can use OpenCV’s
      `cv2.GaussianBlur` in reverse.
    question: What if the image is blurry?
  - answer: 'Yes. Wrap `perform_ocr` in a loop over a list of file paths, ## What
      Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
      - [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
      - [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: Does the script support batch processing?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: OCR végrehajtása képen Pythonban – Teljes szövegkinyerési útmutató
url: /hu/python-java/general/perform-ocr-on-image-in-python-full-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép OCR végrehajtása Pythonban – Teljes szövegkinyerési útmutató

Valaha is szükséged volt **OCR végrehajtására képfájlokon**, de a kód rejtélyesnek tűnt? Nem vagy egyedül. Akár egy kupac beolvasott nyugtát szeretnél kereshető PDF‑vé alakítani, akár egy JPEG‑ből szeretnél feliratokat kinyerni egy adat‑tudományi projekthez, a szöveg felismerése JPEG‑ekből és más formátumokból ma már elengedhetetlen képesség minden fejlesztő számára.

Ebben a bemutatóban egy teljes, futtatható példán keresztül mutatjuk be, hogyan **detektálj szöveget képfájlokból**, **nyerd ki a szöveget beolvasott képdokumentumokból**, és még **tölts be képet OCR‑hez** néhány sorban. A végére egy stabil, termelés‑kész kódrészletet kapsz, amelyet egyszerűen beilleszthetsz a saját projektjeidbe – hiányzó importok nélkül, homályos „lásd a dokumentációt” hivatkozások nélkül.

## Mit fogsz építeni

- Egy apró Python‑szkriptet, amely létrehoz egy OCR‑motort, engedélyezi az automatikus kiegyenesítést, betölti a JPEG‑et (vagy bármely támogatott formátumot), és kiírja a felismert szöveget.
- Magyarázatokat arra, **miért** fontos minden beállítás, nem csak arra, **hogyan** kell beírni.
- Tippeket többoldalas PDF‑ek, nem‑angol nyelvek és gyakori buktatók, például elmosódott beolvasások kezelésére.

### Előfeltételek

- Python 3.8+ telepítve (a példa a `ocr` csomagot használja, amely a `pip install ocr-lib` paranccsal érhető el – cseréld le a saját könyvtárad nevére).
- Alapvető ismeretek a Python függvényekről és a virtuális környezetekről.
- Egy képfájl (JPEG, PNG, TIFF), amelyet feldolgozni szeretnél; a példában `skewed_page.jpg` a helyettesítő név.

> **Pro tipp:** Windows rendszeren futtasd a terminált rendszergazdaként az OCR‑könyvtár telepítésekor, hogy elkerüld a jogosultsági problémákat.

---

## OCR végrehajtása képen – Beállítás és konfiguráció

Az első dolog, amire szükséged van, egy tiszta OCR‑motor példány. Gondolj rá úgy, mint a művelet agyára; megfelelő konfiguráció nélkül még a legélesebb kép is értelmetlen szöveget ad vissza.

```python
# Step 1: Import the OCR library and create an engine
import ocr

engine = ocr.OcrEngine()
# Set the recognition language – English works for most cases
engine.language = ocr.Language.English
```

**Miért fontos:**  
Az `engine.language` beállítása szűkíti a karakterkészletet, amelyet az OCR‑motor elvár, ez drámaian növeli a pontosságot. Ha kihagyod, a motor kitalálja, gyakran félreolvassa az egyszerű szavakat.

---

## Automatikus kiegyenesítés engedélyezése – Döntött beolvasások javítása

A beolvasott oldalak ritkán tökéletesen síkak. Egy enyhe dőlés megzavarhatja a karakterszegmentálást, a „Hello” helyett „H3llo” jelenik meg. Az `auto_deskew` jelző elvégzi a nehéz munkát helyetted.

```python
# Step 2: Turn on automatic deskew to straighten tilted images
engine.image_preprocessing.auto_deskew = True
```

**Szélsőséges eset:** Ha tudod, hogy a képeid már egyenesek, a deskew letiltása néhány milliszekundummal csökkentheti a feldolgozási időt – hasznos, ha több ezer oldalt kell batch‑feladatban kezelni.

---

## Kép betöltése OCR‑hez – JPEG, PNG, TIFF támogatás

Most ténylegesen **betöltjük a képet OCR‑hez**. Az `ocr.Image.load` metódus rugalmas; bármely támogatott raszteres formátum útvonalát elfogadja.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/skewed_page.jpg"
image = ocr.Image.load(image_path)
```

> **Miért kulcsfontosságú ez a lépés:** A könyvtár beolvassa a fájlt egy belső bitmap‑be, szükség esetén színteret konvertál. Ennek kihagyása vagy egy nyers bájtfolyam átadása `FileNotFoundError`‑t vagy, rosszabb esetben, csendes, üres eredményt eredményez.

Ha kifejezetten **szöveget szeretnél felismerni JPEG** fájlokból, csak győződj meg róla, hogy a fájlkiterjesztés `.jpeg` vagy `.jpg`. Ugyanez a hívás működik PNG (`.png`) vagy TIFF (`.tif`) esetén módosítás nélkül.

---

## OCR végrehajtása képen – Motor futtatása

Miután a motor előkészítve és a kép a memóriában van, itt az ideje **OCR végrehajtásának a képen**. Ez az egyetlen sor végzi a nehéz munkát: előfeldolgozás, szegmentálás, osztályozás és szövegösszeállítás.

```python
# Step 4: Run OCR and capture the result object
result = engine.recognize(image)
```

**Mi történik a háttérben?**  
- A motor alkalmazza a deskew transzformációt (ha engedélyezve van).  
- Egy neurális hálózatot vagy Tesseract backendet futtat a karakterek azonosítására.  
- Végül a karaktereket szavakká és sorokká fűzi, egy gazdag `result` objektumot visszaadva.

---

## Szöveg kinyerése beolvasott képből – Eredmények megjelenítése

Az utolsó lépés **szöveg kinyerése beolvasott képből** és annak kiírása. A `result.text` attribútum tartalmazza a tiszta szöveges reprezentációt.

```python
# Step 5: Print the detected text to the console
print("Detected text:")
print(result.text)
```

A tipikus kimenet például:

```
Detected text:
Invoice #12345
Date: 2023‑09‑01
Total: $1,234.56
Thank you for your business!
```

Ha az OCR‑motor nem talál karaktereket, a `result.text` egy üres string lesz. Ilyenkor ellenőrizd a kép minőségét, vagy fontold meg a `engine.confidence_threshold` tulajdonság módosítását (ha a könyvtárad támogatja).

---

## Gyakori variációk kezelése

### Szöveg felismerése JPEG‑ből vs PNG‑ből

Mindkét formátum támogatott, de a JPEG tömörítés artefaktusokat hozhat létre, amelyek megzavarhatják a motort. Ha gyakran előfordulnak hibás felismerések, próbáld meg a JPEG‑et először PNG‑re konvertálni:

```python
from PIL import Image
Image.open(image_path).save("temp.png", format="PNG")
image = ocr.Image.load("temp.png")
```

### Szöveg detektálása több nyelven

Ha a dokumentum keveri az angolt és a spanyolt, állíts be többnyelvű módot:

```python
engine.language = ocr.Language.English | ocr.Language.Spanish
```

A motor ekkor mindkét ábécét figyelembe veszi a felismerés során.

### Szöveg kinyerése beolvasott PDF‑ekből

PDF‑ek esetén először minden oldalt rasterizálni kell képpé. Az olyan könyvtárak, mint a `pdf2image`, ezt egyszerűvé teszik:

```python
from pdf2image import convert_from_path

pages = convert_from_path("document.pdf", dpi=300)
for i, page_image in enumerate(pages):
    image = ocr.Image.from_pil(page_image)   # assuming the library accepts a PIL image
    result = engine.recognize(image)
    print(f"Page {i+1} text:")
    print(result.text)
```

---

## Teljes működő példa

Az alábbiakban a teljes szkript látható, amelyet egyszerűen másolj be egy `ocr_demo.py` fájlba. Tartalmaz hibakezelést és egy kis segédfüggvényt a futási idő mérésére.

```python
import ocr
import time
import sys
from pathlib import Path

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a given image file and return the extracted text.
    Handles auto‑deskew and basic error reporting.
    """
    if not Path(image_path).exists():
        sys.exit(f"❌ Error: File not found – {image_path}")

    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.image_preprocessing.auto_deskew = True

    try:
        image = ocr.Image.load(image_path)
    except Exception as e:
        sys.exit(f"❌ Failed to load image: {e}")

    start = time.time()
    result = engine.recognize(image)
    elapsed = time.time() - start

    if not result.text.strip():
        print("⚠️ No text detected. Try a higher‑resolution image or adjust preprocessing.")
    else:
        print(f"✅ OCR completed in {elapsed:.2f}s")
        print("Detected text:")
        print(result.text)

    return result.text

if __name__ == "__main__":
    # Replace with the path to your JPEG/PNG/TIFF file
    perform_ocr("YOUR_DIRECTORY/skewed_page.jpg")
```

**Várható kimenet** (tiszta beolvasás esetén):

```
✅ OCR completed in 0.87s
Detected text:
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

---

## Gyakran Ismételt Kérdések

**K: Futtatható ez egy fej nélküli szerveren?**  
V: Természetesen. A könyvtár GUI nélkül is működik; csak győződj meg róla, hogy a szükséges natív binárisok (pl. Tesseract) telepítve vannak a szerveren.

**K: Mi a teendő, ha a kép elmosódott?**  
V: Fontold meg egy élesítő szűrő hozzáadását a `engine.recognize` előtt. Sok OCR‑könyvtárban elérhető az `image_preprocessing.sharpen = True`, vagy használhatod az OpenCV `cv2.GaussianBlur` visszafelé alkalmazását.

**K: Támogatja a szkript a kötegelt feldolgozást?**  
V: Igen. Csak csomagold be a `perform_ocr`‑t egy ciklusba, amely egy fájlútvonal‑listát dolgoz fel,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}