---
category: general
date: 2026-03-26
description: come eseguire OCR batch in modo efficiente con Python—impara a estrarre
  testo da immagini e conversione OCR di PDF con elaborazione parallela
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: it
og_description: come eseguire OCR batch in modo efficiente—guida passo passo per estrarre
  testo da immagini, conversione OCR di PDF e elaborazione batch OCR usando Python.
og_title: 'come fare OCR in batch: estrazione rapida di testo in parallelo'
tags:
- OCR
- Python
- Parallel Computing
title: 'come eseguire OCR in batch: estrazione rapida di testo in parallelo'
url: /it/python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# come eseguire OCR in batch: estrazione rapida di testo in parallelo

Ti sei mai chiesto **come eseguire OCR in batch** quando hai a disposizione decine di pagine scansionate, screenshot e PDF sparsi? Non sei l'unico—la maggior parte degli sviluppatori si imbatte nello stesso ostacolo: elaborare ogni file uno alla volta diventa un collo di bottiglia doloroso.  

La buona notizia è che puoi avviare una manciata di thread worker, fornire loro tutti i tuoi file e vedere il motore OCR divorare il batch in parallelo. In questo tutorial percorreremo un esempio completo, pronto‑da‑eseguire, che mostra **estrarre testo dalle immagini**, eseguire **conversione OCR di PDF** e sfruttare **elaborazione OCR in parallelo** per la velocità.

> **Cosa otterrai**  
> * Uno script Python pienamente funzionante che elabora un elenco misto di file PNG, TIFF, PDF e JPG in un solo passaggio.  
> * Comprensione del motivo per cui un pool di thread accelera i compiti OCR I/O‑bound.  
> * Suggerimenti per gestire errori, PDF di grandi dimensioni e conteggi di thread personalizzati.  

## Prerequisiti

Prima di immergerci, assicurati di avere:

| Requisito | Motivo |
|-----------|--------|
| Python 3.8+ | Sintassi moderna & `concurrent.futures` |
| libreria `ocr` (o qualsiasi wrapper OCR compatibile) | Fornisce `OcrBatchProcessor` e oggetti risultato |
| Una manciata di file di esempio (PNG, TIFF, PDF, JPG) | Per vedere **estrarre testo dalle immagini** in azione |
| Familiarità di base con i thread (opzionale) | Utile ma non obbligatoria |

Se non hai ancora installato il pacchetto `ocr`, esegui:

```bash
pip install ocr-lib   # replace with the actual package name
```

Ora che l'ambiente è pronto, scomponiamo il problema.

## Passo 1: Importa gli helper e istanzia il processore batch

La prima cosa di cui abbiamo bisogno è un luogo dove raccogliere tutti i job OCR. La classe `OcrBatchProcessor` fa esattamente questo—mette in coda gli item di lavoro e ti restituisce una lista di oggetti `Future`.

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*Perché è importante*: importare `as_completed` ci permette di reagire a ogni job terminato istantaneamente, invece di attendere il file più lento. Questo è il cuore del **batch OCR processing**.

## Passo 2: Regola il pool di worker per l'esecuzione parallela

Di default il processore potrebbe usare un solo thread, il che vanifica lo scopo del batching. Chiediamo esplicitamente quattro worker—sentiti libero di aumentare questo numero fino al numero di core CPU a tua disposizione.

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*Suggerimento*: per compiti I/O‑bound come l'OCR, spesso si ottengono ritorni decrescenti dopo `CPU cores * 2`. Prova qualche valore e scegli il punto ottimale.

## Passo 3: Metti in coda ogni file che vuoi OCRare

Qui aggiungiamo un mix di file immagine e PDF. Il metodo `add` registra semplicemente il percorso; il lavoro reale non inizierà finché non invieremo il batch.

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

Se devi elaborare un'intera cartella, un rapido ciclo `glob` fa al caso tuo:

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## Passo 4: Avvia i job e raccogli i futures

Chiamare `submit_all` dà al processore il via libera. Restituisce una lista di oggetti `Future`—pensali come segnaposto per risultati che appariranno più tardi.

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

A questo punto il motore OCR è occupato in background, ogni thread sta masticando un file.

## Passo 5: Recupera i risultati non appena terminano

Usando `as_completed` iteriamo sui futures nell'ordine in cui finiscono, non nell'ordine in cui li abbiamo inviati. Questo mantiene lo script reattivo, specialmente quando alcuni PDF richiedono più tempo rispetto a semplici PNG.

```python
# Step 5 – retrieve each result as it completes
for future in as_completed(ocr_futures):
    try:
        ocr_result = future.result()          # May raise if the job failed
        print("Batch result:\n", ocr_result.get_text())
    except Exception as exc:
        # Graceful error handling – you can log or retry here
        print(f"An OCR job failed: {exc}")
```

**Output previsto** (troncato per brevità):

