---
category: general
date: 2026-04-26
description: Wie man OCR bei gescannten PDFs verwendet, Text aus PDFs extrahiert,
  OCR auf PDFs ausführt und gescannte PDFs in durchsuchbare Dateien umwandelt – in
  wenigen Schritten.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: de
og_description: 'Wie man OCR in Python verwendet: Erfahren Sie, wie Sie Text aus PDFs
  extrahieren, OCR auf PDFs anwenden und gescannte PDFs in durchsuchbare Dokumente
  umwandeln.'
og_title: Wie man OCR verwendet – Schnellleitfaden zum Extrahieren von Text aus PDF
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Wie man OCR verwendet – Text aus PDF mit Python extrahieren
url: /de/python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR verwendet – Text aus PDF mit Python extrahieren

Haben Sie sich jemals gefragt **wie man OCR verwendet**, um Text aus einem gescannten Vertrag, einer Quittung oder einem E‑Book zu extrahieren? Sie sind nicht allein. In vielen realen Projekten ist das PDF, das Sie erhalten, nur ein Bild, und ohne OCR können Sie dessen Inhalt nicht durchsuchen, indexieren oder analysieren.  

In diesem Tutorial führen wir Sie durch ein vollständiges, ausführbares Beispiel, das **zeigt, wie man OCR verwendet**, **wie man Text aus PDF extrahiert** und warum Sie **gescannte PDF**‑Dateien in durchsuchbare Dokumente umwandeln möchten. Wir behandeln außerdem die feine Kunst des **Ladens von PDF als Bild**, damit die OCR‑Engine jede Seite klar erkennen kann.

> **Schnelle Vorschau:** Am Ende haben Sie ein Skript, das ein mehrseitiges PDF lädt, OCR auf jeder Seite ausführt und den erkannten Text ausgibt – ohne externe Dienste.

## Was Sie benötigen

- Python 3.9+ (jede aktuelle Version funktioniert)
- `aocr`-Paket (oder jede kompatible OCR‑Bibliothek, die `OcrEngine` und `Image.load` bereitstellt)
- Eine gescannte PDF‑Datei, die Sie verarbeiten möchten (z. B. `contract.pdf`)
- Ein bescheidener Arbeitsspeicher (≈ 200 MB pro 100‑Seiten‑PDF ist in der Regel ausreichend)

Wenn Sie die OCR‑Bibliothek noch nicht installiert haben, führen Sie aus:

```bash
pip install aocr
```

> **Pro‑Tipp:** Verwenden Sie eine virtuelle Umgebung, um Ihre Abhängigkeiten übersichtlich zu halten.

## Schritt 1: PDF als Bild laden – Das erste Puzzleteil

Bevor irgendeine OCR stattfinden kann, muss das PDF als Bild dargestellt werden. Hier kommt das sekundäre Schlüsselwort **load pdf as image** ins Spiel.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*Warum das wichtig ist:* `aocr.Image.load` rastert jede PDF‑Seite intern in ein Bitmap, das die OCR‑Engine verstehen kann. Wenn Sie diesen Schritt überspringen und das rohe PDF übergeben, wirft die Engine einen Fehler, weil sie Pixeldaten und keine Vektordaten erwartet.

> **Hinweis:** Der Pfad kann absolut oder relativ sein. Stellen Sie sicher, dass die Datei lesbar ist; andernfalls erhalten Sie einen `FileNotFoundError`.

## Schritt 2: OCR auf PDF ausführen – Pixel in Zeichen umwandeln

Jetzt, wo das PDF als Bild vorliegt, können wir endlich **OCR auf PDF ausführen**. Das folgende Snippet verarbeitet alle Seiten auf einmal:

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*Was passiert im Hintergrund?* `process_all_pages` durchläuft die gerasterten Seiten, wendet das OCR‑Modell an und gibt eine Liste von Ergebnisobjekten zurück – eines pro Seite. Jedes Ergebnis enthält den erkannten Text, Vertrauenswerte und Begrenzungsrahmen (falls Sie diese später benötigen).

## Schritt 3: Text aus PDF extrahieren – Die Zeichen herausziehen

Mit den OCR‑Ergebnissen in der Hand wird das Extrahieren des Klartexts trivial. Wir iterieren über die Seiten und geben die Ausgabe aus, wobei wir das sekundäre Schlüsselwort **extract text from pdf** demonstrieren.

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**Erwartete Ausgabe** (gekürzt für die Kürze):

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

