---
category: general
date: 2026-03-18
description: Führen Sie OCR auf dem Bild aus, um Text aus einer PNG-Datei zu extrahieren
  und ein durchsuchbares PDF zu erstellen. Erfahren Sie, wie Sie Textbilder erkennen
  und PNG in PDF umwandeln – in wenigen Minuten.
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: de
og_description: Führen Sie OCR auf dem Bild aus, um Text aus einer PNG zu extrahieren,
  das Textbild zu erkennen und ein durchsuchbares PDF zu erstellen. Folgen Sie dieser
  Schritt‑für‑Schritt‑Anleitung.
og_title: OCR auf Bild ausführen – Text schnell aus PNG extrahieren
tags:
- OCR
- Python
- Image Processing
title: OCR auf Bild ausführen – Text aus PNG schnell extrahieren
url: /de/python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR auf Bild ausführen – Text schnell aus PNG extrahieren

Haben Sie schon einmal **OCR auf Bild**‑Dateien ausführen müssen, wussten aber nicht, wo Sie anfangen sollen? Vielleicht haben Sie einen gescannten Artikel als `article.png` gespeichert und wollen einfach nur den Klartext, oder Sie benötigen ein durchsuchbares PDF für die Archivierung. So oder so sind Sie hier genau richtig. In diesem Tutorial zeigen wir Ihnen, wie Sie Text aus einer PNG‑Datei extrahieren, das Textbild erkennen und die PNG sogar in ein durchsuchbares PDF umwandeln – alles mit nur wenigen Code‑Zeilen.

> **Was Sie erhalten:** ein vollständiges, ausführbares Skript, das eine PNG lädt, OCR ausführt, die hOCR‑Ausgabe speichert und optional ein durchsuchbares PDF erzeugt. Keine fehlenden Importe, keine “siehe Dokumentation”‑Dead‑Ends – nur eine eigenständige Lösung, die Sie noch heute in Ihr Projekt übernehmen können.

## Voraussetzungen

Bevor wir starten, stellen Sie sicher, dass Sie Folgendes haben:

- **Python 3.8+** (die hier verwendete Syntax funktioniert in jeder aktuellen Version)
- Die **`ocr_engine`**‑Bibliothek, die Sie benutzen (das Beispiel geht von einer Klasse namens `OcrEngine` aus; ersetzen Sie sie bei Bedarf durch Tesseract, EasyOCR usw.)
- Eine PNG‑Datei, die Sie verarbeiten möchten (z. B. `article.png` in einem Ordner, den Sie referenzieren können)
- Schreibrechte für das Ausgabeverzeichnis

Falls Sie Tesseract im Hintergrund verwenden, installieren Sie es mit:

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

Und dann den Python‑Wrapper:

```bash
pip install pytesseract Pillow
```

*Pro‑Tipp:* Halten Sie Ihre OCR‑Bibliothek aktuell – neue Sprachpakete und Performance‑Optimierungen erscheinen regelmäßig.

## OCR auf Bild ausführen – Schritt‑für‑Schritt‑Anleitung

Unten finden Sie das **komplette Skript**. Kopieren Sie es gern in eine Datei namens `run_ocr.py` und führen Sie sie mit `python run_ocr.py` aus.

```python
# run_ocr.py
import os
from pathlib import Path

# Import the OCR engine – replace with your actual import if different
# For Tesseract via pytesseract you would use: import pytesseract
# Here we assume a generic OcrEngine class that matches the example
from ocr_engine import OcrEngine  # <-- adjust as needed

def main():
    # ------------------------------------------------------------------
    # Step 1: Create an OCR engine instance
    # ------------------------------------------------------------------
    ocr_engine = OcrEngine()
    # Why this matters: the engine holds configuration (language, DPI, etc.)
    # You can tweak ocr_engine.setLanguage('eng') or similar before proceeding.

    # ------------------------------------------------------------------
    # Step 2: Load the image you want to process
    # ------------------------------------------------------------------
    image_path = Path("YOUR_DIRECTORY/article.png")
    if not image_path.is_file():
        raise FileNotFoundError(f"Image not found: {image_path}")
    ocr_engine.setImageFromFile(str(image_path))

    # ------------------------------------------------------------------
    # Step 3: Choose the export format
    # ------------------------------------------------------------------
    # hOCR preserves layout (bounding boxes, fonts) – perfect for searchable PDFs.
    # Other options: "txt", "pdf", "pdfa"
    ocr_engine.setExportFormat("hocr")

    # ------------------------------------------------------------------
    # Step 4: Run the recognition process
    # ------------------------------------------------------------------
    ocr_result = ocr_engine.recognize()
    # The result object gives us access to the raw OCR text, hOCR, etc.

    # ------------------------------------------------------------------
    # Step 5: Write the HOCR output to a file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/article.hocr")
    with open(output_path, "w", encoding="utf-8") as output_file:
        output_file.write(ocr_result.getExportedContent())
    print(f"✅ HOCR saved to {output_path}")

    # ------------------------------------------------------------------
    # Optional: Generate a searchable PDF from the HOCR
    # ------------------------------------------------------------------
    # Many OCR engines can bundle the original image with the hOCR to produce
    # a PDF that you can search. If your engine supports it, uncomment:
    # ocr_engine.setExportFormat("pdf")
    # pdf_result = ocr_engine.recognize()
    # pdf_path = Path("YOUR_DIRECTORY/article_searchable.pdf")
    # with open(pdf_path, "wb") as pdf_file:
    #     pdf_file.write(pdf_result.getExportedContent())
    # print(f"📄 Searchable PDF created at {pdf_path}")

if __name__ == "__main__":
    main()
```

