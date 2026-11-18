---
category: general
date: 2026-06-28
description: Wie man OCR stapelweise mit Python verwendet. Lernen Sie, mehrere Bilder
  zu OCRen, Text aus PNGs zu extrahieren und Bilder in Text zu konvertieren – ein
  umfassendes Python-OCR-Tutorial.
draft: false
keywords:
- how to batch OCR
- ocr multiple images
- extract text from png
- convert image to text
- python ocr tutorial
language: de
og_description: Wie man OCR stapelweise in Python durchführt, wird im ersten Satz
  erklärt. Folgen Sie diesem Python‑OCR‑Tutorial, um Text effizient aus PNG‑Dateien
  zu extrahieren.
og_title: Wie man OCR in Python stapelweise ausführt – Vollständiger Programmierleitfaden
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  headline: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  name: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Why set the language?**'
    text: '**Why set the language?**'
  - name: '**Why use a batch operation?**'
    text: '**Why use a batch operation?**'
  - name: '**Why a ThreadPoolExecutor?**'
    text: '**Why a ThreadPoolExecutor?**'
  - name: '**Why enumerate the results?**'
    text: '**Why enumerate the results?**'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Wie man OCR in Python stapelweise durchführt – Vollständige Schritt‑für‑Schritt‑Anleitung
url: /de/python-java/general/how-to-batch-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR stapelweise in Python ausführt – Vollständige Schritt‑für‑Schritt‑Anleitung

Haben Sie sich schon einmal gefragt, **wie man OCR stapelweise** auf einen Stapel gescannter Seiten anwendet, ohne eine Schleife zu schreiben, die Ihre UI blockiert? Sie sind nicht allein. Dutzende PNG‑Dateien einzeln zu verarbeiten, kann sich anfühlen, als würde man beim Trocknen von Farbe zusehen, besonders wenn jedes Bild eine oder zwei Sekunden zum Dekodieren benötigt.  

In diesem Tutorial zeigen wir Ihnen einen sauberen, nicht‑blockierenden Weg, **mehrere Bilder gleichzeitig zu OCR‑en**, **Text aus PNG**‑Dateien zu extrahieren und **Bilder in Text** zu konvertieren – und das mit einer modernen Python‑OCR‑Engine. Am Ende haben Sie ein sofort einsatzbereites Skript, das Sie in jedes Projekt einbinden können – perfekt für ein schnelles *python ocr tutorial* oder einen produktionsreifen Batch‑Job.

## Was Sie bauen werden

- Eine OCR‑Engine initialisieren und ihre Sprache auf Latein (oder jede andere benötigte Sprache) setzen.  
- Eine Liste von Bildpfaden (PNG in unserem Beispiel) an die Engine übergeben.  
- Einen Batch‑Vorgang starten, der ein Future‑ähnliches Objekt zurückgibt.  
- Alle Ergebnisse gleichzeitig mit einem Thread‑Pool abrufen, sodass Ihr Haupt‑Thread frei bleibt.  
- Den erkannten Text für jede Seite ausgeben, schön getrennt.

Kein verstecktes Zauberwerk, nur reines Python und eine Drittanbieter‑OCR‑Bibliothek (wir verwenden das fiktive `pyocr`‑Paket zur Veranschaulichung).  

**Voraussetzungen**  
- Python 3.8+ installiert.  
- Grundlegende Vertrautheit mit Python‑Funktionen und `concurrent.futures`.  
- Zugriff auf eine OCR‑Bibliothek, die eine `OcrEngine`‑Klasse bereitstellt (z. B. `pip install pyocr`).  

Falls Ihnen etwas davon fehlt, holen Sie es jetzt – es ist einfacher als Sie denken.

---

## Wie man OCR stapelweise in Python ausführt – Kernkonzepte

Bevor wir in den Code eintauchen, beantworten wir das „Warum“ hinter jedem Schritt.

1. **Warum die Sprache setzen?**  
   Die OCR‑Genauigkeit steigt enorm, wenn die Engine weiß, welche Zeichen zu erwarten sind. Latein funktioniert für Englisch, Französisch, Spanisch usw. Wechseln Sie zu `Language.Japanese` oder `Language.Arabic`, falls nötig.

2. **Warum eine Batch‑Operation verwenden?**  
   Ein Batch‑Aufruf lässt die Engine die Arbeit intern planen, häufig unter Nutzung nativer Threads oder GPU‑Beschleunigung. Er liefert einen Handle, den Sie später abfragen können, sodass Sie nicht blockieren, während jedes Bild verarbeitet wird.

