---
category: general
date: 2026-03-28
description: Estrai rapidamente il testo da PNG usando Aspose OCR in Python. Impara
  a convertire il testo delle pagine scansionate con il riconoscimento immagini parallelo
  in Python per risultati ad alte prestazioni.
draft: false
keywords:
- extract text from png
- convert scanned pages text
- parallel image recognition python
- recognize image text python
- async OCR batch processing
- Aspose OCR Python
language: it
og_description: Estrai rapidamente il testo da PNG usando Aspose OCR in Python. Questa
  guida mostra come convertire il testo delle pagine scansionate con il riconoscimento
  di immagini in parallelo in Python, offrendo risultati ad alta velocità.
og_title: Estrai testo da PNG – OCR veloce e parallelo con Python
tags:
- OCR
- Python
- Image Processing
- Concurrency
title: Estrai testo da PNG – OCR veloce e parallelo con Python e Aspose
url: /it/python-java/general/extract-text-from-png-fast-parallel-ocr-with-python-and-aspo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da PNG – OCR parallelo veloce con Python

Ti è mai capitato di **estrarre testo da PNG** e trovare l'OCR a thread singolo dolorosamente lento? Non sei l'unico. Che tu stia digitalizzando una pila di ricevute scannerizzate o trasformando diapositive di lezione in PDF ricercabili, il collo di bottiglia è solitamente il passaggio OCR stesso.  

In questo tutorial ti mostreremo una soluzione completa, pronta‑all‑uso, che **converte il testo delle pagine scannerizzate** in parallelo, usando la modalità batch asincrona di Aspose OCR insieme a `ThreadPoolExecutor` di Python. Alla fine sarai in grado di **recognize image text python**‑style, gestendo decine di immagini in una frazione del tempo che richiederebbe un semplice ciclo.

> **Cosa otterrai**  
> * Uno script completamente funzionante che estrae testo da immagini PNG in modo concorrente.  
> * Comprensione del perché la modalità batch asincrona velocizza le cose.  
> * Suggerimenti per scalare la soluzione a carichi di lavoro più grandi.

## Cosa ti serve

| Prerequisito | Motivo |
|--------------|--------|
| Python 3.9+ | Sintassi moderna e type hints. |
| `aspose-ocr` e `aspose-storage` packages | Forniscono il motore OCR e il caricatore di immagini. |
| Una cartella di file PNG (es. pagine scannerizzate) | Il materiale sorgente che vuoi elaborare. |
| Conoscenza di base della concorrenza in Python | Utile ma non obbligatoria; spiegheremo tutto. |

Puoi installare le librerie Aspose con:

```bash
pip install aspose-ocr aspose-storage
```

> **Consiglio professionale:** Mantieni i pacchetti aggiornati (`pip list --outdated`) per beneficiare degli ultimi miglioramenti di performance.

## Passo 1: Inizializzare il motore Aspose OCR in modalità batch asincrona

