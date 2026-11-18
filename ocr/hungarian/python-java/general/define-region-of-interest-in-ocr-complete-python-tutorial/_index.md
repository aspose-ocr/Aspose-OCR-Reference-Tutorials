---
category: general
date: 2026-06-16
description: Határozza meg az érdeklődési területet az OCR-ben a spanyol szöveg kinyeréséhez
  a személyi igazolványokról. Tanulja meg, hogyan töltsön be képet az OCR-hez, és
  hatékonyan adja meg az ROI-t.
draft: false
keywords:
- define region of interest
- load image for ocr
- how to specify roi
- extract id card text
- extract spanish text image
language: hu
og_description: Határozza meg az érdeklődési területet az OCR-ben a spanyol szöveg
  kinyeréséhez a személyi igazolványokról. Lépésről lépésre útmutató a képek betöltéséhez
  és az ROI megadásához.
og_title: Érdeklődési terület meghatározása az OCR-ben – Teljes Python oktatóanyag
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Define region of interest in OCR to extract Spanish text from ID cards.
    Learn how to load image for OCR and specify ROI efficiently.
  headline: Define region of interest in OCR – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Érdeklődési terület meghatározása az OCR-ben – Teljes Python útmutató
url: /hu/python-java/general/define-region-of-interest-in-ocr-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definiálja az érdeklődési területet az OCR-ben – Teljes Python útmutató

Gondolta már, hogyan **definiálja az érdeklődési területet az OCR-ben**, hogy csak a képből a szükséges részt olvassa? Ebben az útmutatóban lépésről lépésre végigvezetjük ezen, valamint megmutatjuk, hogyan **töltsön be képet az OCR-hez** és hogyan nyerjen ki spanyol szöveget egy személyi igazolványról néhány Python sorral.  

Ha már unott már egy zajos szkennel, és azt gondolta: „Biztos van tisztább módja a névmező kinyerésének”, akkor jó helyen jár. A végére képes lesz a személyi igazolvány szövegét kinyerni anélkül, hogy a háttérzajba botlana.

## Mit fog megtanulni

- Miért kell **definiálni az érdeklődési területet** az OCR futtatása előtt.  
- A pontos lépések a **kép betöltéséhez OCR-hez** egy népszerű Python OCR csomaggal.  
- Hogyan **megadja az ROI-t** pixelkoordinátákkal.  
- Hogyan **megbízhatóan kinyerje az igazolvány szövegét**, még akkor is, ha a forrásnyelv spanyol.  
- Tippek a szélhelyzetek kezelésére, például elfordított kártyák vagy alacsony kontrasztú szkennek.  

Előzetes OCR tudás nem szükséges – csak egy működő Python 3 környezet és egy JPEG a tesztelni kívánt személyi igazolványról.

---

![Define region of interest illustration](placeholder.png){alt="Érdeklődési terület példája, amely egy kiemelt téglalapot mutat egy személyi igazolvány képen"}

## 1. lépés: Az OCR könyvtár telepítése és importálása

Először is szüksége van egy könyvtárra, amely egy `OcrEngine` osztályt biztosít, hasonlóan a korábban látott kódrészlethez. Ebben az útmutatóban a fiktív `ocr` csomagot használjuk, de ugyanazok a koncepciók érvényesek a `pytesseract`, `easyocr` vagy bármely olyan csomag esetén, amely lehetővé teszi a nyelv és az ROI beállítását.

```bash
pip install ocr   # Replace with the actual package name you use
```

```python
# Import the library and any helper classes
import ocr
from ocr import Rectangle, Image
```

*Pro tipp:* Ha a `pytesseract`-ot használja, a `Rectangle` osztály egyszerűen egy `(left, top, width, height)` tuple lesz. A többi rész ugyanúgy működik.

## 2. lépés: Kép betöltése OCR-hez

Most **betöltjük a képet OCR-hez**. A motor egy `ocr.Image` objektumot vár, ezért mutassuk rá a fájlra, amely az igazolványt tartalmazza. Győződjön meg róla, hogy az útvonal abszolút vagy a szkript munkakönyvtárához relatív.

```python
# Create the OCR engine instance
engine = ocr.OcrEngine()

# Tell the engine which language we’re interested in – Spanish in this case
engine.language = ocr.Language.SPANISH

# Load the source image that contains the text to be recognized
engine.image = Image.load_from_file("YOUR_DIRECTORY/id-card.jpg")
```

Ha a kép nagyon nagy, érdemes előbb átméretezni; az OCR motorok gyorsabban dolgoznak 1500 px szélesség alatti képeken.

## 3. lépés: Hogyan adja meg az ROI-t (Érdeklődési terület definiálása)

Itt jön a tutorial középpontja: **hogyan adja meg az ROI-t**. Egy érdeklődési terület egyszerűen egy téglalap, amely azt mondja az OCR motornak: „Csak ezen pixelhatárokon belül nézz”. Olyan, mintha egy dobozt rajzolna a névmező köré egy személyi igazolványon.

```python
# Define the region of interest – left, top, width, height (all in pixels)
engine.region_of_interest = Rectangle(
    left=120,   # X‑coordinate of the left edge
    top=80,     # Y‑coordinate of the top edge
    width=340,  # Width of the box
    height=200  # Height of the box
)
```

Miért ezek a számok? A mintaképünkben a név körülbelül 120 px-re van a bal szegélytől és 80 px-re a felső szegélytől. Igazítsa őket a saját kártyái elrendezéséhez.  

