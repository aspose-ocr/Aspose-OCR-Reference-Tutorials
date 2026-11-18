---
category: general
date: 2026-04-29
description: Szöveg kinyerése PDF‑ből az Aspose OCR használatával Pythonban. Tanulja
  meg a kötegelt OCR PDF feldolgozást, a beolvasott PDF szöveg konvertálását, és az
  alacsony megbízhatóságú oldalak kezelését.
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: hu
og_description: Szöveg kinyerése PDF‑ből az Aspose OCR‑rel Pythonban. Ez az útmutató
  bemutatja a kötegelt OCR PDF‑feldolgozást, a beolvasott PDF‑szöveg konvertálását
  és az alacsony bizalomú eredmények kezelését.
og_title: Szöveg kinyerése PDF-ből – OCR PDF Python-nal
tags:
- OCR
- Python
- PDF processing
title: Szöveg kinyerése PDF-ből – OCR PDF Python-nal
url: /hu/python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szöveg kinyerése PDF-ből – OCR PDF Pythonban

Valaha szükséged volt **szöveg kinyerésére PDF-ből**, de a fájl csak egy beolvasott kép? Nem vagy egyedül – sok fejlesztő ütközik ebbe a falba, amikor a PDF-eket kereshető adatokká szeretnék alakítani. A jó hír? Az Aspose OCR for Python segítségével néhány sorban átalakíthatod a beolvasott PDF szövegét, és akár **csoportos OCR PDF feldolgozást** is futtathatsz, ha tucatnyi fájlt kell kezelned.

Ebben az útmutatóban végigvezetünk a teljes munkafolyamaton: a könyvtár beállítása, OCR futtatása egyetlen PDF-en, a folyamat skálázása csoportos feldolgozásra, valamint az alacsony bizalomú oldalakkal való foglalkozás, hogy tudd, mikor szükséges a kézi felülvizsgálat. A végére egy kész‑futtatható szkriptet kapsz, amely bármely beolvasott PDF-ből kinyeri a szöveget, és megérted az egyes lépések okát.

## Szükséged lesz

Mielőtt belemerülnénk, győződj meg róla, hogy rendelkezel:

- Python 3.8 vagy újabb (a kód f‑stringeket használ, így a 3.6+ működik, de a 3.8+ ajánlott)
- Aspose OCR for Python licenc vagy egy ingyenes próbaverzió kulcs (a Aspose weboldaláról szerezhető be)
- Egy mappa egy vagy több beolvasott PDF-fájllal, amelyet feldolgozni szeretnél
- Mérsékelt mennyiségű lemezterület a generált *.txt* jelentésekhez

Ennyi—nincs nehéz külső függőség, nincs OpenCV akrobácia. Az Aspose OCR motor elvégzi a nehéz munkát helyetted.

## A környezet beállítása

Először telepítsd az Aspose OCR csomagot a PyPI‑ról:

```bash
pip install aspose-ocr
```

Ha rendelkezel licencfájllal (`Aspose.OCR.lic`), helyezd a projekt gyökerébe, és aktiváld a következő módon:

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **Pro tipp:** Tartsd a licencfájlt a verziókezelésen kívül; add hozzá a `.gitignore`‑hoz, hogy elkerüld a véletlen kiszivárgást.

## OCR végrehajtása egyetlen PDF-en

Most vonjunk ki szöveget egyetlen beolvasott PDF-ből. A fő lépések a következők:

1. Hozz létre egy `OcrEngine` példányt.
2. Add meg a PDF fájlt.
3. Szerezd meg az `OcrResult`‑ot minden oldalhoz.
4. Írd a sima szöveges kimenetet a lemezre.
5. Felszabadítsd a motort a natív erőforrások felszabadításához.

Itt a teljes, futtatható szkript:

```python
# Step 1: Import the OCR engine and create an instance
from aspose.ocr import OcrEngine

# Optional: activate license (see previous section)
# from aspose.ocr import License
# License().set_license("Aspose.OCR.lic")

ocr_engine = OcrEngine()

# Step 2: Specify the PDF file to be processed
pdf_file_path = r"YOUR_DIRECTORY/input.pdf"

# Step 3: Extract OCR results – one OcrResult object per page
ocr_pages = ocr_engine.extract_from_pdf(pdf_file_path)

# Step 4: Iterate through the results, show confidence, flag low‑confidence pages, and save the plain text
for ocr_page in ocr_pages:
    print(f"Page {ocr_page.page_number}: confidence {ocr_page.confidence:.2%}")

    # If confidence is below 80 %, flag it for manual review
    if ocr_page.confidence < 0.80:
        print("  Low confidence – consider manual review")

    # Build the output filename
    output_txt = f"YOUR_DIRECTORY/Report_page{ocr_page.page_number}.txt"
    with open(output_txt, "w", encoding="utf-8") as f:
        f.write(ocr_page.text)

# Step 5: Release resources used by the engine
ocr_engine.dispose()
```

**Ami látható:** Minden oldalnál a szkript valami ilyesmit ír ki: `Page 1: confidence 97.45%`. Ha egy oldal a 80 % küszöb alá esik, figyelmeztetés jelenik meg, jelezve, hogy az OCR esetleg kihagyott karaktereket.

### Miért működik ez

