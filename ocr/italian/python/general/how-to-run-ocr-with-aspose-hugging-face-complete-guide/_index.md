---
category: general
date: 2026-04-29
description: Scopri come eseguire l'OCR sulle tue scansioni, utilizzare automaticamente
  il modello Hugging Face e riconoscere il testo dalle scansioni con Aspose OCR in
  pochi minuti.
draft: false
keywords:
- how to run OCR
- use hugging face model
- recognize text from scans
- download model automatically
language: it
og_description: Come eseguire l'OCR su scansioni usando Aspose OCR, scaricare automaticamente
  un modello Hugging Face e ottenere testo pulito e con punteggiatura.
og_title: Come eseguire OCR con Aspose e Hugging Face – Guida completa
tags:
- OCR
- Aspose
- Hugging Face
- Python
title: Come eseguire OCR con Aspose e Hugging Face – Guida completa
url: /it/python/general/how-to-run-ocr-with-aspose-hugging-face-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR con Aspose & Hugging Face – Guida completa

Ti sei mai chiesto **come eseguire OCR** su una pila di documenti scansionati senza passare ore a regolare le impostazioni? Non sei il solo. In molti progetti, gli sviluppatori devono **riconoscere il testo dalle scansioni** rapidamente, ma si imbattono in download dei modelli e post‑processing.

Buone notizie: questo tutorial ti mostra una soluzione pronta all'uso che **utilizza un modello Hugging Face**, lo scarica automaticamente e aggiunge la punteggiatura in modo che l'output sembri scritto da un umano. Alla fine avrai uno script che elabora ogni immagine in una cartella e genera un file `.txt` pulito accanto a ciascuna scansione.

## Cosa ti serve

- Python 3.8+ (il codice usa le f‑string, quindi le versioni più vecchie non vanno bene)
- Pacchetto `aspose-ocr` (installalo con `pip install aspose-ocr`)
- Accesso a Internet per il download del modello al primo avvio  
- Una cartella di scansioni immagine (`.png`, `.jpg` o `.tif`)

Tutto qui—nessun binario extra, nessuna manipolazione manuale del modello. Iniziamo.

