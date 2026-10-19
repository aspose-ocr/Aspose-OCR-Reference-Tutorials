---
category: general
date: 2026-05-31
description: Keressenelhető PDF létrehozása beolvasott képekből Python OCR-rel. Tanulja
  meg, hogyan konvertáljon beolvasott képes PDF-et, hogyan konvertáljon TIFF-et PDF-be,
  és hogyan adjon hozzá OCR szövegréteget percek alatt.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- convert tiff to pdf
- how to run OCR
- add OCR text layer
language: hu
og_description: Készítsen azonnal kereshető PDF-et. Ez az útmutató bemutatja, hogyan
  futtathat OCR-t, konvertálhat beolvasott képes PDF-et, és adhat hozzá OCR szövegréteget
  egyetlen Python szkript segítségével.
og_title: Kereshető PDF létrehozása Python segítségével – Teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  headline: Create Searchable PDF with Python – Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  name: Create Searchable PDF with Python – Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: 1️⃣ Can I process multi‑page PDFs?
    text: Yes. Use `ocr_engine.load_image("file.pdf")` and then loop over each page
      with `ocr_engine.recognize(pdf_save_options, page_number)`. The library will
      automatically generate a multi‑page searchable PDF.
  - name: 2️⃣ What if my source file is a high‑resolution TIFF (300 dpi+)?
    text: 'Higher DPI yields better OCR accuracy but also larger memory usage. If
      you hit a `MemoryError`, downscale the image first:'
  - name: 3️⃣ How do I change the language of the OCR?
    text: 'Set the `language` property on the engine before loading the image:'
  - name: 4️⃣ What if I need to keep the original image quality?
    text: The `PdfSaveOptions` class has a `compression` property. Set it to `PdfCompression.None`
      to preserve the raster data exactly as it was.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Document Automation
title: Kereshető PDF létrehozása Python‑ban – Lépésről‑lépésre útmutató
url: /hu/python-java/general/create-searchable-pdf-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása Python‑nal – Lépésről‑lépésre útmutató

Gondolkodtál már azon, hogyan lehet **create searchable PDF**-t létrehozni egy beolvasott oldalból anélkül, hogy tucatnyi eszközt kellene cserélgetned? Nem vagy egyedül. Sok irodai munkafolyamatban egy beolvasott TIFF vagy JPEG kerül a megosztott meghajtóra, és a következő személynek kézzel kell másolnia‑beillesztenie a szöveget – fájdalmas, hibára hajlamos és időpazarló.  

Ebben az útmutatóban egy tiszta, programozott megoldáson keresztül vezetünk végig, amely lehetővé teszi, hogy **convert scanned image PDF**, **convert TIFF to PDF**, és **add OCR text layer** egy lépésben. A végére egy kész‑használatra szánt szkriptet kapsz, amely futtatja az OCR‑t, beágyazza a rejtett szöveget, és egy kereshető PDF‑et állít elő, amelyet indexelhetsz, kereshetsz vagy magabiztosan megoszthatsz.

## Amire szükséged lesz

- Python 3.9+ (bármely friss verzió működik)
- `aspose-ocr` és `aspose-pdf` csomagok (telepítve a `pip install aspose-ocr aspose-pdf` paranccsal)
- Egy beolvasott képfájl (`.tif`, `.png`, `.jpg`, vagy akár egy PDF‑oldal, amely csak egy kép)
- Mérsékelt mennyiségű RAM (az OCR motor könnyű; még egy laptop is képes kezelni)

> **Pro tipp:** Ha Windows‑t használsz, a csomagok legegyszerűbb beszerzési módja, ha a parancsot egy emelt jogosultságú PowerShell ablakban futtatod.

```bash
pip install aspose-ocr aspose-pdf
```

Most, hogy az előfeltételek rendben vannak, merüljünk el a kódban.

## 1. lépés: OCR motor példány létrehozása – *create searchable pdf*

