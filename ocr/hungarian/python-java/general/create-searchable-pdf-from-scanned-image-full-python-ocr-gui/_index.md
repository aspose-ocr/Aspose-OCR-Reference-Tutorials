---
category: general
date: 2026-07-05
description: Készíts kereshető PDF-et Python segítségével. Tanuld meg, hogyan OCR-ozz
  beolvasott PNG-t, konvertálj beolvasott képet PDF-be, és szerezd meg a kereshető
  PDF-et percek alatt.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: hu
og_description: Készítsen gyorsan kereshető PDF-et. Ez az útmutató bemutatja, hogyan
  lehet OCR-t alkalmazni egy PNG-re, átalakítani egy beolvasott képes PDF-et, és Python
  segítségével kereshető PDF-et létrehozni.
og_title: Kereshető PDF létrehozása beolvasott képből – Python OCR útmutató
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF with Python. Learn how to OCR a scanned PNG,
    convert scanned image PDF, and get a searchable PDF in minutes.
  headline: Create Searchable PDF from Scanned Image – Full Python OCR Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF
- Automation
title: Kereshető PDF létrehozása beolvasott képből – Teljes Python OCR útmutató
url: /hu/python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kereshető PDF létrehozása beolvasott képből – Teljes Python OCR útmutató

Gondolkodtál már azon, hogyan **hozhatsz létre kereshető PDF-et** egy beolvasott képből anélkül, hogy drága szoftvert kellene vásárolnod? Nem vagy egyedül. Sok irodában a PDF-ek lapos képként érkeznek – nehezen kereshetők, lehetetlen másolni‑beilleszteni, és rémálom a megfelelőségi auditok során. A jó hír? Néhány Python sorral ezt a statikus PNG‑t teljesen kereshető PDF‑vé alakíthatod, és a folyamat egyszerűbb, mint gondolnád.

Ebben az útmutatóban egy komplett **OCR felismerési példát** dolgozunk fel, az első lépéstől a megfelelő könyvtár telepítéséig egészen a végleges PDF fájl írásáig. A végére pontosan tudni fogod, hogyan **konvertálj beolvasott kép PDF‑et**, hogyan **ocr pdf-et hajts végre** programozottan, és egy újrahasználható szkriptet kapsz, amelyet bármely projektbe beilleszthetsz.

## Mit fogsz megtanulni

- Python OCR könyvtár telepítése és konfigurálása (használjuk a `pytesseract`‑ot és a `pdf2image`‑t).
- Az OCR motor inicializálása és a nyelv beállítása.
- Beolvasott PNG (vagy bármely kép) betöltése és OCR‑ra futtatása.
- Az OCR eredmény átalakítása **kereshető PDF‑dé** (byte array) és mentése.
- Tippek többoldalas dokumentumok, különböző nyelvek és gyakori buktatók kezeléséhez.

Előzetes OCR tapasztalat nem szükséges – csak egy működő Python 3 környezet és egy kis kíváncsiság.

---

## Kereshető PDF létrehozása – Áttekintés

Az alábbi magas szintű folyamatábra mutatja a megvalósítandó lépéseket.  

