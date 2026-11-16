---
category: general
date: 2026-06-19
description: Scopri come eseguire l'OCR su un'immagine usando Aspose OCR e il post‑processore
  AI in Python. Include modello scaricato automaticamente, correzione ortografica
  e accelerazione GPU.
draft: false
keywords:
- perform OCR on image
- Aspose OCR Python
- AI post‑processor
- auto‑downloaded model
- spellcheck post‑processor
- GPU acceleration
language: it
og_description: Esegui OCR su immagine usando Aspose OCR e il post‑processore AI.
  Guida passo‑passo con modello scaricato automaticamente, correzione ortografica
  e accelerazione GPU.
og_title: Esegui OCR su un'immagine – Tutorial completo di Python
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  headline: perform OCR on image with Aspose AI – Full Python Guide
  type: TechArticle
- description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  name: perform OCR on image with Aspose AI – Full Python Guide
  steps:
  - name: Initializes the Aspose OCR engine and loads a sample invoice image.
    text: Initializes the Aspose OCR engine and loads a sample invoice image.
  - name: Runs a basic OCR pass and prints the raw text.
    text: Runs a basic OCR pass and prints the raw text.
  - name: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
    text: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
  - name: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
    text: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
  - name: Releases all resources cleanly.
    text: Releases all resources cleanly.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: Esegui OCR su un'immagine con Aspose AI – Guida completa in Python
url: /it/python/general/perform-ocr-on-image-with-aspose-ai-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su immagine – Tutorial Python Completo

Ti sei mai chiesto come **eseguire OCR su immagine** senza impazzire con decine di librerie? Nella mia esperienza il punto critico è solitamente gestire un motore OCR grezzo, per poi cercare di pulire l'output rumoroso. Fortunatamente, Aspose OCR per Python abbinato al suo post‑processore AI rende l'intera pipeline un gioco da ragazzi.

In questa guida percorreremo un esempio pratico, end‑to‑end, che ti mostra esattamente come **eseguire OCR su immagine**, aumentare la precisione con un modello scaricato automaticamente, abilitare il controllo ortografico e persino sfruttare l'accelerazione GPU quando è disponibile. Quando avrai finito, avrai uno script riutilizzabile da inserire in qualsiasi progetto di fatturazione, scansione di ricevute o digitalizzazione di documenti.

## Cosa Costruirai

Creeremo un piccolo programma Python che:

1. Inizializza il motore Aspose OCR e carica un'immagine di fattura di esempio.  
2. Esegue una prima passata OCR e stampa il testo grezzo.  
3. Configura **Aspose AI** con un **modello scaricato automaticamente** da Hugging Face.  
4. Esegue il **post‑processore AI** (incluso un **post‑processore di correzione ortografica**) per pulire l'output OCR.  
5. Rilascia tutte le risorse in modo pulito.

Nessun servizio esterno, nessuna chiave API—solo poche righe di Python e la potenza di Aspose.

> **Consiglio esperto:** Se lavori su una macchina con una GPU decente, impostare `gpu_layers` può far risparmiare secondi nella fase di post‑processing.

## Prerequisiti

- Python 3.8 o superiore (il codice usa i type hint ma sono opzionali).  
- Pacchetti `aspose-ocr` e `aspose-ai` installati via `pip`.  
  ```bash
  pip install aspose-ocr aspose-ai
  ```  
- Un'immagine di esempio (PNG, JPG o TIFF) posizionata in un percorso accessibile, ad esempio `sample_invoice.png`.  
- (Opzionale) Una GPU con supporto CUDA e i driver appropriati se desideri **accelerazione GPU**.

Ora che le basi sono pronte, immergiamoci nel codice.

![perform OCR on image example](image.png)

## Esegui OCR su immagine – Passo 1: Inizializza il motore OCR e carica l'immagine

La prima cosa di cui abbiamo bisogno è un'istanza del motore OCR. Aspose OCR offre un'API pulita, orientata agli oggetti, che astrae la pre‑elaborazione dell'immagine a basso livello.

```python
from aspose.ocr import OcrEngine

# Initialise the OCR engine
ocr_engine = OcrEngine()
ocr_engine.Language = "en"                     # English; change as needed

# Load the image you want to analyse
ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")
```

**Perché è importante:**  
Impostare la lingua fin dall'inizio indica al motore quale set di caratteri aspettarsi, migliorando velocità e accuratezza. Se lavori con documenti multilingue, basta cambiare `"en"` in `"fr"` o `"de"` a seconda delle necessità.

## Passo 2: Esegui OCR di base e visualizza il testo grezzo

Ora eseguiamo effettivamente il riconoscimento. L'oggetto risultato contiene il testo grezzo, i punteggi di confidenza e persino le bounding box se ti servono in seguito.

```python
# Run OCR
ocr_result = ocr_engine.Recognize()

# Show the unprocessed output
print("Raw OCR output:")
print(ocr_result.Text)
```

Un output tipico può apparire così (nota i caratteri occasionalmente errati):

```
Raw OCR output:
Inv0ice N0: 12345
Date: 2023/09/15
Total Am0unt: $1,2O0.00
```

Puoi vedere gli zero (`0`) dove il motore ha interpretato una “O”. È qui che brilla il **post‑processore AI**.

## Configura Aspose AI – modello scaricato automaticamente e correzione ortografica

