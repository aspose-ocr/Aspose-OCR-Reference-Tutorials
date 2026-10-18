---
category: general
date: 2026-04-26
description: Come creare OCR rapidamente e in modo affidabile. Impara a estrarre il
  testo da un'immagine, caricare l'immagine per l'OCR e eseguire l'OCR su PNG con
  un dizionario personalizzato.
draft: false
keywords:
- how to create OCR
- extract text from image
- extract text scanned document
- load image for OCR
- run OCR on png
language: it
og_description: Come creare OCR in Python ed estrarre testo da un'immagine. Questa
  guida mostra come caricare un'immagine per l'OCR, eseguire l'OCR su PNG e utilizzare
  un dizionario personalizzato.
og_title: Come creare OCR in Python – Estrazione rapida del testo
tags:
- OCR
- Python
- Image Processing
title: Come creare OCR in Python – Estrarre testo da un'immagine
url: /it/python-java/general/how-to-create-ocr-in-python-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare OCR in Python – Guida passo‑passo

Ti sei mai chiesto **come creare OCR** che possa leggere i tuoi PDF scansionati, screenshot o appunti scritti a mano? Non sei l'unico. In molti progetti reali dobbiamo *estrarre testo da file immagine*, ma i motori pronti all'uso spesso inciampano su parole specifiche del dominio.  

In questo tutorial vedrai un esempio completo e eseguibile che carica un'immagine per OCR, applica un dizionario personalizzato e infine **esegue OCR su file PNG**. Alla fine sarai in grado di estrarre testo da qualsiasi immagine e adattare il motore alla tua terminologia.

## Cosa copre questo tutorial

* Installare il piccolo ma potente pacchetto `aocr` (o qualsiasi libreria compatibile).  
* Configurare un **dizionario personalizzato** in modo che termini come `aspocorp` o `licensekey` vengano riconosciuti.  
* **Caricare un'immagine per OCR**, sia essa PNG, JPEG o una pagina PDF scansionata.  
* Eseguire il processo OCR e stampare il risultato.  

Nessun link a documentazione esterna, solo una soluzione autonoma che puoi copiare‑incollare ed eseguire subito.

### Prerequisiti

