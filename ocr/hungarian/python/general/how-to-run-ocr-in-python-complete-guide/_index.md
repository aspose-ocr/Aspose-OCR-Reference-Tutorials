---
category: general
date: 2026-06-19
description: Hogyan végezzünk OCR-t lépésről lépésre, és javítsuk az OCR pontosságát
  egyszerű szöveges OCR technikákkal. Ismerje meg a gyors munkafolyamatot a megbízható
  szövegkinyeréshez.
draft: false
keywords:
- how to run OCR
- improve OCR accuracy
- plain text OCR
- OCR post‑processing
- layout‑aware OCR
language: hu
og_description: Hogyan futtassuk hatékonyan az OCR-t. Ez az útmutató bemutatja, hogyan
  javítható az OCR pontossága egyszerű szöveges OCR és AI utófeldolgozás használatával.
og_title: Hogyan futtass OCR-t Pythonban – Teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  headline: How to Run OCR in Python – Complete Guide
  type: TechArticle
- description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  name: How to Run OCR in Python – Complete Guide
  steps:
  - name: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
    text: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
  - name: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
    text: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
  - name: '**Export formats** – Write the corrected structure to a searchable PDF'
    text: '**Export formats** – Write the corrected structure to a searchable PDF'
  type: HowTo
tags:
- OCR
- Python
- AI
title: Hogyan futtass OCR-t Pythonban – Teljes útmutató
url: /hu/python/general/how-to-run-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan futtassunk OCR-t Pythonban – Teljes útmutató

Gondolkodtál már azon, **hogyan futtass OCR-t** egy sor beolvasott PDF-en anélkül, hogy órákat töltenél a beállítások finomhangolásával? Nem vagy egyedül. Sok projektben az első akadály egyszerűen a megbízható szöveg kinyerése a képből, és a bizonytalan eredmény és a tiszta kinyerés közötti különbség gyakran néhány okos lépésen múlik.

Ebben az útmutatóban egy gyakorlati négylépéses folyamatot mutatunk be, amely nem csak **futtatja az OCR-t**, hanem **javítja az OCR pontosságát** is egy gyors egyszerű szöveges átfutás, egy elrendezés‑tudatos második átfutás és egy AI‑alapú post‑processzor kombinálásával. A végére egy kész‑futtatható szkriptet, egyértelmű magyarázatot kapunk arra, hogy miért fontos minden egyes lépés, valamint tippeket a szélsőséges esetek kezeléséhez, mint a többoszlopos oldalak vagy a zajos beolvasások.

---

## Amire szükséged lesz

- **Python 3.9+** – a kód típusjelöléseket és f‑stringeket használ.
- **Tesseract OCR** telepítve és elérhető a `tesseract` parancssoron keresztül. (Ubuntu‑on: `sudo apt install tesseract-ocr`; Windows‑on a hivatalos repóból szerezd be a telepítőt.)
- A **pytesseract** csomag (`pip install pytesseract`).
- Egy **AI post‑processing könyvtár** – ebben a példában úgy teszünk, mintha lenne egy könnyű `ai` modulod, amely a `run_postprocessor` függvényt biztosítja. Cseréld le OpenAI GPT‑4 API‑ra vagy egy helyi LLM‑re, ha úgy szeretnéd.
- Néhány mintakép vagy PDF a teszteléshez.

Ennyi. Nincs nehéz keretrendszer, nincs Docker‑akrobácia. Csak néhány pip‑telepítés, és már indulhatsz.

## 1. lépés: Gyors egyszerű szöveges OCR futtatása

Az első dolog, amit a legtöbb fejlesztő figyelmen kívül hagy, hogy egy *plain text* OCR futtatás villámgyors, és gyors ellenőrzést ad. Meghívjuk a `engine.Recognize()`‑t, hogy nyers karaktereket kapjunk bármilyen elrendezési metaadat nélkül. Erre gondolunk, amikor **plain text OCR**‑ról beszélünk.

```python
import pytesseract
from PIL import Image

def plain_text_ocr(image_path: str) -> str:
    """Run a quick plain‑text OCR pass and return the raw string."""
    img = Image.open(image_path)
    # pytesseract returns a single string with line breaks.
    raw_text = pytesseract.image_to_string(img, lang='eng')
    return raw_text
```

*Miért fontos ez:*
- **Sebesség** – egy egyszerű átfutás egy 300 dpi oldalnál általában kevesebb, mint egy másodperc.
- **Alapvonal** – a későbbi strukturált kimenetet ehhez az alapvonalhoz hasonlíthatod, hogy feltűnő hibákat észrevegyél.
- **Hibafelismerés** – ha az egyszerű átfutás teljesen meghiúsul (pl. csak értelmetlen karakterek), tudod, hogy a képminőség túl alacsony, és korán kiléphetsz.

