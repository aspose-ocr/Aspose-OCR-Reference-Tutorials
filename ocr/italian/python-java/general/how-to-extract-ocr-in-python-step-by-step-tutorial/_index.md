---
category: general
date: 2026-04-26
description: come estrarre OCR da immagini usando Python – un esempio di OCR in Python
  che mostra come caricare un'immagine per l'OCR ed estrarre il testo da una ricevuta.
draft: false
keywords:
- how to extract ocr
- python ocr example
- extract text from receipt
- load image for ocr
- how to use OCR
language: it
og_description: come estrarre OCR da immagini usando Python. Impara un esempio di
  OCR in Python, carica l'immagine per l'OCR e estrai il testo da una ricevuta in
  pochi minuti.
og_title: Come estrarre OCR in Python – Guida completa
tags:
- OCR
- Python
- Image Processing
title: come estrarre OCR in Python – tutorial passo‑a‑passo
url: /it/python-java/general/how-to-extract-ocr-in-python-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# come estrarre OCR in Python – Guida completa

Ti sei mai chiesto **come estrarre OCR** da una ricevuta sfocata o da una fattura scansionata? Non sei l'unico: gli sviluppatori si scontrano continuamente con il problema quando hanno bisogno di testo pulito, leggibile da macchine, dalle immagini. La buona notizia? Con poche righe di Python puoi trasformare una foto di una ricevuta in testo ad alta fiducia e ricercabile.

In questo tutorial percorreremo un **esempio python OCR** che dimostra **come caricare immagine per OCR**, eseguire il motore e conservare solo i caratteri che superano una soglia di fiducia dell'85 %. Alla fine sarai in grado di **estrarre testo da ricevuta** immagini senza dover setacciare la documentazione o indovinare i parametri dell'API.

## Cosa ti serve

- Python 3.9 o più recente (la sintassi che usiamo funziona su 3.8+)
- Il pacchetto `aocr` (o qualsiasi libreria OCR che fornisce una classe `OcrEngine`). Installalo con:

```bash
pip install aocr
```

- Un'immagine di esempio di una ricevuta (`receipt.png`) posizionata in una cartella a cui puoi fare riferimento.
- Un editor di testo o IDE—VS Code, PyCharm, o anche un semplice notebook.

Questo è tutto. Nessun framework pesante, nessun servizio esterno, solo puro Python.

![Risultato OCR ad alta fiducia – come estrarre OCR da una ricevuta](/images/ocr-high-confidence.png)

*Testo alternativo dell'immagine: come estrarre OCR da una ricevuta usando Python OCR*

## Passo 1 – Crea l'istanza del motore OCR (come estrarre OCR)

La prima cosa che facciamo è avviare un motore OCR. Pensalo come il cervello che leggerà i pixel per noi.

```python
# Step 1: Initialize the OCR engine
from aocr import OcrEngine

ocr_engine = OcrEngine()
```

**Perché?** L'istanziazione di `OcrEngine` ti fornisce un nuovo oggetto di configurazione. Puoi successivamente modificare i modelli linguistici, le impostazioni DPI o i passaggi di pre‑elaborazione—tutto senza toccare il ciclo di elaborazione principale.

## Passo 2 – Carica l'immagine per OCR

Successivamente indirizziamo il motore verso l'immagine che vogliamo analizzare. È qui che entra in gioco la keyword **carica immagine per OCR**.

```python
# Step 2: Load the receipt image
image_path = "YOUR_DIRECTORY/receipt.png"
ocr_engine.image = OcrEngine.Image.load(image_path)
```

> **Consiglio professionale:** Se la tua immagine si trova in una directory diversa, usa `os.path.join` per costruire un percorso indipendente dalla piattaforma.

**Perché caricare l'immagine in questo modo?** L'helper `Image.load` legge il file in un formato che il motore comprende, gestendo automaticamente i formati comuni (PNG, JPEG, TIFF). Saltare questo passaggio o fornire byte grezzi genererebbe un `ValueError`.

## Passo 3 – Esegui il processo OCR

Ora eseguiamo effettivamente l'OCR. Il metodo `process` restituisce un ricco oggetto risultato contenente i simboli riconosciuti, i punteggi di fiducia e le bounding box.

```python
# Step 3: Execute OCR and capture the result
ocr_result = ocr_engine.process()
```

**Cosa contiene `ocr_result`?** Nella maggior parte delle librerie include:

- `text`: la stringa grezza concatenata.
- `symbol_confidences`: una lista di tuple `(char, confidence)`.
- `boxes`: coordinate per ogni carattere (utile per il debug visivo).

Avere accesso alla fiducia per carattere è essenziale per il passo successivo.

## Passo 4 – Conserva solo i simboli ad alta fiducia (≥ 85 %)

Una ricevuta spesso presenta sbavature, stampa tenue o rumore di fondo. Filtrando i simboli a bassa fiducia miglioriamo notevolmente l'analisi successiva.

