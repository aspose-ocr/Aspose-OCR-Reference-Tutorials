---
category: general
date: 2026-06-25
description: Végezz OCR-t PDF-en Python segítségével—tanuld meg, hogyan tölts be PDF-et
  OCR-hez, hogyan nyerd ki a szöveget a PDF oldalakból, és hogyan tekintsd meg hatékonyan
  a felismert szöveget.
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF pages
- load PDF for OCR
- how to OCR large PDF
- preview recognized text
language: hu
og_description: OCR végrehajtása PDF-en Pythonban. Ez az útmutató bemutatja, hogyan
  töltsünk be PDF-et OCR-hez, hogyan nyerjünk ki szöveget a PDF-oldalakból, és hogyan
  tekintsük meg gyorsan a felismert szöveget.
og_title: OCR végrehajtása PDF-en Python segítségével – Lépésről lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  headline: Perform OCR on PDF with Python – Complete Guide
  type: TechArticle
- description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  name: Perform OCR on PDF with Python – Complete Guide
  steps:
  - name: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
    text: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
  - name: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
    text: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
  - name: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
    text: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
  - name: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
    text: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: OCR végrehajtása PDF-en Python segítségével – Teljes útmutató
url: /hu/python/general/perform-ocr-on-pdf-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR végrehajtása PDF-en Python‑nal – Teljes útmutató

Szükséged volt már **OCR végrehajtására PDF** fájlokon, de nem tudtad, hol kezdjed? Lehet, hogy egy hegynyi beolvasott szerződésed van, vagy egy hatalmas kézikönyv, ami nem hajlandó együttműködni a szokásos szöveg‑kivonóddal. Röviden, **PDF betöltése OCR‑hez**, a szöveg kinyerése, és egy gyors előnézet megjelenítése – mindezt anélkül, hogy a géped memóriáját túlterhelnéd.

Nos, jó helyen jársz. Ebben a tutorialban egy teljesen működő Python‑szkriptet mutatunk be, amely **kivonja a szöveget a PDF oldalakból**, megmutatja, hogyan **előnézetet készíthetsz a felismert szövegről**, és még a klasszikus **hogyan OCR‑ozz nagy PDF‑et** problémát is hatékonyan kezeli.

A végére egy azonnal futtatható programmal, a konfigurációs beállítások világos megértésével és néhány tippel leszel felvértezve, hogy elkerüld a kezdők gyakori buktatóit.

---

## Mit fogsz megtanulni

- Hogyan **PDF‑t tölts be OCR‑hez** a `aocr` könyvtár segítségével.
- A pontos lépések a **OCR végrehajtásához PDF** oldalakon egy‑esével.
- Módszerek a **szöveg kinyerésére PDF oldalakról**, miközben a memóriahasználatot kordában tartod.
- Hogyan **előnézetet készíts a felismert szövegről** a helyesség ellenőrzéséhez.
- Stratégiák **nagy PDF‑ek** kezelésére anélkül, hogy a RAM kimerülne.

> **Tipp:** Ez az útmutató azt feltételezi, hogy Python 3.9+ van telepítve, és van alapvető ismereted a virtuális környezetekről. Ha újonc vagy a Pythonban, először állíts be egy virtualenv‑et – higgy nekem, később rengeteg fejfájást megspórolsz.

---

## Előfeltételek

| Követelmény | Miért fontos |
|-------------|---------------|
| `aocr` Python csomag (vagy bármely kompatibilis OCR motor) | Biztosítja a szkriptben használt `OcrEngine` osztályt. |
| `pip` és egy virtuális környezet | Elkülöníti a függőségeket a rendszer‑Pythonodtól. |
| Elég lemezhely a temporális képekhez | Néhány OCR motor oldalképeket ír a lemezre a feldolgozás előtt. |
| Opcionális: `tqdm` a folyamatjelzőkhöz | Javítja a felhasználói élményt **hogyan OCR‑ozz nagy PDF‑et** feladatoknál. |

Telepítsd a szükséges csomagokat:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate
pip install aocr tqdm
```

Ha a PDF jelszóval védett, később meg kell adnod a jelszót – lásd az „Edge Cases” (különleges esetek) részt.

---

## 1. lépés: OCR motor beállítása

Először is szükségünk van egy OCR motor példányra. Gondolj rá úgy, mint egy agyra, amely minden oldal képét beolvassa és egyszerű szöveget ad vissza.

```python
import aocr                     # The OCR library
from tqdm import tqdm           # Optional, for a nice progress bar