![esempio di come eseguire OCR](https://example.com/ocr-demo.png "esempio di come eseguire OCR")

## Passo 1: Importa le classi Aspose OCR e configura l'ambiente

Iniziamo importando le classi necessarie dalla libreria Aspose OCR. Importare tutto all'inizio mantiene lo script ordinato e facilita l'individuazione di dipendenze mancanti.

```python
# Step 1: Import Aspose OCR classes
import os
from aspose.ocr import OcrEngine, AsposeAI, AsposeAIModelConfig
```

*Perché è importante*: `OcrEngine` fa il lavoro pesante, mentre `AsposeAI` ci permette di collegare un modello di linguaggio di grandi dimensioni per un post‑processing più intelligente. Se salti l'import, il resto del codice non verrà nemmeno compilato—quindi non dimenticarlo.

## Passo 2: Configura un modello Hugging Face consapevole della GPU  

Ora indichiamo ad Aspose dove scaricare il modello e quante layer devono essere eseguite sulla GPU. Il flag `allow_auto_download="true"` gestisce automaticamente il **download del modello** per te.

```python
# Step 2: Configure a GPU‑aware AI model (replace with your own model folder)
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=40,                     # use GPU for faster inference
    directory_model_path=r"YOUR_DIRECTORY/models"
)
```

> **Consiglio professionale**: se non hai una GPU, imposta `gpu_layers=0`. Il modello ricadrà sulla CPU, più lenta ma comunque funzionante.

### Perché scegliere un modello Hugging Face?

Hugging Face ospita una collezione enorme di LLM pronti all'uso. Puntando a `Qwen/Qwen2.5-3B-Instruct-GGUF`, ottieni un modello compatto, istruito per istruzioni, che può aggiungere punteggiatura, correggere spaziature e persino sistemare piccoli errori OCR. Questa è l'essenza dell'**uso di un modello Hugging Face** nella pratica.

## Passo 3: Inizializza il motore AI e abilita il post‑processing di punteggiatura  

Il motore AI non serve solo per chat sofisticate—qui colleghiamo un *aggiuntore di punteggiatura* che pulisce l'output grezzo dell'OCR.

```python
# Step 3: Initialise the AI engine and enable punctuation post‑processing
ai_engine = AsposeAI()
ai_engine.set_post_processor("punctuation_adder", {})
```

*Cosa succede?* La chiamata `set_post_processor` registra un post‑processor integrato che viene eseguito dopo che il motore OCR ha terminato. Prende la stringa grezza e inserisce virgole, punti e lettere maiuscole dove necessario, rendendo il testo finale molto più leggibile.

## Passo 4: Crea il motore OCR e collega il motore AI  

Collegare il motore AI al motore OCR ci fornisce un unico oggetto capace sia di leggere i caratteri sia di rifinire il risultato.

```python
# Step 4: Create the OCR engine and attach the AI engine
ocr_engine = OcrEngine()
ocr_engine.set_ai_engine(ai_engine)
```

Se salti questo passo, l'OCR funzionerà comunque, ma perderai il miglioramento della punteggiatura—quindi l'output sembrerà un flusso di parole senza separazioni.

## Passo 5: Elabora ogni immagine in una cartella  

Ecco il cuore del tutorial. Iteriamo su ciascuna immagine, eseguiamo l'OCR, applichiamo il post‑processor e scriviamo il testo pulito in un file `.txt` affiancato.

```python
# Step 5: Run OCR on each image in a folder, post‑process the result, and save the text
scans_folder = r"YOUR_DIRECTORY/scans"
for image_file in os.listdir(scans_folder):
    # Filter only supported image types
    if not image_file.lower().endswith(('.png', '.jpg', '.tif')):
        continue

    image_path = os.path.join(scans_folder, image_file)

    # Recognise text from the image
    ocr_result = ocr_engine.recognize(image_path)

    # Apply the punctuation post‑processor
    ocr_result = ocr_engine.run_postprocessor(ocr_result)

    # Show a brief confidence summary
    print(f"{image_file} – confidence {ocr_result.confidence:.2%}")

    # Save the cleaned text next to the source image
    txt_path = image_path + ".txt"
    with open(txt_path, "w", encoding="utf-8") as txt_file:
        txt_file.write(ocr_result.text)
```

### Cosa aspettarsi

L'esecuzione dello script stampa qualcosa di simile a:

```
invoice_001.png – confidence 96.73%
receipt_2024.tif – confidence 94.12%
```

Ogni riga indica il punteggio di confidenza (un rapido controllo di salute) e crea file come `invoice_001.png.txt`, `receipt_2024.tif.txt`, ecc., contenenti testo punteggiato e leggibile da un umano.

### Casi limite e variazioni

- **Scansioni non inglesi**: cambia `hugging_face_repo_id` con un modello multilingue (ad es., `microsoft/Multilingual-LLM-GGUF`).
- **Lotti grandi**: avvolgi il ciclo in un `concurrent.futures.ThreadPoolExecutor` per l'elaborazione parallela, ma fai attenzione ai limiti di memoria della GPU.
- **Post‑processing personalizzato**: sostituisci `"punctuation_adder"` con il tuo script se hai bisogno di una pulizia specifica per dominio (ad es., rimuovere numeri di fattura).

## Passo 6: Pulisci le risorse  

Quando il lavoro termina, liberare le risorse evita perdite di memoria, soprattutto importante se lo esegui all'interno di un servizio a lunga durata.

```python
# Step 6: Release resources
ai_engine.free_resources()
ocr_engine.dispose()
```

Trascurare questo passo può lasciare memoria GPU occupata, sabotando esecuzioni successive.

## Riepilogo: Come eseguire OCR end‑to‑end  

In poche righe di codice, abbiamo mostrato **come eseguire OCR** su una cartella di scansioni, **usare un modello Hugging Face** che si scarica da solo al primo avvio, e **riconoscere il testo dalle scansioni** con punteggiatura aggiunta automaticamente. Lo script completo è pronto per il copia‑incolla, per aggiustare i percorsi e per l'esecuzione.

## Prossimi passi e argomenti correlati  

- **Post‑processing batch**: esplora `ocr_engine.run_batch_postprocessor` per una gestione di massa ancora più veloce.  
- **Modelli alternativi**: prova la famiglia `openai/whisper` se ti serve anche speech‑to‑text insieme all'OCR.  
- **Integrazione con database**: memorizza il testo estratto in SQLite o Elasticsearch per archivi ricercabili.  

Sentiti libero di sperimentare—cambia modello, regola `gpu_layers` o aggiungi il tuo post‑processor. La flessibilità di Aspose OCR combinata con l'hub di modelli di Hugging Face rende questa base versatile per qualsiasi progetto di digitalizzazione documentale.

---

*Buon coding! Se incontri problemi, lascia un commento qui sotto o consulta la documentazione di Aspose OCR per opzioni di configurazione più approfondite.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}