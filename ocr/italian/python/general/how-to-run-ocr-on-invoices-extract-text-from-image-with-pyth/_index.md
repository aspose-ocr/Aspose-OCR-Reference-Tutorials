---
category: general
date: 2026-01-07
description: Come eseguire l'OCR e estrarre il testo da un'immagine per l'elaborazione
  delle fatture. Impara a migliorare la precisione dell'OCR, caricare l'immagine per
  l'OCR e processare l'OCR delle fatture in modo efficiente.
draft: false
keywords:
- how to run ocr
- extract text from image
- improve ocr accuracy
- load image for ocr
- process invoice ocr
language: it
og_description: Come eseguire OCR su fatture passo passo. Estrai il testo dall'immagine,
  migliora la precisione dell'OCR e carica l'immagine per l'OCR usando Aspose AI.
og_title: Come eseguire OCR su fatture – Guida completa a Python
tags:
- OCR
- Python
- Image Processing
title: Come eseguire OCR su fatture – Estrarre testo da un'immagine con Python
url: /it/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR su fatture – Estrarre testo da immagine con Python

Ti sei mai chiesto **come eseguire OCR** su una fattura scansionata e ottenere un testo pulito e ricercabile? Non sei solo. Molti sviluppatori si trovano di fronte a un muro quando l'output grezzo dell'OCR è pieno di errori ortografici, interruzioni di riga errate e punteggiatura mancante. In questo tutorial percorreremo una soluzione full‑stack che non solo **estrae testo da immagine** ma anche **migliora l'accuratezza dell'OCR** mediante post‑processing con un modello AI di Aspose.

Vedrai come **caricare l'immagine per OCR**, eseguire il motore integrato e poi applicare un controllo ortograficoo che rende il risultato pronto per le analisi successive. Alla fine, avrai uno script riutilizzabile che può essere inserito in qualsiasi pipeline di elaborazione delle fatture.

> **Cosa ti servirà**  
> * Python 3.9 o più recente  
> * pacchetti `aspose-ocr` e `aspose-ai` (installati via `pip`)  
> * Un'immagine di fattura (PNG, JPEG o TIFF) – useremo `sample_invoice.png` come esempio  
> * Facoltativo: una GPU con almeno 4 GB VRAM per un'inferenza del modello più veloce (lo script funziona anche su CPU)

---

## Passo 1: Installa i pacchetti richiesti e prepara l'ambiente

Prima di poter **caricare l'immagine per OCR**, dobbiamo assicurarci che le librerie necessarie siano disponibili. Il motore OCR di Aspose è fornito con un semplice wrapper Python, mentre il post‑processor AI si basa su un modello quantizzato di Hugging Face.

```bash
# Install Aspose OCR and AI packages
pip install aspose-ocr aspose-ai
```

> **Consiglio professionale:** Se prevedi di usare l'accelerazione GPU, installa `torch` con supporto CUDA (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu121`).

---

## Passo 2: Carica l'immagine della fattura

Caricare l'immagine è semplice, ma vale la pena spiegare perché impostiamo esplicitamente il percorso come stringa grezza (`r"..."`). Questo evita incidenti con caratteri di escape nei percorsi Windows.

```python
import aspose.ocr as ocr

# Define the path to your invoice image
image_path = r"YOUR_DIRECTORY/sample_invoice.png"

# Initialize the OCR engine and attach the image
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)
```

*Perché è importante:* L'uso di `ocr.Image.load` garantisce che l'immagine sia pre‑processata (binarizzazione, correzione inclinazione) secondo le impostazioni predefinite ottimali di Aspose, che già **migliorano l'accuratezza dell'OCR** prima che avvenga qualsiasi magia AI.

---

## Passo 3: Esegui il motore OCR integrato

Ora eseguiamo effettivamente **OCR** e catturiamo il testo grezzo. Questo passo mostra l'output tipico che otterresti da un'esecuzione OCR vanilla—spesso un caos di interruzioni di riga e occasionali errori ortografici.

