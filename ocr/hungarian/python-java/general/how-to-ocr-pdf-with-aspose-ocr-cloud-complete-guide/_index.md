---
category: general
date: 2026-06-06
description: Hogyan OCR-elj PDF-et az Aspose OCR Cloud segítségével. Tanulja meg,
  hogyan nyerjen ki szöveget PDF-ből, konvertáljon PDF-oldalakat PNG-re, és mentse
  el a PDF-oldalak képeit Pythonban.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf page png
- extract plain text pdf
- save pdf page images
language: hu
og_description: Hogyan OCR-eljünk PDF-et az Aspose OCR Cloud segítségével. Ez az útmutató
  bemutatja, hogyan lehet szöveges PDF-et kinyerni, PDF-oldalakat PNG-re konvertálni,
  és PDF-oldalak képeit menteni.
og_title: Hogyan OCR-elj PDF-et az Aspose OCR Cloud segítségével – Lépésről lépésre
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Aspose OCR Cloud. Learn to extract text from PDF,
    convert PDF page PNG, and save PDF page images in Python.
  headline: How to OCR PDF with Aspose OCR Cloud – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Hogyan OCR-eljük a PDF-et az Aspose OCR Cloud segítségével – Teljes útmutató
url: /hu/python-java/general/how-to-ocr-pdf-with-aspose-ocr-cloud-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan OCR-elj PDF-et az Aspose OCR Cloud segítségével – Teljes útmutató

Valaha is elgondolkodtál már azon, hogy **hogyan OCR-elj PDF** fájlokat anélkül, hogy nehéz asztali eszközökkel küzdenél? Nem vagy egyedül – sok fejlesztő ütközik ebbe a falba, amikor gyors, programozott módra van szükségük a beolvasott dokumentumok szövegének kinyeréséhez. A jó hír? Az Aspose OCR Cloud segítségével **kivonhatod a szöveget a PDF‑ből**, minden oldalt PNG‑vé alakíthatsz, és akár **elmentheted a PDF oldal képeit** későbbi felhasználásra, mindezt egy rendezett Python szkriptből.

Ebben az útmutatóban mindent végigvezetünk, amit tudnod kell: a SDK telepítésétől, a motor licencelésén át a többoldalas PDF‑ek felismeréséig, a sima szöveg kinyeréséig, az oldalak PNG‑re konvertálásáig, és a képek lemezre mentéséig. A végére egy újrahasználható kódrészletet kapsz, amelyet bármely projektbe beilleszthetsz, amelynek **hogyan OCR-elj PDF** képességre van szüksége.

## Amire szükséged lesz

- **Python 3.8+** (a kód 3.10‑n és újabb verziókon is működik)  
- Aspose OCR Cloud fiók – ingyenes próba licencfájlt kapsz (`Aspose.OCR.lic`)  
- A `asposeocrcloud` csomag (`pip install asposeocrcloud`)  
- Egy beolvasott, többoldalas PDF, amelyet fel szeretnél dolgozni  

Ennyi. Nincs extra bináris, nincs natív függőség, csak tiszta Python.

## Hogyan OCR-elj PDF – Beállítás és licenc

Mielőtt bármilyen OCR metódust meghívnál, el kell mondanod a SDK-nak, ki vagy. Az Aspose egy könnyű licencfájlt használ, amelyet a szkripted számára elérhető helyre kell elhelyezned.

```python
# Step 1: Import the OCR package and apply your license (optional but recommended)
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply the license – replace the path with your actual .lic file location
License().set_license("Aspose.OCR.lic")
```

*Pro tipp:* Ha kihagyod a licenc lépést, a SDK még mindig működik, de egy kis vízjelet ágyaz be a kimeneti képekbe. Nem ideális a termeléshez.

## 2. lépés: Az Aspose OCR Cloud Python SDK telepítése

Nyiss egy terminált és futtasd:

```bash
pip install asposeocrcloud
```

A csomag letölti az összes szükséges függőséget (requests, pillow, stb.), így nem kell mást keresned.

## 3. lépés: OCR motor létrehozása és nyelv kiválasztása

