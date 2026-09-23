---
category: general
date: 2026-01-12
description: Esegui OCR su file PNG rapidamente con Python. Scopri come estrarre testo
  da immagini e fatture e caricare l'immagine per l'OCR usando Aspose.OCR.
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: it
og_description: Esegui OCR su PNG istantaneamente. Questa guida mostra come estrarre
  il testo da un'immagine e da una fattura, caricare l'immagine per l'OCR e salvare
  i risultati in JSON e CSV.
og_title: Esegui OCR su PNG – Tutorial completo di Python
tags:
- OCR
- Python
- Image Processing
title: Esegui OCR su PNG – Guida completa Python per estrarre testo dalle immagini
url: /it/python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su PNG – Guida Completa Python per Estrarre Testo dalle Immagini

Ti è mai capitato di dover **eseguire OCR su file PNG** ma non eri sicuro quale libreria ti avrebbe fornito risultati puliti e strutturati? Non sei solo. In molti progetti reali — pensa all'automazione delle fatture o alla scansione delle ricevute — il primo passo è **estrarre testo da file immagine**, e PNG è un formato comune perché preserva la qualità senza perdita.

In questo tutorial percorreremo un esempio pratico usando il pacchetto Aspose.OCR per Python. Alla fine della guida saprai come **caricare l'immagine per OCR**, estrarre ogni riga di testo, trasformare quei dati in un oggetto JSON ordinato e persino esportarli in CSV per l'elaborazione successiva. Niente superfluo, solo una soluzione pratica e pronta all'uso.

## Cosa Imparerai

- Come installare e importare la libreria Aspose.OCR.  
- I passaggi esatti per **eseguire OCR su PNG** e gestire l'oggetto risultato.  
- Modi per **estrarre testo da fatture** e formattare l'output come JSON o CSV.  
- Suggerimenti per gestire immagini a basso contrasto, documenti multilingua e punteggi di confidenza.  
- Un esempio di codice completo, pronto da copiare e incollare, che puoi eseguire subito.

> **Prerequisito:** Python 3.8+ e una conoscenza di base di pip. Se non hai mai usato Aspose prima, non preoccuparti — questa guida copre tutto ciò di cui hai bisogno per iniziare.

---

## Passo 1 – Installa Aspose.OCR e Prepara il Tuo Ambiente

Prima di poter **eseguire OCR su PNG**, la libreria deve essere presente sul tuo sistema.

```bash
pip install aspose-ocr
```

> **Consiglio Pro:** Usa un ambiente virtuale (`python -m venv venv`) per mantenere le dipendenze isolate. Previene conflitti di versione se gestisci più progetti.

Una volta installata, importa i moduli di cui avremo bisogno:

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

Qui importiamo `asposeocr` per il lavoro pesante e la libreria integrata `json` per la serializzazione successiva.

---

## Passo 2 – Crea il Motore OCR e Imposta la Lingua

Il motore OCR è il componente centrale che legge effettivamente i pixel. Per la maggior parte delle fatture in inglese, vorrai il pacchetto lingua inglese:

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Perché è importante:** Specificare la lingua restringe il set di caratteri, aumentando l'accuratezza e velocizzando l'elaborazione. Se devi gestire fatture multilingua, basta sostituire `ocr.Language.ENGLISH` con l'enumerazione appropriata.

---

## Passo 3 – Carica l'Immagine per OCR

Ora **caricheremo l'immagine per OCR**. Il metodo `Image.load` accetta un percorso file e funziona con PNG, JPEG, BMP e altri formati.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **Caso limite:** Se il PNG è insolitamente grande (oltre 5 MB), considera di ridimensionarlo prima per mantenere un uso della memoria ragionevole. Pillow può farlo in una sola riga:

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

---

## Passo 4 – Esegui OCR su PNG e Cattura il Risultato

Con il motore pronto e l'immagine caricata, è il momento di **eseguire OCR su PNG** e recuperare il risultato strutturato.

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

