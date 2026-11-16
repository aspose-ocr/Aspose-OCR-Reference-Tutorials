---
category: general
date: 2026-06-25
description: Scopri come eseguire l'OCR in Python e individua il modo migliore per
  caricare l'immagine per l'OCR, quindi aumenta la precisione con il post‑processing
  AI di Aspose.
draft: false
keywords:
- how to perform OCR
- load image for OCR
- Aspose OCR Python
- AI post‑processor OCR
- OCR accuracy improvement
- Python image processing OCR
language: it
og_description: Come eseguire l'OCR in Python? Segui questa guida per caricare l'immagine
  per l'OCR, eseguire il riconoscimento di base e migliorare i risultati con il post‑processing
  AI di Aspose.
og_title: Come eseguire l'OCR in Python – Tutorial completo su Aspose OCR e AI
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  headline: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  type: TechArticle
- description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  name: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  steps:
  - name: Expected Output
    text: '``` === Raw OCR === Inv0ice #12345 Date: 2023-08-15 Total: $1,23O'
  - name: What if I don’t have a GPU?
    text: Set `model_config.gpu_layers = 0` and optionally increase `model_config.context_size`
      to 2048 for better CPU performance. The model will run slower, but you still
      get the same quality of correction.
  - name: My image is rotated—will `load_image` handle it?
    text: 'Aspose OCR automatically detects orientation, but for extremely skewed
      scans you may want to pre‑rotate using Pillow:'
  - name: How do I process multiple files in a folder?
    text: Wrap the whole pipeline in a `for` loop and store each `enhanced_text` in
      a list or write directly to a CSV. Remember to call `ocr_ai.free_resources()`
      **once** after the loop, not after each file—re‑initialising the model repeatedly
      is wasteful.
  - name: Can I swap the language model?
    text: Absolutely. Just change `model_config.hugging_face_repo_id` to any GGUF‑compatible
      model on Hugging Face (e.g., `Meta/Llama-3.2-1B-Instruct-GGUF`). Keep the quantization
      setting consistent with your hardware.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: Come eseguire l'OCR in Python – Guida completa ad Aspose OCR e AI
url: /it/python/general/how-to-perform-ocr-in-python-complete-aspose-ocr-ai-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR in Python – Guida completa ad Aspose OCR & AI

Ti sei mai chiesto **come eseguire OCR** in Python senza lottare con trucchi di basso livello sulle immagini? Non sei solo. In questo tutorial vedremo come caricare un'immagine per OCR, eseguire l'estrazione di testo semplice e poi perfezionare l'output con il post‑processor AI di Aspose. Alla fine avrai uno script pronto all'uso che trasforma scansioni rumorose in testo pulito e ricercabile—senza servizi aggiuntivi.

Copriamo tutto, dall'installazione dell'SDK al rilascio delle risorse in applicazioni a lunga esecuzione. Se hai mai provato a **caricare immagine per OCR** e hai ottenuto un pasticcio incomprensibile, questa guida è l'antidoto. Vedrai perché combinare OCR tradizionale con un modello linguistico produce risultati che sembrano scritti da un umano.

## Prerequisiti

Prima di iniziare, assicurati di avere:

- Python 3.9 o più recente (il codice utilizza type hints che gli interpreti più vecchi non supportano)
- Una licenza attiva di Aspose OCR o una prova gratuita (l'edizione community funziona per la valutazione)
- Una GPU con almeno 4 GB di VRAM se vuoi accelerare il modello AI (opzionale ma consigliato)
- Un'immagine di esempio, ad es. `sample_invoice.png`, posizionata in un percorso a cui puoi fare riferimento

Se qualcuno di questi elementi ti è sconosciuto, non farti prendere dal panico—l'installazione dell'SDK è una singola riga, e le impostazioni della GPU possono essere disattivate in seguito.

## Passo 1: Installa Aspose OCR e le dipendenze

Apri un terminale ed esegui:

```bash
pip install aspose-ocr
pip install aspose-ocr-ai
```

Il primo pacchetto ti fornisce `aspose.ocr`, il secondo aggiunge le utility del post‑processor AI. Entrambi sono wheel pure Python, quindi non dovrai compilare nulla da te.

## Passo 2: Carica l'immagine per OCR e inizializza il motore

Ora **caricheremo immagine per OCR** usando `OcrEngine` di Aspose. Pensalo come consegnare un foglio a un impiegato molto diligente che legge ogni carattere.

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Initialise the basic OCR engine
ocr_engine = aocr.OcrEngine()

# Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

# Perform a plain OCR scan – this returns a raw string
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)
```

> **Perché è importante:** La chiamata `load_image` è il ponte tra il tuo file system e il motore OCR. Se il percorso è errato, otterrai un `FileNotFoundError` prima che inizi qualsiasi riconoscimento. Controlla sempre i separatori di directory, specialmente su Windows rispetto a macOS/Linux.

## Passo 3: Configura il Post‑Processor AI di Aspose

Aspose AI può scaricare un modello linguistico da Hugging Face, memorizzarlo nella cache locale e eseguire l'inferenza sulla tua GPU (o CPU). Di seguito configuriamo un modello leggero da 3 miliardi di parametri che si adatta alla maggior parte dei laptop moderni.

```python
# Initialise the AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()

# Allow the SDK to fetch the model automatically
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"

# Use half of the GPU layers – balances speed and VRAM usage
model_config.gpu_layers = 20
model_config.context_size = 1024

