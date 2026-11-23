---
category: general
date: 2026-06-19
description: Crea PDF ricercabile da un'immagine usando OCR con Python. Impara a convertire
  l'OCR in PDF, estrarre il testo dall'immagine ed eseguire rapidamente l'OCR sull'immagine.
draft: false
keywords:
- create searchable pdf
- convert ocr to pdf
- extract text from image
- convert image to pdf
- perform ocr on image
language: it
og_description: Crea PDF ricercabile da un'immagine con Python OCR. Questa guida mostra
  come convertire l'OCR in PDF, estrarre il testo dall'immagine ed eseguire l'OCR
  sull'immagine.
og_title: Crea PDF ricercabile in Python – Guida completa alla programmazione
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  headline: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  name: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  steps:
  - name: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
    text: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
  - name: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
    text: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
  - name: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
    text: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
  type: HowTo
tags:
- OCR
- Python
- PDF
- ImageProcessing
title: Crea PDF Ricercabile in Python – Guida Completa Passo‑Passo
url: /it/python-java/general/create-searchable-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea PDF Ricercabile in Python – Guida Completa Passo‑Passo

Hai mai avuto bisogno di **creare PDF ricercabile** da una ricevuta scansionata ma non sapevi da dove cominciare? Non sei solo—molti sviluppatori incontrano lo stesso ostacolo quando provano per la prima volta a trasformare un'immagine di testo in un PDF effettivamente ricercabile.  

In questo tutorial ti guideremo attraverso una soluzione pratica che ti permette di **eseguire OCR su immagine**, trasformare quel risultato OCR in un **PDF ricercabile**, e persino estrarre il testo grezzo se ti serve per ulteriori elaborazioni. Nessun superfluo, solo un esempio funzionante che puoi copiare‑incollare nel tuo progetto oggi.

## Cosa Imparerai

- Come configurare un motore OCR leggero in Python  
- I passaggi esatti per **convertire OCR in PDF** e salvarlo come documento ricercabile  
- Modi per **estrarre testo da immagine** per analisi successive  
- Consigli per gestire problemi comuni come l'orientamento dell'immagine e file di grandi dimensioni  
- Uno script completo e eseguibile che puoi adattare al tuo caso d'uso

### Prerequisiti

- Python 3.8+ installato sulla tua macchina  
- Familiarità di base con pip e ambienti virtuali (opzionale ma consigliato)  
- Un file immagine (PNG, JPEG, ecc.) che contiene testo chiaro e leggibile da macchina  

Se li hai, tuffiamoci.

## Passo 1: Installa la Libreria Necessaria

Il frammento di codice che hai visto in precedenza utilizza un pacchetto fittizio `ocr`, ma le stesse idee si applicano a librerie reali come **EasyOCR**, **pytesseract** o **pdfminer.six**. Per questa guida useremo **EasyOCR** perché è puro Python, supporta molte lingue e restituisce un comodo metodo di conversione PDF tramite un helper ausiliario.

```bash
pip install easyocr pillow
```

> **Consiglio:** Installa all'interno di un ambiente virtuale (`python -m venv venv && source venv/bin/activate`) per mantenere ordinate le dipendenze.

## Passo 2: Inizializza il Motore OCR – Esegui OCR su Immagine

Ora che la libreria è pronta, creiamo un motore OCR e gli diciamo di lavorare con testo inglese. Questo è il primo punto in cui **eseguiamo OCR su immagine**.

```python
import easyocr
from PIL import Image
import io

# Create an EasyOCR reader for English
reader = easyocr.Reader(['en'])  # ← performs OCR on image
```

Perché abbiamo bisogno di un oggetto reader dedicato? EasyOCR pre‑carica i modelli linguistici, quindi riutilizzare lo stesso `reader` per più immagini è molto più efficiente rispetto a reinizializzarlo ogni volta.

## Passo 3: Carica l'Immagine – Estrai Testo da Immagine

Portiamo l'immagine in memoria. Questo passaggio è dove **estrarremo testo da immagine** più tardi, ma per ora la carichiamo semplicemente.

