---
category: general
date: 2026-03-26
description: Impara a raddrizzare l'immagine, riconoscere il testo dall'immagine e
  creare una pipeline di pre‑elaborazione delle immagini per rimuovere il rumore dalla
  scansione e convertire l'immagine scansionata in testo.
draft: false
keywords:
- how to deskew image
- recognize text from image
- image preprocessing pipeline
- remove noise from scan
- convert scanned image to text
language: it
og_description: Come raddrizzare l'immagine e trasformare una scansione inclinata
  in testo ricercabile. Segui questa guida per riconoscere il testo dall'immagine,
  rimuovere il rumore dalla scansione e convertire l'immagine scansionata in testo.
og_title: Come raddrizzare l'immagine – Guida OCR passo passo
tags:
- OCR
- image-processing
- Python
title: Come raddrizzare l'immagine – Guida completa con OCR
url: /it/python-java/general/how-to-deskew-image-complete-guide-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come raddrizzare un'immagine – Guida completa con OCR

Ti sei mai chiesto **come raddrizzare un'immagine** scansionata con uno scanner economico? Non sei l'unico. Una pagina storta appare poco professionale e, soprattutto, l'inclinazione può compromettere qualsiasi motore OCR che tenta di **riconoscere il testo da un'immagine**.  

In questo tutorial percorreremo una **pipeline completa di pre‑elaborazione delle immagini** che raddrizza, binarizza e denoise una scansione, per poi passarla a un motore OCR così da **convertire l'immagine scansionata in testo** con il minimo sforzo. Nessuna magia, solo puro Python e una piccola libreria che fa il lavoro pesante.

## Cosa ti serve

- Python 3.9+ (il codice funziona su 3.10 e versioni successive)
- Il pacchetto `ocr` (installalo con `pip install ocr‑toolkit` – sostituisci con il nome della tua libreria)
- Un JPEG o PNG scansionato visibilmente inclinato (es. `skewed_scan.jpg`)
- Un pizzico di curiosità sul perché ogni passo di pre‑elaborazione è importante

È tutto. Nessuna dipendenza pesante come OpenCV, a meno che tu non voglia approfondire in seguito.

## Passo 1: Caricare l’immagine scansionata

Il primo passo è caricare il file in memoria. Questa operazione è semplice ma cruciale: se il percorso è errato, tutto il resto va in crash.

```python
# Step 1: Load the scanned image
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)
```

> **Perché?**  
> Caricare l’immagine ci fornisce un oggetto manipolabile con cui `ocr.ImagePreprocessor` può lavorare. Saltare questo passo lascerebbe la pipeline senza accesso ai dati dei pixel.

## Come raddrizzare l’immagine e prepararla per l’OCR

Ora che abbiamo l’immagine, sistemiamola. Il metodo `deskew()` stima l’angolo di inclinazione e ruota l’immagine fino a renderla orizzontale.

```python
# Step 2: Create an image preprocessor and correct the orientation
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()
```

> **Consiglio professionale:** Se le tue scansioni sono solo leggermente inclinate (≤ 3°), l’algoritmo predefinito è di solito perfetto. Per angoli estremi potresti dover regolare i parametri interni—controlla la documentazione della libreria per `max_angle`.

## Binarizzare l’immagine – Renderla in bianco‑e‑nero

I motori OCR amano input ad alto contrasto. Convertire l’immagine in una rappresentazione binaria (bianco‑e‑nero) elimina le sfumature sottili che possono confondere il riconoscimento dei caratteri.

```python
# Step 3: Convert the image to a binary (black‑and‑white) representation
preprocessor.binarize(threshold=128)
```

> **Cosa succede?**  
> I pixel più luminosi di 128 diventano bianchi; tutto il resto diventa nero. Regola la soglia se la tua scansione è insolitamente scura o chiara.

## Rimuovere il rumore dalla scansione prima dell’OCR

Anche un’immagine perfettamente raddrizzata può contenere macchie, polvere o artefatti di compressione. Quei piccoli granelli sono il nemico di qualsiasi motore OCR.

```python
# Step 4: Reduce noise to improve OCR accuracy
preprocessor.denoise(radius=1)
```

