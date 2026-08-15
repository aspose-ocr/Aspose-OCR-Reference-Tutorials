---
category: general
date: 2026-03-28
description: Come eseguire OCR su ROI in Python – Scopri come impostare le opzioni
  di pre‑elaborazione per un'estrazione accurata del testo da regioni specifiche dell'immagine.
draft: false
keywords:
- how to OCR ROI
- how to set preprocessing
- Aspose OCR Python
- ROI extraction
- image preprocessing OCR
language: it
og_description: Come eseguire l'OCR di ROI in Python – Questa guida mostra come impostare
  la preelaborazione per un'estrazione affidabile del testo da regioni d'immagine
  definite.
og_title: Come fare OCR di ROI in Python – Come impostare la pre‑elaborazione
tags:
- OCR
- Python
- Aspose
title: Come fare OCR di ROI in Python – Come impostare la preelaborazione
url: /it/python-java/general/how-to-ocr-roi-in-python-how-to-set-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come fare OCR ROI in Python – Come impostare il preprocessing

Ti sei mai chiesto **come fare OCR ROI** su un’immagine di fattura rumorosa senza caricare l’intera pagina in memoria? Non sei l’unico. In molti progetti reali abbiamo bisogno solo di pochi campi—nome cliente, indirizzo, totali—quindi scansionare l’intero documento è eccessivo.  

La buona notizia? Con Aspose OCR puoi indicare al motore esattamente **dove guardare** e persino chiedergli di pulire l’immagine prima. In questo tutorial vedremo **come impostare le opzioni di preprocessing**, definire le Region of Interest (ROI) e estrarre testo pulito in poche righe di Python.

Alla fine di questa guida avrai uno script pronto all’uso che estrae blocchi specifici da qualsiasi fattura, ricevuta o modulo. Nessuno strumento aggiuntivo necessario, solo Aspose OCR e un po’ di logica Python.

---

## Cosa ti servirà

- **Python 3.8+** (il codice funziona con qualsiasi versione recente)  
- **Aspose OCR for Python via .NET** – installa con `pip install aspose-ocr`  
- Un’immagine di esempio (ad es. `invoice.png`) posizionata in una cartella a cui puoi fare riferimento  
- Familiarità di base con le funzioni Python e la sintassi orientata agli oggetti  

Se hai già tutto questo, ottimo—passiamo subito al codice.

---

![How to OCR ROI diagram](ocr-roi.png "How to OCR ROI example")

*Testo alternativo: diagramma di come fare OCR ROI che mostra le caselle ROI su un’immagine di fattura*

---

## Step 1 – Inizializzare il motore OCR (Come fare OCR ROI)

Prima di poter dire al motore *dove* guardare, ci serve un’istanza del processore OCR. Questo oggetto contiene tutta la configurazione ed esegue il passaggio di riconoscimento.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the engine – this is the entry point for all OCR work
ocr_engine = aocr.OcrEngine()
```

*Perché è importante*: la classe `OcrEngine` astrae il lavoro pesante (rilevamento font, analisi layout, ecc.). Creando un unico motore eviti di reinizializzare risorse pesanti per ogni immagine, mantenendo le prestazioni rapide.

---

## Step 2 – Caricare l’immagine sorgente (Come fare OCR ROI)

Aspose Storage rende il caricamento delle immagini indolore. Indicalo con il percorso del file e otterrai un oggetto `Image` pronto per l’elaborazione.

```python
# Replace YOUR_DIRECTORY with the actual path where invoice.png lives
source_image = storage.Image.load("YOUR_DIRECTORY/invoice.png")
```

*Consiglio*: se lavori con stream (ad es. immagini caricate via API web), puoi passare un oggetto `BytesIO` a `Image.load` invece di un percorso file.

---

## Step 3 – Definire le Region of Interest (ROI)

Ora rispondiamo alla domanda centrale **come fare OCR ROI**: diciamo al motore i rettangoli esatti che contengono i dati di nostro interesse. Ogni ROI è definita dal suo angolo in alto a sinistra (`x`, `y`) e dalle sue dimensioni (`width`, `height`).

```python
from aspose.ocr import Roi

# Each tuple is (x, y, width, height) in pixels
regions_of_interest = [
    Roi(50, 120, 400, 60),   # Customer name block
    Roi(50, 200, 400, 80)    # Address block
]
```

*Perché usare le ROI?*  
- **Velocità** – Il motore ignora le parti irrilevanti dell’immagine.  
- **Precisione** – Concentrandosi su una piccola area, il rumore altrove non può confondere il riconoscitore.  
- **Flessibilità** – Puoi aggiungere quante ROI desideri; il motore restituisce una lista di risultati nello stesso ordine.

---

## Step 4 – Come impostare il preprocessing per una migliore accuratezza OCR

Le immagini provenienti da scanner o telefoni spesso presentano inclinazione, basso contrasto o illuminazione non uniforme. Aspose OCR offre un oggetto `PreprocessingOptions` che consente di attivare correzioni comuni prima dell’esecuzione del riconoscimento.

```python
from aspose.ocr import PreprocessingOptions

