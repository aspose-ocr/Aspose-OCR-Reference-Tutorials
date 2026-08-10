---
category: general
date: 2026-06-25
description: Estrai il testo dalle immagini con la libreria Python aocr – impara l'OCR
  batch, imposta la modalità di riconoscimento stampato e aggiungi un post‑processore
  AI.
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: it
og_description: Estrai il testo dalle immagini usando la libreria Python aocr. Questo
  tutorial mostra l'OCR batch, la modalità di riconoscimento di testo stampato e il
  postprocessore AI opzionale.
og_title: Estrai testo dalle immagini in Python – Guida completa batch aocr
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: Estrai il testo dalle immagini in Python usando aocr OCR Batch
url: /it/python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai Testo dalle Immagini in Python Usando aocr OCR Batch

Hai mai dovuto **estrarre testo dalle immagini** ma ti sei sentito sopraffatto da dozzine di piccoli passaggi? Non sei l'unico. Che tu stia digitalizzando moduli scansionati, estraendo dati da ricevute o creando un archivio ricercabile, ottenere risultati OCR affidabili su larga scala può sembrare una scalata ripida.

La buona notizia? Con la **libreria aocr** puoi avviare un **batch OCR Python** completo in poche righe. In questa guida vedremo come creare un batch OCR, caricare tutte le immagini supportate da una cartella, scegliere la giusta **modalità di riconoscimento printed**, e persino collegare un **post‑processore AI** per quel ulteriore boost di precisione. Alla fine avrai uno script pronto all'uso che estrae testo dalle immagini e ti indica quanto è stato catturato per file.

## Cosa Imparerai

- Come installare e importare il pacchetto `aocr`.
- Configurare un `OcrBatch` per gestire migliaia di file automaticamente.
- Scegliere la modalità di riconoscimento ottimale per documenti stampati.
- (Facoltativo) Collegare un post‑processore AI per pulire i risultati rumorosi.
- Visualizzare ogni percorso file accanto alla lunghezza del testo estratto.
- Suggerimenti per gestire casi limite come formati non supportati o pagine vuote.

### Prerequisiti

- Python 3.8 o versioni successive installato sulla tua macchina.  
- Familiarità di base con gli script Python (cicli, import, ecc.).  
- Accesso a una cartella di immagini scansionate (PNG, JPG, TIFF, ecc.).  

Se hai tutto questo, immergiamoci—nessun servizio esterno richiesto.

## Passo 1: Installa la Libreria aocr

Prima di tutto. Il pacchetto `aocr` non fa parte della libreria standard, quindi dovrai scaricarlo da PyPI.

```bash
pip install aocr
```

> **Consiglio esperto:** Usa un ambiente virtuale (`python -m venv .venv`) per tenere le dipendenze isolate.  

Una volta installato, puoi importare le classi principali.

```python
# core imports
import aocr
```

## Passo 2: Crea un'Istanza OCR Batch

Un `OcrBatch` è il cavallo di battaglia che scandirà la tua directory e terrà traccia di ogni file immagine. Pensalo come un nastro trasportatore che alimenta le foto al motore OCR.

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

A questo punto il batch è vuoto, ma lo riempiremo nel passo successivo.

## Passo 3: Aggiungi Tutte le Immagini Supportate da una Cartella (Ricorsivamente)

Probabilmente hai una struttura di cartelle nidificate—magari una sottocartella per cliente o per mese. Il metodo `add_folder` percorre l'albero per te, includendo ogni immagine che sa leggere.

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

Sostituisci `"YOUR_DIRECTORY/scanned_forms/"` con il percorso reale sul tuo sistema. Dopo questa chiamata `ocr_batch.file_paths` contiene una lista di nomi file assoluti, e il batch sa esattamente quanti elementi dovrà elaborare.

## Passo 4: Scegli la Modalità di Riconoscimento per Testo Stampato

Il motore `aocr` supporta diverse modalità (handwritten, printed, mixed). Poiché stiamo trattando moduli puliti e stampati, imposta la modalità di conseguenza. Questa piccola opzione può migliorare drasticamente la precisione perché il motore evita le heuristics pesanti necessarie per la scrittura corsiva.

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **Perché è importante:** Il testo stampato ha linee di base e forme dei caratteri coerenti, permettendo al modello OCR di applicare dizionari di caratteri più ristretti. Se lasci la modalità su “auto” potresti ottenere rumore extra su scansioni a bassa risoluzione.