def create_engine():
    """
    Initialise the OcrEngine with sensible defaults.
    Returns the configured engine ready for processing.
    """
    engine = aocr.OcrEngine()
    # Limit memory usage – crucial when tackling how to OCR large PDF files
    engine.max_memory_mb = 200               # 200 MB cap, adjust if needed
    # Choose a recognition mode that matches your source material
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine
```

> **Miért állítjuk be a `max_memory_mb`‑t?**  
> Az OCR motorok gyakran a lapképeket a RAM‑ban tárolják. A memória korlátozásával megakadályozod, hogy a szkript összeomoljon egy 500 oldalas szerződésnél.

---

## 2. lépés: PDF betöltése OCR‑hez és beállítások konfigurálása

Most ténylegesen **PDF‑t töltünk be OCR‑hez**. Az útvonal lehet abszolút vagy relatív; csak győződj meg róla, hogy a fájl létezik.

```python
def load_pdf(engine, pdf_path):
    """
    Loads the PDF into the OCR engine.
    Raises FileNotFoundError if the file does not exist.
    """
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages ready.")
    except Exception as e:
        raise RuntimeError(f"Failed to load PDF: {e}")
```

Ha a PDF titkosított, az `engine.load_pdf` általában kivételt dob. Ebben az esetben meghívhatod `engine.load_pdf(pdf_path, password="secret")`‑t – erről később lesz szó.

---

## 3. lépés: Szöveg kinyerése PDF oldalakról – a fő ciklus

Itt történik a **OCR végrehajtása PDF** oldalanként. Emellett **előnézetet készítünk a felismert szövegről** az első néhány száz karakterre, hogy ellenőrizhesd, minden rendben működik-e.

```python
def ocr_pages(engine, preview_len=200):
    """
    Iterates over each page, runs OCR, and yields the recognized text.
    Also prints a short preview for each page.
    """
    for page_index in tqdm(range(engine.page_count), desc="Processing pages"):
        # Select the current page – essential for multi‑page PDFs
        engine.select_page(page_index)

        # Perform the actual OCR
        page_text = engine.recognize()

        # Preview the first `preview_len` characters (helps with debugging)
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))

        yield page_text
```

> **Pro tipp:** A `tqdm` folyamatjelző vizuális visszajelzést ad, ami különösen hasznos **hogyan OCR‑ozz nagy PDF‑et** dokumentumoknál, amelyek feldolgozása perceket vehet igénybe.

---

## 4. lépés: Összeállítás – egy azonnal futtatható szkript

Az alábbiakban a teljes, futtatható példát láthatod. Mentsd el `pdf_ocr.py`‑ként, majd futtasd a `python pdf_ocr.py path/to/your/file.pdf` paranccsal.

```python
#!/usr/bin/env python3
"""
Complete script to perform OCR on PDF, extract text from PDF pages,
and preview recognized text. Works for both small and large PDFs.
"""

import sys
import aocr
from tqdm import tqdm

def create_engine():
    engine = aocr.OcrEngine()
    engine.max_memory_mb = 200
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine

def load_pdf(engine, pdf_path):
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages.")
    except Exception as exc:
        raise RuntimeError(f"Unable to load PDF: {exc}")

def ocr_pages(engine, preview_len=200):
    for page_index in tqdm(range(engine.page_count), desc="OCR progress"):
        engine.select_page(page_index)
        page_text = engine.recognize()
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))
        yield page_text

def main(pdf_path):
    engine = create_engine()
    load_pdf(engine, pdf_path)

    all_text = []
    for txt in ocr_pages(engine):
        all_text.append(txt)

    # Optional: write the combined output to a .txt file
    out_path = pdf_path.rsplit(".", 1)[0] + "_ocr.txt"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write("\n\n".join(all_text))
    print(f"\n✅ OCR complete. Full text saved to: {out_path}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python pdf_ocr.py <path_to_pdf>")
        sys.exit(1)
    pdf_file = sys.argv[1]
    main(pdf_file)
```

### Várható kimenet (részlet)

```
✅ Loaded 'large_contract.pdf' – 342 pages.

