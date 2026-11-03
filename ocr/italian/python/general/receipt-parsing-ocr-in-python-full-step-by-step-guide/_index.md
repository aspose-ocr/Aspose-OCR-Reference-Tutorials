---
category: general
date: 2026-06-28
description: Parsing di ricevute con OCR in Python reso semplice – impara come estrarre
  i dati della ricevuta, caricare l'OCR dell'immagine e vedere un esempio completo
  di OCR in Python.
draft: false
keywords:
- receipt parsing OCR
- how to extract receipt
- python ocr example
- load image ocr
- how to ocr receipt
language: it
og_description: 'OCR per l''analisi delle ricevute in Python: impara come estrarre
  i dati della ricevuta, caricare l''OCR dell''immagine e eseguire un esempio completo
  di OCR in Python in pochi minuti.'
og_title: Parsing di ricevute OCR in Python – Guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Receipt parsing OCR in Python made easy – learn how to extract receipt
    data, load image OCR, and see a complete python OCR example.
  headline: Receipt Parsing OCR in Python – Full Step‑By‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- receipt parsing
- image processing
title: Parsing di ricevute OCR in Python – Guida completa passo passo
url: /it/python/general/receipt-parsing-ocr-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Receipt Parsing OCR in Python – Guida completa passo‑passo

Ti sei mai chiesto come trasformare una ricevuta sfocata del supermercato in un JSON pulito e ricercabile? **Receipt parsing OCR** è la risposta, e non ti serve un dottorato in computer vision per farlo funzionare. In questo tutorial percorreremo un **python ocr example** pratico che carica un'immagine, esegue il riconoscimento di testo strutturato e restituisce una stringa JSON ben formattata—perfetta da alimentare in un software di contabilità o in pipeline di analisi.

Risponderemo anche alla domanda più pressante: **how to extract receipt** dati in modo affidabile, anche quando la scansione non è perfetta. Alla fine avrai uno script riutilizzabile da inserire in qualsiasi progetto Python, sia che tu stia costruendo un'app di finanze personali o un sistema di tracciamento spese di livello enterprise.

## Cosa imparerai

* Come configurare un motore OCR leggero in Python.
* I passaggi esatti per **load image OCR** per un file di ricevuta.
* Come invocare un metodo di riconoscimento strutturato e trasformare il risultato in JSON.
* Suggerimenti per gestire casi limite comuni—ricevute ruotate, basso contrasto e caratteri Unicode.
* Un esempio di codice completo, pronto per copia‑incolla, che puoi eseguire subito.

### Prerequisiti

* Python 3.8 o versioni successive installato sulla tua macchina.  
* Una libreria OCR che fornisce una classe `OcrEngine` e un helper `Image` (molte librerie espongono API simili; per lo scopo di questa guida assumeremo un wrapper generico).  
* Un'immagine di ricevuta (`receipt.png`) posizionata in una cartella a cui puoi fare riferimento.  
* Opzionale ma consigliato: `pip install pillow` per la gestione delle immagini e qualsiasi dipendenza aggiuntiva richiesta dalla tua libreria OCR.

Se ti manca qualcuno di questi, installalo subito—senza problemi, è una singola riga per la maggior parte dei pacchetti.

---

## Receipt Parsing OCR – Passo 1: Installa e importa i moduli richiesti

Prima di tutto, prepariamo l'ambiente Python. Importeremo `json` per la serializzazione e le classi specifiche dell'OCR.

```python
# Step 1: Import required modules
import json                     # Built‑in JSON handling
from ocr_library import OcrEngine, Image   # Replace with your actual library
```

*Perché è importante*: Importare all'inizio mantiene lo script ordinato e garantisce che il motore OCR sia disponibile in tutto il codice. Se dimentichi di importare `json`, la chiamata `json.dumps` più avanti genererà un `NameError`.

**Suggerimento**: Se la tua libreria OCR si trova sotto uno spazio dei nomi diverso (ad esempio `easyocr` o `pytesseract`), adatta la riga di importazione di conseguenza. Il resto del tutorial rimane invariato.

---

## How to Extract Receipt Data – Passo 2: Crea l'istanza del motore OCR

Ora avviamo il motore. Pensa a `OcrEngine()` come al cervello che leggerà la ricevuta.

```python
# Step 2: Create an OCR engine instance
engine = OcrEngine()
```

La maggior parte dei moderni OCR SDK consente di configurare pacchetti linguistici o modalità di rilevamento qui. Per una tipica ricevuta vorrai l'inglese (o la lingua della ricevuta) e una modalità “structured” se disponibile.

> **Nota**: Se la tua libreria richiede una chiave di licenza, passala come argomento: `engine = OcrEngine(api_key="YOUR_KEY")`.

## Load Image OCR – Passo 3: Punta il motore verso la tua ricevuta

Con il motore pronto, dobbiamo fornirgli il file immagine. È qui che entra in gioco **load image OCR**.

