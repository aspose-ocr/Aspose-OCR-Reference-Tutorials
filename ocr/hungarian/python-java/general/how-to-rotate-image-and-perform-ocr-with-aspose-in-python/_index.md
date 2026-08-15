---
category: general
date: 2026-03-26
description: Tanulja meg, hogyan lehet képet forgatni és OCR-t végrehajtani Pythonban.
  Ez az útmutató bemutatja, hogyan lehet előfeldolgozni a képet OCR-hez, és hatékonyan
  kinyerni a szöveget a képből.
draft: false
keywords:
- how to rotate image
- how to perform ocr
- preprocess image for ocr
- recognize text from image
- how to extract text from image
language: hu
og_description: Hogyan forgassuk helyesen a képet, majd ismerjük fel a szöveget a
  képről az Aspose OCR segítségével. Kövesse ezt a lépésről‑lépésre útmutatót a kép
  előfeldolgozásához OCR-hez és a szöveg kinyeréséhez a képről.
og_title: Hogyan forgassunk képet és végezzünk OCR-t – Teljes Python útmutató
tags:
- Aspose
- Python
- Image Processing
- OCR
title: Hogyan forgassuk el a képet és végezzünk OCR-t az Aspose-szal Pythonban
url: /hu/python-java/general/how-to-rotate-image-and-perform-ocr-with-aspose-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan forgassunk képet és végezzünk OCR-t az Aspose segítségével Pythonban

Gondolkodtál már azon, **hogyan forgassunk képet**, hogy egy OCR motor valóban el tudja olvasni a szöveget? Lehet, hogy beolvastál egy űrlapot, ami oldalra került, vagy egy kamera felvétel 90°-kal az óramutató járásával megegyező irányban fordult. Ebben az esetben a szöveg emberi szemmel rendben látszik, de az OCR motor egy káoszt lát. A jó hír? Gyerekjáték a tájolás javítása, a kívánt terület kivágása, majd a szöveg kinyerése – mindezt néhány Python és Aspose könyvtár sorával.

Ebben az útmutatóban végigvezetünk a teljes munkafolyamaton: egy elforgatott TIFF betöltésétől, a tájolás korrigálásáig, **preprocess image for OCR**, és végül **recognize text from image**. A végére megtudod, **how to perform OCR** bármely képen, és magabiztosan **extract text from image** fájlokból.

## Amire szükséged lesz

- Python 3.8+ (a kód bármely friss verzióval működik)
- `asposeocrjava` és `asposeimaging` csomagok telepítve a `pip` segítségével
- Egy minta kép, amelynek forgatásra van szüksége (pl. `rotated_form.tif`)
- Egy kis kíváncsiság a képfeldolgozás iránt

Nem szükséges nehéz keretrendszer – csak a két Aspose csomag és egy kis Python logika.

---

## 1. lépés: Aspose csomagok telepítése (How to Perform OCR)

Mielőtt **rotate image** vagy **recognize text from image** műveleteket végezhetjük, szükségünk van a ténylegesen a nehéz munkát végző könyvtárakra.

```bash
pip install asposeocrjava asposeimaging
```

> **Pro tipp:** Ha vállalati proxy mögött vagy, add hozzá a `--proxy http://proxy:port` opciót a parancshoz. A csomagok tiszta Python wrapper-ek az Aspose .NET/Java magja köré, így a telepítés általában azonnali.

---

## 2. lépés: A forrásfájl betöltése és forgatása – A „How to Rotate Image” lényeges lépés

```python
from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

# Load the original, incorrectly oriented image
source_image = Image.load("YOUR_DIRECTORY/rotated_form.tif")

# Rotate 90° clockwise – this fixes the orientation for OCR
rotated_image = source_image.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)
```

> **Miért forgatunk?** A legtöbb OCR motor feltételezi, hogy a szöveg balról jobbra és fentről lefele folyik. Ha a bitmap oldalra fordul, a motor vagy értelmetlen szöveget, vagy semmit nem ad vissza. A forgatás a pixelrácsot a várt olvasási sorrendhez igazítja, drámai módon javítva a pontosságot.

