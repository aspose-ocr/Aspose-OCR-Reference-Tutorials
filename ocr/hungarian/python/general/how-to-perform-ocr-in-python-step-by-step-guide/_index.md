---
category: general
date: 2026-01-12
description: Hogyan végezzünk OCR-t és konvertáljuk gyorsan a képet szöveggé. Tanulja
  meg a speciális karakterek felismerését, a szöveg kinyerését a képből, és a kép
  betöltését OCR-hez egy teljes Python példával.
draft: false
keywords:
- how to perform OCR
- convert image to text
- recognize special characters
- extract text from image
- load image for OCR
language: hu
og_description: Hogyan végezzünk OCR-t Pythonban, alakítsuk át a képet szöveggé, és
  ismerjük fel a speciális karaktereket. Kövesd ezt a gyakorlati útmutatót a képek
  szövegének kinyeréséhez.
og_title: Hogyan végezzünk OCR-t Pythonban – Teljes útmutató
tags:
- OCR
- Python
- Image Processing
title: Hogyan végezzünk OCR-t Pythonban – Lépésről lépésre útmutató
url: /hu/python/general/how-to-perform-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk OCR-t Pythonban – Lépésről‑lépésre útmutató

Valaha szükséged volt **OCR végrehajtására** egy olyan képernyőképen, amely latin és cirill karaktereket egyaránt tartalmaz? Nem vagy egyedül. Sok projektben – legyen szó számlák digitalizálásáról, többnyelvű dokumentumok indexeléséről vagy kereshető archívum építéséről – **hogyan végezzünk OCR-t** gyorsan a legfontosabb kérdéssé válik.

Ebben az útmutatóban egy teljes, futtatható példán keresztül vezetünk végig, amely megmutatja, hogyan **képet szöveggé alakítás**, **speciális karakterek felismerése**, és **szöveg kinyerése a képből** egy egyszerű Python könyvtár segítségével. A végére egy azonnal futtatható szkriptet kapsz, amely betölti a képet OCR-hez, kezeli a többnyelvű tartalmat, és kiírja az eredményt.

## Amire szükséged lesz

- Python 3.8+ telepítve a gépeden.  
- `ocr` csomag (vagy bármely kompatibilis OCR könyvtár) telepítve a `pip install ocr` paranccsal.  
- Egy kép fájl (`multilingual.png`), amely latin és cirill glifeket egyaránt tartalmaz.  
- Alap szövegszerkesztő vagy IDE – VS Code, PyCharm, vagy akár egy egyszerű Notepad is megfelel.  

Ha nincs meg a `ocr` csomag, helyettesítheted `pytesseract`-tel néhány kisebb módosítással; az alapvető koncepciók változatlanok maradnak.

## 1. lépés: Az OCR könyvtár telepítése és importálása

Először is készítsük elő az OCR motorját. Importáljuk a könyvtárat, létrehozzuk a motor példányát, és beállítjuk a többnyelvű támogatást.

```python
# Install the library (run this once in your terminal)
# pip install ocr

import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: Enable language packs for Latin and Cyrillic
engine.set_languages(['eng', 'rus'])  # 'eng' = English, 'rus' = Russian
```

**Miért fontos ez:**  
A motor létrehozása az alap – nélküle később nem tudod **betölteni a képet OCR-hez**. A nyelvi csomagok engedélyezése biztosítja, hogy a motor helyesen felismerje az olyan karaktereket, mint a “Ŀ”, “Ҕ”, és “Ǣ”. Ha kihagyod ezt a lépést, torz kimenetet kapsz a nem latin írásrendszerekhez.

## 2. lépés: A többnyelvű szöveget tartalmazó kép betöltése

Most a motorra mutatunk a feldolgozni kívánt fájlra. Az útvonal lehet abszolút vagy relatív; csak győződj meg róla, hogy egy olvasható képre mutat.

```python
# Step 2: Load the image containing multilingual text
image_path = "YOUR_DIRECTORY/multilingual.png"  # replace with your actual path
engine.load_image(image_path)
```

> ![OCR példa](/images/ocr-example.png "OCR egy többnyelvű képen")

**Miért fontos ez:**  
A `load_image` hívás beolvassa a képpont adatokat a memóriába, előkészítve az OCR algoritmus számára. Ha a kép nagy, a motor automatikusan lecsökkentheti a felbontást; ezt később finomhangolhatod a `engine.set_max_resolution(3000)` paranccsal a nagy felbontású beolvasásokhoz.

## 3. lépés: A felismerési folyamat futtatása

Miután a motor előkészített és a kép betöltve, végre kinyerhetjük a szöveges tartalmat.

```python
# Step 3: Perform OCR recognition on the loaded image
result = engine.recognize()
```

**Miért fontos ez:**  
`recognize()` a háttérben futtatja a nehéz feladatot ellátó neurális hálót. Egy objektumot ad vissza, amely tartalmazza a nyers szöveget, a megbízhatósági pontszámokat, és akár a határoló dobozokat is, ha vizuális hibakereséshez szükséged van rájuk.

## 4. lépés: A felismert szöveg kiírása

Nézzük meg, mit talált a motor. Kiírjuk a szöveget a konzolra, de akár fájlba vagy adatbázisba is mentheted.

