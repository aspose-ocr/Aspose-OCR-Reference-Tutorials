---
category: general
date: 2026-08-12
description: Esegui OCR su un'immagine usando Python e Aspose AI per estrarre il testo
  dall'immagine e migliorare l'accuratezza dell'OCR con un post‑processore di correzione
  ortografica.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from image
- OCR text correction
- improve OCR accuracy
- load image for OCR
language: it
lastmod: 2026-08-12
og_description: Esegui OCR su un'immagine in Python ed estrai istantaneamente il testo
  dall'immagine migliorando l'accuratezza dell'OCR grazie al post‑processing AI di
  Aspose.
og_image_alt: Diagram showing the run OCR on image workflow in Python
og_title: Esegui OCR su immagine con Python – tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Run OCR on image using Python and Aspose AI to extract text from image
    and improve OCR accuracy with a spell‑checking post‑processor.
  headline: Run OCR on image with Python – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Esegui OCR su un'immagine con Python – guida passo passo
url: /it/python/general/run-ocr-on-image-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su immagine con Python – guida passo‑passo

Se hai bisogno di **eseguire OCR su file immagine** in Python, questa guida ti accompagna attraverso l’intero flusso di lavoro. Imparerai a **estrarre testo da immagine**, applicare **correzione del testo OCR** e **migliorare la precisione OCR** con poche righe di codice.

Elaborare documenti scansionati, ricevute o screenshot spesso genera testo rumoroso. Aggiungendo un correttore ortografico post‑processore puoi trasformare l’output grezzo di OCR in contenuti puliti e ricercabili senza passare a uno strumento separato. Questo tutorial copre tutto ciò che ti serve—dal caricamento dell’immagine alla visualizzazione del risultato corretto.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* Python 3.9 o superiore installato.  
* Accesso ai pacchetti Python Aspose.OCR e Aspose.AI (o ai loro equivalenti open‑source).  
* Un’immagine di esempio (ad es. `sample.png`) collocata in una directory nota.  
* Familiarità di base con le funzioni Python e il codice orientato agli oggetti.

Puoi installare le librerie necessarie con pip:

```bash
pip install aspose-ocr aspose-ai
```

> **Suggerimento:** Usa un ambiente virtuale (`python -m venv .venv`) per mantenere le dipendenze isolate.

## Passo 1: Esegui OCR su immagine – crea l’istanza del motore

Il primo passo è creare un oggetto `OcrEngine`. Questo oggetto incapsula la configurazione del motore OCR e fornisce metodi per la gestione e il riconoscimento delle immagini.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine with default settings
ocr_engine = OcrEngine()
```

Creare il motore una sola volta e riutilizzarlo su più immagini riduce il tempo di avvio e garantisce impostazioni coerenti per tutta la sessione.

## Passo 2: Carica l’immagine per OCR

Prima che il riconoscimento possa avvenire, il motore deve sapere quale immagine analizzare. Il metodo `load_image` accetta un percorso file o uno stream binario.

```python
# Provide the full path to your image file
image_path = "YOUR_DIRECTORY/sample.png"
ocr_engine.load_image(image_path)
```

> **Perché è importante:** Caricare correttamente l’immagine è la base per un OCR accurato. Fornire un’immagine ad alta risoluzione (300 dpi o superiore) tipicamente **migliora la precisione OCR** perché il motore può distinguere i caratteri più chiaramente.

## Passo 3: Estrai testo da immagine – esegui il riconoscimento di base

Con l’immagine caricata, puoi chiamare `recognize()` per ottenere un oggetto risultato. Il risultato contiene il testo grezzo, i punteggi di confidenza e, facoltativamente, i riquadri di delimitazione per ogni parola.

```python
# Run the OCR process
plain_result = ocr_engine.recognize()   # returns a Result object

# The raw OCR output is accessible via the .text attribute
print("Raw OCR output:")
print(plain_result.text)
```

A questo punto hai **eseguito OCR su immagine** e hai estratto i caratteri grezzi. Tuttavia, il testo può contenere errori ortografici, soprattutto per scansioni di bassa qualità.

## Passo 4: Correzione del testo OCR – aggiungi un correttore ortografico post‑processo

Aspose AI fornisce una pipeline di post‑processamento flessibile. Collegando un correttore ortografico personalizzato puoi correggere gli errori tipici di OCR (ad es. “l” vs. “1”, “O” vs. “0”).

```python
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker   # your own implementation

# Initialize the AI engine and set the post‑processor
ai_engine = AsposeAI()
ai_engine.set_post_processor(MySpellChecker())

# Run the post‑processor on the plain OCR result
corrected_result = ai_engine.run_postprocessor(plain_result)
```

**Come funziona il correttore ortografico:** `MySpellChecker` deve implementare un metodo `process(text: str) -> str`. All’interno, puoi usare librerie come `pyspellchecker` o `symspellpy` per sostituire sequenze di parole improbabili con alternative validate dal dizionario.

```python
# Example implementation (very simple)
from spellchecker import SpellChecker

