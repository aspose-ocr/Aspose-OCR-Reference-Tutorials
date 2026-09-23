---
category: general
date: 2026-01-12
description: Come eseguire OCR e convertire rapidamente un'immagine in testo. Impara
  a riconoscere caratteri speciali, estrarre il testo dall'immagine e caricare l'immagine
  per l'OCR con un esempio completo in Python.
draft: false
keywords:
- how to perform OCR
- convert image to text
- recognize special characters
- extract text from image
- load image for OCR
language: it
og_description: Come eseguire l'OCR in Python, convertire un'immagine in testo e riconoscere
  caratteri speciali. Segui questa guida pratica per estrarre il testo dalle immagini.
og_title: Come eseguire l'OCR in Python – Tutorial completo
tags:
- OCR
- Python
- Image Processing
title: Come eseguire OCR in Python – Guida passo passo
url: /it/python/general/how-to-perform-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR in Python – Guida passo‑passo

Ti è mai capitato di **eseguire OCR** su uno screenshot che contiene sia caratteri latini che cirillici? Non sei il solo. In molti progetti—che si tratti di digitalizzare ricevute, indicizzare documenti multilingue o creare un archivio ricercabile—**come eseguire OCR** diventa rapidamente una domanda cruciale.  

In questo tutorial percorreremo un esempio completo e funzionante che mostra come **convertire immagine in testo**, **riconoscere caratteri speciali** e **estrarre testo da immagine** usando una semplice libreria Python. Alla fine avrai uno script pronto all'uso che carica un'immagine per OCR, gestisce contenuti multilingue e stampa il risultato.

## Cosa ti servirà

Prima di immergerci, assicurati di avere i seguenti prerequisiti:

- Python 3.8+ installato sulla tua macchina.  
- Il pacchetto `ocr` (o qualsiasi libreria OCR compatibile) installato tramite `pip install ocr`.  
- Un file immagine (`multilingual.png`) che contenga sia glifi latini che cirillici.  
- Un editor di testo o IDE di base—VS Code, PyCharm, o anche un semplice Notepad andrà bene.  

Se non hai il pacchetto `ocr`, puoi sostituirlo con `pytesseract` apportando qualche piccola modifica; i concetti di base rimangono gli stessi.

## Passo 1: Installa e importa la libreria OCR

Per prima cosa, prepariamo il motore OCR. Importeremo la libreria, creeremo un'istanza del motore e la configureremo per il supporto multilingue.

```python
# Install the library (run this once in your terminal)
# pip install ocr

import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: Enable language packs for Latin and Cyrillic
engine.set_languages(['eng', 'rus'])  # 'eng' = English, 'rus' = Russian
```

**Perché è importante:**  
Creare il motore è la base—senza di esso non potrai **caricare immagine per OCR** in seguito. Abilitare i pacchetti lingua garantisce che il motore possa identificare correttamente caratteri come “Ŀ”, “Ҕ” e “Ǣ”. Se salti questo passo, otterrai output incomprensibili per script non latini.

## Passo 2: Carica l'immagine contenente testo multilingue

Ora indirizziamo il motore al file che vogliamo elaborare. Il percorso può essere assoluto o relativo; assicurati solo che punti a un'immagine leggibile.

```python
# Step 2: Load the image containing multilingual text
image_path = "YOUR_DIRECTORY/multilingual.png"  # replace with your actual path
engine.load_image(image_path)
```

> ![esempio di come eseguire OCR](/images/ocr-example.png "come eseguire OCR su un'immagine multilingue")

**Perché è importante:**  
La chiamata `load_image` legge i dati dei pixel in memoria, preparando l'immagine per l'algoritmo OCR. Se l'immagine è grande, il motore potrebbe ridimensionarla automaticamente; potrai affinare questo aspetto in seguito con `engine.set_max_resolution(3000)` per scansioni ad alta risoluzione.

## Passo 3: Esegui il processo di riconoscimento

Con il motore pronto e l'immagine caricata, possiamo finalmente estrarre il contenuto testuale.

```python
# Step 3: Perform OCR recognition on the loaded image
result = engine.recognize()
```

**Perché è importante:**  
`recognize()` esegue il lavoro pesante della rete neurale dietro le quinte. Restituisce un oggetto che contiene il testo grezzo, i punteggi di confidenza e persino le bounding box se ti servono per il debug visivo.

## Passo 4: Stampa il testo riconosciuto

Vediamo cosa ha trovato il motore. Stamperemo il testo sulla console, ma potresti anche scriverlo su un file o su un database.

```python
# Step 4: Output the recognized text, which should include characters like “Ŀ”, “Ҕ”, “Ǣ”
print("=== OCR Result ===")
print(result.text)
```

