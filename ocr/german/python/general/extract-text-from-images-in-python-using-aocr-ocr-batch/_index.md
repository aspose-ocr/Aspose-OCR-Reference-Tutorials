---
category: general
date: 2026-06-25
description: Extrahiere Text aus Bildern mit der Python‑aocr‑Bibliothek – lerne Batch‑OCR,
  setze den Erkennungsmodus auf gedruckt und füge einen KI‑Postprozessor hinzu.
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: de
og_description: Extrahiere Text aus Bildern mit der Python aocr‑Bibliothek. Dieses
  Tutorial zeigt Batch‑OCR, den Erkennungsmodus für gedruckten Text und einen optionalen
  KI‑Nachbearbeiter.
og_title: Text aus Bildern in Python extrahieren – Vollständige aocr‑Batch‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: Text aus Bildern in Python mit aocr OCR Batch extrahieren
url: /de/python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bildern in Python mit aocr OCR Batch extrahieren

Haben Sie jemals **Text aus Bildern extrahieren** müssen, fühlten sich jedoch von Dutzenden kleiner Schritte überwältigt? Sie sind nicht allein. Egal, ob Sie gescannte Formulare digitalisieren, Daten von Quittungen auslesen oder ein durchsuchbares Archiv erstellen, zuverlässige OCR‑Ergebnisse in großem Maßstab zu erhalten, kann sich anfühlen, als würde man einen steilen Hügel erklimmen.

Die gute Nachricht? Mit der **aocr library** können Sie in nur wenigen Zeilen einen kompletten **Python OCR batch** aufsetzen. In diesem Leitfaden gehen wir Schritt für Schritt durch das Erstellen eines OCR‑Batches, das Laden aller unterstützten Bilder aus einem Ordner, die Auswahl des richtigen **recognition mode printed** und sogar das Anhängen eines **AI postprocessor** für zusätzlichen Genauigkeits‑Boost. Am Ende haben Sie ein sofort ausführbares Skript, das Text aus Bildern extrahiert und Ihnen zeigt, wie viel pro Datei erfasst wurde.

## Was Sie lernen werden

- Wie man das `aocr`‑Paket installiert und importiert.
- Einrichten eines `OcrBatch`, um tausende Dateien automatisch zu verarbeiten.
- Auswahl des optimalen Erkennungsmodus für gedruckte Dokumente.
- (Optional) Anbinden eines KI‑Post‑Processors, um verrauschte Ergebnisse zu bereinigen.
- Anzeige jedes Dateipfads zusammen mit der Länge des extrahierten Textes.
- Tipps zum Umgang mit Randfällen wie nicht unterstützten Formaten oder leeren Seiten.

### Voraussetzungen

- Python 3.8 oder neuer auf Ihrem Rechner installiert.  
- Grundlegende Kenntnisse in Python‑Skripting (Schleifen, Importe usw.).  
- Zugriff auf einen Ordner mit gescannten Bildern (PNG, JPG, TIFF usw.).  

Wenn Sie das haben, legen wir los – ohne externe Dienste.

## Schritt 1: Installieren der aocr‑Bibliothek

First things first. The `aocr` package isn’t part of the standard library, so you’ll need to pull it from PyPI.

```bash
pip install aocr
```

> **Pro‑Tipp:** Verwenden Sie eine virtuelle Umgebung (`python -m venv .venv`), um Abhängigkeiten zu isolieren.  

Nach der Installation können Sie die Kernklassen importieren.

```python
# core imports
import aocr
```

## Schritt 2: Erstellen einer OCR‑Batch‑Instanz

An `OcrBatch` is the workhorse that will crawl your directory and keep track of every image file. Think of it as a conveyor belt that feeds pictures into the OCR engine.

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

An diesem Punkt ist das Batch leer, aber wir füllen es im nächsten Schritt.

## Schritt 3: Alle unterstützten Bilder aus einem Ordner hinzufügen (rekursiv)

You probably have a nested folder structure—maybe one sub‑folder per client or per month. The `add_folder` method walks the tree for you, pulling in every image it knows how to read.

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

Replace `"YOUR_DIRECTORY/scanned_forms/"` with the real path on your system. After this call `ocr_batch.file_paths` holds a list of absolute file names, and the batch knows exactly how many items it will process.

