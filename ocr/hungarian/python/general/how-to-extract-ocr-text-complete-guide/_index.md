---
category: general
date: 2026-02-22
description: Tanulja meg, hogyan lehet kinyerni az OCR‑szöveget, és javítani az OCR
  pontosságát AI utófeldolgozással. Tisztítsa meg az OCR‑szöveget könnyedén Pythonban
  egy lépésről‑lépésre példával.
draft: false
keywords:
- how to extract OCR
- improve OCR accuracy
- clean OCR text
- OCR post‑processing
- AI OCR enhancement
language: hu
og_description: Fedezze fel, hogyan lehet OCR‑szöveget kinyerni, javítani az OCR pontosságát,
  és megtisztítani az OCR‑szöveget egy egyszerű Python munkafolyamat és AI utófeldolgozás
  segítségével.
og_title: Hogyan nyerjünk ki OCR szöveget – Lépésről lépésre útmutató
tags:
- OCR
- AI
- Python
title: Hogyan lehet OCR szöveget kinyerni – Teljes útmutató
url: /hu/python/general/how-to-extract-ocr-text-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan vonjunk ki OCR szöveget – Teljes programozási útmutató

Gondoltad már valaha, **hogyan vonjunk ki OCR**-t egy beolvasott dokumentumból anélkül, hogy betűhibák és törött sorok káoszába kerülnél? Nem vagy egyedül. Sok valós projektben az OCR motor nyers kimenete egy összegabalyodott bekezdésnek tűnik, és annak tisztítása igazi feladat.

A jó hír? Ha követed ezt az útmutatót, gyakorlati módon láthatod, hogyan nyerj ki strukturált OCR adatokat, futtass egy AI utófeldolgozót, és kapj **tiszta OCR szöveget**, amely készen áll a további elemzésre. Emellett érintünk technikákat is a **OCR pontosság javítására**, hogy az eredmények már az első alkalommal megbízhatóak legyenek.

A következő néhány percben mindent áttekintünk, amire szükséged van: a szükséges könyvtárakat, egy teljes futtatható szkriptet, és tippeket a gyakori buktatók elkerüléséhez. Nincsenek homályos „lásd a dokumentációt” megoldások – csak egy teljes, önálló megoldás, amelyet egyszerűen másolhatsz és futtathatsz.

## Amire szükséged lesz

- Python 3.9+ (a kód típusjelöléseket használ, de működik régebbi 3.x verziókon is)
- Egy OCR motor, amely strukturált eredményt tud visszaadni (pl. Tesseract a `pytesseract`‑on keresztül a `--psm 1` kapcsolóval, vagy egy kereskedelmi API, amely blokk/sor metaadatokat kínál)
- Egy AI utófeldolgozó modell – ebben a példában egy egyszerű függvénnyel szimuláljuk, de helyettesítheted az OpenAI `gpt‑4o-mini`, Claude vagy bármely LLM‑mel, amely szöveget fogad és tisztított kimenetet ad vissza
- Néhány sor mintaképet (PNG/JPG), amivel tesztelhetsz

Ha ezek készen állnak, merüljünk bele.

## Hogyan vonjunk ki OCR – Kezdeti lekérdezés

Az első lépés az OCR motor meghívása, és egy **strukturált reprezentáció** kérése a sima szöveg helyett. A strukturált eredmények megőrzik a blokk-, sor- és szóhatárokat, ami a későbbi tisztítást sokkal egyszerűbbé teszi.

```python
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List

# Simple data classes mirroring a typical structured OCR response
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

def recognize_structured(image_path: str) -> StructuredResult:
    """
    Run Tesseract with the `--psm 1` layout mode to get block/line info.
    In a real engine you would get JSON directly; here we simulate it.
    """
    img = Image.open(image_path)

    # Tesseract's TSV output includes level, page_num, block_num, par_num, line_num, word_num, text…
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    current_block_idx = -1
    current_line_idx = -1

    for i, level in enumerate(tsv["level"]):
        if level == 3:  # block level
            result.blocks.append(Block())
            current_block_idx += 1
            current_line_idx = -1
        elif level == 4:  # line level
            result.blocks[current_block_idx].lines.append(Line(text=""))
            current_line_idx += 1

        # level 5 is word; concatenate words into the current line
        if level == 5:
            word = tsv["text"][i]
            if word.strip():
                line_obj = result.blocks[current_block_idx].lines[current_line_idx]
                line_obj.text += (word + " ")

    # Trim trailing spaces
    for block in result.blocks:
        for line in block.lines:
            line.text = line.text.strip()
    return result
```

> **Miért fontos ez:** A blokkok és sorok megőrzésével elkerülhetjük, hogy tippeljük, hol kezdődnek a bekezdések. A `recognize_structured` függvény egy tiszta hierarchiát ad, amelyet később egy AI modellnek adhatunk át.

```python
# Demo call – replace with your own image path
structured_result = recognize_structured("sample_scan.png")
print("Before AI:", structured_result.blocks[0].lines[0].text)
```

A kódrészlet futtatása pontosan úgy írja ki az első sort, ahogy az OCR motor látta, ami gyakran tartalmaz hibás felismeréseket, például a „0cr” helyett az „OCR” szót.

## OCR pontosság javítása AI utófeldolgozással

Miután megvan a nyers strukturált kimenet, adjuk át egy AI utófeldolgozónak. A cél a **OCR pontosság javítása** gyakori hibák javításával, a központozás normalizálásával, és szükség esetén a sorok újraszegmentálásával.

