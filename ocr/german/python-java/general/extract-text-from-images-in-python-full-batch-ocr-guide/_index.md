---
category: general
date: 2026-06-19
description: Extrahiere Text aus Bildern in Python mit einer einfachen OCR‑Engine.
  Lerne, wie man gescannte Bilder in Text umwandelt, Text aus Fotos erkennt und Bilddateien
  in Python effizient auflistet.
draft: false
keywords:
- extract text from images
- convert scanned images to text
- recognize text from pictures
- list image files python
language: de
og_description: Extrahiere Text aus Bildern in Python mit einer leichten OCR-Engine.
  Dieser Leitfaden zeigt dir, wie du gescannte Bilder in Text umwandelst, Text aus
  Bildern erkennst und Bilddateien in Python auflistest – in wenigen Schritten.
og_title: Text aus Bildern in Python extrahieren – Vollständiger Batch‑OCR‑Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Extract text from images in Python with a simple OCR engine. Learn
    how to convert scanned images to text, recognize text from pictures, and list
    image files python efficiently.
  headline: Extract Text from Images in Python – Full Batch OCR Guide
  type: TechArticle
tags:
- Python
- OCR
- Image Processing
title: Text aus Bildern in Python extrahieren – Vollständiger Batch‑OCR‑Leitfaden
url: /de/python-java/general/extract-text-from-images-in-python-full-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bildern in Python extrahieren – Vollständiger Batch‑OCR‑Leitfaden

Haben Sie schon einmal **Text aus Bildern extrahieren** müssen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein – Entwickler stehen ständig vor der Herausforderung, gescannte PDFs, fotografierte Quittungen oder Screenshots in durchsuchbaren Text zu verwandeln. In diesem Tutorial gehen wir Schritt für Schritt durch ein komplettes, sofort ausführbares Beispiel, das zeigt, wie man **gescannte Bilder in Text umwandelt**, Text aus Fotos erkennt und sogar **list image files python**‑artig auflistet. Am Ende haben Sie ein wiederverwendbares Skript, das einen ganzen Ordner in einem Durchgang verarbeitet.

Wir behandeln alles, was Sie benötigen: erforderliche Bibliotheken, warum jeder Schritt wichtig ist, Edge‑Case‑Handling und ein wenig Fehlersuche. Keine Notwendigkeit, externe Dokumentationen zu durchforsten; der Code unten ist eigenständig, und die Erklärungen beantworten das „Wie“ *und* das „Warum“. Öffnen Sie Ihre Lieblings‑IDE und legen wir los.

---

## Was Sie bauen werden

- Einen OCR‑Engine initialisieren (wir verwenden das `ocr`‑Paket zur Veranschaulichung).
- Ein Verzeichnis scannen und **list image files python**‑artig auflisten, wobei PNG, JPG und TIFF gefiltert werden.
- Einen **Batch‑OCR**‑Durchlauf für alle gefundenen Bilder ausführen.
- Den extrahierten Text für jede Datei ausgeben, klar gekennzeichnet.

> **Pro‑Tipp:** Wenn Sie die `ocr`‑Bibliothek nicht installiert haben, können Sie sie mit ein paar kleinen Änderungen durch `pytesseract` ersetzen – die Kernlogik bleibt gleich.

---

## Voraussetzungen

- Python 3.8+ (das Skript nutzt f‑Strings und Type Hints).
- Eine OCR‑Bibliothek, die ein `OcrEngine` mit `recognize_batch` bereitstellt. Für diesen Leitfaden gehen wir von einem fiktiven `ocr`‑Paket aus, aber das Muster funktioniert mit echten Bibliotheken.
- Ein Ordner, der die Bilddateien enthält, die Sie verarbeiten möchten (`.png`, `.jpg`, `.tif`).

---

## Schritt 1 – Installieren & Importieren der benötigten Module

Stellen Sie zunächst sicher, dass das OCR‑Paket verfügbar ist. Wenn Sie eine reale Bibliothek wie `pytesseract` verwenden, passen Sie den Import entsprechend an.

```python
# Install the fictional OCR package (skip if using pytesseract)
# pip install ocr-package

import os
import ocr  # <-- replace with your actual OCR library
from typing import List
```

