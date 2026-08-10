---
category: general
date: 2026-06-25
description: Estrai il testo da un'immagine usando OCR in Python. Scopri come caricare
  l'immagine per l'OCR, eseguire l'OCR in Python e convertire lo scontrino in JSON
  in pochi semplici passaggi.
draft: false
keywords:
- extract text from image
- load image for OCR
- perform OCR in Python
- convert receipt to JSON
language: it
og_description: Estrai il testo da un'immagine usando OCR in Python. Questo tutorial
  ti guida attraverso il caricamento di un'immagine per l'OCR, l'esecuzione dell'OCR
  in Python e la conversione di una ricevuta in JSON.
og_title: Estrai testo da immagine in Python – Guida completa all'OCR
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  headline: Extract Text from Image in Python – Full OCR Guide
  type: TechArticle
- description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  name: Extract Text from Image in Python – Full OCR Guide
  steps:
  - name: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
    text: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
  - name: '**Load an image for OCR** – tell the engine which file to read.'
    text: '**Load an image for OCR** – tell the engine which file to read.'
  - name: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
    text: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
  - name: '**Run the recognition** – actually perform OCR in Python.'
    text: '**Run the recognition** – actually perform OCR in Python.'
  - name: '**Print or store the result** – convert receipt to JSON and see the output.'
    text: '**Print or store the result** – convert receipt to JSON and see the output.'
  - name: Sends the image through a pre‑trained convolutional network.
    text: Sends the image through a pre‑trained convolutional network.
  - name: Decodes the network output into readable characters.
    text: Decodes the network output into readable characters.
  - name: Packages everything into the selected format (JSON in our case).
    text: Packages everything into the selected format (JSON in our case).
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- JSON
title: Estrai testo da un'immagine in Python – Guida completa all'OCR
url: /it/python/general/extract-text-from-image-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai Testo da Immagine in Python – Guida Completa OCR

Ti è mai capitato di dover **estrarre testo da immagine** ma non sapevi da dove cominciare? In questo tutorial ti guideremo passo passo su come **caricare un'immagine per OCR**, **eseguire OCR in Python** e **convertire la ricevuta in JSON**—tutto con poche righe di codice.

Se hai mai costruito un'app di scansione ricevute, un tracciatore di spese, o semplicemente vuoi automatizzare l'inserimento dati, vedrai perché padroneggiare questo flusso è un vero punto di svolta. Alla fine avrai uno script funzionante che legge una foto di una ricevuta e restituisce un payload JSON pulito pronto per i servizi a valle.

## Cosa Imparerai

Copriremo ogni passaggio, dall'installazione della libreria `aocr` alla gestione del risultato grezzo. In particolare imparerai a:

1. **Crea un'istanza del motore OCR** – il punto di ingresso per tutti i lavori di riconoscimento.  
2. **Carica un'immagine per OCR** – indica al motore quale file leggere.  
3. **Scegli il formato di esportazione** – JSON o XML, sceglieremo JSON perché è più facile da consumare.  
4. **Esegui il riconoscimento** – effettua realmente l'OCR in Python.  
5. **Stampa o salva il risultato** – converti la ricevuta in JSON e visualizza l'output.

Non è necessaria alcuna esperienza pregressa con l'OCR; basta un'installazione base di Python e un file immagine (una ricevuta, un volantino, quello che ti serve).  

---

![Diagramma che mostra il flusso di estrazione del testo da immagine usando Python OCR](extract-text-from-image-python-ocr.png){alt="Diagramma che mostra il flusso di estrazione del testo da immagine usando Python OCR"}

## Estrai Testo da Immagine – OCR Python Passo‑per‑Passo

Di seguito trovi lo script completo, pronto per l'esecuzione. Sentiti libero di copiarlo in un file chiamato `receipt_ocr.py` e di eseguirlo con `python receipt_ocr.py`.

```python
# receipt_ocr.py

# 1️⃣ Import the aocr package (make sure it's installed via `pip install aocr`)
import aocr

# 2️⃣ Create an OCR engine instance – this object orchestrates the whole process
engine = aocr.OcrEngine()

# 3️⃣ Load the image you want to process.
#    Replace the path with the location of your receipt or any image.
engine.load_image("YOUR_DIRECTORY/receipt.png")

# 4️⃣ Choose the output format. JSON is handy for APIs and downstream services.
engine.export_format = aocr.ExportFormat.JSON

# 5️⃣ Run the recognition and obtain the raw result.
json_result = engine.recognize()

# 6️⃣ Output the raw JSON string – you can also write it to a file if you prefer.
print(json_result)
```

### Perché Funziona

- **Istanza del motore** – `aocr.OcrEngine()` incapsula tutto il lavoro pesante (caricamento del modello, pre‑elaborazione, ecc.).  
- **Caricamento dell'immagine** – `engine.load_image()` indica alla libreria esattamente quale bitmap analizzare; è possibile fornire JPEG, PNG o anche PDF multi‑pagina.  
- **Formato di esportazione** – Impostare `engine.export_format` a `aocr.ExportFormat.JSON` rende il risultato una stringa strutturata, perfetta per le API che si aspettano JSON.  
- **Chiamata di riconoscimento** – `engine.recognize()` esegue l'inferenza della rete neurale dietro le quinte; restituisce una stringa JSON che contiene i blocchi di testo rilevati, i punteggi di confidenza e le informazioni sul layout.  