Prima di passare il risultato OCR grezzo allo strato AI, dobbiamo indicare ad Aspose AI quale modello utilizzare. La libreria può scaricare automaticamente un modello da Hugging Face, così non devi gestire file `.bin` di grandi dimensioni.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

# Create a model configuration that auto‑downloads the Qwen2.5‑3B‑Instruct model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"   # reduces RAM usage
model_config.gpu_layers = 20                      # use GPU if available

# Initialise the AI engine with the config
ai_engine = AsposeAI(model_config)

# Enable the built‑in spellcheck post‑processor
ai_engine.set_post_processor("spellcheck", None)
```

**Spiegazione delle impostazioni**

| Impostazione | Cosa fa | Quando modificarla |
|--------------|---------|--------------------|
| `allow_auto_download` | Consente ad Aspose di scaricare il modello automaticamente al primo avvio. | Mantieni `true` a meno che tu non abbia pre‑scaricato per uso offline. |
| `hugging_face_repo_id` | Identificatore del modello su Hugging Face. | Sostituiscilo con un modello diverso se ne serve uno specifico per un dominio. |
| `hugging_face_quantization` | Sceglie il livello di quantizzazione (`int8`, `float16`, ecc.). | Usa `int8` per ambienti a bassa memoria; `float16` per maggiore accuratezza. |
| `gpu_layers` | Numero di layer del transformer eseguiti sulla GPU. | Imposta `0` per solo CPU, o un valore fino al totale dei layer del modello (20 per Qwen2.5‑3B). |

## Esegui il post‑processore AI sul risultato OCR

Con il motore pronto, basta alimentare l'output OCR grezzo nella pipeline AI. Il **post‑processore di correzione ortografica** integrato correggerà gli errori evidenti, mentre il modello linguistico potrà riformulare o completare informazioni mancanti se abiliti processori aggiuntivi in seguito.

```python
# Enhance the OCR result using the AI post‑processor
enhanced_result = ai_engine.run_postprocessor(ocr_result)

# Display the cleaned‑up text
print("\nAI‑enhanced OCR output:")
print(enhanced_result.Text)
```

Output previsto dopo la fase di correzione ortografica:

```
AI‑enhanced OCR output:
Invoice No: 12345
Date: 2023/09/15
Total Amount: $1,200.00
```

Nota come gli zero siano stati corretti in lettere corrette e come “Am0unt” sia stato trasformato in “Amount”. Il **post‑processore AI** funziona inviando il testo grezzo al modello selezionato, che restituisce una versione raffinata basata sul suo addestramento.

### Casi limite e consigli

- **Immagini a bassa risoluzione**: Se il motore OCR fatica, considera di ingrandire l'immagine prima (`Pillow` può aiutare) o aumentare `ocr_engine.ImagePreprocessingOptions`.  
- **Script non latini**: Cambia `ocr_engine.Language` nel codice ISO appropriato (`"zh"` per Cinese, `"ar"` per Arabo).  
- **GPU non rilevata**: L'impostazione `gpu_layers` ricade silenziosamente su CPU se non viene trovata una GPU compatibile, quindi non serve gestire errori aggiuntivi.  
- **Limiti di dimensione del modello**: Il modello Qwen2.5‑3B è ~4 GB compresso; assicurati di avere spazio sufficiente per il download automatico.

## Rilascia le risorse – spegnimento pulito

Gli oggetti Aspose mantengono handle nativi, quindi è buona pratica liberarli quando hai finito. Questo evita perdite di memoria, soprattutto in servizi a lungo termine.

```python
# Free AI resources
ai_engine.free_resources()

# Dispose of the OCR engine
ocr_engine.Dispose()
```

Puoi avvolgere l'intero script in un blocco `try…finally` se preferisci una pulizia esplicita.

## Script completo – pronto da copiare e incollare

Di seguito trovi l'intero programma, pronto per l'esecuzione dopo aver sostituito `YOUR_DIRECTORY` con il percorso della tua immagine.

```python
# -*- coding: utf-8 -*-
"""
Full example: perform OCR on image using Aspose OCR + AI post‑processor.
Author: Your Name
Date: 2026‑06‑19
"""

from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = OcrEngine()
    ocr_engine.Language = "en"
    ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Basic OCR
    ocr_result = ocr_engine.Recognize()
    print("Raw OCR output:")
    print(ocr_result.Text)

    # 3️⃣ Configure Aspose AI with auto‑downloaded model
    model_cfg = AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "int8"
    model_cfg.gpu_layers = 20   # GPU acceleration if available

    ai_engine = AsposeAI(model_cfg)
    ai_engine.set_post_processor("spellcheck", None)   # enable spellcheck

    # 4️⃣ AI post‑processing
    enhanced = ai_engine.run_postprocessor(ocr_result)
    print("\nAI‑enhanced OCR output:")
    print(enhanced.Text)

    # 5️⃣ Clean up
    ai_engine.free_resources()
    ocr_engine.Dispose()

if __name__ == "__main__":
    main()
```

Eseguilo con:

```bash
python perform_ocr_on_image.py
```

Dovresti vedere il testo grezzo e quello pulito stampati sulla console.

## Conclusione


## Cosa Dovresti Imparare Dopo?


I tutorial seguenti trattano argomenti strettamente correlati che approfondiscono le tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}