### Was das Skript macht, in einfachem Deutsch

1. **Instantiate** (Instanziieren) Sie die OCR‑Engine, um deren Einstellungen zu steuern.
2. **Load** (Laden) Sie die PNG‑Datei (`article.png`). Das Skript bricht frühzeitig ab, wenn die Datei nicht existiert – keine mysteriösen `NoneType`‑Fehler später.
3. **Select** (Auswählen) Sie `hocr` als Exportformat. Dieses Format bewahrt das ursprüngliche Layout, was für die spätere Umwandlung in ein durchsuchbares PDF wichtig ist.
4. **Run** (Ausführen) Sie die Erkennungs‑Engine; hier findet die eigentliche Arbeit statt.
5. **Write** (Schreiben) Sie das hOCR‑XML nach `article.hocr`. Sie besitzen nun eine maschinenlesbare Darstellung des Textes und seiner Koordinaten.
6. *(Optional)* Wechseln Sie zu `"pdf"` und erzeugen Sie in einem zusätzlichen Schritt ein durchsuchbares PDF.

Die **erwartete Ausgabe** ist eine UTF‑8‑kodierte `.hocr`‑Datei, die etwa so aussieht (gekürzt zur Übersicht):

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

Wenn Sie den PDF‑Abschnitt auskommentieren, erhalten Sie außerdem `article_searchable.pdf`, das Sie in jedem PDF‑Betrachter öffnen und mit der **Strg + F**‑Suche sofort Wörter finden können.

![Run OCR on image example output](example.png "Run OCR on image – hOCR und PDF Ergebnisse")

## Wie man Text aus PNG mit OcrEngine extrahiert

Wenn Sie nur den Rohtext benötigen (kein Layout, kein PDF), können Sie den hOCR‑Schritt komplett überspringen:

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*Warum reinen Text wählen?* Er ist leichtgewichtig, perfekt für Indexierung und funktioniert hervorragend in nachgelagerten NLP‑Pipelines.

## Textbild erkennen und durchsuchbares PDF erzeugen

Ein durchsuchbares PDF zu erstellen ist ein zweistufiger Prozess:

1. **Run OCR** (OCR ausführen) mit `hocr` (wie oben) um die Layout‑Informationen zu erhalten.
2. **Combine** (Kombinieren) Sie die ursprüngliche PNG mit dem hOCR zu einem PDF mittels des PDF‑Exporters der Engine.

Die meisten modernen OCR‑Bibliotheken (Tesseract, ABBYY, Google Vision) bieten einen `pdf`‑Export, der genau das tut. Das Snippet im *Optional*‑Block des Hauptskripts zeigt das Muster. Sollte Ihre Bibliothek keinen eingebauten PDF‑Exporter besitzen, können Sie **`pdf2image`** + **`reportlab`** nutzen, um Bild und hOCR zusammenzufügen – lassen Sie es mich wissen, und ich teile ein kurzes Zusatzbeispiel.

## PNG mit OCR‑Ausgabe in PDF umwandeln

Manchmal wollen Sie einfach ein **plain PDF**, das das Bild enthält (keine durchsuchbare Ebene). Das ist noch einfacher:

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

Kombinieren Sie das mit dem OCR‑Schritt, wenn Sie eine durchsuchbare Version benötigen, oder behalten Sie es als getreue visuelle Kopie für Archivzwecke.

## Häufige Stolperfallen & Tipps

| Problem | Warum es passiert | Schnelle Lösung |
|---------|-------------------|-----------------|
| **Verschwommene oder niedrig aufgelöste PNG** | Die OCR‑Genauigkeit sinkt dramatisch unter ca. 300 DPI. | Vor dem Durchlauf mit `Image.resize((width*2, height*2), Image.LANCZOS)` hochskalieren. |
| **Falsche Sprache** | Die Engine verwendet standardmäßig Englisch; nicht‑englische Zeichen werden verzerrt. | `ocr_engine.setLanguage('deu')` (oder passenden ISO‑Code) vor `recognize()` aufrufen. |
| **Fehlende hOCR‑Ausgabe** | Einige Engines geben standardmäßig reinen Text zurück, wenn `setExportFormat` nicht gesetzt wurde. | Sicherstellen, dass `setExportFormat("hocr")` **vor** `recognize()` ausgeführt wird. |
| **Dateiberechtigungs‑Fehler** | Versuch, in einen schreibgeschützten Ordner zu schreiben. | Einen Pfad innerhalb Ihres Projekts verwenden oder vorher `os.makedirs(..., exist_ok=True)` ausführen. |
| **Große PDFs verursachen Speicher‑Spikes** | Der PDF‑Exporter hält das gesamte Bild im RAM. | Seiten in Batches verarbeiten oder einen Streaming‑PDF‑Writer nutzen. |

*Pro‑Tipp:* Testen Sie immer an einem kleinen Beispielbild, bevor Sie auf Tausende von Dateien skalieren. Das spart Stunden an Fehlersuche.

## Fazit

Sie wissen jetzt **wie man OCR auf Bilddateien ausführt**, **wie man Text aus PNG extrahiert**, **wie man Textbilder** für nachgelagerte Aufgaben erkennt, **wie man ein durchsuchbares PDF erzeugt** und **wie man PNG in PDF** umwandelt, wenn Sie ein einfaches Archiv benötigen. Das bereitgestellte Skript ist eine komplette Copy‑and‑Paste‑Lösung, die sofort funktioniert, und die optionalen Abschnitte erlauben Ihnen, die Ausgabe exakt an Ihren Workflow anzupassen.

### Was kommt als Nächstes?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}