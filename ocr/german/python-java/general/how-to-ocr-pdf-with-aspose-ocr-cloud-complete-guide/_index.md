---
category: general
date: 2026-06-06
description: Wie man PDFs mit Aspose OCR Cloud OCR verarbeitet. Erfahren Sie, wie
  Sie Text aus PDFs extrahieren, PDF‑Seiten in PNG konvertieren und PDF‑Seitenbilder
  in Python speichern.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf page png
- extract plain text pdf
- save pdf page images
language: de
og_description: Wie man PDFs mit Aspose OCR Cloud OCRt. Dieser Leitfaden zeigt, wie
  man reinen Text aus PDFs extrahiert, PDF‑Seiten in PNG konvertiert und PDF‑Seitenbilder
  speichert.
og_title: Wie man PDF mit Aspose OCR Cloud OCRt – Schritt für Schritt
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Aspose OCR Cloud. Learn to extract text from PDF,
    convert PDF page PNG, and save PDF page images in Python.
  headline: How to OCR PDF with Aspose OCR Cloud – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Wie man PDFs mit Aspose OCR Cloud OCRt – vollständige Anleitung
url: /de/python-java/general/how-to-ocr-pdf-with-aspose-ocr-cloud-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man PDF mit Aspose OCR Cloud OCR macht – Vollständige Anleitung

Haben Sie sich jemals gefragt, **wie man PDF**‑Dateien OCR‑t, ohne schwere Desktop‑Tools zu verwenden? Sie sind nicht allein – vielen Entwicklern stößt man an diese Grenze, wenn sie eine schnelle, programmatische Möglichkeit benötigen, Text aus gescannten Dokumenten zu extrahieren. Die gute Nachricht? Mit Aspose OCR Cloud können Sie **Text aus PDF** extrahieren, jede Seite in ein PNG umwandeln und sogar **PDF‑Seitenbilder** für die spätere Verwendung speichern – alles aus einem übersichtlichen Python‑Skript.

In diesem Tutorial gehen wir Schritt für Schritt durch alles, was Sie wissen müssen: von der Installation des SDK, über die Lizenzierung der Engine, bis hin zur Erkennung von mehrseitigen PDFs, dem Extrahieren von Klartext, dem Konvertieren von Seiten zu PNG und dem Persistieren dieser Bilder auf der Festplatte. Am Ende haben Sie einen wiederverwendbaren Code‑Snippet, den Sie in jedes Projekt einbinden können, das **wie man PDF OCR‑t**‑Funktionen benötigt.

## Was Sie benötigen

- **Python 3.8+** (der Code funktioniert auch mit 3.10 und neuer)  
- Ein Aspose OCR Cloud‑Konto – Sie erhalten eine kostenlose Test‑Lizenzdatei (`Aspose.OCR.lic`)  
- Das Paket `asposeocrcloud` (`pip install asposeocrcloud`)  
- Ein gescanntes, mehrseitiges PDF, das Sie verarbeiten möchten  

Das ist alles. Keine zusätzlichen Binärdateien, keine nativen Abhängigkeiten, nur reines Python.

## Wie man PDF OCR‑t – Einrichtung und Lizenz

Bevor Sie irgendeine OCR‑Methode aufrufen können, müssen Sie dem SDK mitteilen, wer Sie sind. Aspose verwendet eine leichte Lizenzdatei, die Sie an einem für Ihr Skript zugänglichen Ort ablegen.

```python
# Step 1: Import the OCR package and apply your license (optional but recommended)
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply the license – replace the path with your actual .lic file location
License().set_license("Aspose.OCR.lic")
```

*Pro‑Tipp:* Wenn Sie den Lizenzschritt überspringen, funktioniert das SDK weiterhin, fügt jedoch ein kleines Wasserzeichen in die Ausgabebilder ein. Für die Produktion nicht ideal.

## Schritt 2: Installieren des Aspose OCR Cloud Python SDK

Öffnen Sie ein Terminal und führen Sie aus:

```bash
pip install asposeocrcloud
```

Das Paket zieht alle erforderlichen Abhängigkeiten (requests, pillow usw.) nach, sodass Sie nichts Weiteres suchen müssen.

