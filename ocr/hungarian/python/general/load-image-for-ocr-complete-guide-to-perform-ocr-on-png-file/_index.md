---
category: general
date: 2026-06-25
description: Tölts be képet OCR-hez, és végezz OCR-t PNG-n egy lépésről‑lépésre Python
  oktatóval az aocr használatával. Tanulj hibakeresést, naplózást és a legjobb gyakorlatokat.
draft: false
keywords:
- load image for OCR
- perform OCR on PNG
- aocr logging setup
- OCR debugging Python
- image preprocessing OCR
language: hu
og_description: Töltsön be képet OCR-hez, és végezzen OCR-t PNG-n az aocr használatával.
  Ez az útmutató végigvezet a naplózáson, a kép betöltésén és a felismerésen a teljes
  kóddal.
og_title: Kép betöltése OCR-hez – Lépésről lépésre Python útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Load image for OCR and perform OCR on PNG with a step‑by‑step Python
    tutorial using aocr. Learn debugging, logging, and best practices.
  headline: Load Image for OCR – Complete Guide to Perform OCR on PNG Files
  type: TechArticle
- questions:
  - answer: Usually not. `aocr` handles PNG natively, but if the image is huge (>10
      MP) you might want to downscale first to speed up processing.
    question: Do I need to convert the PNG to another format?
  - answer: Rotate the log after each run or limit the level to `INFO` once you’re
      confident the pipeline works.
    question: What if the logger file grows too large?
  - answer: Absolutely. Just call `ocr_png` for each file; the function creates a
      fresh logger each time, keeping logs isolated.
    question: Can I process multiple images in a loop?
  - answer: Yes – `engine.result` also contains `boxes` and `confidences`. Explore
      the `aocr` docs for `result.boxes` if you need layout information.
    question: Is there a way to get bounding boxes instead of plain text?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: Kép betöltése OCR-hez – Teljes útmutató a PNG fájlok OCR-hez
url: /hu/python/general/load-image-for-ocr-complete-guide-to-perform-ocr-on-png-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép betöltése OCR-hez – Teljes útmutató PNG fájlok OCR végrehajtásához

Volt már szükséged **load image for OCR**-ra, de nem tudtad, hogyan állíts be megfelelő hibakeresést? Nem vagy egyedül. Sok projektben az első akadály az, hogy a PNG-t bejuttassuk a motorba, miközben még mindig látható, mi zajlik a háttérben.  

Ebben a bemutatóban végigvezetünk mindenen, amire szükséged van a **perform OCR on PNG** fájlokhoz a `aocr` könyvtár használatával – a részletes kimenethez szükséges naplózó beállításától a tényleges szövegfelismerésig. A végére egy újrahasználható szkriptet kapsz, amelyet bármely Python projektbe beilleszthetsz, és megérted, miért fontos minden lépés.

## Mit fogsz megtanulni

- Hogyan inicializáld a `aocr` naplózót, hogy minden lépést nyomon követhess.
- A pontos kód a **load image for OCR**-hoz a `aocr.OcrEngine` használatával.
- Hogyan állítsd be a naplózási szintet a részletes hibakereséshez.
- A motor futtatása a **perform OCR on PNG** érdekében és az eredmények lekérése.
- Tippek a gyakori buktatók kezeléséhez, mint a hiányzó fájlok vagy nem támogatott formátumok.

Nem szükséges előzetes tapasztalat a `aocr`-ral; csak egy működő Python 3 telepítés és egy kép, amit be szeretnél olvasni. Kezdjünk is bele.

![load image for OCR example](assets/load-image-ocr.png "Kép betöltése OCR-hez Pythonban")

## Előfeltételek

| Követelmény | Miért fontos |
|-------------|--------------|
| Python 3.8+ | A `aocr` modern interpretereket céloz, és típusjelzéseket használ. |
| `aocr` library installed (`pip install aocr`) | A csomag nélkül a használt osztályok nem léteznek. |
| A PNG image you want to read | A bemutató a **perform OCR on PNG**-ra fókuszál, ezért PNG elengedhetetlen. |
| Write permission to a log directory | A naplózó létrehozza az `ocr_debug.log` fájlt. |

