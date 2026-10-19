---
category: general
date: 2026-04-29
description: Extrahieren Sie Text aus PDFs mit Aspose OCR in Python. Erfahren Sie,
  wie Sie die Batch‑OCR‑PDF‑Verarbeitung durchführen, gescannte PDF‑Texte konvertieren
  und Seiten mit geringer Vertrauenswürdigkeit behandeln.
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: de
og_description: Extrahieren Sie Text aus PDF mit Aspose OCR in Python. Dieser Leitfaden
  zeigt die stapelweise OCR‑PDF‑Verarbeitung, das Konvertieren von gescanntem PDF‑Text
  und den Umgang mit Ergebnissen geringer Vertrauenswürdigkeit.
og_title: Text aus PDF extrahieren – PDF mit OCR in Python
tags:
- OCR
- Python
- PDF processing
title: Text aus PDF extrahieren – PDF mit OCR in Python
url: /de/python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus PDF extrahieren – OCR PDF mit Python

Haben Sie jemals **Text aus PDF** extrahieren müssen, aber die Datei ist nur ein gescanntes Bild? Sie sind nicht allein – viele Entwickler stoßen an diese Grenze, wenn sie PDFs in durchsuchbare Daten umwandeln wollen. Die gute Nachricht? Mit Aspose OCR für Python können Sie gescannten PDF‑Text in wenigen Zeilen konvertieren und sogar **Batch-OCR-PDF-Verarbeitung** durchführen, wenn Sie Dutzende von Dateien zu bearbeiten haben.

In diesem Tutorial führen wir Sie durch den gesamten Workflow: Bibliothek einrichten, OCR auf einer einzelnen PDF ausführen, auf ein Batch skalieren und mit Seiten niedriger Vertrauenswürdigkeit umgehen, sodass Sie wissen, wann eine manuelle Überprüfung erforderlich ist. Am Ende haben Sie ein sofort einsatzbereites Skript, das Text aus jeder gescannten PDF extrahiert, und Sie verstehen das „Warum“ hinter jedem Schritt.

## Was Sie benötigen

Bevor wir starten, stellen Sie sicher, dass Sie Folgendes haben:

- Python 3.8 oder neuer (der Code verwendet f‑Strings, daher funktioniert 3.6+, aber 3.8+ wird empfohlen)
- Eine Aspose OCR für Python Lizenz oder ein kostenloser Testschlüssel (Sie können einen von der Aspose‑Website erhalten)
- Ein Ordner mit einem oder mehreren gescannten PDFs, die Sie verarbeiten möchten
- Ein bescheidener Speicherplatz für die erzeugten *.txt*-Berichte

Das war’s – keine schweren externen Abhängigkeiten, kein OpenCV‑Gymnastik. Die Aspose‑OCR‑Engine übernimmt die schwere Arbeit für Sie.

## Umgebung einrichten

Zuerst installieren Sie das Aspose OCR‑Paket von PyPI:

```bash
pip install aspose-ocr
```

Wenn Sie eine Lizenzdatei (`Aspose.OCR.lic`) haben, legen Sie sie im Projekt‑Root ab und aktivieren Sie sie wie folgt:

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **Profi‑Tipp:** Halten Sie die Lizenzdatei außerhalb der Versionskontrolle; fügen Sie sie zu `.gitignore` hinzu, um versehentliche Offenlegung zu vermeiden.

## OCR auf einer einzelnen PDF ausführen

Jetzt extrahieren wir Text aus einer einzelnen gescannten PDF. Die Kernschritte sind:

1. Erstellen Sie eine `OcrEngine`‑Instanz.  
2. Zeigen Sie sie auf die PDF‑Datei.  
3. Rufen Sie ein `OcrResult` für jede Seite ab.  
4. Schreiben Sie die Klartext‑Ausgabe auf die Festplatte.  
5. Entsorgen Sie die Engine, um native Ressourcen freizugeben.

Hier ist das vollständige, ausführbare Skript:

```python
# Step 1: Import the OCR engine and create an instance
from aspose.ocr import OcrEngine

# Optional: activate license (see previous section)
# from aspose.ocr import License
# License().set_license("Aspose.OCR.lic")

ocr_engine = OcrEngine()

# Step 2: Specify the PDF file to be processed
pdf_file_path = r"YOUR_DIRECTORY/input.pdf"

# Step 3: Extract OCR results – one OcrResult object per page
ocr_pages = ocr_engine.extract_from_pdf(pdf_file_path)

# Step 4: Iterate through the results, show confidence, flag low‑confidence pages, and save the plain text
for ocr_page in ocr_pages:
    print(f"Page {ocr_page.page_number}: confidence {ocr_page.confidence:.2%}")

    # If confidence is below 80 %, flag it for manual review
    if ocr_page.confidence < 0.80:
        print("  Low confidence – consider manual review")

    # Build the output filename
    output_txt = f"YOUR_DIRECTORY/Report_page{ocr_page.page_number}.txt"
    with open(output_txt, "w", encoding="utf-8") as f:
        f.write(ocr_page.text)

# Step 5: Release resources used by the engine
ocr_engine.dispose()
```

**Was Sie sehen werden:** Für jede Seite gibt das Skript etwas wie `Page 1: confidence 97.45%` aus. Fällt eine Seite unter die 80 %-Schwelle, erscheint eine Warnung, die Sie darauf hinweist, dass das OCR Zeichen möglicherweise verpasst hat.

### Warum das funktioniert

