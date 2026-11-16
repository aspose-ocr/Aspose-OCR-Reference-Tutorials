---
category: general
date: 2026-03-18
description: Hogyan használjuk az OCR-t a képek szövegének kinyeréséhez – egy gyors
  útmutató a PNG-fájlok szövegének felismeréséhez és a képek OCR-hez való betöltéséhez.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- how to extract text
- load image for OCR
language: hu
og_description: Hogyan használjunk OCR-t a képekből származó szöveg kinyeréséhez –
  tanulja meg a szöveg felismerését PNG-ből, a kép betöltését OCR-hez, és a szöveg
  kinyerését egy egyszerű Python szkripttel.
og_title: 'Hogyan használjunk OCR-t: Szöveg kinyerése képekből Pythonban'
tags:
- OCR
- Python
- Image Processing
title: 'Hogyan használjuk az OCR-t: Szöveg kinyerése képekből Pythonban'
url: /hu/python-java/general/how-to-use-ocr-extract-text-from-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjunk OCR-t: Szöveg kinyerése képekből Pythonban

Gondolkodtál már **hogyan használjunk OCR-t**, amikor egy rendezetlen képernyőképről vagy beolvasott nyugtáról van szó? Nem vagy egyedül – a fejlesztőknek folyamatosan kell olvasható szöveget kinyerniük a képekből, különösen a mobilalkalmazásokból vagy webes feltöltésekből származó PNG‑ekből. Ebben a bemutatóban egy teljes, futtatható példán keresztül mutatjuk be, hogyan **nyerhetünk ki szöveget képfájlokból**, **ismerhetünk fel szöveget PNG‑eszközökből**, és még **betölthetünk képet OCR‑hez** néhány Python‑sorral.

Mindent lefedünk, az adott könyvtár telepítésétől a többnyelvű dokumentumok kezeléséig, így a végére pontosan tudni fogod, *hogyan nyerj ki szöveget* bármilyen képből, amit az OCR‑motorba adsz. Nincs homályos hivatkozás, csak egy világos, lépésről‑lépésre megoldás, amit kimásolhatsz és futtathatsz.

## Mit fogsz megtanulni

A következő szakaszokban:

1. Beállítunk egy könnyűsúlyú OCR‑motort (nincs nehéz függőség).  
2. Betöltünk egy képfájlt – konkrétan egy PNG‑t – a motorba.  
3. Engedélyezzük az automatikus nyelvfelismerést, hogy a motor többnyelvű tartalmat is kezelhessen.  
4. Futattjuk a felismerési folyamatot és lekérjük a nyers‑szöveg eredményt.  
5. Finomhangoljuk a munkafolyamatot olyan szélhelyzetekhez, mint hiányzó fájlok vagy nem támogatott formátumok.

Ha már ismered az alap Python‑t, készen állsz. Nem szükséges előzetes OCR‑tapasztalat, bár egy gyors pillantás a könyvtár dokumentációjára sosem árt.

---

![Hogyan használjunk OCR-t PNG képen](placeholder.png "Hogyan használjunk OCR-t PNG képen – lépésről‑lépésre útmutató")

## Hogyan használjunk OCR‑t – Kép betöltése és szöveg felismerése {#how-to-use-ocr}

### 1. Lépés: Telepítsd az OCR könyvtárat

Először is szükséged van egy Python‑csomagra, amely egy `OcrEngine` osztályt biztosít. A bemutató kedvéért a fiktív, de szemléletes **SimpleOCR** csomagot használjuk, amelyet a pip‑el telepíthetsz:

```bash
pip install simple-ocr
```

> **Pro tipp:** Ha virtuális környezetben dolgozol (erősen ajánlott), aktiváld azt a telepítési parancs futtatása előtt. Így a projekt függőségei rendezettek maradnak.

### 2. Lépés: Importáld a motort és hozz létre egy példányt

A motor létrehozása olyan egyszerű, mint a konstruktor meghívása. Tekintsd a motort a “agyra”, amely később feldolgozza a betáplált képet.

```python
# Step 2: Import and instantiate the OCR engine
from simple_ocr import OcrEngine

# Create a fresh engine instance – this allocates internal buffers
engine = OcrEngine()
```

