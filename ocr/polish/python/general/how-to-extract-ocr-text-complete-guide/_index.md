---
category: general
date: 2026-02-22
description: Dowiedz się, jak wyodrębniać tekst OCR i poprawiać jego dokładność dzięki
  przetwarzaniu AI. Łatwo oczyszczaj tekst OCR w Pythonie, korzystając z przykładu
  krok po kroku.
draft: false
keywords:
- how to extract OCR
- improve OCR accuracy
- clean OCR text
- OCR post‑processing
- AI OCR enhancement
language: pl
og_description: Odkryj, jak wyodrębniać tekst OCR, poprawiać dokładność OCR i oczyszczać
  tekst OCR, korzystając z prostego przepływu pracy w Pythonie z post‑procesowaniem
  AI.
og_title: Jak wyodrębnić tekst OCR – przewodnik krok po kroku
tags:
- OCR
- AI
- Python
title: Jak wyodrębnić tekst OCR – Kompletny przewodnik
url: /pl/python/general/how-to-extract-ocr-text-complete-guide/
---

with same structure.

Make sure to keep shortcodes at top and bottom unchanged.

Also ensure no extra spaces that could break formatting.

Let's craft final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyodrębnić tekst OCR – Kompletny samouczek programistyczny

Zastanawiałeś się kiedyś **jak wyodrębnić OCR** ze zeskanowanego dokumentu, nie kończąc z bałaganem literówek i przerwanych linii? Nie jesteś sam. W wielu projektach w rzeczywistym świecie surowy wynik silnika OCR wygląda jak pomieszany akapit, a jego czyszczenie przypomina żmudne zadanie.  

Dobre wieści? Postępując zgodnie z tym przewodnikiem zobaczysz praktyczny sposób na pobranie ustrukturyzowanych danych OCR, uruchomienie AI post‑procesora i uzyskanie **czystego tekstu OCR**, gotowego do dalszej analizy. Poruszymy także techniki **poprawy dokładności OCR**, aby wyniki były wiarygodne od pierwszego razu.

W ciągu kilku minut omówimy wszystko, czego potrzebujesz: wymagane biblioteki, pełny działający skrypt oraz wskazówki, jak unikać typowych pułapek. Bez niejasnych „zobacz dokumentację” skrótów — tylko kompletny, samodzielny zestaw, który możesz skopiować‑wkleić i uruchomić.

## Czego będziesz potrzebować

- Python 3.9+ (kod używa podpowiedzi typów, ale działa również na starszych wersjach 3.x)
- Silnik OCR, który może zwrócić ustrukturyzowany wynik (np. Tesseract poprzez `pytesseract` z flagą `--psm 1` lub komercyjne API oferujące metadane bloków/wierszy)
- Model AI do post‑procesowania – w tym przykładzie zamockujemy go prostą funkcją, ale możesz podmienić go na `gpt‑4o-mini` od OpenAI, Claude lub dowolny LLM, który przyjmuje tekst i zwraca wyczyszczony wynik
- Kilka przykładowych obrazów (PNG/JPG) do przetestowania

Jeśli masz to gotowe, zanurzmy się.

## Jak wyodrębnić OCR – początkowe pobranie

Pierwszym krokiem jest wywołanie silnika OCR i poproszenie go o **ustrukturyzowaną reprezentację** zamiast zwykłego ciągu znaków. Ustrukturyzowane wyniki zachowują granice bloków, linii i słów, co znacznie ułatwia późniejsze czyszczenie.

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

> **Dlaczego to ważne:** Zachowując bloki i linie, unikamy zgadywania, gdzie zaczynają się paragrafy. Funkcja `recognize_structured` dostarcza nam czystą hierarchię, którą później możemy przekazać modelowi AI.

```python
# Demo call – replace with your own image path
structured_result = recognize_structured("sample_scan.png")
print("Before AI:", structured_result.blocks[0].lines[0].text)
```

Uruchomienie fragmentu wypisuje pierwszą linię dokładnie tak, jak zobaczył ją silnik OCR, co często zawiera błędne rozpoznania, takie jak „0cr” zamiast „OCR”.

## Popraw dokładność OCR przy użyciu AI post‑processing

Teraz, gdy mamy surowy ustrukturyzowany wynik, przekażmy go AI post‑processorowi. Celem jest **poprawa dokładności OCR** poprzez korektę typowych błędów, normalizację interpunkcji i nawet ponowne segmentowanie linii w razie potrzeby.

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

> **Wskazówka:** Jeśli nie masz subskrypcji LLM, możesz zamienić wywołanie na lokalny transformer (np. `sentence‑transformers` + wytrenowany model korekcji) lub nawet podejście oparte na regułach. Kluczowa idea polega na tym, że AI widzi każdą linię osobno, co zazwyczaj wystarcza, aby **wyczyścić tekst OCR**.

```python
# Apply the AI post‑processor
structured_result = run_postprocessor(structured_result)
print("After AI:", structured_result.blocks[0].lines[0].text)
```

Teraz powinieneś zobaczyć znacznie czystsze zdanie — literówki zastąpione, zbędne spacje usunięte, a interpunkcja poprawiona.

## Wyczyść tekst OCR dla lepszych wyników

Nawet po korekcie AI możesz chcieć zastosować końcowy krok sanitizacji: usunąć znaki nie‑ASCII, ujednolicić podziały linii i zredukować wielokrotne spacje. Ten dodatkowy przebieg zapewnia, że wynik jest gotowy do dalszych zadań, takich jak NLP czy import do bazy danych.

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

Funkcja `final_cleanup` zwraca zwykły ciąg znaków, który możesz bezpośrednio wprowadzić do indeksu wyszukiwania, modelu językowego lub eksportu CSV. Ponieważ zachowaliśmy granice bloków, struktura paragrafów pozostaje nienaruszona.

## Przypadki brzegowe i scenariusze „co‑jeśli”

- **Układy wielokolumnowe:** Jeśli źródło ma kolumny, silnik OCR może przeplatać linie. Możesz wykryć współrzędne kolumn z wyjścia TSV i przestawić linie przed wysłaniem ich do AI.
- **Skrypty niełacińskie:** Dla języków takich jak chiński czy arabski, zmień prompt LLM, aby żądał korekty specyficznej dla języka, lub użyj modelu wytrenowanego na tym piśmie.
- **Duże dokumenty:** Wysyłanie każdej linii osobno może być wolne. Grupuj linie (np. po 10 na żądanie) i pozwól LLM zwrócić listę wyczyszczonych linii. Pamiętaj o limitach tokenów.
- **Brakujące bloki:** Niektóre silniki OCR zwracają tylko płaską listę słów. W takim przypadku możesz odtworzyć linie, grupując słowa o podobnych wartościach `line_num`.

## Pełny działający przykład

Łącząc wszystko razem, oto pojedynczy plik, który możesz uruchomić od początku do końca. Zastąp symbole zastępcze własnym kluczem API i ścieżką do obrazu.

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