Az első dolog, amit teszünk, elindítjuk az OCR motort. Gondolj rá úgy, mint egy agyra, amely minden pixelt elolvas és karakterekké alakít.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine – this is the core of the create searchable pdf process
ocr_engine = OcrEngine()
```

> **Miért fontos:** A motor egyszeri inicializálása alacsony memóriahasználatot biztosít. Ha `OcrEngine()`‑t egy ciklusban minden oldalra meghívnád, gyorsan kifogynál az erőforrásokból.

## 2. lépés: Beolvasott kép betöltése – *convert tiff to pdf* & *convert scanned image pdf*

Ezután irányítsd a motort arra a fájlra, amelyet feldolgozni szeretnél. Az API bármilyen raszteres képet elfogad, így egy TIFF ugyanolyan jól működik, mint egy JPEG.

```python
# Load the image you want to OCR. Replace the path with your own file location.
ocr_engine.load_image("YOUR_DIRECTORY/scanned_page.tif")
```

Ha egy PDF‑ed csak egy beolvasott képet tartalmaz, akkor is használhatod a `load_image`‑t, mivel az Aspose automatikusan kinyeri az első oldalt.

## 3. lépés: PDF mentési beállítások előkészítése – *add OCR text layer*

Itt konfiguráljuk, hogyan nézzen ki a végleges PDF. A kulcsfontosságú jelző a `create_searchable_pdf`; `True`‑ra állítva a könyvtár egy láthatatlan szövegréteget ágyaz be, amely tükrözi a vizuális tartalmat.

```python
from aspose.pdf import PdfSaveOptions

pdf_save_options = PdfSaveOptions()
pdf_save_options.create_searchable_pdf = True   # embed OCR text layer
pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"
```

> **Mit csinál a szövegréteg:** Amikor megnyitod a létrehozott fájlt az Adobe Readerben és megpróbálsz szöveget kijelölni, a rejtett karaktereket fogod látni. A keresőmotorok is indexelni tudják őket – tökéletes megfelelőség vagy archiválás esetén.

## 4. lépés: OCR futtatása és mentés – *how to run OCR* egyetlen hívásban

Most történik a varázslat. Egy metódushívás lefuttatja a felismerő motort és a kereshető PDF‑et a lemezre írja.

```python
# Run OCR and generate the searchable PDF in one go
ocr_engine.recognize(pdf_save_options)

print("PDF saved as searchable PDF.")
```

A `recognize` metódus egy státuszobjektust ad vissza, amelyet hibák után ellenőrizhetsz, de a legtöbb egyszerű esetben a fenti egyszerű hívás elegendő.

### Várt kimenet

A szkript futtatása a következőt írja ki:

```
PDF saved as searchable PDF.
```

Ha megnyitod a `scanned_page_searchable.pdf` fájlt, észre fogod venni, hogy szöveget kijelölhetsz, másolhatsz‑beilleszthetsz, és még egy `Ctrl+F` keresést is futtathatsz. Ez a **create searchable pdf** munkafolyamat jellemzője.

## Teljes működő szkript

Az alábbiakban a teljes, futtatható szkript található. Csak cseréld ki a helyőrző útvonalakat a saját fájlhelyeidre.

```python
# ------------------------------------------------------------
# create_searchable_pdf.py – Convert scanned image to searchable PDF
# ------------------------------------------------------------

from aspose.ocr import OcrEngine
from aspose.pdf import PdfSaveOptions

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load image (TIFF, JPEG, PNG, or scanned PDF page)
    image_path = "YOUR_DIRECTORY/scanned_page.tif"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure PDF output – embed OCR text layer
    pdf_save_options = PdfSaveOptions()
    pdf_save_options.create_searchable_pdf = True
    pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"

    # 4️⃣ Run OCR and write searchable PDF
    ocr_engine.recognize(pdf_save_options)

    print("PDF saved as searchable PDF.")

if __name__ == "__main__":
    main()
