---
category: general
date: 2026-06-16
description: Riconoscere il testo da un'immagine usando Python OCR. Scopri come caricare
  l'immagine per l'OCR, impostare la modalità ad alta precisione e avviare il riconoscimento
  OCR per convertire l'immagine in testo.
draft: false
keywords:
- recognize text from image
- convert image to text
- load image for ocr
- run ocr recognition
- set high accuracy mode
language: it
og_description: Riconoscere il testo da un'immagine in Python. Questa guida mostra
  come caricare l'immagine per l'OCR, impostare la modalità ad alta precisione e avviare
  il riconoscimento OCR per convertire l'immagine in testo.
og_title: Riconosci il testo da un'immagine – Tutorial completo di OCR in Python
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text from image using Python OCR. Learn how to load image
    for OCR, set high accuracy mode, and run OCR recognition to convert image to text.
  headline: recognize text from image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: recognize text from image using Python OCR. Learn how to load image
    for OCR, set high accuracy mode, and run OCR recognition to convert image to text.
  name: recognize text from image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: 1. Empty Result
    text: 'Sometimes the engine returns an empty string. This usually means the image
      is too blurry or the text color blends with the background. Try:'
  - name: 2. Non‑Latin Scripts
    text: 'If your picture contains Cyrillic, Chinese, or Arabic characters, you’ll
      need to tell the OCR engine which language pack to use:'
  - name: 3. Large Batches
    text: Processing a folder of images? Wrap the core logic in a loop and reuse the
      same engine instance to avoid repeated initialization overhead.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Riconoscere il testo da un'immagine con Python – Guida completa passo passo
url: /it/python-java/general/recognize-text-from-image-with-python-complete-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# riconoscere testo da immagine – Guida completa OCR in Python

Ti sei mai chiesto come **recognize text from image** senza pagare per un servizio cloud? Non sei l'unico. Che tu stia digitalizzando vecchie ricevute o estraendo didascalie da screenshot, trasformare un'immagine in testo modificabile è una capacità utile da avere.

In questo tutorial passeremo in rassegna un **complete, runnable example** che ti mostra come **load image for OCR**, **set high accuracy mode**, e **run OCR recognition** così potrai **convert image to text** in poche righe di Python. Niente fronzoli, solo le parti pratiche che puoi copiare‑incollare subito.

## Cosa costruirai

Alla fine di questa guida avrai un piccolo script che:

1. Istanzia un motore OCR.
2. Abilita il flag **set high accuracy mode** per risultati migliori su immagini a bassa risoluzione.
3. **Loads an image for OCR** dal disco.
4. **Runs OCR recognition** per **recognize text from image**.
5. Stampa la stringa estratta – convertendo effettivamente **convert image to text**.

Se hai Python 3.8+ e un po' di curiosità, sei pronto per cominciare.

## Prerequisiti

