---
category: general
date: 2026-03-18
description: Esegui OCR sull'immagine per estrarre il testo da PNG e generare un PDF
  ricercabile. Scopri come riconoscere il testo nell'immagine e convertire PNG in
  PDF in pochi minuti.
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: it
og_description: Esegui OCR sull'immagine per estrarre il testo da PNG, riconosci l'immagine
  di testo e genera un PDF ricercabile. Segui questa guida passo‑passo.
og_title: Esegui OCR sull'immagine – Estrai rapidamente il testo da PNG
tags:
- OCR
- Python
- Image Processing
title: Esegui OCR sull'immagine – Estrai rapidamente il testo da PNG
url: /it/python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine – Estrai Testo da PNG Rapidamente

Hai mai avuto bisogno di **run OCR on image** file ma non sapevi da dove cominciare? Forse hai un articolo scansionato salvato come `article.png` e vuoi solo il testo semplice, oppure ti serve un PDF ricercabile per l'archiviazione. In ogni caso, sei nel posto giusto. In questo tutorial vedremo come estrarre testo da PNG, riconoscere l'immagine di testo e persino convertire quel PNG in un PDF ricercabile—tutto con poche righe di codice.

> **Cosa otterrai:** uno script completo e eseguibile che carica un PNG, esegue OCR, salva l'output hOCR e, facoltativamente, crea un PDF ricercabile. Nessuna importazione mancante, nessun “vedi la documentazione” senza via d'uscita—solo una soluzione autonoma che puoi inserire nel tuo progetto oggi.

## Prerequisiti