> **Perché rimuovere il rumore?**  
> Il rumore crea bordi falsi che il motore OCR potrebbe interpretare come caratteri. Un raggio piccolo funziona per la maggior parte delle scansioni; aumentalo per documenti molto granulosi.

## Applicare la pipeline di pre‑elaborazione delle immagini

Tutte le impostazioni sono pronte—adesso eseguiamo la pipeline sull’immagine originale.

```python
# Step 5: Apply the preprocessing pipeline to the loaded image
processed_image = preprocessor.apply(original_image)
```

> **Risultato:** `processed_image` è un bitmap pulito, dritto e ad alto contrasto, pronto per l’estrazione del testo.

## Riconoscere il testo dall’immagine con il motore OCR

È il momento di leggere realmente il testo. Inizializziamo il motore OCR, gli forniamo la nostra immagine perfezionata e chiediamo la stringa grezza.

```python
# Step 6: Initialise the OCR engine and provide the processed image
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# Step 7: Recognise text and output the result
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Output atteso** (esempio):

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Se vedi caratteri incomprensibili, ricontrolla il passo di raddrizzamento o sperimenta con un valore di `threshold` diverso.

## Creare una pipeline di pre‑elaborazione delle immagini – Script completo

Mettendo tutto insieme, ecco uno script unico e eseguibile che puoi salvare in un file `.py` e lanciare:

```python
import ocr  # Replace with the actual import path of your OCR library

# -------------------------------------------------
# 1️⃣ Load the scanned image
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)

# -------------------------------------------------
# 2️⃣ Deskew – how to deskew image
# -------------------------------------------------
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()

# -------------------------------------------------
# 3️⃣ Binarize – convert to black‑and‑white
# -------------------------------------------------
preprocessor.binarize(threshold=128)

# -------------------------------------------------
# 4️⃣ Denoise – remove noise from scan
# -------------------------------------------------
preprocessor.denoise(radius=1)

# -------------------------------------------------
# 5️⃣ Apply the pipeline
# -------------------------------------------------
processed_image = preprocessor.apply(original_image)

# -------------------------------------------------
# 6️⃣ OCR – recognize text from image
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# -------------------------------------------------
# 7️⃣ Output – convert scanned image to text
# -------------------------------------------------
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Suggerimento:** Avvolgi il tutto in una funzione (`def ocr_from_file(path): …`) se prevedi di elaborare molti file in batch.

## Domande frequenti e casi particolari

- **E se l’immagine è già dritta?**  
  Il metodo `deskew()` rileva un angolo quasi nullo e lascia l’immagine intatta, quindi puoi usarlo tranquillamente su ogni file.

- **La mia scansione è a colori—devo mantenerla?**  
  Il colore non aggiunge valore nella maggior parte dei compiti OCR. La binarizzazione lo elimina, velocizzando l’elaborazione e riducendo l’uso di memoria.

- **Posso concatenare più passaggi di pre‑elaborazione?**  
  Assolutamente. La classe `ImagePreprocessor` è pensata per le pipeline; puoi aggiungere `sharpen()`, `contrast_enhance()` o filtri personalizzati prima di chiamare `apply()`.

- **L’output OCR contiene interruzioni di riga indesiderate—come risolvere?**  
  Post‑processa la stringa con `text.replace("\n", " ").strip()` oppure usa una libreria di analisi del layout più avanzata come le modalità `--psm` di Tesseract.

## Prossimi passi

Ora che sai **come raddrizzare un’immagine** e disponi di una solida **pipeline di pre‑elaborazione delle immagini**, potresti approfondire:

- Integrare **riconoscere testo da immagine** in una API Flask per caricamenti di documenti on‑the‑fly.
- Usare la pipeline per **rimuovere il rumore da scansioni** di documenti storici, dove la conservazione è fondamentale.
- Scalare il processo per gestire migliaia di pagine in batch e generare un PDF ricercabile usando `pdfminer` o `PyMuPDF`.

Sentiti libero di sperimentare con soglie diverse, raggi di denoise o persino sostituire il backend OCR con Tesseract se ti serve il supporto multilingue. I principi rimangono gli stessi: raddrizza, pulisci, poi leggi.

---

*Buon coding! Se incontri problemi, lascia un commento qui sotto—sarò felice di aiutarti a perfezionare la pipeline.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}