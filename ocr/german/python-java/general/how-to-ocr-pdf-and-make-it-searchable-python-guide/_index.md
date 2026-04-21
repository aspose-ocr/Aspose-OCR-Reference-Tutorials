---
category: general
date: 2026-01-12
description: Erfahren Sie, wie Sie PDFs in Python OCRen und PDFs schnell durchsuchbar
  machen. Konvertieren Sie gescannte PDFs, extrahieren Sie Text aus PDFs und OCRen
  Sie gescannte PDFs in Python mit Aspose OCR.
draft: false
keywords:
- how to ocr pdf
- make pdf searchable
- convert scanned pdf
- extract text pdf
- ocr scanned pdf python
language: de
og_description: Wie man PDFs in Python OCRt? Dieses Schritt‑für‑Schritt‑Tutorial zeigt
  Ihnen, wie Sie gescannte PDF‑Dateien in durchsuchbare PDFs umwandeln und Text mit
  Aspose OCR extrahieren.
og_title: Wie man PDFs OCRt und durchsuchbar macht – Python‑Leitfaden
tags:
- OCR
- Python
- PDF processing
title: Wie man PDFs OCRt und durchsuchbar macht – Python‑Leitfaden
url: /de/python-java/general/how-to-ocr-pdf-and-make-it-searchable-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man PDF OCR und durchsuchbar macht – Python‑Leitfaden

Haben Sie sich jemals gefragt, **wie man PDF OCR** durchführt, ohne ein Vermögen für kommerzielle Software auszugeben? Sie sind nicht allein. Viele Entwickler stoßen an ihre Grenzen, wenn sie einen gescannten Vertrag, eine Rechnung oder irgendeine bildbasierte PDF in ein durchsuchbares Dokument umwandeln müssen. Die gute Nachricht? Mit ein paar Zeilen Python und Aspose OCR können Sie gescannte PDFs konvertieren, Text‑PDF extrahieren und schließlich PDFs in wenigen Minuten durchsuchbar machen.

In diesem Tutorial führen wir Sie durch alles, was Sie benötigen: von der Installation der Bibliothek, über die Konfiguration der Sprache, die Verarbeitung eines gescannten PDFs bis hin zum Speichern des Ergebnisses als durchsuchbares PDF, das sowohl das Originalbild als auch eine versteckte Textebene enthält. Am Ende haben Sie ein wiederverwendbares Skript, das Sie in jedes Projekt einbinden können – ohne manuelles Kopieren und Einfügen.

---

## Was Sie benötigen

- **Python 3.8+** (der Code funktioniert auf 3.9, 3.10 und neuer)
- Eine aktive **Aspose OCR for Python**‑Lizenz (ein kostenloser Testzugang reicht für Experimente)
- Eine gescannte PDF‑Datei (z. B. `scanned_contract.pdf`), die Sie durchsuchbar machen möchten
- Grundlegende Erfahrung mit der Befehlszeile und virtuellen Umgebungen (optional, aber empfohlen)

> **Pro‑Tipp:** Wenn Sie noch keine Lizenz haben, melden Sie sich für eine 30‑tägige Testversion auf der Aspose‑Website an; die Testversion ist für Entwicklungszwecke vollständig funktionsfähig.

---

## Wie man PDF mit Aspose OCR OCR‑t (Primäres Schlüsselwort in H2)

Der erste Schritt besteht darin, das richtige Paket zu erhalten. Aspose OCR bietet eine saubere, hoch‑level API, die die low‑level Bildverarbeitungsdetails abstrahiert.

```bash
# Create a virtual environment (optional but tidy)
python -m venv venv
source venv/bin/activate   # On Windows use `venv\Scripts\activate`

# Install the Aspose OCR package
pip install aspose-ocr
```

Sobald das Paket installiert ist, können Sie mit dem Schreiben des Skripts beginnen.

```python
# Step 1: Import the Aspose OCR module
import asposeocr as ocr

# Step 2: Create an OCR engine instance and set the recognition language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Warum die Sprache festlegen?**  
> Die OCR‑Genauigkeit hängt stark vom Sprachmodell ab. Indem Sie der Engine explizit mitteilen, dass englischer Text erwartet wird, reduzieren Sie Fehlalarme und beschleunigen die Verarbeitung.

---

## Schritt 2: Gescanntes PDF in ein durchsuchbares PDF konvertieren

Jetzt, wo die Engine bereit ist, zeigen Sie ihr Ihr gescanntes Dokument. Die Methode `process_pdf` gibt ein `PdfResult`‑Objekt zurück, das sowohl die ursprünglichen Bilddaten als auch den erkannten Text enthält.

```python
# Step 3: Process the scanned PDF to extract text
input_pdf_path = "YOUR_DIRECTORY/scanned_contract.pdf"
pdf_result = ocr_engine.process_pdf(input_pdf_path)
```

Wenn Sie **gescannte PDF**‑Dateien stapelweise konvertieren müssen, schleifen Sie einfach über ein Verzeichnis und rufen `process_pdf` für jede Datei auf. Die Engine verarbeitet mehrseitige PDFs out‑of‑the‑box.

---

## Schritt 3: Ergebnis als durchsuchbares PDF speichern (PDF durchsuchbar machen)

Der letzte Baustein des Puzzles ist das Persistieren der durchsuchbaren Version. Aspose OCR macht das mit einer einzigen Zeile:

```python
# Step 4: Define the output path for the searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"

