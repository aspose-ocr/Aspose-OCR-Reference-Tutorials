---
category: general
date: 2026-03-18
description: Futtass OCR-t képen gyorsan Python segítségével. Tanuld meg, hogyan ismerj
  fel szöveget PNG-ből, tölts be képet OCR-hez, és nyerj ki szavakat a képből egy
  lépésről‑lépésre útmutatóban.
draft: false
keywords:
- run OCR on image
- recognize text from png
- python OCR example
- extract words from image
- load image for OCR
language: hu
og_description: Futtass OCR-t képen Python használatával. Ez az útmutató bemutatja,
  hogyan ismerhetünk fel szöveget PNG-ből, hogyan tölthetünk be képet OCR-hez, és
  hogyan nyerhetünk ki szavakat a képből egy teljes kódrészlettel.
og_title: OCR futtatása képen – Python útmutató
tags:
- OCR
- Python
- Image Processing
title: OCR futtatása képen – Teljes Python OCR példa
url: /hu/python-java/general/run-ocr-on-image-complete-python-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép OCR futtatása – Teljes Python OCR példa

Valaha is szükséged volt **run OCR on image** fájlok futtatására, de nem tudtad, hol kezdj? Nem vagy egyedül; sok fejlesztő szembesül ezzel, amikor először próbál szöveget kinyerni beolvasott dokumentumokból. Ebben az útmutatóban egy **Python OCR example**-t mutatunk be, amely lehetővé teszi **recognize text from PNG** fájlok, **load image for OCR**, és **extract words from image** bizalmi pontszámokkal – mindezt néhány sor kóddal.

Mindent lefedünk, amire szükséged lesz: a szükséges könyvtárat, hogyan állítsd be a motort, miért fontos minden lépés, és milyen lesz a kimenet. A végére képes leszel ezt a kódrészletet beilleszteni a saját projektedbe, és azonnal szöveget kinyerni bármely képről. Nincs felesleges információ, csak egy gyakorlati, futtatható megoldás.

## Amire szükséged lesz

- Python 3.8 vagy újabb telepítve  
- Az `ocrengine` csomag (vagy bármely könyvtár, amely `OcrEngine` osztályt biztosít). Telepítheted a `pip install ocrengine` paranccsal – módosítsd a nevet, ha más OCR könyvtárat, például `pytesseract`-ot használsz.  
- Egy képfájl (PNG, JPG, stb.), amelyet feldolgozni szeretnél – ebben az útmutatóban a `invoice.png`-t használjuk.  

Ennyi. Nincs nehéz függőség, nincs külső szolgáltatás, csak tiszta Python.

![run OCR on image példa, amely egy beolvasott számlát mutat](/images/run-ocr-on-image.png)

*Alt text: run OCR on image példa – beolvasott számla feldolgozása*

## 1. lépés – Az OCR könyvtár telepítése és importálása

Először is, hozzuk be az OCR motort a környezetünkbe, és importáljuk. Ha a hipotetikus `ocrengine` csomagot használod, az import így néz ki:

```python
# Install the package (run once in your terminal)
# pip install ocrengine

# Import the OCR engine class
from ocrengine import OcrEngine
```

**Miért fontos ez:**  
Az megfelelő osztály importálása hozzáférést biztosít a később hívott metódusokhoz, mint a `setImageFromFile` és a `recognize`. Ha kihagyod ezt a lépést, a Python `ModuleNotFoundError`-t dob, és már a kép betöltése előtt elakadsz.

## 2. lépés – OCR motor példány létrehozása

Most, hogy a könyvtár készen áll, szükségünk van egy motor objektumra, amely a konfigurációt és az állapotot tárolja a felismerési folyamat során.

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()
```

*Pro tip:* Néhány OCR motor lehetővé teszi a nyelvi modellek vagy DPI beállítások finomhangolását ebben a pontban. Egy alap **python OCR example** esetén az alapértelmezések rendben vannak, de ha alacsony felbontású beolvasásról van szó, érdemes itt módosítani őket.

## 3. lépés – A feldolgozni kívánt kép betöltése

A következő logikus lépés a **load image for OCR**. A motort a PNG (vagy bármely támogatott formátum) fájlútvonalára irányítod, amelyet elemezni szeretnél.

```python
# Step 3: Load the image you want to process
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice.png")
```

**Mi történik a háttérben?**  
A motor beolvassa a pixeladatokat, átalakítja egy olyan formátumba, amelyet a felismerő algoritmus megért, és belsőleg tárolja. Ha a fájlútvonal hibás, `FileNotFoundError`-t kapsz, ezért ellenőrizd, hogy a kép létezik-e.

## 4. lépés – A felismerő algoritmus futtatása

A kép betöltése után végre **run OCR on image**, hogy kinyerjük a szöveges tartalmat.

```python
# Step 4: Run the recognition algorithm to obtain results
ocr_result = ocr_engine.recognize()
```

Ebben a pontban a motor átvizsgálja a bitmapet, mintázat-illesztést alkalmaz, és egy objektumot ad vissza, amely minden felismert szót, sort és bizalmi metrikát tartalmaz.

## 5. lépés – A felismert szavak iterálása és a bizalom megjelenítése

Az OCR munkafolyamat leghasznosabb része, hogy lássuk **the confidence** minden kinyert tokennél. Ez megmutatja, mennyire biztos a motor az egyes szavakban, így alacsony bizalmi eredményeket szűrhetsz, ha szükséges.

```python
# Step 5: Iterate over each recognized word and display its text with confidence
for recognized_word in ocr_result.getWords():
    word_text = recognized_word.getText()
    confidence = recognized_word.getConfidence()   # 0‑100%
    print(f"Word: '{word_text}' – confidence: {confidence}%")
