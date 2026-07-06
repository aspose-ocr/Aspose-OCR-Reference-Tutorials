---
category: general
date: 2026-06-06
description: Riconoscere il testo da un'immagine con Aspose OCR – impara come caricare
  l'immagine per l'OCR ed eseguire l'OCR sull'immagine usando il post‑processing AI
  in Python.
draft: false
keywords:
- recognize text from image
- perform ocr on image
- load image for ocr
language: it
og_description: Riconosci rapidamente il testo da un'immagine. Questa guida mostra
  come caricare un'immagine per OCR, eseguire l'OCR sull'immagine e migliorare i risultati
  con il post‑processing AI.
og_title: Riconosci il testo da un'immagine con Aspose OCR e AI
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: recognize text from image with Aspose OCR – learn how to load image
    for OCR and perform OCR on image using AI post‑processing in Python.
  headline: recognize text from image using Aspose OCR & AI
  type: TechArticle
- description: recognize text from image with Aspose OCR – learn how to load image
    for OCR and perform OCR on image using AI post‑processing in Python.
  name: recognize text from image using Aspose OCR & AI
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer - `asposeocr` package (`pip install asposeocr`) -
      An image file (e.g., `doc.png`) that contains printed or handwritten text -
      Optional: a GPU for faster LLM inference (the script works on CPU too)'
  - name: Install and import the required modules
    text: '```python # Install the library (run once in your environment) # pip install
      asposeocr'
  - name: Create the OCR engine and enable handwritten text recognition
    text: '```python # Initialise the OCR engine ocr_engine = ocr.OcrEngine()'
  - name: Load the image for OCR
    text: '```python # Point the engine at the file you want to process ocr_engine.load_image("YOUR_DIRECTORY/doc.png")
      ```'
  - name: Run the raw OCR pass
    text: '```python # Execute the recognition pipeline and capture the raw result
      raw_result = ocr_engine.recognize() ```'
  - name: Configure the Aspose AI model for LLM post‑processing
    text: '```python ai_config = AsposeAIModelConfig( allow_auto_download="true",
      # Pull the model if missing hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
      hugging_face_quantization="int8", # Reduce RAM usage gpu_layers=20, # Use 20
      GPU layers if a GPU is present directory_model_path="YOUR_DIRECTORY/mo'
  - name: Initialise the AI processor and attach it as a post‑processor
    text: '```python # Instantiate the AI processor with the configuration above ai_processor
      = AsposeAI() ai_processor.initialize(ai_config)'
  - name: Run the post‑processor to enhance the OCR output
    text: '```python # Apply AI‑driven post‑processing enhanced_result = ocr_engine.run_postprocessor(raw_result)'
  - name: Release resources
    text: '```python # Free GPU/CPU memory held by the AI model ai_processor.free_resources()'
  type: HowTo
- questions:
  - answer: No. The script falls back to CPU, but inference will be slower.
    question: Do I need a GPU?
  - answer: Absolutely—just change `hugging_face_repo_id` and adjust `gpu_layers`
      accordingly.
    question: Can I use a different LLM?
  - answer: Resize it first (e.g., using Pillow) to keep memory usage reasonable.
    question: What if my image is huge?
  - answer: You can toggle `enable_handwritten_recognition` depending on your workload.
    question: Is handwritten recognition always on?
  type: FAQPage
tags:
- OCR
- Aspose
- Python
title: Riconosci il testo da un'immagine usando Aspose OCR e AI
url: /it/python/general/recognize-text-from-image-using-aspose-ocr-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# riconoscere testo da immagine usando Aspose OCR & AI

Ti è mai capitato di dover riconoscere testo da un'immagine ma non eri sicuro quale libreria ti offrisse sia velocità che precisione? Non sei solo. In questa guida percorreremo un esempio completo, end‑to‑end, che mostra **come caricare l'immagine per OCR**, **eseguire OCR sull'immagine**, e poi rifinire l'output con il post‑processore AI di Aspose. Alla fine avrai uno script pronto all'uso che trasforma un PNG in testo pulito e ricercabile.

## Cosa imparerai

Copriamo tutto, dall'installazione del pacchetto Aspose OCR al rilascio delle risorse alla fine dell'esecuzione. Vedrai perché abilitare il riconoscimento del testo scritto a mano è importante, come configurare un LLM Qwen 2.5 per il post‑processing e come appare l'output finale. Nessun riferimento esterno necessario—basta copiare, incollare e eseguire.

### Prerequisiti

- Python 3.8 o versioni successive  
- pacchetto `asposeocr` (`pip install asposeocr`)  
- Un file immagine (ad es., `doc.png`) che contiene testo stampato o scritto a mano  
- Opzionale: una GPU per un'inferenza LLM più veloce (lo script funziona anche su CPU)

---

## Riconoscere testo da immagine – Passo‑per‑Passo

Sotto ogni blocco di codice troverai una breve spiegazione del **perché** facciamo quella specifica azione, non solo del **cosa** fa la riga.

### Passo 1: Installa e importa i moduli richiesti

```python
# Install the library (run once in your environment)
# pip install asposeocr

import asposeocr as ocr
from asposeocr.ai import AsposeAI, AsposeAIModelConfig
```

*Perché?* Importare `asposeocr` ci fornisce la classe `OcrEngine`, mentre il sottomodulo `ai` fornisce il post‑processore basato su LLM che migliora notevolmente l'output OCR grezzo.

### Passo 2: Crea il motore OCR e abilita il riconoscimento del testo scritto a mano

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Turn on handwritten‑text support – useful for notes, signatures, etc.
ocr_engine.ocr_settings.enable_handwritten_recognition = True
```

Abilitare il riconoscimento della scrittura a mano espande il set di caratteri del motore, così non perderai le scarabocchiature quando **esegui OCR sull'immagine** su file che contengono testo stampato e corsivo misto.

### Passo 3: Carica l'immagine per OCR

```python
# Point the engine at the file you want to process
ocr_engine.load_image("YOUR_DIRECTORY/doc.png")
```

La chiamata `load_image` è il momento in cui **carichi l'immagine per OCR**; se il percorso è errato, il motore solleverà un'eccezione informativa, risparmiandoti errori criptici a valle.

### Passo 4: Esegui la fase OCR grezza

```python
# Execute the recognition pipeline and capture the raw result
raw_result = ocr_engine.recognize()
```

In questa fase ottieni un oggetto `RecognitionResult` che contiene il testo non filtrato, i punteggi di confidenza e i metadati di layout. È spesso rumoroso—da qui la necessità di una pulizia guidata dall'AI.

### Passo 5: Configura il modello AI di Aspose per il post‑processing LLM

```python
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # Pull the model if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # Reduce RAM usage
    gpu_layers=20,                                  # Use 20 GPU layers if a GPU is present
    directory_model_path="YOUR_DIRECTORY/models/ocr_ai"
)
```

Perché preoccuparsi di queste impostazioni?  
- **auto‑download** garantisce che il modello sia disponibile al primo avvio.  
- **int8 quantization** riduce drasticamente la memoria richiesta senza una grande perdita di precisione.  
- **gpu_layers** ti permette di sfruttare una GPU compatibile per un'inferenza più veloce.

### Passo 6: Inizializza il processore AI e collegalo come post‑processore

```python
# Instantiate the AI processor with the configuration above
ai_processor = AsposeAI()
ai_processor.initialize(ai_config)