> **Különleges eset:** Ha nem vagy biztos benne, hogy a képnek 90°, 180° vagy 270°-os fordításra van-e szüksége, ellenőrizheted a `source_image.width` és `source_image.height` értékeket, vagy használhatod az `exif` orientációs címkéket. Az Aspose `rotate_flip` metódusa támogatja a `ROTATE_180` és `ROTATE_270_CLOCKWISE` opciókat is.

> **Image preview (optional):**  
> ![hogyan forgassunk képet példa](/assets/rotate-demo.png "Hogyan forgassunk képet – forgatás előtti és utáni állapot")

---

## 3. lépés: A érdeklődésre számító terület kivágása – Preprocess Image for OCR

Gyakran csak a lap egy kis részére van szükség – például egy aláírás mezőre vagy egy számblokkra. A kivágás eltávolítja a zajt és felgyorsítja a **how to perform OCR** folyamatot.

```python
# Define the rectangle that encloses the text you care about
# (x=100, y=200, width=800, height=300) – adjust to your form
roi = Rectangle(100, 200, 800, 300)

# Crop the rotated image to that rectangle
roi_image = rotated_image.crop(roi)
```

> **Miért vágunk?** A kép méretének csökkentése korlátozza az OCR motor keresési területét, ami csökkenti a hamis pozitív találatokat és lerövidíti a feldolgozási időt. Emellett segít, ha a forrásfájl vízjeleket vagy egyéb grafikákat tartalmaz, amelyek összezavarhatják a motort.

> **Tipp:** Ha több mezővel dolgozol, ismételd meg a kivágási lépést különböző téglalapokkal, és futtasd az OCR-t minden darabon külön.

---

## 4. lépés: Az OCR motor inicializálása – A „How to Perform OCR” alapja

```python
# Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

> **A háttérben:** Az Aspose OCR a Tesseract és egy saját képanalízis kombinációját használja. A motor egyszeri példányosítása és többszöri újrahasználata több kép esetén hatékonyabb, mint minden alkalommal új objektum létrehozása.

---

## 5. lépés: A kivágott kép betáplálása és a szöveg felismerése – How to Extract Text from Image

```python
# Set the cropped image as the input for OCR
ocr_engine.set_image(roi_image)

# Run the recognition process
result = ocr_engine.recognize()

# Extract the plain text
extracted_text = result.get_text()
print(extracted_text)
```

### Várt kimenet

Ha a ROI (érdeklődésre számító terület) a „Invoice #12345 – Paid” kifejezést tartalmazza, valami ilyesmit fogsz látni:

```
Invoice #12345 – Paid
```

Ha az OCR nehezen boldogul, előfordulhatnak felesleges szóközök vagy helytelen karakterek (pl. „Invo1ce #I2345 – Pa1d”). Itt jönnek képbe a **preprocess image for OCR** trükkök – például a kontraszt beállítása vagy binarizálás alkalmazása. Az Aspose további szűrőket kínál, amelyeket az 5. lépés előtt láncolhatsz, de a fenti alapfolyamat a legtöbb tiszta szkennél működik.

---

## 6. lépés: Opcionális – Az OCR beállítások finomhangolása (Advanced “How to Perform OCR”)

```python
# Example: Restrict recognition to English alphanumerics only
ocr_engine.get_recognition_settings().set_recognition_language("en")
ocr_engine.get_recognition_settings().set_characters_blacklist("!@#$%^&*()")
```

> **Mikor használjuk:** Akkor használd, ha a dokumentum sok díszítő szimbólumot tartalmaz, amelyekre nincs szükséged. A tiltólista csökkenti a hamis detektálásokat.

---

## Teljes vég‑végi szkript

Mindent összegezve, itt egy azonnal futtatható szkript, amely **how to rotate image**, **preprocess image for OCR**, és végül **recognize text from image**:

```python
# -*- coding: utf-8 -*-
"""
Complete example: rotate, crop, and OCR an image with Aspose.
Author: Your Name
Date: 2026-03-26
"""

