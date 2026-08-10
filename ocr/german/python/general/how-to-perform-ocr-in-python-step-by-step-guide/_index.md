---
category: general
date: 2026-01-12
description: Wie man OCR durchführt und Bilder schnell in Text umwandelt. Lernen Sie,
  Sonderzeichen zu erkennen, Text aus Bildern zu extrahieren und Bilder für OCR zu
  laden – mit einem vollständigen Python‑Beispiel.
draft: false
keywords:
- how to perform OCR
- convert image to text
- recognize special characters
- extract text from image
- load image for OCR
language: de
og_description: Wie man OCR in Python durchführt, Bilder in Text umwandelt und Sonderzeichen
  erkennt. Folgen Sie dieser praxisorientierten Anleitung zum Extrahieren von Text
  aus Bildern.
og_title: Wie man OCR in Python durchführt – vollständiges Tutorial
tags:
- OCR
- Python
- Image Processing
title: Wie man OCR in Python durchführt – Schritt‑für‑Schritt‑Anleitung
url: /de/python/general/how-to-perform-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in Python durchführt – Schritt‑für‑Schritt‑Anleitung

Hast du schon einmal **OCR** auf einem Screenshot durchführen müssen, der sowohl lateinische als auch kyrillische Zeichen enthält? Du bist nicht allein. In vielen Projekten – sei es beim Digitalisieren von Quittungen, Indexieren mehrsprachiger Dokumente oder beim Aufbau eines durchsuchbaren Archivs – **wie man OCR durchführt** wird schnell zur wichtigsten Frage.  

In diesem Tutorial gehen wir ein komplettes, ausführbares Beispiel durch, das zeigt, wie man **Bild in Text umwandelt**, **Sonderzeichen erkennt** und **Text aus Bild extrahiert** mithilfe einer einfachen Python‑Bibliothek. Am Ende hast du ein sofort einsatzbereites Skript, das ein Bild für OCR lädt, mehrsprachige Inhalte verarbeitet und das Ergebnis ausgibt.

## Was du brauchst

Bevor wir starten, stelle sicher, dass du die folgenden Voraussetzungen erfüllst:

- Python 3.8+ auf deinem Rechner installiert.  
- Das `ocr`‑Paket (oder eine kompatible OCR‑Bibliothek) installiert via `pip install ocr`.  
- Eine Bilddatei (`multilingual.png`), die sowohl lateinische als auch kyrillische Glyphen enthält.  
- Ein einfacher Text‑Editor oder eine IDE – VS Code, PyCharm oder sogar ein einfacher Notepad reichen aus.  

Falls du das `ocr`‑Paket nicht hast, kannst du es durch `pytesseract` ersetzen; die Kernkonzepte bleiben gleich.

## Schritt 1: Installieren und Importieren der OCR‑Bibliothek

Zuerst machen wir die OCR‑Engine bereit. Wir importieren die Bibliothek, erstellen eine Engine‑Instanz und konfigurieren sie für mehrsprachige Unterstützung.

```python
# Install the library (run this once in your terminal)
# pip install ocr

import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: Enable language packs for Latin and Cyrillic
engine.set_languages(['eng', 'rus'])  # 'eng' = English, 'rus' = Russian
```

**Warum das wichtig ist:**  
Das Erstellen der Engine ist die Grundlage – ohne sie kannst du später kein **Bild für OCR laden**. Das Aktivieren von Sprachpaketen stellt sicher, dass die Engine Zeichen wie „Ŀ“, „Ҕ“ und „Ǣ“ korrekt erkennt. Wenn du diesen Schritt überspringst, bekommst du ein verstümmeltes Ergebnis für nicht‑lateinische Schriften.

## Schritt 2: Laden des Bildes mit mehrsprachigem Text

Jetzt zeigen wir der Engine, welche Datei sie verarbeiten soll. Der Pfad kann absolut oder relativ sein; achte nur darauf, dass er auf ein lesbares Bild verweist.

```python
# Step 2: Load the image containing multilingual text
image_path = "YOUR_DIRECTORY/multilingual.png"  # replace with your actual path
engine.load_image(image_path)
```

> ![how to perform OCR example](/images/ocr-example.png "how to perform OCR on a multilingual image")

**Warum das wichtig ist:**  
Der Aufruf `load_image` liest die Pixeldaten in den Speicher und bereitet sie für den OCR‑Algorithmus vor. Wenn das Bild groß ist, kann die Engine es automatisch verkleinern; du kannst das später mit `engine.set_max_resolution(3000)` für hochauflösende Scans feinjustieren.

## Schritt 3: Ausführen des Erkennungsprozesses

Nachdem die Engine vorbereitet und das Bild geladen ist, können wir endlich den Textinhalt extrahieren.

```python
# Step 3: Perform OCR recognition on the loaded image
result = engine.recognize()
```

**Warum das wichtig ist:**  
`recognize()` führt das schwere neuronale Netzwerk im Hintergrund aus. Es gibt ein Objekt zurück, das den Rohtext, Konfidenzwerte und sogar Begrenzungsrahmen enthält, falls du sie für visuelles Debugging brauchst.

## Schritt 4: Ausgabe des erkannten Textes

Schauen wir, was die Engine gefunden hat. Wir geben den Text in der Konsole aus, du könntest ihn aber auch in eine Datei oder Datenbank schreiben.

