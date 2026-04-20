---
category: general
date: 2026-03-18
description: Erfahren Sie, wie Sie Text aus Bildern extrahieren und den Text gescannter
  Bilder in editierbare Zeichenketten mit Aspose OCR in Python umwandeln. Schritt‑für‑Schritt‑Code
  ist enthalten.
draft: false
keywords:
- extract text from images
- convert scanned images text
- Aspose OCR Python
- batch OCR processing
- image to text conversion
language: de
og_description: Extrahiere Text aus Bildern mit Aspose OCR in Python. Dieses Tutorial
  zeigt, wie man gescannten Bildtext mit nur wenigen Codezeilen konvertiert.
og_title: Text aus Bildern mit Aspose OCR extrahieren – Python‑Leitfaden
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Text aus Bildern mit Aspose OCR extrahieren – Python‑Leitfaden
url: /de/python-java/general/extract-text-from-images-with-aspose-ocr-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bildern extrahieren mit Aspose OCR – Python‑Leitfaden

Haben Sie jemals **Text aus Bildern** extrahieren müssen, wussten aber nicht, wo Sie anfangen sollten? Sie sind nicht allein – Entwickler stehen ständig vor der Herausforderung, gescannte PDFs, verrauschte Screenshots oder fotografierte Quittungen in durchsuchbare, editierbare Zeichenketten zu verwandeln.  

Die gute Nachricht? Mit Aspose OCR für Python können Sie **gescannten Bildtext** massenhaft konvertieren, und das ganz ohne Ihre IDE zu verlassen. In diesem Tutorial führen wir Sie durch ein vollständiges, sofort ausführbares Beispiel, das genau zeigt, wie es geht, warum jeder Schritt wichtig ist und worauf Sie achten sollten.

## Was Sie lernen werden

- Richten Sie die Aspose OCR‑Bibliothek in einer Python‑Umgebung ein.  
- Erstellen Sie eine Liste von Bilddateien (PNG, JPG, TIFF usw.).  
- Führen Sie die Batch‑OCR mit einem einzigen Methodenaufruf aus.  
- Greifen Sie auf den extrahierten Text für jede Datei zu und zeigen Sie ihn an.  
- Behandeln Sie häufige Fallstricke wie nicht unterstützte Formate und Speicherverbrauch bei großen Dateien.  

Am Ende haben Sie ein wiederverwendbares Skript, das **Text aus Bildern** auf Abruf extrahieren kann – ideal zur Automatisierung von Dateneingaben, zur Indexierung von Dokumenten oder zur Versorgung nachgelagerter NLP‑Pipelines.

---

![Beispiel für das Extrahieren von Text aus Bildern](/images/ocr-extract-text.png "Text aus Bildern extrahieren")

*Bild‑Alt‑Text: “Text aus Bildern mit Aspose OCR in Python extrahieren”*

## Voraussetzungen

- Python 3.8 oder neuer (der Code verwendet f‑Strings).  
- Eine gültige Aspose OCR für Python‑Lizenz oder ein kostenloser Testschlüssel.  
- Die Bilder, die Sie verarbeiten möchten, lokal gespeichert (beliebige Mischung aus PNG, JPG oder TIFF).  

