---
category: general
date: 2026-11-20
description: Esegui OCR su un'immagine con Aspose OCR e poi estrai il testo dall’immagine
  usando il post‑processore AI integrato. Impara un flusso di lavoro Python completo
  in pochi minuti.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from image
language: it
lastmod: 2026-11-20
og_description: Esegui l'OCR sull'immagine con Aspose OCR, quindi estrai il testo
  dall'immagine tramite post‑elaborazione AI. Segui questa guida Python passo‑passo.
og_image_alt: Diagram showing how to perform OCR on image and extract text from image
  using Aspose
og_title: Esegui OCR sull'immagine ed estrai il testo dall'immagine usando Aspose
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Perform OCR on image with Aspose OCR and then extract text from image
    using the built‑in AI post‑processor. Learn a complete Python workflow in minutes.
  headline: Perform OCR on image and extract text from image with Aspose
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- AI post‑processing
title: Esegui OCR su un'immagine ed estrai il testo dall'immagine con Aspose
url: /it/python/general/perform-ocr-on-image-and-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su immagine ed estrai testo dall'immagine con Aspose

Se devi **eseguire OCR su file immagine** in Python, questa guida ti mostra una soluzione completa end‑to‑end. Utilizzando Aspose OCR insieme al post‑processore Aspose AI, puoi **estrarre testo dall'immagine** in modo affidabile e migliorare l'output OCR grezzo con un modello linguistico leggero.

In questo tutorial imparerai a:

* Configurare il motore Aspose OCR.
* Eseguire OCR per **estrarre testo dall'immagine**.
* (Facoltativo) Configurare un modello AI per il post‑processing.
* Registrare una funzione di post‑processing personalizzata.
* Produrre testo migliorato e liberare le risorse.

I passaggi funzionano con qualsiasi immagine raster (PNG, JPEG, BMP) e richiedono solo il pacchetto `aspose-ocr`.

## Prerequisiti

Prima di iniziare, assicurati di avere:

| Requisito | Perché è importante |
|-----------|----------------------|
| Python 3.8+ | Richiesto dall'Aspose SDK. |
| Pacchetto pip `aspose-ocr` | Fornisce `AsposeOCR`, `AsposeAI` e le classi di configurazione del modello. |
| Un file immagine (es. `sample_image.png`) | La sorgente su cui **eseguire OCR su immagine**. |
| Facoltativo: supporto GPU | Se prevedi di eseguire un modello più grande su GPU, imposta `gpu_layers` di conseguenza. |

Installa l'SDK con:

```bash
pip install aspose-ocr
```

## Passo 1: Esegui OCR su immagine

La prima operazione è leggere l'immagine e ottenere il testo grezzo. Questo è il passaggio centrale **eseguire OCR su immagine**.

```python
from aspose.ocr import AsposeOCR

# Initialise the OCR engine
ocr_engine = AsposeOCR()

# Path to the image you want to process
image_path = "YOUR_DIRECTORY/sample_image.png"

# Execute OCR – this returns the plain text extracted from the image
raw_text = ocr_engine.recognize_image(image_path)

print("Raw OCR result:")
print(raw_text)
```

**Perché funziona:** `AsposeOCR.recognize_image` esegue un modello di riconoscimento ottico dei caratteri pre‑addestrato, ottimizzato per velocità e precisione su font comuni. Il metodo restituisce una stringa Unicode semplice, che costituisce la base per qualsiasi ulteriore elaborazione.

> **Consiglio professionale:** Se l'immagine contiene più lingue, imposta `ocr_engine.language = "eng+spa"` (o qualsiasi codice ISO‑639‑2 supportato) prima di chiamare `recognize_image`.

## Passo 2: Inizializzare il post‑processore AI

Aspose AI fornisce uno strato di post‑processing leggero che può pulire gli errori OCR, correggere la punteggiatura o applicare logiche aziendali personalizzate.

```python
from aspose.ocr import AsposeAI

# Initialise the AI post‑processor with default logging
ai_processor = AsposeAI()
```

**Perché ti serve:** L'OCR grezzo spesso riconosce erroneamente i caratteri (es. “0” vs “O”). Il passaggio AI affina l'output, rendendo il risultato **estrarre testo dall'immagine** più affidabile per attività successive come indicizzazione o analisi.

## Passo 3: (Facoltativo) Configurare il modello AI

Puoi indirizzare il processore a un modello specifico di Hugging Face, abilitare i download automatici o forzare l'esecuzione su CPU. Questo passaggio è opzionale ma utile quando desideri un comportamento deterministico.

```python
from aspose.ocr import AsposeAIModelConfig

# Create a configuration object
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"          # Download model if missing
model_config.hugging_face_repo_id = "openai/gpt2"   # Small, fast model
model_config.gpu_layers = 0                        # Use CPU; set >0 for GPU

# Apply the configuration to the AI processor
ai_processor.configure(model_config)
```

**Spiegazione:**  
* `allow_auto_download` ti salva dalla gestione manuale dei modelli.  
* `hugging_face_repo_id` seleziona un modello; `gpt2` è un buon compromesso tra dimensione e qualità per la correzione di testi brevi.  
* `gpu_layers` controlla quante layer del trasformatore vengono eseguite sulla GPU; `0` forza l'esecuzione pura su CPU, sicura su tutte le macchine.

## Passo 4: Registrare una funzione di post‑processing personalizzata

