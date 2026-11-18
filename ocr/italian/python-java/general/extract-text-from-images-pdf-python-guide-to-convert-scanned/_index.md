---
category: general
date: 2026-06-06
description: Estrai il testo da PDF di immagini usando OCR in Python. Scopri come
  convertire rapidamente documenti scansionati in testo con riconoscimento batch asincrono.
draft: false
keywords:
- extract text from images pdf
- convert scanned documents to text
- python ocr batch processing
- asynchronous OCR python
- image to text conversion
language: it
og_description: Estrai il testo da immagini PDF con Python. Questa guida passo passo
  mostra come convertire i documenti scansionati in testo usando OCR asincrono.
og_title: Estrai testo da PDF di immagini – Tutorial OCR in Python
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from images pdf using Python OCR. Learn how to convert
    scanned documents to text quickly with async batch recognition.
  headline: Extract Text from Images PDF – Python Guide to Convert Scanned Documents
    to Text
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Estrai testo da PDF di immagini – Guida Python per convertire documenti scansionati
  in testo
url: /it/python-java/general/extract-text-from-images-pdf-python-guide-to-convert-scanned/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai Testo da PDF Immagini – Guida Python per Convertire Documenti Scansionati in Testo

Hai mai avuto bisogno di **estrarre testo da PDF immagini** senza passare ore a riscrivere? In questa guida ti mostreremo come **convertire documenti scansionati in testo** usando un semplice flusso di lavoro OCR asincrono in Python.  

Se ti sei mai trovato davanti a una pila di PDF scansionati e hai pensato: “Deve esserci un modo più veloce”, sei nel posto giusto. Esamineremo ogni riga di codice, spiegheremo perché ogni pezzo è importante e tratteremo anche alcuni casi limite che potresti incontrare.

## Cosa Imparerai

- Come avviare un motore OCR e impostare la lingua di riconoscimento.  
- La meccanica di alimentare un elenco misto di PNG e PDF in un riconoscitore batch.  
- Eseguire il lavoro OCR in modo asincrono così la tua app rimane reattiva.  
- Recuperare i risultati, abbinarli ai file di origine e stampare un output pulito.  

**Prerequisiti**: Python 3.8+, una conoscenza di base di `asyncio` o `concurrent.futures`, e una libreria OCR che esponga una classe `OcrEngine` simile a quella dell’esempio (ad es., Aspose.OCR, wrapper Tesseract, o un wrapper personalizzato). Nessuna configurazione complessa—basta installare la libreria e sei pronto a partire.

