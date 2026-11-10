---
category: general
date: 2026-06-06
description: Hogyan előfeldolgozzuk a képeket OCR-hez Python használatával. Tanulja
  meg, hogyan binarizálja a képet Otsu módszerrel, hogyan korrigálja a beolvasott
  dokumentumok dőlését, és hogyan javítsa az OCR pontosságát német szövegek esetén.
draft: false
keywords:
- how to preprocess images for OCR
- binarize image using otsu
- how to deskew scanned documents
- how to improve OCR accuracy
- extract text from german image
language: hu
og_description: Hogyan előfeldolgozzuk a képeket OCR-hez Pythonban. Ez az útmutató
  bemutatja, hogyan binarizáljuk a képet Otsu módszerrel, hogyan korrigáljuk a beolvasott
  dokumentumok dőlését, és hogyan javítható az OCR pontossága német nyelvű képeken.
og_title: Hogyan előfeldolgozzuk a képeket OCR-hez – Teljes Python útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  headline: How to Preprocess Images for OCR – Complete Python Guide
  type: TechArticle
- description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  name: How to Preprocess Images for OCR – Complete Python Guide
  steps:
  - name: How to Deskew Scanned Documents
    text: The `deskew` call above is the concrete answer to **how to deskew scanned
      documents**. Internally it estimates the dominant text line angle via Hough
      transform and rotates the image back. If your documents are rotated more than
      5°, bump `max_angle` up, but beware of over‑rotation artifacts.
  - name: Binarize Image Using Otsu
    text: The `binarize(method="otsu")` line directly answers the query **binarize
      image using otsu**. Otsu’s algorithm computes a threshold that minimizes intra‑class
      variance, which is perfect for documents with bimodal histograms (dark text
      vs. light background).
  - name: Expected Output
    text: 'Assuming the sample scan contains the sentence “Die schnelle braune Füchsin
      springt über den faulen Hund.” you should see something like:'
  type: HowTo
tags:
- OCR
- image preprocessing
- Python
- German language
title: Hogyan előfeldolgozzuk a képeket OCR-hez – Teljes Python útmutató
url: /hu/python-java/general/how-to-preprocess-images-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan előfeldolgozzuk a képeket OCR-hez – Teljes Python útmutató

Valaha is elgondolkodtál **hogyan előfeldolgozzuk a képeket OCR-hez**, hogy a szöveg kristálytiszta legyen? Nem vagy egyedül. A beolvasott dokumentumok – különösen a zajos német oldalak – rémálom lehet bármely OCR motor számára. A jó hír? Néhány okos előfeldolgozási lépés egy homályos, pöttyös szkennelt oldalt tiszta, gép‑olvasható képpé változtathat.

Ebben a tutorialban egy gyakorlati példán keresztül mutatjuk be, **hogyan előfeldolgozzuk a képeket OCR-hez** Python használatával. Megtanulod, hogyan **binarizáld a képet Otsu‑val**, **hogyan korrigáld a ferde beolvasott dokumentumokat**, és általánosságban **hogyan javítható az OCR pontossága**, amikor **német képfájlokból kell szöveget kinyerni**. Felesleges szócséplés nélkül, csak egy működő szkript, amit ma is másolhatsz‑beilleszthetsz.

## Amire szükséged lesz

- **Python 3.9+** (bármely friss verzió megfelelő)
- Egy OCR könyvtár, amely egy `OcrEngine` osztályt biztosít – a bemutatóhoz egy általános `ocr` csomagot feltételezünk. Telepítsd a `pip install ocr-lib` paranccsal.
- Egy zajos német szken (`noisy_german_scan.tif`), amivel tesztelni szeretnél.
- Alapvető Python‑függvényismeret (ha már írtál `def`‑et, akkor jó vagy).

> **Pro tipp:** Ha másik OCR SDK‑t használsz (pl. Tesseract a `pytesseract`‑on keresztül), a koncepciók ugyanazok – csak a metódusneveket igazítsd a saját könyvtáradhoz.

## A megoldás áttekintése

1. **Hozz létre egy OCR motor példányt.**  
2. **Állítsd be a felismert nyelvet németre.**  
3. **Építs egy egyedi előfeldolgozó pipeline‑t**, amely tartalmazza a ferdekorrekciót, zajszűrést, binarizálást (Otsu) és kontrasztnyújtást.  
4. **Csatold a pipeline‑t a motorhoz**, hogy minden kép automatikusan átmenjen rajta.  
5. **Futtasd az OCR‑t** egy zajos német szkennelt képen.  
6. **Írd ki a kinyert szöveget**, hogy ellenőrizd az eredményt.

