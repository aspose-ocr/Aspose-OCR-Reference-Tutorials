---
category: general
date: 2026-06-06
description: Come fare OCR di PDF con Aspose OCR Cloud. Impara a estrarre il testo
  da PDF, convertire le pagine PDF in PNG e salvare le immagini delle pagine PDF in
  Python.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf page png
- extract plain text pdf
- save pdf page images
language: it
og_description: Come eseguire OCR su PDF con Aspose OCR Cloud. Questa guida mostra
  come estrarre il testo semplice da un PDF, convertire le pagine PDF in PNG e salvare
  le immagini delle pagine PDF.
og_title: Come fare OCR di PDF con Aspose OCR Cloud – Passo dopo passo
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Aspose OCR Cloud. Learn to extract text from PDF,
    convert PDF page PNG, and save PDF page images in Python.
  headline: How to OCR PDF with Aspose OCR Cloud – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Come eseguire l'OCR di PDF con Aspose OCR Cloud – Guida completa
url: /it/python-java/general/how-to-ocr-pdf-with-aspose-ocr-cloud-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come fare OCR su PDF con Aspose OCR Cloud – Guida completa

Ti sei mai chiesto **come fare OCR su PDF** senza lottare con strumenti desktop ingombranti? Non sei solo—molti sviluppatori si trovano di fronte a questo ostacolo quando hanno bisogno di un modo rapido e programmatico per estrarre il testo da documenti scansionati. La buona notizia? Con Aspose OCR Cloud puoi **estrarre testo da PDF**, trasformare ogni pagina in un PNG e persino **salvare le immagini delle pagine PDF** per un uso successivo, il tutto da un pulito script Python.

In questo tutorial percorreremo tutto ciò che devi sapere: dall'installazione dell'SDK, alla licenza del motore, al riconoscimento di PDF multi‑pagina, fino all'estrazione di testo semplice, alla conversione delle pagine in PNG e al salvataggio di queste immagini su disco. Alla fine avrai uno snippet riutilizzabile da inserire in qualsiasi progetto che necessiti di funzionalità **come fare OCR su PDF**.

## Cosa ti servirà

- **Python 3.8+** (il codice funziona anche su 3.10 e versioni successive)  
- Un account Aspose OCR Cloud – otterrai un file di licenza di prova gratuito (`Aspose.OCR.lic`)  
- Il pacchetto `asposeocrcloud` (`pip install asposeocrcloud`)  
- Un PDF scansionato, multi‑pagina che desideri elaborare  

È tutto. Nessun binario aggiuntivo, nessuna dipendenza nativa, solo puro Python.

## Come fare OCR su PDF – Configurazione e Licenza

Prima di poter chiamare qualsiasi metodo OCR, devi indicare all'SDK chi sei. Aspose utilizza un file di licenza leggero che devi posizionare in un luogo accessibile al tuo script.

```python
# Step 1: Import the OCR package and apply your license (optional but recommended)
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply the license – replace the path with your actual .lic file location
License().set_license("Aspose.OCR.lic")
```

*Consiglio:* Se salti il passaggio della licenza, l'SDK funzionerà comunque ma inserirà una piccola filigrana nelle immagini di output. Non è ideale per la produzione.

## Passo 2: Installa l'SDK Python di Aspose OCR Cloud

Apri un terminale ed esegui:

```bash
pip install asposeocrcloud
```

Il pacchetto scarica tutte le dipendenze necessarie (requests, pillow, ecc.) così non devi cercare nient'altro.

## Passo 3: Crea un motore OCR e scegli una lingua

Il motore è il cuore dell'operazione. Puoi specificare qualsiasi lingua supportata da Aspose; l'inglese funziona nella maggior parte dei casi.

```python
# Step 3: Create an OCR engine and set the recognition language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)
```

Perché impostare la lingua? Perché il motore OCR utilizza dizionari specifici per lingua per migliorare l'accuratezza. Se stai elaborando PDF in francese, basta sostituire `ENGLISH` con `FRENCH`.

## Passo 4: Indica il tuo PDF multi‑pagina

Fornisci al motore il percorso completo del file che desideri elaborare. I percorsi relativi vanno bene finché risolvono correttamente dalla directory di lavoro dello script.

```python
# Step 4: Specify the path to the multi‑page PDF you want to process
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"
```

Assicurati che il file sia leggibile; altrimenti vedrai un `FileNotFoundError`.

## Passo 5: Esegui OCR – Ottieni una lista di risultati

Chiamare `recognize_pdf` restituisce una lista in cui ogni elemento corrisponde a una pagina del PDF di origine.

```python
# Step 5: Run OCR on the PDF – a list of OcrResult objects is returned (one per page)
results = engine.recognize_pdf(pdf_path)
```

Ogni `OcrResult` contiene due utili proprietà:

* `text` – la rappresentazione in testo semplice della pagina (ottimo per **estrarre testo semplice da pdf**)  
* `image` – un oggetto `Image` di Pillow della pagina renderizzata (perfetto per **convertire pagina pdf in png**)  

## Passo 6: Estrarre testo da PDF e convertire le pagine in PNG

Ora iteriamo sui risultati, stampiamo il testo estratto e salviamo una versione PNG di ogni pagina.

```python
# Step 6: Iterate through each page, output the extracted text and optionally save the page image
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    # Extract plain text for this page
    print(res.text)                     # <-- this is the "extract plain text pdf" part
    # Convert the page to PNG and save it
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # <-- this does the "convert pdf page png"
```

### Output previsto nella console

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Troverai anche `page_1.png`, `page_2.png`, … nella cartella `YOUR_DIRECTORY`. Queste sono le immagini rasterizzate delle pagine che puoi inserire in pipeline di elaborazione immagini successive.

## Passo 7: Salva le immagini delle pagine PDF (Post‑processing opzionale)

Se ti servono solo le immagini e non il testo, puoi saltare la riga `print(res.text)`. Al contrario, se vuoi salvare il testo in file `.txt` separati, aggiungi una piccola scrittura:

```python
# Optional: Save each page's text to a .txt file
for i, res in enumerate(results, start=1):
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)
```

Questa piccola aggiunta dimostra quanto sia semplice **salvare le immagini delle pagine PDF** mantenendo anche il contenuto estratto.

## Esempio completo funzionante

Mettendo tutto insieme, ecco lo script completo che puoi copiare‑incollare in `ocr_pdf.py`:

```python
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply your license – optional but removes watermarks
License().set_license("Aspose.OCR.lic")

# Initialize the OCR engine and set language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)

# Path to the source PDF
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"

# Run OCR – get a list of results (one per page)
results = engine.recognize_pdf(pdf_path)

# Process each page
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(res.text)  # extract plain text PDF
    # Save the rendered page as PNG
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # convert PDF page PNG
    # Optional: also save the text to a .txt file
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)  # save PDF page images + text
```

Eseguilo con:

```bash
python ocr_pdf.py
```

Dovresti vedere nella console il dump del testo di ogni pagina e una serie di file PNG

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}