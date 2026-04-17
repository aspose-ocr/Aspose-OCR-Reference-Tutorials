---
category: general
date: 2026-03-26
description: Come eseguire l'OCR su un file PNG ed estrarre il testo dall'immagine
  con un dizionario personalizzato per migliorare l'accuratezza dell'OCR. Impara a
  caricare rapidamente l'immagine per l'OCR.
draft: false
keywords:
- how to run OCR
- extract text from image
- recognize text from png
- improve OCR accuracy
- load image for OCR
language: it
og_description: Come eseguire l'OCR su un file PNG ed estrarre il testo dall'immagine
  con un dizionario personalizzato per migliorare l'accuratezza dell'OCR. Guida passo
  passo.
og_title: Come eseguire l'OCR – Estrarre testo da un'immagine in Python
tags:
- OCR
- Python
- Image Processing
title: Come eseguire OCR – Estrarre testo da un'immagine in Python
url: /it/python-java/general/how-to-run-ocr-extract-text-from-image-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR – Estrarre testo da un'immagine in Python

Ti sei mai chiesto **come eseguire OCR** su una fattura scannerizzata o su uno screenshot e ottenere testo pulito e ricercabile? Non sei solo. In molti progetti il collo di bottiglia è semplicemente caricare l'immagine per l'OCR e poi convincere il motore a comprendere parole specifiche del dominio.  

In questo tutorial percorreremo un esempio completo, pronto all'uso, che **estrae testo da file immagine**, ti mostra come **riconoscere testo da PNG** e persino dimostra trucchi per **migliorare la precisione dell'OCR** con dizionari personalizzati e caratteri speciali. Alla fine avrai uno script autonomo da inserire in qualsiasi codebase Python.

## Cosa ti serve

- Python 3.8+ (il codice usa type hints ma funziona anche su versioni 3.x precedenti)
- La libreria `ocr` fornita con il motore OCR che stai utilizzando (installa via `pip install ocr‑engine` – sostituisci con il nome reale del pacchetto)
- Un file immagine (`input.png`) che desideri elaborare
- Opzionale: un file di testo semplice (`invoice_terms.txt`) con parole specifiche del dominio, una per riga

Nessuna dipendenza esterna pesante, nessuna chiave API cloud, solo un motore OCR locale.

---

## Passo 1: Installa e importa la libreria OCR

Per prima cosa, assicurati che il pacchetto OCR sia installato. Se usi il pacchetto ipotetico `ocr-engine`, esegui:

```bash
pip install ocr-engine
```

Ora importa le classi di cui avrai bisogno:

```python
# Step 1: Import the OCR SDK
import ocr
from ocr import Imaging
```

> **Consiglio:** Se lavori in un ambiente virtuale, attivalo prima di installare per mantenere pulito il tuo Python globale.

## Passo 2: Crea un'istanza del motore OCR

Creare un oggetto motore è il punto di ingresso per ogni attività OCR. Pensalo come accendere l'hardware dello scanner in software.

```python
# Step 2: Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
```

Perché è importante: il motore conserva configurazioni come pacchetti linguistici, modalità di riconoscimento e qualsiasi risorsa personalizzata che allegherai in seguito. Senza di esso non puoi **caricare l'immagine per OCR** né eseguire la pipeline di riconoscimento.

## Passo 3: Carica l'immagine da riconoscere

Qui **carichiamo l'immagine per OCR**. Il metodo `Imaging.Image.load()` legge il file e lo converte nel formato bitmap interno che il motore si aspetta.

```python
# Step 3: Load the PNG image you want to process
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Imaging.Image.load(image_path))
```

Se hai un JPEG o TIFF, lo stesso metodo funziona—basta cambiare l'estensione. Il motore rileva automaticamente il formato.

> **Caso limite:** Immagini molto grandi (oltre 5 MP) possono provocare picchi di memoria. Considera di ridimensionarle con Pillow prima del caricamento se incontri problemi di prestazioni.

## Passo 4: Fornisci un dizionario personalizzato per aumentare la precisione

La maggior parte dei motori OCR include modelli linguistici generici. Per fatture, ricevute o documenti legali spesso mancano parole. Fornire una lista di parole personalizzata dice al motore “questi termini sono legittimi, trattali come corretti”.

```python
# Step 4: Attach a custom dictionary (one word per line)
custom_dict_path = "YOUR_DIRECTORY/invoice_terms.txt"
ocr_engine.set_custom_dictionary(custom_dict_path)
```

Esempi tipici di voci potrebbero essere:

```
VAT
InvoiceNumber
Øre
ß
Ħ
```

Aggiungere queste migliora drasticamente la metrica **migliorare la precisione OCR**—soprattutto per simboli non ASCII.

## Passo 5: Aggiungi caratteri speciali non coperti dal set predefinito

