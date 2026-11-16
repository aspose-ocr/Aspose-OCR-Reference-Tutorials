---
category: general
date: 2026-06-28
description: Impara a riconoscere il testo da un'immagine ed eseguire l'OCR sull'immagine
  usando Aspose OCR per Python. Include i passaggi per impostare la lingua OCR ed
  estrarre i punteggi di confidenza.
draft: false
keywords:
- recognize text from image
- perform ocr on image
- how to set OCR language
language: it
og_description: Riconoscere il testo da un'immagine usando Aspose OCR in Python. Questa
  guida mostra come impostare la lingua OCR, eseguire l'OCR sull'immagine e leggere
  i livelli di confidenza.
og_title: Riconosci il testo da un'immagine – Tutorial completo di OCR in Python
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text from image and perform OCR on image using
    Aspose OCR for Python. Includes steps to set OCR language and extract confidence
    scores.
  headline: recognize text from image with Aspose OCR – Complete Python Guide
  type: TechArticle
- description: Learn how to recognize text from image and perform OCR on image using
    Aspose OCR for Python. Includes steps to set OCR language and extract confidence
    scores.
  name: recognize text from image with Aspose OCR – Complete Python Guide
  steps:
  - name: What if my image contains multiple languages?
    text: 'Aspose OCR supports multi‑language detection, but you need to pass a **combined
      language flag**. For example, to handle both Latin and Cyrillic:'
  - name: How do I improve accuracy on low‑resolution images?
    text: '- **Pre‑process** the image: increase contrast, apply binarization, or
      upscale using a library like Pillow. - **Set the correct DPI** if you know it;
      Aspose respects the image metadata. - **Choose the right language**—the more
      specific you are, the better the model performs.'
  - name: Can I extract only certain regions of the image?
    text: Yes. Use the `recognizeRegion` method (not shown in the basic example) and
      pass a rectangle object defining the area of interest. This is handy when you
      only need a table or a specific block of text.
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: Riconoscere il testo da un'immagine con Aspose OCR – Guida completa Python
url: /it/python-java/general/recognize-text-from-image-with-aspose-ocr-complete-python-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# riconoscere il testo da immagine con Aspose OCR – Guida completa Python

Hai mai avuto bisogno di **recognize text from image** ma non eri sicuro quale libreria ti offrisse sia velocità che precisione? Non sei solo. Nel mondo dell'automazione dei documenti, essere in grado di **perform OCR on image** è una necessità quotidiana—che tu stia digitalizzando ricevute, scannerizzando passaporti o estraendo dati da cartelli multilingue.

In questo tutorial percorreremo un esempio pratico che mostra esattamente come **recognize text from image** usando Aspose OCR per Python, e tratteremo anche **how to set OCR language** così che il motore sappia se sta gestendo Latin, Cyrillic o qualsiasi altro script. Alla fine avrai uno script pronto all'uso che stampa il testo completo, la confidenza riga per riga e persino le bounding box per ogni parola.

## Cosa ti serve

- **Python 3.8+** (il codice funziona su qualsiasi versione recente)
- **Aspose.OCR for Python via Java** package – installalo con `pip install aspose-ocr`
- Un file immagine (ad es., `mixed_script.png`) che contiene il testo che desideri estrarre
- Un IDE o editor di base—VS Code, PyCharm, o anche un semplice editor di testo andrà bene

Nessuna dipendenza pesante, nessun binario nativo da compilare. Basta un pip install e sei pronto.

## Passo 1: Installa e importa il motore OCR

Prima di tutto, scarichiamo la libreria sul tuo computer e importiamo le classi necessarie.

```python
# Install the package (run this once in your terminal)
# pip install aspose-ocr

# Import the OCR engine and the language enumeration
from asposeocrjava import OcrEngine, Language
```

> **Pro tip:** Se sei dietro un proxy aziendale, aggiungi il flag `--proxy` al comando pip. Ti farà risparmiare molti grattacapi in seguito.

## Passo 2: Crea il motore e **how to set OCR language**

Creare un'istanza di `OcrEngine` è semplice come chiamare il suo costruttore, ma il vero potere arriva quando indichi al motore quale lingua aspettarsi. Questa è la parte che risponde alla domanda “**how to set OCR language**”.

```python
# Instantiate the OCR engine
ocr_engine = OcrEngine()

# Tell the engine we’re dealing with Latin script (you can pick others like Language.Cyrillic)
ocr_engine.setLanguage(Language.Latin)
```

Perché è importante? Gli algoritmi OCR usano modelli di caratteri specifici per lingua; impostare la lingua corretta aumenta notevolmente la precisione, soprattutto per script con glifi simili (pensa a “0” vs “O” in Latino rispetto a “О” in Cirillico).

## Passo 3: **perform OCR on image** – Riconosci il testo

Ora forniamo al motore il percorso di un'immagine e lasciamo che faccia la sua magia. Il metodo restituisce un oggetto `RecognitionResult` che contiene tutto ciò di cui potresti aver bisogno.

```python
# Path to the image you want to process
image_path = "YOUR_DIRECTORY/mixed_script.png"

# Run the OCR operation
recognition_result = ocr_engine.recognizeImage(image_path)
```

Se il file non viene trovato, Aspose solleverà un `FileNotFoundError`. Avvolgi la chiamata in un blocco `try/except` per il codice di produzione—niente è peggio di un'eccezione non gestita che blocca il tuo servizio.

## Passo 4: Stampa il testo riconosciuto completo

La richiesta più comune è semplicemente “dammi il testo”. Il metodo `getText()` concatena tutte le linee rilevate in una singola stringa.