```python
# Perform OCR
engine.recognize()
raw_text = engine.recognized_text

print("Raw OCR output:")
print(raw_text)
```

**Output grezzo tipico** (troncato per brevità):

```
INVOICE NO: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Potresti notare che “Invoice” appare come “Invo1ce” o che la punteggiatura è assente. È qui che entra in gioco il post‑processor AI.

---

## Passo 4: Configura il modello AI di Aspose

Il modello AI che utilizzeremo è **Qwen2.5‑3B‑Instruct‑GGUF**, un LLM leggero ottimizzato per istruzioni che gira comodamente su una GPU di fascia media. La configurazione qui sotto indica ad Aspose dove recuperare il modello, quante layer mantenere sulla GPU e la dimensione del contesto per gestire paragrafi lunghi.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,               # 30 layers on GPU, remainder on CPU
    context_size=4096            # larger context for long paragraphs
)

ai = AsposeAI()
ai.initialize(model_config)   # you could also pass `model_config` to the constructor
```

> **Perché questa configurazione?**  
> * `gpu_layers=30` bilancia velocità e memoria—la maggior parte dell'inferenza avviene sulla GPU, mentre le layer rimanenti rimangono sulla CPU per evitare errori OOM.  
> * `context_size=4096` garantisce che il modello possa vedere l'intera fattura in una volta, evitando di troncare campi importanti.

---

## Passo 5: Crea un semplice post‑processor di correzione ortografica

Avvolgeremo la chiamata AI in una piccola funzione chiamata `simple_spell_check`. Il prompt è deliberatamente conciso: “Correct spelling and punctuation:” seguito dal testo OCR grezzo. Il modello restituisce una versione pulita.

```python
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

# Register the post‑processor with the AI instance
ai.set_post_processor(simple_spell_check, None)
```

**Come funziona:** `ai.run_prompt` invia il prompt al LLM caricato localmente, che restituisce una singola stringa con ortografia corretta, punteggiatura appropriata e una disposizione delle interruzioni di riga più naturale.

---

## Passo 6: Applica il post‑processor al testo OCR grezzo

Ora avviene la magia. Inviamo l'output OCR grezzo al nostro post‑processor e stampiamo il risultato migliorato.

```python
enhanced_text = ai.run_postprocessor(raw_text)

print("\nAI‑enhanced OCR output:")
print(enhanced_text)
```

**Esempio di output migliorato**:

```
Invoice No: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Nota la correzione dell'ortografia di “Invoice”, l'uso corretto dei due punti e le interruzioni di riga coerenti—esattamente ciò di cui hai bisogno per un parsing affidabile a valle.

---

## Passo 7: Pulisci le risorse

Sia il motore OCR che il modello AI allocano risorse native. È buona pratica liberarle quando hai finito, specialmente in servizi a lungo termine.

```python
ai.free_resources()
engine.dispose()
```

---

## Script completo – Pronto da incollare

Di seguito trovi lo script completo, eseguibile, che collega tutti i passaggi. Salvalo come `invoice_ocr.py`, sostituisci `YOUR_DIRECTORY` con la cartella contenente l'immagine della tua fattura, ed esegui con `python invoice_ocr.py`.

```python
# invoice_ocr.py
import aspose.ocr as ocr
from aspose.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1: Load the image to be processed
# -------------------------------------------------
image_path = r"YOUR_DIRECTORY/sample_invoice.png"
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)

# -------------------------------------------------
# Step 2: Run the built‑in OCR engine and obtain raw text
# -------------------------------------------------
engine.recognize()
raw_text = engine.recognized_text
print("Raw OCR output:")
print(raw_text)

# -------------------------------------------------
# Step 3: Configure the Aspose AI model for post‑processing
# -------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,
    context_size=4096
)

ai = AsposeAI()
ai.initialize(model_config)   # alternatively, pass config to the constructor

