---
category: general
date: 2026-03-18
description: Végezzen OCR-t a képen, és nyerje ki a kézzel írt szöveget egy fényképről.
  Tanulja meg, hogyan konvertáljon kézzel írt képet, hogyan nyerjen ki szöveget JPG-ből,
  és hogyan ismerje fel a szöveget egy fényképről.
draft: false
keywords:
- perform OCR on image
- convert handwritten image
- extract text from jpg
- extract handwritten text
- recognize text from photo
language: hu
og_description: Képen OCR-t végezve kézzel írott szöveget nyer ki egy fényképről.
  Ez az útmutató bemutatja, hogyan konvertáljon kézzel írott képet, és hogyan ismerje
  fel a szöveget JPG fájlokból.
og_title: OCR végrehajtása képen – Teljes kézírásos szöveg útmutató
tags:
- OCR
- Python
- Handwriting Recognition
title: OCR végrehajtása képen – Kézírásos kép átalakítása szöveggé
url: /hu/python/general/perform-ocr-on-image-convert-handwritten-image-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Képen történő OCR – Teljes körű kézírásos szövegkivonás

Szükséged volt már **képen történő OCR** végrehajtására, de nem tudtad, hogy a motor képes‑e olvasni a kusza kézírást? Nem vagy egyedül. Sok valós alkalmazásban – gondolj a költségnyugta‑szkennerekre vagy a jegyzetkészítő segédeszközökre – előfordulnak karcolt fényképek, amelyeket egyszerű szöveggé kell alakítani.  

Ebben az útmutatóban megmutatjuk, hogyan **konvertálj kézírásos képfájlokat**, **nyerd ki a szöveget jpg‑ből**, és akár **szöveget is ismerj fel fénykép‑folyamokból** egy apró, Python‑szerű könyvtárral, az `ocr`‑rel. A végére egy kész‑futtatható szkriptet kapsz, amely minden szót kiemel egy kézírásos jegyzetből, bármilyen ingatag is legyen a toll.

## Amire szükséged lesz

- Python 3.8+ (a kód bármely friss interpreteren működik)
- A feltételezett `ocr` csomag – telepítsd a `pip install ocr-lib` paranccsal (cseréld le a tényleges csomagnévre)
- Egy tiszta fénykép egy kézírásos jegyzetről, mentve `note.jpg`‑ként (vagy bármely más képfájlformátumban)
- Egy kis adag kíváncsiság – nincs szükség haladó ML háttérre

Ennyi. Nincs külső szolgáltatás, nincs API‑kulcs, csak egy helyi motor, amely **képen történő OCR**‑t tud végezni.

![képen történő OCR képernyőképe](example.png)

*Alt szöveg: képen történő OCR képernyőképe, amely egy kódszerkesztőben lévő OCR‑szkriptet mutat.*

## Lépés‑ről‑lépésre megvalósítás

Az alábbiakban a folyamatot kisebb egységekre bontjuk. Minden címsor tartalmaz egy kulcsszót, hogy gyorsan átfuthasd, és minden blokk elmagyarázza, **miért** csináljuk, amit csinálunk – nem csak **mit**.

### 1. lépés: Az OCR könyvtár telepítése és ellenőrzése

Mielőtt **képen történő OCR**‑t hajtanál végre, a könyvtárnak jelen kell lennie a környezetedben. Nyiss egy terminált és futtasd:

```bash
pip install ocr-lib
```

> **Pro tipp:** Ha virtuális környezetben dolgozol (erősen ajánlott), előbb aktiváld azt. Így a függőségek rendezettek maradnak, és elkerülöd a verzióütközéseket.

A telepítés után ellenőrizzük, hogy a Python be tudja‑e importálni a csomagot:

```python
try:
    import ocr
    print("OCR library loaded successfully.")
except ImportError as e:
    raise SystemExit("Failed to import ocr library. Did you run pip install?") from e
```

Ha a sikerüzenetet látod, készen állsz a **kézírásos kép** adat konvertálására.

### 2. lépés: Motorpéldány létrehozása és kézírásos mód kiválasztása

A legtöbb OCR motor alapértelmezésben nyomtatott szöveg felismerésére van beállítva. Mivel **kézírásos szöveget** akarunk **kivonni**, explicit módon át kell állítanunk a módot. Ez a lépés kulcsfontosságú, mert a kézírás gyakran más előfeldolgozást igényel (például vonalak simítása).

```python
# Step 2: Initialize the OCR engine
engine = ocr.OcrEngine()

# Tell the engine we’re dealing with handwriting
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

print("Engine configured for handwritten recognition.")
```

*Miért fontos:* A kézírásos karakterek mérete és dőlésszöge nagyon változó lehet. A `RecognitionMode.HANDWRITTEN` beállításával a motor egy, kézírásos mintákon tanított modellt használ, ami drámaian növeli a pontosságot.

### 3. lépés: A feldolgozni kívánt fénykép betöltése

Most már ténylegesen **képen történő OCR**‑t hajtunk végre. A `load_image` metódus elfogad egy elérési utat vagy fájlszerű objektumot. Bemutatásként egy JPEG‑et töltünk be, de ugyanaz a hívás működik PNG, BMP vagy akár PDF‑oldalak esetén is.

```python
# Step 3: Load the image file (replace the path with yours)
image_path = "YOUR_DIRECTORY/note.jpg"
engine.load_image(image_path)

print(f"Image '{image_path}' loaded into the OCR engine.")
```

Ha a képed egy felhő‑bucketben van, előbb töltsd le, vagy adj át egy `BytesIO` streamet – az `ocr` elég rugalmas ahhoz, hogy mindkettőt kezelje.

### 4. lépés: A felismerési folyamat futtatása

