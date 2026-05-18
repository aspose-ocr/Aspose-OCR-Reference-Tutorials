---
category: general
date: 2026-04-26
description: Hogyan postprocesszáljuk az OCR eredményeket és nyerjünk ki szöveget
  koordinátákkal. Tanuljon meg egy lépésről‑lépésre megoldást strukturált kimenet
  és AI‑korrekció használatával.
draft: false
keywords:
- how to post‑process OCR
- extract text with coordinates
- OCR structured output
- AI post‑processing OCR
- bounding box OCR
language: hu
og_description: Hogyan utófeldolgozzuk az OCR-eredményeket, és szöveget nyerjünk ki
  koordinátákkal. Kövesd ezt az átfogó útmutatót egy megbízható munkafolyamatért.
og_title: Hogyan utófeldolgozzuk az OCR-t – Teljes útmutató
tags:
- OCR
- Python
- AI
- Text Extraction
title: Hogyan utófeldolgozzuk az OCR‑t – Szöveg kinyerése koordinátákkal Pythonban
url: /hu/python/general/how-to-post-process-ocr-extract-text-with-coordinates-in-pyt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan kell utófeldolgozni az OCR‑t – Szöveg kinyerése koordinátákkal Pythonban

Volt már, hogy **hogyan kell utófeldolgozni az OCR** eredményeket, mert a nyers kimenet zajos vagy rosszul igazított volt? Nem vagy egyedül. Sok valós projektben – számlabeolvasás, nyugták digitalizálása vagy akár AR‑élmények kiegészítése – az OCR motor nyers szavakat ad, de neked még mindig tisztítanod kell őket, és nyomon kell követned, hogy a szó hol helyezkedik el az oldalon. Itt jön képbe a strukturált kimeneti mód egy AI‑vezérelt utófeldolgozóval kombinálva.

Ebben a tutorialban végigvezetünk egy teljes, futtatható Python pipeline‑on, amely **koordinátákkal együtt kinyeri a szöveget** egy képből, egy AI‑alapú korrekciós lépést hajt végre, és minden szót kiír a (x, y) pozíciójával együtt. Nincs hiányzó import, nincs homályos „lásd a dokumentációt” hivatkozás – csak egy önálló megoldás, amelyet ma be tudsz illeszteni a projektedbe.

> **Pro tip:** Ha másik OCR könyvtárat használsz, keresd a „structured” vagy „layout” módot; a koncepciók ugyanazok.

---

## Előfeltételek

Mielőtt belevágnánk, győződj meg róla, hogy a következők rendelkezésre állnak:

| Követelmény | Miért fontos |
|-------------|--------------|
| Python 3.9+ | Modern szintaxis és típusjelölések |
| `ocr` könyvtár, amely támogatja az `OutputMode.STRUCTURED`‑t (pl. egy fiktív `myocr`) | Szükséges a körülhatároló doboz adatokhoz |
| AI utófeldolgozó modul (lehet OpenAI, HuggingFace vagy egy egyedi modell) | Javítja a pontosságot az OCR után |
| Képfájl (`input.png`) a munkakönyvtáradban | A forrás, amelyet beolvasunk |

Ha bármelyik ismeretlennek tűnik, telepítsd a helyettesítő csomagokat a `pip install myocr ai‑postproc` paranccsal. Az alábbi kód tartalmaz fallback stub‑okat is, így a folyamatot a valódi könyvtárak nélkül is tesztelheted.

---

## 1. lépés: Strukturált kimeneti mód engedélyezése az OCR motorban  

Az első dolog, amit megteszünk, hogy az OCR motorra azt mondjuk, adjon nekünk többet, mint egyszerű szöveget. A strukturált kimenet minden szót a körülhatároló dobozzal és a megbízhatósági pontszámmal együtt adja vissza, ami elengedhetetlen a **szöveg kinyerése koordinátákkal** később.

```python
# step1_structured_output.py
import myocr as ocr  # fictional OCR library

# Initialize the engine (replace with your actual init code)
engine = ocr.Engine()

# Switch to structured mode – this makes the engine emit word‑level data
engine.set_output_mode(ocr.OutputMode.STRUCTURED)

print("✅ Structured output mode enabled")
```

*Miért fontos:* Strukturált mód nélkül csak egy hosszú karakterláncot kapnál, és elveszítenéd a térbeli információkat, amelyekre a szöveg képre való ráhelyezéséhez vagy a downstream layout elemzéshez szükség van.

---

## 2. lépés: Kép felismerése és a szavak, dobozok, valamint a megbízhatóság rögzítése  

