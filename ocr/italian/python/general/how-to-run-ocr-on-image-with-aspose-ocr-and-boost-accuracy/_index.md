---
category: general
date: 2026-09-22
description: Scopri come eseguire l'OCR su un'immagine usando Aspose OCR, configurare
  il modello OCR, estrarre il testo da una fattura e migliorare la precisione dell'OCR
  in Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from invoice
- improve OCR accuracy
- configure OCR model
language: it
lastmod: 2026-09-22
og_description: Esegui l'OCR su un'immagine con Aspose OCR, configura il modello OCR,
  estrai il testo dalla fattura e migliora l'accuratezza dell'OCR in un tutorial completo,
  passo dopo passo.
og_image_alt: Screenshot showing raw OCR and AI‑enhanced text extracted from an invoice
  image
og_title: Esegui OCR su immagine con Aspose OCR – guida completa Python
schemas:
- author: Aspose
  dateModified: '2026-09-22'
  description: Learn how to run OCR on image using Aspose OCR, configure the OCR model,
    extract text from invoice and improve OCR accuracy in Python.
  headline: How to run OCR on image with Aspose OCR and boost accuracy
  type: TechArticle
tags:
- Aspose OCR
- Python
- AI post‑processing
title: Come eseguire l'OCR su un'immagine con Aspose OCR e migliorare l'accuratezza
url: /it/python/general/how-to-run-ocr-on-image-with-aspose-ocr-and-boost-accuracy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR su immagine con Aspose OCR e migliorare l'accuratezza

Se hai bisogno di **eseguire OCR su immagine** file in Python, questa guida ti mostra un flusso di lavoro completo, pronto per la produzione. Vedrai come configurare il modello OCR, estrarre testo dalle foto delle fatture e migliorare l'accuratezza OCR con il post‑processore AI di Aspose.

Elaborare fatture scansionate è un problema comune—l'OCR grezzo restituisce spesso parole errate o numeri interrotti. Alla fine di questo tutorial avrai uno script pronto all'uso che fornisce un'estrazione di testo più pulita e affidabile, e comprenderai perché ogni passaggio di configurazione è importante.

## Prerequisiti

* Python 3.8 o versioni successive installato.
* Una licenza attiva di Aspose OCR (la prova gratuita è valida per la valutazione).
* Un'immagine di fattura di esempio (ad es., `sample_invoice.png`) posizionata in una directory nota.
* Familiarità di base con l'installazione di pacchetti Python.

Non sono richieste dipendenze di sistema aggiuntive; l'SDK gestisce automaticamente i download del modello.

## Passo 1: Installa il pacchetto Aspose OCR

La prima cosa da fare è aggiungere la libreria Aspose OCR al tuo ambiente. Il pacchetto include il modello AI e il post‑processore di cui avrai bisogno più avanti.

```bash
pip install aspose-ocr
```

Eseguendo questo comando si installa `asposeocr`, che fornisce la classe `AsposeAI` usata per **configurare le impostazioni del modello OCR** come i download automatici e l'esecuzione solo su CPU.

## Passo 2: Configura il modello OCR (opzionale ma consigliato)

Il fine‑tuning del modello migliora velocità e accuratezza, specialmente quando esegui OCR su immagini di fatture che contengono molti numeri e caratteri speciali. Il codice seguente dimostra le impostazioni più utili:

```python
import asposeocr as ocr   # import the Aspose OCR package

# Create an AsposeAI instance with default logging
ai = ocr.AsposeAI()

# Enable automatic model download, force CPU execution, and enlarge the context window
ai.allow_auto_download = "true"   # download missing model files automatically
ai.gpu_layers = 0                 # use CPU only – avoids GPU‑related errors on most machines
ai.context_size = 2048           # larger context improves correction quality
```

*Perché questi flag?*  
* `allow_auto_download` garantisce che il modello OCR sia presente anche su una macchina nuova.  
* `gpu_layers = 0` rimuove la necessità di una GPU compatibile CUDA, che molti sviluppatori non possiedono.  
* `context_size` controlla quanti token circostanti l'AI considera durante la correzione degli errori; una finestra più ampia spesso **migliora l'accuratezza OCR** su testi densi come le fatture.

