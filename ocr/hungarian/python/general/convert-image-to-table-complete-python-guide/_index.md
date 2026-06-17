---
category: general
date: 2026-03-26
description: Kép átalakítása táblázattá Python segítségével OCR-rel és AI-val. Tanulja
  meg, hogyan lehet táblázatot kinyerni a képből, javítani az OCR pontosságát, és
  gyorsan strukturált eredményeket kapni.
draft: false
keywords:
- convert image to table
- extract table from image
- extract tabular data image
- enhance OCR accuracy
language: hu
og_description: Kép átalakítása táblázattá Pythonban. Ez az útmutató bemutatja, hogyan
  lehet táblázatot kinyerni a képből, növelni az OCR pontosságát, és strukturált adatokkal
  dolgozni.
og_title: Kép átalakítása táblázattá – Lépésről lépésre Python útmutató
tags:
- OCR
- Python
- AI post‑processing
title: Kép konvertálása táblázattá – Teljes Python útmutató
url: /hu/python/general/convert-image-to-table-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert image to table – Teljes Python útmutató

Valaha is szükséged volt **convert image to table**-ra, de elakadtál egy homályos képernyőképnél? Nem vagy egyedül. Sok adat‑központú projektben a leggyorsabb módja a számok dataframe‑be juttatásának, ha lefotózod a nyomtatott táblázatot, és egy script végzi a nehéz munkát. A jó hír? Egy modern OCR motorral és egy apró AI post‑processzorral szinte bármely képből ki tudsz nyerni egy tiszta, strukturált táblázatot.

Ebben az útmutatóban egy **real‑world example that extracts tabular data image**-t fogunk végigjárni, megtisztítjuk, és minden sort egyszerű szövegként kiírjuk. A végére megérted, hogyan **enhance OCR accuracy**, kezelheted a gyakori buktatókat, és hogyan igazíthatod a kódot a saját folyamatodhoz. Nincs varázslat, csak Python, néhány könyvtár, és egy kis gondolkodás.

> **Szükséged lesz**  
> * Python 3.9+  
> * Egy OCR könyvtár, amely támogatja a `OutputFormat.Structured`-t (pl. `myocr`)  
> * Egy opcionális AI post‑processor (lehet egy könnyű transformer vagy szabály‑alapú függvény)  
> * Egy minta kép fájl (`table.png`), amely egy egyszerű táblázatot tartalmaz

---

## 1. lépés: Convert image to table – Kép felismerése strukturált kimenettel

Az első dolog, amit teszünk, hogy a képet betápláljuk az OCR motorba, és **structured** eredményt kérünk. A strukturált kimenet azt jelenti, hogy a motor megpróbálja meghatározni a sorokat, oszlopokat és cellahatárokat ahelyett, hogy egy egyszerű szöveget adna vissza.

```python
import myocr as ocr          # Hypothetical OCR package
import myengine as engine    # Wrapper around the OCR engine
import myai as ai            # Simple AI post‑processor

def recognize_image(path: str):
    """
    Sends the image to the OCR engine and asks for a tabular
    (structured) representation.
    """
    # Step 1: Recognize the image and request a structured (tabular) result
    structured_result = engine.recognize_image(
        path,
        output_format=ocr.OutputFormat.Structured
    )
    return structured_result
```

**Miért fontos ez:**  
Ha a OCR-t egyszerű szövegért kérdezed, egy karakterrengeteget kapsz, amely nem ismeri a sorokat vagy oszlopokat. Strukturált formátum kérése esetén a motor elvégzi a sorok detektálását, oszlopok igazítását, és még az alapvető cella egyesítéseket is. Ez drámaian csökkenti a későbbi manuális feldolgozás mennyiségét.

> **Pro tipp:** Győződj meg róla, hogy a kép jó kontraszttal és minimális ferdeséggel rendelkezik. Egy 300 dpi-s beolvasás általában a legjobb eredményt adja.

---

## 2. lépés: Enhance OCR accuracy – Nyers struktúra post‑processzálása

Az OCR nem tökéletes – különösen, ha a forráskép halvány vonalakat vagy szokatlan betűtípusokat tartalmaz. Itt jön képbe egy könnyű AI (vagy akár egy szabály‑alapú script), amely megtisztítja a kimenetet, kijavítja a gyakori félreolvasásokat, és hozzáadja a hiányzó kontextust.

```python
def enhance_structure(structured_result):
    """
    Runs a post‑processor that fixes typical OCR errors
    (e.g., 'O' vs '0', merged cells) and adds semantic context.
    """
    # Step 2: Enhance the raw OCR structure with AI (adds context, corrects errors)
    enhanced_structure = ai.run_postprocessor(structured_result)
    return enhanced_structure
```

**Miért fontos ez:**  
Egy nyers OCR táblázat fejlécként „Q1 2022”-t jelölhet, de a „1”-et „l”-ként olvassa. Az AI réteg egy kis tanuló adathalmazból megtanulhatja ezeket a mintákat, és tisztább táblázatot ad ki. Még egy egyszerű heurisztika (az egyedülálló „l” cseréje „1”-re, ha számok között van) drámaian növelheti az **enhance OCR accuracy**-t.

