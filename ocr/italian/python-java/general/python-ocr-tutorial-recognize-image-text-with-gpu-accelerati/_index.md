---
category: general
date: 2026-06-06
description: Tutorial OCR in Python che mostra come riconoscere il testo nelle immagini,
  eseguire OCR ad alta risoluzione ed estrarre testo spagnolo usando OCR accelerato
  da GPU.
draft: false
keywords:
- python ocr tutorial
- recognize image text
- high resolution ocr
- gpu accelerated ocr
- extract spanish text
language: it
og_description: Tutorial OCR in Python che ti guida nel riconoscere il testo nelle
  immagini, OCR ad alta risoluzione e nell'estrazione di testo spagnolo con accelerazione
  GPU.
og_title: Tutorial OCR in Python – Riconoscimento del testo accelerato da GPU
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Python OCR tutorial showing how to recognize image text, perform high
    resolution OCR and extract Spanish text using GPU accelerated OCR.
  headline: Python OCR Tutorial – Recognize Image Text with GPU Acceleration
  type: TechArticle
- description: Python OCR tutorial showing how to recognize image text, perform high
    resolution OCR and extract Spanish text using GPU accelerated OCR.
  name: Python OCR Tutorial – Recognize Image Text with GPU Acceleration
  steps:
  - name: Prerequisites
    text: '- Python 3.9+ (the code works on 3.10 and newer as well). - A CUDA‑compatible
      GPU (optional but highly recommended). - Basic familiarity with pip and virtual
      environments.'
  - name: 6.1 Fallback When No GPU Is Present
    text: "```python if not torch.cuda.is_available(): # Re‑initialize the reader
      without GPU to avoid hidden errors reader = Reader(lang_list=[\"es\"], gpu=False)
      print(\"\U0001F504 Re‑initialized reader for CPU execution.\") ```"
  - name: 6.2 Down‑sampling Very Large Images
    text: 'If your image is larger than 4000 × 4000 px, you might run out of GPU memory.
      Down‑sample proportionally while preserving DPI:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- GPU
- Spanish
title: Tutorial OCR Python – Riconosci il testo delle immagini con accelerazione GPU
url: /it/python-java/general/python-ocr-tutorial-recognize-image-text-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR Tutorial – Riconoscere il Testo nelle Immagini con Accelerazione GPU

Ti sei mai chiesto come **riconoscere il testo nelle immagini** in uno script Python senza passare ore a regolare le impostazioni? Non sei l'unico. In questo **python ocr tutorial** ti mostreremo un modo pulito, end‑to‑end, per estrarre testo spagnolo da un'immagine ad alta risoluzione, e aggiungeremo l'accelerazione GPU così il processo sarà fulmineo.

Pensalo come una dimostrazione veloce da fare durante una pausa caffè, che potrai poi espandere in una pipeline di livello produzione. Alla fine di questa guida avrai un programma eseguibile che esegue **OCR ad alta risoluzione**, sfrutta una GPU con supporto CUDA e restituisce i caratteri spagnoli esatti di cui hai bisogno.

## Cosa Imparerai

- Come installare e importare una libreria OCR moderna che supporta l'accelerazione GPU.  
- Come creare un'istanza del motore OCR e impostarla per **riconoscere il testo nelle immagini** in spagnolo.  
- Come abilitare **OCR accelerato da GPU** per guadagni di velocità massicci su file ad alta risoluzione.  
- Come gestire casi limite come driver CUDA mancanti o fallback alla CPU.  
- Consigli per migliorare l'accuratezza quando devi **estrarre testo spagnolo** da scansioni rumorose.

### Prerequisiti

- Python 3.9+ (il codice funziona anche su 3.10 e versioni successive).  
- Una GPU compatibile con CUDA (opzionale ma altamente consigliata).  
- Familiarità di base con pip e gli ambienti virtuali.  

Se ti manca qualcuno di questi, il tutorial funziona comunque—basta saltare il passaggio GPU e la libreria tornerà automaticamente alla CPU.

---

## Python OCR Tutorial: Installa i Pacchetti Necessari

Prima di tutto, ci serve un motore OCR solido. Per questo tutorial useremo il pacchetto open‑source **`easyocr`**, che include il supporto GPU integrato quando viene rilevato un dispositivo compatibile.

```bash
# Create a fresh virtual environment (optional but tidy)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows use `ocr-env\Scripts\activate`

# Install EasyOCR and its optional torch dependencies
pip install easyocr[torch]   # Installs both CPU and GPU builds of PyTorch
```

> **Pro tip:** Se hai già installato PyTorch, assicurati che corrisponda alla tua versione CUDA (`pip install torch==2.2.0+cu121 -f https://download.pytorch.org/whl/torch_stable.html`). Versioni non allineate sono una causa comune di errori “GPU not found”.

---

## Passo 1: Crea un'Istanza del Motore OCR

Ora avviamo il motore. EasyOCR chiama la sua classe principale `Reader`. Il costruttore accetta una lista di codici lingua; noi passeremo `"es"` per lo spagnolo.

```python
# Step 1: Initialize the OCR reader for Spanish
from easyocr import Reader

# The `gpu` flag tells EasyOCR to try using CUDA if it’s available.
reader = Reader(lang_list=["es"], gpu=True)
```

*Perché è importante:* Dichiarando la lingua in anticipo, il motore carica solo i pesi della rete neurale necessari, risparmiando memoria e velocizzando l'inferenza—particolarmente utile quando si tratta di **OCR ad alta risoluzione** più avanti.

---

## Passo 2: Prepara un'Immagine ad Alta Risoluzione

Le immagini ad alta risoluzione forniscono al modello più pixel su cui lavorare, il che di solito si traduce in un riconoscimento dei caratteri migliore. Supponiamo tu abbia un file chiamato `high_res_spanish.png` in una cartella denominata `samples`.

```python
import os

# Construct an absolute path – keeps the script portable
image_path = os.path.join("samples", "high_res_spanish.png")

# Quick sanity check – raise a clear error if the file is missing
if not os.path.isfile(image_path):
    raise FileNotFoundError(f"Image not found at {image_path}")
```

Se non hai a disposizione un campione ad alta risoluzione, puoi scaricarne uno gratuito da Unsplash o generare un'immagine sintetica con Pillow. La chiave è mantenere i DPI sopra 300 per ottenere i migliori risultati.

---

## Passo 3: Abilita l'Accelerazione GPU (Opzionale ma Raccomandata)

EasyOCR tenta già di usare la GPU quando imposti `gpu=True`. Tuttavia, è buona pratica verificare che il dispositivo sia effettivamente utilizzato, soprattutto su configurazioni con più GPU.

```python
import torch

# Verify CUDA availability – helpful for debugging
if torch.cuda.is_available():
    print(f"✅ CUDA device detected: {torch.cuda.get_device_name(0)}")
else:
    print("⚠️ No CUDA device found – falling back to CPU. Performance will be slower.")
```

*Perché controllare?* Se lo script ricade silenziosamente sulla CPU, potresti chiederti perché un'operazione di 5 secondi improvvisamente richiede 30 secondi. Questo piccolo controllo rende il comportamento trasparente e mantiene la tua pipeline **OCR accelerato da GPU** prevedibile.

---

## Passo 4: Esegui OCR ad Alta Risoluzione e Riconosci il Testo nell'Immagine

Ora la parte divertente—leggere effettivamente il testo. Il metodo `readtext` di EasyOCR restituisce una lista di tuple contenenti il bounding box, la stringa riconosciuta e un punteggio di confidenza.

```python
# Step 4: Run OCR on the high‑resolution image
results = reader.readtext(image_path, detail=1, paragraph=False)

# `results` looks like:
# [
#   ([(x1, y1), (x2, y2), (x3, y3), (x4, y4)], 'Texto reconocido', 0.98),
#   ...
# ]
```

Se ti serve la stringa grezza senza coordinate, imposta `detail=0`. Per la maggior parte dei casi d'uso di **riconoscere il testo nelle immagini**, il valore predefinito (`detail=1`) ti offre abbastanza contesto per una post‑elaborazione successiva.

---

## Passo 5: Estrarre il Testo Spagnolo e Pulire l'Output

Poiché abbiamo chiesto a EasyOCR lo spagnolo, le stringhe restituite sono già in quella lingua. Tuttavia, potresti volerle concatenare, rimuovere spazi bianchi o filtrare le rilevazioni a bassa confidenza.

```python
# Step 5: Consolidate high‑confidence Spanish strings
extracted_text = []
for bbox, text, conf in results:
    if conf > 0.85:                # Drop anything below 85 % confidence
        extracted_text.append(text)

# Join everything into a single block – perfect for further NLP tasks
final_text = "\n".join(extracted_text)

print("📝 Extracted Spanish text:")
print(final_text)
```

**E se la confidenza è bassa?** Puoi abbassare la soglia (rischiando più rumore) o pre‑processare l'immagine (aumentare il contrasto, binarizzare o correggere l'inclinazione). Questi trucchi sono comuni quando si affronta **OCR ad alta risoluzione** su documenti scansionati.

---

## Passo 6: Gestire i Casi Limite e Ottimizzazioni di Prestazioni

Anche i modelli meglio addestrati inciampano in alcuni scenari. Di seguito trovi un paio di correzioni rapide da incollare nello script.

### 6.1 Fallback Quando Non C'è GPU

```python
if not torch.cuda.is_available():
    # Re‑initialize the reader without GPU to avoid hidden errors
    reader = Reader(lang_list=["es"], gpu=False)
    print("🔄 Re‑initialized reader for CPU execution.")
```

### 6.2 Down‑sampling di Immagini Molto Grandi

Se la tua immagine supera i 4000 × 4000 px, potresti esaurire la memoria GPU. Esegui un down‑sampling proporzionale mantenendo i DPI:

```python
from PIL import Image

def resize_if_needed(path, max_dim=3000):
    img = Image.open(path)
    if max(img.size) > max_dim:
        scale = max_dim / max(img.size)
        new_size = (int(img.width * scale), int(img.height * scale))
        img = img.resize(new_size, Image.LANCZOS)
        resized_path = path.replace(".png", "_resized.png")
        img.save(resized_path)
        return resized_path
    return path

image_path = resize_if_needed(image_path)
```

Questi snippet mantengono lo script robusto, sia che tu lo esegua su una workstation sia su un laptop modesto.

---

## Esempio Completo Funzionante

Mettendo tutto insieme, ecco lo script completo che puoi copiare‑incollare ed eseguire subito:

```python
# python_ocr_tutorial.py
import os
import torch
from PIL import Image
from easyocr import Reader

# ----------------------------------------------------------------------
# Helper: Resize very large images to avoid GPU OOM errors
def resize_if_needed(path, max_dim=3000):
    img = Image.open(path)
    if max(img.size) > max_dim:
        scale = max_dim / max(img.size)
        new_size = (int(img.width * scale), int(img.height * scale))
        img = img.resize(new_size, Image.LANCZOS)
        resized_path = path.replace(".png", "_resized.png")
        img.save(resized_path)
        return resized_path
    return path
# ----------------------------------------------------------------------

# 1️⃣ Verify CUDA availability (optional)
if torch.cuda.is_available():
    print(f"✅ CUDA device detected: {torch.cuda.get_device_name(0)}")
else:
    print("⚠️ No CUDA device – using CPU (expect slower performance).")

# 2️⃣ Initialize the OCR engine for Spanish (GPU if possible)
reader = Reader(lang_list=["es"], gpu=torch.cuda.is_available())

# 3️⃣ Path to the high‑resolution image
image_path = os.path.join("samples", "high_res_spanish.png")
if not os.path.isfile(image_path):
    raise FileNotFoundError(f"Image not found at {image_path}")

# 4️⃣ Resize if the image is gigantic
image_path = resize_if_needed(image_path)

# 5️⃣ Run OCR – this is the core **recognize image text** step
results = reader.readtext(image_path, detail=1, paragraph=False)

# 6️⃣ Filter and concatenate high‑confidence Spanish strings
extracted = []
for bbox, txt, conf in results:
    if conf > 0.85:
        extracted.append(txt)

final_text = "\n".join(extracted)

# 7️⃣ Output the result – **extract spanish text** ready for downstream processing
print("\n📝 Extracted Spanish text:")
print(final_text)
```

**Output previsto (esempio):**



## Cosa Dovresti Imparare Dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Recognize Page Rectangles for OCR Text Recognition in Aspose.OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}