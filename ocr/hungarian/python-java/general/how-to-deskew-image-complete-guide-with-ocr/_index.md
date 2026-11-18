---
category: general
date: 2026-03-26
description: Tanulja meg, hogyan korrigálja a kép dőlését, hogyan ismerje fel a szöveget
  a képről, és hogyan építsen fel egy képelőfeldolgozó csővezetéket a szkennelés zajának
  eltávolítására, valamint a szkennelt kép szöveggé alakítására.
draft: false
keywords:
- how to deskew image
- recognize text from image
- image preprocessing pipeline
- remove noise from scan
- convert scanned image to text
language: hu
og_description: Hogyan korrigáljuk a kép dőlését, és egy ferde beolvasást kereshető
  szöveggé alakítsunk. Kövesse ezt az útmutatót a kép szövegének felismeréséhez, a
  beolvasás zajának eltávolításához, és a beolvasott kép szöveggé konvertálásához.
og_title: Hogyan kiegyenesítsünk képet – Lépésről lépésre OCR útmutató
tags:
- OCR
- image-processing
- Python
title: Hogyan korrigáljuk a kép ferdeségét – Teljes útmutató OCR-rel
url: /hu/python-java/general/how-to-deskew-image-complete-guide-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan korrigáljuk a kép dőlését – Teljes útmutató OCR-rel

Gondoltad már, **hogyan korrigáljuk a kép dőlését**, ami egy olcsó szkennerből származik? Nem vagy egyedül. Egy ferde oldal amatőrnek tűnik, és ami még fontosabb, a dőlés megzavarhat bármely OCR motor működését, amikor **szöveget próbál felismerni a képről**.  

Ebben a tutorialban végigvezetünk egy teljes **kép előfeldolgozási pipeline‑on**, amely korrigálja a dőlést, binarizálja és zajtalanítja a szkennelt képet, majd átadja egy OCR motor számára, hogy **a beolvasott képet szöveggé alakítsa** minimális fáradsággal. Nincs varázslat, csak tiszta Python és egy kis könyvtár, ami a nehéz munkát elvégzi.

## Amire szükséged lesz

- Python 3.9+ (a kód 3.10‑n és újabb verziókon is működik)
- Az `ocr` csomag (telepítés: `pip install ocr‑toolkit` – cseréld le a saját könyvtárad nevére)
- Egy beolvasott JPEG vagy PNG, amely nyilvánvalóan ferde (pl. `skewed_scan.jpg`)
- Egy kis kíváncsiság arról, hogy miért fontos minden előfeldolgozási lépés

Ennyi. Nincsenek nehéz függőségek, mint az OpenCV, hacsak később nem akarsz mélyebbre merülni.

## 1. lépés: A beolvasott kép betöltése

Az első dolog, hogy a fájlt memóriába olvassuk. Ez a lépés egyszerű, de kulcsfontosságú – ha az útvonal hibás, minden más összeomlik.

```python
# Step 1: Load the scanned image
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)
```

> **Miért?**  
> A kép betöltése egy manipulálható objektumot ad, amellyel az `ocr.ImagePreprocessor` dolgozhat. Ennek kihagyása azt jelentené, hogy a pipeline nem fér hozzá a tényleges pixeladatokhoz.

## Hogyan korrigáljuk a kép dőlését és készítsük elő OCR-hez

Most, hogy megvan a kép, egyenesítsük ki. A `deskew()` metódus becsli a dőlés szögét, és visszaforgatja a képet vízszintes állapotba.

```python
# Step 2: Create an image preprocessor and correct the orientation
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()
```

> **Pro tipp:** Ha a szkennelt képek csak enyhén eltérnek (≤ 3°), az alapértelmezett algoritmus általában tökéletes. Extrém szögek esetén előfordulhat, hogy a belső paramétereket finomhangolni kell – nézd meg a könyvtár dokumentációját a `max_angle` beállításhoz.

## A kép binarizálása – fekete‑fehérre alakítás

Az OCR motorok a nagy kontrasztú bemenetet kedvelik. A kép bináris (fekete‑fehér) ábrázolásra konvertálása eltávolítja azokat a finom árnyalatokat, amelyek összezavarhatják a karakterfelismerést.

```python
# Step 3: Convert the image to a binary (black‑and‑white) representation
preprocessor.binarize(threshold=128)
```

> **Mi történik?**  
> A 128-nál világosabb pixelek fehérek lesznek; minden más fekete. Állítsd a küszöböt, ha a szkenned szokatlanul sötét vagy világos.

## Zaj eltávolítása a szkennelés előtt OCR előtt

Még egy tökéletesen korrigált kép is tartalmazhat foltokat, port vagy tömörítési hibákat. Ezek a kis foltok minden OCR motor átokja.

