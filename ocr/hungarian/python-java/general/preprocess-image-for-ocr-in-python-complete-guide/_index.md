---
category: general
date: 2026-06-25
description: Kép előfeldolgozása OCR-hez és szöveg felismerése beolvasott dokumentumból
  Python segítségével. Lépésről‑lépésre útmutató teljes kóddal.
draft: false
keywords:
- preprocess image for OCR
- recognize text from scanned document
- Python OCR tutorial
- image deskewing Python
- OCR preprocessing tips
language: hu
og_description: Előfeldolgozza a képet OCR-hez, és Python segítségével felismeri a
  szkennelt dokumentum szövegét. Kövesse ezt a részletes, futtatható útmutatót.
og_title: Kép előfeldolgozása OCR-hez Pythonban – Teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  headline: Preprocess Image for OCR in Python – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  name: Preprocess Image for OCR in Python – Complete Guide
  steps:
  - name: Create an OCR Engine Instance
    text: '```python import ocr # <-- make sure the OCR library is installed'
  - name: Enable Automatic Deskewing and Binarization
    text: '```python # Step 2: Enable automatic deskewing and binarization to improve
      recognition engine.image_preprocessing = ocr.ImagePreProcessingOptions( auto_deskew=True,
      auto_binarize=True ) ```'
  - name: Load the Skewed Image You Want to Process
    text: '```python # Step 3: Load the skewed image you want to process image_path
      = "YOUR_DIRECTORY/skewed_document.jpg" image = ocr.Image.load(image_path) ```'
  - name: Perform OCR on the Pre‑processed Image
    text: '```python # Step 4: Perform OCR on the pre‑processed image result = engine.recognize(image)
      ```'
  - name: Output the Recognized Text
    text: '```python # Step 5: Output the recognized text print("Deskewed & binarized
      text:", result.text) ```'
  - name: 1. Handling Multiple Languages
    text: 'If your document contains both English and French, configure the engine
      before step 1:'
  - name: 2. Fine‑Tuning Binarization Thresholds
    text: 'Automatic binarization works for most cases, but some old photocopies need
      a custom threshold:'
  - name: 3. Extracting Layout Information
    text: 'Sometimes you need more than raw text—you want to know where each paragraph
      lives on the page. Many engines expose a `result.blocks` collection:'
  - name: 4. Processing a Batch of Files
    text: 'If you have a folder full of scanned PDFs converted to JPEGs, wrap the
      whole flow in a loop:'
  - name: 5. Dealing with Low‑Resolution Scans
    text: 'Low‑resolution images (< 150 dpi) often produce fuzzy characters. A quick
      remedy is to upscale using a high‑quality algorithm before feeding the image
      to the OCR engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Kép előfeldolgozása OCR-hez Pythonban – Teljes útmutató
url: /hu/python-java/general/preprocess-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép előfeldolgozása OCR-hez Pythonban – Teljes útmutató

Valaha is elgondolkodtál, hogyan **preprocess image for OCR** úgy, hogy a szöveg tiszta és megbízható legyen? Nem vagy egyedül – a legtöbb fejlesztő ugyanazzal a problémával szembesül, amikor a beolvasott oldal ferde vagy a kontraszt nagyon változó. A jó hír, hogy néhány Python sorral kiegyenesítheted a rendetlenséget, binarizálhatod a képet, és tiszta, kereshető szöveget kapsz.

Ebben az útmutatóban végigvezetünk a pontos lépéseken, hogy **preprocess image for OCR** *és* **recognize text from scanned document** fájlok esetén, egy népszerű OCR könyvtár használatával. A végére egy azonnal futtatható szkriptet kapsz, megérted, miért fontos minden beállítás, és tudni fogod, hogyan finomhangold a nehéz esetekhez.

## Amire szükséged lesz

- Python 3.8 vagy újabb (a kód 3.10+ verzión is működik)
- Egy OCR csomag, amely elérhetővé teszi az `OcrEngine`, `ImagePreProcessingOptions` és `Image` osztályokat (pl. a példában használt fiktív `ocr` modul)
- Egy beolvasott vagy fényképezett dokumentum, amely kissé ferde vagy alacsony kontrasztú
- Kedvenc IDE-d vagy egy egyszerű terminál – nincs szükség nehéz GUI-ra

Ennyi. Nincs extra bináris, nincs Docker akrobátika. Merüljünk bele.

## Kép előfeldolgozása OCR-hez – Lépésről‑lépésre