Most betápláljuk a képet a motorba. Az eredmény egy objektum, amely szólistát tartalmaz, minden szó objektuma pedig rendelkezik `text`, `x`, `y`, `width`, `height` és `confidence` mezőkkel.

```python
# step2_recognize.py
from pathlib import Path

# Path to your image
image_path = Path("YOUR_DIRECTORY/input.png")

# Perform OCR – returns a StructuredResult with .words collection
structured_result = engine.recognize_image(str(image_path))

print(f"🔎 Detected {len(structured_result.words)} words")
```

*Edge case:* Ha a kép üres vagy nem olvasható, a `structured_result.words` egy üres listát ad vissza. Jó gyakorlat ellenőrizni ezt, és megfelelően kezelni.

---

## 3. lépés: AI‑alapú utófeldolgozás a pozíciók megőrzésével  

Még a legjobb OCR motorok is hibáznak – gondolj a „O” és a „0” közti különbségre vagy a hiányzó diakritikus jelekre. Egy domain‑specifikus szövegre tanított AI modell kijavíthatja ezeket a hibákat. Lényeges, hogy az eredeti koordinátákat megtartsuk, így a térbeli elrendezés változatlan marad.

```python
# step3_ai_postprocess.py
import ai_postproc as ai  # placeholder for your AI module

# The AI post‑processor expects the structured result and returns a new one
corrected_result = ai.run_postprocessor(structured_result)

print("🤖 AI post‑processing complete")
```

*Miért őrizzük meg a koordinátákat:* Sok downstream feladat (pl. PDF generálás, AR címkézés) pontos elhelyezést igényel. Az AI csak a `text` mezőt módosítja, a `x`, `y`, `width`, `height` változatlan marad.

---

## 4. lépés: A javított szavak iterálása és a szöveg koordinátákkal való megjelenítése  

Végül végigjárjuk a javított szavakat, és kiírjuk minden szót a bal‑felső sarok `(x, y)` koordinátáival együtt. Ez teljesíti a **szöveg kinyerése koordinátákkal** célt.

```python
# step4_display.py
for recognized_word in corrected_result.words:
    # Using f‑string for clean formatting
    print(f"{recognized_word.text} (x:{recognized_word.x}, y:{recognized_word.y})")
```

**Várt kimenet (példa):**

```
Invoice (x:45, y:112)
Number (x:120, y:112)
12345 (x:190, y:112)
Total (x:45, y:250)
$ (x:120, y:250)
199.99 (x:130, y:250)
```

Minden sor a javított szót és annak pontos helyét mutatja az eredeti képen.

---

## Teljes működő példa  

Az alábbi egyetlen szkript mindent összekapcsol. Másold be, igazítsd a importokat a saját könyvtáraidhoz, és futtasd közvetlenül.

```python
# ocr_postprocess_demo.py
"""
Complete demo: how to post‑process OCR and extract text with coordinates.
Works with any OCR library exposing a structured output mode and an AI post‑processor.
"""

import sys
from pathlib import Path

# ----------------------------------------------------------------------
# 1️⃣ Imports – replace these with your real packages
# ----------------------------------------------------------------------
try:
    import myocr as ocr               # OCR engine with structured output
    import ai_postproc as ai          # AI correction module
except ImportError:  # Fallback stubs for quick testing
    class DummyWord:
        def __init__(self, text, x, y, w, h, conf):
            self.text = text
            self.x = x
            self.y = y
            self.width = w
            self.height = h
            self.confidence = conf

    class DummyResult:
        def __init__(self, words):
            self.words = words

    class StubEngine:
        class OutputMode:
            STRUCTURED = "structured"

        def set_output_mode(self, mode):
            print(f"[Stub] set_output_mode({mode})")

        def recognize_image(self, path):
            # Very simple fake OCR output
            sample = [
                DummyWord("Invoice", 45, 112, 60, 20, 0.98),
                DummyWord("Number", 120, 112, 55, 20, 0.96),
                DummyWord("12345", 190, 112, 40, 20, 0.97),
                DummyWord("Total", 45, 250, 50, 20, 0.99),
                DummyWord("$", 120, 250, 10, 20, 0.95),
                DummyWord("199.99", 130, 250, 55, 20, 0.94),
            ]
            return DummyResult(sample)

    class StubAI:
        @staticmethod
        def run_postprocessor(structured_result):
            # Pretend we corrected "12345" to "12346"
            for w in structured_result.words:
                if w.text == "12345":
                    w.text = "12346"
            return structured_result

    engine = StubEngine()
    ai = StubAI

# ----------------------------------------------------------------------
# 2️⃣ Enable structured output
# ----------------------------------------------------------------------
engine.set_output_mode(ocr.Engine.OutputMode.STRUCTURED)

# ----------------------------------------------------------------------
# 3️⃣ Recognize image
# ----------------------------------------------------------------------
image_path = Path("YOUR_DIRECTORY/input.png")
if not image_path.is_file():
    print(f"⚠️  Image not found at {image_path}. Using stub data.")
structured_result = engine.recognize_image(str(image_path))

# ----------------------------------------------------------------------
# 4️⃣ AI post‑processing
# ----------------------------------------------------------------------
corrected_result = ai.run_postprocessor(structured_result)

# ----------------------------------------------------------------------
# 5️⃣ Display results
# ----------------------------------------------------------------------
print("\n🗒️  Final OCR output with coordinates:")
for word in corrected_result.words:
    print(f"{word.text} (x:{word.x}, y:{word.y})")
```

