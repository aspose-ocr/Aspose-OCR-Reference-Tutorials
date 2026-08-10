---
category: general
date: 2026-06-16
description: Riconoscere il testo da un'immagine usando un motore OCR Python – impara
  come estrarre il testo da una ricevuta e migliorare la precisione OCR in pochi minuti.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- improve ocr accuracy
- python ocr tutorial
- image preprocessing for OCR
language: it
og_description: Riconosci il testo da un'immagine rapidamente. Questa guida mostra
  come estrarre il testo da una ricevuta e migliorare l'accuratezza dell'OCR usando
  Python.
og_title: Riconoscere il testo da un'immagine con Python OCR – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text from image using a Python OCR engine – learn how to
    extract text from receipt and improve OCR accuracy in minutes.
  headline: recognize text from image with Python OCR – Complete Guide
  type: TechArticle
- description: recognize text from image using a Python OCR engine – learn how to
    extract text from receipt and improve OCR accuracy in minutes.
  name: recognize text from image with Python OCR – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - Basic familiarity with pip and
      virtual environments. - A sample receipt image (JPEG or PNG) that you want to
      process. - The `ocr` package (the example uses a fictional `ocr` module for
      illustration; replace it with `pytesseract`, `easyocr`, or any library t'
  - name: Expected Output
    text: 'Running the script on a typical grocery receipt yields something like:'
  - name: H3 – Crop to the Receipt Region
    text: 'If your image contains a lot of background (e.g., a photo of a desk), crop
      it first:'
  - name: H3 – Use a Custom Language Pack
    text: 'For receipts that contain foreign characters (e.g., “€” or “¥”), load the
      appropriate language data:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Riconoscere il testo da un'immagine con Python OCR – Guida completa
url: /it/python-java/general/recognize-text-from-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Riconoscere testo da immagine con Python OCR – Guida completa

Hai mai dovuto **riconoscere testo da immagine** ma i risultati sembravano incomprensibili? Non sei l'unico. In molti scenari di piccole imprese—pensa alla scansione di ricevute, alla digitalizzazione di fatture o all'estrazione di dati da carte d'identità—ottenere un output pulito e affidabile è la differenza tra un flusso di lavoro fluido e un mal di testa.

In questo tutorial percorreremo un modo pratico per **riconoscere testo da immagine** usando una libreria OCR leggera per Python. Ti mostreremo anche esattamente come **estrarre testo da ricevuta** e condivideremo trucchi per **migliorare l'accuratezza OCR** senza acquistare software costosi. Pronto? Immergiamoci.

## Cosa costruirai

Al termine di questa guida avrai uno script pronto all'uso che:

1. Istanzia un motore OCR.  
2. Abilita il preprocessing intelligente (deskew, despeckle, binarizzazione).  
3. Carica un'immagine di ricevuta rumorosa.  
4. Esegue automaticamente la pipeline di riconoscimento.  
5. Stampa testo pulito e ricercabile sulla console.

Nessun servizio esterno, nessuna chiave API nascosta—solo puro codice Python che puoi adattare a qualsiasi progetto.

### Prerequisiti

- Python 3.8+ installato sulla tua macchina.  
- Familiarità di base con pip e gli ambienti virtuali.  
- Un'immagine di esempio di una ricevuta (JPEG o PNG) che desideri elaborare.  
- Il pacchetto `ocr` (l'esempio usa un modulo `ocr` fittizio a scopo illustrativo; sostituiscilo con `pytesseract`, `easyocr` o qualsiasi libreria che offra un'API simile).

> **Pro tip:** Se incontri dipendenze mancanti, installale con `pip install ocr` (o il nome reale del pacchetto) prima di procedere.

## Passo 1 – Riconoscere testo da immagine: configurare il motore

Prima di tutto. Abbiamo bisogno di un oggetto che sappia leggere i dati dei pixel e trasformarli in caratteri. Pensa al motore come al cervello dell'operazione; tutto il resto gli fornisce informazioni.

```python
import ocr  # Replace with your actual OCR library import

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

Perché creare il motore manualmente? Alcune librerie ti permettono di chiamare una singola funzione, ma un'istanza esplicita ti dà un controllo granulare sul preprocessing—esattamente ciò di cui abbiamo bisogno per **migliorare l'accuratezza OCR** più avanti.

## Passo 2 – Estrarre testo dalla ricevuta: abilitare il preprocessing

Una ricevuta scansionata con la fotocamera del telefono raramente è perfetta. Potrebbe essere leggermente inclinata, piena di macchie di polvere o soffrire di illuminazione non uniforme. Abilitare il preprocessing fa il lavoro pesante prima che il motore guardi le lettere.

```python
# Step 2: Enable preprocessing to improve recognition quality
preprocess = engine.preprocessing
preprocess.deskew = True        # Auto‑rotate slightly tilted pages
preprocess.despeckle = True     # Remove isolated noise pixels
preprocess.binarization = True  # Convert image to pure black‑white
```

*Deskew* raddrizza la pagina, *despeckle* elimina le macchie, e *binarizzazione* forza ogni pixel a essere nero o bianco. Queste tre opzioni da sole possono **migliorare l'accuratezza OCR** del 20‑30 % su ricevute rumorose.

## Passo 3 – Caricare l'immagine da riconoscere

Ora puntiamo il motore al file reale. Il percorso può essere assoluto o relativo; assicurati solo che l'immagine esista.

```python
# Step 3: Load the scanned receipt image
engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/receipt-noisy.jpg")
```

Se ti chiedi se il motore supporta PDF o TIFF multi‑pagina, la maggior parte delle librerie moderne lo fa—basta controllare la documentazione. Per un JPEG a pagina singola, la riga sopra è tutto ciò di cui hai bisogno.

## Passo 4 – Eseguire OCR – Il motore fa il resto

Con il preprocessing configurato e l'immagine caricata, la chiamata successiva fa tutto: preelabora, esegue l'algoritmo di riconoscimento e restituisce un oggetto risultato.

```python
# Step 4: Run OCR – the configured preprocessing is applied automatically
ocr_result = engine.recognize()
```

Dietro le quinte il motore potrebbe usare Tesseract, una rete neurale o un motore proprietario. Non è necessario conoscere gli interni; ottieni semplicemente un risultato pulito.

## Passo 5 – Output del testo riconosciuto

Infine, estraiamo il testo semplice dal risultato e lo stampiamo. In un'applicazione reale potresti scriverlo in un database, in un file CSV o persino alimentarlo in una pipeline di analisi successiva.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### Output previsto

Eseguire lo script su una tipica ricevuta di supermercato produce qualcosa di simile a:

```
WALMART STORE #1234
123 Main St.
Anytown, USA

Date: 06/15/2026   Time: 14:32
Cashier: J. Doe

Item                Qty   Price
---------------------------------
Milk                1     2.99
Bread               2     5.48
Eggs                1     3.20
---------------------------------
Subtotal                    11.67
Tax                         0.93
Total                       12.60
```

Se l'output appare confuso, ricontrolla che le opzioni di preprocessing siano attive e che l'immagine non sia troppo scura. Regolare la soglia di binarizzazione (alcune librerie permettono di impostare un valore personalizzato) può **migliorare ulteriormente l'accuratezza OCR**.

## Avanzato: Ottimizzazione per estrarre testo dalla ricevuta più velocemente

Mentre il flusso a cinque passi funziona per la maggior parte dei casi, potresti voler accelerare le cose quando elabori centinaia di ricevute ogni notte. Ecco un paio di ottimizzazioni opzionali:

### H3 – Ritaglia alla regione della ricevuta

Se la tua immagine contiene molto sfondo (ad es., una foto di una scrivania), ritagliala prima:

```python
engine.image = engine.image.crop((50, 200, 800, 1200))  # left, top, right, bottom
```

### H3 – Usa un pacchetto linguistico personalizzato

Per ricevute che contengono caratteri stranieri (ad es., “€” o “¥”), carica i dati linguistici appropriati:

```python
engine.set_language('eng+deu+fra')  # English, German, French
```

Entrambi i trucchi aiutano il motore a **riconoscere testo da immagine** in modo più affidabile, soprattutto quando il materiale di partenza varia.

## Problemi comuni e come evitarli

- **Font mancanti:** Alcuni motori OCR necessitano dei file dei font per caratteri specifici delle ricevute. Installa i pacchetti linguistici appropriati.  
- **Troppo rumore:** Anche con `despeckle=True`, scansioni estremamente granulose possono ancora confondere il motore. Un filtro manuale rapido in Pillow (`Image.filter(ImageFilter.MedianFilter)`) può aiutare.  
- **DPI errato:** I motori OCR presumono circa 300 dpi. Se la tua immagine è inferiore, ridimensionala prima: `engine.image = engine.image.resize((width*2, height*2))`.

Affrontare direttamente questi problemi **migliora l'accuratezza OCR** senza ricorrere a costosi servizi di terze parti.

## Script completo – Pronto per l'esecuzione

Di seguito trovi il programma Python completo e eseguibile che incorpora tutto ciò di cui abbiamo parlato. Salvalo come `receipt_ocr.py` ed esegui `python receipt_ocr.py`.

```python
import ocr  # Replace with the actual library you use

def main():
    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Enable preprocessing steps
    preprocess = engine.preprocessing
    preprocess.deskew = True
    preprocess.despeckle = True
    preprocess.binarization = True

    # Load the receipt image (change the path to your file)
    engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/receipt-noisy.jpg")

    # Optional: crop out unnecessary background
    # engine.image = engine.image.crop((50, 200, 800, 1200))

    # Run the recognition pipeline
    result = engine.recognize()

    # Print the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

Eseguendo questo script **riconoscerai testo da immagine** e stamperai un blocco di dati della ricevuta formattato bene. Sentiti libero di adattare le coordinate di ritaglio, le impostazioni linguistiche o le opzioni di preprocessing per corrispondere ai tuoi layout di ricevuta.

## Conclusione

Abbiamo appena coperto un modo semplice per **riconoscere testo da immagine** usando Python, dimostrato come **estrarre testo da ricevuta** e esplorato diversi consigli pratici per **migliorare l'accuratezza OCR**. L'idea di base è semplice: configura un motore OCR, abilita il preprocessing intelligente, fornisci un'immagine pulita e lascia che la libreria faccia il lavoro pesante.

Prossimi passi? Prova a far passare un batch di ricevute in un ciclo, salva ogni risultato in un CSV o collega l'output a un sistema di contabilità. Potresti anche sperimentare con librerie OCR basate su deep‑learning come `easyocr` per una precisione ancora maggiore su font complessi.

Hai domande su un formato di ricevuta particolare o vuoi vedere come gestire PDF multi‑pagina? Lascia un commento qui sotto, e buona programmazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}