> **Warum das wichtig ist:** Der Import von `os` liefert plattformübergreifende Pfad‑Handling‑Funktionen, während `typing.List` IDE‑Autocomplete und Zukunftssicherheit unterstützt.

---

## Schritt 2 – **Extract Text from Images**: OCR‑Engine initialisieren

Die Erstellung der Engine ist der erste Schritt für jede OCR‑Arbeit. Wir setzen die Sprache auf Auto‑Detect, damit die Engine gemischte Sprachdokumente verarbeiten kann.

```python
def create_engine() -> ocr.OcrEngine:
    """
    Initializes the OCR engine with automatic language detection.
    Returns:
        An instance of ocr.OcrEngine ready for batch processing.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto  # Auto‑detect language
    return engine
```

> **Erklärung:** Durch das Kapseln der Engine‑Erstellung in einer Funktion bleibt der Code modular. Wenn Sie später DPI oder OCR‑Modus anpassen müssen, ändern Sie nur diese eine Stelle.

---

## Schritt 3 – **List Image Files Python**: Dateien aus einem Verzeichnis sammeln

Jetzt müssen wir jedes Bild finden, das wir verarbeiten wollen. Die List‑Comprehension unten spiegelt ein übliches „list image files python“‑Muster wider.

```python
def get_image_files(input_dir: str) -> List[str]:
    """
    Scans `input_dir` and returns a list of absolute paths
    for files ending with .png, .jpg, or .tif (case‑insensitive).
    """
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]
```

> **Edge‑Case‑Handling:** Die Funktion ignoriert Unterordner (Sie können später Rekursion hinzufügen) und filtert versteckte Dateien automatisch heraus, weil diese typischerweise nicht mit den unterstützten Erweiterungen enden.

---

## Schritt 4 – **Convert Scanned Images to Text**: Batch‑OCR ausführen

Die meisten OCR‑Bibliotheken bieten eine Batch‑Methode, die weitaus schneller ist als die Verarbeitung einzelner Bilder. So rufen wir sie auf.

```python
def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    """
    Sends a list of image file paths to the OCR engine for batch recognition.
    Returns a list of OcrResult objects, preserving order.
    """
    # The fictional `recognize_batch` returns a list of results matching input order
    return engine.recognize_batch(image_paths)
```

> **Warum Batch?** Das gleichzeitige Senden aller Bilder reduziert Overhead (z. B. wiederholtes Laden des OCR‑Modells) und führt häufig zu besserer CPU/GPU‑Auslastung.

---

## Schritt 5 – **Recognize Text from Pictures**: Ergebnisse anzeigen

Abschließend iterieren wir über die gepaarten Dateinamen und OCR‑Ergebnisse und geben für jedes Bild eine klare Überschrift aus.

```python
def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    """
    Prints the extracted text for each image, prefixed with the file name.
    """
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        # Some OCR engines store the plain text in a `.text` attribute
        print(result.text.strip())
        print()  # Blank line for readability
```

> **Tipp:** `strip()` entfernt führende bzw. nachfolgende Leerzeichen, die OCR häufig hinzufügt.

---

## Vollständiges Skript – Alles zusammenführen

Unten finden Sie das komplette, ausführbare Programm. Speichern Sie es als `batch_ocr.py` und führen Sie `python batch_ocr.py <your_folder>` aus.

```python
#!/usr/bin/env python3
"""
Batch OCR script – extracts text from images in a given folder.
Usage: python batch_ocr.py /path/to/images
"""

import sys
import os
import ocr  # Replace with your OCR library if different
from typing import List

def create_engine() -> ocr.OcrEngine:
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto
    return engine

def get_image_files(input_dir: str) -> List[str]:
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]

def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    return engine.recognize_batch(image_paths)

def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        print(result.text.strip())
        print()

def main() -> None:
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <input_directory>")
        sys.exit(1)

    input_dir = sys.argv[1]

    if not os.path.isdir(input_dir):
        print(f"Error: '{input_dir}' is not a valid directory.")
        sys.exit(1)

    engine = create_engine()
    image_files = get_image_files(input_dir)

    if not image_files:
        print("No supported image files found in the directory.")
        sys.exit(0)

    ocr_results = run_batch_ocr(engine, image_files)
    display_results(image_files, ocr_results)

if __name__ == "__main__":
    main()
```