A motor a művelet szíve. Bármely, az Aspose által támogatott nyelvet megadhatod; az angol a legtöbb esetben működik.

```python
# Step 3: Create an OCR engine and set the recognition language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)
```

Miért állítsd be a nyelvet? Mert az OCR motor nyelvspecifikus szótárakat használ a pontosság javításához. Ha francia PDF‑eket dolgozol fel, egyszerűen cseréld le az `ENGLISH`‑t `FRENCH`‑re.

## 4. lépés: Mutass a többoldalas PDF‑re

Add meg a motor számára a teljes elérési utat a feldolgozni kívánt fájlhoz. Relatív utak is megfelelőek, amíg a szkript munkakönyvtárából feloldódnak.

```python
# Step 4: Specify the path to the multi‑page PDF you want to process
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"
```

Győződj meg róla, hogy a fájl olvasható; különben `FileNotFoundError` hibát kapsz.

## 5. lépés: OCR futtatása – Lista eredményekkel

A `recognize_pdf` hívása egy listát ad vissza, ahol minden elem a forrás PDF egy oldalának felel meg.

```python
# Step 5: Run OCR on the PDF – a list of OcrResult objects is returned (one per page)
results = engine.recognize_pdf(pdf_path)
```

Minden `OcrResult` két hasznos tulajdonságot tartalmaz:

* `text` – az oldal egyszerű szöveges ábrázolása (nagyszerű a **extract plain text pdf**-hez)  
* `image` – egy Pillow `Image` objektum a renderelt oldalról (tökéletes a **convert pdf page png**-hez)

## 6. lépés: Szöveg kinyerése a PDF‑ből és oldalak PNG‑re konvertálása

Most végigiterálunk az eredményeken, kiírjuk a kinyert szöveget, és minden oldalról elmentünk egy PNG verziót.

```python
# Step 6: Iterate through each page, output the extracted text and optionally save the page image
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    # Extract plain text for this page
    print(res.text)                     # <-- this is the "extract plain text pdf" part
    # Convert the page to PNG and save it
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # <-- this does the "convert pdf page png"
```

### Várható konzolkimenet

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

A `page_1.png`, `page_2.png`, … fájlok is megtalálhatók a `YOUR_DIRECTORY` könyvtárban. Ezek a rasterizált oldalképek, amelyeket továbbadhatsz az utólagos képfeldolgozó csővezetékeknek.

## 7. lépés: PDF oldal képek mentése (opcionális utófeldolgozás)

Ha csak a képekre van szükséged, a szövegre nem, kihagyhatod a `print(res.text)` sort. Fordítva, ha a szöveget külön `.txt` fájlokban szeretnéd tárolni, csak adj hozzá egy apró írási lépést:

```python
# Optional: Save each page's text to a .txt file
for i, res in enumerate(results, start=1):
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)
```

Ez a kis kiegészítés azt mutatja, milyen egyszerű **PDF oldal képek mentése**, miközben a kinyert tartalmat is elmentjük.

## Teljes működő példa

Mindent összevonva, itt a teljes szkript, amelyet átmásolhatsz a `ocr_pdf.py` fájlba:

```python
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply your license – optional but removes watermarks
License().set_license("Aspose.OCR.lic")

# Initialize the OCR engine and set language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)

# Path to the source PDF
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"

# Run OCR – get a list of results (one per page)
results = engine.recognize_pdf(pdf_path)

# Process each page
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(res.text)  # extract plain text PDF
    # Save the rendered page as PNG
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # convert PDF page PNG
    # Optional: also save the text to a .txt file
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)  # save PDF page images + text
```

Futtasd a következővel:

```bash
python ocr_pdf.py
```

A konzolon látnod kell minden oldal szövegének kiírását és egy sor PNG fájlt

## Mit érdemes következőként megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan OCR-elj PDF-et .NET-ben az Aspose.OCR-rel](/ocr/english/net/text-recognition/recognize-pdf/)  
- [PDF szöveg felismerése – OCR műveletek az Aspose.OCR Java verziójával](/ocr/english/java/ocr-operations/recognize-pdf/)  
- [Képek konvertálása PDF‑re C#‑ban – Többoldalas OCR eredmény mentése](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}