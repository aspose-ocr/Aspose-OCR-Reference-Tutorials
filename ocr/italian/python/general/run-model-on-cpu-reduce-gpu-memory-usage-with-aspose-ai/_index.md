---
category: general
date: 2026-06-22
description: Esegui il modello su CPU e impara a ridurre l'uso della memoria GPU configurando
  i layer GPU in Aspose AI. Guida passo passo con snippet di codice.
draft: false
keywords:
- run model on cpu
- reduce gpu memory usage
- limit gpu layers
- configure gpu layers
language: it
og_description: Esegui il modello sulla CPU e riduci il consumo di memoria della GPU
  configurando i layer GPU. Tutorial completo per la configurazione del modello Aspose
  AI.
og_title: Esegui il modello sulla CPU – Riduci l'uso della memoria GPU
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Run model on CPU and learn to reduce GPU memory usage by configuring
    GPU layers in Aspose AI. Step-by-step guide with code snippets.
  headline: Run Model on CPU – Reduce GPU Memory Usage with Aspose AI
  type: TechArticle
- description: Run model on CPU and learn to reduce GPU memory usage by configuring
    GPU layers in Aspose AI. Step-by-step guide with code snippets.
  name: Run Model on CPU – Reduce GPU Memory Usage with Aspose AI
  steps:
  - name: Attach any required post‑processors.
    text: Attach any required post‑processors.
  - name: Choose a configuration (`gpu_layers=0` for pure CPU, or a modest number
      for mixed mode).
    text: Choose a configuration (`gpu_layers=0` for pure CPU, or a modest number
      for mixed mode).
  - name: Initialize the model with that configuration.
    text: Initialize the model with that configuration.
  - name: Verify placement and run a test inference.
    text: Verify placement and run a test inference.
  type: HowTo
tags:
- AsposeAI
- CPU inference
- GPU optimization
title: Esegui il modello su CPU – Riduci l'uso della memoria GPU con Aspose AI
url: /it/python/general/run-model-on-cpu-reduce-gpu-memory-usage-with-aspose-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui il modello su CPU – Riduci l'uso della memoria GPU con Aspose AI

Ti sei mai chiesto come **run model on CPU** quando il tuo server non ha una GPU a disposizione? O forse stai combattendo errori di out‑of‑memory su una GPU modesta e hai bisogno di **reduce GPU memory usage** senza sacrificare troppo la velocità. In questa guida ti mostreremo esattamente questo: collegare un post‑processor, inizializzare Aspose AI sulla CPU e regolare il numero di layer GPU per mantenere le impronte di memoria ridotte.

Copriremo tutto, dalla prima riga di codice alla convalida che il modello stia effettivamente usando la configurazione richiesta. Alla fine sarai in grado di **run model on CPU**, **limit GPU layers** e **configure GPU layers** per qualsiasi carico di lavoro—niente magia, solo puro Python.

## Prerequisiti

- Python 3.8+ installato (il codice usa type hints ma funziona anche su versioni precedenti)
- Pacchetto `asposeai` (installalo tramite `pip install asposeai`)
- Familiarità di base con i concetti di inferenza delle reti neurali (non serve un dottorato, solo curiosità)
- Opzionale: una macchina con GPU per testare il contrasto tra esecuzioni su CPU e GPU

Se ti manca qualcuno di questi, procedi prima all'installazione dell'SDK; il resto del tutorial presuppone che l'importazione funzioni.

![Diagram illustrating how to run model on cpu instead of gpu](run-model-on-cpu-diagram.png)

## Passo 1: Collegare il Post‑Processor di Controllo Ortografico (Nessuna Impostazione Personalizzata Necessaria)

Prima ancora di pensare a CPU o GPU, colleghiamo il post‑processor di controllo ortografico fornito da Aspose AI. È una buona abitudine collegare i post‑processor subito, così fanno parte di ogni chiamata di inferenza.

```python
from asposeai import AI, spell_check_processor

# Create the AI client
ai = AI()

# Attach the built‑in spell‑check processor; no custom settings required
ai.set_post_processor(spell_check_processor, custom_settings={})
```

*Perché è importante:* i post‑processor vengono eseguiti **after** che il modello produce token grezzi. Collegandoli ora, garantisci che qualsiasi testo generato in seguito—sia su CPU che su GPU—venga pulito automaticamente. È un piccolo passo che previene bug a valle.

## Passo 2: Eseguire il modello su CPU – Inizializzare Aspose AI senza GPU

Ecco la parte centrale del tutorial: indicare ad Aspose AI di **run model on CPU**. L'SDK espone `AsposeAIModelConfig`, dove il parametro `gpu_layers` controlla quante layer rimangono sulla GPU. Impostandolo a `0` si forza l'intera rete sulla CPU.

```python
from asposeai import AsposeAIModelConfig

# Initialize the model configuration to use zero GPU layers (i.e., CPU only)
cpu_config = AsposeAIModelConfig(gpu_layers=0)

# Apply the configuration; this will load the model onto the CPU
ai.initialize(cpu_config)

print("✅ Model initialized on CPU – ready for inference.")
```

*Cosa succede dietro le quinte?* Quando `gpu_layers=0`, il runtime assegna tutti i tensori nella memoria host. Questo elimina la necessità di driver CUDA, rendendo lo script eseguibile su praticamente qualsiasi server. Il compromesso è una velocità di throughput più lenta, ma per lavori batch o prototipi a bassa latenza la semplicità spesso supera la pura velocità.

## Passo 3: Limitare le layer GPU per Ridurre l'Uso della Memoria GPU

Se disponi di una GPU ma la memoria è limitata, puoi **limit GPU layers** invece di spostare tutto sulla CPU. Mantenendo solo alcune delle prime layer sulla GPU, benefici ancora dell'accelerazione hardware riducendo drasticamente il consumo di memoria.

