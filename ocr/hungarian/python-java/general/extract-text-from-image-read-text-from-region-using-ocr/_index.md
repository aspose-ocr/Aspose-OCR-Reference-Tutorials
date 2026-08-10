---
category: general
date: 2026-07-05
description: Szöveg kinyerése képről Python OCR-rel. Tanulja meg, hogyan töltsön be
  képet OCR-hez, olvassa el a szöveget egy régióból, és néhány sor kóddal nyerje ki
  a számla szövegét.
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: hu
og_description: Kép szövegének kinyerése Python OCR-rel. Ez az útmutató megmutatja,
  hogyan töltsünk be képet OCR-hez, hogyan olvassunk szöveget egy területről, és hogyan
  nyerjünk gyorsan szöveget egy számlából.
og_title: Szöveg kinyerése képből – Szöveg olvasása régióból OCR-rel
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Képből szöveg kinyerése – Szöveg olvasása a régióból OCR segítségével
url: /hu/python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép szövegének kinyerése – Szöveg olvasása régióból OCR-rel

Volt már szükséged **kép szövegének kinyerésére**, de csak egy konkrét rész számít — például a számla végösszege? Nem vagy egyedül. Sok valós projektben előfordul, hogy **szöveget kell olvasni egy régióból**, a teljes képet nem kell feldolgozni. Szerencsére néhány Python sorral betölthetsz egy képet OCR-hez, definiálhatsz egy érdeklődési területet (ROI), és pontosan azokat a karaktereket nyerheted ki, amikre szükséged van.

Ebben az útmutatóban egy teljes, futtatható példán keresztül mutatjuk be, hogyan **tölts be képet OCR-hez**, állíts be egy ROI-t, és végül **nyerd ki a szöveget a számláról**. A végére egy azonnal használható kódrészletet kapsz, amely bármely népszerű, régió‑alapú felismerést támogató OCR‑könyvtárral működik.

---

## Amire szükséged lesz

- Python 3.8+ (a kód 3.10‑en is működik)  
- Egy OCR‑csomag, amely egy `OcrEngine` osztályt biztosít (a bemutatóhoz egy fiktív `ocr` modult használunk; cseréld le `pytesseract`‑re, `easyocr`‑ra vagy bármely ROI‑t támogató könyvtárra)  
- Egy minta kép — például `invoice.png` — amely tiszta, nyomtatott szöveget tartalmaz  
- Alapvető ismeretek a Python függvényekről és osztályokról (mélytanulási háttér nem szükséges)

Ha már megvannak ezek, nagyszerű — vágjunk bele. Ha nem, töltsd le a legújabb Python‑t a python.org‑ról, és telepítsd az OCR‑csomagot a `pip install your-ocr-lib` paranccsal.

---

![Kép szövegének kinyerése példa](extract-text-from-image.png "Kép szövegének kinyerése – régió‑alapú OCR bemutató")

*Az előző kép a régiót (piros téglalap) mutatja, amelyet a **kép szövegének kinyeréséhez** célozunk meg.*

---

## 1. lépés: Az OCR‑könyvtár telepítése és importálása

Először győződj meg róla, hogy az OCR‑könyvtár elérhető a környezetedben. Az alábbi importminta a legtöbb, `OcrEngine` osztályt biztosító csomagnál működik.

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **Pro tipp:** Ha `pytesseract`‑et használsz, külön kell telepítened a Tesseract binárist, és be kell állítanod a `pytesseract.pytesseract.tesseract_cmd`‑t a megfelelő útvonalra.

---

## 2. lépés: OCR‑motor létrehozása és nyelv beállítása

Az motor létrehozása egyszerű, de a nyelv megadása drámaian javítja a pontosságot, különösen olyan számlák esetén, amelyek számokat és angol szavakat tartalmaznak.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

Miért fontos ez? Az OCR‑motor nyelvi modelleket használ a karakterek előrejelzéséhez; ha megmondod, hogy angolt vár, csökken a hamis pozitív, például a „0” „O”‑ként való félreolvasása.

---

## 3. lépés: Kép betöltése OCR‑hez

Most ténylegesen **betöltjük a képet OCR‑hez**. A legtöbb könyvtár elfogad egy fájlútvonalat vagy egy Pillow képobjektumot. Itt a könyvtár beépített betöltőjét használjuk egyszerűség kedvéért.

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

