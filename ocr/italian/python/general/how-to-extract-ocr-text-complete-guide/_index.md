---
category: general
date: 2026-02-22
description: Scopri come estrarre il testo OCR e migliorare l'accuratezza OCR con
  il post‑processing basato sull'IA. Pulisci facilmente il testo OCR in Python con
  un esempio passo‑passo.
draft: false
keywords:
- how to extract OCR
- improve OCR accuracy
- clean OCR text
- OCR post‑processing
- AI OCR enhancement
language: it
og_description: Scopri come estrarre il testo OCR, migliorare l'accuratezza OCR e
  pulire il testo OCR utilizzando un semplice flusso di lavoro Python con post‑elaborazione
  AI.
og_title: Come estrarre il testo OCR – Guida passo passo
tags:
- OCR
- AI
- Python
title: Come estrarre il testo OCR – Guida completa
url: /it/python/general/how-to-extract-ocr-text-complete-guide/
---

We keep them.

Now produce final output with translated content.

Be careful to keep markdown formatting.

Let's write final.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come Estrarre Testo OCR – Tutorial di Programmazione Completo

Ti sei mai chiesto **come estrarre OCR** da un documento scansionato senza finire con un caos di errori di battitura e righe interrotte? Non sei solo. In molti progetti reali l'output grezzo di un motore OCR appare come un paragrafo confuso, e pulirlo sembra un compito noioso.  

La buona notizia? Seguendo questa guida vedrai un modo pratico per ottenere dati OCR strutturati, eseguire un post‑processore AI e ottenere **testo OCR pulito** pronto per l'analisi a valle. Tratteremo anche tecniche per **migliorare l'accuratezza OCR** così i risultati saranno affidabili al primo tentativo.

Nei prossimi minuti copriremo tutto ciò di cui hai bisogno: librerie richieste, uno script completo eseguibile e consigli per evitare gli errori più comuni. Niente scorciatoie vaghe tipo “vedi la documentazione” — solo una soluzione completa e autonoma che puoi copiare‑incollare ed eseguire.

## Cosa Ti Serve

- Python 3.9+ (il codice usa type hints ma funziona anche su versioni 3.x più vecchie)
- Un motore OCR che possa restituire un risultato strutturato (ad es. Tesseract via `pytesseract` con il flag `--psm 1`, o un'API commerciale che fornisce metadati di blocco/riga)
- Un modello di post‑processing AI – per questo esempio lo simuleremo con una semplice funzione, ma puoi sostituirlo con `gpt‑4o-mini` di OpenAI, Claude o qualsiasi LLM che accetti testo e restituisca output pulito
- Alcune righe di immagine di esempio (PNG/JPG) su cui testare

Se hai tutto pronto, immergiamoci.

## Come Estrarre OCR – Recupero Iniziale

Il primo passo è chiamare il motore OCR e chiedergli una **rappresentazione strutturata** invece di una semplice stringa. I risultati strutturati preservano i confini di blocchi, righe e parole, rendendo la pulizia successiva molto più semplice.

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

> **Perché è importante:** Preservando blocchi e righe evitiamo di dover indovinare dove iniziano i paragrafi. La funzione `recognize_structured` ci fornisce una gerarchia pulita che possiamo poi passare a un modello AI.

```python
# Demo call – replace with your own image path
structured_result = recognize_structured("sample_scan.png")
print("Before AI:", structured_result.blocks[0].lines[0].text)
```

Eseguire lo snippet stampa la prima riga esattamente come l'ha vista il motore OCR, che spesso contiene errori di riconoscimento come “0cr” al posto di “OCR”.

## Migliorare l'Accuratezza OCR con il Post‑Processing AI

Ora che abbiamo l'output strutturato grezzo, lo passiamo a un post‑processore AI. L'obiettivo è **migliorare l'accuratezza OCR** correggendo errori comuni, normalizzando la punteggiatura e persino risegmentando le righe quando necessario.

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

> **Consiglio professionale:** Se non disponi di un abbonamento LLM, puoi sostituire la chiamata con un transformer locale (ad es. `sentence‑transformers` + un modello di correzione fine‑tuned) o anche con un approccio basato su regole. L'idea chiave è che l'AI vede ogni riga in isolamento, il che è di solito sufficiente per **pulire il testo OCR**.

```python
# Apply the AI post‑processor
structured_result = run_postprocessor(structured_result)
print("After AI:", structured_result.blocks[0].lines[0].text)
```

Ora dovresti vedere una frase molto più pulita — errori di battitura corretti, spazi extra rimossi e punteggiatura sistemata.

## Pulire il Testo OCR per Risultati Migliori

Anche dopo la correzione AI, potresti voler applicare un passaggio finale di sanitizzazione: rimuovere caratteri non‑ASCII, uniformare le interruzioni di riga e comprimere spazi multipli. Questo passaggio extra garantisce che l'output sia pronto per attività a valle come NLP o ingestione in un database.

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

La funzione `final_cleanup` ti restituisce una stringa semplice che puoi alimentare direttamente in un indice di ricerca, un modello linguistico o un'esportazione CSV. Poiché abbiamo mantenuto i confini dei blocchi, la struttura dei paragrafi rimane preservata.

## Casi Limite e Scenari “What‑If”

- **Layout a più colonne:** Se la tua sorgente ha colonne, il motore OCR potrebbe intercalare le righe. Puoi rilevare le coordinate delle colonne dall'output TSV e riordinare le righe prima di inviarle all'AI.
- **Script non latini:** Per lingue come cinese o arabo, modifica il prompt dell'LLM per richiedere correzioni specifiche della lingua, o usa un modello fine‑tuned su quello script.
- **Documenti di grandi dimensioni:** Inviare ogni riga singolarmente può essere lento. Raggruppa le righe (ad es. 10 per richiesta) e lascia che l'LLM restituisca una lista di righe pulite. Ricorda di rispettare i limiti di token.
- **Blocchi mancanti:** Alcuni motori OCR restituiscono solo una lista piatta di parole. In tal caso, puoi ricostruire le righe raggruppando le parole con valori `line_num` simili.

## Esempio Completo Funzionante

Mettendo tutto insieme, ecco un unico file che puoi eseguire end‑to‑end. Sostituisci i segnaposto con la tua chiave API e il percorso dell'immagine.

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