## Schritt 3: Erstellen einer OCR‑Engine und Auswahl einer Sprache

Die Engine ist das Herzstück der Operation. Sie können jede von Aspose unterstützte Sprache angeben; Englisch funktioniert in den meisten Fällen.

```python
# Step 3: Create an OCR engine and set the recognition language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)
```

Warum die Sprache setzen? Weil die OCR‑Engine sprachspezifische Wörterbücher nutzt, um die Genauigkeit zu verbessern. Wenn Sie französische PDFs verarbeiten, ersetzen Sie einfach `ENGLISH` durch `FRENCH`.

## Schritt 4: Verweisen Sie auf Ihr mehrseitiges PDF

Geben Sie der Engine den vollständigen Pfad zu der Datei, die Sie verarbeiten möchten. Relative Pfade sind in Ordnung, solange sie vom Arbeitsverzeichnis des Skripts aus aufgelöst werden können.

```python
# Step 4: Specify the path to the multi‑page PDF you want to process
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"
```

Stellen Sie sicher, dass die Datei lesbar ist; andernfalls erhalten Sie einen `FileNotFoundError`.

## Schritt 5: OCR ausführen – Sie erhalten eine Ergebnisliste

Der Aufruf von `recognize_pdf` liefert eine Liste, wobei jedes Element einer Seite des Quell‑PDF entspricht.

```python
# Step 5: Run OCR on the PDF – a list of OcrResult objects is returned (one per page)
results = engine.recognize_pdf(pdf_path)
```

Jedes `OcrResult` enthält zwei praktische Eigenschaften:

* `text` – die Klartext‑Darstellung der Seite (ideal für **extract plain text pdf**)  
* `image` – ein Pillow‑`Image`‑Objekt der gerenderten Seite (perfekt für **convert pdf page png**)

## Schritt 6: Text aus PDF extrahieren und Seiten zu PNG konvertieren

Jetzt durchlaufen wir die Ergebnisse, geben den extrahierten Text aus und speichern eine PNG‑Version jeder Seite.

```python
# Step 6: Iterate through each page, output the extracted text and optionally save the page image
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    # Extract plain text for this page
    print(res.text)                     # <-- this is the "extract plain text pdf" part
    # Convert the page to PNG and save it
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # <-- this does the "convert pdf page png"
```

### Erwartete Konsolenausgabe

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Sie finden außerdem `page_1.png`, `page_2.png`, … im Verzeichnis `YOUR_DIRECTORY`. Das sind die gerasterten Seitenbilder, die Sie in nachgelagerte Bild‑Verarbeitungspipelines einspeisen können.

## Schritt 7: PDF‑Seitenbilder speichern (optionale Nachbearbeitung)

Wenn Sie nur die Bilder und nicht den Text benötigen, können Sie die Zeile `print(res.text)` weglassen. Wenn Sie hingegen den Text in separate `.txt`‑Dateien speichern möchten, fügen Sie einfach einen kleinen Schreibvorgang hinzu:

```python
# Optional: Save each page's text to a .txt file
for i, res in enumerate(results, start=1):
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)
```

Diese kleine Ergänzung zeigt, wie einfach es ist, **PDF‑Seitenbilder** zu **speichern**, während gleichzeitig der extrahierte Inhalt persistiert wird.

## Vollständiges funktionierendes Beispiel

Alles zusammengeführt, hier das komplette Skript, das Sie in `ocr_pdf.py` kopieren‑und‑einfügen können:

```python
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply your license – optional but removes watermarks
License().set_license("Aspose.OCR.lic")

# Initialize the OCR engine and set language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)

# Path to the source PDF
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"

# Run OCR – get a list of results (one per page)
results = engine.recognize_pdf(pdf_path)

# Process each page
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(res.text)  # extract plain text PDF
    # Save the rendered page as PNG
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # convert PDF page PNG
    # Optional: also save the text to a .txt file
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)  # save PDF page images + text
```

Führen Sie es aus mit:

```bash
python ocr_pdf.py
```

Sie sollten die Konsolenausgabe jedes Seiten‑Texts sowie eine Reihe von PNG‑Dateien sehen.


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}