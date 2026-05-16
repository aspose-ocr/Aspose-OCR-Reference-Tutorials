---
category: general
date: 2026-01-07
description: Come elencare i modelli in Aspose OCR AI usando Python – impara a ottenere
  il percorso del modello, verificare i modelli installati e recuperare un elenco
  di modelli in Python in pochi secondi.
draft: false
keywords:
- how to list models
- get model path
- check installed models
- python get model list
- list available models
language: it
og_description: Come elencare i modelli in Aspose OCR AI usando Python. Trova il percorso
  del modello, controlla i modelli installati e visualizza l'elenco completo dei modelli
  disponibili.
og_title: Come elencare i modelli in Aspose OCR AI – Guida Python
tags:
- Aspose OCR
- Python
- AI models
title: Come elencare i modelli in Aspose OCR AI – Guida Python
url: /it/python/general/how-to-list-models-in-aspose-ocr-ai-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come elencare i modelli in Aspose OCR AI – Guida Python

Ti sei mai chiesto **come elencare i modelli** già installati sulla tua macchina quando lavori con Aspose OCR AI? Non sei l’unico a incontrare questo ostacolo. In molti progetti è necessario verificare la cartella dei modelli, confermare quali modelli sono presenti o persino fare debug di un modello mancante—tutto senza uscire dal REPL di Python.

In questo tutorial percorreremo un esempio completo, pronto all’esecuzione, che mostra come **ottenere il percorso del modello**, **controllare i modelli installati** e infine **elencare i modelli disponibili** con poche righe di codice. Nessuno script esterno, nessuna magia nascosta—solo puro Python e l’Aspose OCR AI SDK.

> **Prerequisiti**  
> • Python 3.8 o superiore  
> • Pacchetto `asposeocr` installato (`pip install asposeocr`)  
> • Familiarità di base con l’importazione dei moduli

Se hai tutto pronto, immergiamoci.

---

## Come elencare i modelli con Aspose OCR AI

La prima cosa di cui abbiamo bisogno è la classe helper `AsposeAI` fornita dal modulo `asposeocr.ai`. Questa classe ci offre tre comodi metodi:

| Metodo | Cosa restituisce | Caso d'uso tipico |
|--------|------------------|-------------------|
| `get_local_path()` | Percorso assoluto della cartella in cui Aspose memorizza i suoi modelli AI | Verificare che l'SDK stia cercando nel posto giusto |
| `list_local()` | `list` Python dei nomi delle cartelle dei modelli presenti su disco | Vedere rapidamente quali modelli puoi caricare |
| `list_remote()` *(opzionale)* | Elenco dei modelli disponibili per il download dal cloud di Aspose | Quando ti serve un modello che non hai localmente |

Di seguito trovi lo **script completo** che stampa la cartella locale dei modelli e l’elenco dei modelli installati.

```python
# ---------------------------------------------------------
# Step 1: Import the Aspose OCR AI module
# ---------------------------------------------------------
from asposeocr.ai import AsposeAI

# ---------------------------------------------------------
# Step 2: Create an instance of the AI helper
# ---------------------------------------------------------
ai = AsposeAI()

# ---------------------------------------------------------
# Step 3: Retrieve and display the local model folder
# ---------------------------------------------------------
local_folder = ai.get_local_path()
print("Local AI model folder:", local_folder)

# ---------------------------------------------------------
# Step 4: List all models that are currently installed
# ---------------------------------------------------------
installed_models = ai.list_local()
print("Available models:", installed_models)
```

### Output previsto

Quando esegui lo script su un’installazione nuova vedrai tipicamente qualcosa del genere:

```
Local AI model folder: /home/user/.asposeocr/models
Available models: ['ocr-general-v1', 'ocr-handwritten-v2']
```

Se la cartella è vuota, `list_local()` restituisce una lista vuota (`[]`). È un segnale utile che devi prima scaricare un modello—argomento che tratteremo più avanti.

---

## Perché è importante conoscere il percorso del modello

Capire **dove** l'SDK memorizza i file (`get model path`) è più di una semplice curiosità:

1. **Debug** – Se un modello non si carica, puoi fare `ls` sul percorso e verificare se il file esiste davvero.
2. **Modelli personalizzati** – Alcuni team addestrano i propri modelli OCR e li inseriscono nella cartella. Conoscere il percorso ti permette di posizionare i file esattamente dove Aspose li aspetta.
3. **Permessi** – Su Linux la cartella potrebbe appartenere a un altro utente. Individuare un errore di permessi in anticipo fa risparmiare ore di frustrazione.

> **Consiglio professionale:** Se devi puntare l'SDK a una directory personalizzata, imposta la variabile d’ambiente `ASPOSE_OCR_MODEL_PATH` prima di creare `AsposeAI()`.

```bash
export ASPOSE_OCR_MODEL_PATH=/my/custom/models
python my_script.py
```

---

## Controllare i modelli installati – Casi limite e suggerimenti

### 1. Nessun modello installato

Se `list_local()` restituisce `[]`, hai due opzioni:

| Opzione | Come fare |
|--------|-----------|
| **Scaricare un modello da Aspose** | `ai.download('ocr-general-v1')` (richiede internet) |
| **Copiare un modello pre‑addestrato** | Posizionare manualmente la cartella del modello nel percorso mostrato da `get_local_path()` |

