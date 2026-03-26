---
category: general
date: 2026-03-26
description: Tabellen aus einem Bild extrahieren und das Bild mit Python‑OCR in eine
  Tabellenkalkulation umwandeln. Erfahren Sie, wie Sie ein Bild für OCR laden, Tabellen
  lesen und Tabellendaten extrahieren.
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: de
og_description: Tabellen aus Bild mit Python OCR extrahieren. Dieser Leitfaden zeigt,
  wie man ein Bild für OCR lädt, Tabellen liest und sie in ein Tabellenkalkulationsdokument
  umwandelt.
og_title: Tabellen aus Bild extrahieren – Vollständiges OCR‑Tutorial
tags:
- OCR
- Python
- Data Extraction
title: Tabellen aus Bild extrahieren – Schritt‑für‑Schritt OCR‑Anleitung
url: /de/python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tabellen aus Bild extrahieren – Komplettes OCR‑Tutorial

Hast du schon einmal **Tabellen aus einem Bild extrahieren** müssen, wusstest aber nicht, wo du anfangen sollst? Du bist nicht allein. Viele Entwickler stoßen auf ein Problem, wenn ein PDF oder Screenshot tabellarische Daten enthält, die in editierbare Zeilen und Spalten umgewandelt werden müssen. Die gute Nachricht? Ein paar Zeilen Python‑Code, kombiniert mit einer soliden OCR‑Engine, können dieses Bild in Sekundenschnelle in eine nutzbare Tabelle verwandeln.

In diesem Tutorial gehen wir Schritt für Schritt durch das Laden eines Bildes für OCR, das Ausführen der Erkennungs‑Engine und das Herausziehen jeder Tabelle Zeile für Zeile. Am Ende kannst du **Bild in Tabelle umwandeln**, und du siehst, wie man **ocr read tables** und **ocr extract table data** für die Weiterverarbeitung nutzt. Kein verstecktes Zauberwerk, nur klarer, ausführbarer Code, den du noch heute in dein Projekt einbinden kannst.

---

## Was du brauchst

Bevor wir loslegen, stelle sicher, dass du Folgendes zur Hand hast:

- **Python 3.9+** – die neueste stabile Version funktioniert am besten.
- Die **`ocr`**‑Bibliothek (oder ein kompatibles OCR‑SDK, das `OcrEngine`, `Image` und tabellenbezogene Methoden bereitstellt). Installiere sie mit `pip install ocr‑sdk` (ersetze den Namen durch das tatsächliche Paket).
- Eine Bilddatei (`.png`, `.jpg`, etc.), die eine klar gedruckte Tabelle enthält.  
- Optional: **pandas**, wenn du die extrahierten Daten direkt in eine CSV‑ oder Excel‑Datei schreiben möchtest (`pip install pandas`).

Alles bereit? Super – dann legen wir los.

---

## Schritt 1: Das OCR‑SDK importieren und die Umgebung vorbereiten

Zuerst müssen wir die OCR‑Klassen in unser Skript bringen und einen kleinen Helfer einrichten, der später die rohen Tabellendaten in ein DataFrame umwandelt.

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**Warum das wichtig ist:** Durch das Importieren von `ocr` erhalten wir Zugriff auf `OcrEngine`, `Imaging.Image` und die Tabellenobjekte, über die wir iterieren werden. `pandas` ist für die reine Extraktion nicht zwingend nötig, erleichtert aber den Teil **Bild in Tabelle umwandeln** erheblich.

---

## Schritt 2: Das Bild laden, das du verarbeiten willst

Jetzt **laden wir das Bild für OCR**. Das SDK erwartet ein `Image`‑Objekt, also verpacken wir unseren Dateipfad mit der Hilfsmethode `Image.load()`.

```python
# Step 2 – Load the image that contains a table
image_path = Path("YOUR_DIRECTORY/table_image.png")

# Verify the file exists early to avoid cryptic SDK errors
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Attach the image to the engine
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))
```

**Pro‑Tipp:** Lege deine Bilddateien in einem eigenen Ordner ab (`assets/` oder `data/`) und verwende relative Pfade. So bleibt das Skript auf verschiedenen Rechnern portabel.

---

## Schritt 3: Den Erkennungsprozess starten

Nachdem das Bild angehängt ist, können wir die Engine schließlich anweisen, **ocr read tables**. Der Aufruf `recognize()` liefert ein Ergebnisobjekt, das alles enthält, was die Engine entdeckt hat – Textblöcke, Zeilen und, am wichtigsten für uns, Tabellen.

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**Warum wir prüfen:** Manche Bilder sind verrauscht oder die Tabellenrahmen sind schwach, sodass die Engine sie übersehen könnte. Eine Warnung zu protokollieren gibt dir frühzeitiges Feedback, ohne das Skript zum Absturz zu bringen.

---

## Schritt 4: Zeilen und Zellen jeder Tabelle extrahieren

Hier passiert die eigentliche Magie. Wir iterieren über jede erkannte Tabelle, holen jede Zeile und dann den Text jeder Zelle. Die innere List‑Comprehension macht den Code kompakt, wir erklären aber trotzdem den Ablauf.

