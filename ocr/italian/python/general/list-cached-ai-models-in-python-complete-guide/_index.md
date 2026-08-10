---
category: general
date: 2026-06-22
description: Scopri come elencare i modelli AI memorizzati nella cache utilizzando
  l'SDK AI in Python. Include i passaggi per recuperare la directory della cache dei
  modelli e gestire efficacemente i modelli AI locali.
draft: false
keywords:
- list cached ai models
- retrieve model cache directory
- list local ai models
- ai sdk python
- manage ai model cache
language: it
og_description: Elenca i modelli AI memorizzati nella cache con Python usando l'SDK
  AI. Segui questo tutorial passo‑passo per recuperare la directory della cache dei
  modelli e gestire i modelli AI locali.
og_title: Elenco dei modelli AI in cache in Python – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  headline: List Cached AI Models in Python – Complete Guide
  type: TechArticle
- description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  name: List Cached AI Models in Python – Complete Guide
  steps:
  - name: Import the AI SDK
    text: '```python # Step 1: Import the AI SDK (replace with the actual package
      name if different) import ai ```'
  - name: List All Cached Models
    text: '```python # Step 2: List all models that are cached locally cached_models
      = ai.list_local() print("Cached models:", cached_models) ```'
  - name: Retrieve the Model Cache Directory
    text: '```python # Step 3: Retrieve the directory where the model files are stored
      cache_dir = ai.get_local_path() print("Model cache directory:", cache_dir) ```'
  - name: Empty Cache
    text: If `ai.list_local()` returns an empty list, you might wonder whether the
      SDK is misconfigured. Double‑check the environment variable `AI_CACHE_DIR` (or
      the SDK’s config file) to ensure it points to a writable location.
  - name: Permissions Issues
    text: When accessing `ai.get_local_path()`, a `PermissionError` can surface on
      restrictive systems. The fix is usually to run the script with appropriate user
      rights or to adjust the directory’s ACLs.
  - name: Version Mismatches
    text: 'Sometimes the cache contains an older version of a model while your code
      requests a newer one. The SDK will automatically download the newer version,
      but you can pre‑empt this by inspecting the version tag in the list:'
  - name: Cleaning Up Old Models
    text: 'If you need to free up space, you can delete a specific model folder directly:'
  type: HowTo
- questions:
  - answer: Yes. The SDK abstracts away OS‑specific paths, so `ai.get_local_path()`
      returns a valid string on Linux, macOS, and Windows.
    question: Does this work on all operating systems?
  - answer: The built‑in `list_local()` only reports locally stored artifacts. For
      remote registries you’d use `ai.list_remote()` (if your SDK version provides
      it).
    question: Can I list models from a remote cache?
  - answer: 'Replace the import line with the actual package name, e.g., `import myai
      as ai`. All subsequent calls stay the same because the API contract is consistent
      across implementations. --- ## Conclusion You now have a solid, production‑ready
      method to **list cached AI models** using the **AI SDK Python** '
    question: What if the SDK name isn’t `ai`?
  type: FAQPage
tags:
- python
- ai
- sdk
title: Elenco dei modelli AI nella cache in Python – Guida completa
url: /it/python/general/list-cached-ai-models-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Elenca i Modelli AI nella Cache in Python – Guida Completa

Ti sei mai chiesto come **elencare i modelli AI nella cache** sul tuo workstation senza dover setacciare cartelle oscure? Non sei solo. Molti sviluppatori si trovano in difficoltà quando devono verificare quali modelli sono già memorizzati localmente, soprattutto quando lavorano con larghezza di banda limitata o distribuzioni offline. In questo tutorial vedrai un modo rapido e senza fronzoli per interrogare l'AI SDK, stampare il contenuto della cache e scoprire esattamente dove si trovano quei file.

Tratteremo anche argomenti correlati come **recuperare la directory della cache dei modelli**, gestire cache vuote e le migliori pratiche per **gestire la cache dei modelli AI** negli script di produzione. Alla fine avrai uno snippet autonomo da inserire in qualsiasi progetto Python.

## Prerequisiti

- Python 3.8 o superiore installato.
- L'AI SDK (il pacchetto `ai`) installato tramite `pip install ai-sdk` o dal repository interno della tua organizzazione.
- Familiarità di base con l'esecuzione di script da riga di comando.

Non sono richieste librerie aggiuntive, quindi l'esempio rimane leggero e portabile.

---

## Elenca i Modelli AI nella Cache – Panoramica Rapida

La prima cosa da fare è importare l'SDK e chiamare le sue funzioni di supporto. L'SDK espone due metodi utili:

1. `ai.list_local()` – restituisce una lista Python di identificatori di modello già presenti nella cache.
2. `ai.get_local_path()` – restituisce la directory assoluta dove risiedono quei file di modello.

Entrambe le chiamate sono sincrone e sollevano un chiaro `AIError` se qualcosa va storto, il che rende la gestione degli errori semplice.

> **Perché usare queste funzioni?**  
> Conoscere l'insieme esatto dei modelli nella cache ti consente di evitare download inutili, debug di incompatibilità di versione e di pulire automaticamente gli artefatti vecchi. È un piccolo pezzo del più ampio flusso di lavoro **AI SDK Python**, ma può farti risparmiare ore di ricerca manuale nel file system.

### Passo 1: Importa l'AI SDK

```python
# Step 1: Import the AI SDK (replace with the actual package name if different)
import ai
```

*Perché è importante:* L'importazione del pacchetto registra le C‑extension sottostanti e carica i file di configurazione (come i percorsi della cache) dal tuo ambiente. Saltare questo passo solleverà un `ModuleNotFoundError` non appena chiami qualsiasi funzione dell'SDK.

### Passo 2: Elenca Tutti i Modelli nella Cache

```python
# Step 2: List all models that are cached locally
cached_models = ai.list_local()
print("Cached models:", cached_models)
```

**Cosa vedrai:** Se hai tre modelli memorizzati, l'output potrebbe apparire così:

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
```