If you already have a virtual environment, great—if not, create one with:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate
```

Jetzt sind Sie bereit, das SDK zu installieren.

## Schritt 1: Installieren des Aspose OCR SDK

Aspose verteilt seine OCR‑Engine über PyPI, sodass ein einzelner `pip`‑Befehl ausreicht:

```bash
pip install aspose-ocr
```

> **Pro‑Tipp:** Fixieren Sie die Version (z. B. `aspose-ocr==22.12`), um später unerwartete Breaking‑Changes zu vermeiden.

## Schritt 2: Importieren der OCR‑Engine‑Klasse

Der Kernklasse, mit der Sie arbeiten werden, ist `OcrEngine`. Importieren Sie sie am Anfang Ihres Skripts:

```python
# Step 2: Import the OCR engine class
from asposeocr import OcrEngine
```

> *Warum das wichtig ist:* Nur das zu importieren, was Sie benötigen, hält die Startzeit niedrig, besonders wenn Sie das Skript später in eine größere Anwendung einbetten.

## Schritt 3: Definieren der zu verarbeitenden Bilddateien

Erstellen Sie eine Python‑Liste, die die vollständigen Pfade zu jedem Bild enthält, das Sie scannen möchten. Ersetzen Sie `YOUR_DIRECTORY` durch den tatsächlichen Ordnerpfad.

```python
# Step 3: Define the image files to be processed
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.jpg",
    "YOUR_DIRECTORY/page3.tif"
]
```

> **Randfall:** Wenn Sie Hunderte von Dateien haben, sollten Sie diese Liste programmgesteuert mit `glob.glob('*.png')` erzeugen, um manuelle Änderungen zu vermeiden.

## Schritt 4: OCR auf alle Bilder gleichzeitig ausführen

Aspose OCR bietet eine bequeme `processMultiple`‑Methode, die eine Liste von `OcrResult`‑Objekten zurückgibt – eines für jede Eingabedatei.

```python
# Step 4: Run OCR on all images at once
ocr_engine = OcrEngine()               # instantiate the engine
ocr_results = ocr_engine.processMultiple(image_files)
```

> *Warum Batch‑Verarbeitung?* Das Senden jedes Bildes einzeln verursacht zusätzlichen Overhead (Initialisierung der Engine, Laden nativer Bibliotheken). Der Batch‑Aufruf reduziert die CPU‑Belastung und beschleunigt den gesamten Vorgang.

### Fehler elegant behandeln

Wenn ein Bild nicht gelesen werden kann (beschädigte Datei, nicht unterstütztes Format), wird `processMultiple` eine Ausnahme auslösen. Umschließen Sie den Aufruf in einem `try/except`‑Block, um das Skript am Laufen zu halten:

```python
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as e:
    print(f"⚠️ OCR failed: {e}")
    ocr_results = []   # fallback to empty list
