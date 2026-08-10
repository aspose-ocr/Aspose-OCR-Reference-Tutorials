---
category: general
date: 2026-02-22
description: Erfahren Sie, wie Sie OCR‑Text extrahieren und die OCR‑Genauigkeit mit
  KI‑Nachbearbeitung verbessern. Bereinigen Sie OCR‑Text einfach in Python mit einem
  Schritt‑für‑Schritt‑Beispiel.
draft: false
keywords:
- how to extract OCR
- improve OCR accuracy
- clean OCR text
- OCR post‑processing
- AI OCR enhancement
language: de
og_description: Entdecken Sie, wie Sie OCR‑Text extrahieren, die OCR‑Genauigkeit verbessern
  und OCR‑Text mit einem einfachen Python‑Workflow und KI‑Nachbearbeitung bereinigen.
og_title: Wie man OCR‑Text extrahiert – Schritt‑für‑Schritt‑Anleitung
tags:
- OCR
- AI
- Python
title: Wie man OCR-Text extrahiert – Vollständiger Leitfaden
url: /de/python/general/how-to-extract-ocr-text-complete-guide/
---

a line "Provide ONLY the translated content, no explanations." That's instruction for us, not part of content.

Thus final output should be the same structure with translations.

Make sure to keep placeholders and shortcodes unchanged.

Let's write the translation.

Be careful with markdown formatting: headings with #.

Also ensure we keep the blockquote syntax >.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR‑Text extrahiert – Vollständiges Programmier‑Tutorial

Haben Sie sich schon einmal gefragt, **wie man OCR** aus einem gescannten Dokument extrahiert, ohne am Ende ein Durcheinander aus Tippfehlern und zerbrochenen Zeilen zu erhalten? Sie sind nicht allein. In vielen realen Projekten sieht die Rohausgabe eines OCR‑Engines aus einem wirren Absatz aus, und das Aufräumen fühlt sich wie eine lästige Aufgabe an.  

Die gute Nachricht? Wenn Sie diesem Leitfaden folgen, sehen Sie eine praktische Methode, strukturierte OCR‑Daten zu holen, einen KI‑Post‑Processor auszuführen und mit **sauberem OCR‑Text** zu enden, der bereit für nachgelagerte Analysen ist. Wir gehen auch auf Techniken ein, um **die OCR‑Genauigkeit zu verbessern**, sodass die Ergebnisse beim ersten Mal zuverlässig sind.

In den nächsten Minuten behandeln wir alles, was Sie brauchen: erforderliche Bibliotheken, ein vollständiges ausführbares Skript und Tipps, um häufige Fallstricke zu vermeiden. Keine vagen „siehe die Docs“-Abkürzungen – nur eine komplette, eigenständige Lösung, die Sie kopieren‑einfügen und ausführen können.

## Was Sie benötigen

- Python 3.9+ (der Code verwendet Typ‑Hints, funktioniert aber auch mit älteren 3.x‑Versionen)
- Eine OCR‑Engine, die ein strukturiertes Ergebnis zurückgeben kann (z. B. Tesseract via `pytesseract` mit dem Flag `--psm 1`, oder eine kommerzielle API, die Block‑/Zeilen‑Metadaten liefert)
- Ein KI‑Post‑Processing‑Modell – für dieses Beispiel mocken wir es mit einer einfachen Funktion, Sie können aber auch OpenAI’s `gpt‑4o-mini`, Claude oder jedes andere LLM einsetzen, das Text akzeptiert und bereinigte Ausgabe zurückgibt
- Ein paar Beispielbilder (PNG/JPG), um zu testen

Wenn Sie das alles bereit haben, legen wir los.

## Wie man OCR extrahiert – Erste Abfrage

Der erste Schritt besteht darin, die OCR‑Engine aufzurufen und sie um eine **strukturierte Darstellung** statt eines einfachen Strings zu bitten. Strukturierte Ergebnisse bewahren Block‑, Zeilen‑ und Wortgrenzen, was das spätere Bereinigen erheblich erleichtert.

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

