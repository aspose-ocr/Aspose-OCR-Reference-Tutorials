---
category: general
date: 2026-08-12
description: Come utilizzare l'OCR in Python per riconoscere il testo da un'immagine,
  estrarre il testo, convertire l'immagine in testo e pulire il testo OCR con il post‑processing
  AI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- recognize text from image
- extract text from image
- convert image to text
- clean up OCR text
language: it
lastmod: 2026-08-12
og_description: Come utilizzare OCR in Python per trasformare le immagini in testo
  modificabile. Impara a riconoscere il testo dalle immagini, estrarre il testo, convertire
  l'immagine in testo e pulire il testo OCR con l'IA.
og_image_alt: Screenshot of Python code converting an image to clean text using OCR
  and AI post‑processing
og_title: Come usare l'OCR in Python – guida completa di programmazione
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: How to use OCR in Python to recognize text from image, extract text,
    convert image to text, and clean up OCR text with AI post‑processing.
  headline: How to use OCR in Python – step‑by‑step guide
  type: TechArticle
- description: How to use OCR in Python to recognize text from image, extract text,
    convert image to text, and clean up OCR text with AI post‑processing.
  name: How to use OCR in Python – step‑by‑step guide
  steps:
  - name: Loads an image file (PNG, JPEG, or TIFF).
    text: Loads an image file (PNG, JPEG, or TIFF).
  - name: Recognizes text from the image using an OCR engine.
    text: Recognizes text from the image using an OCR engine.
  - name: Improves the raw output with an AI‑driven post‑processor.
    text: Improves the raw output with an AI‑driven post‑processor.
  - name: Prints the cleaned‑up text to the console.
    text: Prints the cleaned‑up text to the console.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- AI post‑processing
title: Come usare l'OCR in Python – guida passo passo
url: /it/python/general/how-to-use-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare OCR in Python – guida passo‑passo

Se hai bisogno di **how to use OCR** per trasformare documenti scansionati o screenshot in testo modificabile, questo tutorial mostra una soluzione completa in Python. Imparerai a riconoscere il testo da un'immagine, estrarre il testo da un'immagine, convertire l'immagine in testo e pulire il testo OCR con un leggero post‑processore AI.

La guida copre tutto, dall'installazione delle librerie necessarie alla gestione di immagini di bassa qualità, così potrai integrare OCR in qualsiasi pipeline di automazione senza indovinare quale passaggio manca.

## Cosa costruirai

Alla fine di questo articolo avrai uno script Python unico che:

1. Carica un file immagine (PNG, JPEG o TIFF).  
2. Riconosce il testo dall'immagine usando un motore OCR.  
3. Migliora l'output grezzo con un post‑processore guidato dall'AI.  
4. Stampa il testo pulito sulla console.

Nessun servizio esterno è richiesto—tutto gira localmente, rendendo la soluzione adatta a ambienti offline o progetti sensibili alla privacy.

## Prerequisiti

- Python 3.9 o successivo.  
- Librerie `pytesseract` e `Pillow` (`pip install pytesseract pillow`).  
- Binario Tesseract‑OCR installato e disponibile nel `PATH` del tuo sistema.  
- Una comprensione di base delle funzioni in Python.  

Se hai già questi elementi, puoi passare direttamente al primo blocco di codice.

## Come usare OCR con Python

Il nucleo di **how to use OCR** è inizializzare il motore OCR e fornirgli un'immagine. In questo tutorial usiamo `pytesseract`, un leggero wrapper attorno al motore open‑source Tesseract.

```python
import pytesseract
from PIL import Image

def load_image(path: str) -> Image.Image:
    """
    Open an image file and return a Pillow Image object.
    Pillow handles many formats (PNG, JPEG, TIFF) and ensures
    the image is in a mode that Tesseract can read.
    """
    return Image.open(path)
```

> **Perché questo passaggio è importante** – Tesseract si aspetta un'immagine pulita e correttamente orientata. L'uso di Pillow garantisce che i dati dell'immagine siano normalizzati prima dell'esecuzione di OCR, migliorando l'accuratezza dell'operazione successiva di **recognize text from image**.

## Riconoscere il testo da immagine

Ora chiamiamo `pytesseract.image_to_string` per estrarre la stringa grezza. Questa è la classica chiamata “recognize text from image”.

```python
def ocr_recognize(image: Image.Image) -> str:
    """
    Run Tesseract OCR on the supplied image and return the raw text.
    """
    raw_text = pytesseract.image_to_string(image, lang='eng')
    return raw_text
```

> **Perché separiamo la funzione** – Isolare il passaggio OCR ti permette di cambiare motore in seguito (ad es., passare a EasyOCR) senza toccare il resto della pipeline. Inoltre rende più semplice il testing unitario.

## Estrarre testo da immagine e migliorare la qualità

L'output grezzo di OCR spesso contiene interruzioni di riga, caratteri erranti o parole riconosciute in modo sbagliato. Un post‑processore AI può pulire automaticamente questi artefatti. Di seguito un esempio minimale che usa la libreria `transformers` per eseguire localmente un piccolo modello linguistico. Puoi sostituirlo con qualsiasi servizio proprietario se preferisci.