```python
# Print the complete text extracted from the image
print("Full text:", recognition_result.getText())
```

Vedrai qualcosa del genere:

```
Full text: Hello World!
This is a sample mixed‑script image.
```

Questo è il cuore di **recognize text from image**—una singola riga che restituisce tutto ciò che il motore è riuscito a decifrare.

## Passo 5: (Opzionale) Mostra la confidenza per ogni linea rilevata

I punteggi di confidenza ti permettono di valutare l'affidabilità. Le linee con un punteggio inferiore, ad esempio, a 0,70 potrebbero richiedere una revisione umana.

```python
print("\n--- Line‑by‑Line Confidence ---")
for line in recognition_result.getLines():
    # Each line object provides its text and a confidence value between 0 and 1
    print(f"Line: '{line.getText()}'  Confidence: {line.getConfidence():.2f}")
```

Output tipico:

```
Line: 'Hello World!'  Confidence: 0.98
Line: 'This is a sample mixed‑script image.'  Confidence: 0.85
```

## Passo 6: (Opzionale) Recupera le bounding box per ogni parola – Ottimo per evidenziare nell'interfaccia

Se stai costruendo un visualizzatore che permette agli utenti di cliccare su una parola per vedere i dati OCR, le coordinate della bounding box sono preziose.

```python
print("\n--- Word Bounding Boxes ---")
for word in recognition_result.getWords():
    bbox = word.getBoundingBox()   # Returns (x, y, width, height)
    print(f"Word '{word.getText()}' at {bbox}")
```

Esempio di output:

```
Word 'Hello' at (12, 34, 58, 20)
Word 'World' at (78, 34, 60, 20)
```

Queste coordinate sono in pixel relative all'immagine originale, quindi puoi sovrapporle direttamente su una canvas.

## Script completo funzionante

Mettendo tutto insieme, ecco uno script pronto all'uso che puoi inserire in qualsiasi progetto. Sostituisci `YOUR_DIRECTORY/mixed_script.png` con il percorso reale della tua immagine.

```python
# ocr_demo.py
from asposeocrjava import OcrEngine, Language

def main(image_path: str, language: Language = Language.Latin):
    """
    Recognize text from an image using Aspose OCR.
    Parameters:
        image_path (str): Full path to the image file.
        language (Language): OCR language to use (default: Latin).
    """
    # Create the OCR engine and set the desired language
    ocr_engine = OcrEngine()
    ocr_engine.setLanguage(language)

    try:
        # Perform OCR
        result = ocr_engine.recognizeImage(image_path)

        # Full text output
        print("Full text:", result.getText())

        # Optional: line confidence
        print("\n--- Line‑by‑Line Confidence ---")
        for line in result.getLines():
            print(f"Line: '{line.getText()}'  Confidence: {line.getConfidence():.2f}")

        # Optional: word bounding boxes
        print("\n--- Word Bounding Boxes ---")
        for word in result.getWords():
            bbox = word.getBoundingBox()
            print(f"Word '{word.getText()}' at {bbox}")

    except FileNotFoundError:
        print(f"Error: Image file not found at {image_path}")
    except Exception as e:
        print(f"An unexpected error occurred: {e}")

if __name__ == "__main__":
    # Change the path below to point at your own test image
    IMAGE_PATH = "YOUR_DIRECTORY/mixed_script.png"
    main(IMAGE_PATH, Language.Latin)
```

Eseguilo con:

```bash
python ocr_demo.py
```

Dovresti vedere il testo estratto completo, i punteggi di confidenza e le bounding box stampati sulla console.

## Domande comuni e casi particolari

### E se la mia immagine contiene più lingue?

Aspose OCR supporta il rilevamento multilingua, ma è necessario passare un **combined language flag**. Per esempio, per gestire sia Latino che Cirillico:

```python
ocr_engine.setLanguage(Language.Latin | Language.Cyrillic)
```

L'operatore pipe (`|`) unisce gli enum. Questo risponde al requisito “**perform OCR on image**” per scenari multilingua.

### Come miglioro la precisione su immagini a bassa risoluzione?

- **Pre‑process** l'immagine: aumenta il contrasto, applica la binarizzazione o ingrandisci usando una libreria come Pillow.
- **Set the correct DPI** se lo conosci; Aspose rispetta i metadati dell'immagine.
- **Choose the right language**—più specifica è la lingua, migliore sarà il modello.

### Posso estrarre solo certe regioni dell'immagine?

Sì. Usa il metodo `recognizeRegion` (non mostrato nell'esempio base) e passa un oggetto rettangolo che definisce l'area di interesse. È utile quando ti serve solo una tabella o un blocco di testo specifico.

## Conclusione

Abbiamo appena percorso un esempio completo, end‑to‑end, di come **recognize text from image** usando Aspose OCR per Python. Ora sai come **perform OCR on image**, impostare correttamente la **OCR language** e recuperare sia i punteggi di confidenza sia le bounding box a livello di parola per il lavoro UI successivo.

Da qui potresti:

- Sperimentare con altre lingue (`Language.Arabic`, `Language.Japanese`, ecc.)
- Integrare lo script in un servizio web (Flask/Django) per fornire OCR come API
- Combinare i dati delle bounding‑box con una canvas frontend per permettere agli utenti di evidenziare il testo

Le possibilità sono ampie quanto i documenti che devi digitalizzare. Hai un'immagine difficile che non collabora? Lascia un commento e risolveremo il problema insieme. Buona programmazione!

![recognize text from image example](/images/ocr_example.png "recognize text from image – Aspose OCR output")

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}