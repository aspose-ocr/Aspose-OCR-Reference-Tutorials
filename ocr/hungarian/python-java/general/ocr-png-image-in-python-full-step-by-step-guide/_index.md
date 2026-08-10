---
category: general
date: 2026-06-06
description: OCR PNG kép Python-nal – tanulja meg, hogyan lehet szöveget kinyerni
  a képből, futtasson egy Python OCR példát, és még az ókori görög szöveget is könnyedén
  olvashassa.
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: hu
og_description: OCR PNG kép Pythonban magyarázva. Ez az útmutató megmutatja, hogyan
  lehet szöveget kinyerni a képből, futtatni egy Python OCR példát, és könnyedén olvasni
  az ókori görög nyelvet.
og_title: OCR PNG kép Pythonban – Teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR PNG kép Pythonban – Teljes lépésről lépésre útmutató
url: /hu/python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR PNG Kép Pythonban – Teljes Lépésről‑Lépésre Útmutató

Gondolkodtál már azon, hogyan **OCR PNG képet** tudsz közvetlenül egy Python szkriptből? Talán egy mappád tele van szkennelt ókori kéziratokkal, és **szöveget szeretnél kinyerni a képből** anélkül, hogy mindent kézzel gépelnél be. A jó hír, hogy nem kell PhD‑nek lenned a számítógépes látás területén – csak néhány sor kód és a megfelelő könyvtár, és már percek alatt olvasni tudsz ókori görögül.

Ebben a bemutatóban egy **python OCR példát** fogunk végigvinni, amely PNG‑ból ismeri fel a szöveget, a nyelvet görög polytonikusra állítja, és kiírja az eredményt. A végére pontosan tudni fogod, hogyan **ismerj fel képen lévő szöveget**, hogyan kezeld a gyakori buktatókat, és hogyan adaptáld a szkriptet más nyelvekre vagy képtípusokra.

## Mit Tanulhatsz Meg

- Python OCR könyvtár telepítése és konfigurálása (pytesseract + Tesseract OCR)
- OCR motor példány létrehozása és PNG fájl betöltése
- A felismerési nyelv beállítása görög polytonikusra, hogy **olvasni tudj ókori görögül**
- A felismert szöveg kiírása és tipikus problémák megoldása
- A szkript kiterjesztése több PNG kötegelt feldolgozására vagy más nyelvre váltásra

### Előfeltételek

| Követelmény | Miért fontos |
|-------------|--------------|
| Python 3.8+ | Modern szintaxis és típusjelölések |
| `pytesseract` csomag | Vékony wrapper a Tesseract motor körül |
| Tesseract OCR binárisok (≥ 5.0) | A tényleges motor, ami a nehéz munkát végzi |
| Görög nyelvi adat (`grc.traineddata`) | Szükséges a **ó görög olvasásához** |
| Egy PNG kép, amit elemezni szeretnél (pl. `ancient_greek.png`) | A **ocr png image** demó célja |

A Python oldalt a következővel telepítheted:

```bash
pip install pytesseract Pillow
```

Ubuntu/macOS rendszeren a motor telepítése:

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

Ne felejtsd el letölteni a görög polytonikus nyelvi adatot:

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

*(Az útvonal eltérhet; szükség esetén állítsd be a `TESSDATA_PREFIX` változót.)*

---

## OCR PNG Kép: Motor Példány Létrehozása

Az első dolog, amire szükségünk van, egy objektum, ami a Tesseracttal kommunikál. A `pytesseract` esetében a motor a modul‑szintű függvényeken keresztül érhető el, de a tisztaság kedvéért egy kis osztályba csomagoljuk. Ez tükrözi az eredeti kódrészletben látható „engine” koncepciót.

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**Miért csomagoljuk?**  
- Az API nyilvános felülete megegyezik az eredeti snippet‑el, így a migráció zökkenőmentes.  
- Később könnyen hozzáadhatunk naplózást vagy hibakezelést anélkül, hogy a fő folyamatot módosítanánk.  
- Jó OOP gyakorlatot mutat – amit a senior fejlesztők értékelnek.

---

## Szöveg Kinyerése Képből: Állítsd be a Nyelvet Görög Polytonikusra

Most, hogy van egy motorunk, meg kell mondanunk, milyen nyelvet várjon. A görög polytonikus diakritikus jeleket használ, amik nincsenek benne a standard „greek” adatokban, ezért a Tesseractot a `grc` tréningfájlra irányítjuk.

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

Ha valaha **szöveget szeretnél kinyerni a képből** egy másik nyelven, egyszerűen cseréld a `"grc"`‑t `"eng"`‑re angolhoz, `"fra"`‑ra franciához, stb. Ugyanez a sor minden telepített nyelvre működik.