- **`OcrEngine`** ist das Tor zur nativen Aspose‑OCR‑Bibliothek; sie übernimmt alles von der Bildvorverarbeitung bis zur Zeichenerkennung.  
- **`extract_from_pdf`** rasterisiert jede PDF‑Seite automatisch, sodass Sie das PDF nicht selbst in Bilder umwandeln müssen.  
- **Vertrauens‑Scores** ermöglichen automatisierte Qualitätsprüfungen – entscheidend, wenn Sie rechtliche oder medizinische Dokumente verarbeiten, bei denen Genauigkeit wichtig ist.

## Batch-OCR-PDF-Verarbeitung mit Python

Die meisten realen Projekte umfassen mehr als eine Datei. Wir erweitern das Einzel‑Datei‑Skript zu einer **Batch-OCR-PDF-Verarbeitung**‑Pipeline, die ein Verzeichnis durchläuft, jede PDF verarbeitet und die Ergebnisse in einem passenden Unterordner speichert.

```python
import os
from pathlib import Path
from aspose.ocr import OcrEngine

def ocr_pdf_file(pdf_path: Path, output_dir: Path, engine: OcrEngine, confidence_threshold: float = 0.80):
    """Extract text from a single PDF and write per‑page .txt files."""
    ocr_pages = engine.extract_from_pdf(str(pdf_path))
    for page in ocr_pages:
        print(f"{pdf_path.name} – Page {page.page_number}: {page.confidence:.2%}")
        if page.confidence < confidence_threshold:
            print("  ⚠️ Low confidence – manual review may be needed")

        out_file = output_dir / f"{pdf_path.stem}_page{page.page_number}.txt"
        out_file.write_text(page.text, encoding="utf-8")

def batch_ocr_pdf(input_folder: str, output_folder: str):
    """Iterate over all PDFs in input_folder and run OCR."""
    engine = OcrEngine()
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(parents=True, exist_ok=True)

    pdf_files = list(input_path.glob("*.pdf"))
    if not pdf_files:
        print("🚫 No PDF files found in the specified folder.")
        return

    for pdf_file in pdf_files:
        # Create a sub‑folder for each PDF to keep pages organized
        pdf_out_dir = output_path / pdf_file.stem
        pdf_out_dir.mkdir(exist_ok=True)
        ocr_pdf_file(pdf_file, pdf_out_dir, engine)

    # Clean up native resources
    engine.dispose()
    print("✅ Batch OCR completed.")

# Example usage:
if __name__ == "__main__":
    batch_ocr_pdf("YOUR_DIRECTORY/input_pdfs", "YOUR_DIRECTORY/ocr_output")
```

#### Wie das hilft

- **Skalierbarkeit:** Die Funktion durchläuft den Ordner einmal und erstellt für jede PDF einen eigenen Ausgabe‑Unterordner. Das hält die Dinge ordentlich, wenn Sie Dutzende von Dokumenten haben.  
- **Wiederverwendbarkeit:** `ocr_pdf_file` kann aus anderen Skripten (z. B. einem Web‑Service) aufgerufen werden, weil es eine reine Funktion ist.  
- **Fehlerbehandlung:** Das Skript gibt eine freundliche Meldung aus, wenn der Eingabe‑Ordner leer ist, und verhindert so ein stilles Scheitern.

## Gescannten PDF-Text konvertieren – Sonderfälle behandeln

Während der obige Code für die meisten PDFs funktioniert, können Ihnen ein paar Eigenheiten begegnen:

| Situation | Warum es passiert | Wie man es mildert |
|-----------|-------------------|--------------------|
| **Verschlüsselte PDFs** | Das PDF ist passwortgeschützt. | Übergeben Sie das Passwort an `extract_from_pdf(pdf_path, password="yourPwd")`. |
| **Mehrsprachige Dokumente** | Aspose OCR verwendet standardmäßig Englisch. | Setzen Sie `ocr_engine.language = "spa"` für Spanisch oder geben Sie eine Liste für gemischte Sprachen an. |
| **Sehr große PDFs (>500 Seiten)** | Der Speicherverbrauch steigt, weil jede Seite in den RAM geladen wird. | Verarbeiten Sie das PDF in Teilen mit `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` und einer Schleife. |
| **Schlechte Scan‑Qualität** | Niedrige DPI oder starkes Rauschen reduziert das Vertrauen. | Vorverarbeiten Sie das PDF mit `engine.image_preprocessing = True` oder erhöhen Sie die DPI über `engine.dpi = 300`. |

> **Achtung:** Das Einschalten der Bildvorverarbeitung kann die CPU‑Zeit deutlich erhöhen. Wenn Sie ein nächtliches Batch‑Job laufen lassen, planen Sie genug Zeit ein oder starten Sie einen separaten Worker.

## Ausgabe überprüfen

Nach Abschluss des Skripts finden Sie eine Ordnerstruktur wie:

```
ocr_output/
├─ invoice_2023/
│  ├─ invoice_2023_page1.txt
│  ├─ invoice_2023_page2.txt
│  └─ …
└─ contract_A/
   ├─ contract_A_page1.txt
   └─ …
```

Öffnen Sie eine beliebige `.txt`‑Datei; Sie sollten sauberen, UTF‑8‑kodierten Text sehen, der den ursprünglichen gescannten Inhalt widerspiegelt. Wenn Sie verzerrte Zeichen bemerken, überprüfen Sie die Spracheinstellungen des PDFs und stellen Sie sicher, dass die richtigen Schriftpakete auf dem Rechner installiert sind.

## Ressourcen bereinigen

Aspose OCR nutzt native DLLs, daher ist es wichtig, `engine.dispose()` aufzurufen, sobald Sie fertig sind. Das Vergessen dieses Schrittes kann zu Speicherlecks führen, besonders bei lang laufenden Batch‑Jobs.

```python
# Always the last line of your script
engine.dispose()
```

## Vollständiges End‑zu‑End‑Beispiel

Alles zusammengeführt, hier ein einzelnes

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}