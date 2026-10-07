---
category: general
date: 2026-01-02
description: Scopri come raddrizzare le immagini e aumentare il contrasto per ottenere
  rapidamente testo semplice. Include codice Python passo‑passo e consigli per l'estrazione
  del testo.
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: it
og_description: Come correggere l'inclinazione di un'immagine e aumentare il contrasto
  per ottenere testo semplice. Esempio completo in Python con estrazione di tabelle
  e accelerazione GPU.
og_title: Come raddrizzare l'immagine – Tutorial completo OCR su GPU
tags:
- OCR
- Python
- Image Processing
title: Come raddrizzare l'immagine – Guida OCR accelerata da GPU
url: /it/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come correggere l'inclinazione di un'immagine – Guida OCR accelerata da GPU

Ti sei mai chiesto **come correggere l'inclinazione di un'immagine** quando le tue ricevute arrivano con un angolo strano? Non sei solo; una foto inclinata può trasformare una ricevuta perfettamente leggibile in un caos confuso. La buona notizia è che, con poche righe di Python, puoi auto‑correggere l'inclinazione, aumentare il contrasto e ottenere testo pulito—niente Photoshop manuale.

In questo tutorial percorreremo un esempio completo e eseguibile che non solo **mostra come correggere l'inclinazione di un'immagine**, ma dimostra anche **come aumentare il contrasto**, **come ottenere testo semplice** e persino **come estrarre testo** da tabelle che il motore OCR rileva. Alla fine avrai uno script autonomo da inserire in qualsiasi progetto.

## Cosa ti servirà

- Python 3.9+ installato (il codice usa type hints, quindi un interprete recente è consigliato)
- La libreria `ocr` che fornisce `OcrEngine`, `EngineMode`, `ImageProcessingOptions` e `OcrResult` (installa via `pip install ocr‑sdk` – sostituisci con il nome reale del pacchetto che usi)
- Una GPU con driver compatibili se vuoi la spinta di velocità (opzionale ma consigliata)
- Un file immagine leggermente ruotato o a basso contrasto, ad esempio `receipt_skewed.jpg`

> **Consiglio esperto:** Se non hai una GPU, basta cambiare `EngineMode.GPU` in `EngineMode.CPU` e lo script funziona comunque—solo un po' più lento.

## Implementazione passo‑passo

Di seguito suddividiamo la soluzione in blocchi logici. Ogni blocco ha un **H2** descrittivo che contiene la parola chiave principale *come correggere l'inclinazione di un'immagine* o una delle parole chiave secondarie. Il codice è completo, commentato e pronto per l'esecuzione.

### Come correggere l'inclinazione di un'immagine con OCR accelerato da GPU

La prima cosa che facciamo è dire al motore OCR di girare sulla GPU e abilitare la funzione di auto‑correzione dell'inclinazione. L'auto‑correzione analizza la geometria dell'immagine e la ruota nuovamente in posizione verticale.

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **Perché è importante:** L'accelerazione GPU può ridurre il tempo di elaborazione da secondi a millisecondi, cosa cruciale quando gestisci decine di ricevute al minuto.

### Aumentare il contrasto dell'immagine per un riconoscimento migliore

Una ricevuta a basso contrasto è un incubo per qualsiasi sistema OCR. Aumentando il contrasto diamo al motore bordi più chiari con cui lavorare.

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **Come aumentare il contrasto:** Il metodo `set_contrast_boost` accetta una percentuale; il 30 % è un valore predefinito sicuro che funziona per la maggior parte delle ricevute scansionate. Se le tue immagini sono estremamente scure, alzalo al 50 % o sperimenta.

### Ottenere testo semplice dall'immagine elaborata

Ora che l'immagine è dritta e luminosa, la inviamo al motore e chiediamo il risultato in testo semplice.

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**Output atteso** (troncato per brevità):

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **Come ottenere testo semplice:** Il metodo `get_text()` rimuove qualsiasi informazione di layout e restituisce una stringa pulita, che puoi poi memorizzare in un database, inviare a un'API o alimentare a un'analisi successiva.

### Come estrarre testo da tabelle rilevate

Spesso le ricevute contengono dati tabulari (articoli, quantità, prezzi). L'SDK OCR può rilevare le tabelle e permetterti di iterare su righe e celle.

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**Esempio di output tabella**:

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **Perché estrarre le tabelle:** I dati strutturati rendono banale calcolare totali, generare report o alimentarli a un software di contabilità.

### Script completo funzionante

Mettendo tutto insieme, ecco lo script che puoi copiare‑incollare in `deskew_and_ocr.py`:

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

Eseguilo con:

```bash
python deskew_and_ocr.py
```

Dovresti vedere il testo pulito e le eventuali tabelle rilevate stampate sulla console.

## Casi limite comuni e come gestirli

| Situazione | Cosa fare |
|------------|-----------|
| **L'immagine è capovolta** | Aumenta la fiducia di `set_auto_deskew(True)` chiamando anche `set_rotation_correction(True)` se l'SDK lo supporta. |
| **L'aumento del contrasto rende l'immagine troppo luminosa** | Riduci la percentuale passata a `set_contrast_boost` (ad es., 15 %). |
| **GPU non disponibile** | Passa da `EngineMode.GPU` a `EngineMode.CPU`; il resto della pipeline rimane invariato. |
| **Le tabelle non vengono rilevate** | Prova una scansione a risoluzione più alta o abilita `set_table_detection(True)` se la libreria lo fornisce. |

## Prossimi passi: dal testo semplice ai dati strutturati

Ora che sai **come correggere l'inclinazione di un'immagine**, **come aumentare il contrasto** e **come ottenere testo semplice**, potresti voler:

- Analizzare il testo semplice con espressioni regolari per estrarre coppie chiave‑valore (es., `total`, `date`).
- Memorizzare i risultati in un database SQLite o PostgreSQL per report futuri.
- Collegare lo script a una funzione serverless (AWS Lambda, Azure Functions) per processare gli upload automaticamente.

Tutte queste estensioni si basano sulla stessa fondazione trattata qui.

## Conclusione

Abbiamo percorso **come correggere l'inclinazione di un'immagine** usando un motore OCR accelerato da GPU, dimostrato **come aumentare il contrasto** per un riconoscimento più nitido, mostrato esattamente **come ottenere testo semplice** e persino coperto **come estrarre testo** da tabelle. Lo script completo e eseguibile lega tutto insieme, così puoi inserirlo in qualsiasi progetto Python e iniziare subito a estrarre dati puliti da foto inclinate e a basso contrasto.

Provalo con alcune delle tue ricevute, regola il livello di contrasto e lascia che l'OCR faccia il lavoro pesante. Se incontri stranezze, torna alla tabella dei casi limite sopra—la maggior parte dei problemi si risolve con una piccola regolazione.

Buona programmazione, e che le tue immagini siano sempre dritte e luminose!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}