## Passo 3: Inizializza il motore AI

L'inizializzazione verifica che i file del modello siano pronti e li carica in memoria. Saltare questo passaggio può causare un errore di runtime quando successivamente chiami il post‑processore.

```python
# Initialise the AI engine – ensures the model is ready to use
if not ai.is_initialized():
    raise RuntimeError("AI engine failed to initialise")
```

Se il motore fallisce, l'eccezione ti indica esattamente dove si è verificato il problema, risparmiandoti tempo nel debug.

## Passo 4: Esegui il motore OCR standard su un'immagine

Ora puoi **eseguire OCR su immagine** file. La classe `OcrEngine` esegue l'estrazione di testo grezzo senza alcuna correzione basata su AI.

```python
# Path to the invoice image you want to process
image_path = "YOUR_DIRECTORY/sample_invoice.png"

# Perform raw OCR
ocr_result = ocr.OcrEngine().recognize_image(image_path)
```

`ocr_result.text` contiene la stringa semplice riconosciuta dal motore OCR. Per una fattura tipica, potresti vedere cifre mancanti, punteggiatura fuori posto o parole interrotte.

## Passo 5: Applica il post‑processore AI per migliorare l'accuratezza OCR

Il post‑processore AI di Aspose analizza l'output grezzo e corregge gli errori OCR comuni (ad es., “5um” → “Sum”). Eseguire questo passaggio è la chiave per **migliorare l'accuratezza OCR** per i documenti finanziari.

```python
# Apply the AI post‑processor
cleaned_result = ai.run_postprocessor(ocr_result)
```

Il post‑processore utilizza la configurazione impostata nel Passo 2, quindi un `context_size` più grande contribuisce a correzioni più affidabili.

## Passo 6: Estrai il testo dalla fattura e visualizza i risultati

A questo punto hai due versioni del testo estratto: l'output OCR grezzo e la versione migliorata dall'AI. Stampare entrambe ti permette di verificare il miglioramento e ti offre anche la possibilità di registrare i dati originali per scopi di audit.

```python
# Display both the raw and the AI‑enhanced text
print("=== Raw OCR ===")
print(ocr_result.text)

print("\n=== AI‑enhanced ===")
print(cleaned_result.text)
```

**Output tipico**

```
=== Raw OCR ===
Inv0ice No: 12345
Date: 2023/09/15
Total Am0unt: $1,2O0.00

=== AI‑enhanced ===
Invoice No: 12345
Date: 2023/09/15
Total Amount: $1,200.00
```

Nota come il passaggio AI abbia corretto le confusioni zero‑uno e sistemato la formattazione dell'importo—esattamente il tipo di miglioramento di cui hai bisogno quando **estrai testo da fattura** file.

## Passo 7: Rilascia le risorse

Infine, libera le risorse native utilizzate dal motore AI. Questo è particolarmente importante in servizi a lungo termine o lavori batch.

```python
# Release resources when finished
ai.free_resources()
```

Trascurare questa chiamata può provocare perdite di memoria perché il modello sottostante gira in codice nativo.

## Script completo da copiare‑incollare

Di seguito trovi il programma completo e eseguibile che incorpora tutti i passaggi descritti sopra. Sostituisci `YOUR_DIRECTORY` con il percorso reale del tuo file immagine.