*Szélhelyzet:* Ha a kártya 90°-kal el van fordítva, cserélje fel a `width` és `height` értékeket, és ennek megfelelően módosítsa a `left`/`top` értékeket, vagy előre forgassa el a képet a Pillow-val, mielőtt a motorhoz adná.

## 4. lépés: OCR végrehajtása az ROI-n belül

Az ROI definiálása után a motor figyelmen kívül hagyja a téglalapon kívül eső részeket. Ez nem csak felgyorsítja a feldolgozást, hanem csökkenti a háttérgrafikák által okozott hamis pozitív eredményeket is.

```python
# Run OCR only inside the defined ROI
roi_result = engine.recognize()
```

A `recognize()` hívás egy olyan objektumot ad vissza, amely tartalmazza a felismert szöveget, a megbízhatósági pontszámokat és a szavak körvonalait.

## 5. lépés: Igazolvány szövegének kinyerése (és a spanyol kimenet ellenőrzése)

Végül **kinyerjük az igazolvány szövegét** az ROI eredményéből és kiírjuk. Mivel korábban a nyelvet spanyolra állítottuk, az OCR motor nyelvspecifikus szótárakat használ, ami javítja a pontosságot az olyan ékezetes karaktereknél, mint a „ñ” vagy „á”.

```python
# Output the recognized text from the ROI
print("ROI text:", roi_result.text)
```

### Várható kimenet

```
ROI text: JUAN PÉREZ GARCÍA
```

Ha szemét karaktereket lát, ellenőrizze, hogy a kép valóban spanyol nyelvű-e, és hogy az OCR könyvtár nyelvi adatfájljai telepítve vannak-e.

## Gyakori buktatók és elkerülésük módja

| Tünet | Valószínű ok | Megoldás |
|---------|--------------|-----|
| Üres karakterlánc visszatér | Az ROI nem metszi a szöveget | Ellenőrizze a koordinátákat képnézővel; használja a `engine.debug_draw_roi()`-t, ha elérhető. |
| Sok szemét karakter | Rossz nyelvi csomag | Telepítse újra a spanyol nyelvi adatokat vagy váltson `ocr.Language.AUTO`-ra. |
| Alacsony megbízhatósági pontszám | A kép homályos vagy alacsony kontrasztú | Előfeldolgozás OpenCV-vel – alkalmazzon `cv2.GaussianBlur`-t és `cv2.threshold`-ot. |
| Az OCR a teljes képen fut az ROI ellenére | Régebbi könyvtárverzió használata | Frissítse a legújabb `ocr` csomagra; a régebbi verziók figyelmen kívül hagyták az ROI-t. |

## Példa kiterjesztése: Több ROI

Néha több mezőt is ki kell nyerni (pl. név és személyi szám). A minta ugyanaz: módosítsa a `engine.region_of_interest`-t és hívja újra a `recognize()`-t.

```python
# ROI for the ID number (different coordinates)
engine.region_of_interest = Rectangle(120, 300, 340, 80)
id_result = engine.recognize()
print("ID Number:", id_result.text)
```

Ha a könyvtár támogatja, egy listát is batch‑feldolgozhat a téglalapokból, ami csökkenti a motorhoz való többszöri hívásokat.

## Teljes működő szkript

Mindent összegezve, itt egy kész‑futású szkript, amely **definiálja az érdeklődési területet**, **betölti a képet OCR-hez**, és **kivonja a spanyol szöveget** egy személyi igazolványról.

```python
import ocr
from ocr import Rectangle, Image

def extract_name_from_id(image_path):
    """
    Loads an image, defines a ROI around the name field,
    runs OCR in Spanish, and returns the recognized text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.SPANISH
    engine.image = Image.load_from_file(image_path)

    # Adjust these numbers to match your card layout
    engine.region_of_interest = Rectangle(left=120, top=80, width=340, height=200)

    result = engine.recognize()
    return result.text.strip()

if __name__ == "__main__":
    name = extract_name_from_id("YOUR_DIRECTORY/id-card.jpg")
    print("Extracted Name:", name)
```

Futtassa a szkriptet, és a névnek meg kell jelennie a konzolon. Cserélje ki a téglalap értékeit más mezők célzásához, és egy újrahasználható segédeszközt kap minden ID‑kártya‑típusú dokumentumhoz.

## Következő lépések

- **Batch feldolgozás:** Egy mappában lévő személyi igazolványok bejárása és minden kinyert név CSV‑fájlba mentése.  
- **Nyelvfelismerés:** Engedje a felhasználót dinamikusan kiválasztani a nyelvet; a `ocr.Language.AUTO` hasznos lehet.  
- **Utófeldolgozás:** Alkalmazzon regex mintákat a gyakori OCR hibák tisztításához (pl. cserélje a „0”‑t „O”‑ra, ha nevekben jelenik meg).  

Az **érdeklődési terület definiálásának** elsajátításával egy hatékony módszert nyitott meg az **igazolvány szövegének gyors és pontos kinyerésére**, különösen spanyol nyelvű dokumentumok esetén.

---

### TL;DR

Megmutattuk, hogyan **definiálja az érdeklődési területet az OCR-ben**, **betölti a képet OCR-hez**, és **hogyan adja meg az ROI-t** a **spanyol szöveg kinyeréséhez** egy személyi igazolványról. A teljes példa egy perc alatt lefut, és néhány koordináta módosítással bármely elrendezéshez alkalmazható. Próbálja ki, állítsa be a téglalapot, és nézze, ahogy az OCR egy lézerhez hasonlóan fókuszál.

Boldog kódolást!


## Mit érdemes még megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen további API funkciók elsajátításában és alternatív megvalósítási megközelítések felfedezésében saját projektjeiben.

- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}