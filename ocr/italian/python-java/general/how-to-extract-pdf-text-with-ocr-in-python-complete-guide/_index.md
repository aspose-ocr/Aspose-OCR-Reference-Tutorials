---
category: general
date: 2026-06-19
description: Come estrarre PDF usando OCR in Python – tutorial passo‑passo che copre
  l'estrazione del testo da PDF, il riconoscimento del testo da immagine e un esempio
  di OCR in Python.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize text from image
- ocr python example
- read pdf with ocr
language: it
og_description: Come estrarre PDF usando OCR in Python. Impara a estrarre testo da
  PDF, riconoscere il testo da un'immagine e vedere un esempio completo di OCR in
  Python.
og_title: Come estrarre il testo PDF con OCR in Python – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  headline: How to Extract PDF Text with OCR in Python – Complete Guide
  type: TechArticle
- description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  name: How to Extract PDF Text with OCR in Python – Complete Guide
  steps:
  - name: – Install the Required Packages
    text: First, we need an OCR engine. The example below uses the popular **ocr**
      package (a thin wrapper around Tesseract). If you prefer a different backend,
      the concepts stay the same.
  - name: – Initialize the OCR Engine and Set Language
    text: Now we spin up the engine and tell it to look for English characters. You
      can swap `ocr.Language.English` for any supported language code.
  - name: – Load a PDF Page as an Image
    text: OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper
      renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based
      indexing).
  - name: – Recognize Text from the Rendered Image
    text: Here’s the heart of the **ocr python example**. The engine processes the
      bitmap and returns an object containing the extracted string.
  - name: – Print or Store the Extracted Text
    text: Finally, we output the result. In a real application you’d probably write
      to a file or a database.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Come estrarre il testo PDF con OCR in Python – Guida completa
url: /it/python-java/general/how-to-extract-pdf-text-with-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come estrarre testo PDF con OCR in Python – Guida completa

Ti sei mai chiesto **come estrarre PDF** quando il file è solo un'immagine scansionata? Non sei l'unico. In molti progetti reali—pensate a contratti, fatture o archivi storici—il PDF che ricevi non contiene testo selezionabile. La buona notizia? Poche righe di Python possono trasformare quelle pagine solo immagine in testo ricercabile e modificabile.

In questo tutorial percorreremo un **esempio OCR Python** pratico che legge un PDF, rende la sua prima pagina come immagine e poi **estrae testo dal PDF** usando un motore OCR. Alla fine saprai esattamente **come leggere PDF con OCR**, perché ogni passaggio è importante e come adattare il codice per documenti multi‑pagina o lingue diverse.

## Cosa imparerai

- Installa e configura una libreria OCR affidabile per Python.  
- Converti le pagine PDF in immagini adatte all'OCR.  
- **Riconosci il testo da un'immagine** e recupera stringhe Unicode pulite.  
- Problemi comuni (PDF a bassa risoluzione, pagine ruotate) e come evitarli.  
- Estendere lo script per gestire più pagine o l'elaborazione batch.

**Prerequisiti**: Python 3.8+, pip e una conoscenza di base degli ambienti virtuali. Nessuna esperienza pregressa con OCR richiesta—basta seguire.

---

## ## Come estrarre testo PDF con OCR in Python

Questo header H2 contiene la nostra parola chiave principale proprio dove i motori di ricerca amano vederla. Immergiamoci subito nel codice.

### Step 1 – Install the Required Packages

Prima di tutto, ci serve un motore OCR. L'esempio qui sotto utilizza il popolare pacchetto **ocr** (un thin wrapper attorno a Tesseract). Se preferisci un backend diverso, i concetti rimangono gli stessi.

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR wrapper and Pillow for image handling
pip install ocr pillow
```

> **Pro tip:** Su Linux, avrai anche bisogno del binario Tesseract: `sudo apt-get install tesseract-ocr`. Gli utenti macOS possono ottenerlo tramite Homebrew: `brew install tesseract`.

### Step 2 – Initialize the OCR Engine and Set Language

Ora avviamo il motore e gli diciamo di cercare caratteri inglesi. Puoi sostituire `ocr.Language.English` con qualsiasi codice lingua supportato.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
```

**Perché è importante:** Specificare la lingua migliora drasticamente l'accuratezza perché il motore può applicare dizionari e modelli di caratteri specifici per la lingua.

### Step 3 – Load a PDF Page as an Image

L'OCR funziona su immagini raster, non su oggetti PDF. L'helper `ocr.Image.from_pdf` rende la pagina scelta in una bitmap. Regola `page_number` per altre pagine (indice a partire da 0).

```python
# Step 2: Load the first page of the PDF as an image
pdf_file_path = "YOUR_DIRECTORY/contract.pdf"
page_image = ocr.Image.from_pdf(pdf_file_path, page_number=1)
```

> **Edge case:** Se il PDF contiene grafica vettoriale anziché immagini scansionate, potresti ottenere un rendering nitido. Per scansioni a bassa risoluzione, considera di aumentare il DPI: `ocr.Image.from_pdf(..., dpi=300)`.

### Step 4 – Recognize Text from the Rendered Image

Ecco il cuore del **ocr python example**. Il motore elabora la bitmap e restituisce un oggetto contenente la stringa estratta.

```python
# Step 3: Recognize text from the rendered page image
ocr_result = ocr_engine.recognize(page_image)
```

