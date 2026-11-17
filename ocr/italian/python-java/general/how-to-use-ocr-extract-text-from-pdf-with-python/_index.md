---
category: general
date: 2026-04-26
description: come utilizzare l'OCR su PDF scansionati, estrarre il testo dal PDF,
  eseguire l'OCR sul PDF e convertire i PDF scansionati in file ricercabili in pochi
  passaggi
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: it
og_description: 'come usare OCR in Python: impara a estrarre testo da PDF, eseguire
  OCR su PDF e convertire PDF scansionati in documenti ricercabili.'
og_title: come usare l'OCR – Guida rapida per estrarre testo da PDF
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Come usare l'OCR – Estrarre il testo da PDF con Python
url: /it/python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# come usare OCR – Estrarre testo da PDF con Python

Ti sei mai chiesto **come usare OCR** per estrarre testo da un contratto, una ricevuta o un ebook scansionato? Non sei l'unico. In molti progetti reali il PDF che ricevi è solo un'immagine e, senza OCR, non puoi cercare, indicizzare o analizzare il suo contenuto.  

In questo tutorial percorreremo un esempio completo e funzionante che mostra **come usare OCR**, come **estrarre testo da PDF** e perché potresti voler **convertire PDF scansionati** in documenti ricercabili. Tratteremo anche l'arte sottile di **caricare PDF come immagine** affinché il motore OCR possa vedere ogni pagina chiaramente.

> **Anteprima rapida:** Alla fine avrai uno script che carica un PDF multipagina, esegue OCR su ogni pagina e stampa il testo riconosciuto – senza servizi esterni.

## Cosa ti servirà

- Python 3.9+ (qualsiasi versione recente va bene)
- pacchetto `aocr` (o qualsiasi libreria OCR compatibile che fornisca `OcrEngine` e `Image.load`)
- Un file PDF scansionato da elaborare (ad es., `contract.pdf`)
- Una quantità modesta di RAM (≈ 200 MB per PDF di 100 pagine è solitamente sufficiente)

Se non hai ancora installato la libreria OCR, esegui:

```bash
pip install aocr
```

> **Consiglio professionale:** Usa un ambiente virtuale per mantenere ordinate le dipendenze.

## Passo 1: Caricare PDF come immagine – Il primo pezzo del puzzle

Prima che possa avvenire qualsiasi OCR, il PDF deve essere rappresentato come immagine. È qui che entra in gioco la keyword secondaria **load pdf as image**.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*Perché è importante:* `aocr.Image.load` rasterizza internamente ogni pagina del PDF in una bitmap che il motore OCR può comprendere. Se salti questo passaggio e fornisci il PDF grezzo, il motore solleverà un errore perché si aspetta dati pixel, non dati vettoriali.

> **Nota:** Il percorso può essere assoluto o relativo. Assicurati che il file sia leggibile; altrimenti otterrai un `FileNotFoundError`.

## Passo 2: Eseguire OCR su PDF – Trasformare i pixel in caratteri

Ora che il PDF è un'immagine, possiamo finalmente **run OCR on PDF**. Il frammento seguente elabora tutte le pagine in un unico passaggio:

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*Cosa succede dietro le quinte?* `process_all_pages` scorre le pagine rasterizzate, applica il modello OCR e restituisce una lista di oggetti risultato—uno per pagina. Ogni risultato contiene il testo riconosciuto, i punteggi di confidenza e le bounding box (se ti servono in seguito).

## Passo 3: Estrarre testo da PDF – Estrarre le stringhe

Con i risultati OCR a disposizione, estrarre il testo semplice diventa banale. Itereremo sulle pagine e stamperemo l'output, dimostrando la keyword secondaria **extract text from pdf**.

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**Output atteso** (troncato per brevità):

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

Se ti serve il testo in un'unica stringa, basta concatenare:

```python
full_text = "\n".join(r.text for r in page_results)
```

Ora hai **estratto testo da PDF** usando OCR.

## Passo 4: Convertire PDF scansionato – Renderlo ricercabile

Molti strumenti a valle (come Elasticsearch o SharePoint) si aspettano un PDF ricercabile anziché un dump di testo semplice. Puoi incorporare l'output OCR nel PDF originale, **convertendo PDF scansionati** in una versione ricercabile.

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*Perché farlo?* Un PDF ricercabile mantiene il layout e le immagini originali consentendo al contempo la selezione e l'indicizzazione del testo — una vittoria sia per gli esseri umani che per le macchine.

## Problemi comuni & casi limite

### PDF multipagina più grandi della memoria

Se il tuo PDF ha centinaia di pagine, caricare tutto in una volta può esaurire la RAM. La libreria `aocr` supporta il caricamento pigro:

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

Poi elabora le pagine una alla volta:

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### Scansioni di bassa qualità

La precisione OCR cala drasticamente su scansioni sfocate o a basso contrasto. Prima di passare l'immagine al motore, considera una pre‑elaborazione:

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### Supporto linguistico

Di default il motore assume l'inglese. Per **run OCR on PDF** in un'altra lingua, imposta il codice lingua:

```python
ocr_engine.language = "spa"  # Spanish
```

Assicurati che il modello linguistico corrispondente sia installato.

## Esempio completo funzionante

Riunendo tutto, ecco uno script autonomo che puoi salvare in un file chiamato `ocr_pdf.py` ed eseguire subito:

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

Eseguilo così:

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

Vedrai il testo stampato sulla console e, se hai fornito `-o`, apparirà un PDF ricercabile accanto al file originale.

## Consigli professionali & migliori pratiche

- **Elaborazione batch:** Quando gestisci decine di PDF, avvolgi la logica sopra in un ciclo e registra il successo/fallimento di ogni file.
- **Filtraggio per confidenza:** Ogni `page_result` include una metrica di confidenza. Scarta o segnala le pagine con bassa confidenza per una revisione manuale.
- **Parallelismo:** Se la tua CPU ha più core, considera l'uso di `concurrent.futures` per elaborare le pagine in parallelo — facendo attenzione all'uso della memoria.
- **Blocco di versione:** L'API `aocr` può evolvere. Blocca la versione in `requirements.txt` (es., `aocr==2.3.1`) per evitare cambiamenti incompatibili.

## Conclusione

Abbiamo percorso **come usare OCR** per **estrarre testo da PDF**, **run OCR on PDF**, **load PDF as image**, e persino **convertire PDF scansionati** in un formato ricercabile. Il codice è completo, le spiegazioni coprono sia il *cosa* sia il *perché*, e ora disponi di un pattern riutilizzabile per qualsiasi progetto che tratti PDF basati su immagine.

Qual è il prossimo passo? Prova a inviare il testo estratto in una pipeline di linguaggio naturale, indicizza i PDF ricercabili con Elasticsearch, o sperimenta con diversi back‑end OCR come Tesseract o Azure Computer Vision. Il cielo è il limite, e gli strumenti sono a portata di mano.

Buon coding, e che i tuoi PDF siano sempre ricercabili! 

![come usare OCR esempio](/images/ocr_workflow.png "come usare OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}