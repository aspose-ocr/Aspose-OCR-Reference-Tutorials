---
category: general
date: 2026-06-16
description: Wie man OCR in Python verwendet, um Text aus Bilddateien wie PNG zu extrahieren.
  Lernen Sie die schrittweise Umwandlung von Bild zu Text mit Aspose OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- read text from png
- convert image to text
- ocr image to text python
language: de
og_description: Wie man OCR in Python verwendet, um Text aus Bildern zu extrahieren.
  Dieser Leitfaden führt Sie durch die Umwandlung von PNG‑Dateien in durchsuchbaren
  Text mit Aspose OCR.
og_title: Wie man OCR in Python verwendet – Text aus Bildern extrahieren
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to use OCR in Python to extract text from image files like PNG.
    Learn step‑by‑step conversion of image to text with Aspose OCR.
  headline: How to Use OCR in Python – Extract Text from Images
  type: TechArticle
- description: How to use OCR in Python to extract text from image files like PNG.
    Learn step‑by‑step conversion of image to text with Aspose OCR.
  name: How to Use OCR in Python – Extract Text from Images
  steps:
  - name: Expected Output
    text: '``` Detected language: English Recognized text: Hello, world! This is a
      multi‑language test. こんにちは世界 ```'
  - name: 1. License Not Found
    text: If you see an error like `License file not found`, double‑check the path
      you passed to `set_license`. Using a raw string (`r"..."`) helps avoid escape‑character
      mishaps on Windows.
  - name: 2. Blank Output
    text: 'A blank `ocr_result.text` usually means the image is too noisy or the text
      is too faint. Try increasing the image contrast:'
  - name: 3. Wrong Language Detection
    text: 'If the auto‑detect picks the wrong language, you can force a specific one:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Aspose
title: Wie man OCR in Python verwendet – Text aus Bildern extrahieren
url: /de/python-java/general/how-to-use-ocr-in-python-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in Python verwendet – Text aus Bildern extrahieren

Haben Sie sich schon einmal gefragt, **wie man OCR** in einem Python‑Projekt verwendet? Sie sind nicht allein. Egal, ob Sie einen Belegscanner, ein Dokumentenarchiv erstellen oder einfach nur neugierig darauf sind, einen Screenshot in editierbaren Text zu verwandeln – die Möglichkeit, **Text aus Bild**‑Dateien zu **extrahieren**, ist ein echter Wendepunkt.

In diesem Tutorial führen wir Sie durch den gesamten Prozess – von der Installation der Aspose OCR‑Bibliothek bis zum Auslesen von Text aus einer PNG‑Datei – sodass Sie **Bild zu Text konvertieren** können, und das mit nur wenigen Codezeilen. Am Ende wissen Sie genau, **wie man Text aus PNG** liest und sogar mehrsprachige Inhalte automatisch verarbeitet.

> **Pro‑Tipp:** Die automatische Spracherkennung von Aspose OCR bedeutet, dass Sie die Sprache nicht im Voraus erraten müssen – perfekt für Apps, die weltweit eingesetzt werden.

## Was Sie benötigen

- Python 3.8+ (die neueste stabile Version ist in Ordnung)
- Eine gültige Aspose OCR‑Lizenzdatei (`Aspose.OCR.lic`). Die kostenlose Testversion funktioniert zum Testen, aber eine richtige Lizenz entfernt Evaluationsbeschränkungen.
- Das Aspose OCR‑Paket, installiert über `pip`:

```bash
pip install aspose-ocr
```

- Eine Bilddatei, die Sie verarbeiten möchten – wir verwenden `sample-multi-lang.png` als Demo.

Wenn diese Voraussetzungen bereitstehen, verläuft der Ablauf reibungslos und Sie vermeiden später überraschende „module not found“-Fehler.

![Wie man OCR in Python verwendet – Arbeitsablauf](https://example.com/ocr-workflow.png "Wie man OCR in Python verwendet – Schritt‑für‑Schritt‑Illustration")

*Bildbeschreibung: Diagramm, das zeigt, wie man OCR in Python verwendet, um Text aus einem Bild zu extrahieren.*

## Schritt 1: Laden Sie Ihre Aspose OCR‑Lizenz (einmal pro Anwendung erforderlich)

Das allererste, was jedes ernsthafte OCR‑Projekt tut, ist das Laden einer Lizenz. Ohne diese gibt Aspose eine Warnung aus und begrenzt die Anzahl der Seiten, die Sie verarbeiten können.

```python
# Import the license class
from aspose.ocr import License

