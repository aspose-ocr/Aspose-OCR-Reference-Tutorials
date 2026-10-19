---
category: general
date: 2026-06-06
description: Esegui OCR su un'immagine usando Python e visualizza i punteggi di confidenza.
  Scopri come filtrare le parole a bassa confidenza, impostare soglie e gestire i
  casi limite.
draft: false
keywords:
- run OCR on image
- Python OCR tutorial
- OCR confidence threshold
- low‑confidence word detection
- image text extraction
language: it
og_description: Esegui OCR su un'immagine in Python, controlla i livelli di confidenza
  e filtra le parole a bassa confidenza. Questo tutorial ti guida attraverso un esempio
  completo e funzionante.
og_title: Esegui OCR su immagine con Python – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  headline: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  name: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: Install and Import the OCR Engine
    text: First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box
      for many languages and gives you a confidence score per word.
  - name: Run OCR on the Image
    text: Now we actually **run OCR on image**. The `recognize_image` method from
      the original example is replaced with EasyOCR’s `readtext` call, which returns
      a list of `(bbox, text, confidence)` tuples.
  - name: Summarize Overall Confidence
    text: 'Unlike the earlier snippet that printed a single `confidence` attribute,
      EasyOCR gives a confidence per word. To get an overall sense, we’ll average
      them:'
  - name: List Low‑Confidence Words
    text: Now comes the part that directly answers the “list words whose confidence
      is below the desired threshold” requirement. We’ll set a **OCR confidence threshold**
      of 0.80 (80 %) by default, but you can adjust it.
  - name: Edge Cases & Variations
    text: 1. **Batch Processing** – If you need to **run OCR on image** files in bulk,
      wrap the above logic in a loop that iterates over a directory. 2. **Multiple
      Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine
      will detect both. 3. **Alternative Engines** – Want to try **pyte
  type: HowTo
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`)
      and then feed the PNG/JPEG into the script.
    question: Does this work with PDFs?
  - answer: 'Try image preprocessing: increase contrast, remove background noise,
      or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths`
      parameter you can tweak.'
    question: My confidence numbers are all low—what can I do?
  - answer: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter`
      where each row contains `text`, `confidence`, and bounding‑box coordinates.
    question: Can I export the results to CSV?
  - answer: 'EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed.
      Verify with `torch.cuda.is_available()` before running the script. --- ## Conclusion
      We’ve just **run OCR on image** using Python, inspected the overall confidence,
      and isolated any low‑confidence words that need a {{< /b'
    question: Is there a GPU‑accelerated version?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Esegui OCR su un'immagine con Python – Guida completa passo passo
url: /it/python-java/general/run-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine con Python – Guida Completa Passo‑Passo

Hai mai dovuto **eseguire OCR su file immagine** ma non sapevi come ottenere testo affidabile? Non sei solo: molti sviluppatori si trovano di fronte a parole estratte instabili e a un punteggio di confidenza misterioso.  

In questa guida entreremo subito in una soluzione funzionante: vedrai come eseguire OCR su immagine, leggere la confidenza complessiva e estrarre le parole a bassa confidenza che potrebbero richiedere una revisione manuale. Alla fine avrai uno script riutilizzabile, comprenderai perché ogni riga è importante e saprai come regolare la soglia di confidenza per i tuoi progetti.

## Cosa Copre Questo Tutorial

Percorreremo l’intero flusso di lavoro—dal caricamento di un’immagine alla stampa di un report ordinato delle parole che sono scese sotto l’80 % di confidenza. Lungo il percorso discuteremo di:

* Scegliere un motore OCR solido (useremo **EasyOCR**, una popolare libreria OCR per Python)  
* Interpretare l’attributo `confidence` che ogni risultato OCR restituisce  
* Filtrare le parole con una **soglia di confidenza OCR** personalizzata  
* Estendere lo script per l’elaborazione batch o per motori alternativi come **pytesseract**  

Non è necessaria alcuna esperienza pregressa con OCR, basta una familiarità di base con Python e un ambiente di lavoro funzionante (Python 3.9+ consigliato).  

Pronto a trasformare screenshot sfocati in testo pulito e ricercabile? Iniziamo.

---

## ## Come Eseguire OCR su Immagine con Python

Il cuore del tutorial è uno snippet a tre passaggi che rispecchia il codice che hai già visto. Di seguito analizzeremo ogni riga, spiegheremo il perché e poi ti forniremo uno script completo pronto da copiare‑incollare.

### Passo 1: Installa e Importa il Motore OCR

Per prima cosa, assicurati che la libreria OCR sia disponibile. **EasyOCR** funziona subito per molte lingue e fornisce un punteggio di confidenza per parola.

```bash
pip install easyocr
```

```python
import easyocr  # The engine that will run OCR on image files
import os
```

*Perché EasyOCR?* Include un modello di deep‑learning addestrato su dataset diversificati, quindi ottieni tipicamente valori di confidenza più alti rispetto al vecchio motore Tesseract, soprattutto su immagini di qualità mista.

> **Consiglio professionale:** Se lavori in un ambiente limitato (ad es. un piccolo container Docker), `pytesseract` potrebbe essere più leggero, ma perderai parte della precisione moderna offerta da EasyOCR.

### Passo 2: Esegui OCR sull'Immagine

Ora **eseguiamo OCR su immagine**. Il metodo `recognize_image` dell’esempio originale è sostituito dalla chiamata `readtext` di EasyOCR, che restituisce una lista di tuple `(bbox, text, confidence)`.

```python
# Initialize the OCR reader for English (you can add more languages as needed)
reader = easyocr.Reader(['en'])