- **Python 3.8 or newer** – il codice utilizza type hints che le versioni più vecchie non comprendono.
- Una libreria OCR che espone un modulo `ocr` (l'esempio imita un wrapper generico; sostituiscilo con `pytesseract`, `easyocr` o qualsiasi SDK specifico del fornitore che preferisci).
- Un JPEG a bassa risoluzione chiamato `low-res.jpg` in una cartella che controlli.
- (Opzionale) Un ambiente virtuale per mantenere ordinate le dipendenze: `python -m venv venv && source venv/bin/activate`.

```bash
# Example installation for a hypothetical `ocr` package
pip install ocr-lib
```

> **Pro tip:** Se stai usando `pytesseract`, installa il motore Tesseract separatamente (`sudo apt-get install tesseract-ocr` su Linux, Homebrew su macOS).

---

## Passo 1: Recognize Text from Image – Inizializza il motore OCR

Prima di tutto. Abbiamo bisogno di un nuovo oggetto motore OCR che gestirà il lavoro pesante.

```python
# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Perché è importante:* La classe `OcrEngine` è il punto di ingresso per tutte le operazioni successive. Pensala come il cervello che interpreterà i pixel che le fornisci. Creare una nuova istanza ad ogni esecuzione garantisce uno stato pulito, specialmente quando attivi impostazioni come **set high accuracy mode** più tardi.

---

## Passo 2: Set High Accuracy Mode – Migliora i risultati a bassa risoluzione

Le immagini a bassa risoluzione sono famose per confondere i motori OCR. Abilitare il flag high‑accuracy indica al motore di applicare un pre‑processing aggiuntivo (up‑scaling, riduzione del rumore, ecc.) prima di leggere effettivamente i caratteri.

```python
# Step 2: Enable high‑accuracy mode for better results
engine.high_accuracy = True   # <-- activates advanced preprocessing
```

> **Perché abilitarlo?** Quando l'immagine di origine è granulosa o piccola, la modalità predefinita può perdere lettere o unire parole. Il percorso high‑accuracy scambia un po' di velocità per un notevole aumento di correttezza—perfetto per script una tantum dove la latenza non è critica.

---

## Passo 3: Load Image for OCR – Preparazione del file

Ora carichiamo effettivamente **load image for OCR**. L'helper `ocr.Image.load_from_file` astrae i passaggi di I/O del file e di decodifica dell'immagine.

```python
# Step 3: Load the low‑resolution image to be processed
engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/low-res.jpg")
```

*Cosa succede dietro le quinte?* La libreria legge il JPEG, lo converte in una bitmap e lo memorizza all'interno dell'istanza del motore. Se devi lavorare con un'immagine già in memoria (ad esempio da una richiesta web), la maggior parte delle librerie espone anche un metodo `from_bytes`—basta sostituire la chiamata.

---

## Passo 4: Run OCR Recognition – L'azione principale

Con il motore pronto e l'immagine al suo posto, finalmente **run OCR recognition**. Questo passaggio esegue l'effettiva estrazione del testo.

```python
# Step 4: Perform OCR recognition on the image
high_res_result = engine.recognize()
```

Il metodo `recognize()` restituisce un oggetto risultato contenente la stringa grezza, i punteggi di confidenza e talvolta i metadati dei bounding‑box. Per lo scopo di **convert image to text**, ci concentreremo sull'attributo `text`.

---

## Passo 5: Output the Recognized Text – Convert Image to Text

Il culmine del processo: stampare la stringa estratta. È qui che l'immagine diventa finalmente testo modificabile.

```python
# Step 5: Output the recognized text
print(high_res_result.text)
```

**Output previsto** (il tuo testo reale varierà in base all'immagine):

```
Invoice #12345
Date: 2024‑03‑15
Total: $256.78
Thank you for your business!
```

Se vedi caratteri illeggibili, ricontrolla che **set high accuracy mode** sia effettivamente `True` e che l'immagine non sia eccessivamente compressa.

---

## Gestione dei casi limite comuni

### 1. Risultato vuoto

A volte il motore restituisce una stringa vuota. Questo di solito significa che l'immagine è troppo sfocata o che il colore del testo si confonde con lo sfondo. Prova a:

- Aumentare la risoluzione dell'immagine prima del caricamento (`PIL.Image.resize`).
- Regolare il contrasto (`ImageEnhance.Contrast`).

### 2. Script non latini

Se la tua immagine contiene caratteri cirillici, cinesi o arabi, dovrai indicare al motore OCR quale pacchetto linguistico utilizzare:

```python
engine.language = "eng+rus"   # Example for English + Russian
```

### 3. Lotti grandi

Stai elaborando una cartella di immagini? Avvolgi la logica principale in un ciclo e riutilizza la stessa istanza del motore per evitare il sovraccarico di inizializzazioni ripetute.

```python
import pathlib

engine = ocr.OcrEngine()
engine.high_accuracy = True
engine.language = "eng"

for img_path in pathlib.Path("batch/").glob("*.jpg"):
    engine.image = ocr.Image.load_from_file(str(img_path))
    result = engine.recognize()
    print(f"{img_path.name}: {result.text[:50]}...")
```

---

## Esempio completo funzionante

Mettendo tutto insieme, ecco uno script che puoi inserire in un file chiamato `ocr_demo.py` ed eseguire subito.

```python
#!/usr/bin/env python3
"""
ocr_demo.py – Recognize text from image using a generic OCR library.
"""

import ocr  # Replace with the actual OCR package you installed

def main():
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.high_accuracy = True          # set high accuracy mode
    engine.language = "eng"              # optional: specify language pack

    # Load image – change the path to your own file
    image_path = "YOUR_DIRECTORY/low-res.jpg"
    engine.image = ocr.Image.load_from_file(image_path)

    # Perform recognition
    result = engine.recognize()

    # Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

Salva, rendilo eseguibile (`chmod +x ocr_demo.py`), e avvialo:

```bash
./ocr_demo.py
```

Dovresti vedere l'output **convert image to text** stampato sulla console.

---

## Consigli e trucchi dal campo

- **Cache the engine** se stai elaborando molte immagini; creare una nuova istanza per ogni file può raddoppiare il tempo di esecuzione.
- **Pre‑process yourself** quando la modalità high‑accuracy integrata non è sufficiente: usa OpenCV per denoise (`cv2.fastNlMeansDenoisingColored`) o binarizzare (`cv2.threshold`).
- **Log confidence** (`result.confidence`) se devi filtrare automaticamente i risultati di bassa qualità.
- **Avoid hard‑coding paths**; usa `pathlib.Path` per la compatibilità cross‑platform.

---

## Conclusione

Abbiamo appena **recognize text from image** usando un flusso di lavoro Python semplice: **load image for OCR**, **set high accuracy mode**, **run OCR recognition**, e infine **convert image to text**. L'intera pipeline sta in meno di venti righe, ma è sufficientemente flessibile per gestire lavori batch, documenti multilingue e input rumorosi.

Pronto per la prossima sfida? Prova a sostituire la libreria generica `ocr` con `pytesseract` o `easyocr`, sperimenta passaggi di preprocessing aggiuntivi, o integra lo script in un'API Flask così da poter caricare immagini da una pagina web e ricevere trascrizioni in tempo reale.

Hai domande o un caso d'uso interessante? Lascia un commento qui sotto, e buona programmazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}