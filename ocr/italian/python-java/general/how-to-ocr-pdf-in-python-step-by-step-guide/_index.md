---
category: general
date: 2026-03-28
description: Impara a fare OCR su PDF con Python rapidamente. Questa guida ti mostra
  come estrarre testo da PDF, riconoscere il testo da PDF e convertire PDF scansionati
  in testo usando Aspose OCR.
draft: false
keywords:
- how to ocr pdf
- ocr pdf with python
- extract text from pdf
- recognize text from pdf
- convert scanned pdf to text
language: it
og_description: Impara a fare OCR su PDF con Python. Estrai il testo da PDF, riconosci
  il testo da PDF e converti PDF scansionati in testo in pochi minuti.
og_title: Come fare OCR di PDF in Python – Guida completa
tags:
- PDF
- OCR
- Python
- Aspose
title: Come eseguire l'OCR di PDF in Python – Guida passo passo
url: /it/python-java/general/how-to-ocr-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come fare OCR su PDF in Python – Guida passo‑passo

Ti sei mai chiesto **come fare OCR su PDF** quando il file è solo un’immagine di una pagina? Non sei il solo. In questo tutorial percorreremo passo dopo passo le fasi per fare OCR su file PDF, estrarre testo da PDF e trasformare un PDF scansionato in testo ricercabile — tutto con puro codice Python.

Copriamo tutto, dall’installazione della libreria Aspose OCR all’estrazione del testo riconosciuto da ogni pagina. Alla fine sarai in grado di **fare OCR su PDF con Python**, **estrarre testo da PDF** e **convertire PDF scansionati in testo** senza dover setacciare documenti sparsi. Niente fronzoli, solo un esempio pratico e funzionante da copiare‑incollare.

## Cosa ti serve

Prima di iniziare, assicurati di avere:

* Python 3.8+ (l’ultima versione stabile è la migliore)  
* Una licenza Aspose OCR per Python o una chiave di prova gratuita – puoi ottenerla dal sito di Aspose.  
* Un PDF scansionato da elaborare (lo chiameremo `input.pdf`).  

Se li hai già, ottimo — cominciamo. Altrimenti, l’installazione del pacchetto è un gioco da ragazzi e ti mostriamo come fare.

## Come fare OCR su PDF – Configurare l’ambiente

La prima cosa da fare è ottenere il modulo Aspose OCR sulla tua macchina. Il pacchetto si chiama `aspose-ocr` e lo puoi installare con pip:

```bash
pip install aspose-ocr
```

> **Consiglio:** Usa un ambiente virtuale (`python -m venv venv`) così le dipendenze rimangono ordinate.

Una volta installato il pacchetto, sei pronto a importarlo e avviare il motore OCR. Questa è la base per ogni workflow **ocr pdf with python** che costruirai in seguito.

## OCR PDF con Python – Importare Aspose OCR

Ora che la libreria è disponibile, importiamola nello script. Imposteremo anche il motore per lavorare in *modalità PDF diretto*, che dice ad Aspose di leggere i byte del PDF direttamente dal file invece di convertire ogni pagina in un’immagine prima.

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr

# Step 2: Create an OCR engine instance and enable direct PDF processing
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
```

Perché usare `PdfMode.DIRECT`? Perché evita un passaggio extra di rasterizzazione, rendendo il processo più veloce e preservando il layout originale — particolarmente utile quando devi **recognize text from PDF** con precisione.

## Riconoscere testo da PDF – Eseguire il motore

Con il motore pronto, puntalo al tuo file scansionato. Il metodo `recognize_from_pdf` fa tutto il lavoro pesante: analizza ogni pagina, esegue l’algoritmo OCR e restituisce un oggetto `OcrResult` che contiene una collezione di oggetti `Page`.

```python
# Step 3: Define the path to the PDF you want to process
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# Step 4: Perform OCR on the PDF and obtain the result object
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)
```

Ti chiedi se funziona con PDF criptati? Sì, basta fornire la password tramite `ocr_engine.password = "secret"` prima di chiamare `recognize_from_pdf`. È un caso limite che molti tutorial tralascia, ma è utile in pipeline reali.

## Estrarre testo da PDF – Accedere ai risultati delle pagine

La lista `ocr_result.pages` contiene una voce per ogni pagina. Ogni oggetto `Page` ha un attributo `.text` che contiene la rappresentazione in testo semplice della pagina scansionata. Scorriamola e stampiamo i risultati così da vedere esattamente cosa è stato estratto.

```python
# Step 5: Iterate through each page and display the recognized text
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)
```

Eseguendo lo script otterrai qualcosa del genere:

```
PDF OCR complete. Text per page:
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Questo output dimostra che hai **extract text from PDF** e **recognize text from PDF** con Aspose OCR. Ora puoi inviare le stringhe a un database, a un indice di ricerca o a qualsiasi pipeline NLP successiva.

