---
category: general
date: 2026-03-26
description: Ismerje fel gyorsan a szöveget a képen, megtanulva, hogyan töltsön be
  képet OCR-hez, és hogyan nyerjen ki adatot egy meghatározott területről. Kövesse
  ezt a gyakorlati útmutatót.
draft: false
keywords:
- recognize text from image
- load image for ocr
- OCR region of interest
- extract text from ROI
- Python OCR library
- image preprocessing for OCR
language: hu
og_description: Ismerje fel a szöveget képről Pythonban OCR képfájl betöltésével,
  egy érdeklődési terület meghatározásával és a tiszta szöveg kinyerésével. Ismerje
  meg a teljes munkafolyamatot.
og_title: Szöveg felismerése képről – Teljes Python OCR útmutató
tags:
- OCR
- Python
- Image Processing
title: Szöveg felismerése képről – Lépésről lépésre Python OCR útmutató
url: /hu/python-java/general/recognize-text-from-image-step-by-step-python-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# szöveg felismerése képről – Teljes Python OCR útmutató

Valaha szükséged volt **szöveg felismerése képről**, de nem tudtad, hol kezdjed? Lehet, hogy van egy beolvasott űrlapod, egy nyugta, vagy egy képernyőmentés, és csak egy adott mezőben lévő szavakat szeretnéd. A jó hír, hogy néhány Python sorral betöltheted a képet OCR-hez, egyetlen területre fókuszálhatsz, és ki tudod nyerni a pontos szöveget – manuális másolás nélkül.

Ebben a bemutatóban végigvezetünk a teljes folyamaton: a kép betöltése, egy érdeklődési terület (ROI) meghatározása, az OCR motor futtatása, és az eredmény kiírása. A végére képes leszel beágyazni ezt a kódrészletet bármely projektbe, amelynek egy adott képrészletből kell szöveget kinyernie. Nincs nehéz képfeldolgozó csővezeték, csak tiszta, olvasható kód, ami ma már működik.

## Előfeltételek

- Python 3.8+ telepítve  
- Az `ocr` csomag (vagy bármely kompatibilis OCR könyvtár) – telepítsd a `pip install ocr-lib` paranccsal (cseréld ki a ténylegesen használt csomagnévre)  
- Egy PNG/JPEG kép, amely tartalmazza a beolvasni kívánt űrlapot  
- Alapvető ismeretek a Python függvényekkel és osztályokkal kapcsolatban  

Ha már magabiztos vagy ezekkel, nagyszerű—ugorj tovább. Ellenkező esetben készíts egy gyors kávét, és győződj meg róla, hogy a fenti elemek készen állnak; a későbbi lépések feltételezik, hogy minden megvan.

## 1. lépés: OCR motor példány létrehozása – a “szöveg felismerése képről” magja

Az első dolog, amire szükségünk van, egy olyan objektum, amely tud kommunikálni az OCR motorral. Gondolj rá úgy, mint az agyra, amely később **szöveg felismerése képről** adatokat fog feldolgozni.

```python
import ocr  # Import the OCR library

# Initialize the engine
ocr_engine = ocr.OcrEngine()
```

> **Miért fontos:** A motor egyszeri inicializálása lehetővé teszi a beállítások (például nyelvi csomagok) újrahasználatát több képnél, ami javítja a teljesítményt és rendezetten tartja a kódot.

## 2. lépés: Kép betöltése OCR-hez – a kép memóriába hozása

Most ténylegesen **load image for OCR**. A könyvtár egy kényelmes statikus metódust biztosít, amely beolvassa a fájlt, és egy olyan objektumot ad vissza, amelyet a motor megérthet.

```python
# Load the source image (replace the path with your own)
image_path = "YOUR_DIRECTORY/form.png"
ocr_engine.set_image(ocr.Imaging.Image.load(image_path))
```

> **Pro tip:** Ha a képed nagy, fontold meg átméretezését a betöltés előtt. A kisebb képek felgyorsítják az OCR-t anélkül, hogy a legtöbb nyomtatott szöveg pontosságát csökkentenék.

## 3. lépés: OCR érdeklődési terület (ROI) meghatározása

Gyakran nincs szükség az egész oldalra—csak egy konkrét mezőre, ahová a felhasználó adatot írt be. Egy **OCR region of interest** meghatározása azt mondja a motornak, hogy hagyja figyelmen kívül a többit, ami csökkenti a zajt és felgyorsítja a feldolgozást.

```python
# Define ROI: (left, top, width, height) in pixels
region_of_interest = ocr.Rectangle(120, 340, 560, 90)

# Register the ROI with the engine
ocr_engine.add_region_of_interest(region_of_interest)
```

> **Miért fókuszáljunk az ROI-ra?**  
> - **Sebesség:** A motor kevesebb pixelt vizsgál.  
> - **Pontosság:** Az ROI-n kívüli háttérgrafika összezavarhatja a karakterfelismerést.  
> - **Egyszerűség:** Egy tiszta karakterláncot kapsz, amely pontosan megfelel annak a mezőnek, amely érdekel.

