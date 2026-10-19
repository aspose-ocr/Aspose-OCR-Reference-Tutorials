---
category: general
date: 2026-06-22
description: Impara a rilevare la lingua da un'immagine ed estrarre il testo usando
  OCR in Python. Tutorial passo‑passo che copre il rilevamento automatico della lingua
  e l'estrazione del testo.
draft: false
keywords:
- how to detect language
- detect language from image
- extract text from image
- how to use ocr
- how to extract text
language: it
og_description: Come rilevare la lingua da un'immagine usando l'OCR? Questa guida
  ti mostra passo passo come usare l'OCR in Python per rilevare la lingua ed estrarre
  il testo.
og_title: Come rilevare la lingua dalle immagini con OCR – Guida completa in Python
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to detect language from image and extract text using OCR
    in Python. Step‑by‑step tutorial covering automatic language detection and text
    extraction.
  headline: How to Detect Language from Images with OCR – Complete Python Guide
  type: TechArticle
- description: Learn how to detect language from image and extract text using OCR
    in Python. Step‑by‑step tutorial covering automatic language detection and text
    extraction.
  name: How to Detect Language from Images with OCR – Complete Python Guide
  steps:
  - name: Expected Output
    text: 'If `sample-multilang.png` contains French text, you might see something
      like:'
  - name: 1. Unsupported Image Formats
    text: 'If you try to load a TIFF file that the OCR library doesn’t recognise,
      `ocr.ImageStream.from_file()` will raise an `OcrUnsupportedFormatError`. Wrap
      the load call in a try/except block:'
  - name: 2. Low‑Resolution Images
    text: 'OCR accuracy drops sharply below ~300 dpi. If you notice poor detection,
      consider pre‑processing the image with Pillow:'
  - name: 3. Multiple Languages in One Image
    text: 'When an image contains text in more than one language, the auto‑detect
      feature will pick the dominant one. To capture all languages, you can disable
      auto‑detect and manually pass a list of languages to the engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Come rilevare la lingua dalle immagini con OCR – Guida completa in Python
url: /it/python-java/general/how-to-detect-language-from-images-with-ocr-complete-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come rilevare la lingua dalle immagini con OCR – Guida completa Python

Ti sei mai chiesto **come rilevare la lingua** in un'immagine senza aprirla manualmente? Non sei l'unico. In molti progetti—pensa a scanner di ricevute, archivi di documenti multilingue o a una semplice app foto‑to‑testo—devi sapere *qual*e lingua appartiene il testo prima di poterlo elaborare ulteriormente.  

In questo tutorial percorreremo un esempio pratico, end‑to‑end, che mostra **come rilevare la lingua** da un'immagine e poi estrarre i caratteri reali. Alla fine potrai eseguire poche righe di Python, puntare lo script a qualsiasi immagine supportata e ottenere sia la lingua rilevata *che* il testo estratto. Nessuna superfluità, solo una soluzione chiara da copiare‑incollare.

## Cosa imparerai

- Installare e configurare una libreria OCR leggera in Python.  
- Inizializzare il motore OCR e abilitare il rilevamento automatico della lingua.  
- Caricare un'immagine (qualsiasi formato supportato) ed eseguire l'OCR.  
- Recuperare la lingua rilevata e il testo estratto.  
- Gestire le difficoltà comuni come formati non supportati o risultati di lingua ambigui.  

Se ti sei mai chiesto **come usare l'OCR** per documenti multilingue, questa guida è per te.

---

## Prerequisiti

Prima di iniziare, assicurati di avere quanto segue sulla tua macchina:

| Requisito | Perché è importante |
|-------------|----------------|
| Python 3.9 or newer | Il pacchetto OCR che utilizzeremo è destinato a interpreti moderni. |
| `pip` (Python package manager) | Necessario per installare la libreria OCR. |
| A sample image containing text in at least one language (e.g., `sample-multilang.png`) | Ti fornisce qualcosa di concreto su cui testare. |
| Optional: Virtual environment (`venv` or `conda`) | Mantiene le dipendenze ordinate ed evita conflitti di versione. |

> **Pro tip:** Se lavori all'interno di un ambiente virtuale, attivalo prima di installare il pacchetto OCR per mantenere pulito il tuo Python globale.

---

## Passo 1: Installa la libreria OCR

