---
category: general
date: 2026-07-05
description: Crea PDF ricercabili con Python. Scopri come fare OCR su un PNG scansionato,
  convertire un PDF di immagini scansionate e ottenere un PDF ricercabile in pochi
  minuti.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: it
og_description: Crea PDF ricercabili rapidamente. Questa guida mostra come eseguire
  l'OCR su un PNG, convertire un PDF di immagini scannerizzate e produrre un PDF ricercabile
  usando Python.
og_title: Crea PDF ricercabile da immagine scansionata – tutorial OCR in Python
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF with Python. Learn how to OCR a scanned PNG,
    convert scanned image PDF, and get a searchable PDF in minutes.
  headline: Create Searchable PDF from Scanned Image – Full Python OCR Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF
- Automation
title: Crea PDF Ricercabile da Immagine Scansionata – Guida Completa OCR in Python
url: /it/python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea PDF Ricercabile da Immagine Scansionata – Guida Completa OCR in Python

Ti sei mai chiesto come **creare PDF ricercabile** da un'immagine scansionata senza pagare software costosi? Non sei l'unico. In molti uffici, i PDF arrivano come immagini piatte—difficili da cercare, impossibili da copiare‑incollare, e un incubo per gli audit di conformità. La buona notizia? Con poche righe di Python puoi trasformare quel PNG statico in un PDF completamente ricercabile, e il processo è più semplice di quanto pensi.

In questo tutorial percorreremo un esempio completo di **riconoscimento OCR**, coprendo tutto, dall'installazione della libreria giusta alla scrittura del file PDF finale. Alla fine saprai esattamente come **convertire PDF di immagini scansionate**, come **eseguire OCR su PDF** programmaticamente, e avrai uno script riutilizzabile da inserire in qualsiasi progetto.

## Cosa Imparerai

- Installa e configura una libreria Python OCR (useremo `pytesseract` e `pdf2image`).
- Inizializza il motore OCR e imposta la lingua.
- Carica un PNG scansionato (o qualsiasi immagine) ed esegui l'OCR su di esso.
- Converti il risultato OCR in un **PDF ricercabile** (array di byte) e salvalo.
- Suggerimenti per gestire documenti multi‑pagina, lingue diverse e problemi comuni.

Non è necessaria alcuna esperienza pregressa con l'OCR—basta un ambiente Python 3 funzionante e un po' di curiosità.

---

## Crea PDF Ricercabile – Panoramica

Di seguito è riportato un diagramma di flusso ad alto livello dei passaggi che implementeremo.  

