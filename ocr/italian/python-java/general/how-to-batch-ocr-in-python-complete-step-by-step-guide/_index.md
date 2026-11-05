---
category: general
date: 2026-06-28
description: Come eseguire OCR batch con Python. Impara a fare OCR su più immagini,
  estrarre testo da PNG e convertire un'immagine in testo con un tutorial completo
  di OCR in Python.
draft: false
keywords:
- how to batch OCR
- ocr multiple images
- extract text from png
- convert image to text
- python ocr tutorial
language: it
og_description: Come fare OCR in batch con Python, spiegato nella prima frase. Segui
  questo tutorial OCR in Python per estrarre il testo dai file PNG in modo efficiente.
og_title: Come eseguire OCR in batch con Python – Guida completa alla programmazione
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  headline: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  name: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Why set the language?**'
    text: '**Why set the language?**'
  - name: '**Why use a batch operation?**'
    text: '**Why use a batch operation?**'
  - name: '**Why a ThreadPoolExecutor?**'
    text: '**Why a ThreadPoolExecutor?**'
  - name: '**Why enumerate the results?**'
    text: '**Why enumerate the results?**'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Come eseguire l'OCR in batch con Python – Guida completa passo passo
url: /it/python-java/general/how-to-batch-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR batch in Python – Guida completa passo‑per‑passo

Ti sei mai chiesto **come eseguire OCR batch** su una pila di pagine scansionate senza scrivere un ciclo che blocca la tua UI? Non sei l'unico. Elaborare decine di file PNG uno‑a‑uno può sembrare come guardare la vernice asciugarsi, soprattutto quando ogni immagine richiede uno o due secondi per essere decodificata.  

In questo tutorial ti mostreremo un modo pulito e non bloccante per **eseguire OCR su più immagini** contemporaneamente, **estrarre testo da file PNG** e **convertire immagine in testo** usando un moderno motore OCR per Python. Alla fine avrai uno script pronto all'uso che potrai inserire in qualsiasi progetto – perfetto per un rapido *python ocr tutorial* o per un lavoro batch di livello produzione.

## Cosa Costruirai

- Inizializzare un motore OCR e impostare la sua lingua su Latino (o qualsiasi lingua ti serva).  
- Fornire al motore un elenco di percorsi immagine (PNG nel nostro esempio).  
- Avviare un'operazione batch che restituisce un oggetto simile a Future.  
- Recuperare tutti i risultati in modo concorrente con un thread pool, mantenendo libero il thread principale.  
- Stampare il testo riconosciuto per ogni pagina, separato in modo chiaro.

Nessuna magia nascosta, solo puro Python e una libreria OCR di terze parti (useremo il pacchetto fittizio `pyocr` per illustrazione).  

**Prerequisiti**  
- Python 3.8+ installato.  
- Familiarità di base con le funzioni Python e `concurrent.futures`.  
- Accesso a una libreria OCR che espone una classe `OcrEngine` (ad es., `pip install pyocr`).  

Se ti manca qualcuno di questi, procurateli subito – è più facile di quanto pensi.

---

## Come eseguire OCR batch in Python – Concetti fondamentali

Prima di immergerci nel codice, rispondiamo al “perché” dietro ogni passaggio.

1. **Perché impostare la lingua?**  
   La precisione dell'OCR aumenta drasticamente quando il motore sa quali caratteri aspettarsi. Il Latino funziona per inglese, francese, spagnolo, ecc. Passa a `Language.Japanese` o `Language.Arabic` se necessario.

2. **Perché usare un'operazione batch?**  
   Una chiamata batch consente al motore di pianificare il lavoro internamente, spesso sfruttando thread nativi o accelerazione GPU. Restituisce un handle che puoi interrogare in seguito, il che significa che non blocchi mentre ogni immagine viene elaborata.

3. **Perché un ThreadPoolExecutor?**  
   L'oggetto Future che riceviamo è *lazy* – inizia a recuperare i risultati solo quando lo chiediamo. Passando un thread pool a `getAll`, lasciamo che Python recuperi il testo di ogni pagina in parallelo, riducendo drasticamente il tempo di esecuzione complessivo.

