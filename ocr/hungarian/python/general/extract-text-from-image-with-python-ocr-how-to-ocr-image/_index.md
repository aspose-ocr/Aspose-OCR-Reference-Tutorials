---
category: general
date: 2026-05-31
description: Szöveg kinyerése képből a Python aocr könyvtárával. Tanulja meg, hogyan
  végezzen OCR-t egy képen, hogyan töltsön be képet OCR-hez, és hogyan ismerjen fel
  speciális karaktereket néhány sorban.
draft: false
keywords:
- extract text from image
- recognize special characters
- convert image to text
- how to ocr image
- load image for ocr
language: hu
og_description: Szöveg kinyerése képből a Python aocr könyvtárával. Ez az útmutató
  bemutatja, hogyan kell OCR-t végezni a képen, betölteni a képet OCR-hez, és gyorsan
  felismerni a speciális karaktereket.
og_title: Szöveg kinyerése képből Python OCR-rel – Hogyan OCR-eljünk képet
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Extract text from image using Python's aocr library. Learn how to OCR
    image, load image for OCR, and recognize special characters in just a few lines.
  headline: Extract Text from Image with Python OCR – How to OCR Image
  type: TechArticle
- description: Extract text from image using Python's aocr library. Learn how to OCR
    image, load image for OCR, and recognize special characters in just a few lines.
  name: Extract Text from Image with Python OCR – How to OCR Image
  steps:
  - name: 5.1 Low‑Resolution Images
    text: 'If the image is under 150 dpi, the OCR accuracy can drop dramatically.
      A quick fix is to upscale before feeding it to aocr:'
  - name: 5.2 Incorrect Language Detection
    text: 'aocr auto‑detects language, but you can force a specific script for better
      results:'
  - name: 5.3 Noise and Background Patterns
    text: 'A noisy background can confuse the model. Pre‑process with OpenCV to binarize:'
  type: HowTo
- questions:
  - answer: Not directly. Convert PDF pages to images first (e.g., using `pdf2image`)
      and then feed each image to aocr.
    question: Does this work on PDFs?
  - answer: For typical 300 dpi scans, aocr processes a page in ~0.3 s on a modern
      laptop—roughly twice as fast as vanilla Tesseract with default settings.
    question: How fast is aocr compared to Tesseract?
  - answer: 'Absolutely. Wrap the `main` function in a loop over `Path(folder).glob("*.png")`
      and collect results in a CSV. --- ## Conclusion You now have a solid, end‑to‑end
      workflow to **extract text from image** using Python’s aocr library. From loading
      the file to printing Unicode output, every step is expla'
    question: Can I batch‑process a folder of images?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Szöveg kinyerése képből Python OCR-rel – Hogyan OCR-eljük a képet
url: /hu/python/general/extract-text-from-image-with-python-ocr-how-to-ocr-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép szövegének kinyerése Python OCR-rel – Hogyan OCR-eljünk képet

Valaha is szükséged volt **kép szövegének kinyerésére**, de nem tudtad, melyik könyvtár kezeli a különös szimbólumokat, mint a “Ł”, “Ž”, vagy “ß”? Nem vagy egyedül. Sok valós projektben – gondolj beolvasott számlákra, többnyelvű táblákra vagy történelmi dokumentumokra – a **különleges karakterek felismerése** döntő lehet a használható adathalmaz és a zsákutca között.

A jó hír? Néhány Python sorral és a könnyű **aocr** csomaggal bármilyen képet kereshető szöveggé alakíthatsz. Az alábbiakban egy teljes, azonnal futtatható szkriptet láthatsz, valamint a *miért* magyarázatát minden lépésnek, hogy ne csak másolj‑beilleszd, hanem valóban megértsd, mi történik.

## Amiről szól ez a bemutató

- A **aocr** könyvtár telepítése és importálása  
- Kép betöltése OCR-hez (a gyakori buktatókkal együtt)  
- A motor futtatása a **kép szöveggé konvertálásához**  
- Az eredmény kiírása és a speciális karakterek kezelése  
- Az alapfolyamat kibővítése többnyelvű támogatásra és hibakezelésre  

A útmutató végére képes leszel **kép szövegének kinyerésére** bármely nyelven, és tudni fogod, hogyan finomhangold a folyamatot, ha az alapbeállítások nem elegendőek.

## Előfeltételek

