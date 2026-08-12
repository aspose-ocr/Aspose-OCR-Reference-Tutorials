---
category: general
date: 2026-08-12
description: Futtass OCR-t a képen Python és az Aspose AI használatával, hogy szöveget
  nyerj ki a képből, és javítsd az OCR pontosságát egy helyesírás-ellenőrző utófeldolgozóval.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from image
- OCR text correction
- improve OCR accuracy
- load image for OCR
language: hu
lastmod: 2026-08-12
og_description: Futtass OCR-t egy képen Pythonban, és azonnal kinyerheted a szöveget
  a képből, miközben az OCR pontosságát javítod az Aspose AI utófeldolgozással.
og_image_alt: Diagram showing the run OCR on image workflow in Python
og_title: Kép OCR futtatása Pythonban – teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Run OCR on image using Python and Aspose AI to extract text from image
    and improve OCR accuracy with a spell‑checking post‑processor.
  headline: Run OCR on image with Python – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- Image Processing
title: OCR futtatása képen Python segítségével – lépésről lépésre útmutató
url: /hu/python/general/run-ocr-on-image-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR futtatása képen Python‑ban – lépésről‑lépésre útmutató

Ha **OCR‑t kell futtatnod képfájlokon** Pythonban, ez az útmutató végigvezet a teljes munkafolyamaton. Megtanulod, hogyan **nyerj ki szöveget a képből**, alkalmazz **OCR szövegkorrekciót**, és **javítsd az OCR pontosságát** néhány sor kóddal.

A beolvasott dokumentumok, nyugták vagy képernyőképek gyakran zajos szöveget eredményeznek. Egy helyesírás‑ellenőrző utófeldolgozó csatolásával a nyers OCR kimenetet tiszta, kereshető tartalommá alakíthatod anélkül, hogy külön eszközre váltanál. Ez a tutorial mindent lefed, ami szükséges – a kép betöltésétől a javított eredmény megjelenítéséig.

## Előfeltételek

Mielőtt elkezdenéd, győződj meg róla, hogy:

* Python 3.9 vagy újabb telepítve van.
* Hozzáférésed van az Aspose.OCR és Aspose.AI Python csomagokhoz (vagy azok megfelelő nyílt‑forrású csomagjaihoz).
* Van egy mintakép (pl. `sample.png`) egy ismert könyvtárban.
* Alapvető ismereteid vannak a Python függvényekről és az objektum‑orientált kódról.

A szükséges könyvtárak telepíthetők pip‑pel:

```bash
pip install aspose-ocr aspose-ai
```

> **Pro tipp:** Használj virtuális környezetet (`python -m venv .venv`), hogy a függőségek izoláltak maradjanak.

## 1. lépés: OCR futtatása képen – hozd létre a motor példányt

Az első lépés egy `OcrEngine` objektum létrehozása. Ez az objektum tartalmazza az OCR motor konfigurációját, és módszereket biztosít a képkezeléshez és a felismeréshez.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine with default settings
ocr_engine = OcrEngine()
```

A motor egyszeri létrehozása és többszöri újrahasználata különböző képeken csökkenti az indítási költséget, és biztosítja a beállítások konzisztenciáját a munkamenet során.

## 2. lépés: Kép betöltése OCR‑hez

Mielőtt a felismerés megtörténhet, a motoron meg kell adni, melyik képet elemezze. A `load_image` metódus egy fájlútvonalat vagy bináris adatfolyamot fogad.

```python
# Provide the full path to your image file
image_path = "YOUR_DIRECTORY/sample.png"
ocr_engine.load_image(image_path)
```

> **Miért fontos ez:** A kép helyes betöltése az alapja a pontos OCR‑nek. Egy nagy felbontású kép (300 dpi vagy magasabb) általában **javítja az OCR pontosságát**, mivel a motor tisztábban tudja megkülönböztetni a karaktereket.

## 3. lépés: Szöveg kinyerése a képből – alapvető felismerés végrehajtása

Miután a kép betöltődött, meghívhatod a `recognize()`‑t, hogy egy eredményobjektumot kapj. Az eredmény tartalmazza a nyers szöveget, a megbízhatósági pontszámokat, és opcionálisan a szavak körvonalait.

```python
# Run the OCR process
plain_result = ocr_engine.recognize()   # returns a Result object

# The raw OCR output is accessible via the .text attribute
print("Raw OCR output:")
print(plain_result.text)
```

Ekkor már sikeresen **OCR‑t futtattál képen**, és kinyerted a nyers karaktereket. Azonban a szöveg hibás írásjeleket tartalmazhat, különösen alacsony minőségű beolvasások esetén.

## 4. lépés: OCR szövegkorrekció – helyesírás‑ellenőrző csatolása utófeldolgozásként

Az Aspose AI rugalmas utófeldolgozó csővezetéket biztosít. Egy egyedi helyesírás‑ellenőrző beillesztésével javíthatod a tipikus OCR hibákat (pl. „l” vs. „1”, „O” vs. „0”).

```python
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker   # your own implementation

# Initialize the AI engine and set the post‑processor
ai_engine = AsposeAI()
ai_engine.set_post_processor(MySpellChecker())

# Run the post‑processor on the plain OCR result
corrected_result = ai_engine.run_postprocessor(plain_result)
```

**Hogyan működik a helyesírás‑ellenőrző:** A `MySpellChecker`‑nek implementálnia kell egy `process(text: str) -> str` metódust. Ennek belsejében használhatsz olyan könyvtárakat, mint a `pyspellchecker` vagy a `symspellpy`, hogy a valószínűtlen szóösszetételeket szótár‑ellenőrzött alternatívákkal helyettesítsd.

```python
# Example implementation (very simple)
from spellchecker import SpellChecker

