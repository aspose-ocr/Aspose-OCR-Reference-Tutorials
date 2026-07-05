---
category: general
date: 2026-07-05
description: Erstelle ein durchsuchbares PDF mit Python. Erfahre, wie man ein gescanntes
  PNG OCRt, ein gescanntes Bild‑PDF konvertiert und in wenigen Minuten ein durchsuchbares
  PDF erhält.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: de
og_description: Erstellen Sie schnell durchsuchbare PDFs. Dieser Leitfaden zeigt,
  wie man ein PNG OCR‑t, ein gescanntes Bild‑PDF konvertiert und mit Python ein durchsuchbares
  PDF erzeugt.
og_title: Erstelle ein durchsuchbares PDF aus gescanntem Bild – Python OCR‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF with Python. Learn how to OCR a scanned PNG,
    convert scanned image PDF, and get a searchable PDF in minutes.
  headline: Create Searchable PDF from Scanned Image – Full Python OCR Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF
- Automation
title: Erstelle ein durchsuchbares PDF aus einem gescannten Bild – Vollständiger Python-OCR-Leitfaden
url: /de/python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Durchsuchbares PDF aus gescanntem Bild erstellen – Vollständige Python OCR Anleitung

Haben Sie sich schon einmal gefragt, wie man **durchsuchbare PDFs** aus einem gescannten Bild erstellt, ohne teure Software zu bezahlen? Sie sind nicht allein. In vielen Büros kommen PDFs als flache Bilder – schwer zu durchsuchen, unmöglich zu kopieren‑einzufügen und ein Albtraum für Compliance‑Audits. Die gute Nachricht? Mit ein paar Zeilen Python können Sie dieses statische PNG in ein voll durchsuchbares PDF verwandeln, und der Prozess ist einfacher, als Sie denken.

In diesem Tutorial gehen wir ein komplettes **OCR‑Erkennungsbeispiel** durch, von der Installation der richtigen Bibliothek bis zum Schreiben der finalen PDF‑Datei. Am Ende wissen Sie genau, wie Sie **gescannte Bild‑PDFs** konvertieren, wie Sie **ocr pdf programmatisch** ausführen und Sie besitzen ein wiederverwendbares Skript, das Sie in jedes Projekt einbinden können.

## Was Sie lernen werden

- Installation und Konfiguration einer Python‑OCR‑Bibliothek (wir verwenden `pytesseract` und `pdf2image`).
- Initialisierung der OCR‑Engine und Festlegung der Sprache.
- Laden eines gescannten PNGs (oder eines beliebigen Bildes) und Ausführen von OCR darauf.
- Umwandlung des OCR‑Ergebnisses in ein **durchsuchbares PDF** (Byte‑Array) und Speichern.
- Tipps zum Umgang mit mehrseitigen Dokumenten, verschiedenen Sprachen und häufigen Fallstricken.

Vorkenntnisse in OCR sind nicht erforderlich – nur eine funktionierende Python 3‑Umgebung und ein wenig Neugier.

---

## Durchsuchbares PDF erstellen – Überblick

Unten sehen Sie ein hoch‑level Diagramm der Schritte, die wir implementieren werden.  