* Python 3.8 o superiore (il codice utilizza le f‑string).  
* Familiarità di base con la riga di comando – digiterai un paio di comandi `pip install`.  
* Un file immagine (`technical_doc.png` nell'esempio) posizionato in un percorso a cui puoi fare riferimento.  

Se soddisfi questi tre punti, sei pronto per procedere.  

---

## Passo 1: Installa la libreria OCR

Per prima cosa, ci serve un motore OCR che supporti un oggetto di configurazione programmabile. Il pacchetto `aocr` è un wrapper leggero attorno a un motore OCR nativo e funziona bene per le demo.

```bash
# Install the library (run once)
pip install aocr
```

> **Suggerimento:** Se sei su Windows e incontri un errore di compilazione, prova `pip install aocr‑binary` che fornisce wheel pre‑compilati.

### Perché installare questa libreria?

`aocr` ci dà accesso diretto a un oggetto `config` dove possiamo iniettare un **dizionario personalizzato**. È il segreto per migliorare la precisione su vocabolari di nicchia.

---

## Passo 2: Crea l'istanza del motore OCR e aggiungi un dizionario personalizzato

Ora avviamo il motore e gli diciamo quali parole deve considerare note.

```python
from aocr import OcrEngine

# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Provide a custom dictionary to improve recognition of domain‑specific terms
ocr_engine.config.custom_dictionary = [
    "aspocorp",      # our company's brand name
    "ocrengine",    # the library name itself
    "licensekey"    # a common field in our contracts
]
```

### Perché un dizionario personalizzato è importante

I modelli OCR standard sono addestrati su corpora generici. Quando il modello vede “aspocorp”, potrebbe dividerlo in “aspo corp” o eliminare lettere del tutto. Fornendo una lista personalizzata, orientiamo il riconoscitore verso l'ortografia esatta di cui abbiamo bisogno, riducendo drasticamente lo sforzo di post‑processing.

---

## Passo 3: Carica l'immagine da elaborare

Qui è dove **carichiamo l'immagine per OCR**. Il metodo `Image.load` accetta una stringa di percorso e determina automaticamente il tipo di file.

```python
import aocr

# Step 3: Load the image that contains the text you want to extract
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/technical_doc.png")
```

> **Caso limite:** Se la tua fonte è un PDF multi‑pagina, converti prima ogni pagina in PNG (ad esempio con `pdf2image`) e fornisci le immagini una alla volta al motore.

### Consigli per una migliore qualità dell'immagine

* Mantieni la risoluzione di almeno 300 dpi.  
* Assicurati che l'immagine sia dritta; ruotala con `Pillow` se necessario.  
* Converti le scansioni a colori in scala di grigi per ridurre il rumore.

---

## Passo 4: Esegui il processo OCR sul file PNG

Con il motore configurato e l'immagine caricata, finalmente **eseguiamo OCR su PNG**.

```python
# Step 4: Run the OCR process
ocr_result = ocr_engine.process()
```

La chiamata `process()` restituisce un oggetto che contiene il testo riconosciuto, i punteggi di confidenza e le bounding box per ogni parola.

---

## Passo 5: Output del testo riconosciuto

Il modo più semplice per vedere cosa ha trovato il motore è stampare l'attributo `text`.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### Output previsto

Se `technical_doc.png` contiene la frase *“The Aspocorp licensekey expires on 2025‑12‑31.”*, la console dovrebbe mostrare:

```
The Aspocorp licensekey expires on 2025-12-31.
```

Nota come il dizionario personalizzato ha mantenuto intatto il nome del brand—qualcosa che un OCR standard potrebbe aver distorto.

---

## Esempio completo funzionante (pronto per copia‑incolla)

Di seguito trovi l'intero script, pronto per essere salvato come `run_ocr.py`. Sostituisci semplicemente il percorso segnaposto con la posizione della tua immagine.

```python
# run_ocr.py
# -------------------------------------------------
# Complete example showing how to create OCR,
# load an image, apply a custom dictionary,
# and extract text from a PNG file.
# -------------------------------------------------

from aocr import OcrEngine
import aocr

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Add domain‑specific words
    ocr_engine.config.custom_dictionary = [
        "aspocorp",
        "ocrengine",
        "licensekey"
    ]

    # 3️⃣ Load the image you want to process
    #    (Make sure the path points to a real file)
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    ocr_engine.image = aocr.Image.load(image_path)

    # 4️⃣ Run the OCR engine
    ocr_result = ocr_engine.process()

    # 5️⃣ Print the extracted text
    print("=== Extracted Text ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

Eseguilo dal terminale:

```bash
python run_ocr.py
```

Dovresti vedere il testo estratto stampato sulla console, esattamente come mostrato nell'esempio precedente.

---

## Domande frequenti (FAQ)

| Question | Answer |
|----------|--------|
| **Posso estrarre testo da un PDF scansionato?** | Sì. Converti prima ogni pagina in PNG (o TIFF), poi fornisci le immagini allo stesso script. |
| **E se la mia immagine è un JPEG invece di PNG?** | Il metodo `Image.load` supporta JPEG, BMP, TIFF e PNG nativamente. Basta cambiare l'estensione del file. |
| **Come posso migliorare la precisione su scansioni a basso contrasto?** | Pre‑processa con `Pillow` – aumenta il contrasto, applica la binarizzazione o usa `opencv` per correggere l'inclinazione. |
| **È possibile ottenere i punteggi di confidenza per ogni parola?** | `ocr_result` include `words` – ogni parola ha un attributo `confidence` che puoi iterare. |
| **Posso eseguire questo su un server headless?** | Assolutamente. `aocr` non ha dipendenze GUI, rendendolo perfetto per pipeline CI. |

---

## Prossimi passi e argomenti correlati

Ora che sai **come creare OCR** e **estrarre testo da file immagine**, considera di esplorare:

* **Tecniche di pre‑processing** – `load image for OCR` è solo il primo passo; usa `opencv` per denoise o sharpen.  
* **Elaborazione batch** – cicla su una directory di PNG per generare un archivio ricercabile.  
* **Supporto multilingua** – aggiungi pacchetti linguistici al motore se devi leggere documenti in francese o tedesco.  
* **Integrazione con Elasticsearch** – indicizza il testo estratto per la ricerca full‑text tra le risorse scansionate.  

Ognuna di queste estensioni si basa sul modello di base che abbiamo appena coperto, quindi troverai la transizione senza problemi.

---

## Conclusioni

In pochi minuti abbiamo risposto a **come creare OCR** che estragga in modo affidabile **testo da file immagine**, specialmente PNG, e ti abbiamo mostrato come **caricare immagine per OCR**, applicare un **dizionario personalizzato** e **eseguire OCR su PNG** senza alcun servizio esterno.  

Prova lo script, modifica il dizionario per adattarlo al tuo gergo, e avrai una solida base per qualsiasi progetto di digitalizzazione di documenti.  

Se hai incontrato problemi, lascia un commento qui sotto—siamo felici di aiutare. E non dimenticare di condividere le tue storie di successo; la community impara meglio dagli esempi reali.  

**Pronto a automatizzare la tua burocrazia?** Prendi il codice, adattalo e inizia a trasformare i pixel in testo ricercabile oggi stesso!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}