![esempio di come fare OCR su PDF](placeholder-image.png "esempio di come fare OCR su PDF")

*Testo alternativo immagine:* **esempio di come fare OCR su PDF** – mostra l’output della console con il testo riconosciuto per pagina.

## Convertire PDF scansionato in testo – Salvare l’output

La maggior parte degli sviluppatori non vuole solo vedere il testo sulla console; ha bisogno di un file persistente. Qui trovi un piccolo helper che scrive il testo di ogni pagina in un file `.txt` separato, realizzando così **convert scanned PDF to text** in una cartella chiamata `output`.

```python
import os

output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

Al termine dello script avrai una directory ordinata:

```
output_text/
│─ page_1.txt
│─ page_2.txt
└─ …
```

Ora hai completato **convert scanned PDF to text** e puoi alimentare quei file a qualsiasi processo successivo — ricerca, analisi o anche un semplice `grep`.

## Domande frequenti e casi particolari

**E se il mio PDF contiene immagini mescolate a testo reale?**  
Aspose OCR cercherà di riconoscere tutto, ma puoi velocizzare le cose disabilitando l’OCR per le pagine che già contengono testo selezionabile. Imposta `ocr_engine.auto_detect_page_orientation = True` e poi chiama `ocr_engine.recognize_from_pdf(..., detect_text=False)` per le pagine note.

**Posso controllare il modello linguistico?**  
Assolutamente. Imposta `ocr_engine.language = aocr.Language.English` (o qualsiasi lingua supportata) prima di chiamare `recognize_from_pdf`. Questo migliora l’accuratezza per documenti non‑inglesi.

**Come gestire PDF molto grandi (100+ pagine)?**  
Elaborali a blocchi. Il metodo `recognize_from_pdf` accetta un argomento `page_range`, ad esempio `ocr_engine.recognize_from_pdf(path, page_range=(1, 20))`. Cicla sui range per mantenere basso l’uso di memoria.

## Esempio completo funzionante

Mettendo tutto insieme, ecco uno script unico che puoi salvare in un file chiamato `ocr_pdf.py` ed eseguire:

```python
import os
import aspose.ocr as aocr

# -------------------------------------------------
# 1️⃣  Initialize the OCR engine (direct PDF mode)
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
# Optional: set language for better accuracy
ocr_engine.language = aocr.Language.English

# -------------------------------------------------
# 2️⃣  Path to the scanned PDF you want to process
# -------------------------------------------------
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# -------------------------------------------------
# 3️⃣  Run OCR – this is where we actually recognize text from PDF
# -------------------------------------------------
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)

# -------------------------------------------------
# 4️⃣  Print the extracted text (shows how to extract text from PDF)
# -------------------------------------------------
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)

# -------------------------------------------------
# 5️⃣  Save each page as a .txt file (convert scanned PDF to text)
# -------------------------------------------------
output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

Eseguilo con:

```bash
python ocr_pdf.py
```

Dovresti vedere l’output della console che conferma il testo di ogni pagina e la posizione dei file `.txt` salvati.

## Conclusione

Abbiamo coperto **come fare OCR su PDF** usando Python, mostrato un modo pulito per **ocr pdf with python**, spiegato come **extract text from PDF**, illustrato i meccanismi dietro **recognize text from PDF**, e infine fornito uno snippet pronto all’uso che **convert scanned PDF to text**. L’intero processo è confezionato

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}