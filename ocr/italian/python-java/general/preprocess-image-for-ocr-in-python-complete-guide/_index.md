---
category: general
date: 2026-06-25
description: Preprocessa l'immagine per OCR e riconosci il testo da un documento scansionato
  usando Python. Tutorial passo‑passo con codice completo.
draft: false
keywords:
- preprocess image for OCR
- recognize text from scanned document
- Python OCR tutorial
- image deskewing Python
- OCR preprocessing tips
language: it
og_description: Preprocessa l'immagine per l'OCR e riconosci il testo da un documento
  scansionato con Python. Segui questo tutorial dettagliato e eseguibile.
og_title: Preelaborazione dell'immagine per OCR in Python – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  headline: Preprocess Image for OCR in Python – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  name: Preprocess Image for OCR in Python – Complete Guide
  steps:
  - name: Create an OCR Engine Instance
    text: '```python import ocr # <-- make sure the OCR library is installed'
  - name: Enable Automatic Deskewing and Binarization
    text: '```python # Step 2: Enable automatic deskewing and binarization to improve
      recognition engine.image_preprocessing = ocr.ImagePreProcessingOptions( auto_deskew=True,
      auto_binarize=True ) ```'
  - name: Load the Skewed Image You Want to Process
    text: '```python # Step 3: Load the skewed image you want to process image_path
      = "YOUR_DIRECTORY/skewed_document.jpg" image = ocr.Image.load(image_path) ```'
  - name: Perform OCR on the Pre‑processed Image
    text: '```python # Step 4: Perform OCR on the pre‑processed image result = engine.recognize(image)
      ```'
  - name: Output the Recognized Text
    text: '```python # Step 5: Output the recognized text print("Deskewed & binarized
      text:", result.text) ```'
  - name: 1. Handling Multiple Languages
    text: 'If your document contains both English and French, configure the engine
      before step 1:'
  - name: 2. Fine‑Tuning Binarization Thresholds
    text: 'Automatic binarization works for most cases, but some old photocopies need
      a custom threshold:'
  - name: 3. Extracting Layout Information
    text: 'Sometimes you need more than raw text—you want to know where each paragraph
      lives on the page. Many engines expose a `result.blocks` collection:'
  - name: 4. Processing a Batch of Files
    text: 'If you have a folder full of scanned PDFs converted to JPEGs, wrap the
      whole flow in a loop:'
  - name: 5. Dealing with Low‑Resolution Scans
    text: 'Low‑resolution images (< 150 dpi) often produce fuzzy characters. A quick
      remedy is to upscale using a high‑quality algorithm before feeding the image
      to the OCR engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Preelaborazione dell'immagine per OCR in Python – Guida completa
url: /it/python-java/general/preprocess-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Preprocessare le Immagini per OCR in Python – Guida Completa

Ti sei mai chiesto come **preprocessare un'immagine per OCR** in modo che il testo risulti pulito e affidabile? Non sei solo: la maggior parte degli sviluppatori si imbatte nello stesso problema quando la pagina scansionata è inclinata o il contrasto è irregolare. La buona notizia è che poche righe di Python possono raddrizzare il caos, binarizzare l'immagine e restituirti testo nitido e ricercabile.

In questo tutorial percorreremo passo passo le fasi per **preprocessare un'immagine per OCR** *e* **riconoscere il testo da documenti scansionati**, usando una popolare libreria OCR. Alla fine avrai uno script pronto all'uso, comprenderai perché ogni impostazione è importante e saprai come modificarla per i casi più difficili.

## Cosa Ti Serve