Miért hozunk létre minden alkalommal egy új példányt? Izoláció miatt. Egy friss motor garantálja, hogy egy korábbi futás maradványai ne szennyezzék a jelenlegi felismerést, ami kulcsfontosságú, ha sok fájlt dolgozol fel egy kötegben.

### 3. Lépés: Töltsd be a feldolgozni kívánt képet

Most ténylegesen **betöltjük a képet OCR‑hez**. A `setImageFromFile` metódus bármely raszteres kép útvonalát elfogadja; mi egy `mixed_doc.png` nevű PNG‑re mutatunk.

```python
# Step 3: Load the PNG image you want to read
image_path = "YOUR_DIRECTORY/mixed_doc.png"
engine.setImageFromFile(image_path)
```

Ha a fájl nem található, a `SimpleOCR` egy egyértelmű `FileNotFoundError`‑t dob. Elkapva ezt barátságos hibaüzenetet adhatunk:

```python
try:
    engine.setImageFromFile(image_path)
except FileNotFoundError:
    print(f"❗️ Unable to locate '{image_path}'. Check the path and try again.")
    raise
```

### 4. Lépés: Engedélyezd az automatikus nyelvfelismerést

A legtöbb modern OCR‑motor nyelvcsomagokkal érkezik. A `"multilingual"` átadással azt mondjuk a motornak, hogy szagolja meg a szöveget és automatikusan válassza ki a megfelelő nyelvi modellt. Ez különösen hasznos, ha a PNG például angol és spanyol keverékét tartalmazza.

```python
# Step 4: Turn on auto‑language detection (covers all installed packs)
engine.setLanguage("multilingual")
```

Ha előre tudod a nyelvet, a `"multilingual"` helyett megadhatsz egy konkrét locale‑t, például `"eng"` vagy `"spa"` a feldolgozás felgyorsítása érdekében.

### 5. Lépés: Futtasd a felismerési folyamatot

Itt történik a nehéz munka. A `recognize()` beolvassa a képet, szegmentál, futtatja a neurális hálót, és belsőleg felépít egy szöveg‑pufferet.

```python
# Step 5: Execute OCR – this may take a moment for large images
engine.recognize()
```

A motor a háttérben a következőket végzi:

- **Előfeldolgozás** (ferdejavítás, binarizálás)  
- **Elrendezés‑elemzés** (oszlopok, táblázatok detektálása)  
- **Karakter‑osztályozás** (mélytanuló modell használatával)  

Mindez el van rejtve, ezért csak egy sorra van szükséged.

### 6. Lépés: Szerezd meg és írd ki a felismert szöveget

Végül lekérjük az eredményobjektumot és kinyerjük a nyers karakterláncot. Ez az a rész, ahol ténylegesen **kivonod a szöveget a képből**.

```python
# Step 6: Get the OCR result and display the plain text
result = engine.getResult()
text = result.getText()
print("📝 Recognized Text:\n")
print(text)
```

**Várható kimenet** (rövidítve a tömörség kedvéért):

```
📝 Recognized Text:

Invoice #12345
Date: 2026‑03‑15
Total: $89.99
Thank you for your purchase!
```

Ha a kép nem tartalmaz felismerhető karaktereket, a `text` egy üres string lesz. Ezt ellenőrizheted:

```python
if not text.strip():
    print("⚠️ No text detected – try a higher‑resolution image or adjust preprocessing.")
```

---

## Szöveg kinyerése képből – Gyakori szélhelyzetek kezelése

### Több nyelv egy fájlban

Ha egy dokumentum több nyelvet kever, a `"multilingual"` beállítás általában helyesen működik. Ha azonban hibás felismeréseket észlelsz, megadhatsz egy tartalék nyelvlistát:

```python
engine.setLanguage(["eng", "spa", "fra"])  # English, Spanish, French
```

### Nem‑PNG formátumok

Bár a fókuszunk a **szöveg felismerése PNG‑ből**, a `SimpleOCR` JPEG‑et, BMP‑t és TIFF‑et is elfogad. Csak cseréld ki a fájlkiterjesztést a `setImageFromFile`‑ben. TIFF‑készleteknél esetleg egy konkrét oldalt kell kiválasztani:

