---
category: general
date: 2026-06-28
description: Előfeldolgozza a képet OCR-hez automatikus forgatással, binarizálással
  és zajcsökkentéssel Pythonban. Strukturált JSON kimenetet kap egy OCR motor segítségével.
draft: false
keywords:
- preprocess image for OCR
- auto rotate image OCR
- OCR engine Python
- OCR structured JSON output
- image binarization for OCR
- denoise OCR image
language: hu
og_description: Előfeldolgozza a képet OCR-hez automatikus forgatással, binarizálással
  és zajcsökkentéssel Pythonban. Tanulja meg, hogyan lehet strukturált JSON-t kinyerni
  egy OCR-motor segítségével.
og_title: Kép előfeldolgozása OCR-hez – Teljes Python útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Preprocess image for OCR with auto‑rotate, binarization and denoising
    in Python. Get structured JSON output using an OCR engine.
  headline: Preprocess Image for OCR – Complete Python Guide
  type: TechArticle
- description: Preprocess image for OCR with auto‑rotate, binarization and denoising
    in Python. Get structured JSON output using an OCR engine.
  name: Preprocess Image for OCR – Complete Python Guide
  steps:
  - name: '**Binarization** – converting the picture to pure black‑and‑white, which
      sharpens character edges.'
    text: '**Binarization** – converting the picture to pure black‑and‑white, which
      sharpens character edges.'
  - name: '**Denoising** – removing speckles that the OCR engine might mistake for
      glyphs.'
    text: '**Denoising** – removing speckles that the OCR engine might mistake for
      glyphs.'
  - name: '**Add language packs** (`engine.set_language(''eng+spa'')`) for multilingual
      documents.'
    text: '**Add language packs** (`engine.set_language(''eng+spa'')`) for multilingual
      documents.'
  - name: '**Integrate with Pandas** to turn the JSON tables into DataFrames for analytics.'
    text: '**Integrate with Pandas** to turn the JSON tables into DataFrames for analytics.'
  - name: '**Run batch processing** by looping over a folder of images and appending
      results to a master JSON file.'
    text: '**Run batch processing** by looping over a folder of images and appending
      results to a master JSON file.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Képek előfeldolgozása OCR-hez – Teljes Python útmutató
url: /hu/python/general/preprocess-image-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép előfeldolgozása OCR-hez – Teljes Python útmutató

Valaha is elgondolkodtál, hogyan **preprocess image for OCR**, hogy a motor valóban azt olvassa, amit látsz? Nem vagy egyedül — a legtöbb fejlesztő ugyanarra a problémára bukkan, amikor a beolvasott dokumentumok összezavarodottak. A jó hír? Néhány jól elhelyezett lépés — auto‑rotate, binarization és denoising — egy rendetlen fényképet tiszta, gép‑olvasható szöveggé alakíthat.

Ebben az útmutatóban végigvezetünk egy **Python** munkafolyamaton, amely nem csak megtisztítja a képet, hanem egy szépen strukturált JSON fájlt is visszaad. A végére tudni fogod, hogyan auto‑rotate-olj egy képet OCR-hez, hogyan alkalmazz image binarization‑t OCR-hez, és még az OCR image adatokat is denoise‑old, mielőtt egy **OCR engine Python** példányba táplálnád.

## Amire szükséged lesz

Mielőtt belevágnánk, győződj meg róla, hogy a következők telepítve vannak a gépeden:

- Python 3.9+ (bármely friss verzió megfelelő)
- `Pillow` a képek kezeléséhez (`pip install pillow`)
- `ocrutil` — egy fiktív segédkönyvtár, amely becsomagolja az OCR motort (telepítés: `pip install ocrutil`)
- Egy példa ferde kép (`skewed.jpg`) egy olyan mappában, amelyre hivatkozhatsz

Ennyi — nincs nehéz keretrendszer, nincs GPU varázslat. Csak tiszta Python és néhány hasznos könyvtár.

## 1. lépés: Kép betöltése – OCR előkészítése