```python
# Step 3: Load the image to be processed
engine.set_image(Image.from_file("YOUR_DIRECTORY/receipt.png"))
```

*Cosa sta succedendo*: `Image.from_file` legge il PNG (o JPG, TIFF, ecc.) e lo avvolge in un formato che il motore OCR comprende. Se la tua ricevuta è un PDF, converti prima la prima pagina in immagine—molte librerie forniscono un helper `pdf2image`.

**Caso limite**: Le ricevute scansionate capovolte saranno comunque leggibili se le ruoti:

```python
# Optional: auto‑rotate if needed
image = Image.from_file("YOUR_DIRECTORY/receipt.png")
image = image.rotate(180) if image.is_upside_down() else image
engine.set_image(image)
```

## How to OCR Receipt – Passo 4: Esegui il riconoscimento di testo strutturato

Ora avviene la magia. Chiediamo al motore di eseguire una scansione strutturata, che tenta di raggruppare articoli, totali e date.

```python
# Step 4: Perform structured text recognition
result = engine.recognize_structured()
```

Se la tua libreria OCR offre solo un metodo semplice `recognize()`, puoi comunque estrarre i campi manualmente, ma `recognize_structured()` restituisce spesso un dizionario con chiavi come `items`, `total` e `date`.

## Python OCR Example – Passo 5: Converti il risultato in JSON

L'oggetto risultato grezzo è solitamente una classe personalizzata. Convertirlo in un semplice dict Python lo rende facile da serializzare.

```python
# Step 5: Convert the recognition result to a nicely formatted JSON string
json_str = json.dumps(result.to_dict(), ensure_ascii=False, indent=2)
```

*Perché `ensure_ascii=False`?* Le ricevute possono contenere simboli di valuta (€, £) o caratteri accentati. Questa opzione li preserva invece di convertirli in escape `\u00e9`.

## How to Extract Receipt – Passo 6: Output della rappresentazione JSON

Infine, stampiamo (o scriviamo) il JSON così puoi inviarlo a un database, a un foglio di calcolo o a un'API.

```python
# Step 6: Output the JSON representation of the recognized data
print(json_str)
```

**Output previsto** (formattato per leggibilità):

```json
{
  "merchant": "Coffee House",
  "date": "2024-03-15",
  "items": [
    {"name": "Latte", "quantity": 1, "price": "3.50"},
    {"name": "Bagel", "quantity": 2, "price": "4.00"}
  ],
  "subtotal": "7.50",
  "tax": "0.60",
  "total": "8.10"
}
```

Se vedi un dict vuoto o campi mancanti, ricontrolla che l'immagine della ricevuta sia chiara e che il motore OCR sia impostato sulla lingua corretta.

---

## Suggerimenti professionali e problemi comuni (Sezione bonus)

| Problema | Perché succede | Soluzione rapida |
|----------|----------------|------------------|
| **Immagine sfocata o a basso contrasto** | L'OCR ha difficoltà con il rumore | Preprocessare con OpenCV: `cv2.threshold` o `cv2.bilateralFilter` |
| **Ricevuta ruotata** | Il motore assume testo verticale | Rileva l'orientamento con `engine.detect_orientation()` o ruota manualmente (vedi Passo 3) |
| **Caratteri non latini** | Pacchetto lingua errato | Inizializza il motore con `language="spa"` per lo spagnolo, ecc. |
| **Ricevute grandi causano errore di memoria** | L'intera immagine viene caricata tutta in una volta | Ritaglia la regione di interesse: `engine.set_image(image.crop((x, y, w, h)))` |

## Cosa fare dopo? Estendi il flusso di lavoro

Hai appena padroneggiato **receipt parsing OCR** in Python. Ecco alcune idee per mantenere lo slancio:

* **Batch processing** – itera su una cartella di immagini di ricevute e aggiungi ogni JSON a un file master.  
* **Database insertion** – usa `sqlite3` o `SQLAlchemy` per memorizzare ogni ricevuta come una riga.  
* **Machine‑learning enrichment** – fornisci gli elementi estratti a un modello di categorizzazione per l'etichettatura delle spese.  

Tutti questi si basano sui passaggi fondamentali che abbiamo coperto, e ciascuno utilizzerà lo stesso modello **python ocr example**: load → recognize → serialize → store.

## Conclusione

In questa guida abbiamo percorso un flusso di lavoro completo **receipt parsing OCR** in Python, mostrando esattamente **how to extract receipt** informazioni, come **load image OCR**, e fornendo un **python ocr example** funzionale che puoi eseguire oggi. Seguendo i sei passaggi—install, import, instantiate, load, recognize e serialize—ora hai una solida base per qualsiasi progetto di elaborazione di ricevute.

Sentiti libero di sperimentare: prova diversi motori OCR, modifica il preprocessing o aggiungi la gestione degli errori per i campi mancanti. Il cielo è il limite quando combini un OCR affidabile con la flessibilità di Python. Hai domande o un'idea interessante su questa ricetta? Lascia un commento qui sotto e continuiamo la conversazione.

Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}