---
category: general
date: 2026-08-12
description: Führen Sie OCR auf einem Bild mit Python und Aspose AI durch, um Text
  aus dem Bild zu extrahieren und die OCR‑Genauigkeit mit einem nachträglichen Rechtschreib‑Korrektur‑Post‑Processor
  zu verbessern.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from image
- OCR text correction
- improve OCR accuracy
- load image for OCR
language: de
lastmod: 2026-08-12
og_description: Führen Sie OCR auf einem Bild in Python aus und extrahieren Sie sofort
  Text aus dem Bild, während Sie die OCR‑Genauigkeit mit der Nachbearbeitung durch
  Aspose AI verbessern.
og_image_alt: Diagram showing the run OCR on image workflow in Python
og_title: OCR auf Bild mit Python ausführen – vollständiges Tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Run OCR on image using Python and Aspose AI to extract text from image
    and improve OCR accuracy with a spell‑checking post‑processor.
  headline: Run OCR on image with Python – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- Image Processing
title: OCR auf Bild mit Python ausführen – Schritt‑für‑Schritt‑Anleitung
url: /de/python/general/run-ocr-on-image-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR auf Bild mit Python ausführen – Schritt‑für‑Schritt‑Anleitung

Wenn Sie **OCR auf Bild**‑Dateien in Python ausführen müssen, führt Sie diese Anleitung durch den gesamten Workflow. Sie lernen, wie Sie **Text aus Bild** extrahieren, **OCR‑Textkorrektur** anwenden und **OCR‑Genauigkeit** mit nur wenigen Code‑Zeilen verbessern.

Das Verarbeiten gescannter Dokumente, Quittungen oder Screenshots liefert häufig verrauschten Text. Durch das Anbinden einer Rechtschreib‑Nachbearbeitung können Sie rohe OCR‑Ausgaben in sauberen, durchsuchbaren Inhalt verwandeln, ohne zu einem separaten Tool zu wechseln. Dieses Tutorial deckt alles ab – vom Laden des Bildes bis zur Anzeige des korrigierten Ergebnisses.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie:

* Python 3.9 oder neuer installiert haben.
* Zugriff auf die Aspose.OCR‑ und Aspose.AI‑Python‑Pakete (oder deren gleichwertige Open‑Source‑Wrapper) besitzen.
* Ein Beispielbild (z. B. `sample.png`) in einem bekannten Verzeichnis abgelegt haben.
* Grundlegende Kenntnisse in Python‑Funktionen und objektorientiertem Code.

Sie können die erforderlichen Bibliotheken mit pip installieren:

```bash
pip install aspose-ocr aspose-ai
```

> **Pro‑Tipp:** Verwenden Sie eine virtuelle Umgebung (`python -m venv .venv`), um Abhängigkeiten isoliert zu halten.

## Schritt 1: OCR auf Bild ausführen – Engine‑Instanz erstellen

Der erste Schritt besteht darin, ein `OcrEngine`‑Objekt zu erstellen. Dieses Objekt kapselt die OCR‑Engine‑Konfiguration und stellt Methoden für Bildverarbeitung und Erkennung bereit.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine with default settings
ocr_engine = OcrEngine()
```

Die Engine einmal zu erstellen und über mehrere Bilder hinweg wiederzuverwenden reduziert den Start‑Overhead und sorgt für konsistente Einstellungen während der gesamten Sitzung.

## Schritt 2: Bild für OCR laden

Bevor eine Erkennung stattfinden kann, muss die Engine wissen, welches Bild analysiert werden soll. Die Methode `load_image` akzeptiert einen Dateipfad oder einen Binär‑Stream.

```python
# Provide the full path to your image file
image_path = "YOUR_DIRECTORY/sample.png"
ocr_engine.load_image(image_path)
```

> **Warum das wichtig ist:** Das Bild korrekt zu laden ist die Grundlage für genaue OCR. Das Bereitstellen eines hochauflösenden Bildes (300 dpi oder höher) **verbessert typischerweise die OCR‑Genauigkeit**, weil die Engine die Zeichen klarer unterscheiden kann.

## Schritt 3: Text aus Bild extrahieren – Grundlegende Erkennung durchführen

Nachdem das Bild geladen ist, können Sie `recognize()` aufrufen, um ein Ergebnis‑Objekt zu erhalten. Das Ergebnis enthält den rohen Text, Vertrauenswerte und optional Begrenzungsrahmen für jedes Wort.

```python
# Run the OCR process
plain_result = ocr_engine.recognize()   # returns a Result object

# The raw OCR output is accessible via the .text attribute
print("Raw OCR output:")
print(plain_result.text)
```

An diesem Punkt haben Sie erfolgreich **OCR auf Bild** ausgeführt und die rohen Zeichen extrahiert. Der Text kann jedoch Rechtschreibfehler enthalten, insbesondere bei minderwertigen Scans.

## Schritt 4: OCR‑Textkorrektur – Post‑Processing‑Rechtschreibprüfung anhängen

Aspose AI bietet eine flexible Nachbearbeitungspipeline. Durch das Einbinden einer eigenen Rechtschreibprüfung können typische OCR‑Fehler korrigiert werden (z. B. „l“ vs. „1“, „O“ vs. „0“).

```python
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker   # your own implementation

# Initialize the AI engine and set the post‑processor
ai_engine = AsposeAI()
ai_engine.set_post_processor(MySpellChecker())

