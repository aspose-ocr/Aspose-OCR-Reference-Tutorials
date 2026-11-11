---
category: general
date: 2026-06-25
description: Tutorial Python OCR che mostra come estrarre testo da file PNG, leggere
  immagini di testo e riconoscere il testo nelle immagini utilizzando un motore semplice
  e senza licenza.
draft: false
keywords:
- python ocr tutorial
- extract text png
- read text image
- recognize image text
- load image for ocr
language: it
og_description: Il tutorial OCR in Python ti insegna a caricare un'immagine per l'OCR,
  estrarre il testo da file PNG e riconoscere il testo dell'immagine in poche righe
  di codice.
og_title: Tutorial OCR Python – Estrai il testo da PNG
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  headline: 'Python OCR Tutorial: Extract Text from PNG Images'
  type: TechArticle
- description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  name: 'Python OCR Tutorial: Extract Text from PNG Images'
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer (the library works with 3.7+ but 3.8+ is recommended).
      - Basic familiarity with pip and virtual environments. - An image file named
      `sample.png` (or any PNG you’d like to test) saved in a folder you can reference.'
  - name: 1. Low Contrast or Dark Backgrounds
    text: '```python # Increase contrast before recognition (optional step) image
      = image.adjust_contrast(1.5) # 1.0 = no change, >1 = higher contrast result
      = engine.recognize(image) ```'
  - name: 2. Skewed Text Lines
    text: '```python # Auto‑deskew the image image = image.deskew() result = engine.recognize(image)
      ```'
  - name: 3. Non‑English Characters
    text: 'If your PNG contains accented letters or non‑Latin scripts, initialise
      the engine with the appropriate language pack:'
  - name: 4. Very Large Images
    text: 'Processing a 4000×3000 PNG can be slow. Downscale it while preserving readability:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Tutorial
title: 'Tutorial OCR Python: estrai il testo dalle immagini PNG'
url: /it/python-java/general/python-ocr-tutorial-extract-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutorial OCR Python – Estrarre Testo da Immagini PNG

Ti sei mai chiesto come **python ocr tutorial** possa trasformare uno screenshot di una ricevuta in testo modificabile? Non sei l'unico. In molti progetti reali dobbiamo *read text image* file rapidamente, e farlo da soli è meglio che copiare‑incollare da un'interfaccia grafica ogni volta.  

In questa guida percorreremo un esempio pratico che **extracts text PNG** file, ti mostrerà come *load image for OCR* e infine stampa il risultato di *recognize image text* — il tutto con un motore OCR gratuito, solo per valutazione. Nessuna chiave di licenza, nessuna dipendenza pesante — solo Python puro e un paio di piccoli pacchetti.

## Cosa Imparerai

- Come installare e importare la libreria OCR leggera.
- I passaggi esatti per **load image for OCR** e gestire le insidie comuni.
- Modi per **read text image** file di qualità variabile.
- Suggerimenti per migliorare l'accuratezza quando **extract text png** file.
- Come visualizzare la stringa riconosciuta e opzionalmente scriverla su disco.

### Prerequisiti

- Python 3.8 o superiore (la libreria funziona con 3.7+ ma si consiglia 3.8+).
- Familiarità di base con pip e ambienti virtuali.
- Un file immagine chiamato `sample.png` (o qualsiasi PNG tu voglia testare) salvato in una cartella a cui puoi fare riferimento.

Se qualcuno di questi ti è sconosciuto, fermati un minuto e configurali — credimi, il risultato ne vale la pena.

---

## Tutorial OCR Python – Configurare il Motore

Prima di tutto: ci serve un oggetto motore OCR. La libreria che useremo è un piccolo wrapper attorno a un motore OCR nativo che funziona subito per la valutazione. Non richiede una chiave di licenza, il che rende il *python ocr tutorial* perfetto per prototipi rapidi.

```python
# Step 1: Install the OCR package (run once in your terminal)
# pip install simple-ocr-lib

# Step 2: Import the library and create an engine instance
import ocr

# No license needed for evaluation mode – the engine is ready to go
engine = ocr.OcrEngine()
```

**Perché è importante:** Creare il motore isola il runtime OCR dal resto del tuo codice, permettendoti di riutilizzarlo per più immagini senza reinizializzare risorse pesanti ogni volta.

---

## Caricare Immagine per OCR – Leggere un File PNG

Ora che il motore esiste, dobbiamo *load image for OCR*. Il metodo `Image.load` della libreria accetta un percorso e decodifica automaticamente PNG, JPEG, BMP e alcuni altri formati.

```python
# Step 3: Load the PNG you want to process
image_path = "YOUR_DIRECTORY/sample.png"   # replace with your actual path
image = ocr.Image.load(image_path)
```

> **Consiglio professionale:** Se il tuo PNG contiene un canale alfa, la libreria lo eliminerà automaticamente. Tuttavia, per i migliori risultati nelle attività di *read text image*, mantieni l'immagine in scala di grigi — questo riduce il rumore e velocizza il riconoscimento.

---

## Riconoscere Testo Immagine – Eseguire il Motore OCR

Con l'oggetto immagine pronto, possiamo finalmente **recognize image text**. Questo è il fulcro del *python ocr tutorial* e richiede solo una singola riga di codice.

```python
# Step 4: Perform OCR on the loaded image
result = engine.recognize(image)
```

**Cosa succede dietro le quinte?** Il motore esegue una serie di filtri di pre‑elaborazione (deskew, binarizzazione) prima di inviare il bitmap a una rete neurale addestrata su milioni di caratteri. Ecco perché ottieni spesso risultati sorprendentemente accurati anche su PNG a bassa risoluzione.

---

## Visualizzare e Salvare il Testo Estratto

Avere il risultato è ottimo, ma probabilmente vuoi vederlo o salvarlo da qualche parte. L'oggetto `result` espone un attributo `text` che contiene l'output in forma di stringa semplice.

```python
# Step 5: Print the recognized text to the console
print("Eval-mode result:", result.text)

