---
category: general
date: 2026-06-25
description: Esegui OCR su PDF con Python—impara come caricare PDF per l'OCR, estrarre
  il testo dalle pagine PDF e visualizzare in modo efficiente il testo riconosciuto.
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF pages
- load PDF for OCR
- how to OCR large PDF
- preview recognized text
language: it
og_description: Esegui OCR su PDF in Python. Questa guida mostra come caricare PDF
  per l'OCR, estrarre il testo dalle pagine PDF e visualizzare rapidamente il testo
  riconosciuto.
og_title: Esegui OCR su PDF con Python – Tutorial passo passo
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  headline: Perform OCR on PDF with Python – Complete Guide
  type: TechArticle
- description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  name: Perform OCR on PDF with Python – Complete Guide
  steps:
  - name: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
    text: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
  - name: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
    text: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
  - name: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
    text: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
  - name: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
    text: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Esegui OCR su PDF con Python – Guida completa
url: /it/python/general/perform-ocr-on-pdf-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eseguire OCR su PDF con Python – Guida Completa

Ti è mai capitato di **eseguire OCR su PDF** senza sapere da dove cominciare? Forse hai una montagna di contratti scansionati, o un unico voluminoso manuale che rifiuta di collaborare con il tuo estrattore di testo abituale. In breve, vuoi **caricare PDF per OCR**, estrarre il testo e ottenere un’anteprima rapida—tutto senza far esplodere la memoria della tua macchina.

Bene, sei nel posto giusto. In questo tutorial percorreremo uno script Python completamente funzionante che **estrae testo dalle pagine PDF**, ti mostra come **visualizzare in anteprima il testo riconosciuto**, e affronta anche il classico problema di **come fare OCR su PDF di grandi dimensioni** in modo efficiente.

Alla fine avrai un programma pronto da eseguire, una chiara comprensione di ogni impostazione configurabile, e una serie di consigli per evitare le insidie più comuni che ostacolano i principianti.

---

## Cosa Imparerai

- Come **caricare PDF per OCR** usando la libreria `aocr`.
- I passaggi esatti per **eseguire OCR su PDF** pagina per pagina.
- Modi per **estrarre testo da pagine PDF** mantenendo sotto controllo l'uso della memoria.
- Come **visualizzare in anteprima il testo riconosciuto** per verificare i risultati.
- Strategie per gestire **PDF di grandi dimensioni** senza esaurire la RAM.

> **Suggerimento:** Questa guida presuppone che tu abbia Python 3.9+ installato e una conoscenza di base degli ambienti virtuali. Se sei nuovo a Python, crea prima un virtualenv—fidati, ti farà risparmiare mal di testa in seguito.

---

## Prerequisiti

| Requisito | Perché è importante |
|-------------|----------------|
| Pacchetto Python `aocr` (o qualsiasi motore OCR compatibile) | Fornisce la classe `OcrEngine` usata nello script. |
| `pip` e un ambiente virtuale | Mantiene le dipendenze isolate dal Python di sistema. |
| Spazio su disco sufficiente per gli estratti di immagine temporanei | Alcuni motori OCR scrivono le immagini delle pagine su disco prima dell'elaborazione. |
| Opzionale: `tqdm` per le barre di avanzamento | Migliora l'esperienza utente quando si gestiscono lavori di **how to OCR large PDF**. |

Installa gli elementi essenziali con:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate
pip install aocr tqdm
```

Se il tuo PDF è protetto da password, dovrai fornire la password in seguito—vedi la sezione “Casi Limite”.

---

## Passo 1: Eseguire OCR su PDF – Configurare il Motore

Prima di tutto, ci serve un'istanza del motore OCR. Pensala come il cervello che leggerà l'immagine di ogni pagina e produrrà testo semplice.

```python
import aocr                     # The OCR library
from tqdm import tqdm           # Optional, for a nice progress bar

def create_engine():
    """
    Initialise the OcrEngine with sensible defaults.
    Returns the configured engine ready for processing.
    """
    engine = aocr.OcrEngine()
    # Limit memory usage – crucial when tackling how to OCR large PDF files
    engine.max_memory_mb = 200               # 200 MB cap, adjust if needed
    # Choose a recognition mode that matches your source material
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine
```

> **Perché impostare `max_memory_mb`?**  
> I motori OCR spesso memorizzano nella RAM le immagini delle pagine. Limitando la memoria, eviti che lo script vada in crash su un contratto di 500 pagine.

---

## Passo 2: Caricare PDF per OCR e Configurare le Impostazioni

Ora **carichiamo PDF per OCR**. Il percorso può essere assoluto o relativo; assicurati solo che il file esista.

```python
def load_pdf(engine, pdf_path):
    """
    Loads the PDF into the OCR engine.
    Raises FileNotFoundError if the file does not exist.
    """
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages ready.")
    except Exception as e:
        raise RuntimeError(f"Failed to load PDF: {e}")
```

Se il PDF è criptato, `engine.load_pdf` solleverà tipicamente un'eccezione. In tal caso puoi chiamare `engine.load_pdf(pdf_path, password="secret")`—ne parleremo più avanti.

---

## Passo 3: Estrarre Testo dalle Pagine PDF – Il Ciclo Principale

Ecco dove **eseguiamo OCR su PDF** pagina per pagina. Inoltre **visualizzeremo in anteprima il testo riconosciuto** per i primi centinaia di caratteri così potrai verificare che tutto funzioni.

```python
def ocr_pages(engine, preview_len=200):
    """
    Iterates over each page, runs OCR, and yields the recognized text.
    Also prints a short preview for each page.
    """
    for page_index in tqdm(range(engine.page_count), desc="Processing pages"):
        # Select the current page – essential for multi‑page PDFs
        engine.select_page(page_index)

        # Perform the actual OCR
        page_text = engine.recognize()

        # Preview the first `preview_len` characters (helps with debugging)
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))

        yield page_text