```python
engine.setImageFromFile("scanned.tif", page=0)  # first page only
```

### Nagy fájlok és memóriahasználat

Ha gigapixeles beolvasásokat dolgozol fel, érdemes a OCR előtt átméretezni:

```python
from PIL import Image

with Image.open(image_path) as img:
    img.thumbnail((2000, 2000))  # keep aspect ratio, max 2000px
    img.save("temp_resized.png")
engine.setImageFromFile("temp_resized.png")
```

Az átméretezés csökkenti a memória terhelését, miközben elegendő részletet megőriz a pontos felismeréshez.

### Sikertelen betöltések hibakeresése

Néha egy kép szemetnek rendben tűnik, de belül hibás. Engedélyezd a részletes naplózást, hogy lásd, mit lát a motor:

```python
engine.enableDebug(True)   # prints internal steps to stdout
engine.recognize()
```

---

## Teljes, futtatható szkript

Az alábbiakban a teljes program látható, amely összerakja az összes elemet. Másold egy `ocr_demo.py` nevű fájlba, állítsd be a `YOUR_DIRECTORY` helyőrzőt, majd futtasd a `python ocr_demo.py` parancsot.

```python
# ocr_demo.py
# Full example showing how to use OCR to extract text from a PNG image.
# Requires: pip install simple-ocr pillow

from simple_ocr import OcrEngine
import os
from PIL import Image

def main():
    # 1️⃣ Create the OCR engine
    engine = OcrEngine()

    # 2️⃣ Define the image path – change this to your actual file location
    image_path = os.path.join("YOUR_DIRECTORY", "mixed_doc.png")

    # 3️⃣ Load the image (with a safety net for missing files)
    try:
        engine.setImageFromFile(image_path)
    except FileNotFoundError:
        print(f"❗️ Cannot find image at '{image_path}'. Exiting.")
        return

    # Optional: resize large images to keep memory usage low
    # (uncomment if you deal with huge scans)
    # with Image.open(image_path) as img:
    #     img.thumbnail((2000, 2000))
    #     resized_path = "temp_resized.png"
    #     img.save(resized_path)
    #     engine.setImageFromFile(resized_path)

    # 4️⃣ Enable automatic language detection (covers all installed packs)
    engine.setLanguage("multilingual")

    # 5️⃣ Run the OCR engine
    engine.recognize()

    # 6️⃣ Retrieve and print the recognized text
    result = engine.getResult()
    text = result.getText()

    if text.strip():
        print("\n📝 Recognized Text:\n")
        print(text)
    else:
        print("⚠️ No recognizable text found. Try a clearer image or adjust preprocessing.")

if __name__ == "__main__":
    main()
```

A szkript futtatása a `mixed_doc.png` tartalmának nyers‑szöveges változatát kell, hogy kiírja. Nyugodtan cseréld le a fájlt bármilyen más képre – a **szöveg kinyerése** ugyanúgy működik.

---

## Összegzés

Most végigmentünk azon, **hogyan használjunk OCR‑t** Pythonban a **szöveg kinyeréséhez képfájlokból**, különösen a **szöveg felismerése PNG‑eszközökből**, és a gyakorlati lépéseken, hogy **betöltsünk képet OCR‑hez**. A fenti kódrészlet egy önálló megoldás: telepítsd a csomagot, add meg a fájlt, engedélyezd a többnyelvű felismerést, futtasd a motort, és vedd ki az eredményt.

Innen tovább:

- Integráld a szkriptet egy webszolgáltatásba, amely felhasználói feltöltéseket fogad.  
- Kötegelt feldolgozást végezz egy PNG‑re konvertált PDF‑mappán.  
- Adj hozzá utófeldolgozást (pl. regex‑tisztítás, helyesírás‑ellenőrzés) a pontosság növelése érdekében.

Ne feledd, az OCR minősége a kép tisztaságától, a megfelelő nyelvi csomagoktól és néha egy kis előfeldolgozástól függ – ezért kísérletezz!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}