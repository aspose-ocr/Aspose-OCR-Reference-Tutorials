---
category: general
date: 2026-06-28
description: Esegui OCR su un'immagine usando Aspose AI ed estrai il testo semplice
  dall'immagine in poche righe di Python. Tutorial passo‑passo per un'integrazione
  rapida.
draft: false
keywords:
- perform OCR on image
- extract plain text from image
- Aspose AI OCR
- Python OCR tutorial
- spell‑check post‑processor
- OCR result handling
language: it
og_description: Esegui l'OCR su un'immagine con Aspose AI ed estrai il testo semplice
  dall'immagine senza sforzo. Scopri l'intero flusso di lavoro in questo breve tutorial.
og_title: Esegui OCR su immagine con Aspose AI – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Perform OCR on image using Aspose AI and extract plain text from image
    in just a few lines of Python. Step‑by‑step tutorial for fast integration.
  headline: Perform OCR on Image with Aspose AI – Complete Guide
  type: TechArticle
- questions:
  - answer: Aspose’s OCR engine works best with 300 dpi or higher. If you’re dealing
      with lower quality scans, consider pre‑processing the image (e.g., sharpening,
      binarisation) before feeding it to `engine.set_image`.
    question: What if the image is low‑resolution?
  - answer: Yes. Loop over a list of image files, re‑using the same `engine` and `ai`
      instances. Just remember to call `engine.set_image` for each new file.
    question: Can I process multiple pages?
  - answer: Only on the first run, when the AI model is downloaded. After that, everything
      runs offline from the cached directory you specified.
    question: Do I need an internet connection?
  - answer: 'Pass a language code in the options dictionary, e.g., `ai.set_post_processor(AIProcessor.SpellCheck,
      {"lang": "fr"})` for French.'
    question: How do I change the language of the spell‑check?
  type: FAQPage
tags:
- OCR
- Python
- Aspose
- AI
title: Esegui OCR su immagine con Aspose AI – Guida completa
url: /it/python/general/perform-ocr-on-image-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine con Aspose AI – Guida Completa

Ti sei mai chiesto come **eseguire OCR su immagine** senza impazzire con librerie ingombranti? In molte applicazioni reali ti basta estrarre il testo da una fattura o da una ricevuta scannerizzata, e poi magari pulirlo con un correttore ortografico. La buona notizia è che Aspose AI rende tutto questo un gioco da ragazzi, e puoi anche **estrarre testo semplice da immagine** in un unico script leggibile.

In questo tutorial percorreremo l’intera pipeline: caricare un’immagine, eseguire OCR, ottenere sia i risultati grezzi che strutturati, applicare il post‑processore di correzione ortografica integrato e, infine, liberare le risorse. Alla fine avrai un esempio Python pronto all’uso da inserire nel tuo progetto.

## Cosa Imparerai

- Come inizializzare il motore Aspose OCR e fornirgli un file immagine.  
- La differenza tra l’output di stringa semplice e un `OcrResult` strutturato che conserva il layout.  
- Come collegare il bridge Aspose AI, scaricare il modello automaticamente e puntarlo a una cartella di cache personalizzata.  
- Utilizzare il post‑processore di correzione ortografica per **estrarre testo semplice da immagine** con ortografia corretta mantenendo le bounding box.  
- Consigli di best‑practice per rilasciare le risorse AI ed evitare perdite di memoria.  

Non è necessaria alcuna esperienza pregressa con Aspose—basta un ambiente Python 3 funzionante e un’immagine a tua scelta. Iniziamo.

![Esempio di esecuzione OCR su immagine](image.png "Diagramma che mostra la pipeline OCR – esegui OCR su immagine")

## Passo 1 – Inizializza il Motore OCR e Carica la Tua Immagine

La prima cosa da fare è avviare il motore OCR e indicargli l’immagine che vuoi leggere. Considera il motore come uno scanner che trasforma i pixel in caratteri.

```python
# Step 1: Initialise the OCR engine and load the image
engine = OcrEngine()
engine.set_image(Image.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **Perché è importante:** `OcrEngine()` crea una nuova sessione, mentre `set_image` indica al motore esattamente quale file analizzare. Se salti questo passaggio, le successive chiamate a `recognize` genereranno un'eccezione perché non c’è nulla da elaborare.

## Passo 2 – Esegui OCR e Ottieni sia Risultati Semplici che Strutturati

Ora eseguiamo davvero **OCR su immagine**. Aspose fornisce due tipologie di output:

1. `plain_text` – una stringa semplice, perfetta quando ti servono solo le parole.  
2. `structured` – un oggetto `OcrResult` che conserva le interruzioni di riga, le bounding box e altri metadati di layout.

```python
# Step 2: Perform OCR – obtain plain text and structured result
plain_text = engine.recognize()                # plain string
structured = engine.recognize_structured()    # OcrResult with layout info
```

> **Suggerimento professionale:** usa `plain_text` quando ti interessano solo i caratteri (ad es., ricerca in un documento). Usa `structured` quando devi mappare il testo alla sua posizione originale, ad esempio per evidenziare errori sulla scansione originale.

## Passo 3 – Inizializza il Bridge Aspose AI (Download del Modello al Primo Utilizzo)

Aspose AI è il cervello che alimenta il post‑processore di correzione ortografica. La prima volta che lo esegui, il modello verrà scaricato automaticamente. Puoi anche fornire una cartella personalizzata per la cache del modello, il che velocizza le esecuzioni successive.

```python
# Step 3: Initialise the Aspose AI bridge (model will be downloaded on first use)
# Optional: specify a custom directory for the cached model
ai_config = AsposeAIModelConfig()
ai_config.directory_model_path = "YOUR_DIRECTORY/models"
ai = AsposeAI(ai_config)
```

> **Perché è importante:** la cache del modello evita chiamate di rete ripetute e mantiene la tua applicazione reattiva, soprattutto negli ambienti di produzione.

## Passo 4 – Registra il Post‑Processore di Correzione Ortografica Integrato

Aspose include un pratico processore di correzione ortografica che funziona sia su stringhe semplici sia su risultati OCR strutturati. Registralo una volta e sarai pronto a correggere eventuali errori tipografici introdotti dall’OCR.

```python
# Step 4: Register the built‑in spell‑check post‑processor
ai.set_post_processor(AIProcessor.SpellCheck, {})
```

> **Nota:** il dizionario vuoto `{}` è il luogo dove potresti passare dizionari personalizzati o impostazioni di lingua se avessi bisogno di più controllo.

## Passo 5 – Applica la Correzione Ortografica al Testo OCR Semplice

Qui è dove **estraiamo testo semplice da immagine** e correggiamo simultaneamente gli errori ortografici. Il metodo `run_postprocessor` prende la stringa grezza e restituisce una versione pulita.

```python
# Step 5: Apply spell‑check to the plain OCR text
corrected_text = ai.run_postprocessor(plain_text)
print("Corrected:", corrected_text)
```

**Output previsto (esempio):**

```
Corrected: Invoice Number 2023‑07‑15
Date: 07/15/2023
Total Amount: $1,250.00
```

> **Perché è importante:** i motori OCR spesso riconoscono erroneamente caratteri come “0” vs “O” o “1” vs “l”. Il passaggio di correzione ortografica elimina questi errori, fornendoti dati più puliti per l’elaborazione successiva.

## Passo 6 – Applica la Correzione Ortografica al Risultato OCR Strutturato (Preserva le Bounding Box)

Se devi mantenere il layout originale—ad esempio per evidenziare le parole corrette sul documento scannerizzato—puoi passare il risultato strutturato allo stesso post‑processore. L’oggetto restituito contiene ancora le informazioni di riga.

```python
# Step 6: Apply spell‑check to the structured OCR result (preserves bounding boxes)
corrected_struct = ai.run_postprocessor(structured)
for line in corrected_struct.Lines:
    print(line.Text)
```

**Esempio di output console:**

```
Invoice Number 2023‑07‑15
Date: 07/15/2023
Total Amount: $1,250.00
```

> **Suggerimento professionale:** poiché la collezione `Lines` conserva le coordinate `BoundingBox`, ora puoi sovrapporre il testo corretto sull’immagine originale usando qualsiasi libreria grafica (Pillow, OpenCV, ecc.).

## Passo 7 – Rilascia le Risorse AI Quando Hai Finito

Le perdite di memoria sono i killer silenziosi dei servizi a lungo termine. Libera sempre le risorse AI una volta completato il lavoro.

```python
# Step 7: Release AI resources when done
ai.free_resources()
```

> **Perché è importante:** `free_resources()` chiude i thread in background e libera il modello dalla memoria, mantenendo la tua applicazione leggera.

## Esempio Completo Funzionante

Mettendo tutto insieme, ecco lo script completo che puoi copiare‑incollare ed eseguire (basta sostituire `YOUR_DIRECTORY` con percorsi reali):

```python
from aspose.ocr import OcrEngine, Image
from aspose.ai import AsposeAI, AsposeAIModelConfig, AIProcessor

# Initialise OCR engine
engine = OcrEngine()
engine.set_image(Image.from_file("YOUR_DIRECTORY/invoice.png"))

# Perform OCR
plain_text = engine.recognize()
structured = engine.recognize_structured()

# Initialise Aspose AI bridge
ai_config = AsposeAIModelConfig()
ai_config.directory_model_path = "YOUR_DIRECTORY/models"
ai = AsposeAI(ai_config)

# Register spell‑check post‑processor
ai.set_post_processor(AIProcessor.SpellCheck, {})

# Correct plain text
corrected_text = ai.run_postprocessor(plain_text)
print("Corrected:", corrected_text)

# Correct structured result
corrected_struct = ai.run_postprocessor(structured)
for line in corrected_struct.Lines:
    print(line.Text)

# Clean up
ai.free_resources()
```

Esegui lo script e vedrai l’output corretto stampato sulla console. Questo è l’intero flusso di lavoro **perform OCR on image** dall’inizio alla fine.

## Domande Frequenti & Casi Limite

- **E se l’immagine è a bassa risoluzione?**  
  Il motore OCR di Aspose funziona al meglio con 300 dpi o superiori. Se lavori con scansioni di qualità inferiore, considera di pre‑elaborare l’immagine (ad es., nitidezza, binarizzazione) prima di passarla a `engine.set_image`.

- **Posso elaborare più pagine?**  
  Sì. Itera su una lista di file immagine, riutilizzando le stesse istanze `engine` e `ai`. Ricorda solo di chiamare `engine.set_image` per ogni nuovo file.

- **Ho bisogno di una connessione internet?**  
  Solo al primo avvio, quando il modello AI viene scaricato. Dopo di che, tutto funziona offline dalla directory di cache specificata.

- **Come cambio la lingua del correttore ortografico?**  
  Passa un codice lingua nel dizionario delle opzioni, ad esempio `ai.set_post_processor(AIProcessor.SpellCheck, {"lang": "fr"})` per il francese.

## Conclusione

Ora sai esattamente come **eseguire OCR su immagine** con Aspose AI e come **estrarre testo semplice da immagine** correggendo automaticamente gli errori OCR comuni. Il tutorial ha coperto l’inizializzazione del motore, i risultati semplici vs strutturati, la cache del modello, l’integrazione della correzione ortografica e la corretta pulizia delle risorse.  

Da qui potresti esplorare l’aggiunta di dizionari personalizzati, l’invio del testo corretto a una pipeline NLP successiva, o il rendering delle bounding box sull’immagine originale per una verifica visiva. Le possibilità sono molte, e il codice che hai appena costruito è una solida base.

Sentiti libero di sperimentare—sostituisci l’immagine, modifica le impostazioni del post‑processore o concatena moduli AI aggiuntivi. Se incontri problemi, lascia un commento qui sotto; buona programmazione!

## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrai Testo da Immagine con Aspose OCR – Guida Passo‑Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Come Usare Aspose OCR per Risultato JSON nel Riconoscimento Immagini](/ocr/english/net/text-recognition/get-result-as-json/)
- [Riconosci testo in immagine con Aspose OCR per più lingue](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}