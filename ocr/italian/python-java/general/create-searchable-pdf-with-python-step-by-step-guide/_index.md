---
category: general
date: 2026-05-31
description: Crea PDF ricercabili da immagini scansionate usando Python OCR. Scopri
  come convertire PDF di immagini scansionate, convertire TIFF in PDF e aggiungere
  un livello di testo OCR in pochi minuti.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- convert tiff to pdf
- how to run OCR
- add OCR text layer
language: it
og_description: Crea PDF ricercabili all'istante. Questa guida mostra come eseguire
  l'OCR, convertire PDF di immagini scannerizzate e aggiungere un livello di testo
  OCR usando un unico script Python.
og_title: Crea PDF Ricercabile con Python – Tutorial Completo
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  headline: Create Searchable PDF with Python – Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  name: Create Searchable PDF with Python – Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: 1️⃣ Can I process multi‑page PDFs?
    text: Yes. Use `ocr_engine.load_image("file.pdf")` and then loop over each page
      with `ocr_engine.recognize(pdf_save_options, page_number)`. The library will
      automatically generate a multi‑page searchable PDF.
  - name: 2️⃣ What if my source file is a high‑resolution TIFF (300 dpi+)?
    text: 'Higher DPI yields better OCR accuracy but also larger memory usage. If
      you hit a `MemoryError`, downscale the image first:'
  - name: 3️⃣ How do I change the language of the OCR?
    text: 'Set the `language` property on the engine before loading the image:'
  - name: 4️⃣ What if I need to keep the original image quality?
    text: The `PdfSaveOptions` class has a `compression` property. Set it to `PdfCompression.None`
      to preserve the raster data exactly as it was.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Document Automation
title: Crea PDF Ricercabile con Python – Guida Passo‑Passo
url: /it/python-java/general/create-searchable-pdf-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea PDF Ricercabile con Python – Guida Passo‑Passo

Ti sei mai chiesto come **creare PDF ricercabili** da una pagina scansionata senza dover gestire decine di strumenti? Non sei il solo. In molti flussi di lavoro d'ufficio un TIFF o JPEG scansionato finisce su un'unità condivisa, e la persona successiva deve copiare‑incollare il testo manualmente—un'operazione dolorosa, soggetta a errori e dispendiosa in termini di tempo.  

In questo tutorial percorreremo una soluzione pulita e programmatica che ti permette di **convertire PDF immagine scansionata**, **convertire TIFF in PDF**, e **aggiungere un livello di testo OCR** in un unico passaggio. Alla fine avrai uno script pronto all'uso che esegue l'OCR, incorpora il testo nascosto e genera un PDF ricercabile che puoi indicizzare, cercare o condividere con fiducia.

## Cosa Ti Serve