# Path to the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "mixed_quality.png")

# Perform OCR – this is the step where we run OCR on image
ocr_results = reader.readtext(image_path, detail=1, paragraph=False)
```

Ogni voce in `ocr_results` appare così:

```python
[
    ((x1, y1, x2, y2, x3, y3, x4, y4), "Detected text", 0.92),
    ...
]
```

Il terzo elemento (`0.92` nell’esempio) è il punteggio di confidenza, compreso tra 0 e 1.

### Passo 3: Riassumi la Confidenza Complessiva

Diversamente dallo snippet precedente che stampava un singolo attributo `confidence`, EasyOCR fornisce una confidenza per parola. Per avere una panoramica generale, ne calcoleremo la media:

```python
# Extract just the confidence numbers
confidences = [item[2] for item in ocr_results]

# Compute the mean confidence (overall confidence)
overall_confidence = sum(confidences) / len(confidences) if confidences else 0

print(f"Overall confidence: {overall_confidence:.2%}")
```

*Perché la media?* Ti dà un rapido controllo di salute—se la confidenza complessiva è sotto, ad esempio, il 70 %, probabilmente dovrai migliorare l’immagine (migliore illuminazione, pre‑elaborazione, ecc.).

### Passo 4: Elenca le Parole a Bassa Confidenza

Ora arriva la parte che risponde direttamente alla richiesta “elencare le parole la cui confidenza è inferiore alla soglia desiderata”. Imposteremo una **soglia di confidenza OCR** di 0.80 (80 %) per impostazione predefinita, ma potrai modificarla.

```python
# Define the confidence threshold – tweak as needed
THRESHOLD = 0.80

print("\nLow‑confidence words:")
low_confidence_found = False
for bbox, text, conf in ocr_results:
    if conf < THRESHOLD:
        low_confidence_found = True
        print(f"  • '{text}' ({conf:.2%})")
if not low_confidence_found:
    print("  All words meet the confidence threshold.")
```

Il ciclo stampa ogni parola che non ha superato la soglia, insieme alla sua percentuale di confidenza. Questo è l’esatto analogo del ciclo originale `for recognized_word in recognition_result.words`, ma ora funziona con il formato di output di EasyOCR.

---

## ## Comprendere i Punteggi di Confidenza OCR

La confidenza non è un numero magico; è la stima del modello su quanto sia sicuro della trascrizione specifica. Ecco alcune cose da tenere a mente:

| Situazione | Confidenza Tipica | Cosa Fare |
|------------|-------------------|-----------|
| Scansione chiara ad alta risoluzione | 0.95 – 1.00 | Nessun lavoro aggiuntivo necessario |
| Leggero sfocamento o illuminazione non uniforme | 0.80 – 0.94 | Considera una leggera pre‑elaborazione (aumento contrasto) |
| Rumore intenso, testo ruotato | < 0.70 | Applica pre‑elaborazione (deskew, denoise) o passa a un motore OCR diverso |

> **Attenzione:** Alcune lingue (ad es. scrittura corsiva) producono naturalmente punteggi più bassi. Regola la soglia di conseguenza.

### Casi Limite e Varianti

1. **Elaborazione Batch** – Se devi **eseguire OCR su file immagine** in blocco, avvolgi la logica sopra in un ciclo che itera su una directory.  
2. **Molteplici Lingue** – Passa una lista come `['en', 'fr']` a `easyocr.Reader` e il motore rileverà entrambe.  
3. **Motori Alternativi** – Vuoi provare **pytesseract**? Sostituisci il blocco del lettore con:

   ```python
   import pytesseract
   from PIL import Image

   img = Image.open(image_path)
   raw_text = pytesseract.image_to_string(img, output_type=pytesseract.Output.DICT)
   # raw_text['text'] contains the full string,
   # raw_text['conf'] holds per‑character confidence.
   ```

   Dovrai poi aggregare le confidenze per carattere in valori per parola—un po' più di lavoro ma fattibile.

4. **Trucchi di Pre‑elaborazione** – L’applicazione di filtri OpenCV (`cv2.threshold`, `cv2.GaussianBlur`) può aumentare la confidenza per scansioni rumorose.  

---

## ## Script Completo, Pronto‑All‑Uso

Di seguito trovi il file Python completo che puoi inserire nel tuo progetto. Salvalo come `ocr_report.py` ed esegui `python ocr_report.py`. Assicurati che il percorso dell’immagine punti a un file reale.

```python
#!/usr/bin/env python3
"""
run_ocr_on_image.py

A self‑contained script that:
  1. Runs OCR on an image using EasyOCR.
  2. Prints the overall confidence.
  3. Lists any words whose confidence falls below a configurable threshold.

Author: Your Name
Date: 2026‑06‑06
"""

