---
category: general
date: 2026-05-31
description: Erstelle ein durchsuchbares PDF aus gescannten Bildern mit Python‑OCR.
  Erfahre, wie du ein gescanntes Bild‑PDF konvertierst, TIFF in PDF umwandelst und
  in wenigen Minuten eine OCR‑Textschicht hinzufügst.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- convert tiff to pdf
- how to run OCR
- add OCR text layer
language: de
og_description: Erstelle sofort durchsuchbare PDFs. Diese Anleitung zeigt, wie man
  OCR ausführt, gescannte Bild‑PDFs konvertiert und eine OCR‑Textschicht mit einem
  einzigen Python‑Skript hinzufügt.
og_title: Erstelle durchsuchbare PDF mit Python – Komplettes Tutorial
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  headline: Create Searchable PDF with Python – Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  name: Create Searchable PDF with Python – Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: 1️⃣ Can I process multi‑page PDFs?
    text: Yes. Use `ocr_engine.load_image("file.pdf")` and then loop over each page
      with `ocr_engine.recognize(pdf_save_options, page_number)`. The library will
      automatically generate a multi‑page searchable PDF.
  - name: 2️⃣ What if my source file is a high‑resolution TIFF (300 dpi+)?
    text: 'Higher DPI yields better OCR accuracy but also larger memory usage. If
      you hit a `MemoryError`, downscale the image first:'
  - name: 3️⃣ How do I change the language of the OCR?
    text: 'Set the `language` property on the engine before loading the image:'
  - name: 4️⃣ What if I need to keep the original image quality?
    text: The `PdfSaveOptions` class has a `compression` property. Set it to `PdfCompression.None`
      to preserve the raster data exactly as it was.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Document Automation
title: Durchsuchbares PDF mit Python erstellen – Schritt‑für‑Schritt‑Anleitung
url: /de/python-java/general/create-searchable-pdf-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Erstellen durchsuchbare PDF mit Python – Schritt‑für‑Schritt-Anleitung

Haben Sie sich jemals gefragt, wie man **create searchable PDF** aus einer gescannten Seite erstellt, ohne Dutzende Werkzeuge zu jonglieren? Sie sind nicht allein. In vielen Büroabläufen landet ein gescanntes TIFF oder JPEG auf einem gemeinsamen Laufwerk, und die nächste Person muss den Text manuell copy‑pasten – schmerzhaft, fehleranfällig und zeitaufwendig.  

In diesem Tutorial gehen wir eine saubere, programmatische Lösung durch, die es Ihnen ermöglicht, **convert scanned image PDF**, **convert TIFF to PDF** und **add OCR text layer** in einem Schritt. Am Ende haben Sie ein einsatzbereites Skript, das OCR ausführt, den versteckten Text einbettet und ein durchsuchbares PDF ausgibt, das Sie indexieren, durchsuchen oder mit Vertrauen teilen können.

## Was Sie benötigen

- Python 3.9+ (jede aktuelle Version funktioniert)
- Pakete `aspose-ocr` und `aspose-pdf` (installiert über `pip install aspose-ocr aspose-pdf`)
- Eine gescannte Bilddatei (`.tif`, `.png`, `.jpg` oder sogar eine PDF‑Seite, die nur ein Bild enthält)
- Ein bescheidener Arbeitsspeicher (die OCR‑Engine ist leichtgewichtig; selbst ein Laptop bewältigt das)

> **Pro‑Tipp:** Wenn Sie Windows verwenden, ist der einfachste Weg, die Pakete zu erhalten, den Befehl in einem erhöhten PowerShell‑Fenster auszuführen.

```bash
pip install aspose-ocr aspose-pdf
```

Jetzt, da die Voraussetzungen erledigt sind, tauchen wir in den Code ein.

## Schritt 1: OCR‑Engine‑Instanz erstellen – *create searchable pdf*

