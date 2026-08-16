---
category: general
date: 2026-03-18
description: Erstellen Sie ein durchsuchbares PDF aus Ihren gescannten Dateien mit
  Aspose OCR. Erfahren Sie, wie Sie gescannte PDFs konvertieren, Text aus PDFs extrahieren
  und Text‑PDFs schnell erkennen.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- extract text from pdf
- recognize text pdf
- convert image pdf
language: de
og_description: Erstellen Sie sofort ein durchsuchbares PDF. Befolgen Sie diese Anleitung,
  um gescannte PDFs zu konvertieren, Text aus PDFs zu extrahieren und Text‑PDFs mit
  Aspose OCR zu erkennen.
og_title: Durchsuchbares PDF erstellen – Schritt für Schritt mit Aspose OCR
tags:
- OCR
- PDF
- Aspose
- Python
title: Durchsuchbare PDF erstellen – Gescanntes PDF mit Aspose OCR konvertieren
url: /de/python-java/general/create-searchable-pdf-convert-scanned-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Durchsuchbares PDF erstellen – Schritt‑für‑Schritt‑Anleitung  

Haben Sie jemals **durchsuchbare PDFs** aus einem Stapel gescannter Seiten erstellen müssen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein – die meisten Entwickler stoßen an diese Grenze, sobald der erste Scan auf ihrem Server landet.  

Die gute Nachricht ist, dass Sie mit Aspose OCR **convert scanned pdf** in nur wenigen Zeilen durchführen, **extract text from pdf** zur Validierung extrahieren und sogar **recognize text pdf** on the fly. In diesem Tutorial führen wir Sie durch den gesamten Prozess, von der Installation der Bibliothek bis zum Speichern eines vollständig durchsuchbaren Dokuments, und geben ein paar Tipps zum Umgang mit **convert image pdf** Edge Cases.

## Was Sie erreichen werden  

* Laden Sie ein gescanntes PDF (oder ein PDF, das nur Bilder enthält) in Aspose OCR.  
* Teilen Sie der Engine mit, welche Seiten verarbeitet werden sollen – praktisch, wenn Sie nur einen Teil benötigen.  
* Betten Sie die OCR-Ergebnisse wieder in die Originaldatei ein, sodass die Ausgabe ein echtes **searchable PDF** ist.  
* Verifizieren Sie den Vorgang, indem Sie die Seitenzahl ausgeben und, falls gewünscht, den extrahierten Text ausgeben.  

Keine externen Dienste, keine versteckte Magie – nur reines Python und Aspose’s eigene API.

## Voraussetzungen  

* Python 3.8 oder neuer.  
* `aspose-ocr`‑Paket – installieren Sie es mit `pip install aspose-ocr`.  
* Eine gescannte PDF‑Datei (oder ein PDF, das nur Bilder enthält).  
* Grundlegende Erfahrung mit Python‑Skripting.  

Wenn Sie das bereits haben, großartig – lassen Sie uns eintauchen.

<img src="searchable-pdf-workflow.png" alt="Durchsuchbares PDF erstellen Workflow">  

*(Illustration der OCR-Pipeline – nicht für den Code erforderlich, aber hilfreich für visuelle Lernende.)*

## Schritt 1 – OCR‑Engine initialisieren  

Zuerst benötigen Sie eine `OcrEngine`‑Instanz. Denken Sie daran als das Gehirn, das jedes Pixel liest und in Unicode‑Zeichen umwandelt.

```python
# Step 1: Import the required classes and create the engine
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

# Initialize the OCR engine – this object holds all settings
ocr_engine = OcrEngine()
```

**Warum das wichtig ist:** Ohne die Engine können Sie keine Optionen festlegen oder die Erkennung ausführen. Eine frühzeitige Initialisierung gibt Ihnen außerdem einen Ort, um später benutzerdefinierte Wörterbücher anzuhängen.

## Schritt 2 – Quell‑PDF laden  

Aspose OCR kann PDFs direkt lesen, das bedeutet, Sie müssen jede Seite nicht selbst rasterisieren. Zeigen Sie der Engine einfach auf die Datei.

```python
# Step 2: Load the scanned PDF (replace with your actual path)
input_path = "YOUR_DIRECTORY/input.pdf"
ocr_engine.setImageFromFile(input_path)
```