![Create searchable PDF workflow diagram](https://example.com/flowchart.png "Create searchable PDF workflow diagram")

*Alt text: Kereshető PDF munkafolyamat diagram, amely bemutatja a motor inicializálását, a kép betöltését, az OCR felismerést, a PDF konvertálást és a fájl írását.*

---

## 1. lépés: Az OCR motor inicializálása (how to ocr pdf)

Miért kell egyáltalán inicializálni valamit? Az OCR motor az az agy, amely a pixelmintákat karakterekké értelmezi. Egy motorpéldány létrehozásával és a nyelv kifejezett megadásával azt mondjuk a könyvtárnak, milyen ábécét várjon, ami drámaian javítja a pontosságot.

```python
import pytesseract
from pdf2image import convert_from_path
from PIL import Image
import io

# Ensure Tesseract is on your PATH or provide the executable location
pytesseract.pytesseract.tesseract_cmd = r"/usr/local/bin/tesseract"  # adjust as needed

# Define the language – ENGLISH is the default, but you can add more (e.g., 'fra' for French)
ocr_language = "eng"
```

**Pro tipp:** Ha több nyelven szeretnél OCR‑t végezni, telepítsd a megfelelő nyelvi csomagokat a Tesseract‑hez, és adj meg egy listát, például `"eng+spa"` a `ocr_language`‑nek.

---

## 2. lépés: A beolvasott kép betöltése (convert scanned image pdf)

A következő feladat a képadatok Pythonba juttatása. Akár egyetlen PNG‑ről, akár egy többoldalas TIFF‑ről van szó, a `PIL.Image` osztály képes megnyitni azt. Ha egy már beolvasott képeket tartalmazó PDF‑ből indulsz, a `pdf2image` minden oldalt képpé konvertál számunkra.

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**Miért fontos:** A kép Pillow objektumként való betöltése hozzáférést biztosít a nyers pixeladatokhoz, amelyekre az OCR motornak szüksége van. Ennek kihagyása és a nyers bájtok közvetlen átadása hibához vezet.

---

## 3. lépés: OCR felismerés végrehajtása a képen (ocr recognition example)

Most jön a szórakoztató rész – a motor hagyja, hogy elolvassa a szöveget. A `pytesseract.image_to_pdf_or_hocr` egy PDF bájtfolyamot ad vissza, amely már tartalmaz egy láthatatlan szövegréteget, éppen ezt akarjuk egy **kereshető PDF‑hez**.

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**Szélsőséges eset:** Ha a képed alacsony kontrasztú, fontold meg egy egyszerű küszöb alkalmazását OCR előtt:

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

Ez a kis előfeldolgozási lépés drámai módon növelheti a pontosságot.

---

## 4. lépés: PDF bájtok fájlba írása (convert png searchable pdf)

Az OCR könyvtár egy byte array‑t ad át – tekintsd úgy, mint egy PDF fájl nyers tartalmát. Most már csak ezt a bájtot kell lemezre írni.

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**Mit fogsz látni:** Nyisd meg a keletkezett fájlt bármely PDF‑olvasóban, és keress egy olyan szót, amely biztosan szerepel az eredeti képen. A kiemelésnek közvetlenül a megfelelő helyre kell ugrania, bizonyítva, hogy a láthatatlan szövegréteg működik.

---

## 5. lépés: Többoldalas dokumentumok kezelése (convert scanned image pdf)

A valóságban a szerződések gyakran több oldalasak. **Convert scanned image pdf** fájlok több oldallal való feldolgozásához iterálj minden oldalon, OCR‑zd őket, majd fűzd össze a kapott PDF‑eket.

```python
def ocr_image_to_pdf(image_obj, lang="eng"):
    """Helper that returns PDF bytes for a single image."""
    return pytesseract.image_to_pdf_or_hocr(image_obj, lang=lang, extension='pdf')

def merge_pdfs(pdf_bytes_list):
    """Combine multiple PDF byte streams into one."""
    from PyPDF2 import PdfMerger
    merger = PdfMerger()
    for i, pdf_bytes in enumerate(pdf_bytes_list):
        merger.append(io.BytesIO(pdf_bytes))
    output = io.BytesIO()
    merger.write(output)
    merger.close()
    return output.getvalue()

# Example: convert a multi‑page scanned PDF to searchable PDF
pages = convert_from_path("YOUR_DIRECTORY/scanned_contract.pdf", dpi=300)
pdf_parts = [ocr_image_to_pdf(p, lang=ocr_language) for p in pages]
final_pdf = merge_pdfs(pdf_parts)

with open("YOUR_DIRECTORY/contract_searchable.pdf", "wb") as f:
    f.write(final_pdf)

print("✅ Multi‑page searchable PDF created.")
```

**Miért egyesítünk?** Minden `image_to_pdf_or_hocr` hívás egy önálló PDF‑et hoz létre. Az egyes PDF‑ek egyesítése biztosítja, hogy a végdokumentum megőrizze az eredeti oldalsorrendet.

---

## Gyakori buktatók és megoldások

| Tünet | Valószínű ok | Megoldás |
|-------|--------------|----------|
| A PDF megnyitása után nincs kereshető szöveg | A Tesseract nem talál karaktereket (üres kimenet) | Ellenőrizd a képminőséget, növeld a DPI‑t, vagy alkalmazz előfeldolgozást (kontraszt, binarizálás). |
| torz karakterek (pl. �) | Rossz nyelvi csomag vagy hiányzó betűkészletek | Telepítsd a megfelelő nyelvi adatot (`tesseract‑lang‑eng`) és győződj meg róla, hogy az `ocr_language` egyezik. |
| PDF fájlméret hatalmas (>10 MB egyoldalas képnél) | Lossless PNG használata forrásként; az OCR egy teljes felbontású képet ad hozzá | Méretezz le a képet OCR előtt (`image.thumbnail((1240, 1754))` A4-hez). |
| A szkript Windows‑on “tesseract.exe not found” hibát dob | A Tesseract bináris nincs a PATH‑ban | Add hozzá: `pytesseract.pytesseract.tesseract_cmd = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"` (állítsd be a megfelelő útvonalat). |

---

## Teljes, azonnal futtatható szkript

Összegezve, itt egy egyetlen fájl, amelyet kimásolhatsz és futtathatsz:

```python
#!/usr/bin/env python3
"""
create_searchable_pdf.py
A complete example that converts a scanned PNG (or PDF) into a searchable PDF using Tesseract OCR.
"""

import io
import sys
from pathlib import Path

import pytesseract
from pdf2image import convert_from_path
from PIL import Image
from PyPDF2 import PdfMerger

# -------------------- Configuration --------------------
# Adjust these paths for your environment
TESSERACT_CMD = r"/usr/local/bin/tesseract"   # macOS/Linux
# TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"  # Windows
OCR_LANGUAGE = "eng"                         # Add '+spa' for Spanish, etc.
INPUT_PATH = Path("YOUR_DIRECTORY/scanned_agreement.png")
OUTPUT_PATH = Path("YOUR_DIRECTORY/agreement_searchable.pdf")
# -------------------------------------------------------

# Point pytesseract at the executable
pytesseract.pytesseract.tesseract_cmd = TESSERACT_CMD

def load_image(path: Path) -> Image.Image:
    """Load an image from disk; supports PNG, JPG, TIFF."""
    if not path.is_file():
        sys.exit(f"❌ File not found: {path}")
    return Image.open(path)

def ocr_to_pdf_bytes(img: Image.Image, lang: str = OCR_LANGUAGE) -> bytes:
    """Run OCR on a Pillow image and return PDF bytes with hidden text."""
    return pytesseract.image_to_pdf_or_hocr(img, lang=lang, extension='pdf')

def write_pdf(data: bytes, dest: Path):
    """Write PDF byte stream to a file."""
    dest.parent.mkdir(parents=True, exist_ok=True)
    with open(dest, "wb") as f:
        f.write(data)
    print(f"✅ Searchable PDF saved to {dest}")

def main():
    # Load the scanned image
    image = load_image(INPUT_PATH)

    # Optional: improve contrast for low‑quality scans
    # image = image.convert('L').point(lambda x: 0 if x < 128 else 255, '1')

    # OCR → PDF bytes
    pdf_bytes = ocr_to_pdf_bytes(image)

    # Save the result
    write_pdf(pdf_bytes, OUTPUT_PATH)

if __name__ == "__main__":
    main()
```

Mentsd el `create_searchable_pdf.py` néven, cseréld ki a helyőrzőket a valós útvonalakra, majd futtasd:

```bash
python create_searchable_pdf.py
```

Látnod kell egy


## Mit érdemes még megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy további API‑funkciókat saját projektjeidben is könnyedén alkalmazhass, illetve alternatív megvalósítási módokat fedezhess fel.

- [Hogyan OCR‑zz PDF‑et .NET‑ben az Aspose.OCR‑val](/ocr/english/net/text-recognition/recognize-pdf/)
- [Képek PDF‑vé konvertálása C# – Többoldalas OCR eredmény mentése](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [OCR PDF dokumentumok felismerése Aspose.OCR‑val Java‑ban](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}