Das Erste, was wir tun, ist die OCR‑Engine zu starten. Stellen Sie sich sie als das Gehirn vor, das jedes Pixel liest und in Zeichen umwandelt.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine – this is the core of the create searchable pdf process
ocr_engine = OcrEngine()
```

> **Warum das wichtig ist:** Die Engine nur einmal zu initialisieren hält den Speicherverbrauch niedrig. Wenn Sie `OcrEngine()` in einer Schleife für jede Seite aufrufen würden, würden Sie schnell an Ressourcenmangel geraten.

## Schritt 2: Gescanntes Bild laden – *convert tiff to pdf* & *convert scanned image pdf*

Als Nächstes zeigen Sie die Engine auf die Datei, die Sie verarbeiten möchten. Die API akzeptiert jedes Rasterbild, sodass ein TIFF genauso gut funktioniert wie ein JPEG.

```python
# Load the image you want to OCR. Replace the path with your own file location.
ocr_engine.load_image("YOUR_DIRECTORY/scanned_page.tif")
```

Falls Sie ein PDF haben, das nur ein gescanntes Bild enthält, können Sie weiterhin `load_image` verwenden, da Aspose die erste Seite automatisch extrahiert.

## Schritt 3: PDF‑Speicheroptionen vorbereiten – *add OCR text layer*

Hier konfigurieren wir, wie das endgültige PDF aussehen soll. Das entscheidende Flag ist `create_searchable_pdf`; wird es auf `True` gesetzt, weist dies die Bibliothek an, eine unsichtbare Textebene einzubetten, die den visuellen Inhalt widerspiegelt.

```python
from aspose.pdf import PdfSaveOptions

pdf_save_options = PdfSaveOptions()
pdf_save_options.create_searchable_pdf = True   # embed OCR text layer
pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"
```

> **Was die Textebene bewirkt:** Wenn Sie die resultierende Datei in Adobe Reader öffnen und versuchen, Text zu markieren, sehen Sie die versteckten Zeichen. Suchmaschinen können sie ebenfalls indexieren – ideal für Compliance oder Archivierung.

## Schritt 4: OCR ausführen und speichern – *how to run OCR* in a single call

Jetzt geschieht die Magie. Ein Methodenaufruf führt die Erkennungs‑Engine aus und schreibt das durchsuchbare PDF auf die Festplatte.

```python
# Run OCR and generate the searchable PDF in one go
ocr_engine.recognize(pdf_save_options)

print("PDF saved as searchable PDF.")
```

Die Methode `recognize` gibt ein Status‑Objekt zurück, das Sie auf Fehler prüfen können, aber für die meisten einfachen Szenarien reicht der obige einfache Aufruf aus.

### Erwartete Ausgabe

Das Ausführen des Skripts gibt Folgendes aus:

```
PDF saved as searchable PDF.
```

Wenn Sie `scanned_page_searchable.pdf` öffnen, werden Sie feststellen, dass Sie Text auswählen, copy‑pasten und sogar eine `Ctrl+F`‑Suche durchführen können. Das ist das Kennzeichen eines **create searchable pdf** Workflows.

## Vollständiges funktionierendes Skript

Unten finden Sie das vollständige, sofort ausführbare Skript. Ersetzen Sie einfach die Platzhalter‑Pfade durch Ihre tatsächlichen Dateipfade.

```python
# ------------------------------------------------------------
# create_searchable_pdf.py – Convert scanned image to searchable PDF
# ------------------------------------------------------------

from aspose.ocr import OcrEngine
from aspose.pdf import PdfSaveOptions

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load image (TIFF, JPEG, PNG, or scanned PDF page)
    image_path = "YOUR_DIRECTORY/scanned_page.tif"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure PDF output – embed OCR text layer
    pdf_save_options = PdfSaveOptions()
    pdf_save_options.create_searchable_pdf = True
    pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"

    # 4️⃣ Run OCR and write searchable PDF
    ocr_engine.recognize(pdf_save_options)

    print("PDF saved as searchable PDF.")

if __name__ == "__main__":
    main()
