---
category: general
date: 2026-03-28
description: Erfahren Sie, wie Sie PDF mit Python schnell OCRen. Dieser Leitfaden
  zeigt Ihnen, wie Sie Text aus PDFs extrahieren, Text aus PDFs erkennen und gescannte
  PDFs mit Aspose OCR in Text umwandeln.
draft: false
keywords:
- how to ocr pdf
- ocr pdf with python
- extract text from pdf
- recognize text from pdf
- convert scanned pdf to text
language: de
og_description: Lerne, wie man PDFs mit Python OCR verarbeitet. Extrahiere Text aus
  PDFs, erkenne Text aus PDFs und konvertiere gescannte PDFs in Text in wenigen Minuten.
og_title: Wie man PDFs in Python OCRt – Komplettanleitung
tags:
- PDF
- OCR
- Python
- Aspose
title: Wie man PDFs in Python OCRt – Schritt‑für‑Schritt‑Anleitung
url: /de/python-java/general/how-to-ocr-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man PDFs in Python OCR‑t – Schritt‑für‑Schritt‑Anleitung

Haben Sie sich schon einmal gefragt, **wie man PDFs OCR‑t**, wenn die Datei nur ein Bild einer Seite ist? Sie sind nicht allein. In diesem Tutorial gehen wir die genauen Schritte durch, um PDF‑Dateien zu OCR‑en, Text aus PDFs zu extrahieren und ein gescanntes PDF in durchsuchbaren Text zu verwandeln – alles mit reinem Python‑Code.

Wir behandeln alles von der Installation der Aspose OCR‑Bibliothek bis zum Auslesen des erkannten Textes jeder Seite. Am Ende können Sie **PDFs mit Python OCR‑en**, **Text aus PDFs extrahieren** und **gescannte PDFs in Text umwandeln**, ohne durch verstreute Dokumentationen zu wühlen. Kein Schnickschnack, nur ein praktisches, lauffähiges Beispiel, das Sie kopieren‑und‑einfügen können.

## Was Sie benötigen

Bevor wir loslegen, stellen Sie sicher, dass Sie Folgendes haben:

* Python 3.8+ (die neueste stabile Version funktioniert am besten)  
* Eine Aspose OCR‑für‑Python‑Lizenz oder einen kostenlosen Testschlüssel – Sie können ihn von der Aspose‑Website holen.  
* Ein gescanntes PDF, das Sie verarbeiten möchten (wir nennen es `input.pdf`).  

Wenn Sie das bereits haben, super – los geht’s. Wenn nicht, die Installation des Pakets ist ein Kinderspiel und wir zeigen Ihnen, wie es geht.

## Wie man PDFs OCR‑t – Umgebung einrichten

Das Erste, was Sie tun müssen, ist das Aspose OCR‑Modul auf Ihren Rechner zu holen. Das Paket heißt `aspose-ocr` und Sie können es über pip installieren:

```bash
pip install aspose-ocr
```

> **Pro‑Tipp:** Verwenden Sie eine virtuelle Umgebung (`python -m venv venv`), damit Ihre Abhängigkeiten ordentlich bleiben.

Sobald das Paket installiert ist, können Sie es importieren und die OCR‑Engine starten. Das ist die Grundlage für jeden **ocr pdf with python**‑Workflow, den Sie später bauen werden.

## OCR PDF mit Python – Aspose OCR importieren

Jetzt, wo die Bibliothek verfügbar ist, bringen wir sie in unser Skript. Wir stellen die Engine außerdem auf *direct PDF mode*, was Aspose anweist, die PDF‑Bytes direkt aus der Datei zu lesen, anstatt jede Seite zuerst in ein Bild zu konvertieren.

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr

# Step 2: Create an OCR engine instance and enable direct PDF processing
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
```

Warum `PdfMode.DIRECT` verwenden? Weil dadurch ein zusätzlicher Rasterisierungsschritt übersprungen wird, was den Vorgang schneller macht und das ursprüngliche Layout bewahrt – besonders praktisch, wenn Sie **recognize text from PDF** exakt benötigen.

## Text aus PDF erkennen – Engine ausführen

Mit der bereitstehenden Engine zeigen Sie ihr Ihre gescannte Datei. Die Methode `recognize_from_pdf` erledigt die schwere Arbeit: Sie parst jede Seite, führt den OCR‑Algorithmus aus und gibt ein `OcrResult`‑Objekt zurück, das eine Sammlung von `Page`‑Objekten enthält.

```python
# Step 3: Define the path to the PDF you want to process
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# Step 4: Perform OCR on the PDF and obtain the result object
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)
```

Falls Sie sich fragen, ob das mit verschlüsselten PDFs funktioniert – ja, solange Sie das Passwort vorher via `ocr_engine.password = "secret"` setzen, bevor Sie `recognize_from_pdf` aufrufen. Das ist ein Randfall, den viele Tutorials auslassen, der aber in realen Pipelines nützlich ist.

## Text aus PDF extrahieren – Seiten‑Ergebnisse zugreifen

Die Liste `ocr_result.pages` enthält einen Eintrag pro Seite. Jedes `Page`‑Objekt hat ein `.text`‑Attribut, das die reine Textdarstellung der gescannten Seite enthält. Lassen Sie uns darüber iterieren und die Ergebnisse ausgeben, damit Sie genau sehen, was extrahiert wurde.

```python
# Step 5: Iterate through each page and display the recognized text
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)
```

Das Ausführen des Skripts liefert etwa Folgendes:

```
PDF OCR complete. Text per page:
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Diese Ausgabe beweist, dass Sie erfolgreich **extract text from PDF** und **recognize text from PDF** mit Aspose OCR durchgeführt haben. Sie können die Zeichenketten nun in eine Datenbank, einen Suchindex oder jede nachgelagerte NLP‑Pipeline einspeisen.

