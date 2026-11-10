---
category: general
date: 2026-06-22
description: Tutorial OCR batch in Python che mostra come eseguire OCR multithread
  su una cartella di immagini PNG usando Tesseract e pathlib. Impara l'OCR veloce
  di immagini in batch con Python.
draft: false
keywords:
- python batch ocr tutorial
- multithreaded OCR in Python
- tesseract OCR batch processing
- pathlib image handling
- OCR thread count optimization
language: it
og_description: Il tutorial Python batch OCR ti guida attraverso uno script completo
  e eseguibile che elabora numerosi PNG con Tesseract usando più thread.
og_title: Tutorial OCR batch in Python – OCR multithread veloce per immagini PNG
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  headline: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  type: TechArticle
- description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  name: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  steps:
  - name: '**Collects** every PNG with **pathlib image handling**.'
    text: '**Collects** every PNG with **pathlib image handling**.'
  - name: '**Spins up** a **multithreaded OCR in Python** worker pool.'
    text: '**Spins up** a **multithreaded OCR in Python** worker pool.'
  - name: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
    text: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
  - name: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
    text: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
  type: HowTo
tags:
- OCR
- Python
- Batch Processing
title: 'Tutorial OCR batch in Python: elabora più PNG in modo efficiente'
url: /it/python-java/general/python-batch-ocr-tutorial-process-multiple-pngs-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# python batch ocr tutorial – OCR multithread veloce per immagini PNG

Ti sei mai chiesto come **python batch ocr tutorial** attraversare centinaia di screenshot PNG senza vedere la tua CPU sciogliersi? Non sei l'unico. Che tu stia digitalizzando moduli scansionati, estraendo testo da ricevute o creando un archivio ricercabile, una solida pipeline OCR batch ti fa risparmiare ore.

In questa guida creeremo uno script piccolo ma potente che raccoglie tutti i `*.png` in una cartella, li passa a Tesseract tramite un processore multithread e salva i risultati in testo semplice in una cartella di output ordinata. Nessuna libreria misteriosa—solo `pathlib`, `concurrent.futures` e l'affidabile `pytesseract`. Alla fine avrai un **python batch ocr tutorial** che potrai copiare‑incollare in qualsiasi progetto.

## Cosa Imparerai

- Come raccogliere file immagine con **pathlib image handling**  
- Configurare un pool di worker **multithreaded OCR in Python**  
- Ottimizzare **OCR thread count optimization** per i core della tua CPU  
- Salvare ogni risultato con uno schema di denominazione chiaro per ricerche future  
- Eseguire il tutto come script unico e autonomo  

## Prerequisiti (Cosa Ti Serve Prima)

| Requisito | Perché è Importante |
|-------------|----------------|
| Python 3.9+ | Sintassi moderna (`pathlib`, f‑strings) |
| Tesseract 5.x installato e accessibile in `PATH` | Il motore OCR dietro `pytesseract` |
| `pytesseract` (`pip install pytesseract`) | Wrapper Python per Tesseract |
| `Pillow` (`pip install pillow`) | Caricamento immagini per Tesseract |
| Una cartella di file PNG da elaborare | Il nostro obiettivo **tesseract OCR batch processing** |

> **Consiglio Pro:** Se sei su Windows, aggiungi `C:\Program Files\Tesseract-OCR` al tuo `PATH` di sistema così `pytesseract` può trovare l'eseguibile automaticamente.

---

## Passo 1 – Raccogli Tutte le Immagini PNG (Usando pathlib)

Prima di tutto: abbiamo bisogno di un elenco di tutte le immagini su cui eseguire l'OCR. `pathlib` rende questo un'unica riga e mantiene il codice indipendente dal sistema operativo.

```python
import pathlib

# Adjust the path to point at your source folder
source_dir = pathlib.Path("YOUR_DIRECTORY/batch_images")
image_files = list(source_dir.glob("*.png"))

print(f"Found {len(image_files)} PNG files to process.")
```

*Perché `pathlib`?* Astrae le barre rovesciate di Windows da quelle di Unix, permettendo allo stesso script di funzionare ovunque. Questo è il fondamento di **pathlib image handling** nel nostro tutorial.

---

## Passo 2 – Definisci una Classe Semplice per il Processore OCR Batch

Di seguito è un wrapper leggero che nasconde il boilerplate del threading. Rispecchia il pseudo‑codice mostrato prima ma è pienamente funzionale.

```python
import concurrent.futures
import pytesseract
from PIL import Image
import os

class BatchOcrProcessor:
    """Encapsulates multithreaded OCR logic."""

    def __init__(self):
        self.thread_count = os.cpu_count() or 4  # sensible default
        self.output_folder = pathlib.Path("ocr_results")
        self.output_folder.mkdir(parents=True, exist_ok=True)

    def set_thread_count(self, count: int):
        """Adjust the number of worker threads (OCR thread count optimization)."""
        if count < 1:
            raise ValueError("Thread count must be at least 1")
        self.thread_count = count
        print(f"Thread pool size set to {self.thread_count}")

    def set_output_folder(self, folder: str):
        """Where each OCR result will be saved (tesseract OCR batch processing)."""
        self.output_folder = pathlib.Path(folder)
        self.output_folder.mkdir(parents=True, exist_ok=True)
        print(f"Output folder set to {self.output_folder}")

    def _process_single(self, image_path: pathlib.Path):
        """Run OCR on a single image and write the text file."""
        try:
            img = Image.open(image_path)
            text = pytesseract.image_to_string(img)
            out_file = self.output_folder / f"{image_path.stem}.txt"
            out_file.write_text(text, encoding="utf-8")
            return f"✅ {image_path.name} → {out_file.name}"
        except Exception as exc:
            return f"❌ {image_path.name} failed: {exc}"

    def process(self, image_paths):
        """Run OCR on the entire batch using a thread pool."""
        print("🚀 Starting batch OCR...")
        with concurrent.futures.ThreadPoolExecutor(max_workers=self.thread_count) as executor:
            results = list(executor.map(self._process_single, image_paths))
        for line in results:
            print(line)
        print("🏁 Batch OCR completed.")
```

