---
category: general
date: 2026-07-05
description: Estrai il testo da un'immagine usando Python OCR. Scopri come riconoscere
  il testo da un'immagine, caricare l'immagine per l'OCR e impostare la lingua dell'OCR
  in poche righe.
draft: false
keywords:
- extract text from image
- how to recognize text from image
- load image for ocr
- create ocr engine python
- set ocr language
language: it
og_description: Estrai testo da un'immagine con OCR in Python. Questa guida mostra
  come riconoscere il testo da un'immagine, caricare l'immagine per l'OCR, creare
  un motore OCR in stile Python e impostare la lingua dell'OCR.
og_title: Estrai testo da un'immagine in Python – Riconosci il testo velocemente
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to recognize text
    from image, load image for OCR, and set OCR language in just a few lines.
  headline: Extract Text from Image in Python – Recognize Text Fast
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Estrai testo da un'immagine in Python – Riconosci il testo rapidamente
url: /it/python-java/general/extract-text-from-image-in-python-recognize-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da immagine in Python – Riconosci il testo rapidamente

Hai mai avuto bisogno di **estrarre testo da immagine** ma non sapevi quale libreria scegliere? Se ti sei mai chiesto *come riconoscere il testo da un'immagine* senza dover gestire strumenti esterni, sei nel posto giusto. In questo tutorial avvieremo un piccolo motore OCR, lo punteremo a un'immagine e ne estrarremo il testo—nient'altro, nientomeno.

Passeremo in rassegna ogni passaggio: **create OCR engine python**, **set OCR language**, **load image for OCR**, avvieremo il riconoscimento in modo asincrono e infine leggeremo il risultato. Alla fine avrai uno script autonomo che potrai inserire in qualsiasi progetto, sia esso un digitalizzatore di documenti o un chatbot che legge i meme.

## Di cosa avrai bisogno

- Python 3.8+ (il codice funziona anche su 3.10 e versioni successive)  
- Il pacchetto `ocr` (un leggero wrapper attorno a Tesseract – installalo con `pip install ocr` o il tuo fork preferito)  
- Un file immagine (`.jpg`, `.png`, ecc.) che contiene testo leggibile  
- Un pizzico di pazienza per la parte async (è veloce, promesso)

Questo è tutto—nessuna dipendenza pesante, nessuna compilazione nativa. Se hai già Tesseract sul tuo sistema, il wrapper `ocr` lo troverà automaticamente.

## Passo 1: Crea il motore OCR – il cuore dell'estrazione

Prima di tutto: ti serve un oggetto engine che sappia comunicare con il motore OCR sottostante. Pensalo come il “cervello” che in seguito elaborerà l'immagine.

```python
import ocr

# Step 1: Instantiate the OCR engine
engine = ocr.OcrEngine()
```

*Perché è importante*: senza un engine non hai contesto per le impostazioni della lingua o le capacità async. La classe `OcrEngine` astrae le chiamate a riga di comando a basso livello di Tesseract, fornendoti una pulita API Python.

## Passo 2: Imposta la lingua OCR – dici all'engine cosa aspettarsi

Se il tuo documento è in inglese, puoi lasciare il valore predefinito, ma è buona pratica impostarlo esplicitamente. Questo mostra anche come **set OCR language** per altre lingue.

```python
# Step 2: Explicitly set the language to English
engine.language = ocr.Language.ENGLISH
```

> **Consiglio**: Per PDF multilingue, puoi passare una lista come `[ocr.Language.ENGLISH, ocr.Language.FRENCH]`. Il motore proverà entrambe le lingue automaticamente.

## Passo 3: Carica l'immagine per OCR – porta la tua foto in memoria

Ora effettivamente **load image for OCR**. Il wrapper supporta il lazy loading, quindi il file non viene letto finché l'engine non ne ha bisogno.

```python
# Step 3: Load the image you want to process
image_path = "YOUR_DIRECTORY/large_document.jpg"
image = ocr.Image.load(image_path)
```

*Caso limite*: Se l'immagine è enorme (oltre 5 MB), considera di ridimensionarla prima per velocizzare il riconoscimento. Puoi farlo con Pillow:

```python
from PIL import Image as PilImage

pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio, max 2000px
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")
```

## Passo 4: Avvia il riconoscimento asincrono – non bloccare la tua app

Eseguire OCR può richiedere un secondo o due, specialmente su scansioni grandi. Il metodo `recognize_async` restituisce un future che puoi interrogare in seguito, permettendoti di **eseguire altre operazioni mentre OCR gira in background**.

```python
# Step 4: Start the recognition asynchronously
future = engine.recognize_async(image)

# While OCR works, we can do something else
print("Processing other tasks while OCR runs...")
# Example placeholder work
for i in range(3):
    print(f"Task {i+1} done.")
```

Perché async? In un server web non vuoi che una singola richiesta blocchi l'intero pool di worker. L'oggetto future ti dà controllo: puoi `await` su di esso nel codice async o bloccare solo quando hai realmente bisogno del risultato.

## Passo 5: Recupera il risultato – blocca solo quando necessario

Quando finalmente ti serve il testo, chiama `future.get()`. Questa chiamata **blocca solo qui**, il che significa che il resto del tuo programma rimane reattivo finché OCR non termina.

```python
# Step 5: Get the recognized text (blocks here)
result = future.get()   # blocks only at this point
```

Se sei dentro un loop `asyncio`, potresti invece `await future` – il wrapper supporta entrambi gli stili.

## Passo 6: Usa il testo riconosciuto – i tuoi dati sono pronti

Ora che hai un oggetto `result`, estrarre la stringa semplice è banale. Stampiamola e mostriamo anche come potresti scriverla su un file.

```python
# Step 6: Output the OCR result
print("OCR completed:")
print(result.text)

# Optional: save to a .txt file
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**Output previsto** (troncato per brevità):

```
OCR completed:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

Se l'immagine non contiene testo, `result.text` sarà una stringa vuota—gestisci questo caso in modo appropriato.

## Esempio completo funzionante – Tutti i passi in un unico script

Di seguito trovi il programma completo, pronto‑da‑eseguire. Copia‑incolla, regola `image_path`, e sei pronto.

```python
import ocr
from PIL import Image as PilImage

# -------------------------------------------------
# 1️⃣ Create OCR engine
engine = ocr.OcrEngine()

# 2️⃣ Set language (English)
engine.language = ocr.Language.ENGLISH

# 3️⃣ Load image (optional resize for large files)
original_path = "YOUR_DIRECTORY/large_document.jpg"
pil_img = PilImage.open(original_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")

# 4️⃣ Start async recognition
future = engine.recognize_async(image)
print("Processing other tasks while OCR runs...")
for i in range(3):
    print(f"Task {i+1} done.")

# 5️⃣ Wait for result
result = future.get()

# 6️⃣ Use the text
print("OCR completed:")
print(result.text)
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

> **Nota**: Sostituisci `"YOUR_DIRECTORY/large_document.jpg"` con il percorso reale della tua immagine. Lo script funziona su Windows, macOS e Linux purché Tesseract sia installato e raggiungibile nel tuo `PATH`.

## Problemi comuni e come evitarli

| Problema | Perché succede | Soluzione |
|----------|----------------|-----------|
| **Caratteri spazzatura** | Lingua errata o file di dati della lingua mancanti. | Assicurati che `engine.language` corrisponda al testo e che il relativo file `.traineddata` esista nella cartella `tessdata` di Tesseract. |
| **Prestazioni lente su immagini grandi** | L'OCR scala approssimativamente con il numero di pixel. | Ridimensiona o riduci la risoluzione prima di passare l'immagine al motore (vedi lo snippet Pillow). |
| **Future non si risolve mai** | File immagine corrotto o illeggibile. | Avvolgi `future.get()` in un blocco try/except e valida `image.is_valid()` prima del riconoscimento. |
| **Perdita di Unicode** |  |  |

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrai testo da immagine con Aspose OCR – Guida passo‑passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Converti immagine in testo – Esegui OCR su immagine da URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Estrai testo da immagine – Ottimizzazione OCR con Aspose OCR per .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}