class MySpellChecker:
    def __init__(self):
        self.spell = SpellChecker()

    def process(self, text: str) -> str:
        corrected = []
        for word in text.split():
            corrected.append(self.spell.correction(word))
        return " ".join(corrected)
```

## 5. lépés: Eredeti és javított OCR szöveg megjelenítése

Végül hasonlítsd össze a nyers és a javított kimeneteket. Ez segít ellenőrizni, hogy a **OCR szövegkorrekció** valóban **javította-e az OCR pontosságát** a saját esetedben.

```python
print("\nOriginal :", plain_result.text)
print("Corrected:", corrected_result.text)
```

### Várható kimenet

```
Original : Th1s is a s4mpl3 rec3pt with som3 err0rs.
Corrected: This is a simple receipt with some errors.
```

A javított sor azt mutatja, hogy a helyesírás‑ellenőrző lecserélte a gyakori OCR félreolvasásokat (`Th1s` → `This`, `s4mpl3` → `simple`, `rec3pt` → `receipt`, `som3` → `some`, `err0rs` → `errors`).

## 6. lépés: OCR pontosság javítása – legjobb gyakorlatok ellenőrzőlistája

Még az utófeldolgozás mellett is növelheted az OCR motor kiindulási minőségét:

| Ellenőrzőlista elem | Miért segít |
|---------------------|--------------|
| **Használj nagy felbontású képeket (≥300 dpi)** | Több pixeladat csökkenti a karakterek homályosságát. |
| **Konvertáld a színes képeket szürkeárnyalatúra** | Eltávolítja a színzajt, ami összezavarhatja a motort. |
| **Alkalmazz kép kiegyenesítést** | Egyenesíti a ferde szöveget, megakadályozva a sortörés hibákat. |
| **Állítsd be a nyelvet/locale‑t explicit módon** | Irányítja a felismerőt a megfelelő karakterkészlet felé. |
| **Engedélyezd a nyelvi modellt** (ha a könyvtár támogatja) | Kontextus‑érzékeny előrejelzéseket biztosít, tovább **javítva az OCR pontosságát**. |

Ezeket az előfeldolgozó lépéseket megvalósíthatod Pillow vagy OpenCV segítségével, mielőtt a képet átadnád a `ocr_engine`‑nek.

```python
from PIL import Image, ImageOps
import cv2
import numpy as np

def preprocess_image(path: str) -> str:
    # Load with Pillow, convert to grayscale, and increase contrast
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)

    # Save a temporary preprocessed file
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

# Use the preprocessor
preprocessed_path = preprocess_image(image_path)
ocr_engine.load_image(preprocessed_path)
```

## Teljes futtatható szkript

Mindent összegezve, az alábbi szkript készen áll a másolás‑beillesztésre egy `run_ocr.py` nevű fájlba, majd futtatásra.

```python
# run_ocr.py
from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker
from PIL import Image, ImageOps

def preprocess_image(path: str) -> str:
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load and preprocess the image
    raw_path = "YOUR_DIRECTORY/sample.png"
    processed_path = preprocess_image(raw_path)
    ocr_engine.load_image(processed_path)

    # 3️⃣ Perform basic OCR
    plain_result = ocr_engine.recognize()

    # 4️⃣ Run OCR text correction
    ai_engine = AsposeAI()
    ai_engine.set_post_processor(MySpellChecker())
    corrected_result = ai_engine.run_postprocessor(plain_result)

    # 5️⃣ Show both results
    print("\nOriginal :", plain_result.text)
    print("Corrected:", corrected_result.text)

if __name__ == "__main__":
    main()
```

A szkript futtatása kiírja az eredeti és a javított szöveget, megerősítve, hogy sikeresen **OCR‑t futtattál képen**, **kivontad a szöveget a képből**, és **javítottad az OCR pontosságát** **OCR szövegkorrekció** segítségével.

## Összegzés

Most már tudod, hogyan **futtass OCR‑t képen** Pythonban, hogyan nyerd ki a nyers szöveget, és hogyan alkalmazz egy utófeldolgozó helyesírás‑ellenőrzőt a tisztább eredményekért. A **OCR pontosság javítása** ellenőrzőlista követésével ezt a munkafolyamatot nyugtákra, számlákra, személyi igazolványokra vagy bármely beolvasott dokumentumra is testre szabhatod.

### Mi a következő?

* Fedezd fel a **nyelvspecifikus szótárakat** a többnyelvű OCR‑hez.
* Integráld a csővezetéket egy adatbázissal vagy keresőindexszel (pl. Elasticsearch), hogy a kinyert szöveg kereshető legyen.
* Cseréld le az egyszerű helyesírás‑ellenőrzőt egy neurális nyelvi modellre (pl. GPT‑alapú korrekció) a még magasabb pontosság érdekében.

Nyugodtan kísérletezz különböző kép‑előfeldolgozási technikákkal, különböző utófeldolgozókkal vagy alternatív OCR motorokkal. Az alapminta – **OCR futtatása képen → szöveg kinyerése a képből → OCR szövegkorrekció → OCR pontosság javítása** – változatlan marad, erős alapot biztosítva bármely dokumentum‑digitalizációs projekthez.


## Mit kellene legközelebb megtanulnod?


A következő tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}