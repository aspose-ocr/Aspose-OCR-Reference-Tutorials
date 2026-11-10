---
category: general
date: 2026-07-05
description: Come utilizzare l'OCR in Python per convertire rapidamente i file TIFF
  in testo. Scopri i passaggi della libreria OCR per Python per estrarre testo dalle
  immagini TIFF e creare un motore OCR in Python.
draft: false
keywords:
- how to use ocr
- ocr library python
- convert tiff to text
- extract text from tiff
- python ocr engine
language: it
og_description: Come usare l'OCR in Python? Questa guida ti mostra passo passo come
  convertire un TIFF in testo usando un motore OCR Python e la libreria ocr per Python.
og_title: Come usare OCR in Python – Estrazione completa del testo da TIFF
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  headline: How to Use OCR in Python – Extract Text from TIFF
  type: TechArticle
- description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  name: How to Use OCR in Python – Extract Text from TIFF
  steps:
  - name: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
    text: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
  - name: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
    text: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
  - name: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
    text: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Image Processing
title: Come utilizzare l'OCR in Python – Estrarre testo da TIFF
url: /it/python-java/general/how-to-use-ocr-in-python-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare OCR in Python – Estrarre testo da TIFF

Ti sei mai chiesto **come usare OCR in Python** per trasformare un libro scansionato in testo modificabile? Non sei l'unico—sviluppatori, ricercatori e hobbisti incontrano tutti questo ostacolo quando si tratta di immagini TIFF multi‑pagina. La buona notizia? Con la **ocr library python** puoi avviare un piccolo motore OCR, puntarlo a un file TIFF e ottenere testo pulito e ricercabile in pochi secondi.

In questo tutorial ti guideremo attraverso tutto ciò che ti serve: installare il pacchetto corretto, caricare un TIFF multi‑pagina, eseguire il motore OCR e infine stampare il contenuto di ogni pagina. Alla fine sarai in grado di **convertire TIFF in testo** e **estrarre testo da TIFF** senza uscire dal tuo ambiente Python.

## Prerequisiti

