---
category: general
date: 2026-04-29
description: Estrai testo da PDF usando Aspose OCR in Python. Impara l'elaborazione
  OCR di PDF in batch, converti il testo dei PDF scansionati e gestisci le pagine
  a bassa confidenza.
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: it
og_description: Estrai il testo da PDF con Aspose OCR in Python. Questa guida mostra
  l'elaborazione OCR batch di PDF, la conversione del testo di PDF scansionati e la
  gestione dei risultati a bassa confidenza.
og_title: Estrai testo da PDF – OCR PDF con Python
tags:
- OCR
- Python
- PDF processing
title: Estrai testo da PDF – OCR PDF con Python
url: /it/python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrarre testo da PDF – OCR PDF con Python

Hai mai dovuto **estrarre testo da un PDF** ma il file è solo un’immagine scannerizzata? Non sei solo: molti sviluppatori si trovano di fronte a questo ostacolo quando cercano di trasformare i PDF in dati ricercabili. La buona notizia? Con Aspose OCR per Python puoi convertire il testo di PDF scannerizzati in poche righe di codice, e persino eseguire **elaborazione batch OCR PDF** quando hai dozzine di file da gestire.

In questo tutorial percorreremo l’intero flusso di lavoro: configurare la libreria, eseguire l’OCR su un singolo PDF, scalare a un batch e gestire le pagine a bassa confidenza così saprai quando è necessaria una revisione manuale. Alla fine avrai uno script pronto all’uso che estrae testo da qualsiasi PDF scannerizzato e comprenderai il perché di ogni passaggio.

## Cosa ti servirà

Prima di iniziare, assicurati di avere:

- Python 3.8 o superiore (il codice usa le f‑string, quindi 3.6+ funziona, ma 3.8+ è consigliato)
- Una licenza Aspose OCR per Python o una chiave di prova gratuita (puoi ottenerla dal sito Aspose)
- Una cartella con uno o più PDF scannerizzati da elaborare
- Una quantità modesta di spazio su disco per i report *.txt* generati

Tutto qui—nessuna dipendenza esterna pesante, nessun esercizio con OpenCV. Il motore OCR di Aspose fa il lavoro pesante per te.

## Configurare l’ambiente

Per prima cosa, installa il pacchetto Aspose OCR da PyPI:

```bash
pip install aspose-ocr
```

Se disponi di un file di licenza (`Aspose.OCR.lic`), posizionalo nella radice del progetto e attivalo così:

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **Pro tip:** Tieni il file di licenza fuori dal controllo di versione; aggiungilo a `.gitignore` per evitare esposizioni accidentali.

## Eseguire l’OCR su un singolo PDF

Ora estraiamo il testo da un singolo PDF scannerizzato. I passaggi fondamentali sono:

1. Creare un’istanza di `OcrEngine`.
2. Puntarla al file PDF.
3. Recuperare un `OcrResult` per ogni pagina.
4. Scrivere l’output di testo semplice su disco.
5. Rilasciare il motore per liberare le risorse native.

Ecco lo script completo, pronto per l’esecuzione:

```python
# Step 1: Import the OCR engine and create an instance
from aspose.ocr import OcrEngine

# Optional: activate license (see previous section)
# from aspose.ocr import License
# License().set_license("Aspose.OCR.lic")

ocr_engine = OcrEngine()

# Step 2: Specify the PDF file to be processed
pdf_file_path = r"YOUR_DIRECTORY/input.pdf"

# Step 3: Extract OCR results – one OcrResult object per page
ocr_pages = ocr_engine.extract_from_pdf(pdf_file_path)

# Step 4: Iterate through the results, show confidence, flag low‑confidence pages, and save the plain text
for ocr_page in ocr_pages:
    print(f"Page {ocr_page.page_number}: confidence {ocr_page.confidence:.2%}")

    # If confidence is below 80 %, flag it for manual review
    if ocr_page.confidence < 0.80:
        print("  Low confidence – consider manual review")

    # Build the output filename
    output_txt = f"YOUR_DIRECTORY/Report_page{ocr_page.page_number}.txt"
    with open(output_txt, "w", encoding="utf-8") as f:
        f.write(ocr_page.text)

# Step 5: Release resources used by the engine
ocr_engine.dispose()
```

**Cosa vedrai:** Per ogni pagina lo script stampa qualcosa del tipo `Page 1: confidence 97.45%`. Se una pagina scende sotto la soglia dell’80 %, appare un avviso, indicandoti che l’OCR potrebbe aver perso dei caratteri.

### Perché funziona

- **`OcrEngine`** è il gateway verso la libreria nativa Aspose OCR; gestisce tutto, dalla pre‑elaborazione delle immagini al riconoscimento dei caratteri.
- **`extract_from_pdf`** rasterizza automaticamente ogni pagina del PDF, quindi non è necessario convertire il PDF in immagini manualmente.
- **I punteggi di confidenza** ti permettono di automatizzare i controlli di qualità—critico quando elabori documenti legali o medici dove la precisione è fondamentale.