Wenn Sie den Text in einem einzigen String benötigen, einfach verketten:

```python
full_text = "\n".join(r.text for r in page_results)
```

Jetzt haben Sie erfolgreich **Text aus PDF extrahiert** mithilfe von OCR.

## Schritt 4: Gescannte PDF konvertieren – Durchsuchbar machen

Viele nachgelagerte Werkzeuge (wie Elasticsearch oder SharePoint) erwarten ein durchsuchbares PDF statt eines reinen Text‑Dumps. Sie können die OCR‑Ausgabe wieder in das Original‑PDF einbetten und damit **gescannte PDF** in eine durchsuchbare Version umwandeln.

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*Warum das sinnvoll ist?* Ein durchsuchbares PDF behält das ursprüngliche Layout und die Bilder bei, ermöglicht jedoch Textauswahl und Indexierung – ein Gewinn für Menschen und Maschinen.

## Häufige Fallstricke & Randfälle

### Mehrseitige PDFs, die größer als der Speicher sind

Wenn Ihr PDF Hunderte von Seiten hat, kann das Laden von allem auf einmal den RAM erschöpfen. Die `aocr`‑Bibliothek unterstützt Lazy Loading:

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

Dann die Seiten einzeln verarbeiten:

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### Scans von schlechter Qualität

Die OCR‑Genauigkeit sinkt bei unscharfen oder kontrastarmen Scans drastisch. Vor dem Übergeben des Bildes an die Engine sollten Sie eine Vorverarbeitung in Betracht ziehen:

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### Sprachunterstützung

Standardmäßig geht die Engine von Englisch aus. Um **OCR auf PDF** in einer anderen Sprache auszuführen, setzen Sie den Sprachcode:

```python
ocr_engine.language = "spa"  # Spanish
```

Stellen Sie sicher, dass das entsprechende Sprachmodell installiert ist.

## Vollständiges funktionierendes Beispiel

Alles zusammengeführt, hier ein eigenständiges Skript, das Sie in eine Datei namens `ocr_pdf.py` legen und sofort ausführen können:

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

Führen Sie es folgendermaßen aus:

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

Sie sehen den Text in der Konsole ausgegeben, und wenn Sie `-o` angegeben haben, erscheint ein durchsuchbares PDF neben der Originaldatei.

## Pro‑Tipps & bewährte Vorgehensweisen

- **Batch‑Verarbeitung:** Beim Umgang mit Dutzenden PDFs die obige Logik in einer Schleife einbetten und den Erfolg/Fehlschlag jeder Datei protokollieren.
- **Vertrauensfilterung:** Jeder `page_result` enthält eine Vertrauensmetrik. Seiten mit niedrigem Vertrauen verwerfen oder markieren für manuelle Überprüfung.
- **Parallelität:** Wenn Ihre CPU mehrere Kerne hat, sollten Sie `concurrent.futures` verwenden, um Seiten parallel zu verarbeiten – achten Sie dabei auf den Speicherverbrauch.
- **Versionssperre:** Die `aocr`‑API kann sich ändern. Fixieren Sie die Version in `requirements.txt` (z. B. `aocr==2.3.1`), um breaking changes zu vermeiden.

## Fazit

Wir haben **gezeigt, wie man OCR verwendet**, um **Text aus PDF zu extrahieren**, **OCR auf PDF auszuführen**, **PDF als Bild zu laden** und sogar **gescannte PDF** in ein durchsuchbares Format zu **konvertieren**. Der Code ist vollständig, die Erklärungen decken sowohl das *Was* als auch das *Warum* ab, und Sie besitzen nun ein wiederverwendbares Muster für jedes Projekt, das bildbasierte PDFs verarbeitet.

Was kommt als Nächstes? Versuchen Sie, den extrahierten Text in eine Natural‑Language‑Pipeline zu speisen, indexieren Sie die durchsuchbaren PDFs mit Elasticsearch oder experimentieren Sie mit verschiedenen OCR‑Back‑Ends wie Tesseract oder Azure Computer Vision. Der Himmel ist die Grenze, und die Werkzeuge liegen bereits in Ihren Händen.

Viel Spaß beim Coden, und mögen Ihre PDFs stets durchsuchbar sein! 

![Beispiel für die Verwendung von OCR](/images/ocr_workflow.png "Beispiel für die Verwendung von OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}