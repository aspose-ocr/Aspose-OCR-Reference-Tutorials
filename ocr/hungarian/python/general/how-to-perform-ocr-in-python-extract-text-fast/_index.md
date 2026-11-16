---
category: general
date: 2026-03-26
description: Tanulja meg, hogyan végezhet OCR-t Pythonban, és egyszerűen kinyerheti
  a szöveget képből, beolvashatja a szöveget szkennelésből, vagy kinyerheti a szöveget
  számláról egy egyszerű OcrEngine segítségével.
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from scan
- extract text from invoice
- how to use OCR
language: hu
og_description: Hogyan végezzünk OCR-t Pythonban? Ez az útmutató megmutatja, hogyan
  lehet szöveget kinyerni képből, beolvasni szöveget szkennelésből, és percek alatt
  szöveget kinyerni számlából.
og_title: Hogyan végezzünk OCR-t Pythonban – Szöveget gyorsan kinyerni
tags:
- OCR
- Python
- Image Processing
title: Hogyan hajtsunk végre OCR-t Pythonban – Gyors szövegkivonás
url: /hu/python/general/how-to-perform-ocr-in-python-extract-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan végezzünk OCR-t Pythonban – Szöveg gyors kinyerése

Gondolkodtál már azon, **hogyan végezzünk OCR-t** egy beolvasott nyugta vagy egy homályos PDF esetén? Nem vagy egyedül. Sok projektben a **szöveg kinyerése képből** szükségessé válik hamarabb, mint később, és a szokásos „mindent kézzel beírni” megközelítés egyszerűen nem skálázható.  

Ebben a bemutatóban egy teljes, azonnal futtatható példát látsz, amely megmutatja, **hogyan használjunk OCR-t** a szöveg beolvasásához, adatok kinyeréséhez egy számláról, és még az automatikus dőléskorrekció kezeléséhez – mindezt csak néhány Python sorral.

## Mit fogsz megtanulni

* A pontos függőségek és importok, amelyekre szükség van.
* Hogyan hozzunk létre és konfiguráljunk egy `OcrEngine` példányt.
* Módszerek a **szöveg kinyerése képből**, **szöveg beolvasása szkennelésből**, és **szöveg kinyerése számláról** ugyanazzal a motorral.
* Gyakori buktatók (rossz nyelv, hiányzó fájlok, nagy képek) és azok elkerülése.
* Várható kimenet, hogy ellenőrizhesd, sikeres volt-e az OCR.

Nincs szükség külső dokumentációs hivatkozásokra – minden önálló, így a kódot egyszerűen másolhatod‑beillesztheted, és azonnal láthatod az eredményt.

## Előfeltételek

* Python 3.8+ telepítve (az `ocr` csomag bármely friss verzióval működik).
* Az `ocr` könyvtár elérhető (`pip install ocr‑engine` – cseréld le a tényleges csomagnévre, ha más).
* Egy képfájl, amelyet feldolgozni szeretnél – a bemutatóhoz a `invoice.png` fájlt használjuk, amely a `YOUR_DIRECTORY` mappában található.

Ennyi. Ha már megvannak ezek, kezdheted is.

## Step 1: Install and Import the OCR Module

Első lépésként szükségünk van az OCR könyvtárra. Ha még nem telepítetted, futtasd a következő parancsot a terminálodban:

```bash
pip install ocr-engine
```

Most importáljuk a modult a szkriptünkben.

```python
# Step 1: Import the OCR module
import ocr
```

> **Pro tip:** Tartsd tisztán a virtuális környezeted; ez megakadályozza a verzióütközéseket, amikor később más kép‑feldolgozó csomagokat adsz hozzá.

## Step 2: Create and Configure the OCR Engine

A motor létrehozása olyan egyszerű, mint a konstruktor meghívása, de az igazi erő a helyes konfigurációban rejlik. Beállítjuk a nyelvet angolra, és bekapcsoljuk az automatikus dőléskorrekciót, ami elengedhetetlen a tökéletesen igazítotttól eltérő beolvasott számlák esetén.

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Step 3: Configure the engine – set language and enable automatic skew correction
engine.language = ocr.Language.English   # any supported language, e.g., Spanish, French
engine.auto_skew = True                 # fixes tilted scans automatically
```

Miért engedélyezzük az `auto_skew`-et? Sok szkenner olyan képeket készít, amelyek néhány fokkal el vannak fordítva. Korrekció nélkül a motor kihagyhat karaktereket, és egy tökéletesen olvasható számlát érthetetlen szöveggé változtathat.

## Step 3: Perform OCR on Your Target Image

Most betápláljuk a képfájlt a motorba. A `recognize_image` metódus egy olyan objektumot ad vissza, amely a nyers szöveget és a biztonsági pontszámokat (ha a könyvtár biztosítja) tartalmazza.

```python
# Step 4: Perform OCR on the target image
ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

Ha **szöveg beolvasása szkennelésből** szituációval dolgozol, egyszerűen cseréld le az útvonalat a PNG‑re vagy JPEG‑re konvertált beolvasott PDF‑re. Ugyanaz a hívás bármely, az alaprendszer által támogatott képformátummal működik.

## Step 4: Inspect and Use the Extracted Text