Se la cache è vuota, otterrai una lista vuota:

```
Cached models: []
```

> **Consiglio professionale:** Avvolgi la chiamata in un blocco try/except se sospetti che l'SDK non sia stato inizializzato correttamente.

```python
try:
    cached_models = ai.list_local()
except ai.AIError as e:
    print("Failed to list cached models:", e)
    cached_models = []
```

### Passo 3: Recupera la Directory della Cache del Modello

```python
# Step 3: Retrieve the directory where the model files are stored
cache_dir = ai.get_local_path()
print("Model cache directory:", cache_dir)
```

Output tipico su un sistema Unix‑like:

```
Model cache directory: /home/you/.cache/ai/models
```

Su Windows potresti vedere qualcosa come `C:\Users\you\AppData\Local\ai\models`. Conoscere questo percorso è essenziale quando devi **gestire la cache dei modelli AI** manualmente—ad esempio per eliminare versioni vecchie o copiare file su un'unità condivisa.

---

## Riepilogo Visivo

![Diagramma che mostra come elencare i modelli AI nella cache, recuperare i loro nomi e individuare la directory della cache](https://example.com/images/list-cached-ai-models.png)

*Testo alternativo:* Diagramma che illustra il processo per **elencare i modelli AI nella cache** usando l'AI SDK in Python.

## Gestione dei Casi Limite e delle Trappole Comuni

### Cache Vuota

Se `ai.list_local()` restituisce una lista vuota, potresti chiederti se l'SDK è configurato in modo errato. Controlla nuovamente la variabile d'ambiente `AI_CACHE_DIR` (o il file di configurazione dell'SDK) per assicurarti che punti a una posizione scrivibile.

```python
if not cached_models:
    print("No models are cached. Consider downloading a model first.")
```

### Problemi di Permessi

Quando accedi a `ai.get_local_path()`, può comparire un `PermissionError` su sistemi restrittivi. La soluzione è solitamente eseguire lo script con i diritti utente appropriati o modificare le ACL della directory.

### Incompatibilità di Versione

A volte la cache contiene una versione più vecchia di un modello mentre il tuo codice richiede una più recente. L'SDK scaricherà automaticamente la versione più recente, ma puoi anticipare questo controllando il tag di versione nella lista:

```python
for model in cached_models:
    if "v2" not in model:
        print(f"Model {model} may be outdated.")
```

### Pulizia dei Modelli Vecchi

Se hai bisogno di liberare spazio, puoi eliminare direttamente una cartella di modello specifica:

```python
import shutil, os

def purge_model(model_name):
    path = os.path.join(cache_dir, model_name)
    if os.path.isdir(path):
        shutil.rmtree(path)
        print(f"Purged {model_name} from cache.")
    else:
        print(f"{model_name} not found in cache.")
```

Eseguire `purge_model('bert-base-uncased')` rimuoverà quel modello e libererà spazio su disco.

## Script Completo da Copiare‑Incollare

Di seguito trovi uno script pronto all'uso che combina tutti i passaggi, aggiunge una gestione di base degli errori e stampa un riepilogo amichevole.

```python
#!/usr/bin/env python3
"""
Complete example: list cached AI models and show cache directory.
"""

import ai
import os
import sys
import shutil

def main():
    try:
        # Retrieve cached model list
        cached = ai.list_local()
        print("Cached models:", cached)

        # Retrieve cache directory
        cache_dir = ai.get_local_path()
        print("Model cache directory:", cache_dir)

        # Summarize status
        if not cached:
            print("\n⚠️  No models are currently cached.")
        else:
            print("\n✅  Found {} model(s) in cache.".format(len(cached)))

        # Optional: ask user if they want to purge an old model
        if cached:
            to_purge = input("\nEnter a model name to purge (or press Enter to skip): ").strip()
            if to_purge:
                purge_path = os.path.join(cache_dir, to_purge)
                if os.path.isdir(purge_path):
                    shutil.rmtree(purge_path)
                    print(f"🗑️  Purged {to_purge} from cache.")
                else:
                    print(f"❌  Model {to_purge} not found in cache.")
    except ai.AIError as err:
        print("AI SDK error:", err, file=sys.stderr)
        sys.exit(1)
    except Exception as exc:
        print("Unexpected error:", exc, file=sys.stderr)
        sys.exit(1)

if __name__ == "__main__":
    main()
```

**Output previsto (quando la cache è popolata):**

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
Model cache directory: /home/you/.cache/ai/models

✅  Found 3 model(s) in cache.

Enter a model name to purge (or press Enter to skip):
```

Esegui lo script con `python list_models.py` e saprai immediatamente cosa è presente sul disco.

## Domande Frequenti

**D: Questo funziona su tutti i sistemi operativi?**  
R: Sì. L'SDK astrae i percorsi specifici del sistema operativo, quindi `ai.get_local_path()` restituisce una stringa valida su Linux, macOS e Windows.

**D: Posso elencare i modelli da una cache remota?**  
R: Il `list_local()` integrato riporta solo gli artefatti memorizzati localmente. Per i registri remoti useresti `ai.list_remote()` (se la tua versione dell'SDK lo fornisce).

**D: E se il nome dell'SDK non fosse `ai`?**  
R: Sostituisci la riga di importazione con il nome effettivo del pacchetto, ad esempio `import myai as ai`. Tutte le chiamate successive rimangono le stesse perché il contratto API è coerente tra le implementazioni.

## Conclusione

Ora disponi di un metodo solido e pronto per la produzione per **elencare i modelli AI nella cache** usando la libreria **AI SDK Python**, recuperare la **directory della cache dei modelli** e persino pulire i file vecchi. Questa conoscenza ti aiuta a mantenere l'ambiente ordinato, evitare download ridondanti e debug delle problematiche di versione con facilità.

Pronto per il passo successivo? Prova a estendere lo script per scaricare automaticamente i modelli mancanti, o integralo in una pipeline CI che valida lo stato della cache prima di ogni build. Esplorare le strategie per **gestire la cache dei modelli AI** renderà le tue applicazioni alimentate da AI più veloci e affidabili.

Buona programmazione, e che le tue cache rimangano leggere!

## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come elaborare in batch immagini OCR con List in Aspose.OCR per .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Estrai testo da immagine C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Come estrarre testo da archivi ZIP usando Aspose.OCR per .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}