Az alábbiakban a fő munkafolyamat öt egyértelmű szakaszra van bontva. Minden szakasz tartalmazza, **miért** csináljuk, a pontos **kódot**, és egy rövid **magyarázatot** arról, mi történik a háttérben.

### 1. lépés: OCR motor példány létrehozása

```python
import ocr  # <-- make sure the OCR library is installed

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Miért fontos ez:*  
Az `OcrEngine` objektum a művelet agya. Tartalmazza a konfigurációt, például a nyelvi csomagokat, a megbízhatósági küszöböket, és – számunkra a legfontosabb – a kép‑előfeldolgozási jelzőket. Az első példányosítás tiszta alapot ad a további trükkök engedélyezéséhez.

### 2. lépés: Automatikus kiegyenesítés és binarizálás engedélyezése

```python
# Step 2: Enable automatic deskewing and binarization to improve recognition
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
```

*Miért fontos ez:*  
- **Deskewing** (kiegyenesítés) elforgatja a képet, hogy a szövegsorok vízszintessé váljanak. Az OCR motorok nehezen birkóznak meg, ha az alapvonal néhány foknál jobban dől.  
- **Binarization** (binarizálás) a képet tisztán fekete‑fehérre konvertálja, eltávolítva a háttérzajt, amely összezavarhatja a karakter osztályozókat.  
Mindkét opció *automatikus* sok modern könyvtárban, de mégis be kell kapcsolni őket – ezért van a kifejezett hozzárendelés.

> **Pro tipp:** Ha a forrásképek már tökéletesen igazítottak, beállíthatod `auto_deskew=False`-t, hogy egy milliszekundumot spórolj a feldolgozási időből.

### 3. lépés: Töltsd be a feldolgozni kívánt ferde képet

```python
# Step 3: Load the skewed image you want to process
image_path = "YOUR_DIRECTORY/skewed_document.jpg"
image = ocr.Image.load(image_path)
```

*Miért fontos ez:*  
Az `Image.load` metódus beolvassa a fájlt a memóriába, és egy olyan objektumba csomagolja, amelyet az OCR motor ért. Emellett kinyeri a metaadatokat, például a DPI-t, ami befolyásolhatja a kiegyenesítés alapértelmezett skálázási tényezőjét.

> **Szélsőséges eset:** Ha a kép egy többoldalas TIFF, akkor iterálnod kell minden oldalon, vagy használhatsz egy segédeszközt, például `ocr.MultiPageImage.load`-ot. Ugyanazok az előfeldolgozási beállítások minden oldalra érvényesek.

### 4. lépés: OCR végrehajtása az előfeldolgozott képen

```python
# Step 4: Perform OCR on the pre‑processed image
result = engine.recognize(image)
```

*Miért fontos ez:*  
Ezen a ponton a motor alkalmazza a korábban engedélyezett kiegyenesítési és binarizálási lépéseket, majd lefuttatja a neurális hálózatát (vagy a klasszikus Tesseract‑stílusú folyamatot) a tisztított bitmapen. A visszakapott `result` objektum általában tartalmazza a sima szöveget, a megbízhatósági pontszámokat, és néha a pozíciós adatokat minden egyes szóhoz.

> **Mi van, ha a szöveg még mindig torz?**  
Ellenőrizd a kép felbontását: az OCR a legjobban 300 dpi vagy annál magasabb felbontásnál működik. Ha a forrás alacsonyabb, fontold meg a felméretezést a betöltés előtt, vagy kérd az eredeti beolvasást a dokumentum forrásától.

### 5. lépés: A felismert szöveg kiírása

```python
# Step 5: Output the recognized text
print("Deskewed & binarized text:", result.text)
```

*Miért fontos ez:*  
A `result.text` egy egyszerű karakterlánc, amely mindent tartalmaz, amit a motor ki tudott olvasni. Kiíratása gyors hibakereséshez hasznos; egy valódi alkalmazásban valószínűleg egy `.txt` fájlba, adatbázisba írnád, vagy egy downstream NLP csővezetékbe továbbítanád.

---

## Szöveg felismerése beolvasott dokumentumból – Alapokon túl

Miután az alapvető csővezeték működik, nézzünk meg néhány gyakori változatot, amelyekkel találkozhatsz, amikor **recognize text from scanned document** képeket próbálsz feldolgozni a valóságban.

### 1. Több nyelv kezelése

Ha a dokumentumod tartalmazza az angolt és a franciát is, állítsd be a motort az 1. lépés előtt:

```python
engine = ocr.OcrEngine(languages=["eng", "fra"])
```

A legtöbb OCR motor elfogadja az ISO‑639‑2 kódokat; további nyelvi csomagok betöltése kis extra terhet jelent, de drámaian javítja a pontosságot a többnyelvű oldalakon.

### 2. Binarizálási küszöb finomhangolása

Az automatikus binarizálás a legtöbb esetben működik, de néhány régi fotómásolat egyedi küszöböt igényel:

```python
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=False,          # turn off auto
    binarization_threshold=180   # manual threshold (0‑255)
)
```

Kísérletezz 120 és 220 közötti értékekkel, amíg a háttér eltűnik anélkül, hogy a halvány karakterek elvésznének.

### 3. Elrendezési információk kinyerése

Néha többre van szükség, mint a nyers szöveg – tudni akarod, hol helyezkedik el az egyes bekezdés az oldalon. Sok motor egy `result.blocks` gyűjteményt biztosít:

```python
for block in result.blocks:
    print(f"Block at ({block.x}, {block.y}) size {block.width}x{block.height}")
    print(block.text)
