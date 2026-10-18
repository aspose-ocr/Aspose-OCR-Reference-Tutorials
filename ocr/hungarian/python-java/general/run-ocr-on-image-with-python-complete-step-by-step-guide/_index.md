---
category: general
date: 2026-06-06
description: Futtass OCR-t egy képen Python segítségével, és nézd meg a bizalmi pontszámokat.
  Tanuld meg, hogyan szűrd ki az alacsony bizalomú szavakat, állíts be küszöbértékeket,
  és kezeld a szélső eseteket.
draft: false
keywords:
- run OCR on image
- Python OCR tutorial
- OCR confidence threshold
- low‑confidence word detection
- image text extraction
language: hu
og_description: Futtass OCR-t képen Pythonban, vizsgáld meg a megbízhatósági szinteket,
  és szűrd ki az alacsony megbízhatóságú szavakat. Ez az útmutató végigvezet egy teljes,
  futtatható példán.
og_title: OCR futtatása képen Python segítségével – Teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  headline: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  name: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: Install and Import the OCR Engine
    text: First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box
      for many languages and gives you a confidence score per word.
  - name: Run OCR on the Image
    text: Now we actually **run OCR on image**. The `recognize_image` method from
      the original example is replaced with EasyOCR’s `readtext` call, which returns
      a list of `(bbox, text, confidence)` tuples.
  - name: Summarize Overall Confidence
    text: 'Unlike the earlier snippet that printed a single `confidence` attribute,
      EasyOCR gives a confidence per word. To get an overall sense, we’ll average
      them:'
  - name: List Low‑Confidence Words
    text: Now comes the part that directly answers the “list words whose confidence
      is below the desired threshold” requirement. We’ll set a **OCR confidence threshold**
      of 0.80 (80 %) by default, but you can adjust it.
  - name: Edge Cases & Variations
    text: 1. **Batch Processing** – If you need to **run OCR on image** files in bulk,
      wrap the above logic in a loop that iterates over a directory. 2. **Multiple
      Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine
      will detect both. 3. **Alternative Engines** – Want to try **pyte
  type: HowTo
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`)
      and then feed the PNG/JPEG into the script.
    question: Does this work with PDFs?
  - answer: 'Try image preprocessing: increase contrast, remove background noise,
      or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths`
      parameter you can tweak.'
    question: My confidence numbers are all low—what can I do?
  - answer: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter`
      where each row contains `text`, `confidence`, and bounding‑box coordinates.
    question: Can I export the results to CSV?
  - answer: 'EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed.
      Verify with `torch.cuda.is_available()` before running the script. --- ## Conclusion
      We’ve just **run OCR on image** using Python, inspected the overall confidence,
      and isolated any low‑confidence words that need a {{< /b'
    question: Is there a GPU‑accelerated version?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: OCR futtatása képen Python segítségével – Teljes lépésről lépésre útmutató
url: /hu/python-java/general/run-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR futtatása képen Python‑nal – Teljes lépés‑ről‑lépésre útmutató

Valaha is szükséged volt **OCR futtatására képen** fájlokon, de nem tudtad, hogyan nyerj megbízható szöveget belőlük? Nem vagy egyedül – sok fejlesztő szembesül ugyanazzal a problémával, amikor a kinyert szavak bizonytalanok, és a biztonsági pontszám rejtély marad.  

Ebben az útmutatóban egy működő megoldásba mélyedünk el: megmutatjuk, hogyan futtass OCR‑t képen, olvasd ki az általános biztonságot, és szűrd ki az alacsony biztonságú szavakat, amelyeket manuálisan kell ellenőrizni. A végére egy újrahasználható szkriptet kapsz, megérted, miért fontos minden sor, és tudni fogod, hogyan állítsd be a biztonsági küszöböt a saját projektjeidhez.

## Mit fed le ez a tutorial

Áttekintjük a teljes munkafolyamatot – a kép betöltésétől egy rendezett jelentés nyomtatásáig, amely a 80 % alatti biztonságú szavakat listázza. Útközben megvitatjuk:

* Egy megbízható OCR motor kiválasztását (használni fogjuk a **EasyOCR**‑t, egy népszerű Python OCR könyvtárat)  
* A `confidence` attribútum értelmezését, amely minden OCR eredményhez tartozik  
* Szavak szűrését egy egyedi **OCR confidence threshold**‑el  
* A szkript kiterjesztését kötegelt feldolgozáshoz vagy alternatív motorokhoz, mint a **pytesseract**  

Előzetes OCR tapasztalat nem szükséges, csak alapvető Python ismeret és egy működő környezet (Python 3.9+ ajánlott).  

Készen állsz, hogy a homályos képernyőképeket tiszta, kereshető szöveggé alakítsd? Kezdjünk bele.

---

## ## Hogyan futtass OCR‑t képen Python‑nal

A tutorial központja egy háromlépéses kódrészlet, amely tükrözi a már látott kódot. Alább minden sort külön bontunk, elmagyarázzuk a miértjét, majd egy teljes, másolás‑beillesztésre kész szkriptet adunk.

### 1. lépés: Telepítsd és importáld az OCR motort

Először győződj meg róla, hogy az OCR könyvtár elérhető. **EasyOCR** azonnal működik sok nyelven, és minden szóhoz biztonsági pontszámot ad.

```bash
pip install easyocr
```

```python
import easyocr  # The engine that will run OCR on image files
import os
```

*Miért EasyOCR?* Egy mélytanuló modellt tartalmaz, amely változatos adathalmazokon lett betanítva, így általában magasabb biztonsági értékeket kapsz, mint a régebbi Tesseract motor, különösen vegyes minőségű képeken.

> **Pro tip:** Ha korlátozott környezetben vagy (pl. egy kis Docker konténer), a `pytesseract` könnyebb lehet, de elveszítheted az EasyOCR által nyújtott modern pontosságot.

### 2. lépés: OCR futtatása a képen

Most ténylegesen **run OCR on image**. Az eredeti példában szereplő `recognize_image` metódus helyett az EasyOCR `readtext` hívását használjuk, amely egy `(bbox, text, confidence)` elemekből álló listát ad vissza.

```python
# Initialize the OCR reader for English (you can add more languages as needed)
reader = easyocr.Reader(['en'])

