---
category: general
date: 2026-06-28
description: Come eseguire OCR in batch con Python—estrarre testo dalle immagini e
  convertire pagine scannerizzate in testo usando l'elaborazione OCR batch.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: it
og_description: Scopri come eseguire OCR in batch con Python, estrarre testo dalle
  immagini e convertire pagine scannerizzate in testo con un'elaborazione OCR batch
  efficiente.
og_title: Come eseguire OCR in batch con Python – Guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR in Python—extract text from images and convert scanned
    pages to text using batch OCR processing.
  headline: How to Batch OCR in Python – Complete Guide to Extract Text from Images
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Come fare OCR in batch con Python – Guida completa per estrarre testo dalle
  immagini
url: /it/python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR batch in Python – Guida completa per estrarre testo dalle immagini

Se ti chiedi **come eseguire OCR batch in Python**, sei nel posto giusto. Questo tutorial ti mostra un modo rapido per **estrarre testo dalle immagini** e **convertire pagine scannerizzate in testo** usando una singola istanza del motore OCR. Niente più copia‑incolla di un file dopo l'altro—lascia che sia il codice a fare il lavoro pesante.

Passeremo in rassegna tutto ciò di cui hai bisogno: installare la libreria, caricare un'intera cartella di scansioni, eseguire l'elaborazione OCR batch e gestire i risultati in modo elegante. Alla fine avrai uno script riutilizzabile che trasforma una pila di PNG o JPEG in file di testo ricercabili in pochi secondi.

## Cosa ti servirà

Prima di immergerci, assicurati di avere:

* Python 3.9+ installato (il codice funziona anche su 3.8, ma 3.9+ offre le più recenti funzionalità di typing).
* Una libreria OCR moderna—qui usiamo **Aspose.OCR for Python via .NET**, che espone la classe `OcrEngine` mostrata nello snippet originale.  
  ```bash
  pip install aspose-ocr
  ```
* Una cartella con pagine scannerizzate (`page1.png`, `page2.png`, …). Qualsiasi formato che Pillow può aprire funzionerà, quindi PDF, TIFF o BMP vanno bene.
* Un pizzico di curiosità—se non hai mai automatizzato la conversione immagine‑testo, vedrai perché l'OCR batch è una svolta.

> **Consiglio professionale:** Se preferisci una libreria puramente Python, sostituisci `OcrEngine` con `pytesseract.image_to_string`. La logica circostante rimane identica.

## Come eseguire OCR batch in Python – Guida passo‑passo

Di seguito trovi lo script completo, eseguibile. Ogni riga è commentata così puoi capire *perché* ogni parte è importante, non solo *cosa* fa.

```python
# batch_ocr.py
import os
from aspose.ocr import OcrEngine, Image  # Aspose OCR library
from typing import List

def load_images(folder: str) -> List[Image]:
    """
    Scan a directory and return a list of Aspose.Image objects.
    Supports PNG, JPEG, BMP, and TIFF out of the box.
    """
    supported_ext = {".png", ".jpg", ".jpeg", ".bmp", ".tif", ".tiff"}
    images = []
    for filename in sorted(os.listdir(folder)):
        _, ext = os.path.splitext(filename)
        if ext.lower() in supported_ext:
            path = os.path.join(folder, filename)
            try:
                img = Image.from_file(path)
                images.append(img)
            except Exception as e:
                print(f"⚠️  Could not load {filename}: {e}")
    return images

def batch_ocr_process(images: List[Image]) -> List[str]:
    """
    Perform OCR on the whole batch at once.
    Returns a list of recognized strings, one per image.
    """
    engine = OcrEngine()          # Step 1: create an OCR engine instance
    # The recognize_batch method is optimized for bulk work.
    return engine.recognize_batch(images)

def save_results(texts: List[str], output_folder: str):
    """
    Write each page's text to a separate .txt file.
    """
    os.makedirs(output_folder, exist_ok=True)
    for idx, page_text in enumerate(texts, start=1):
        out_path = os.path.join(output_folder, f"page_{idx}.txt")
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(page_text)
        print(f"✅  Saved page {idx} → {out_path}")

def main():
    # -----------------------------------------------------------------
    # 1️⃣ Load the images you want to process
    # -----------------------------------------------------------------
    image_folder = "YOUR_DIRECTORY"          # <-- replace with your path
    images = load_images(image_folder)

    if not images:
        print("❌  No supported images found. Exiting.")
        return

    # -----------------------------------------------------------------
    # 2️⃣ Perform OCR on the whole batch at once
    # -----------------------------------------------------------------
    print(f"🔎  Running batch OCR on {len(images)} images...")
    page_texts = batch_ocr_process(images)

    # -----------------------------------------------------------------
    # 3️⃣ Output the recognized text for each page
    # -----------------------------------------------------------------
    for i, txt in enumerate(page_texts, start=1):
        print(f"\n--- Page {i} ---")
        print(txt[:200] + ("…" if len(txt) > 200 else ""))  # preview first 200 chars

    # -----------------------------------------------------------------
    # 4️⃣ (Optional) Save each page's text to a file
    # -----------------------------------------------------------------
    save_results(page_texts, "ocr_output")

if __name__ == "__main__":
    main()
```

