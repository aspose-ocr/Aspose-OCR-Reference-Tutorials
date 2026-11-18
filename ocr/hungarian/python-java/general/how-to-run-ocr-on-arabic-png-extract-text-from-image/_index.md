---
category: general
date: 2026-03-26
description: Tanulja meg, hogyan végezzen OCR-t arab PNG képeken, és gyorsan nyerje
  ki az arab szöveget. Ez az útmutató lépésről lépésre bemutatja a kép szöveggé alakítását
  Python kóddal.
draft: false
keywords:
- how to run ocr
- extract arabic text
- recognize arabic text
- convert image to text
- extract text from png
language: hu
og_description: Hogyan futtassunk OCR-t arab nyelvű PNG képeken? Kövesd ezt a teljes
  útmutatót az arab szöveg kinyeréséhez, felismeréséhez és a kép szöveggé konvertálásához
  Python segítségével.
og_title: Hogyan végezzünk OCR-t arab PNG-en – Szöveg kinyerése a képből
tags:
- OCR
- Python
- Arabic
title: Hogyan futtassunk OCR-t arab PNG-n – Szöveg kinyerése a képből
url: /hu/python-java/general/how-to-run-ocr-on-arabic-png-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan futtassunk OCR-t arab nyelvű PNG-n – Szöveg kinyerése a képből

Gondoltad már valaha, **hogyan futtassunk OCR-t** egy olyan képen, amely arab írást tartalmaz? Lehet, hogy egy beolvasott nyugtát, egy történelmi kéziratot vagy csak egy közösségi média bejegyzés képernyőképet kaptál, és a szöveget kereshető formátumban szeretnéd. Nem vagy egyedül – a fejlesztők világszerte szembesülnek ezzel a problémával, amikor jobbról balra író nyelvekkel dolgoznak.

Ebben az útmutatóban egy teljes, futtatható példán keresztül mutatjuk be, **hogyan futtassunk OCR-t** egy PNG fájlon, hogyan nyerjünk ki arab szöveget, és hogyan írjuk ki az eredményt a konzolra. Nincs homályos „lásd a dokumentációt” hivatkozás; csak a másolható‑beilleszthető kód, valamint magyarázatok arról, hogy miért fontos minden egyes sor. A végére **kép‑szöveg konvertálás** képességet fogsz elsajátítani megbízhatóan, még akkor is, ha a forrás egy nehézkes arab PNG.

> **Mit fogsz megtanulni**
> - Python OCR motor beállítása arab nyelvhez  
> - PNG kép betöltése és gyakori buktatók kezelése  
> - Arab szöveg felismerése és az eredmény ellenőrzése  
> - Tippek **arab szöveg kinyeréséhez** különböző képminőségekből  

Mielőtt belemerülnénk, győződj meg róla, hogy a Python 3.8+ telepítve van, és rendelkezel a `ocr` könyvtár (a példában használt) legújabb verziójával. Ha virtuális környezetet használsz, aktiváld most – ez segít a függőségek tisztán tartásában.

## Előfeltételek

- Python 3.8 vagy újabb  
- `ocr` csomag (`pip install ocr‑engine` – cseréld le a tényleges csomagnévre)  
- Egy arab nyelvű PNG kép (`arabic_doc.png`) egy elérhető helyen  
- Alapvető ismeretek a Python függvényekről és osztályokról  

Ennyi. Nincs nehéz keretrendszer, nincs Docker konténer – csak tiszta Python.

## 1. lépés: Az OCR könyvtár telepítése és importálása

Először is szükségünk van magára az OCR motorra. A könyvtár, amelyet használni fogunk, egy `OcrEngine` osztályt biztosít egy egyszerű API-val.

```python
# Install the library (run once in your terminal)
# pip install ocr-engine   # <-- replace with the correct package name

# Import the necessary classes
import ocr
from ocr import Imaging
```

*Miért importáljuk külön a `Imaging`-et?* A `Imaging` almodul egy kényelmes `Image.load` metódust ad, amely alapból érti a PNG, JPEG és TIFF formátumokat. Ennek a lépésnek a kihagyása nyers bájtok kézi kezelése mellett kényszerítene, ami a legtöbb esetben felesleges.

