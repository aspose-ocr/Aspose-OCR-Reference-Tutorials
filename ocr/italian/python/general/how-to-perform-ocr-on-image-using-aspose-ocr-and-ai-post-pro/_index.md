---
category: general
date: 2026-09-25
description: Scopri come eseguire l'OCR su un'immagine con Aspose OCR, caricare l'immagine
  per l'OCR e riconoscere il testo da una ricevuta in un esempio completo in Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- load image for OCR
- recognize text from receipt
- Aspose OCR Python
- AI post‑processor OCR
language: it
lastmod: 2026-09-25
og_description: Esegui OCR su un'immagine usando Aspose OCR in Python. Questa guida
  mostra come caricare l'immagine per l'OCR e riconoscere il testo da una ricevuta
  con miglioramento AI.
og_image_alt: Screenshot of Python code performing OCR on an image and showing original
  vs AI‑enhanced text
og_title: Esegui OCR su immagine con Aspose OCR e post‑processore AI – Guida Python
schemas:
- author: Aspose
  dateModified: '2026-09-25'
  description: Learn how to perform OCR on image with Aspose OCR, load image for OCR,
    and recognize text from receipt in a complete Python example.
  headline: How to perform OCR on image using Aspose OCR and AI post‑processor in
    Python
  type: TechArticle
tags:
- OCR
- Python
- Aspose
title: Come eseguire l'OCR su un'immagine usando Aspose OCR e il post‑processore AI
  in Python
url: /it/python/general/how-to-perform-ocr-on-image-using-aspose-ocr-and-ai-post-pro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR su immagine usando Aspose OCR e AI post‑processor in Python

Se hai bisogno di **eseguire OCR su immagine** in Python, questo tutorial ti mostra una soluzione completa, pronta‑all’uso. Imparerai come **caricare l’immagine per OCR**, avviare il motore Aspose OCR e **riconoscere il testo da ricevuta** con un opzionale post‑processing guidato dall’AI.

Ti guideremo passo passo, dall’installazione dell'SDK al rilascio delle risorse, così potrai integrare un’estrazione di testo affidabile nelle tue applicazioni senza perdere alcun dettaglio.

## Prerequisiti

Prima di iniziare, assicurati di avere:

- Python 3.8+ installato  
- Un Aspose OCR per Python via pip (`pip install aspose-ocr`)  
- Accesso a Internet per il download opzionale del modello AI  
- Un’immagine di esempio di una ricevuta (`receipt.png`) collocata in una directory nota  

Non sono richiesti servizi esterni aggiuntivi; il codice viene eseguito localmente e utilizza il modello gratuito Qwen2‑3B‑Instruct quando sono disponibili layer GPU.

## Step 1: Installa i pacchetti richiesti

```bash
pip install aspose-ocr
```

Il pacchetto `aspose-ocr` contiene sia la classe `OcrEngine` sia il post‑processor `AsposeAI` che useremo per **eseguire OCR su immagine**.

## Step 2: Crea e configura il motore OCR – carica immagine per OCR

```python
from aspose.ocr import OcrEngine

# Initialise the OCR engine
ocr_engine = OcrEngine()

# Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/receipt.png")   # <-- load image for OCR
```

Chiamare `load_image` indica al motore quale file analizzare. Puoi sostituire il percorso con qualsiasi file PNG, JPG o TIFF su cui devi **eseguire OCR su immagine**.

## Step 3: Configura il post‑processor opzionale AsposeAI

Il post‑processor AI può correggere l’ortografia, migliorare la formattazione o applicare logiche personalizzate dopo che il risultato grezzo dell’OCR è stato restituito.

```python
from aspose.ocr import AsposeAI, AsposeAIModelConfig

# Initialise the AI processor (logging is optional)
ai_processor = AsposeAI()   # AsposeAI(logging=my_logger)

# Define which model to use – it will auto‑download if missing
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20                     # use GPU layers when available
)

# Load the model configuration into the processor
ai_processor.initialize(model_config)   # implicit in many examples
```

La configurazione indica al processore di scaricare il modello Qwen2 predefinito, consentendoti di **eseguire OCR su immagine** con una comprensione linguistica di livello superiore.

## Step 4: Collega una semplice funzione di post‑processing

Puoi collegare qualsiasi callable che riceve il testo grezzo e restituisce una versione corretta. Ecco un esempio minimale che corregge un errore di battitura comune:

```python
def simple_spell_check(text, **kwargs):
    """Correct a frequent misspelling in receipt OCR results."""
    return text.replace("reciept", "receipt")

# Register the function with the AI processor
ai_processor.set_post_processor(simple_spell_check, {})
```

