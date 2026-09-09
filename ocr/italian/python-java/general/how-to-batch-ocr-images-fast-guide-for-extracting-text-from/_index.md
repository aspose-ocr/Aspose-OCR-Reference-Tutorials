---
category: general
date: 2026-01-12
description: Come eseguire OCR di immagini in batch rapidamente ed estrarre testo
  da file JPEG in Python. Impara il processamento batch passo‑passo con un esempio
  completo e funzionante.
draft: false
keywords:
- how to batch OCR images
- extract text from JPEG files
language: it
og_description: Come eseguire l'OCR di immagini in batch ed estrarre il testo da file
  JPEG. Questa guida ti accompagna passo passo in una soluzione Python completa e
  pronta all'uso.
og_title: Come eseguire OCR di immagini in batch – Rapido tutorial Python
tags:
- OCR
- Python
- image processing
title: Come fare OCR di immagini in batch – Guida rapida per estrarre testo da file
  JPEG
url: /it/python-java/general/how-to-batch-ocr-images-fast-guide-for-extracting-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR batch su immagini – Guida rapida per estrarre testo da file JPEG

Ti sei mai chiesto **come eseguire OCR batch su immagini** senza dover scrivere uno script separato per ogni file? Non sei l'unico. In molti progetti—scansione di fatture, digitalizzazione di archivi o moderazione di contenuti—abbiamo bisogno di estrarre testo da decine o centinaia di file JPEG in un'unica operazione. La buona notizia è che puoi farlo con poche righe di Python, ottenendo un motore riutilizzabile da inserire in qualsiasi pipeline.

In questo tutorial ti mostreremo esattamente **come eseguire OCR batch su immagini**, poi passeremo all'estrazione del testo da file JPEG, alla gestione dei casi limite e alla verifica dell'output. Alla fine avrai uno script autonomo che potrai eseguire su qualsiasi cartella di immagini, e comprenderai perché l'elaborazione batch è importante per le prestazioni e la manutenibilità.

## Cosa imparerai

- Configurare un semplice motore OCR e impostarlo per l'inglese.  
- Raccogliere tutti i file JPEG da una directory con `pathlib`.  
- Chiamare il motore OCR una sola volta per elaborare l'intero batch.  
- Visualizzare un'anteprima del testo riconosciuto per ogni immagine.  
- Suggerimenti per gestire batch di grandi dimensioni, lingue diverse e problemi comuni.

**Prerequisiti**: Python 3.8+, la libreria `ocr` (o qualsiasi wrapper compatibile) e una cartella di immagini JPEG da analizzare. Non sono richiesti servizi esterni—tutto gira in locale.

---

## Passo 1: Inizializzare il motore OCR – Il nucleo di Come eseguire OCR batch su immagini

Prima di poter **eseguire OCR batch su immagini**, abbiamo bisogno di un motore che sappia leggere il testo. Nella maggior parte delle librerie si crea un oggetto motore, si imposta opzionalmente la lingua, e lo si riutilizza per ogni file.

```python
import ocr
import pathlib

# Create the OCR engine and set it to English (the most common case)
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

*Perché è importante*: Inizializzare il motore una sola volta evita il sovraccarico di caricare ripetutamente i modelli linguistici. Inoltre ti offre un unico punto dove modificare le impostazioni (ad es., DPI, whitelist di caratteri) che verranno applicate a tutto il batch.

> **Consiglio professionale**: Se prevedi di elaborare documenti multilingue, sostituisci `ocr.Language.ENGLISH` con `ocr.Language.MULTI` o carica più pacchetti linguistici prima dell'inizio del batch.

---

## Passo 2: Raccogliere tutti i file JPEG – La parte “Estrai testo da file JPEG”

Ora che il motore è pronto, dobbiamo dirgli su quali immagini lavorare. Usare `pathlib` rende il codice indipendente dalla piattaforma e conciso.

```python
# Replace YOUR_DIRECTORY with the path that holds your JPEG files
image_dir = pathlib.Path("YOUR_DIRECTORY/")
image_paths = list(image_dir.glob("*.jpg"))  # only JPEG files, case‑sensitive
```

*Perché è importante*: Raccogliendo prima l'elenco dei file, possiamo passare l'intera collezione al motore OCR in una sola chiamata—esattamente ciò che significa **come eseguire OCR batch su immagini**. Se hai sottocartelle, puoi cambiare `glob("**/*.jpg")` in una ricerca ricorsiva.

> **Caso limite**: Se le tue immagini hanno estensioni miste (`.jpeg`, `.JPG`), estendi il pattern glob: `image_dir.rglob("*.[jJ][pP][eE]?g")`.

---

## Passo 3: Elaborare l'intero batch in una sola chiamata – Il vero potere dell'OCR batch

La maggior parte delle librerie OCR moderne espone un metodo `process_batch` (o con nome simile) che accetta un iterabile di percorsi file. Questo è il cuore di **come eseguire OCR batch su immagini** in modo efficiente.

```python
# Process every JPEG file in a single batch operation
ocr_results = ocr_engine.process_batch(image_paths)
```

*Perché è importante*: Una singola chiamata batch riduce il numero di transizioni Python‑to‑C, mantiene il modello linguistico caricato in memoria e spesso abilita il parallelismo interno. Il risultato è una lista di oggetti—ognuno contenente il testo riconosciuto e i punteggi di confidenza.

> **Nota sulle prestazioni**: Per batch molto grandi (migliaia di immagini), considera di suddividere l'elenco in blocchi più piccoli (ad es., 200 file) per evitare un consumo eccessivo di memoria.

---

## Passo 4: Mostrare un'anteprima del testo estratto – Validazione rapida

Al termine del batch, è utile dare un'occhiata ai primi caratteri di ogni risultato. Questo ti aiuta a confermare che l'OCR stia effettivamente estraendo testo dai tuoi file JPEG.

```python
for image_path, ocr_result in zip(image_paths, ocr_results):
    # Show the image name and the first 100 characters of its recognised text
    preview = ocr_result.text[:100].replace("\n", " ").strip()
    print(f"{image_path.name}: {preview}...")
