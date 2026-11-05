---
category: general
date: 2026-03-26
description: Scopri come eseguire l'OCR in Python ed estrarre facilmente il testo
  da un'immagine, leggere il testo da una scansione o estrarre il testo da una fattura
  utilizzando un semplice OcrEngine.
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from scan
- extract text from invoice
- how to use OCR
language: it
og_description: Come eseguire l'OCR in Python? Questa guida ti mostra come estrarre
  testo da un'immagine, leggere testo da una scansione e estrarre testo da una fattura
  in pochi minuti.
og_title: Come eseguire l'OCR in Python – Estrarre il testo rapidamente
tags:
- OCR
- Python
- Image Processing
title: Come eseguire OCR in Python – Estrai il testo rapidamente
url: /it/python/general/how-to-perform-ocr-in-python-extract-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR in Python – Estrarre testo rapidamente

Ti sei mai chiesto **come eseguire OCR** su una ricevuta scansionata o su un PDF sfocato? Non sei solo. In molti progetti la necessità di **estrarre testo da immagine** compare prima o poi, e l’approccio “digitare tutto a mano” semplicemente non è scalabile.  

In questo tutorial vedrai un esempio completo, pronto‑all‑uso, che mostra **come usare OCR** per leggere testo da una scansione, estrarre dati da una fattura e persino gestire la correzione automatica dell’inclinazione—tutto con poche righe di Python.

## Cosa imparerai

Passeremo in rassegna tutto ciò che devi sapere:

* Le dipendenze e le importazioni esatte necessarie.  
* Come creare e configurare un’istanza di `OcrEngine`.  
* Modi per **estrarre testo da immagine**, **leggere testo da scansione** e **estrarre testo da fattura** usando lo stesso motore.  
* Trappole comuni (lingua errata, file mancanti, immagini grandi) e come evitarle.  
* Output previsto così potrai verificare che l’OCR abbia avuto successo.

Non servono link a documentazione esterna—tutto è contenuto qui, quindi puoi copiare‑incollare il codice e vedere i risultati subito.

## Prerequisiti

Prima di immergerci, assicurati di avere:

* Python 3.8+ installato (il pacchetto `ocr` funziona con qualsiasi versione recente).  
* La libreria `ocr` disponibile (`pip install ocr‑engine` – sostituisci con il nome reale del pacchetto se diverso).  
* Un file immagine da elaborare – per la demo useremo `invoice.png` situato in una cartella chiamata `YOUR_DIRECTORY`.

Questo è tutto. Se hai già questi elementi, sei pronto per partire.

## Passo 1: Installa e importa il modulo OCR

Prima di tutto: ci serve la libreria OCR. Se non l’hai ancora installata, esegui il comando seguente nel terminale:

```bash
pip install ocr-engine
```

Ora importiamo il modulo nel nostro script.

```python
# Step 1: Import the OCR module
import ocr
```

> **Pro tip:** Mantieni il tuo ambiente virtuale ordinato; evita conflitti di versione quando aggiungi in seguito altri pacchetti di elaborazione immagini.

## Passo 2: Crea e configura il motore OCR

Creare il motore è semplice come chiamare il suo costruttore, ma il vero potere sta nella configurazione corretta. Imposteremo la lingua su English e attiveremo la correzione automatica dell’inclinazione, fondamentale quando si trattano fatture scansionate non perfettamente allineate.

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Step 3: Configure the engine – set language and enable automatic skew correction
engine.language = ocr.Language.English   # any supported language, e.g., Spanish, French
engine.auto_skew = True                 # fixes tilted scans automatically
```

Perché abilitare `auto_skew`? Molti scanner producono immagini leggermente inclinate di qualche grado. Senza correzione il motore potrebbe perdere caratteri, trasformando una fattura perfettamente leggibile in un miscuglio incomprensibile.

## Passo 3: Esegui OCR sull’immagine di destinazione

Ora forniamo il file immagine al motore. Il metodo `recognize_image` restituisce un oggetto che contiene il testo grezzo così come i punteggi di confidenza (se la libreria li fornisce).

```python
# Step 4: Perform OCR on the target image
ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

Se stai lavorando con uno scenario **leggere testo da scansione**, sostituisci semplicemente il percorso con il PDF scansionato convertito in PNG o JPEG. La stessa chiamata funziona per qualsiasi formato immagine supportato dalla libreria sottostante.

## Passo 4: Ispeziona e utilizza il testo estratto

Stampiamo l’output OCR grezzo. In una pipeline reale di elaborazione fatture probabilmente parserai questa stringa, estrarrai righe di dettaglio, totali e date, ma per ora un rapido sguardo confermerà che l’OCR ha avuto successo.