Aspose AI ti consente di collegare qualsiasi callable che riceve la stringa OCR grezza e restituisce una versione trasformata. Di seguito un esempio semplice che converte tutto in maiuscolo.

```python
def my_post_processor(text):
    """
    Custom post‑processor that transforms the OCR result.
    Replace this logic with your own business rules.
    """
    return text.upper()

# Register the function with the AI processor
ai_processor.set_post_processor(my_post_processor, custom_settings=None)
```

**Quando personalizzare:** Usa una funzione personalizzata quando hai bisogno di pulizia specifica del dominio, ad esempio rimuovere identificatori riservati, normalizzare date o applicare correzioni basate su regex. Il modello AI verrà eseguito *dopo* questa funzione, permettendoti di combinare regole deterministiche con miglioramenti probabilistici.

## Passo 5: Migliorare il risultato OCR usando il post‑processore AI

Ora esegui l'intera pipeline: il testo OCR grezzo viene prima passato attraverso la tua funzione personalizzata, poi attraverso il modello AI, e infine ricevi l'output raffinato.

```python
# Run the AI post‑processor on the raw OCR text
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("\nOriginal OCR :")
print(raw_text)
print("\nAI‑enhanced   :")
print(enhanced_text)
```

**Cosa dovresti vedere:**  
Se l'immagine originale conteneva “Hello world”, la console potrebbe mostrare:

```
Original OCR :
Hello world

AI‑enhanced   :
HELLO WORLD
```

In uno scenario reale, il modello AI correggerebbe errori di ortografia, aggiungerebbe la punteggiatura mancante o riformatterebbe le interruzioni di riga, fornendoti un risultato **estrarre testo dall'immagine** più pulito, pronto per l'archiviazione o l'analisi.

## Passo 6: Rilasciare le risorse al termine

Sia il motore OCR sia il post‑processore AI allocano risorse native. Liberarle esplicitamente evita perdite di memoria, specialmente in servizi a lunga esecuzione.

```python
# Clean up native resources
ai_processor.free_resources()
```

Se hai anche istanziato `ocr_engine` con un backend pesante, potresti chiamare `ocr_engine.dispose()` (se disponibile) nello stesso modo.

## Variazioni comuni e casi limite

| Situazione | Adeguamento consigliato |
|------------|--------------------------|
| **Grandi PDF con molte pagine** | Itera su ogni pagina, chiama `recognize_image` per ogni pagina rasterizzata e aggrega i risultati. |
| **Ambiente con GPU abilitata** | Imposta `model_config.gpu_layers` al numero di layer che desideri sulla GPU (es. `4`). Assicurati che i driver CUDA siano installati. |
| **Testo non inglese** | Cambia `ocr_engine.language` al codice lingua appropriato e, se necessario, seleziona un modello Hugging Face specifico per la lingua. |
| **Scansioni molto rumorose** | Pre‑processa l'immagine con OpenCV (denoise, threshold) prima di chiamare `recognize_image`. |
| **Necessità di mantenere il casing originale** | Sostituisci la funzione `my_post_processor` con un no‑op o una regola più sfumata invece di `text.upper()`. |

## Esempio completo funzionante

Mettendo tutto insieme, ecco uno script unico che puoi eseguire così com'è (sostituisci `YOUR_DIRECTORY/sample_image.png` con il percorso reale del tuo file):

```python
from aspose.ocr import AsposeOCR, AsposeAI, AsposeAIModelConfig

# 1️⃣ Perform OCR on image
ocr_engine = AsposeOCR()
image_path = "YOUR_DIRECTORY/sample_image.png"
raw_text = ocr_engine.recognize_image(image_path)

# 2️⃣ Initialise the AI post‑processor
ai_processor = AsposeAI()

# 3️⃣ (Optional) Configure the AI model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "openai/gpt2"
model_config.gpu_layers = 0            # CPU execution
ai_processor.configure(model_config)

# 4️⃣ Register a custom post‑processor (example: uppercase)
def my_post_processor(text):
    return text.upper()

ai_processor.set_post_processor(my_post_processor, custom_settings=None)

# 5️⃣ Enhance the OCR result
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("Original OCR :", raw_text)
print("AI‑enhanced   :", enhanced_text)

# 6️⃣ Release resources
ai_processor.free_resources()
```

Eseguendo questo script verranno stampati sia l'output OCR grezzo sia la versione migliorata dall'AI, dimostrando come puoi **eseguire OCR su file immagine** e **estrarre testo dall'immagine** in un flusso di lavoro unico, riproducibile e affidabile.

## Conclusione

Ora sai come **eseguire OCR su file immagine** con Aspose OCR, quindi **estrarre testo dall'immagine** usando il post‑processore AI integrato. Il tutorial ha coperto:

* Inizializzare il motore OCR.
* Eseguire OCR per ottenere testo grezzo.
* (Facoltativo) Configurare un modello leggero di Hugging Face.
* Aggiungere una funzione di post‑processing personalizzata.
* Rilasciare le risorse al termine.

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Extract Text Image with Aspose OCR & AI – Full Step‑by‑Step Guide](/ocr/english/python/general/extract-text-image-with-aspose-ocr-ai-full-step-by-step-guid/)
- [How to Correct OCR Errors – Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image Python – Complete Aspose OCR Guide](/ocr/english/python-java/general/extract-text-from-image-python-complete-aspose-ocr-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}