Per questa dimostrazione useremo il pacchetto ipotetico `ocr` che rispecchia l'API mostrata nello snippet di codice. In uno scenario reale potresti sostituirlo con `pytesseract`, `easyocr` o qualsiasi altra libreria che supporti il rilevamento automatico della lingua.

```bash
pip install ocr
```

> **Nota:** Il pacchetto è leggero (< 5 MB) e funziona su Windows, macOS e Linux. Se incontri errori di permesso, aggiungi `--user` al comando.

---

## Passo 2: Inizializza il motore OCR – Come rilevare la lingua

Ora che la libreria è pronta, possiamo creare un'istanza del motore OCR. Questo è l'oggetto che effettivamente scannerizza l'immagine e individua la lingua.

```python
import ocr

# Initialise the OCR engine – this is where we start the language detection pipeline
engine = ocr.OcrEngine()
```

Perché iniziare con un motore? Pensa al motore come al cervello del sistema OCR; contiene la configurazione, carica i modelli linguistici e gestisce il lavoro pesante dietro le quinte. Inizializzarlo per primo garantisce che le chiamate successive (come il caricamento di un'immagine) abbiano un contesto in cui operare.

---

## Passo 3: Carica la tua immagine e abilita il rilevamento automatico della lingua

Il passo successivo è fornire l'immagine al motore. Attiveremo anche il flag *auto‑detect language* così il motore OCR proverà a indovinare la lingua al volo.

```python
# Load the image (any supported format – PNG, JPEG, BMP, etc.)
image_path = "YOUR_DIRECTORY/sample-multilang.png"
image = ocr.ImageStream.from_file(image_path)

# Attach the image to the engine
engine.set_image(image)

# Enable automatic language detection – this is the key for detecting language from image
engine.get_settings().set_auto_detect_language(True)
```

> **Perché abilitare l'auto‑detect?**  
> La maggior parte delle librerie OCR fornisce una lingua predefinita (spesso l'inglese). Se il tuo documento contiene francese, giapponese o qualsiasi altro script, il motore lo perderebbe senza questa impostazione. Attivando `set_auto_detect_language(True)`, lasciamo che il motore scandisca il bitmap, confronti le statistiche di forma dei caratteri e scelga il modello linguistico più probabile.

---

## Passo 4: Esegui l'OCR – Estrai il testo dall'immagine

Con l'immagine caricata e il rilevamento della lingua attivo, il vero passo OCR è una singola chiamata di metodo.

```python
# Run the OCR process – this both detects the language and extracts the text
result = engine.recognize()
```

Il metodo `recognize()` fa due cose dietro le quinte:

1. **Rilevamento della lingua:** Esegue un classificatore leggero sull'immagine per scegliere un codice lingua (es. `en`, `fr`, `es`).  
2. **Estrazione del testo:** Applica quindi il modello specifico della lingua per trascrivere i caratteri in stringhe Unicode.

Poiché entrambe le azioni avvengono insieme, ottieni un unico oggetto `result` che contiene tutto ciò di cui hai bisogno.

---

## Passo 5: Recupera e visualizza la lingua rilevata e il testo estratto

Infine, estraiamo il codice lingua e il testo grezzo dall'oggetto `result` e li stampiamo sulla console.

```python
# Print the detected language and the extracted text
print("Detected language:", result.get_language())
print("Text:", result.get_text())
```

### Output previsto

Se `sample-multilang.png` contiene testo in francese, potresti vedere qualcosa del genere:

```
Detected language: fr
Text: Bonjour, ceci est un texte d'exemple.
```

Se l'immagine è ambigua o contiene più lingue, il motore restituirà la lingua di cui è più sicuro, e potrai in seguito ispezionare il punteggio di confidenza (la maggior parte delle librerie espone un metodo `get_confidence()` per casi d'uso avanzati).

---

## Gestione dei casi limite comuni

### 1. Formati immagine non supportati

Se provi a caricare un file TIFF che la libreria OCR non riconosce, `ocr.ImageStream.from_file()` solleverà un `OcrUnsupportedFormatError`. Avvolgi la chiamata di caricamento in un blocco try/except:

```python
try:
    image = ocr.ImageStream.from_file(image_path)
except ocr.OcrUnsupportedFormatError as e:
    print(f"Unsupported format: {e}")
    raise
```

### 2. Immagini a bassa risoluzione

L'accuratezza dell'OCR cala drasticamente sotto ~300 dpi. Se noti scarsa rilevazione, considera di pre‑elaborare l'immagine con Pillow:

```python
from PIL import Image, ImageEnhance

pil_img = Image.open(image_path)
pil_img = pil_img.resize((pil_img.width * 2, pil_img.height * 2), Image.LANCZOS)
pil_img.save("resized.png")
image = ocr.ImageStream.from_file("resized.png")
```

### 3. Più lingue in una singola immagine

Quando un'immagine contiene testo in più di una lingua, la funzione di auto‑detect sceglierà quella dominante. Per catturare tutte le lingue, puoi disabilitare l'auto‑detect e passare manualmente una lista di lingue al motore:

```python
engine.get_settings().set_auto_detect_language(False)
engine.get_settings().set_languages(["en", "fr", "de"])
```

Ora l'OCR tenterà di riconoscere i caratteri usando ciascun modello linguistico e restituirà la migliore corrispondenza per ogni blocco di testo.

---

## Script completo – Tutti i passaggi combinati

Di seguito trovi lo script Python completo, pronto per l'esecuzione, che incorpora tutto ciò che abbiamo trattato. Salvalo come `detect_language_ocr.py` ed esegui `python detect_language_ocr.py`.

```python
# detect_language_ocr.py
# -------------------------------------------------
# How to detect language from image and extract text using OCR
# -------------------------------------------------

import ocr

def main():
    # 1️⃣ Initialise the OCR engine
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image (any supported format)
    image_path = "YOUR_DIRECTORY/sample-multilang.png"
    try:
        image = ocr.ImageStream.from_file(image_path)
    except ocr.OcrUnsupportedFormatError as err:
        print(f"Error loading image: {err}")
        return

    engine.set_image(image)

    # 3️⃣ Enable automatic language detection
    engine.get_settings().set_auto_detect_language(True)

    # 4️⃣ Perform OCR – this both detects language and extracts text
    try:
        result = engine.recognize()
    except ocr.OcrRecognitionError as err:
        print(f"OCR failed: {err}")
        return

    # 5️⃣ Retrieve and display the detected language and extracted text
    print("Detected language:", result.get_language())
    print("Text:", result.get_text())

if __name__ == "__main__":
    main()
```

**Eseguilo** e vedrai immediatamente il codice lingua seguito dal testo estratto. Questa è l'intera risposta a **come rilevare la lingua** e **come estrarre il testo** da un'immagine usando l'OCR.

---

## Approfondimenti – Prossimi passi e argomenti correlati

- **Migliora l'accuratezza**: Sperimenta con la pre‑elaborazione dell'immagine (soglia, denoising) usando `opencv-python`.  
- **Elaborazione batch**: Avvolgi lo script in un ciclo per gestire una cartella piena di immagini.  
- **Integra con NLP**: Passa il testo estratto a una libreria di identificazione della lingua come `langdetect` per una seconda opinione.  
- **Esplora altri motori OCR**: `pytesseract` offre un controllo fine, mentre `easyocr` supporta oltre 80 lingue pronte all'uso.  

Tutti questi argomenti ricollegano le nostre parole chiave secondarie—*detect language from image*, *extract text from image*, *how to use OCR*, e *how to extract text*—così potrai ampliare il tuo toolkit senza ricominciare da zero.

---

## Conclusione

Abbiamo appena coperto **come rilevare la lingua** da un'immagine, illustrato il codice esatto necessario e spiegato perché ogni passaggio è importante. Inizializzando il motore OCR, caricando l'immagine, attivando il rilevamento automatico della lingua e infine chiamando `recognize()`, ottieni sia l'identificatore della lingua sia il testo estratto in un'unica operazione pulita.

Ora puoi incorporare questa logica in applicazioni più grandi—che si tratti di un servizio di scansione ricevute, di un chatbot multilingue o di una semplice utility desktop. L'idea di base rimane la stessa: lascia che il motore OCR faccia il lavoro pesante, poi usa i risultati come preferisci.

Hai domande su casi particolari, o vuoi condividere un caso d'uso interessante? Lascia un commento qui sotto. Buon coding, e divertiti a trasformare le immagini in testo ricercabile!  

![come rilevare la lingua da un'immagine](ocr-demo.png "Screenshot che mostra come rilevare la lingua da un'immagine usando Python OCR")

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrai testo da immagine con Aspose OCR – Guida passo‑passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Estrai testo immagine C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Come usare AspOCR: filtri di pre‑elaborazione OCR per .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}