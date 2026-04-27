---
category: general
date: 2026-04-26
description: Hogyan használjunk OCR-t beolvasott PDF-eken, szöveget nyerjünk ki PDF-ből,
  OCR-t futtassunk PDF-en, és néhány lépésben alakítsuk a beolvasott PDF-et kereshető
  fájlokká.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: hu
og_description: 'hogyan használjunk OCR-t Pythonban: tanulja meg, hogyan nyerjen ki
  szöveget PDF-ből, futtasson OCR-t PDF-en, és alakítsa a beolvasott PDF-et kereshető
  dokumentummá.'
og_title: Hogyan használjuk az OCR-t – Gyors útmutató a PDF-ből szöveg kinyeréséhez
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Hogyan használjuk az OCR-t – Szöveg kinyerése PDF-ből Python segítségével
url: /hu/python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan használjuk az OCR-t – Szöveg kinyerése PDF-ből Python segítségével

Gondoltad már valaha, **hogyan használjuk az OCR-t**, hogy szöveget nyerjünk ki egy beolvasott szerződésből, nyugtából vagy e‑könyvből? Nem vagy egyedül. Sok valós projektben a kapott PDF csak egy kép, és OCR nélkül nem tudod keresni, indexelni vagy elemezni a tartalmát.  

Ebben az oktatóanyagban végigvezetünk egy teljes, futtatható példán, amely bemutatja, **hogyan használjuk az OCR-t**, hogyan **nyerhetünk ki szöveget PDF-ből**, és miért lehet érdemes **beolvasott PDF** fájlokat kereshető dokumentumokká konvertálni. Emellett érintjük a **PDF képként betöltése** finom művészetét is, hogy az OCR motor minden oldalt tisztán láthasson.

> **Gyors előzetes:** A végére egy olyan szkriptet kapsz, amely betölti a többoldalas PDF-et, OCR-t futtat minden oldalon, és kiírja a felismert szöveget – külső szolgáltatások nélkül.

## Amire szükséged lesz

- Python 3.9+ (bármely friss verzió működik)
- `aocr` csomag (vagy bármely kompatibilis OCR könyvtár, amely biztosítja az `OcrEngine` és `Image.load` funkciókat)
- Egy beolvasott PDF fájl, amelyet feldolgozni szeretnél (pl. `contract.pdf`)
- Mérsékelt mennyiségű RAM (≈ 200 MB 100‑oldalas PDF-enként általában elegendő)

Ha még nem telepítetted az OCR könyvtárat, futtasd:

```bash
pip install aocr
```

> **Pro tipp:** Használj virtuális környezetet a függőségek rendezett tartásához.

## Step 1: PDF betöltése képként – A kirakós első darabja

Mielőtt bármilyen OCR végrehajtható lenne, a PDF-et képként kell ábrázolni. Itt jön képbe a másodlagos kulcsszó **load pdf as image**.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*Miért fontos ez:* A `aocr.Image.load` belsőleg rasterizálja a PDF minden oldalát egy bitmapre, amelyet az OCR motor megért. Ha kihagyod ezt a lépést és a nyers PDF-et adod át, a motor hibát dob, mert pixel adatot vár, nem vektor adatot.

> **Megjegyzés:** Az útvonal lehet abszolút vagy relatív. Győződj meg róla, hogy a fájl olvasható; különben `FileNotFoundError`-t kapsz.

## Step 2: OCR futtatása PDF-en – Pixelek karakterekké alakítása

Most, hogy a PDF képként létezik, végre **futtathatunk OCR-t PDF-en**. Az alábbi kódrészlet egy lépésben feldolgozza az összes oldalt:

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*Mi történik a háttérben?* A `process_all_pages` végigiterál a rasterizált oldalakon, alkalmazza az OCR modellt, és egy listát ad vissza az eredményobjektumokról – egyet oldalanként. Minden eredmény tartalmazza a felismert szöveget, a megbízhatósági pontszámokat és a határoló dobozokat (ha később szükséged van rájuk).

## Step 3: Szöveg kinyerése PDF-ből – A karakterek kihúzása