```

Mentsd el `create_searchable_pdf.py` néven, és futtasd:

```bash
python create_searchable_pdf.py
```

## Gyakori kérdések és széljegyek

### 1️⃣ Feldolgozhatok többoldalas PDF‑eket?

Igen. Használd a `ocr_engine.load_image("file.pdf")`‑t, majd egy ciklussal dolgozd fel az egyes oldalakat a `ocr_engine.recognize(pdf_save_options, page_number)`‑val. A könyvtár automatikusan többoldalas kereshető PDF‑et generál.

### 2️⃣ Mi van, ha a forrásfájl egy nagy felbontású TIFF (300 dpi+)?

A magasabb DPI jobb OCR pontosságot eredményez, de nagyobb memóriahasználatot is. Ha `MemoryError`‑t kapsz, először méretezd le a képet:

```python
from PIL import Image
img = Image.open(image_path)
img = img.resize((int(img.width * 0.5), int(img.height * 0.5)), Image.ANTIALIAS)
img.save("temp.tif")
ocr_engine.load_image("temp.tif")
```

### 3️⃣ Hogyan változtathatom meg az OCR nyelvét?

Állítsd be a `language` tulajdonságot a motoron, mielőtt betöltenéd a képet:

```python
ocr_engine.language = "fra"   # French
```

A támogatott nyelvkódok teljes listája az Aspose dokumentációban található.

### 4️⃣ Mi van, ha meg kell őriznem az eredeti képminőséget?

A `PdfSaveOptions` osztálynak van egy `compression` tulajdonsága. Állítsd `PdfCompression.None`‑ra, hogy a raszteres adatot pontosan úgy őrizd meg, ahogy volt.

```python
pdf_save_options.compression = "None"
```

## Tippek a termelés‑kész telepítésekhez

- **Kötegelt feldolgozás:** Csomagold a fő logikát egy olyan függvénybe, amely fájlútvonalak listáját fogadja. Minden sikeres vagy sikertelen műveletet naplózz CSV‑ben az audit nyomvonalakhoz.
- **Párhuzamosság:** Használd a `concurrent.futures.ThreadPoolExecutor`‑t, hogy több magon futtass OCR‑t. Csak ne feledd, hogy minden szálnak saját `OcrEngine` példányra van szüksége.
- **Biztonság:** Ha érzékeny dokumentumokat kezelsz, futtasd a szkriptet egy sandbox környezetben, és a feldolgozás után azonnal töröld a temporális fájlokat.

## Összegzés

Most már tudod, hogyan kell **create searchable PDF** fájlokat létrehozni beolvasott képekből egy tömör Python szkript segítségével. Az OCR motor inicializálásával, egy TIFF (vagy bármilyen raszter) betöltésével, a `PdfSaveOptions` beállításával **add OCR text layer**, és végül a `recognize` meghívásával az egész **convert scanned image pdf** és **convert TIFF to PDF** folyamat egyetlen, ismételhető parancssá válik.

Következő lépések? Próbáld meg összekapcsolni ezt a szkriptet egy fájlfigyelővel, hogy bármely új beolvasás, amely egy mappába kerül, automatikusan kereshető legyen. Vagy kísérletezz különböző OCR nyelvekkel a többnyelvű archívumok támogatásához. A határ csak a képzeleted, ha az OCR‑t a PDF‑generálással kombinálod.

Van még kérdésed a **how to run OCR**-rel kapcsolatban más nyelvekben vagy keretrendszerekben? Hagyj egy megjegyzést alább, és jó kódolást! 

![Diagram, amely a beolvasott képből → OCR motor → kereshető PDF (create searchable pdf) folyamatot mutatja](searchable-pdf-flow.png "Create searchable pdf folyamat diagram")

## Mit érdemes még megtanulni?

- [Hogyan OCR‑elj PDF-et .NET‑ben az Aspose.OCR segítségével](/ocr/english/net/text-recognition/recognize-pdf/)
- [Képek konvertálása PDF‑be C# – Többoldalas OCR eredmény mentése](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Hogyan OCR‑elj képszöveget nyelvvel az Aspose.OCR használatával](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}