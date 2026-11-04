---
category: general
date: 2026-06-06
description: OCR di immagini PNG con Python – impara come estrarre il testo dall’immagine,
  esegui un esempio di OCR in Python e leggi facilmente anche testi in greco antico.
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: it
og_description: OCR di immagini PNG in Python spiegato. Questa guida mostra come estrarre
  testo dall'immagine, eseguire un esempio di OCR in Python e leggere il greco antico
  con facilità.
og_title: OCR immagine PNG in Python – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR di immagine PNG in Python – Guida completa passo passo
url: /it/python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR PNG Image in Python – Guida Completa Passo‑Passo

Ti sei mai chiesto come **OCR PNG image** file direttamente da uno script Python? Forse hai una cartella piena di manoscritti antichi scansionati e hai bisogno di **extract text from image** file senza digitare tutto manualmente. La buona notizia è che non ti serve un dottorato in computer vision—basta qualche riga di codice e la libreria giusta, e leggerai greco antico in pochi secondi.

In questo tutorial percorreremo un **python OCR example** che riconosce il testo da un PNG, imposta la lingua al greco politonico e stampa il risultato. Alla fine saprai esattamente come **recognize image text**, gestire le insidie comuni e adattare lo script ad altre lingue o formati di immagine.

## Cosa Imparerai

- Installa e configura una libreria Python OCR (pytesseract + Tesseract OCR)
- Crea un'istanza del motore OCR e carica un file PNG
- Imposta la lingua di riconoscimento al greco politonico così potrai **read ancient greek**
- Stampa il testo riconosciuto e risolvi i problemi tipici
- Estendi lo script per elaborare in batch più PNG o cambiare lingua

### Prerequisiti

| Requisito | Perché è importante |
|-------------|----------------|
| Python 3.8+ | Sintassi moderna e type hints |
| `pytesseract` package | Leggera interfaccia attorno al motore Tesseract |
| Tesseract OCR binaries (≥ 5.0) | Il motore reale che esegue il lavoro pesante |
| Greek language data (`grc.traineddata`) | Necessario per **read ancient greek** correttamente |
| A PNG image you want to analyse (e.g., `ancient_greek.png`) | Il nostro obiettivo per la demo **ocr png image** |

Puoi installare la parte Python con:

```bash
pip install pytesseract Pillow
```

E su Ubuntu/macOS aggiungeresti il motore stesso:

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

Non dimenticare di scaricare i dati di addestramento greco politonico:

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

*(Il percorso può differire; regola `TESSDATA_PREFIX` se necessario.)*

## OCR PNG Image: Crea l'Istanza del Motore

La prima cosa di cui abbiamo bisogno è un oggetto che comunica con Tesseract. In `pytesseract` il motore è accessibile tramite funzioni a livello di modulo, ma per chiarezza lo avvolgeremo in una piccola classe. Questo rispecchia il concetto di “engine” che hai visto nello snippet originale.

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**Perché avvolgerlo?**  
- Mantiene l'API pubblica identica allo snippet di partenza, rendendo la migrazione indolore.  
- Ci permette di aggiungere logging o gestione degli errori in seguito senza toccare il flusso principale.  
- Dimostra una buona pratica OOP—qualcosa che gli sviluppatori senior apprezzano.

## Estrai Testo dall'Immagine: Imposta la Lingua al Greco Politonico

Ora che abbiamo un motore, dobbiamo dirgli quale lingua aspettarsi. Il greco politonico utilizza diacritici che non sono coperti dai dati “greek” standard, quindi indirizziamo Tesseract al file di addestramento `grc`.

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

Se vuoi **extract text from image** file in un'altra lingua, basta sostituire `"grc"` con `"eng"` per l'inglese, `"fra"` per il francese, ecc. La stessa riga funziona per qualsiasi lingua installata.

## Riconosci Testo nell'Immagine: Esegui l'OCR su un PNG