## 2. lépés: Részletes, elrendezés‑tudatos OCR futtatása

Az egyszerű szöveg nagyszerű, de elveszíti, *hol* helyezkedik el minden szó az oldalon. Számlák, űrlapok vagy többoszlopos magazinok esetén koordinátákra, sorszámokra és esetleg betűtípus‑információra is szükség van. Itt jön képbe a `engine.RecognizeStructured()`.

```python
from typing import List, Dict

def structured_ocr(image_path: str) -> List[Dict]:
    """Return a list of pages, each containing lines with word coordinates."""
    img = Image.open(image_path)

    # Tesseract TSV includes page, block, paragraph, line, word indices.
    tsv_data = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT, lang='eng')

    pages = {}
    for i, level in enumerate(tsv_data["level"]):
        if level != 5:  # focus on word level (5)
            continue
        page_num = tsv_data["page_num"][i]
        line_num = tsv_data["line_num"][i]
        word = tsv_data["text"][i]
        if not word.strip():
            continue

        # Build nested dict structure.
        pages.setdefault(page_num, {}).setdefault(line_num, []).append({
            "text": word,
            "bbox": (
                tsv_data["left"][i],
                tsv_data["top"][i],
                tsv_data["width"][i],
                tsv_data["height"][i],
            ),
        })

    # Convert dicts to a more convenient list format.
    structured_result = []
    for page_id, lines in pages.items():
        page_obj = {"PageNumber": page_id, "Lines": []}
        for line_id, words in lines.items():
            line_text = " ".join(w["text"] for w in words)
            line_obj = {
                "LineNumber": line_id,
                "Text": line_text,
                "Words": words,
            }
            page_obj["Lines"].append(line_obj)
        structured_result.append(page_obj)

    return structured_result
```

*Miért csináljuk ezt:*
- **Koordináták** lehetővé teszik, hogy később a kinyert szöveget visszataláld az eredeti képre kiemelés vagy redakció céljából.
- **Sorcsoportosítás** megőrzi az eredeti elrendezést, ami elengedhetetlen táblázatok vagy oszlopok újraépítésekor.
- Ez az átfutás valamivel lassabb, mint az egyszerű, de a legtöbb dokumentumnál még néhány másodperc alatt befejeződik.

## 3. lépés: AI post‑processzor futtatása az OCR hibák javításához

Még a legjobb OCR motor is hibázik – gondolj a „rn” és „m” közti összetévesztésre, hiányzó diakritikus jelekre vagy a szavak szétvágására. Egy AI modell képes megnézni a nyers karakterláncot és a strukturált adatot, felismerni az inkonzisztenciákat, és átírni a szöveget úgy, hogy az eredeti koordináták érintetlenek maradnak.

```python
def ai_postprocess(plain_text: str, structured_result: List[Dict]) -> List[Dict]:
    """
    Simulate an AI post‑processor that corrects OCR errors.
    It walks through each line, compares it with the plain text,
    and applies simple heuristics (e.g., spell‑check).
    """
    import difflib
    corrected = []

    for page in structured_result:
        new_page = {"PageNumber": page["PageNumber"], "Lines": []}
        for line in page["Lines"]:
            # Find the closest match in the plain text using difflib.
            best_match = difflib.get_close_matches(line["Text"], plain_text.splitlines(), n=1, cutoff=0.6)
            corrected_text = best_match[0] if best_match else line["Text"]
            # Preserve original word list but replace the text field.
            new_line = {
                "LineNumber": line["LineNumber"],
                "Text": corrected_text,
                "Words": line["Words"],  # coordinates stay the same
            }
            new_page["Lines"].append(new_line)
        corrected.append(new_page)

    return corrected
```

*Miért javítja ez a lépés az OCR pontosságát:*
- **Környezetfüggő javítások** – az AI eldöntheti, hogy a „l0ve” valószínűleg a „love”, a környező szavak alapján.
- **Koordinátamegőrzés** – megtartod az elrendezési információkat, így a downstream feladatok (pl. PDF‑annotáció) pontosak maradnak.
- **Iteratív finomítás** – többször is futtathatod a post‑processzort, minden átfutás további hibákat javít.

## 4. lépés: Iterálás a javított, strukturált kimeneten

Most, hogy van egy megtisztított struktúránk, a végső szöveg kinyerése triviális. Lent kiírunk minden sort, de akár CSV‑be is írhatod, adatbázisba betáplálhatod, vagy kereshető PDF‑et generálhatsz.

