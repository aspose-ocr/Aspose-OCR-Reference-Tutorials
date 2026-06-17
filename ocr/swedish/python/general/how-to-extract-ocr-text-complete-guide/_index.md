---
category: general
date: 2026-02-22
description: Lär dig hur du extraherar OCR‑text och förbättrar OCR‑noggrannheten med
  AI‑efterbehandling. Rengör OCR‑text enkelt i Python med ett steg‑för‑steg‑exempel.
draft: false
keywords:
- how to extract OCR
- improve OCR accuracy
- clean OCR text
- OCR post‑processing
- AI OCR enhancement
language: sv
og_description: Upptäck hur du extraherar OCR‑text, förbättrar OCR‑noggrannheten och
  rensar OCR‑text med ett enkelt Python‑arbetsflöde med AI‑efterbehandling.
og_title: Hur man extraherar OCR‑text – Steg‑för‑steg‑guide
tags:
- OCR
- AI
- Python
title: Hur man extraherar OCR‑text – Komplett guide
url: /sv/python/general/how-to-extract-ocr-text-complete-guide/
---

-backtop-button >}}

We keep them unchanged.

We need to ensure we didn't miss any text after the code block: The code block ends with `txt = re.sub(r"\s+", " ", txt).strip` then the closing tags. That is fine.

Now produce final output with all translated content and unchanged elements.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man extraherar OCR‑text – Komplett programmeringshandledning

Har du någonsin undrat **hur man extraherar OCR** från ett skannat dokument utan att sluta med en röra av stavfel och brutna rader? Du är inte ensam. I många verkliga projekt ser den råa utdata från en OCR‑motor ut som ett förvirrat stycke, och att rensa upp det känns som ett jobb.  

Den goda nyheten? Genom att följa den här guiden får du se ett praktiskt sätt att hämta strukturerad OCR‑data, köra en AI‑postprocessor och sluta med **ren OCR‑text** som är klar för vidare analys. Vi kommer också att beröra tekniker för att **förbättra OCR‑noggrannheten** så att resultaten är pålitliga redan första gången.

Under de kommande minuterna går vi igenom allt du behöver: nödvändiga bibliotek, ett komplett körbart skript och tips för att undvika vanliga fallgropar. Inga vaga “se dokumentationen”-genvägar—bara en komplett, självständig lösning som du kan kopiera, klistra in och köra.

## Vad du behöver

- Python 3.9+ (koden använder typ‑hints men fungerar på äldre 3.x‑versioner)
- En OCR‑motor som kan returnera ett strukturerat resultat (t.ex. Tesseract via `pytesseract` med flaggan `--psm 1`, eller ett kommersiellt API som erbjuder block‑/linjemetadata)
- En AI‑postprocessormodell – i det här exemplet mockar vi den med en enkel funktion, men du kan byta ut mot OpenAI:s `gpt‑4o-mini`, Claude eller någon LLM som accepterar text och returnerar rensad output
- Några rader med exempelbild (PNG/JPG) att testa mot

Om du har detta redo, låt oss dyka in.

## Hur man extraherar OCR – Initial hämtning

Det första steget är att anropa OCR‑motorn och be om en **strukturerad representation** istället för en vanlig sträng. Strukturerade resultat bevarar block‑, rad‑ och ordgränser, vilket gör efterföljande rensning mycket enklare.

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

> **Varför detta är viktigt:** Genom att bevara block och rader undviker vi att behöva gissa var stycken börjar. Funktionen `recognize_structured` ger oss en ren hierarki som vi senare kan mata in i en AI‑modell.

```python
# Demo call – replace with your own image path
structured_result = recognize_structured("sample_scan.png")
print("Before AI:", structured_result.blocks[0].lines[0].text)
```

När du kör kodsnutten skrivs den första raden ut exakt som OCR‑motorn såg den, vilket ofta innehåller feligenkänningar som “0cr” istället för “OCR”.

## Förbättra OCR‑noggrannhet med AI‑postprocessering

Nu när vi har den råa strukturerade utdata, låt oss ge den till en AI‑postprocessor. Målet är att **förbättra OCR‑noggrannheten** genom att korrigera vanliga misstag, normalisera interpunktion och till och med omsegmentera rader när det behövs.

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

> **Proffstips:** Om du inte har en LLM‑prenumeration kan du ersätta anropet med en lokal transformer (t.ex. `sentence‑transformers` + en finjusterad korrigeringsmodell) eller till och med ett regelbaserat tillvägagångssätt. Huvudidén är att AI:n ser varje rad isolerat, vilket vanligtvis räcker för att **rensa OCR‑text**.

```python
# Apply the AI post‑processor
structured_result = run_postprocessor(structured_result)
print("After AI:", structured_result.blocks[0].lines[0].text)
```

Du bör nu se en mycket renare mening—stavfel ersatta, extra mellanslag borttagna och interpunktion korrigerad.

## Rensa OCR‑text för bättre resultat

Även efter AI‑korrigering kan du vilja applicera ett sista saneringssteg: ta bort icke‑ASCII‑tecken, förena radbrytningar och slå ihop flera mellanslag. Detta extra pass säkerställer att utdata är klar för efterföljande uppgifter som NLP eller databasinmatning.

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

Funktionen `final_cleanup` ger dig en ren sträng som du kan mata in direkt i ett sökindex, en språkmodell eller en CSV‑export. Eftersom vi behöll blockgränserna bevaras styckestrukturen.

## Kantfall & “Vad‑om”‑scenarier

- **Multi‑column layouts:** Om din källa har kolumner kan OCR‑motorn blanda rader. Du kan upptäcka kolumnkoordinater från TSV‑utdata och omordna rader innan du skickar dem till AI:n.
- **Non‑Latin scripts:** För språk som kinesiska eller arabiska, byt LLM‑prompten för att begära språk‑specifik korrigering, eller använd en modell finjusterad på det skriptet.
- **Large documents:** Att skicka varje rad individuellt kan vara långsamt. Batcha rader (t.ex. 10 per förfrågan) och låt LLM:n returnera en lista med rensade rader. Kom ihåg att respektera token‑gränser.
- **Missing blocks:** Vissa OCR‑motorer returnerar bara en platt lista med ord. I så fall kan du rekonstruera rader genom att gruppera ord med liknande `line_num`‑värden.

## Fullständigt fungerande exempel

När vi sätter ihop allt, här är en enda fil du kan köra från början till slut. Ersätt platshållarna med din egen API‑nyckel och bildsökväg.

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