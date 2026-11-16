---
category: general
date: 2026-03-26
description: Impara a ruotare l'immagine e a eseguire l'OCR in Python. Questa guida
  mostra anche come pre‑elaborare l'immagine per l'OCR ed estrarre il testo dall'immagine
  in modo efficiente.
draft: false
keywords:
- how to rotate image
- how to perform ocr
- preprocess image for ocr
- recognize text from image
- how to extract text from image
language: it
og_description: Come ruotare correttamente l'immagine e poi riconoscere il testo dall'immagine
  usando Aspose OCR. Segui questo tutorial passo‑passo per pre‑elaborare l'immagine
  per l'OCR ed estrarre il testo dall'immagine.
og_title: Come ruotare l'immagine e eseguire OCR – Guida completa a Python
tags:
- Aspose
- Python
- Image Processing
- OCR
title: Come ruotare l'immagine ed eseguire OCR con Aspose in Python
url: /it/python-java/general/how-to-rotate-image-and-perform-ocr-with-aspose-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come ruotare un'immagine ed eseguire OCR con Aspose in Python

Ti sei mai chiesto **come ruotare un'immagine** in modo che un motore OCR possa effettivamente leggere il testo? Forse hai scansionato un modulo che è finito di lato, o una foto è stata catturata ruotata di 90° in senso orario. In tal caso il testo sembra corretto all'occhio umano, ma il motore OCR lo vede come un caos. La buona notizia? È un gioco da ragazzi correggere l'orientamento, ritagliare l'area di interesse e poi estrarre il testo—tutto con poche righe di Python e le librerie Aspose.

In questo tutorial percorreremo l'intero flusso di lavoro: dal caricamento di un TIFF ruotato, alla correzione della sua orientazione, **preprocess image for OCR**, e infine **recognize text from image**. Alla fine saprai **how to perform OCR** su qualsiasi immagine e potrai **extract text from image** con sicurezza.

## Cosa ti serve

- Python 3.8+ (il codice funziona con qualsiasi versione recente)
- Pacchetti `asposeocrjava` e `asposeimaging` installati via `pip`
- Un'immagine di esempio che necessita di rotazione (ad es., `rotated_form.tif`)
- Un po' di curiosità sull'elaborazione delle immagini

Nessun framework pesante necessario—solo i due pacchetti Aspose e un po' di logica Python.

---

## Passo 1: Installare i pacchetti Aspose (How to Perform OCR)

Prima di poter **rotate image** o **recognize text from image**, abbiamo bisogno delle librerie che fanno davvero il lavoro pesante.

```bash
pip install asposeocrjava asposeimaging
```

> **Consiglio professionale:** Se sei dietro un proxy aziendale, aggiungi `--proxy http://proxy:port` al comando. I pacchetti sono wrapper Python puri attorno al core Aspose .NET/Java, quindi l'installazione è solitamente istantanea.

---

## Passo 2: Caricare il file sorgente e ruotarlo – Il passaggio centrale “How to Rotate Image”

```python
from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

# Load the original, incorrectly oriented image
source_image = Image.load("YOUR_DIRECTORY/rotated_form.tif")

# Rotate 90° clockwise – this fixes the orientation for OCR
rotated_image = source_image.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)
```

> **Perché ruotare?** La maggior parte dei motori OCR assume che il testo scorra da sinistra a destra e dall'alto verso il basso. Se il bitmap è ruotato di lato, il motore restituirà o un nonsense o nulla. Ruotare allinea la griglia di pixel all'ordine di lettura previsto, migliorando notevolmente l'accuratezza.

> **Caso limite:** Se non sei sicuro se l'immagine necessiti di una rotazione di 90°, 180° o 270°, puoi controllare `source_image.width` vs `source_image.height` o usare i tag di orientamento `exif`. Il metodo `rotate_flip` di Aspose supporta anche `ROTATE_180` e `ROTATE_270_CLOCKWISE`.