Miután a motor fel van készítve és a kép a memóriában van, végre **képen történő OCR**‑t hajtunk végre, és lekérjük a nyers szöveget.

```python
# Step 4: Execute recognition
extracted_text = engine.recognize()

print("=== Extracted Text ===")
print(extracted_text)
```

A `recognize()` hívás egy egyszerű Unicode‑stringet ad vissza. A legtöbb esetben közvetlenül egy `.txt` fájlba írhatod, átadhatod egy természetes nyelvi csővezetéknek, vagy megjelenítheted egy GUI‑ban.

### 5. lépés: Opcionális – Kimenet tisztítása vagy utófeldolgozása

A kézírásos OCR nem tökéletes; gyakran előfordulnak felesleges sortörések vagy félreolvasott karakterek. Egy gyors tisztítási lépés javíthatja a további eredményeket.

```python
# Step 5: Simple post‑processing (optional)
def tidy(text):
    # Collapse multiple spaces, strip leading/trailing whitespace
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(extracted_text)

print("\n=== Cleaned Text ===")
print(clean_text)
```

Nyugodtan csatlakoztass helyesírás‑ellenőrzőket, nyelvi modelleket vagy egyedi reguláris kifejezéseket a saját területednek megfelelően.

### Teljes szkript – Másolás és beillesztés

Mindent összegezve, itt a teljes, futtatható program, amely **kézírásos szöveget** nyer ki egy JPEG‑ből, és rendezett eredményt nyomtat.

```python
# -*- coding: utf-8 -*-
"""
Complete example: Perform OCR on image to extract handwritten text.
"""

# -------------------------------------------------
# Step 1: Import the OCR library and create an engine
# -------------------------------------------------
import ocr

engine = ocr.OcrEngine()

# -------------------------------------------------
# Step 2: Set the engine to recognize handwritten text
# -------------------------------------------------
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

# -------------------------------------------------
# Step 3: Load the image you want to analyze
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/note.jpg"   # <-- change this to your file
engine.load_image(image_path)

# -------------------------------------------------
# Step 4: Perform recognition and output the extracted text
# -------------------------------------------------
raw_text = engine.recognize()
print("=== Raw OCR Output ===")
print(raw_text)

# -------------------------------------------------
# Step 5: Optional cleanup for nicer display
# -------------------------------------------------
def tidy(text):
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(raw_text)
print("\n=== Cleaned OCR Output ===")
print(clean_text)
```

**Várható kimenet** (a tényleges szöveg természetesen eltérő lesz):

```
=== Raw OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3

=== Cleaned OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3
```

Ha értelmetlen szöveget látsz, ellenőrizd a kép minőségét (jó megvilágítás, minimális elmosódás) és győződj meg róla, hogy `HANDWRITTEN` módban vagy. Ezek a két tényező felel meg a legtöbb felismerési hibáért.

## Gyakran Ismételt Kérdések (GYIK)

| Kérdés | Válasz |
|----------|--------|
| **Használhatom ezt PNG‑ből szöveg kinyerésére?** | Természetesen. Az `engine.load_image("scan.png")` ugyanúgy működik. |
| **Mi van, ha a képem egy PDF‑oldal?** | Először konvertáld az oldalt képpé (pl. a `pdf2image`‑el), majd add át a motorhoz. |
| **A könyvtár szálbiztos?** | Igen, minden szálhoz létrehozhatsz külön `OcrEngine` objektumot. |
| **Miben különbözik a `pytesseract`‑tól?** | Az `ocr` elrejti a Tesseract binárist és beépített kézírásos modellt tartalmaz, így nem kell külső végrehajtható fájlokat telepíteni. |
| **Hogyan tudok **JPG‑ből szöveget kinyerni** tömegesen?** | Csomagold a szkriptet egy ciklusba, vagy használd az `engine.load_image`‑t minden fájlon, és gyűjtsd az eredményeket listába vagy CSV‑be. |

## Szélsőséges esetek és legjobb gyakorlatok

1. **Alacsony kontrasztú fotók** – Növeld a kontrasztot programozottan a betöltés előtt, vagy használd az `engine.apply_preprocessing('contrast', level=2)`‑t.
2. **Keverék nyomtatott és kézírásos** – Két átfutás: először `HANDWRITTEN`, majd `PRINTED`, és egyesítsd a kimeneteket.
3. **Nagy képek** – Méretezd le körülbelül 1500 px szélességre; az OCR motorok általában gyorsabban dolgoznak kisebb pufferekkel, pontosságvesztés nélkül.
4. **Unicode karakterek** – A könyvtár UTF‑8 stringeket ad vissza, így emoji‑kat, ékezetes betűket vagy matematikai szimbólumokat is kezelhetsz natívan.

## Összegzés

Átmentünk egy konkrét példán, hogyan **képen történő OCR**‑t hajtsunk végre, különösen kézírásos jegyzetekre fókuszálva. Az `ocr` csomag telepítésével, a motor `HANDWRITTEN` módra állításával, egy fénykép betöltésével és a `recognize()` meghívásával **kézírásos képadatot** alakíthatsz tiszta, kereshető szöveggé.  

Innen már **JPG‑ből szöveget tudsz kinyerni** tömegesen, az eredményt beillesztheted egy jegyzetkészítő alkalmazásba, vagy kombinálhatod beszéd‑szintézissel a hozzáférhetőség érdekében. A lehetőségek végtelenek, a fenti kód pedig szilárd alapot ad a kísérletezéshez.

Van egy saját trükköd – mondjuk más fájlformátum vagy egy különleges előfeldolgozási módszer? Írj egy megjegyzést, és folytassuk a beszélgetést. Boldog kódolást, és élvezd a karikák digitális aranyá alakítását!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}