**Spiegazione delle scelte chiave**

- **ThreadPoolExecutor** ci fornisce vero multithreading per compiti I/O‑bound come la lettura di file e l'invocazione del binario esterno Tesseract.  
- Il metodo `set_thread_count` è dove puoi sperimentare con **OCR thread count optimization**; più thread spesso significano maggiore velocità fino al punto in cui i core della CPU si saturano.  
- Ogni immagine produce un file `.txt` con lo stesso nome del PNG originale—perfetto per indicizzazione o ricerca successiva.

---

## Passo 3 – Collegare Tutto Insieme

Adesso istanziamo il processore, impostiamo il conteggio dei thread, lo puntiamo alla nostra cartella di output e infine gli passiamo l'elenco delle immagini.

```python
if __name__ == "__main__":
    # 1️⃣ Gather PNGs (already done above)
    # 2️⃣ Create processor instance
    ocr_processor = BatchOcrProcessor()

    # 3️⃣ Configure thread pool – feel free to change 8 → your core count
    ocr_processor.set_thread_count(8)   # multithreaded OCR in Python

    # 4️⃣ Choose where results land
    ocr_processor.set_output_folder("YOUR_DIRECTORY/ocr_results")

    # 5️⃣ Run the batch – this call blocks until everything is done
    ocr_processor.process(image_files)

    # 6️⃣ All done – a friendly console message
    print("✅ All images processed. Check the ocr_results folder.")
```

Eseguendo lo script otterrai un output simile a:

```
Found 42 PNG files to process.
Thread pool size set to 8
Output folder set to YOUR_DIRECTORY/ocr_results
🚀 Starting batch OCR...
✅ invoice_001.png → invoice_001.txt
✅ receipt_2023-04-15.png → receipt_2023-04-15.txt
...
🏁 Batch OCR completed.
✅ All images processed. Check the ocr_results folder.
```

Ogni `.txt` contiene l'output OCR grezzo. Apri qualsiasi file e vedrai il testo estratto pronto per indicizzazione, analisi del sentiment o qualsiasi altra operazione successiva.

---

## Passo 4 – Problemi Comuni & Come Evitarli

| Sintomo | Probabile Causa | Soluzione |
|---------|----------------|-----------|
| File `.txt` vuoti | Tesseract non trova i dati della lingua o l'immagine è troppo scura | Installa i pacchetti lingua (`tesseract-ocr-eng`) e preelabora le immagini (aumenta il contrasto). |
| `UnicodeDecodeError` durante la lettura dei risultati | L'output contiene caratteri non‑UTF‑8 | Scrivi i file con `encoding="utf-8"` (già nel codice) o usa `errors="ignore"` per una soluzione rapida. |
| Picchi di CPU, nessun guadagno di velocità | Il conteggio dei thread supera i core fisici | Riduci `set_thread_count` a `os.cpu_count()` o meno. |
| `FileNotFoundError` durante l'apertura dell'immagine | Il percorso contiene caratteri non‑ASCII su Windows | Anteponi la stringa con `r` o usa direttamente oggetti `pathlib` (come facciamo noi). |

---

## Passo 5 – Estendere il Tutorial (Prossimi Passi)

- **Aggiungi pre‑elaborazione delle immagini** con OpenCV (`cv2`) per migliorare l'accuratezza OCR (es., correzione inclinazione, soglia).  
- **Parallelizza su più macchine** usando `multiprocessing` o una semplice coda di task come RabbitMQ per carichi di lavoro massivi.  
- **Integra con un motore di ricerca** (Elasticsearch) per rendere il testo estratto ricercabile in tempo reale.  
- **Sostituisci Tesseract con un'API OCR cloud** (Google Vision, Azure Computer Vision) se ti serve maggiore accuratezza su testo scritto a mano.

Tutte queste idee si basano sulla fondazione che ora possiedi: un **python batch ocr tutorial** pulito che funziona subito.

---

## Conclusione

Hai appena costruito un **python batch ocr tutorial** completo che:

1. **Raccoglie** ogni PNG con **pathlib image handling**.  
2. **Avvia** un pool di worker **multithreaded OCR in Python**.  
3. **Ottimizza** il numero di thread per il tuo hardware (**OCR thread count optimization**).  
4. **Scrive** ogni risultato in una cartella dedicata (**tesseract OCR batch processing**).  

Lo script è pronto per essere inserito in qualsiasi pipeline, che tu stia elaborando ricevute, documenti legali o una montagna di screenshot. Gioca con il conteggio dei thread, aggiungi pre‑elaborazione delle immagini o collega l'output a un database—a te la scelta.

Hai domande? Sentiti libero di commentare qui sotto, e buona programmazione!

![Diagramma del flusso di lavoro del python batch ocr tutorial che elabora più file PNG in parallelo](/images/python-batch-ocr-workflow.png){.center width=600 alt="flusso di lavoro python batch ocr tutorial"}

---


## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Tutorial Aspose OCR – Riconoscimento Ottico dei Caratteri](/ocr/english/)
- [Come eseguire OCR batch di immagini con List in Aspose.OCR per .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Estrai testo da immagine C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}