| Követelmény | Miért fontos |
|-------------|--------------|
| Python 3.8+ | az aocr modern típusdefiníciókat használ |
| `pip` hozzáférés | a könyvtár telepítéséhez |
| Minta kép (pl. `multilingual.png`) | ezzel mutatjuk be a speciális karaktereket |
| Alapvető ismeretek a virtuális környezetekről (opcionális) | a függőségek tisztán tartása |

Nincs szükség nehéz külső eszközökre, mint a Tesseract – a **aocr** egy gyors neurális motort csomagol, amely azonnal működik.

---

## 1. lépés: Az aocr könyvtár telepítése

Először nyiss egy terminált (vagy az IDE konzolját), és futtasd:

```bash
pip install aocr
```

*Pro tipp:* Ha több projektet kezelsz egyszerre, előbb hozz létre egy virtuális környezetet:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # macOS/Linux
.\ocr-env\Scripts\activate    # Windows
pip install aocr
```

Ez elkülöníti az OCR függőségeket a rendszer többi részétől – ami később rengeteg fejfájást megspórol.

---

## 2. lépés: Kép betöltése OCR-hez

Miután a csomag készen áll, **betölteni kell a képet OCR-hez**. Az `OcrEngine` osztály egy fájl elérési útját várja, ezért győződj meg róla, hogy a kép létezik és olvasható.

```python
import aocr

# Step 2: Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Step 2b: Point to your image file (adjust the path as needed)
image_path = r"YOUR_DIRECTORY/multilingual.png"
ocr_engine.load_image(image_path)
```

> **Miért fontos:**  
> - A `load_image` gyors ellenőrzést végez (fájl létezése, támogatott formátum).  
> - A nyers string (`r"..."`) használata elkerüli a véletlen escape‑karakter hibákat Windows útvonalaknál.  
> - Ha a kép hatalmas, az aocr automatikusan lecsökkenti a méretét, hogy a memóriahasználat ésszerű maradjon.  

Ha `FileNotFoundError` hibát kapsz, ellenőrizd újra az útvonalat, és győződj meg róla, hogy a fájlkiterjesztés PNG, JPEG vagy BMP.

---

## 3. lépés: OCR végrehajtása – Kép szöveggé konvertálása

A memóriában lévő képpel a következő hívás ténylegesen **felismeri a speciális karaktereket**, és Unicode karakterláncot ad vissza.

```python
# Step 3: Run the OCR engine
recognized_text = ocr_engine.recognize()
```

A háttérben az aocr egy könnyű konvolúciós‑rekurrens hálózatot futtat, amely többnyelvű adathalmazokon lett betanítva. Ezért a cirill, latin‑kiterjesztett és még néhány ritka glif is helyesen jelenik meg.

---

## 4. lépés: Kinyert szöveg megjelenítése

Végül nyomtassuk ki az eredményt. A kimenet tartalmazni fog minden karaktert, amelyet a motor dekódolt, beleértve a makacs diakritikus jeleket is.

```python
# Step 4: Show what we extracted
print("=== OCR RESULT ===")
print(recognized_text)
```

**Minta kimenet** (a tényleges eredmény a kép tartalmától függ):

```
=== OCR RESULT ===
Łąka žužuҖß – multilingual test string
```

*Kép példa:*  
![Kép szövegének kinyerése – minta kimenet](https://example.com/ocr-output.png "Kép szövegének kinyerése – minta kimenet")

> **Megjegyzés:** A `print` hívás alapértelmezés szerint UTF‑8 kódolást használ a modern Pythonban, így a speciális karaktereknek a legtöbb terminálban helyesen kell megjelenniük. Ha torz kimenetet látsz, állítsd a konzolt UTF‑8-ra, vagy írd a sztringet fájlba `encoding='utf-8'` paraméterrel.

---

## 5. lépés: Szélsőséges esetek és gyakori buktatók kezelése

### 5.1 Alacsony felbontású képek

Ha a kép 150 dpi alatti, az OCR pontossága drámaian csökkenhet. Egy gyors megoldás a felméretezés a aocr-ba való betáplálás előtt:

```python
from PIL import Image

