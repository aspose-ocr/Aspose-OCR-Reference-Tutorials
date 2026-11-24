---
category: general
date: 2026-07-05
description: Estrai il testo da un'immagine usando Python OCR. Scopri come caricare
  l'immagine per l'OCR, leggere il testo da una regione e estrarre il testo da una
  fattura con poche righe di codice.
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: it
og_description: Estrai il testo da un'immagine con OCR in Python. Questa guida mostra
  come caricare l'immagine per l'OCR, leggere il testo da una regione e estrarre rapidamente
  il testo da una fattura.
og_title: Estrai testo da immagine – Leggi il testo da una regione con OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Estrai testo dall'immagine – Leggi il testo da una regione con OCR
url: /it/python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da immagine – Leggi testo da regione usando OCR

Hai mai avuto bisogno di **estrarre testo da immagine** ma solo una parte specifica è importante — come l'importo totale su una fattura? Non sei l'unico. In molti progetti reali ti troverai a dover **leggere testo da regione** anziché analizzare l'intera immagine. Fortunatamente, con poche righe di Python puoi caricare un'immagine per OCR, definire una regione di interesse (ROI) e ottenere esattamente i caratteri di cui hai bisogno.

In questo tutorial percorreremo un esempio completo e eseguibile che mostra come **caricare immagine per OCR**, impostare una ROI e infine **estrarre testo da fattura**. Alla fine avrai uno snippet pronto da inserire che funziona con qualsiasi libreria OCR popolare che supporta il riconoscimento basato su regione.

---

## Cosa ti servirà

- Python 3.8+ (il codice funziona anche su 3.10)  
- Un pacchetto OCR che espone una classe `OcrEngine` (per la demo useremo un modulo fittizio `ocr`; sostituiscilo con `pytesseract`, `easyocr` o qualsiasi libreria che offra supporto ROI)  
- Un'immagine di esempio — ad es. `invoice.png` — che contenga testo stampato chiaro  
- Familiarità di base con funzioni e classi Python (non è richiesto un background di deep learning)

Se hai già tutto questo, ottimo — immergiamoci. Altrimenti, scarica l'ultima versione di Python da python.org e installa il pacchetto OCR tramite `pip install your-ocr-lib`.

![Esempio di estrazione testo da immagine](extract-text-from-image.png "Estrai testo da immagine – demo OCR basata su regione")

*L'immagine sopra illustra la regione (rettangolo rosso) che prenderemo di mira per **estrarre testo da immagine**.*

---

## Passo 1: Installa e importa la libreria OCR

Prima di tutto, assicurati che la libreria OCR sia disponibile nel tuo ambiente. Il modello di importazione qui sotto funziona per la maggior parte dei pacchetti che espongono una classe `OcrEngine` di alto livello.

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **Pro tip:** Se stai usando `pytesseract`, dovrai installare il binario Tesseract separatamente e impostare `pytesseract.pytesseract.tesseract_cmd` al suo percorso.

---

## Passo 2: Crea il motore OCR e imposta la lingua

Creare il motore è semplice, ma specificare la lingua migliora notevolmente la precisione, soprattutto per le fatture che contengono numeri e parole in inglese.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

Perché lo facciamo? Il motore OCR utilizza modelli linguistici per prevedere i caratteri; indicargli di aspettarsi l'inglese riduce i falsi positivi, come confondere “0” con “O”.

---

## Passo 3: Carica immagine per OCR

Ora **carichiamo immagine per OCR**. La maggior parte delle librerie accetta un percorso file o un oggetto immagine Pillow. Qui usiamo il loader integrato della libreria per semplicità.

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

Assicurati che il percorso punti alla directory corretta; un errore comune è dimenticare il percorso relativo quando lo script viene eseguito da una directory di lavoro diversa.

---

## Passo 4: Definisci la Regione di Interesse (ROI)

Definire la ROI è il cuore di **leggere testo da regione**. Pensala come disegnare un rettangolo attorno alla parte della fattura che contiene l'importo totale.

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left` e `top` rappresentano le coordinate X e Y dell'angolo superiore sinistro del rettangolo.  
- `width` e `height` impostano le dimensioni della casella.  
- Puoi sperimentare con valori diversi usando un visualizzatore di immagini che mostri le coordinate dei pixel.

> **Perché la ROI è importante:** Eseguire OCR sull'intera pagina spreca cicli CPU e spesso introduce rumore da testo, tabelle o grafiche non pertinenti. Concentrandoti su una regione, ottieni risultati più puliti e una velocità di elaborazione maggiore.

---

## Passo 5: Esegui OCR sulla regione specificata

Con tutto pronto, finalmente **estraiamo testo da immagine** — ma solo all'interno della ROI che abbiamo definito.

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

Il metodo `recognize` restituisce un oggetto che tipicamente contiene la stringa grezza, i punteggi di confidenza e talvolta i riquadri di delimitazione per ogni parola. Per i nostri scopi ci serve solo il testo semplice.

---

## Passo 6: Stampa il testo estratto

Stampiamo il risultato e vediamo cosa otteniamo. Questo passo dimostra **estrarre testo da fattura** in uno scenario reale.

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### Output previsto

```
Text inside ROI:
Total Amount: $1,245.67
```

Se la tua fattura utilizza un layout diverso, vedrai il testo che si trova all'interno del rettangolo — forse un numero di fattura, una data o un riferimento PO.

---

## Passo 7: Raggruppa tutto in una funzione riutilizzabile (opzionale)

Per rendere la soluzione riutilizzabile su più fatture, incapsula la logica in una funzione. Questo illustra anche **ocr on region** come utility generica.

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

Ora puoi chiamare la funzione con qualsiasi fattura:

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

---

## Problemi comuni e come evitarli

| Problema | Perché succede | Soluzione |
|----------|----------------|-----------|
| **Output vuoto** | La ROI non copre effettivamente alcun testo (coordinate errate). | Ricontrolla i valori dei pixel con un editor di immagini; aggiungi un overlay di debug visivo. |
| **Caratteri spazzatura** | Bassa risoluzione dell'immagine o scarsa contrasto. | Pre‑elabora l'immagine: converti in scala di grigi, applica sogliatura (`cv2.threshold`). |
| **Lingua errata** | Il motore usa di default una lingua priva del set di caratteri necessario. | Imposta esplicitamente `ocr_engine.language` a `ENGLISH` o alla locale appropriata. |
| **Ritardo di prestazioni** | Esecuzione di OCR su immagini grandi ripetutamente. | Ridimensiona l'immagine prima del caricamento, o elabora solo la ROI ritagliandola prima. |

---

## Estendere l'esempio: ROI multipli

A volte una fattura contiene diversi campi di cui hai bisogno — come **estrarre testo da fattura** sia per l'importo totale sia per la data della fattura. Puoi iterare su un elenco di rettangoli:

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

Questo schema mantiene il codice pulito e rende facile aggiungere altre regioni in seguito.

---

## Conclusione

Abbiamo appena coperto un flusso di lavoro completo, end‑to‑end, per **estrarre testo da immagine** usando Python OCR, concentrandoci su una regione specifica. **Caricando immagine per OCR**, definendo una **regione di interesse** e invocando il motore, puoi affidabilmente **leggere testo da regione** — perfetto per estrarre totali da fatture, date da ricevute o qualsiasi altro dato localizzato.  

Sentiti libero di sperimentare

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑a‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrai testo da immagine con Aspose OCR – Guida passo‑a‑passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Estrai testo da immagine – Ottimizzazione OCR con Aspose.OCR per .NET](/ocr/english/net/ocr-optimization/)
- [Come estrarre testo da immagine preparando rettangoli in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}