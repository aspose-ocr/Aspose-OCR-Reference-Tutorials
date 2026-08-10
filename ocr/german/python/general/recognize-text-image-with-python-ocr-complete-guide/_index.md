---
category: general
date: 2026-06-28
description: Lernen Sie, wie Sie Textbilder mit Python OCR erkennen, Text‑PNG‑Dateien
  extrahieren und den erkannten Text mit robuster Fehlerbehandlung ausgeben.
draft: false
keywords:
- recognize text image
- extract text png
- load image ocr
- process image ocr
- print recognized text
language: de
og_description: Schritt‑für‑Schritt‑Anleitung zur Texterkennung in Bildern mit Python,
  zum Extrahieren von Text‑PNG und zum sicheren Ausgeben des erkannten Textes.
og_title: Texterkennung von Bildern mit Python OCR – Komplettanleitung
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text image using Python OCR, extract text png
    files, and print recognized text with robust error handling.
  headline: recognize text image with Python OCR – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Texterkennung in Bildern mit Python OCR – Komplettanleitung
url: /de/python/general/recognize-text-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Textbild mit Python OCR erkennen – Vollständige Anleitung

Haben Sie sich schon einmal gefragt, wie man **Text aus einem Bild** in einem Python‑Skript erkennt, ohne ein schwergewichtiges Framework zu verwenden? Sie sind nicht allein. Viele Entwickler benötigen eine schnelle Möglichkeit, *Bild‑OCR* für einen Screenshot, eine gescannte Quittung oder ein einfaches PNG zu laden und den Text zurückzubekommen.  

In diesem Tutorial verbinden wir eine minimale OCR‑Engine, hängen einen benutzerdefinierten Logger an, **laden Bild‑OCR**, führen die **process image OCR** aus und schließlich **print recognized text**. Am Ende haben Sie ein eigenständiges Skript, das auf Abruf **extract text png** Dateien erzeugen kann.

## Was Sie am Ende wissen werden

- Ein voll funktionsfähiger Python‑Snippet, der eine OCR‑Engine erstellt, jeden Schritt protokolliert und Fehler elegant behandelt.  
- Klare Erklärungen, *warum* jede Zeile wichtig ist – damit Sie den Code leicht auf Tesseract, EasyOCR oder ein anderes Backend anpassen können.  
- Tipps zu häufigen Stolperfallen (fehlende Fonts, beschädigte PNGs) und wie man sie debuggt.  

### Voraussetzungen

- Python 3.8+ installiert  
- Eine OCR‑Bibliothek, die eine `OcrEngine`‑Klasse bereitstellt (das Beispiel nutzt eine fiktive, aber typische API; ersetzen Sie sie durch `pytesseract`, `easyocr` usw.).  
- Ein PNG‑Bild, das Sie analysieren möchten, gespeichert als `input.png` in einem Ordner Ihrer Wahl.  

> **Pro‑Tipp:** Wenn Sie `pytesseract` verwenden, installieren Sie zuerst das System‑Tesseract‑Binary (`sudo apt install tesseract-ocr` unter Linux) und dann `pip install pytesseract pillow`.

---

## ## Textbild erkennen: Logger einrichten

Ein guter Logger ist der unbeachtete Held jeder OCR‑Pipeline. Er sagt Ihnen *wann* die Engine gestartet wurde, *welche* Datei sie geöffnet hat und *warum* sie eventuell fehlgeschlagen ist.

```python
# Step 1: Define a simple logger for the OCR engine
def my_logger(level, message):
    """
    level: str – e.g., "INFO", "WARN", "ERROR"
    message: str – human‑readable description of the event
    """
    print(f"[{level}] {message}")
```

*Warum das wichtig ist:*  
Der Logger trennt die Diagnoseausgabe vom OCR‑Kern, sodass Sie Logs leicht in eine Datei, einen Monitoring‑Service oder später sogar in eine UI umleiten können.  

---

## ## Bild‑OCR laden: Engine mit einem PNG füttern

Bevor die Engine **process image OCR** ausführen kann, benötigt sie ein korrektes Bildobjekt. Die meisten Bibliotheken akzeptieren eine Pillow‑`Image`‑Instanz.

```python
from PIL import Image

# Step 2: Create the OCR engine and attach the logger
ocr_engine = OcrEngine(logging=my_logger)

# Step 3: Load the image to be processed
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Image.from_file(image_path))
my_logger("INFO", f"Loaded image from {image_path}")
```

*Wichtige Punkte:*  

- **load image ocr** – `Image.from_file` versteckt die Details der PNG‑Dekodierung.  
- Halten Sie den Pfad konfigurierbar; Hard‑Coding macht das Skript spröde.  
- Der Logger‑Aufruf bestätigt, dass das Bild erfolgreich gelesen wurde – nützlich, wenn die Datei fehlt oder beschädigt ist.

---

## ## Process Image OCR: Text erkennen

Jetzt beginnt die eigentliche Arbeit. Die Engine scannt das Bitmap, wendet ihre neuronalen Netze oder Heuristiken an und gibt einen Unicode‑String zurück.

```python
# Step 4: Recognize text from the image
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:
    # Step 5: Handle OCR errors gracefully
    my_logger("ERROR", f"OCR failed with code {e.code}: {e.message}")
    extracted_text = None
```

*Warum wir es in `try/except` einbetten:*  
OCR kann bei niedrig aufgelösten PNGs, nicht unterstützten Farbräumen oder fehlenden Sprachdaten abstürzen. Das Abfangen von `OcrException` ermöglicht es, **print recognized text** nur dann auszugeben, wenn tatsächlich Text vorhanden ist, und verhindert kryptische Stack‑Traces für Endnutzer.