# Step 5: Save the result as a searchable PDF (image + hidden text layer)
pdf_result.save_as_searchable_pdf(searchable_pdf_path)
```

Wenn Sie `contract_searchable.pdf` in einem beliebigen PDF‑Betrachter öffnen, sehen Sie das ursprüngliche gescannte Bild, können aber nun **nach jedem Wort** suchen, das die OCR‑Engine erkannt hat. Die versteckte Textebene ist für das Auge unsichtbar, aber vollständig indexierbar.

---

### Vollständiges Skript – Bereit zum Ausführen

Unten finden Sie das komplette, ausführbare Beispiel. Kopieren Sie es in eine Datei namens `make_searchable.py` und passen Sie die Pfade an Ihre Umgebung an.

```python
# make_searchable.py
# -------------------------------------------------
# Complete script to OCR a scanned PDF and make it searchable
# -------------------------------------------------

import os
import asposeocr as ocr

def ocr_to_searchable(input_path: str, output_path: str, language=ocr.Language.ENGLISH):
    """
    Convert a scanned PDF into a searchable PDF.
    
    Parameters
    ----------
    input_path : str
        Path to the scanned PDF file.
    output_path : str
        Destination path for the searchable PDF.
    language : ocr.Language, optional
        OCR language model (default is English).
    """
    if not os.path.isfile(input_path):
        raise FileNotFoundError(f"Input file not found: {input_path}")

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = language

    # Process the PDF (extracts images + hidden text)
    result = engine.process_pdf(input_path)

    # Save as searchable PDF
    result.save_as_searchable_pdf(output_path)
    print(f"✅ Searchable PDF saved to: {output_path}")

if __name__ == "__main__":
    # Example usage – replace with your actual file locations
    INPUT_PDF = "YOUR_DIRECTORY/scanned_contract.pdf"
    OUTPUT_PDF = "YOUR_DIRECTORY/contract_searchable.pdf"
    ocr_to_searchable(INPUT_PDF, OUTPUT_PDF)
```

**Erwartete Ausgabe:**  
Beim Ausführen des Skripts wird eine Bestätigungszeile ausgegeben und `contract_searchable.pdf` erstellt. Öffnen Sie die Datei, drücken Sie `Ctrl + F` und geben Sie ein beliebiges Wort ein, das im ursprünglichen gescannten Bild vorkommt – Sie sollten sofort Treffer sehen.

---

## Häufige Fragen & Sonderfälle

### 1. Was, wenn das PDF mehrere Sprachen enthält?

Sie können der Engine eine Liste von Sprachen übergeben:

```python
engine.language = [ocr.Language.ENGLISH, ocr.Language.SPANISH]
```

Aspose OCR versucht, Text in beiden Sprachen auf derselben Seite zu erkennen.

### 2. Wie gehe ich mit niedrig aufgelösten Scans um?

Wenn die Quellbilder unter 150 dpi liegen, kann die OCR‑Genauigkeit leiden. Vorverarbeiten Sie das PDF mit einem Tool wie `pdfimages`, um Seiten zu extrahieren, skalieren Sie sie mit Pillow hoch und geben Sie die hochauflösenden Bilder wieder an `process_pdf` weiter.

### 3. Kann ich den Klartext extrahieren, ohne ein durchsuchbares PDF zu erstellen?

Absolut. Das `PdfResult`‑Objekt stellt eine `text`‑Eigenschaft bereit:

```python
plain_text = pdf_result.text
print(plain_text[:500])  # preview first 500 characters
```

Damit wird der **extract text pdf**‑Anwendungsfall abgedeckt, wenn Sie nur die rohen Zeichen benötigen.

### 4. Gibt es eine Möglichkeit, einen Ordner mit PDFs stapelweise zu verarbeiten?

Ja – wickeln Sie die Funktion `ocr_to_searchable` in eine einfache Schleife ein:

```python
import glob

for src in glob.glob("scans/*.pdf"):
    dst = src.replace("scans/", "searchable/").replace(".pdf", "_searchable.pdf")
    ocr_to_searchable(src, dst)
```

Jetzt können Sie **gescannte pdf**‑Dateien massenhaft mit einem einzigen Befehl **konvertieren**.

---

## Leistungstipps

- **Engine wiederverwenden**: Das Erstellen einer neuen `OcrEngine` für jede Datei verursacht zusätzlichen Aufwand. Instanziieren Sie sie einmal und nutzen Sie sie für mehrere Aufrufe.
- **Parallelverarbeitung**: Für große Stapel sollten Sie Python’s `concurrent.futures.ThreadPoolExecutor` in Betracht ziehen – Aspose OCR ist für Lese‑Operationen thread‑sicher.
- **Speichermanagement**: Wenn Sie sehr große PDFs (Hunderte Seiten) verarbeiten, rufen Sie nach jeder Datei `gc.collect()` auf, um den Speicher freizugeben.

---

## Fazit

Wir haben gezeigt, **wie man PDF OCR** in Python durchführt, diese Scans in **durchsuchbare PDFs** umwandelt und sogar **Text‑PDF** direkt extrahiert. Mit Aspose OCR erhalten Sie eine zuverlässige Engine, die mehrseitige Dokumente, mehrere Sprachen und hochgenaue Erkennung unterstützt – alles mit nur wenigen Codezeilen.

Probieren Sie es an Ihren eigenen Verträgen, Rechnungen oder archivierten Forschungsarbeiten aus. Sobald Sie die Grundlagen beherrschen, experimentieren Sie mit erweiterten Funktionen – wie benutzerdefinierten Wörterbüchern, Bildvorverarbeitung oder der Integration des Outputs in einen Volltext‑Suchindex wie Elasticsearch.

Haben Sie weitere Fragen zu **ocr scanned pdf python** oder benötigen Hilfe bei der Fehlersuche eines kniffligen Scans? Hinterlassen Sie einen Kommentar unten, und happy coding! 

--- 

![how to ocr pdf example](image-placeholder.png){alt="Beispiel für OCR von PDF"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}