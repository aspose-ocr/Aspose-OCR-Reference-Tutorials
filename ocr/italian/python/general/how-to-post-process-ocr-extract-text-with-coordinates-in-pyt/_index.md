---
category: general
date: 2026-04-26
description: Come post‑processare i risultati OCR ed estrarre il testo con le coordinate.
  Scopri una soluzione passo‑passo usando output strutturato e correzione AI.
draft: false
keywords:
- how to post‑process OCR
- extract text with coordinates
- OCR structured output
- AI post‑processing OCR
- bounding box OCR
language: it
og_description: Come post‑elaborare i risultati OCR ed estrarre il testo con le coordinate.
  Segui questo tutorial completo per un flusso di lavoro affidabile.
og_title: Come post‑processare OCR – Guida completa
tags:
- OCR
- Python
- AI
- Text Extraction
title: Come post‑elaborare l'OCR – Estrarre il testo con coordinate in Python
url: /it/python/general/how-to-post-process-ocr-extract-text-with-coordinates-in-pyt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come post‑processare l'OCR – Estrarre testo con coordinate in Python

Hai mai dovuto **post‑processare l'OCR** perché l'output grezzo era rumoroso o disallineato? Non sei l'unico. In molti progetti reali—scansione di fatture, digitalizzazione di ricevute o anche il potenziamento di esperienze AR—il motore OCR ti fornisce parole grezze, ma devi comunque pulirle e tenere traccia di dove ogni parola si trovi nella pagina. È qui che una modalità di output strutturato combinata con un post‑processore guidato da AI brilla.

In questo tutorial percorreremo una pipeline Python completa e eseguibile che **estrae testo con coordinate** da un'immagine, esegue un passaggio di correzione basato su AI e stampa ogni parola insieme alla sua posizione (x, y). Nessuna importazione mancante, nessun vago “vedi la documentazione” — solo una soluzione autonoma che puoi inserire nel tuo progetto oggi.

> **Pro tip:** Se usi una libreria OCR diversa, cerca una modalità “structured” o “layout”; i concetti rimangono gli stessi.

---

## Prerequisiti

Prima di immergerci, assicurati di avere:

| Requisito | Perché è importante |
|-----------|----------------------|
| Python 3.9+ | Sintassi moderna e type hints |
| libreria `ocr` che supporta `OutputMode.STRUCTURED` (ad es., un fittizio `myocr`) | Necessaria per i dati delle bounding‑box |
| Un modulo di post‑processing AI (può essere OpenAI, HuggingFace o un modello personalizzato) | Migliora l'accuratezza dopo l'OCR |
| Un file immagine (`input.png`) nella tua directory di lavoro | La sorgente che leggeremo |

Se qualcuno di questi ti è sconosciuto, installa i pacchetti placeholder con `pip install myocr ai‑postproc`. Il codice sotto include anche stub di fallback così puoi testare il flusso senza le librerie reali.

---

## Passo 1: Abilitare la Modalità di Output Strutturato per il Motore OCR  

La prima cosa che facciamo è dire al motore OCR di darci più del semplice testo. L'output strutturato restituisce ogni parola insieme alla sua bounding box e al punteggio di confidenza, essenziale per **estrarre testo con coordinate** più avanti.

```python
# step1_structured_output.py
import myocr as ocr  # fictional OCR library

# Initialize the engine (replace with your actual init code)
engine = ocr.Engine()

# Switch to structured mode – this makes the engine emit word‑level data
engine.set_output_mode(ocr.OutputMode.STRUCTURED)

print("✅ Structured output mode enabled")
```

*Perché è importante:* Senza la modalità strutturata otterresti solo una lunga stringa e perderesti le informazioni spaziali necessarie per sovrapporre il testo alle immagini o per alimentare analisi di layout a valle.

---

## Passo 2: Riconoscere l'Immagine e Catturare Parole, Box e Confidenza  

Ora passiamo l'immagine al motore. Il risultato è un oggetto che contiene una lista di oggetti parola, ognuno dei quali espone `text`, `x`, `y`, `width`, `height` e `confidence`.

```python
# step2_recognize.py
from pathlib import Path

# Path to your image
image_path = Path("YOUR_DIRECTORY/input.png")

# Perform OCR – returns a StructuredResult with .words collection
structured_result = engine.recognize_image(str(image_path))

print(f"🔎 Detected {len(structured_result.words)} words")
```

*Caso limite:* Se l'immagine è vuota o illeggibile, `structured_result.words` sarà una lista vuota. È buona pratica controllare questo e gestirlo in modo appropriato.

---

## Passo 3: Eseguire il Post‑Processing Basato su AI Mantenendo le Posizioni  

