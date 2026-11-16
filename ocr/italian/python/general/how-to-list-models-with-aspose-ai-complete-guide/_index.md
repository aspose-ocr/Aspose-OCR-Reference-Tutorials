---
category: general
date: 2026-07-05
description: Come elencare i modelli con Aspose AI, abilitare il download automatico
  e scaricare il modello Hugging Face in Python. Segui questo tutorial passo‑passo
  per configurare la cache e iniziare a usare Aspose AI oggi.
draft: false
keywords:
- how to list models
- enable auto download
- download hugging face model
- how to use aspose
- how to set cache
language: it
og_description: Come elencare i modelli con Aspose AI, abilitare il download automatico
  e scaricare un modello Hugging Face. Impara a impostare la cache e a utilizzare
  Aspose AI in pochi minuti.
og_title: Come elencare i modelli con Aspose AI – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  headline: How to list models with Aspose AI – Complete Guide
  type: TechArticle
- description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  name: How to list models with Aspose AI – Complete Guide
  steps:
  - name: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
    text: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
  - name: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
    text: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
  - name: Initialise the AI, then call `list_local()` to see exactly what’s cached.
    text: Initialise the AI, then call `list_local()` to see exactly what’s cached.
  - name: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
    text: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
  type: HowTo
tags:
- Aspose
- Python
- LLM
- Model Management
title: Come elencare i modelli con Aspose AI – Guida completa
url: /it/python/general/how-to-list-models-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come elencare i modelli con Aspose AI – Guida completa

Come elencare i modelli con Aspose AI è una domanda che sorge non appena inizi a sperimentare con grandi modelli linguistici in Python. In questo tutorial vedremo come abilitare **auto download**, configurare una cache locale e scaricare un modello direttamente da Hugging Face—così potrai essere operativo senza dover cercare manualmente i file.

Se ti sei mai chiesto *“come uso Aspose per l'AI basata su OCR?”* o *“qual è il modo più semplice per impostare la cache per i file dei modelli?”* sei nel posto giusto. Alla fine avrai uno script completamente funzionante che elenca tutti i modelli memorizzati localmente, scarica automaticamente quelli mancanti e ti mostra esattamente dove i file risiedono sul disco.

---

## Cosa ti serve

- Python 3.9 o più recente (la libreria utilizza type hints che richiedono un interprete recente)
- Accesso a `pip` per installare il pacchetto **Aspose OCR** (`aocr`).  
  ```bash
  pip install aocr
  ```
- Una connessione internet per il primo download da Hugging Face.
- Una cartella dove desideri conservare la cache dei modelli (ad esempio `./model_cache`).

È tutto—nessun container Docker extra, nessun ambiente virtuale pesante oltre a una pulita installazione di Python.

---

## ## Come elencare i modelli con Aspose AI

Il cuore di questa guida è la capacità di **elencare i modelli** che Aspose AI ha memorizzato nella cache localmente. Una volta configurata la cache, la libreria può enumerare tutto ciò che conosce, rendendo il debug e il controllo delle versioni un gioco da ragazzi.

```python
import aocr

# 1️⃣ Create an Aspose AI instance
ai = aocr.AsposeAI()

# 2️⃣ Configure the model cache and auto‑download behavior
cfg = aocr.AsposeAIModelConfig()
cfg.allow_auto_download = "true"                     # ← enable auto download
cfg.directory_model_path = r"./model_cache"          # ← how to set cache
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

# 3️⃣ Initialise the AI with the config we just built
ai.initialize(cfg)

# 4️⃣ List the models that are already cached locally
print("🗂️ Models cached at:", ai.get_local_path())
print("📦 Available models:", ai.list_local())
```

**Perché funziona:**  
- `AsposeAI()` crea il punto di ingresso di alto livello che comunica con il motore di inferenza sottostante.  
- `AsposeAIModelConfig()` contiene tutte le impostazioni configurabili; impostare `allow_auto_download` su `"true"` indica alla libreria di scaricare automaticamente i file mancanti dal repository specificato.  
- `directory_model_path` è la *directory della cache*—il luogo dove risiedono tutti i binari scaricati.  
- `initialize()` applica la configurazione, eseguendo il primo download se la cache è vuota.  
- Infine, `list_local()` scansiona la cartella della cache e restituisce una lista Python di identificatori di modello, che stampiamo.

### Output previsto (prima esecuzione)

```
🗂️ Models cached at: ./model_cache
📦 Available models: ['Qwen2.5-3B-Instruct-GGUF']
```

Se esegui nuovamente lo script, la libreria salterà il download e semplicemente elencherà il modello già presente, dimostrando che **impostare la cache** è davvero vantaggioso per le esecuzioni successive.

---

## ## Abilita il download automatico per i modelli mancanti

Spesso lavorerai con diversi modelli in vari progetti. Scaricare manualmente ciascuno da Hugging Face può essere noioso. Abilitando il download automatico, Aspose AI si occupa del lavoro pesante.

```python
cfg.allow_auto_download = "true"
```

> **Consiglio professionale:** Mantieni `allow_auto_download` impostato su `"true"` **solo** negli ambienti di sviluppo o CI. In produzione potresti voler bloccare la cache per evitare traffico di rete imprevisto.

Se in seguito decidi di disattivarlo, imposta semplicemente il flag su `"false"` prima di chiamare nuovamente `initialize()`.

---

## ## Scarica il modello Hugging Face al volo

La riga

```python
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
```

indica ad Aspose AI da quale repository remoto scaricare. La libreria supporta qualsiasi modello pubblico su Hugging Face che fornisce un file GGUF. Vuoi un modello diverso? Sostituisci l'ID del repository:

```python
cfg.hugging_face_repo_id = "mistralai/Mistral-7B-Instruct-v0.2"
```