Alább minden lépést részletezünk, elmagyarázzuk, **miért** fontos, és megmutatjuk a pontos kódot, amire szükséged lesz.

![hogyan előfeldolgozzuk a képeket OCR-hez példa](image.png "hogyan előfeldolgozzuk a képeket OCR-hez példa")

## 1. lépés: OCR motor példány létrehozása

Először is – motor nélkül semmi sem történik. Az `OcrEngine` objektum a belépési pont, amely koordinálja a későbbi feldolgozást.

```python
# Step 1: Initialize the OCR engine
from ocr import OcrEngine, Language

ocr_engine = OcrEngine()
```

*Miért fontos:* A motor inicializálása beállítja a belső erőforrásokat (például nyelvi modelleket), és tiszta alapot ad a későbbi egyedi pipeline csatolásához.

## 2. lépés: A felismert nyelv beállítása németre

Az OCR pontossága erősen nyelvtől függ. Ha a motor tudja, hogy német szöveget vár, aktiválja a megfelelő karakterkészletet és nyelvi modellt.

```python
# Step 2: Tell the engine we’re working with German text
ocr_engine.set_recognition_language(Language.GERMAN)
```

Ha ezt kihagyod, a motor alapértelmezés szerint angolt használhat, és hibásan ismeri fel az umlautokat (ä, ö, ü) valamint a ß karaktert – gyakori buktatók német szkennelt anyagoknál.

## 3. lépés: Egyedi előfeldolgozó pipeline felépítése

Ez a **hogyan előfeldolgozzuk a képeket OCR-hez** központi része. Négy átalakítást láncolunk össze:

| Átalakítás | Mit csinál | Miért segít |
|------------|------------|-------------|
| **Deskew** | Visszaforgatja a képet vízszintesre (max 5°) | A szkenek ritkán tökéletesen igazodnak; a ferdekorrekció eltávolítja a dőlést, ami megzavarja a karakterszegmentálást. |
| **Denoise** | Csökkenti a véletlenszerű pöttyöket (erősség 0.7) | A zaj hamis éleket hoz létre, amelyeket az OCR motor karakterként értelmezhet. |
| **Binarize (Otsu)** | Fekete‑fehérre konvertálja Otsu módszerével | Egy tiszta bináris kép éles kontrasztot biztosít az előtér (szöveg) és a háttér között. |
| **Contrast Stretch** | Kiterjeszti a dinamikus tartományt | Javítja a gyenge vonalak olvashatóságát, különösen régi dokumentumoknál. |

```python
# Step 3: Assemble the preprocessing pipeline
preprocessing_pipeline = (
    ocr_engine.preprocessing()
               .deskew(max_angle=5)          # auto‑deskew up to 5°
               .denoise(strength=0.7)       # medium denoise
               .binarize(method="otsu")      # **binarize image using Otsu**
               .contrast(stretch=True)      # auto contrast stretch
)

# Explanation:
# - `deskew` corrects rotation; 5° is a safe ceiling for most scans.
# - `denoise` with 0.7 balances smoothing without erasing thin characters.
# - `binarize` with method "otsu" automatically selects the optimal threshold.
# - `contrast` stretch brightens faint ink while keeping dark ink dark.
```

### Hogyan korrigáljuk a ferde beolvasott dokumentumokat

A fenti `deskew` hívás a konkrét válasz a **hogyan korrigáljuk a ferde beolvasott dokumentumokat** kérdésre. Belsőleg a domináns szövegsor‑szöget Hough‑transzformációval becsüli, majd elforgatja a képet. Ha a dokumentumaid több mint 5°‑kal vannak elforgatva, növeld a `max_angle` értékét, de vigyázz a túlzott forgatás miatti artefaktusokra.

### Képbinarizálás Otsu‑val

A `binarize(method="otsu")` sor közvetlenül válasz a **binarize image using otsu** kérdésre. Az Otsu‑algoritmus egy olyan küszöböt számol ki, amely minimalizálja az osztályon belüli varianciát, ami tökéletes a kétcsúcsú hisztogramú dokumentumokhoz (sötét szöveg vs. világos háttér).

## 4. lépés: Pipeline csatolása a motorhoz

