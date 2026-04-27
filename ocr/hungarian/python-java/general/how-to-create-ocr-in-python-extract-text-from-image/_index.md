---
category: general
date: 2026-04-26
description: Hogyan készítsünk OCR-t gyorsan és megbízhatóan. Tanulja meg, hogyan
  lehet szöveget kinyerni képből, betölteni a képet OCR-hez, és futtatni az OCR-t
  PNG-n egy egyéni szótárral.
draft: false
keywords:
- how to create OCR
- extract text from image
- extract text scanned document
- load image for OCR
- run OCR on png
language: hu
og_description: Hogyan készítsünk OCR-t Pythonban és vonjunk ki szöveget képből. Ez
  az útmutató bemutatja, hogyan töltsünk be képet OCR-hez, hogyan futtassuk az OCR-t
  PNG-n, és hogyan használjunk egy egyéni szótárat.
og_title: Hogyan készítsünk OCR-t Pythonban – Gyors szövegkivonás
tags:
- OCR
- Python
- Image Processing
title: Hogyan készítsünk OCR-t Pythonban – Szöveg kinyerése képből
url: /hu/python-java/general/how-to-create-ocr-in-python-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan hozzunk létre OCR-t Pythonban – Lépésről‑lépésre útmutató

Gondoltad már valaha, **hogyan hozzunk létre OCR-t**, amely képes beolvasni a beolvasott PDF-jeidet, képernyőképeidet vagy kézzel írt jegyzeteidet? Nem vagy egyedül. Sok valós projektben szükségünk van *szöveg kinyerésére képfájlokból*, de a kész megoldások gyakran elakadhatnak a szakterület‑specifikus szavaknál.  

Ebben az útmutatóban egy teljes, futtatható példát látsz, amely betölt egy képet OCR-hez, alkalmaz egy egyedi szótárat, és végül **futtat OCR-t PNG** fájlokon. A végére képes leszel bármilyen képről szöveget kinyerni, és a motorot a saját terminológiádhoz igazítani.

## Amit ez az útmutató lefed

* A kis, de erőteljes `aocr` csomag telepítése (vagy bármely kompatibilis könyvtár).  
* Egy **egyedi szótár** konfigurálása, hogy a `aspocorp` vagy `licensekey` kifejezések fel legyenek ismerve.  
* **Kép betöltése OCR-hez**, legyen az PNG, JPEG vagy egy beolvasott PDF oldal.  
* Az OCR folyamat futtatása és az eredmény kiírása.  

Nincs külső dokumentációs hivatkozás, csak egy önálló megoldás, amelyet ma másolhatsz és futtathatsz.

### Előfeltételek

* Python 3.8 vagy újabb (a kód f‑stringeket használ).  
* Alapvető ismeretek a parancssorral – néhány `pip install` parancsot kell beírnod.  
* Egy képfájl (`technical_doc.png` a példában), amelyet valahol elhelyezel, ahonnan hivatkozhatsz.  

Ha megfelelsz ezeknek a három pontnak, már indulhatsz.  

---

## 1. lépés: Az OCR könyvtár telepítése

Először is szükségünk van egy OCR motorra, amely támogatja a programozható konfigurációs objektumot. A `aocr` csomag egy könnyű réteg egy natív OCR motor körül, és jól működik demókhoz.

```bash
# Install the library (run once)
pip install aocr
```

> **Pro tipp:** Ha Windows-on vagy és fordítási hibát kapsz, próbáld a `pip install aocr‑binary` parancsot, amely előre lefordított kerekeket (wheels) tartalmaz.

### Miért telepítsük ezt a könyvtárat?

`aocr` közvetlen hozzáférést biztosít egy `config` objektumhoz, ahol beilleszthetünk egy **egyedi szótárat**. Ez a titkos összetevő a pontosság javításához szűkebb szókészleteken.

---

## 2. lépés: OCR motor példány létrehozása és egyedi szótár hozzáadása

Most elindítjuk a motort, és megmondjuk, mely szavakat tekintse ismertnek.

```python
from aocr import OcrEngine

# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Provide a custom dictionary to improve recognition of domain‑specific terms
ocr_engine.config.custom_dictionary = [
    "aspocorp",      # our company's brand name
    "ocrengine",    # the library name itself
    "licensekey"    # a common field in our contracts
]
```

### Miért fontos egy egyedi szótár

A standard OCR modellek általános korpuszokon vannak betanítva. Amikor a modell a “aspocorp” szót látja, előfordulhat, hogy “aspo corp”‑ra bontja, vagy teljesen elhagyja a betűket. Egy egyedi lista betáplálásával a felismerőt a szükséges pontos helyesírás felé irányítjuk, ezzel drasztikusan csökkentve az utófeldolgozási munkát.

---

## 3. lépés: A feldolgozni kívánt kép betöltése

Itt jön a **kép betöltése OCR-hez**. A `Image.load` metódus egy útvonal karakterláncot fogad, és automatikusan meghatározza a fájltípust.

```python
import aocr

# Step 3: Load the image that contains the text you want to extract
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/technical_doc.png")
```

> **Különleges eset:** Ha a forrásod egy többoldalas PDF, először konvertáld minden oldalt PNG‑re (pl. a `pdf2image`‑vel), és egyesével add át a motorhoz.

### Tippek a jobb képminőséghez

