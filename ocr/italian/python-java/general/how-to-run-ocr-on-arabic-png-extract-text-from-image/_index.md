---
category: general
date: 2026-03-26
description: Impara come eseguire l'OCR su immagini PNG in arabo ed estrarre rapidamente
  il testo arabo. Questa guida mostra come convertire l'immagine in testo con codice
  Python passo‑passo.
draft: false
keywords:
- how to run ocr
- extract arabic text
- recognize arabic text
- convert image to text
- extract text from png
language: it
og_description: Come eseguire OCR su immagini PNG in arabo? Segui questa guida completa
  per estrarre testo arabo, riconoscere testo arabo e convertire l'immagine in testo
  usando Python.
og_title: Come eseguire OCR su PNG arabo – Estrarre il testo dall'immagine
tags:
- OCR
- Python
- Arabic
title: Come eseguire l'OCR su PNG arabi – Estrarre il testo dall'immagine
url: /it/python-java/general/how-to-run-ocr-on-arabic-png-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR su PNG arabo – Estrarre testo dall'immagine

Ti sei mai chiesto **come eseguire OCR** su un'immagine che contiene script arabo? Forse hai una ricevuta scansionata, un manoscritto storico, o semplicemente uno screenshot di un post sui social‑media e ti serve il testo in un formato ricercabile. Non sei solo: sviluppatori di tutto il mondo incontrano questo ostacolo quando lavorano con lingue da destra a sinistra.

In questo tutorial ti guideremo passo passo attraverso un esempio completo e eseguibile che mostra **come eseguire OCR** su un file PNG, estrarre testo arabo e stampare il risultato sulla console. Niente link vaghi “vedi la documentazione”; solo il codice pronto da copiare‑incollare, più spiegazioni sul perché ogni riga è importante. Alla fine sarai in grado di **convert image to text** in modo affidabile, anche quando la sorgente è un PNG arabo difficile.

> **What you’ll learn**
> - Configurare un motore OCR Python per l'arabo  
> - Caricare un'immagine PNG e gestire le difficoltà comuni  
> - Riconoscere testo arabo e verificare l'output  
> - Suggerimenti per **extracting Arabic text** da immagini di diversa qualità  

Prima di immergerci, assicurati di avere Python 3.8+ installato e una versione recente della libreria `ocr` (quella usata nello snippet). Se usi un ambiente virtuale, attivalo ora—così le dipendenze rimarranno ordinate.

## Prerequisiti

- Python 3.8 o più recente  
- Pacchetto `ocr` (`pip install ocr‑engine` – sostituisci con il nome reale del pacchetto)  
- Un'immagine PNG araba (`arabic_doc.png`) posizionata in un percorso accessibile  
- Familiarità di base con funzioni e classi Python  

Questo è tutto. Nessun framework pesante, nessun container Docker—solo Python puro.

## Passo 1: Installare e importare la libreria OCR

Prima di tutto. Abbiamo bisogno del motore OCR stesso. La libreria che useremo espone una classe `OcrEngine` con un'API semplice.

```python
# Install the library (run once in your terminal)
# pip install ocr-engine   # <-- replace with the correct package name

# Import the necessary classes
import ocr
from ocr import Imaging
```

*Why import `Imaging` separately?* Il sotto‑modulo `Imaging` ci fornisce un comodo metodo `Image.load` che comprende PNG, JPEG e TIFF fin da subito. Saltare questo passaggio ti costringerebbe a gestire i byte grezzi da solo, il che è superfluo per la maggior parte dei casi d'uso.

## Passo 2: Creare l'istanza del motore OCR

Ora creiamo un'istanza del motore. Pensa a questo oggetto come al “cervello” che elaborerà l'immagine.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

> **Pro tip:** Se prevedi di elaborare molte immagini di seguito, riutilizza la stessa istanza `ocr_engine`. Essa memorizza nella cache i modelli linguistici, accelerando le riconoscimenti successivi.

## Passo 3: Impostare la lingua su arabo

L'arabo non è latino; ha un proprio set di caratteri, direzione da destra a sinistra e forme contestuali. Per questo dobbiamo indicare esplicitamente al motore quale modello linguistico caricare.

```python
# Step 3: Set the language to Arabic (language code "ar")
ocr_engine.set_language("ar")
```

Se dimentichi questa riga, il motore usa per impostazione predefinita l'inglese e otterrai un output incomprensibile—qualcosa che ho visto accadere troppe volte.

## Passo 4: Caricare la tua immagine PNG

È qui che la parte **convert image to text** inizia davvero. Caricheremo il file PNG che contiene lo script arabo.

```python
# Step 4: Load the image that contains the Arabic text
image_path = "YOUR_DIRECTORY/arabic_doc.png"   # replace with your actual path
ocr_engine.set_image(Imaging.Image.load(image_path))
```

### Casi limite comuni

| Problema | Sintomo | Soluzione |
|----------|---------|-----------|
| L'immagine è troppo scura | L'output contiene molti spazi vuoti | Pre‑processare con Pillow (`ImageEnhance.Brightness`) |
| Il PNG ha un canale alfa | Alcuni motori OCR leggono male i pixel trasparenti | Convertire in RGB (`image.convert("RGB")`) prima del caricamento |
| Il testo è ruotato | Il testo riconosciuto è capovolto | Ruotare l'immagine (`image.rotate(90, expand=True)`) prima di passarla al motore |