*Pro‑Tipp:* Wenn das PDF sehr groß ist, sollten Sie es aus einem Stream laden, um ein Sperren der Datei auf dem Datenträger zu vermeiden.

## Schritt 3 – PDF‑Erkennungsoptionen konfigurieren  

Hier kommen die sekundären Schlüsselwörter zum Einsatz. Sie können der Engine mitteilen, **convert scanned pdf** nur auf bestimmten Seiten auszuführen, den erkannten Text einzubetten oder sogar die Originalbilder unverändert zu lassen.

```python
# Step 3: Create and configure PDF recognition options
pdf_options = PdfRecognitionOptions()
pdf_options.setEmbedRecognisedText(True)          # Makes the PDF searchable
pdf_options.setPageRange(1, 3)                    # Process only pages 1‑3 (optional)
pdf_options.setTextExtractionMode(True)          # Enables text extraction for verification
```

**Warum das wichtig ist:**  
* `setEmbedRecognisedText(True)` ist der Schlüssel, um ein Raster‑PDF in ein **searchable PDF** zu verwandeln.  
* `setPageRange` hilft Ihnen, **convert image pdf** selektiv auszuführen – nützlich für große Dokumente, bei denen Sie nur wenige Seiten OCR‑verarbeiten müssen.  
* Das Aktivieren der Textextraktion ermöglicht es Ihnen später, **extract text from pdf** durchzuführen, ohne einen Viewer zu öffnen.

## Schritt 4 – Optionen an die Engine anhängen  

Jetzt binden Sie die Optionen an die Engine. Dieser Schritt wird leicht übersehen, aber das Überspringen führt dazu, dass die Engine mit den Standardeinstellungen läuft (kein durchsuchbarer Text).

```python
# Step 4: Attach the options to the OCR engine
ocr_engine.setPdfRecognitionOptions(pdf_options)
```

## Schritt 5 – OCR auf den ausgewählten Seiten ausführen  

Wenn alles verbunden ist, erfolgt die eigentliche Erkennung mit einem einzigen Methodenaufruf.

```python
# Step 5: Perform OCR – this may take a few seconds per page
ocr_result = ocr_engine.recognize()
```

Wenn Sie ein mehrmegabytegroßes Dokument verarbeiten, sollten Sie dies in einen try/except‑Block einbetten, um `OcrException` abzufangen und die problematische Seite zu protokollieren.

## Schritt 6 – Ergebnis überprüfen  

Ein schneller Plausibilitätstest besteht darin, auszugeben, wie viele Seiten die Engine verarbeitet hat. Sie können auch den Rohtext abrufen, falls Sie **extract text from pdf** für weitere Analysen benötigen.

```python
# Step 6: Show how many pages were processed
print("Pages processed:", ocr_result.getPageCount())

# Optional: dump extracted text for the first page (helps debugging)
first_page_text = ocr_result.getPageText(0)   # 0‑based index
print("\n--- Extracted Text (Page 1) ---\n", first_page_text[:500])  # show first 500 chars
```

**Warum das wichtig ist:** Die Anzeige der Seitenzahl bestätigt, dass `setPageRange` funktioniert hat, und das Snippet des extrahierten Textes beweist, dass die OCR tatsächlich Zeichen erkannt hat.

## Schritt 7 – Durchsuchbares PDF speichern  

Zum Schluss schreiben Sie die Ausgabe zurück auf die Festplatte. Die Konstante `ImageFormats.PDF` weist Aspose an, die Datei als PDF zu behalten, jetzt angereichert mit durchsuchbarem Text.

```python
# Step 7: Save the searchable PDF
output_path = "YOUR_DIRECTORY/output.pdf"
ocr_engine.save(output_path, ImageFormats.PDF)

print(f"Searchable PDF saved to: {output_path}")
```

Öffnen Sie die resultierende Datei in einem beliebigen PDF‑Reader und führen Sie eine Textsuche durch – voilà, Sie haben **created searchable pdf**!

## Umgang mit häufigen Sonderfällen  

### Wenn die Quelle ein *nur‑Bild*‑PDF ist  

Wenn Ihr Eingabe‑PDF nur Bilder enthält (keine Textebene), funktioniert derselbe Code – stellen Sie nur sicher, dass `setEmbedRecognisedText(True)` aktiviert bleibt. Sie können außerdem die DPI für bessere Genauigkeit erhöhen:

```python
pdf_options.setResolution(300)  # 300 DPI gives sharper OCR results
```

### Umgang mit mehreren Sprachen  

Aspose OCR unterstützt Sprachpakete. Laden Sie eine Sprache, bevor Sie `recognize()` aufrufen:

```python
ocr_engine.setLanguage("spa")   # Spanish language pack
```

### Große Dokumente  

Die Verarbeitung eines 500‑seitigen gescannten PDFs kann speicherintensiv sein. Teilen Sie den Auftrag:

1. Durchlaufen Sie Seitenbereiche (`setPageRange(start, end)`).  
2. Speichern Sie jeden Abschnitt als temporäres durchsuchbares PDF.  
3. Fügen Sie die Abschnitte mit `PdfMerger` (einer weiteren Aspose‑Komponente) zusammen.

## Vollständiges funktionierendes Beispiel (Alle Schritte zusammen)

```python
# Full script – create searchable PDF from a scanned document
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

def create_searchable_pdf(input_file: str, output_file: str, start_page: int = 1, end_page: int = 0):
    """
    Convert a scanned or image‑only PDF into a searchable PDF.
    :param input_file: Path to the source PDF.
    :param output_file: Destination path for the searchable PDF.
    :param start_page: First page to process (1‑based). Default = 1.
    :param end_page: Last page to process. 0 means “till the end”.
    """
    # Initialize engine
    ocr_engine = OcrEngine()
    ocr_engine.setImageFromFile(input_file)

    # Set options
    pdf_opts = PdfRecognitionOptions()
    pdf_opts.setEmbedRecognisedText(True)          # embed searchable text
    pdf_opts.setTextExtractionMode(True)           # allow text extraction
    if end_page > 0:
        pdf_opts.setPageRange(start_page, end_page)  # selective processing
    else:
        pdf_opts.setPageRange(start_page, start_page)  # process from start_page onward

    # Attach options
    ocr_engine.setPdfRecognitionOptions(pdf_opts)

    # Run OCR
    result = ocr_engine.recognize()
    print("Pages processed:", result.getPageCount())

    # Optional verification
    print("\nSample extracted text (first page):")
    print(result.getPageText(0)[:300])

    # Save searchable PDF
    ocr_engine.save(output_file, ImageFormats.PDF)
    print(f"Searchable PDF saved to: {output_file}")

if __name__ == "__main__":
    create_searchable_pdf(
        input_file="YOUR_DIRECTORY/input.pdf",
        output_file="YOUR_DIRECTORY/output.pdf",
        start_page=1,
        end_page=3   # change or set to 0 to process the whole file
    )
```

Das Ausführen dieses Skripts liefert Ihnen ein **searchable PDF**, das Sie in Adobe Reader, Chrome oder jedem PDF‑Viewer öffnen und sofort nach Wörtern durchsuchen können.

## Fazit  

Sie haben nun eine vollständige End‑zu‑End‑Lösung, um **create searchable PDF**‑Dateien mit Aspose OCR zu erstellen. Vom Laden der Quelle, über das Konfigurieren von Optionen, die **convert scanned pdf** ermöglichen, bis hin zum Extrahieren und Verifizieren von Text und schließlich dem Speichern des durchsuchbaren Ergebnisses – jeder Schritt ist abgedeckt.  

Als Nächstes möchten Sie vielleicht **convert image pdf**‑Szenarien erkunden, bei denen die Quelle eine Reihe von JPEGs ist, die in ein PDF gepackt wurden, oder tiefer in sprachspezifische OCR eintauchen, um die Genauigkeit bei mehrsprachigen Dokumenten zu verbessern. In jedem Fall bleibt das Muster gleich: Optionen setzen, `recognize()` ausführen und speichern.  

Fühlen Sie sich frei zu experimentieren – ändern Sie den Seitenbereich, passen Sie die DPI an oder schließen Sie ein benutzerdefiniertes Wörterbuch ein. Wenn Sie auf Probleme stoßen, hinterlassen Sie unten einen Kommentar oder prüfen Sie die offiziellen Aspose‑Dokumente für die neuesten API‑Nuancen. Viel Spaß beim OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}