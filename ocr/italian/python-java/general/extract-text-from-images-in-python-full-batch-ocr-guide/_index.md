---
category: general
date: 2026-06-19
description: Estrai il testo dalle immagini in Python con un semplice motore OCR.
  Scopri come convertire le immagini scannerizzate in testo, riconoscere il testo
  dalle foto e elencare i file immagine in Python in modo efficiente.
draft: false
keywords:
- extract text from images
- convert scanned images to text
- recognize text from pictures
- list image files python
language: it
og_description: Estrai testo dalle immagini in Python usando un motore OCR leggero.
  Questa guida ti mostra come convertire immagini scannerizzate in testo, riconoscere
  il testo dalle foto e elencare i file immagine in Python in pochi passaggi.
og_title: Estrai testo dalle immagini in Python – Guida completa all'OCR batch
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Extract text from images in Python with a simple OCR engine. Learn
    how to convert scanned images to text, recognize text from pictures, and list
    image files python efficiently.
  headline: Extract Text from Images in Python – Full Batch OCR Guide
  type: TechArticle
tags:
- Python
- OCR
- Image Processing
title: Estrai testo dalle immagini in Python – Guida completa all'OCR batch
url: /it/python-java/general/extract-text-from-images-in-python-full-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrarre Testo da Immagini in Python – Guida Completa all'OCR di Massa

Hai mai dovuto **estrarre testo da immagini** ma non sapevi da dove cominciare? Non sei solo: gli sviluppatori affrontano costantemente la sfida di trasformare PDF scansionati, ricevute fotografate o screenshot in testo ricercabile. In questo tutorial percorreremo un esempio completo, pronto‑all'uso, che mostra come **convertire immagini scansionate in testo**, riconoscere il testo dalle foto e persino **list image files python**. Alla fine avrai uno script riutilizzabile che elabora un’intera cartella in un solo passaggio.

Copriamo tutto ciò di cui hai bisogno: librerie richieste, perché ogni passaggio è importante, gestione dei casi limite e un po' di troubleshooting. Non è necessario consultare documentazione esterna; il codice qui sotto è autonomo e le spiegazioni rispondono al “come” *e* al “perché”. Apri il tuo IDE preferito e cominciamo.

---

## Cosa Costruirai

- Inizializzare un motore OCR (useremo il pacchetto `ocr` a scopo illustrativo).
- Scansionare una directory e **list image files python**, filtrando PNG, JPG e TIFF.
- Eseguire un’operazione **batch OCR** su tutte le immagini trovate.
- Stampare il testo estratto per ogni file, con etichetta chiara.

> **Consiglio professionale:** Se non hai la libreria `ocr` installata, puoi sostituirla con `pytesseract` con poche modifiche minori – la logica di base rimane invariata.

---

## Prerequisiti

- Python 3.8+ (lo script usa f‑strings e type hints).
- Una libreria OCR che esponga un `OcrEngine` con `recognize_batch`. Per questa guida assumiamo un pacchetto fittizio `ocr`, ma il modello funziona anche con librerie reali.
- Una cartella contenente i file immagine da elaborare (`.png`, `.jpg`, `.tif`).

---

## Passo 1 – Installa & Importa i Moduli Necessari

Per prima cosa, assicurati che il pacchetto OCR sia disponibile. Se usi una libreria reale come `pytesseract`, sostituisci l’importazione di conseguenza.

```python
# Install the fictional OCR package (skip if using pytesseract)
# pip install ocr-package

import os
import ocr  # <-- replace with your actual OCR library
from typing import List
```

> **Perché è importante:** L’importazione di `os` fornisce una gestione dei percorsi cross‑platform, mentre `typing.List` aiuta l’autocompletamento nell’IDE e rende il codice più robusto per il futuro.

---

## Passo 2 – **Extract Text from Images**: Inizializza il Motore OCR

Creare il motore è il primo passo per qualsiasi lavoro di OCR. Impostiamo anche la lingua su auto‑rilevamento così il motore può gestire documenti multilingua.

```python
def create_engine() -> ocr.OcrEngine:
    """
    Initializes the OCR engine with automatic language detection.
    Returns:
        An instance of ocr.OcrEngine ready for batch processing.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto  # Auto‑detect language
    return engine
```

> **Spiegazione:** Incapsulando la creazione del motore in una funzione manteniamo il codice modulare. Se in seguito dovrai modificare DPI o modalità OCR, dovrai intervenire solo in questo punto.

---

## Passo 3 – **List Image Files Python**: Raccogli i File da una Directory

Ora dobbiamo individuare ogni immagine da elaborare. La list comprehension qui sotto rispecchia il tipico pattern “list image files python”.

```python
def get_image_files(input_dir: str) -> List[str]:
    """
    Scans `input_dir` and returns a list of absolute paths
    for files ending with .png, .jpg, or .tif (case‑insensitive).
    """
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]
```

> **Gestione dei casi limite:** La funzione ignora le sotto‑cartelle (puoi aggiungere ricorsione in seguito) e filtra automaticamente i file nascosti perché tipicamente non terminano con le estensioni supportate.

---

## Passo 4 – **Convert Scanned Images to Text**: Esegui il Batch OCR

La maggior parte delle librerie OCR fornisce un metodo batch molto più veloce rispetto all’elaborazione immagine per immagine. Ecco come lo invochiamo.