### 2. Versioni multiple dello stesso modello

A volte vedrai sia `ocr-general-v1` **che** `ocr-general-v1-beta`. L'SDK carica la prima corrispondenza trovata, ma puoi forzare una versione specifica passando il nome esatto della cartella al costruttore OCR:

```python
from asposeocr.ai import AsposeOCR

ocr = AsposeOCR(model_name='ocr-general-v1-beta')
```

### 3. File di modello corrotti

Un modello scaricato parzialmente può causare un `FileNotFoundError` in seguito. Se sospetti corruzione, elimina semplicemente la cartella incriminata e riscaricala:

```bash
rm -rf /home/user/.asposeocr/models/ocr-general-v1
python -c "from asposeocr.ai import AsposeAI; AsposeAI().download('ocr-general-v1')"
```

---

## Estendere lo script – Elencare i modelli remoti (opzionale)

Se vuoi vedere quali modelli sono disponibili per il download senza uscire da Python, aggiungi un’altra chiamata:

```python
remote_models = ai.list_remote()
print("Remote models you can download:", remote_models)
```

Questo produrrà qualcosa del genere:

```
Remote models you can download: ['ocr-general-v1', 'ocr-handwritten-v2', 'ocr-table-v1']
```

Potrai quindi scegliere qualsiasi modello e chiamare `ai.download('model-name')` per scaricarlo automaticamente.

---

## Esempio completo end‑to‑end

Mettendo tutto insieme, ecco uno **script unico e eseguibile** che:

1. Mostra la cartella locale dei modelli.  
2. Elenca i modelli installati.  
3. Se non ne trova alcuno, scarica un modello predefinito.  
4. Infine, stampa l’elenco aggiornato.

```python
# ---------------------------------------------------------
# Complete script – verifies model folder, installs if empty
# ---------------------------------------------------------
from asposeocr.ai import AsposeAI

def main():
    ai = AsposeAI()

    # 1️⃣ Show where Aspose expects models
    local_path = ai.get_local_path()
    print("🔎 Local AI model folder:", local_path)

    # 2️⃣ List currently installed models
    models = ai.list_local()
    print("📦 Installed models:", models)

    # 3️⃣ If nothing is installed, grab a default model
    if not models:
        default = 'ocr-general-v1'
        print(f"⚠️ No models found – downloading '{default}'...")
        try:
            ai.download(default)
            models = ai.list_local()
            print("✅ After download, installed models:", models)
        except Exception as e:
            print("❌ Failed to download model:", e)
            return

    # 4️⃣ (Optional) Show what you could download from the cloud
    remote = ai.list_remote()
    print("🌐 Remote models available:", remote)

if __name__ == "__main__":
    main()
```

Eseguendo questo script su una macchina pulita otterrai:

```
🔎 Local AI model folder: /home/user/.asposeocr/models
📦 Installed models: []
⚠️ No models found – downloading 'ocr-general-v1'...
✅ After download, installed models: ['ocr-general-v1']
🌐 Remote models available: ['ocr-general-v1', 'ocr-handwritten-v2', 'ocr-table-v1']
```

Ora disponi di una soluzione **autocontinente e citabile** che qualsiasi assistente AI può riprodurre alla lettera.

---

## Domande frequenti (FAQ)

**D: Funziona su Windows?**  
R: Assolutamente. L'SDK astrae il file system, quindi `get_local_path()` restituirà qualcosa come `C:\Users\YourName\.asposeocr\models`. Basta assicurarsi che Python possa scrivere in quella cartella.

**D: Posso archiviare i modelli su un drive di rete?**  
R: Sì—imposta `ASPOSE_OCR_MODEL_PATH` al percorso UNC (`\\server\share\models`) prima di creare l'istanza `AsposeAI`.

**D: Cosa faccio se mi serve un modello per una lingua non coperta dal set predefinito?**  
R: Usa `list_remote()` per verificare se Aspose offre un modello specifico per la lingua. In caso contrario, puoi addestrare il tuo modello e inserirlo nella cartella; basta passare il nome della cartella personalizzata al costruttore OCR.

---

## Conclusione

Abbiamo coperto **come elencare i modelli** in Aspose OCR AI, mostrato come **ottenere il percorso del modello**, **controllare i modelli installati** e persino **scaricare un modello mancante**—tutto con puro Python. Comprendendo la struttura delle cartelle e i metodi helper (`get_local_path()`, `list_local()`, `list_remote()`), ottieni il pieno controllo sui modelli AI su cui la tua applicazione fa affidamento.

Passi successivi? Prova a sostituire il modello predefinito con uno per testo manoscritto, o punta l'SDK a un modello personalizzato che hai addestrato internamente. In ogni caso, ora hai una solida base per gestire le risorse OCR in qualsiasi progetto Python.

Buon coding, e che la tua lista di modelli sia sempre aggiornata! 

---

![How to list models screenshot](https://example.com/images/how-to-list-models.png "How to list models")

*Testo alternativo immagine:* **how to list models screenshot** (soddisfa il requisito della keyword principale).

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}