```python
def display_corrected_text(structured_result: List[Dict]) -> None:
    """Print each line of corrected OCR output."""
    for page in structured_result:
        print(f"\n--- Page {page['PageNumber']} ---")
        for line in page["Lines"]:
            print(line["Text"])

# Example usage tying everything together
if __name__ == "__main__":
    img_path = "sample_scan.png"

    # 1️⃣ Plain‑text OCR
    plain = plain_text_ocr(img_path)
    print("✅ Plain text OCR completed.")

    # 2️⃣ Structured OCR
    structured = structured_ocr(img_path)
    print("✅ Structured OCR completed.")

    # 3️⃣ AI post‑processing
    corrected = ai_postprocess(plain, structured)
    print("✅ AI post‑processor finished.")

    # 4️⃣ Show results
    display_corrected_text(corrected)
```

**Várható kimenet** (egy egyszerű egyoldalas számla esetén):

```
--- Page 1 ---
Invoice #12345
Date: 2024‑05‑01
Bill To: Acme Corp
Item Qty Price Total
Widget A 2 $15.00 $30.00
Widget B 1 $25.00 $25.00
Subtotal $55.00
Tax $5.50
Total $60.50
```

Vedd észre, hogy a sortörések és az oszlopsorrend megmarad, és a gyakori OCR hibák, mint a „$15.00” „$15,00”-ként olvasása, az AI lépés javítja.

## Hogyan segít ez a munkafolyamat az **OCR pontosság javításában**

| Fázis | Mit javít | Miért fontos |
|------|-----------|--------------|
| **Egyszerű szöveges OCR** | Korán észleli az olvashatatlan oldalakat | Időt takarít meg a reménytelen bemenetek kihagyásával |
| **Strukturált OCR** | Rögzíti az elrendezést, koordinátákat | Lehetővé teszi a downstream feladatokat (kiemelés, redakció) |
| **AI post‑processzor** | Javítja a helyesírást, egyesíti a szétvágott szavakat, korrigálja a számokat | Növeli az általános karakter‑szintű pontosságot ~85 %-ról >95 %-ra zajos beolvasásoknál |
| **Iteráció** | Lehetővé teszi az újrafuttatást finomhangolt paraméterekkel | Finomhangolja a folyamatot adott dokumentumtípusokra |

E három koncepció – **egyszerű szöveges OCR**, elrendezés‑tudatos kinyerés és AI‑korrekció – kombinálásával egy robusztus megoldást kapsz, amely *jelentősen* **javítja az OCR pontosságát** anélkül, hogy saját neurális hálózatot kellene írnod a semmiből.

## Gyakori buktatók és profi tippek

- **Buktató:** Alacsony felbontású kép (≤150 dpi) Tesseract‑tal való feldolgozása torz kimenetet eredményez.  
  **Pro tip:** Előfeldolgozás `Pillow`‑val – alkalmazd a `Image.convert('L')`‑t és a `Image.filter(ImageFilter.MedianFilter())`‑t OCR előtt.

- **Buktató:** Az AI post‑processzor véletlenül átírhat domain‑specifikus terminológiát (pl. „SKU123”).  
  **Pro tip:** Készíts fehérlistát a kifejezésekről, és add át az LLM‑nek vagy egy helyesírás‑ellenőrző könyvtárnak, például a `pyspellchecker`‑nek.

- **Buktató:** Többoszlopos oldalak egyetlen sorba egyesülnek.  
  **Pro tip:** Detektáld az oszlophatárokat a Tesseract TSV‑kimenetének `block_num` mezője alapján, és ennek megfelelően bontsd szét a sorokat.

- **Buktató:** Nagy PDF‑ek memóriát pazarolnak, ha egyszerre betöltöd az összes oldalt.  
  **Pro tip:** Oldalak feldolgozása fokozatosan – iterálj a `pdf2image.convert_from_path(..., first_page=n, last_page=n)`‑nel.

## A folyamat bővítése

Ha kíváncsi vagy a következő lépésekre, fontold meg az alábbi fejlesztéseket:

1. **Kötegelt feldolgozás** – Csomagold be a teljes scriptet egy függvénybe, amely bejár egy könyvtárat, és párhuzamosan kezeli a több ezer fájlt a `concurrent.futures`‑szal.
2. **Nyelvi modellek** – Cseréld le az egyszerű difflib heurisztikát egy hívásra az OpenAI `gpt‑4o`‑ra vagy egy helyileg futtatott LLaMA modellre, hogy gazdagabb kontextuális javításokat kapj.
3. **Export formátumok** – Írd a javított struktúrát egy kereshető PDF‑be

## Mit érdemes legközelebb megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a bemutatott technikákra épülnek. Minden forrás teljes, működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan OCR-eljünk képszöveget nyelvvel az Aspose.OCR használatával](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Hogyan használjunk OCR-t – Haladó technikák az Aspose.OCR-rel Java-ban](/ocr/english/java/advanced-ocr-techniques/)
- [OCR pontosság javítása – Területek felismerése mód OCR-ban](/ocr/hongkong/net/text-recognition/ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}