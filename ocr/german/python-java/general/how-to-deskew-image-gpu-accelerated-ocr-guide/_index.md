---
category: general
date: 2026-01-02
description: Erfahren Sie, wie Sie Bilder entzerren und den Bildkontrast erhöhen,
  um schnell Klartext zu erhalten. Enthält Schritt‑für‑Schritt‑Python‑Code und Tipps
  zur Textextraktion.
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: de
og_description: Wie man ein Bild entneigt und den Kontrast erhöht, um Klartext zu
  erhalten. Vollständiges Python‑Beispiel mit Tabellenauszug und GPU‑Beschleunigung.
og_title: Wie man ein Bild entzerrt – vollständiges GPU-OCR‑Tutorial
tags:
- OCR
- Python
- Image Processing
title: Wie man ein Bild entzerrt – GPU‑beschleunigter OCR-Leitfaden
url: /de/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein Bild deskewt – GPU‑beschleunigter OCR‑Leitfaden

Haben Sie sich schon einmal gefragt, **wie man ein Bild deskewt**, wenn Ihre Belege schräg eingescannt werden? Sie sind nicht allein; ein verzerrtes Foto kann einen eigentlich gut lesbaren Beleg in ein Durcheinander verwandeln. Die gute Nachricht: Mit wenigen Zeilen Python können Sie das Bild automatisch deskewen, den Kontrast erhöhen und sauberen Klartext extrahieren – ganz ohne manuelles Photoshop.

In diesem Tutorial gehen wir Schritt für Schritt durch ein vollständiges, ausführbares Beispiel, das nicht nur **wie man ein Bild deskewt**, sondern auch **wie man den Kontrast erhöht**, **wie man Klartext erhält** und sogar **wie man Text aus Tabellen extrahiert**, die die OCR‑Engine erkennt. Am Ende haben Sie ein eigenständiges Skript, das Sie in jedes Projekt einbinden können.

## Was Sie benötigen

- Python 3.9+ installiert (der Code verwendet Typannotationen, ein aktueller Interpreter hilft)
- Die `ocr`‑Bibliothek, die `OcrEngine`, `EngineMode`, `ImageProcessingOptions` und `OcrResult` bereitstellt (Installation via `pip install ocr‑sdk` – ersetzen Sie den Namen durch das von Ihnen genutzte Paket)
- Eine GPU mit kompatiblen Treibern, wenn Sie den Geschwindigkeitsvorteil nutzen möchten (optional, aber empfohlen)
- Eine Bilddatei, die leicht gedreht oder kontrastarm ist, z. B. `receipt_skewed.jpg`

> **Pro‑Tipp:** Wenn Sie keine GPU haben, ändern Sie einfach `EngineMode.GPU` zu `EngineMode.CPU` – das Skript funktioniert weiterhin, nur etwas langsamer.

## Schritt‑für‑Schritt‑Implementierung

Im Folgenden zerlegen wir die Lösung in logische Abschnitte. Jeder Abschnitt hat eine beschreibende **H2**, die entweder das Hauptkeyword *wie man ein Bild deskewt* oder eines der sekundären Keywords enthält. Der Code ist vollständig, kommentiert und sofort ausführbar.

### Wie man ein Bild deskewt mit GPU‑beschleunigtem OCR

Zuerst konfigurieren wir die OCR‑Engine, damit sie auf der GPU läuft und die Auto‑Deskew‑Funktion aktiviert wird. Auto‑Deskew analysiert die Geometrie des Bildes und dreht es wieder aufrecht.

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **Warum das wichtig ist:** GPU‑Beschleunigung kann die Verarbeitungszeit von Sekunden auf Millisekunden reduzieren, was entscheidend ist, wenn Sie Dutzende Belege pro Minute bearbeiten.

### Bildkontrast für bessere Erkennung erhöhen

Ein kontrastarmer Beleg ist ein Albtraum für jedes OCR‑System. Durch das Erhöhen des Kontrasts geben wir der Engine klarere Kanten zum Arbeiten.

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **Wie man den Kontrast erhöht:** Die Methode `set_contrast_boost` akzeptiert einen Prozentsatz; 30 % ist ein sicherer Standard, der für die meisten gescannten Belege funktioniert. Wenn Ihre Bilder extrem dunkel sind, erhöhen Sie den Wert auf 50 % oder experimentieren Sie.