```python
# Step 4: Filter out low‑confidence characters
high_confidence_text = ''.join(
    char for char, confidence in ocr_result.symbol_confidences
    if confidence >= 0.85
)
```

**Perché 85 %?** Empiricamente, una soglia intorno a 0,85 bilancia richiamo e precisione per la maggior parte delle ricevute stampate. Se noti numeri mancanti, abbassa la soglia; se ottieni spazzatura, alzala.

## Passo 5 – Output del testo estratto ad alta fiducia

Infine, stampiamo (o salviamo) la stringa sanitizzata. Questo è il cuore del nostro flusso di lavoro **estrarre testo da ricevuta**.

```python
# Step 5: Show the cleaned result
print("High‑confidence text:", high_confidence_text)
```

L'output tipico appare così:

```
High‑confidence text: Store XYZ
Date: 2024‑04‑22
Total: $23.45
```

Ora puoi inserire questa stringa in un writer CSV, un database o qualsiasi pipeline di analisi successiva.

## Script completo, pronto da eseguire

Di seguito trovi lo snippet di codice completo che puoi copiare‑incollare in `ocr_receipt.py` ed eseguire immediatamente.

```python
# ocr_receipt.py
# A complete python ocr example that extracts high‑confidence text from a receipt.

from aocr import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the image you want to analyze
    image_path = "YOUR_DIRECTORY/receipt.png"
    ocr_engine.image = OcrEngine.Image.load(image_path)

    # 3️⃣ Run the OCR process
    ocr_result = ocr_engine.process()

    # 4️⃣ Keep only symbols with confidence ≥ 85%
    high_confidence_text = ''.join(
        char for char, confidence in ocr_result.symbol_confidences
        if confidence >= 0.85
    )

    # 5️⃣ Output the result
    print("High‑confidence text:", high_confidence_text)

if __name__ == "__main__":
    main()
```

Salva il file, assicurati che `receipt.png` esista, ed esegui:

```bash
python ocr_receipt.py
```

Dovresti vedere il testo pulito della ricevuta stampato sulla console.

## Casi limite e scenari “what‑if”

| Situazione | Soluzione suggerita |
|-----------|----------------------|
| **Fiducia molto bassa su tutta l'immagine** | Pre‑elabora l'immagine: aumenta il contrasto, converti in scala di grigi o applica un filtro di denoising (`cv2.GaussianBlur`). |
| **Caratteri non latini** | Passa un modello linguistico a `OcrEngine` (ad es., `ocr_engine.language = "spa"` per lo spagnolo). |
| **Più ricevute in una sola immagine** | Esegui l'OCR sull'intera immagine, poi dividi il risultato usando espressioni regolari che rilevano `\n\n+` (doppi ritorni a capo). |
| **Necessità del testo OCR grezzo** | Mantieni `ocr_result.text` accanto alla versione filtrata per il debug. |

Queste variazioni assicurano che la tua conoscenza **come usare OCR** si estenda oltre il caso più semplice.

## Errori comuni (e come evitarli)

- **Dimenticare di installare la libreria** – `pip install aocr` deve riuscire prima di importare.
- **Usare il separatore di percorso sbagliato** su Windows (`\` vs `/`). Usa `os.path.join`.
- **Hard‑codare la soglia di fiducia** senza test – esegui sempre un rapido controllo visivo su alcune ricevute prima.
- **Ignorare la normalizzazione Unicode** – alcune ricevute contengono caratteri di trattino speciali; esegui `unicodedata.normalize('NFKC', text)` se prevedi di memorizzare l'output.

## Prossimi passi – Oltre le basi

Ora che sai **come estrarre OCR** da una singola ricevuta, potresti voler:

1. **Processare in batch una cartella di ricevute** – iterare su tutti i file PNG/JPG e scrivere ogni risultato in un CSV.
2. **Integrare con un database** – memorizzare `high_confidence_text` in SQLite per ricerche rapide.
3. **Applicare il parsing di linguaggio naturale** – usa regex o `dateutil` per estrarre date, totali e importi fiscali.
4. **Sperimentare con librerie alternative** – `pytesseract`, `easyocr`, o servizi cloud (Google Vision, Azure OCR) se hai bisogno di supporto multilingue o maggiore accuratezza.

Ciascuno di questi argomenti incorpora naturalmente le nostre parole chiave secondarie: *python ocr example*, *extract text from receipt*, *load image for ocr*, e *how to use OCR*.

## Conclusione

Abbiamo appena percorso un **python ocr example** completo che mostra **come estrarre OCR** da un'immagine di ricevuta, filtrare i simboli a bassa fiducia e produrre risultati puliti. I passaggi sono semplici, il codice è autonomo e l'approccio è sufficientemente flessibile da adattarsi a progetti più grandi.

Provalo con le tue ricevute, regola la soglia di fiducia e poi scala al batch processing. Se incontri stranezze—come un logo tenue o un font insolito—ricorda i consigli per i casi limite sopra. Buon coding, e che le tue pipeline OCR siano sempre accurate!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}