* Tartsd a felbontást legalább 300 dpi‑n.  
* Győződj meg róla, hogy a kép függőleges; ha szükséges, forgasd a `Pillow`‑al.  
* A színes beolvasásokat konvertáld szürkeárnyalatosra a zaj csökkentése érdekében.

---

## 4. lépés: OCR folyamat futtatása a PNG fájlon

A motor konfigurálása és a kép betöltése után végül **futtatjuk az OCR-t a PNG‑en**.

```python
# Step 4: Run the OCR process
ocr_result = ocr_engine.process()
```

A `process()` hívás egy objektumot ad vissza, amely tartalmazza a felismert szöveget, a biztonsági pontszámokat és a szavak körülhatároló dobozait.

---

## 5. lépés: A felismert szöveg kiírása

A legegyszerűbb módja annak, hogy lásd, mit talált a motor, a `text` attribútum kiírása.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### Várt kimenet

Ha a `technical_doc.png` a *“The Aspocorp licensekey expires on 2025‑12‑31.”* mondatot tartalmazza, a konzolnak a következőt kell mutatnia:

```
The Aspocorp licensekey expires on 2025-12-31.
```

Vedd észre, hogy az egyedi szótár megőrizte a márkanevet – amit egy alap OCR eltorzíthatott volna.

---

## Teljes működő példa (másolás‑beillesztés kész)

Az alábbiakban az egész szkript található, amelyet elmenthetsz `run_ocr.py`‑ként. Csak cseréld ki a helyőrző útvonalat a saját képed helyére.

```python
# run_ocr.py
# -------------------------------------------------
# Complete example showing how to create OCR,
# load an image, apply a custom dictionary,
# and extract text from a PNG file.
# -------------------------------------------------

from aocr import OcrEngine
import aocr

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Add domain‑specific words
    ocr_engine.config.custom_dictionary = [
        "aspocorp",
        "ocrengine",
        "licensekey"
    ]

    # 3️⃣ Load the image you want to process
    #    (Make sure the path points to a real file)
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    ocr_engine.image = aocr.Image.load(image_path)

    # 4️⃣ Run the OCR engine
    ocr_result = ocr_engine.process()

    # 5️⃣ Print the extracted text
    print("=== Extracted Text ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

Futtasd a terminálból:

```bash
python run_ocr.py
```

A konzolon meg kell jelennie a kinyert szövegnek, pontosan úgy, ahogy az előző példában láttad.

---

## Gyakran Ismételt Kérdések (GYIK)

| Kérdés | Válasz |
|----------|--------|
| **Kinyerhetek szöveget egy beolvasott PDF‑ből?** | Igen. Először konvertáld minden oldalt PNG‑re (vagy TIFF‑re), majd add át a képeket ugyanabban a szkriptben. |
| **Mi van, ha a képem JPEG a PNG helyett?** | A `Image.load` metódus natívan támogatja a JPEG, BMP, TIFF és PNG formátumokat. Csak változtasd meg a fájlkiterjesztést. |
| **Hogyan javíthatom a pontosságot alacsony kontrasztú beolvasásokon?** | Előfeldolgozás `Pillow`‑rel – növeld a kontrasztot, alkalmazz binarizációt, vagy használd az `opencv`‑t a dőlés korrigálásához. |
| **Van mód arra, hogy minden szóhoz kapjak biztonsági pontszámot?** | `ocr_result` tartalmazza a `words` elemet – minden szó rendelkezik `confidence` attribútummal, amelyet iterálhatsz. |
| **Futtathatom ezt egy fej nélküli szerveren?** | Természetesen. Az `aocr` nem igényel GUI függőségeket, így tökéletes CI pipeline‑okhoz. |

---

## Következő lépések és kapcsolódó témák

Most, hogy tudod, **hogyan hozzunk létre OCR-t** és **szöveget nyerjünk ki képfájlokból**, érdemes tovább kutatni:

* **Előfeldolgozási technikák** – a `load image for OCR` csak az első lépés; használj `opencv`‑t a zajcsökkentéshez vagy élesítéshez.  
* **Kötegelt feldolgozás** – iterálj egy PNG‑k könyvtárán, hogy kereshető archívumot hozz létre.  
* **Többnyelvű támogatás** – adj hozzá nyelvi csomagokat a motorhoz, ha francia vagy német dokumentumokat kell olvasnod.  
* **Integráció Elasticsearch‑szel** – indexeld a kinyert szöveget a teljes szöveges kereséshez a beolvasott anyagok között.  

Ezek a kiegészítések mind a most bemutatott alapmintára épülnek, így a váltás zökkenőmentes lesz.

---

## Összegzés

Néhány perc alatt megválaszoltuk, **hogyan hozzunk létre OCR-t**, amely megbízhatóan **kivonja a szöveget képfájlokból**, különösen PNG‑kből, és megmutattuk, hogyan **tölts be képet OCR-hez**, alkalmazz egy **egyedi szótárat**, és **futtass OCR-t PNG‑n** külső szolgáltatások nélkül.  

Próbáld ki a szkriptet, finomítsd a szótárat a saját zsargonodhoz, és egy erős alapot kapsz bármilyen dokumentum‑digitalizációs projekthez.  

Ha bármilyen problémába ütköztél, írj egy megjegyzést alább – szívesen segítek. És ne felejtsd el megosztani a sikertörténeteidet; a közösség a valós példákból tanul a legjobban.  

**Készen állsz a papírmunka automatizálására?** Szerezd meg a kódot, igazítsd a saját igényeidhez, és kezdj el ma pixelből kereshető szöveget varázsolni!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}