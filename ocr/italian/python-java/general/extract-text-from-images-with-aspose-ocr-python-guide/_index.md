---
category: general
date: 2026-03-18
description: Scopri come estrarre il testo dalle immagini e convertire il testo delle
  immagini scannerizzate in stringhe modificabili usando Aspose OCR in Python. Codice
  passo‑passo incluso.
draft: false
keywords:
- extract text from images
- convert scanned images text
- Aspose OCR Python
- batch OCR processing
- image to text conversion
language: it
og_description: Estrai il testo dalle immagini usando Aspose OCR in Python. Questo
  tutorial mostra come convertire il testo delle immagini scansionate in poche righe
  di codice.
og_title: Estrai testo dalle immagini con Aspose OCR – Guida Python
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Estrai il testo dalle immagini con Aspose OCR – Guida Python
url: /it/python-java/general/extract-text-from-images-with-aspose-ocr-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo dalle immagini con Aspose OCR – Guida Python

Hai mai avuto bisogno di **estrarre testo dalle immagini** ma non sapevi da dove cominciare? Non sei l'unico: gli sviluppatori si trovano spesso a dover trasformare PDF scansionati, screenshot rumorosi o ricevute fotografate in stringhe ricercabili e modificabili.  

La buona notizia? Con Aspose OCR per Python puoi **convertire il testo delle immagini scansionate** in blocco, il tutto senza uscire dal tuo IDE. In questo tutorial ti guideremo attraverso un esempio completo, pronto‑da‑eseguire, che mostra esattamente come fare, perché ogni passaggio è importante e a cosa fare attenzione.

## Cosa imparerai

- Configurare la libreria Aspose OCR in un ambiente Python.  
- Preparare un elenco di file immagine (PNG, JPG, TIFF, ecc.).  
- Eseguire OCR batch con una singola chiamata di metodo.  
- Accedere e visualizzare il testo estratto per ciascun file.  
- Gestire le difficoltà comuni come formati non supportati e l'uso di memoria per file di grandi dimensioni.  

Al termine, avrai uno script riutilizzabile che può **estrarre testo dalle immagini** su richiesta—perfetto per automatizzare l'inserimento dati, indicizzare documenti o alimentare pipeline NLP a valle.

---

![Esempio di estrazione testo dalle immagini](/images/ocr-extract-text.png "estrazione testo dalle immagini")

*Testo alternativo dell'immagine: “estrarre testo dalle immagini usando Aspose OCR in Python”*

## Prerequisiti

- Python 3.8 o superiore (il codice utilizza le f‑stringhe).  
- Una licenza valida di Aspose OCR per Python o una chiave di prova gratuita.  
- Le immagini che desideri elaborare salvate localmente (qualsiasi combinazione di PNG, JPG o TIFF).  

Se hai già un ambiente virtuale, ottimo—altrimenti, creane uno con:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate
```

Ora sei pronto per installare l'SDK.

## Passo 1: Installa l'SDK Aspose OCR

Aspose distribuisce il suo motore OCR tramite PyPI, quindi un unico comando `pip` fa al caso tuo:

```bash
pip install aspose-ocr
```

> **Consiglio professionale:** Fissa la versione (ad es., `aspose-ocr==22.12`) per evitare cambiamenti inattesi in futuro.

## Passo 2: Importa la classe OCR Engine

La classe principale con cui interagirai è `OcrEngine`. Importala all'inizio del tuo script:

```python
# Step 2: Import the OCR engine class
from asposeocr import OcrEngine
```

> *Perché è importante:* Importare solo ciò di cui hai bisogno mantiene basso il tempo di avvio, specialmente quando in seguito incorpori lo script in un'applicazione più grande.

## Passo 3: Definisci i file immagine da elaborare

Crea una lista Python contenente i percorsi completi di ogni immagine che desideri analizzare. Sostituisci `YOUR_DIRECTORY` con il percorso reale della cartella.

```python
# Step 3: Define the image files to be processed
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.jpg",
    "YOUR_DIRECTORY/page3.tif"
]
```

> **Caso limite:** Se hai centinaia di file, considera di generare questa lista programmaticamente con `glob.glob('*.png')` per evitare modifiche manuali.

## Passo 4: Esegui OCR su tutte le immagini contemporaneamente

Aspose OCR fornisce un comodo metodo `processMultiple` che restituisce una lista di oggetti `OcrResult`—uno per ogni file di input.

```python
# Step 4: Run OCR on all images at once
ocr_engine = OcrEngine()               # instantiate the engine
ocr_results = ocr_engine.processMultiple(image_files)
```

> *Perché l'elaborazione batch?* Inviare ogni immagine singolarmente comporta un overhead aggiuntivo (inizializzare il motore, caricare le librerie native). La chiamata batch riduce il carico CPU e accelera il lavoro complessivo.

### Gestione degli errori in modo elegante

Se un'immagine non può essere letta (file corrotto, formato non supportato), `processMultiple` solleverà un'eccezione. Avvolgi la chiamata in un blocco `try/except` per mantenere lo script attivo:

```python
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as e:
    print(f"⚠️ OCR failed: {e}")
    ocr_results = []   # fallback to empty list