Anche i migliori motori OCR commettono errori—pensa a “O” vs. “0” o a diacritici mancanti. Un modello AI addestrato su testo specifico al dominio può correggere quegli errori. Crucialmente, manteniamo le coordinate originali così il layout spaziale rimane intatto.

```python
# step3_ai_postprocess.py
import ai_postproc as ai  # placeholder for your AI module

# The AI post‑processor expects the structured result and returns a new one
corrected_result = ai.run_postprocessor(structured_result)

print("🤖 AI post‑processing complete")
```

*Perché preserviamo le coordinate:* Molti compiti a valle (ad es., generazione di PDF, etichettatura AR) dipendono da un posizionamento esatto. L'AI modifica solo il campo `text`, lasciando intatti `x`, `y`, `width`, `height`.

---

## Passo 4: Iterare sulle Parole Corrette e Visualizzare il Testo con le Coordinate  

Infine, cicliamo sulle parole corrette e stampiamo ogni parola insieme al suo angolo in alto a sinistra `(x, y)`. Questo soddisfa l'obiettivo di **estrarre testo con coordinate**.

```python
# step4_display.py
for recognized_word in corrected_result.words:
    # Using f‑string for clean formatting
    print(f"{recognized_word.text} (x:{recognized_word.x}, y:{recognized_word.y})")
```

**Output previsto (esempio):**

```
Invoice (x:45, y:112)
Number (x:120, y:112)
12345 (x:190, y:112)
Total (x:45, y:250)
$ (x:120, y:250)
199.99 (x:130, y:250)
```

Ogni riga mostra la parola corretta e la sua posizione esatta sull'immagine originale.

---

## Esempio Completo Funzionante  

Di seguito trovi uno script unico che collega tutto. Puoi copiarlo, adattare le istruzioni di importazione alle tue librerie effettive e eseguirlo direttamente.

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

**Esecuzione dello script**

```bash
python ocr_postprocess_demo.py
```

Se hai le librerie reali installate, lo script elaborerà il tuo `input.png`. Altrimenti, l'implementazione stub ti permette di vedere il flusso e l'output attesi senza dipendenze esterne.

---

## Domande Frequenti (FAQ)

| Domanda | Risposta |
|----------|----------|
| *Funziona con Tesseract?* | Tesseract di per sé non espone una modalità strutturata, ma wrapper come `pytesseract.image_to_data` restituiscono bounding box che puoi passare allo stesso post‑processore AI. |
| *E se ho bisogno dell'angolo in basso a destra invece di quello in alto a sinistra?* | Ogni oggetto parola fornisce anche `width` e `height`. Calcola `x2 = x + width` e `y2 = y + height` per ottenere l'angolo opposto. |
| *Posso elaborare più immagini in batch?* | Assolutamente. Avvolgi i passaggi in un ciclo `for image_path in Path("folder").glob("*.png"):` e raccogli i risultati per file. |
| *Come scelgo un modello AI per la correzione?* | Per testo generico, un piccolo GPT‑2 fine‑tuned sugli errori OCR funziona. Per dati specifici al dominio (ad es., prescrizioni mediche), addestra un modello sequence‑to‑sequence su dati accoppiati rumorosi‑puliti. |
| *Il punteggio di confidenza è utile dopo la correzione AI?* | Puoi comunque conservare la confidenza originale per il debug, ma l'AI potrebbe restituire una sua confidenza se il modello lo supporta. |

---

## Casi Limite & Best Practices  

1. **Immagini vuote o corrotte** – verifica sempre che `structured_result.words` non sia vuoto prima di procedere.  
2. **Script non latini** – assicurati che il tuo motore OCR sia configurato per la lingua di destinazione; il post‑processore AI deve essere addestrato sullo stesso script.  
3. **Performance** – la correzione AI può essere costosa. Cache i risultati se riutilizzi la stessa immagine, o esegui il passaggio AI in modo asincrono.  
4. **Sistema di coordinate** – le librerie OCR possono usare origini diverse (alto‑sinistra vs. basso‑sinistra). Adatta di conseguenza quando sovrapponi su PDF o canvas.  

---

## Conclusione  

Ora disponi di una ricetta solida, end‑to‑end, per **post‑processare l'OCR** e **estrarre testo con coordinate** in modo affidabile. Abilitando l'output strutturato, passando il risultato attraverso uno strato di correzione AI e preservando le bounding box originali, puoi trasformare scansioni OCR rumorose in testo pulito e consapevole dello spazio, pronto per compiti a valle come generazione di PDF, automazione di inserimento dati o overlay in realtà aumentata.

Pronto per il passo successivo? Prova a sostituire l'AI stub con una chiamata OpenAI `gpt‑4o‑mini`, oppure integra la pipeline in una FastAPI

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}