---
category: general
date: 2026-05-31
description: Scopri come utilizzare la regione di interesse OCR per caricare l'immagine
  per l'OCR ed estrarre il testo da un rettangolo, perfetto per riconoscere l'importo
  su una fattura.
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: it
og_description: Padroneggia la regione di interesse OCR per caricare l'immagine per
  l'OCR, estrarre il testo dal rettangolo e riconoscere il testo della fattura in
  un unico tutorial.
og_title: OCR Regione di Interesse – Guida Python Passo‑passo
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  headline: OCR Region of Interest – Extract Text from Rectangle in Python
  type: TechArticle
- description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  name: OCR Region of Interest – Extract Text from Rectangle in Python
  steps:
  - name: Loads an invoice image from disk.
    text: Loads an invoice image from disk.
  - name: Marks a rectangular ROI where the total amount lives.
    text: Marks a rectangular ROI where the total amount lives.
  - name: Runs OCR only inside that ROI.
    text: Runs OCR only inside that ROI.
  - name: Prints the cleaned‑up amount string.
    text: Prints the cleaned‑up amount string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR Regione di Interesse – Estrai il Testo da un Rettangolo in Python
url: /it/python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Region of Interest – Estrarre Testo da Rettangolo in Python

Ti sei mai chiesto come **ocr region of interest** una parte specifica di una fattura scannerizzata senza fornire l'intera pagina al motore? Non sei il primo a fissare una ricevuta sfocata e a pensare: “Come estraggo l'importo che si trova da qualche parte in basso a destra?” La buona notizia è che puoi indicare alla libreria OCR esattamente dove guardare, aumentando notevolmente sia la velocità sia la precisione.

In questa guida percorreremo un esempio completo e eseguibile che ti mostra come **load image for OCR**, definire una **region of interest**, e poi **extract text from rectangle** per infine **recognize text from invoice** e rispondere alla classica domanda “come estrarre l'importo”. Nessun riferimento vago—solo codice concreto, spiegazioni chiare e qualche consiglio professionale che avresti voluto conoscere prima.

---

## Cosa Costruirai

1. Carica un'immagine di fattura dal disco.  
2. Contrassegna un ROI rettangolare dove si trova l'importo totale.  
3. Esegue OCR solo all'interno di quel ROI.  
4. Stampa la stringa dell'importo pulita.  

Tutto questo funziona con qualsiasi libreria OCR che supporta ROI—qui useremo un pacchetto fittizio ma rappresentativo `SimpleOCR` che imita strumenti popolari come Tesseract o EasyOCR. Sentiti libero di sostituirlo; i concetti rimangono gli stessi.

---

## Prerequisiti

- Python 3.8+ installato (`python --version` dovrebbe mostrare ≥3.8).  
- Un pacchetto OCR installabile via pip (es., `pip install simpleocr`).  
- Un'immagine di fattura (PNG o JPEG) collocata in una cartella a cui puoi fare riferimento.  
- Familiarità di base con funzioni e classi Python (nulla di complesso).

Se li hai già, ottimo—tuffiamoci. Altrimenti, procurati prima l'immagine; il resto dei passaggi è indipendente dal contenuto effettivo del file.

---

## Passo 1: Carica Immagine per OCR

La prima cosa di cui ha bisogno qualsiasi flusso di lavoro OCR è una bitmap da cui leggere. La maggior parte delle librerie espone un semplice metodo `load_image` che accetta un percorso file. Ecco come farlo con il nostro motore `SimpleOCR`:

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Pro tip:** Usa percorsi assoluti o `os.path.join` per evitare sorprese “file not found” quando esegui lo script da una directory di lavoro diversa.

---

## Passo 2: Definisci OCR Region of Interest

Invece di far scansionare al motore l'intera pagina, gli diciamo *esattamente* dove si trova l'importo. Questo è il passo **ocr region of interest**, ed è la chiave per un'estrazione affidabile, specialmente quando il documento contiene intestazioni o piè di pagina rumorosi.

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

Perché questi numeri? `x` e `y` sono offset in pixel dall'angolo in alto a sinistra, mentre `width` e `height` descrivono le dimensioni del riquadro. Se non sei sicuro, apri l'immagine in qualsiasi editor, attiva un righello e annota le coordinate. Molti IDE permettono anche di stampare la posizione del cursore al passaggio del mouse.

---

## Passo 3: Estrarre Testo da Rettangolo

Ora che il ROI è impostato, chiediamo al motore di **recognize text from invoice** ma limitato al rettangolo appena aggiunto. La chiamata restituisce un oggetto risultato che tipicamente contiene la stringa grezza, i punteggi di confidenza e talvolta i riquadri di delimitazione.

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

Dietro le quinte, `recognize()` itera su ogni ROI, ritaglia quella porzione, esegue il modello OCR e unisce i risultati. Ecco perché definire una regione **extract text from rectangle** stretta può risparmiare secondi sul tempo di elaborazione per lavori batch.

---

## Passo 4: Come Estrarre l'Importo – Pulire l'Uscita