class MySpellChecker:
    def __init__(self):
        self.spell = SpellChecker()

    def process(self, text: str) -> str:
        corrected = []
        for word in text.split():
            corrected.append(self.spell.correction(word))
        return " ".join(corrected)
```

## Passo 5: Visualizza il testo OCR originale e quello corretto

Infine, confronta gli output grezzo e corretto. Questo ti aiuta a verificare che la **correzione del testo OCR** abbia effettivamente **migliorato la precisione OCR** per il tuo caso d’uso.

```python
print("\nOriginal :", plain_result.text)
print("Corrected:", corrected_result.text)
```

### Output previsto

```
Original : Th1s is a s4mpl3 rec3pt with som3 err0rs.
Corrected: This is a simple receipt with some errors.
```

La riga corretta mostra che il correttore ortografico ha sostituito le comuni errate interpretazioni OCR (`Th1s` → `This`, `s4mpl3` → `simple`, `rec3pt` → `receipt`, `som3` → `some`, `err0rs` → `errors`).

## Passo 6: Migliora la precisione OCR – checklist delle migliori pratiche

Anche con il post‑processamento, puoi aumentare la qualità di base del motore OCR:

| Voce della checklist | Perché aiuta |
|----------------------|--------------|
| **Usa immagini ad alta risoluzione (≥300 dpi)** | Più dati pixel riducono l’ambiguità dei caratteri. |
| **Converti le immagini a colori in scala di grigi** | Rimuove il rumore cromatico che può confondere il motore. |
| **Applica la correzione di inclinazione dell’immagine** | Raddrizza il testo inclinato, evitando errori di interruzione di riga. |
| **Imposta lingua/locale esplicitamente** | Guida il riconoscitore verso il set di caratteri corretto. |
| **Abilita il modello linguistico** (se la libreria lo supporta) | Fornisce previsioni contestuali, migliorando ulteriormente la **precisione OCR**. |

Puoi implementare questi passaggi di pre‑elaborazione con Pillow o OpenCV prima di passare l’immagine a `ocr_engine`.

```python
from PIL import Image, ImageOps
import cv2
import numpy as np

def preprocess_image(path: str) -> str:
    # Load with Pillow, convert to grayscale, and increase contrast
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)

    # Save a temporary preprocessed file
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

# Use the preprocessor
preprocessed_path = preprocess_image(image_path)
ocr_engine.load_image(preprocessed_path)
```

## Script completo eseguibile

Riunendo tutto, lo script seguente è pronto per essere copiato‑incollato in un file chiamato `run_ocr.py` ed eseguito.

```python
# run_ocr.py
from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker
from PIL import Image, ImageOps

def preprocess_image(path: str) -> str:
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load and preprocess the image
    raw_path = "YOUR_DIRECTORY/sample.png"
    processed_path = preprocess_image(raw_path)
    ocr_engine.load_image(processed_path)

    # 3️⃣ Perform basic OCR
    plain_result = ocr_engine.recognize()

    # 4️⃣ Run OCR text correction
    ai_engine = AsposeAI()
    ai_engine.set_post_processor(MySpellChecker())
    corrected_result = ai_engine.run_postprocessor(plain_result)

    # 5️⃣ Show both results
    print("\nOriginal :", plain_result.text)
    print("Corrected:", corrected_result.text)

if __name__ == "__main__":
    main()
```

L’esecuzione dello script stampa il testo originale e quello corretto, confermando che hai **eseguito OCR su immagine**, **estratto testo da immagine** e **migliorato la precisione OCR** tramite **correzione del testo OCR**.

## Conclusione

Ora sai come **eseguire OCR su immagine** in Python, estrarre il testo grezzo e applicare un correttore ortografico post‑processo per ottenere risultati più puliti. Seguendo la checklist per **migliorare la precisione OCR**, puoi adattare questo flusso di lavoro a ricevute, fatture, carte d’identità o qualsiasi documento scansionato.

### Cosa fare dopo?

* Esplora **dizionari specifici per lingua** per OCR multilingue.  
* Integra la pipeline con un database o un indice di ricerca (ad es. Elasticsearch) per rendere il testo estratto ricercabile.  
* Sostituisci il semplice correttore ortografico con un modello linguistico neurale (ad es. correzione basata su GPT) per una precisione ancora più alta.

Sentiti libero di sperimentare con diverse tecniche di pre‑elaborazione dell’immagine, diversi post‑processori o motori OCR alternativi. Il modello di base—**esegui OCR su immagine → estrai testo da immagine → correzione del testo OCR → migliora la precisione OCR**—rimane lo stesso, fornendoti una solida base per qualsiasi progetto di digitalizzazione di documenti.

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}