# Path to the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "mixed_quality.png")

# Perform OCR – this is the step where we run OCR on image
ocr_results = reader.readtext(image_path, detail=1, paragraph=False)
```

Az `ocr_results` minden eleme így néz ki:

```python
[
    ((x1, y1, x2, y2, x3, y3, x4, y4), "Detected text", 0.92),
    ...
]
```

A harmadik elem (`0.92` a példában) a biztonsági pontszám, amely 0‑tól 1‑ig terjed.

### 3. lépés: Az általános biztonság összegzése

Míg a korábbi kódrészlet egyetlen `confidence` attribútumot írt ki, az EasyOCR minden szóhoz ad biztonságot. Az általános kép érdekében átlagoljuk őket:

```python
# Extract just the confidence numbers
confidences = [item[2] for item in ocr_results]

# Compute the mean confidence (overall confidence)
overall_confidence = sum(confidences) / len(confidences) if confidences else 0

print(f"Overall confidence: {overall_confidence:.2%}")
```

*Miért átlagolunk?* Gyors egészségügyi ellenőrzést nyújt – ha az általános biztonság 70 % alá esik, valószínűleg javítanod kell a képet (jobb megvilágítás, előfeldolgozás stb.).

### 4. lépés: Alacsony biztonságú szavak listázása

Most jön a rész, amely közvetlenül a “list words whose confidence is below the desired threshold” követelményt teljesíti. Alapértelmezés szerint **OCR confidence threshold**‑et 0.80‑ra (80 %) állítjuk, de ezt módosíthatod.

```python
# Define the confidence threshold – tweak as needed
THRESHOLD = 0.80

print("\nLow‑confidence words:")
low_confidence_found = False
for bbox, text, conf in ocr_results:
    if conf < THRESHOLD:
        low_confidence_found = True
        print(f"  • '{text}' ({conf:.2%})")
if not low_confidence_found:
    print("  All words meet the confidence threshold.")
```

A ciklus kiírja minden olyan szót, amely nem érte el a küszöböt, a százalékos biztonságával együtt. Ez pontosan az eredeti `for recognized_word in recognition_result.words` ciklus analógja, de most az EasyOCR kimeneti formátumával működik.

---

## ## Az OCR biztonsági pontszámok megértése

A biztonság nem varázslatos szám; a modell becslése arról, mennyire biztos a konkrét transzkripcióban. Néhány fontos szempont:

| Helyzet | Tipikus biztonság | Mit tegyünk |
|-----------|-------------------|------------|
| Tiszta, nagy felbontású szken | 0.95 – 1.00 | Nincs további teendő |
| Enyhe elmosódás vagy egyenetlen megvilágítás | 0.80 – 0.94 | Fontold meg a kisebb előfeldolgozást (kontraszt növelése) |
| Erős zaj, elfordított szöveg | < 0.70 | Alkalmazz képelőfeldolgozást (kiegyenesítés, zajszűrés) vagy válts másik OCR motorra |

> **Figyelem:** Egyes nyelvek (pl. folyó kézírás) természetesen alacsonyabb pontszámokat adnak. Ennek megfelelően állítsd be a küszöböt.

### Szélsőséges esetek és variációk

1. **Kötegelt feldolgozás** – Ha **run OCR on image** fájlokat nagy mennyiségben kell feldolgozni, csomagold a fenti logikát egy ciklusba, amely egy könyvtár fájljait iterálja.  
2. **Több nyelv** – Adj meg egy listát, például `['en', 'fr']` a `easyocr.Reader`‑nek, és a motor mindkettőt felismeri.  
3. **Alternatív motorok** – Szeretnéd kipróbálni a **pytesseract**‑ot? Cseréld le a reader blokkot a következőre:

   ```python
   import pytesseract
   from PIL import Image

   img = Image.open(image_path)
   raw_text = pytesseract.image_to_string(img, output_type=pytesseract.Output.DICT)
   # raw_text['text'] contains the full string,
   # raw_text['conf'] holds per‑character confidence.
   ```

   Ezután össze kell gyűjtened a karakterek biztonságát szónként – egy kicsit több munka, de megoldható.

4. **Előfeldolgozási trükkök** – OpenCV szűrők (`cv2.threshold`, `cv2.GaussianBlur`) alkalmazása növelheti a biztonságot zajos szkenek esetén.  

---

## ## Teljes, futtatható szkript

Az alábbiakban a teljes Python fájl található, amelyet egyszerűen beilleszthetsz a projektedbe. Mentsd `ocr_report.py`‑ként, és futtasd `python ocr_report.py`‑vel. Győződj meg róla, hogy a kép útvonala valós fájlra mutat.

```python
#!/usr/bin/env python3
"""
run_ocr_on_image.py

A self‑contained script that:
  1. Runs OCR on an image using EasyOCR.
  2. Prints the overall confidence.
  3. Lists any words whose confidence falls below a configurable threshold.

Author: Your Name
Date: 2026‑06‑06
"""