```python
# Step 4: Output the recognized text, which should include characters like “Ŀ”, “Ҕ”, “Ǣ”
print("=== OCR Result ===")
print(result.text)
```

### Erwartete Ausgabe

```
=== OCR Result ===
Hello, world! Ŀ is a Latin‑extended character.
Привет, мир! Ҕ is a Cyrillic character.
Special combo: Ǣ is a ligature.
```

Wenn du etwas Ähnliches siehst, herzlichen Glückwunsch – du hast erfolgreich **Bild in Text umgewandelt** und **Sonderzeichen erkannt**.

## Umgang mit häufigen Fallstricken

Selbst bei einem einfachen Skript können ein paar Stolpersteine auftreten. Hier ein paar praktische Tipps aus meiner Erfahrung.

### 1. Fehlende Sprachpakete

Wenn du anstelle von kyrillischen Buchstaben Fragezeichen (`?`) bekommst, prüfe, ob die Sprachpakete installiert sind. Bei vielen OCR‑Engines musst du die entsprechenden `.traineddata`‑Dateien herunterladen und in den `tessdata`‑Ordner der Engine legen.

```python
# Example for pytesseract
import pytesseract
pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
# Ensure 'eng' and 'rus' data files exist in tessdata
```

### 2. Niedrige Bildqualität

Verschwommene oder kontrastarme Bilder führen zu niedrigen Konfidenzwerten. Verarbeite das Bild vorher mit OpenCV:

```python
import cv2

# Load, convert to grayscale, and apply thresholding
raw = cv2.imread(image_path)
gray = cv2.cvtColor(raw, cv2.COLOR_BGR2GRAY)
_, thresh = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)

# Save a temporary cleaned image and feed it to the OCR engine
cv2.imwrite("cleaned.png", thresh)
engine.load_image("cleaned.png")
```

### 3. Große Dateien und Speicherverbrauch

Die Verarbeitung eines 10 MB‑Fotos kann den Speicher stark beanspruchen. Verwende `engine.set_max_image_size(2000)`, um die Auflösung zu begrenzen, oder teile das Bild in Kacheln und OCR jede Kachel separat.

### 4. Erfassen von Begrenzungsrahmen

Wenn du hervorheben möchtest, wo jedes Wort erscheint (nützlich für UI‑Overlays), greife auf `result.boxes` zu:

```python
for box in result.boxes:
    print(f"Word: {box.text} – Coordinates: {box.x0},{box.y0},{box.x1},{box.y1}")
```

## Komplettes Skript – Ein‑Klick‑Ausführung

Alles zusammengeführt, hier eine einzelne Datei, die du als `python ocr_demo.py` ausführen kannst. Sie enthält Fehlerbehandlung, optionale Vorverarbeitung und Kommentare zur Klarheit.

```python
#!/usr/bin/env python3
"""
Complete OCR demo: load image, recognize multilingual text,
and print results. Works with the generic 'ocr' library.
"""

import os
import sys
import ocr

def main(image_path: str):
    # Verify the image exists
    if not os.path.isfile(image_path):
        sys.exit(f"Error: File not found – {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()
    engine.set_languages(['eng', 'rus'])          # load language packs
    engine.set_max_image_size(2500)               # limit memory usage

    # Load the image
    try:
        engine.load_image(image_path)
    except Exception as e:
        sys.exit(f"Failed to load image: {e}")

    # Perform recognition
    try:
        result = engine.recognize()
    except Exception as e:
        sys.exit(f"OCR failed: {e}")

    # Output the text
    print("\n=== OCR Result ===")
    print(result.text)

    # Optional: display confidence scores
    if hasattr(result, "confidence"):
        avg_conf = sum(result.confidence) / len(result.confidence)
        print(f"\nAverage confidence: {avg_conf:.1%}")

if __name__ == "__main__":
    # Replace with your actual image path or pass as CLI argument
    img = sys.argv[1] if len(sys.argv) > 1 else "YOUR_DIRECTORY/multilingual.png"
    main(img)
```

Ausführen mit:

```bash
python ocr_demo.py path/to/multilingual.png
```

Du solltest die gleiche Ausgabe wie zuvor sehen, was bestätigt, dass du **Text aus Bild extrahiert** hast.

## Fazit

Wir haben **wie man OCR in Python durchführt** von Anfang bis Ende behandelt: Bibliothek installieren, Bild laden, mehrsprachige Inhalte erkennen und die häufigsten Randfälle behandeln. Mit dieser Anleitung kannst du jetzt **Bild in Text umwandeln**, **Sonderzeichen erkennen** und **Text aus Bild extrahieren** in deinen eigenen Projekten – keine manuelle Transkription mehr.

Was kommt als Nächstes? Experimentiere mit:

- Mehr Sprachpaketen (z. B. `spa` für Spanisch).  
- Exportieren der Ergebnisse nach JSON für nachgelagerte Verarbeitung.  
- Integration des OCR‑Schritts in eine Flask‑API, damit andere Dienste ihn aufrufen können.  

Wenn du auf Eigenheiten stößt, ist die Community rund um die meisten OCR‑Bibliotheken aktiv – suche nach „ocr library language pack installation“ oder hinterlasse einen Kommentar unten. Viel Spaß beim Coden und beim Verwandeln von Bildern in durchsuchbaren Text!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}