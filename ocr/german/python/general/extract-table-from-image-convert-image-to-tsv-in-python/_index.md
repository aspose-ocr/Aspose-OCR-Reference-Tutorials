---
category: general
date: 2026-07-05
description: Tabelle aus Bild mit Python OCR extrahieren. Erfahren Sie, wie Sie Tabellen
  extrahieren, das Bild in TSV umwandeln und OCR‑Tabellen‑Python‑Techniken meistern.
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: de
og_description: Tabelle aus Bild mit Python OCR extrahieren. Dieser Leitfaden zeigt,
  wie man eine Tabelle extrahiert, das Bild in TSV umwandelt und OCR‑Tabellen‑Bild‑Python‑Tools
  verwendet.
og_title: Tabelle aus Bild extrahieren – Bild in TSV mit Python konvertieren
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  headline: Extract Table from Image – Convert Image to TSV in Python
  type: TechArticle
- description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  name: Extract Table from Image – Convert Image to TSV in Python
  steps:
  - name: Initialise the aocr OCR engine.
    text: Initialise the aocr OCR engine.
  - name: Attach the AI post‑processor.
    text: Attach the AI post‑processor.
  - name: Load a table image.
    text: Load a table image.
  - name: Perform structured OCR.
    text: Perform structured OCR.
  - name: Clean the results.
    text: Clean the results.
  - name: Export the table as a TSV file.
    text: Export the table as a TSV file.
  type: HowTo
tags:
- OCR
- Python
- Table Extraction
title: Tabelle aus Bild extrahieren – Bild in TSV konvertieren mit Python
url: /de/python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tabelle aus Bild extrahieren – Bild in TSV konvertieren mit Python

Haben Sie sich jemals gefragt, wie man eine Tabelle aus einem Bild extrahiert, ohne sich die Haare zu raufen? In diesem Tutorial führen wir Sie durch **wie man Tabellendaten** aus einem Bild mit der `aocr`‑Bibliothek extrahiert und diese dann in eine saubere TSV‑Datei umwandelt. Kein Zauber, nur ein paar Zeilen Python und ein wenig KI‑gestützte Nachbearbeitung.

Wenn Sie schon einmal versucht haben, eine Tabelle aus einer gescannten Rechnung oder einem Screenshot zu kopieren und dabei ein wirres Durcheinander erhalten haben, werden Sie verstehen, warum ein OCR‑basiertes Vorgehen es wert ist, gemeistert zu werden. Am Ende können Sie jedes Bild einer Tabelle in Python einlesen und saubere, tabulatorgetrennte Werte erhalten, die bereit für Tabellenkalkulationen oder Datenbanken sind.

---

## Was Sie benötigen

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| Python 3.9+ | Das `aocr`‑Paket richtet sich an moderne Python‑Laufzeiten. |
| `aocr` library (`pip install aocr`) | Stellt die OCR‑Engine und den KI‑Nachbearbeiter bereit, den wir verwenden. |
| An image file containing a table (PNG, JPG, etc.) | Die Quelldaten, die wir extrahieren. |
| Optional: a virtual environment | Hält Abhängigkeiten isoliert – sehr empfohlen. |

Wenn Sie diese bereit haben, vermeiden Sie Unterbrechungen mitten im Leitfaden.

---

## Installieren der Abhängigkeiten

Zuerst installieren wir das OCR‑Werkzeug. Öffnen Sie ein Terminal und führen Sie aus:

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **Pro Tipp:** Wenn Sie Berechtigungsfehler erhalten, fügen Sie `--user` zum `pip install`‑Befehl hinzu oder verwenden Sie `pipx` für eine globale Installation.

---

## Schritt 1 – OCR‑Engine initialisieren

Die Engine ist das Herzstück des Prozesses. Denken Sie an sie als das „Gehirn“, das jedes Pixel betrachtet und entscheidet, welches Zeichen wo hingehört.

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

Warum instanziieren wir eine Engine, anstatt eine einzelne Funktion aufzurufen? Das Engine‑Objekt ermöglicht es uns, später benutzerdefinierte Nachbearbeiter anzuhängen, was uns eine feinkörnige Kontrolle über die Ausgabe gibt – essenziell, wenn Sie **ocr table image python**‑Genauigkeit benötigen.

---

## Schritt 2 – KI‑Nachbearbeiter anhängen

`aocr` wird mit einem leichten KI‑Nachbearbeiter geliefert, der Roh‑OCR‑Ergebnisse bereinigt und gleichzeitig Zellgrenzen bewahrt. Es werden keine zusätzlichen Argumente benötigt, was den Code übersichtlich hält.

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

Wenn Sie diesen Schritt überspringen, erhalten Sie immer noch Rohtext, aber die Tabellenstruktur wird unübersichtlich – denken Sie an eine Tabellenkalkulation, in der jede Zelle ein Rätsel ist. Der Nachbearbeiter übernimmt das schwere Heben, indem er den Text an das ursprüngliche Raster ausrichtet.

---

## Schritt 3 – Laden Sie Ihr Tabellenbild

Sie können ein Bild von jedem Pfad laden, aber zur Übersicht verwenden wir ein Platzhalter‑Verzeichnis. Ersetzen Sie `"YOUR_DIRECTORY/invoice_table.png"` durch den tatsächlichen Pfad zu Ihrer Datei.

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

> **Hinweis:** `aocr.Image` erkennt das Bildformat automatisch und normalisiert die Farbkanäle, sodass Sie die Datei nicht vorverarbeiten müssen, es sei denn, sie ist stark beschädigt.

---

