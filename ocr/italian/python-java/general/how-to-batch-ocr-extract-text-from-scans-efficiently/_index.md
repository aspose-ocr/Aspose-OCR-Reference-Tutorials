---
category: general
date: 2026-04-26
description: Come eseguire OCR in batch dei tuoi documenti ed estrarre il testo dalle
  scansioni in Python. Impara il processamento batch passo‑passo con OcrEngine per
  l'output JSON.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- OCR batch processing
- Python OCR automation
- JSON OCR output
language: it
og_description: Come eseguire l'OCR batch dei tuoi file scansionati ed estrarre il
  testo dalle scansioni in un unico script. Codice completo, consigli e gestione dei
  casi limite.
og_title: Come fare OCR in batch – Guida Python veloce
tags:
- OCR
- Python
- Automation
title: Come eseguire OCR in batch – Estrarre testo dalle scansioni in modo efficiente
url: /it/python-java/general/how-to-batch-ocr-extract-text-from-scans-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR in batch – Estrarre testo da scansioni in modo efficiente

Ti sei mai chiesto **come eseguire OCR in batch** su una montagna di PDF scansionati senza perdere la pazienza? Non sei l'unico: gli sviluppatori chiedono continuamente, *“Come posso estrarre testo dalle scansioni in un solo passaggio?”* La buona notizia è che poche righe di Python possono trasformare questo compito noioso in una pipeline fluida e automatizzata.

In questo tutorial percorreremo una soluzione completa, pronta all'uso, che **estrae testo dalle scansioni**, salva i risultati in JSON e fornisce un rapido controllo di coerenza alla fine. Nessun servizio esterno, nessuna magia—solo Python puro, la classe `OcrEngine` e un po' di gestione delle cartelle.

## Cosa otterrai

- Uno script completamente funzionale che **esegue OCR in batch** su qualsiasi cartella di immagini.
- Spiegazioni chiare del *perché* di ogni riga, non solo del *cosa* fa.
- Suggerimenti per gestire cartelle vuote, file non‑immagine e batch di grandi dimensioni.
- Un metodo per verificare che l'output JSON contenga effettivamente il testo estratto.

### Prerequisiti (il minimo indispensabile)

| Requisito | Perché è importante |
|-------------|----------------|
| Python 3.8+ | Sintassi moderna e type hints |
| `OcrEngine` library (or a compatible wrapper) | Funzionalità OCR di base |
| A directory with scanned image files (PNG, JPG, TIFF) | Dati di input |
| Write permissions for the output folder | Salvataggio dei risultati JSON |

Se hai già tutto questo, ottimo—tuffiamoci.

![how to batch OCR workflow](image-placeholder.png){alt="flusso di lavoro per batch OCR"}

## Passo 1 – Inizializzare il motore OCR (come eseguire OCR in batch)

Prima di poter elaborare qualsiasi cosa, abbiamo bisogno di un'istanza del motore OCR. Pensala come il “cervello” che leggerà ogni immagine e produrrà testo. Inizializzarla una sola volta e riutilizzarla per tutto il batch è il modello più efficiente.

```python
# Step 1: Create an OCR engine instance
# The OcrEngine class abstracts the low‑level OCR library (Tesseract, EasyOCR, etc.)
ocr_engine = OcrEngine()
```

> **Perché riutilizzare la stessa istanza?**  
> Creare un nuovo motore per ogni file caricherebbe ripetutamente modelli pesanti in memoria, rallentando drasticamente il batch. Un'istanza mantiene il modello in RAM e ti permette di elaborare migliaia di immagini senza un rallentamento evidente.

## Passo 2 – Indicare la cartella delle scansioni (estrarre testo dalle scansioni)

Le tue scansioni sono salvate da qualche parte sul disco. Diciamo allo script dove trovarle. L'uso di percorsi assoluti evita sorprese del tipo “file non trovato” quando lo script viene avviato da una directory di lavoro diversa.

```python
import os

# Step 2: Specify the folder that contains scanned images
# Replace YOUR_DIRECTORY with the actual base path on your machine.
input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
```

> **Consiglio professionale:**  
> Se sei su Windows, le barre oblique (`/`) funzionano perfettamente con `os.path.abspath`, quindi non è necessario eseguire l'escape dei backslash.

## Passo 3 – Scegliere dove salvare i risultati JSON

Probabilmente desideri una cartella ordinata per i risultati OCR. Tenere l'output separato dalla sorgente facilita la pulizia successiva o l'inserimento del JSON in un'altra pipeline.

```python
# Step 3: Specify where the JSON results should be saved
output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
os.makedirs(output_dir, exist_ok=True)   # Ensure the folder exists
```

> **Perché creare la cartella programmaticamente?**  
> Garantisce che lo script non vada in crash se la directory è assente, e `exist_ok=True` rende l'operazione idempotente—puoi eseguire lo script più volte senza errori.

## Passo 4 – Eseguire il processo batch (come eseguire OCR in batch)

Ora il nocciolo della questione: far sì che `ocr_engine` attraversi ogni file in `input_dir`, esegua l'OCR e scriva il JSON in `output_dir`. Il flag `format="json"` indica al motore di serializzare il risultato in modo strutturato, apprezzato dagli strumenti a valle.

```python
# Step 4: Run batch processing to convert all scans to JSON format
ocr_engine.batch_process(
    input_folder=input_dir,
    output_folder=output_dir,
    format="json"
)
```

### Cosa succede dietro le quinte?