![Create searchable PDF workflow diagram](https://example.com/flowchart.png "Create searchable PDF workflow diagram")

*Alt‑Text: Diagramm des Workflows zum Erstellen eines durchsuchbaren PDFs, das Engine‑Initialisierung, Bild‑Laden, OCR‑Erkennung, PDF‑Konvertierung und Dateischreiben zeigt.*

---

## Schritt 1: Initialisierung der OCR‑Engine (how to ocr pdf)

Warum müssen wir überhaupt etwas initialisieren? Die OCR‑Engine ist das Gehirn, das Pixel‑Muster als Zeichen interpretiert. Indem wir eine Engine‑Instanz erstellen und explizit die Sprache setzen, teilen wir der Bibliothek mit, welches Alphabet zu erwarten ist, was die Genauigkeit dramatisch erhöht.

```python
import pytesseract
from pdf2image import convert_from_path
from PIL import Image
import io

# Ensure Tesseract is on your PATH or provide the executable location
pytesseract.pytesseract.tesseract_cmd = r"/usr/local/bin/tesseract"  # adjust as needed

# Define the language – ENGLISH is the default, but you can add more (e.g., 'fra' for French)
ocr_language = "eng"
```

**Pro‑Tipp:** Wenn Sie Dokumente in mehreren Sprachen OCR‑en müssen, installieren Sie die entsprechenden Sprachpakete für Tesseract und übergeben Sie eine Liste wie `"eng+spa"` an `ocr_language`.

---

## Schritt 2: Das gescannte Bild laden (convert scanned image pdf)

Der nächste Baustein ist, die Bilddaten nach Python zu holen. Egal, ob Sie ein einzelnes PNG oder ein mehrseitiges TIFF haben, die Klasse `PIL.Image` kann es öffnen. Wenn Sie von einem PDF ausgehen, das bereits gescannte Bilder enthält, konvertiert `pdf2image` jede Seite für uns in ein Bild.

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**Warum das wichtig ist:** Das Laden des Bildes als Pillow‑Objekt gibt uns Zugriff auf die rohen Pixeldaten, die die OCR‑Engine benötigt. Würden wir diesen Schritt überspringen und rohe Bytes direkt übergeben, kämen Fehler auf.

---

## Schritt 3: OCR‑Erkennung auf dem Bild durchführen (ocr recognition example)

Jetzt kommt der spaßige Teil – die Engine den Text lesen lassen. `pytesseract.image_to_pdf_or_hocr` liefert einen PDF‑Byte‑Stream, der bereits eine unsichtbare Textebene enthält, genau das, was wir für ein **durchsuchbares PDF** benötigen.

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**Randfall:** Wenn Ihr Bild einen niedrigen Kontrast hat, sollten Sie vor dem OCR eine einfache Schwellenwert‑Operation anwenden:

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

Dieser winzige Vorverarbeitungsschritt kann die Genauigkeit dramatisch steigern.

---

## Schritt 4: Die PDF‑Bytes in eine Datei schreiben (convert png searchable pdf)

Die OCR‑Bibliothek gibt uns ein Byte‑Array – denken Sie daran als den rohen Inhalt einer PDF‑Datei. Jetzt müssen wir diese Bytes nur noch auf die Festplatte schreiben.

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**Was Sie sehen werden:** Öffnen Sie die resultierende Datei in einem beliebigen PDF‑Betrachter und suchen Sie nach einem Wort, von dem Sie wissen, dass es im Originalbild vorkommt. Die Hervorhebung sollte sofort zur richtigen Stelle springen und beweisen, dass die unsichtbare Textebene funktioniert.

---

## Schritt 5: Erweiterung für mehrseitige Dokumente (convert scanned image pdf)

Echte Verträge erstrecken sich oft über mehrere Seiten. Um **gescannte Bild‑PDFs** zu **convert scanned image pdf** Dateien zu konvertieren, die mehrere Seiten enthalten, iterieren Sie über jede Seite, OCR‑en Sie sie und fügen die resultierenden PDFs zusammen.

```python
def ocr_image_to_pdf(image_obj, lang="eng"):
    """Helper that returns PDF bytes for a single image."""
    return pytesseract.image_to_pdf_or_hocr(image_obj, lang=lang, extension='pdf')

def merge_pdfs(pdf_bytes_list):
    """Combine multiple PDF byte streams into one."""
    from PyPDF2 import PdfMerger
    merger = PdfMerger()
    for i, pdf_bytes in enumerate(pdf_bytes_list):
        merger.append(io.BytesIO(pdf_bytes))
    output = io.BytesIO()
    merger.write(output)
    merger.close()
    return output.getvalue()

# Example: convert a multi‑page scanned PDF to searchable PDF
pages = convert_from_path("YOUR_DIRECTORY/scanned_contract.pdf", dpi=300)
pdf_parts = [ocr_image_to_pdf(p, lang=ocr_language) for p in pages]
final_pdf = merge_pdfs(pdf_parts)

with open("YOUR_DIRECTORY/contract_searchable.pdf", "wb") as f:
    f.write(final_pdf)

print("✅ Multi‑page searchable PDF created.")
```

**Warum zusammenführen?** Jeder Aufruf von `image_to_pdf_or_hocr` erzeugt ein eigenständiges PDF. Das Zusammenführen stellt sicher, dass das Enddokument die ursprüngliche Seitenreihenfolge beibehält.

---

## Häufige Fallstricke & Lösungen

| Symptom | Wahrscheinliche Ursache | Lösung |
|---------|--------------------------|--------|
| Kein durchsuchbarer Text nach dem Öffnen des PDFs | Tesseract findet keine Zeichen (leere Ausgabe) | Bildqualität prüfen, DPI erhöhen oder Vorverarbeitung anwenden (Kontrast, Binärisierung). |
| verfälschte Zeichen (z. B. �) | Falsches Sprachpaket oder fehlende Fonts | Das korrekte Sprachpaket installieren (`tesseract‑lang‑eng`) und sicherstellen, dass `ocr_language` übereinstimmt. |
| PDF‑Dateigröße riesig (>10 MB für ein einseitiges Bild) | Verlustfreies PNG als Quelle; OCR fügt ein hochauflösendes Bild hinzu | Bild vor OCR verkleinern (`image.thumbnail((1240, 1754))` für A4). |
| Skript stürzt unter Windows mit “tesseract.exe not found” ab | Tesseract‑Binary nicht im PATH | `pytesseract.pytesseract.tesseract_cmd = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"` hinzufügen (Pfad anpassen). |

---

## Vollständiges, sofort ausführbares Skript

Alles zusammengeführt, hier ein einzelnes File, das Sie kopieren und ausführen können:

```python
#!/usr/bin/env python3
"""
create_searchable_pdf.py
A complete example that converts a scanned PNG (or PDF) into a searchable PDF using Tesseract OCR.
"""

import io
import sys
from pathlib import Path

import pytesseract
from pdf2image import convert_from_path
from PIL import Image
from PyPDF2 import PdfMerger

# -------------------- Configuration --------------------
# Adjust these paths for your environment
TESSERACT_CMD = r"/usr/local/bin/tesseract"   # macOS/Linux
# TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"  # Windows
OCR_LANGUAGE = "eng"                         # Add '+spa' for Spanish, etc.
INPUT_PATH = Path("YOUR_DIRECTORY/scanned_agreement.png")
OUTPUT_PATH = Path("YOUR_DIRECTORY/agreement_searchable.pdf")
# -------------------------------------------------------

# Point pytesseract at the executable
pytesseract.pytesseract.tesseract_cmd = TESSERACT_CMD

def load_image(path: Path) -> Image.Image:
    """Load an image from disk; supports PNG, JPG, TIFF."""
    if not path.is_file():
        sys.exit(f"❌ File not found: {path}")
    return Image.open(path)

def ocr_to_pdf_bytes(img: Image.Image, lang: str = OCR_LANGUAGE) -> bytes:
    """Run OCR on a Pillow image and return PDF bytes with hidden text."""
    return pytesseract.image_to_pdf_or_hocr(img, lang=lang, extension='pdf')

def write_pdf(data: bytes, dest: Path):
    """Write PDF byte stream to a file."""
    dest.parent.mkdir(parents=True, exist_ok=True)
    with open(dest, "wb") as f:
        f.write(data)
    print(f"✅ Searchable PDF saved to {dest}")

def main():
    # Load the scanned image
    image = load_image(INPUT_PATH)

    # Optional: improve contrast for low‑quality scans
    # image = image.convert('L').point(lambda x: 0 if x < 128 else 255, '1')

    # OCR → PDF bytes
    pdf_bytes = ocr_to_pdf_bytes(image)

    # Save the result
    write_pdf(pdf_bytes, OUTPUT_PATH)

if __name__ == "__main__":
    main()
```

Speichern Sie dies als `create_searchable_pdf.py`, ersetzen Sie die Platzhalter durch echte Pfade und führen Sie es aus:

```bash
python create_searchable_pdf.py
```

Sie sollten ein


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}