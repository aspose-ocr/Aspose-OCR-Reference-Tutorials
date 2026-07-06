---
category: general
date: 2026-01-02
description: Táblázat kinyerése dokumentumból Python segítségével. Tanulja meg, hogyan
  olvassa be a táblázatokat PDF-ből, és hogyan iteráljon a sorokon egy tiszta, újrahasználható
  megoldással.
draft: false
keywords:
- extract table from document
- how to read tables from pdf
- how to iterate table rows
- pdf table extraction python
- document layout detection
language: hu
og_description: Táblázat kinyerése dokumentumból Pythonban. Ez az útmutató bemutatja,
  hogyan olvassunk be táblázatokat PDF-ből, és hogyan iteráljunk a táblázatsorokon
  egy megbízható motorral.
og_title: Táblázat kinyerése dokumentumból – Teljes Python oktató
tags:
- Python
- PDF
- Data Extraction
title: Táblázat kinyerése dokumentumból – Lépésről lépésre Python útmutató
url: /hu/python/general/extract-table-from-document-step-by-step-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract table from document – Teljes Python útmutató

Valaha szükséged volt **extract table from document**-ra, de nem tudtad, hol kezdjed? Nem vagy egyedül — sok fejlesztő ütközik ugyanabba a falba, amikor PDF-ekkel dolgozik, amelyek táblázatokban rejtenek adatokat. Ebben az útmutatóban egy gyakorlati, vég‑től‑végig megoldást mutatunk be, amely nem csak **how to read tables from pdf** fájlok olvasását mutatja be, hanem **how to iterate table rows**-t is, így az adatokat bárhová továbbíthatod.

Képzeld el, hogy van egy sor számla, mindegyik egy összegző táblázattal a tételekről. Ezeket a sorokat CSV‑be szeretnéd exportálni a későbbi elemzésekhez. A végére egy újrahasználható kódrészletet kapsz, amely pontosan ezt megteszi, plusz néhány tippet a gyakori buktatók elkerüléséhez.

## Mit fogsz megtanulni

- Dokumentum elrendezésének felismerése egy layout motorral.  
- A nyers felismerés finomítása egy post‑processzorral a tisztább táblázatszerkezetért.  
- A felismerett táblázat minden sorának bejárása és a cellaértékek kiírása (vagy tárolása).  

Nincs külső szolgáltatás, nincs varázslatos fekete doboz — csak tiszta Python és egy népszerű OCR/layout könyvtár (pl. **pdfplumber**, **pdfminer.six**, vagy egy már meglévő `engine`, amelyet használsz). Ha már rendelkezel egy `engine` objektummal, amely implementálja a `recognize_layout()` és a `run_postprocessor()` metódusokat, akkor a kódot közvetlenül beillesztheted.

> **Pro tip:** Ha kereskedelmi SDK‑t használsz, győződj meg róla, hogy engedélyezted a „table detection” funkciót; különben a nyers layout kihagyhat egyes egyesített cellákat.

---

## 1. lépés: A táblázat struktúrájának felismerése – Extract table from document

Az első dolog, amire szükséged van, egy nyers layout, amely megmutatja, hol helyezkednek el a táblázatok az oldalon. A legtöbb modern PDF‑könyvtár kínál egy olyan metódust, mint a `recognize_layout()`, amely egy hierarchikus blokk‑, sor‑ és cellastruktúrát ad vissza.

```python
# Step 1 – Detect the document layout using the engine
# ---------------------------------------------------
# `engine` is assumed to be an instantiated object from your PDF library.
# It could be pdfplumber, a custom OCR SDK, or any tool that supports layout detection.
raw_layout = engine.recognize_layout()
```

**Miért fontos:**  
A nyers layout koordinátákat ad minden szövegelemhez, de gyakran tartalmaz zajt — fejlécet, láblécet vagy eltévedt karaktereket, amelyek nem részei a táblázatnak. Ezért a következő lépés kulcsfontosságú.

> **Gyakori kérdés:** *Mi van, ha a PDF‑nek több oldala van?*  
> A `recognize_layout()` hívás általában egy oldalkészletet ad vissza. Iterálj rajtuk, és alkalmazd ugyanazt a post‑processzáló logikát minden oldalra.

---

## 2. lépés: A felismerés finomítása – How to read tables from pdf

Miután megvan a `raw_layout`, tisztítani kell. A legtöbb motor szállít egy post‑processzort, amely egyesíti a széttördelt cellákat, eltávolítja a nem releváns szöveget, és egy megfelelő `Table` objektumot épít.

```python
# Step 2 – Refine the detected layout with the post‑processor
# ----------------------------------------------------------
# The post‑processor returns an enhanced layout where tables are
# represented as a list of rows, each row being a list of Cell objects.
enhanced_layout = engine.run_postprocessor(raw_layout)
```

**Miért van erre szükséged:**  
A nyers layout egyetlen táblázatsort akár tucatnyi apró fragmentumként is jelenthet. A post‑processzor ezeket a fragmentumokat logikai cellákká csoportosítja, így a későbbi bejárás egyszerűvé válik.

> **Szélsőséges eset:** Egyes PDF‑ek láthatatlan szegélyeket használnak. Ha hiányzó sorokat észlelsz, engedélyezd a „detect invisible lines” kapcsolót a motorodban (ha elérhető).

---

## 3. lépés: Táblázatsorok bejárása – How to iterate table rows

Most, hogy van egy tiszta `enhanced_layout`, az adatok kinyerése gyerekjáték. Az alábbiakban minden sort végigjárunk, a cellák szövegét tabulátorral (`\t`) fűzzük össze (így a kimenet szépen igazodik), és kiírjuk az eredményt. A `print` helyett bármilyen tárolási logikát használhatsz — CSV‑író, adatbázis‑insert, stb.

