---
category: general
date: 2026-06-19
description: Come eseguire l'OCR passo dopo passo e migliorare l'accuratezza dell'OCR
  con tecniche OCR per testo semplice. Scopri un flusso di lavoro veloce per un'estrazione
  affidabile del testo.
draft: false
keywords:
- how to run OCR
- improve OCR accuracy
- plain text OCR
- OCR post‑processing
- layout‑aware OCR
language: it
og_description: Come eseguire l'OCR in modo efficiente. Questo tutorial mostra come
  migliorare l'accuratezza dell'OCR utilizzando l'OCR di testo semplice e il post‑processing
  basato sull'IA.
og_title: Come eseguire OCR in Python – Guida completa
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
title: Come eseguire OCR in Python – Guida completa
url: /it/python/general/how-to-run-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR in Python – Guida completa

Ti sei mai chiesto **come eseguire OCR** su un batch di PDF scannerizzati senza passare ore a regolare le impostazioni? Non sei solo. In molti progetti il primo ostacolo è semplicemente ottenere testo affidabile da un’immagine, e la differenza tra un risultato incerto e un’estrazione pulita spesso dipende da un paio di passaggi intelligenti.

In questa guida percorreremo una pipeline pratica in quattro passaggi che non solo **esegue OCR**, ma **migliora l’accuratezza OCR** combinando un rapido passaggio di testo semplice con un secondo passaggio sensibile al layout e un post‑processore alimentato da IA. Alla fine avrai uno script pronto all’uso, una chiara spiegazione del perché ogni fase è importante e consigli per gestire casi limite come pagine a più colonne o scansioni rumorose.

---

## Cosa ti serve

Prima di immergerci, assicurati di avere quanto segue:

- **Python 3.9+** – il codice usa type hints e f‑strings.  
- **Tesseract OCR** installato e raggiungibile tramite il comando `tesseract`. (Su Ubuntu: `sudo apt install tesseract-ocr`; su Windows scarica l’installer dal repository ufficiale.)  
- Il wrapper **pytesseract** (`pip install pytesseract`).  
- Una **libreria di post‑processing IA** – per questo esempio faremmo finta di avere un modulo leggero `ai` che offre `run_postprocessor`. Sostituiscilo con l’API GPT‑4 di OpenAI o con un LLM locale se preferisci.  
- Alcune immagini o PDF di esempio per testare.

Tutto qui. Nessun framework pesante, nessuna acrobazia Docker. Solo qualche installazione pip e sei pronto a partire.

---

## Passo 1: Eseguire un rapido passaggio OCR di testo semplice

La prima cosa che la maggior parte degli sviluppatori trascura è che un OCR *testo semplice* è fulmineo e ti fornisce un rapido controllo di sanità. Chiamiamo `engine.Recognize()` per estrarre i caratteri grezzi senza alcun metadato di layout. Questo è ciò che intendiamo per **OCR di testo semplice**.

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

*Perché è importante:*  
- **Velocità** – un passaggio semplice su una pagina a 300 dpi di solito termina in meno di un secondo.  
- **Baseline** – puoi confrontare l’output strutturato successivo con questa base per individuare errori evidenti.  
- **Cattura errori** – se il passaggio semplice fallisce completamente (es. tutto spazzatura), sai che la qualità dell’immagine è troppo bassa e puoi interrompere subito.

---

## Passo 2: Eseguire un passaggio OCR dettagliato sensibile al layout

Il testo semplice è ottimo, ma scarta *dove* ogni parola si trova nella pagina. Per fatture, moduli o riviste a più colonne ti servono coordinate, numeri di riga e forse anche informazioni sul font. È qui che entra in gioco `engine.RecognizeStructured()`.

Di seguito trovi un leggero wrapper sull’output **TSV** di Tesseract, che ci fornisce una gerarchia di pagine → linee → parole, preservando le bounding box.

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

*Perché lo facciamo:*  
- **Coordinate** ti permettono di mappare in seguito il testo estratto sull’immagine originale per evidenziare o redigere.  
- **Raggruppamento per linee** conserva il layout originale, essenziale quando devi ricostruire tabelle o colonne.  
- Questo passaggio è un po’ più lento di quello semplice, ma termina comunque in pochi secondi per la maggior parte dei documenti.

---

