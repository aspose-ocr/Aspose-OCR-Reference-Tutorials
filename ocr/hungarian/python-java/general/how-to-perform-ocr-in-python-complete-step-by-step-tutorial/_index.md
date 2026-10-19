---
category: general
date: 2026-03-26
description: Tanulja meg, hogyan hajthat végre OCR-t Pythonban, és hogyan ismerhet
  fel szöveget képfájlokból. Ez az útmutató bemutatja, hogyan lehet szöveget kinyerni
  PNG-ből, és gyorsan képet szöveggé konvertálni.
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: hu
og_description: Hogyan végezzünk OCR-t Pythonban? Kövesd ezt az útmutatót, hogy szöveget
  ismerj fel képről, szöveget nyerj ki PNG-ből, és képet szöveggé alakíts egy próba
  licenccel.
og_title: Hogyan végezzünk OCR-t Pythonban – Teljes útmutató
tags:
- OCR
- Python
- Image Processing
title: Hogyan végezzünk OCR-t Pythonban – Teljes lépésről‑lépésre útmutató
url: /hu/python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk OCR-t Pythonban – Teljes lépésről‑lépésre útmutató  

Gondoltad már, **hogyan végezzünk OCR-t** egy képen, amit épp a telefonoddal készítettél? Nem vagy egyedül – a fejlesztők világszerte megbízható módra vágynak, hogy szöveget ismerjenek fel képfájlokból anélkül, hogy bonyolult natív könyvtárakkal küzdenének.  

Ebben az útmutatóban egy gyakorlati példán keresztül mutatjuk be, hogyan **végezzünk OCR-t**, **szöveget ismerjünk fel képről**, és **szöveget nyerjünk ki PNG‑ből** egy könnyű Python wrapper segítségével. A végére képes leszel **képet szöveggé konvertálni** néhány kódsorral, és nem kell aggódnod a licencelési problémák miatt, mivel a beépített próba módot használjuk.  

## Amit megtanulsz  

* Hogyan állíts be egy próba licencet az OCR motorhoz (fájlútvonal nélkül).  
* A pontos hívássorozat a **recognize text from image** objektumokhoz.  
* Módszerek a **extract text from PNG** fájlokból, és a gyakori buktatók kezelése, mint például a hiányzó betűkészletek.  
* Tippek a megoldás skálázásához, amikor a próba licencből termelési licencre váltasz.  

**Prerequisites** – szükséged van Python 3.8+ és az `ocr` csomagra (telepíthető a `pip install ocr` paranccsal). Más külső eszközre nincs szükség.  

---  

