---
category: general
date: 2026-09-19
description: Das Python-OCR‑Tutorial zeigt, wie man PNG mit Aspose OCR in Text umwandelt.
  Lernen Sie die OCR‑Textextraktion in Python und extrahieren Sie Text aus gescannten
  Bildern.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- python OCR tutorial
- convert PNG to text
- OCR text extraction python
- extract text image python
- extract text scanned image
language: de
lastmod: 2026-09-19
og_description: Python OCR‑Tutorial führt Sie durch die Umwandlung von PNG in Text
  mit Aspose OCR. Meistern Sie die OCR‑Textextraktion mit Python und extrahieren Sie
  Text aus gescannten Bildern.
og_image_alt: Screenshot of Python OCR code extracting text from a PNG image
og_title: Python OCR‑Tutorial – PNG in Text umwandeln mit Aspose
schemas:
- author: Aspose
  dateModified: '2026-09-19'
  description: Python OCR tutorial shows how to convert PNG to text using Aspose OCR.
    Learn OCR text extraction python and extract text from scanned images.
  headline: 'Python OCR tutorial: convert PNG to text with Aspose'
  type: TechArticle
- description: Python OCR tutorial shows how to convert PNG to text using Aspose OCR.
    Learn OCR text extraction python and extract text from scanned images.
  name: 'Python OCR tutorial: convert PNG to text with Aspose'
  steps:
  - name: Expected output
    text: 'If `sample.png` contains the sentence “Hello, world!”, the console will
      show:'
  - name: 1. Non‑PNG formats
    text: Even though this tutorial focuses on **convert PNG to text**, you might
      receive JPEG or TIFF files. The same code works; just change the file extension
      in `load_image`.
  - name: 2. Low‑resolution images
    text: 'OCR accuracy drops below 150 dpi. If you encounter poor results, upscale
      the image first using Pillow:'
  - name: 3. Extracting text from a scanned image with multiple languages
    text: 'Set a comma‑separated list of language codes:'
  - name: 4. Large documents
    text: 'Processing many pages in a single run can exhaust memory. Process each
      page individually:'
  type: HowTo
tags:
- python
- OCR
- image processing
title: 'Python OCR‑Tutorial: PNG in Text konvertieren mit Aspose'
url: /de/python/general/python-ocr-tutorial-convert-png-to-text-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR‑Tutorial: PNG in Text konvertieren mit Aspose

Wenn Sie ein **python OCR‑Tutorial** benötigen, das ein PNG‑Bild in editierbaren Text umwandelt, bietet Ihnen dieser Leitfaden eine vollständige, sofort ausführbare Lösung. Sie sehen, wie Sie die Aspose OCR‑Bibliothek installieren, ein Bild laden, die Erkennungs‑Engine starten und die Ergebnisse ausgeben – alles in wenigen prägnanten Schritten.

Ein Dokument zu scannen und den Text herauszuziehen kann mühsam sein, besonders wenn Sie mit Bildformaten und Spracheinstellungen jonglieren. Dieses Tutorial nimmt das Rätselraten ab, indem es Ihnen genau zeigt, welche Methoden Sie aufrufen müssen und warum sie wichtig sind, sodass Sie sich auf die Integration von OCR in Ihre eigenen Anwendungen konzentrieren können.

Sie lernen außerdem, wie Sie **PNG in Text konvertieren**, gängige Stolperfallen umgehen und den Code für andere Bildtypen wie JPEG oder TIFF anpassen. Am Ende können Sie Text aus jedem gescannten Bild mit Zuversicht extrahieren.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

* Python 3.8 oder neuer installiert.
* Eine Internetverbindung zum Herunterladen des Aspose OCR‑Pakets.
* Ein PNG‑Bild (oder ein beliebiges unterstütztes Format), das lesbaren Text enthält.

Sie benötigen **keinen** separaten OCR‑Engine oder externe Binärdateien – Aspose OCR bündelt alles, was Sie brauchen.

## Schritt 1: Das Aspose OCR‑Paket installieren

Der erste Schritt besteht darin, die Bibliothek zu Ihrer Umgebung hinzuzufügen. Aspose stellt ein reines Python‑Paket bereit, das über pip installiert werden kann.

```bash
pip install aspose-ocr
```

> **Pro‑Tipp:** Verwenden Sie eine virtuelle Umgebung (`python -m venv venv`), um Abhängigkeiten von anderen Projekten zu isolieren.

Durch die Installation des Pakets wird das Modul `aspose.ocr` verfügbar, das die Klasse `OcrEngine` enthält, die in diesem Tutorial durchgehend verwendet wird.

## Schritt 2: Die OCR‑Engine‑Klasse importieren

Jetzt, wo das Paket vorhanden ist, importieren Sie die Klasse, die den Erkennungsprozess steuert.

```python
# Step 2: Import the OCR engine class
from aspose.ocr import OcrEngine
```

`OcrEngine` kapselt die gesamte Logik zum Laden von Bildern, Konfigurieren der Sprache und Extrahieren von Text. Der Import am Anfang folgt dem üblichen Python‑Stil und hält das Skript übersichtlich.

## Schritt 3: Eine Instanz der OCR‑Engine erstellen

Durch das Erstellen einer Instanz erhalten Sie eine frische Engine mit Standardeinstellungen. Sie können später Eigenschaften wie Sprache oder Bildvorverarbeitung anpassen.

```python
# Step 3: Create an instance of the OCR engine
engine = OcrEngine()
```

Ein neues `engine`‑Objekt repräsentiert eine einzelne OCR‑Sitzung. Die Wiederverwendung derselben Instanz für mehrere Bilder kann die Leistung verbessern, da interne Ressourcen zwischengespeichert werden.

## Schritt 4: Das zu verarbeitende Bild laden

