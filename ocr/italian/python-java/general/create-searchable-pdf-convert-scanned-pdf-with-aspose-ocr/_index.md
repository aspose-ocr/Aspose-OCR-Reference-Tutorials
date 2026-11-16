---
category: general
date: 2026-03-18
description: Crea PDF ricercabili dai tuoi file scansionati con Aspose OCR. Scopri
  come convertire PDF scansionati, estrarre testo da PDF e riconoscere rapidamente
  il testo nei PDF.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- extract text from pdf
- recognize text pdf
- convert image pdf
language: it
og_description: Crea PDF ricercabili istantaneamente. Segui questa guida per convertire
  PDF scansionati, estrarre testo da PDF e riconoscere il testo nei PDF usando Aspose
  OCR.
og_title: Crea PDF ricercabile – Passo dopo passo con Aspose OCR
tags:
- OCR
- PDF
- Aspose
- Python
title: Crea PDF ricercabile – Converti PDF scansionato con Aspose OCR
url: /it/python-java/general/create-searchable-pdf-convert-scanned-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea PDF Ricercabile – Guida Passo‑Passo  

Ti è mai capitato di dover **create searchable PDF** da una pila di pagine scansionate ma non sapevi da dove cominciare? Non sei solo—la maggior parte degli sviluppatori si imbatte in questo ostacolo quando la prima scansione arriva sul loro server.  

La buona notizia è che con Aspose OCR puoi **convert scanned pdf** in poche righe di codice, **extract text from pdf** per la validazione, e persino **recognize text pdf** al volo. In questo tutorial percorreremo l'intero processo, dall'installazione della libreria al salvataggio di un documento completamente ricercabile, e inseriremo alcuni consigli per gestire i casi limite di **convert image pdf**.

## Cosa Riuscirai a Ottenere  

* Carica un PDF scansionato (o un PDF solo‑immagine) in Aspose OCR.  
* Indica al motore quali pagine elaborare – utile quando ti serve solo un sottoinsieme.  
* Incorpora i risultati OCR nel file originale in modo che l'output sia un vero **searchable PDF**.  
* Verifica l'operazione stampando il conteggio delle pagine e, se lo desideri, esportando il testo estratto.  

Nessun servizio esterno, nessuna magia nascosta—solo puro Python e l'API di Aspose.

## Prerequisiti  

* Python 3.8 o versioni successive.  
* Pacchetto `aspose-ocr` – installalo con `pip install aspose-ocr`.  
* Un file PDF scansionato (o un PDF che contiene solo immagini).  
* Familiarità di base con lo scripting Python.  

Se li hai già, ottimo—tuffiamoci.

<img src="searchable-pdf-workflow.png" alt="Crea flusso di lavoro PDF ricercabile">  

*(Illustrazione della pipeline OCR – non necessaria per il codice ma utile per gli apprendenti visivi.)*

## Passo 1 – Inizializza il Motore OCR  

Prima di tutto: ti serve un'istanza di `OcrEngine`. Pensala come il cervello che leggerà ogni pixel e lo convertirà in caratteri Unicode.

```python
# Step 1: Import the required classes and create the engine
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

# Initialize the OCR engine – this object holds all settings
ocr_engine = OcrEngine()
```

**Perché è importante:** Senza il motore non puoi impostare opzioni o eseguire il riconoscimento. Inizializzarlo subito ti fornisce anche un punto dove allegare eventuali dizionari personalizzati in seguito.

## Passo 2 – Carica il PDF di Origine  

Aspose OCR può leggere i PDF direttamente, il che significa che non devi rasterizzare ogni pagina manualmente. Basta puntare il motore al file.

```python
# Step 2: Load the scanned PDF (replace with your actual path)
input_path = "YOUR_DIRECTORY/input.pdf"
ocr_engine.setImageFromFile(input_path)
```

*Consiglio:* Se il PDF è enorme, considera di caricarlo da uno stream per evitare di bloccare il file su disco.

## Passo 3 – Configura le Opzioni di Riconoscimento PDF  

Ecco dove le parole chiave secondarie iniziano a brillare. Puoi dire al motore di **convert scanned pdf** solo su determinate pagine, incorporare il testo riconosciuto, o persino mantenere intatte le immagini originali.

```python
# Step 3: Create and configure PDF recognition options
pdf_options = PdfRecognitionOptions()
pdf_options.setEmbedRecognisedText(True)          # Makes the PDF searchable
pdf_options.setPageRange(1, 3)                    # Process only pages 1‑3 (optional)
pdf_options.setTextExtractionMode(True)          # Enables text extraction for verification
```

**Perché è importante:**  
* `setEmbedRecognisedText(True)` è la chiave per trasformare un PDF raster in un **searchable PDF**.  
* `setPageRange` ti aiuta a **convert image pdf** in modo selettivo—utile per documenti grandi dove ti servono OCR solo su poche pagine.  
* Abilitare l'estrazione del testo ti permette in seguito di **extract text from pdf** senza aprire un visualizzatore.

## Passo 4 – Allega le Opzioni al Motore  

Ora collega le opzioni al motore. Questo passaggio è facile da trascurare, ma saltarlo significa che il motore funziona con le impostazioni predefinite (nessun testo ricercabile).

```python
# Step 4: Attach the options to the OCR engine
ocr_engine.setPdfRecognitionOptions(pdf_options)
```

## Passo 5 – Esegui l'OCR sulle Pagine Selezionate  

Con tutto collegato, il riconoscimento vero e proprio è una singola chiamata di metodo.