# Hook the AI processor into the OCR engine
ocr_engine.set_post_processor(ai_processor, None)
```

Collegare il processore significa che ogni volta che chiami `run_postprocessor`, il LLM pulirà l'ortografia, unirà parole spezzate e persino inferirà la punteggiatura mancante.

### Passo 7: Esegui il post‑processore per migliorare l'output OCR

```python
# Apply AI‑driven post‑processing
enhanced_result = ocr_engine.run_postprocessor(raw_result)

# Print the polished text
print(enhanced_result.text)
```

`enhanced_result.text` è solitamente molto più leggibile della stringa grezza—pensalo come un correttore ortografico che comprende anche il contesto.

### Passo 8: Rilascia le risorse

```python
# Free GPU/CPU memory held by the AI model
ai_processor.free_resources()

# Dispose of the OCR engine to close file handles, etc.
ocr_engine.dispose()
```

Pulire è fondamentale nei servizi a lungo termine; altrimenti perderai memoria GPU e alla fine l'applicazione si bloccherà.

---

## Script completo che puoi eseguire oggi

```python
import asposeocr as ocr
from asposeocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Initialise OCR engine with handwritten support
ocr_engine = ocr.OcrEngine()
ocr_engine.ocr_settings.enable_handwritten_recognition = True