## Passo 5: (Facoltativo) Collega un Post‑Processore AI

Se le tue scansioni soffrono di sfocatura, basso contrasto o font insoliti, un post‑processore AI può pulire l'output OCR grezzo prima di passarlo ai sistemi a valle. Il metodo `set_ai_postprocessor` si aspetta un oggetto che implementi un’interfaccia `process(text: str) -> str`.

Di seguito un esempio minimale usando una classe fittizia `SimpleCleaner`. In pratica potresti collegare un transformer HuggingFace, un modello linguistico personalizzato, o anche un correttore ortografico basato su regole.

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

Se salti questo passo, il batch restituirà semplicemente le stringhe OCR grezze.

## Passo 6: Esegui l'OCR su Tutto il Batch e Raccogli i Risultati

Ora inizia il lavoro pesante. Il metodo `run` itera su ogni file, esegue il motore OCR, passa l'output attraverso il post‑processore AI opzionale, e restituisce una lista di stringhe—una per immagine.

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

Poiché il metodo restituisce una semplice lista Python, puoi trattarla come qualsiasi altra collezione—memorizzarla, scriverla in un CSV, o inserirla in un database.

## Passo 7: Visualizza Ogni Percorso File con la Lunghezza del Testo Estratto

Un rapido controllo di sanità è stampare quanti caratteri sono stati estratti da ciascun file. Se una pagina è vuota o l'OCR è fallito, vedrai una lunghezza di `0`.

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

Un output tipico appare così:

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

Vedere subito un flag `0` ti indica immediatamente quali file necessitano di una seconda occhiata (forse sono corrotti o non sono affatto immagini).

## Gestione dei Casi Limite Comuni

### 1. Tipi di File Non Supportati

`aocr` ignora silenziosamente i file che non può decodificare. Se sospetti di avere PDF o BMP mescolati, filtrali in anticipo:

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. Batch di Grandi Dimensioni e Consumo di Memoria

Elaborare migliaia di scansioni ad alta risoluzione può far crescere l'uso di memoria. Mitiga il problema processando a blocchi:

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. Pagine Vuote o a Basso Contrasto

Se una pagina produce meno di 10 caratteri, potresti volerla segnalare per una revisione manuale:

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## Esempio Completo Funzionante

Mettendo tutto insieme, ecco uno script che puoi copiare‑incollare ed eseguire subito. Salvalo come `batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**Output previsto** (troncato per brevità):

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

Eseguilo con:

```bash
python batch_ocr.py
```

Se tutto è configurato correttamente, vedrai una riga per ogni immagine, ciascuna con il conteggio dei caratteri del testo estratto.

## Domande Frequenti

**D: Questo funziona sui PDF?**  
R: Non direttamente. `aocr` gestisce solo immagini raster. Converte i PDF in PNG/TIFF prima (ad esempio con `pdf2image`).

**D: Posso cambiare la modalità di riconoscimento in handwritten?**  
R: Assolutamente—basta sostituire `aocr.RecognitionMode.PRINTED` con `aocr.RecognitionMode.HANDWRITTEN`. Aspettati un tempo di esecuzione più lento ma risultati migliori su note corsive.

**D: E se ho bisogno di supporto multilingue?**  
R: La libreria include pacchetti linguistici. Installa il modulo lingua desiderato (`pip install aocr-lang-fr` per il francese, ecc.) e imposta `ocr_batch.language = "fr"` prima di eseguire.

## Prossimi Passi e Argomenti Correlati

- **Elaborazione parallela:** Avvolgi l'esecuzione del batch in un `concurrent.futures.ThreadPoolExecutor` per sfruttare più core CPU.  
- **Salvataggio dei risultati:** Scrivi `ocr_results` in un CSV o in un database SQLite per analisi successive.  
- **Integrazione con AI cloud:** Sostituisci `SimpleCleaner` con un modello transformer di HuggingFace per una correzione ortografica all'avanguardia.  
- **Fine‑tuning di aocr:** Se disponi di un set di font personalizzato, esplora `aocr.Trainer` per migliorare la precisione in modalità printed.

---

Questo è tutto—ora hai una base solida


## Cosa Dovresti Imparare Dopo?


I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci alternativi nei tuoi progetti.

- [Estrai Testo da Immagine con Aspose OCR – Guida Passo‑Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Estrai Testo da Immagini Usando l'Operazione OCR su Cartelle](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Come Eseguire OCR Batch su Immagini con Lista in Aspose.OCR per .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}