## Passo 5: Eseguire il processo di riconoscimento

Con tutto pronto, chiediamo finalmente al motore di fare il suo lavoro.

```python
# Step 5: Run the recognition process
ocr_result = ocr_engine.recognize()
```

Il metodo `recognize` restituisce un oggetto che contiene la stringa Unicode grezza, i punteggi di confidenza e le bounding box. Per la maggior parte degli sviluppatori, il testo semplice è tutto ciò di cui hai bisogno.

## Passo 6: Stampare il testo arabo riconosciuto

Ora stampiamo il risultato. In un'applicazione reale potresti scrivere su un file, su un database, o inviarlo a un'API di traduzione.

```python
# Step 6: Output the recognized text
print(ocr_result.get_text())
```

Quando esegui lo script, dovresti vedere i caratteri arabi visualizzati nella console (assicurati che il tuo terminal supporti Unicode). Se vedi punti interrogativi o stringhe vuote, ricontrolla l'impostazione della lingua e la qualità dell'immagine.

### Output previsto

```
هذا نص عربي من صورة PNG تم استخراجها باستخدام OCR.
```

Se l'output appare simile alla riga sopra, congratulazioni—hai estratto con successo **Arabic text** da un PNG!

## Esempio completo funzionante

Di seguito trovi lo script intero, pronto da copiare‑incollare. Sostituisci `YOUR_DIRECTORY/arabic_doc.png` con il percorso del tuo file.

```python
import ocr
from ocr import Imaging

def main():
    # Create OCR engine
    ocr_engine = ocr.OcrEngine()
    
    # Set Arabic language
    ocr_engine.set_language("ar")
    
    # Load the PNG image
    image_path = "YOUR_DIRECTORY/arabic_doc.png"
    ocr_engine.set_image(Imaging.Image.load(image_path))
    
    # Recognize text
    ocr_result = ocr_engine.recognize()
    
    # Print the extracted Arabic text
    print(ocr_result.get_text())

if __name__ == "__main__":
    main()
```

Eseguilo con `python run_ocr.py` (o qualunque nome tu abbia dato al file). Se tutto è installato correttamente, vedrai la frase araba stampata sulla console.

## Come eseguire OCR su diversi formati immagine

Lo stesso codice funziona per JPEG, TIFF o BMP—basta cambiare l'estensione del file. Il metodo `Image.load` rileva automaticamente il formato, così puoi **convert image to text** senza codice aggiuntivo.

```python
# Example for a JPEG file
ocr_engine.set_image(Imaging.Image.load("sample.jpg"))
```

Ricorda, la qualità dell'immagine sorgente influisce notevolmente sull'accuratezza del passo **recognize Arabic text**. Immagini ad alta risoluzione e a bassa compressione danno i migliori risultati.

## Estrarre testo da PNG: consigli per una migliore precisione

1. **DPI Matters** – Punta a almeno 300 dpi. DPI più bassi spesso portano a caratteri mancanti.  
2. **Contrast is King** – Usa strumenti di elaborazione immagini (es. OpenCV) per aumentare il contrasto prima di fornire l'immagine al motore OCR.  
3. **Noise Removal** – Piccole macchie possono confondere il modello; la filtrazione mediana aiuta.  

Ecco uno snippet veloce che usa Pillow per migliorare un PNG prima dell'OCR:

```python
from PIL import Image, ImageEnhance, ImageFilter

def preprocess_png(path):
    img = Image.open(path).convert("L")          # grayscale
    img = ImageEnhance.Contrast(img).enhance(2)  # boost contrast
    img = img.filter(ImageFilter.MedianFilter()) # denoise
    return img

# Use the preprocessed image
prepped = preprocess_png("arabic_doc.png")
ocr_engine.set_image(Imaging.Image.from_pil(prepped))
```

## Domande frequenti

**Q: Does this work with right‑to‑left languages other than Arabic?**  
A: Assolutamente. Basta cambiare il codice lingua (`"ar"` → `"he"` per l'ebraico, `"fa"` per il persiano) e il motore caricherà il modello appropriato.

**Q: What if I need to extract text from multiple PNGs in a folder?**  
A: Scorri i file, riutilizza la stessa istanza `ocr_engine`, e raccogli i risultati in una lista o scrivi ciascuno in un file `.txt` separato.

**Q: Can I get confidence scores for each word?**  
A: Sì. `ocr_result` espone spesso un metodo `get_confidences()`. Associa ogni confidenza alla parola corrispondente per il controllo di qualità.

## Prossimi passi

Ora che sai **how to run OCR** su PNG arabi, considera queste idee successive:

- **Batch processing:** Combina lo script con `os.listdir` per **extract Arabic text** da un'intera directory.  
- **Post‑processing:** Usa le librerie `arabic_reshaper` e `python-bidi` per visualizzare correttamente l'output da destra a sinistra nei PDF.  
- **Integration:** Invia il testo estratto a un indice di ricerca (es. Elasticsearch) per rendere i documenti scansionati ricercabili.  

Ognuno di questi argomenti si basa sui fondamenti trattati qui e ti aiuterà a trasformare un semplice script **convert image to text** in una pipeline pronta per la produzione.

---

![how to run OCR on Arabic PNG](

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}