### Klartext aus dem verarbeiteten Bild erhalten

Jetzt, wo das Bild gerade und hell ist, übergeben wir es an die Engine und fragen nach dem Klartext‑Ergebnis.

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**Erwartete Ausgabe** (gekürzt zur Übersicht):

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **Wie man Klartext erhält:** Die Methode `get_text()` entfernt alle Layout‑Informationen und gibt einen sauberen String zurück, den Sie dann in einer Datenbank speichern, an eine API senden oder in nachgelagerte Analysen einspeisen können.

### Wie man Text aus erkannten Tabellen extrahiert

Oft enthalten Belege tabellarische Daten (Artikel, Mengen, Preise). Das OCR‑SDK kann Tabellen erkennen und Ihnen erlauben, über Zeilen und Zellen zu iterieren.

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**Beispielhafte Tabellenausgabe**:

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **Warum Tabellen extrahieren:** Strukturierte Daten machen es trivial, Summen zu berechnen, Berichte zu erstellen oder sie in Buchhaltungssoftware zu importieren.

### Vollständiges funktionierendes Skript

Alles zusammengefügt, hier das Skript, das Sie in `deskew_and_ocr.py` kopieren können:

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

Ausführen mit:

```bash
python deskew_and_ocr.py
```

Sie sollten den bereinigten Text und alle erkannten Tabellen in der Konsole ausgegeben sehen.

## Häufige Randfälle & deren Behandlung

| Situation | Was zu tun ist |
|-----------|----------------|
| **Bild ist verkehrt herum** | Erhöhen Sie die Zuverlässigkeit von `set_auto_deskew(True)`, indem Sie zusätzlich `set_rotation_correction(True)` aufrufen, falls das SDK dies unterstützt. |
| **Kontrastverstärkung macht das Bild zu hell** | Reduzieren Sie den Prozentsatz, der an `set_contrast_boost` übergeben wird (z. B. 15 %). |
| **GPU nicht verfügbar** | Wechseln Sie `EngineMode.GPU` zu `EngineMode.CPU`; der Rest der Pipeline bleibt unverändert. |
| **Tabellen werden nicht erkannt** | Versuchen Sie einen Scan mit höherer Auflösung oder aktivieren Sie `set_table_detection(True)`, falls die Bibliothek dies bietet. |

## Nächste Schritte: Von Klartext zu strukturierten Daten

Jetzt, wo Sie **wie man ein Bild deskewt**, **wie man den Kontrast erhöht** und **wie man Klartext erhält**, können Sie:

- Den Klartext mit regulären Ausdrücken parsen, um Schlüssel‑Wert‑Paare zu extrahieren (z. B. `total`, `date`).
- Die Ergebnisse in einer SQLite‑ oder PostgreSQL‑Datenbank für spätere Berichte speichern.
- Das Skript in eine serverlose Funktion (AWS Lambda, Azure Functions) einbinden, um Uploads automatisch zu verarbeiten.

All diese Erweiterungen bauen auf derselben Grundlage auf, die wir hier behandelt haben.

## Fazit

Wir haben gezeigt, **wie man ein Bild deskewt** mit einer GPU‑beschleunigten OCR‑Engine, **wie man den Kontrast erhöht** für schärfere Erkennung, **wie man Klartext erhält** und sogar **wie man Text aus Tabellen extrahiert**. Das vollständige, ausführbare Skript verbindet alles, sodass Sie es in jedes Python‑Projekt einbinden und sofort saubere Daten aus schrägen, kontrastarmen Fotos ziehen können.

Probieren Sie es mit ein paar Ihrer eigenen Belege aus, passen Sie den Kontrast an und lassen Sie die OCR die schwere Arbeit übernehmen. Wenn Sie auf Besonderheiten stoßen, schauen Sie noch einmal in die Randfall‑Tabelle – die meisten Probleme lassen sich mit einer kleinen Anpassung beheben.

Viel Spaß beim Coden, und mögen Ihre Bilder immer gerade und hell sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}