---

## Carica Immagine per OCR con aocr

Se ti chiedi se l'immagine necessiti di qualche pre‑elaborazione speciale, la risposta breve è **no**—`aocr` gestisce automaticamente la maggior parte dei casi comuni (regolazione del contrasto, correzione dell'inclinazione). Tuttavia, puoi migliorare l'accuratezza:

- Assicurarsi che l'immagine sia almeno a 300 dpi.  
- Ritagliare i bordi irrilevanti.  
- Convertire in scala di grigi prima di caricarla (opzionale, `engine.load_image()` lo farà per te).

```python
# Optional preprocessing example using Pillow
from PIL import Image, ImageOps

original = Image.open("YOUR_DIRECTORY/receipt.png")
# Convert to grayscale and increase contrast
processed = ImageOps.autocontrast(original.convert("L"))
processed.save("processed_receipt.png")
engine.load_image("processed_receipt.png")
```

*Consiglio professionale:* Se la ricevuta contiene molto rumore, il passaggio extra sopra può aumentare la precisione del **perform OCR in Python** di un margine notevole.

---

## Scegli il Formato di Esportazione e Converti la Ricevuta in JSON

Potresti chiederti: “Perché non ottenere semplicemente il testo plain?” Perché JSON preserva la struttura gerarchica (righe, parole, bounding box). Questo rende molto più semplice mappare campi come *importo totale* o *data* in seguito.

```python
engine.export_format = aocr.ExportFormat.JSON   # Switch to XML with aocr.ExportFormat.XML if needed
```

Quando esegui lo script, `json_result` avrà un aspetto simile a questo (troncato per brevità):

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "bbox": [12, 34, 210, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.96,
          "bbox": [15, 400, 190, 420]
        }
      ]
    }
  ]
}
```

Ora disponi di un payload **convert receipt to JSON** che puoi inviare direttamente a un database, a un endpoint REST o a un modello di machine‑learning.

---

## Esegui il Riconoscimento e Recupera i Risultati

L'ultimo passaggio—eseguire realmente l'OCR—è semplice come chiamare `recognize()`. Dietro le quinte la libreria:

1. Invia l'immagine attraverso una rete convoluzionale pre‑addestrata.  
2. Decodifica l'output della rete in caratteri leggibili.  
3. Imballa tutto nel formato selezionato (JSON nel nostro caso).  

```python
json_result = engine.recognize()
print(json_result)   # <-- This prints the JSON string to stdout
```

Se devi salvare l'output invece di stamparlo, scrivilo semplicemente su un file:

```python
with open("receipt_output.json", "w", encoding="utf-8") as f:
    f.write(json_result)
```

*Caso limite:* Alcune ricevute contengono caratteri non‑ASCII (ad esempio “€”). Assicurati di aprire il file con codifica UTF‑8, come mostrato sopra, per evitare testo corrotto.

---

## Esempio Completo (Tutti i Passaggi in Un Solo Script)

Riunendo tutto, ecco lo script finale che puoi eseguire end‑to‑end:

```python
import aocr
from PIL import Image, ImageOps

# Create engine
engine = aocr.OcrEngine()

# Optional: preprocess image for better accuracy
raw = Image.open("YOUR_DIRECTORY/receipt.png")
processed = ImageOps.autocontrast(raw.convert("L"))
processed.save("processed_receipt.png")

# Load the (processed) image
engine.load_image("processed_receipt.png")

# Choose JSON output
engine.export_format = aocr.ExportFormat.JSON

# Run OCR
json_result = engine.recognize()

# Save result
with open("receipt_output.json", "w", encoding="utf-8") as out_file:
    out_file.write(json_result)

print("OCR complete! JSON saved to receipt_output.json")
```

Eseguilo con:

```bash
python receipt_ocr.py
```

Dovresti vedere una riga di conferma e, nella stessa cartella, un file `receipt_output.json` contenente i dati strutturati.

---

## Conclusione

Ora sai **come estrarre testo da immagine** usando Python, come **caricare un'immagine per OCR**, come **eseguire OCR in Python** e come **convertire la ricevuta in JSON** per il consumo a valle. Questo flusso end‑to‑end è leggero, richiede solo il pacchetto `aocr` e può essere inserito in qualsiasi pipeline di automazione.

Qual è il prossimo passo? Prova a cambiare il formato di esportazione in XML, sperimenta diverse tecniche di pre‑elaborazione dell'immagine, o costruisci una piccola API Flask che accetti una ricevuta caricata e restituisca immediatamente il payload JSON. Il cielo è il limite una volta che hai le basi.

Hai domande o hai incontrato un problema? Lascia un commento qui sotto, e buon coding!

## Cosa Dovresti Imparare Dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑per‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrai Testo da Immagine con Aspose OCR – Guida Passo‑per‑Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Estrai Testo da Immagine – Ottimizzazione OCR con Aspose.OCR per .NET](/ocr/english/net/ocr-optimization/)
- [Come estrarre una tabella da immagine usando Aspose.OCR per .NET](/ocr/english/net/text-recognition/recognize-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}