4. **Perché enumerare i risultati?**  
   L'ordine dei risultati corrisponde all'ordine dei percorsi di input, così possiamo etichettare in modo sicuro il numero di ogni pagina.

Comprendere questi “perché” ti aiuta ad adattare il modello ad altre librerie o a set di dati più grandi.

---

## Passo 1: Installa e importa i pacchetti necessari

Per prima cosa, assicurati che la libreria OCR sia installata. L'esempio utilizza un pacchetto generico `pyocr`; sostituiscilo con la libreria reale che preferisci (ad es., `pytesseract`, `easyocr`).

```bash
pip install pyocr
```

Ora importa tutto il necessario.

```python
# Standard library imports
import concurrent.futures
from pathlib import Path

# Third‑party OCR library (hypothetical)
from pyocr import OcrEngine, Language
```

> **Consiglio:** Usare `Path` da `pathlib` rende il tuo script indipendente dal sistema operativo e più facile da leggere.

---

## Passo 2: Crea il motore OCR e imposta la lingua

Creare il motore è semplice. Lo bloccheremo su Latino per questa demo.

```python
# Step 2: Initialise the OCR engine
engine = OcrEngine()
engine.setLanguage(Language.Latin)   # Change to Language.YourChoice if needed
```

La chiamata `setLanguage` è opzionale per alcuni motori, ma è una buona abitudine. Indica al modello OCR di concentrarsi sul set di caratteri di tuo interesse, migliorando sia la velocità che la precisione.

---

## Passo 3: Elenca i file immagine da elaborare (Estrarre testo da PNG)

Raccogli tutti i file PNG che vuoi convertire. Usare `Path.glob` ti permette di inserire un'intera cartella senza modificare lo script.

```python
# Step 3: Gather PNG images – this is the “extract text from png” part
image_dir = Path("YOUR_DIRECTORY")   # Replace with your actual folder
image_paths = sorted(image_dir.glob("*.png"))   # Returns a list of Path objects

# Convert Path objects to strings for the OCR library (if required)
image_paths = [str(p) for p in image_paths]

if not image_paths:
    raise FileNotFoundError("No PNG files found in the specified directory.")
```

> **Perché è importante:** Ordinando la lista garantiamo un ordine deterministico, che in seguito allinea ogni risultato con il numero di pagina corretto.

---

## Passo 4: Avvia un'operazione OCR batch (Convertire immagine in testo)

Ora passiamo la lista al motore. Il metodo restituisce un contenitore simile a Future che interrogheremo più tardi.

```python
# Step 4: Start batch OCR – returns a Future‑like object
batch_future = engine.ocrBatch(image_paths)
```

Nel backend il motore può avviare i propri thread di lavoro o anche una pipeline GPU. Tutto ciò che ci interessa è avere un handle (`batch_future`) che sappia come recuperare i risultati individuali.

---

## Passo 5: Recupera tutti i risultati in modo concorrente (OCR più immagini)

Qui è dove realmente *batchiamo* il lavoro. Passando un `ThreadPoolExecutor` a `getAll`, il testo di ogni pagina viene recuperato nel proprio thread.

```python
# Step 5: Pull results using a thread pool – this speeds up OCR multiple images
with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    # getAll returns a list of Result objects in the same order as image_paths
    results = batch_future.getAll(executor)
```

Puoi regolare `max_workers` in base ai core della tua CPU o alle raccomandazioni della libreria OCR. Più worker ≠ sempre più veloce – controlla l'uso della CPU.

---

## Passo 6: Stampa il testo riconosciuto (Finale del tutorial Python OCR)

Infine, stampa il testo di ogni pagina. L'oggetto `Result` espone `getText()` – modifica se la tua libreria usa un nome di metodo diverso.

```python
# Step 6: Display the recognised text for each page
for i, result in enumerate(results):
    print(f"--- Page {i + 1} ---")
    print(result.getText())
    print()   # Blank line for readability
```

