---
category: general
date: 2026-03-26
description: Wie man OCR effizient stapelweise mit Python durchführt – lerne, Text
  aus Bildern und PDFs zu extrahieren und OCR‑Konvertierung mit Parallelverarbeitung.
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: de
og_description: Wie man OCR stapelweise effizient durchführt – Schritt‑für‑Schritt‑Anleitung
  zum Extrahieren von Text aus Bildern, PDF‑OCR‑Konvertierung und Batch‑OCR‑Verarbeitung
  mit Python.
og_title: 'Wie man OCR im Batch ausführt: schnelle parallele Textextraktion'
tags:
- OCR
- Python
- Parallel Computing
title: 'Wie man OCR stapelt: Schnelle parallele Textextraktion'
url: /de/python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR stapelt: schnelle parallele Textextraktion

Haben Sie sich jemals gefragt **wie man OCR stapelt**, wenn Sie Dutzende gescannter Seiten, Screenshots und PDFs herumliegen haben? Sie sind nicht allein – die meisten Entwickler stoßen auf dasselbe Problem: das Verarbeiten jeder Datei einzeln wird zu einem schmerzhaften Engpass.  

Die gute Nachricht ist, dass Sie ein paar Worker‑Threads starten, ihnen alle Ihre Dateien zuführen und beobachten können, wie die OCR‑Engine den Stapel parallel abarbeitet. In diesem Tutorial gehen wir Schritt für Schritt ein vollständiges, sofort ausführbares Beispiel durch, das **extract text from images** zeigt, **pdf ocr conversion** durchführt und **parallel ocr processing** für Geschwindigkeit nutzt.

> **Was Sie am Ende wissen werden**  
> * Ein voll funktionsfähiges Python‑Skript, das eine gemischte Liste von PNG-, TIFF-, PDF‑ und JPG‑Dateien in einem Durchlauf verarbeitet.  
> * Verständnis dafür, warum ein Thread‑Pool I/O‑intensive OCR‑Aufgaben beschleunigt.  
> * Tipps zum Umgang mit Fehlern, großen PDFs und benutzerdefinierten Thread‑Anzahlen.  

## Voraussetzungen

Bevor wir starten, stellen Sie sicher, dass Sie Folgendes haben:

| Requirement | Reason |
|-------------|--------|
| Python 3.8+ | Moderne Syntax & `concurrent.futures` |
| `ocr` library (or any compatible OCR wrapper) | Provides `OcrBatchProcessor` and result objects |
| A handful of sample files (PNG, TIFF, PDF, JPG) | To see the **extract text from images** in action |
| Basic familiarity with threads (optional) | Helpful but not mandatory |

Wenn Sie das `ocr`‑Paket noch nicht installiert haben, führen Sie aus:

```bash
pip install ocr-lib   # replace with the actual package name
```

Jetzt, wo die Umgebung bereit ist, zerlegen wir das Problem.

## Schritt 1: Hilfsfunktionen importieren und den Batch‑Processor instanziieren

Das Erste, was wir benötigen, ist ein Ort, um alle OCR‑Jobs zu sammeln. Die Klasse `OcrBatchProcessor` erledigt genau das – sie queue‑t Arbeitsitems und gibt Ihnen eine Liste von `Future`‑Objekten zurück.

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*Why this matters*: Importing `as_completed` lets us react to each finished job instantly, rather than waiting for the slowest file. This is the core of **batch ocr processing**.

## Schritt 2: Den Worker‑Pool für parallele Ausführung abstimmen

Standardmäßig könnte der Prozessor nur einen einzelnen Thread verwenden, was den Sinn des Batchings zunichte macht. Wir fordern explizit vier Worker an – passen Sie die Zahl gern an die Anzahl Ihrer CPU‑Kerne an.

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*Pro tip*: Für I/O‑bound Aufgaben wie OCR erhalten Sie oft abnehmende Erträge nach `CPU cores * 2`. Testen Sie ein paar Werte und wählen Sie den Sweet Spot.

## Schritt 3: Jede Datei, die Sie OCR‑verarbeiten wollen, in die Queue legen

Hier fügen wir einen gemischten Satz von Bild‑ und PDF‑Dateien hinzu. Die Methode `add` speichert lediglich den Pfad; die eigentliche Arbeit beginnt erst, wenn wir den Batch einreichen.

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

Falls Sie einen ganzen Ordner verarbeiten müssen, erledigt eine schnelle `glob`‑Schleife das:

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## Schritt 4: Die Jobs starten und Futures sammeln

Ein Aufruf von `submit_all` gibt dem Prozessor das grüne Licht. Er liefert eine Liste von `Future`‑Objekten zurück – denken Sie an sie als Platzhalter für Ergebnisse, die später erscheinen.

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

Zu diesem Zeitpunkt arbeitet die OCR‑Engine im Hintergrund, jeder Thread mampft an einer Datei.

## Schritt 5: Ergebnisse sofort abholen, sobald sie fertig sind

Mit `as_completed` iterieren wir über Futures in der Reihenfolge, in der sie fertig werden, nicht in der Reihenfolge, in der wir sie eingereicht haben. Das hält unser Skript reaktionsfähig, besonders wenn einige PDFs länger dauern als einfache PNGs.

```python
# Step 5 – retrieve each result as it completes
for future in as_completed(ocr_futures):
    try:
        ocr_result = future.result()          # May raise if the job failed
        print("Batch result:\n", ocr_result.get_text())
    except Exception as exc:
        # Graceful error handling – you can log or retry here
        print(f"An OCR job failed: {exc}")
```

**Expected output** (truncated for brevity):