# -------------------------------------------------
# Step 4: Define a simple spell‑check post‑processor
# -------------------------------------------------
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

ai.set_post_processor(simple_spell_check, None)

# -------------------------------------------------
# Step 5: Apply the post‑processor to the raw OCR text
# -------------------------------------------------
enhanced_text = ai.run_postprocessor(raw_text)
print("\nAI‑enhanced OCR output:")
print(enhanced_text)

# -------------------------------------------------
# Step 6: Release resources
# -------------------------------------------------
ai.free_resources()
engine.dispose()
```

Esegui lo script e vedrai sia il dump grezzo e rumoroso dell'OCR sia la versione rifinita, **migliorata in accuratezza OCR**, affiancate.

---

## Domande frequenti e casi particolari

### 1. E se la mia immagine di fattura è un PDF multi‑pagina?

Aspose OCR può caricare direttamente le pagine PDF. Sostituisci la riga di caricamento immagine con:

```python
engine.image = ocr.Image.load("invoice.pdf", page_index=0)  # 0‑based page number
```

Itera `page_index` per elaborare ogni pagina in sequenza.

### 2. La mia GPU esaurisce la memoria—posso usare solo la CPU?

Assolutamente. Imposta `gpu_layers=0` in `AsposeAIModelConfig`. Il modello verrà eseguito interamente sulla CPU, più lento ma sicuro per hardware di fascia bassa.

### 3. Come gestire fatture non in inglese?

Sostituisci l'ID del repository del modello con un modello specifico per lingua, ad esempio `"mistralai/Mistral-7B-Instruct-v0.2"` per supporto multilingue. Il resto della pipeline rimane invariato.

### 4. Posso concatenare più post‑processor (ad es., formattare date, estrarre totali)?

Sì. `ai.set_post_processor` accetta una lista di callable. Per esempio:

```python
def extract_totals(text):
    # simple regex to pull monetary values
    import re
    totals = re.findall(r"\$\d+(?:,\d{3})*(?:\.\d{2})?", text)
    return "\n".join(totals)

ai.set_post_processor([simple_spell_check, extract_totals], None)
```

L'output verrà prima corretto ortograficamente, poi avranno i totali estratti.

---

## Suggerimenti sulle prestazioni e migliori pratiche

| Suggerimento | Perché aiuta |
|-----|---------------|
| **Elabora più fatture in batch** – caricale in una lista e processale in un ciclo. | Riduce l'overhead dell'interprete Python e mantiene il modello AI caldo in memoria. |
| **Cache del modello** – evita di chiamare `initialize` ripetutamente in un servizio web. | Il caricamento del modello può richiedere ~30 secondi; la cache fornisce risposte istantanee. |
| **Ridimensiona le immagini grandi** a larghezza 1500 px prima dell'OCR. | Immagini più piccole accelerano sia l'OCR sia l'inferenza AI senza sacrificare l'accuratezza. |
| **Imposta `allow_auto_download="false"` in produzione** – distribuisci il modello con il tuo deployment. | Garantisce tempi di avvio deterministici ed evita interruzioni di rete. |

---

## Conclusione

Abbiamo coperto **come eseguire OCR** su fatture, dal caricamento dell'immagine alla rifinitura del risultato con un controllo ortografico guidato dall'AI. Seguendo questi passaggi puoi in modo affidabile **estrarre testo da immagine**, **migliorare l'accuratezza OCR**, e processare senza problemi **OCR di fatture** in qualsiasi workflow basato su Python.

Provalo con diversi layout di fattura—magari una ricevuta scritta a mano o un contratto scansionato. La stessa pipeline si adatta con minime modifiche, dimostrando che una combinazione OCR + AI ben strutturata è uno strumento versatile per qualsiasi progetto di automazione documentale.

Se hai trovato utile questa guida, considera di condividerla con i colleghi o di mettere una stella al repository che ospita i pacchetti Aspose

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}