Geben Sie den Pfad zur PNG‑Datei an, die Sie konvertieren möchten. Die Methode `load_image` akzeptiert jedes Format, das Aspose OCR unterstützt, sodass Sie auch JPEG, BMP oder TIFF‑Dateien übergeben können.

```python
# Step 4: Load the image you want to process
engine.load_image("YOUR_DIRECTORY/sample.png")
```

Falls die Datei nicht gefunden wird, wirft `load_image` einen `FileNotFoundError`. Um in Produktionscode eine benutzerfreundliche Fehlermeldung zu liefern, sollten Sie den Aufruf in einen `try/except`‑Block einbetten.

## Schritt 5: OCR ausführen, um Text aus dem Bild zu extrahieren

Der Aufruf von `recognize` startet die Erkennungspipeline und gibt den extrahierten String zurück. Die Methode übernimmt automatisch Layout‑Analyse, Zeichen‑Segmentierung und Spracherkennung (Standard ist Englisch).

```python
# Step 5: Perform OCR to extract text from the image
text = engine.recognize()
```

Sie können die Sprache vor dem Aufruf von `recognize` ändern:

```python
engine.language = "fr"   # for French text
```

Diese Flexibilität ist nützlich, wenn Sie **OCR‑Text‑Extraktion python** für mehrsprachige Dokumente benötigen.

## Schritt 6: Den erkannten Text ausgeben

Zum Schluss geben Sie das Ergebnis aus oder speichern es. Für einen schnellen Plausibilitäts‑Check zeigt `print` den Rohstring in der Konsole an.

```python
# Step 6: Output the recognized text
print(text)
```

### Erwartete Ausgabe

Enthält `sample.png` den Satz „Hello, world!“, erscheint in der Konsole:

```
Hello, world!
```

Die Ausgabe kann Zeilenumbrüche oder zusätzlichen Leerraum enthalten, abhängig vom ursprünglichen Layout. Sie können den String mit `str.strip()` oder regulären Ausdrücken nachbearbeiten, um ihn zu bereinigen.

## Umgang mit gängigen Sonderfällen

### 1. Nicht‑PNG‑Formate

Obwohl dieses Tutorial **PNG in Text konvertieren** behandelt, erhalten Sie möglicherweise JPEG‑ oder TIFF‑Dateien. Der gleiche Code funktioniert; ändern Sie lediglich die Dateierweiterung in `load_image`.

```python
engine.load_image("scanned_page.tiff")
```

### 2. Niedrigauflösende Bilder

Die OCR‑Genauigkeit sinkt unter 150 dpi. Wenn Sie schlechte Ergebnisse erhalten, skalieren Sie das Bild zuerst mit Pillow hoch:

```python
from PIL import Image

img = Image.open("sample.png")
high_res = img.resize((img.width * 2, img.height * 2), Image.LANCZOS)
high_res.save("sample_high_res.png")
engine.load_image("sample_high_res.png")
```

### 3. Text aus einem gescannten Bild mit mehreren Sprachen extrahieren

Setzen Sie eine kommagetrennte Liste von Sprachcodes:

```python
engine.language = "en,es,de"
```

Aspose OCR versucht, Zeichen aus allen angegebenen Sprachen zu erkennen.

### 4. Große Dokumente

Die Verarbeitung vieler Seiten in einem Durchlauf kann den Speicher erschöpfen. Verarbeiten Sie jede Seite einzeln:

```python
for page_path in ["page1.png", "page2.png", "page3.png"]:
    engine.load_image(page_path)
    print(engine.recognize())
```

## Vollständiges, ausführbares Skript

Wenn Sie alle Schritte zusammenfügen, erhalten Sie ein eigenständiges Programm, das Sie kopieren, einfügen und ausführen können.

```python
# python_ocr_tutorial.py
# Complete script for extracting text from a PNG image using Aspose OCR

# Install the library first:
# pip install aspose-ocr

from aspose.ocr import OcrEngine

def extract_text(image_path: str) -> str:
    """
    Loads an image and returns the recognized text.
    Parameters:
        image_path: Path to the PNG (or other supported) image.
    Returns:
        Recognized text as a string.
    """
    engine = OcrEngine()          # Create OCR engine instance
    engine.load_image(image_path) # Load the target image
    return engine.recognize()     # Perform OCR and return result

if __name__ == "__main__":
    # Replace with the actual path to your image
    path = "YOUR_DIRECTORY/sample.png"
    try:
        result = extract_text(path)
        print("=== Recognized Text ===")
        print(result)
    except Exception as e:
        print(f"Error during OCR processing: {e}")
```

Führen Sie das Skript aus mit:

```bash
python python_ocr_tutorial.py
```

Sie sollten den extrahierten Text in der Konsole sehen.

## Fazit

Dieses **python OCR‑Tutorial** hat gezeigt, wie Sie **PNG in Text konvertieren** mit Aspose OCR, von der Installation über das Laden des Bildes bis hin zur Erkennung und Ausgabe. Sie besitzen nun ein zuverlässiges Muster für **OCR‑Text‑Extraktion python** und können den Code anpassen, um **Text aus Bild python** aus jedem gescannten Dokument zu extrahieren.

Von hier aus können Sie:

* Das Skript in einen Web‑Service (z. B. Flask) integrieren, um OCR als API bereitzustellen.
* Extrahierten Text in einer Datenbank speichern, um durchsuchbare Archive zu erstellen.
* Mit verschiedenen Spracheinstellungen experimentieren, um mehrsprachige Scans zu verarbeiten.

Viel Spaß beim Coden und beim Umwandeln von Bildern in durchsuchbaren, editierbaren Text!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Python OCR Tutorial: Extract Table Text from Images](/ocr/english/python-java/general/python-ocr-tutorial-extract-table-text-from-images/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}