Con la lingua impostata, forniamo il PNG al motore. L'esempio originale usava un percorso hard‑coded; lo renderemo un po' più flessibile usando oggetti `Path`.

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**Suggerimenti & Casi Limite**

- **File not found** – avvolgi la chiamata in un `try/except FileNotFoundError` per fornire un messaggio amichevole.  
- **Low‑resolution PNG** – considera il pre‑processing (es., ridimensionamento, binarizzazione) con Pillow prima dell'OCR.  
- **Non‑Greek text** – Tesseract proverà comunque a decodificare, ma l'accuratezza cala drasticamente. Assicurati sempre di corrispondere alla lingua.

## Stampa il Testo Riconosciuto

Infine, stampiamo il risultato. In un progetto reale potresti scrivere su un database, un CSV, o anche inserirlo in una pipeline di traduzione.

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

Quando esegui lo script su una scansione chiara di un'iscrizione greca antica, dovresti vedere qualcosa del genere:

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

Se l'output appare confuso, ricontrolla che il file **greek.traineddata** sia nella cartella corretta e che il PNG non sia troppo rumoroso.

## Esempio Completo Funzionante (Tutti i Passaggi in Un Solo Script)

Di seguito il programma completo, pronto per l'esecuzione. Salvalo come `ocr_greek.py` ed esegui `python ocr_greek.py`.

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**Output atteso** (troncato per brevità):

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

Se vedi i corretti caratteri greci, congratulazioni—hai eseguito con successo un'operazione **ocr png image** in Python!

## Domande Frequenti & Consigli Pro

### Come migliorare l'accuratezza su un PNG rumoroso?

- Converti l'immagine in scala di grigi: `img = img.convert('L')`
- Applica una soglia binaria: `img = img.point(lambda x: 0 if x < 128 else 255, '1')`
- Ingrandisci con `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`

Questi passaggi spesso trasformano un incubo di **recognize image text** in un risultato pulito.

### Posso elaborare un'intera cartella di PNG?

Assolutamente. Avvolgi la chiamata `recognize_image` in un ciclo `for` su `Path.glob("*.png")`. Salva ogni risultato in un dizionario o scrivilo in un CSV per analisi successive.

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### E se ho bisogno di estrarre solo numeri?

Passa una stringa **config** personalizzata a `image_to_string`:

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

In questo modo puoi **extract text from image** file che contengono tabelle, numeri di serie o timestamp.

### Esiste un modo per ottenere i punteggi di confidenza?

Sì—usa `pytesseract.image_to_data` che restituisce un TSV con la confidenza per parola. Puoi filtrare i token a bassa confidenza prima di assemblare la stringa finale.

## Estendere il Tutorial

Ora che hai padroneggiato le basi, considera di esplorare questi argomenti correlati:

- **Batch OCR with multiprocessing** – velocizza grandi corpora di PNG.  
- **Hybrid OCR + NLP pipelines** – traduci automaticamente il greco antico estratto in inglese moderno.  
- **Alternative engines** – prova `easyocr` o metodi basati su `opencv` per casi d'uso specifici.  
- **Cloud OCR services** – Google Vision, Azure Computer Vision, o AWS Textract per scalabilità serverless.

Ognuno di questi si basa sul core **python ocr example** che abbiamo appena trattato, così ti sentirai a tuo agio ad approfondire.

## Conclusione

Abbiamo preso uno snippet semplice e lo abbiamo trasformato in un flusso di lavoro robusto **ocr png image** in Python. Creando un `OcrEngine`, impostando la lingua al greco politonico, fornendo un PNG e stampando il risultato, ora sai come **extract text from image** file, **recognize image text**, e persino **read ancient greek**.

## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrai Testo da Immagine con Aspose OCR – Guida Passo‑Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Come Impostare il Valore di Soglia nel Riconoscimento OCR di Immagini](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Riconosci testo immagine con Aspose OCR per più lingue](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}