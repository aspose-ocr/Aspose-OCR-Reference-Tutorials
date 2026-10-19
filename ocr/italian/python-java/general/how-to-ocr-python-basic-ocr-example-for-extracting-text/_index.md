---
category: general
date: 2026-04-26
description: 'come fare OCR in Python: Impara a estrarre testo da un''immagine e a
  leggere file TIFF in Python usando un esempio base di OCR. Codice rapido e eseguibile
  incluso.'
draft: false
keywords:
- how to ocr python
- extract text from image
- read tiff file python
- basic ocr example
- convert scanned image text
language: it
og_description: 'come fare OCR in Python: una guida passo‑passo che mostra come estrarre
  testo da un’immagine, leggere file TIFF con Python e convertire il testo di un’immagine
  scannerizzata con uno script semplice e eseguibile.'
og_title: come fare OCR in Python – Esempio base di OCR per estrarre testo
tags:
- OCR
- Python
- Image Processing
title: come fare OCR in Python – Esempio base di OCR per estrarre testo
url: /it/python-java/general/how-to-ocr-python-basic-ocr-example-for-extracting-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# come fare OCR con Python – Esempio base di OCR per estrarre testo

Ti sei mai chiesto **come fare OCR con Python** quando hai un file TIFF scansionato sulla scrivania? Non sei l'unico a fissare una serie di file immagine e chiedersi: “Come estrarre le parole da questo?” La buona notizia è che trasformare un'immagine in testo semplice è un gioco da ragazzi con la libreria giusta e pochi passaggi chiari.

In questo tutorial vedremo un **esempio base di OCR** che legge un file TIFF, estrae il testo e lo stampa sulla console. Alla fine saprai esattamente come **estrarre testo da immagini**, come gestire le particolarità dei formati TIFF e cosa modificare se devi **convertire testo da immagini scansionate** in qualcosa di più utile. Nessuna magia nascosta—solo Python lineare che puoi copiare‑incollare ed eseguire subito.

## Cosa ti servirà

Prima di iniziare, assicurati di avere:

- Python 3.9+ installato (la versione stabile più recente è consigliata).
- Una libreria OCR installabile con pip. Per questa guida useremo un pacchetto fittizio `aocr` che imita strumenti popolari come Tesseract; potrai sostituirlo con `pytesseract` o `easyocr` in seguito.
- Un’immagine TIFF da elaborare – chiamala `input.tiff` e posizionala in una cartella a cui farai riferimento nel codice.
- Familiarità di base con la riga di comando (solo per installare il pacchetto).

Tutto qui. Nessuna dipendenza pesante, nessun container Docker, solo poche righe di codice.

## Passo 1 – Installa e importa le dipendenze (come fare OCR con Python)

Per prima cosa, ottieni il pacchetto OCR. Apri un terminale e esegui:

```bash
pip install aocr
```

Se preferisci una libreria reale, sostituisci `aocr` con `pytesseract` e installa separatamente il motore Tesseract.

Ora importa ciò che serve. La classe `Path` di `pathlib` ci offre un modo pulito per gestire i percorsi dei file su tutti i sistemi operativi.

```python
# Step 1: Import the Path class for handling file paths
from pathlib import Path

# Import the OCR engine and image loader from the chosen library
from aocr import OcrEngine, Image
```