- Python 3.8 o superiore (il codice funziona anche su 3.10+)
- Un pacchetto OCR che espone le classi `OcrEngine`, `ImagePreProcessingOptions` e `Image` (ad esempio il fittizio modulo `ocr` usato nell'esempio)
- Un documento scansionato o fotografato che sia leggermente inclinato o a basso contrasto
- Il tuo IDE preferito o un semplice terminale—non è necessario alcun GUI pesante

Tutto qui. Nessun binario extra, nessun Docker. Immergiamoci.

## Preprocessare l'Immagine per OCR – Passo‑per‑Passo

Di seguito il flusso di lavoro principale suddiviso in cinque fasi chiare. Ogni fase include **il perché** la eseguiamo, il **codice** esatto e una breve **spiegazione** di cosa succede dietro le quinte.

### Passo 1: Creare un'Istanza di OCR Engine

```python
import ocr  # <-- make sure the OCR library is installed

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Perché è importante:*  
L'oggetto `OcrEngine` è il cervello dell'operazione. Contiene configurazioni come i pacchetti lingua, le soglie di confidenza e—soprattutto per noi—i flag di preprocessamento immagine. Istanziarlo per primo ci dà una base pulita su cui abilitare i trucchi successivi.

### Passo 2: Abilitare la Correzione Automatica dell'Inclinazione e la Binarizzazione

```python
# Step 2: Enable automatic deskewing and binarization to improve recognition
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
```

*Perché è importante:*  
- **Deskewing** ruota l'immagine affinché le linee di testo diventino orizzontali. I motori OCR faticano quando la linea di base è inclinata di più di qualche grado.  
- **Binarizzazione** converte l'immagine in puro bianco‑nero, eliminando il rumore di sfondo che può confondere i classificatori di caratteri.  
Entrambe le opzioni sono *automatiche* in molte librerie moderne, ma è comunque necessario attivarle—da qui l'assegnazione esplicita.

> **Consiglio:** Se le tue immagini di origine sono già perfettamente allineate, puoi impostare `auto_deskew=False` per risparmiare un millisecondo di tempo di elaborazione.

### Passo 3: Caricare l'Immagine Inclinata da Processare

```python
# Step 3: Load the skewed image you want to process
image_path = "YOUR_DIRECTORY/skewed_document.jpg"
image = ocr.Image.load(image_path)
```

*Perché è importante:*  
Il metodo `Image.load` legge il file in memoria e lo avvolge in un oggetto comprensibile al motore OCR. Estrae anche metadati come DPI, che possono influenzare il fattore di scala predefinito per la correzione dell'inclinazione.

> **Caso limite:** Se l'immagine è un TIFF multi‑pagina, dovrai iterare su ogni pagina o usare un helper come `ocr.MultiPageImage.load`. Le stesse impostazioni di preprocessamento si applicano a ogni pagina.

### Passo 4: Eseguire l'OCR sull'Immagine Pre‑processata

```python
# Step 4: Perform OCR on the pre‑processed image
result = engine.recognize(image)
```

*Perché è importante:*  
A questo punto il motore applica le fasi di correzione dell'inclinazione e binarizzazione che abbiamo abilitato prima, quindi esegue la sua rete neurale (o la classica pipeline in stile Tesseract) sul bitmap pulito. L'oggetto `result` restituito contiene tipicamente il testo puro, i punteggi di confidenza e talvolta dati posizionali per ogni parola.

> **E se il testo è ancora illeggibile?**  
Controlla la risoluzione dell'immagine: l'OCR funziona al meglio a 300 dpi o più. Se la tua fonte è inferiore, considera di ingrandire l'immagine prima del caricamento, o richiedi la scansione originale alla fonte del documento.

### Passo 5: Restituire il Testo Riconosciuto

```python
# Step 5: Output the recognized text
print("Deskewed & binarized text:", result.text)
```

*Perché è importante:*  
`result.text` è una stringa semplice che rappresenta tutto ciò che il motore è riuscito a leggere. Stampare il risultato è comodo per un rapido debug; in un'app reale probabilmente lo scriveresti in un file `.txt`, in un database, o lo passeresti a una pipeline NLP successiva.

---

## Riconoscere il Testo da Documenti Scansionati – Oltre le Basi

Ora che la pipeline base funziona, esploriamo alcune variazioni comuni che potresti incontrare quando provi a **riconoscere il testo da documenti scansionati** in situazioni reali.

### 1. Gestire più Lingue

Se il tuo documento contiene sia inglese che francese, configura il motore prima del passo 1:

```python
engine = ocr.OcrEngine(languages=["eng", "fra"])
```

La maggior parte dei motori OCR accetta codici ISO‑639‑2; caricare pacchetti lingua aggiuntivi aggiunge un piccolo overhead ma migliora notevolmente l'accuratezza su pagine multilingue.

### 2. Regolare Manualmente le Soglie di Binarizzazione

La binarizzazione automatica funziona nella maggior parte dei casi, ma alcune vecchie fotocopie richiedono una soglia personalizzata:

```python
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=False,          # turn off auto
    binarization_threshold=180   # manual threshold (0‑255)
)
```

Sperimenta valori tra 120 e 220 finché lo sfondo scompare senza cancellare i caratteri più deboli.

### 3. Estrarre Informazioni di Layout

A volte ti serve più del semplice testo—vuoi sapere dove si trova ogni paragrafo nella pagina. Molti motori espongono una collezione `result.blocks`:

```python
for block in result.blocks:
    print(f"Block at ({block.x}, {block.y}) size {block.width}x{block.height}")
    print(block.text)
