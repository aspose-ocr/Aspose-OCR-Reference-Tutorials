---
category: general
date: 2026-01-12
description: Come eseguire OCR rapidamente e con precisione. Impara a eseguire OCR
  su un documento, estrarre testo da un TIFF, caricare un'immagine per OCR e impostare
  la lingua OCR in Python.
draft: false
keywords:
- how to perform ocr
- run ocr on document
- extract text from tiff
- load image for ocr
- set OCR language
language: it
og_description: Come eseguire OCR in Python. Questo tutorial ti mostra come eseguire
  OCR su un documento, estrarre testo da un file TIFF, caricare un'immagine per l'OCR
  e impostare la lingua dell'OCR.
og_title: Come eseguire l'OCR su un documento TIFF – Guida completa
tags:
- OCR
- Python
- Image Processing
title: Come eseguire l'OCR su un documento TIFF – Guida passo passo
url: /it/python-java/general/how-to-perform-ocr-on-a-tiff-document-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR su un documento TIFF – Guida completa

Ti sei mai chiesto **come eseguire OCR** su un file TIFF scansionato senza passare ore a cercare la libreria giusta? Non sei solo. Molti sviluppatori si trovano in difficoltà quando devono estrarre testo da immagini TIFF, soprattutto quando le prestazioni e le impostazioni della lingua sono importanti.

In questo tutorial ti guideremo attraverso tutto ciò che devi sapere: dall'installazione del pacchetto OCR, al caricamento dell'immagine per l'OCR, alla impostazione della lingua OCR, fino a **eseguire OCR sul documento** e ottenere testo pulito. Alla fine avrai uno script pronto‑all'uso che potrai inserire in qualsiasi progetto.

> **Consiglio professionale:** Sebbene l'esempio utilizzi un modulo generico `ocr`, gli stessi concetti si applicano a Tesseract, EasyOCR o a qualsiasi motore OCR moderno che espone un'API Python.

---

## Cosa ti servirà

