---
category: general
date: 2026-03-26
description: 'Tutorial OCR Python: impara come estrarre il testo da un''immagine,
  caricare l''immagine per l''OCR e riconoscere il testo da una ricevuta usando Aspose
  OCR in pochi passaggi.'
draft: false
keywords:
- python ocr tutorial
- extract text from image
- load image for ocr
- perform ocr in python
- recognize text from receipt
language: it
og_description: 'Tutorial OCR in Python: impara rapidamente a estrarre testo da un''immagine,
  caricare l''immagine per l''OCR e riconoscere il testo da una ricevuta con Aspise
  OCR.'
og_title: Tutorial OCR in Python – Estrai il testo dall'immagine
tags:
- OCR
- Aspose
- Python
title: Tutorial OCR in Python – Estrai il testo dall'immagine con Aspose
url: /it/python-java/general/python-ocr-tutorial-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutorial Python OCR – Estrarre Testo da Immagine con Aspose

Ti sei mai chiesto come estrarre il testo da una ricevuta sfocata o da un modulo scansionato senza passare ore a scrivere regex personalizzate? Non sei solo. In questo **python ocr tutorial** vedremo come caricare un'immagine per OCR, eseguire OCR in Python e, infine, riconoscere il testo da file di ricevute usando la libreria Aspose OCR.  

Al termine di questa guida avrai uno script pronto all'uso che legge qualsiasi formato immagine supportato, estrae il contenuto testuale e lo stampa sulla console. Nessun servizio esterno, nessuna chiave API—solo puro Python e un potente motore OCR.  

## Cosa Ti Serve

- Python 3.8 o versioni successive (il codice usa type hints, quindi è consigliato un interprete recente)
- Pacchetto `asposeocrjava` installato con `pip install aspose-ocr`
- Un'immagine di esempio – ad esempio `receipt_noisy.jpg` che contiene una tipica ricevuta di negozio
- (Opzionale) Un ambiente virtuale per tenere ordinate le dipendenze

Se hai spuntato tutti questi punti, possiamo passare subito al codice.  

## Passo 1: Installa e Importa le Classi Aspose OCR

Per prima cosa, assicurati che il pacchetto Aspose OCR sia disponibile. Poi importa le classi di cui avremo bisogno.

```python
# Install the package (run once)
# pip install aspose-ocr

# Import the required Aspose OCR modules
import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult
```

**Perché è importante:** Importare solo i simboli necessari mantiene pulito lo spazio dei nomi e indica all'interprete quali parti della libreria utilizzi realmente. Inoltre accorcia le righe di codice successive, rendendo il tutorial più facile da seguire.

> **Consiglio professionale:** Se usi un notebook Jupyter, anteponi il comando di installazione con `!` per eseguirlo all'interno della cella.

## Passo 2: Crea il Motore OCR e Abilita la Modalità Deep‑Learning

Aspose offre diverse modalità di motore. Per la maggior parte delle ricevute reali, il modello deep‑learning fornisce la massima precisione, soprattutto su scansioni rumorose.

```python
# Initialise the OCR engine
ocr_engine = OcrEngine()

# Switch to deep‑learning mode for better accuracy on complex images
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
```

**Perché deep‑learning?** L'OCR tradizionale basato su regole può inciampare su caratteri a basso contrasto o distorti. Il modello deep‑learning, addestrato su milioni di glifi, si adatta meglio alle variazioni—esattamente ciò di cui hai bisogno quando *perform OCR in Python* su ricevute scattate con la fotocamera del telefono.

## Passo 3: Carica l'Immagine per OCR

Ora **carichiamo l'immagine per OCR**. Aspose.Imaging supporta PNG, JPEG, BMP, TIFF e molto altro, così puoi puntare praticamente a qualsiasi foto di un documento.

```python
# Load the image (replace the path with your own file)
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/receipt_noisy.jpg")

# Attach the image to the OCR engine
ocr_engine.set_image(input_image)
```

**Errore comune:** Dimenticare di impostare l'immagine sul motore provoca una `NullReferenceException` a runtime. Chiama sempre `set_image` dopo aver caricato il file.

## Passo 4: Esegui OCR ed Estrai il Testo

Con il motore pronto e l'immagine allegata, possiamo finalmente **perform OCR in Python** e recuperare il risultato testuale.

```python
# Run the recognition process
ocr_result: OcrResult = ocr_engine.recognize()

# Extract plain text from the result object
recognized_text = ocr_result.get_text()
```

Il metodo `recognize()` restituisce un oggetto `OcrResult` che contiene non solo il testo grezzo ma anche punteggi di confidenza, bounding box e informazioni sulla lingua. Per un caso d'uso rapido di **extract text from image** ci serve solo `get_text()`.

