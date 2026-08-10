---
category: general
date: 2026-01-12
description: Scopri come visualizzare le informazioni da AsposeAI elencando i modelli
  locali, mostrando il nome del modello, la dimensione e il timestamp dell'ultimo
  utilizzo in un chiaro esempio Python.
draft: false
keywords:
- how to display info
- list local models
- display model name
- show model size
- show last used
language: it
og_description: 'Come visualizzare le informazioni da AsposeAI: elencare i modelli
  locali, mostrare il nome del modello, la dimensione e il timestamp dell''ultimo
  utilizzo con una guida completa in Python.'
og_title: Come visualizzare le informazioni – Elenca i modelli locali, nome, dimensione,
  ultimo utilizzo
tags:
- AsposeAI
- Python
- Model Management
title: Come visualizzare le informazioni – Elenco dei modelli locali, nome, dimensione,
  ultimo utilizzo
url: /it/python/general/how-to-display-info-list-local-models-name-size-last-used/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come visualizzare le informazioni – Elencare i modelli locali, nome, dimensione, ultimo utilizzo

Ti sei mai chiesto **come visualizzare le informazioni** dalla tua installazione di AsposeAI senza dover setacciare i log o l'interfaccia? Non sei l'unico. In molte pipeline di data‑science la prima cosa di cui hai bisogno è un rapido sguardo a quali modelli sono presenti sulla tua macchina, come si chiamano, quanto sono grandi e quando li hai usati l'ultima volta.

È esattamente questo che tratteremo: uno snippet Python conciso, end‑to‑end, che **elenca i modelli locali**, poi **mostra il nome del modello**, **mostra la dimensione del modello** e **mostra il timestamp dell'ultimo utilizzo**. Nessuna libreria esterna, nessuna magia nascosta—solo il client AsposeAI che già possiedi.

Alla fine di questo tutorial potrai inserire il codice in qualsiasi script, eseguirlo e ottenere immediatamente una tabella ordinata dei modelli memorizzati localmente. È perfetto per verificare lo stato degli ambienti, costruire dashboard di salute o semplicemente soddisfare la curiosità su cosa si nasconde sul disco.

## Prerequisiti