La prima cosa che facciamo è creare un'istanza di `OcrEngine` e passare alla **modalità batch asincrona**. Questa modalità accoda internamente le richieste di riconoscimento, permettendo al motore di elaborare più immagini senza bloccare il thread Python.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the OCR engine
ocr_engine = aocr.OcrEngine()
# Enable async batch processing – crucial for parallel speed‑up
ocr_engine.batch_mode = aocr.BatchMode.ASYNC
```

*Perché asincrono?*  
Quando chiami `recognize` in modalità sincrona, la chiamata blocca fino a quando l'immagine non è completamente processata. In modalità asincrona, il motore può iniziare a lavorare sulla prossima immagine mentre quella corrente è ancora in fase di decodifica, sovrapponendo effettivamente I/O e lavoro CPU.

## Passo 2: Elencare i file PNG da elaborare

Qui definiamo la collezione di immagini. In un progetto reale potresti generare questa lista dinamicamente (es. `glob.glob("*.png")`), ma mantenerla esplicita rende l'esempio più facile da seguire.

```python
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]
```

> **Nota:** Sostituisci `YOUR_DIRECTORY` con il percorso reale dove risiedono le tue scansioni PNG. Se hai centinaia di file, considera l'uso di `os.listdir` filtrando per `.png`.

## Passo 3: Scrivere un helper che carica un'immagine e ne restituisce il testo

L'helper astrae il processo a due step di caricamento di un file tramite **Aspose Storage** e poi lo passa al motore OCR. Aggiungere una piccola docstring rende la funzione auto‑documentante—utile per la manutenzione futura.

```python
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the recognized text.
    """
    # Load the image using Aspose Storage (handles many formats)
    img = storage.Image.load(path)
    # Perform OCR; the result object contains the extracted text
    result = ocr_engine.recognize(img)
    return result.text
```

*Perché una funzione separata?*  
Mantiene il codice del thread‑pool pulito e ci permette di riutilizzare la logica altrove (es. in un endpoint Flask). Inoltre, isolare l'I/O semplifica il debug—se un file specifico fallisce, vedrai il nome del file nella traccia dell'eccezione.

## Passo 4: Eseguire il riconoscimento immagine in parallelo con Python usando un Thread Pool

Ora introduciamo `ThreadPoolExecutor`. Per impostazione predefinita avviamo quattro worker, ma puoi regolare `max_workers` in base ai core CPU e alla dimensione del set di immagini.

```python
from concurrent.futures import ThreadPoolExecutor, as_completed

with ThreadPoolExecutor(max_workers=4) as pool:
    # Submit each image to the pool; map futures back to filenames
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    
    # Process results as they finish (order may differ from input order)
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)
```

### Come questo fornisce riconoscimento immagine in parallelo con Python

* **ThreadPoolExecutor** crea un pool di thread worker che ciascuno chiama `recognize_image`.  
* Poiché il motore OCR è in modalità batch asincrona, ogni thread può delegare lavoro al motore rimanendo reattivo.  
* `as_completed` restituisce i future nell'ordine in cui terminano, così ottieni i risultati non appena sono pronti—perfetto per lo streaming di grandi batch.

> **Errore comune:** Usare `max_workers=1` annulla lo scopo del parallelismo. Su una macchina a 8 core, `max_workers=8` spesso offre la migliore resa, ma prova diversi valori per trovare il punto ottimale per il tuo hardware.

## Passo 5: Verificare l'output e gestire i casi limite

Quando esegui lo script, dovresti vedere un blocco di testo per ogni PNG, preceduto dal nome del file:

```
--- YOUR_DIRECTORY/page1.png ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- YOUR_DIRECTORY/page2.png ---
Sed do eiusmod tempor incididunt ut labore et dolore...

--- YOUR_DIRECTORY/page3.png ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

Se qualche immagine fallisce (file corrotto, formato non supportato), il blocco `except` stampa un messaggio d'errore utile invece di far crashare l'intero batch.

### Estendere la soluzione

| Scenario | Suggerimento |
|----------|--------------|
| **Migliaia di pagine** | Passa a `ProcessPoolExecutor` per sfruttare più processi CPU, oppure suddividi la lista e processa i batch sequenzialmente. |
| **Formati immagine diversi (JPG, TIFF)** | Il metodo `storage.Image.load` rileva automaticamente il formato, quindi aggiungi semplicemente i file a `input_images`. |
| **Necessità di salvare i risultati** | Scrivi `text` in un file `.txt` o inseriscilo in un database dentro il blocco `else`. |
| **Monitoraggio delle performance** | Avvolgi `recognize_image` con un timer (`time.perf_counter`) e registra la durata per file. |

## Esempio completo funzionante (pronto per copia‑incolla)

Di seguito lo script completo, pronto per essere inserito in un file chiamato `parallel_ocr.py`. Nessuna parte è mancante—tutto ciò di cui hai bisogno è qui.

```python
# parallel_ocr.py
import aspose.ocr as aocr
import aspose.storage as storage
from concurrent.futures import ThreadPoolExecutor, as_completed

# -------------------------------------------------
# Step 1: Initialize OCR engine in async batch mode
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.batch_mode = aocr.BatchMode.ASYNC   # enable asynchronous batch processing

# -------------------------------------------------
# Step 2: Define the PNG files you want to recognize
# -------------------------------------------------
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]

# -------------------------------------------------
# Step 3: Helper that loads an image and returns the recognized text
# -------------------------------------------------
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the OCR‑extracted text.
    """
    img = storage.Image.load(path)
    result = ocr_engine.recognize(img)
    return result.text

# -------------------------------------------------
# Step 4: Run OCR on all images concurrently using a thread pool
# -------------------------------------------------
with ThreadPoolExecutor(max_workers=4) as pool:
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)

# -------------------------------------------------
# Step 5: Output is printed to the console.
# -------------------------------------------------
```

Salva il file, regola il segnaposto `YOUR_DIRECTORY` e esegui:

```bash
python parallel_ocr.py
```

Dovresti vedere il testo estratto per ogni PNG apparire nella console, proprio come mostrato in precedenza.

## Conclusione

Abbiamo appena dimostrato come **estrarre testo da PNG** in modo efficiente combinando la modalità batch asincrona di Aspose OCR con `ThreadPoolExecutor` di Python. Lo script converte il testo delle pagine scannerizzate in parallelo, offrendoti un modo scalabile per **recognize image text python**‑style senza scrivere un thread‑pool personalizzato da zero.  

Se sei pronto a spingere oltre, prova:

* Salvare i risultati in un database SQLite ricercabile.  
* Aggiungere pre‑elaborazione dell'immagine (deskew, denoise) con OpenCV prima dell'OCR.  
* Distribuire lo script come microservizio dietro un endpoint Flask o FastAPI.

Ricorda, la chiave per un OCR ad alte prestazioni non è solo un motore più veloce—è anche fornire al motore lavoro in modo da massimizzare la concorrenza. Con il pattern mostrato qui, puoi gestire decine o anche centinaia di scansioni PNG con minime modifiche al codice.

Buona programmazione, e che i tuoi PDF siano sempre ricercabili!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}