Ha valamelyik hiányzik, telepítsd most – csak egy percet vesz igénybe.

```bash
pip install aocr
```

## 1. lépés: Kép betöltése OCR-hez – Naplózás inicializálása

Mielőtt még a képet megérintenéd, állíts be egy naplózót. Az OCR hibakeresése rémálom lehet, ha nem látod, mit csinál a motor. A `aocr.Logging` osztály mindent egy fájlba ír, és a szint `DEBUG`-ra állításával minden belső hívást láthatsz.

```python
import aocr

# Create a logger instance
ocr_logger = aocr.Logging()
# Choose where the log file will live – adjust the path to suit your project
ocr_logger.set_output_file("logs/ocr_debug.log")

# DEBUG gives you the most detail; you can switch to INFO for less noise
ocr_logger.set_level(aocr.LoggingLevel.DEBUG)
```

**Miért fontos ez:**  
Ha az OCR motor nem találja a fájlt vagy a képformátum nem támogatott, a naplózó rögzíti a kivétel stack trace‑ét. Ez megment a végtelen találgatástól később.

## 2. lépés: OCR végrehajtása PNG-n – Motor konfigurálása

Most, hogy a naplózó készen áll, csatold a OCR motorhoz. Ez a lépés köti össze a kettőt, így minden motor művelet rögzítésre kerül.

```python
# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
# Plug the logger into the engine
ocr_engine.logging = ocr_logger
```

**Pro tipp:**  
Ugyanazt az `ocr_engine` példányt több képnél is újra felhasználhatod. Csak ne felejtsd el törölni az előző állapotot, ha kötegelt feldolgozást végzel.

## 3. lépés: Kép betöltése OCR-hez – PNG fájl betáplálása

Itt jön a bemutató lényege: ténylegesen **load image for OCR**. A `load_image` metódus egy fájlútvonalat vár; belül dekódolja a PNG-t egy bitmapre, amit a motor megért.

```python
# Path to the PNG you want to read
image_path = "samples/invoice.png"

# Load the image – this is where we “load image for OCR”
ocr_engine.load_image(image_path)
```

### Különleges esetek, amire figyelni kell

1. **File Not Found** – Ha az útvonal hibás, a `aocr` `FileNotFoundError`‑t dob. A naplózó feljegyzi, de te is elkaphatod:

   ```python
   try:
       ocr_engine.load_image(image_path)
   except FileNotFoundError as e:
       print(f"❌ Could not locate {image_path}: {e}")
       raise
   ```

2. **Unsupported Format** – Bár a PNG széles körben támogatott, egy sérült fájl `UnsupportedFormatError`‑t válthat ki. Ebben az esetben érdemes a képet a Pillow‑val tiszta PNG‑re konvertálni, mielőtt betöltenéd.

## 4. lépés: OCR végrehajtása PNG-n – Felismerés futtatása

Miután a kép a memóriában van, végre is **perform OCR on PNG**. A `recognize` metódus elindítja a motor csővezetékét (előfeldolgozás, szegmentálás, osztályozás) és feltölti az eredményobjektumot.

```python
# Execute the OCR process
ocr_engine.recognize()
```

Ez után a motor tartalmazza a felismert szöveget. Az `result` attribútumon keresztül érheted el:

```python
# Retrieve the plain text output
recognized_text = ocr_engine.result.text
print("📝 OCR Result:")
print(recognized_text)
```

**Miért érdemes ellenőrizni az eredményt:**  
Néhány OCR motor üres karakterláncot ad alacsony kontrasztú képek esetén. Az eredmény azonnali megtekintése lehetővé teszi, hogy eldöntsd, szükséges‑e előfeldolgozás (pl. kontraszt növelése) a újrafuttatás előtt.

## 5. lépés: Összeállítás – Újrahasználható függvény

A részek egyetlen függvénybe való összevonása megkönnyíti a hívást más szkriptekből vagy webszolgáltatásokból. Ez egyben bemutatja, hogyan **load image for OCR** és **perform OCR on PNG** egy rendezett csomagban.

