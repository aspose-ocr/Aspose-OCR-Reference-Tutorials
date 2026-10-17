---
category: general
date: 2026-06-22
description: Riconosci il testo da file PNG usando Aspose OCR in Python. Esegui OCR
  batch di immagini e imposta i layer GPU per una rapida elaborazione.
draft: false
keywords:
- recognize text from png
- batch ocr images
- set gpu layers
- Aspose OCR Python
- GPU acceleration OCR
language: it
og_description: Riconosci il testo da file PNG con Aspose OCR in Python. Questa guida
  mostra come eseguire l'OCR di immagini in batch e impostare i layer GPU per velocizzare.
og_title: Riconosci il testo da PNG – Tutorial Aspose OCR passo passo
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  headline: recognize text from png – Complete Guide with Aspose OCR & AI
  type: TechArticle
- description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  name: recognize text from png – Complete Guide with Aspose OCR & AI
  steps:
  - name: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
    text: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
  - name: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
    text: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
  - name: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
    text: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
  - name: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
    text: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
  type: HowTo
tags:
- OCR
- Python
- AsposeAI
title: Riconoscere il testo da PNG – Guida completa con Aspose OCR e AI
url: /it/python/general/recognize-text-from-png-complete-guide-with-aspose-ocr-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# riconoscere testo da png – Tutorial completo Aspose OCR & AI

Hai mai dovuto **riconoscere testo da file png** ma ti sei impantanato nei dettagli di configurazione? Non sei il solo. Che tu stia digitalizzando ricevute, scansionando moduli o trasformando screenshot in testo ricercabile, padroneggiare il batch OCR di immagini in Python può farti risparmiare ore.  

In questa guida percorreremo un esempio pronto all'uso che non solo **riconosce testo da png**, ma mostra anche come **impostare i layer GPU** per un notevole aumento di velocità. Alla fine avrai uno script autonomo, una spiegazione chiara di ogni passaggio e una serie di consigli pratici da copiare‑incollare nei tuoi progetti.

## Cosa copre questo tutorial

- Installazione dei pacchetti Python Aspose OCR e Aspose AI  
- Configurazione di un modello AI con download automatico da Hugging Face  
- Creazione di un piccolo post‑processor che corregge gli errori OCR più comuni  
- Esecuzione di un ciclo **batch OCR images** su un’intera cartella di PNG  
- Utilizzo dell’opzione **set GPU layers** per sfruttare la tua scheda grafica  
- Pulizia sicura delle risorse dopo l’elaborazione  

Nessun servizio esterno, nessuna magia nascosta—solo puro codice Python che puoi inserire in un file `.py` e farlo girare.

![Diagramma del flusso di riconoscimento del testo da png](workflow.png){alt="diagramma del flusso di riconoscimento del testo da png"}

## Prerequisiti

| Requisito | Perché è importante |
|-----------|----------------------|
| Python 3.8+ | Le wheel di Aspose AI puntano a interpreti recenti |
| Una GPU compatibile CUDA (opzionale) | Necessaria se vuoi **impostare i layer GPU** per l’accelerazione |
| Accesso a Internet al primo avvio | Il modello verrà scaricato automaticamente da Hugging Face |
| `pip` installato | Per recuperare i pacchetti Aspose |

Se li hai già, ottimo—sei pronto a partire. Altrimenti, i passaggi di installazione qui sotto ti guideranno attraverso gli elementi mancanti.

---

## Passo 1: Installa i pacchetti Aspose OCR e Aspose AI

Per prima cosa, scarica le librerie da PyPI. Il comando qui sotto installa sia il motore OCR sia l’aiuto AI in un’unica operazione.

```bash
pip install aspose-ocr aspose-ai
```

*Consiglio:* Usa un ambiente virtuale (`python -m venv .venv`) così i pacchetti rimangono isolati dalla tua installazione globale di Python.

---

## Passo 2: Crea e configura l'istanza Aspose AI

Il componente AI alimenta la modalità “intelligente” del motore OCR. Lo punteremo al modello `Qwen/Qwen2.5-3B-Instruct-GGUF`, gli chiederemo di scaricare automaticamente se manca, e **imposteremo i layer GPU** a 30 (potrai regolarli in seguito).

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Initialize the AI wrapper
ai = AsposeAI()

# Build a model configuration
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",                     # Grab the model automatically
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # Smaller footprint, still accurate
    directory_model_path="YOUR_DIRECTORY/ai_models", # Where the model will live
    gpu_layers=30                                   # <-- set gpu layers for GPU acceleration
)

# Apply the configuration and spin up the model
ai.initialize(model_cfg)
```

**Perché è importante:**  
- `allow_auto_download` elimina il passaggio manuale di scaricare un modello da ~2 GB.  
- `gpu_layers=30` indica al transformer sottostante di eseguire i primi 30 layer sulla GPU, riducendo drasticamente il tempo di inferenza quando è presente una GPU compatibile.  
- L’utilizzo della quantizzazione `int8` mantiene basso l’utilizzo di memoria senza sacrificare molto l’accuratezza.

---

## Passo 3: Definisci un semplice post‑processor per correggere gli errori OCR

L’OCR non è perfetto—soprattutto su PNG a bassa risoluzione. Una correzione rapida è sostituire i caratteri che vengono frequentemente fraintesi. La funzione seguente scambia “0” con “o” e “1” con “l”, un pattern che vediamo spesso nelle fatture scansionate.

```python
def fix_common_errors(text, **_):
    """
    Post‑processor that corrects typical OCR mis‑recognitions.
    Feel free to extend this with regexes or custom dictionaries.
    """
    return text.replace("0", "o").replace("1", "l")