Se il tuo dominio utilizza simboli come il segno Euro (€) o la Ø scandinava, puoi aggiungerli esplicitamente:

```python
# Step 5: Register additional characters
ocr_engine.add_custom_characters("ØßĦ")
```

Il motore tratterà ora quei glifi come validi durante la fase di riconoscimento, riducendo la probabilità di output “spazzatura”.

## Passo 6: Esegui il processo OCR e recupera il testo

Infine, invoca il riconoscitore e ottieni il risultato in plain‑text. La chiamata `recognize()` restituisce un oggetto ricco; per la maggior parte dei casi ti serve solo la stringa grezza.

```python
# Step 6: Execute OCR and print the result
result = ocr_engine.recognize()
print("=== Recognized Text ===")
print(result.get_text())
```

**Output previsto** (troncato per brevità):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total: €1,250.00
VAT: 25%
...
```

Se l'output appare confuso, verifica che il tuo dizionario personalizzato e i caratteri speciali siano stati caricati correttamente.

---

## Panoramica visiva

![diagramma di come eseguire OCR](ocr-workflow.png){alt="diagramma di come eseguire OCR"}

Il diagramma sopra illustra il flusso dal caricamento dell'immagine all'ottenimento di testo pulito, evidenziando dove è possibile inserire dizionari personalizzati e set di caratteri.

---

## Domande frequenti e trappole

### Funziona con PDF multi‑pagina?

Sì—basta convertire ogni pagina in PNG (usando `pdf2image` o simili) e passarle sequenzialmente alla stessa istanza `ocr_engine`. Il motore elabora ogni immagine indipendentemente, così otterrai una lista di stringhe che potrai concatenare.

### E se l'immagine è ruotata?

La maggior parte dei motori OCR moderni rileva automaticamente l'orientamento, ma puoi forzare una rotazione con:

```python
ocr_engine.set_image(Imaging.Image.load(image_path).rotate(90))
```

### Come gestire lingue diverse dall'inglese?

Scambia il modello linguistico prima di caricare l'immagine:

```python
ocr_engine.set_language("de")  # German
```

Assicurati che il relativo pacchetto linguistico sia installato.

---

## Script completo – Pronto da copiare e incollare

Di seguito trovi l'intero programma, pronto per l'esecuzione dopo aver sostituito i percorsi segnaposto.

```python
#!/usr/bin/env python3
"""
How to Run OCR – Complete example that extracts text from a PNG,
uses a custom dictionary, and adds special characters for better accuracy.
"""

# Install the OCR package first:
# pip install ocr-engine

import ocr
from ocr import Imaging

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = ocr.OcrEngine()

    # 2️⃣ Load the image you want to recognize
    image_path = "YOUR_DIRECTORY/input.png"      # <-- change this
    ocr_engine.set_image(Imaging.Image.load(image_path))

    # 3️⃣ Provide a custom dictionary (optional but recommended)
    dict_path = "YOUR_DIRECTORY/invoice_terms.txt"   # one word per line
    ocr_engine.set_custom_dictionary(dict_path)

    # 4️⃣ Add any special characters not covered by the default set
    ocr_engine.add_custom_characters("ØßĦ")   # e.g., currency symbols

    # 5️⃣ Run the OCR process
    result = ocr_engine.recognize()

    # 6️⃣ Output the recognized text
    print("=== Recognized Text ===")
    print(result.get_text())

if __name__ == "__main__":
    main()
```

Eseguilo con:

```bash
python run_ocr.py
```

Dovresti vedere il testo estratto stampato sulla console. Da lì potrai scriverlo su un file, inserirlo in un database o passarlo a pipeline NLP successive.

---

## Riepilogo e prossimi passi

Abbiamo coperto **come eseguire OCR** su un PNG, come **estrarre testo da immagine**, e mostrato modi pratici per **riconoscere testo da PNG** migliorando **la precisione OCR** con dizionari e caratteri personalizzati.  

Prossimi step consigliati:

- **Elaborazione batch:** cicla su una cartella di immagini.
- **Post‑processing:** usa regex per estrarre numeri di fattura o date.
- **Integrazione:** collega lo script a un'API Flask per servizi OCR on‑demand.

Se vuoi approfondire, dai un'occhiata ai tutorial su **caricare immagine per OCR** con pre‑elaborazione OpenCV, o esplora modelli OCR basati su deep‑learning come Tesseract 4+ con layer LSTM.

---

### Continua a sperimentare!

Prova a sostituire `invoice_terms.txt` con una lista di terminologia medica, aggiungi caratteri greci, o fornisci al motore una foto a bassa risoluzione per vedere fino a che punto può arrivare la precisione. Più sperimenti, più comprenderai i compromessi tra pre‑elaborazione, vocabolari personalizzati e impostazioni del motore.

Buon coding, e che i tuoi risultati OCR siano sempre nitidi!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}