L'attributo `ocr_result.text` contiene l'output in plain‑text, preservando i ritorni a capo dove possibile.

### Step 5 – Print or Store the Extracted Text

Infine, mostriamo il risultato. In un'applicazione reale probabilmente scriveresti su un file o su un database.

```python
# Step 4: Print the extracted text
print(ocr_result.text)
```

Eseguendo lo script dovrebbe comparire qualcosa del genere:

```
THIS AGREEMENT is made on the 1st day of January 2024...
```

Questo è un flusso di lavoro completo **estrarre testo da pdf** usando OCR.

---

## ## Riconosci testo da immagine – Ottimizzare l'accuratezza

Se ti interessa solo **riconoscere testo da immagine** (ad esempio un JPEG di una ricevuta), puoi saltare il passaggio di conversione PDF:

```python
image_path = "receipt.jpg"
page_image = ocr.Image.from_file(image_path)   # Directly load an image
ocr_result = ocr_engine.recognize(page_image)
print(ocr_result.text)
```

**Suggerimenti per risultati migliori:**

- **Pre‑processa** l'immagine: converti in scala di grigi, applica sogliatura o correggi l'inclinazione. Pillow lo rende facile.
- **Aumenta DPI** durante il rendering del PDF: una risoluzione più alta fornisce più dettagli al motore OCR.
- **Abilita la configurazione del motore OCR** per la segmentazione delle pagine (`ocr_engine.config = "--psm 6"` per blocchi uniformi).

---

## ## Leggi PDF con OCR – Gestire più pagine

La maggior parte dei contratti si estende su più pagine. Iterare su ciascuna pagina è semplice:

```python
def extract_all_pages(pdf_path):
    all_text = []
    for i in range(ocr.Image.pdf_page_count(pdf_path)):
        img = ocr.Image.from_pdf(pdf_path, page_number=i)
        result = ocr_engine.recognize(img)
        all_text.append(result.text)
    return "\n--- PAGE BREAK ---\n".join(all_text)

full_text = extract_all_pages("YOUR_DIRECTORY/contract.pdf")
print(full_text)
```

Questa funzione **legge PDF con OCR**, concatena l'output e inserisce un chiaro marcatore di interruzione di pagina. Puoi quindi alimentare `full_text` in un indice di ricerca o salvarlo come file `.txt`.

---

## ## Problemi comuni e come risolverli

| Sintomo | Probabile causa | Soluzione |
|---------|-----------------|-----------|
| Caratteri confusi, molti `?` | Lingua errata o file di dati della lingua mancanti | Installa il pacchetto lingua Tesseract corretto (`tesseract-ocr-<lang>`) e imposta `ocr_engine.language`. |
| Linee mancanti o parole troncate | Bassa DPI (meno di 150) | Renderizza il PDF a 300 DPI o superiore (`dpi=300`). |
| Il testo è ruotato o capovolto | Pagina scansionata non orientata correttamente | Usa `ocr.Image.deskew(page_image)` prima del riconoscimento. |
| Elaborazione lenta su PDF grandi | Elaborazione delle pagine sequenzialmente su un singolo thread | Parallelizza con `concurrent.futures.ThreadPoolExecutor`. |

---

## ## Estendere l'esempio OCR Python

- **Esporta in PDF/A**: Dopo l'estrazione, puoi incorporare il testo in un PDF ricercabile usando `reportlab` o `pypdf2`.
- **Rilevamento della lingua**: Usa `langdetect` sull'output OCR per cambiare dinamicamente `ocr_engine.language`.
- **Elaborazione batch**: Scorri una directory con `os.listdir` e applica `extract_all_pages` a ogni file.

---

## ## Output atteso e verifica

Quando esegui lo script su una scansione chiara in lingua inglese, dovresti vedere un blocco di testo pulito con punteggiatura corretta. Verifica tramite:

1. Confrontare alcune righe con l'immagine scansionata originale.  
2. Eseguire un semplice conteggio parole (`len(ocr_result.text.split())`) per assicurarsi che l'output non sia vuoto.  
3. Facoltativamente, passare il risultato a un correttore ortografico come `pyspellchecker` per individuare errori OCR.

---

## Conclusione

Abbiamo coperto **come estrarre PDF** quando il parsing tradizionale fallisce, mostrato un **esempio OCR python** completo e spiegato come **riconoscere testo da immagine** e **leggere PDF con OCR** per scenari sia a pagina singola che multi‑pagina. Con gli snippet di codice sopra puoi ora trasformare qualsiasi PDF scansionato in testo ricercabile e modificabile—niente più digitazione manuale.

Prossimi passi? Prova a cambiare la lingua in spagnolo (`ocr.Language.Spanish`) o sperimenta tecniche di pre‑processamento dell'immagine per aumentare l'accuratezza. Se stai costruendo un sistema di gestione documentale, considera di indicizzare il testo estratto con Elasticsearch per ricerche ultra‑veloci.

Hai domande o ti imbatti in un PDF strano? Lascia un commento, e buon coding!  

![Come estrarre PDF usando OCR in Python](image.png "Come estrarre PDF usando OCR in Python")

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrai testo da immagine con Aspose OCR – Guida passo‑passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Riconosci testo PDF – Operazioni OCR con Aspose.OCR per Java](/ocr/english/java/ocr-operations/)
- [Estrai testo da immagine C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}