```python
import openai  # Example: using OpenAI's API; replace with your provider

def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    """
    Sends each line to an LLM that returns a cleaned version.
    This simple loop can be parallelized for large documents.
    """
    api_key = "YOUR_OPENAI_API_KEY"
    openai.api_key = api_key

    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "You are an OCR cleanup assistant. Fix any spelling, spacing, "
                "or punctuation errors in the following line while preserving the original meaning:\n\n"
                f"\"{line.text}\""
            )
            response = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=200,
            )
            cleaned = response.choices[0].message.content.strip()
            line.text = cleaned
    return structured
```

> **Pro tipp:** Ha nincs LLM előfizetésed, a hívást helyettesítheted egy helyi transzformátorral (pl. `sentence‑transformers` + egy finomhangolt javító modell) vagy akár szabályalapú megközelítéssel. A lényeg, hogy az AI minden sort önállóan lát, ami általában elegendő a **OCR szöveg tisztításához**.

```python
# Apply the AI post‑processor
structured_result = run_postprocessor(structured_result)
print("After AI:", structured_result.blocks[0].lines[0].text)
```

Most már egy sokkal tisztább mondatot kell látnod – a helyesírási hibák javítva, a felesleges szóközök eltávolítva, és a központozás korrigálva.

## OCR szöveg tisztítása a jobb eredményekért

Még az AI javítás után is érdemes egy végső szanitizációs lépést alkalmazni: eltávolítani a nem ASCII karaktereket, egységesíteni a sortöréseket, és összevonni a többszörös szóközöket. Ez a plusz átfutás biztosítja, hogy a kimenet készen áll a további feladatokra, mint az NLP vagy adatbázis importálás.

```python
import re

def final_cleanup(structured: StructuredResult) -> str:
    """
    Flattens the hierarchy into a single string and performs
    additional regex‑based cleaning.
    """
    lines = []
    for block in structured.blocks:
        for line in block.lines:
            # Remove any lingering non‑printable characters
            cleaned = re.sub(r"[^\x20-\x7E]", "", line.text)
            # Collapse multiple spaces
            cleaned = re.sub(r"\s+", " ", cleaned).strip()
            lines.append(cleaned)
    # Join blocks with double newline to preserve paragraph breaks
    return "\n\n".join(lines)

clean_text = final_cleanup(structured_result)
print("\n=== Cleaned OCR Text ===\n")
print(clean_text)
```

A `final_cleanup` függvény egy egyszerű sztringet ad, amelyet közvetlenül betáplálhatsz egy keresőindexbe, egy nyelvi modellbe vagy CSV exportba. Mivel megőriztük a blokkhatárokat, a bekezdés struktúra is megmarad.

## Szélsőséges esetek és mi‑történik‑ha‑szcenáriók

- **Többoszlopos elrendezések:** Ha a forrásod oszlopokból áll, az OCR motor összekeverheti a sorokat. A TSV kimenetből kinyerheted az oszlopkoordinátákat, és átrendezheted a sorokat, mielőtt az AI-nek küldenéd.
- **Nem latin írásrendszerek:** Kínai vagy arab nyelvek esetén módosítsd az LLM promptját, hogy nyelvspecifikus javítást kérjen, vagy használj egy erre a szkriptre finomhangolt modellt.
- **Nagy dokumentumok:** Minden sor egyenkénti küldése lassú lehet. Csoportosíts sorokat (pl. 10 sor kérésenként), és hagyd, hogy az LLM egy listát adjon vissza a tisztított sorokról. Ne feledd a tokenkorlátokat.
- **Hiányzó blokkok:** Egyes OCR motorok csak egy lapos szósort adnak vissza. Ebben az esetben a sorokat újraépítheted úgy, hogy a hasonló `line_num` értékű szavakat csoportosítod.

## Teljes működő példa

Mindent összevonva, itt egy egyetlen fájl, amelyet vég‑től‑végig futtathatsz. Cseréld ki a helyőrzőket a saját API kulcsodra és képfájl útvonaladra.

```python
# ocr_cleanup.py
import re
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List
import openai

# ---------- Data structures ----------
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

# ---------- Step 1: Extract OCR ----------
def recognize_structured(image_path: str) -> StructuredResult:
    img = Image.open(image_path)
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    cur_block = -1
    cur_line = -1

    for i, lvl in enumerate(tsv["level"]):
        if lvl == 3:                # block
            result.blocks.append(Block())
            cur_block += 1
            cur_line = -1
        elif lvl == 4:              # line
            result.blocks[cur_block].lines.append(Line(text=""))
            cur_line += 1
        elif lvl == 5:              # word
            word = tsv["text"][i]
            if word.strip():
                result.blocks[cur_block].lines[cur_line].text += word + " "

    # Trim spaces
    for blk in result.blocks:
        for ln in blk.lines:
            ln.text = ln.text.strip()
    return result

# ---------- Step 2: AI post‑processor ----------
def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    openai.api_key = "YOUR_OPENAI_API_KEY"
    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "Correct OCR errors (spelling, spacing, punctuation) in this line:\n"
                f"\"{line.text}\""
            )
            resp = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=150,
            )
            line.text = resp.choices[0].message.content.strip()
    return structured

# ---------- Step 3: Final cleanup ----------
def final_cleanup(structured: StructuredResult) -> str:
    out = []
    for block in structured.blocks:
        for line in block.lines:
            txt = re.sub(r"[^\x20-\x7E]", "", line.text)   # strip non‑ASCII
            txt = re.sub(r"\s+", " ", txt).strip

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}