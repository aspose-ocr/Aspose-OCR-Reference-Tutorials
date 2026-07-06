---
category: general
date: 2026-06-22
description: Preprocessare l'immagine per l'OCR al fine di estrarre il testo dall'immagine
  e migliorare l'accuratezza dell'OCR utilizzando Aspose OCR in Python. Esempio completo
  e funzionante incluso.
draft: false
keywords:
- preprocess image for OCR
- extract text from image
- improve OCR accuracy
language: it
og_description: Preprocessa l'immagine per l'OCR, estrai il testo dall'immagine e
  migliora l'accuratezza dell'OCR con Aspose OCR. Scopri il flusso di lavoro completo
  in Python.
og_title: Preelaborazione dell'immagine per OCR – Tutorial completo in Python
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Preprocess image for OCR to extract text from image and improve OCR
    accuracy using Aspose OCR in Python. Complete, runnable example included.
  headline: Preprocess Image for OCR – Step‑by‑Step Python Guide
  type: TechArticle
- description: Preprocess image for OCR to extract text from image and improve OCR
    accuracy using Aspose OCR in Python. Complete, runnable example included.
  name: Preprocess Image for OCR – Step‑by‑Step Python Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Aspose OCR’s wheels target modern interpreters. | | `aspose-ocr` package
      (`pip install aspose-ocr`) | Provides the `OcrEngine`, `ImagePreprocessor`,
      and filter classes. | | A sample image (e.g., `noisy-document.jpg`) |'
  - name: – Initialise the OCR Engine and Load Your Source Image
    text: '```python import aspose.ocr as ocr'
  - name: – Build a Preprocessing Chain to Clean the Image
    text: '```python # Initialise the preprocessor – a container for a series of filters
      preprocessor = ocr.ImagePreprocessor()'
  - name: – Attach the Preprocessor to the Engine
    text: '```python # Hook the preprocessing pipeline into the OCR engine ocr_engine.set_preprocessor(preprocessor)
      ```'
  - name: – Run OCR and Extract Text from Image
    text: '```python # Perform the recognition on the pre‑processed image recognition_result
      = ocr_engine.recognize()'
  - name: – Verify the Output and Fine‑Tune for Better Accuracy
    text: '```python # Quick sanity check: print length and a sample snippet print(f"Detected
      {len(extracted_text)} characters.") print("First 200 chars:", extracted_text[:200])
      ```'
  type: HowTo
- questions:
  - answer: Yes. Convert each page to an image (e.g., using `pdf2image`) and feed
      it through the same pipeline in a loop. The same `preprocess image for OCR`
      steps apply per page.
    question: Does this work with multi‑page PDFs?
  - answer: 'Set the language before recognition: `engine.set_language(ocr.Language.FRENCH)`.
      The preprocessing filters stay the same; only the language model changes.'
    question: What if my document is in a language other than English?
  - answer: 'Absolutely. The `ImagePreprocessor` is extensible—just call `add_filter`
      again. For heavy‑dotted backgrounds, `ocr.Filters.MedianFilter(kernel=3)` can
      be useful. --- ## Wrap‑Up We’ve just **preprocess image for OCR**, run Aspose’s
      engine, and **extract text from image** while showcasing several tric'
    question: Can I chain more filters?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Preelaborazione dell'immagine per OCR – Guida Python passo passo
url: /it/python-java/general/preprocess-image-for-ocr-step-by-step-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Preprocessare l'Immagine per OCR – Tutorial Completo in Python

Se hai bisogno di **preprocessare l'immagine per OCR**, probabilmente ti sei imbattuto in scansioni rumorose, pagine inclinate o foto a basso contrasto che semplicemente non collaborano. Hai mai provato a estrarre testo da un'immagine per poi ottenere un pasticcio incomprensibile? È qui che una solida catena di preprocessing può fare la differenza tra qualche parola leggibile e un incubo di trascrizione completo.

In questa guida percorreremo un esempio completo, end‑to‑end, che **estrae testo da immagine** mostrando anche come **migliorare la precisione OCR** usando Aspose OCR per Python. Niente riferimenti vaghi—solo il codice pronto da copiare‑incollare, la logica dietro ogni riga e consigli per casi reali.

## Cosa Otterrai

- Uno script Python pronto all'uso che carica un documento rumoroso, lo pulisce e stampa il testo riconosciuto.  
- Una comprensione del perché ogni filtro di preprocessing è importante e come regolare i suoi parametri.  
- Strategie per gestire ostacoli comuni come rumore a granelli intenso, rotazioni estreme o scansioni a basso contrasto.  

### Prerequisiti

| Requisito | Perché è importante |
|-----------|---------------------|
| Python 3.8+ | Le wheel di Aspose OCR puntano a interpreti moderni. |
| Pacchetto `aspose-ocr` (`pip install aspose-ocr`) | Fornisce `OcrEngine`, `ImagePreprocessor` e le classi filtro. |
| Un'immagine di esempio (es. `noisy-document.jpg`) | Useremo una foto deliberatamente caotica per mostrare i vantaggi del preprocessing. |
| Familiarità di base con le funzioni Python | Ti aiuta ad adattare lo script al tuo flusso di lavoro. |

> **Consiglio:** Se sei su Windows, esegui lo script all'interno di un ambiente virtuale per evitare conflitti di versione.

---

## Preprocessare l'Immagine per OCR con Aspose OCR (Python)

Di seguito trovi il cuore del tutorial—una spiegazione passo‑a‑passo del codice necessario. Ogni sezione spiega **cosa** facciamo *e* **perché**, così potrai modificare la pipeline in seguito senza indovinare.

![preprocessare immagine per OCR esempio](ocr-preprocess.png){alt="preprocessare immagine per OCR"}

### Passo 1 – Inizializzare l'OCR Engine e Caricare l'Immagine Sorgente

```python
import aspose.ocr as ocr