```python
# Step 5: Perform OCR – this may take a few seconds per page
ocr_result = ocr_engine.recognize()
```

Se stai elaborando un documento multi‑megabyte, potresti voler avvolgere questo in un blocco try/except per catturare `OcrException` e registrare la pagina problematica.

## Passo 6 – Verifica il Risultato  

Un rapido controllo di coerenza è stampare quante pagine il motore pensa di aver elaborato. Puoi anche estrarre il testo grezzo se hai bisogno di **extract text from pdf** per un'analisi più approfondita.

```python
# Step 6: Show how many pages were processed
print("Pages processed:", ocr_result.getPageCount())

# Optional: dump extracted text for the first page (helps debugging)
first_page_text = ocr_result.getPageText(0)   # 0‑based index
print("\n--- Extracted Text (Page 1) ---\n", first_page_text[:500])  # show first 500 chars
```

**Perché ti interessa:** Vedere il conteggio delle pagine conferma che `setPageRange` ha funzionato, e lo snippet di testo estratto dimostra che l'OCR ha effettivamente riconosciuto i caratteri.

## Passo 7 – Salva il PDF Ricercabile  

Infine, scrivi l'output su disco. La costante `ImageFormats.PDF` indica ad Aspose di mantenere il file come PDF, ora arricchito con testo ricercabile.

```python
# Step 7: Save the searchable PDF
output_path = "YOUR_DIRECTORY/output.pdf"
ocr_engine.save(output_path, ImageFormats.PDF)

print(f"Searchable PDF saved to: {output_path}")
```

Apri il file risultante in qualsiasi lettore PDF e prova una ricerca di testo—voilà, hai **created searchable pdf**!

## Gestione dei Casi Limite Comuni  

### Quando la sorgente è un PDF *solo‑immagine*  

Se il tuo PDF di input contiene solo immagini (nessun livello di testo), lo stesso codice funziona—basta assicurarsi che `setEmbedRecognisedText(True)` rimanga abilitato. Potresti anche voler aumentare il DPI per una maggiore precisione:

```python
pdf_options.setResolution(300)  # 300 DPI gives sharper OCR results
```

### Gestione di più Lingue  

Aspose OCR supporta i pacchetti lingua. Carica una lingua prima di chiamare `recognize()`:

```python
ocr_engine.setLanguage("spa")   # Spanish language pack
```

### Documenti di grandi dimensioni  

Elaborare un PDF scansionato di 500 pagine può richiedere molta memoria. Dividi il lavoro:

1. Itera sui range di pagine (`setPageRange(start, end)`).  
2. Salva ogni blocco come un PDF ricercabile temporaneo.  
3. Unisci i blocchi con `PdfMerger` (un altro componente Aspose).

## Esempio Completo Funzionante (Tutti i Passi Insieme)

```python
# Full script – create searchable PDF from a scanned document
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

def create_searchable_pdf(input_file: str, output_file: str, start_page: int = 1, end_page: int = 0):
    """
    Convert a scanned or image‑only PDF into a searchable PDF.
    :param input_file: Path to the source PDF.
    :param output_file: Destination path for the searchable PDF.
    :param start_page: First page to process (1‑based). Default = 1.
    :param end_page: Last page to process. 0 means “till the end”.
    """
    # Initialize engine
    ocr_engine = OcrEngine()
    ocr_engine.setImageFromFile(input_file)

    # Set options
    pdf_opts = PdfRecognitionOptions()
    pdf_opts.setEmbedRecognisedText(True)          # embed searchable text
    pdf_opts.setTextExtractionMode(True)           # allow text extraction
    if end_page > 0:
        pdf_opts.setPageRange(start_page, end_page)  # selective processing
    else:
        pdf_opts.setPageRange(start_page, start_page)  # process from start_page onward

    # Attach options
    ocr_engine.setPdfRecognitionOptions(pdf_opts)

    # Run OCR
    result = ocr_engine.recognize()
    print("Pages processed:", result.getPageCount())

    # Optional verification
    print("\nSample extracted text (first page):")
    print(result.getPageText(0)[:300])

    # Save searchable PDF
    ocr_engine.save(output_file, ImageFormats.PDF)
    print(f"Searchable PDF saved to: {output_file}")

if __name__ == "__main__":
    create_searchable_pdf(
        input_file="YOUR_DIRECTORY/input.pdf",
        output_file="YOUR_DIRECTORY/output.pdf",
        start_page=1,
        end_page=3   # change or set to 0 to process the whole file
    )
```

Eseguendo questo script otterrai un **searchable PDF** che potrai aprire in Adobe Reader, Chrome o qualsiasi lettore PDF e cercare istantaneamente parole.

## Conclusione  

Ora hai una soluzione completa, end‑to‑end, per **create searchable PDF** usando Aspose OCR. Dal caricamento della sorgente, configurazione delle opzioni che **convert scanned pdf**, estrazione e verifica del testo, fino al salvataggio finale del risultato ricercabile, ogni passaggio è coperto.  

Successivamente, potresti voler esplorare gli scenari di **convert image pdf** dove la sorgente è una serie di JPEG inseriti in un PDF, o approfondire l'OCR specifico per lingua per migliorare la precisione nei documenti multilingue. In ogni caso, il modello rimane lo stesso: imposta le opzioni, esegui `recognize()`, e salva.  

Sentiti libero di sperimentare—cambia il range di pagine, modifica il DPI, o inserisci un dizionario personalizzato. Se incontri problemi, lascia un commento qui sotto o consulta la documentazione ufficiale di Aspose per le ultime novità dell'API. Buon OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}