## Schritt 4 – Strukturiertes OCR ausführen

Jetzt scannt die Engine das Bild und gibt ein Roh‑Tabellenobjekt zurück. Dieses Objekt enthält Zeilen, Spalten und den Rohtext für jede Zelle.

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

Warum `recognize_structured` anstelle eines generischen `recognize`‑Aufrufs verwenden? Die strukturierte Variante versucht, Zeilen‑/Spalten‑Grenzen zu ermitteln, was Ihnen ein matrixähnliches Ergebnis liefert, das später viel einfacher in TSV zu konvertieren ist.

---

## Schritt 5 – Daten mit dem KI‑Nachbearbeiter bereinigen

Das Ausführen des Nachbearbeiters verfeinert die Rohausgabe: Es entfernt fehlende Zeichen, fügt geteilte Fragmente zusammen und stellt sicher, dass der Text jeder Zelle korrekt ausgerichtet ist.

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

Wenn Sie `processed_table.table` inspizieren, sehen Sie eine Liste von Zeilen, wobei jede Zeile eine Liste von `Cell`‑Objekten ist. Jede `Cell` hat ein `.text`‑Attribut, das die bereinigte Zeichenkette enthält.

---

## Schritt 6 – Tabelle als TSV exportieren

Der letzte Schritt besteht darin, die verarbeiteten Daten in eine tabulatorgetrennte Datei (TSV) zu verwandeln – genau das, was Sie benötigen, wenn Sie ein **Bild in TSV konvertieren** für Excel oder Google Sheets wollen.

```python
import csv

# Define the output TSV path
tsv_path = "extracted_table.tsv"

# Open the file and write rows as tab‑separated values
with open(tsv_path, "w", newline="", encoding="utf-8") as tsv_file:
    writer = csv.writer(tsv_file, delimiter="\t")
    for row in processed_table.table:
        # Extract text from each cell and write the row
        writer.writerow([cell.text for cell in row])

print(f"✅ Table successfully saved to {tsv_path}")
```

Das Ausführen des Skripts gibt jede Zeile in der Konsole aus (falls Sie das bevorzugen) und schreibt eine saubere TSV‑Datei, die Sie in jedem Tabellenkalkulationsprogramm öffnen können.

### Schnelle Überprüfung

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

Sie sollten ordentlich ausgerichtete Spalten sehen, zum Beispiel:

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

Wenn die Ausgabe wirr aussieht, überprüfen Sie die Bildqualität (Schärfe, Kontrast) und überlegen Sie, die Einstellungen der OCR‑Engine anzupassen – `engine.set_config(...)` ermöglicht das Anpassen von Sprachmodellen und Vertrauensschwellen.

---

## Umgang mit häufigen Randfällen

| Situation | Vorgeschlagene Lösung |
|-----------|-----------------------|
| **Schiefes Bild** | Vorab drehen Sie das Bild mit `Pillow` (`Image.rotate`), bevor Sie es an `aocr` übergeben. |
| **Geringer Kontrast** | Wenden Sie Histogramm‑Equalisation (`cv2.equalizeHist`) an, um die Lesbarkeit zu erhöhen. |
| **Zusammengeführte Zellen** | Nachbearbeiten Sie die TSV, um Zellen anhand bekannter Trennzeichen zu splitten, oder verwenden Sie das Flag `merge_cells=False`, falls verfügbar. |
| **Mehrseitige PDFs** | Konvertieren Sie zuerst jede Seite in ein Bild (`pdf2image`) und führen Sie die Pipeline in einer Schleife aus. |

Diese Anpassungen halten Ihren **ocr table image python**‑Workflow robust über verschiedenes Ausgangsmaterial hinweg.

---

## Vollständiges Skript – All‑in‑One‑Lösung

Unten finden Sie das vollständige, sofort ausführbare Skript, das alle besprochenen Schritte bündelt. Speichern Sie es als `extract_table.py` und führen Sie `python extract_table.py` aus.

```python
#!/usr/bin/env python3
"""
Extract Table from Image – Convert Image to TSV (Python)

This script demonstrates how to:
1. Initialise the aocr OCR engine.
2. Attach the AI post‑processor.
3. Load a table image.
4. Perform structured OCR.
5. Clean the results.
6. Export the table as a TSV file.

Author: Your Name
Date: 2026-07-05
"""

import aocr
import csv
import sys
from pathlib import Path

def main(image_path: str, output_tsv: str = "extracted_table.tsv"):
    # Step 1 – Initialise engine
    engine = aocr.OcrEngine()

    # Step 2 – Attach AI post‑processor
    engine.set_post_processor(ai.run_postprocessor, None)

    # Step 3 – Load image
    if not Path(image_path).is_file():
        sys.exit(f"❌ Image not found: {image_path}")
    image = aocr.Image.from_file(image_path)

    # Step 4 – Structured OCR
    raw_table = engine.recognize_structured(image)

    # Step 5 – Clean with post‑processor
    processed_table = engine.run_postprocessor(raw_table)

    # Step 6 – Write TSV
    with open(output_tsv, "w", newline="", encoding="utf-8") as tsv_file:
        writer = csv.writer(tsv_file, delimiter="\


## Was Sie als Nächstes lernen sollten

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Text aus Bild mit Aspose OCR extrahieren – Schritt‑für‑Schritt‑Anleitung](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Wie man eine Tabelle aus einem Bild mit Aspose.OCR für .NET extrahiert](/ocr/english/net/text-recognition/recognize-table/)
- [Wie man Text aus einem Bild extrahiert, indem man Rechtecke für OCR vorbereitet](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}