```python
# Step 4: Reduce noise to improve OCR accuracy
preprocessor.denoise(radius=1)
```

> **Miért távolítsuk el a zajt?**  
> A zaj hamis éleket hoz létre, amelyeket az OCR motor karakterként értelmezhet. Egy kis sugár a legtöbb szkenneléshez megfelelő; növeld, ha a dokumentum erősen szemcsés.

## Az előfeldolgozási pipeline alkalmazása

Minden beállítás készen áll – most futtassuk a pipeline‑t az eredeti képen.

```python
# Step 5: Apply the preprocessing pipeline to the loaded image
processed_image = preprocessor.apply(original_image)
```

> **Eredmény:** `processed_image` egy megtisztított, egyenes, nagy kontrasztú bitmap, amely készen áll a szövegkinyerésre.

## Szöveg felismerése a képről OCR motorral

Itt az ideje, hogy ténylegesen elolvassuk a szöveget. Inicializáljuk az OCR motort, betápláljuk a polírozott képet, és kérjük a nyers karakterláncot.

```python
# Step 6: Initialise the OCR engine and provide the processed image
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# Step 7: Recognise text and output the result
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Várható kimenet** (példa):

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Ha értelmetlen karaktereket látsz, ellenőrizd a dőléskorrekciós lépést, vagy kísérletezz egy másik `threshold` értékkel.

## Kép előfeldolgozási pipeline felépítése – Teljes szkript

Mindent összegezve, itt egy önálló, futtatható szkript, amelyet `.py` fájlba másolhatsz és végrehajthatsz:

```python
import ocr  # Replace with the actual import path of your OCR library

# -------------------------------------------------
# 1️⃣ Load the scanned image
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)

# -------------------------------------------------
# 2️⃣ Deskew – how to deskew image
# -------------------------------------------------
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()

# -------------------------------------------------
# 3️⃣ Binarize – convert to black‑and‑white
# -------------------------------------------------
preprocessor.binarize(threshold=128)

# -------------------------------------------------
# 4️⃣ Denoise – remove noise from scan
# -------------------------------------------------
preprocessor.denoise(radius=1)

# -------------------------------------------------
# 5️⃣ Apply the pipeline
# -------------------------------------------------
processed_image = preprocessor.apply(original_image)

# -------------------------------------------------
# 6️⃣ OCR – recognize text from image
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# -------------------------------------------------
# 7️⃣ Output – convert scanned image to text
# -------------------------------------------------
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Tipp:** Csomagold be az egészet egy függvénybe (`def ocr_from_file(path): …`), ha sok fájlt szeretnél kötegelt módon feldolgozni.

## Gyakori kérdések és szélhelyzetek

- **Mi van, ha a kép már egyenes?**  
  A `deskew()` metódus szinte nulla szöget észlel, és érintetlenül hagyja a képet, így biztonságosan futtatható minden fájlon.

- **A szkennem színes – tartsam meg?**  
  A szín a legtöbb OCR feladathoz nem ad hozzá értéket. A binarizálás eltávolítja, gyorsítja a feldolgozást és csökkenti a memóriahasználatot.

- **Láncolhatok több előfeldolgozási lépést?**  
  Természetesen. Az `ImagePreprocessor` osztály pipeline‑okra van tervezve; hozzáadhatsz `sharpen()`, `contrast_enhance()` vagy egyedi szűrőket, mielőtt meghívod az `apply()`‑t.

- **Az OCR kimenetben felesleges sortörések vannak – hogyan javítsam?**  
  Utófeldolgozd a karakterláncot a `text.replace("\n", " ").strip()`‑vel, vagy használj fejlettebb elrendezés‑elemző könyvtárat, például a Tesseract `--psm` módjait.

## Következő lépések

Most, hogy tudod, **hogyan korrigáljuk a kép dőlését**, és van egy stabil **kép előfeldolgozási pipeline**, érdemes lehet:

- **Szöveg felismerése a képről** integrálása egy Flask API‑ba, hogy valós időben lehessen dokumentumokat feltölteni.
- A pipeline használata **zaj eltávolítása a szkennelésből** történő történelmi dokumentumok esetén, ahol a megőrzés kulcsfontosságú.
- Tömeges feldolgozás skálázása több ezer oldalra, és kereshető PDF előállítása a `pdfminer` vagy `PyMuPDF` segítségével.

Nyugodtan kísérletezz különböző küszöbökkel, zajszűrési sugarakkal, vagy akár cseréld le az OCR backendet Tesseract‑ra, ha többnyelvű támogatásra van szükséged. Az alapelvek változatlanok: egyenesíts, tisztíts, majd olvasd.

---

*Boldog kódolást! Ha problémába ütközöl, hagyj egy megjegyzést alább – szívesen segítek finomhangolni a pipeline‑t.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}