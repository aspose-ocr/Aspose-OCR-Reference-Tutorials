---
category: general
date: 2026-06-28
description: Impara come riconoscere le immagini di testo usando OCR in Python, estrarre
  file PNG di testo e stampare il testo riconosciuto con una gestione degli errori
  robusta.
draft: false
keywords:
- recognize text image
- extract text png
- load image ocr
- process image ocr
- print recognized text
language: it
og_description: Tutorial passo‑passo per riconoscere un'immagine di testo in Python,
  estrarre il testo da PNG e stampare il testo riconosciuto in modo sicuro.
og_title: Riconoscere il testo di un'immagine con Python OCR – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text image using Python OCR, extract text png
    files, and print recognized text with robust error handling.
  headline: recognize text image with Python OCR – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Riconoscere il testo da un'immagine con Python OCR – Guida completa
url: /it/python/general/recognize-text-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# riconoscere immagine di testo con Python OCR – Guida completa

Ti sei mai chiesto come **recognize text image** in uno script Python senza dover includere un framework pesante? Non sei l'unico. Molti sviluppatori hanno bisogno di un modo rapido per *load image OCR* uno screenshot, una ricevuta scansionata o un semplice PNG e ottenere il testo.  

In questo tutorial configureremo un motore OCR minimale, aggiungeremo un logger personalizzato, **load image OCR**, eseguiremo il **process image OCR** e infine **print recognized text**. Alla fine avrai uno script autonomo che può anche **extract text png** file su richiesta.

## Cosa otterrai

- Uno snippet Python completamente funzionale che crea un motore OCR, registra ogni passaggio e gestisce gli errori in modo elegante.  
- Spiegazioni chiare del *perché* ogni riga è importante—così potrai adattare il codice a Tesseract, EasyOCR o qualsiasi altro backend.  
- Suggerimenti per le difficoltà comuni (font mancanti, PNG corrotti) e come eseguirne il debug.  

### Prerequisiti

- Python 3.8+ installato  
- Una libreria OCR che espone una classe `OcrEngine` (l'esempio utilizza un'API fittizia ma tipica; sostituiscila con `pytesseract`, `easyocr`, ecc.).  
- Un'immagine PNG che vuoi analizzare, salvata come `input.png` in una cartella che controlli.  

> **Consiglio professionale:** Se stai usando `pytesseract`, installa prima il binario di sistema Tesseract (`sudo apt install tesseract-ocr` su Linux) e poi `pip install pytesseract pillow`.

---

## ## Riconoscere immagine di testo: Configurare il logger

Un buon logger è l'eroe non celebrato di qualsiasi pipeline OCR. Ti indica *quando* il motore è avviato, *qual* file ha aperto e *perché* potrebbe aver fallito.

```python
# Step 1: Define a simple logger for the OCR engine
def my_logger(level, message):
    """
    level: str – e.g., "INFO", "WARN", "ERROR"
    message: str – human‑readable description of the event
    """
    print(f"[{level}] {message}")
```

*Perché è importante:*  
Il logger separa l'output diagnostico dal core OCR, rendendo facile reindirizzare i log a un file, a un servizio di monitoraggio o anche a un'interfaccia utente in seguito.

---

## ## Caricare immagine OCR: Alimentare il motore con un PNG

Prima che il motore possa **process image OCR**, ha bisogno di un oggetto immagine appropriato. La maggior parte delle librerie accetta un'istanza `Image` di Pillow.

```python
from PIL import Image

# Step 2: Create the OCR engine and attach the logger
ocr_engine = OcrEngine(logging=my_logger)

# Step 3: Load the image to be processed
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Image.from_file(image_path))
my_logger("INFO", f"Loaded image from {image_path}")
```

*Punti chiave:*  

- **load image ocr** – `Image.from_file` astrae i dettagli della decodifica PNG.  
- Mantieni il percorso configurabile; l'hard‑coding rende lo script fragile.  
- La chiamata al logger conferma che l'immagine è stata letta con successo, utile quando il file è mancante o corrotto.

---

## ## Processare immagine OCR: Riconoscere il testo

Ora inizia il lavoro pesante. Il motore scansiona il bitmap, applica le sue reti neurali o euristiche e restituisce una stringa Unicode.

```python
# Step 4: Recognize text from the image
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:
    # Step 5: Handle OCR errors gracefully
    my_logger("ERROR", f"OCR failed with code {e.code}: {e.message}")
    extracted_text = None
```

*Perché lo avvolgiamo in `try/except`:*  
L'OCR può fallire su PNG a bassa risoluzione, spazi colore non supportati o dati di lingua mancanti. Catturare `OcrException` ti permette di **print recognized text** solo quando esiste realmente, evitando tracce di stack criptiche per gli utenti finali.

---

## ## Stampare testo riconosciuto & estrarre testo PNG

Se il riconoscimento ha avuto successo, mostriamo il risultato e opzionalmente lo scriviamo in un file `.txt` che rispecchia il nome del PNG originale.