```
Batch result:
 The quick brown fox jumps over the lazy dog.
...
Batch result:
 Invoice #12345
 Date: 2026-03-01
 Total: $1,234.56
...
```

Jeder Block entspricht der Nur‑Text‑Darstellung der Originaldatei. Wenn Sie **pdf ocr conversion** durchführen, enthält der Text alles, was die OCR‑Engine von jeder Seite entschlüsseln konnte.

## Umgang mit Randfällen & häufigen Stolperfallen

| Situation | What to watch for | Quick fix |
|-----------|-------------------|-----------|
| A corrupted image | `future.result()` raises `OSError` | Wrap in `try/except` (see code above) |
| Very large PDFs ( > 100 MB ) | Memory pressure, slower threads | Increase `thread_count` modestly or split PDF into chapters first |
| Mixed language documents | Default OCR model may mis‑detect | Pass language hints to `OcrBatchProcessor` if the library supports it |
| Need to preserve layout | Plain `get_text()` loses columns | Use `ocr_result.get_hocr()` or similar layout‑aware method |

### Pro tip: Benutzerdefinierte Thread‑Anzahl basierend auf Dateityp

Wenn Sie wissen, dass der Großteil Ihrer Arbeit PDFs sind, können Sie dafür mehr Threads zuweisen und für kleine PNGs weniger. Einige Bibliotheken erlauben das Setzen einer `priority` pro Job; andernfalls können Sie zwei separate Batches erstellen – einen für Bilder, einen für PDFs – und sie gleichzeitig ausführen.

## Visueller Überblick (optional)

![Diagramm zum Batch-OCR-Workflow](https://example.com/ocr-workflow.png "Diagramm zum Batch-OCR-Workflow")

*Das Diagramm veranschaulicht den Ablauf von Dateierkennung → Batch‑Erstellung → parallele Ausführung → Ergebnisaggregation.*

## Vollständiges Skript zum Kopieren & Einfügen

Unten finden Sie das gesamte Programm, fertig zum Einfügen in eine `.py`‑Datei. Es enthält alle oben gezeigten Snippets sowie einen kleinen Helfer, der automatisch unterstützte Dateien in einem Verzeichnis entdeckt.

```python
#!/usr/bin/env python3
"""
How to Batch OCR – Complete Example
-----------------------------------
This script demonstrates parallel OCR processing of mixed image and PDF files.
It shows how to extract text from images, perform pdf ocr conversion, and
handle errors gracefully.
"""

from concurrent.futures import as_completed
import pathlib, fnmatch, sys
import ocr  # replace with your actual OCR library import

def discover_files(root_dir):
    """Yield paths of supported OCR files under *root_dir*."""
    for path in pathlib.Path(root_dir).rglob("*"):
        if fnmatch.fnmatch(path.suffix.lower(), ".png") \
           or fnmatch.fnmatch(path.suffix.lower(), ".tif") \
           or fnmatch.fnmatch(path.suffix.lower(), ".pdf") \
           or fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
            yield str(path)

def main(directory, workers=4):
    # 1️⃣ Initialise batch processor
    ocr_batch = ocr.OcrBatchProcessor()
    ocr_batch.set_thread_count(workers)

    # 2️⃣ Queue every discovered file
    for file_path in discover_files(directory):
        ocr_batch.add(file_path)

    # 3️⃣ Submit all jobs
    futures = ocr_batch.submit_all()

    # 4️⃣ Process results as they arrive
    for fut in as_completed(futures):
        try:
            result = fut.result()
            print("=== OCR RESULT ===")
            print(result.get_text())
            print("\n---\n")
        except Exception as e:
            print(f"[ERROR] OCR failed for a job: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-files>")
        sys.exit(1)
    main(sys.argv[1])
```

Speichern Sie dies als `batch_ocr.py`, verweisen Sie auf einen Ordner mit Ihren Scans und beobachten Sie, wie die Konsole mit extrahiertem Text gefüllt wird.  

### Warum das funktioniert

* **Thread pool** – OCR wartet meist auf Festplatten‑I/O und externe Engine‑Aufrufe, sodass mehrere Threads die CPU auslasten.  
* **`as_completed`** – Sie erhalten Ergebnisse, sobald sie bereit sind, was ideal für UI‑Feedback oder Streaming‑Pipelines ist.  
* **Error isolation** – Eine fehlerhafte Datei bringt nicht den gesamten Batch zum Absturz; der `try/except`‑Block isoliert Fehlerschläge.

## Fazit

Kurz gesagt, Sie wissen jetzt **how to batch ocr** mit Python’s `concurrent.futures` zusammen mit einer OCR‑Bibliothek, die Batch‑Verarbeitung unterstützt. Durch die Konfiguration eines modesten Thread‑Pools, das Queuen aller unterstützten Dateien und das Abrufen der Ergebnisse, sobald sie fertig sind, erreichen Sie schnelle **parallel ocr processing** ohne Einbußen bei der Zuverlässigkeit.  

Ab hier könnten Sie:

* Die Ausgabe in einen Suchindex einspeisen für schnellen Dokumentenzugriff.  
* Das Skript erweitern, sodass jedes Ergebnis neben der Originaldatei in eine `.txt`‑Datei geschrieben wird.  
* Den eingebauten Thread‑Pool durch `asyncio` ersetzen, falls Ihre OCR‑Bibliothek asynchrone APIs anbietet.  

Experimentieren Sie weiter – tauschen Sie Tesseract, Azure Cognitive Services oder Google Vision aus, und Sie werden das gleiche Muster anwenden. Viel Spaß beim OCR‑en!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}