from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

def ocr_rotated_image(
    input_path: str,
    output_path: str = None,
    crop_rect: Rectangle = Rectangle(100, 200, 800, 300)
) -> str:
    """
    Loads an image, rotates it 90° clockwise, crops the region of interest,
    runs OCR, and returns the extracted text.

    Parameters
    ----------
    input_path : str
        Path to the original (possibly rotated) image file.
    output_path : str, optional
        If provided, saves the processed (rotated + cropped) image for inspection.
    crop_rect : Rectangle, optional
        Rectangle defining the ROI. Adjust to match your document layout.

    Returns
    -------
    str
        The plain text extracted from the ROI.
    """
    # Load and rotate
    src = Image.load(input_path)
    rotated = src.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)

    # Crop to region of interest
    roi = rotated.crop(crop_rect)

    # Optionally save the processed image for debugging
    if output_path:
        roi.save(output_path)

    # OCR
    engine = OcrEngine()
    engine.set_image(roi)
    result = engine.recognize()
    return result.get_text()

if __name__ == "__main__":
    text = ocr_rotated_image(
        "YOUR_DIRECTORY/rotated_form.tif",
        output_path="processed_roi.png"
    )
    print("=== Extracted Text ===")
    print(text)
```

A szkript futtatása kiírja a felismert szöveget a konzolra, és elmenti a feldolgozott ROI vizuális megjelenítését `processed_roi.png` néven. Megnyithatod ezt a PNG-t, hogy ellenőrizd, a forgatás és a kivágás a várt módon működött-e.

---

## Gyakori kérdések és buktatók

| Question | Answer |
|----------|--------|
| **Mi van, ha a kép már függőlegesen áll?** | A forgatási lépés idempotens – egy helyesen orientált kép 90°‑os forgatása nyilvánvalóan tönkreteszi, ezért a `rotate_flip` hívása előtt ellenőrizned kell a `source_image.width` és `height` értékeket, vagy használhatod az EXIF orientációs adatokat. |
| **Az OCR kimenetem extra sortöréseket tartalmaz.** | Használd a `result.get_text().replace("\n", " ").strip()` függvényt a tisztításhoz, vagy engedélyezd a `ocr_engine.get_recognition_settings().set_remove_line_breaks(True)` beállítást. |
| **Feldolgozhatok PDF-eket közvetlenül?** | Igen – az Aspose Imaging képes PDF oldalakat képként betölteni (`Image.load("file.pdf")`), ezután ugyanazokat a forgatási és OCR lépéseket követheted. |
| **Van mód sok fájl kötegelt feldolgozására?** | Tegyük a `ocr_rotated_image` függvényt egy könyvtáron végig iteráló ciklusba, vagy használjuk a Python `concurrent.futures` modulját a párhuzamos feldolgozáshoz. |
| **Hogyan kezeljem az angolon kívüli nyelveket?** | Állítsd be a felismerési nyelvet a `ocr_engine.get_recognition_settings().set_recognition_language("fr")` hívással, például franciához, stb. |

---

## Következtetés

Áttekintettük, hogyan **how to rotate image** helyesen, hogyan **preprocess image for OCR** a kivágással, és végül **how to perform OCR** a **recognize text from image** és **extract text from image** segítségével az Aspose Python könyvtáraival. A teljes szkript egy gyakorlati, termelés‑kész munkafolyamatot mutat be, amelyet bármely automatizálási csővezetékbe beilleszthetsz.

Ha készen állsz a továbblépésre, próbálj ki a következőkkel:

- **Képjavítás** (kontraszt, binarizálás) OCR előtt
- **Több ROI kinyerés** űrlapok több mezőjéhez
- **Kötegelt feldolgozás** a beolvasott dokumentumok teljes mappáiról
- **Integráció** a downstream rendszerekkel (pl. a kinyert adatok adatbázisba való betáplálása)

Nyugodtan igazítsd a kódot a saját felhasználási esetedhez, és jó kódolást! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}