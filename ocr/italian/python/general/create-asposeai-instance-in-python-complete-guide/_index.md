---
category: general
date: 2026-06-19
description: Crea rapidamente un'istanza AsposeAI in Python, includendo la configurazione
  predefinita del modello e una callback di logging personalizzata per una migliore
  comprensione.
draft: false
keywords:
- create asposeai instance
- AsposeAI default instance
- Python logging callback
- custom logging for AsposeAI
- AsposeAI model configuration
- using AsposeAI in Python
language: it
og_description: Crea rapidamente un'istanza di AsposeAI in Python. Scopri le configurazioni
  di logging predefinite e personalizzate per un'integrazione AI robusta.
og_title: Crea un'istanza AsposeAI in Python – Guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create AsposeAI instance in Python quickly, covering default model
    configuration and a custom logging callback for better insight.
  headline: Create AsposeAI Instance in Python – Complete Guide
  type: TechArticle
- description: Create AsposeAI instance in Python quickly, covering default model
    configuration and a custom logging callback for better insight.
  name: Create AsposeAI Instance in Python – Complete Guide
  steps:
  - name: 1. Import the AsposeAI class
    text: First we bring the class into the current namespace. This mirrors the typical
      “import‑library” pattern you see in most Python SDKs.
  - name: 2. Spin up the default model configuration
    text: Creating an instance without any arguments gives you the SDK’s built‑in
      model, which is perfect for quick trials.
  - name: 3. Define a simple logging callback
    text: If you want insight into what the SDK is doing—like request payloads or
      internal warnings—you can attach a logging function. Here’s a minimal example
      that just prints to stdout.
  - name: 4. Create an instance that uses the custom logging callback
    text: Now we combine the default model with our logger. The `logging` parameter
      expects a callable that receives a single string argument.
  type: HowTo
tags:
- AsposeAI
- Python
- AI SDK
title: Crea un'istanza AsposeAI in Python – Guida completa
url: /it/python/general/create-asposeai-instance-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea un'istanza AsposeAI in Python – Guida completa

Hai mai dovuto **creare un'istanza AsposeAI** in un progetto Python ma non eri sicuro di quali argomenti del costruttore utilizzare? Non sei solo. Che tu stia prototipando una demo veloce o costruendo un servizio AI di livello produzione, ottenere l'istanza corretta è il primo passo verso risultati affidabili.

In questo tutorial percorreremo l'intero processo: dall'avviare l'**istanza predefinita AsposeAI** al collegare un **callback di logging personalizzato** che ti permette di vedere esattamente cosa sta facendo l'SDK dietro le quinte. Alla fine avrai un oggetto `AsposeAI` funzionante da inserire in qualsiasi script, oltre a una serie di consigli per evitare i soliti problemi.

## Di cosa avrai bisogno