# Run the post‑processor on the plain OCR result
corrected_result = ai_engine.run_postprocessor(plain_result)
```

**Wie die Rechtschreibprüfung funktioniert:** `MySpellChecker` sollte eine Methode `process(text: str) -> str` implementieren. Darin können Sie Bibliotheken wie `pyspellchecker` oder `symspellpy` nutzen, um unwahrscheinliche Wortfolgen durch wörterbuchvalidierte Alternativen zu ersetzen.

```python
# Example implementation (very simple)
from spellchecker import SpellChecker

class MySpellChecker:
    def __init__(self):
        self.spell = SpellChecker()

    def process(self, text: str) -> str:
        corrected = []
        for word in text.split():
            corrected.append(self.spell.correction(word))
        return " ".join(corrected)
```

## Schritt 5: Originalen und korrigierten OCR‑Text anzeigen

Zum Schluss vergleichen Sie die rohen und korrigierten Ausgaben. Das hilft Ihnen zu überprüfen, dass die **OCR‑Textkorrektur** tatsächlich die **OCR‑Genauigkeit** für Ihren Anwendungsfall **verbessert** hat.

```python
print("\nOriginal :", plain_result.text)
print("Corrected:", corrected_result.text)
```

### Erwartete Ausgabe

```
Original : Th1s is a s4mpl3 rec3pt with som3 err0rs.
Corrected: This is a simple receipt with some errors.
```

Die korrigierte Zeile zeigt, dass die Rechtschreibprüfung häufige OCR‑Fehlinterpretationen ersetzt hat (`Th1s` → `This`, `s4mpl3` → `simple`, `rec3pt` → `receipt`, `som3` → `some`, `err0rs` → `errors`).

## Schritt 6: OCR‑Genauigkeit verbessern – Best‑Practice‑Checkliste

Selbst mit Nachbearbeitung können Sie die Basisqualität der OCR‑Engine steigern:

| Checklisten‑Punkt | Warum es hilft |
|-------------------|----------------|
| **Verwenden Sie hochauflösende Bilder (≥300 dpi)** | Mehr Pixeldaten reduzieren Zeichen‑Mehrdeutigkeiten. |
| **Konvertieren Sie Farbbilder in Graustufen** | Entfernt Farbrauschen, das die Engine verwirren kann. |
| **Bildentzerrung anwenden** | Gerade Texte verhindern Zeilenumbruch‑Fehler. |
| **Sprache/Locale explizit setzen** | Leitet den Erkenner zur richtigen Zeichensatz‑Auswahl. |
| **Sprachmodell aktivieren** (falls die Bibliothek es unterstützt) | Liefert kontextabhängige Vorhersagen und verbessert weiter die **OCR‑Genauigkeit**. |

Sie können diese Vorverarbeitungsschritte mit Pillow oder OpenCV implementieren, bevor Sie das Bild an `ocr_engine` übergeben.

```python
from PIL import Image, ImageOps
import cv2
import numpy as np

def preprocess_image(path: str) -> str:
    # Load with Pillow, convert to grayscale, and increase contrast
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)

    # Save a temporary preprocessed file
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

# Use the preprocessor
preprocessed_path = preprocess_image(image_path)
ocr_engine.load_image(preprocessed_path)
```

## Vollständiges ausführbares Skript

Wenn Sie alles zusammenfügen, ist das folgende Skript bereit zum Kopieren‑Einfügen in eine Datei namens `run_ocr.py` und zur Ausführung.

```python
# run_ocr.py
from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker
from PIL import Image, ImageOps

def preprocess_image(path: str) -> str:
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load and preprocess the image
    raw_path = "YOUR_DIRECTORY/sample.png"
    processed_path = preprocess_image(raw_path)
    ocr_engine.load_image(processed_path)

    # 3️⃣ Perform basic OCR
    plain_result = ocr_engine.recognize()

    # 4️⃣ Run OCR text correction
    ai_engine = AsposeAI()
    ai_engine.set_post_processor(MySpellChecker())
    corrected_result = ai_engine.run_postprocessor(plain_result)

    # 5️⃣ Show both results
    print("\nOriginal :", plain_result.text)
    print("Corrected:", corrected_result.text)

if __name__ == "__main__":
    main()
```

Das Ausführen des Skripts gibt den originalen und den korrigierten Text aus und bestätigt, dass Sie erfolgreich **OCR auf Bild** ausgeführt, **Text aus Bild** extrahiert und die **OCR‑Genauigkeit** durch **OCR‑Textkorrektur** verbessert haben.

## Fazit

Sie wissen nun, wie Sie **OCR auf Bild**‑Dateien in Python ausführen, den rohen Text extrahieren und eine Post‑Processing‑Rechtschreibprüfung anwenden, um sauberere Ergebnisse zu erzielen. Durch Befolgen der Checkliste zur **Verbesserung der OCR‑Genauigkeit** können Sie diesen Workflow an Quittungen, Rechnungen, Ausweise oder jedes gescannte Dokument anpassen.

### Was kommt als Nächstes?

* Erkunden Sie **sprachspezifische Wörterbücher** für mehrsprachige OCR.
* Integrieren Sie die Pipeline in eine Datenbank oder einen Suchindex (z. B. Elasticsearch), um den extrahierten Text durchsuchbar zu machen.
* Ersetzen Sie die einfache Rechtschreibprüfung durch ein neuronales Sprachmodell (z. B. GPT‑basierte Korrektur) für noch höhere Genauigkeit.

Experimentieren Sie gern mit verschiedenen Bildvorverarbeitungstechniken, unterschiedlichen Nachbearbeitern oder alternativen OCR‑Engines. Das Kernmuster — **OCR auf Bild → Text aus Bild extrahieren → OCR‑Textkorrektur → OCR‑Genauigkeit verbessern** — bleibt gleich und bietet Ihnen eine robuste Grundlage für jedes Dokument‑Digitalisierungsprojekt.

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}