![hogyan végezzünk OCR példát](https://example.com/ocr-demo.png "hogyan végezzünk OCR Pythonban – felismert szöveg megjelenítve")  

*Kép alt szöveg: hogyan végezzünk OCR Pythonban – minta kimenet*  

## 1. lépés – Próba licenc aktiválása (fájlútvonal nélkül)  

Mielőtt a motor bármit is olvasna, szüksége van egy érvényes licencre. A próba mód tökéletes kísérletekhez és kis projektekhez.  

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*Miért fontos:* A licenc objektum azt jelzi az OCR könyvtárnak, hogy egy sandbox környezetben dolgozol. Ha kihagyod ezt a lépést, a motor `LicenseError`‑t dob, amint meghívod a `recognize()`‑t.  

**Pro tipp:** Amikor fizetős licencre váltasz, cseréld le a fenti két sort erre: `ocr.License("path/to/your/license.key").apply()`.  

## 2. lépés – OCR Engine példány létrehozása  

Most, hogy a próba aktív, példányosítjuk a fő motort. Gondolj rá úgy, mint egy “agyként”, amely megnézi a képet és eldönti, hol mely karakterek vannak.  

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*Miért fontos:* A `OcrEngine` tárolja a konfigurációt, például a nyelvi csomagokat és a DPI beállításokat. Később módosíthatod ezeket, de az alapértelmezett a legtöbb csak angol nyelvű PNG‑hez megfelelő.  

## 3. lépés – A feldolgozni kívánt PNG betöltése  

Itt történik a **recognize text from image**. Az `ocr.Imaging.Image.load()` metódus támogatja a PNG, JPEG, BMP és néhány további formátumot.  

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*Szélsőséges eset:* Ha a PNG indexed palettát használ (gyakori képernyőképeknél), a betöltő automatikusan 24‑bit RGB pufferre konvertálja. Ez a konverzió apró teljesítménycsökkenést okozhat, de biztosítja a pontos OCR eredményeket.  

## 4. lépés – OCR futtatása és a szöveg kinyerése  

Végül megkérjük a motort, hogy elvégezze a feladatát, majd kinyerjük a sima szöveges eredményt.  

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**Várható kimenet** (példa egy egyszerű, „Hello World” szöveget tartalmazó képre):  

```
Hello World
```

Ha a kép több sort tartalmaz, a kimenet megőrzi a sortöréseket, így könnyen továbbadható olyan downstream folyamatoknak, mint a CSV elemzők vagy NLP csővezetékek.  

## Opcionális: Finomhangolás a jobb pontosságért  

* **Language packs:** `ocr_engine.set_language("eng")` (alapértelmezett) vagy `"fra"` a francia nyelvhez.  
* **DPI scaling:** `ocr_engine.set_dpi(300)` javíthatja az eredményeket alacsony felbontású szkenneléseknél.  
* **Pre‑processing:** Bináris küszöb alkalmazása (`ocr.Imaging.Image.threshold()`) a `set_image` előtt gyakran tisztább szöveget eredményez zajos háttér esetén.  

Ezek a finomhangolások hasznosak, amikor egy gyors demóról egy termelés‑szintű **ocr tutorial python**-ra váltasz, amely naponta több száz fájlt dolgoz fel.  

## Teljes szkript – Kész a másolásra és beillesztésre  

Az alábbiakban a teljes, futtatható szkript látható, amely összekapcsolja a fenti lépéseket. Mentsd `run_ocr.py` néven, és cseréld le a `YOUR_DIRECTORY/sample1.png`-t a saját PNG‑d elérési útjára.  

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

Futtasd a parancssorból:  

```bash
python run_ocr.py
```

A konzolon meg kell jelennie a kinyert szövegnek. Ha üres stringet kapsz, ellenőrizd, hogy a kép valóban tiszta, nagy kontrasztú szöveget tartalmaz-e, és hogy a próba licenc hibamentesen alkalmazva lett-e.  

## Gyakori kérdések és buktatók  

* **„Működik ez JPEG‑kel?”** – Teljesen. A `load()` metódus automatikusan felismeri a formátumot, így a PNG‑t cserélheted JPEG‑re kódbeli változtatás nélkül.  
* **„Mi van, ha a kép el van forgatva?”** – A motor képes automatikusan felismerni a tájolást, de a legjobb eredményért előre forgathatod a képet `input_image.rotate(90)`‑vel a `set_image` előtt.  
* **„Feldolgozhatok több képet egy ciklusban?”** – Igen. Csak helyezd a betöltést és a `recognize()` hívásokat egy `for` ciklusba; ugyanaz a `ocr_engine` példány újrahasználható, ami egy kis teljesítménymegtakarítást eredményez.  

## Következő lépések – Demóról a termelésig  

Most, hogy tudod, **hogyan végezzünk OCR-t**, fontold meg ezeket a további témákat:  

* **Batch processing** – Kombináld ezt a szkriptet az `os.listdir()`‑vel, hogy **extract text from PNG** fájlokat tömegesen dolgozz fel.  
* **Integrate with PDF** – Használd a `pdf2image`‑t PDF oldalak PNG‑re konvertálásához, majd add őket ugyanabba a csővezetékbe.  
* **Post‑processing** – Alkalmazz regexet vagy fuzzy matchinget a gyakori OCR hibák (pl. „0” vs „O”) tisztításához.  

Ezek mind a **convert image to text** alapgondolatára épülnek, és kibővítik az OCR munkafolyamatod hasznosságát.  

---  

### TL;DR  

Mindezt lefedtük, amit a **hogyan végezzünk OCR** Pythonban tudni kell: aktiváld a próba licencet, hozd létre a motort, tölts be egy PNG‑t, futtasd a felismerést, és nyomtasd ki az eredményt. Néhány sor kóddal képes vagy **recognize text from image**, **extract text from PNG**, és **convert image to text** bármely downstream alkalmazáshoz.  

Próbáld ki, finomhangold a DPI vagy nyelvi beállításokat, és hagyd, hogy a motor végezze a nehéz munkát. Boldog kódolást!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}