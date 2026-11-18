---
category: general
date: 2026-07-05
description: Esegui OCR su un'immagine usando Python. Impara come convertire un'immagine
  in testo con Python, caricare l'immagine per l'OCR ed estrarre testo cirilico dall'immagine
  in pochi minuti.
draft: false
keywords:
- perform OCR on image
- convert image to text python
- load image for OCR
- extract Cyrillic text from image
- recognize Cyrillic text
language: it
og_description: Esegui OCR su un'immagine in Python. Questa guida ti mostra come convertire
  un'immagine in testo con Python, caricare l'immagine per l'OCR ed estrarre rapidamente
  testo cirillico dall'immagine.
og_title: Esegui OCR su un'immagine con Python – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image using Python. Learn how to convert image to text
    python, load image for OCR and extract Cyrillic text from image in minutes.
  headline: Perform OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- Cyrillic
title: Esegui OCR su un'immagine con Python – Guida completa passo passo
url: /it/python/general/perform-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine con Python – Guida Completa Passo‑per‑Passo

Ti sei mai chiesto come **eseguire OCR su file immagine** senza affidarti a un servizio di terze parti? Non sei solo. In molti progetti—scanner di passaporti, digitalizzatori di ricevute o strumenti di archiviazione—ottenere il testo grezzo da una foto è il primo ostacolo.  

In questo tutorial percorreremo un esempio pratico che **converte immagine in testo python**, ti mostrerà come **caricare immagine per OCR**, e infine **estrarre testo cirillico da immagine** usando la libreria open‑source `aocr`. Alla fine sarai in grado di **riconoscere testo cirillico** in qualsiasi immagine gli venga sottoposta.

> **Cosa otterrai:** uno script pronto all'uso, spiegazioni chiare di ogni passaggio e consigli per gestire le difficoltà comuni (come scansioni sfocate o font inattesi). Nessuna API esterna, solo puro Python.

---

## Prerequisiti

Prima di iniziare, assicurati di avere:

- Python 3.8 o versioni successive installate.
- Un terminale o prompt dei comandi con cui ti trovi a tuo agio.
- Il pacchetto `aocr` (installabile con `pip install aocr`).
- Un file immagine che contenga caratteri cirillici (ad esempio, un passaporto russo scansionato).  

Se qualcuno di questi punti ti è poco familiare, non preoccuparti—ogni voce sarà trattata brevemente man mano che procediamo.

---

## Step 1: Perform OCR on Image – Setting Up the Environment

La prima cosa di cui abbiamo bisogno è un ambiente Python pulito dove risieda la libreria OCR. Usare un ambiente virtuale isola le dipendenze e previene conflitti di versione.

```bash
# Create a virtual environment (optional but recommended)
python -m venv ocr-env
# Activate it (Windows)
ocr-env\Scripts\activate
# Activate it (macOS/Linux)
source ocr-env/bin/activate

# Install the aocr library
pip install aocr
```

**Perché?**  
Un ambiente dedicato garantisce che il pacchetto `aocr` e i suoi binari nativi non interferiscano con altri progetti. Inoltre rende la riproducibilità un gioco da ragazzi—qualcun altro può clonare il tuo repository e eseguire lo stesso comando `pip install -r requirements.txt`.

> **Suggerimento professionale:** Congela le tue dipendenze con `pip freeze > requirements.txt` così saprai sempre esattamente quali versioni sono state usate.

---

## Step 2: Load Image for OCR – Importing and Preparing the File

Ora che la libreria è pronta, dobbiamo **caricare immagine per OCR**. Il metodo `aocr.Image.from_file` gestisce i formati più comuni (PNG, JPEG, TIFF). Ecco come fare:

```python
import aocr

# Path to the Cyrillic image – replace with your actual file location
image_path = "YOUR_DIRECTORY/rus_passport.png"

# Load the image into an aocr.Image object
cyrillic_image = aocr.Image.from_file(image_path)
```

**Cosa sta succedendo?**  
`aocr.Image.from_file` legge i dati binari, li decodifica e li memorizza in un oggetto che il motore OCR può comprendere. Se il file non viene trovato, Python solleverà un `FileNotFoundError`, che potrai intercettare in seguito per gestire gli errori in modo più elegante.

> **Caso limite:** Alcuni scanner producono TIFF a più pagine. In quel caso, dovrai prima dividere le pagine—`aocr` fornisce `Image.from_tiff_pages()` per questo scopo.

---

## Step 3: Configure the OCR Engine – Forcing Cyrillic Recognition

Per impostazione predefinita, molti motori OCR cercano di indovinare la lingua, il che può portare a risultati incomprensibili per script non latini. Per **riconoscere testo cirillico** in modo affidabile, impostiamo esplicitamente la lingua su “cyrillic”.

```python
# Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Force the engine to use the Cyrillic recognizer
ocr_engine.language = "cyrillic"
```

**Perché forzare la lingua?**  
I caratteri cirillici condividono somiglianze visive con le lettere latine (es. “A” vs “А”). Dire al motore di aspettarsi il cirillico riduce drasticamente gli errori di riconoscimento, soprattutto su scansioni a bassa risoluzione.

---

## Step 4: Perform OCR on Image – Running the Recognition