# Create a License object and point it to your .lic file
ocr_license = License()
ocr_license.set_license(r"C:\Path\To\Your\Aspose.OCR.lic")
```

> **Warum das wichtig ist:** Das Vorab‑Laden der Lizenz stellt sicher, dass die **ocr image to text python**‑Engine mit voller Geschwindigkeit und ohne Wasserzeichen läuft. Betrachten Sie es als das Freischalten der Premium‑Funktionen, bevor Sie mit der Konvertierung beginnen.

## Schritt 2: Erstellen Sie eine OCR‑Engine und aktivieren Sie die automatische Spracherkennung

Jetzt instanziieren wir die Kern‑Engine. Das Aktivieren von `language_auto_detect` ist entscheidend, wenn Sie nicht wissen, ob das Bild Englisch, Spanisch, Chinesisch oder eine Mischung verschiedener Sprachen enthält.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine
ocr_engine = OcrEngine()

# Turn on auto‑language detection – it works for over 60 languages
ocr_engine.language_auto_detect = True
```

Wenn Sie die Sprache *vorab* kennen, können Sie `ocr_engine.language = "English"` (oder einen anderen unterstützten ISO‑Code) setzen, um den Vorgang etwas zu beschleunigen. Für ein generisches „Text aus PNG lesen“-Dienstprogramm ist jedoch die automatische Erkennung die sicherste Wahl.

## Schritt 3: Laden Sie das Bild, das Sie verarbeiten möchten

Aspose OCR arbeitet mit einer Vielzahl von Formaten – PNG, JPEG, BMP, TIFF, Sie nennen es. Laden wir eine PNG‑Datei, die mehrere Sprachen enthält.

```python
from aspose.ocr import Image

# Load the image from disk (replace with your actual path)
ocr_image = Image.load_from_file(r"C:\Path\To\sample-multi-lang.png")

# Assign the image to the engine
ocr_engine.image = ocr_image
```

> **Randfall:** Wenn das Bild sehr groß ist (über ein paar Megabyte), sollten Sie es zuerst verkleinern, um die Leistung zu verbessern. Aspose stellt dafür `ocr_image.resize(width, height)` bereit.

## Schritt 4: OCR‑Erkennung durchführen

Wenn alles verbunden ist, erfolgt die eigentliche Textextraktion mit einem einzigen Methodenaufruf. Das Ergebnisobjekt liefert sowohl den erkannten Text als auch die erkannte Sprache.

```python
# Run the recognition process
ocr_result = ocr_engine.recognize()
```

Im Hintergrund nutzt Aspose ausgeklügelte neuronale Netze und Mustererkennungs‑Algorithmen, um jede Pixelgruppe in Zeichen zu verwandeln. Die schwere Arbeit wird komplett im nativen Code erledigt, sodass Sie **schnelles, genaues OCR** selbst auf bescheidener Hardware erhalten.

## Schritt 5: Zeigen Sie die erkannte Sprache und den erkannten Text an

Zum Schluss geben wir aus, was wir erhalten haben. Die Eigenschaft `detected_language` zeigt an, welche Sprache Aspose vermutet hat, und `text` enthält die vollständige Transkription.

```python
print("Detected language:", ocr_result.detected_language)
print("Recognized text:\n", ocr_result.text)
```

### Erwartete Ausgabe

```
Detected language: English
Recognized text:
 Hello, world!
 This is a multi‑language test.
 こんにちは世界
```

Wenn Sie das Skript mit einem Bild ausführen, das sowohl Englisch als auch Japanisch enthält, wird die Sprache automatisch umgeschaltet – dank der zuvor aktivierten Auto‑Detect‑Funktion.

## Umgang mit häufigen Problemen

### 1. Lizenz nicht gefunden

Wenn Sie einen Fehler wie `License file not found` sehen, überprüfen Sie den Pfad, den Sie an `set_license` übergeben haben, erneut. Die Verwendung eines rohen Strings (`r"..."`) hilft, Escape‑Zeichen‑Probleme unter Windows zu vermeiden.

### 2. Leere Ausgabe

Ein leerer `ocr_result.text` bedeutet in der Regel, dass das Bild zu verrauscht oder der Text zu schwach ist. Versuchen Sie, den Bildkontrast zu erhöhen:

```python
ocr_image = Image.load_from_file("sample.png")
ocr_image = ocr_image.adjust_contrast(1.5)  # Boost contrast by 50%
ocr_engine.image = ocr_image
```

### 3. Falsche Spracherkennung

Wenn die Auto‑Detect‑Funktion die falsche Sprache auswählt, können Sie eine bestimmte Sprache erzwingen:

```python
ocr_engine.language = "Japanese"  # ISO code or language name
```

## Erweiterung des Beispiels: Stapelverarbeitung mehrerer PNG‑Dateien

Oft möchten Sie **Bild zu Text konvertieren** für einen ganzen Ordner, nicht nur für eine einzelne Datei. Hier ist eine kurze Schleife, die jedes PNG in einem Verzeichnis verarbeitet:

```python
import os
from pathlib import Path

input_folder = Path(r"C:\Images")
output_folder = Path(r"C:\OCR_Output")
output_folder.mkdir(exist_ok=True)

for png_path in input_folder.glob("*.png"):
    # Load and assign image
    ocr_image = Image.load_from_file(str(png_path))
    ocr_engine.image = ocr_image

    # Recognize
    result = ocr_engine.recognize()

    # Write result to a .txt file with the same base name
    txt_path = output_folder / (png_path.stem + ".txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(f"Detected language: {result.detected_language}\n")
        f.write(result.text)

    print(f"Processed {png_path.name} → {txt_path.name}")
```

Dieses Snippet zeigt eine praktische Methode, **Text aus Bild**‑Dateien massenhaft zu **extrahieren**, ein häufiges Bedürfnis in Dokumenten‑Digitalisierungspipelines.

## Vollständiges funktionierendes Skript

Alles zusammengefasst, hier ist eine einzelne Datei, die Sie von Anfang bis Ende ausführen können:

```python
# ocr_demo.py
import os
from aspose.ocr import License, OcrEngine, Image

# -------------------------------------------------
# 1️⃣ Apply license (replace with your own path)
# -------------------------------------------------
license_path = r"C:\Path\To\Aspose.OCR.lic"
ocr_license = License()
ocr_license.set_license(license_path)

# -------------------------------------------------
# 2️⃣ Create engine and enable auto‑detect
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.language_auto_detect = True

# -------------------------------------------------
# 3️⃣ Load image (change to your PNG file)
# -------------------------------------------------
image_path = r"C:\Path\To\sample-multi-lang.png"
ocr_image = Image.load_from_file(image_path)
ocr_engine.image = ocr_image

# -------------------------------------------------
# 4️⃣ Recognize and output results
# -------------------------------------------------
ocr_result = ocr_engine.recognize()
print("Detected language:", ocr_result.detected_language)
print("Recognized text:\n", ocr_result.text)
```

Speichern Sie dies als `ocr_demo.py`, führen Sie `python ocr_demo.py` aus, und Sie sehen die Sprache und den Text in der Konsole ausgegeben.

## Fazit

Wir haben gezeigt, **wie man OCR** in Python von Anfang bis Ende verwendet, und Ihnen gezeigt, wie man **Text aus Bild** extrahiert, **Text aus PNG** liest und allgemein **Bild zu Text** konvertiert, wobei die leistungsstarke Engine von Aspose zum Einsatz kommt. Durch das Laden einer Lizenz, das Aktivieren der automatischen Spracherkennung und das Einspeisen eines Bildes in die `OcrEngine` erhalten Sie in Sekunden sauberen, durchsuchbaren Text.

Was kommt als Nächstes? Versuchen Sie, Aspose durch eine Open‑Source‑Alternative wie Tesseract zu ersetzen, um die Genauigkeit zu vergleichen, experimentieren Sie mit PDF‑Eingaben oder integrieren Sie den OCR‑Schritt in eine Flask‑API für die sofortige Bildverarbeitung. Der Himmel ist das Limit, wenn Sie die Grundlagen von **ocr image to text python** beherrschen.

Haben Sie Fragen zum Umgang mit schwierigen Schriftarten, zur Leistungsoptimierung oder zur Lizenzierung? Hinterlassen Sie unten einen Kommentar, und viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Text aus Bild mit Aspose OCR extrahieren – Schritt‑für‑Schritt‑Anleitung](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Text aus Bild extrahieren – OCR‑Optimierung mit Aspose.OCR für .NET](/ocr/english/net/ocr-optimization/)
- [Bildtext in C# mit Sprachauswahl mittels Aspose.OCR extrahieren](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}