```

## Schritt 5: Ausgabe des extrahierten Textes für jede Datei

Iterieren Sie über die Ergebnisse und verbinden Sie jedes `OcrResult` mit seinem ursprünglichen Dateinamen. Die Methode `getText()` gibt die erkannte Zeichenkette zurück.

```python
# Step 5: Output the extracted text for each file
for index, result in enumerate(ocr_results, start=1):
    file_path = image_files[index - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")   # add a blank line for readability
```

### Erwartete Ausgabe

Das Ausführen des vollständigen Skripts mit drei einfachen Screenshots könnte etwa Folgendes erzeugen:

```
--- Text from file YOUR_DIRECTORY/page1.png ---
Invoice #12345
Date: 2024‑07‑01
Total: $256.78

--- Text from file YOUR_DIRECTORY/page2.jpg ---
Welcome to the Annual Report
Prepared by: Finance Dept.

--- Text from file YOUR_DIRECTORY/page3.tif ---
© 2025 Acme Corp. All rights reserved.
```

Wenn ein Bild keine erkennbaren Zeichen enthält, sehen Sie eine leere Zeichenkette – nichts bricht, und Sie können entscheiden, ob Sie diese Datei zur manuellen Überprüfung markieren.

## Bonus: Feinabstimmung der OCR‑Genauigkeit

Aspose OCR bietet mehrere optionale Einstellungen, mit denen Sie experimentieren können:

| Einstellung | Was es bewirkt | Wann zu verwenden |
|------------|----------------|-------------------|
| `ocr_engine.setLanguage('eng')` | Erzwingt das englische Sprachmodell (reduziert Fehlalarme). | Meist englische Dokumente. |
| `ocr_engine.setResolution(300)` | Verbessert die Genauigkeit bei Low‑DPI‑Scans. | Scans unter 200 dpi. |
| `ocr_engine.setPageSegMode('single_block')` | Betrachtet das gesamte Bild als einen Textblock. | Einfache Quittungen oder Ausweise. |

Sie können diese Zeilen direkt nach der Erstellung von `ocr_engine` hinzufügen:

```python
ocr_engine.setLanguage('eng')
ocr_engine.setResolution(300)
ocr_engine.setPageSegMode('single_block')
```

## Häufige Stolperfallen & wie man sie vermeidet

1. **Große TIFF‑Stacks** – Ein mehrseitiges TIFF kann beim Laden auf einmal Gigabytes RAM verbrauchen. Teilen Sie die Datei in Einzel‑Seiten‑Bilder, bevor Sie sie an `processMultiple` übergeben.  
2. **Nicht‑lateinische Schriften** – Wenn Sie **Text aus Bildern** extrahieren müssen, die Kyrillisch, Arabisch oder Chinesisch enthalten, ändern Sie den Sprachcode entsprechend (`'rus'`, `'ara'`, `'chi_sim'`).  
3. **Dateipfad‑Leerzeichen** – Windows‑Pfade mit Leerzeichen können `FileNotFoundError` auslösen. Umschließen Sie jeden Pfad in Rohstrings (`r"C:\My Folder\image.png"`) oder verwenden Sie `os.path.abspath`.  

Das frühzeitige Behandeln dieser Probleme bewahrt Sie später vor kryptischen Laufzeitfehlern.

---

## Vollständiges funktionierendes Beispiel

Unten finden Sie das vollständige Skript, das Sie in eine Datei namens `batch_ocr.py` kopieren können. Es enthält alle oben besprochenen Best‑Practice‑Anpassungen.

```python
# batch_ocr.py
# -------------------------------------------------
# Complete example: extract text from images using Aspose OCR (Python)
# -------------------------------------------------

from asposeocr import OcrEngine
import os

# -------------------------------------------------
# Configuration – adjust these values for your environment
# -------------------------------------------------
IMAGE_DIR = "YOUR_DIRECTORY"   # <-- replace with your folder path
SUPPORTED_EXT = (".png", ".jpg", ".jpeg", ".tif", ".tiff")

# Build a list of image file paths automatically
image_files = [
    os.path.join(IMAGE_DIR, f)
    for f in os.listdir(IMAGE_DIR)
    if f.lower().endswith(SUPPORTED_EXT)
]

if not image_files:
    print("⚠️ No supported image files found in the specified directory.")
    exit(1)

# -------------------------------------------------
# Initialize OCR engine with optional tweaks
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.setLanguage('eng')          # English language model
ocr_engine.setResolution(300)          # Boost low‑dpi accuracy
ocr_engine.setPageSegMode('single_block')  # Treat whole image as one block

# -------------------------------------------------
# Run batch OCR and handle potential errors
# -------------------------------------------------
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as exc:
    print(f"❌ OCR processing failed: {exc}")
    ocr_results = []

# -------------------------------------------------
# Display extracted text
# -------------------------------------------------
for idx, result in enumerate(ocr_results, start=1):
    file_path = image_files[idx - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")
```

Speichern Sie, aktivieren Sie Ihre virtuelle Umgebung und führen Sie aus:

```bash
python batch_ocr.py
```

Sie sollten die extrahierten Zeichenketten in der Konsole sehen, bereit für die weitere Verarbeitung (z. B. Speicherung in einer Datenbank oder Weitergabe an ein Natural‑Language‑Modell).

---

## Fazit

In diesem Leitfaden haben wir gezeigt, wie man **Text aus Bildern** mit Aspose OCR für Python extrahiert, und dabei alles von der Installation über die Batch‑Verarbeitung bis hin zur Fehlerbehandlung abgedeckt. Das Skript ist kompakt, voll funktionsfähig und leicht erweiterbar – egal, ob Sie **gescannten Bildtext** in CSV‑Dateien umwandeln, einen Suchindex füttern oder einfach die Dateneingabe automatisieren müssen.

Bereit für den nächsten Schritt? Erwägen Sie, diese OCR‑Pipeline mit einem PDF‑Merger zu kombinieren, um durchsuchbare PDFs zu erstellen, oder binden Sie sie in einen Cloud‑Speicher‑Trigger ein, sodass jeder hochgeladene Scan sofort verarbeitet wird. Der Himmel ist die Grenze, und Sie haben jetzt eine solide Grundlage zum Weiterbauen.

Haben Sie Fragen oder Verbesserungsvorschläge? Hinterlassen Sie unten einen Kommentar, und happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}