---

## Kép Szöveg Felismerése: OCR futtatása PNG-n

A nyelv beállítása után betöltjük a PNG‑t a motorba. Az eredeti példa egy keményen kódolt útvonalat használt; most egy kicsit rugalmasabbá tesszük `Path` objektumokkal.

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**Tippek és Szélsőséges Esetek**

- **Fájl nem található** – csomagold a hívást `try/except FileNotFoundError`‑rel, hogy barátságos üzenetet kapj.  
- **Alacsony felbontású PNG** – fontold meg előfeldolgozást (pl. átméretezés, binarizálás) a Pillow‑val az OCR előtt.  
- **Nem‑görög szöveg** – a Tesseract megpróbálja dekódolni, de a pontosság drasztikusan csökken. Mindig a megfelelő nyelvet válaszd.

---

## A Felismert Szöveg Kiírása

Végül kiírjuk az eredményt. Egy valódi projektben adatbázisba, CSV‑be vagy akár egy fordítási pipeline‑ba is mentheted.

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

Amikor a szkriptet egy tiszta ókori görög felirat szkennelésén futtatod, valami ilyesmit kell látnod:

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

Ha a kimenet összezavartnak tűnik, ellenőrizd, hogy a **greek.traineddata** fájl a megfelelő mappában van-e, és hogy a PNG nem túl zajos-e.

---

## Teljes Működő Példa (Minden Lépés Egy Szkriptben)

Az alábbiakban a teljes, azonnal futtatható program látható. Mentsd `ocr_greek.py` néven és futtasd `python ocr_greek.py`.

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**Várható kimenet** (rövidítve):

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

Ha a megfelelő görög karaktereket látod, gratulálok – sikeresen végrehajtottad az **ocr png image** műveletet Pythonban!

---

## Gyakori Kérdések és Profi Tippek

### Hogyan javítható a pontosság egy zajos PNG‑n?

- Konvertáld a képet szürkeárnyalatossá: `img = img.convert('L')`  
- Alkalmazz bináris küszöböt: `img = img.point(lambda x: 0 if x < 128 else 255, '1')`  
- Növeld fel a felbontást: `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`

Ezek a lépések gyakran egy **recognize image text** rémálmot tiszta eredménnyé változtatnak.

### Feldolgozhatok egy egész mappát PNG‑kből?

Természetesen. Csomagold a `recognize_image` hívást egy `for` ciklusba, ami a `Path.glob("*.png")`‑t iterálja. Az eredményeket tárold szótárban vagy írd CSV‑be későbbi elemzéshez.

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### Mi van, ha csak számokat kell kinyerni?

Adj egy egyedi **config** stringet az `image_to_string`‑nek:

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

Így **szöveget tudsz kinyerni a képből**, amely táblázatokat, sorozatszámokat vagy időbélyegeket tartalmaz.

### Van mód a megbízhatósági pontszámok lekérésére?

Igen – használd a `pytesseract.image_to_data`‑t, ami TSV‑t ad vissza szó‑szintű megbízhatósági értékekkel. Alacsony bizalomú tokeneket kiszűrhetsz, mielőtt összeállítod a végső szöveget.

---

## A Bemutató Bővítése

Miután elsajátítottad az alapokat, érdemes ezeket a kapcsolódó témákat is felfedezni:

- **Batch OCR multiprocessing‑kel** – gyorsítsd fel a nagy PNG korpuszok feldolgozását.  
- **Hibrid OCR + NLP pipeline** – automatikusan fordítsd le az ókori görög szöveget modern angolra.  
- **Alternatív motorok** – próbáld ki az `easyocr`‑t vagy az `opencv`‑alapú módszereket speciális esetekre.  
- **Felhő alapú OCR szolgáltatások** – Google Vision, Azure Computer Vision vagy AWS Textract szerver‑nélküli skálázáshoz.

Mindegyik a most bemutatott **python OCR példára** épül, így magabiztosan merülhetsz el mélyebben.

---

## Következtetés

Egy egyszerű snippet‑ből egy robusztus **ocr png image** munkafolyamatot hoztunk létre Pythonban. Létrehoztunk egy `OcrEngine`‑t, beállítottuk a nyelvet görög polytonikusra, betápláltunk egy PNG‑t, és kiírtuk az eredményt. Most már tudod, hogyan **szöveget nyerj ki a képből**, hogyan **ismerj fel képen lévő szöveget**, és még **olvasni tudsz ókori görögül** is.

## Mit Tanulj Meg Következőként?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutató technikáira épülnek. Minden forrás komplett, működő kódrészleteket és lépésről‑lépésre magyarázatokat tartalmaz, hogy további API‑funkciókat saját projektjeidben is könnyedén alkalmazhass.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}