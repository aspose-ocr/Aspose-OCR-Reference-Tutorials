---
category: general
date: 2026-05-03
description: Tutorial Python OCR che mostra come caricare file immagine PNG, riconoscere
  il testo dall'immagine e risorse AI gratuite per l'elaborazione OCR in batch.
draft: false
keywords:
- python ocr tutorial
- batch ocr processing
- free ai resources
- load png image
- recognize text from image
language: it
og_description: Il tutorial OCR in Python ti guida nel caricamento di immagini PNG,
  nel riconoscimento del testo dall’immagine e nella gestione delle risorse AI gratuite
  per l’elaborazione OCR batch.
og_title: Tutorial OCR Python – OCR batch veloce con risorse AI gratuite
tags:
- OCR
- Python
- AI
title: Tutorial Python OCR – Elaborazione OCR batch semplificata
url: /it/python/general/python-ocr-tutorial-batch-ocr-processing-made-easy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutorial Python OCR – Elaborazione OCR in Batch Semplificata

Hai mai avuto bisogno di un **python ocr tutorial** che ti permetta davvero di eseguire OCR su decine di file PNG senza impazzire? Non sei solo. In molti progetti reali devi **load png image** file, alimentarli a un motore, e poi pulire le risorse AI quando hai finito.  

In questa guida percorreremo un esempio completo, pronto‑da‑eseguire, che mostra esattamente come **recognize text from image** file, elaborarli in batch e liberare la memoria AI sottostante. Alla fine avrai uno script autonomo che potrai inserire in qualsiasi progetto—senza fronzoli, solo l’essenziale.

## Cosa ti servirà

- Python 3.10 o versioni successive (la sintassi usata qui si basa su f‑strings e type hints)  
- Una libreria OCR che esponga un metodo `engine.recognize` – per scopi dimostrativi assumiamo un pacchetto fittizio `aocr`, ma puoi sostituirlo con Tesseract, EasyOCR, ecc.  
- Il modulo helper `ai` mostrato nello snippet di codice (gestisce l’inizializzazione del modello e la pulizia delle risorse)  
- Una cartella piena di file PNG che desideri processare  

Se non hai `aocr` o `ai` installati, puoi simularli con stub—vedi la sezione “Stub Opzionali” alla fine.

## Step 1: Inizializza il Motore AI (Free AI Resources)

Prima di alimentare qualsiasi immagine nella pipeline OCR, il modello sottostante deve essere pronto. Inizializzare una sola volta salva memoria e velocizza i lavori batch.

```python
# step_1_initialize.py
import ai                # hypothetical helper that wraps the AI model
import aocr               # OCR library

def init_engine(config_path: str = "config.yaml"):
    """
    Initialize the AI engine if it hasn't been set up yet.
    This uses free AI resources – the engine will be released later.
    """
    if not ai.is_initialized():
        ai.initialize(config_path)   # auto‑initialize with the provided configuration
    else:
        print("Engine already initialized.")
```

**Perché è importante:**  
Chiamare `ai.initialize` ripetutamente per ogni immagine allocerebbe memoria GPU più e più volte, finendo per far crashare lo script. Controllando `ai.is_initialized()` garantiamo un’unica allocazione – è il principio del “free AI resources”.

## Step 2: Carica i File PNG per l'Elaborazione OCR in Batch

Ora raccogliamo tutti i file PNG che vogliamo far passare attraverso l’OCR. Usare `pathlib` mantiene il codice indipendente dal sistema operativo.

```python
# step_2_load_images.py
from pathlib import Path
from typing import List

def collect_png_paths(directory: str) -> List[Path]:
    """
    Scan `directory` and return a list of Path objects pointing to PNG files.
    """
    base_path = Path(directory)
    if not base_path.is_dir():
        raise NotADirectoryError(f"'{directory}' is not a valid folder.")
    
    png_files = sorted(base_path.glob("*.png"))
    if not png_files:
        raise FileNotFoundError("No PNG images found in the specified directory.")
    
    print(f"Found {len(png_files)} PNG image(s) to process.")
    return png_files
```

**Caso limite:**  
Se la cartella contiene file non‑PNG (ad es., JPEG) verranno ignorati, evitando che `engine.recognize` si blocchi su un formato non supportato.

## Step 3: Esegui OCR su Ogni Immagine e Applica il Post‑Processing

Con il motore pronto e la lista di file preparata, possiamo iterare sulle immagini, estrarre il testo grezzo e passarlo a un post‑processore che pulisce gli artefatti OCR comuni (come interruzioni di riga indesiderate).

```python
# step_3_ocr_batch.py
import aocr
import ai
from pathlib import Path
from typing import List

def ocr_batch(image_paths: List[Path]) -> List[str]:
    """
    Perform OCR on each PNG image and return a list of cleaned strings.
    """
    results = []
    for image_path in image_paths:
        # Load the image – aocr.Image.load abstracts away Pillow/OpenCV details
        img = aocr.Image.load(str(image_path))
        
        # Recognize raw text
        raw_text = engine.recognize(img)
        
        # Refine the raw OCR output using the AI post‑processor
        cleaned_text = ai.run_postprocessor(raw_text)
        results.append(cleaned_text)
        
        print(f"Processed {image_path.name}: {len(cleaned_text)} characters extracted.")
    
    return results
```

**Perché separiamo il caricamento dal riconoscimento:**  
`aocr.Image.load` può eseguire una decodifica lazy, più veloce per grandi batch. Tenere esplicito il passaggio di caricamento rende anche più semplice sostituire la libreria immagine se in seguito dovrai gestire JPEG o TIFF.

## Step 4: Pulizia – Free AI Resources Dopo il Batch