> **Warum das wichtig ist:** Durch das Bewahren von Blöcken und Zeilen vermeiden wir das Rätseln, wo Absätze beginnen. Die Funktion `recognize_structured` liefert uns eine saubere Hierarchie, die wir später einem KI‑Modell zuführen können.

```python
# Demo call – replace with your own image path
structured_result = recognize_structured("sample_scan.png")
print("Before AI:", structured_result.blocks[0].lines[0].text)
```

Das Ausführen des Snippets gibt die erste Zeile exakt so aus, wie die OCR‑Engine sie gesehen hat, was häufig Fehlinterpretationen wie „0cr“ statt „OCR“ enthält.

## OCR‑Genauigkeit mit KI‑Post‑Processing verbessern

Jetzt, wo wir die rohe strukturierte Ausgabe haben, übergeben wir sie einem KI‑Post‑Processor. Ziel ist es, **die OCR‑Genauigkeit** zu steigern, indem häufige Fehler korrigiert, Interpunktion normalisiert und bei Bedarf Zeilen neu segmentiert werden.

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

> **Pro‑Tipp:** Wenn Sie kein LLM‑Abonnement haben, können Sie den Aufruf durch einen lokalen Transformer ersetzen (z. B. `sentence‑transformers` + ein feinabgestimmtes Korrektursmodell) oder sogar einen regelbasierten Ansatz nutzen. Die Kernidee ist, dass die KI jede Zeile isoliert sieht, was meist ausreicht, um **OCR‑Text zu bereinigen**.

```python
# Apply the AI post‑processor
structured_result = run_postprocessor(structured_result)
print("After AI:", structured_result.blocks[0].lines[0].text)
```

Sie sollten jetzt einen deutlich saubereren Satz sehen – Tippfehler ersetzt, überflüssige Leerzeichen entfernt und Interpunktion korrigiert.

## OCR‑Text für bessere Ergebnisse bereinigen

Selbst nach der KI‑Korrektur möchten Sie vielleicht einen letzten Bereinigungsschritt anwenden: nicht‑ASCII‑Zeichen entfernen, Zeilenumbrüche vereinheitlichen und mehrere Leerzeichen zusammenfassen. Dieser zusätzliche Durchlauf stellt sicher, dass die Ausgabe bereit für nachgelagerte Aufgaben wie NLP oder Datenbank‑Import ist.

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

Die Funktion `final_cleanup` liefert Ihnen einen einfachen String, den Sie direkt in einen Suchindex, ein Sprachmodell oder einen CSV‑Export einspeisen können. Da wir die Block‑Grenzen beibehalten haben, bleibt die Absatzstruktur erhalten.

## Sonderfälle & Was‑wenn‑Szenarien

- **Mehrspaltige Layouts:** Wenn Ihre Quelle Spalten enthält, kann die OCR‑Engine Zeilen vermischen. Sie können Spaltenkoordinaten aus der TSV‑Ausgabe ermitteln und Zeilen vor dem Senden an die KI neu anordnen.
- **Nicht‑lateinische Schriften:** Für Sprachen wie Chinesisch oder Arabisch passen Sie den Prompt des LLM an, um sprachspezifische Korrekturen anzufordern, oder nutzen ein auf diese Schriftart feinabgestimmtes Modell.
- **Große Dokumente:** Das Senden jeder Zeile einzeln kann langsam sein. Bündeln Sie Zeilen (z. B. 10 pro Anfrage) und lassen Sie das LLM eine Liste bereinigter Zeilen zurückgeben. Beachten Sie dabei die Token‑Grenzen.
- **Fehlende Blöcke:** Einige OCR‑Engines geben nur eine flache Wortliste zurück. In diesem Fall können Sie Zeilen rekonstruieren, indem Sie Wörter mit ähnlichen `line_num`‑Werten gruppieren.

## Vollständiges funktionsfähiges Beispiel

Hier ist eine einzelne Datei, die Sie von Anfang bis Ende ausführen können. Ersetzen Sie die Platzhalter durch Ihren eigenen API‑Key und den Bildpfad.

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