- Python 3.9+ (qualsiasi versione recente va bene)
- `aspose-ocr` e `aspose-pdf` pacchetti (installati tramite `pip install aspose-ocr aspose-pdf`)
- Un file immagine scansionato (`.tif`, `.png`, `.jpg`, o anche una pagina PDF che è solo un'immagine)
- Una quantità modesta di RAM (il motore OCR è leggero; anche un laptop lo gestisce)

> **Suggerimento professionale:** Se sei su Windows, il modo più semplice per ottenere i pacchetti è eseguire il comando in una finestra PowerShell elevata.

```bash
pip install aspose-ocr aspose-pdf
```

Ora che i prerequisiti sono sistemati, immergiamoci nel codice.

## Passo 1: Crea un'Istanza del Motore OCR – *create searchable pdf*

La prima cosa che facciamo è avviare il motore OCR. Pensalo come il cervello che leggerà ogni pixel e lo trasformerà in caratteri.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine – this is the core of the create searchable pdf process
ocr_engine = OcrEngine()
```

> **Perché è importante:** Inizializzare il motore una sola volta mantiene basso l'uso della memoria. Se chiamassi `OcrEngine()` all'interno di un ciclo per ogni pagina, esauriresti rapidamente le risorse.

## Passo 2: Carica l'Immagine Scansionata – *convert tiff to pdf* & *convert scanned image pdf*

Successivamente, indica al motore il file che vuoi elaborare. L'API accetta qualsiasi immagine raster, quindi un TIFF funziona altrettanto bene di un JPEG.

```python
# Load the image you want to OCR. Replace the path with your own file location.
ocr_engine.load_image("YOUR_DIRECTORY/scanned_page.tif")
```

Se per caso disponi di un PDF che contiene solo un'immagine scansionata, puoi comunque usare `load_image` perché Aspose estrarrà automaticamente la prima pagina.

## Passo 3: Prepara le Opzioni di Salvataggio PDF – *add OCR text layer*

Qui configuriamo l'aspetto del PDF finale. Il flag cruciale è `create_searchable_pdf`; impostarlo a `True` indica alla libreria di incorporare un livello di testo invisibile che rispecchia il contenuto visivo.

```python
from aspose.pdf import PdfSaveOptions

pdf_save_options = PdfSaveOptions()
pdf_save_options.create_searchable_pdf = True   # embed OCR text layer
pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"
```

> **Cosa fa il livello di testo:** Quando apri il file risultante in Adobe Reader e provi a selezionare del testo, vedrai i caratteri nascosti. Anche i motori di ricerca possono indicizzarli—perfetto per conformità o archiviazione.

## Passo 4: Esegui OCR e Salva – *how to run OCR* in a single call

Ora avviene la magia. Una singola chiamata al metodo esegue il motore di riconoscimento e scrive il PDF ricercabile su disco.

```python
# Run OCR and generate the searchable PDF in one go
ocr_engine.recognize(pdf_save_options)

print("PDF saved as searchable PDF.")
```

Il metodo `recognize` restituisce un oggetto di stato che puoi ispezionare per eventuali errori, ma per la maggior parte degli scenari semplici la chiamata sopra è sufficiente.

### Output Previsto

Eseguendo lo script stampa:

```
PDF saved as searchable PDF.
```

Se apri `scanned_page_searchable.pdf` noterai che puoi selezionare il testo, copiarlo‑incollarlo e persino eseguire una ricerca `Ctrl+F`. Questo è il segno distintivo di un flusso di lavoro **create searchable pdf**.

## Script Completo Funzionante

Di seguito trovi lo script completo, pronto all'esecuzione. Sostituisci semplicemente i percorsi segnaposto con le tue posizioni di file effettive.

```python
# ------------------------------------------------------------
# create_searchable_pdf.py – Convert scanned image to searchable PDF
# ------------------------------------------------------------

from aspose.ocr import OcrEngine
from aspose.pdf import PdfSaveOptions

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load image (TIFF, JPEG, PNG, or scanned PDF page)
    image_path = "YOUR_DIRECTORY/scanned_page.tif"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure PDF output – embed OCR text layer
    pdf_save_options = PdfSaveOptions()
    pdf_save_options.create_searchable_pdf = True
    pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"

    # 4️⃣ Run OCR and write searchable PDF
    ocr_engine.recognize(pdf_save_options)

    print("PDF saved as searchable PDF.")

if __name__ == "__main__":
    main()
```

Salva questo file come `create_searchable_pdf.py` ed esegui:

```bash
python create_searchable_pdf.py
```

## Domande Frequenti & Casi Limite

### 1️⃣ Posso elaborare PDF multi‑pagina?

Sì. Usa `ocr_engine.load_image("file.pdf")` e poi itera su ogni pagina con `ocr_engine.recognize(pdf_save_options, page_number)`. La libreria genererà automaticamente un PDF ricercabile multi‑pagina.

### 2️⃣ Cosa succede se il mio file di origine è un TIFF ad alta risoluzione (300 dpi+)?

Una DPI più alta fornisce una migliore accuratezza OCR ma richiede più memoria. Se incontri un `MemoryError`, ridimensiona prima l'immagine:

```python
from PIL import Image
img = Image.open(image_path)
img = img.resize((int(img.width * 0.5), int(img.height * 0.5)), Image.ANTIALIAS)
img.save("temp.tif")
ocr_engine.load_image("temp.tif")
```

### 3️⃣ Come cambio la lingua dell'OCR?

Imposta la proprietà `language` sul motore prima di caricare l'immagine:

```python
ocr_engine.language = "fra"   # French
```

Un elenco completo dei codici lingua supportati è disponibile nella documentazione di Aspose.

### 4️⃣ Cosa fare se devo mantenere la qualità originale dell'immagine?

La classe `PdfSaveOptions` dispone di una proprietà `compression`. Impostala a `PdfCompression.None` per preservare i dati raster esattamente com'erano.

```python
pdf_save_options.compression = "None"
```

## Consigli per Distribuzioni Pronte alla Produzione

- **Elaborazione batch:** Avvolgi la logica principale in una funzione che accetta una lista di percorsi file. Registra ogni successo/fallimento in un CSV per tracciabilità.
- **Parallelismo:** Usa `concurrent.futures.ThreadPoolExecutor` per eseguire OCR su più core. Ricorda che ogni thread necessita della propria istanza `OcrEngine`.
- **Sicurezza:** Se gestisci documenti sensibili, esegui lo script in un ambiente sandbox e elimina immediatamente i file temporanei dopo l'elaborazione.

## Conclusione

Ora sai come **creare PDF ricercabili** da immagini scansionate usando uno script Python conciso. Inizializzando un motore OCR, caricando un TIFF (o qualsiasi raster), configurando `PdfSaveOptions` per **add OCR text layer**, e infine chiamando `recognize`, l'intera pipeline **convert scanned image pdf** e **convert TIFF to PDF** diventa un unico comando ripetibile.

Prossimi passi? Prova a concatenare questo script con un watcher di file in modo che ogni nuova scansione depositata in una cartella diventi automaticamente ricercabile. Oppure sperimenta con diverse lingue OCR per supportare archivi multilingue. Il cielo è il limite quando combini OCR e generazione PDF.

Hai altre domande su **how to run OCR** in altri linguaggi o framework? Lascia un commento qui sotto, e buona programmazione! 

![Diagram showing the flow from scanned image → OCR engine → searchable PDF (create searchable pdf)](searchable-pdf-flow.png "Create searchable pdf flow diagram")


## Cosa Dovresti Imparare Dopo?

- [Come fare OCR di PDF in .NET con Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Converti Immagini in PDF C# – Salva Risultato OCR Multi‑pagina](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Come fare OCR di Testo Immagine con Lingua usando Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}