- **`OcrEngine`** a natív Aspose OCR könyvtár kapuja; mindent kezel a képelőfeldolgozástól a karakterfelismerésig.
- **`extract_from_pdf`** automatikusan rasterizálja a PDF minden oldalát, így neked nem kell a PDF-et képekké konvertálni.
- **A bizalmi pontszámok** lehetővé teszik a minőség-ellenőrzés automatizálását – kritikus, ha jogi vagy orvosi dokumentumokat dolgozol fel, ahol a pontosság számít.

## Csoportos OCR PDF feldolgozás Pythonban

A legtöbb valós projekt több fájlt is érint. Bővítsük a egyfájlos szkriptet egy **csoportos OCR PDF feldolgozó** csővezetékké, amely bejár egy könyvtárat, feldolgozza minden PDF-et, és az eredményeket egy megfelelő alkönyvtárba menti.

```python
import os
from pathlib import Path
from aspose.ocr import OcrEngine

def ocr_pdf_file(pdf_path: Path, output_dir: Path, engine: OcrEngine, confidence_threshold: float = 0.80):
    """Extract text from a single PDF and write per‑page .txt files."""
    ocr_pages = engine.extract_from_pdf(str(pdf_path))
    for page in ocr_pages:
        print(f"{pdf_path.name} – Page {page.page_number}: {page.confidence:.2%}")
        if page.confidence < confidence_threshold:
            print("  ⚠️ Low confidence – manual review may be needed")

        out_file = output_dir / f"{pdf_path.stem}_page{page.page_number}.txt"
        out_file.write_text(page.text, encoding="utf-8")

def batch_ocr_pdf(input_folder: str, output_folder: str):
    """Iterate over all PDFs in input_folder and run OCR."""
    engine = OcrEngine()
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(parents=True, exist_ok=True)

    pdf_files = list(input_path.glob("*.pdf"))
    if not pdf_files:
        print("🚫 No PDF files found in the specified folder.")
        return

    for pdf_file in pdf_files:
        # Create a sub‑folder for each PDF to keep pages organized
        pdf_out_dir = output_path / pdf_file.stem
        pdf_out_dir.mkdir(exist_ok=True)
        ocr_pdf_file(pdf_file, pdf_out_dir, engine)

    # Clean up native resources
    engine.dispose()
    print("✅ Batch OCR completed.")

# Example usage:
if __name__ == "__main__":
    batch_ocr_pdf("YOUR_DIRECTORY/input_pdfs", "YOUR_DIRECTORY/ocr_output")
```

#### Hogyan segít ez

- **Skálázhatóság:** A függvény egyszer bejárja a mappát, minden PDF-hez létrehoz egy dedikált kimeneti alkönyvtárat. Ez rendezetten tartja a dolgokat, ha tucatnyi dokumentumod van.
- **Újrahasználhatóság:** A `ocr_pdf_file` más szkriptekből (pl. egy webszolgáltatásból) is meghívható, mivel tiszta függvény.
- **Hibakezelés:** A szkript barátságos üzenetet ír ki, ha a bemeneti mappa üres, így elkerülve a csendes hibát.

## Beolvasott PDF szöveg konvertálása – Szélsőséges esetek kezelése

Bár a fenti kód a legtöbb PDF-re működik, előfordulhatnak néhány furcsaságok:

| Helyzet | Miért fordul elő | Hogyan lehet enyhíteni |
|-----------|----------------|-----------------|
| **Titkosított PDF-ek** | A PDF jelszóval védett. | Add meg a jelszót a `extract_from_pdf(pdf_path, password="yourPwd")` hívásban. |
| **Többnyelvű dokumentumok** | Az Aspose OCR alapértelmezés szerint angol. | Állítsd be `ocr_engine.language = "spa"` spanyolhoz, vagy adj meg egy listát vegyes nyelvekhez. |
| **Nagyon nagy PDF-ek (>500 oldal)** | A memóriahasználat megugrik, mivel minden oldal RAM-ba töltődik. | A PDF-et darabokban dolgozd fel a `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` használatával, és ismételd a ciklust. |
| **Rossz minőségű beolvasás** | Alacsony DPI vagy erős zaj csökkenti a bizalmat. | Előfeldolgozd a PDF-et a `engine.image_preprocessing = True` beállítással, vagy növeld a DPI-t a `engine.dpi = 300` segítségével. |

> **Figyelem:** A képelőfeldolgozás bekapcsolása jelentősen növelheti a CPU időt. Ha éjszakai batch-et futtatsz, ütemezz elegendő időt, vagy indíts egy külön munkavégzőt.

## A kimenet ellenőrzése

A szkript befejezése után egy ilyen mappaszerkezetet találsz:

```
ocr_output/
├─ invoice_2023/
│  ├─ invoice_2023_page1.txt
│  ├─ invoice_2023_page2.txt
│  └─ …
└─ contract_A/
   ├─ contract_A_page1.txt
   └─ …
```

Nyiss meg egy `.txt` fájlt; tiszta, UTF‑8 kódolású szöveget kell látnod, amely tükrözi az eredeti beolvasott tartalmat. Ha torz karaktereket látsz, ellenőrizd a PDF nyelvi beállításait, és győződj meg róla, hogy a megfelelő betűkészletek telepítve vannak a gépen.

## Erőforrások tisztítása

Az Aspose OCR natív DLL-ekre támaszkodik, ezért elengedhetetlen a `engine.dispose()` meghívása a munka befejezése után. Ennek elhagyása memória szivárgáshoz vezethet, különösen hosszú ideig futó batch feladatoknál.

```python
# Always the last line of your script
engine.dispose()
```

## Teljes vég‑től‑végig példa

Mindent összevonva, itt egy egyetlen

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}