Una volta terminato il batch, dobbiamo rilasciare il modello per evitare perdite di memoria, specialmente su macchine con GPU.

```python
# step_4_cleanup.py
import ai

def release_resources():
    """
    Free any allocated AI resources. Safe to call multiple times.
    """
    if ai.is_initialized():
        ai.free_resources()
        print("AI resources have been released.")
    else:
        print("No AI resources were allocated.")
```

## Mettiamo Tutto Insieme – Lo Script Completo

Di seguito trovi un unico file che unisce i quattro passaggi in un flusso di lavoro coerente. Salvalo come `batch_ocr.py` ed eseguilo da riga di comando.

```python
# batch_ocr.py
"""
Python OCR tutorial – end‑to‑end batch OCR processing.
Loads PNG images, runs OCR, post‑processes results, and frees AI resources.
"""

import sys
from pathlib import Path
import ai
import aocr

# ----------------------------------------------------------------------
# Helper functions (copied from the steps above)
# ----------------------------------------------------------------------
def init_engine(cfg: str = "config.yaml"):
    if not ai.is_initialized():
        ai.initialize(cfg)
    else:
        print("Engine already initialized.")

def collect_png_paths(directory: str):
    base_path = Path(directory)
    if not base_path.is_dir():
        raise NotADirectoryError(f"'{directory}' is not a valid folder.")
    png_files = sorted(base_path.glob("*.png"))
    if not png_files:
        raise FileNotFoundError("No PNG images found in the specified directory.")
    print(f"Found {len(png_files)} PNG image(s) to process.")
    return png_files

def ocr_batch(image_paths):
    results = []
    for image_path in image_paths:
        img = aocr.Image.load(str(image_path))
        raw_text = engine.recognize(img)
        cleaned_text = ai.run_postprocessor(raw_text)
        results.append(cleaned_text)
        print(f"Processed {image_path.name}: {len(cleaned_text)} characters.")
    return results

def release_resources():
    if ai.is_initialized():
        ai.free_resources()
        print("AI resources released.")
    else:
        print("No resources to release.")

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-png>")
        sys.exit(1)

    image_dir = sys.argv[1]

    try:
        init_engine()
        png_paths = collect_png_paths(image_dir)
        texts = ocr_batch(png_paths)

        # Optional: write results to a single text file
        output_file = Path("ocr_results.txt")
        with output_file.open("w", encoding="utf-8") as f:
            for path, txt in zip(png_paths, texts):
                f.write(f"--- {path.name} ---\n")
                f.write(txt + "\n\n")
        print(f"All results saved to {output_file.resolve()}")
    finally:
        release_resources()
```

### Output Atteso

Eseguendo lo script su una cartella contenente tre PNG potrebbe stampare:

```
Engine already initialized.
Found 3 PNG image(s) to process.
Processed invoice1.png: 452 characters.
Processed receipt2.png: 317 characters.
Processed flyer3.png: 689 characters.
All results saved to /home/user/ocr_results.txt
AI resources released.
```

Il file `ocr_results.txt` conterrà un delimitatore chiaro per ogni immagine seguito dal testo OCR pulito.

## Stub Opzionali per aocr & ai (Se Non Hai Pacchetti Reali)

Se vuoi solo testare il flusso senza importare librerie OCR pesanti, puoi creare moduli mock minimi:

```python
# aocr/__init__.py
class Image:
    @staticmethod
    def load(path):
        return f"ImageObject({path})"

def dummy_recognize(image):
    return "Raw OCR output for " + str(image)

engine = type("Engine", (), {"recognize": dummy_recognize})()
```

```python
# ai/__init__.py
_state = {"initialized": False}

def is_initialized():
    return _state["initialized"]

def initialize(cfg):
    print(f"Initializing AI engine with {cfg}")
    _state["initialized"] = True

def run_postprocessor(text):
    # Very naive cleanup: strip extra spaces
    return " ".join(text.split())

def free_resources():
    print("Freeing AI resources")
    _state["initialized"] = False
```

Posiziona queste cartelle accanto a `batch_ocr.py` e lo script verrà eseguito, stampando risultati mock.

## Consigli Pro & Trappole Comuni

- **Picchi di memoria:** Se elabori migliaia di PNG ad alta risoluzione, considera di ridimensionarli prima dell’OCR. `aocr.Image.load` accetta spesso un argomento `max_size`.  
- **Gestione Unicode:** Apri sempre il file di output con `encoding="utf-8"`; i motori OCR possono emettere caratteri non‑ASCII.  
- **Parallelismo:** Per OCR CPU‑bound puoi avvolgere `ocr_batch` in un `concurrent.futures.ThreadPoolExecutor`. Ricorda però di mantenere una singola istanza `ai` – avviare molti thread che chiamano tutti `ai.initialize` vanifica l’obiettivo del “free AI resources”.  
- **Resilienza agli errori:** Avvolgi il ciclo per immagine in un blocco `try/except` così un singolo PNG corrotto non interromperà l’intero batch.

## Conclusione

Ora hai un **python ocr tutorial** che dimostra come **load png image** file, eseguire **batch OCR processing** e gestire responsabilmente **free AI resources**. L’esempio completo e funzionante mostra esattamente come **recognize text from image** oggetti e pulire le risorse a fine operazione, così puoi copiarlo e incollarlo nei tuoi progetti senza cercare pezzi mancanti.

Pronto per il passo successivo? Prova a sostituire i moduli stub `aocr` e `ai` con librerie reali come `pytesseract` e `torchvision`. Puoi anche estendere lo script per generare JSON, inviare i risultati a un database o integrarlo con un bucket di storage cloud. Il cielo è il limite—buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}