![Diagramma del flusso per creare PDF ricercabile](https://example.com/flowchart.png "Diagramma del flusso per creare PDF ricercabile")

*Testo alternativo: Diagramma del flusso per creare PDF ricercabile che mostra l'inizializzazione del motore, il caricamento dell'immagine, il riconoscimento OCR, la conversione PDF e la scrittura del file.*

---

## Passo 1: Inizializza il Motore OCR (how to ocr pdf)

Perché dobbiamo inizializzare qualcosa? Il motore OCR è il cervello che interpreta i pattern di pixel come caratteri. Creando un'istanza del motore e impostando esplicitamente la lingua, indichiamo alla libreria quale alfabeto aspettarsi, migliorando notevolmente l'accuratezza.

```python
import pytesseract
from pdf2image import convert_from_path
from PIL import Image
import io

# Ensure Tesseract is on your PATH or provide the executable location
pytesseract.pytesseract.tesseract_cmd = r"/usr/local/bin/tesseract"  # adjust as needed

# Define the language – ENGLISH is the default, but you can add more (e.g., 'fra' for French)
ocr_language = "eng"
```

**Suggerimento:** Se hai bisogno di eseguire OCR su documenti in più lingue, installa i relativi language pack per Tesseract e passa una lista come `"eng+spa"` a `ocr_language`.

## Passo 2: Carica l'Immagine Scansionata (convert scanned image pdf)

Il prossimo pezzo del puzzle è ottenere i dati dell'immagine in Python. Che tu abbia un PNG singolo o un TIFF multi‑pagina, la classe `PIL.Image` può aprirlo. Se parti da un PDF che contiene già immagini scansionate, `pdf2image` convertirà ogni pagina in un'immagine per noi.

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**Perché è importante:** Caricare l'immagine come oggetto Pillow ci dà accesso ai dati grezzi dei pixel, di cui il motore OCR ha bisogno. Saltare questo passaggio e fornire direttamente i byte grezzi causerebbe errori.

## Passo 3: Esegui il Riconoscimento OCR sull'Immagine (ocr recognition example)

Ora la parte divertente—far leggere il testo al motore. `pytesseract.image_to_pdf_or_hocr` restituisce un flusso di byte PDF che contiene già uno strato di testo invisibile, esattamente ciò di cui abbiamo bisogno per un **PDF ricercabile**.

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**Caso limite:** Se la tua immagine ha basso contrasto, considera di applicare una semplice soglia prima dell'OCR:

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

Questo piccolo passo di pre‑elaborazione può aumentare drasticamente l'accuratezza.

## Passo 4: Scrivi i Byte PDF su un File (convert png searchable pdf)

La libreria OCR ci fornisce un array di byte—pensalo come il contenuto grezzo di un file PDF. Tutto quello che dobbiamo fare ora è scrivere quei byte su disco.

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**Cosa vedrai:** Apri il file risultante in qualsiasi visualizzatore PDF e prova a cercare una parola che sai comparire nell'immagine originale. L'evidenziazione dovrebbe saltare direttamente alla posizione, dimostrando che lo strato di testo invisibile funziona.

## Passo 5: Estendere a Documenti Multi‑Pagina (convert scanned image pdf)

I contratti del mondo reale spesso si estendono su più pagine. Per **convertire PDF di immagini scansionate** che contengono diverse pagine, itera su ogni pagina, esegui l'OCR e concatena i PDF risultanti.

```python
def ocr_image_to_pdf(image_obj, lang="eng"):
    """Helper that returns PDF bytes for a single image."""
    return pytesseract.image_to_pdf_or_hocr(image_obj, lang=lang, extension='pdf')

def merge_pdfs(pdf_bytes_list):
    """Combine multiple PDF byte streams into one."""
    from PyPDF2 import PdfMerger
    merger = PdfMerger()
    for i, pdf_bytes in enumerate(pdf_bytes_list):
        merger.append(io.BytesIO(pdf_bytes))
    output = io.BytesIO()
    merger.write(output)
    merger.close()
    return output.getvalue()

# Example: convert a multi‑page scanned PDF to searchable PDF
pages = convert_from_path("YOUR_DIRECTORY/scanned_contract.pdf", dpi=300)
pdf_parts = [ocr_image_to_pdf(p, lang=ocr_language) for p in pages]
final_pdf = merge_pdfs(pdf_parts)

with open("YOUR_DIRECTORY/contract_searchable.pdf", "wb") as f:
    f.write(final_pdf)

print("✅ Multi‑page searchable PDF created.")
```

**Perché unire?** Ogni chiamata a `image_to_pdf_or_hocr` produce un PDF autonomo. Unirli garantisce che il documento finale mantenga l'ordine originale delle pagine.

## Problemi Comuni & Come Risolverli

| Sintomo | Probabile Causa | Soluzione |
|---------|----------------|-----------|
| Nessun testo ricercabile dopo aver aperto il PDF | Tesseract non trova alcun carattere (output vuoto) | Controlla la qualità dell'immagine, aumenta DPI, o applica pre‑elaborazione (contrasto, binarizzazione). |
| caratteri illeggibili (es., �) | Pacchetto lingua errato o font mancanti | Installa i dati della lingua corretti (`tesseract‑lang‑eng`) e assicurati che `ocr_language` corrisponda. |
| Dimensione file PDF enorme (>10 MB per un'immagine a pagina singola) | Uso di PNG lossless come sorgente; OCR aggiunge un'immagine a piena risoluzione | Ridimensiona l'immagine prima dell'OCR (`image.thumbnail((1240, 1754))` per A4). |
| Script si arresta su Windows con “tesseract.exe non trovato” | Binario Tesseract non presente nel PATH | Aggiungi `pytesseract.pytesseract.tesseract_cmd = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"` (adatta il percorso). |

## Script Completo, Pronto‑da‑Eseguire

Mettendo tutto insieme, ecco un unico file che puoi copiare‑incollare ed eseguire:

```python
#!/usr/bin/env python3
"""
create_searchable_pdf.py
A complete example that converts a scanned PNG (or PDF) into a searchable PDF using Tesseract OCR.
"""

import io
import sys
from pathlib import Path

import pytesseract
from pdf2image import convert_from_path
from PIL import Image
from PyPDF2 import PdfMerger

# -------------------- Configuration --------------------
# Adjust these paths for your environment
TESSERACT_CMD = r"/usr/local/bin/tesseract"   # macOS/Linux
# TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"  # Windows
OCR_LANGUAGE = "eng"                         # Add '+spa' for Spanish, etc.
INPUT_PATH = Path("YOUR_DIRECTORY/scanned_agreement.png")
OUTPUT_PATH = Path("YOUR_DIRECTORY/agreement_searchable.pdf")
# -------------------------------------------------------

# Point pytesseract at the executable
pytesseract.pytesseract.tesseract_cmd = TESSERACT_CMD

def load_image(path: Path) -> Image.Image:
    """Load an image from disk; supports PNG, JPG, TIFF."""
    if not path.is_file():
        sys.exit(f"❌ File not found: {path}")
    return Image.open(path)

def ocr_to_pdf_bytes(img: Image.Image, lang: str = OCR_LANGUAGE) -> bytes:
    """Run OCR on a Pillow image and return PDF bytes with hidden text."""
    return pytesseract.image_to_pdf_or_hocr(img, lang=lang, extension='pdf')

def write_pdf(data: bytes, dest: Path):
    """Write PDF byte stream to a file."""
    dest.parent.mkdir(parents=True, exist_ok=True)
    with open(dest, "wb") as f:
        f.write(data)
    print(f"✅ Searchable PDF saved to {dest}")

def main():
    # Load the scanned image
    image = load_image(INPUT_PATH)

    # Optional: improve contrast for low‑quality scans
    # image = image.convert('L').point(lambda x: 0 if x < 128 else 255, '1')

    # OCR → PDF bytes
    pdf_bytes = ocr_to_pdf_bytes(image)

    # Save the result
    write_pdf(pdf_bytes, OUTPUT_PATH)

if __name__ == "__main__":
    main()
```

Salva questo come `create_searchable_pdf.py`, sostituisci i segnaposto con percorsi reali, e esegui:

```bash
python create_searchable_pdf.py
```

Dovresti vedere un

## Cosa Dovresti Imparare Dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come eseguire OCR su PDF in .NET con Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Converti Immagini in PDF C# – Salva Risultato OCR Multi‑pagina](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Riconoscimento OCR di Documenti PDF in Aspose.OCR per Java](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}