```

**Várt kimenet** (példa):

```
Word: 'Invoice' – confidence: 98%
Word: 'Number' – confidence: 95%
Word: ':' – confidence: 92%
Word: '2023-07-15' – confidence: 97%
Word: 'Total' – confidence: 96%
Word: ':' – confidence: 93%
Word: '$' – confidence: 88%
Word: '1,250.00' – confidence: 94%
```

Most pontosan láthatod, **what words were extracted from the image**, és mennyire megbízható minden egyes felismerés. Ez a **extract words from image** folyamat magja.

## Gyakori szélhelyzetek kezelése

### Mi van, ha a kép szürkeárnyalatos?

Néhány OCR motor jobban teljesít színes képekkel. Ha alacsony bizalmat látsz mindenhol, próbáld meg a PNG-t magas kontrasztú fekete‑fehér változatra konvertálni, mielőtt a motorba adod. A Pillow segíthet:

```python
from PIL import Image, ImageOps

img = Image.open("YOUR_DIRECTORY/invoice.png")
bw = ImageOps.grayscale(img).point(lambda x: 0 if x < 128 else 255, '1')
bw.save("YOUR_DIRECTORY/invoice_bw.png")
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice_bw.png")
```

### Több nyelv kezelése

Ha a dokumentumod tartalmaz angol és spanyol szöveget is, akkor **recognize text from PNG** egy többnyelvű modellel. A legtöbb motor lehetővé teszi a nyelvlista beállítását az inicializálás során:

```python
ocr_engine = OcrEngine(languages=["eng", "spa"])
```

### Alacsony bizalomú szavak szűrése

Néha csak a 90 % feletti bizalmi szintű szavakra van szükség. Egy gyors szűrő így néz ki:

```python
high_confidence_words = [
    w.getText()
    for w in ocr_result.getWords()
    if w.getConfidence() >= 90
]
print(high_confidence_words)
```

## Teljes, azonnal futtatható szkript

Mindent összegezve, itt egy egyetlen szkript, amelyet másolhatsz‑beilleszthetsz és azonnal futtathatsz (csak cseréld le a PNG útvonalát).

```python
# run_ocr_on_image.py
# -------------------------------------------------
# Complete Python OCR example: load image for OCR,
# run OCR on image, and extract words from image.
# -------------------------------------------------

# Install the library first:
# pip install ocrengine pillow   # pillow only needed for optional preprocessing

from ocrengine import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the target PNG (replace with your own file)
    image_path = "YOUR_DIRECTORY/invoice.png"
    ocr_engine.setImageFromFile(image_path)

    # 3️⃣ Run recognition
    ocr_result = ocr_engine.recognize()

    # 4️⃣ Print each word with its confidence
    print("\n--- OCR Results ---")
    for word in ocr_result.getWords():
        text = word.getText()
        conf = word.getConfidence()
        print(f"Word: '{text}' – confidence: {conf}%")

if __name__ == "__main__":
    main()
```

Futtasd a következővel:

```bash
python run_ocr_on_image.py
```

A konzolon meg kell jelennie a szavak és a bizalmi százalékok listájának, pontosan úgy, ahogy korábban láttad.

## Gyakran Ismételt Kérdések

**Működik ez JPG vagy TIFF fájlokkal?**  
Természetesen. A `setImageFromFile` metódus bármilyen formátumot elfogad, amelyet az alaprendszer képes dekódolni, így **run OCR on image** fájlokat is használhatsz JPG, TIFF, BMP stb. típusokban.

**Feldolgozhatok több képet egy ciklusban?**  
Igen. Csak tedd a betöltési és felismerési lépéseket egy `for` ciklusba a fájlútvonalak listáján. Ne feledd, hogy ha a könyvtár megköveteli, újra kell inicializálni a motort minden egyes képhez.

**Mi van, ha a szöveget egyetlen karakterláncban szeretném, nem szóként?**  
A legtöbb OCR eredményobjektum rendelkezik egy `getText()` metódussal, amely visszaadja a teljes dokumentumot. Példa:

```python
full_text = ocr_result.getText()
print(full_text)
```

## Következő lépések és kapcsolódó témák

Most, hogy tudod, hogyan **run OCR on image**, érdemes továbbgondolni:

- **Post‑processing**: Használj reguláris kifejezéseket a számlákból kinyert dátumok, összegek vagy azonosítók tisztításához.  
- **Batch processing**: Kombináld a szkriptet az `os.listdir()`-el, hogy teljes mappákat kezelj beolvasott dokumentumokból.  
- **Alternative libraries**: A `pytesseract` egy népszerű nyílt forráskódú opció; a munkafolyamat hasonló – csak cseréld le a motor hívásait.  
- **Exporting results**: Írd ki a kinyert szavakat és bizalmi pontszámokat CSV-be a további elemzéshez.  

Ezek a kiterjesztések közvetlenül az itt felépített alapra épülnek, lehetővé téve, hogy a nyers OCR adatokat hasznos információvá alakítsd.

---

### TL;DR

Bemutattunk egy tömör, **python OCR example**-t, amely megmutatja, hogyan **load image for OCR**, **run OCR on image**, és **extract words from image**, miközben a bizalmi értékeket is jelzi. A teljes szkript készen áll a futtatásra, és most már tudod alkalmazni bármely projekthez, amelynek **recognize text from PNG** (vagy más formátum) szüksége van. Próbáld ki, állítsd be a bizalmi küszöböt, és nézd meg, hogyan válik alkalmazásod szöveg‑érzékennyé percek alatt. Jó kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}