```python
# Replace with the path to your receipt or scanned document
image_path = "YOUR_DIRECTORY/receipt.png"

# Open the image with Pillow (helps with format handling)
pil_image = Image.open(image_path).convert("RGB")
```

Se la tua immagine è capovolta o inclinata, considera di usare i metodi `rotate` o `transpose` di Pillow prima di passarla al motore OCR. Un rapido controllo visivo può salvarti ore di debug in seguito.

## Passo 4: Esegui il Motore OCR e Cattura i Risultati

Ecco il cuore del processo—inviare l'immagine al motore OCR e ottenere dati strutturati.

```python
# EasyOCR returns a list of (bbox, text, confidence) tuples
ocr_result = reader.readtext(image_path, detail=1, paragraph=True)
```

Il flag `detail=1` ci fornisce le bounding box, che ci serviranno quando più tardi **convertiremo OCR in PDF**. Se ti interessano solo le stringhe grezze, imposta `detail=0`.

## Passo 5: Converti il Risultato OCR in un PDF Ricercabile – Converti OCR in PDF

EasyOCR non fornisce un writer PDF diretto, ma possiamo assemblare il PDF noi stessi usando Pillow e la libreria `reportlab`. Per mantenere il tutorial leggero, useremo `fpdf2`, che ci permette di incorporare l'immagine originale e sovrapporre testo invisibile.

```bash
pip install fpdf2
```

```python
from fpdf import FPDF

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        # Set invisible text style
        self.set_text_color(255, 255, 255)   # white on white background
        self.set_font("Helvetica", size=12)

        for bbox, text, conf in ocr_data:
            # bbox = [(x1,y1), (x2,y2), (x3,y3), (x4,y4)]
            x_min = min(point[0] for point in bbox)
            y_min = min(point[1] for point in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

# Create PDF instance with the original image as background
pdf = SearchablePDF(image_path)

# Add invisible OCR text on top of the image
pdf.add_ocr_text(ocr_result)

# Save the searchable PDF
output_path = "YOUR_DIRECTORY/receipt_searchable.pdf"
pdf.output(output_path)
```

Cosa è successo? Abbiamo posizionato l'immagine scansionata come livello visibile, poi scritto le parole riconosciute sopra usando testo bianco che si fonde con lo sfondo bianco. Gli strumenti di ricerca leggono comunque il livello nascosto, così il PDF diventa **ricercabile** senza alterare l'aspetto visivo.

## Passo 6: Salva i Byte del PDF – Converti Immagine in PDF

