---
category: general
date: 2026-08-12
description: Crea rapidamente un'istanza AsposeAI in Python usando la libreria Aspose
  AI OCR per Python. Scopri le impostazioni predefinite e il callback di logging personalizzato
  in pochi minuti.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create asposeai instance
- Aspose AI OCR Python
- custom logging callback
- AsposeAI default settings
- initialize AsposeAI
language: it
lastmod: 2026-08-12
og_description: Crea un'istanza AsposeAI in Python con la libreria ufficiale Aspose
  AI OCR. Questo tutorial mostra come utilizzare le impostazioni predefinite, aggiungere
  un callback di logging personalizzato e verificare che l'istanza funzioni, così
  da poter integrare rapidamente l'OCR.
og_image_alt: Screenshot showing Python code to create AsposeAI instance with optional
  logging
og_title: Crea un'istanza di AsposeAI in Python – guida concisa all'OCR
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Create AsposeAI instance in Python quickly using Aspose AI OCR Python
    library. Learn default settings and custom logging callback in minutes.
  headline: Create AsposeAI instance in Python – concise OCR guide
  type: TechArticle
- description: Create AsposeAI instance in Python quickly using Aspose AI OCR Python
    library. Learn default settings and custom logging callback in minutes.
  name: Create AsposeAI instance in Python – concise OCR guide
  steps:
  - name: Why use the default settings?
    text: '- **Out‑of‑the‑box accuracy:** The SDK ships with a pre‑trained model that
      works well for most printed and handwritten text. - **Zero configuration:**
      No need to specify language packs, image preprocessing, or hardware acceleration
      unless you have specific performance goals.'
  - name: What is a custom logging callback?
    text: A **custom logging callback** is a Python callable that the `AsposeAI` constructor
      invokes whenever it wants to report status, warnings, or errors. By providing
      your own function, you control where and how those messages appear—whether in
      the console, a file, or a monitoring system.
  - name: Why supply a logger?
    text: '- **Visibility:** You see real‑time feedback, which is crucial when processing
      large batches of images. - **Diagnostics:** Errors like “image too blurry” surface
      immediately, allowing you to skip or retry problematic files.'
  type: HowTo
tags:
- AsposeAI
- OCR
- Python
title: Crea un'istanza AsposeAI in Python – guida concisa all'OCR
url: /it/python/general/create-asposeai-instance-in-python-concise-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea un'istanza AsposeAI in Python – guida OCR concisa

Se hai bisogno di **creare un'istanza AsposeAI** in Python, questo tutorial ti guida passo passo. Che tu stia costruendo una pipeline di elaborazione documenti o sperimentando con l'OCR, vedrai come avviare l'oggetto sia con le impostazioni predefinite sia con un callback di logging personalizzato.

La libreria Aspose AI OCR per Python rende l'integrazione dell'OCR semplice, ma molti sviluppatori si chiedono come **inizializzare AsposeAI** correttamente e catturare i messaggi diagnostici. Nelle sezioni seguenti otterrai un esempio completo e eseguibile, spiegazioni sul perché ogni riga è importante e consigli per le difficoltà comuni.