### Output previsto

```
=== OCR Result ===
Hello, world! Ŀ is a Latin‑extended character.
Привет, мир! Ҕ is a Cyrillic character.
Special combo: Ǣ is a ligature.
```

Se vedi qualcosa di simile, congratulazioni—hai **convertito immagine in testo** e **riconosciuto caratteri speciali** con successo.

## Gestione dei problemi più comuni

Anche con uno script semplice, potresti incontrare qualche intoppo. Di seguito alcuni consigli pratici basati sulla mia esperienza.

### 1. Pacchetti lingua mancanti

Se ottieni punti interrogativi (`?`) al posto delle lettere cirilliche, verifica che i pacchetti lingua siano installati. Per molti motori OCR devi scaricare i file `.traineddata` corrispondenti e collocarli nella cartella `tessdata` del motore.

```python
# Example for pytesseract
import pytesseract
pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
# Ensure 'eng' and 'rus' data files exist in tessdata
```

### 2. Bassa qualità dell'immagine

Immagini sfocate o a basso contrasto producono punteggi di confidenza bassi. Pre‑elabora l'immagine con OpenCV:

```python
import cv2

# Load, convert to grayscale, and apply thresholding
raw = cv2.imread(image_path)
gray = cv2.cvtColor(raw, cv2.COLOR_BGR2GRAY)
_, thresh = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)

# Save a temporary cleaned image and feed it to the OCR engine
cv2.imwrite("cleaned.png", thresh)
engine.load_image("cleaned.png")
```

### 3. File di grandi dimensioni e uso della memoria

Elaborare una foto da 10 MB può aumentare il consumo di memoria. Usa `engine.set_max_image_size(2000)` per limitare la risoluzione, oppure suddividi l'immagine in tasselli e OCR ogni tassello separatamente.

### 4. Cattura delle bounding box

Se devi evidenziare dove appare ogni parola (utile per overlay UI), accedi a `result.boxes`:

```python
for box in result.boxes:
    print(f"Word: {box.text} – Coordinates: {box.x0},{box.y0},{box.x1},{box.y1}")
```

## Script completo – Esecuzione con un click

Riunendo tutto, ecco un unico file che puoi eseguire con `python ocr_demo.py`. Include gestione degli errori, pre‑elaborazione opzionale e commenti per chiarezza.

```python
#!/usr/bin/env python3
"""
Complete OCR demo: load image, recognize multilingual text,
and print results. Works with the generic 'ocr' library.
"""

import os
import sys
import ocr

def main(image_path: str):
    # Verify the image exists
    if not os.path.isfile(image_path):
        sys.exit(f"Error: File not found – {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()
    engine.set_languages(['eng', 'rus'])          # load language packs
    engine.set_max_image_size(2500)               # limit memory usage

    # Load the image
    try:
        engine.load_image(image_path)
    except Exception as e:
        sys.exit(f"Failed to load image: {e}")

    # Perform recognition
    try:
        result = engine.recognize()
    except Exception as e:
        sys.exit(f"OCR failed: {e}")

    # Output the text
    print("\n=== OCR Result ===")
    print(result.text)

    # Optional: display confidence scores
    if hasattr(result, "confidence"):
        avg_conf = sum(result.confidence) / len(result.confidence)
        print(f"\nAverage confidence: {avg_conf:.1%}")

if __name__ == "__main__":
    # Replace with your actual image path or pass as CLI argument
    img = sys.argv[1] if len(sys.argv) > 1 else "YOUR_DIRECTORY/multilingual.png"
    main(img)
```

Eseguilo con:

```bash
python ocr_demo.py path/to/multilingual.png
```

Dovresti vedere lo stesso output mostrato in precedenza, confermando che hai **estratto testo da immagine** con successo.

## Conclusione

Abbiamo coperto **come eseguire OCR** in Python dall'inizio alla fine: installazione della libreria, caricamento di un'immagine, riconoscimento di contenuti multilingue e gestione dei casi limite più comuni. Seguendo questa guida ora puoi **convertire immagine in testo**, **riconoscere caratteri speciali** e **estrarre testo da immagine** nei tuoi progetti—niente più trascrizioni manuali.

Qual è il prossimo passo? Prova a sperimentare con:

- Aggiungere altri pacchetti lingua (ad esempio `spa` per lo spagnolo).  
- Esportare i risultati in JSON per elaborazioni successive.  
- Integrare il passo OCR in un'API Flask così che altri servizi possano chiamarlo.  

Se incontri qualche strano comportamento, la community intorno alla maggior parte delle librerie OCR è attiva—cerca “ocr library language pack installation” o lascia un commento qui sotto. Buon coding e divertiti a trasformare le immagini in testo ricercabile!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}