--- Page 1 Preview ---
Contract Agreement between Party A and Party B ... 

--- Page 2 Preview ---
Recitals: Whereas, the parties desire to ...

...
✅ OCR complete. Full text saved to: large_contract_ocr.txt
```

Minden oldalhoz egy rövid előnézetet látsz, majd egy végső megerősítést, hogy az összefűzött szövegfájl sikeresen létrejött.

---

## Különleges esetek és gyakorlati tippek

| Helyzet | Mit tegyünk |
|---------|-------------|
| **Titkosított PDF** | Add meg a jelszót: `engine.load_pdf(pdf_path, password="mySecret")`. |
| **Nagyon nagy PDF (> 1000 oldal)** | Növeld óvatosan a `max_memory_mb` értékét, vagy dolgozz darabokban (pl. 200 oldalanként). |
| **Vegyes tartalom (nyomtatott + kézírás)** | Állítsd át az `engine.recognition_mode`‑t `aocr.RecognitionMode.MIXED`‑re, ha a könyvtár támogatja. |
| **Hiányzó betűkészletek vagy rossz minőségű beolvasás** | Előfeldolgozd az oldalakat egy képenhálózó könyvtárral (pl. Pillow) a `recognize()` hívása előtt. |
| **Memória‑kimerüléses összeomlások** | Csökkentsd a `preview_len`‑t, vagy írd ki minden oldal szövegét közvetlenül a lemezre a lista helyett. |

---

## Hogyan OCR‑ozz nagy PDF‑et hatékonyan – haladó stratégiák

Amikor a **hogyan OCR‑ozz nagy PDF‑et** kérdésével foglalkozol, a sebesség és a stabilitás kritikus. Íme néhány trükk, amit beépíthetsz a szkriptbe:

1. **Oldalonkénti párhuzamosítás** – Használd a `concurrent.futures.ThreadPoolExecutor`‑t, ha az OCR motor szál‑biztonságú.
2. **Köztes képek gyorsítótárazása** – Néhány motor engedélyezi a rasterizált oldalak SSD‑re mentését, ami drámaian csökkenti a CPU‑terhelést az újrafuttatásoknál.
3. **Kimenet kötegelt írása** – Ahelyett, hogy egy Python listához adnád hozzá, nyisd meg egyszer a kimeneti fájlt, és írd ki az oldal szövegét, amint elkészül.
4. **DPI beállítása** – A DPI csökkentése a rasterizálás során memóriát takarít meg, de befolyásolhatja a pontosságot; találj egy megfelelő értéket (általában 200‑300 DPI).

Az alábbi rövid kódrészlet mutatja, hogyan párhuzamosíthatod az OCR lépést (opcionális, a használathoz kommenteld ki a sorokat):

```python
# from concurrent.futures import ThreadPoolExecutor

# def ocr_page(engine, idx):
#     engine.select_page(idx)
#     return engine.recognize()

# with ThreadPoolExecutor(max_workers=4) as executor:
#     results = list(tqdm(executor.map(lambda i: ocr_page(engine, i),
#                                    range(engine.page_count)),
#                     total=engine.page_count,
#                     desc="Parallel OCR"))
```

Ne feledd: a párhuzamosítás növelheti a CPU‑használatot, ezért figyeld a rendszer hőmérsékletét hosszú futtatások során.

---

## Gyakran ismételt kérdések

**K: Használhatom ezt a szkriptet más OCR könyvtárakkal, például a Tesseracttal?**  
V: Természetesen. Cseréld le az `aocr` hívásokat `pytesseract.image_to

## Mit érdemes még tanulni?

A következő tutorialok szorosan kapcsolódó témákat fednek le, amelyek tovább építenek a jelen útmutatóban bemutatott technikákra. Minden forrás tartalmaz teljesen működő kódpéldákat lépés‑ről‑lépésre magyarázatokkal, hogy segítsenek az API további funkcióinak elsajátításában és alternatív megvalósítási megközelítések felfedezésében a saját projektjeidben.

- [Hogyan OCR PDF-et .NET-ben az Aspose.OCR használatával](/ocr/english/net/text-recognition/recognize-pdf/)
- [Hogyan végezz képszöveg‑kivonást stream‑ből Aspose OCR‑rel](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Hogyan nyerj ki szöveget egy URL‑ről származó képből Aspose.OCR‑val Java-ban](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}