```python
if extracted_text:
    # Step 6: Print the recognized text
    print("Recognized text:", extracted_text)
    my_logger("INFO", "Printed recognized text to console")

    # Optional: Save extracted text for later use
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
```

*Cosa ottieni:*  

- **print recognized text** – feedback visivo immediato nel terminale.  
- Un file `.txt` affiancato che effettivamente **extract text png** per l'elaborazione a valle (indicizzazione di ricerca, inserimento dati, ecc.).

---

## ## Casi limite comuni & come affrontarli

| Situazione | Sintomo | Soluzione |
|-----------|---------|-----|
| PNG è solo in scala di grigi | OCR restituisce stringa vuota | Converti in RGB (`Image.convert("RGB")`) prima di alimentare il motore. |
| Lingua non supportata | `OcrException` con codice `LANG_NOT_FOUND` | Installa il pacchetto lingua (ad es., `tesseract‑lang‑fra` per il francese) e imposta `ocr_engine.language = "fra"`. |
| Immagine molto grande ( > 5 MB ) | Riconoscimento lento o errore di memoria | Ridimensiona con `image.thumbnail((2000, 2000))` prima di `set_image`. |
| Caratteri inattesi | Output confuso | Assicurati che l'immagine sia davvero PNG; alcuni file si spacciano per PNG ma sono in realtà JPEG. Usa `Image.verify()` per convalidare. |

---

## ## Esempio completo funzionante (pronto per copia‑incolla)

```python
# -*- coding: utf-8 -*-
"""
Complete script to recognize text image using a generic OCR engine.
Replace OcrEngine, OcrException with the concrete classes from your library.
"""

from PIL import Image

# ----------------------------------------------------------------------
# 1️⃣  Logger definition
# ----------------------------------------------------------------------
def my_logger(level: str, message: str) -> None:
    """Simple console logger."""
    print(f"[{level}] {message}")

# ----------------------------------------------------------------------
# 2️⃣  Engine creation & image loading
# ----------------------------------------------------------------------
ocr_engine = OcrEngine(logging=my_logger)   # <- adapt to your library

image_path = "YOUR_DIRECTORY/input.png"
try:
    img = Image.open(image_path)
    img.verify()                     # sanity check the PNG
    img = Image.open(image_path)     # reopen after verify
    ocr_engine.set_image(img)
    my_logger("INFO", f"Loaded image from {image_path}")
except Exception as load_err:
    my_logger("ERROR", f"Failed to load image: {load_err}")
    raise SystemExit(1)

# ----------------------------------------------------------------------
# 3️⃣  Text recognition
# ----------------------------------------------------------------------
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:            # replace with actual exception class
    my_logger("ERROR", f"OCR failed ({e.code}): {e.message}")
    extracted_text = None

# ----------------------------------------------------------------------
# 4️⃣  Output handling
# ----------------------------------------------------------------------
if extracted_text:
    print("Recognized text:", extracted_text)          # ✅ print recognized text
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
else:
    my_logger("WARN", "No text extracted; check image quality.")
```

**Output console previsto (scenario positivo):**

```
[INFO] Loaded image from YOUR_DIRECTORY/input.png
[INFO] OCR succeeded
Recognized text: Invoice #12345
Total Amount: $1,250.00
Date: 2026‑06‑01
[INFO] Saved extracted text to YOUR_DIRECTORY/input.txt
```

Se qualcosa va storto, vedrai una chiara riga `[ERROR]` con il motivo, grazie al logger personalizzato.

---

## ## Prossimi passi & argomenti correlati

- **extract text png** da batch: avvolgi lo script in un ciclo `for` che attraversa un albero di directory.  
- **process image ocr** con pre‑elaborazione (deskew, aumento contrasto) usando OpenCV prima di alimentare il motore.  
- Passa a un servizio OCR cloud (Google Vision, Azure Read) sostituendo l'implementazione `OcrEngine`—il tuo codice circostante rimane lo stesso.  
- Impara come **print recognized text** in PDF usando `reportlab` per la generazione automatica di report.  

## Conclusione

Abbiamo appena illustrato un modo compatto e pronto per la produzione per **recognize text image** in Python, dal caricamento del PNG al **print recognized text** e al salvataggio del risultato. Iniettando un piccolo logger, gestendo le eccezioni e opzionalmente persistendo l'output, lo script è pronto sia per esperimenti rapidi sia per l'integrazione in pipeline più grandi.

Provalo con i tuoi screenshot, sperimenta con la pre‑elaborazione delle immagini, e presto estrarrai testo da qualsiasi PNG tu inserisca. Hai domande? Lascia un commento—buon OCR!

![recognize text image example](placeholder.png)


## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrai testo da immagine con Aspose OCR – Guida passo‑passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Come eseguire l'estrazione di testo da immagine da stream usando Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Converti immagine in testo – Esegui OCR su immagine da URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}