Se preferisci gestire il PDF in memoria (ad esempio, inviandolo tramite un'API), puoi catturare i byte invece di scrivere direttamente su disco.

```python
pdf_bytes = pdf.output(dest='S').encode('latin1')  # returns a byte string

# Example: write bytes to a file (same as Step 5 but shows the conversion)
with open(output_path, "wb") as f:
    f.write(pdf_bytes)
```

Quella riga dimostra il classico workflow **convertire immagine in PDF**: parti da un'immagine, esegui OCR, sovrapponi testo e infine emetti uno stream PDF.

## Passo 7: Verifica il Risultato – Controlli Rapidi

Dopo aver eseguito lo script, apri `receipt_searchable.pdf` in qualsiasi visualizzatore PDF e prova la casella di ricerca (Ctrl + F). Digita una parola che sai comparire nella ricevuta—se il visualizzatore salta al punto giusto, hai **creato con successo un PDF ricercabile**!  

Se la ricerca fallisce, ricontrolla:

1. I punteggi di confidenza OCR (`conf`). Una bassa confidenza può indicare che l'immagine è sfocata.  
2. Le coordinate delle bounding box—a volte EasyOCR le riporta in un'orientazione diversa.  
3. Che il visualizzatore PDF non sia impostato in modalità “solo immagine” (raro, ma alcuni visualizzatori hanno questa opzione).

## Script Completo Funzionante

Unendo tutto, ecco il file Python completo e pronto all'uso:

```python
# searchable_pdf.py
import easyocr
from PIL import Image
from fpdf import FPDF

# ---------- Configuration ----------
IMAGE_PATH = "YOUR_DIRECTORY/receipt.png"
OUTPUT_PDF = "YOUR_DIRECTORY/receipt_searchable.pdf"
# ----------------------------------

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        # Fit the image to the page size
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        self.set_text_color(255, 255, 255)   # invisible white text
        self.set_font("Helvetica", size=12)
        for bbox, text, conf in ocr_data:
            x_min = min(p[0] for p in bbox)
            y_min = min(p[1] for p in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

def main():
    # 1️⃣ Initialize OCR engine – perform OCR on image
    reader = easyocr.Reader(['en'])

    # 2️⃣ Load the image – extract text from image later
    pil_image = Image.open(IMAGE_PATH).convert("RGB")

    # 3️⃣ Run OCR and capture results
    ocr_result = reader.readtext(IMAGE_PATH, detail=1, paragraph=True)

    # 4️⃣ Convert OCR result to searchable PDF – convert OCR to PDF
    pdf = SearchablePDF(IMAGE_PATH)
    pdf.add_ocr_text(ocr_result)

    # 5️⃣ Save the PDF – convert image to PDF (or keep bytes in memory)
    pdf.output(OUTPUT_PDF)
    print(f"✅ Searchable PDF saved to {OUTPUT_PDF}")

if __name__ == "__main__":
    main()
```

Salva questo file come `searchable_pdf.py`, sostituisci i placeholder `YOUR_DIRECTORY` con percorsi reali, e avvia:

```bash
python searchable_pdf.py
```

Dovresti vedere un messaggio di conferma e un nuovo PDF ricercabile nella tua cartella.

## Domande Frequenti & Casi Limite

**Cosa succede se l'immagine è a colori?**  
EasyOCR funziona sia con immagini in scala di grigi che a colori, ma convertire in scala di grigi (`pil_image.convert("L")`) a volte migliora la precisione su scansioni rumorose.

**Posso gestire PDF multi‑pagina?**  
Sì—itera su ogni immagine di pagina, esegui i passaggi OCR e aggiungi ogni pagina allo stesso oggetto `FPDF`. Ricorda di resettare il cursore (`self.add_page()`) per ogni nuova immagine.

**C'è un modo per mantenere il livello di testo originale invece del testo bianco invisibile?**  
Se ti serve un vero PDF “testo‑sotto‑immagine” (ad esempio per l'accessibilità), considera l'uso di `pdfminer` o `pikepdf` per incorporare un livello di testo nascosto con i tag PDF appropriati. È più avanzato, ma il principio resta lo stesso: immagine di sfondo + testo sovrapposto.

**Cosa fare se la confidenza OCR è bassa?**  
Puoi filtrare le parole a bassa confidenza:

```python
filtered = [item for item in ocr_result if item[2] > 0.8]  # keep >80% confidence
pdf.add_ocr_text(filtered)
```

## Conclusione – Cosa Abbiamo Raggiunto

Abbiamo iniziato con una semplice immagine di una ricevuta, **eseguito OCR su immagine**, estratto le stringhe riconosciute e infine **creato un PDF ricercabile** che si comporta come qualsiasi documento scansionato professionalmente. Il processo ha coperto tutte le parole chiave secondarie—**convertire OCR in PDF**, **estrarre testo da immagine**, **convertire immagine in PDF**, e **eseguire OCR su immagine**—così ora disponi di una cassetta degli attrezzi riutilizzabile per qualsiasi progetto simile.

### Prossimi Passi

- Sperimenta con altre lingue passando i loro codici ISO a `easyocr.Reader(['en', 'es'])`.  
- Sostituisci EasyOCR con Tesseract se ti serve una soluzione completamente offline; il resto della pipeline rimane invariato.  
- Aggiungi la visualizzazione della confidenza OCR (disegna le bounding box sull'immagine) per debug di scansioni problematiche.  

Hai un'idea da condividere? Lascia un commento, fai fork

## Cosa Dovresti Imparare Dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrai Testo da Immagine con Aspose OCR – Guida Passo‑Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Converti Immagini in PDF C# – Salva Risultato OCR Multipagina](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Come OCR Immagine – Esegui OCR su Immagine nel Riconoscimento Immagini OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}