```

La collegheremo all’istanza AI nel passo successivo così ogni risultato di riconoscimento passerà automaticamente attraverso di essa.

---

## Passo 4: Collega il post‑processor e il motore OCR

Ora uniamo tutto: il motore OCR, il modello AI e il post‑processor.

```python
import ocr  # Aspose OCR module

# Attach the post‑processor
ai.set_post_processor(fix_common_errors, {})

# Spin up the OCR engine and bind the AI
engine = ocr.OcrEngine()
engine.set_ai(ai)
```

**Cosa succede dietro le quinte?**  
L’`OcrEngine` delega il lavoro pesante al modello AI configurato. Dopo che il modello restituisce il testo grezzo, Aspose chiama `fix_common_errors` per pulire l’output prima che tu lo veda.

---

## Passo 5: Batch OCR Images – Processa ogni PNG in una cartella

Ecco il cuore del tutorial: un ciclo che attraversa una directory, carica ogni `.png`, esegue l’OCR e stampa il risultato pulito. Questo schema è il modo canonico per **batch OCR images** in modo efficiente.

```python
from pathlib import Path

# Replace with the folder that holds your PNG files
image_folder = Path("YOUR_DIRECTORY")

# Iterate over every PNG file in the folder
for img_path in image_folder.glob("*.png"):
    # Load the image into the engine
    engine.load_image(str(img_path))

    # Perform recognition
    result = engine.recognize()

    # Output the filename and the extracted text
    print(f"[{img_path.name}] → {result.text}")
```

**Output previsto** (esempio per una ricevuta):

```
[receipt_001.png] → Total amount: $23.45
[receipt_002.png] → Item: Coffee, Price: $3.50
```

Se hai decine o centinaia di file, questo ciclo li gestirà sequenzialmente, riutilizzando la stessa istanza AI per evitare il sovraccarico del caricamento ripetuto del modello.

---

## Passo 6: Pulizia – Libera le risorse e smaltisci il motore

Quando hai finito, è buona pratica rilasciare la memoria GPU e le altre risorse native. Aspose fornisce metodi espliciti per farlo.

```python
# Release the AI model and any GPU buffers
ai.free_resources()

# Dispose of the OCR engine to close native handles
engine.dispose()
```

Saltare questo passo può lasciare memoria GPU residua allocata, con il rischio di errori di out‑of‑memory al prossimo avvio dello script.

---

## Bonus: Regolare i layer GPU per hardware diverso

Il valore `gpu_layers` impostato in precedenza è un buon compromesso per molte GPU moderne, ma potresti doverlo adeguare:

| Memoria GPU (GB) | `gpu_layers` consigliati |
|------------------|--------------------------|
| 4 GB o meno      | 10‑15                    |
| 6‑8 GB           | 20‑30                    |
| 12 GB+           | 35‑45 (o più)            |

Se superi la memoria della GPU, il motore tornerà automaticamente alla CPU per i layer rimanenti, quindi non crasha—solo più lento. Sentiti libero di sperimentare e monitorare l’uso con `nvidia‑smi`.

---

## Problemi comuni e come evitarli

1. **Il download del modello fallisce** – Assicurati che l’ambiente possa raggiungere `https://huggingface.co`. Un proxy aziendale potrebbe richiedere configurazione (`https_proxy` env var).  
2. **GPU non rilevata** – Verifica che la libreria `torch` (installata come dipendenza) veda la GPU: `import torch; print(torch.cuda.is_available())`. Se restituisce `False`, installa la wheel di PyTorch compatibile con CUDA.  
3. **Percorso immagine errato** – `Path.glob("*.png")` è case‑sensitive su Linux. Usa `*.PNG` o `*.png` di conseguenza, oppure aggiungi `pathlib.Path(...).rglob("*.[pP][nN][gG]")` per maggiore sicurezza.  
4. **Il post‑processor corregge troppo** – La semplice sostituzione può trasformare caratteri “0” legittimi in “o”. Testa su un campione rappresentativo e adatta la logica secondo necessità.

---

## Esempio completo funzionante (pronto da copiare‑incollare)

```python
# recognize_text_from_png_batch.py
# -------------------------------------------------
# Author: Your Name
# Date:   2026‑06‑22
# -------------------------------------------------
from pathlib import Path
import ocr                      # Aspose OCR module
from aspose_ai import AsposeAI, AsposeAIModelConfig

# ----- Step 1: AI configuration -----
ai = AsposeAI()
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    directory_model_path="YOUR_DIRECTORY/ai_models",
    gpu_layers=30               # <-- set gpu layers
)
ai.initialize(model_cfg)

# ----- Step 2: Post‑processor -----
def fix_common_errors(text, **_):
    """Replace typical OCR mis‑reads."""
    return text.replace("0", "o").replace("1", "l")

ai.set_post_processor(fix_common_errors, {})

# ----- Step 3: OCR engine -----
engine = ocr.OcrEngine()
engine.set_ai(ai)

# ----- Step 4: Batch processing -----
image_folder = Path("YOUR_DIRECTORY")
for img_path in image_folder.glob("*.png"):
    engine.load_image(str(img_path))
    result = engine.recognize()
    print(f"[{img_path.name}] → {result.text}")

# ----- Step 5: Cleanup -----
ai.free_resources()
engine.dispose()
```

Eseguilo con:

```bash
python recognize_text_from_png_batch.py
```

Dovresti vedere ogni nome di file PNG seguito dal testo estratto, esattamente come mostrato in precedenza.

---

## Conclusione

Abbiamo appena percorso un flusso di lavoro completo, pronto per la produzione, per **riconoscere testo da png** usando Aspose OCR e Aspose AI in Python. Raggruppando i passaggi in uno script pulito, puoi eseguire facilmente **batch OCR images**, e grazie al `set gpu layers`

## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell’API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}