```python
from transformers import pipeline

# Initialize a zero‑shot text‑generation pipeline once (expensive operation)
_ai_postprocessor = pipeline("text2text-generation", model="google/flan-t5-small")

def clean_ocr_text(raw: str) -> str:
    """
    Send the raw OCR string to a lightweight AI model that rewrites
    the text, removing obvious errors and normalizing whitespace.
    """
    # The prompt guides the model to act as a post‑processor
    prompt = f"Clean up the following OCR output, fixing spelling mistakes and removing extra line breaks:\n\n{raw}"
    result = _ai_postprocessor(prompt, max_length=512, do_sample=False)
    # The pipeline returns a list of dicts; we take the generated text
    cleaned = result[0]["generated_text"]
    return cleaned.strip()
```

> **Perché un post‑processore AI aiuta** – I motori OCR tradizionali eccellono nel riconoscimento dei caratteri ma faticano con layout e rumore. Un modello linguistico comprende il contesto, così può trasformare “Th1s 1s 4 test.” in “This is a test.” Questo passaggio risponde direttamente al requisito **clean up OCR text**.

## Convertire immagine in testo – script completo

Unendo tutto otteniamo uno script breve che **convert image to text** end‑to‑end.

```python
import sys
from pathlib import Path

def main(image_path: str):
    """
    Complete pipeline:
    1. Load image.
    2. Recognize text from image.
    3. Clean up OCR text.
    4. Print the final result.
    """
    # 1️⃣ Load the image file
    img = load_image(image_path)

    # 2️⃣ Recognize text from image (raw OCR)
    raw_text = ocr_recognize(img)
    print("=== Raw OCR output ===")
    print(raw_text)
    print("\n---\n")

    # 3️⃣ Clean up OCR text with AI post‑processor
    cleaned_text = clean_ocr_text(raw_text)
    print("=== Cleaned‑up text ===")
    print(cleaned_text)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python ocr_pipeline.py <path-to-image>")
        sys.exit(1)

    image_file = Path(sys.argv[1])
    if not image_file.is_file():
        print(f"Error: file '{image_file}' does not exist.")
        sys.exit(1)

    main(str(image_file))
```

### Output previsto

Eseguire lo script con un'immagine di esempio (`sample.png`) potrebbe produrre:

```
=== Raw OCR output ===
Th1s 1s 4 sampl3
text from an im4ge.

--- 

=== Cleaned‑up text ===
This is a sample text from an image.
```

Nota come il post‑processore AI abbia corretto i caratteri letti erroneamente e rimosso l'interruzione di riga superflua. Questo dimostra l'intero workflow di **extract text from image** e mostra il beneficio della pulizia del testo OCR.

## Gestire casi limite comuni

| Situazione                              | Modifica consigliata                                                               |
|----------------------------------------|------------------------------------------------------------------------------------|
| Immagine a basso contrasto             | Converti in scala di grigi e aumenta il contrasto con `ImageEnhance` prima di OCR. |
| Documento multilingua                  | Passa una lista separata da virgole a `lang` (es., `lang='eng+fra'`).               |
| Immagini molto grandi ( > 2000 px )    | Ridimensiona con `img.thumbnail((2000, 2000))` per velocizzare Tesseract.          |
| Binario Tesseract mancante             | Verifica che `pytesseract.pytesseract.tesseract_cmd` punti all'eseguibile.        |
| Post‑processore AI troppo lento        | Usa un modello più piccolo (`t5-small`) o esegui il post‑processore su GPU.        |

> **Consiglio professionale:** Metti in cache l'oggetto modello AI (`_ai_postprocessor`) al momento dell'importazione del modulo, come mostrato, per evitare di ricaricarlo ad ogni chiamata. Questo riduce drasticamente la latenza quando si elaborano molte immagini.

## Approcci alternativi

- **EasyOCR**: Una libreria OCR pure‑Python che supporta oltre 80 lingue senza un binario esterno. Sostituisci `ocr_recognize` con `EasyOCR.Reader` se preferisci una soluzione solo pip.
- **Cloud OCR APIs**: Google Cloud Vision, Azure Computer Vision o Amazon Textract offrono maggiore accuratezza per layout complessi ma richiedono accesso di rete e fatturazione.
- **Post‑processing personalizzato**: Per una pulizia deterministica, le espressioni regolari (`re.sub`) possono correggere pattern comuni (es., rimuovere interruzioni di riga con trattini) senza un modello AI.

## Riepilogo

Ora sai **how to use OCR** in Python per riconoscere testo da immagine, estrarre testo da immagine, convertire immagine in testo e pulire il testo OCR con un post‑processore AI. Lo script completo dimostra una pipeline pronta per la produzione che puoi estendere con ulteriori pre‑processamenti (riduzione del rumore, correzione di inclinazione) o azioni successive (salvataggio in un database, alimentazione di un indice di ricerca).

### Prossimi passi

- Sperimenta con diversi modelli AI (es., `gpt‑2`, `flan‑ul2`) per vedere quale offre la migliore pulizia per il tuo dominio.  
- Integra la pipeline in un servizio web usando Flask o FastAPI, trasformando lo script in un endpoint OCR on‑demand.  
- Esplora l'elaborazione batch: itera su una cartella di immagini e scrivi ogni output pulito in un file `.txt` corrispondente.

Sentiti libero di adattare il codice al tuo flusso di lavoro specifico, e lascia che il testo pulito e ricercabile potenzi la fase successiva della tua applicazione. Buona programmazione!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Converti immagine in testo: estrarre testo da immagine usando Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Estrarre testo da immagine con Aspose OCR – Guida passo‑passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Estrarre testo da immagine – Ottimizzazione OCR con Aspose.OCR per .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}