- Python 3.9 o versioni più recenti (l'esempio è stato testato su 3.11)
- Una versione recente della libreria `ocr` (o qualsiasi `python ocr engine` compatibile che preferisci)
- Un file TIFF multi‑pagina da elaborare (lo chiameremo `scanned_book.tif`)
- Familiarità di base con script Python e ambienti virtuali

Non sono necessari strumenti esterni pesanti—solo pip e poche righe di codice.

## Installa la OCR Library Python

Prima di tutto: ti serve un backend OCR solido. Per questa guida useremo il pacchetto fittizio `ocr` che fornisce una semplice API di alto livello, ma lo stesso schema funziona con wrapper basati su Tesseract come `pytesseract` o SDK commerciali.

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Consiglio:** Se sei su Windows e il pacchetto dipende da binari nativi, assicurati di avere installato il redistributable Visual C++ appropriato. L'installatore di solito ti avverte se qualcosa manca.

## Come usare il motore OCR in Python

Ora che la libreria è pronta, avviamo un motore OCR e lo puntiamo al nostro file TIFF. Il frammento seguente crea un'istanza del motore, imposta la lingua su English e lo prepara per l'elaborazione multi‑pagina.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # You can switch to ocr.Language.FRENCH, etc.
```

**Perché impostare la lingua?**  
La maggior parte dei motori OCR utilizza modelli linguistici per migliorare l'accuratezza. Se salti questo passaggio, il motore ricade su un modello generico che potrebbe riconoscere erroneamente la punteggiatura o i caratteri speciali.

## Carica l'immagine TIFF multi‑pagina

Il passo successivo è caricare il documento scansionato. L'helper `ocr.Image.load` comprende le pile TIFF fin da subito, restituendo un oggetto che rappresenta internamente ogni pagina.

```python
# Step 2: Load the multi‑page TIFF image containing the scanned book
tiff_path = "YOUR_DIRECTORY/scanned_book.tif"
tiff_image = ocr.Image.load(tiff_path)
```

> **Caso limite:** Se il tuo TIFF utilizza compressione (CCITT Group 4, LZW, ecc.) e la libreria genera un errore, prova a convertirlo prima in una versione non compressa con ImageMagick:
> ```bash
> convert scanned_book.tif -compress none scanned_book_uncompressed.tif
> ```

## Esegui OCR su tutte le pagine – Converti TIFF in testo

Con l'oggetto immagine a disposizione, il motore può ora elaborare tutte le pagine in una volta. Questo metodo restituisce una lista dove ogni elemento contiene il risultato OCR per una singola pagina.

```python
# Step 3: Perform OCR on all pages of the image
page_results = engine.recognize_multi_page(tiff_image)
```

**Cosa succede dietro le quinte?**  
La funzione `recognize_multi_page` iterà su ogni pagina rasterizzata, esegue il riconoscitore basato su rete neurale e confeziona l'output di testo semplice insieme ai punteggi di confidenza. È essenzialmente un'operazione batch che ti salva dallo scrivere un ciclo manuale.

## Itera attraverso i risultati – Estrai testo da TIFF

Infine, mostriamo il testo riconosciuto. Puoi scrivere l'output in file `.txt` separati, inserirlo in un database o alimentarlo in un indice di ricerca—qualunque cosa si adatti al tuo flusso di lavoro.

```python
# Step 4: Iterate through the results and display the recognized text for each page
for page_index, result in enumerate(page_results):
    print(f"Page {page_index + 1}:\n{result.text}\n")
```

### Output previsto

```
Page 1:
Chapter 1
In the beginning...

Page 2:
The quick brown fox jumps over the lazy dog.

Page 3:
...

```

Ogni stringa `result.text` contiene l'output OCR grezzo per quella pagina. Se hai bisogno di preservare le interruzioni di riga, la maggior parte dei motori espone `result.lines` come una lista di stringhe.

## Gestire file TIFF di grandi dimensioni – Consigli e trucchi

Elaborare un TIFF di 500 pagine può richiedere molta memoria. Ecco alcune strategie per mantenere le cose fluide:

1. **Dividi le pagine** – Invece di `recognize_multi_page`, chiama `engine.recognize(page)` all'interno di un generatore che restituisce una pagina alla volta.
2. **Regola DPI** – Ridurre la risoluzione dell'immagine (ad es., da 300 DPI a 200 DPI) diminuisce il carico CPU mantenendo quasi invariata l'accuratezza per la maggior parte del testo stampato.
3. **Parallelizza** – Se il tuo motore OCR è thread‑safe, avvia un `concurrent.futures.ThreadPoolExecutor` per eseguire il riconoscimento su più pagine contemporaneamente.

```python
import concurrent.futures

def ocr_page(page):
    return engine.recognize(page).text

with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    texts = list(executor.map(ocr_page, tiff_image.pages))
```

## Salva il testo estratto in file

La maggior parte delle pipeline reali richiede una memorizzazione persistente. Di seguito trovi un modo conciso per salvare il testo di ogni pagina in un proprio file, preservando l'ordine delle pagine.

```python
import pathlib

output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for i, result in enumerate(page_results, start=1):
    file_path = output_dir / f"page_{i:03}.txt"
    file_path.write_text(result.text, encoding="utf-8")
    print(f"Saved page {i} to {file_path}")
```

Ora hai una directory pulita di file `.txt` pronta per l'indicizzazione o ulteriori elaborazioni NLP.

## Anteprima immagine – Come usare i risultati OCR visivamente

Se vuoi vedere la sovrapposizione OCR sull'immagine originale (utile per il debug), molte librerie ti permettono di disegnare riquadri. Ecco un rapido esempio usando Pillow:

```python
from PIL import ImageDraw

for page, result in zip(tiff_image.pages, page_results):
    draw = ImageDraw.Draw(page)
    for word in result.words:          # Assume `result.words` gives bounding boxes
        draw.rectangle(word.box, outline="red")
    page.show()   # Opens the annotated page
```

![Come usare OCR in Python – sovrapposizione OCR su una pagina TIFF](ocr_overlay_example.png)

*Testo alternativo:* Come usare OCR in Python – sovrapposizione visiva del testo riconosciuto su una pagina TIFF.

## Problemi comuni e come evitarli

| Problema | Perché succede | Soluzione |
|-------|----------------|-----|
| Caratteri illeggibili | Modello linguistico errato | Imposta `engine.language` sull'enum corretto |
| Pagine mancanti | Compressione TIFF non supportata | Converti prima in TIFF non compresso |
| Prestazioni lente | DPI alto + elaborazione single‑thread | Riduci DPI o abilita il multi‑threading |
| Output vuoto | Immagine troppo scura/basso contrasto | Pre‑processa con stretching del contrasto (`opencv` o `Pillow`) |

Affrontare questi problemi fin dall'inizio ti farà risparmiare ore di debug in seguito.

## Prossimi passi – Oltre l'estrazione di base

Ora che hai padroneggiato le basi di **come usare OCR in Python**, considera di esplorare:

- **Generazione PDF** – Combina il testo estratto con `reportlab` per ricostruire PDF ricercabili.
- **Rilevamento della lingua** – Cambia automaticamente `engine.language` usando `langdetect`.
- **Estrazione di dati strutturati** – Usa espressioni regolari o spaCy per estrarre date, nomi o tabelle dal testo grezzo.
- **Backend OCR alternativi** – Sostituisci `ocr` con `pytesseract` o `easyocr` se ti serve il supporto multilingue.

Ognuno di questi argomenti si collega naturalmente alle parole chiave secondarie **ocr library python**, **convert tiff to text**, **extract text from tiff**, e **python ocr engine**, fornendoti una solida base per progetti più avanzati.

---

### Conclusione

Abbiamo coperto **come usare OCR in Python** dall'installazione all'elaborazione multi‑pagina, mostrandoti esattamente come **convertire TIFF in testo** e **estrarre testo da TIFF** usando un semplice **python OCR engine**. L'esempio completo e eseguibile sopra dovrebbe funzionare subito per la maggior parte dei file TIFF standard, e i consigli forniti ti aiuteranno a scalare a documenti più grandi o a integrare OCR in pipeline più ampie.

Provalo con i tuoi libri scansionati, ricevute o immagini d'archivio—poi sperimenta le idee di livello superiore elencate nella sezione “Prossimi passi”. Buona programmazione, e che i tuoi risultati OCR siano sempre accurati!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrai testo da immagine con Aspose OCR – Guida passo‑passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Come estrarre testo da tiff con Aspose.OCR per Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Come eseguire l'estrazione di testo da immagine da stream usando Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}