1. **Scoperta dei file** – Il motore scansiona `input_folder` in modo ricorsivo, ignorando i file nascosti.
2. **Validazione dei file** – Solo le estensioni immagine supportate (`.png`, `.jpg`, `.tif`, ecc.) vengono inviate al modello OCR.
3. **Esecuzione OCR** – Ogni immagine viene inviata al motore OCR; testo, punteggi di confidenza e dati di layout vengono catturati.
4. **Serializzazione JSON** – Il risultato viene scritto in un file con lo stesso nome base ma estensione `.json` in `output_folder`.

> **Gestione dei casi limite:**  
> - **Cartella vuota:** Il motore registra “No files found” e termina senza errori.  
> - **Immagine corrotta:** Salta il file, registra una voce di errore in `batch_errors.log` e continua.  
> - **Batch enorme (10k+ file):** L'uso della memoria rimane basso perché ogni immagine viene elaborata indipendentemente.

## Passo 5 – Confermare il completamento della conversione

Una semplice istruzione `print` fornisce un feedback immediato nella console. Per pipeline di produzione potresti sostituirla con una chiamata di logging o una notifica email.

```python
# Step 5: Inform the user that the batch conversion has finished
print("Batch conversion complete.")
```

Quando vedi quella riga, puoi ispezionare in sicurezza la cartella `json_output`. Ogni file JSON avrà un aspetto simile a questo:

```json
{
  "file_name": "invoice_001.png",
  "text": "Invoice #001\nDate: 2024‑12‑01\nTotal: $1,234.56",
  "confidence": 0.97,
  "layout": [
    {"line": 1, "bbox": [10, 20, 200, 40]},
    {"line": 2, "bbox": [10, 50, 180, 70]},
    {"line": 3, "bbox": [10, 80, 150, 100]}
  ]
}
```

Ora puoi inserire questi file JSON in un database, un indice di ricerca o qualsiasi strumento di analisi a valle.

## Domande frequenti (e risposte rapide)

**Q: E se devo elaborare PDF invece di immagini?**  
A: Converti ogni pagina PDF in un'immagine prima (ad esempio, usando `pdf2image`) e posiziona i file PNG/JPG risultanti in `input_dir`. La logica di batch OCR rimane invariata.

**Q: Posso cambiare il formato di output in testo semplice?**  
A: Assolutamente. Sostituisci `format="json"` con `format="txt"` e il motore scriverà un file `.txt` contenente solo il testo estratto.

**Q: Le mie scansioni sono in più sottocartelle—lo script ricorrerà?**  
A: Sì. `batch_process` attraversa l'albero delle directory per impostazione predefinita. Se desideri un output piatto, imposta `flatten=True` (se la libreria lo supporta) o post‑processa i nomi dei file JSON.

**Q: Come gestire script non latini?**  
A: Inizializza `OcrEngine` con un parametro di lingua, ad esempio `OcrEngine(lang="spa+eng")`. Il ciclo batch di per sé non richiede modifiche.

## Consigli professionali e insidie comuni

- **La dimensione del batch è importante:** Se noti picchi di CPU, rallenta il processo con un semplice `time.sleep(0.1)` tra i file.
- **Logging:** Sostituisci la chiamata `print` con il modulo `logging` di Python per catturare timestamp e livelli di errore.
- **Collisioni di nomi file:** Se due scansioni condividono lo stesso nome base ma si trovano in sottocartelle diverse, i file JSON si sovrascriveranno. Aggiungi un hash del percorso relativo al nome di output per evitarlo.
- **Perdite di memoria:** Alcuni back‑end OCR mantengono risorse native. Chiama `ocr_engine.close()` alla fine dello script se la libreria fornisce un metodo di pulizia.

## Script completo – Pronto da copiare e incollare

```python
import os
from ocr_engine import OcrEngine   # Replace with the actual import path

def main():
    # Step 1: Initialize the OCR engine (how to batch OCR)
    ocr_engine = OcrEngine()

    # Step 2: Directory with scanned images (extract text from scans)
    input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
    if not os.path.isdir(input_dir):
        raise FileNotFoundError(f"Input folder not found: {input_dir}")

    # Step 3: Destination for JSON results
    output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
    os.makedirs(output_dir, exist_ok=True)

    # Step 4: Run the batch OCR process
    ocr_engine.batch_process(
        input_folder=input_dir,
        output_folder=output_dir,
        format="json"
    )

    # Step 5: Confirmation message
    print("Batch conversion complete.")

if __name__ == "__main__":
    main()
```

**Output console previsto**

```
Scanning folder: /home/user/YOUR_DIRECTORY/scans/
Found 42 image files.
Processing file 1/42: invoice_001.png … done.
Processing file 2/42: receipt_2024-03.jpg … done.
…
Batch conversion complete.
```

Puoi verificare il JSON aprendo qualsiasi file in `json_output` con un editor di testo o caricandolo in Python:

```python
import json, pathlib

sample = pathlib.Path(output_dir) / "invoice_001.json"
data = json.loads(sample.read_text())
print(data["text"])
```

Dovresti vedere il testo OCR‑estratto grezzo stampato nella console.

## Conclusioni

Abbiamo appena illustrato **come eseguire OCR in batch** su un'intera directory di immagini scansionate e **estrarre testo dalle scansioni** in file JSON puliti e leggibili da macchine. L'approccio è deliberatamente semplice: configura il motore una volta, puntalo a una cartella e lascia che la libreria gestisca il lavoro pesante. Da qui puoi:

- Collega il JSON

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}