### Erwartete Ausgabe

Angenommen, der Ordner enthält `invoice1.png` und `receipt.jpg`, dann könnte die Ausgabe etwa so aussehen:

```
--- invoice1.png ---
Invoice #12345
Date: 2024‑04‑01
Total: $256.78

--- receipt.jpg ---
Store: Coffee Corner
Item: Latte
Price: $4.50
```

Jeder Block ist klar gekennzeichnet, sodass nachgelagerte Verarbeitung (z. B. Speichern in einer Datenbank) unkompliziert ist.

---

## Häufige Stolperfallen behandeln

| Problem | Warum es passiert | Schnelllösung |
|---------|-------------------|---------------|
| **Kein Text erscheint** | OCR‑Sprache nicht erkannt oder Bild hat zu geringen Kontrast. | Sprache erzwingen (`engine.language = ocr.Language.English`) oder Bilder vorverarbeiten (Kontrast erhöhen). |
| **Speicherfehler bei großen Batches** | Die Engine versucht, alle Bilder gleichzeitig zu laden. | `image_files` in Stücke aufteilen (`batch_size = 20`) und `recognize_batch` wiederholt aufrufen. |
| **Nicht unterstütztes Dateiformat** | Sie haben eine `.gif`‑ oder `.bmp`‑Datei hinzugefügt. | `supported_exts`‑Tuple erweitern oder Bilder vorher in PNG/JPG konvertieren. |
| **Unicode‑Verzerrung** | OCR gibt Bytes statt Strings zurück. | Sicherstellen, dass die OCR‑Bibliothek Unicode ausgibt (`result.text.decode('utf‑8')` falls nötig). |

---

## Workflow erweitern

Jetzt, wo Sie **Text aus Bildern extrahieren** können, denken Sie an folgende nächste Schritte:

- **Export nach CSV** – Schreiben Sie jeden Dateinamen und den extrahierten Text in eine Tabelle für Analysen.
- **Parallelverarbeitung** – Nutzen Sie `concurrent.futures.ThreadPoolExecutor`, um mehrere Batches gleichzeitig zu bearbeiten.
- **Integration mit Cloud‑OCR** – Ersetzen Sie die lokale Engine durch Google Vision oder Azure OCR für höhere Genauigkeit bei komplexen Layouts.
- **Bildvorverarbeitung hinzufügen** – Bibliotheken wie Pillow oder OpenCV können Bilder entzerren, entrauschen oder schwellen, bevor sie OCR unterzogen werden, was die Ergebnisse verbessert.

All diese Ideen bauen auf denselben Kernfunktionen auf, die wir erstellt haben, sodass Sie nicht von Grund auf neu beginnen müssen.

---

## Fazit

Wir haben gerade eine komplette Lösung zum **Extrahieren von Text aus Bildern** in Python durchgegangen, von **list image files python** über **recognize text from pictures** bis hin zu **convert scanned images to text** in einem sauberen Batch‑Verfahren. Das Skript ist bewusst einfach gehalten, aber flexibel genug, um als Grundlage für größere Projekte zu dienen – sei es beim Digitalisieren von Quittungen, beim Aufbau eines durchsuchbaren Archivs oder beim Betreiben einer Daten‑Extraktions‑Pipeline.

Probieren Sie es aus, passen Sie die Vorverarbeitungsschritte an und beobachten Sie, wie Ihre OCR‑Genauigkeit steigt. Wenn Sie auf Probleme stoßen, werfen Sie einen Blick zurück in die Tabelle „Häufige Stolperfallen“; die meisten Probleme lassen sich mit einer kleinen Konfigurationsänderung beheben.

Bereit für die nächste Herausforderung? Versuchen Sie, einen PDF‑zu‑Bild‑Konvertierungsschritt mit `pdf2image` hinzuzufügen und füttern Sie diese Bilder direkt in dieselbe Pipeline. Der Himmel ist die Grenze, wenn Sie OCR mit dem reichen Python‑Ökosystem kombinieren.

Viel Spaß beim Coden und möge Ihr Text stets lesbar sein!


## Was Sie als Nächstes lernen sollten


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}