```python
# Step 5: Display the raw extracted text
print("Raw OCR text:\n", ocr_result.text)
```

**Output previsto (troncato per brevità):**

```
Raw OCR text:
 Invoice #12345
 Date: 2026‑03‑01
 Bill To: Acme Corp.
 Item          Qty   Price   Total
 ------------------------------------------------
 Widget A      10    5.00    50.00
 Widget B      5     12.00   60.00
 ------------------------------------------------
 Subtotal:                     110.00
 Tax (5%):                     5.50
 Grand Total:                  115.50
```

Se l’output appare confuso, ricontrolla che l’immagine sia nitida e che `engine.language` corrisponda alla lingua del documento.

## Passo 5: Gestione dei casi limite comuni

### Immagini grandi

Elaborare una scansione di 5000 × 5000 pixel può consumare molta memoria. Un modo rapido per mitigare il problema è ridimensionare l’immagine prima di inviarla al motore:

```python
from PIL import Image

def load_and_resize(path, max_dim=2000):
    img = Image.open(path)
    img.thumbnail((max_dim, max_dim), Image.ANTIALIAS)
    return img

scaled_image = load_and_resize("YOUR_DIRECTORY/invoice.png")
ocr_result = engine.recognize_image(scaled_image)
```

### Lingue multiple

Se devi **estrarre testo da immagine** contenente sia inglese che spagnolo, puoi impostare una lista di lingue:

```python
engine.language = [ocr.Language.English, ocr.Language.Spanish]
```

Il motore proverà a riconoscere i caratteri di entrambi i set.

### Gestione degli errori

Non dare mai per scontato che il file esista. Avvolgi la chiamata in un blocco try‑except per fornire un messaggio amichevole:

```python
try:
    ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
    print("OCR succeeded!")
except FileNotFoundError:
    print("Error: The image file was not found. Check the path and try again.")
except ocr.OcrError as e:
    print(f"OCR failed with error: {e}")
```

## Riferimento visivo

Di seguito uno screenshot della fattura di esempio usata nella demo. Nota la leggera inclinazione—esattamente ciò che corregge `auto_skew`.

![how to perform OCR on an invoice](/images/ocr-example.png)

*Alt text:* come eseguire OCR su un’immagine di fattura che mostra la correzione automatica dell’inclinazione.

## Esempio completo, eseguibile

Riunendo tutto, ecco uno script unico che puoi eseguire dalla riga di comando. Copre installazione, configurazione, gestione degli errori e un semplice passaggio di post‑processing che scrive il testo estratto in un file chiamato `output.txt`.

```python
# full_ocr_demo.py
# -------------------------------------------------
# Demonstrates how to perform OCR, extract text from image,
# read text from scan, and extract text from invoice.
# -------------------------------------------------

import ocr
from pathlib import Path

def main(image_path: str, output_path: str = "output.txt"):
    # Create and configure the engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.auto_skew = True

    # Verify the image exists
    if not Path(image_path).is_file():
        print(f"❌  Image not found: {image_path}")
        return

    # Run OCR
    try:
        result = engine.recognize_image(image_path)
    except ocr.OcrError as err:
        print(f"❌  OCR failed: {err}")
        return

    # Output the raw text
    print("✅  OCR completed. Raw text:")
    print(result.text)

    # Save to a text file for later processing
    Path(output_path).write_text(result.text, encoding="utf-8")
    print(f"💾  Text saved to {output_path}")

if __name__ == "__main__":
    # Replace with your actual file location
    main("YOUR_DIRECTORY/invoice.png")
```

Eseguendo `python full_ocr_demo.py` verrà stampato il testo estratto nella console e salvato in `output.txt`. Da lì potrai applicare espressioni regolari, scrittori CSV o qualsiasi altra logica necessaria per l’automazione di **estrarre testo da fattura**.

## Conclusione

Ora disponi di una risposta solida, end‑to‑end, a **come eseguire OCR** in Python. Creando un `OcrEngine`, configurando lingua e correzione dell’inclinazione, e gestendo alcuni casi pratici, puoi affidabilmente **estrarre testo da immagine**, **leggere testo da scansione**, e **estrarre testo da fattura** senza dover setacciare documentazione sparsa.

Qual è il prossimo passo? Prova a elaborare un batch di file in un ciclo, sperimenta con lingue diverse, o collega l’output a una libreria di generazione PDF per creare PDF ricercabili. Il cielo è il limite, e il codice appena mostrato è una solida piattaforma di lancio.

Hai domande su un formato di file specifico o hai bisogno di aiuto per regolare le soglie di confidenza? Lascia un commento qui sotto—felice di aiutarti a perfezionare la tua pipeline OCR!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}