---
category: general
date: 2026-02-22
description: Leer hoe je OCR‑tekst kunt extraheren en de OCR‑nauwkeurigheid kunt verbeteren
  met AI‑nabewerking. Maak OCR‑tekst eenvoudig schoon in Python met een stapsgewijs
  voorbeeld.
draft: false
keywords:
- how to extract OCR
- improve OCR accuracy
- clean OCR text
- OCR post‑processing
- AI OCR enhancement
language: nl
og_description: Ontdek hoe je OCR‑tekst kunt extraheren, de OCR‑nauwkeurigheid kunt
  verbeteren en OCR‑tekst kunt opschonen met een eenvoudige Python‑workflow met AI‑nabewerking.
og_title: Hoe OCR-tekst te extraheren – Stapsgewijze handleiding
tags:
- OCR
- AI
- Python
title: Hoe OCR-tekst te extraheren – Complete gids
url: /nl/python/general/how-to-extract-ocr-text-complete-guide/
---

text: The code block after final_cleanup is truncated; we keep as is.

Make sure to keep markdown formatting.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR-tekst te extraheren – Complete programmeertutorial

Heb je je ooit afgevraagd **hoe je OCR kunt extraheren** uit een gescand document zonder te eindigen met een rommel van typefouten en gebroken regels? Je bent niet de enige. In veel real‑world projecten ziet de ruwe output van een OCR‑engine eruit als een warachtige alinea, en het opschonen voelt als een karwei.  

Het goede nieuws? Door deze gids te volgen zie je een praktische manier om gestructureerde OCR‑gegevens op te halen, een AI‑postprocessor uit te voeren, en te eindigen met **schone OCR‑tekst** die klaar is voor downstream‑analyse. We zullen ook ingaan op technieken om **OCR‑nauwkeurigheid te verbeteren** zodat de resultaten de eerste keer betrouwbaar zijn.

In de komende paar minuten behandelen we alles wat je nodig hebt: vereiste bibliotheken, een volledig uitvoerbaar script, en tips om veelvoorkomende valkuilen te vermijden. Geen vage “zie de docs” shortcuts—maar een complete, zelfstandige oplossing die je kunt kopiëren‑plakken en uitvoeren.

## Wat je nodig hebt

- Python 3.9+ (de code gebruikt type hints maar werkt op oudere 3.x versies)
- Een OCR‑engine die een gestructureerd resultaat kan teruggeven (bijv. Tesseract via `pytesseract` met de `--psm 1` vlag, of een commerciële API die blok‑/lijn‑metadata biedt)
- Een AI‑post‑processing model – voor dit voorbeeld mocken we het met een eenvoudige functie, maar je kunt OpenAI’s `gpt‑4o-mini`, Claude, of elke LLM die tekst accepteert en een opgeschoond resultaat teruggeeft, gebruiken
- Een paar voorbeeldafbeeldingen (PNG/JPG) om tegen te testen

Als je deze klaar hebt, laten we erin duiken.

## Hoe OCR te extraheren – Initiële ophalen

De eerste stap is om de OCR‑engine aan te roepen en te vragen om een **gestructureerde representatie** in plaats van een platte string. Gestructureerde resultaten behouden blok‑, lijn‑ en woordgrenzen, waardoor later opschonen veel makkelijker wordt.

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

> **Waarom dit belangrijk is:** Door blokken en lijnen te behouden hoeven we niet te raden waar alinea’s beginnen. De `recognize_structured` functie geeft ons een schone hiërarchie die we later aan een AI‑model kunnen voeren.

```python
# Demo call – replace with your own image path
structured_result = recognize_structured("sample_scan.png")
print("Before AI:", structured_result.blocks[0].lines[0].text)
```

Het uitvoeren van de snippet print de eerste regel precies zoals de OCR‑engine die zag, wat vaak mis‑herkenningen bevat zoals “0cr” in plaats van “OCR”.

## OCR‑nauwkeurigheid verbeteren met AI‑post‑processing

Nu we de ruwe gestructureerde output hebben, laten we deze aan een AI‑post‑processor geven. Het doel is om **OCR‑nauwkeurigheid te verbeteren** door veelvoorkomende fouten te corrigeren, interpunctie te normaliseren, en zelfs lijnen opnieuw te segmenteren wanneer nodig.

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

> **Pro tip:** Als je geen LLM‑abonnement hebt, kun je de oproep vervangen door een lokale transformer (bijv. `sentence‑transformers` + een fijn afgestemd correctiemodel) of zelfs een regel‑gebaseerde aanpak. Het belangrijkste idee is dat de AI elke regel afzonderlijk ziet, wat meestal voldoende is om **OCR‑tekst schoon te maken**.

```python
# Apply the AI post‑processor
structured_result = run_postprocessor(structured_result)
print("After AI:", structured_result.blocks[0].lines[0].text)
```

Je zou nu een veel schonere zin moeten zien — typefouten vervangen, extra spaties verwijderd, en interpunctie gecorrigeerd.

## OCR‑tekst opschonen voor betere resultaten

Zelfs na AI‑correctie wil je misschien een laatste sanitatiestap toepassen: niet‑ASCII‑tekens verwijderen, regeleinden uniform maken, en meerdere spaties samenvouwen. Deze extra doorloop zorgt ervoor dat de output klaar is voor downstream‑taken zoals NLP of database‑invoer.

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

De `final_cleanup` functie geeft je een platte string die je direct kunt invoeren in een zoekindex, een taalmodel, of een CSV‑export. Omdat we de blok‑grenzen hebben behouden, blijft de alinea‑structuur behouden.

## Randgevallen & Wat‑als scenario's

- **Meerkolomsindelingen:** Als je bron kolommen heeft, kan de OCR‑engine lijnen door elkaar husselen. Je kunt kolomcoördinaten uit de TSV‑output detecteren en lijnen herschikken voordat je ze naar de AI stuurt.
- **Niet‑Latijnse scripts:** Voor talen zoals Chinees of Arabisch, wijzig de prompt van de LLM om taalspecifieke correctie te vragen, of gebruik een model dat op dat script is getraind.
- **Grote documenten:** Het individueel verzenden van elke regel kan traag zijn. Batch regels (bijv. 10 per verzoek) en laat de LLM een lijst met opgeschoonde regels teruggeven. Houd rekening met token‑limieten.
- **Ontbrekende blokken:** Sommige OCR‑engines geven alleen een platte lijst van woorden terug. In dat geval kun je regels reconstrueren door woorden met vergelijkbare `line_num` waarden te groeperen.

## Volledig werkend voorbeeld

Door alles samen te voegen, hier is een enkel bestand dat je end‑to‑end kunt uitvoeren. Vervang de placeholders door je eigen API‑sleutel en afbeeldingspad.

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