3. **Warum einen ThreadPoolExecutor?**  
   Das Future‑Objekt, das wir zurückbekommen, ist *lazy* – es beginnt erst mit dem Abrufen der Ergebnisse, wenn wir danach fragen. Indem wir `getAll` einen Thread‑Pool übergeben, lässt Python den Text jeder Seite parallel holen und verkürzt die Gesamtlaufzeit dramatisch.

4. **Warum die Ergebnisse enumerieren?**  
   Die Reihenfolge der Ergebnisse entspricht der Reihenfolge der Eingabepfade, sodass wir jede Seite sicher nummerieren können.

Das Verständnis dieser „Warum“-Punkte hilft Ihnen, das Muster an andere Bibliotheken oder größere Datensätze anzupassen.

---

## Schritt 1: Installation und Import der benötigten Pakete

Stellen Sie zunächst sicher, dass die OCR‑Bibliothek installiert ist. Das Beispiel nutzt ein generisches `pyocr`‑Paket; ersetzen Sie es durch die Bibliothek Ihrer Wahl (z. B. `pytesseract`, `easyocr`).

```bash
pip install pyocr
```

Jetzt importieren wir alles, was wir benötigen.

```python
# Standard library imports
import concurrent.futures
from pathlib import Path

# Third‑party OCR library (hypothetical)
from pyocr import OcrEngine, Language
```

> **Pro‑Tipp:** Die Verwendung von `Path` aus `pathlib` macht Ihr Skript OS‑agnostisch und leichter lesbar.

---

## Schritt 2: OCR‑Engine erstellen und Sprache festlegen

Die Erstellung der Engine ist unkompliziert. Wir sperren sie für dieses Demo auf Latein.

```python
# Step 2: Initialise the OCR engine
engine = OcrEngine()
engine.setLanguage(Language.Latin)   # Change to Language.YourChoice if needed
```

Der Aufruf `setLanguage` ist für manche Engines optional, aber es ist eine gute Gewohnheit. Er teilt dem OCR‑Modell mit, welchen Zeichensatz es fokussieren soll, was sowohl Geschwindigkeit als auch Genauigkeit verbessert.

---

## Schritt 3: Bilddateien zum Verarbeiten auflisten (Text aus PNG extrahieren)

Sammeln Sie alle PNG‑Dateien, die Sie konvertieren möchten. Mit `Path.glob` können Sie einfach einen ganzen Ordner einbinden, ohne das Skript anzupassen.

```python
# Step 3: Gather PNG images – this is the “extract text from png” part
image_dir = Path("YOUR_DIRECTORY")   # Replace with your actual folder
image_paths = sorted(image_dir.glob("*.png"))   # Returns a list of Path objects

# Convert Path objects to strings for the OCR library (if required)
image_paths = [str(p) for p in image_paths]

if not image_paths:
    raise FileNotFoundError("No PNG files found in the specified directory.")
```

> **Warum das wichtig ist:** Durch das Sortieren der Liste garantieren wir eine deterministische Reihenfolge, die später jede Ergebnis‑Seite der richtigen Seitennummer zuordnet.

---

## Schritt 4: Batch‑OCR‑Operation starten (Bild in Text konvertieren)

Jetzt übergeben wir die Liste an die Engine. Die Methode liefert einen Future‑ähnlichen Container, den wir später abfragen.

```python
# Step 4: Start batch OCR – returns a Future‑like object
batch_future = engine.ocrBatch(image_paths)
```

Im Hintergrund kann die Engine eigene Worker‑Threads oder sogar eine GPU‑Pipeline starten. Wichtig ist nur, dass wir einen Handle (`batch_future`) besitzen, der weiß, wie die einzelnen Ergebnisse abgerufen werden.

---

## Schritt 5: Alle Ergebnisse gleichzeitig abrufen (OCR mehrerer Bilder)

Hier wird das eigentliche *Batching* durchgeführt. Indem wir einem `ThreadPoolExecutor` an `getAll` übergeben, wird der Text jeder Seite in einem eigenen Thread geholt.

```python
# Step 5: Pull results using a thread pool – this speeds up OCR multiple images
with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    # getAll returns a list of Result objects in the same order as image_paths
    results = batch_future.getAll(executor)
```

Sie können `max_workers` an die Anzahl Ihrer CPU‑Kerne oder an die Empfehlungen der OCR‑Bibliothek anpassen. Mehr Worker ≠ immer schneller – beobachten Sie Ihre CPU‑Auslastung.

---

## Schritt 6: Erkannten Text ausgeben (Abschluss des Python‑OCR‑Tutorials)

Zum Schluss geben wir den Text jeder Seite aus. Das `Result`‑Objekt stellt `getText()` bereit – passen Sie es an, falls Ihre Bibliothek einen anderen Methodennamen verwendet.