Nyomtassuk ki a nyers OCR kimenetet. Egy valós számlafeldolgozó folyamatban valószínűleg elemeznéd ezt a karakterláncot, kinyernéd a tételeket, összegeket és dátumokat, de most egy gyors pillantás is megerősíti, hogy az OCR sikeres volt.

```python
# Step 5: Display the raw extracted text
print("Raw OCR text:\n", ocr_result.text)
```

**Várható kimenet (rövidítve a tömörség kedvéért):**

```
Raw OCR text:
 Invoice #12345
 Date: 2026‑03‑01
 Bill To: Acme Corp.
 Item          Qty   Price   Total
 ------------------------------------------------
 Widget A      10    5.00    50.00
 Widget B      5     12.00   60.00
 ------------------------------------------------
 Subtotal:                     110.00
 Tax (5%):                     5.50
 Grand Total:                  115.50
```

Ha a kimenet értelmetlennek tűnik, ellenőrizd, hogy a kép tiszta‑e, és hogy az `engine.language` megegyezik a dokumentum nyelvével.

## Step 5: Handling Common Edge Cases

### Large Images

Nagy felbontású, például 5000 × 5000 pixeles szkennelés memóriaigényes lehet. Egy gyors megoldás, ha a képet lecsökkented, mielőtt a motorhoz küldenéd:

```python
from PIL import Image

def load_and_resize(path, max_dim=2000):
    img = Image.open(path)
    img.thumbnail((max_dim, max_dim), Image.ANTIALIAS)
    return img

scaled_image = load_and_resize("YOUR_DIRECTORY/invoice.png")
ocr_result = engine.recognize_image(scaled_image)
```

### Multiple Languages

Ha olyan **szöveg kinyerése képből** van szükséged, amely angolt és spanyolt is tartalmaz, beállíthatsz egy nyelvlistát:

```python
engine.language = [ocr.Language.English, ocr.Language.Spanish]
```

A motor megpróbálja felismerni mindkét nyelv karaktereit.

### Error Handling

Soha ne feltételezd, hogy a fájl létezik. Tedd a hívást egy try‑except blokkba, hogy barátságos üzenetet adhass:

```python
try:
    ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
    print("OCR succeeded!")
except FileNotFoundError:
    print("Error: The image file was not found. Check the path and try again.")
except ocr.OcrError as e:
    print(f"OCR failed with error: {e}")
```

## Visual Reference

Az alábbi képernyőkép a bemutatóban használt mintaszámlát mutatja. Figyeld meg a kis dőlést – éppen ezt korrigálja az `auto_skew`.

![how to perform OCR on an invoice](/images/ocr-example.png)

*Alt text:* hogyan végezzünk OCR-t egy számla képen, amely automatikus dőléskorrekciót mutat.

## Full, Runnable Example

Mindent egy helyen összerakva, itt egy önálló szkript, amelyet a parancssorból futtathatsz. Tartalmazza a telepítést, konfigurációt, hibakezelést, és egy egyszerű utófeldolgozási lépést, amely a kinyert szöveget az `output.txt` fájlba írja.

```python
# full_ocr_demo.py
# -------------------------------------------------
# Demonstrates how to perform OCR, extract text from image,
# read text from scan, and extract text from invoice.
# -------------------------------------------------

import ocr
from pathlib import Path

def main(image_path: str, output_path: str = "output.txt"):
    # Create and configure the engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.auto_skew = True

    # Verify the image exists
    if not Path(image_path).is_file():
        print(f"❌  Image not found: {image_path}")
        return

    # Run OCR
    try:
        result = engine.recognize_image(image_path)
    except ocr.OcrError as err:
        print(f"❌  OCR failed: {err}")
        return

    # Output the raw text
    print("✅  OCR completed. Raw text:")
    print(result.text)

    # Save to a text file for later processing
    Path(output_path).write_text(result.text, encoding="utf-8")
    print(f"💾  Text saved to {output_path}")

if __name__ == "__main__":
    # Replace with your actual file location
    main("YOUR_DIRECTORY/invoice.png")
```

A `python full_ocr_demo.py` futtatása kiírja a kinyert szöveget a konzolra, és elmenti az `output.txt`‑be. Innen már alkalmazhatsz reguláris kifejezéseket, CSV‑írókat vagy bármilyen más logikát, amelyre a **szöveg kinyerése számláról** automatizáláshoz szükséged van.

## Conclusion

Most már van egy szilárd, vég‑től‑végig megoldásod arra, **hogyan végezzünk OCR-t** Pythonban. Egy `OcrEngine` létrehozásával, a nyelv és a dőléskorrekció beállításával, valamint néhány gyakorlati edge case kezelésével megbízhatóan **szöveg kinyerése képből**, **szöveg beolvasása szkennelésből**, és **szöveg kinyerése számláról** végezhetsz anélkül, hogy szétszórt dokumentációt kellene átböngészned.

Mi a következő? Próbálj meg egy fájlkészletet egy ciklusba betáplálni, kísérletezz különböző nyelvekkel, vagy csatlakoztasd a kimenetet egy PDF‑generáló könyvtárhoz, hogy kereshető PDF‑eket hozz létre. A lehetőségek végtelenek, és a most látott kód egy stabil kiindulópont.

Van kérdésed egy konkrét fájlformátummal kapcsolatban, vagy segítségre van szükséged a biztonsági küszöbök finomhangolásához? Írj egy megjegyzést alább – szívesen segítek finomhangolni az OCR‑csővezetékedet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}