![how to ocr pdf example](placeholder-image.png "how to ocr pdf example")

*Bild‑Alt‑Text:* **how to ocr pdf example** – zeigt die Konsolenausgabe des erkannten Textes pro Seite.

## Gescanntes PDF in Text umwandeln – Ausgabe speichern

Die meisten Entwickler wollen den Text nicht nur in der Konsole sehen; sie benötigen eine persistente Datei. Unten finden Sie einen kleinen Helfer, der den Text jeder Seite in eine separate `.txt`‑Datei schreibt und damit **convert scanned PDF to text** in einem Ordner namens `output` realisiert.

```python
import os

output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

Nach Abschluss des Skripts haben Sie ein aufgeräumtes Verzeichnis:

```
output_text/
│─ page_1.txt
│─ page_2.txt
└─ …
```

Damit haben Sie **convert scanned PDF to text** vollständig umgesetzt und können diese Dateien in jeden nachgelagerten Prozess einspeisen – Suche, Analysen oder sogar ein einfaches `grep`.

## Häufige Fragen & Randfälle

**Was, wenn mein PDF Bilder gemischt mit echtem Text enthält?**  
Aspose OCR versucht, alles zu erkennen, aber Sie können den Vorgang beschleunigen, indem Sie OCR für Seiten deaktivieren, die bereits auswählbaren Text enthalten. Setzen Sie `ocr_engine.auto_detect_page_orientation = True` und rufen Sie dann `ocr_engine.recognize_from_pdf(..., detect_text=False)` für bekannte, gut lesbare Seiten auf.

**Kann ich das Sprachmodell steuern?**  
Natürlich. Setzen Sie `ocr_engine.language = aocr.Language.English` (oder eine andere unterstützte Sprache) bevor Sie `recognize_from_pdf` aufrufen. Das erhöht die Genauigkeit bei nicht‑englischen Dokumenten.

**Wie gehe ich mit sehr großen PDFs (100+ Seiten) um?**  
Verarbeiten Sie sie in Teilen. Die Methode `recognize_from_pdf` akzeptiert ein `page_range`‑Argument, z. B. `ocr_engine.recognize_from_pdf(path, page_range=(1, 20))`. Schleifen Sie über Bereiche, um den Speicherverbrauch gering zu halten.

## Vollständiges funktionierendes Beispiel

Alles zusammengeführt, hier ein einzelnes Skript, das Sie in eine Datei namens `ocr_pdf.py` speichern und ausführen können:

```python
import os
import aspose.ocr as aocr

# -------------------------------------------------
# 1️⃣  Initialize the OCR engine (direct PDF mode)
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
# Optional: set language for better accuracy
ocr_engine.language = aocr.Language.English

# -------------------------------------------------
# 2️⃣  Path to the scanned PDF you want to process
# -------------------------------------------------
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# -------------------------------------------------
# 3️⃣  Run OCR – this is where we actually recognize text from PDF
# -------------------------------------------------
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)

# -------------------------------------------------
# 4️⃣  Print the extracted text (shows how to extract text from PDF)
# -------------------------------------------------
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)

# -------------------------------------------------
# 5️⃣  Save each page as a .txt file (convert scanned PDF to text)
# -------------------------------------------------
output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

Ausführen mit:

```bash
python ocr_pdf.py
```

Sie sollten eine Konsolenausgabe sehen, die den Text jeder Seite bestätigt und den Speicherort der gespeicherten `.txt`‑Dateien angibt.

## Fazit

Wir haben gezeigt, **wie man PDFs OCR‑t** mit Python, einen sauberen Weg zu **ocr pdf with python** demonstriert, erklärt, wie man **extract text from PDF** durchführt, die Funktionsweise von **recognize text from PDF** erläutert und schließlich ein einsatzbereites Snippet bereitgestellt, das **convert scanned PDF to text** erledigt. Der gesamte Prozess ist jetzt vollständig abgedeckt.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}