import os
import easyocr

# --------------------------- Configuration --------------------------- #
IMAGE_DIR = "YOUR_DIRECTORY"          # <-- Change to your folder
IMAGE_NAME = "mixed_quality.png"      # <-- Change to your file name
THRESHOLD = 0.80                       # Confidence threshold (0‑1)

# --------------------------- Helper Functions ----------------------- #
def load_image_path():
    """Construct the absolute path to the target image."""
    return os.path.join(IMAGE_DIR, IMAGE_NAME)

def run_ocr(image_path):
    """Run OCR on the image and return detailed results."""
    reader = easyocr.Reader(['en'])
    return reader.readtext(image_path, detail=1, paragraph=False)

def compute_overall_confidence(results):
    """Return the mean confidence across all detected words."""
    if not results:
        return 0.0
    confidences = [item[2] for item in results]
    return sum(confidences) / len(confidences)

def report_low_confidence_words(results, threshold):
    """Print words whose confidence is below the given threshold."""
    low_conf = [(text, conf) for _, text, conf in results if conf < threshold]
    if not low_conf:
        print("All words meet the confidence threshold.")
    else:
        for text, conf in low_conf:
            print(f"Low‑confidence word: '{text}' ({conf:.2%})")

# --------------------------- Main Execution ------------------------ #
def main():
    image_path = load_image_path()
    if not os.path.isfile(image_path):
        print(f"❌ Image not found: {image_path}")
        return

    # Step 1: Run OCR on image
    ocr_results = run_ocr(image_path)

    # Step 2: Show overall confidence
    overall = compute_overall_confidence(ocr_results)
    print(f"Overall confidence: {overall:.2%}")

    # Step 3: List low‑confidence words
    print("\n--- Low‑confidence words (threshold: {0:.0%}) ---".format(THRESHOLD))
    report_low_confidence_words(ocr_results, THRESHOLD)

if __name__ == "__main__":
    main()
```

**Várható kimenet** (a számaid eltérhetnek):

```
Overall confidence: 78.45%

--- Low‑confidence words (threshold: 80%) ---
Low‑confidence word: 'recgnition' (62.13%)
Low‑confidence word: 'imgae' (57.90%)
```

Ha minden szó átmegy a 80 % küszöbön, akkor a barátságos “All words meet the confidence threshold.” üzenetet fogod látni.

---

## ## Gyakran Ismételt Kérdések (FAQ)

**Q: Működik ez PDF‑ekkel?**  
A: Nem közvetlenül. Először minden PDF oldalt alakíts át képpé (pl. a `pdf2image`‑vel), majd add a PNG/JPEG fájlt a szkriptnek.

**Q: A biztonsági számok mind alacsonyak – mit tehetek?**  
A: Próbálj meg képelőfeldolgozást: növeld a kontrasztot, távolítsd el a háttérzajt, vagy forgasd a képet vízszintes alapvonalra. Az EasyOCR egy `contrast_ths` paramétert is elfogad, amelyet finomhangolhatsz.

**Q: Exportálhatom az eredményeket CSV‑be?**  
A: Természetesen. Az alacsony‑biztonságú ciklus után írd ki az `ocr_results`‑t egy `csv.DictWriter`‑rel, ahol minden sor tartalmazza a `text`, `confidence` és a keretkoordinátákat.

**Q: Van GPU‑gyorsított változat?**  
A: Az EasyOCR automatikusan használja a CUDA‑t, ha kompatibilis GPU és a PyTorch telepítve van. Ellenőrizd a `torch.cuda.is_available()` függvénnyel a futtatás előtt.

---

## Következtetés

Most már **run OCR on image** Python‑nal, megvizsgáltuk az általános biztonságot, és elkülönítettük az alacsony biztonságú szavakat, amelyeket manuálisan kell felülvizsgálni.

## Mit érdemes még megtanulni?

A következő tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket és lépés‑ről‑lépésre magyarázatokat tartalmaz, hogy elsajátíthasd a további API funkciókat és alternatív megvalósítási megközelítéseket saját projektjeidben.

- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}