Először is szükségünk van egy képobjektumra, amelyet a pipeline többi része felhasználhat.

```python
from PIL import Image
import ocrutil

# Load the image you want to process
img_path = "YOUR_DIRECTORY/skewed.jpg"
img = Image.open(img_path)          # Pillow gives us a convenient Image object
print(f"Loaded image size: {img.size}")
```

*Miért fontos ez:* A kép Pillow‑al történő betöltése biztosítja, hogy megőrizzük az összes eredeti pixeladatot, ami kulcsfontosságú a későbbi binarization során. Ennek a lépésnek a kihagyása vagy egy alacsony minőségű betöltő használata már most tönkreteheti az OCR pontosságát.

## 2. lépés: Kép auto‑rotate‑olása OCR-hez (auto rotate image OCR)

Egy telefonról készült fénykép gyakran ferdén vagy akár fejjel lefelé áll. Az `ocrutil.auto_rotate` segédfüggvény felismeri a szöveg alapvonalát és ennek megfelelően elforgatja a képet.

```python
# Automatically correct 90°/180° rotation
img = ocrutil.auto_rotate(img)
print("Auto‑rotation applied.")
```

*Pro tipp:* Ha tudod, hogy a dokumentumaid mindig függőlegesen állnak, kihagyhatod ezt a lépést, de a „auto rotate image OCR” a valóságban rengeteg kézi tisztítást takarít meg.

## 3. lépés: Kép előfeldolgozása OCR-hez – Binarizáció + Denoising

Most jön a lényeg: **preprocess image for OCR**. A két leghatékony trükk:

1. **Binarizáció** — a kép átalakítása tiszta fekete‑fehér formába, ami élesíti a karakterek kontúrjait.
2. **Denoising** — a zajpontok eltávolítása, amelyeket az OCR motor glyph‑ként értelmezhet.

```python
# Apply preprocessing: binarization + denoising
img = ocrutil.preprocess(img)   # Under the hood: thresholding + median filter
print("Preprocessing completed.")
```

Ha megnézed a képet a lépés után (pl. `img.show()`), szembetűnő kontrasztot látsz a háttérrel — pontosan azt, amit egy jó OCR motor igényel.

## 4. lépés: OCR motor beállítása (OCR engine Python)

Egy tiszta képpel a kezünkben példányosítjuk az OCR motort. Az `ocrutil.OcrEngine` osztály egy népszerű nyílt‑forrású OCR backendet (gondoljunk a Tesseract‑ra) csomagol be, miközben egy barátságos Python API‑t kínál.

```python
# Create and configure the OCR engine
engine = ocrutil.OcrEngine()
engine.set_image(img)           # Feed the preprocessed image
print("Engine ready for recognition.")
```

*Miért csináljuk:* A előfeldolgozott kép átadása a **OCR engine Python** objektumnak garantálja, hogy a motor a legmagasabb minőségű adatot kapja, ami közvetlenül a pontosság növekedéséhez vezet.

## 5. lépés: Egyszerű szöveg felismerése (Opcionális, de hasznos)

Néha csak a nyers szövegre van szükség. Ez a lépés opcionális, mivel a tutorial fő célja a strukturált kimenet, de gyors ellenőrzéshez hasznos.

```python
# Get plain text (useful for debugging)
plain_text = engine.recognize()
print("Plain‑text output:\n", plain_text[:200])   # Print first 200 chars
```

Egy olyan karakterláncot fogsz látni, amely hasonlít az eredeti dokumentumra, bár layout információ nélkül. Ha a szöveg összezavarodott, menj vissza, és finomítsd a előfeldolgozási paramétereket.

## 6. lépés: Strukturált adatok kinyerése és mentése JSON‑ként (OCR structured JSON output)

A modern OCR motorok igazi ereje a layout információ visszaadása — táblázatok, oszlopok, sőt űrlapmezők. Az `engine.recognize_structured()` pontosan ezt teszi, és az eredményt egy rendezett JSON fájlba dump-oljuk.