# Optional: Save the text to a .txt file for later use
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**Output previsto** (supponendo che `sample.png` contenga “Hello, OCR!”):

```
Eval-mode result: Hello, OCR!
```

Se ottieni spazzatura invece di caratteri leggibili, controlla la sezione successiva per le correzioni comuni.

---

## Gestire Problemi Comuni Quando Estrarre Testo PNG

Anche i migliori motori OCR inciampano su certe immagini. Di seguito i tipici ostacoli e come superarli.

### 1. Basso Contrasto o Sfondo Scuro

```python
# Increase contrast before recognition (optional step)
image = image.adjust_contrast(1.5)   # 1.0 = no change, >1 = higher contrast
result = engine.recognize(image)
```

### 2. Linee di Testo Inclinate

```python
# Auto‑deskew the image
image = image.deskew()
result = engine.recognize(image)
```

### 3. Caratteri Non‑Inglesi

Se il tuo PNG contiene lettere accentate o script non latini, inizializza il motore con il pacchetto lingua appropriato:

```python
engine = ocr.OcrEngine(languages=["eng", "spa"])   # English + Spanish
```

### 4. Immagini Molto Grandi

Elaborare un PNG 4000×3000 può essere lento. Ridimensiona mantenendo la leggibilità:

```python
image = image.resize(width=1024)   # keep aspect ratio
result = engine.recognize(image)
```

Queste modifiche fanno parte di un robusto *python ocr tutorial* che funziona oltre lo scenario ideale.

---

## Script Completo – Soluzione in Un Solo File

Di seguito lo script completo, pronto per l'esecuzione, che incorpora tutti i passaggi e i miglioramenti opzionali discussi. Copialo in `ocr_extract.py` ed esegui `python ocr_extract.py`.

```python
# ocr_extract.py
# Complete Python OCR tutorial – extract text from PNG images

import ocr
import sys
import os

def main(image_path):
    # Verify the file exists
    if not os.path.isfile(image_path):
        print(f"Error: File not found → {image_path}")
        sys.exit(1)

    # 1️⃣ Create the OCR engine (evaluation mode, no license needed)
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image – this is the "load image for OCR" step
    image = ocr.Image.load(image_path)

    # Optional preprocessing for better accuracy
    # Uncomment any of the following lines as needed:
    # image = image.adjust_contrast(1.5)   # boost contrast
    # image = image.deskew()               # correct skew
    # image = image.resize(width=1024)     # downscale large images

    # 3️⃣ Recognize the text
    result = engine.recognize(image)

    # 4️⃣ Output the result
    print("Eval-mode result:", result.text)

    # 5️⃣ Save to a .txt file (useful for batch processing)
    txt_path = os.path.splitext(image_path)[0] + "_extracted.txt"
    with open(txt_path, "w", encoding="utf-8") as out_file:
        out_file.write(result.text)
    print(f"Extracted text saved to {txt_path}")

if __name__ == "__main__":
    # Pass the image path as a command‑line argument, e.g.:
    # python ocr_extract.py ./samples/sample.png
    if len(sys.argv) < 2:
        print("Usage: python ocr_extract.py <path_to_png>")
        sys.exit(1)
    main(sys.argv[1])
```

**Eseguilo:**  
```bash
python ocr_extract.py ./sample.png
```

Dovresti vedere la stringa riconosciuta stampata e un file `sample_extracted.txt` creato accanto all'immagine.

---

## Panoramica Visiva

![Tutorial OCR Python – caricare immagine per OCR ed estrarre testo da PNG](/images/python-ocr-flow.png)

*Testo alternativo:* *Diagramma del tutorial OCR Python che mostra il flusso dal caricamento di un'immagine per OCR all'estrazione del testo PNG.*

Il diagramma illustra la progressione lineare da **load image for OCR** → **recognize image text** → **extract text PNG** e evidenzia dove è possibile inserire passaggi di pre‑elaborazione.

---

## Conclusione

Abbiamo appena completato un **python ocr tutorial** che dimostra come *load image for OCR*, *recognize image text* e infine **extract text png** file con solo pochi comandi Python. Lo script è completamente funzionale, gestisce i casi limite comuni e può essere esteso per l'elaborazione batch o il supporto multilingue.

Pronto per la prossima sfida? Prova a fornire al motore PDF convertiti in immagini, sperimenta con diversi pacchetti lingua, o integra il passaggio OCR in un'API Flask così la tua web app può leggere gli screenshot caricati al volo. Le possibilità per l'automazione *read text image* sono praticamente infinite.

Hai domande o un'immagine difficile da decifrare? Lascia un commento qui sotto e risolviamo insieme. Buon coding!

## Cosa Dovresti Imparare Dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrai Testo da Immagine con Aspose OCR – Guida Passo‑Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Estrai Testo da Immagine – Ottimizzazione OCR con Aspose.OCR per .NET](/ocr/english/net/ocr-optimization/)
- [Come Eseguire OCR su Testo Immagine con Lingua Usando Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}