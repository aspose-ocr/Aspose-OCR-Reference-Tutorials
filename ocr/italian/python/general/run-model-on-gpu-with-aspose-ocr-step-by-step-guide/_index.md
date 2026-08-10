---
category: general
date: 2026-03-26
description: Esegui il modello su GPU usando Aspose OCR. Scopri come scaricare il
  repository di Hugging Face, impostare i layer GPU, importare Aspose OCR e caricare
  il modello Qwen2.5 in pochi minuti.
draft: false
keywords:
- run model on gpu
- download hugging face repo
- import aspose ocr
- set gpu layers
- load qwen2.5 model
language: it
og_description: Esegui il modello su GPU con Aspose OCR. Questo tutorial mostra come
  scaricare un repository Hugging Face, impostare i layer GPU, importare Aspose OCR
  e caricare il modello Qwen2.5.
og_title: Esegui il modello su GPU con Aspose OCR – Guida completa
tags:
- Aspose OCR
- GPU acceleration
- Hugging Face
- Python AI
title: Esegui il modello su GPU con Aspose OCR – Guida passo passo
url: /it/python/general/run-model-on-gpu-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui il modello su GPU con Aspose OCR – Tutorial Completo

Ti sei mai chiesto come **eseguire un modello su GPU** senza dover combattere con codice CUDA a basso livello? Non sei l’unico. Molti sviluppatori si trovano bloccati quando devono accelerare un grande modello di linguaggio ma vogliono comunque la semplicità di una libreria ad alto livello. La buona notizia? Aspose OCR include un motore AI facile da usare che può scaricare un modello direttamente da Hugging Face, quantizzarlo e spostare le prime dozzine di layer sulla tua GPU—tutto in poche righe di Python.

In questa guida percorreremo l’intero processo: **scaricare il repository Hugging Face**, **importare Aspose OCR**, configurare i **layer GPU**, e infine **caricare il modello Qwen2.5**. Alla fine avrai un motore OCR pronto all’uso già in esecuzione sulla tua scheda grafica, e comprenderai perché ogni impostazione è importante.

## Cosa ti servirà

- Python 3.9 o superiore (il codice usa type hints e f‑strings)
- Una GPU compatibile CUDA (opzionale ma consigliata per le prestazioni)
- Accesso a Internet per scaricare il modello da Hugging Face
- Il pacchetto `asposeocr` (`pip install asposeocr`)  

Nessuna altra dipendenza esterna è necessaria—Aspose OCR gestisce il lavoro pesante per te.

## Passo 1: Scarica il repository Hugging Face e importa Aspose OCR

La prima cosa da fare è assicurarsi che i file del modello siano disponibili localmente. `AsposeAIModelConfig` di Aspose OCR può recuperare automaticamente un repository da Hugging Face, così non devi clonare nulla manualmente.

```python
# Step 1: Import the Aspose OCR package
import asposeocr as ocr
from asposeocr import AsposeAI, AsposeAIModelConfig
```

**Perché è importante:** L’importazione del pacchetto ti dà accesso alla classe `AsposeAI`, che avvolge il modello transformer sottostante. L’oggetto `AsposeAIModelConfig` è dove indichi al motore *dove* ottenere il modello e *come* trattarlo (ad es., quantizzazione, allocazione GPU).

> **Consiglio professionale:** Se sei dietro un proxy aziendale, imposta la variabile d’ambiente `HTTPS_PROXY` prima di eseguire lo script—Aspose OCR rispetta le impostazioni proxy standard di Python.

## Passo 2: Imposta i layer GPU per prestazioni ottimali

Eseguire un modello su GPU non è un semplice interruttore “on/off”. Puoi decidere quanti dei primi layer transformer devono rimanere sulla GPU mentre il resto ritorna alla CPU. Questo approccio ibrido è utile quando la memoria della GPU è limitata.

```python
# Step 2: Define the model configuration
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # automatically pull repo if missing
    hugging_face_repo_id="bartowski/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # int8 reduces memory footprint
    gpu_layers=20                                   # first 20 layers run on GPU
)
```

**Perché 20 layer?** Il modello Qwen2.5‑3B ha 32 blocchi transformer. Allocare i primi 20 sulla GPU ti offre un notevole aumento di velocità mantenendo l’uso di memoria sotto controllo su una scheda da 12 GB. Sentiti libero di modificare `gpu_layers` in base al tuo hardware—impostandolo a `0` forzi l’esecuzione solo su CPU, mentre `32` tenta di inserire tutto nella GPU (potrebbe causare OOM su schede modeste).

## Passo 3: Crea il motore AI e carica il modello Qwen2.5

Ora istanziamo il motore e gli forniamo la configurazione appena creata. La chiamata esplicita `initialize` è opzionale—Aspose OCR si inizializza pigramente al primo utilizzo—ma chiamarla in anticipo rende più chiaro il controllo di prontezza.

```python
# Step 3: Create and initialize the AI engine with the configuration
ocr_engine = AsposeAI()
ocr_engine.initialize(model_config)   # explicit call for clarity
```