```python
# Recognize structured data (tables, layout) and export to JSON
structured_result = engine.recognize_structured()
output_path = "YOUR_DIRECTORY/out.json"
ocrutil.save_result(structured_result, output_path)
print(f"Structured OCR result saved to {output_path}")
```

Egy JSON‑részlet így nézhet ki:

```json
{
  "pages": [
    {
      "blocks": [
        {
          "type": "text",
          "bbox": [12, 34, 560, 120],
          "text": "Invoice #12345"
        },
        {
          "type": "table",
          "bbox": [15, 130, 580, 400],
          "rows": [
            ["Item", "Qty", "Price"],
            ["Widget A", "2", "$19.99"]
          ]
        }
      ]
    }
  ]
}
```

*Mit jelent ez számodra:* Egy gép‑olvasható reprezentáció, amelyet közvetlenül betáplálhatsz adatbázisba, API‑ba vagy jelentéskészítő eszközbe — többé már nincs szükség kézi másolás‑beillesztésre.

## Bónusz: Vizuális ellenőrzés (Kép alt szöveggel)

Alább látható egy elő‑ és utólagos pillanatkép a pipeline‑ról. Figyeld meg, hogyan nő a kontraszt, és a zaj eltűnik.

![Kép előfeldolgozása OCR-hez – eredeti vs tisztított](/images/ocr_preprocess_example.png){: .align-center alt="preprocess image for OCR példa"}

*Ha kíváncsi vagy:* Cseréld le az `ocrutil.preprocess`‑t a saját OpenCV rutinodra, és továbbra is a **preprocess image for OCR** filozófiát követed — threshold, filter, majd betáplálás.

## Gyakori buktatók és hogyan kerüld el őket

- **Túlzott binarizáció:** Ha a küszöbértéket túl magasra állítod, elmoshatod a halvány karaktereket. Ha hiányzó betűket látsz, csökkentsd a küszöböt az `ocrutil.preprocess`‑ban.
- **Rossz DPI:** Az OCR motorok körülbelül 300 dpi‑t feltételeznek nyomtatott anyagokhoz. Ha a képed alacsony felbontású, fontold meg a felméretezést az előfeldolgozás előtt.
- **Auto‑rotate kihagyása:** Már egy 5‑fokos dőlésszög is megzavarhatja a sorok detektálását. A „auto rotate image OCR” lépés olcsó, és órákat takarít meg a hibakeresésben.

## A munkafolyamat kiterjesztése

Most, hogy van egy stabil alapod, érdemes lehet:

1. **Nyelvi csomagok hozzáadása** (`engine.set_language('eng+spa')`) többnyelvű dokumentumokhoz.  
2. **Integrálás Pandas‑szal**, hogy a JSON‑táblákat DataFrame‑ekké alakítsd elemzésekhez.  
3. **Kötegelt feldolgozás futtatása** egy mappában lévő képek felett, és az eredményeket egy fő JSON fájlba fűzd.

Mindezek a kiterjesztések továbbra is az alapötletre épülnek: **preprocess image for OCR** mielőtt bármikor meghívnád a motort.

## Következtetés

Most már tudod, hogyan **preprocess image for OCR** Python‑ban — auto‑rotate, binarizálás, denoise, majd a tiszta képet átadni egy **OCR engine Python** példánynak, amely egyszerű szöveget és gazdag **OCR structured JSON output**‑ot is kiad. Ezeknek a lépéseknek a követésével drámaian javíthatod a felismerési arányt, és olyan adatot kapsz, amely készen áll a további feldolgozásra.

Készen állsz a következő szintre? Próbáld ki a beépített `ocrutil.preprocess` helyett egy saját OpenCV pipeline‑t, kísérletezz különböző binarizációs technikákkal, vagy tápláld a JSON‑t egy jelentéskészítő dashboardba. A lehetőségek határtalanok, és az általad most felépített alap megakadályozza, hogy újra ugyanazzal a képminőségi problémával akadj bele.

Boldog kódolást, és legyenek az OCR eredményeid mindig kristálytisztek!

## Mit érdemes még megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljesen működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}