## 2. lépés: Az OCR motor példányosítása

Most létrehozzuk a motor egy példányát. Tekintsd ezt az objektumot a „agyként”, amely feldolgozza a képet.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

> **Pro tipp:** Ha sok képet szeretnél egymás után feldolgozni, használd ugyanazt a `ocr_engine` példányt. Ez gyorsítja a későbbi felismeréseket, mivel a nyelvi modelleket cache-eli.

## 3. lépés: A nyelv beállítása arabra

Az arab nem latin; saját karakterkészlettel, jobbról balra irányú írással és kontextuális formázással rendelkezik. Ezért expliciten meg kell mondanunk a motornak, melyik nyelvi modellt töltse be.

```python
# Step 3: Set the language to Arabic (language code "ar")
ocr_engine.set_language("ar")
```

Ha elfelejted ezt a sort, a motor alapértelmezés szerint angolt használ, és torz kimenetet kapsz – ezt már túl gyakran láttam.

## 4. lépés: PNG kép betöltése

Itt kezdődik igazán a **kép‑szöveg konvertálás** rész. Betöltjük azt a PNG fájlt, amely az arab írást tartalmazza.

```python
# Step 4: Load the image that contains the Arabic text
image_path = "YOUR_DIRECTORY/arabic_doc.png"   # replace with your actual path
ocr_engine.set_image(Imaging.Image.load(image_path))
```

### Gyakori edge case-ek

| Probléma | Tünet | Megoldás |
|----------|-------|----------|
| A kép túl sötét | Sok üres hely jelenik meg a kimenetben | Előfeldolgozás Pillow‑al (`ImageEnhance.Brightness`) |
| PNG alfa csatornával rendelkezik | Egyes OCR motorok hibásan olvassák a transzparens pixeleket | Konvertálás RGB‑re (`image.convert("RGB")`) betöltés előtt |
| A szöveg el van forgatva | A felismert szöveg fejjel lefelé jelenik meg | Kép forgatása (`image.rotate(90, expand=True)`) a motorhoz való átadás előtt |

## 5. lépés: A felismerési folyamat elindítása

Minden beállítva, most végre megkérjük a motort, hogy végezze el a feladatát.

```python
# Step 5: Run the recognition process
ocr_result = ocr_engine.recognize()
```

A `recognize` metódus egy objektumot ad vissza, amely a nyers Unicode karakterláncot, a biztonsági pontszámokat és a bounding box-okat tartalmazza. A legtöbb fejlesztőnek a sima szöveg elegendő.

## 6. lépés: A felismert arab szöveg kiírása

Most kiírjuk az eredményt. Egy valódi alkalmazásban fájlba, adatbázisba vagy egy fordító API-ba is továbbíthatod.

```python
# Step 6: Output the recognized text
print(ocr_result.get_text())
```

A szkript futtatásakor az arab karaktereknek meg kell jelenniük a konzolon (győződj meg róla, hogy a terminálod támogatja a Unicode‑t). Ha kérdőjelek vagy üres stringek jelennek meg, ellenőrizd a nyelvi beállítást és a kép minőségét.

### Várható kimenet

```
هذا نص عربي من صورة PNG تم استخراجها باستخدام OCR.
```

Ha a kimenet hasonló a fenti sorhoz, gratulálok – sikeresen **kivontad az arab szöveget** egy PNG‑ből!

## Teljes működő példa

Az alábbiakban az egész szkript látható, készen a másolás‑beillesztésre. Cseréld le a `YOUR_DIRECTORY/arabic_doc.png` útvonalat a saját fájlod elérési útjára.

```python
import ocr
from ocr import Imaging

def main():
    # Create OCR engine
    ocr_engine = ocr.OcrEngine()
    
    # Set Arabic language
    ocr_engine.set_language("ar")
    
    # Load the PNG image
    image_path = "YOUR_DIRECTORY/arabic_doc.png"
    ocr_engine.set_image(Imaging.Image.load(image_path))
    
    # Recognize text
    ocr_result = ocr_engine.recognize()
    
    # Print the extracted Arabic text
    print(ocr_result.get_text())

if __name__ == "__main__":
    main()
```