> **Anteprima immagine (opzionale):**  
> ![esempio di come ruotare un'immagine](/assets/rotate-demo.png "Come ruotare un'immagine – prima e dopo la rotazione")

---

## Passo 3: Ritagliare l'area di interesse – Preprocess Image for OCR

Spesso ti serve solo una piccola parte della pagina—ad esempio, un campo firma o un blocco di numeri. Il ritaglio rimuove il rumore e velocizza **how to perform OCR**.

```python
# Define the rectangle that encloses the text you care about
# (x=100, y=200, width=800, height=300) – adjust to your form
roi = Rectangle(100, 200, 800, 300)

# Crop the rotated image to that rectangle
roi_image = rotated_image.crop(roi)
```

> **Perché ritagliare?** Ridurre le dimensioni dell'immagine limita lo spazio di ricerca del motore OCR, riducendo i falsi positivi e il tempo di elaborazione. Aiuta anche se il file sorgente contiene filigrane o altre grafiche che potrebbero confondere il motore.

> **Suggerimento:** Se lavori con più campi, ripeti il passaggio di ritaglio con rettangoli diversi ed esegui l'OCR su ogni pezzo separatamente.

---

## Passo 4: Inizializzare il motore OCR – Il nucleo “How to Perform OCR”

```python
# Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

> **Dietro le quinte:** Aspose OCR utilizza una combinazione di Tesseract e analisi di immagine proprietaria. Istanziare il motore una volta e riutilizzarlo per più immagini è più efficiente che creare un nuovo oggetto ogni volta.

---

## Passo 5: Fornire l'immagine ritagliata e riconoscere il testo – How to Extract Text from Image

```python
# Set the cropped image as the input for OCR
ocr_engine.set_image(roi_image)

# Run the recognition process
result = ocr_engine.recognize()

# Extract the plain text
extracted_text = result.get_text()
print(extracted_text)
```

### Output previsto

Se la ROI contiene la frase “Invoice #12345 – Paid”, vedrai qualcosa di simile:

```
Invoice #12345 – Paid
```

Se l'OCR ha difficoltà, potresti ottenere spazi extra o caratteri letti male (ad es., “Invo1ce #I2345 – Pa1d”). È qui che i trucchi **preprocess image for OCR**—come regolare il contrasto o applicare la binarizzazione—entrano in gioco. Aspose offre filtri aggiuntivi che puoi concatenare prima del passo 5, ma il flusso base sopra funziona per la maggior parte delle scansioni pulite.

---

## Passo 6: Opzionale – Ottimizzare le impostazioni OCR (Advanced “How to Perform OCR”)

Se hai bisogno di maggiore accuratezza per una lingua specifica o vuoi ignorare certi caratteri, puoi modificare il motore:

```python
# Example: Restrict recognition to English alphanumerics only
ocr_engine.get_recognition_settings().set_recognition_language("en")
ocr_engine.get_recognition_settings().set_characters_blacklist("!@#$%^&*()")
```

> **Quando usarlo:** Usalo quando il documento contiene molti simboli decorativi di cui non ti interessa. La blacklist riduce le rilevazioni false.

---

## Script completo end‑to‑end

Mettendo tutto insieme, ecco uno script pronto all'uso che **how to rotate image**, **preprocess image for OCR**, e infine **recognize text from image**:

```python
# -*- coding: utf-8 -*-
"""
Complete example: rotate, crop, and OCR an image with Aspose.
Author: Your Name
Date: 2026-03-26
"""

from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

def ocr_rotated_image(
    input_path: str,
    output_path: str = None,
    crop_rect: Rectangle = Rectangle(100, 200, 800, 300)
) -> str:
    """
    Loads an image, rotates it 90° clockwise, crops the region of interest,
    runs OCR, and returns the extracted text.

    Parameters
    ----------
    input_path : str
        Path to the original (possibly rotated) image file.
    output_path : str, optional
        If provided, saves the processed (rotated + cropped) image for inspection.
    crop_rect : Rectangle, optional
        Rectangle defining the ROI. Adjust to match your document layout.

    Returns
    -------
    str
        The plain text extracted from the ROI.
    """
    # Load and rotate
    src = Image.load(input_path)
    rotated = src.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)

    # Crop to region of interest
    roi = rotated.crop(crop_rect)

    # Optionally save the processed image for debugging
    if output_path:
        roi.save(output_path)

    # OCR
    engine = OcrEngine()
    engine.set_image(roi)
    result = engine.recognize()
    return result.get_text()

if __name__ == "__main__":
    text = ocr_rotated_image(
        "YOUR_DIRECTORY/rotated_form.tif",
        output_path="processed_roi.png"
    )
    print("=== Extracted Text ===")
    print(text)
```

Eseguendo questo script stampa il testo riconosciuto nella console e salva un'immagine della ROI elaborata come `processed_roi.png`. Puoi aprire quel PNG per verificare che la rotazione e il ritaglio siano avvenuti come previsto.

---

## Domande frequenti e problemi comuni

| Question | Answer |
|----------|--------|
| **E se l'immagine è già in posizione verticale?** | Il passaggio di rotazione è idempotente—ruotare un'immagine già correttamente orientata di 90° la romperà ovviamente, quindi dovresti controllare `source_image.width` vs `height` o usare i dati di orientamento EXIF prima di chiamare `rotate_flip`. |
| **Il mio output OCR contiene interruzioni di riga extra.** | Usa `result.get_text().replace("\n", " ").strip()` per pulire, oppure abilita `ocr_engine.get_recognition_settings().set_remove_line_breaks(True)`. |
| **Posso elaborare i PDF direttamente?** | Sì—Aspose Imaging può caricare le pagine PDF come immagini (`Image.load("file.pdf")`), dopodiché segui gli stessi passaggi di rotazione e OCR. |
| **C'è un modo per elaborare in batch molti file?** | Avvolgi `ocr_rotated_image` in un ciclo su una directory, oppure usa `concurrent.futures` di Python per parallelizzare. |
| **Come gestire lingue diverse dall'inglese?** | Imposta la lingua di riconoscimento tramite `ocr_engine.get_recognition_settings().set_recognition_language("fr")` per il francese, ecc. |

---

## Conclusione

Abbiamo coperto **how to rotate image** correttamente, **preprocess image for OCR** tramite ritaglio, e infine **how to perform OCR** per **recognize text from image** e **extract text from image** usando le librerie Python di Aspose. Lo script completo dimostra un flusso di lavoro pratico e pronto per la produzione che puoi inserire in qualsiasi pipeline di automazione.

Se sei pronto a andare oltre, prova a sperimentare con:

- **Image enhancement** (contrasto, binarizzazione) prima dell'OCR
- **Multiple ROI extraction** per moduli con diversi campi
- **Batch processing** di intere cartelle di documenti scansionati
- **Integration** con sistemi a valle (ad es., inserire i dati estratti in un database)

Sentiti libero di adattare il codice al tuo caso d'uso, e buona programmazione! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}