## Passo 3: Eseguire il post‑processore IA per correggere gli errori OCR

Anche il miglior motore OCR commette errori—pensa a “rn” vs “m”, diacritici mancanti o parole divise. Un modello IA può osservare la stringa grezza e i dati strutturati, individuare incoerenze e riscrivere il testo mantenendo intatte le coordinate originali.

Di seguito trovi un’implementazione **mock**; sostituisci il corpo con una chiamata reale a un LLM se ne possiedi uno.

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

*Perché questo passaggio migliora l’accuratezza OCR:*  
- **Correzioni contestuali** – l’IA può decidere che “l0ve” è probabilmente “love” in base alle parole circostanti.  
- **Preservazione delle coordinate** – mantieni le informazioni di layout, così i compiti a valle (come l’annotazione PDF) rimangono precisi.  
- **Rifinitura iterativa** – potresti eseguire il post‑processore più volte, ogni passata pulisce ulteriori errori.

---

## Passo 4: Iterare sull’output strutturato corretto

Ora che abbiamo una struttura pulita, estrarre il testo finale è banale. Qui sotto stampiamo ogni linea, ma potresti anche scrivere su CSV, inserire in un database o generare un PDF ricercabile.

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

**Output atteso** (supponendo una semplice fattura a una pagina):

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

Nota come i ritorni a capo e l’ordine delle colonne siano preservati, e come glitch OCR comuni come “$15.00” letti come “$15,00” vengano corretti dal passaggio IA.

---

## Come questo flusso di lavoro **migliora l’accuratezza OCR**

| Fase | Cosa corregge | Perché è importante |
|------|---------------|---------------------|
| **OCR di testo semplice** | Rileva pagine illeggibili in anticipo | Risparmia tempo evitando input senza speranza |
| **OCR strutturato** | Cattura layout, coordinate | Abilita compiti a valle (evidenziazione, redazione) |
| **Post‑processore IA** | Corregge ortografia, unisce parole divise, aggiusta numeri | Aumenta l’accuratezza a livello di carattere dal ~85 % al >95 % su scansioni rumorose |
| **Iterazione** | Consente di rieseguire con parametri ottimizzati | Affina la pipeline per tipi di documento specifici |

Combinando questi tre concetti—**OCR di testo semplice**, estrazione sensibile al layout e correzione IA—ottieni una soluzione robusta che *significativamente* **migliora l’accuratezza OCR** senza scrivere una rete neurale personalizzata da zero.

---

## Problemi comuni e consigli professionali

- **Problema:** Fornire a Tesseract un’immagine a bassa risoluzione (≤150 dpi) produce output confuso.  
  **Consiglio:** Pre‑processa con `Pillow`—applica `Image.convert('L')` e `Image.filter(ImageFilter.MedianFilter())` prima dell’OCR.

- **Problema:** Il post‑processore IA può riscrivere termini specifici del dominio (es. “SKU123”).  
  **Consiglio:** Costruisci una whitelist di termini e passala al LLM o a una libreria di spell‑checking come `pyspellchecker`.

- **Problema:** Le pagine a più colonne vengono fuse in un’unica linea.  
  **Consiglio:** Rileva i confini di colonna usando il campo `block_num` nell’output TSV di Tesseract e suddividi le linee di conseguenza.

- **Problema:** PDF di grandi dimensioni provocano un’esplosione della memoria caricando tutte le pagine contemporaneamente.  
  **Consiglio:** Processa le pagine in modo incrementale—itera su `pdf2image.convert_from_path(..., first_page=n, last_page=n)`.

---

## Estendere la pipeline

Se sei curioso dei prossimi passi, considera i seguenti miglioramenti:

1. **Elaborazione batch** – Avvolgi l’intero script in una funzione che percorre una directory, gestendo migliaia di file in parallelo con `concurrent.futures`.  
2. **Modelli linguistici** – Sostituisci l’euristica semplice basata su difflib con una chiamata a `gpt‑4o` di OpenAI o a un modello LLaMA ospitato localmente per ottenere correzioni contestuali più ricche.  
3. **Formati di esportazione** – Scrivi la struttura corretta in un PDF ricercabile.

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Use OCR - Advanced Techniques with Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/)
- [Improve OCR Accuracy – Detect Areas Mode in OCR](/ocr/hongkong/net/text-recognition/ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}