# Create the OCR engine – the central object that drives recognition
ocr_engine = ocr.OcrEngine()

# Load the raw image file. Using ImageStream lets Aspose handle various formats.
ocr_engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/noisy-document.jpg"))
```

- **Perché** un `OcrEngine`? Incapsula il riconoscitore, le impostazioni di lingua e (in seguito) il preprocessore.  
- **Perché** `ImageStream.from_file`? Astrae la gestione del tipo di file, così puoi sostituire JPEG con PNG senza modificare il codice.

### Passo 2 – Costruire una Catena di Preprocessing per Pulire l'Immagine

```python
# Initialise the preprocessor – a container for a series of filters
preprocessor = ocr.ImagePreprocessor()

# 1️⃣ Deskew – corrects any rotation so text lines become horizontal.
preprocessor.add_filter(ocr.Filters.Deskew())

# 2️⃣ Despeckle – removes isolated noise pixels; strength=2 is a good middle ground.
preprocessor.add_filter(ocr.Filters.Despeckle(strength=2))

# 3️⃣ ContrastBoost – lifts faint characters; level=1.5 amplifies contrast without blowing out highlights.
preprocessor.add_filter(ocr.Filters.ContrastBoost(level=1.5))
```

**Come questi filtri migliorano la precisione OCR:**  
- **Deskew** elimina il comune problema della “pagina inclinata” che confonde la segmentazione dei caratteri.  
- **Despeckle** rimuove i granelli prodotti da scanner di bassa qualità; una forza maggiore elimina più rumore ma può erodere dettagli fini.  
- **ContrastBoost** fa risaltare il testo scuro su sfondi chiari, un vantaggio classico per la maggior parte dei motori OCR.

> **Caso limite:** Se il tuo documento è già perfettamente dritto, puoi saltare `Deskew()` per risparmiare qualche millisecondo.

### Passo 3 – Collegare il Preprocessore al Motore

```python
# Hook the preprocessing pipeline into the OCR engine
ocr_engine.set_preprocessor(preprocessor)
```

Ora, ogni volta che `ocr_engine.recognize()` viene eseguito, prima verranno applicati i tre filtri nell'ordine esatto che abbiamo definito. L'ordine è importante: vuoi **deskew prima del despeckle**, altrimenti il filtro dei granelli potrebbe interpretare i bordi ruotati come rumore.

### Passo 4 – Eseguire OCR ed Estrarre Testo dall'Immagine

```python
# Perform the recognition on the pre‑processed image
recognition_result = ocr_engine.recognize()