```
Batch result:
 The quick brown fox jumps over the lazy dog.
...
Batch result:
 Invoice #12345
 Date: 2026-03-01
 Total: $1,234.56
...
```

Ogni blocco corrisponde alla rappresentazione plain‑text del file originale. Se stai facendo **conversione OCR di PDF**, il testo includerà tutto ciò che il motore OCR è riuscito a decifrare da ogni pagina.

## Gestione dei casi limite e problemi comuni

| Situazione | Cosa controllare | Correzione rapida |
|------------|------------------|-------------------|
| Un'immagine corrotta | `future.result()` solleva `OSError` | Avvolgi in `try/except` (vedi il codice sopra) |
| PDF molto grandi ( > 100 MB ) | Pressione sulla memoria, thread più lenti | Aumenta moderatamente `thread_count` o dividi il PDF in capitoli prima |
| Documenti multilingua | Il modello OCR predefinito può rilevare male | Passa suggerimenti di lingua a `OcrBatchProcessor` se la libreria lo supporta |
| Necessità di preservare il layout | `get_text()` plain perde le colonne | Usa `ocr_result.get_hocr()` o metodo simile sensibile al layout |

### Suggerimento: conteggio personalizzato dei thread in base al tipo di file

Se sai che la maggior parte del carico è costituita da PDF, potresti assegnare più thread a questi e meno a piccoli PNG. Alcune librerie permettono di passare una `priority` per job; altrimenti, puoi creare due batch separati—uno per le immagini, uno per i PDF—e farli girare contemporaneamente.

## Panoramica visiva (opzionale)

![how to batch ocr workflow diagram](https://example.com/ocr-workflow.png "how to batch ocr workflow")

*Il diagramma illustra il flusso dalla scoperta dei file → creazione del batch → esecuzione parallela → aggregazione dei risultati.*

## Script completo da copiare‑incollare

Di seguito trovi l'intero programma, pronto per essere inserito in un file `.py`. Include tutti gli snippet sopra, più un piccolo helper che scopre automaticamente i file supportati in una directory.

```python
#!/usr/bin/env python3
"""
How to Batch OCR – Complete Example
-----------------------------------
This script demonstrates parallel OCR processing of mixed image and PDF files.
It shows how to extract text from images, perform pdf ocr conversion, and
handle errors gracefully.
"""

from concurrent.futures import as_completed
import pathlib, fnmatch, sys
import ocr  # replace with your actual OCR library import

def discover_files(root_dir):
    """Yield paths of supported OCR files under *root_dir*."""
    for path in pathlib.Path(root_dir).rglob("*"):
        if fnmatch.fnmatch(path.suffix.lower(), ".png") \
           or fnmatch.fnmatch(path.suffix.lower(), ".tif") \
           or fnmatch.fnmatch(path.suffix.lower(), ".pdf") \
           or fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
            yield str(path)

def main(directory, workers=4):
    # 1️⃣ Initialise batch processor
    ocr_batch = ocr.OcrBatchProcessor()
    ocr_batch.set_thread_count(workers)

    # 2️⃣ Queue every discovered file
    for file_path in discover_files(directory):
        ocr_batch.add(file_path)

    # 3️⃣ Submit all jobs
    futures = ocr_batch.submit_all()

    # 4️⃣ Process results as they arrive
    for fut in as_completed(futures):
        try:
            result = fut.result()
            print("=== OCR RESULT ===")
            print(result.get_text())
            print("\n---\n")
        except Exception as e:
            print(f"[ERROR] OCR failed for a job: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-files>")
        sys.exit(1)
    main(sys.argv[1])
```

Salva questo come `batch_ocr.py`, puntalo a una cartella contenente le tue scansioni e guarda la console riempirsi di testo estratto.  

### Perché funziona

* **Thread pool** – L'OCR è per lo più in attesa di I/O su disco e chiamate a motori esterni, quindi più thread mantengono la CPU occupata.  
* **`as_completed`** – Ottieni i risultati non appena sono pronti, ideale per feedback UI o pipeline di streaming.  
* **Isolamento degli errori** – Un file difettoso non blocca l'intero batch; il blocco `try/except` isola i fallimenti.

## Conclusione

In sintesi, ora sai **come eseguire OCR in batch** usando `concurrent.futures` di Python insieme a una libreria OCR che supporta l'elaborazione batch. Configurando un modesto pool di thread, mettendo in coda ogni file supportato e recuperando i risultati al volo, ottieni un **processo OCR parallelo** veloce senza sacrificare l'affidabilità.  

Da qui potresti:

* Collegare l'output a un indice di ricerca per un rapido recupero dei documenti.  
* Estendere lo script per scrivere ogni risultato in un file `.txt` accanto all'originale.  
* Sostituire il thread pool integrato con `asyncio` se la tua libreria OCR offre API asincrone.  

Continua a sperimentare—sostituisci Tesseract, Azure Cognitive Services o Google Vision, e vedrai che lo stesso schema si applica. Buon OCR!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}