```

## Passo 5: Stampa il testo estratto per ogni file

Itera sui risultati, associando ogni `OcrResult` al nome del file originale. Il metodo `getText()` restituisce la stringa riconosciuta.

```python
# Step 5: Output the extracted text for each file
for index, result in enumerate(ocr_results, start=1):
    file_path = image_files[index - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")   # add a blank line for readability
```

### Output previsto

Eseguendo lo script completo su tre semplici screenshot potresti ottenere qualcosa di simile:

```
--- Text from file YOUR_DIRECTORY/page1.png ---
Invoice #12345
Date: 2024‑07‑01
Total: $256.78

--- Text from file YOUR_DIRECTORY/page2.jpg ---
Welcome to the Annual Report
Prepared by: Finance Dept.

--- Text from file YOUR_DIRECTORY/page3.tif ---
© 2025 Acme Corp. All rights reserved.
```

Se un'immagine non contiene caratteri riconoscibili, vedrai una stringa vuota—nulla si rompe, e puoi decidere se segnalare quel file per una revisione manuale.

## Bonus: Ottimizzare la precisione OCR

Aspose OCR offre diverse impostazioni opzionali con cui potresti voler sperimentare:

| Impostazione | Cosa fa | Quando usarla |
|--------------|---------|---------------|
| `ocr_engine.setLanguage('eng')` | Forza il modello linguistico inglese (riduce i falsi positivi). | Principalmente documenti in inglese. |
| `ocr_engine.setResolution(300)` | Migliora la precisione su scansioni a bassa risoluzione (dpi). | Scansioni sotto i 200 dpi. |
| `ocr_engine.setPageSegMode('single_block')` | Tratta l'intera immagine come un unico blocco di testo. | Ricevute semplici o carte d'identità. |

Puoi aggiungere queste righe subito dopo aver creato `ocr_engine`:

```python
ocr_engine.setLanguage('eng')
ocr_engine.setResolution(300)
ocr_engine.setPageSegMode('single_block')
```

## Problemi comuni e come evitarli

1. **Stack TIFF di grandi dimensioni** – Un TIFF multi‑pagina può consumare gigabyte di RAM se caricato tutto in una volta. Dividi il file in immagini a pagina singola prima di passarle a `processMultiple`.  
2. **Script non latini** – Se devi **estrarre testo dalle immagini** che contengono caratteri cirillici, arabi o cinesi, cambia il codice lingua di conseguenza (`'rus'`, `'ara'`, `'chi_sim'`).  
3. **Spazi nei percorsi dei file** – I percorsi Windows con spazi possono causare `FileNotFoundError`. Avvolgi ogni percorso in stringhe raw (`r"C:\\My Folder\\image.png"`) o usa `os.path.abspath`.  

Affrontare questi problemi in anticipo ti salva da errori di runtime criptici in seguito.

---

## Esempio completo funzionante

Di seguito trovi lo script completo che puoi copiare‑incollare in un file chiamato `batch_ocr.py`. Include tutte le ottimizzazioni di best‑practice discusse sopra.

```python
# batch_ocr.py
# -------------------------------------------------
# Complete example: extract text from images using Aspose OCR (Python)
# -------------------------------------------------

from asposeocr import OcrEngine
import os

# -------------------------------------------------
# Configuration – adjust these values for your environment
# -------------------------------------------------
IMAGE_DIR = "YOUR_DIRECTORY"   # <-- replace with your folder path
SUPPORTED_EXT = (".png", ".jpg", ".jpeg", ".tif", ".tiff")

# Build a list of image file paths automatically
image_files = [
    os.path.join(IMAGE_DIR, f)
    for f in os.listdir(IMAGE_DIR)
    if f.lower().endswith(SUPPORTED_EXT)
]

if not image_files:
    print("⚠️ No supported image files found in the specified directory.")
    exit(1)

# -------------------------------------------------
# Initialize OCR engine with optional tweaks
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.setLanguage('eng')          # English language model
ocr_engine.setResolution(300)          # Boost low‑dpi accuracy
ocr_engine.setPageSegMode('single_block')  # Treat whole image as one block

# -------------------------------------------------
# Run batch OCR and handle potential errors
# -------------------------------------------------
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as exc:
    print(f"❌ OCR processing failed: {exc}")
    ocr_results = []

# -------------------------------------------------
# Display extracted text
# -------------------------------------------------
for idx, result in enumerate(ocr_results, start=1):
    file_path = image_files[idx - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")
```

Salva, attiva il tuo ambiente virtuale e esegui:

```bash
python batch_ocr.py
```

Dovresti vedere le stringhe estratte stampate sulla console, pronte per ulteriori elaborazioni (ad es., salvataggio in un database o alimentazione di un modello di linguaggio naturale).

---

## Conclusione

In questa guida abbiamo mostrato come **estrarre testo dalle immagini** usando Aspose OCR per Python, coprendo tutto dall'installazione all'elaborazione batch e alla gestione degli errori. Lo script è compatto, completamente funzionale e facile da estendere—che tu debba **convertire il testo delle immagini scansionate** in file CSV, alimentare un indice di ricerca o semplicemente automatizzare l'inserimento dati.

Pronto per il passo successivo? Considera di abbinare questa pipeline OCR a un unificatore PDF per creare PDF ricercabili, o collegala a un trigger di storage cloud in modo che ogni scansione caricata venga processata immediatamente. Il cielo è il limite, e ora hai una solida base su cui costruire.

Hai domande o idee per miglioramenti? Lascia un commento qui sotto, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}