```python
# Step 4 – Iterate over detected tables and collect data
all_tables = []   # Will hold a list of pandas DataFrames

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")

    rows_data = []   # Temporary storage for this table's rows

    for row_obj in table_obj.get_rows():
        # Extract text from each cell in the current row
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    # Convert the raw list of rows into a DataFrame
    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    # Print a human‑readable version to the console
    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))
```

**Was passiert?**  

- `enumerate(..., start=1)` liefert eine freundliche Tabellennummer für das Logging.  
- `row_obj.get_cells()` gibt jedes Zellenobjekt zurück; `cell.get_text()` liefert den OCR‑dekodierten String.  
- Wir speichern die Zeilen in `rows_data` und übergeben sie an `pandas.DataFrame`, das die Spalten automatisch ausrichtet.  
- Der `print`‑Block spiegelt die **essential output** aus dem Originalsnippet wider, sodass du die Ergebnisse sofort prüfen kannst.

**Umgang mit Sonderfällen:** Wenn eine Zeile eine andere Anzahl Zellen hat als die übrigen, füllt `pandas` die fehlenden Stellen mit `NaN`. Du kannst das DataFrame später mit `df.fillna('')` bereinigen, falls du leere Strings bevorzugst.

---

## Schritt 5: Die extrahierten Tabellen in einer Tabelle speichern

Jetzt, wo wir eine Liste von DataFrames haben, ist das Schreiben in eine Excel‑Arbeitsmappe (oder CSV‑Dateien) ein Kinderspiel. Das erfüllt das Ziel **Bild in Tabelle umwandeln**.

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**Warum Excel?** Die meisten Business‑User bevorzugen `.xlsx`. Wenn du CSV bevorzugst, ersetze die Schleife durch `df.to_csv(f"table_{idx}.csv", index=False)`.

---

## Vollständiges, sofort ausführbares Skript

Alles zusammengefügt, hier das komplette Programm, das du kopieren und ausführen kannst.

```python
import ocr
from pathlib import Path
import pandas as pd
import logging

logging.basicConfig(level=logging.INFO)

# ---------- Configuration ----------
image_path = Path("YOUR_DIRECTORY/table_image.png")
output_path = Path("extracted_tables.xlsx")
# ----------------------------------

# Verify image exists
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Initialize OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))

# Run recognition
ocr_result = ocr_engine.recognize()

if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
    exit(0)

all_tables = []

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")
    rows_data = []

    for row_obj in table_obj.get_rows():
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))

# Save to Excel
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        df.to_excel(writer, sheet_name=f"Table_{idx}", index=False)

logging.info(f"All tables saved to {output_path}")
```

**Erwartete Konsolenausgabe** (bei einer einfachen 2×3‑Tabelle):

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

Und du findest `extracted_tables.xlsx` im Ordner des Skripts, jede Tabelle auf einem eigenen Blatt.

---

## Häufig gestellte Fragen & Tipps

| Frage | Antwort |
|----------|--------|
| **Kann ich eine andere OCR‑Bibliothek verwenden?** | Absolut. Das Muster bleibt gleich: Bild laden → erkennen → über `get_tables()` iterieren. Nur die Importe und Objektnamen anpassen. |
| **Was, wenn mein Bild verrauscht ist?** | Vorverarbeiten mit OpenCV (Schwellwert, Deskew) bevor du es an die OCR‑Engine übergibst. Rauschreduzierung verbessert oft die **ocr extract table data**‑Genauigkeit. |
| **Muss ich `openpyxl` installieren?** | Ja, `pandas` nutzt es im Hintergrund für die Excel‑Ausgabe. Installiere es mit `pip install openpyxl`. |
| **Wie gehe ich mit zusammengeführten Zellen um?** | Einige SDKs bieten `cell.is_merged()`; du kannst den Wert manuell über den zusammengeführten Bereich verbreiten. |
| **Gibt es eine Möglichkeit, nur bestimmte Tabellen zu extrahieren?** | Nach `table_obj.get_confidence()` filtern oder Header‑Schlüsselwörter prüfen, bevor du weiterverarbeitest. |

---

## Fazit

Du hast jetzt eine komplette End‑zu‑End‑Lösung, um **Tabellen aus Bild** zu extrahieren, das Ergebnis in eine übersichtliche Tabelle zu konvertieren und sogar mehrere Tabellen in einem Bild zu verarbeiten. Das Skript zeigt, wie man **Bild für OCR lädt**, **ocr read tables** und **ocr extract table data** durchführt, bleibt dabei aber flexibel genug für reale Anwendungsfälle.

Was kommt als Nächstes? Versuche, einer PDF‑Seite, die als Bild gerendert wurde, die OCR‑Engine zuzuführen, oder experimentiere mit verschiedenen Sprachen und Schriftarten. Du könntest die DataFrames auch direkt in eine Datenbank oder ein Reporting‑Tool pipen – deiner Fantasie sind keine Grenzen gesetzt.

Wenn dir dieser Leitfaden geholfen hat, teile ihn gern, gib dem Repository, das das SDK hostet, einen Stern oder hinterlasse einen Kommentar mit deinen eigenen Tricks. Viel Spaß beim Coden und möge deine Tabellen immer perfekt geparst werden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}