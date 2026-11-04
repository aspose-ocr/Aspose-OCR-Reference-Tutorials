---
category: general
date: 2026-03-28
description: Esegui OCR sull'immagine e ottieni testo pulito con le coordinate delle
  bounding box. Scopri come estrarre l'OCR, pulire l'OCR e visualizzare i risultati
  passo dopo passo.
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: it
og_description: Esegui OCR sull'immagine, pulisci l'output e mostra le coordinate
  del riquadro di delimitazione in un tutorial conciso.
og_title: Esegui OCR sull'immagine – risultati puliti e riquadri
tags:
- OCR
- Computer Vision
- Python
title: Esegui OCR sull'immagine – Risultati puliti e mostra le coordinate del riquadro
  di delimitazione
url: /it/python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine – Pulizia dei Risultati e Visualizzazione delle Coordinate delle Bounding Box

Hai mai dovuto **eseguire OCR su file immagine** ma hai ottenuto testo confuso e non sai dove si trovi ogni parola nella foto? Non sei solo. In molti progetti—digitalizzazione di fatture, scansione di ricevute o semplice estrazione di testo—ottenere l'output grezzo dell'OCR è solo il primo ostacolo. La buona notizia? Puoi pulire quell'output e vedere immediatamente le coordinate della bounding box di ogni regione senza scrivere una montagna di codice boilerplate.

In questa guida vedremo **come estrarre OCR**, eseguire un **come pulire OCR** post‑processore, e infine **visualizzare le coordinate della bounding box** per ogni regione pulita. Alla fine avrai uno script unico, eseguibile, che trasforma una foto sfocata in testo ordinato e strutturato pronto per l'elaborazione successiva.

## Cosa Ti Serve

- Python 3.9+ (la sintassi qui sotto funziona su 3.8 e versioni successive)
- Un motore OCR che supporti `recognize(..., return_structured=True)` – ad esempio, una libreria fittizia `engine` usata nello snippet. Sostituiscila con Tesseract, EasyOCR o qualsiasi SDK che restituisca dati di regione.
- Familiarità di base con funzioni e cicli Python
- Un file immagine che desideri analizzare (PNG, JPG, ecc.)

> **Consiglio:** Se usi Tesseract, la funzione `pytesseract.image_to_data` fornisce già le bounding box. Puoi avvolgere il suo risultato in un piccolo adattatore che imiti l'API `engine.recognize` mostrata qui sotto.

---

![perform OCR on image example](image-placeholder.png "perform OCR on image example")

*Testo alternativo: diagramma che mostra come eseguire OCR su immagine e visualizzare le coordinate delle bounding box*

## Passo 1 – Esegui OCR su Immagine e Ottieni Regioni Strutturate

La prima cosa è chiedere al motore OCR di restituire non solo testo semplice ma un elenco strutturato di regioni di testo. Questo elenco contiene la stringa grezza e il rettangolo che la racchiude.

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**Perché è importante:**  
Quando chiedi solo il testo semplice perdi il contesto spaziale. I dati strutturati ti permettono in seguito di **visualizzare le coordinate della bounding box**, allineare il testo con tabelle o fornire posizioni precise a un modello successivo.

## Passo 2 – Come Pulire l'Output OCR con un Post‑Processore

I motori OCR sono ottimi nel riconoscere i caratteri, ma spesso lasciano spazi superflui, artefatti di interruzioni di riga o simboli riconosciuti erroneamente. Un post‑processore normalizza il testo, corregge gli errori OCR comuni e rimuove gli spazi bianchi inutili.

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

Se costruisci il tuo pulitore, considera:

- Rimuovere i caratteri non‑ASCII (`re.sub(r'[^\x00-\x7F]+',' ', text)`)
- Collassare più spazi in un singolo spazio
- Applicare un correttore ortografico come `pyspellchecker` per errori evidenti

**Perché dovresti interessartene:**  
Una stringa ordinata rende la ricerca, l'indicizzazione e le pipeline NLP successive molto più affidabili. In altre parole, **come pulire OCR** è spesso la differenza tra un dataset utilizzabile e un mal di testa.

## Passo 3 – Visualizza le Coordinate della Bounding Box per Ogni Regione Pulita

Ora che il testo è pulito, iteriamo su ogni regione, stampando il suo rettangolo e la stringa pulita. Questa è la parte in cui finalmente **visualizziamo le coordinate della bounding box**.

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**Output di esempio**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

Ora puoi inserire quelle coordinate in una libreria di disegno (ad es., OpenCV) per sovrapporre le box sull'immagine originale, o salvarle in un database per query successive.

## Script Completo, Pronto‑da‑Eseguire

Di seguito trovi il programma completo che unisce tutti e tre i passaggi. Sostituisci le chiamate placeholder `engine` con il tuo SDK OCR reale.

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### Come Eseguire

```bash
python perform_ocr.py sample_invoice.jpg
```

Dovresti vedere un elenco di bounding box associate al testo pulito, esattamente come l'output di esempio sopra.

## Domande Frequenti & Casi Limite

| Domanda | Risposta |
|----------|----------|
| **E se il motore OCR non supporta `return_structured`?** | Scrivi un wrapper leggero che converta l'output grezzo del motore (di solito un elenco di parole con coordinate) in oggetti con attributi `text` e `bounding_box`. |
| **Posso ottenere i punteggi di confidenza?** | Molti SDK espongono una metrica di confidenza per regione. Aggiungila alla stampa: `print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")`. |
| **Come gestire testo ruotato?** | Pre‑processa l'immagine con `cv2.minAreaRect` di OpenCV per correggere l'inclinazione prima di chiamare `recognize`. |
| **E se ho bisogno dell'output in JSON?** | Serializza `processed_result.regions` con `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)`. |
| **C'è un modo per visualizzare le box?** | Usa OpenCV: `cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)` dentro il ciclo, poi `cv2.imwrite("annotated.jpg", img)`. |

## Conclusione

Hai appena imparato **come eseguire OCR su immagine**, pulire l'output grezzo e **visualizzare le coordinate della bounding box** per ogni regione. Il flusso a tre step—riconoscimento → post‑processo → iterazione—è un modello riutilizzabile che puoi inserire in qualsiasi progetto Python che richieda un'estrazione di testo affidabile.

### Qual è il Prossimo Passo?

- **Esplora diversi back‑end OCR** (Tesseract, EasyOCR, Google Vision) e confronta l'accuratezza.
- **Integra con un database** per memorizzare i dati delle regioni in archivi ricercabili.
- **Aggiungi il rilevamento della lingua** per indirizzare ogni regione al correttore ortografico appropriato.
- **Sovrapponi le box sull'immagine originale** per una verifica visiva (vedi lo snippet OpenCV sopra).

Se incontri stranezze, ricorda che il maggior vantaggio deriva da un solido passo di post‑processing; una stringa pulita è molto più facile da gestire rispetto a un dump grezzo di caratteri.

Buon coding, e che le tue pipeline OCR siano sempre ordinate!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}