Most megmondjuk az OCR motornak, hogy minden bejövő képet futtasson le a most épített pipeline‑on.

```python
# Step 4: Register the custom pipeline
ocr_engine.set_preprocessing(preprocessing_pipeline)
```

*Miért fontos:* Regisztráció nélkül a motor a nyers szkennel dolgozna, figyelmen kívül hagyva az általunk beállított tisztítást. Ez a lépés biztosítja, hogy **hogyan javítható az OCR pontossága** a konzisztens előfeldolgozással.

## 5. lépés: Szövegfelismerés egy zajos német szkennelt képen

Most rakjuk össze a teljes folyamatot. Betápláljuk a motorba a zajos német képet, és hagyjuk, hogy elvégezze a nehéz munkát.

```python
# Step 5: Run OCR on the target file
image_path = "YOUR_DIRECTORY/noisy_german_scan.tif"
recognition_result = ocr_engine.recognize_image(image_path)
```

Ha érdekel a teljesítmény, időzítsd a hívást:

```python
import time
start = time.time()
result = ocr_engine.recognize_image(image_path)
print(f"OCR took {time.time() - start:.2f}s")
```

## 6. lépés: A felismert szöveg kiírása

Végül kiírjuk a kinyert karakterláncot. Ez a közvetlen válasz a **extract text from german image** kérdésre.

```python
# Step 6: Display the OCR output
print("=== Recognized German Text ===")
print(recognition_result.text)
```

### Várt kimenet

Tegyük fel, hogy a minta szken a következő mondatot tartalmazza: „Die schnelle braune Füchsin springt über den faulen Hund.” A kimenet valahogy így nézhet ki:

```
=== Recognized German Text ===
Die schnelle braune Füchsin springt über den faulen Hund.
```

Ha a kimenet még mindig torz karaktereket tartalmaz, próbáld finomhangolni a `denoise` erősségét vagy növeld a `max_angle` értékét a ferdekorrekcióhoz.

## Gyakori hibák és megoldások

- **Hiányzó nyelvi modell:** A `set_recognition_language(Language.GERMAN)` elhagyása gyakran eredményez hiányzó umlautokat. Ellenőrizd a hívást.
- **Túlzott zajszűrés:** 0.9‑nél nagyobb erősség törölheti a vékony vonalakat, különösen a régi betűtípusoknál. 0.5‑0.7 közötti érték a legtöbb esetben megfelelő.
- **Nem megfelelő fájlformátum:** Egyes OCR motorok nem bírnak meg többoldalas TIFF‑ekkel. Ha többoldalas dokumentumod van, bontsd szét egyoldalas fájlokra először.
- **Pipeline sorrend:** A bemutatott sorrend (deskew → denoise → binarize → contrast) szándékos. A binarizálás zajszűrés előtt rögzítheti a zajt; mindig előbb zajszűrj.

## A pipeline bővítése (Mi következik?)

Miután van egy stabil alapod, érdemes lehet:

- **Morfológiai nyitást** hozzáadni a kis foltok tisztításához (`.morph_open(kernel=3)`).
- **Nyelvi modellt** integrálni a poszt‑feldolgozási korrekcióhoz (`ocr_engine.apply_spellcheck()`).
- **Kötegelt feldolgozást párhuzamosítani** nagy adathalmazok esetén a `concurrent.futures` használatával.

Ezek mind természetes kiterjesztései a **hogyan előfeldolgozzuk a képeket OCR-hez** koncepciónak, miközben tovább növelik a **hogyan javítható az OCR pontossága**.

## Összegzés

Most már ismered a **hogyan előfeldolgozzuk a képeket OCR-hez** teljes folyamatát: motor létrehozása, német nyelv beállítása, olyan pipeline építése, amely **binarize image using Otsu**, **how to deskew scanned documents**, és végül **extract text from german image** magasabb megbízhatósággal. A hat lépés követésével jelentős javulást fogsz látni a felismert szöveg minőségében – többé már nincs végtelen kézi javítás.

Próbáld ki a szkriptet a saját szkenneiddel, kísérletezz a paraméterekkel, és hagyd, hogy az eredmények beszéljenek. Van kérdésed egy konkrét előfeldolgozási trükkel kapcsolatban? Írj kommentet, és mélyebben is belemerülünk.

Boldog kódolást, és legyen az OCR‑ed mindig pontos!

## Mit érdemes még megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy további API‑funkciókat saját projektjeidben is könnyedén alkalmazhasd.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}