```python
import asposeocr as ocr   # import the Aspose OCR package

# Step 1: Create an AsposeAI instance (default logging)
ai = ocr.AsposeAI()

# Step 2: (Optional) Tune the model configuration for this demo
#   • Enable automatic download of the model if missing
#   • Use CPU only (no GPU layers)
#   • Increase context size for better correction quality
ai.allow_auto_download = "true"
ai.gpu_layers = 0
ai.context_size = 2048

# Step 3: Initialise the AI engine – ensures the model is ready to use
if not ai.is_initialized():
    raise RuntimeError("AI engine failed to initialise")

# Step 4: Run the standard OCR engine on an image
image_path = "YOUR_DIRECTORY/sample_invoice.png"
ocr_result = ocr.OcrEngine().recognize_image(image_path)

# Step 5: Apply the AI post‑processor to improve the raw OCR output
cleaned_result = ai.run_postprocessor(ocr_result)

# Step 6: Display both the raw and the AI‑enhanced text
print("=== Raw OCR ===")
print(ocr_result.text)
print("\n=== AI‑enhanced ===")
print(cleaned_result.text)

# Step 7: Release resources when finished
ai.free_resources()
```

Salva questo come `process_invoice.py` ed esegui:

```bash
python process_invoice.py
```

Dovresti vedere il testo grezzo e corretto stampato sulla console, confermando che hai eseguito con successo **OCR su immagine**, **configurato il modello OCR** e **migliorato l'accuratezza OCR** per il tuo compito di estrazione delle fatture.

## Domande comuni e casi limite

| Domanda | Risposta |
|----------|--------|
| *Cosa succede se il modello non riesce a scaricarsi?* | Assicurati che la tua macchina abbia accesso a Internet e che il flag `allow_auto_download` sia impostato su `"true"`. Puoi anche scaricare manualmente il modello dal portale Aspose e puntare `AsposeAI` alla cartella locale tramite `ai.model_path = "path/to/model"` |
| *Posso eseguirlo su una GPU?* | Sì. Imposta `ai.gpu_layers` a un intero positivo (ad es., `2`) e installa le librerie CUDA appropriate. L'esecuzione su GPU accelera grandi batch ma richiede una GPU compatibile. |
| *Come posso elaborare molte fatture in una cartella?* | Avvolgi la logica principale in un ciclo che itera su `os.listdir(folder)`. Ricorda di chiamare `ai.free_resources()` solo dopo che il ciclo è terminato, non dopo ogni file, per mantenere il modello caricato. |
| *Il post‑processore è sicuro per fatture non in inglese?* | Il modello predefinito è addestrato su testo inglese. Per altre lingue, scarica il pacchetto linguistico corrispondente e imposta `ai.language = "fr"` (o il codice ISO appropriato). |
| *Cosa succede se il risultato OCR è vuoto?* | Verifica che `image_path` punti a un'immagine leggibile e che il file non sia corrotto. Puoi anche aumentare `ai.context_size` per fornire al modello più contesto per scansioni di bassa qualità. |

## Prossimi passi

Ora che puoi **eseguire OCR su immagine** e estrarre in modo affidabile **testo da fattura** file, considera queste estensioni:

* **Elaborazione batch** – combina lo script con `multiprocessing` per gestire migliaia di fatture in parallelo.
* **Validazione dei dati** – utilizza espressioni regolari per verificare numeri di fattura, date e valori monetari dopo l'estrazione.
* **Integrazione con database** – memorizza il testo pulito direttamente in PostgreSQL o MongoDB per analisi successive.
* **Fine‑tuning di modello personalizzato** – se disponi di un ampio dataset proprietario, addestra un modello specifico per il dominio e punta `ai.model_path` a esso per una precisione ancora maggiore.

Sperimentando con queste idee, trasformerai una semplice demo OCR in una pipeline di elaborazione documenti robusta che soddisfa i requisiti di produzione.

---

*Ora sai come eseguire OCR su file immagine con Aspose OCR, configurare il modello OCR per prestazioni ottimali e migliorare l'accuratezza OCR usando il post‑processore AI. Applica questi passaggi ai tuoi flussi di lavoro di elaborazione fatture e goditi un'estrazione di testo più pulita e affidabile.*

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come eseguire OCR su fatture – Estrarre testo da immagine con Python](/ocr/english/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/)
- [Estrarre testo da immagine con Aspose OCR – Guida passo‑passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Converti immagine in testo: estrarre testo da immagine usando Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}