*Perché usare `Path`?* Perché astrae le barre (`/` vs `\`) e ti permette di unire directory senza preoccuparti del sistema operativo sottostante. Questo piccolo dettaglio spesso evita grattacapi quando sposti lo script su un server CI.

## Passo 2 – Crea l'istanza del motore OCR (esempio base di OCR)

Successivamente, avvia il motore OCR. Pensa a `OcrEngine` come al cervello che leggerà l’immagine e produrrà i caratteri.

```python
# Step 2: Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

La maggior parte delle librerie OCR ti permette di regolare lingua, DPI o soglie di confidenza qui. Per questo **esempio base di OCR** rimarremo sui valori predefiniti, ma potrai esplorare `ocr_engine.config` più avanti se devi gestire documenti multilingue.

## Passo 3 – Carica la tua immagine TIFF (leggi file tiff con Python)

Ecco dove entra in gioco la parte **leggi file tiff con Python**. I TIFF possono contenere più pagine, ma `Image.load` carica la prima pagina per impostazione predefinita—perfetto per una scansione a pagina singola.

```python
# Step 3: Load the image you want to recognize
# Using a generic placeholder path makes it easy to adapt the example
ocr_engine.image = Image.load(Path("YOUR_DIRECTORY/input.tiff"))
```

Sostituisci `"YOUR_DIRECTORY"` con la cartella reale che contiene `input.tiff`. Se non sei sicuro da dove venga eseguito lo script, `Path.cwd()` stampa la directory di lavoro corrente—utile per il debug dei percorsi.

## Passo 4 – Esegui il processo OCR (estrai testo da immagine)

Ora avviene la magia. Chiamare `process()` invia l’immagine attraverso la pipeline OCR e restituisce un oggetto risultato.

```python
# Step 4: Run the OCR process to extract text from the image
ocr_result = ocr_engine.process()
```

Dietro le quinte il motore potrebbe convertire l’immagine in scala di grigi, applicare una soglia e passarla a una rete neurale. Non devi gestire questi passaggi; la libreria li astrae.

## Passo 5 – Stampa il testo riconosciuto (converti testo da immagine scansionata)

Infine, stampa il testo. Nei progetti reali probabilmente lo scriveresti su un file o in un database, ma la stampa mantiene l’esempio ordinato.

```python
# Step 5: Print the recognized text to the console
print(ocr_result.text)
```

Quando esegui lo script, dovresti vedere qualcosa del genere:

```
Hello, world!
This is a sample scanned document.
```

Se l’output appare confuso, ricontrolla che l’immagine di origine sia chiara e che la lingua OCR corrisponda al testo.

## Script completo funzionante

Mettendo tutto insieme, ecco il programma completo, pronto da eseguire:

```python
# Full script: how to ocr python – basic OCR example

from pathlib import Path
from aocr import OcrEngine, Image  # Replace with your OCR library if needed

def main():
    # Initialize the OCR engine
    ocr_engine = OcrEngine()

    # Load the TIFF image (adjust the path as needed)
    image_path = Path("YOUR_DIRECTORY/input.tiff")
    if not image_path.is_file():
        raise FileNotFoundError(f"Could not find {image_path}. Make sure the file exists.")
    
    ocr_engine.image = Image.load(image_path)

    # Perform OCR
    ocr_result = ocr_engine.process()

    # Output the extracted text
    print("=== OCR Output ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

### Output atteso

```
=== OCR Output ===
Your scanned document’s text appears here, line by line.
```

Se devi **convertire testo da immagini scansionate** in un PDF ricercabile, puoi passare `ocr_result.text` a un generatore PDF come `reportlab`—ma questo è un tutorial a sé stante.

## Problemi comuni & consigli professionali

- **Scansioni a bassa risoluzione**: l’OCR fatica sotto i 150 DPI. Se il tuo TIFF è sfocato, aumentane la risoluzione prima con Pillow (`Image.open(...).resize(...)`).
- **Pagine multiple**: per TIFF multi‑pagina, itera su `Image.load_multi_page()` (se la tua libreria lo supporta) e concatena i risultati.
- **Supporto linguistico**: molti motori usano l’inglese di default. Imposta `ocr_engine.language = "spa"` per lo spagnolo, ad esempio.
- **Gestione degli spazi**: l’OCR aggiunge spesso interruzioni di riga indesiderate. Usa `str.splitlines()` o espressioni regolari per pulire l’output.
- **Prestazioni**: per elaborazioni in blocco, riutilizza una singola istanza di `OcrEngine` invece di crearne una nuova per ogni file.

## Estendere l'esempio

Ora che hai padroneggiato **come fare OCR con Python** per un’immagine singola, considera i prossimi passi:

1. **Elaborazione batch** – Scorri una directory di TIFF e scrivi ogni risultato in un file `.txt`.
2. **Integrazione con Pandas** – Salva il testo estratto insieme ai metadati per analisi rapide.
3. **Approccio ibrido** – Combina OCR con librerie NLP come `spaCy` per estrarre entità (nomi, date, importi) da fatture scansionate.
4. **Formati di file alternativi** – Sostituisci `Image.load` con `Image.from_bytes` per gestire immagini provenienti da API o database.

Tutti questi si basano sull’idea centrale di **estrarre testo da immagini** e **convertire testo da immagini scansionate** in qualcosa che le macchine possano comprendere.

## Conclusione

Abbiamo percorso un **esempio base di OCR** che mostra **come fare OCR con Python**, come **leggere file tiff con Python** e come **estrarre testo da immagini** con poche righe di codice. Lo script è autonomo, include la gestione degli errori e stampa direttamente il risultato, fornendo una solida base per qualsiasi progetto che debba trasformare documenti scansionati in testo modificabile.

Sentiti libero di sperimentare—sostituisci il backend OCR, modifica il pre‑processing o collega l’output a un flusso di lavoro successivo. Il cielo è il limite quando riesci a **convertire testo da immagini scansionate** in dati ricercabili e utilizzabili.

Hai domande su casi limite, pacchetti linguistici o ottimizzazione delle prestazioni? Lascia un commento qui sotto, e buona programmazione!

![esempio di come fare OCR con Python](/images/ocr-python-example.png "Screenshot dell'output dello script di OCR con Python")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}