**A szkript futtatása**

```bash
python ocr_postprocess_demo.py
```

Ha a valódi könyvtárak telepítve vannak, a szkript feldolgozza a `input.png` fájlt. Ellenkező esetben a stub implementáció lehetővé teszi, hogy a várt folyamatot és kimenetet láthasd külső függőségek nélkül.

---

## Gyakran Ismételt Kérdések (FAQ)

| Kérdés | Válasz |
|--------|--------|
| *Működik ez Tesseract‑tal?* | A Tesseract önmagában nem kínál strukturált módot, de a `pytesseract.image_to_data` wrapper visszaadja a körülhatároló dobozokat, amelyeket ugyanabba az AI utófeldolgozóba táplálhatsz. |
| *Mi van, ha a jobb‑alsó sarok koordinátájára van szükségem a bal‑felső helyett?* | Minden szó objektum tartalmazza a `width` és `height` értékeket. Számold ki `x2 = x + width` és `y2 = y + height` a ellentétes sarokhoz. |
| *Tudok több képet egyszerre feldolgozni?* | Természetesen. Csomagold a lépéseket egy `for image_path in Path("folder").glob("*.png"):` ciklusba, és gyűjtsd az eredményeket fájlonként. |
| *Hogyan válasszak AI modellt a korrekcióhoz?* | Általános szöveghez egy kis GPT‑2 modell, amely OCR hibákon finomhangolt, megfelelő. Domain‑specifikus adatokhoz (pl. orvosi receptek) taníts egy sequence‑to‑sequence modellt párhuzamos zajos‑tiszta adatokon. |
| *Hasznos a confidence score az AI korrekció után?* | Megtarthatod az eredeti confidence értéket hibakereséshez, de az AI is adhat saját confidence‑t, ha a modell támogatja. |

---

## Edge case‑ek és legjobb gyakorlatok  

1. **Üres vagy sérült képek** – mindig ellenőrizd, hogy a `structured_result.words` nem üres, mielőtt folytatnád.  
2. **Nem latin írásrendszerek** – győződj meg róla, hogy az OCR motor a célnyelvre van konfigurálva; az AI utófeldolgozónak ugyanazon írásrendszeren kell lennie tréningezve.  
3. **Teljesítmény** – az AI korrekció költséges lehet. Cache‑eld az eredményeket, ha ugyanazt a képet többször használod, vagy futtasd az AI lépést aszinkron módon.  
4. **Koordináta rendszer** – az OCR könyvtárak különböző origókat (bal‑felső vs. bal‑alsó) használhatnak. Igazítsd a koordinátákat, amikor PDF‑ekre vagy vásznakra helyezed őket.  

---

## Összegzés  

Most már van egy szilárd, vég‑től‑végig recept a **hogyan kell utófeldolgozni az OCR**-t és megbízhatóan **szöveget kinyerni koordinátákkal**. A strukturált kimenet engedélyezésével, az eredmény AI‑korrekciós rétegen való áthaladásával és az eredeti körülhatároló dobozok megőrzésével a zajos OCR beolvasásokat tiszta, térbeli információval rendelkező szöveggé alakíthatod, amely készen áll downstream feladatokra, mint PDF generálás, adatbevitel automatizálás vagy augmentált valóság overlay‑k.

Készen állsz a következő lépésre? Próbáld ki a stub AI helyett egy OpenAI `gpt‑4o‑mini` hívással, vagy integráld a pipeline‑t egy FastAPI‑ba

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}