L'OCR non è perfetto; spesso otterrai spazi superflui, interruzioni di riga o anche caratteri letti erroneamente (pensa a “S” vs “5”). Un rapido `strip()` e una piccola regex di solito risolvono il problema per i valori monetari.

```python
# Step 4: Clean and display the recognized amount
import re

raw_amount = ocr_result.text.strip()
# Simple regex to keep digits, commas, periods, and optional currency symbols
clean_amount = re.search(r'[\d,.]+', raw_amount)
if clean_amount:
    print("Amount:", clean_amount.group())
else:
    print("Could not locate a numeric amount in the ROI.")
```

> **Why this matters:** Se prevedi di inserire l'importo in un database o in un gateway di pagamento, ti serve un formato prevedibile. Rimuovere gli spazi bianchi e filtrare i caratteri non numerici previene errori a valle.

---

## Passo 5: Recognize Text from Invoice – Script Completo

Mettendo tutto insieme, ecco lo script completo, pronto per l'esecuzione. Salvalo come `extract_amount.py` ed esegui `python extract_amount.py`.

```python
# extract_amount.py
import re
from simpleocr import OcrEngine, Rectangle

def main():
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load the invoice image (adjust the path)
    ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

    # Define ROI where the amount is located
    amount_region = Rectangle(120, 340, 200, 40)
    ocr_engine.add_roi(amount_region)

    # Run OCR on the ROI
    ocr_result = ocr_engine.recognize()

    # Clean and print the amount
    raw_amount = ocr_result.text.strip()
    match = re.search(r'[\d,.]+', raw_amount)
    if match:
        print("Amount:", match.group())
    else:
        print("Could not locate a numeric amount in the ROI.")

if __name__ == "__main__":
    main()
```

### Output Atteso

```
Amount: 1,245.67
```

Se il ROI è disallineato, potresti vedere qualcosa come `Amount: 1245.6S`—nota la “S” estranea. Regola le coordinate del rettangolo e riesegui finché l'output non appare pulito.

---

## Problemi Comuni & Casi Limite

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| **ROI troppo piccolo** | Il testo dell'importo viene tagliato, portando a un riconoscimento parziale. | Espandi `width`/`height` del ~10‑20 % e ritesta. |
| **DPI errato** | Scansioni a bassa risoluzione (≤150 dpi) riducono la precisione dell'OCR. | Ricampiona l'immagine a 300 dpi prima del caricamento, o richiedi una DPI più alta allo scanner. |
| **Valute multiple** | La regex prende il primo gruppo numerico, che potrebbe essere il numero della fattura. | Raffina la regex per cercare i simboli di valuta (`$`, `€`, `£`) prima delle cifre. |
| **Fatture ruotate** | I motori OCR assumono testo verticale; le pagine ruotate interrompono il riconoscimento. | Applica una correzione di rotazione (`ocr_engine.rotate(90)`) prima di aggiungere il ROI. |
| **Rumore di sfondo** | Ombre o timbri confondono il modello. | Pre‑processa con una semplice soglia (`cv2.threshold`) o usa un filtro di denoising. |

Affrontare questi casi limite in anticipo ti salva ore di debugging in seguito.

---

## Consigli Pro per Progetti Reali

- **Batch Processing:** Scorri una cartella di fatture, calcola il ROI dinamicamente (es., basato sul rilevamento del modello), e salva i risultati in CSV.  
- **Template Matching:** Se gestisci diversi layout di fatture, mantieni una mappa JSON di `template_id → ROI coordinates`. Cambia il ROI in base a un rapido classificatore di layout.  
- **Parallel Execution:** Usa `concurrent.futures.ThreadPoolExecutor` per eseguire più istanze OCR in parallelo—ideale per pipeline back‑office ad alto volume.  
- **Confidence Filtering:** La maggior parte dei risultati OCR includono un punteggio di confidenza. Scarta i risultati al di sotto di una soglia (es., 85 %) e contrassegnali per revisione manuale.

---

## Conclusione

Abbiamo coperto tutto ciò di cui hai bisogno per **ocr region of interest**, **load image for OCR**, **extract text from rectangle**, e infine **recognize text from invoice** per rispondere alla classica domanda **how to extract amount**. Lo script è compatto, ma sufficientemente flessibile da adattarsi a diversi formati di documento, lingue e back‑end OCR.

Ora che hai padroneggiato le basi, considera di estendere il flusso di lavoro: aggiungere la scansione di codici a barre, integrare un parser PDF, o inviare l'importo estratto a un'API contabile. Il cielo è il limite, e con un ROI ben definito otterrai sempre risultati più rapidi e puliti.

Se incontri un problema, lascia un commento qui sotto—buon OCR!

![ocr region of interest example](https://example.com/ocr_roi_example.png "ocr region of interest example")

## Cosa Dovresti Imparare Dopo?

- [Come Estrarre Testo da Immagine Preparando Rettangoli in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Estrarre Testo da Immagine Java con Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Estrarre Testo da Immagine – Ottimizzazione OCR con Aspose.OCR per .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}