Futtasd a `python run_ocr.py` (vagy amilyen névre elnevezted a fájlt) paranccsal. Ha minden helyesen telepítve van, az arab mondat megjelenik a konzolon.

## Hogyan futtassunk OCR-t különböző képformátumokon

Ugyanez a kód működik JPEG, TIFF vagy BMP esetén is – csak a fájlkiterjesztést kell módosítani. Az `Image.load` metódus automatikusan felismeri a formátumot, így **kép‑szöveg konvertálás** extra kód nélkül végezhető.

```python
# Example for a JPEG file
ocr_engine.set_image(Imaging.Image.load("sample.jpg"))
```

Ne feledd, a forráskép minősége erősen befolyásolja a **arab szöveg felismerése** lépés pontosságát. A nagy felbontású, alacsony tömörítésű képek a legjobb eredményt adják.

## Szöveg kinyerése PNG‑ből: Tippek a nagyobb pontosságért

1. **DPI számít** – Legalább 300 dpi‑t célozz meg. Alacsony DPI gyakran hiányzó karakterekhez vezet.  
2. **A kontraszt a király** – Használj kép‑feldolgozó eszközöket (pl. OpenCV) a kontraszt növelésére, mielőtt a képet az OCR motorhoz adnád.  
3. **Zajszűrés** – A kis foltok összezavarhatják a modellt; a medián szűrés segít.  

Itt egy gyors snippet, amely Pillow‑t használ a PNG javítására OCR előtt:

```python
from PIL import Image, ImageEnhance, ImageFilter

def preprocess_png(path):
    img = Image.open(path).convert("L")          # grayscale
    img = ImageEnhance.Contrast(img).enhance(2)  # boost contrast
    img = img.filter(ImageFilter.MedianFilter()) # denoise
    return img

# Use the preprocessed image
prepped = preprocess_png("arabic_doc.png")
ocr_engine.set_image(Imaging.Image.from_pil(prepped))
```

## Gyakran Ismételt Kérdések

**Q: Működik ez más jobbról balra író nyelvekkel is, mint az arab?**  
A: Természetesen. Csak cseréld le a nyelvkódot (`"ar"` → `"he"` a héberhez, `"fa"` a perzsához), és a motor betölti a megfelelő modellt.

**Q: Mi a teendő, ha több PNG‑ből kell szöveget kinyerni egy mappában?**  
A: Iterálj a fájlokon, használd ugyanazt a `ocr_engine` példányt, és gyűjtsd az eredményeket egy listába vagy írd ki külön `.txt` fájlokba.

**Q: Kaphatok biztonsági pontszámot minden egyes szóhoz?**  
A: Igen. Az `ocr_result` gyakran rendelkezik egy `get_confidences()` metódussal. Párosítsd a pontszámot a megfelelő szóval a minőség‑ellenőrzéshez.

## Következő lépések

Most, hogy tudod, **hogyan futtassunk OCR-t** arab PNG‑ken, gondolj ezekre a további ötletekre:

- **Kötegelt feldolgozás:** Kombináld a szkriptet az `os.listdir`‑el, hogy **arab szöveget nyerj ki** egy teljes könyvtárból.  
- **Utófeldolgozás:** Használd az `arabic_reshaper` és `python-bidi` könyvtárakat a jobbról balra kimenet helyes megjelenítéséhez PDF‑ekben.  
- **Integráció:** Tápláld a kinyert szöveget egy kereső indexbe (pl. Elasticsearch), hogy a beolvasott dokumentumok kereshetők legyenek.  

Ezek a témák a jelen cikkben lefektetett alapokra épülnek, és segítenek egy egyszerű **kép‑szöveg konvertálás** szkriptet egy termelés‑kész csővezetékké alakítani.

---

![how to run OCR on Arabic PNG](

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}