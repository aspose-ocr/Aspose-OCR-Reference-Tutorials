---
category: general
date: 2026-02-22
description: Naučte se, jak extrahovat text z OCR a zlepšit přesnost OCR pomocí AI
  post‑zpracování. Jednoduše vyčistěte OCR text v Pythonu pomocí krok‑za‑krokem příkladu.
draft: false
keywords:
- how to extract OCR
- improve OCR accuracy
- clean OCR text
- OCR post‑processing
- AI OCR enhancement
language: cs
og_description: Objevte, jak extrahovat OCR text, zlepšit přesnost OCR a vyčistit
  OCR text pomocí jednoduchého pracovního postupu v Pythonu s AI post‑processing.
og_title: Jak extrahovat OCR text – krok za krokem
tags:
- OCR
- AI
- Python
title: Jak extrahovat OCR text – kompletní průvodce
url: /cs/python/general/how-to-extract-ocr-text-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak extrahovat OCR text – kompletní programovací tutoriál

Už jste se někdy zamýšleli **jak extrahovat OCR** ze skenovaného dokumentu, aniž byste skončili s hromadou překlepů a rozbitých řádků? Nejste v tom sami. V mnoha reálných projektech vypadá surový výstup z OCR enginu jako zamotaný odstavec a jeho čištění připadá na obtížnou práci.  

Dobrá zpráva? Pokud budete postupovat podle tohoto návodu, uvidíte praktický způsob, jak získat strukturovaná OCR data, spustit AI post‑processor a získat **čistý OCR text**, který je připravený pro další analýzu. Dotkneme se také technik, jak **zlepšit přesnost OCR**, aby byly výsledky spolehlivé hned napoprvé.

V následujících několika minutách probereme vše, co potřebujete: požadované knihovny, kompletní spustitelný skript a tipy, jak se vyhnout běžným úskalím. Žádné vágní „viz dokumentaci“ zkratky — jen kompletní, samostatné řešení, které můžete zkopírovat a spustit.

## Co budete potřebovat

- Python 3.9+ (kód používá typové nápovědy, ale funguje i na starších 3.x verzích)
- OCR engine, který dokáže vrátit strukturovaný výsledek (např. Tesseract přes `pytesseract` s příznakem `--psm 1`, nebo komerční API, které poskytuje metadata o blocích/řádcích)
- AI post‑processing model — v tomto příkladu jej nahradíme jednoduchou funkcí, ale můžete použít OpenAI `gpt‑4o-mini`, Claude nebo jakýkoli LLM, který přijímá text a vrací vyčištěný výstup
- Několik ukázkových obrázků (PNG/JPG) pro testování

Pokud máte vše připravené, pojďme na to.

## Jak extrahovat OCR – počáteční získání

Prvním krokem je zavolat OCR engine a požádat ho o **strukturovanou reprezentaci** místo prostého řetězce. Strukturované výsledky zachovávají hranice bloků, řádků a slov, což usnadňuje následné čištění.

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

> **Proč je to důležité:** Zachováním bloků a řádků se vyhneme hádání, kde začínají odstavce. Funkce `recognize_structured` nám poskytne čistou hierarchii, kterou můžeme později předat AI modelu.

```python
# Demo call – replace with your own image path
structured_result = recognize_structured("sample_scan.png")
print("Before AI:", structured_result.blocks[0].lines[0].text)
```

Spuštěním úryvku se vytiskne první řádek přesně tak, jak jej OCR engine viděl, což často obsahuje chyby jako “0cr” místo “OCR”.

## Zlepšení přesnosti OCR pomocí AI post‑processingu

Nyní, když máme surový strukturovaný výstup, předáme ho AI post‑processoru. Cílem je **zlepšit přesnost OCR** opravou častých chyb, normalizací interpunkce a případným pře‑segmentováním řádků.

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

> **Tip:** Pokud nemáte předplatné na LLM, můžete volání nahradit lokálním transformerem (např. `sentence‑transformers` + jemně doladěný korekční model) nebo i pravidlovým přístupem. Hlavní myšlenka je, že AI vidí každý řádek izolovaně, což obvykle stačí k **vyčištění OCR textu**.

```python
# Apply the AI post‑processor
structured_result = run_postprocessor(structured_result)
print("After AI:", structured_result.blocks[0].lines[0].text)
```

Nyní byste měli vidět mnohem čistší větu — překlepy opravené, nadbytečné mezery odstraněné a interpunkce upravená.

## Čištění OCR textu pro lepší výsledky

I po AI korekci můžete chtít provést poslední sanitizační krok: odstranit ne‑ASCII znaky, sjednotit konce řádků a sloučit vícenásobné mezery. Tento dodatečný průchod zajistí, že výstup je připravený pro následné úkoly jako NLP nebo import do databáze.

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

Funkce `final_cleanup` vám vrátí prostý řetězec, který můžete přímo předat vyhledávacímu indexu, jazykovému modelu nebo exportovat do CSV. Díky zachování hranic bloků zůstává struktura odstavců zachována.

## Okrajové případy a co‑když scénáře

- **Více‑sloupcové rozvržení:** Pokud má zdroj sloupce, OCR engine může proplétat řádky. Sloupce můžete detekovat podle souřadnic v TSV výstupu a před odesláním AI řádky přeuspořádat.
- **Nelatecké skripty:** Pro jazyky jako čínština nebo arabština změňte prompt LLM tak, aby požadoval korekci specifickou pro daný jazyk, nebo použijte model jemně doladěný na tento skript.
- **Velké dokumenty:** Odesílání každého řádku zvlášť může být pomalé. Zpracovávejte řádky po dávkách (např. 10 na požadavek) a nechte LLM vrátit seznam vyčištěných řádků. Nezapomeňte respektovat limity tokenů.
- **Chybějící bloky:** Některé OCR enginy vrací jen plochý seznam slov. V takovém případě můžete řádky zrekonstruovat seskupením slov s podobnými hodnotami `line_num`.

## Kompletní funkční příklad

Sestavením všeho dohromady získáte jeden soubor, který můžete spustit od začátku do konce. Nahraďte zástupné hodnoty svým API klíčem a cestou k obrázku.

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