- Python 3.8 o superiore (l'esempio utilizza le f‑string, quindi è necessario 3.6+)
- Pacchetto `asposeai` installato (`pip install asposeai`)
- Una licenza AsposeAI valida o una chiave di prova (il client recupererà le credenziali dalle variabili d'ambiente o da un file di configurazione)

Se hai già spuntato queste caselle, ottimo—entriamo nel vivo.

## Passo 1: Come visualizzare le informazioni – Inizializzare il client AsposeAI

Prima di poter **elencare i modelli locali**, ci serve un oggetto client che comunichi con il runtime di AsposeAI. Questo passo è la base; senza di esso il resto del codice solleverebbe un `NameError`.

```python
# Step 1: Create an instance of the AsposeAI client
# The client automatically reads credentials from the environment
aspose_ai = AsposeAI()
```

*Perché è importante*: l'inizializzazione del client stabilisce una sessione con il motore di inferenza locale, caricando eventuali librerie native necessarie. Inoltre verifica che la tua licenza sia attiva, evitando errori criptici in seguito quando proverai a interrogare i modelli.

> **Consiglio professionale**: se esegui questo su un server CI, imposta `ASPOSEAI_LICENSE` nell'ambiente affinché il client possa avviarsi senza prompt interattivi.

## Passo 2: Elencare i modelli locali – Recuperare i modelli disponibili

Ora che il client è pronto, possiamo **elencare i modelli locali**. Il metodo `list_local()` restituisce una collezione di oggetti, ognuno dei quali espone proprietà come `name`, `size_mb` e `last_used`.

```python
# Step 2: Retrieve the list of locally available models
local_models = aspose_ai.list_local()
```

*Cosa succede dietro le quinte*: `list_local()` scandisce la directory in cui AsposeAI memorizza i file dei modelli (`~/.asposeai/models` per impostazione predefinita) e costruisce oggetti di metadati leggeri. È veloce perché non carica i pesi del modello—legge solo un piccolo manifest JSON.

Se ti chiedi se un modello specifico è già nella cache, questa chiamata è il modo più rapido per verificarlo.

## Passo 3: Visualizzare il nome del modello, mostrare la dimensione e l'ultimo utilizzo

Con i modelli in mano, finalmente **visualizziamo le informazioni** iterando sulla collezione e stampando ogni attributo. Qui **visualizziamo il nome del modello**, **mostriamo la dimensione** e **mostriamo l'ultimo utilizzo** in un'unica riga ordinata.

```python
# Step 3: Print each model's name, size (in MB), and last‑used timestamp
print("Available local models:")
print("-" * 50)
for model_info in local_models:
    # Using an f‑string to format the output cleanly
    print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
```

**Output previsto** (i tuoi timestamp saranno diversi):

```
Available local models:
--------------------------------------------------
gpt‑tiny‑en – 120 MB – last used 2025-11-02 14:23:11
bert‑base‑fr – 420 MB – last used 2025-10-18 09:07:45
whisper‑large‑audio – 1580 MB – last used 2025-09-30 22:41:02
```

*Perché lo formattiamo così*: il trattino (`–`) separa i campi per leggibilità, e la riga di intestazione rende l'output della console più scansibile. Se in seguito ti serve un formato leggibile da macchine (CSV, JSON), puoi facilmente sostituire la chiamata `print` con `writer.writerow` o `json.dump`.

### Gestione dei casi limite

- **Nessun modello nella cache** – `list_local()` restituisce una lista vuota. Il ciclo semplicemente non eseguirà alcuna iterazione, lasciandoti solo l'intestazione. Potresti aggiungere una guardia:

  ```python
  if not local_models:
      print("No local models found. Use aspose_ai.download(...) to fetch one.")
  ```

- **Attributi mancanti** – In rari casi un manifest può essere corrotto. Accedere a `model_info.last_used` potrebbe sollevare `AttributeError`. Avvolgi la stampa in un `try/except` se prevedi tali problemi.

- **Directory di modelli molto grandi** – Se hai centinaia di modelli, considera di paginare l'output o scrivere su file anziché stampare a console.

## Riepilogo visivo (opzionale)

Se preferisci un'indicazione visiva rapida, il diagramma qui sotto illustra il flusso dall'inizializzazione del client alla visualizzazione finale.  

![Diagramma che mostra come visualizzare le informazioni dal client AsposeAI](/images/how-to-display-info.png "diagramma di visualizzazione delle informazioni")

*Testo alternativo*: **come visualizzare le informazioni** – schema dell'inizializzazione del client AsposeAI, elencazione dei modelli e visualizzazione delle informazioni.

## Script completo funzionante

Riunendo tutto, ecco lo script completo, pronto da eseguire:

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
How to display info from AsposeAI:
List local models and show each model's name, size, and last‑used timestamp.
"""

from asposeai import AsposeAI

def main():
    # Initialize client
    aspose_ai = AsposeAI()

    # Retrieve local models
    local_models = aspose_ai.list_local()

    # Header
    print("Available local models:")
    print("-" * 50)

    if not local_models:
        print("No local models found. Use aspose_ai.download(...) to fetch one.")
        return

    # Display each model's details
    for model_info in local_models:
        try:
            print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
        except AttributeError:
            # Fallback if any attribute is missing
            print(f"{model_info.name} – info incomplete")

if __name__ == "__main__":
    main()
```

Salvalo come `list_models.py`, rendilo eseguibile (`chmod +x list_models.py`) ed eseguilo:

```bash
./list_models.py
```

Vedrai la lista ordinata mostrata in precedenza.

## Conclusione

Abbiamo percorso **come visualizzare le informazioni** da AsposeAI **elencando i modelli locali**, poi **visualizzando il nome del modello**, **mostrando la dimensione** e **mostrando l'ultimo utilizzo**. L'approccio è leggero, richiede solo il pacchetto standard `asposeai` e può essere inserito in qualsiasi pipeline di automazione o sessione di debug.

Da qui potresti:

- Esportare l'output in CSV per analisi in foglio di calcolo (`module csv`).
- Inviare i timestamp a una dashboard di monitoraggio per avvisare su modelli inattivi.
- Combinare questo script con `aspose_ai.download()` per aggiornare automaticamente i modelli non usati da tempo.

Ricorda, una chiara visibilità sul tuo inventario di modelli fa risparmiare tempo, riduce l'accumulo di spazio e mantiene i tuoi servizi AI in perfetta efficienza. Prova lo script, adatta la formattazione ai tuoi gusti e fallo diventare un punto fermo nel tuo toolbox.

Buon coding, e che i tuoi modelli siano sempre freschi!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}