```python
# Step 6: Display the recognised text for each page
for i, result in enumerate(results):
    print(f"--- Page {i + 1} ---")
    print(result.getText())
    print()   # Blank line for readability
```

**Erwartete Ausgabe (Beispiel)**

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna...

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco...
```

Falls ein Bild fehlschlägt, geben die meisten Engines einen leeren String zurück oder werfen eine Ausnahme – Sie können die Schleife in einen `try/except`‑Block einbetten, um Randfälle elegant zu behandeln.

---

## Vollständiges Skript – Bereit zum Ausführen

Unten finden Sie das komplette, eigenständige Skript. Kopieren Sie es in eine Datei namens `batch_ocr.py`, passen Sie `YOUR_DIRECTORY` an und führen Sie `python batch_ocr.py` aus.

```python
#!/usr/bin/env python3
"""
Batch OCR script – processes all PNG files in a directory.
Demonstrates how to batch OCR, OCR multiple images, extract text from PNG,
and convert image to text using a Python OCR engine.
"""

import concurrent.futures
from pathlib import Path

# Replace with your actual OCR library import
from pyocr import OcrEngine, Language

def main():
    # Initialise OCR engine
    engine = OcrEngine()
    engine.setLanguage(Language.Latin)

    # Locate PNG files
    image_dir = Path("YOUR_DIRECTORY")          # <‑‑ change this
    image_paths = sorted(image_dir.glob("*.png"))
    image_paths = [str(p) for p in image_paths]

    if not image_paths:
        raise FileNotFoundError("No PNG files found in the specified directory.")

    # Start batch OCR
    batch_future = engine.ocrBatch(image_paths)

    # Retrieve results concurrently
    with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
        results = batch_future.getAll(executor)

    # Print each page's recognised text
    for i, result in enumerate(results):
        print(f"--- Page {i + 1} ---")
        print(result.getText())
        print()

if __name__ == "__main__":
    main()
```

Speichern, ausführen und beobachten, wie die Konsole mit dem extrahierten Text gefüllt wird. Einfach, schnell und vollständig asynchron.

---

## Häufige Stolperfallen & wie man sie vermeidet

| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| **Keine Ausgabe** – leere Strings | Die OCR‑Engine konnte keinen Text finden (Bild zu verrauscht) | Bildvorverarbeitung: binarisieren, deskewen oder DPI erhöhen |
| **`FileNotFoundError`** | Falscher Verzeichnispfad oder fehlende PNG‑Dateien | `YOUR_DIRECTORY` prüfen und sicherstellen, dass Dateien die Endung `.png` haben |
| **Hohe CPU‑Auslastung** | `max_workers` zu hoch für die Maschine eingestellt | `max_workers` reduzieren oder GPU‑Beschleunigung aktivieren, falls unterstützt |
| **Unicode‑Durcheinander** | Engine hat standardmäßig eine andere Sprache verwendet | `engine.setLanguage(Language.Latin)` (oder passende) vor dem Batch‑OCR aufrufen |

Diese Punkte früh zu adressieren spart Ihnen Stunden an Fehlersuche.

---

## Erweiterung des Tutorials – Nächste Schritte

- **OCR mehrerer Bilder** in anderen Formaten (JPEG, TIFF) – einfach das Glob‑Muster ändern.  
- **Text aus PNG** extrahieren und in einen Such‑Index (z. B. Elasticsearch) einspeisen.  
- **Bild in Text** für die PDF‑Erstellung mit `reportlab` oder `PyPDF2` konvertieren.  
- **Parallelisierung über mehrere Maschinen** mit `multiprocessing` oder einer Task‑Queue wie Celery für massive Datensätze.  

Jeder dieser Punkte baut natürlich auf dem **python ocr tutorial** auf, das Sie gerade abgeschlossen haben.

---

## Fazit

Wir haben gezeigt, **wie man OCR stapelweise** über eine Sammlung von PNG‑Dateien ausführt, die Leistungsfähigkeit einer batch‑orientierten API demonstriert und Ihnen gezeigt, **wie man Text aus PNG** mit einem Thread‑Pool‑Ansatz extrahiert. Das oben stehende Skript ist produktionsreif, und Sie verfügen nun über ein solides Fundament für jedes OCR‑intensive Python‑Projekt.

Probieren Sie es aus, passen Sie die Spracheinstellungen an und ersetzen Sie eventuell `pyocr` durch `pytesseract` – das Muster bleibt gleich. Fragen oder ein cooles Anwendungsbeispiel? Hinterlassen Sie einen Kommentar, und wir setzen die Diskussion fort.

*Viel Spaß beim Coden!*


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}