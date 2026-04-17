---
category: general
date: 2026-03-26
description: Hogyan futtassunk OCR-t egy PNG fájlon, és nyerjünk ki szöveget a képből
  egy egyéni szótárral a jobb OCR pontosság érdekében. Tanulja meg, hogyan töltsön
  be képet gyorsan az OCR-hez.
draft: false
keywords:
- how to run OCR
- extract text from image
- recognize text from png
- improve OCR accuracy
- load image for OCR
language: hu
og_description: Hogyan futtassunk OCR-t egy PNG fájlon, és nyerjünk ki szöveget a
  képből egy egyedi szótárral a jobb OCR pontosság érdekében. Lépésről‑lépésre útmutató.
og_title: Hogyan futtassuk az OCR-t – Szöveg kinyerése képből Pythonban
tags:
- OCR
- Python
- Image Processing
title: Hogyan futtassunk OCR-t – Szöveg kinyerése képből Pythonban
url: /hu/python-java/general/how-to-run-ocr-extract-text-from-image-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan futtassunk OCR – Szöveg kinyerése képből Pythonban

Gondolkodtál már azon, **hogyan futtassunk OCR‑t** egy beolvasott számlán vagy egy képernyőképen, és tiszta, kereshető szöveget kapj? Nem vagy egyedül. Sok projektben a szűk keresztmetszet egyszerűen a kép betöltése OCR‑hez, majd a motor rábeszélése, hogy a domain‑specifikus szavakat megértse.  

Ebben az útmutatóban egy teljes, azonnal futtatható példán keresztül mutatjuk be, hogyan **extraháljunk szöveget képből**, hogyan **ismerjünk fel szöveget PNG** fájlokból, és még trükköket is bemutatunk a **OCR pontosság javítására** egyedi szótárakkal és speciális karakterekkel. A végére egy önálló szkriptet kapsz, amelyet bármely Python kódbázisba beilleszthetsz.

## Amire szükséged lesz

- Python 3.8+ (a kód típusjelöléseket használ, de korábbi 3.x verziókon is működik)
- A `ocr` könyvtár, amely a célzott OCR motorral együtt érkezik (telepítsd a `pip install ocr‑engine` paranccsal – cseréld ki a tényleges csomagnévre)
- Egy képfájl (`input.png`), amelyet feldolgozni szeretnél
- Opcionálisan: egy egyszerű szövegfájl (`invoice_terms.txt`) domain‑specifikus szavakkal, soronként egy

Nincsenek nehéz külső függőségek, nincs felhő API kulcs, csak egy helyi OCR motor.

---

## 1. lépés: Az OCR könyvtár telepítése és importálása

Először győződj meg róla, hogy az OCR csomag telepítve van. Ha a hipotetikus `ocr-engine` csomagot használod, futtasd:

```bash
pip install ocr-engine
```

Most importáld a szükséges osztályokat:

```python
# Step 1: Import the OCR SDK
import ocr
from ocr import Imaging
```

> **Pro tipp:** Ha virtuális környezetet használsz, aktiváld azt a telepítés előtt, hogy a globális Python környezet tiszta maradjon.

## 2. lépés: OCR motor példány létrehozása

Egy motor objektum létrehozása a belépési pont minden OCR feladathoz. Gondolj rá úgy, mint a szkenner hardverének bekapcsolására a szoftveren belül.

```python
# Step 2: Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
```

Miért fontos: a motor tárolja a konfigurációt, például nyelvi csomagokat, felismerési módokat és minden egyedi erőforrást, amelyet később csatolni fogsz. Enélkül nem tudsz **load image for OCR** vagy futtatni a felismerési folyamatot.

## 3. lépés: A felismertetni kívánt kép betöltése

Itt ténylegesen **load image for OCR**. A `Imaging.Image.load()` metódus beolvassa a fájlt, és átalakítja a motor által elvárt belső bitmap formátumba.

```python
# Step 3: Load the PNG image you want to process
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Imaging.Image.load(image_path))
```

Ha JPEG vagy TIFF fájlod van, ugyanaz a metódus működik – csak cseréld le a kiterjesztést. A motor automatikusan felismeri a formátumot.

> **Edge case:** Nagyon nagy képek (5 MP felett) memóriacsúcsokat okozhatnak. Ha teljesítményproblémákat tapasztalsz, gondolj a Pillow‑al történő lecsökkentésre a betöltés előtt.

## 4. lépés: Egyedi szótár biztosítása a pontosság növeléséhez

A legtöbb OCR motor általános nyelvi modellekkel érkezik. Számlák, nyugták vagy jogi dokumentumok esetén gyakran hiányoznak a szavak. Egy egyedi szószótár megadása azt mondja a motornak: „ezek a kifejezések legitimek, kezeld őket helyesnek”.

```python
# Step 4: Attach a custom dictionary (one word per line)
custom_dict_path = "YOUR_DIRECTORY/invoice_terms.txt"
ocr_engine.set_custom_dictionary(custom_dict_path)
```

Tipikus bejegyzések például:

```
VAT
InvoiceNumber
Øre
ß
Ħ
```

Ezek hozzáadása drámaian javítja a **improve OCR accuracy** mutatót – különösen a nem‑ASCII szimbólumok esetén.

## 5. lépés: Speciális karakterek hozzáadása, amelyek nincsenek az alapértelmezett készletben