- Python 3.8 o versioni successive installato (l'SDK supporta 3.7+).
- Il pacchetto `asposeai` installato tramite `pip install asposeai`.
- Un terminale o IDE con cui ti trovi a tuo agio (VS Code, PyCharm, o anche un semplice editor di testo).

Non sono necessarie credenziali aggiuntive per il modello predefinito incorporato, così puoi iniziare a sperimentare subito.

## Come creare un'istanza AsposeAI – Passo‑per‑passo

Di seguito trovi una guida concisa, numerata. Ogni passo include uno snippet di codice, una spiegazione del **perché** è importante, e un rapido controllo di coerenza che puoi eseguire.

### 1. Importa la classe AsposeAI

Per prima cosa importiamo la classe nello spazio dei nomi corrente. Questo rispecchia il tipico schema “import‑library” che trovi nella maggior parte degli SDK Python.

```python
# Step 1: Import the AsposeAI class
from asposeai import AsposeAI
```

> **Perché?** L'importazione isola l'API pubblica dell'SDK, mantenendo lo script ordinato ed evitando conflitti di nomi accidentali.

### 2. Avvia la configurazione del modello predefinito

Creare un'istanza senza argomenti ti fornisce il modello incorporato dell'SDK, perfetto per prove rapide.

```python
# Step 2: Create an instance using the default built‑in model configuration
ai_default = AsposeAI()
```

> **Cosa succede dietro le quinte?** `AsposeAI()` carica un modello linguistico leggero, incluso localmente. Non richiede accesso alla rete, quindi puoi eseguirlo offline.

### 3. Definisci un semplice callback di logging

Se vuoi avere visibilità su cosa sta facendo l'SDK—come i payload delle richieste o avvisi interni—puoi collegare una funzione di logging. Ecco un esempio minimale che stampa semplicemente su stdout.

```python
# Step 3: Define a simple logging callback to capture AI messages
def log(message):
    print("[AI] " + message)
```

> **Perché un callback?** L'SDK emette eventi di log tramite una funzione fornita dall'utente. Questo design ti permette di indirizzare i log dove preferisci—stdout, un file o un servizio di monitoraggio.

### 4. Crea un'istanza che utilizza il callback di logging personalizzato

Ora combiniamo il modello predefinito con il nostro logger. Il parametro `logging` si aspetta un callable che riceve un singolo argomento stringa.

```python
# Step 4: Create an instance that uses the custom logging callback
ai_with_logging = AsposeAI(logging=log)
```

> **Risultato:** Ogni messaggio interno generato dall'SDK verrà ora stampato con il prefisso `[AI]`, fornendoti visibilità in tempo reale.

#### Output previsto (esempio)

Eseguire lo snippet sopra non produrrà output immediatamente perché l'SDK registra solo durante le chiamate di inferenza reali. Per vederlo in azione, prova una chiamata rapida `generate` (mostrata nella sezione successiva).

## Utilizzare l'istanza predefinita AsposeAI

Una volta ottenuto `ai_default`, puoi chiamare i suoi metodi come qualsiasi altro oggetto Python. Ecco un esempio base di generazione di testo:

```python
# Generate a short response using the default instance
response = ai_default.generate(prompt="Explain the difference between AI and ML.")
print("Response:", response)
```

Output tipico della console:

```
Response: AI (Artificial Intelligence) is the broader concept...
```

Nessun log appare perché non abbiamo fornito un logger, ma la chiamata ha successo, confermando che **creare un'istanza AsposeAI** funziona subito.

## Aggiungere un callback di logging personalizzato (Esempio completo)

Combiniamo tutto in un unico script che crea l'istanza e dimostra il logging:

```python
from asposeai import AsposeAI

def log(message):
    # Simple logger that timestamps each line
    from datetime import datetime
    timestamp = datetime.now().strftime("%H:%M:%S")
    print(f"[{timestamp}] [AI] {message}")

# Create the instance with custom logging
ai = AsposeAI(logging=log)

# Trigger a request to see logs in action
result = ai.generate(prompt="What is the capital of France?")
print("Result:", result)
```

Esempio di output della console:

```
[12:34:56] [AI] Sending request to AsposeAI service...
[12:34:56] [AI] Received response (status 200)
Result: Paris
```

> **Perché è importante:** Il log mostra il ciclo di vita della richiesta, il che è inestimabile quando si debugga timeout di rete o discrepanze nei payload.

## Verificare che l'istanza funzioni su diversi ambienti

Una configurazione robusta del **modello AsposeAI** dovrebbe comportarsi allo stesso modo su Windows, macOS e Linux. Per confermare:

1. Esegui lo script su ciascun OS.
2. Verifica che la stringa di risposta non sia vuota e che le righe di log compaiano (se hai abilitato il logging).
3. Facoltativamente, verifica l'output in un test unitario:

```python
import unittest

class TestAsposeAI(unittest.TestCase):
    def test_default_instance(self):
        ai = AsposeAI()
        out = ai.generate(prompt="2+2")
        self.assertIn("4", out)

if __name__ == "__main__":
    unittest.main()
```

Se il test passa, hai creato con successo **un'istanza AsposeAI** che funziona in una pipeline CI.

## Problemi comuni e consigli professionali

| Sintomo | Causa probabile | Soluzione |
|---------|-----------------|-----------|
| `ImportError: cannot import name 'AsposeAI'` | Pacchetto non installato o ambiente Python errato | Esegui `pip install asposeai` nello stesso interprete |
| Nessun log appare anche dopo aver passato `logging=log` | Firma del callback non corrispondente (deve accettare una singola stringa) | Assicurati che sia `def log(message):` e non `def log(*args)` |
| `generate` si blocca indefinitamente | Rete bloccata (quando si usano modelli cloud) | Passa al modello predefinito incorporato o configura un proxy |
| La risposta è vuota | Prompt troppo breve o modello non caricato | Fornisci un prompt più lungo e chiaro; verifica che `ai` non sia `None` |

> **Consiglio pro:** Mantieni il logger leggero. I/O pesante (come scrivere su un DB remoto) all'interno del callback può rallentare drasticamente l'inferenza.

## Prossimi passi – Estendere la tua configurazione AsposeAI

Ora che sai come **creare un'istanza AsposeAI** con logging predefinito e personalizzato, considera questi argomenti di approfondimento:

- **Utilizzare la configurazione del modello AsposeAI** per caricare un modello fine‑tuned da un percorso locale.
- **Integrare con codice asincrono** (`await ai.generate_async(...)`) per servizi ad alta velocità.
- **Reindirizzare i log su un file** o su un sistema di logging strutturato come `loguru` per diagnostica in produzione.
- **Combinare più istanze** (ad esempio, una per risposte rapide, un'altra per ragionamento pesante) nella stessa applicazione.

Ognuno di questi si basa sulle fondamenta che abbiamo posto, permettendoti di scalare da uno script semplice a un backend AI completo.

---

*Buon coding! Se incontri problemi mentre provi a **creare un'istanza AsposeAI**, lascia un commento qui sotto—sarò felice di aiutarti.*

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come estrarre OCR – Configurazione OCR](/ocr/english/net/ocr-configuration/)
- [Estrai testo da immagine C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Estrai testo da immagini usando l'operazione OCR su cartelle](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}