![estrai testo da PDF immagini](https://example.com/placeholder.png "Screenshot dell'output OCR – estrai testo da PDF immagini")

## Estrai Testo da PDF Immagini – Configurare il Motore OCR

La prima cosa di cui hai bisogno è un'istanza del motore OCR configurata per la lingua dei tuoi documenti. Nel nostro caso useremo il francese, ma puoi sostituirla con qualsiasi lingua supportata.

```python
# Import the OCR library – replace with your actual import
from ocr import OcrEngine, Language

# Step 1: Create and configure the OCR engine
engine = OcrEngine()
engine.set_recognition_language(Language.FRENCH)   # Change to Language.ENGLISH, etc.
```

**Perché è importante**: impostare la lingua in anticipo migliora drasticamente la precisione. Il motore utilizza dizionari e modelli di caratteri specifici per lingua; fornire la lingua sbagliata è una causa comune di output confuso.

## Preparare l'Elenco dei File – Immagini e PDF Insieme

Il nostro riconoscitore batch può gestire sia immagini raster (`.png`, `.jpg`) sia contenitori PDF. Basta fornire una semplice lista Python di percorsi file.

```python
# Step 2: Define the files to be processed (use your own directory)
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.pdf"
]
```

**Suggerimento**: mantieni la lista piatta; il motore estrarrà internamente ogni pagina PDF in immagini prima del riconoscimento. Se hai migliaia di file, considera di suddividere la lista in batch più piccoli per evitare picchi di memoria.

## Avviare il Riconoscimento Batch Asincrono

Invece di bloccare il thread principale, avviamo il lavoro OCR in background. Il metodo restituisce un `Future` che conterrà eventualmente una lista di oggetti `OcrResult`.

```python
# Step 3: Start asynchronous batch recognition
future = engine.recognize_batch_async(files)   # returns a Future[List[OcrResult]]
```

**Come funziona**: sotto il cofano il motore avvia un pool di thread (o un task asincrono, a seconda dell'implementazione). Questo ti permette di continuare a fare altre cose—come aggiornare un’interfaccia, scaricare altri file o registrare l’avanzamento—mentre il lavoro pesante avviene altrove.

## Fai Qualcosa di Utile Mentre l'OCR è in Esecuzione

Un errore comune è stare inattivi e interrogare il future in un ciclo stretto. Invece, puoi eseguire qualsiasi lavoro non correlato. Per dimostrazione, stamperemo semplicemente una riga di stato.

```python
# Step 4: Perform other work while OCR runs
print("Batch started – doing other work...")
# Imagine you could be uploading files, sending heartbeats, etc.
```

## Raccogliere i Risultati Una Volta che il Future è Completo

Quando sei pronto a raccogliere l'output OCR, usa `as_completed` da `concurrent.futures`. Questo schema funziona sia con un future sia con molti.

```python
from concurrent.futures import as_completed

# Step 5: Wait for the batch to finish and retrieve the results
for completed in as_completed([future]):
    ocr_results = completed.result()   # List[OcrResult] in the same order as `files`
    for path, result in zip(files, ocr_results):
        print(f"{path} →\n{result.text}\n")
```

**Ciò che vedrai**: ogni percorso file seguito dalla rappresentazione di testo semplice estratta. Per i PDF, `result.text` contiene il testo concatenato di tutte le pagine.

### Output Atteso (esempio)

```
YOUR_DIRECTORY/doc1.png →
Bonjour, ceci est un test d’OCR.

YOUR_DIRECTORY/doc2.png →
Le texte de la deuxième image apparaît ici.

YOUR_DIRECTORY/doc3.pdf →
Page 1 du PDF : Lorem ipsum dolor sit amet…
Page 2 du PDF : Consectetur adipiscing elit…
```

Se noti caratteri mancanti, verifica che la lingua impostata corrisponda a quella del documento e considera di pre‑processare le immagini (raddrizzare, aumentare il contrasto) prima di passarle al motore.

## Gestire i Casi Limite e le Trappole Comuni

| Situazione | Cosa Fare |
|------------|-----------|
| **Lingue miste** | Esegui prima una fase di rilevamento della lingua, poi istanzia motori separati per ciascuna lingua. |
| **PDF di grandi dimensioni (> 100 MB)** | Dividi il PDF in pagine individuali su disco (ad es., usando `PyPDF2`) e alimentale come voci separate. |
| **Script non latini** | Assicurati che la libreria OCR includa il pacchetto linguistico necessario; alcune librerie richiedono il download di file dati aggiuntivi. |
| **Collo di bottiglia delle prestazioni** | Aumenta la dimensione del pool di thread (`engine.set_thread_pool_size(8)`) o passa a un backend accelerato da GPU se disponibile. |
| **Testo mancante in immagini a bassa risoluzione** | Pre‑processa con OpenCV: `cv2.resize`, `cv2.threshold` e `cv2.medianBlur` per migliorare la leggibilità. |

## Esempio Completo Funzionante (Pronto per Copia‑Incolla)

```python
# ------------------------------------------------------------
# Full script: extract text from images pdf – async OCR batch
# ------------------------------------------------------------
import os
from concurrent.futures import as_completed
# Replace the import below with the actual OCR library you use
from ocr import OcrEngine, Language, OcrResult

def main():
    # 1️⃣ Initialize OCR engine
    engine = OcrEngine()
    engine.set_recognition_language(Language.FRENCH)   # Change as needed

    # 2️⃣ Build list of files (images + PDFs)
    base_dir = "YOUR_DIRECTORY"
    files = [
        os.path.join(base_dir, "doc1.png"),
        os.path.join(base_dir, "doc2.png"),
        os.path.join(base_dir, "doc3.pdf")
    ]

    # 3️⃣ Launch async batch recognition
    future = engine.recognize_batch_async(files)

    # 4️⃣ Do other work – here we just print a placeholder
    print("Batch started – doing other work...")

    # 5️⃣ Retrieve results when ready
    for completed in as_completed([future]):
        ocr_results = completed.result()   # List[OcrResult]
        for path, result in zip(files, ocr_results):
            print(f"{path} →\n{result.text}\n")

if __name__ == "__main__":
    main()
```

Salva questo file come `extract_text_async.py`, sostituisci `YOUR_DIRECTORY` con il percorso dei tuoi file, installa il pacchetto OCR (`pip install your-ocr-lib`) ed esegui `python extract_text_async.py`. Dovresti vedere l'output console illustrato in precedenza.

## Prossimi Passi – Oltre l'Estrazione Base

- **Post‑elaborazione**: rimuovi spazi bianchi extra, normalizza Unicode (`unicodedata.normalize`) o esegui un correttore ortografico per pulire il rumore OCR.  
- **Output strutturato**: esporta i risultati in CSV, JSON o direttamente in un database per ricerche successive.  
- **Batch paralleli**: se hai centinaia di file, avvia più future e usa una coda per tenere occupata la CPU senza sovraccaricare la memoria.  
- **Integrare con framework web**: collega questo script a un endpoint Flask o FastAPI per fornire OCR on‑demand come servizio.

---

### TL;DR

Ora sai come **estrarre testo da PDF immagini** con uno script Python minimale che esegue OCR in modo asincrono, permettendoti di **convertire documenti scansionati in testo** mentre il tuo programma resta reattivo. Gioca con le impostazioni della lingua, le dimensioni dei batch e le tecniche di pre‑processamento per ottenere la massima precisione possibile.

Hai un trucco da condividere—magari OCR su note scritte a mano o un servizio basato su cloud? Lascia un commento e buona programmazione!

## Cosa Dovresti Imparare Dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrai Testo da Immagine con Aspose OCR – Guida Passo‑Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Estrai Testo da Immagini Usando l'Operazione OCR su Cartelle](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Estrai Testo da Immagini Usando Aspose.OCR – Caratteri Consentiti](/ocr/english/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}