## 4. lépés: OCR folyamat futtatása – A döntő pillanat

Minden előkészítve, végre **szöveg felismerése képről** a meghatározott ROI-ban.

```python
# Execute OCR on the specified region
ocr_result = ocr_engine.recognize()
```

Ha a motor több területet támogat, az `ocr_result` egy listát tartalmaz; egyetlen‑ROI esetünkben ez egy egyszerű objektum, amely rendelkezik egy `get_text()` metódussal.

## 5. lépés: Szöveg kinyerése és kiírása – A végső kimenet

Most kinyerjük a sima karakterláncot az eredményobjektumból, és megjelenítjük. Itt csatlakoztathatod a kimenetet egy adatbázishoz, CSV fájlhoz vagy bármilyen további logikához.

```python
# Retrieve the recognized text
extracted_text = ocr_result.get_text()

# Show the result
print("Text inside ROI:\n", extracted_text)
```

**Várható kimenet** (példa egy kitöltött név mezőre):

```
Text inside ROI:
 John Doe
```

Ha az OCR motor extra szóközöket vagy sortöréseket ad vissza, tisztíthatod őket a `.strip()` vagy egy reguláris kifejezés segítségével.

## Gyakori szélhelyzetek kezelése

| Helyzet                               | Mit tegyünk                                                               |
|---------------------------------------|---------------------------------------------------------------------------|
| **Alacsony felbontású kép**           | Nagyítsd fel a `Pillow` (`Image.resize`) segítségével a betöltés előtt. |
| **Dőlő vagy elforgatott szöveg**      | Alkalmazz forgatáskorrekciót (`ocr.Imaging.Image.rotate`).               |
| **Több nyelv**                        | Állítsd be a nyelvi csomagot a motoron: `ocr_engine.set_language('eng+spa')`. |
| **Nincs ROI definiálva**              | Hagyjuk ki a `add_region_of_interest` hívást; a motor a teljes képet dolgozza fel. |
| **Váratlan karakterek (pl. vesszők)** | Utófeldolgozd a karakterláncot: `extracted_text.replace(',', '')`.       |

Ezek a tippek biztosítják, hogy a **load image for OCR** csővezetéked robusztus marad akkor is, ha a forrásanyag nem tökéletes.

## Teljes működő példa – Másolj, illessz be, futtasd

Az alábbi teljes szkriptet beillesztheted egy `.py` fájlba, és futtathatod. Tartalmazza az összes importot, hibakezelést, valamint egy apró segédfüggvényt, amely ellenőrzi, hogy a kép létezik-e.

```python
import os
import ocr

def recognize_text_from_image(image_path: str,
                              roi: tuple = (120, 340, 560, 90)):
    """
    Recognize text from a specific region of an image.

    Parameters
    ----------
    image_path : str
        Full path to the image file.
    roi : tuple
        (left, top, width, height) defining the region of interest.

    Returns
    -------
    str
        The extracted text, stripped of surrounding whitespace.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Step 1 – create engine
    engine = ocr.OcrEngine()

    # Step 2 – load image for OCR
    engine.set_image(ocr.Imaging.Image.load(image_path))

    # Step 3 – define ROI
    left, top, width, height = roi
    engine.add_region_of_interest(ocr.Rectangle(left, top, width, height))

    # Step 4 – run OCR
    result = engine.recognize()

    # Step 5 – extract text
    text = result.get_text().strip()
    return text


if __name__ == "__main__":
    # Adjust the path to point at your form image
    img_path = "YOUR_DIRECTORY/form.png"

    try:
        roi_text = recognize_text_from_image(img_path)
        print("Text inside ROI:\n", roi_text)
    except Exception as e:
        print("OCR failed:", e)
```

A szkript futtatása kiírja a megtisztított karakterláncot az ROI-ból, így egy azonnal használható adatdarabot kapsz.

## Összegzés

Most már van egy világos, vég‑végi módszered a **szöveg felismerése képről**, először **load image for OCR**, egy pontos **OCR region of interest** meghatározásával, majd végül a tiszta szöveg kinyerésével. A megközelítés bármely Python OCR könyvtárral működik, amely követi a fent bemutatott mintát, és könnyen bővíthető több ROI, különböző nyelvek vagy előfeldolgozási lépések kezelésére.

Ezután érdemes felfedezni:

- **kép előfeldolgozás OCR-hez** (küszöbölés, zajcsökkentés) a pontosság növelése érdekében zajos beolvasásoknál.  
- A **kivont szöveg ROI-ból** eredmény felhasználása pandas DataFrame feltöltésére tömeges adat-elemzéshez.  
- Átváltás felhőalapú OCR szolgáltatásra (Google Vision, Azure Computer Vision), ha nagyobb megbízhatóságra van szükség nagy méretekben.

Próbáld ki, finomítsd a téglalap koordinátáit a saját űrlapeidhez, és nézd meg, ahogy az automatizálás átveszi a feladatot. Boldog kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}