## Passo 5: Visualizza il Testo Riconosciuto

Vediamo cosa ha effettivamente letto il motore dalla ricevuta.

```python
print("Recognized text:\n", recognized_text)
```

Un output tipico appare così:

```
Recognized text:
   Store XYZ
   04/26/2026  14:32
   Item A   2.99
   Item B   5.49
   TOTAL    8.48
   THANK YOU!
```

Se l'output contiene caratteri illeggibili, considera di pre‑elaborare l'immagine (ad esempio aumentando il contrasto o applicando un filtro di deskew) prima di caricarla nel motore OCR. Aspose.Imaging offre una suite completa di strumenti di miglioramento immagine che puoi concatenare.

## Gestione dei Casi Limite & Consigli per Maggiore Precisione

### 1. Gestire Ricevute Estremamente Rumorose
Se la ricevuta è molto macchiata, potresti voler passare alla modalità `OcrEngineMode.HIGH_SPEED` per una prima scansione più veloce, sebbene meno accurata, per poi eseguire una seconda passata in `DEEP_LEARNING` sull'immagine pulita.

```python
ocr_engine.set_engine_mode(OcrEngineMode.HIGH_SPEED)
# ... run first pass, then...
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
# ... run second pass on the same image
```

### 2. Specificare la Lingua
Di default Aspose tenta di auto‑rilevare la lingua. Per le ricevute in inglese puoi fissarla così:

```python
ocr_engine.set_language("eng")
```

### 3. Gestione della Memoria
Quando elabori molte immagini in un ciclo, rilascia esplicitamente le risorse:

```python
input_image.dispose()
ocr_engine.dispose()
```

### 4. Salvare i Risultati OCR su File
A volte è necessario persistere il testo estratto per analisi successive.

```python
with open("receipt_output.txt", "w", encoding="utf-8") as f:
    f.write(recognized_text)
```

## Esempio Completo Funzionante

Di seguito lo script completo che mette insieme tutti i passaggi. Copialo in un file chiamato `receipt_ocr.py`, aggiusta il percorso dell'immagine e avvia `python receipt_ocr.py`.

```python
# receipt_ocr.py
# -------------------------------------------------
# Complete Python OCR tutorial using Aspose OCR
# -------------------------------------------------

# 1️⃣ Install the package (run once):
# pip install aspose-ocr

import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult

def main():
    # 2️⃣ Initialise engine in deep‑learning mode
    engine = OcrEngine()
    engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)

    # 3️⃣ Load your receipt image
    image_path = "YOUR_DIRECTORY/receipt_noisy.jpg"   # <-- change this
    img = ocr.Imaging.Image.load(image_path)
    engine.set_image(img)

    # 4️⃣ Recognise text
    result: OcrResult = engine.recognize()
    text = result.get_text()

    # 5️⃣ Output the result
    print("=== Recognized text from receipt ===")
    print(text)

    # Optional: write to a file
    with open("receipt_output.txt", "w", encoding="utf-8") as out_file:
        out_file.write(text)

    # Clean up resources
    img.dispose()
    engine.dispose()

if __name__ == "__main__":
    main()
```

L'esecuzione dello script dovrebbe mostrare il contenuto della ricevuta nella console e creare anche `receipt_output.txt` con gli stessi dati.

![Python OCR tutorial – sample receipt output](https://example.com/receipt_output.png "esempio di tutorial python ocr")

*Testo alternativo dell'immagine:* **python ocr tutorial – esempio di ricevuta**

## Riepilogo & Prossimi Passi

Abbiamo appena completato un **python ocr tutorial** che mostra come **load image for OCR**, **perform OCR in Python** e infine **recognize text from receipt** usando Aspose. I punti chiave sono:

- Scegli la modalità di motore adeguata (deep‑learning per la massima precisione)
- Allegare sempre l'immagine prima di chiamare `recognize()`
- Utilizzare l'oggetto `OcrResult` per estrarre il testo pulito, quindi salvarlo o elaborarlo secondo necessità

Qual è il prossimo passo? Prova a concatenare i filtri di Aspose Imaging per migliorare scansioni a basso contrasto, oppure integra lo script in una API Flask così da poter caricare le ricevute tramite un form web. Potresti anche esplorare l'esportazione dei dati OCR in CSV per l'automazione contabile.

Hai domande su come gestire PDF multi‑pagina o script non latini? Lascia un commento—siamo felici di aiutare!  

**Pronto a potenziare la tua automazione documentale?** Prendi il codice, sperimenta con immagini diverse e lascia che il motore OCR faccia il lavoro pesante. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}