# Load (or download) the model now
ocr_ai.initialize(model_config)
```

> **Suggerimento:** Se sei su una macchina solo CPU, imposta `gpu_layers = 0`. Il modello funzionerà comunque, solo un po' più lentamente. La quantizzazione `int8` mantiene l'impronta di memoria ridotta preservando la maggior parte dell'accuratezza del modello.

## Passo 4: Registra un Post‑Processor personalizzato

Il modello AI ha bisogno di un prompt che gli dica cosa fare. Qui gli chiediamo di comportarsi come un correttore OCR, correggendo errori ortografici, unendo parole spezzate e rimuovendo artefatti.

```python
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    # Temperature 0.0 makes the output deterministic
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

# Hook the custom processor into the AI pipeline
ocr_ai.set_post_processor(correction_processor, custom_settings=None)
```

> **Perché un processore personalizzato?** Il post‑processor predefinito potrebbe aggiungere spiegazioni extra o formattazioni di cui non hai bisogno. Fornendo la nostra funzione, manteniamo l'output strettamente al testo pulito, perfetto per l'indicizzazione a valle o per la memorizzazione in database.

## Passo 5: Esegui la pipeline OCR potenziata da AI

Ora alimentiamo l'output OCR grezzo nello strato AI. Il motore chiamerà il nostro `correction_processor`, che a sua volta interagirà con il modello linguistico.

```python
# Apply the AI post‑processor to the raw OCR result
enhanced_text = ocr_ai.run_postprocessor(raw_text)

print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)
```

Dovresti notare un miglioramento evidente: i caratteri mancanti vengono ripristinati, le comuni letture errate di OCR come “0” vs “O” vengono corrette e le interruzioni di riga diventano più logiche.

## Passo 6: Pulizia – Rilascia le risorse

Se prevedi di eseguire questo all'interno di un servizio web o di un demone a lunga esecuzione, il rilascio della memoria GPU è cruciale. Dimenticare di chiamare `free_resources` può provocare crash “out‑of‑memory” dopo qualche centinaio di richieste.

```python
ocr_ai.free_resources()
```

Questo è tutto—la tua pipeline OCR completa è ora pronta per la produzione.

## Riepilogo completo dello script

Di seguito trovi l'esempio completo e eseguibile. Copialo in un file chiamato `ocr_with_ai.py`, regola il percorso dell'immagine e avvia `python ocr_with_ai.py`.

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Step 1: Load image for OCR and perform basic recognition
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)

# Step 2: Initialise the Aspose AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"
model_config.gpu_layers = 20          # half of GPU layers
model_config.context_size = 1024
ocr_ai.initialize(model_config)

# Step 3: Register custom correction processor
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

ocr_ai.set_post_processor(correction_processor, custom_settings=None)

# Step 4: Run AI post‑processor on raw OCR output
enhanced_text = ocr_ai.run_postprocessor(raw_text)
print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)

# Step 5: Release resources (important for long‑running apps)
ocr_ai.free_resources()
```

### Output previsto

```
=== Raw OCR ===
Inv0ice #12345
Date: 2023-08-15
Total: $1,23O

=== AI‑enhanced OCR ===
Invoice #12345
Date: 2023-08-15
Total: $1,230
```

Nota come “Inv0ice” diventa “Invoice” e la “O” errante dopo l'importo scompare. È l'AI che compie la sua magia.

## Domande comuni e casi limite

### E se non ho una GPU?

Imposta `model_config.gpu_layers = 0` e, facoltativamente, aumenta `model_config.context_size` a 2048 per migliorare le prestazioni su CPU. Il modello sarà più lento, ma otterrai comunque la stessa qualità di correzione.

### La mia immagine è ruotata—`load_image` la gestirà?

Aspose OCR rileva automaticamente l'orientamento, ma per scansioni estremamente inclinate potresti voler pre‑ruotare usando Pillow:

```python
from PIL import Image
img = Image.open("sample.png")
rotated = img.rotate(90, expand=True)
rotated.save("rotated.png")
ocr_engine.load_image("rotated.png")
```

### Come elaborare più file in una cartella?

Avvolgi l'intera pipeline in un ciclo `for` e memorizza ogni `enhanced_text` in una lista o scrivilo direttamente in un CSV. Ricorda di chiamare `ocr_ai.free_resources()` **una sola volta** dopo il ciclo, non dopo ogni file—riinizializzare il modello ripetutamente è uno spreco.

```python
import os

for filename in os.listdir("invoices"):
    if filename.lower().endswith(".png"):
        ocr_engine.load_image(os.path.join("invoices", filename))
        raw = ocr_engine.recognize()
        clean = ocr_ai.run_postprocessor(raw)
        # Save or index `clean`
```

### Posso cambiare il modello linguistico?

Assolutamente. Basta cambiare `model_config.hugging_face_repo_id` con qualsiasi modello compatibile GGUF su Hugging Face (ad es., `Meta/Llama-3.2-1B-Instruct-GGUF`). Mantieni la configurazione di quantizzazione coerente con il tuo hardware.

## Consigli professionali e insidie

- **Consiglio pro:** Imposta `temperature=0.0` per correzioni deterministic​he. Temperature più alte possono introdurre modifiche creative ma errate.
- **Attenzione a:** Documenti estremamente lunghi (> 5000 caratteri). La finestra di contesto del modello è limitata a 1024 token nell'esempio; suddividi il testo in paragrafi prima di inviarlo all'AI.
- **Nota di sicurezza:** Se esegui questo in un ambiente regolamentato, assicurati che l'URL di download del modello sia nella whitelist. Il flag `allow_auto_download` può

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrai testo da immagine con Aspose OCR – Guida passo‑passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Come usare AspOCR: filtri di pre‑elaborazione OCR per .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Estrai testo da immagine C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}