![Esempio di codice Python che crea un'istanza AsposeAI con logging opzionale](image.png "Codice Python che crea un'istanza AsposeAI con logging opzionale")

## Cosa ti servirà

- Python 3.8 o versioni successive installate  
- Accesso al pacchetto **Aspose AI OCR Python** (disponibile via `pip`)  
- Una conoscenza di base delle funzioni Python e dei callback  

Avere questi prerequisiti garantisce che il codice venga eseguito senza configurazioni aggiuntive.

## Passo 1: Installa il pacchetto Aspose AI OCR per Python

La prima cosa da fare è aggiungere l'SDK ufficiale Aspose OCR al tuo ambiente. Il pacchetto si chiama `aspose-ocr`.

```bash
pip install aspose-ocr
```

> **Perché è importante:** la ruota `aspose-ocr` contiene la classe `AsposeAI` e tutte le dipendenze native necessarie per l'OCR on‑device. Saltare questo passo genera un `ImportError` quando provi a importare `AsposeAI`.

## Passo 2: Importa la classe AsposeAI

Ora che l'SDK è presente, importa la classe che rappresenta il motore OCR.

```python
# Step 1: Import the AsposeAI class from the OCR package
from aspose.ocr import AsposeAI
```

> **Spiegazione:** `AsposeAI` è il punto di ingresso per tutte le operazioni OCR. Importarla da `aspose.ocr` segue l'API pubblica del pacchetto, garantendo compatibilità futura con le prossime versioni.

## Passo 3: Crea un'istanza base AsposeAI con impostazioni predefinite

Se non ti serve alcuna configurazione speciale, puoi istanziare il motore con le impostazioni predefinite incorporate.

```python
# Step 2: Create a basic AsposeAI instance with default settings
ai_default = AsposeAI()
```

### Perché usare le impostazioni predefinite?

- **Precisione pronta all'uso:** L'SDK include un modello pre‑addestrato che funziona bene per la maggior parte del testo stampato e scritto a mano.  
- **Zero configurazione:** Non è necessario specificare pacchetti linguistici, pre‑elaborazione delle immagini o accelerazione hardware, a meno che non abbia obiettivi di prestazioni specifici.

> **Consiglio professionale:** mantieni un riferimento a `ai_default` se prevedi di riutilizzare la stessa configurazione OCR su più file. Questo evita il sovraccarico di ri‑inizializzare il modello.

## Passo 4: Definisci un semplice callback di logging

Catturare i messaggi interni ti aiuta a debugare i fallimenti dell'OCR, come formati immagine non supportati o input a bassa risoluzione.

```python
# Step 3: Define a simple logging callback to capture AI messages
def my_logger(message):
    print("AI log:", message)
```

### Che cos'è un custom logging callback?

Un **custom logging callback** è un callable Python che il costruttore `AsposeAI` invoca ogni volta che vuole segnalare stato, avvisi o errori. Fornendo la tua funzione, controlli dove e come quei messaggi appaiono — nella console, in un file o in un sistema di monitoraggio.

## Passo 5: Crea un'istanza AsposeAI che utilizza il callback di logging personalizzato

Passa il callback al costruttore usando il parametro `logging`.

```python
# Step 4: Create an AsposeAI instance that uses the custom logging callback
ai_with_logging = AsposeAI(logging=my_logger)
```

### Perché fornire un logger?

- **Visibilità:** Vedi feedback in tempo reale, fondamentale quando elabori grandi batch di immagini.  
- **Diagnostica:** Errori come “immagine troppo sfocata” emergono immediatamente, permettendoti di saltare o ritentare i file problematici.

> **Attenzione:** il logger deve accettare un singolo argomento stringa; altrimenti, l'SDK solleverà un `TypeError`.

## Passo 6: Verifica che le istanze funzionino

Un rapido controllo di sanità conferma che entrambe le istanze sono pronte a elaborare immagini.

```python
def test_instance(ai_instance, image_path):
    try:
        # Perform a minimal OCR call; we only need the call to succeed
        result = ai_instance.recognize(image_path)
        print("OCR succeeded, detected text length:", len(result.text))
    except Exception as e:
        print("OCR failed:", e)

# Replace with a path to a small test image on your machine
sample_image = "sample.png"

print("Testing default instance:")
test_instance(ai_default, sample_image)

print("\nTesting instance with custom logger:")
test_instance(ai_with_logging, sample_image)
```

**Output previsto (quando `sample.png` contiene testo leggibile):**

```
Testing default instance:
OCR succeeded, detected text length: 42

Testing instance with custom logger:
AI log: Loading OCR model...
AI log: Pre‑processing image...
OCR succeeded, detected text length: 42
```

Se il file manca o l'immagine non è supportata, il logger emetterà un avviso e il blocco di eccezione stamperà il messaggio di errore.

## Varianti comuni e casi limite

| Situazione                              | Approccio consigliato                                                                 |
|----------------------------------------|--------------------------------------------------------------------------------------|
| **Esecuzione su un server headless**       | Disabilita il logging della console passando `logging=None` e reindirizza i log a un file.     |
| **Elaborazione di immagini ad alta risoluzione**  | Usa `ai_instance.set_option('max_image_size', 2000)` per limitare l'uso della memoria.         |
| **Necessità di un modello linguistico specifico**     | Inizializza con `AsposeAI(language='fr')` per migliorare la precisione OCR in francese.           |
| **Thread multipli**                   | Crea un'istanza `AsposeAI` separata per thread; la classe **non** è thread‑safe. |

## Consigli professionali per l'uso in produzione

1. **Riutilizza la stessa istanza** per un batch di immagini. Il modello sottostante viene caricato una sola volta, riducendo drasticamente la latenza.  
2. **Cache l'output del logger** in un handler di file rotante se ti aspetti un alto volume; questo impedisce che la console diventi un collo di bottiglia.  
3. **Convalida le immagini di input** (dimensione, formato) prima di chiamare `recognize` per evitare eccezioni inutili.  
4. **Monitora la memoria**: il motore OCR mantiene un tensor di grandi dimensioni in RAM; tieni sotto controllo la memoria del processo quando elabori migliaia di pagine.

## Riepilogo

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Converti immagine in testo: estrai testo da immagine usando Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Come registrare l'AI con Aspose OCR – Esempio di logger personalizzato](/ocr/english/python/general/how-to-log-ai-with-aspose-ocr-custom-logger-example/)
- [Come fare OCR di testo immagine con lingua usando Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}