Az OCR eredményekkel a tiszta szöveg kinyerése egyszerű. Végigiterálunk az oldalakon és kiírjuk a kimenetet, bemutatva a másodlagos kulcsszót **extract text from pdf**.

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**Várható kimenet** (rövidítve a tömörség kedvéért):

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

Ha a szöveget egyetlen karakterláncban szeretnéd, egyszerűen fűzd össze:

```python
full_text = "\n".join(r.text for r in page_results)
```

Most már sikeresen **kinyerted a szöveget PDF-ből** OCR segítségével.

## Step 4: Beolvasott PDF konvertálása – Kereshetővé tétele

Sok downstream eszköz (például Elasticsearch vagy SharePoint) kereshető PDF-et vár el a tiszta szöveg dump helyett. Beágyazhatod az OCR kimenetet az eredeti PDF-be, így hatékonyan **convert scanned PDF**-t kereshető verzióvá alakítva.

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*Miért éri meg?* A kereshető PDF megtartja az eredeti elrendezést és képeket, miközben lehetővé teszi a szöveg kijelölését és indexelését – nyer-nyer mind az emberek, mind a gépek számára.

## Gyakori buktatók és szélhelyzetek

### Többoldalas PDF-ek, amelyek nagyobbak a memóriánál

Ha a PDF-ed több száz oldalt tartalmaz, az egyszerre történő betöltése kimerítheti a RAM-ot. Az `aocr` könyvtár támogatja a lusta betöltést:

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

Ezután dolgozd fel az oldalakat egyesével:

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### Alacsony minőségű beolvasások

Az OCR pontossága drámaikusan csökken a homályos vagy alacsony kontrasztú beolvasásoknál. Mielőtt a képet az motorba adod, fontold meg az előfeldolgozást:

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### Nyelvtámogatás

Alapértelmezés szerint a motor angolt feltételez. Ahhoz, hogy **run OCR on PDF** más nyelven, állítsd be a nyelvkódot:

```python
ocr_engine.language = "spa"  # Spanish
```

Győződj meg róla, hogy a megfelelő nyelvi modell telepítve van.

## Teljes működő példa

Összeállítva minden elemet, itt egy önálló szkript, amelyet beilleszthetsz egy `ocr_pdf.py` nevű fájlba, és azonnal futtathatsz:

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

Futtasd így:

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

Láthatod a szöveget a konzolon, és ha megadtad a `-o` kapcsolót, egy kereshető PDF jelenik meg az eredeti fájl mellett.

## Pro tippek és legjobb gyakorlatok

- **Kötegelt feldolgozás:** Több tucat PDF kezelésekor csomagold be a fenti logikát egy ciklusba, és naplózd minden fájl sikerét/kudarcát.
- **Bizalmi szűrés:** Minden `page_result` tartalmaz egy bizalmi mutatót. Dobd el vagy jelöld meg a alacsony bizalomú oldalakat manuális felülvizsgálatra.
- **Párhuzamosság:** Ha a CPU-d több maggal rendelkezik, fontold meg a `concurrent.futures` használatát az oldalak párhuzamos feldolgozásához – csak ügyelj a memóriahasználatra.
- **Verzió rögzítés:** Az `aocr` API változhat. Rögzítsd a verziót a `requirements.txt`-ben (pl. `aocr==2.3.1`), hogy elkerüld a tör breaking változásokat.

## Összegzés

Áttekintettük, **hogyan használjuk az OCR-t** a **szöveg kinyeréséhez PDF-ből**, **OCR futtatását PDF-en**, **PDF képként betöltését**, és még a **beolvasott PDF konvertálását** kereshető formátumba. A kód teljes, a magyarázatok lefedik a *mit* és a *miért* is, és most már van egy újrahasználható minta minden olyan projekthez, amely képalapú PDF-ekkel dolgozik.

Mi a következő? Próbáld meg a kinyert szöveget egy természetes nyelvi csővezetékbe betáplálni, indexeld a kereshető PDF-eket Elasticsearch-szel, vagy kísérletezz különböző OCR háttérrendszerekkel, mint a Tesseract vagy az Azure Computer Vision. A lehetőségek végtelenek, és az eszközök a kezedben vannak.

Boldog kódolást, és legyenek a PDF-jeid mindig kereshetők! 

![OCR használatának példája](/images/ocr_workflow.png "OCR használata")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}