# 2️⃣ Load the image you want to analyse
ocr_engine.load_image("YOUR_DIRECTORY/doc.png")   # <-- replace with your path

# 3️⃣ Perform the basic OCR pass
raw_result = ocr_engine.recognize()

# 4️⃣ Set up the AI model for smarter output
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    directory_model_path="YOUR_DIRECTORY/models/ocr_ai"
)

# 5️⃣ Initialise and attach the AI post‑processor
ai_processor = AsposeAI()
ai_processor.initialize(ai_config)
ocr_engine.set_post_processor(ai_processor, None)

# 6️⃣ Enhance the OCR result with the LLM
enhanced_result = ocr_engine.run_postprocessor(raw_result)

# 7️⃣ Show the final, cleaned‑up text
print("=== Enhanced OCR Output ===")
print(enhanced_result.text)

# 8️⃣ Clean up
ai_processor.free_resources()
ocr_engine.dispose()
```

**Output atteso** (esempio per un'immagine di fattura semplice):

```
=== Enhanced OCR Output ===
Invoice #12345
Date: 2024‑04‑01
Total Amount: $1,250.00
Thank you for your business!
```

Nota come lo strato AI ha corretto “Inv0ice” → “Invoice” e ha aggiunto la punteggiatura mancante.

---

## Domande frequenti (e risposte rapide)

- **Ho bisogno di una GPU?** No. Lo script ricade su CPU, ma l'inferenza sarà più lenta.  
- **Posso usare un LLM diverso?** Assolutamente—basta cambiare `hugging_face_repo_id` e regolare `gpu_layers` di conseguenza.  
- **E se la mia immagine è enorme?** Ridimensionala prima (ad es., usando Pillow) per mantenere un uso della memoria ragionevole.  
- **Il riconoscimento della scrittura a mano è sempre attivo?** Puoi attivare/disattivare `enable_handwritten_recognition` a seconda del tuo carico di lavoro.

---

## Conclusione

Ora sai come **riconoscere testo da immagine** usando Aspose OCR, come **caricare l'immagine per OCR** e come **eseguire OCR sull'immagine** con post‑processing potenziato dall'AI. L'esempio completo e eseguibile sopra ti fornisce una solida base per integrare OCR in qualsiasi progetto Python—che si tratti di scansionare ricevute, digitalizzare contratti o estrarre dati da moduli scritti a mano.

Pronto per il passo successivo? Prova a sostituire il modello Qwen con uno più grande, sperimenta diversi schemi di quantizzazione o concatena più immagini per l'elaborazione batch. Le possibilità sono infinite, e il codice che hai appena creato le gestirà con eleganza.

Buona programmazione, e che i risultati del tuo OCR siano sempre cristallini!  

![Screenshot of Python console showing enhanced OCR output](/images/ocr_output.png){alt="Screenshot che mostra come riconoscere testo da immagine usando Aspose OCR"}

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑per‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrai testo da immagine con Aspose OCR – Guida passo‑per‑passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Converti immagine in testo – Esegui OCR su immagine da URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Estrai testo immagine C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}