Győződj meg róla, hogy az útvonal a megfelelő könyvtárra mutat; gyakori hiba, hogy elfelejtjük a relatív útvonalat, ha a szkript más munkakönyvtárból fut.

---

## 4. lépés: Érdeklődési terület (ROI) definiálása

A ROI definiálása a **szöveg olvasása régióból** lényege. Gondolj rá úgy, mint egy téglalap rajzolására a számla azon részén, ahol a végösszeg található.

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left` és `top` a téglalap bal‑felső sarkának X és Y koordinátáit jelentik.  
- `width` és `height` a doboz méretét állítják be.  
- Különböző értékekkel kísérletezhetsz egy olyan képnéző program segítségével, amely pixelkoordinátákat mutat.

> **Miért fontos a ROI:** Az egész oldal OCR‑je felesleges CPU‑ciklusokat pazarol, és gyakran zajt hoz be a nem releváns szövegekből, táblázatokból vagy grafikákból. Egy régióra fókuszálva tisztább eredményeket és gyorsabb feldolgozást kapsz.

---

## 5. lépés: OCR végrehajtása a megadott régióban

Minden beállítva, most végre **kivonjuk a szöveget a képből** — de csak a definiált ROI‑n belül.

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

A `recognize` metódus egy olyan objektumot ad vissza, amely általában a nyers karakterláncot, a biztonsági pontszámokat és néha a szavak körvonalait tartalmazza. Számunkra csak a tiszta szöveg érdekel.

---

## 6. lépés: A kinyert szöveg kiírása

Nyomtassuk ki az eredményt, és nézzük meg, mi jött ki. Ez a lépés bemutatja a **szöveg kinyerését a számláról** egy valós helyzetben.

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### Várható kimenet

```
Text inside ROI:
Total Amount: $1,245.67
```

Ha a számlád más elrendezést használ, akkor a téglalapba eső szöveget fogod látni — például számlaszámot, dátumot vagy PO‑referenciát.

---

## 7. lépés: Csomagolás újrahasználható függvénybe (opcionális)

A megoldás újrahasználhatóságának növelése érdekében csomagold a logikát egy függvénybe. Ez egyúttal bemutatja az **ocr on region** általános segédfunkcióját is.

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

Most már bármely számlával meghívhatod a függvényt:

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

---

## Gyakori hibák és elkerülésük módja

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| **Üres kimenet** | A ROI valójában nem fed le szöveget (rossz koordináták). | Ellenőrizd a pixelértékeket egy képszerkesztővel; adj hozzá vizuális hibakereső réteget. |
| **Zavaros karakterek** | Alacsony felbontású vagy rossz kontrasztú kép. | Előfeldolgozás: konvertálás szürkeárnyalatosra, küszöbölés alkalmazása (`cv2.threshold`). |
| **Rossz nyelv** | A motor alapértelmezésben olyan nyelvet használ, amely nem tartalmazza a szükséges karakterkészletet. | Állítsd be explicit módon az `ocr_engine.language`‑t `ENGLISH`‑re vagy a megfelelő helyi beállításra. |
| **Teljesítményprobléma** | Nagy képek ismételt OCR‑ja. | Méretezd át a képet betöltés előtt, vagy először vágd ki a ROI‑t, majd csak azt dolgozd fel. |

---

## A példa kibővítése: Több ROI

Néha egy számlán több mezőre is szükség van — például **szöveg kinyerése a számláról** a végösszeg és a számla dátuma esetén. Egy téglalaplista felett ciklusolhatsz:

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

Ez a minta tisztán tartja a kódot, és később könnyen hozzáadhatsz további régiókat.

---

## Összegzés

Most egy teljes, vég‑től‑végig működő munkafolyamatot mutattunk be a **kép szövegének kinyerésére** Python OCR‑vel, egy konkrét régióra fókuszálva. A **kép betöltése OCR‑hez**, egy **érdeklődési terület** definiálásával és a motor meghívásával megbízhatóan **olvasd a szöveget a régióból** — tökéletes a végösszegek számlákról, a dátumok nyugtákról vagy bármilyen más lokális adat kinyeréséhez.  

Nyugodtan kísérletezz

## Mit tanulj meg legközelebb?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}