```python
def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    """
    Sends a list of image file paths to the OCR engine for batch recognition.
    Returns a list of OcrResult objects, preserving order.
    """
    # The fictional `recognize_batch` returns a list of results matching input order
    return engine.recognize_batch(image_paths)
```

> **Perché batch?** Inviare tutte le immagini in una volta riduce l’overhead (ad es., il caricamento ripetuto del modello OCR) e spesso migliora l’utilizzo di CPU/GPU.

---

## Passo 5 – **Recognize Text from Pictures**: Visualizza i Risultati

Infine, iteriamo sui nomi dei file associati ai risultati OCR, stampando un’intestazione pulita per ogni immagine.

```python
def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    """
    Prints the extracted text for each image, prefixed with the file name.
    """
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        # Some OCR engines store the plain text in a `.text` attribute
        print(result.text.strip())
        print()  # Blank line for readability
```

> **Suggerimento:** `strip()` rimuove gli spazi bianchi iniziali/finali che l’OCR aggiunge spesso.

---

## Script Completo – Metti Tutto Insieme

Di seguito trovi il programma completo, eseguibile. Salvalo come `batch_ocr.py` ed esegui `python batch_ocr.py <your_folder>`.

```python
#!/usr/bin/env python3
"""
Batch OCR script – extracts text from images in a given folder.
Usage: python batch_ocr.py /path/to/images
"""

import sys
import os
import ocr  # Replace with your OCR library if different
from typing import List

def create_engine() -> ocr.OcrEngine:
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto
    return engine

def get_image_files(input_dir: str) -> List[str]:
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]

def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    return engine.recognize_batch(image_paths)

def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        print(result.text.strip())
        print()

def main() -> None:
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <input_directory>")
        sys.exit(1)

    input_dir = sys.argv[1]

    if not os.path.isdir(input_dir):
        print(f"Error: '{input_dir}' is not a valid directory.")
        sys.exit(1)

    engine = create_engine()
    image_files = get_image_files(input_dir)

    if not image_files:
        print("No supported image files found in the directory.")
        sys.exit(0)

    ocr_results = run_batch_ocr(engine, image_files)
    display_results(image_files, ocr_results)

if __name__ == "__main__":
    main()
```

### Output Atteso

Supponendo che la cartella contenga `invoice1.png` e `receipt.jpg`, potresti vedere:

```
--- invoice1.png ---
Invoice #12345
Date: 2024‑04‑01
Total: $256.78

--- receipt.jpg ---
Store: Coffee Corner
Item: Latte
Price: $4.50
```

Ogni blocco è chiaramente etichettato, rendendo semplice l’elaborazione successiva (ad es., salvataggio in un database).

---

## Gestione dei Problemi Comuni

| Problema | Perché Accade | Soluzione Rapida |
|----------|----------------|------------------|
| **Nessun testo appare** | Lingua OCR non rilevata o immagine a basso contrasto. | Forza una lingua (`engine.language = ocr.Language.English`) o pre‑elabora le immagini (aumenta il contrasto). |
| **Errore di memoria su batch grandi** | Il motore tenta di caricare tutte le immagini contemporaneamente. | Dividi `image_files` in blocchi (`batch_size = 20`) e chiama `recognize_batch` più volte. |
| **Formato file non supportato** | Hai aggiunto un `.gif` o `.bmp`. | Estendi la tupla `supported_exts` o converti le immagini in PNG/JPG prima. |
| **Caratteri Unicode corrotti** | L’OCR restituisce byte anziché stringhe. | Assicurati che la libreria OCR restituisca Unicode (`result.text.decode('utf‑8')` se necessario). |

---

## Estendere il Flusso di Lavoro

Ora che sai **extract text from images**, considera i prossimi passi:

- **Esporta in CSV** – Scrivi ogni nome file e il relativo testo estratto in un foglio di calcolo per analisi.
- **Elaborazione parallela** – Usa `concurrent.futures.ThreadPoolExecutor` per gestire più batch contemporaneamente.
- **Integra con OCR cloud** – Sostituisci il motore locale con Google Vision o Azure OCR per maggiore precisione su layout complessi.
- **Aggiungi pre‑elaborazione immagini** – Librerie come Pillow o OpenCV possono deskew, denoise o threshold le immagini prima dell’OCR, migliorando i risultati.

Tutte queste idee utilizzano le stesse funzioni di base che abbiamo costruito, quindi non dovrai ricominciare da zero.

---

## Conclusione

Abbiamo appena percorso una soluzione completa per **extract text from images** in Python, coprendo tutto, da **list image files python** a **recognize text from pictures** fino a **convert scanned images to text** in un batch ordinato. Lo script è deliberatamente semplice ma sufficientemente flessibile da fungere da base per progetti più grandi—che tu stia digitalizzando ricevute, creando un archivio ricercabile o alimentando una pipeline di estrazione dati.

Provalo, modifica i passaggi di pre‑elaborazione e osserva come la precisione dell’OCR migliora. Se incontri intoppi, ricontrolla la tabella “Gestione dei Problemi Comuni”; la maggior parte dei problemi si risolve con una piccola modifica di configurazione.

Pronto per la prossima sfida? Prova ad aggiungere una fase di conversione PDF‑to‑image usando `pdf2image`, poi alimenta quelle immagini direttamente nello stesso flusso. Il cielo è il limite quando combini OCR e l’ecosistema ricco di Python.

Buon coding, e che il tuo testo sia sempre leggibile!

## Cosa Dovresti Imparare Dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci alternativi nei tuoi progetti.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}