> **Gyakori szélhelyzet:** Ha a táblázat egyesített cellákat tartalmaz, az OCR megduplázhatja a tartalmat az oszlopokban. A post‑processornek fel kell ismernie az azonos szomszédos cellákat, és össze kell vonnia őket.

---

## 3. lépés: Extract tabular data image – Sorok iterálása és cella szöveg megjelenítése

Most, hogy van egy rendezett struktúránk, az adatok kinyerése egyszerű. Végig fogunk iterálni az első észlelt táblán, és minden sort a cellaértékek listájaként kiírjuk.

```python
def print_table(enhanced_structure):
    """
    Prints each row of the first detected table.
    """
    # Step 3: Iterate over the rows of the first detected table and display cell text
    for row in enhanced_structure.tables[0].rows:
        print([cell.text for cell in row.cells])

if __name__ == "__main__":
    # Path to your image file
    image_path = "YOUR_DIRECTORY/table.png"

    # Run the pipeline
    raw = recognize_image(image_path)
    cleaned = enhance_structure(raw)
    print_table(cleaned)
```

**Ami megjelenik:**  
Feltételezve, hogy a `table.png` egy egyszerű 3 × 2-es rácsot tartalmaz, a kimenet így nézhet ki:

```
['Product', 'Price']
['Apple', '$1.20']
['Banana', '$0.80']
```

Ha az OCR kihagy egy fejléct, az AI post‑processor valószínűleg a környező kontextus alapján beilleszti, így a végső táblázat készen áll a pandas vagy bármely további elemzés számára.

> **Vigyázz:** Üres sorok a táblázat végén. Néhány OCR motor üres sort ad hozzá, amikor whitespace-t talál. Egy gyors `if any(cell.text for cell in row.cells):` ellenőrzés kiszűrheti ezeket.

---

## Bónusz: Going beyond – Táblázat mentése CSV‑be vagy DataFrame‑be

A legtöbb valós munkafolyamatnak CSV fájlra vagy pandas DataFrame‑re van szüksége. Itt egy apró kódrészlet, amely a kiírt sorokat CSV‑vé alakítja anélkül, hogy elhagyná a Python folyamatot.

```python
import csv
import pandas as pd

def save_to_csv(enhanced_structure, output_path="output.csv"):
    rows = [
        [cell.text for cell in row.cells]
        for row in enhanced_structure.tables[0].rows
        if any(cell.text for cell in row.cells)  # Skip empty rows
    ]
    # Write CSV
    with open(output_path, "w", newline="", encoding="utf-8") as f:
        writer = csv.writer(f)
        writer.writerows(rows)

    # Also return a DataFrame for immediate use
    return pd.DataFrame(rows[1:], columns=rows[0])  # Assume first row is header

# Example usage:
df = save_to_csv(cleaned, "my_table.csv")
print(df.head())
```

Most már van egy használatra kész DataFrame‑ed, tökéletes elemzéshez, vizualizációhoz vagy gépi tanulási modellbe való betápláláshoz.

---

## Gyakran Ismételt Kérdések (FAQ)

**Q: Működik ez a beolvasott táblázatokat tartalmazó PDF‑ekkel?**  
A: Teljesen – csak minden PDF oldalt konvertáld képpé (pl. a `pdf2image` használatával), és a kapott PNG‑ket add a pipeline‑hoz.

**Q: A táblázatom egyesített fejléccellákat tartalmaz; az AI javítja?**  
A: Egy jól betanított post‑processor képes felismerni az egyesített cellákat a cella‑spánok ellenőrzésével. Ha szabály‑alapú megközelítést használsz, keresd az azonos szöveget a szomszédos cellákban és vondd össze őket.

**Q: Mi van, ha az OCR több táblázatot ad vissza?**  
A: `enhanced_structure.tables` egy lista. Iterálhatsz rajta, vagy kiválaszthatod azt, amelyik a legtöbb sorral/oszloppal rendelkezik – attól függően, mi a várakozásod.

**Q: Lecserélhetem az AI post‑processzort egy egyszerű regex tisztításra?**  
A: Igen. Sok projektnél néhány regex helyettesítés (pl. “O” → “0”) elegendő. A lényeg, hogy valamit futtass az OCR után, hogy javítsd az **enhance OCR accuracy**-t.

---

## Összegzés

Most mutattuk be, hogyan **convert image to table** Pythonban, a nyers OCR felismeréstől egy AI‑javított, használatra kész adatstruktúráig. A háromlépéses pipeline – felismerés, javítás, kinyerés – lefedi a **extract table from image** alapvető kihívásait, és gyakorlati módszereket mutat be az **enhance OCR accuracy** javítására.

Készíts egy képernyőképet bármely táblázatról, irányítsd rá a scriptet, és néhány másodperc alatt lesz egy CSV vagy DataFrame. Innen tovább felfedezhetsz fejlettebb trükköket: többoldalas PDF‑ek, kézírásos táblázatok, vagy akár valós‑idő kamera feedek.

Készen állsz a következő kihívásra? Próbáld meg a pipeline‑t élő videókeretekkel táplálni, vagy kísérletezz nyelvi modell‑alapú post‑processzorokkal, amelyek hiányzó oszlopneveket tudnak kitalálni. A határ a csillagos ég, és most már van egy szilárd alapod a további fejlesztéshez.

Boldog kódolást! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}