---

## ## Print Recognized Text & Extract Text PNG

Wenn die Erkennung erfolgreich war, zeigen wir das Ergebnis an und schreiben optional eine `.txt`‑Datei, die den ursprünglichen PNG‑Namen spiegelt.

```python
if extracted_text:
    # Step 6: Print the recognized text
    print("Recognized text:", extracted_text)
    my_logger("INFO", "Printed recognized text to console")

    # Optional: Save extracted text for later use
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
```

*Was Sie erhalten:*  

- **print recognized text** – sofortiges visuelles Feedback im Terminal.  
- Eine begleitende `.txt`‑Datei, die effektiv **extract text png** für nachgelagerte Verarbeitung (Suchindizierung, Dateneingabe usw.) bereitstellt.

---

## ## Häufige Sonderfälle & Lösungen

| Situation | Symptom | Lösung |
|-----------|---------|--------|
| PNG ist nur Graustufen | OCR liefert leeren String | Vor dem Füttern der Engine in RGB konvertieren (`Image.convert("RGB")`). |
| Sprache nicht unterstützt | `OcrException` mit Code `LANG_NOT_FOUND` | Sprachpaket installieren (z. B. `tesseract‑lang‑fra` für Französisch) und `ocr_engine.language = "fra"` setzen. |
| Sehr großes Bild ( > 5 MB ) | Langsame Erkennung oder Speicherfehler | Vor `set_image` mit `image.thumbnail((2000, 2000))` verkleinern. |
| Unerwartete Zeichen | Verzerrte Ausgabe | Sicherstellen, dass die Datei wirklich PNG ist; manche Dateien tarnen sich als PNG, sind aber JPEGs. Mit `Image.verify()` validieren. |

---

## ## Vollständiges Beispiel (Ein‑Klick‑Bereit)

```python
# -*- coding: utf-8 -*-
"""
Complete script to recognize text image using a generic OCR engine.
Replace OcrEngine, OcrException with the concrete classes from your library.
"""

from PIL import Image

# ----------------------------------------------------------------------
# 1️⃣  Logger definition
# ----------------------------------------------------------------------
def my_logger(level: str, message: str) -> None:
    """Simple console logger."""
    print(f"[{level}] {message}")

# ----------------------------------------------------------------------
# 2️⃣  Engine creation & image loading
# ----------------------------------------------------------------------
ocr_engine = OcrEngine(logging=my_logger)   # <- adapt to your library

image_path = "YOUR_DIRECTORY/input.png"
try:
    img = Image.open(image_path)
    img.verify()                     # sanity check the PNG
    img = Image.open(image_path)     # reopen after verify
    ocr_engine.set_image(img)
    my_logger("INFO", f"Loaded image from {image_path}")
except Exception as load_err:
    my_logger("ERROR", f"Failed to load image: {load_err}")
    raise SystemExit(1)

# ----------------------------------------------------------------------
# 3️⃣  Text recognition
# ----------------------------------------------------------------------
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:            # replace with actual exception class
    my_logger("ERROR", f"OCR failed ({e.code}): {e.message}")
    extracted_text = None

# ----------------------------------------------------------------------
# 4️⃣  Output handling
# ----------------------------------------------------------------------
if extracted_text:
    print("Recognized text:", extracted_text)          # ✅ print recognized text
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
else:
    my_logger("WARN", "No text extracted; check image quality.")
```

**Erwartete Konsolenausgabe (Happy Path):**

```
[INFO] Loaded image from YOUR_DIRECTORY/input.png
[INFO] OCR succeeded
Recognized text: Invoice #12345
Total Amount: $1,250.00
Date: 2026‑06‑01
[INFO] Saved extracted text to YOUR_DIRECTORY/input.txt
```

Falls etwas schiefgeht, sehen Sie eine klare `[ERROR]`‑Zeile mit dem Grund, dank des benutzerdefinierten Loggers.

---

## ## Nächste Schritte & verwandte Themen

- **extract text png** aus Stapeln: Skript in einer `for`‑Schleife verpacken, die einen Verzeichnisbaum durchläuft.  
- **process image ocr** mit Vorverarbeitung (Deskew, Kontrastverstärkung) mittels OpenCV, bevor die Engine gefüttert wird.  
- Auf einen Cloud‑OCR‑Dienst umsteigen (Google Vision, Azure Read), indem Sie die `OcrEngine`‑Implementierung austauschen – Ihr umgebender Code bleibt gleich.  
- Lernen Sie, wie Sie **print recognized text** in PDFs mit `reportlab` für automatisierte Berichtserstellung einbinden.  

---

## Fazit

Wir haben einen kompakten, produktionsreifen Weg gezeigt, **text image** in Python zu erkennen – vom Laden des PNGs bis zum **print recognized text** und dem Speichern des Ergebnisses. Durch das Einbinden eines kleinen Loggers, das Handling von Ausnahmen und das optionale Persistieren der Ausgabe ist das Skript sowohl für schnelle Experimente als auch für die Integration in größere Pipelines bereit.

Probieren Sie es mit Ihren eigenen Screenshots, spielen Sie mit Bildvorverarbeitung, und Sie werden bald Text aus jedem PNG extrahieren, das Sie ihm vorwerfen. Fragen? Hinterlassen Sie einen Kommentar – happy OCRing!  

![Beispiel für Textbild-Erkennung](placeholder.png)


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [Text aus Bild mit Aspose OCR extrahieren – Schritt‑für‑Schritt‑Anleitung](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Wie man Bild‑Text‑Extraktion aus einem Stream mit Aspose OCR durchführt](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Bild zu Text konvertieren – OCR auf Bild von URL ausführen](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}