**Cosa succede dietro le quinte?**  
1. Aspose OCR contatta Hugging Face, scarica il file GGUF (se non è nella cache).  
2. Il file viene convertito in un formato comprensibile al runtime interno.  
3. I primi `gpu_layers` blocchi vengono spostati nella memoria CUDA; il resto rimane sulla CPU.  
4. Il motore si segna come *initialized*, che puoi verificare con `is_initialized()`.

## Passo 4: Verifica che il modello sia pronto per l’esecuzione su GPU

Un rapido controllo di sanità ti salva da errori di runtime criptici in seguito. Il metodo `is_initialized()` restituisce un Boolean, permettendoti di confermare che il download, la conversione e l’allocazione GPU siano riusciti.

```python
# Step 4: Confirm that the engine is ready
print("AI ready:", ocr_engine.is_initialized())
```

Quando tutto procede senza intoppi dovresti vedere:

```
AI ready: True
```

Se ottieni `False`, ricontrolla che i driver CUDA siano aggiornati e che la GPU abbia abbastanza memoria libera per i 20 layer richiesti.

## Opzionale: Esegui un’inferenza OCR veloce per vedere la GPU in azione

Mentre il focus del tutorial è sul caricamento del modello, la maggior parte dei lettori vorrà presto eseguire effettivamente l’OCR. Ecco un esempio minimale che elabora un’immagine locale (`sample.png`) e stampa il testo rilevato.

```python
# Optional: Perform a single OCR inference
image_path = "sample.png"
result = ocr_engine.recognize_image(image_path)

print("Detected text:")
print(result.text)
```

**Perché eseguirlo ora?** Perché la prima inferenza spesso attiva la compilazione JIT dei kernel CUDA. Se misuri il tempo con `time.perf_counter()`, noterai che la seconda esecuzione è drasticamente più veloce—un chiaro segno che il modello sta realmente girando su GPU.

## Problemi comuni & Come risolverli

| Sintomo | Probabile causa | Soluzione |
|---------|-----------------|-----------|
| `RuntimeError: CUDA out of memory` | `gpu_layers` impostato troppo alto per la tua scheda | Riduci `gpu_layers` (ad es., a 12) o passa a quantizzazione `int8` (già attiva). |
| `OSError: Unable to download repository` | Nessuna connessione internet o proxy che blocca | Imposta le variabili d’ambiente `HTTPS_PROXY`/`HTTP_PROXY` o scarica manualmente il file GGUF e punta `hugging_face_repo_id` a un percorso locale. |
| `AttributeError: 'AsposeAI' object has no attribute 'recognize_image'` | Versione più vecchia di `asposeocr` | Aggiorna con `pip install --upgrade asposeocr`. |
| `False` da `is_initialized()` | Incompatibilità driver CUDA | Verifica che `nvidia-smi` mostri una versione driver compatibile con il tuo toolkit CUDA. |

## Riepilogo visivo

![Run model on GPU diagram](run-model-on-gpu.png "Diagram showing model download, GPU layer allocation, and inference flow")

*Testo alternativo:* *diagramma che illustra il download di un repository Hugging Face, l’impostazione dei layer GPU e l’esecuzione del modello Qwen2.5 tramite Aspose OCR.*

## Riepilogo – Cosa abbiamo realizzato

- **Importato Aspose OCR** e le sue classi di supporto AI.  
- **Scaricato automaticamente un repository Hugging Face**, grazie a `allow_auto_download`.  
- **Impostato i layer GPU** (`gpu_layers=20`) per spostare le parti più computazionali sulla scheda grafica.  
- **Caricato il modello Qwen2.5‑3B‑Instruct** con quantizzazione int8, riducendo drasticamente l’uso di memoria.  
- **Verificato** che il motore è pronto (`is_initialized()` restituisce `True`).  

Tutto questo è stato realizzato in meno di 30 righe di Python—senza kernel CUDA personalizzati.

## Prossimi passi & Argomenti correlati

1. **Sperimenta con diverse quantizzazioni** (`float16`, `bfloat16`) per valutare il compromesso tra velocità e accuratezza.  
2. **Scala a modelli più grandi** (es. Qwen2.5‑7B) regolando `gpu_layers` e assicurandoti di avere abbastanza VRAM.  
3. **Elaborazione OCR batch**: passa una lista di percorsi immagine a `ocr_engine.recognize_images()` per aumentare il throughput.  
4. **Integra con FastAPI** per esporre un endpoint REST che esegue OCR su file in ingresso—perfetto per microservizi.  

Se sei interessato a ottimizzazioni GPU più avanzate, consulta la guida ufficiale sulle prestazioni di Aspose OCR o la documentazione del CUDA Toolkit per variabili d’ambiente come `CUDA_VISIBLE_DEVICES`.

---

*Buon coding! Se questo tutorial ti ha aiutato a far girare un modello su GPU, fammelo sapere nei commenti o condividi le tue modifiche. Più sperimentiamo insieme, più velocemente la community impara.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}