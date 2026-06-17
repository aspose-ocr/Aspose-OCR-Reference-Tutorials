---
category: general
date: 2026-03-18
description: Come usare l'OCR per estrarre testo dalle immagini – una guida rapida
  per riconoscere il testo da file PNG e caricare le immagini per l'OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- how to extract text
- load image for OCR
language: it
og_description: Come usare l'OCR per estrarre testo dalle immagini – impara a riconoscere
  il testo da PNG, caricare l'immagine per l'OCR e estrarre il testo con un semplice
  script Python.
og_title: 'Come usare l''OCR: estrarre testo dalle immagini in Python'
tags:
- OCR
- Python
- Image Processing
title: 'Come utilizzare l''OCR: estrarre testo dalle immagini in Python'
url: /it/python-java/general/how-to-use-ocr-extract-text-from-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare OCR: Estrarre testo dalle immagini in Python

Ti sei mai chiesto **come usare OCR** quando hai uno screenshot confuso o una ricevuta scansionata? Non sei solo—gli sviluppatori hanno costantemente bisogno di estrarre testo leggibile dalle immagini, soprattutto PNG provenienti da app mobili o caricamenti web. In questo tutorial ti guideremo attraverso un esempio completo e eseguibile che mostra come **estrarre testo da immagine**, **riconoscere testo da PNG** e persino **caricare immagine per OCR** con poche righe di Python.

Copriremo tutto, dall'installazione della libreria corretta alla gestione di documenti multilingue, così alla fine saprai esattamente *come estrarre testo* da qualsiasi immagine che sottoponi al motore. Nessun riferimento vago, solo una soluzione chiara, passo‑per‑passo, che puoi copiare‑incollare ed eseguire.

## Cosa imparerai

1. Configurare un motore OCR leggero (senza dipendenze ingombranti).  
2. Caricare un file immagine—specificamente un PNG—nel motore.  
3. Abilitare il rilevamento automatico della lingua affinché il motore gestisca contenuti multilingue.  
4. Eseguire il processo di riconoscimento e recuperare il risultato in testo semplice.  
5. Ottimizzare il flusso di lavoro per casi limite come file mancanti o formati non supportati.

Se ti trovi a tuo agio con Python di base, sei pronto. Non è necessaria esperienza pregressa con OCR, anche se dare un'occhiata veloce alla documentazione della libreria non guasta mai.

---