```

Speichern Sie dies als `create_searchable_pdf.py` und führen Sie es aus:

```bash
python create_searchable_pdf.py
```

## Häufige Fragen & Sonderfälle

### 1️⃣ Kann ich mehrseitige PDFs verarbeiten?

Ja. Verwenden Sie `ocr_engine.load_image("file.pdf")` und iterieren Sie dann über jede Seite mit `ocr_engine.recognize(pdf_save_options, page_number)`. Die Bibliothek erzeugt automatisch ein mehrseitiges durchsuchbares PDF.

### 2️⃣ Was, wenn meine Quelldatei ein hochauflösendes TIFF (300 dpi+) ist?

Eine höhere DPI führt zu besserer OCR‑Genauigkeit, aber auch zu höherem Speicherverbrauch. Wenn Sie einen `MemoryError` erhalten, skalieren Sie das Bild zuerst herunter:

```python
from PIL import Image
img = Image.open(image_path)
img = img.resize((int(img.width * 0.5), int(img.height * 0.5)), Image.ANTIALIAS)
img.save("temp.tif")
ocr_engine.load_image("temp.tif")
```

### 3️⃣ Wie ändere ich die Sprache der OCR?

Setzen Sie die Eigenschaft `language` auf der Engine, bevor Sie das Bild laden:

```python
ocr_engine.language = "fra"   # French
```

Eine vollständige Liste der unterstützten Sprachcodes finden Sie in der Aspose‑Dokumentation.

### 4️⃣ Was, wenn ich die ursprüngliche Bildqualität beibehalten muss?

Die Klasse `PdfSaveOptions` verfügt über eine Eigenschaft `compression`. Setzen Sie sie auf `PdfCompression.None`, um die Rasterdaten exakt wie ursprünglich zu erhalten.

```python
pdf_save_options.compression = "None"
```

## Tipps für produktionsreife Bereitstellungen

- **Batch‑Verarbeitung:** Verpacken Sie die Kernlogik in einer Funktion, die eine Liste von Dateipfaden akzeptiert. Protokollieren Sie jeden Erfolg/Fehlschlag in einer CSV für Prüfpfade.
- **Parallelität:** Verwenden Sie `concurrent.futures.ThreadPoolExecutor`, um OCR auf mehreren Kernen auszuführen. Denken Sie daran, dass jeder Thread seine eigene `OcrEngine`‑Instanz benötigt.
- **Sicherheit:** Wenn Sie sensible Dokumente verarbeiten, führen Sie das Skript in einer sandbox‑Umgebung aus und löschen Sie die temporären Dateien sofort nach der Verarbeitung.

## Fazit

Sie wissen jetzt, wie man **create searchable PDF** Dateien aus gescannten Bildern mit einem knappen Python‑Skript erstellt. Durch das Initialisieren einer OCR‑Engine, das Laden eines TIFF (oder eines beliebigen Rasters), das Konfigurieren von `PdfSaveOptions` zum **add OCR text layer** und schließlich das Aufrufen von `recognize` wird die gesamte **convert scanned image pdf** und **convert TIFF to PDF** Pipeline zu einem einzigen, wiederholbaren Befehl.

Nächste Schritte? Versuchen Sie, dieses Skript mit einem Datei‑Watcher zu verketten, sodass jeder neue Scan, der in einen Ordner gelegt wird, automatisch durchsuchbar wird. Oder experimentieren Sie mit verschiedenen OCR‑Sprachen, um mehrsprachige Archive zu unterstützen. Der Himmel ist die Grenze, wenn Sie OCR mit PDF‑Erstellung kombinieren.

Haben Sie weitere Fragen zu **how to run OCR** in anderen Sprachen oder Frameworks? Hinterlassen Sie unten einen Kommentar und viel Spaß beim Programmieren! 

![Diagramm, das den Ablauf von gescanntem Bild → OCR‑Engine → durchsuchbarem PDF (create searchable pdf) zeigt](searchable-pdf-flow.png "Ablaufdiagramm für create searchable pdf")


## Was sollten Sie als Nächstes lernen?

- [Wie man PDF in .NET mit Aspose.OCR OCR‑t](/ocr/english/net/text-recognition/recognize-pdf/)
- [Bilder zu PDF in C# konvertieren – Mehrseitiges OCR‑Ergebnis speichern](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Wie man Bildtext mit Sprache mittels Aspose.OCR OCR‑t](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}