## Elaborazione batch OCR PDF con Python

La maggior parte dei progetti reali coinvolge più di un file. Estendiamo lo script singolo a una pipeline di **elaborazione batch OCR PDF** che attraversa una directory, elabora ogni PDF e salva i risultati in una sottocartella corrispondente.

```python
import os
from pathlib import Path
from aspose.ocr import OcrEngine

def ocr_pdf_file(pdf_path: Path, output_dir: Path, engine: OcrEngine, confidence_threshold: float = 0.80):
    """Extract text from a single PDF and write per‑page .txt files."""
    ocr_pages = engine.extract_from_pdf(str(pdf_path))
    for page in ocr_pages:
        print(f"{pdf_path.name} – Page {page.page_number}: {page.confidence:.2%}")
        if page.confidence < confidence_threshold:
            print("  ⚠️ Low confidence – manual review may be needed")

        out_file = output_dir / f"{pdf_path.stem}_page{page.page_number}.txt"
        out_file.write_text(page.text, encoding="utf-8")

def batch_ocr_pdf(input_folder: str, output_folder: str):
    """Iterate over all PDFs in input_folder and run OCR."""
    engine = OcrEngine()
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(parents=True, exist_ok=True)

    pdf_files = list(input_path.glob("*.pdf"))
    if not pdf_files:
        print("🚫 No PDF files found in the specified folder.")
        return

    for pdf_file in pdf_files:
        # Create a sub‑folder for each PDF to keep pages organized
        pdf_out_dir = output_path / pdf_file.stem
        pdf_out_dir.mkdir(exist_ok=True)
        ocr_pdf_file(pdf_file, pdf_out_dir, engine)

    # Clean up native resources
    engine.dispose()
    print("✅ Batch OCR completed.")

# Example usage:
if __name__ == "__main__":
    batch_ocr_pdf("YOUR_DIRECTORY/input_pdfs", "YOUR_DIRECTORY/ocr_output")
```

#### Come aiuta

- **Scalabilità:** La funzione attraversa la cartella una sola volta, creando una sottocartella di output dedicata per ogni PDF. Questo mantiene tutto ordinato quando hai decine di documenti.
- **Riutilizzabilità:** `ocr_pdf_file` può essere chiamata da altri script (ad es., un servizio web) perché è una funzione pura.
- **Gestione degli errori:** Lo script stampa un messaggio amichevole se la cartella di input è vuota, evitando un fallimento silenzioso.

## Conversione del testo PDF scannerizzato – Gestione dei casi limite

Sebbene il codice sopra funzioni per la maggior parte dei PDF, potresti incontrare alcune particolarità:

| Situazione | Perché accade | Come mitigare |
|-----------|----------------|-----------------|
| **PDF criptati** | Il PDF è protetto da password. | Passa la password a `extract_from_pdf(pdf_path, password="yourPwd")`. |
| **Documenti multilingua** | Aspose OCR usa l’inglese per impostazione predefinita. | Imposta `ocr_engine.language = "spa"` per lo spagnolo, o fornisci una lista per lingue miste. |
| **PDF molto grandi (>500 pagine)** | L’uso di memoria aumenta perché ogni pagina viene caricata in RAM. | Elabora il PDF a blocchi usando `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` e itera. |
| **Scansioni di scarsa qualità** | DPI basso o molto rumore riducono la confidenza. | Pre‑elabora il PDF con `engine.image_preprocessing = True` o aumenta il DPI tramite `engine.dpi = 300`. |

> **Attenzione:** Attivare la pre‑elaborazione delle immagini può aumentare notevolmente il tempo CPU. Se esegui un batch notturno, programma abbastanza tempo o avvia un worker separato.

## Verificare l’output

Al termine dello script, troverai una struttura di cartelle simile a:

```
ocr_output/
├─ invoice_2023/
│  ├─ invoice_2023_page1.txt
│  ├─ invoice_2023_page2.txt
│  └─ …
└─ contract_A/
   ├─ contract_A_page1.txt
   └─ …
```

Apri qualsiasi file `.txt`; dovresti vedere testo pulito, codificato in UTF‑8, che rispecchia il contenuto originale scannerizzato. Se noti caratteri illeggibili, ricontrolla le impostazioni di lingua del PDF e assicurati che i pacchetti di font corretti siano installati sulla macchina.

## Pulizia delle risorse

Aspose OCR si basa su DLL native, quindi è fondamentale chiamare `engine.dispose()` una volta terminato. Dimenticare questo passaggio può provocare perdite di memoria, soprattutto in job batch a lunga esecuzione.

```python
# Always the last line of your script
engine.dispose()
```

## Esempio completo end‑to‑end

Mettendo tutto insieme, ecco un singolo

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}