Ha a domained olyan szimbólumokat használ, mint az eurójel (€) vagy a skandináv Ø, ezeket kifejezetten hozzáadhatod:

```python
# Step 5: Register additional characters
ocr_engine.add_custom_characters("ØßĦ")
```

A motor most ezeket a glifeket érvényesnek tekinti a felismerési fázisban, csökkentve a „szemét” kimenet esélyét.

## 6. lépés: OCR folyamat futtatása és szöveg lekérése

Végül hívd meg a recognizert, és vedd ki a tiszta szöveget. A `recognize()` hívás egy gazdag objektumot ad vissza; a legtöbb esetben csak a nyers stringre van szükségünk.

```python
# Step 6: Execute OCR and print the result
result = ocr_engine.recognize()
print("=== Recognized Text ===")
print(result.get_text())
```

**Várható kimenet** (rövidítve a tömörség kedvéért):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total: €1,250.00
VAT: 25%
...
```

Ha a kimenet értelmezhetetlennek tűnik, ellenőrizd, hogy az egyedi szótár és a speciális karakterek helyesen betöltődtek-e.

---

## Vizuális áttekintés

![how to run OCR diagram](ocr-workflow.png){alt="how to run OCR diagram"}

A fenti diagram illusztrálja a folyamatot a kép betöltésétől a tiszta szöveg eléréséig, kiemelve, hol lehet egyedi szótárakat és karakterkészleteket beilleszteni.

---

## Gyakori kérdések és buktatók

### Működik ez többoldalas PDF‑ekkel?

Igen – egyszerűen konvertáld minden oldalt PNG‑re (például a `pdf2image` vagy hasonló segítségével), majd add át őket sorban ugyanazon `ocr_engine` példánynak. A motor minden képet önállóan feldolgoz, így egy karakterlánc-listát kapsz, amelyet összefűzhetsz.

### Mi van, ha a kép el van forgatva?

A legtöbb modern OCR motor automatikusan felismeri a tájolást, de kényszerítheted a forgatást a következővel:

```python
ocr_engine.set_image(Imaging.Image.load(image_path).rotate(90))
```

### Hogyan kezeljünk más nyelveket, mint az angol?

Cseréld le a nyelvi modellt a kép betöltése előtt:

```python
ocr_engine.set_language("de")  # German
```

Győződj meg róla, hogy a megfelelő nyelvi csomag telepítve van.

---

## Teljes szkript – Kész a másolásra és beillesztésre

Az alábbiakban a teljes program látható, amely készen áll a futtatásra, miután kicserélted a helyettesítő útvonalakat.

```python
#!/usr/bin/env python3
"""
How to Run OCR – Complete example that extracts text from a PNG,
uses a custom dictionary, and adds special characters for better accuracy.
"""

# Install the OCR package first:
# pip install ocr-engine

import ocr
from ocr import Imaging

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = ocr.OcrEngine()

    # 2️⃣ Load the image you want to recognize
    image_path = "YOUR_DIRECTORY/input.png"      # <-- change this
    ocr_engine.set_image(Imaging.Image.load(image_path))

    # 3️⃣ Provide a custom dictionary (optional but recommended)
    dict_path = "YOUR_DIRECTORY/invoice_terms.txt"   # one word per line
    ocr_engine.set_custom_dictionary(dict_path)

    # 4️⃣ Add any special characters not covered by the default set
    ocr_engine.add_custom_characters("ØßĦ")   # e.g., currency symbols

    # 5️⃣ Run the OCR process
    result = ocr_engine.recognize()

    # 6️⃣ Output the recognized text
    print("=== Recognized Text ===")
    print(result.get_text())

if __name__ == "__main__":
    main()
```

Futtasd a következővel:

```bash
python run_ocr.py
```

A konzolon meg kell jelennie a kinyert szövegnek. Innen már elmentheted fájlba, betáplálhatod adatbázisba, vagy továbbadhatod downstream NLP csővezetékeknek.

---

## Összefoglalás és következő lépések

Áttekintettük, **hogyan futtassunk OCR‑t** PNG‑n, **hogyan extraháljunk szöveget képből**, és gyakorlati módszereket mutattunk be a **szöveg felismerésére PNG‑ből** miközben **javítjuk az OCR pontosságát** szótárakkal és egyedi karakterekkel.  

Ezután fontold meg:

- **Kötegelt feldolgozás:** Ciklus egy képek könyvtárán.
- **Utófeldolgozás:** Regex használata számlaszámok vagy dátumok kinyeréséhez.
- **Integráció:** A szkript beágyazása egy Flask API‑ba on‑demand OCR szolgáltatásokhoz.

Ha érdekelnek a haladóbb témák, nézd meg a **load image for OCR** tutorialokat OpenCV előfeldolgozással, vagy merülj el a mélytanulás alapú OCR modellekben, mint a Tesseract 4+ LSTM rétegekkel.

---

### Kísérletezz tovább!

Próbáld ki a `invoice_terms.txt` helyett egy orvosi terminológiai listát, adj hozzá görög karaktereket, vagy tápláld a motort alacsony felbontású fotóval, hogy lásd, meddig tudja nyújtani a pontosságot. Minél többet kísérletezel, annál jobban megérted a előfeldolgozás, egyedi szókészletek és motorbeállítások közti kompromisszumokat.

Boldog kódolást, és legyen az OCR eredményed mindig kristálytiszta!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}