```

Questo è prezioso per ricostruire tabelle o preservare l'ordine delle colonne.

### 4. Processare un Lotto di File

Se hai una cartella piena di PDF scansionati convertiti in JPEG, avvolgi l'intero flusso in un ciclo:

```python
import pathlib

folder = pathlib.Path("YOUR_DIRECTORY")
for img_file in folder.glob("*.jpg"):
    img = ocr.Image.load(str(img_file))
    txt = engine.recognize(img).text
    (folder / f"{img_file.stem}.txt").write_text(txt, encoding="utf-8")
    print(f"Processed {img_file.name}")
```

Il ciclo riutilizza la stessa istanza `engine`, il che è più efficiente rispetto a ricrearla per ogni file.

### 5. Gestire Scansioni a Bassa Risoluzione

Immagini a bassa risoluzione (< 150 dpi) spesso producono caratteri sfocati. Un rimedio rapido è ingrandire usando un algoritmo di alta qualità prima di passare l'immagine al motore OCR:

```python
from PIL import Image as PilImage

pil_img = PilImage.open("low_res.jpg")
upscaled = pil_img.resize((pil_img.width * 2, pil_img.height * 2), PilImage.LANCZOS)
upscaled.save("upscaled.jpg")
image = ocr.Image.load("upscaled.jpg")
```

L'upscaling non crea magicamente dettagli, ma la fase di binarizzazione può lavorare con bordi più nitidi, offrendo un modesto miglioramento.

---

## Output Atteso

Eseguendo lo script a cinque passaggi su una scansione moderatamente inclinata a 300 dpi dovrebbe stampare qualcosa di simile a:

```
Deskewed & binarized text: 
Dear Customer,

Thank you for your recent purchase. Please find your receipt attached.

Best regards,
Acme Corp.
```

Se vedi caratteri illeggibili, ricontrolla i flag di preprocessamento, la risoluzione dell'immagine e la configurazione della lingua.

---

## Conclusione

Abbiamo coperto tutto ciò che ti serve per **preprocessare un'immagine per OCR** e **riconoscere il testo da documenti scansionati** usando Python. Partendo da un'istanza pulita del motore, abbiamo abilitato la correzione automatica dell'inclinazione e la binarizzazione, caricato un'immagine inclinata, eseguito il riconoscimento e stampato il testo pulito. Lungo il percorso abbiamo esplorato il supporto multilingue, le regolazioni manuali della soglia, l'estrazione del layout, il batch processing e le soluzioni per scansioni a bassa risoluzione.

Prova lo script sui tuoi documenti—potrebbe trattarsi di una pila di ricevute, di un modulo scritto a mano o di un ritaglio di giornale d'epoca. Una volta a tuo agio, prova a combinare la generazione di PDF o a inviare l'output a un indice di ricerca. Il cielo è il limite.

**Pronto per la prossima sfida?** Dai un'occhiata ai nostri tutorial su *“Estrarre Tabelle da PDF Scansionati con Python”* e *“Addestrare Modelli OCR Personalizzati con TensorFlow”* per continuare ad ampliare la tua cassetta degli attrezzi per l'automazione dei documenti.

Buon coding, e che il tuo OCR sia sempre nitido!


## Cosa Dovresti Imparare Dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑per‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}