```

> **Consiglio professionale:** La barra di avanzamento `tqdm` ti fornisce un'indicazione visiva, particolarmente utile quando si gestiscono documenti **how to OCR large PDF** che richiedono minuti per essere processati.

---

## Passo 4: Mettere Tutto Insieme – Uno Script Pronto da Eseguire

Di seguito trovi l'esempio completo, eseguibile. Salvalo come `pdf_ocr.py` ed eseguilo con `python pdf_ocr.py path/to/your/file.pdf`.

```python
#!/usr/bin/env python3
"""
Complete script to perform OCR on PDF, extract text from PDF pages,
and preview recognized text. Works for both small and large PDFs.
"""

import sys
import aocr
from tqdm import tqdm

def create_engine():
    engine = aocr.OcrEngine()
    engine.max_memory_mb = 200
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine

def load_pdf(engine, pdf_path):
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages.")
    except Exception as exc:
        raise RuntimeError(f"Unable to load PDF: {exc}")

def ocr_pages(engine, preview_len=200):
    for page_index in tqdm(range(engine.page_count), desc="OCR progress"):
        engine.select_page(page_index)
        page_text = engine.recognize()
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))
        yield page_text

def main(pdf_path):
    engine = create_engine()
    load_pdf(engine, pdf_path)

    all_text = []
    for txt in ocr_pages(engine):
        all_text.append(txt)

    # Optional: write the combined output to a .txt file
    out_path = pdf_path.rsplit(".", 1)[0] + "_ocr.txt"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write("\n\n".join(all_text))
    print(f"\n✅ OCR complete. Full text saved to: {out_path}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python pdf_ocr.py <path_to_pdf>")
        sys.exit(1)
    pdf_file = sys.argv[1]
    main(pdf_file)
```

### Output Atteso (estratto)

```
✅ Loaded 'large_contract.pdf' – 342 pages.

--- Page 1 Preview ---
Contract Agreement between Party A and Party B ... 

--- Page 2 Preview ---
Recitals: Whereas, the parties desire to ...

...
✅ OCR complete. Full text saved to: large_contract_ocr.txt
```

Vedrai un breve anteprima per ogni pagina, seguita da una conferma finale che il file di testo concatenato è stato scritto.

---

## Casi Limite e Consigli Pratici

| Situazione | Cosa Fare |
|-----------|------------|
| **PDF Criptato** | Passare la password: `engine.load_pdf(pdf_path, password="mySecret")`. |
| **PDF molto grande (> 1000 pagine)** | Aumentare `max_memory_mb` con cautela, oppure processare a blocchi (es. 200 pagine alla volta). |
| **Contenuto misto (stampato + scritto a mano)** | Cambiare `engine.recognition_mode` a `aocr.RecognitionMode.MIXED` se la libreria lo supporta. |
| **Font mancanti o scarsa qualità della scansione** | Pre‑processare le pagine con una libreria di miglioramento immagine (es. Pillow) prima di chiamare `recognize()`. |
| **Crash per mancanza di memoria** | Ridurre `preview_len` o scrivere il testo di ogni pagina direttamente su disco invece di mantenerlo tutti in una lista. |

---

## Come Eseguire OCR su PDF di Grandi Dimensioni in Modo Efficiente – Strategie Avanzate

Quando si affronta **how to OCR large PDF**, velocità e stabilità diventano critiche. Ecco alcuni trucchi da inserire nello script:

1. **Parallelizzare per pagina** – Usa `concurrent.futures.ThreadPoolExecutor` se il motore OCR è thread‑safe.  
2. **Cache delle immagini intermedie** – Alcuni motori permettono di salvare le pagine rasterizzate su SSD, riducendo drasticamente il carico CPU nei riavvii.  
3. **Scrittura batch dell'output** – Invece di aggiungere a una lista Python, apri il file di output una volta e scrivi il testo di ogni pagina non appena è pronto.  
4. **Regolare DPI** – Ridurre il DPI durante la rasterizzazione diminuisce la memoria ma può influire sulla precisione; trova il giusto compromesso (solitamente 200‑300 DPI).  

Di seguito un breve snippet che mostra come potresti parallelizzare il passaggio OCR (opzionale, decommenta per usarlo):

```python
# from concurrent.futures import ThreadPoolExecutor

# def ocr_page(engine, idx):
#     engine.select_page(idx)
#     return engine.recognize()

# with ThreadPoolExecutor(max_workers=4) as executor:
#     results = list(tqdm(executor.map(lambda i: ocr_page(engine, i),
#                                    range(engine.page_count)),
#                     total=engine.page_count,
#                     desc="Parallel OCR"))
```

Ricorda: il parallelismo può aumentare l'uso della CPU, quindi monitora la temperatura del sistema durante esecuzioni prolungate.

---

## Domande Frequenti

**D: Posso usare questo script con altre librerie OCR come Tesseract?**  
**R:** Assolutamente. Sostituisci le chiamate `aocr` con `pytesseract.image_to

## Cosa Dovresti Imparare Dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come eseguire OCR su PDF in .NET con Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Come eseguire l'estrazione di testo da immagine da stream usando Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Come estrarre testo da immagine da URL usando Aspose.OCR per Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}