![Come usare OCR su un'immagine PNG](placeholder.png "Come usare OCR su un'immagine PNG – guida passo‑passo")

## Come usare OCR – Carica immagine e riconosci testo {#how-to-use-ocr}

### Passo 1: Installa la libreria OCR

Prima di tutto, ti serve un pacchetto Python che fornisce una classe `OcrEngine`. Per questo tutorial useremo il pacchetto fittizio ma illustrativo **SimpleOCR**, che puoi installare via pip:

```bash
pip install simple-ocr
```

> **Consiglio:** Se lavori in un ambiente virtuale (altamente consigliato), attivalo prima di eseguire il comando di installazione. Questo mantiene ordinate le dipendenze del tuo progetto.

### Passo 2: Importa il motore e crea un'istanza

Creare il motore è semplice come chiamare il suo costruttore. Considera il motore come il “cervello” che in seguito elaborerà l'immagine che gli fornirai.

```python
# Step 2: Import and instantiate the OCR engine
from simple_ocr import OcrEngine

# Create a fresh engine instance – this allocates internal buffers
engine = OcrEngine()
```

Perché creiamo una nuova istanza ogni volta? Per isolamento. Un motore nuovo garantisce che nessuno stato residuo di un'esecuzione precedente contamini il riconoscimento corrente, il che è cruciale quando elabori molti file in batch.

### Passo 3: Carica l'immagine da elaborare

Ora carichiamo effettivamente **load image for OCR**. Il metodo `setImageFromFile` accetta un percorso a qualsiasi immagine raster; lo indirizzeremo a un PNG chiamato `mixed_doc.png`.

```python
# Step 3: Load the PNG image you want to read
image_path = "YOUR_DIRECTORY/mixed_doc.png"
engine.setImageFromFile(image_path)
```

Se il file non viene trovato, `SimpleOCR` solleva un chiaro `FileNotFoundError`. Puoi catturarlo per fornire un messaggio di errore amichevole:

```python
try:
    engine.setImageFromFile(image_path)
except FileNotFoundError:
    print(f"❗️ Unable to locate '{image_path}'. Check the path and try again.")
    raise
```

### Passo 4: Abilita il rilevamento automatico della lingua

La maggior parte dei motori OCR moderni include pacchetti linguistici. Passando `"multilingual"` indichiamo al motore di analizzare il testo e scegliere automaticamente il modello linguistico corretto. Questo è particolarmente utile quando il tuo PNG contiene un mix di inglese e spagnolo, per esempio.

```python
# Step 4: Turn on auto‑language detection (covers all installed packs)
engine.setLanguage("multilingual")
```

Se conosci la lingua in anticipo, puoi sostituire `"multilingual"` con un locale specifico come `"eng"` o `"spa"` per velocizzare l'elaborazione.

### Passo 5: Esegui il processo di riconoscimento

Il lavoro pesante avviene qui. `recognize()` scansiona l'immagine, applica la segmentazione, esegue la rete neurale e costruisce internamente un buffer di testo.

```python
# Step 5: Execute OCR – this may take a moment for large images
engine.recognize()
```

Dietro le quinte il motore esegue:

- **Pre‑processing** (raddrizzamento, binarizzazione)  
- **Layout analysis** (rilevamento di colonne, tabelle)  
- **Character classification** (utilizzando un modello di deep‑learning)

Tutto ciò è astratto, ed è per questo che ti basta una sola riga.

### Passo 6: Recupera e stampa il testo riconosciuto

Infine, recuperiamo l'oggetto risultato ed estraiamo la stringa semplice. Questa è la parte in cui effettivamente **extract text from image**.

```python
# Step 6: Get the OCR result and display the plain text
result = engine.getResult()
text = result.getText()
print("📝 Recognized Text:\n")
print(text)
```

**Output previsto** (troncato per brevità):

```
📝 Recognized Text:

Invoice #12345
Date: 2026‑03‑15
Total: $89.99
Thank you for your purchase!
```

Se l'immagine non contiene caratteri riconoscibili, `text` sarà una stringa vuota. Puoi proteggerti da ciò:

```python
if not text.strip():
    print("⚠️ No text detected – try a higher‑resolution image or adjust preprocessing.")
```

---

## Estrarre testo da immagine – Gestire casi limite comuni

### Più lingue in un unico file

Quando un documento mescola lingue, l'impostazione `"multilingual"` di solito funziona correttamente. Tuttavia, se noti riconoscimenti errati, puoi specificare manualmente una lista di fallback:

```python
engine.setLanguage(["eng", "spa", "fra"])  # English, Spanish, French
```

### Formati non‑PNG

Anche se il nostro focus è **recognize text from PNG**, `SimpleOCR` accetta anche JPEG, BMP e TIFF. Basta cambiare l'estensione del file in `setImageFromFile`. Per stack TIFF, potresti dover selezionare una pagina specifica:

```python
engine.setImageFromFile("scanned.tif", page=0)  # first page only
```

### File di grandi dimensioni e utilizzo della memoria

Se stai elaborando scansioni gigapixel, considera il ridimensionamento prima dell'OCR:

```python
from PIL import Image

with Image.open(image_path) as img:
    img.thumbnail((2000, 2000))  # keep aspect ratio, max 2000px
    img.save("temp_resized.png")
engine.setImageFromFile("temp_resized.png")
```

Il ridimensionamento riduce la pressione sulla memoria mantenendo abbastanza dettaglio per un riconoscimento accurato.

### Debug di caricamenti falliti

A volte un'immagine sembra a occhio nudo a posto ma è corrotta internamente. Abilita il logging verboso per vedere cosa vede il motore:

```python
engine.enableDebug(True)   # prints internal steps to stdout
engine.recognize()
```

---

## Script completo, pronto‑all‑uso

Di seguito trovi il programma completo che unisce tutti i pezzi. Copialo in un file chiamato `ocr_demo.py`, regola il placeholder `YOUR_DIRECTORY`, ed esegui `python ocr_demo.py`.

```python
# ocr_demo.py
# Full example showing how to use OCR to extract text from a PNG image.
# Requires: pip install simple-ocr pillow

from simple_ocr import OcrEngine
import os
from PIL import Image

def main():
    # 1️⃣ Create the OCR engine
    engine = OcrEngine()

    # 2️⃣ Define the image path – change this to your actual file location
    image_path = os.path.join("YOUR_DIRECTORY", "mixed_doc.png")

    # 3️⃣ Load the image (with a safety net for missing files)
    try:
        engine.setImageFromFile(image_path)
    except FileNotFoundError:
        print(f"❗️ Cannot find image at '{image_path}'. Exiting.")
        return

    # Optional: resize large images to keep memory usage low
    # (uncomment if you deal with huge scans)
    # with Image.open(image_path) as img:
    #     img.thumbnail((2000, 2000))
    #     resized_path = "temp_resized.png"
    #     img.save(resized_path)
    #     engine.setImageFromFile(resized_path)

    # 4️⃣ Enable automatic language detection (covers all installed packs)
    engine.setLanguage("multilingual")

    # 5️⃣ Run the OCR engine
    engine.recognize()

    # 6️⃣ Retrieve and print the recognized text
    result = engine.getResult()
    text = result.getText()

    if text.strip():
        print("\n📝 Recognized Text:\n")
        print(text)
    else:
        print("⚠️ No recognizable text found. Try a clearer image or adjust preprocessing.")

if __name__ == "__main__":
    main()
```

Eseguendo questo script dovrebbe stampare la versione in testo semplice di qualsiasi cosa sia contenuta in `mixed_doc.png`. Sentiti libero di sostituire il file con un'altra immagine—**how to extract text** funziona allo stesso modo.

---

## Conclusione

Abbiamo appena illustrato **come usare OCR** in Python per **estrarre testo da file immagine**, concentrandoci in particolare su **recognize text from PNG** e sui passaggi pratici per **load image for OCR**. Lo snippet sopra è una soluzione autonoma: installa il pacchetto, fornisci un file, abilita il rilevamento multilingue, esegui il motore e ottieni il risultato.

Da qui potresti:

- Integrare lo script in un servizio web che accetta upload degli utenti.  
- Elaborare in batch una cartella di PDF convertiti in PNG.  
- Aggiungere post‑elaborazione (ad es., pulizia con regex, correzione ortografica) per migliorare l'accuratezza.

Ricorda, la qualità dell'OCR dipende dalla chiarezza dell'immagine, dai pacchetti linguistici appropriati e talvolta da un po' di pre‑processing—quindi sperimenta

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}