```python
# Step 4: Output the recognized text, which should include characters like “Ŀ”, “Ҕ”, “Ǣ”
print("=== OCR Result ===")
print(result.text)
```

### Várt kimenet

```
=== OCR Result ===
Hello, world! Ŀ is a Latin‑extended character.
Привет, мир! Ҕ is a Cyrillic character.
Special combo: Ǣ is a ligature.
```

Ha hasonlót látsz, gratulálok – sikeresen **képet szöveggé alakítás** és **speciális karakterek felismerése**.

## Gyakori buktatók kezelése

Még egy egyszerű szkript esetén is előfordulhatnak kisebb problémák. Az alábbiakban néhány gyakorlati tippet találsz a saját tapasztalataimból.

### 1. Hiányzó nyelvi csomagok

Ha kérdőjeleket (`?`) látsz a cirill betűk helyett, ellenőrizd, hogy a nyelvi csomagok telepítve vannak-e. Sok OCR motor esetén le kell tölteni a megfelelő `.traineddata` fájlokat, és a motor `tessdata` mappájába kell helyezni őket.

```python
# Example for pytesseract
import pytesseract
pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
# Ensure 'eng' and 'rus' data files exist in tessdata
```

### 2. Alacsony képminőség

Elmosódott vagy alacsony kontrasztú képek alacsony megbízhatósági pontszámot eredményeznek. Előfeldolgozhatod a képet OpenCV-vel:

```python
import cv2

# Load, convert to grayscale, and apply thresholding
raw = cv2.imread(image_path)
gray = cv2.cvtColor(raw, cv2.COLOR_BGR2GRAY)
_, thresh = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)

# Save a temporary cleaned image and feed it to the OCR engine
cv2.imwrite("cleaned.png", thresh)
engine.load_image("cleaned.png")
```

### 3. Nagy fájlok és memóriahasználat

Egy 10 MB-os fénykép feldolgozása memóriát terhelhet. Használd a `engine.set_max_image_size(2000)` parancsot a felbontás korlátozásához, vagy oszd fel a képet csempékre, és OCR-eld őket külön-külön.

### 4. Határoló dobozok rögzítése

Ha ki szeretnéd emelni, hogy hol jelenik meg egy-egy szó (hasznos UI rétegekhez), használd a `result.boxes`-t:

```python
for box in result.boxes:
    print(f"Word: {box.text} – Coordinates: {box.x0},{box.y0},{box.x1},{box.y1}")
```

## Teljes szkript – Egykattintásos végrehajtás

Mindent összevonva, itt egy egyetlen fájl, amelyet futtathatsz `python ocr_demo.py`-ként. Tartalmaz hibakezelést, opcionális előfeldolgozást és magyarázó megjegyzéseket a tisztaság kedvéért.

```python
#!/usr/bin/env python3
"""
Complete OCR demo: load image, recognize multilingual text,
and print results. Works with the generic 'ocr' library.
"""

import os
import sys
import ocr

def main(image_path: str):
    # Verify the image exists
    if not os.path.isfile(image_path):
        sys.exit(f"Error: File not found – {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()
    engine.set_languages(['eng', 'rus'])          # load language packs
    engine.set_max_image_size(2500)               # limit memory usage

    # Load the image
    try:
        engine.load_image(image_path)
    except Exception as e:
        sys.exit(f"Failed to load image: {e}")

    # Perform recognition
    try:
        result = engine.recognize()
    except Exception as e:
        sys.exit(f"OCR failed: {e}")

    # Output the text
    print("\n=== OCR Result ===")
    print(result.text)

    # Optional: display confidence scores
    if hasattr(result, "confidence"):
        avg_conf = sum(result.confidence) / len(result.confidence)
        print(f"\nAverage confidence: {avg_conf:.1%}")

if __name__ == "__main__":
    # Replace with your actual image path or pass as CLI argument
    img = sys.argv[1] if len(sys.argv) > 1 else "YOUR_DIRECTORY/multilingual.png"
    main(img)
```

Futtasd a következővel:

```bash
python ocr_demo.py path/to/multilingual.png
```

Ugyanazt a kimenetet kell látnod, mint korábban, ami megerősíti, hogy sikeresen **szöveg kinyerése a képből**.

## Összegzés

Áttekintettük, **hogyan végezzünk OCR-t** Pythonban a kezdetektől a befejezésig: a könyvtár telepítése, egy kép betöltése, a többnyelvű tartalom felismerése, és a leggyakoribb edge case-ek kezelése. Ezt az útmutatót követve most már **képet szöveggé alakítás**, **speciális karakterek felismerése**, és **szöveg kinyerése a képből** a saját projektjeidben – többé nem kell kézzel másolnod.

Mi a következő? Próbálj ki a következőket:

- További nyelvi csomagok hozzáadása (pl. `spa` a spanyolhoz).  
- Az eredmények JSON formátumba exportálása további feldolgozáshoz.  
- Az OCR lépés integrálása egy Flask API-ba, hogy más szolgáltatások is hívhassák.

Ha bármilyen furcsaságba ütközöl, a legtöbb OCR könyvtár körüli közösség aktív – keress rá a „ocr library language pack installation” kifejezésre, vagy hagyj megjegyzést alább. Boldog kódolást, és élvezd a képek kereshető szöveggé alakítását!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}