# Pull out the plain text string
extracted_text = recognition_result.get_text()
print(extracted_text)
```

- La chiamata `recognize()` restituisce un oggetto `RecognitionResult` che contiene non solo il testo grezzo ma anche punteggi di confidenza, bounding box e dettagli sulla lingua.  
- Qui ci serve solo la stringa semplice, ma potresti esplorare `recognition_result.get_confidence()` per un rapido controllo di **migliorare la precisione OCR**.

### Passo 5 – Verificare l'Uscita e Regolare per Maggiore Precisione

```python
# Quick sanity check: print length and a sample snippet
print(f"Detected {len(extracted_text)} characters.")
print("First 200 chars:", extracted_text[:200])
```

Se l'output contiene ancora simboli incomprensibili, considera queste regolazioni:

| Problema | Correzione Suggerita |
|----------|----------------------|
| Testo ancora sfocato | Aumenta `ContrastBoost(level)` a 2.0 o aggiungi `ocr.Filters.GaussianBlur(radius=1)` prima del despeckle. |
| Troppi caratteri erranti | Alza `Despeckle(strength)` a 3, o inserisci `ocr.Filters.RemoveLines()` per rimuovere le linee orizzontali. |
| L'inclinazione persiste | Chiama `ocr.Filters.Deskew(max_angle=5)` per limitare la correzione a rotazioni lievi. |

---

## Script Completo e Eseguibile

Copia il blocco qui sotto in un file chiamato `ocr_preprocess.py`. Sostituisci `YOUR_DIRECTORY/noisy-document.jpg` con il percorso reale della tua immagine, poi esegui `python ocr_preprocess.py`.

```python
import aspose.ocr as ocr

def main():
    # Initialise engine and load image
    engine = ocr.OcrEngine()
    engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/noisy-document.jpg"))

    # Build preprocessing pipeline
    preproc = ocr.ImagePreprocessor()
    preproc.add_filter(ocr.Filters.Deskew())
    preproc.add_filter(ocr.Filters.Despeckle(strength=2))
    preproc.add_filter(ocr.Filters.ContrastBoost(level=1.5))

    # Attach pipeline
    engine.set_preprocessor(preproc)

    # Recognise and extract text
    result = engine.recognize()
    text = result.get_text()

    # Display results
    print("\n--- OCR Output ---")
    print(text)
    print("\n--- Summary ---")
    print(f"Characters detected: {len(text)}")
    print("Snippet:", text[:200].replace("\n", " "))

if __name__ == "__main__":
    main()
```

Eseguendo questo script su un JPEG rumoroso e leggermente ruotato otterrai testo pulito e leggibile—dimostrando come una catena di preprocessing ben progettata **migliori drasticamente la precisione OCR**.

---

## Domande Frequenti & Risposte

**D: Funziona con PDF multi‑pagina?**  
R: Sì. Converti ogni pagina in un'immagine (es. con `pdf2image`) e passala attraverso la stessa pipeline in un ciclo. Gli stessi passaggi di `preprocessare l'immagine per OCR` si applicano per pagina.

**D: E se il mio documento è in una lingua diversa dall'inglese?**  
R: Imposta la lingua prima del riconoscimento: `engine.set_language(ocr.Language.FRENCH)`. I filtri di preprocessing rimangono invariati; cambia solo il modello linguistico.

**D: Posso concatenare altri filtri?**  
R: Assolutamente. `ImagePreprocessor` è estensibile—basta chiamare nuovamente `add_filter`. Per sfondi con punti pesanti, `ocr.Filters.MedianFilter(kernel=3)` può essere utile.

---

## Conclusione

Abbiamo appena **preprocessato l'immagine per OCR**, eseguito il motore di Aspose e **estratto testo da immagine** mostrando diversi trucchi per **migliorare la precisione OCR**. L'esempio completo è pronto per essere inserito in qualsiasi progetto, e il design modulare dei filtri ti permette di sostituire, aggiungere o rimuovere passaggi a seconda delle esigenze dei tuoi dati.

Prossimi passi consigliati:

- **Elaborazione batch** di decine di scansioni con `concurrent.futures`.  
- **Post‑processing** con librerie di correzione ortografica (es. `pyspellchecker`) per pulire gli errori introdotti dall'OCR.  
- **Integrazione** dello script in un servizio web usando Flask o FastAPI, trasformandolo in un micro‑servizio OCR on‑demand.

Provalo, regola le intensità dei filtri e osserva i tassi di riconoscimento salire. Se incontri difficoltà, lascia un commento—buon coding!

## Cosa Dovresti Imparare Dopo

I tutorial seguenti trattano argomenti strettamente correlati che approfondiscono le tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑a‑passo per aiutarti a padroneggiare ulteriori funzionalità API e a esplorare approcci alternativi nei tuoi progetti.

- [Estrarre Testo da Immagine con Aspose OCR – Guida Passo‑a‑Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Come Usare AspOCR: Filtri di Preprocessing per Immagini OCR in .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Estrarre Testo da Immagine – Ottimizzazione OCR con Aspose.OCR per .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}