## Schritt 4: Auswahl des Erkennungsmodus für gedruckten Text

The `aocr` engine supports several modes (handwritten, printed, mixed). Since we’re dealing with clean, printed forms, set the mode accordingly. This tiny flag can dramatically improve accuracy because the engine skips the heavy‑handed heuristics needed for cursive scripts.

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **Why it matters:** Printed text has consistent baselines and character shapes, letting the OCR model apply tighter character dictionaries. If you leave the mode on “auto” you might get extra noise on low‑resolution scans.

## Schritt 5: (Optional) Einen KI‑Post‑Processor anhängen

If your scans suffer from blur, low contrast, or unusual fonts, an AI post‑processor can clean up the raw OCR output before you hand it off to downstream systems. The `set_ai_postprocessor` method expects an object that implements a `process(text: str) -> str` interface.

Below is a minimal example using a fictional `SimpleCleaner` class. In practice you could plug in a HuggingFace transformer, a custom language model, or even a rule‑based spell‑checker.

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

Wenn Sie diesen Schritt überspringen, gibt das Batch einfach die rohen OCR‑Zeichenketten zurück.

## Schritt 6: OCR auf dem gesamten Batch ausführen und Ergebnisse sammeln

Now the heavy lifting begins. The `run` method loops over every file, runs the OCR engine, pipes the output through the optional AI post‑processor, and returns a list of strings—one per image.

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

Because the method returns a plain Python list, you can treat it like any other collection—store it, write it to a CSV, or feed it into a database.

## Schritt 7: Jeden Dateipfad mit der Länge des extrahierten Textes anzeigen

A quick sanity check is to print out how many characters were extracted from each file. If a page is blank or the OCR failed, you’ll see a length of `0`.

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

Typische Ausgabe sieht so aus:

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

Ein `0`‑Flag zeigt sofort, welche Dateien einen zweiten Blick benötigen (vielleicht sind sie beschädigt oder gar keine Bilder).

## Umgang mit häufigen Randfällen

### 1. Nicht unterstützte Dateitypen

`aocr` silently skips files it can’t decode. If you suspect you have PDFs or BMPs mixed in, filter them beforehand:

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. Große Batches und Speicherverbrauch

Running thousands of high‑resolution scans can balloon memory usage. Mitigate this by processing in chunks:

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. Leere oder kontrastarme Seiten

If a page yields fewer than 10 characters, you might want to flag it for manual review:

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## Vollständiges funktionierendes Beispiel

Putting it all together, here’s a script you can copy‑paste and run immediately. Save it as `batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**Erwartete Ausgabe** (gekürzt für Übersicht):

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

Führen Sie es aus mit:

```bash
python batch_ocr.py
```

If everything is set up correctly, you’ll see a line for every image, each reporting the character count of the extracted text.

## Häufig gestellte Fragen

**Q: Does this work on PDFs?**  
A: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to PNG/TIFF first (e.g., using `pdf2image`).

**Q: Can I change the recognition mode to handwritten?**  
A: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`. Expect a slower run time but better results on cursive notes.

**Q: What if I need multilingual support?**  
A: The library ships with language packs. Install the desired language module (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language = "fr"` before running.

## Nächste Schritte und verwandte Themen

- **Parallel processing:** Wrap the batch execution in a `concurrent.futures.ThreadPoolExecutor` to utilize multiple CPU cores.  
- **Storing results:** Write `ocr_results` to a CSV or SQLite database for downstream analytics.  
- **Integrating with cloud AI:** Swap the `SimpleCleaner` with a transformer model from HuggingFace for state‑of‑the‑art spelling correction.  
- **Fine‑tuning aocr:** If you have a custom font set, explore `aocr.Trainer` to improve the printed‑mode accuracy.

---

Das war's – Sie haben jetzt ein solides

## Was sollten Sie als Nächstes lernen?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Text aus Bild mit Aspose OCR extrahieren – Schritt‑für‑Schritt‑Anleitung](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Text aus Bildern mit OCR‑Operation in Ordnern extrahieren](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Wie man OCR‑Bilder stapelweise mit einer Liste in Aspose.OCR für .NET verarbeitet](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}