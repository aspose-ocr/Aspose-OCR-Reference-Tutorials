---
category: general
date: 2026-03-28
description: Extrahieren Sie Text schnell aus PNGs mit Aspose OCR in Python. Erfahren
  Sie, wie Sie gescannte Seiten mit paralleler Bilderkennung in Python in Text umwandeln,
  um Hochleistungsergebnisse zu erzielen.
draft: false
keywords:
- extract text from png
- convert scanned pages text
- parallel image recognition python
- recognize image text python
- async OCR batch processing
- Aspose OCR Python
language: de
og_description: Extrahieren Sie Text aus PNG schnell mit Aspose OCR in Python. Dieser
  Leitfaden zeigt, wie man gescannte Seiten mit paralleler Bilderkennung in Python
  in Text umwandelt und dabei Hochgeschwindigkeits‑Ergebnisse liefert.
og_title: Text aus PNG extrahieren – Schnelles paralleles OCR mit Python
tags:
- OCR
- Python
- Image Processing
- Concurrency
title: Text aus PNG extrahieren – Schnelle parallele OCR mit Python und Aspose
url: /de/python-java/general/extract-text-from-png-fast-parallel-ocr-with-python-and-aspo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus PNG extrahieren – Schnelles paralleles OCR mit Python

Haben Sie schon einmal **Text aus PNG**‑Dateien extrahieren müssen und dabei festgestellt, dass ein‑Thread‑OCR schmerzhaft langsam ist? Sie sind nicht allein. Ob Sie einen Stapel gescannter Belege digitalisieren oder Vorlesungsfolien in durchsuchbare PDFs umwandeln – der Flaschenhals liegt meist im OCR‑Schritt selbst.  

In diesem Tutorial zeigen wir Ihnen eine komplette, sofort einsatzbereite Lösung, die **gescannte Seiten parallel** in Text umwandelt, indem sie den asynchronen Batch‑Modus von Aspose OCR zusammen mit Pythons `ThreadPoolExecutor` nutzt. Am Ende können Sie **image text python**‑artig erkennen und Dutzende von Bildern in einem Bruchteil der Zeit verarbeiten, die eine naive Schleife benötigen würde.

> **Was Sie am Ende haben**  
> * Ein voll funktionsfähiges Skript, das Text aus PNG‑Bildern gleichzeitig extrahiert.  
> * Verständnis dafür, warum der async‑Batch‑Modus die Verarbeitung beschleunigt.  
> * Tipps, wie Sie die Lösung für größere Workloads skalieren können.

## Was Sie benötigen

| Voraussetzung | Grund |
|---------------|-------|
| Python 3.9+ | Moderne Syntax und Type Hints. |
| `aspose-ocr` und `aspose-storage` Pakete | Stellen die OCR‑Engine und den Bild‑Lader bereit. |
| Ein Ordner mit PNG‑Dateien (z. B. gescannte Seiten) | Das Ausgangsmaterial, das Sie verarbeiten wollen. |
| Grundkenntnisse zu Python‑Concurrency | Hilfreich, aber nicht zwingend; wir erklären alles. |

Sie können die Aspose‑Bibliotheken installieren mit:

```bash
pip install aspose-ocr aspose-storage
```

> **Pro‑Tipp:** Halten Sie Ihre Pakete aktuell (`pip list --outdated`), um von den neuesten Performance‑Verbesserungen zu profitieren.

## Schritt 1: Initialisieren der Aspose OCR‑Engine im Async‑Batch‑Modus