img = Image.open(image_path)
img = img.resize((img.width * 2, img.height * 2), Image.LANCZOS)
img.save("upscaled.png")
ocr_engine.load_image("upscaled.png")
```

### 5.2 Hibás nyelvfelismerés

Az aocr automatikusan felismeri a nyelvet, de jobb eredményért kényszerítheted egy adott írásrendszerre:

```python
ocr_engine.set_language("rus")   # forces Cyrillic detection
```

A támogatott nyelvkódok például `eng`, `deu`, `fra`, `rus`, `spa` stb.

### 5.3 Zaj és háttérminták

A zajos háttér összezavarhatja a modellt. Előfeldolgozhatod OpenCV-vel binarizálásra:

```python
import cv2

raw = cv2.imread(image_path, cv2.IMREAD_GRAYSCALE)
_, thresh = cv2.threshold(raw, 127, 255, cv2.THRESH_BINARY | cv2.THRESH_OTSU)
cv2.imwrite("clean.png", thresh)
ocr_engine.load_image("clean.png")
```

---

## Teljes szkript – Egy‑kattintásos megoldás

Az alábbi **teljes, futtatható példa** minden részt összekapcsol. Mentsd `ocr_demo.py` néven, majd futtasd `python ocr_demo.py` paranccsal.

```python
# ocr_demo.py
# -------------------------------------------------
# Complete example: extract text from image using aocr
# -------------------------------------------------

import aocr
from pathlib import Path
import sys

def main(image_path: str):
    # Verify the file exists early – gives a nicer error message
    if not Path(image_path).is_file():
        sys.exit(f"❌ File not found: {image_path}")

    # 1️⃣ Create OCR engine
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Load the image (you can also call preprocess_image() here)
    ocr_engine.load_image(image_path)

    # Optional: force language if you know it (uncomment)
    # ocr_engine.set_language("eng")

    # 3️⃣ Run OCR – this is where we **convert image to text**
    recognized_text = ocr_engine.recognize()

    # 4️⃣ Output – includes special characters like Ł, Ž, Җ, ß
    print("\n=== OCR RESULT ===")
    print(recognized_text)

if __name__ == "__main__":
    # Example usage: python ocr_demo.py multilingual.png
    if len(sys.argv) != 2:
        sys.exit("Usage: python ocr_demo.py <path-to-image>")
    main(sys.argv[1])
```

Futtatás módja:

```bash
python ocr_demo.py YOUR_DIRECTORY/multilingual.png
```

A konzolon meg kell jelennie a kinyert karaktereknek, ezzel bizonyítva, hogy sikeresen **kép szövegét kinyerted** és **a speciális karaktereket felismered**.

---

## Gyakran Ismételt Kérdések

**K: Működik ez PDF‑ekkel?**  
V: Nem közvetlenül. Előbb konvertáld a PDF oldalakat képekké (pl. `pdf2image` használatával), majd add őket az aocr‑nak.

**K: Milyen gyors az aocr a Tesseract‑hoz képest?**  
V: Átlagos 300 dpi‑es beolvasásoknál az aocr egy oldalt ~0,3 s‑ben dolgoz fel egy modern laptopon – körülbelül kétszer gyorsabban, mint a Tesseract alapbeállításokkal.

**K: Batch‑feldolgozhatok egy mappát képekkel?**  
V: Természetesen. Csomagold a `main` függvényt egy ciklusba, amely a `Path(folder).glob("*.png")`‑t iterálja, és az eredményeket CSV‑be gyűjtheted.

---

## Összegzés

Most már egy szilárd, vég‑től‑végig működő munkafolyamatod van a **kép szövegének kinyerésére** a Python aocr könyvtár segítségével. A fájl betöltésétől a Unicode kimenet kiírásáig minden lépést részleteztünk, így könnyen testre szabhatod saját projektjeidhez – legyen szó számla‑olvasó szolgáltatásról vagy többnyelvű dokumentumarchívumról.

A következő kapcsolódó témákat érdemes felfedezni:

- **convert image to text** PDF‑ekhez (használd a `pdf2image` + OCR kombinációt)  
- **recognize special characters** kézírásos jegyzetekben (próbáld ki az `ocr_engine.set_dpi(600)` beállítást)  
- **load image for OCR** web‑API‑ban (Flask + aocr)  

Próbáld ki, finomítsd a nyelvi beállításokat, és nézd meg, hogyan válik adataid azonnal kereshetővé. Van kérdésed vagy egy izgalmas felhasználási eseted? Írj kommentet alul – jó kódolást!

## Mit érdemes még megtanulni?

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}