```

*Perché è importante*: Un'anteprima breve ti permette di individuare fallimenti evidenti (ad es., output vuoto, caratteri illeggibili) senza aprire ogni file. Se noti problemi sistematici, puoi regolare le impostazioni del motore e rieseguire il batch.

> **Trappola comune**: Dimenticare di rimuovere i caratteri di nuova riga può rendere l'anteprima disordinata. La riga `replace("\n", " ")` la pulisce.

---

## Esempio completo funzionante – Tutti i passaggi combinati

Di seguito trovi lo script completo che puoi copiare‑incollare, modificare il percorso della directory e avviare. Dimostra l'intero workflow di **come eseguire OCR batch su immagini** dall'inizio alla fine.

```python
import ocr
import pathlib

def batch_ocr_jpeg(folder: str):
    """
    Process all JPEG files in `folder` and print a 100‑character preview
    of the recognised text for each image.
    """
    # Step 1 – Initialise OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – Gather JPEG paths
    img_dir = pathlib.Path(folder)
    jpeg_paths = list(img_dir.glob("*.jpg"))  # add more patterns if needed

    if not jpeg_paths:
        print("No JPEG files found in the specified directory.")
        return

    # Step 3 – Batch process
    results = engine.process_batch(jpeg_paths)

    # Step 4 – Display previews
    for path, res in zip(jpeg_paths, results):
        preview = res.text[:100].replace("\n", " ").strip()
        print(f"{path.name}: {preview}...")

if __name__ == "__main__":
    # Replace with the path containing your JPEG images
    batch_ocr_jpeg("YOUR_DIRECTORY/")
```

**Output previsto** (esempio):

```
invoice_001.jpg: Invoice #001  Date: 2024-03-15  Total: $1,245.00  Bill To: Acme Corp...
receipt_202.jpg: Receipt 202  Store: QuickMart  Total: $45.67  Date: 03/12/2024...
...
```

Se l'anteprima mostra testo significativo, hai estratto con successo **testo da file JPEG** usando un approccio batch.

---

## Gestione di batch grandi e scenari avanzati

### Suddivisione di carichi di lavoro voluminosi
Quando si hanno migliaia di immagini, la memoria può diventare un collo di bottiglia. Dividi l'elenco in blocchi più piccoli:

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(jpeg_paths, 200):  # 200 files per batch
    results = engine.process_batch(chunk)
    # process results as shown earlier
```

### Cambio lingua
Se i tuoi documenti contengono francese o spagnolo, cambia la lingua prima del batch:

```python
engine.language = ocr.Language.FRENCH  # or ocr.Language.SPANISH
```

### Salvataggio dei risultati su disco
Invece di stampare, potresti voler scrivere ogni risultato OCR in un file `.txt`:

```python
output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for path, res in zip(jpeg_paths, results):
    txt_path = output_dir / f"{path.stem}.txt"
    txt_path.write_text(res.text, encoding="utf-8")
```

---

## Conclusione

Ora sai **come eseguire OCR batch su immagini** e affidabilmente **estrarre testo da file JPEG** usando uno script Python compatto. Inizializzando il motore una sola volta, raccogliendo tutti i percorsi JPEG, elaborandoli in un unico batch e visualizzando l'output, ottieni sia velocità che semplicità. Da qui puoi ampliare il workflow—aggiungere supporto multilingue, memorizzare i risultati in un database, o integrare lo script in una pipeline di elaborazione documenti più ampia.

Pronto per il passo successivo? Prova a sostituire la libreria `ocr` con Tesseract, sperimenta diversi pre‑processamenti dell'immagine (soglia, ridimensionamento), o alimenta il testo estratto a un modello di elaborazione del linguaggio naturale per una categorizzazione automatica. Il cielo è il limite, e hai ora una solida base su cui costruire.

Buon coding, e che i tuoi batch OCR siano sempre privi di errori!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}