import os
import easyocr

# --------------------------- Configuration --------------------------- #
IMAGE_DIR = "YOUR_DIRECTORY"          # <-- Change to your folder
IMAGE_NAME = "mixed_quality.png"      # <-- Change to your file name
THRESHOLD = 0.80                       # Confidence threshold (0‑1)

# --------------------------- Helper Functions ----------------------- #
def load_image_path():
    """Construct the absolute path to the target image."""
    return os.path.join(IMAGE_DIR, IMAGE_NAME)

def run_ocr(image_path):
    """Run OCR on the image and return detailed results."""
    reader = easyocr.Reader(['en'])
    return reader.readtext(image_path, detail=1, paragraph=False)

def compute_overall_confidence(results):
    """Return the mean confidence across all detected words."""
    if not results:
        return 0.0
    confidences = [item[2] for item in results]
    return sum(confidences) / len(confidences)

def report_low_confidence_words(results, threshold):
    """Print words whose confidence is below the given threshold."""
    low_conf = [(text, conf) for _, text, conf in results if conf < threshold]
    if not low_conf:
        print("All words meet the confidence threshold.")
    else:
        for text, conf in low_conf:
            print(f"Low‑confidence word: '{text}' ({conf:.2%})")

# --------------------------- Main Execution ------------------------ #
def main():
    image_path = load_image_path()
    if not os.path.isfile(image_path):
        print(f"❌ Image not found: {image_path}")
        return

    # Step 1: Run OCR on image
    ocr_results = run_ocr(image_path)

    # Step 2: Show overall confidence
    overall = compute_overall_confidence(ocr_results)
    print(f"Overall confidence: {overall:.2%}")

    # Step 3: List low‑confidence words
    print("\n--- Low‑confidence words (threshold: {0:.0%}) ---".format(THRESHOLD))
    report_low_confidence_words(ocr_results, THRESHOLD)

if __name__ == "__main__":
    main()
```

**Output previsto** (i numeri varieranno):

```
Overall confidence: 78.45%

--- Low‑confidence words (threshold: 80%) ---
Low‑confidence word: 'recgnition' (62.13%)
Low‑confidence word: 'imgae' (57.90%)
```

Se ogni parola supera la soglia dell’80 % vedrai il messaggio amichevole “All words meet the confidence threshold.” al posto.

---

## ## Domande Frequenti (FAQ)

**D: Funziona con i PDF?**  
R: Non direttamente. Converti ogni pagina PDF in immagine prima (ad es. con `pdf2image`) e poi passa il PNG/JPEG allo script.

**D: I miei numeri di confidenza sono tutti bassi—cosa posso fare?**  
R: Prova la pre‑elaborazione dell’immagine: aumenta il contrasto, rimuovi il rumore di fondo o ruota l’immagine su una linea orizzontale. EasyOCR accetta anche un parametro `contrast_ths` che puoi regolare.

**D: Posso esportare i risultati in CSV?**  
R: Assolutamente. Dopo il ciclo delle parole a bassa confidenza, scrivi `ocr_results` in un `csv.DictWriter` dove ogni riga contiene `text`, `confidence` e le coordinate del bounding‑box.

**D: Esiste una versione accelerata da GPU?**  
R: EasyOCR utilizza automaticamente CUDA se è presente una GPU compatibile e PyTorch è installato. Verifica con `torch.cuda.is_available()` prima di eseguire lo script.

---

## Conclusione

Abbiamo appena **eseguito OCR su immagine** usando Python, ispezionato la confidenza complessiva e isolato le parole a bassa confidenza che necessitano di revisione manuale.

## Cosa Dovresti Imparare Dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}