### Output previsto

Eseguendo lo script su una cartella con tre scansioni PNG otterrai qualcosa di simile a:

```
🔎  Running batch OCR on 3 images...

--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit…

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore…

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco…
✅  Saved page 1 → ocr_output/page_1.txt
✅  Saved page 2 → ocr_output/page_2.txt
✅  Saved page 3 → ocr_output/page_3.txt
```

L'anteprima mostra i primi 200 caratteri di ogni pagina, e il testo completo viene salvato nella directory `ocr_output`.

## Estrarre testo dalle immagini usando un unico motore

Perché creiamo **un solo** `OcrEngine` e lo riutilizziamo? L'istanziazione del motore può essere costosa perché carica i pacchetti linguistici e le DLL native. Condividendo la stessa istanza per tutto il batch, ottieni:

* **Risparmio di memoria** – solo un set di risorse vive in RAM.
* **Aumento di velocità** – il motore rimane “caldo”, evitando inizializzazioni ripetute.
* **Coerenza** – le stesse impostazioni di riconoscimento si applicano a ogni pagina, fondamentale quando vuoi **estrarre testo dalle immagini** che condividono lo stesso layout.

Se devi modificare il riconoscimento (ad es. abilitare il controllo ortografico o cambiare la lingua), fallo *prima* di chiamare `recognize_batch`. Tutte le pagine successive erediteranno automaticamente quelle impostazioni.

## Convertire pagine scannerizzate in testo in modo efficiente

Il cuore del problema—**convertire pagine scannerizzate in testo**—è risolto con `engine.recognize_batch(images)`. Internamente la libreria elabora ogni immagine in un pool di thread in background, così ottieni una scalabilità quasi lineare su macchine multi‑core. Alcune cose da tenere a mente:

* **La qualità dell'immagine è importante** – 300 dpi o più garantiscono i migliori risultati. Se le tue scansioni sono a bassa risoluzione, considera l'up‑sampling con Pillow prima di passarle al motore.
* **Colore vs. scala di grigi** – i motori OCR solitamente lavorano più velocemente su scala di grigi a 8 bit. Puoi aggiungere un passaggio di pre‑elaborazione:
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **Supporto linguistico** – Aspose.OCR supporta oltre 40 lingue. Imposta `engine.language = "eng"` o `"fra"` prima della chiamata batch se non lavori in inglese.

## Best practice per l'elaborazione OCR batch

Anche se il codice sopra è già conciso, un OCR batch di livello produzione spesso richiede qualche precauzione aggiuntiva:

| Problema | Approccio consigliato |
|----------|-----------------------|
| **Batch di grandi dimensioni ( > 500 file )** | Suddividi in blocchi di 100–200 immagini per mantenere un consumo di memoria contenuto. |
| **File corrotti o non supportati** | L'helper `load_images` cattura già le eccezioni e registra un avviso; puoi anche aggiungere un fallback per saltare o spostare i file difettosi. |
| **Monitoraggio dell'avanzamento** | Avvolgi `recognize_batch` in un ciclo che restituisce il controllo dopo ogni immagine, se la libreria espone callback per immagine. |
| **Post‑elaborazione** | Esegui un controllo ortografico o una pulizia con regex sulle stringhe risultanti per migliorare la ricercabilità successiva. |
| **Parallelismo** | Se disponi di un'infrastruttura multi‑node, distribuisci le cartelle tra i worker e unisci i file `.txt` alla fine. |

Questi consigli ti aiutano a scalare **l'elaborazione OCR batch** da poche pagine a migliaia senza far crashare lo script.

## Domande frequenti

**D: Posso usarlo direttamente con i PDF?**  
R: Assolutamente. Converti ogni pagina PDF in immagine prima (ad esempio con `pdf2image`) e passa la lista risultante a `recognize_batch`. Il resto della pipeline rimane invariato.

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}