**Output previsto (esempio)**

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna...

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco...
```

Se qualche immagine fallisce, la maggior parte dei motori inserisce una stringa vuota o solleva un'eccezione – puoi avvolgere il ciclo in un blocco `try/except` per gestire i casi limite in modo elegante.

---

## Script completo – Pronto da eseguire

Di seguito trovi lo script completo e autonomo. Copialo in un file chiamato `batch_ocr.py`, modifica `YOUR_DIRECTORY` e esegui `python batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script – processes all PNG files in a directory.
Demonstrates how to batch OCR, OCR multiple images, extract text from PNG,
and convert image to text using a Python OCR engine.
"""

import concurrent.futures
from pathlib import Path

# Replace with your actual OCR library import
from pyocr import OcrEngine, Language

def main():
    # Initialise OCR engine
    engine = OcrEngine()
    engine.setLanguage(Language.Latin)

    # Locate PNG files
    image_dir = Path("YOUR_DIRECTORY")          # <‑‑ change this
    image_paths = sorted(image_dir.glob("*.png"))
    image_paths = [str(p) for p in image_paths]

    if not image_paths:
        raise FileNotFoundError("No PNG files found in the specified directory.")

    # Start batch OCR
    batch_future = engine.ocrBatch(image_paths)

    # Retrieve results concurrently
    with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
        results = batch_future.getAll(executor)

    # Print each page's recognised text
    for i, result in enumerate(results):
        print(f"--- Page {i + 1} ---")
        print(result.getText())
        print()

if __name__ == "__main__":
    main()
```

Salva, esegui e osserva la console riempirsi del testo estratto. Semplice, veloce e completamente asincrono.

---

## Problemi comuni e come evitarli

| Problema | Perché succede | Soluzione |
|----------|----------------|-----------|
| **Nessun output** – stringhe vuote | Il motore OCR non è riuscito a trovare testo (immagine troppo rumorosa) | Pre‑processare le immagini: binarizzare, raddrizzare o aumentare DPI |
| **`FileNotFoundError`** | Percorso della directory errato o file PNG mancanti | Ricontrolla `YOUR_DIRECTORY` e assicurati che i file terminino con `.png` |
| **Elevato utilizzo CPU** | `max_workers` impostato troppo alto per la tua macchina | Riduci `max_workers` o abilita l'accelerazione GPU se supportata |
| **Testo Unicode confuso** | Il motore è tornato a una lingua diversa | Chiama `engine.setLanguage(Language.Latin)` (o appropriata) prima del batch OCR |

Affrontare questi problemi in anticipo ti fa risparmiare ore di debug.

---

## Estendere il tutorial – Prossimi passi

- **Eseguire OCR su più immagini** in altri formati (JPEG, TIFF) – basta cambiare il pattern glob.  
- **Estrarre testo da PNG** e inserirlo in un indice di ricerca (ad es., Elasticsearch).  
- **Convertire immagine in testo** per la generazione di PDF usando `reportlab` o `PyPDF2`.  
- **Parallelizzare su più macchine** con `multiprocessing` o una coda di task come Celery per dataset massivi.  

Ognuno di questi argomenti si costruisce naturalmente sul **python ocr tutorial** appena completato.

---

## Conclusione

Abbiamo illustrato **come eseguire OCR batch** su una collezione di file PNG, dimostrato la potenza di un'API orientata al batch e mostrato come **estrarre testo da PNG** con un approccio basato su thread pool. Lo script completo sopra è pronto per la produzione, e ora hai una solida base per qualsiasi progetto Python con uso intensivo di OCR.

Provalo, modifica le impostazioni della lingua, e magari sostituisci `pyocr` con `pytesseract` – il modello rimane lo stesso. Hai domande o vuoi condividere un caso d'uso interessante? Lascia un commento e continuiamo la conversazione.

*Buona programmazione!*

## Cosa dovresti imparare dopo?

- [Estrarre testo da immagine con Aspose OCR – Guida passo‑per‑passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Estrarre testo da immagini usando l'operazione OCR su cartelle](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Come eseguire OCR batch su immagini con lista in Aspose.OCR per .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}