Als Erstes erstellen wir eine `OcrEngine`‑Instanz und schalten sie in den **asynchronen Batch‑Modus**. Dieser Modus queued Erkennungs‑Requests intern, sodass die Engine mehrere Bilder verarbeiten kann, ohne Ihren Python‑Thread zu blockieren.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the OCR engine
ocr_engine = aocr.OcrEngine()
# Enable async batch processing – crucial for parallel speed‑up
ocr_engine.batch_mode = aocr.BatchMode.ASYNC
```

*Warum async?*  
Wenn Sie `recognize` im synchronen Modus aufrufen, blockiert der Aufruf, bis das Bild vollständig verarbeitet ist. Im async‑Modus kann die Engine bereits am nächsten Bild arbeiten, während das aktuelle noch dekodiert wird – I/O und CPU‑Arbeit überschneiden sich effektiv.

## Schritt 2: Auflisten der PNG‑Dateien, die Sie verarbeiten möchten

Hier definieren wir die Bildsammlung. In einem echten Projekt würden Sie diese Liste dynamisch erzeugen (z. B. `glob.glob("*.png")`), aber das explizite Auflisten macht das Beispiel leichter nachvollziehbar.

```python
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]
```

> **Hinweis:** Ersetzen Sie `YOUR_DIRECTORY` durch den tatsächlichen Pfad, in dem Ihre PNG‑Scans liegen. Wenn Sie Hunderte von Dateien haben, sollten Sie `os.listdir` verwenden und nach `.png` filtern.

## Schritt 3: Hilfsfunktion schreiben, die ein Bild lädt und dessen Text zurückgibt

Der Helfer kapselt den zweistufigen Prozess, eine Datei über **Aspose Storage** zu laden und sie dann an die OCR‑Engine zu übergeben. Ein kurzer Docstring macht die Funktion selbstdokumentierend – praktisch für die zukünftige Wartung.

```python
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the recognized text.
    """
    # Load the image using Aspose Storage (handles many formats)
    img = storage.Image.load(path)
    # Perform OCR; the result object contains the extracted text
    result = ocr_engine.recognize(img)
    return result.text
```

*Warum eine separate Funktion?*  
Sie hält den Thread‑Pool‑Code sauber und ermöglicht die Wiederverwendung der Logik an anderer Stelle (z. B. in einem Flask‑Endpoint). Außerdem erleichtert die Trennung von I/O das Debuggen – wenn eine bestimmte Datei fehlschlägt, sehen Sie den Dateinamen im Ausnahme‑Trace.

## Schritt 4: Parallel‑Bild‑Erkennung in Python mit einem Thread‑Pool ausführen

Jetzt bringen wir `ThreadPoolExecutor` ins Spiel. Standardmäßig starten wir vier Worker, Sie können `max_workers` jedoch an Ihre CPU‑Kerne und die Größe des Bildsatzes anpassen.

```python
from concurrent.futures import ThreadPoolExecutor, as_completed

with ThreadPoolExecutor(max_workers=4) as pool:
    # Submit each image to the pool; map futures back to filenames
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    
    # Process results as they finish (order may differ from input order)
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)
```

### Wie das zu paralleler Bild‑Erkennung in Python führt

* **ThreadPoolExecutor** erzeugt einen Pool von Worker‑Threads, die jeweils `recognize_image` aufrufen.  
* Da die OCR‑Engine im async‑Batch‑Modus läuft, kann jeder Thread Arbeit an die Engine übergeben, während er weiterhin responsiv bleibt.  
* `as_completed` liefert Futures in der Reihenfolge ihres Abschlusses, sodass Sie Ergebnisse sofort erhalten – ideal für das Streamen großer Batches.

> **Häufiges Stolperstein:** `max_workers=1` macht den Parallelismus zunichte. Auf einer 8‑Kern‑Maschine liefert `max_workers=8` oft den besten Durchsatz, testen Sie jedoch ein paar Werte, um den optimalen Punkt für Ihre Hardware zu finden.

## Schritt 5: Ausgabe prüfen und Sonderfälle behandeln

Wenn Sie das Skript ausführen, sehen Sie für jedes PNG einen Textblock, der mit dem Dateinamen prefixed ist:

```
--- YOUR_DIRECTORY/page1.png ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- YOUR_DIRECTORY/page2.png ---
Sed do eiusmod tempor incididunt ut labore et dolore...

--- YOUR_DIRECTORY/page3.png ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

Falls ein Bild fehlschlägt (beschädigte Datei, nicht unterstütztes Format), gibt der `except`‑Block eine hilfreiche Fehlermeldung aus, anstatt das gesamte Batch zum Absturz zu bringen.

### Erweiterung der Lösung

| Szenario | Empfohlene Anpassung |
|----------|----------------------|
| **Tausende von Seiten** | Wechseln Sie zu `ProcessPoolExecutor`, um mehrere CPU‑Prozesse zu nutzen, oder teilen Sie die Liste in Chargen und verarbeiten Sie diese sequenziell. |
| **Andere Bildformate (JPG, TIFF)** | Die Methode `storage.Image.load` erkennt das Format automatisch, fügen Sie einfach die Dateien zu `input_images` hinzu. |
| **Ergebnisse speichern** | Schreiben Sie `text` in eine `.txt`‑Datei oder speichern Sie es in einer Datenbank im `else`‑Block. |
| **Performance‑Monitoring** | Umwickeln Sie `recognize_image` mit einem Timer (`time.perf_counter`) und protokollieren Sie die Dauer pro Datei. |

## Vollständiges Beispiel (Kopier‑und‑Einfügen bereit)

Unten finden Sie das komplette Skript, das Sie direkt in eine Datei namens `parallel_ocr.py` einfügen können. Es fehlt nichts – alles, was Sie benötigen, ist hier enthalten.

```python
# parallel_ocr.py
import aspose.ocr as aocr
import aspose.storage as storage
from concurrent.futures import ThreadPoolExecutor, as_completed

# -------------------------------------------------
# Step 1: Initialize OCR engine in async batch mode
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.batch_mode = aocr.BatchMode.ASYNC   # enable asynchronous batch processing

# -------------------------------------------------
# Step 2: Define the PNG files you want to recognize
# -------------------------------------------------
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]

# -------------------------------------------------
# Step 3: Helper that loads an image and returns the recognized text
# -------------------------------------------------
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the OCR‑extracted text.
    """
    img = storage.Image.load(path)
    result = ocr_engine.recognize(img)
    return result.text