```

Ez felbecsülhetetlen a táblázatok újraépítéséhez vagy az oszlopsorrend megőrzéséhez.

### 4. Fájlok kötegének feldolgozása

Ha van egy mappa, tele beolvasott PDF-ekkel, amelyek JPEG-re konvertáltak, csomagold az egész folyamatot egy ciklusba:

```python
import pathlib

folder = pathlib.Path("YOUR_DIRECTORY")
for img_file in folder.glob("*.jpg"):
    img = ocr.Image.load(str(img_file))
    txt = engine.recognize(img).text
    (folder / f"{img_file.stem}.txt").write_text(txt, encoding="utf-8")
    print(f"Processed {img_file.name}")
```

A ciklus ugyanazt az `engine` példányt használja újra, ami hatékonyabb, mint minden fájlhoz újra létrehozni.

### 5. Alacsony felbontású beolvasások kezelése

Az alacsony felbontású képek (< 150 dpi) gyakran homályos karaktereket eredményeznek. Egy gyors megoldás a felméretezés egy magas minőségű algoritmussal, mielőtt a képet az OCR motorba adod:

```python
from PIL import Image as PilImage

pil_img = PilImage.open("low_res.jpg")
upscaled = pil_img.resize((pil_img.width * 2, pil_img.height * 2), PilImage.LANCZOS)
upscaled.save("upscaled.jpg")
image = ocr.Image.load("upscaled.jpg")
```

A felméretezés nem varázslatosan hoz létre részleteket, de a binarizálási lépés élesebb élekkel dolgozhat, ami mérsékelt javulást eredményez.

---

## Várható kimenet

A kiinduló öt lépéses szkript futtatása egy közepesen ferde, 300 dpi-s beolvasáson valami ilyesmit kell, hogy kiírjon:

```
Deskewed & binarized text: 
Dear Customer,

Thank you for your recent purchase. Please find your receipt attached.

Best regards,
Acme Corp.
```

Ha torz karaktereket látsz, ellenőrizd újra az előfeldolgozási jelzőket, a kép felbontását és a nyelvi beállításokat.

---

## Következtetés

Minden szükségeset áttekintettük a **preprocess image for OCR** és **recognize text from scanned document** fájlok Python használatával. Egy friss motor példánytól kezdve engedélyeztük az automatikus kiegyenesítést és binarizálást, betöltöttük a ferde képet, futtattuk a felismerést, és kiírtuk a tiszta szöveget. Útközben megvizsgáltuk a többnyelvű támogatást, a manuális küszöb finomhangolást, az elrendezés kinyerését, a kötegelt feldolgozást és az alacsony felbontású megoldásokat.

Próbáld ki a szkriptet a saját beolvasásaidon – lehet ez egy csomó nyugta, egy kézzel írt űrlap vagy egy régi újságkivágás. Miután magabiztos vagy, próbáld meg PDF generálással vagy a kimenet keresőindexbe való betáplálásával bővíteni. A lehetőségek határtalanok.

**Készen állsz a következő kihívásra?** Nézd meg a *„Táblázatok kinyerése beolvasott PDF-ekből Pythonnal”* és a *„Egyedi OCR modellek tanítása TensorFlow‑val”* című útmutatóinkat, hogy tovább bővítsd a dokumentum‑automatizálási eszköztárad.

Kellemes kódolást, és legyen az OCR mindig éles!

## Mit érdemes legközelebb megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}