Quando esegui lo script, Aspose AI controlla la cache:

- **Se il modello esiste**, lo carica istantaneamente.  
- **Se non esiste**, il flag di auto‑download avvia un download, salva il file sotto `directory_model_path` e poi lo registra per l'uso immediato.

Questo approccio elimina il processo a due fasi “download‑then‑run” che molti tutorial ti costringono a seguire.

---

## ## Come usare Aspose AI dopo che il modello è stato elencato

Elencare i modelli è solo metà della storia. Una volta che sai che un modello è presente, puoi avviare l'inferenza:

```python
# Assume the model we just listed is the one we want to use
model_name = ai.list_local()[0]

# Create a simple prompt
prompt = "Explain the difference between supervised and unsupervised learning."

# Run inference
response = ai.run_inference(model_name, prompt)

print("🤖 Model response:", response)
```

**Perché è importante:**  
- `run_inference()` astrae la tokenizzazione, il batching e la gestione della GPU.  
- Passando il *nome del modello* ottenuto da `list_local()`, garantisci che la chiamata di inferenza corrisponda al file esatto sul disco.

---

## ## Come impostare la posizione della cache per più progetti

Se gestisci diversi progetti, potresti voler che ciascuno abbia la propria cartella di cache. Il campo `directory_model_path` è semplicemente una stringa, quindi puoi costruirlo dinamicamente:

```python
import os

project_name = "sentiment_analysis"
cache_root   = "./model_cache"
cfg.directory_model_path = os.path.join(cache_root, project_name)
```

Ora ogni progetto ottiene una sottocartella isolata (`./model_cache/sentiment_analysis`), evitando conflitti di versione e rendendo la pulizia semplice.

---

## ## Problemi comuni e come evitarli

| Sintomo | Probabile causa | Soluzione |
|---------|----------------|-----------|
| **`PermissionError` quando si accede alla cache** | Cartella della cache di proprietà di un altro utente (comune su server condivisi) | Crea la cartella manualmente con i permessi corretti: `mkdir -p ./model_cache && chmod 775 ./model_cache` |
| **Il modello non appare mai in `list_local()`** | `allow_auto_download` impostato su `"false"` e il modello non è ancora nella cache | Attiva temporaneamente il flag, esegui una volta, poi disattivalo se desiderato |
| **Versione del modello inattesa** | Due repository diversi condividono lo stesso nome ma hanno file differenti | Fissa l'ID esatto del repository (inclusi tag/commit) o blocca la cache disabilitando l'auto‑download dopo il primo pull riuscito |
| **Errori di out‑of‑memory** | File GGUF di grandi dimensioni su una macchina senza RAM/VRAM sufficienti | Usa un modello più piccolo (ad esempio `Qwen2.5-1.5B`) o imposta `cfg.device = "cpu"` per forzare l'inferenza su CPU |

---

## ## Script completo da copiare‑incollare

Di seguito trovi l'esempio completo, pronto per l'esecuzione, che incorpora tutti i concetti sopra. Salvalo come `list_models_demo.py` ed eseguilo con `python list_models_demo.py`.

```python
# list_models_demo.py
import os
import aocr

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Create the Aspose AI instance
    # ------------------------------------------------------------------
    ai = aocr.AsposeAI()

    # ------------------------------------------------------------------
    # 2️⃣ Build configuration: enable auto download, set cache path,
    #    and point at a Hugging Face repo
    # ------------------------------------------------------------------
    cfg = aocr.AsposeAIModelConfig()
    cfg.allow_auto_download = "true"                               # enable auto download
    cfg.directory_model_path = os.path.abspath("./model_cache")   # how to set cache
    cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

    # ------------------------------------------------------------------
    # 3️⃣ Initialise the AI with the configuration
    # ------------------------------------------------------------------
    ai.initialize(cfg)

    # ------------------------------------------------------------------
    # 4️⃣ Verify cache location and list all locally available models
    # ------------------------------------------------------------------
    print("🗂️ Models cached at:", ai.get_local_path())
    print("📦 Available models:", ai.list_local())

    # ------------------------------------------------------------------
    # 5️⃣ (Optional) Run a quick inference using the first listed model
    # ------------------------------------------------------------------
    if ai.list_local():
        model_name = ai.list_local()[0]
        prompt = "Give a short summary of the Python GIL."
        response = ai.run_inference(model_name, prompt)
        print("\n🤖 Model response:", response)

if __name__ == "__main__":
    main()
```

**Eseguendolo** produrrà un output simile all'esempio precedente, seguito da una risposta concisa del modello. Sentiti libero di sostituire il prompt con qualsiasi cosa ti piaccia—questo è il modo più veloce per verificare che il modello sia davvero utilizzabile dopo aver **elencato i modelli**.

---

## ## Riepilogo

Abbiamo coperto tutto ciò di cui hai bisogno per **elencare i modelli** usando Aspose AI, dall'abilitare **auto download** alla configurazione di una **cache** persistente e al download di un **modello Hugging Face** su richiesta. I punti chiave:

1. Crea un oggetto `AsposeAI` e un `AsposeAIModelConfig`.  
2. Imposta `allow_auto_download = "true"` e punta `directory_model_path` a una cartella che controlli.  
3. Inizializza l'AI, poi chiama `list_local()` per vedere esattamente cosa è nella cache.  
4. Usa il nome del modello elencato per l'inferenza, e sei pronto a costruire applicazioni reali.

---

## Cosa c’è dopo?

- **Sperimenta con modelli diversi** – sostituisci `cfg.hugging_face_repo_id` con un altro repository e osserva come cambia la lista.  
- **Affina la cache**

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [How to Set Aspose OCR License and Verify It in Java](/ocr/english/java/ocr-basics/set-license/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}