```python
# Example: keep only the first 10 layers on the GPU; the rest run on CPU
limited_gpu_config = AsposeAIModelConfig(gpu_layers=10)

ai.initialize(limited_gpu_config)

print("✅ Model initialized with 10 GPU layers – memory usage trimmed.")
```

*Perché limitare le layer GPU aiuta:* I moderni modelli transformer allocano la maggior parte della memoria per layer. Rimuovere anche solo alcune layer dalla GPU può liberare centinaia di megabyte. Questo approccio è perfetto per i “memory‑constrained jobs” dove vuoi ancora un'accelerazione per i calcoli più intensi.

## Passo 4: Configurare le layer GPU per una Gestione Flessibile della Memoria

A volte è necessario un approccio più granulare—magari vuoi **configure GPU layers** in base alla dimensione specifica del lavoro. L'SDK ti permette di leggere il conteggio totale delle layer del modello e calcolare un numero sicuro di layer GPU a runtime.

```python
# Determine total number of layers (this is model‑specific; assume 36 for illustration)
total_layers = ai.model_info.total_layers  

# Choose a safe percentage, e.g., 25% of layers on GPU
gpu_layer_fraction = 0.25
desired_gpu_layers = int(total_layers * gpu_layer_fraction)

# Build the config dynamically
dynamic_config = AsposeAIModelConfig(gpu_layers=desired_gpu_layers)

ai.initialize(dynamic_config)

print(f"✅ Configured {desired_gpu_layers}/{total_layers} layers on GPU.")
```

*Consiglio professionale:* Quando esegui su un server condiviso, interroga prima la memoria GPU disponibile (`torch.cuda.get_device_properties(0).total_memory`) e regola `desired_gpu_layers` di conseguenza. Questo passaggio aggiuntivo garantisce di non sovraccaricare la GPU, evitando crash OOM.

## Passo 5: Verificare la Configurazione e Testare l'Inferenza

Dopo aver impostato la configurazione, è consigliabile ricontrollare dove risiede ogni layer. Aspose AI fornisce un metodo diagnostico che restituisce una mappatura delle layer sui dispositivi.

```python
# Retrieve the device placement map
placement = ai.get_layer_placement()

cpu_layers = [l for l, dev in placement.items() if dev == "cpu"]
gpu_layers = [l for l, dev in placement.items() if dev == "gpu"]

print(f"Layers on CPU: {len(cpu_layers)}")
print(f"Layers on GPU: {len(gpu_layers)}")
```

Una volta soddisfatto, esegui una rapida inferenza per vedere tutto in azione:

```python
input_text = "The quick brown fox jumps over the lazy dog."
output = ai.process(input_text)

print("Model output:", output)
```

Se lo script stampa il testo previsto e il report di posizionamento corrisponde alla tua configurazione, hai con successo **run model on CPU**, **reduce GPU memory usage** e **configure GPU layers** per il tuo scenario.

## Problemi Comuni e Come Evitarli

| Sintomo | Causa Probabile | Soluzione |
|---------|-----------------|-----------|
| `CUDA out of memory` error | Troppi layer GPU | Riduci `gpu_layers` o passa a `gpu_layers=0` |
| No output from `ai.process` | Modello non inizializzato | Assicurati che `ai.initialize` sia chiamato **after** aver collegato i post‑processor |
| Slow inference on GPU | Tutti i layer ancora su CPU | Verifica che `gpu_layers` > 0 e che la mappa dei dispositivi mostri l'uso della GPU |
| Unexpected spelling errors | Post‑processor non collegato | Chiama `set_post_processor` prima di `initialize` |

## Bonus: Passare da CPU a GPU al Volo

Poiché l'SDK reinizializza il modello ogni volta che chiami `initialize`, puoi alternare tra CPU e GPU senza riavviare lo script.

```python
def switch_to_cpu():
    ai.initialize(AsposeAIModelConfig(gpu_layers=0))
    print("🔄 Switched to CPU mode.")

def switch_to_gpu(layers=12):
    ai.initialize(AsposeAIModelConfig(gpu_layers=layers))
    print(f"🔄 Switched to GPU mode with {layers} layers.")
```

Basta chiamare `switch_to_cpu()` quando hai bisogno di un'esecuzione a bassa memoria, e `switch_to_gpu(12)` quando sei pronto per un'accelerazione.

## Conclusione

Abbiamo illustrato un esempio completo e pratico su come **run model on CPU**, **reduce GPU memory usage**, **limit GPU layers** e **configure GPU layers** con Aspose AI. I passaggi sono semplici:

1. Collega tutti i post‑processor necessari.  
2. Scegli una configurazione (`gpu_layers=0` per CPU pura, o un numero modesto per modalità mista).  
3. Inizializza il modello con quella configurazione.  
4. Verifica il posizionamento ed esegui un'inferenza di prova.  

Con queste tecniche puoi mantenere le tue pipeline di inferenza leggere, evitare costosi crash OOM e comunque estrarre prestazioni da una GPU modesta quando è disponibile. Successivamente potresti esplorare strategie di batching, quantizzazione, o persino spostare parti del modello sulla CPU mantenendo le teste di attenzione sulla GPU—ognuno di questi argomenti si basa direttamente sulla base **configure GPU layers** che hai appena padroneggiato.

Hai domande su un'architettura di modello specifica o hai bisogno di aiuto per regolare il conteggio delle layer per un

## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Aspose OCR Tutorial – Riconoscimento Ottico dei Caratteri](/ocr/english/)
- [Estrai Testo da Immagine con Aspose OCR – Guida Passo‑Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Come Eseguire OCR su Testo di Immagine con Lingua Usando Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}