Con l'immagine caricata e il motore configurato, finalmente **eseguiamo OCR su immagine**. Il metodo `recognize` restituisce un oggetto `OcrResult` contenente il testo estratto e i punteggi di confidenza.

```python
# Run the OCR process
ocr_result = ocr_engine.recognize(cyrillic_image)

# Print the raw text
print("Cyrillic text:")
print(ocr_result.text)
```

**Cosa ti fornisce `ocr_result`?**  
- `text`: la stringa semplice dei caratteri riconosciuti.  
- `confidence`: un float (0‑1) che indica la certezza complessiva.  
- `lines`: una lista di oggetti linea se ti serve un controllo più granulare.

> **Domanda comune:** *E se il testo è capovolto?*  
> `aocr` può ruotare automaticamente le immagini; basta impostare `ocr_engine.auto_rotate = True` prima di chiamare `recognize`.

---

## Step 5: Convert Image to Text Python – Post‑Processing the Output

La stringa grezza può contenere spazi bianchi superflui o artefatti di interruzioni di riga. Per **convertire immagine in testo python** in modo pulito, la ripuliremo con pochi semplici passaggi:

```python
import re

# Remove extra whitespace and normalize line breaks
clean_text = re.sub(r'\s+', ' ', ocr_result.text).strip()

print("\nCleaned Cyrillic text:")
print(clean_text)
```

**Perché farlo?**  
Un output pulito è più facile da inserire in pipeline successive—che tu lo stia memorizzando in un database, inviandolo a un'API di traduzione o eseguendo ricerche regex per numeri di passaporto.

---

## Step 6: Extract Cyrillic Text from Image – Putting It All Together

Raccogliamo tutto in una singola funzione riutilizzabile. Così **estrarre testo cirillico da immagine** diventa una riga di codice nei tuoi progetti.

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Loads an image, forces Cyrillic OCR, and returns cleaned text.
    """
    # Load image
    img = aocr.Image.from_file(image_path)

    # Configure OCR engine for Cyrillic
    engine = aocr.OcrEngine()
    engine.language = "cyrillic"

    # Recognize text
    result = engine.recognize(img)

    # Clean up the output
    cleaned = re.sub(r'\s+', ' ', result.text).strip()
    return cleaned

# Example usage
if __name__ == "__main__":
    path = "YOUR_DIRECTORY/rus_passport.png"
    print("Extracted text:", extract_cyrillic_text(path))
```

**Risultato atteso (esempio):**

```
Extracted text: ПАСПОРТ РФ № 1234567890 ИМЯ ФАМИЛИЯ ДАТА РОЖДЕНИЯ 01.01.1990
```

Se l'immagine è nitida e il font corrisponde al modello OCR, otterrai una trascrizione quasi perfetta.

---

## Risoluzione dei problemi e consigli

| Problema | Causa probabile | Soluzione |
|----------|-----------------|-----------|
| Caratteri illeggibili | Impostazione lingua errata | Assicurati che `ocr_engine.language = "cyrillic"` |
| Output vuoto | Immagine troppo scura o a bassa risoluzione | Pre‑elabora con `opencv` per aumentare il contrasto |
| Orientamento sbagliato | Immagine ruotata di 90° | Imposta `ocr_engine.auto_rotate = True` |
| Prestazioni lente | Immagine grande (>5 MP) | Ridimensiona con `aocr.Image.resize(width=1024)` prima del riconoscimento |

---

![perform OCR on image example](ocr_example.png "perform OCR on image example")

*Testo alternativo: “esempio di OCR su immagine che mostra codice Python che estrae testo cirillico da una scansione di passaporto.”*

---

## Conclusione

Abbiamo appena **eseguito OCR su file immagine** usando puro Python, imparato a **caricare immagine per OCR**, forzato il motore a **riconoscere testo cirillico**, e infine **estratto testo cirillico da immagine** con una comoda funzione di supporto. L'intera pipeline—dall'installazione di `aocr` alla pulizia del risultato—si incapsula in poche decine di righe di codice e può essere inserita in qualsiasi progetto che necessiti di **convertire immagine in testo python**.

---

## Cosa c’è dopo?

- **Elaborazione batch:** cicla su una cartella di scansioni e salva i risultati in SQLite.  
- **Rilevamento lingua:** combina `langdetect` con `aocr` per cambiare automaticamente tra cirillico e latino.  
- **Pre‑elaborazione avanzata:** usa `opencv` per correggere l'inclinazione, ridurre il rumore o binarizzare le immagini per una maggiore precisione.  
- **Integrazione con FastAPI:** espone la funzione `extract_cyrillic_text` come endpoint REST per applicazioni web.

Sentiti libero di sperimentare—cambia la lingua in “latin” per passaporti inglesi, o prova un backend OCR diverso. I concetti rimangono gli stessi, e il codice è sufficientemente flessibile da adattarsi.

Buon coding, e che le tue immagini siano sempre leggibili!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che approfondiscono le tecniche illustrate in questa guida. Ogni risorsa include esempi di codice completi e spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci alternativi nei tuoi progetti.

- [Estrai testo da immagine con Aspose OCR – Guida passo‑passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Converti immagine in testo – Esegui OCR su immagine da URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Estrai testo da immagine C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}