```python
# Step 3 – Print the table contents row by row
# --------------------------------------------
# `enhanced_layout.table` is expected to be an iterable of rows.
# Each `row` is a list of Cell objects with a `.text` attribute.
for row in enhanced_layout.table:
    # Join each cell's text with a tab to align columns
    print("\t".join(cell.text for cell in row))
```

**Várható kimenet (példa):**

```
Item	Qty	Price	Total
Widget A	2	$10.00	$20.00
Widget B	1	$15.00	$15.00
Service C	5	$8.00	$40.00
```

Ha CSV‑t szeretnél a tabulátoros nézet helyett, egyszerűen cseréld le a `"\t".join(...)` részt `",".join(...)`‑ra, és írd ki egy fájlba.

---

## Teljes működő példa

Összeállítva, itt egy önálló szkript. Igazítsd az importot és a motor inicializálását a használt könyvtáradhoz.

```python
# --------------------------------------------------------------
# Full script: extract table from document and iterate rows
# --------------------------------------------------------------
import sys

# -----------------------------------------------------------------
# 1️⃣  Import or instantiate your PDF layout engine.
# Replace the placeholder with the actual library you use.
# -----------------------------------------------------------------
# Example with a fictional `pdf_engine` package:
# from pdf_engine import LayoutEngine
# engine = LayoutEngine(api_key="YOUR_KEY")
# -----------------------------------------------------------------
# For pdfplumber (open‑source) you could do:
# import pdfplumber
# engine = pdfplumber.open("sample.pdf")
# -----------------------------------------------------------------
# We'll keep it generic for the tutorial.
# -----------------------------------------------------------------

def extract_table(engine):
    """
    Detect, refine, and iterate over a table in a PDF document.
    Returns a list of rows, where each row is a list of cell strings.
    """
    # Detect layout
    raw_layout = engine.recognize_layout()

    # Refine layout
    enhanced_layout = engine.run_postprocessor(raw_layout)

    # Collect rows
    rows = []
    for row in enhanced_layout.table:
        rows.append([cell.text for cell in row])
    return rows

def main(pdf_path):
    # Initialise your engine – this will differ per library
    # Below is a stub; replace with real initialization.
    engine = initialize_engine(pdf_path)   # <-- implement this

    try:
        table_rows = extract_table(engine)
        for row in table_rows:
            print("\t".join(row))
    except Exception as e:
        print(f"❌ Extraction failed: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python extract_table.py <path-to-pdf>")
    else:
        main(sys.argv[1])
```

**Mit kell cserélni:**

- `initialize_engine(pdf_path)`: Hozd létre a motor példányát a választott könyvtárhoz.  
- `engine.recognize_layout()` / `engine.run_postprocessor()`: Használd a megfelelő metódusneveket, ha eltérnek.

A szkript futtatása `python extract_table.py invoice.pdf` paranccsal egy szépen tabulátorral elválasztott táblázatot ír ki, készen állva a további feldolgozásra.

---

## Képi illusztráció

Alább egy gyors vázlat arról, hogy néz ki a felismerési folyamat.  
![extract table from document diagram showing raw layout → post‑processor → clean table]  

*Alt szöveg:* *extract table from document flow diagram*  

---

## Gyakran Ismételt Kérdések & Szélsőséges Esetek

| Kérdés | Válasz |
|----------|--------|
| **Mi van, ha a PDF‑nek több táblázata van?** | `enhanced_layout.table` csak az első felismerett táblázatot tartalmazhatja. Iterálj a `enhanced_layout.tables` (vesszővel) listán, ha a könyvtár támogatja, és alkalmazd ugyanazt a sor‑bejáró logikát mindegyikre. |
| **Hogyan kezelem az egyesített cellákat?** | A post‑processzor általában szétbontja az egyesített cellákat külön bejegyzésekké. Ha nem, ellenőrizd a motor `merge_cells` kapcsolóját, vagy manuálisan fűzd össze a szomszédos cellákat a koordinátáik alapján. |
| **Kinyerhetők a táblázatok szkennelt PDF‑ekből?** | Igen, de ehhez OCR lépés szükséges a layout felismerése előtt. Sok SDK egy hívásban kombinálja az OCR‑t és a layout felismerést (`recognize_layout()` egy szkennelt dokumentumon). |
| **Teljesítményproblémák nagy kötegek esetén?** | Oldalak párhuzamos feldolgozása (pl. `concurrent.futures` használatával). Az OCR a legnehezebb rész; tartsd életben a motor példányt a fájlok között, hogy ne kelljen újra betölteni a nehéz modelleket. |
| **Szükség van extra függőségek telepítésére?** | Ha a `pdfplumber`‑t használod, telepítsd `pip install pdfplumber`‑rel. Kereskedelmi SDK‑k esetén kövesd a gyártó telepítési útmutatóját. |

---

## Összegzés

Most már tudod, hogyan **extract table from document** a layout felismerésével, annak finomításával, majd a **iterating table rows** segítségével tiszta, felhasználható adatokat nyerni. Akár adatraktárba, jelentéskészítésbe vagy egyszerű PDF‑CSV konverzióba szeretnéd az adatokat, a minta mindig ugyanaz: felismer → tisztít → bejár.

Következő lépések, amelyeket érdemes felfedezni:

- **How to read tables from pdf** további stílusinformációkkal (betűtípusok, színek).  
- Exportálás közvetlenül **pandas DataFrames**‑be elemzéshez.  
- Ugyanazon pipeline használata **táblázatok visszaírásához** új PDF‑be (fordított folyamat).  

Próbáld ki a szkriptet néhány saját PDF‑eddel, és nézd meg, milyen gyorsan tudsz statikus táblázatokat cselekvő adatokká alakítani. Jó kinyerést!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}