# -------------------------------------------------
# Step 4: Run OCR on all images concurrently using a thread pool
# -------------------------------------------------
with ThreadPoolExecutor(max_workers=4) as pool:
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)

# -------------------------------------------------
# Step 5: Output is printed to the console.
# -------------------------------------------------
```

Speichern Sie die Datei, passen Sie den Platzhalter `YOUR_DIRECTORY` an und führen Sie aus:

```bash
python parallel_ocr.py
```

Sie sollten den extrahierten Text für jedes PNG in der Konsole sehen, genau wie zuvor gezeigt.

## Fazit

Wir haben gezeigt, wie man **Text aus PNG**‑Dateien effizient extrahiert, indem man Aspose OCRs async‑Batch‑Modus mit Pythons `ThreadPoolExecutor` kombiniert. Das Skript wandelt gescannte Seiten parallel in Text um und bietet Ihnen eine skalierbare Möglichkeit, **image text python**‑artig zu erkennen, ohne einen eigenen Thread‑Pool von Grund auf zu schreiben.  

Wenn Sie weitergehen wollen, probieren Sie:

* Ergebnisse in einer durchsuchbaren SQLite‑Datenbank speichern.  
* Bild‑Vorverarbeitung (Deskew, Denoise) mit OpenCV vor dem OCR hinzufügen.  
* Das Skript als Microservice hinter einem Flask‑ oder FastAPI‑Endpoint bereitstellen.

Denken Sie daran: Der Schlüssel zu performantem OCR ist nicht nur eine schnellere Engine – es geht auch darum, der Engine Arbeit so zuzuführen, dass die Parallelität maximiert wird. Mit dem hier gezeigten Muster können Sie Dutzende oder sogar Hunderte von PNG‑Scans mit minimalen Code‑Änderungen verarbeiten.

Viel Spaß beim Coden und mögen Ihre PDFs immer durchsuchbar sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}