- Python 3.8+ (qualsiasi versione recente va bene)
- Una libreria OCR che fornisce una classe `OcrEngine` (l'esempio usa un pacchetto fittizio `ocr`; sostituiscilo con quello reale)
- Un file TIFF multi‑pagina che vuoi elaborare (lo chiameremo `big_document.tif`)
- Una macchina con almeno 4 core CPU se prevedi di impostare il numero di thread

Nessun servizio esterno, nessuna chiave cloud—solo codice locale che si esegue in pochi secondi.

![esempio di come eseguire OCR](/images/ocr-example.png "come eseguire OCR su un documento TIFF")

*Testo alternativo dell'immagine: come eseguire OCR su un documento TIFF – anteprima del testo estratto.*

---

## Passo 1: Installa e importa la libreria OCR

Prima di tutto: porta la libreria sul tuo computer. La maggior parte dei pacchetti OCR è su PyPI, quindi un semplice `pip install` fa al caso tuo.

```bash
pip install ocr‑engine   # replace with the actual package name, e.g., pytesseract
```

Ora importa le classi di cui avrai bisogno. Se usi Tesseract, la riga di importazione sarà diversa, ma il resto del codice rimane invariato.

```python
# Step 1: Import the OCR engine and image helper
import ocr                       # fictional package – swap with your real one
from ocr import OcrEngine, Image
```

*Perché è importante:* Importare i simboli corretti fin dall'inizio previene conflitti di namespace in seguito e rende lo script più leggibile.

---

## Passo 2: Crea e configura il motore OCR (Imposta lingua OCR)

Configurare il motore è il punto in cui **imposti la lingua OCR** per un riconoscimento accurato. L'inglese è il valore predefinito, ma puoi passare al francese, tedesco o anche alla modalità multilingue con una sola riga.

```python
# Step 2: Initialize the engine and set language
ocr_engine = OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # set OCR language to English
ocr_engine.set_thread_count(4)               # limit processing to 4 CPU cores
ocr_engine.set_memory_limit(512 * 1024 * 1024)  # 512 MB internal buffer
```

> **Perché 4 thread?** La maggior parte dei laptop moderni ha almeno quattro core, e limitare il numero di thread impedisce al processo OCR di monopolizzare l'intera macchina—particolarmente utile quando lo script viene eseguito su un server condiviso.

Se ti serve un'altra lingua, basta sostituire `ocr.Language.ENGLISH` con `ocr.Language.FRENCH`, `ocr.Language.SPANISH`, ecc.

---

## Passo 3: Carica immagine per OCR (Carica immagine per OCR)

Ora **carichiamo l'immagine per OCR**. Il metodo `Image.load` legge il file TIFF in memoria, gestendo automaticamente i documenti multi‑pagina.

```python
# Step 3: Load the TIFF image you want to process
image_path = "YOUR_DIRECTORY/big_document.tif"
image = Image.load(image_path)   # load image for OCR
```

*Caso limite:* Se il file è enorme, potresti esaurire la RAM. In tal caso, considera di caricare una pagina alla volta con `Image.load_page(page_number)` (se la libreria lo supporta).

---

## Passo 4: Esegui OCR sul documento

Con il motore pronto e l'immagine caricata, è il momento di **eseguire OCR sul documento**. Il metodo `process` esegue il lavoro pesante e restituisce un oggetto risultato.

```python
# Step 4: Execute OCR
ocr_result = ocr_engine.process(image)
```

Dietro le quinte il motore suddivide l'immagine in blocchi di testo, esegue il modello di riconoscimento e unisce i risultati. La chiamata è bloccante, il che significa che lo script attende fino a quando l'intero TIFF è stato elaborato—perfetto per lavori batch.

---

## Passo 5: Estrai testo dal TIFF e verifica l'output

Infine, **estraiamo il testo dal TIFF** accedendo all'attributo `text` del risultato. Stampiamo i primi 200 caratteri come rapido controllo di coerenza.

```python
# Step 5: Show a preview of the recognized text
preview = ocr_result.text[:200]   # first 200 characters
print("Preview of OCR output:\n", preview)
```

**Output atteso (esempio):**

```
Preview of OCR output:
 In the United States, the Constitution guarantees the ...
```

Se ti serve il testo completo, usa semplicemente `ocr_result.text`. Per l'elaborazione successiva potresti volerlo scrivere in un file `.txt`:

```python
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(ocr_result.text)
```

---

## Esempio completo funzionante

Mettendo tutto insieme, ecco uno script pronto‑all'uso. Sostituisci il nome del pacchetto segnaposto con quello che hai effettivamente installato.

```python
# -*- coding: utf-8 -*-
"""
How to Perform OCR on a TIFF Document – Complete Example
"""

# Install the OCR library first:
# pip install ocr-engine   # adjust to your actual package

import ocr
from ocr import OcrEngine, Image

def main():
    # 1️⃣ Initialize and configure the engine
    engine = OcrEngine()
    engine.language = ocr.Language.ENGLISH
    engine.set_thread_count(4)
    engine.set_memory_limit(512 * 1024 * 1024)

    # 2️⃣ Load the TIFF image
    img_path = "YOUR_DIRECTORY/big_document.tif"
    img = Image.load(img_path)

    # 3️⃣ Run OCR on the loaded image
    result = engine.process(img)

    # 4️⃣ Show a short preview and save the full text
    print("First 200 chars of OCR output:")
    print(result.text[:200])

    with open("extracted_text.txt", "w", encoding="utf-8") as out_file:
        out_file.write(result.text)

    print("\n✅ Extraction complete – see 'extracted_text.txt' for full output.")

if __name__ == "__main__":
    main()
```

Esegui lo script con:

```bash
python ocr_tiff_example.py
```

Dovresti vedere un'anteprima stampata sulla console e un file chiamato `extracted_text.txt` contenente la trascrizione completa.

---

## Domande frequenti e casi limite

- **E se il TIFF contiene più pagine?**  
  La maggior parte dei motori OCR tratta ogni pagina come un'immagine separata internamente. `ocr_result.text` conterrà un newline tra le pagine. Se ti serve una gestione per pagina, itera con `Image.load_page(page_number)`.

- **Posso elaborare un PNG o JPEG invece di TIFF?**  
  Assolutamente. Il metodo `Image.load` di solito accetta qualsiasi formato supportato da Pillow o dalla libreria sottostante. Basta cambiare l'estensione del file.

- **Il mio testo è illeggibile—devo cambiare lingua?**  
  Sì. Il passaggio **imposta lingua OCR** è cruciale per documenti non‑inglesi. Assicurati che il pacchetto lingua sia installato (ad esempio, `tesseract‑lang‑fra` per il francese).

- **Esaurisco la memoria?**  
  Riduci il `set_memory_limit` o elabora le pagine una per una. Alcuni motori permettono anche di ridimensionare l'immagine prima del riconoscimento.

---

## Conclusione

Ecco fatto—una guida concisa e completamente funzionale su **come eseguire OCR** su un file TIFF usando Python. Abbiamo coperto tutto, dall'installazione della libreria, alla configurazione del motore (incluso **imposta lingua OCR**), **carica immagine per OCR**, **esegui OCR sul documento**, e infine **estrai testo dal TIFF**.  

Sentiti libero di sperimentare: modifica il conteggio dei thread, cambia lingua, o alimenta l'output OCR in una pipeline di linguaggio naturale. Il cielo è il limite una volta che hai padroneggiato le basi.

Hai altre domande? Lascia un commento qui sotto, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}