```python
def ocr_png(image_path: str, log_dir: str = "logs") -> str:
    """
    Load a PNG image, run aocr OCR, and return the extracted text.
    
    Parameters
    ----------
    image_path : str
        Full path to the PNG file.
    log_dir : str, optional
        Directory where the debug log will be written.
    
    Returns
    -------
    str
        The plain‑text OCR result.
    """
    import os
    import aocr

    # Ensure the log directory exists
    os.makedirs(log_dir, exist_ok=True)

    # ---------- Logging ----------
    logger = aocr.Logging()
    logger.set_output_file(os.path.join(log_dir, "ocr_debug.log"))
    logger.set_level(aocr.LoggingLevel.DEBUG)

    # ---------- Engine ----------
    engine = aocr.OcrEngine()
    engine.logging = logger

    # ---------- Load Image ----------
    try:
        engine.load_image(image_path)
    except Exception as exc:
        logger.error(f"Failed to load image {image_path}: {exc}")
        raise

    # ---------- Recognize ----------
    engine.recognize()
    return engine.result.text

# Example usage
if __name__ == "__main__":
    txt = ocr_png("samples/invoice.png")
    print("\n--- Extracted Text ---\n")
    print(txt)
```

A szkript futtatása részletes `ocr_debug.log` fájlt hoz létre a `logs` mappában, majd a felismert szöveget a konzolra írja. Most már van egy **perform OCR on PNG** segédeszközöd, amelyet máshol is importálhatsz.

## Gyakori kérdések és buktatók

- **Át kell konvertálnom a PNG‑t más formátumra?**  
  Általában nem. A `aocr` natívan kezeli a PNG‑t, de ha a kép nagyon nagy (>10 MP), érdemes előbb lecsökkenteni a feldolgozási sebesség növelése érdekében.

- **Mi van, ha a naplófájl túl nagyra nő?**  
  Forgasd meg a naplót minden futtatás után, vagy állítsd a szintet `INFO`‑ra, amint megbizonyosodtál a pipeline működéséről.

- **Feldolgozhatok több képet egy ciklusban?**  
  Természetesen. Hívd meg egyszerűen az `ocr_png`‑t minden fájlra; a függvény minden alkalommal friss naplózót hoz létre, így a naplók elkülönülnek.

- **Van mód arra, hogy a sima szöveg helyett körvonalakat (bounding boxes) kapjak?**  
  Igen – az `engine.result` tartalmazza a `boxes` és `confidences` mezőket is. Nézd meg a `aocr` dokumentációt a `result.boxes`‑ról, ha elrendezési információra van szükséged.

## Következtetés

Most már tudod, hogyan **load image for OCR** és **perform OCR on PNG** a `aocr` könyvtárral, egy robusztus naplózási beállítással, amely a hibakeresést egyszerűvé teszi. A példafüggvény magába foglalja az egész munkafolyamatot, így bármely projektbe beillesztheted és azonnal elkezdheted a szöveg kinyerését.

Mi a következő lépés? Próbáld ki a motort különböző képformátumokkal (JPEG, TIFF), hogy lásd, hogyan változik a pontosság, vagy kísérletezz előfeldolgozási technikákkal, mint a küszöbölés, hogy javítsd a zajos szkennelt képek eredményeit. Ha érdekel a strukturált adatok (táblázatok, űrlapok) kinyerése, nézd meg a `aocr` szekciókat a layout analízisről – remekül kiegészítik, amit most építettél.

Boldog kódolást, és legyen az OCR pipeline-od mindig hibamentes!

## Mit érdemes még megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy további API funkciókat saját projektjeidben is elsajátíthasd és alternatív megvalósítási megközelítéseket felfedezhess.

- [Képből szöveg kinyerése Aspose OCR‑rel – Lépésről‑lépésre útmutató](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Hogyan OCR‑elj képet – OCR végrehajtása képen az OCR Image Recognition‑ben](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Képből szöveg kinyerése – OCR optimalizálás Aspose.OCR‑rel .NET‑hez](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}