preprocessing_options = PreprocessingOptions()
preprocessing_options.deskew = True          # Auto‑rotate tilted text
preprocessing_options.binarize = True        # Convert to black‑white for clarity
preprocessing_options.contrast = 1.5         # Boost contrast (1.0 = no change)
```

*Come aiuta*:  
- **Deskew** rimuove l’inclinazione che rende ambigui i caratteri.  
- **Binarize** riduce il rumore di colore, fornendo al motore OCR un’immagine binaria pulita.  
- **Contrast** amplifica i tratti deboli, particolarmente utile per ricevute sbiadite.

Puoi sperimentare con questi flag—disattiva uno e osserva se l’output cambia. Questo è lo spirito di **come impostare il preprocessing** in modo efficace.

---

## Step 5 – Eseguire OCR solo nelle ROI definite

Con il motore, l’immagine, le ROI e il preprocessing pronti, è il momento di chiamare `recognize`. Il metodo restituisce un oggetto `OcrResult` che contiene una collezione `regions`—ogni voce corrisponde all’ordine delle ROI fornite.

```python
ocr_result = ocr_engine.recognize(
    source_image,
    rois=regions_of_interest,
    preprocessing=preprocessing_options
)
```

*Dietro le quinte*: il motore ritaglia ogni ROI, applica la pipeline di preprocessing e avvia il modello di riconoscimento sul frammento pulito. Poiché abbiamo passato una lista, il risultato mantiene lo stesso ordine, rendendo il post‑processing semplice.

---

## Step 6 – Leggere e utilizzare il testo estratto (Come fare OCR ROI)

Infine, itera sulla lista `regions` e stampa—o salva—le stringhe riconosciute. L’oggetto `Region` espone una proprietà `text` che contiene il risultato Unicode.

```python
for idx, region in enumerate(ocr_result.regions, start=1):
    print(f"Region {idx} text:")
    print(region.text)
    print("-" * 40)
```

**Output previsto (esempio)**:

```
Region 1 text:
John Doe
----------------------------------------
Region 2 text:
123 Maple Street
Springfield, IL 62704
----------------------------------------
```

Se il testo appare confuso, rivedi **come impostare il preprocessing**: magari aumenta `contrast` o disattiva `binarize` per loghi a colori.

---

## Problemi comuni e consigli esperti

| Problema | Perché accade | Correzione (Come impostare il preprocessing) |
|----------|----------------|----------------------------------------------|
| Il testo inclinato appare come spazzatura | `deskew` disabilitato o immagine troppo ruotata | Abilita `preprocessing_options.deskew = True` |
| I numeri diventano punti o segni sparsi | Basso contrasto o binarizzazione aggressiva | Abbassa `contrast` (es. `1.2`) o imposta `binarize = False` |
| Le coordinate ROI sono sfasate di qualche pixel | DPI diverso o scala dello scanner | Usa uno strumento (es. Paint.NET) per misurare le posizioni esatte, o aggiungi un piccolo margine (`+5` pixel) a ogni ROI |
| Risultato vuoto per una regione | ROI fuori dai limiti dell’immagine | Verifica le dimensioni dell’immagine: `source_image.width`, `source_image.height` |

---

## Estendere la soluzione (Come fare OCR ROI in scenari diversi)

- **ROI dinamiche**: se le tue fatture hanno layout variabili, puoi prima eseguire un rapido OCR a pagina intera per individuare parole chiave (“Customer:”, “Address:”) e poi calcolare le ROI al volo.  
- **Elaborazione batch**: avvolgi i passaggi sopra in una funzione e itera su una cartella di immagini. Ricorda di riutilizzare la stessa istanza `ocr_engine` per mantenere basso l’uso di memoria.  
- **Esportazione in JSON**: invece di stampare, costruisci un dizionario e serializzalo con `json.dumps`; questo rende l’integrazione a valle (es. alimentare un ERP) banale.

```python
import json

def extract_invoice_fields(image_path):
    img = storage.Image.load(image_path)
    result = ocr_engine.recognize(
        img,
        rois=regions_of_interest,
        preprocessing=preprocessing_options
    )
    data = {f"field_{i+1}": r.text.strip() for i, r in enumerate(result.regions)}
    return data

print(json.dumps(extract_invoice_fields("invoice.png"), indent=2))
```

---

## Conclusione

Ora disponi di un esempio completo e funzionante che mostra **come fare OCR ROI** in Python mentre domini **come impostare il preprocessing** per la massima accuratezza. Limitando il motore ai rettangoli esatti di tuo interesse e pulendo l’immagine in anticipo, ottieni risultati più rapidi e più puliti—perfetti per l’automazione di fatture, la digitalizzazione di moduli o qualsiasi scenario in cui conta solo una porzione della pagina.

Pronto per il passo successivo? Prova a modificare le coordinate ROI per un tipo di documento diverso, o sperimenta con flag di preprocessing aggiuntivi come `sharpen` o `noise_reduction`. La flessibilità di Aspose OCR ti permette di personalizzare la pipeline per praticamente qualsiasi qualità d’immagine.

Se incontri difficoltà, controlla l’output della console per regioni vuote e rivedi le impostazioni di preprocessing. Buon coding, e che il tuo OCR sia sempre preciso!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}