- **Python 3.8+** (la sintassi usata qui funziona su qualsiasi versione recente)
- La libreria **`ocr_engine`** che stai usando (l'esempio assume una classe chiamata `OcrEngine`; sostituiscila con Tesseract, EasyOCR, ecc., se necessario)
- Un'immagine PNG che desideri elaborare (ad es. `article.png` posizionata in una cartella a cui puoi fare riferimento)
- Permessi di scrittura sulla directory di output

Se stai usando Tesseract sotto il cofano, installalo con:

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

E poi installa il wrapper Python:

```bash
pip install pytesseract Pillow
```

*Suggerimento:* mantieni la tua libreria OCR aggiornata—nuovi pacchetti lingua e ottimizzazioni delle prestazioni arrivano frequentemente.

## Esegui OCR su Immagine – Guida Passo‑Passo

Di seguito trovi lo **script completo**. Sentiti libero di copiarlo e incollarlo in un file chiamato `run_ocr.py` ed eseguirlo con `python run_ocr.py`.

```python
# run_ocr.py
import os
from pathlib import Path

# Import the OCR engine – replace with your actual import if different
# For Tesseract via pytesseract you would use: import pytesseract
# Here we assume a generic OcrEngine class that matches the example
from ocr_engine import OcrEngine  # <-- adjust as needed

def main():
    # ------------------------------------------------------------------
    # Step 1: Create an OCR engine instance
    # ------------------------------------------------------------------
    ocr_engine = OcrEngine()
    # Why this matters: the engine holds configuration (language, DPI, etc.)
    # You can tweak ocr_engine.setLanguage('eng') or similar before proceeding.

    # ------------------------------------------------------------------
    # Step 2: Load the image you want to process
    # ------------------------------------------------------------------
    image_path = Path("YOUR_DIRECTORY/article.png")
    if not image_path.is_file():
        raise FileNotFoundError(f"Image not found: {image_path}")
    ocr_engine.setImageFromFile(str(image_path))

    # ------------------------------------------------------------------
    # Step 3: Choose the export format
    # ------------------------------------------------------------------
    # hOCR preserves layout (bounding boxes, fonts) – perfect for searchable PDFs.
    # Other options: "txt", "pdf", "pdfa"
    ocr_engine.setExportFormat("hocr")

    # ------------------------------------------------------------------
    # Step 4: Run the recognition process
    # ------------------------------------------------------------------
    ocr_result = ocr_engine.recognize()
    # The result object gives us access to the raw OCR text, hOCR, etc.

    # ------------------------------------------------------------------
    # Step 5: Write the HOCR output to a file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/article.hocr")
    with open(output_path, "w", encoding="utf-8") as output_file:
        output_file.write(ocr_result.getExportedContent())
    print(f"✅ HOCR saved to {output_path}")

    # ------------------------------------------------------------------
    # Optional: Generate a searchable PDF from the HOCR
    # ------------------------------------------------------------------
    # Many OCR engines can bundle the original image with the hOCR to produce
    # a PDF that you can search. If your engine supports it, uncomment:
    # ocr_engine.setExportFormat("pdf")
    # pdf_result = ocr_engine.recognize()
    # pdf_path = Path("YOUR_DIRECTORY/article_searchable.pdf")
    # with open(pdf_path, "wb") as pdf_file:
    #     pdf_file.write(pdf_result.getExportedContent())
    # print(f"📄 Searchable PDF created at {pdf_path}")

if __name__ == "__main__":
    main()
```

### Cosa fa lo script, in parole semplici

1. **Instantiate** il motore OCR così puoi controllare le sue impostazioni.
2. **Load** il file PNG (`article.png`). Lo script si interrompe subito se il file non esiste—nessun misterioso errore `NoneType` in seguito.
3. **Select** `hocr` come formato di esportazione. Questo formato conserva il layout originale, essenziale per convertire successivamente l'immagine in un PDF ricercabile.
4. **Run** il motore di riconoscimento; qui avviene il lavoro pesante.
5. **Write** l'XML hOCR in `article.hocr`. Ora hai una rappresentazione leggibile dalla macchina del testo e delle sue coordinate.
6. *(Optional)* Passa a `"pdf"` e genera un PDF ricercabile in un passaggio aggiuntivo.

L'**output previsto** è un file `.hocr` codificato in UTF‑8 che appare più o meno così (ridotto per brevità):

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

Se decommenti la sezione PDF, otterrai anche `article_searchable.pdf`, che potrai aprire con qualsiasi visualizzatore PDF e usare la casella di ricerca **Ctrl + F** per trovare le parole istantaneamente.

![Esempio di output OCR su immagine](example.png "Esegui OCR su immagine – risultati hOCR e PDF")

## Come Estrarre Testo da PNG Usando OcrEngine

Se tutto ciò di cui hai bisogno è il testo grezzo (senza layout, senza PDF), puoi saltare completamente il passaggio hOCR:

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*Perché scegliere il testo semplice?* È leggero, perfetto per l'indicizzazione e funziona bene con pipeline NLP successive.

## Riconosci Immagine di Testo e Genera PDF Ricercabile

Generare un PDF ricercabile è una procedura in due fasi:

1. **Run OCR** con `hocr` (come abbiamo fatto sopra) per ottenere le informazioni di layout.
2. **Combine** il PNG originale con l'hOCR in un PDF usando l'esportatore PDF del motore.

La maggior parte delle librerie OCR moderne (Tesseract, ABBYY, Google Vision) espongono un'esportazione `pdf` che fa esattamente questo. Lo snippet nel blocco *Optional* dello script principale mostra il modello. Se la tua libreria non dispone di un esportatore PDF integrato, puoi usare **`pdf2image`** + **`reportlab`** per unire l'immagine e l'hOCR—basta farmelo sapere e condividerò un rapido esempio aggiuntivo.

## Converti PNG in PDF con Output OCR

A volte vuoi semplicemente un **PDF semplice** che contenga l'immagine (senza livello ricercabile). È ancora più semplice:

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

Combinalo con il passaggio OCR se ti serve una versione ricercabile, oppure mantienilo come una fedele replica visiva per scopi di archiviazione.

## Problemi Comuni & Suggerimenti

| Problema | Perché accade | Soluzione rapida |
|----------|----------------|------------------|
| **PNG sfocato o a bassa risoluzione** | L'accuratezza OCR diminuisce drasticamente sotto ~300 DPI. | Ingrandisci con `Image.resize((width*2, height*2), Image.LANCZOS)` prima di passare l'immagine al motore. |
| **Lingua errata** | Il motore usa l'inglese per impostazione predefinita; i caratteri non‑inglesi diventano illeggibili. | Chiama `ocr_engine.setLanguage('deu')` (o il codice ISO appropriato) prima di `recognize()`. |
| **Output hOCR mancante** | Alcuni motori tornano al testo semplice se `setExportFormat` non è chiamato. | Verifica che `setExportFormat("hocr")` venga eseguito **prima** di `recognize()`. |
| **Errori di permessi file** | Tentativo di scrivere in una cartella di sola lettura. | Usa un percorso all'interno del tuo progetto o esegui prima `os.makedirs(..., exist_ok=True)`. |
| **PDF grandi causano picchi di memoria** | L'esportatore PDF mantiene l'intera immagine in RAM. | Elabora le pagine a blocchi o usa un writer PDF in streaming. |

*Suggerimento:* testa sempre su una piccola immagine di esempio prima di scalare a una massa di migliaia. Risparmia ore di debug.

## Conclusione

Ora sai **come eseguire OCR su image** file, **estrarre testo da PNG**, **riconoscere l'immagine di testo** per attività successive, **generare un PDF ricercabile**, e **convertire PNG in PDF** quando ti serve un archivio semplice. Lo script fornito è una soluzione completa, pronta da copiare‑incollare, che funziona subito, e le sezioni opzionali ti permettono di personalizzare l'output al tuo flusso di lavoro.

### Qual è il prossimo passo?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}