Poiché la funzione è registrata, ogni volta che chiami `run_postprocessor` l’output dell’OCR passerà attraverso questo passaggio.

## Step 5: Esegui OCR e migliora il risultato – riconosci il testo da ricevuta

```python
# Perform the core OCR operation
raw_result = ocr_engine.recognize()          # <-- recognize text from receipt

# Let the AI processor improve the raw output
enhanced_result = ai_processor.run_postprocessor(raw_result)

# Display both versions
print("Original OCR :", raw_result.text)
print("AI‑enhanced  :", enhanced_result.text)
```

La chiamata `recognize` restituisce un oggetto il cui attributo `text` contiene i caratteri grezzi estratti dall’immagine della ricevuta. La successiva chiamata a `run_postprocessor` restituisce un nuovo risultato in cui il nostro controllo ortografico (e eventuali miglioramenti basati sul modello) sono stati applicati.

### Output previsto

```
Original OCR : Total: $23.45\nSubtotl: $20.00\nTax: $3.45\nThank you for your reciept
AI‑enhanced  : Total: $23.45
Subtotal: $20.00
Tax: $3.45
Thank you for your receipt
```

Nota come il testo migliorato dall’AI corregge l’errore di battitura e inserisce interruzioni di riga per una migliore leggibilità—esattamente ciò che desideri quando **riconosci il testo da ricevuta**.

## Step 6: Pulisci le risorse

```python
# Release memory held by the AI processor
ai_processor.free_resources()

# Dispose of the OCR engine
ocr_engine.dispose()
```

Liberare le risorse è particolarmente importante quando si elaborano molte immagini in un servizio a lungo termine.

## Script completo eseguibile

Unendo tutti i pezzi ottieni uno script unico che puoi copiare, incollare ed eseguire:

```python
# ocr_receipt.py
from aspose.ocr import AsposeAI, AsposeAIModelConfig, OcrEngine

# 1️⃣ Initialise OCR engine and load the image
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/receipt.png")   # load image for OCR

# 2️⃣ Set up optional AI post‑processor
ai_processor = AsposeAI()
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20
)
ai_processor.initialize(model_config)

# 3️⃣ Register a simple spell‑check function
def simple_spell_check(text, **kwargs):
    return text.replace("reciept", "receipt")
ai_processor.set_post_processor(simple_spell_check, {})

# 4️⃣ Perform OCR and enhance the result
raw_result = ocr_engine.recognize()                # recognize text from receipt
enhanced_result = ai_processor.run_postprocessor(raw_result)

print("Original OCR :", raw_result.text)
print("AI‑enhanced  :", enhanced_result.text)

# 5️⃣ Release resources
ai_processor.free_resources()
ocr_engine.dispose()
```

Esegui lo script con:

```bash
python ocr_receipt.py
```

Dovresti vedere gli output originali e quelli migliorati dall’AI stampati sulla console.

## Consigli professionali e ostacoli comuni

- **La qualità dell’immagine è fondamentale** – assicurati che la foto della ricevuta sia ben illuminata e non eccessivamente compressa; altrimenti il motore OCR potrebbe perdere caratteri, riducendo il beneficio del post‑processing.  
- **Disponibilità della GPU** – se il tuo computer non dispone di una GPU compatibile, imposta `gpu_layers=0` per forzare l’inferenza su CPU; il modello funzionerà comunque, sebbene più lentamente.  
- **Post‑processor personalizzati** – puoi concatenare più funzioni o utilizzare un modello linguistico più sofisticato per riformattare date, importi o nomi dei fornitori.  
- **Elaborazione batch** – istanzia un unico oggetto `AsposeAI` e riutilizzalo su più istanze di `OcrEngine` per evitare download ripetuti del modello.  

## Conclusione

Ora sai come **eseguire OCR su immagine** usando Aspose OCR, come **caricare l’immagine per OCR** e come **riconoscere il testo da ricevuta** con miglioramenti guidati dall’AI. Seguendo i passaggi sopra, potrai integrare un’elaborazione di ricevute accurata e ad alta velocità in qualsiasi applicazione Python.

**Passi successivi**: esplora tecniche aggiuntive di post‑processing come la normalizzazione delle valute, integra il risultato in un database o passa a un modello più grande per ricevute multilingue. Per personalizzazioni più profonde, consulta la documentazione di Aspose OCR su pacchetti linguistici personalizzati e pre‑processing avanzato delle immagini.

Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Converti immagine in testo: estrai testo da immagine usando Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Come fare OCR su testo di immagine con lingua usando Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Come eseguire OCR in C# – estrai testo da immagine usando Aspose OCR](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image-using-aspose/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}