L'oggetto `ocr_result` contiene una collezione di elementi `OcrRegion`, ognuno con il testo riconosciuto e un punteggio di confidenza (0‑100). Qui ottieni i dati granulari necessari per **estrarre testo da righe di fattura**.

---

## Passo 5 – Converti il Risultato in JSON e Stampalo Formattato

La maggior parte dei sistemi a valle ama JSON, quindi trasformeremo l'output OCR in una stringa ben formattata.

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### Esempio di Output

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

Nota come ogni riga includa una metrica di confidenza — perfetta per filtrare le voci a bassa confidenza se prevedi di **estrarre testo da fattura** automaticamente.

---

## Passo 6 – Salva i Dati OCR come CSV (Una Riga per Testo + Confidenza)

CSV è ideale per fogli di calcolo o importazioni rapide di dati. Aspose offre una singola riga di codice per esportare tutto in un file CSV.

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

Il CSV generato avrà questo aspetto:

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

Ora puoi aprirlo in Excel, Google Sheets o inserirlo in un database.

---

## Bonus – Gestione del Testo a Bassa Confidenza e PDF Multi‑Pagina

### Filtraggio per Confidenza

Se vuoi solo le righe ad alta certezza, filtra il JSON prima di scriverlo:

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### Documenti Multi‑Pagina

Aspose.OCR crea automaticamente una nuova voce `page` per ogni pagina in un PNG o PDF multi‑pagina. Scorri `ocr_data["pages"]` per processarle tutte — nessun codice aggiuntivo necessario.

---

## Esempio Completo Funzionante

Di seguito trovi lo **script completo** che puoi copiare, incollare ed eseguire immediatamente. Sostituisci `YOUR_DIRECTORY` con la cartella che contiene il tuo file PNG.

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

Esegui lo script con `python run_ocr.py` e vedrai il dump JSON nella console, un file CSV su disco e una lista filtrata di voci ad alta confidenza.

---

## Domande Frequenti

**D: Posso usare questo per estrarre testo da una ricevuta scansionata invece di una fattura?**  
R: Assolutamente. Lo stesso flusso di lavoro si applica — basta puntare `image_path` al tuo PNG della ricevuta. Se la ricevuta usa una lingua diversa, cambia `engine.language` di conseguenza.

**D: E se il mio PNG contiene testo ruotato?**  
R: Aspose.OCR rileva automaticamente l'orientamento, ma per i casi più ostinati puoi ruotare manualmente l'immagine con Pillow prima di passarla al motore.

**D: È necessaria una licenza a pagamento per Aspose.OCR?**  
R: La libreria offre una modalità di valutazione gratuita con una filigrana sull'output. Per l'uso in produzione avrai bisogno di una licenza, che puoi ottenere dal sito web di Aspose.

---

## Conclusione

Abbiamo coperto tutto ciò di cui hai bisogno per **eseguire OCR su file PNG** usando Python: installare l'SDK, caricare l'immagine, estrarre testo strutturato e salvare il risultato come JSON o CSV. Che tu voglia **estrarre testo da immagine** per uno script semplice o **estrarre testo da fattura** per una pipeline contabile automatizzata, i passaggi sopra ti forniscono una solida base pronta per la produzione.

Successivamente, potresti esplorare:

- Integrare l'output CSV con un database per l'archiviazione di fatture in blocco.  
- Aggiungere post‑processing con espressioni regolari per estrarre date, importi o codici fiscali.  
- Usare la funzionalità `ocr_engine.recognize_barcode` se le tue fatture includono codici QR.

Provalo, regola le soglie di confidenza e guarda il tuo flusso di lavoro di elaborazione documenti diventare una passeggiata. Hai altre domande o un caso d'uso interessante da condividere? Lascia un commento qui sotto — buona OCR!

![esempio di OCR su PNG](run-ocr-on-png.png "esempio visivo del risultato OCR su PNG")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}