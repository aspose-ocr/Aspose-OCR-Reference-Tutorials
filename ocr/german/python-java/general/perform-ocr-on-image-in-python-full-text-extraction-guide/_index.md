---
category: general
date: 2026-06-19
description: Führen Sie OCR auf einem Bild mit der OCR‑Bibliothek von Python durch.
  Lernen Sie, wie Sie Text aus einem Bild erkennen, Text aus JPEGs erkennen und Text
  aus gescannten Bildern effizient extrahieren.
draft: false
keywords:
- perform OCR on image
- recognize text from jpeg
- detect text from image
- extract text from scanned image
- load image for OCR
language: de
og_description: Führen Sie OCR auf Bildern mit Python durch und extrahieren Sie Text
  aus gescannten Dateien. Dieser Leitfaden führt Sie Schritt für Schritt durch das
  Laden von Bildern, das Entzerren und die Texterkennung.
og_title: OCR auf Bild in Python durchführen – Vollständiger Leitfaden zur Textextraktion
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  headline: Perform OCR on Image in Python – Full Text Extraction Guide
  type: TechArticle
- description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  name: Perform OCR on Image in Python – Full Text Extraction Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed (the example uses the `ocr` package available via
      `pip install ocr-lib` – replace with your actual library name). - Basic familiarity
      with Python functions and virtual environments. - An image file (JPEG, PNG,
      TIFF) you want to process; we’ll use `skewed_page.jpg` as a placeh'
  - name: Recognize Text from JPEG vs PNG
    text: 'Both formats are supported, but JPEG compression can introduce artifacts
      that confuse the engine. If you notice frequent mis‑recognitions, try converting
      the JPEG to PNG first:'
  - name: Detect Text from Image with Multiple Languages
    text: 'If your document mixes English and Spanish, set a multilingual mode:'
  - name: Extract Text from Scanned PDFs
    text: 'For PDFs, you need to rasterize each page into an image first. Libraries
      like `pdf2image` make this painless:'
  type: HowTo
- questions:
  - answer: Absolutely. The library works without a GUI; just ensure the necessary
      native binaries (e.g., Tesseract) are installed on the server.
    question: Can I run this on a headless server?
  - answer: Consider adding a sharpening filter before `engine.recognize`. Many OCR
      libraries expose `image_preprocessing.sharpen = True` or you can use OpenCV’s
      `cv2.GaussianBlur` in reverse.
    question: What if the image is blurry?
  - answer: 'Yes. Wrap `perform_ocr` in a loop over a list of file paths, ## What
      Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
      - [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
      - [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: Does the script support batch processing?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: OCR auf Bild in Python durchführen – Vollständiger Leitfaden zur Textextraktion
url: /de/python-java/general/perform-ocr-on-image-in-python-full-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR auf Bild in Python durchführen – Vollständiger Leitfaden zur Textextraktion

Haben Sie jemals **OCR auf Bild**‑Dateien durchführen müssen, sind aber an einer Wand gestoßen, weil der Code kryptisch aussah? Sie sind nicht allein. Egal, ob Sie einen Haufen gescannter Quittungen in durchsuchbare PDFs verwandeln oder Bildunterschriften aus einem JPEG für ein Data‑Science‑Projekt extrahieren – die Fähigkeit, Text aus JPEGs und anderen Formaten zu erkennen, ist heute eine unverzichtbare Fähigkeit für jeden Entwickler.

In diesem Tutorial führen wir Sie durch ein komplettes, ausführbares Beispiel, das zeigt, wie Sie **Text aus Bild**‑Dateien **erkennen**, **Text aus gescanntem Bild**‑Dokumenten **extrahieren** und sogar **Bild für OCR laden** – und das in nur wenigen Zeilen Code. Am Ende haben Sie ein solides, produktionsreifes Snippet, das Sie in Ihre eigenen Projekte einbinden können – ohne fehlende Importe, ohne vage „siehe Dokumentation“-Abkürzungen.

## Was Sie erstellen werden

- Ein kleines Python‑Skript, das eine OCR‑Engine erstellt, Auto‑Deskew aktiviert, ein JPEG (oder ein beliebiges unterstütztes Format) lädt und den erkannten Text ausgibt.
- Erklärungen, **warum** jede Einstellung wichtig ist, nicht nur **wie** man sie eingibt.
- Tipps zum Umgang mit mehrseitigen PDFs, nicht‑englischen Sprachen und häufigen Stolperfallen wie unscharfen Scans.

### Voraussetzungen

- Python 3.8+ installiert (das Beispiel verwendet das `ocr`‑Paket, das über `pip install ocr-lib` verfügbar ist – ersetzen Sie es durch den tatsächlichen Bibliotheksnamen).
- Grundlegende Kenntnisse von Python‑Funktionen und virtuellen Umgebungen.
- Eine Bilddatei (JPEG, PNG, TIFF), die Sie verarbeiten möchten; wir verwenden `skewed_page.jpg` als Platzhalter.

> **Pro‑Tipp:** Wenn Sie Windows verwenden, führen Sie Ihr Terminal als Administrator aus, wenn Sie die OCR‑Bibliothek installieren, um Berechtigungsprobleme zu vermeiden.

---

## OCR auf Bild – Einrichtung und Konfiguration

Das Erste, was Sie benötigen, ist eine saubere OCR‑Engine‑Instanz. Denken Sie daran wie an das Gehirn hinter dem Vorgang; ohne richtige Konfiguration liefert selbst das schärfste Bild Kauderwelsch.

```python
# Step 1: Import the OCR library and create an engine
import ocr

engine = ocr.OcrEngine()
# Set the recognition language – English works for most cases
engine.language = ocr.Language.English
```

**Warum das wichtig ist:**  
Durch das Setzen von `engine.language` wird der Zeichensatz, den die OCR‑Engine erwartet, eingegrenzt, was die Genauigkeit dramatisch erhöht. Wenn Sie das überspringen, versucht die Engine zu raten und missinterpretiert häufig einfache Wörter.

---

## Automatisches Deskew aktivieren – Schiefe Scans korrigieren

Gescannte Seiten sind selten perfekt flach. Eine leichte Neigung kann die Zeichensegmentierung durcheinanderbringen und aus „Hello“ ein „H3llo“ machen. Das Flag `auto_deskew` übernimmt die schwere Arbeit für Sie.

```python
# Step 2: Turn on automatic deskew to straighten tilted images
engine.image_preprocessing.auto_deskew = True
```

**Randfall:** Wenn Sie wissen, dass Ihre Bilder bereits gerade sind, kann das Deaktivieren von Deskew ein paar Millisekunden Verarbeitungszeit sparen – nützlich, wenn Sie Tausende von Seiten in einem Batch‑Job verarbeiten.

---

## Bild für OCR laden – Unterstützung für JPEG, PNG, TIFF

Jetzt **laden wir das Bild für OCR**. Die Methode `ocr.Image.load` ist flexibel; sie akzeptiert einen Pfad zu jedem unterstützten Rasterformat.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/skewed_page.jpg"
image = ocr.Image.load(image_path)
```

> **Warum dieser Schritt entscheidend ist:** Die Bibliothek liest die Datei in ein internes Bitmap ein und führt ggf. notwendige Farbraumkonvertierungen durch. Wird dieser Schritt übersprungen und ein roher Byte‑Stream übergeben, führt das zu einem `FileNotFoundError` oder, schlimmer noch, zu stillen leeren Ergebnissen.

Wenn Sie speziell **Text aus JPEG**‑Dateien erkennen möchten, stellen Sie sicher, dass die Dateierweiterung `.jpeg` oder `.jpg` lautet. Der gleiche Aufruf funktioniert für PNG (`.png`) oder TIFF (`.tif`) ohne Änderungen.

---

## OCR auf Bild ausführen – Engine starten

Mit der vorbereiteten Engine und dem Bild im Speicher ist es Zeit, **OCR auf Bild**‑Daten **auszuführen**. Diese eine Zeile erledigt das Schwergewicht: Vorverarbeitung, Segmentierung, Klassifizierung und Textzusammenstellung.

```python
# Step 4: Run OCR and capture the result object
result = engine.recognize(image)
```

**Was im Hintergrund passiert:**  
- Die Engine wendet die Deskew‑Transformation an (falls aktiviert).  
- Sie führt ein neuronales Netzwerk oder das Tesseract‑Backend aus, um Zeichen zu identifizieren.  
- Abschließend fügt sie Zeichen zu Wörtern und Zeilen zusammen und gibt ein reichhaltiges `result`‑Objekt zurück.

---

## Text aus gescanntem Bild extrahieren – Ergebnisse ausgeben

Der letzte Schritt besteht darin, **Text aus gescanntem Bild** zu **extrahieren** und anzuzeigen. Das Attribut `result.text` enthält die reine Textdarstellung.

```python
# Step 5: Print the detected text to the console
print("Detected text:")
print(result.text)
```

Typische Ausgabe sieht etwa so aus:

```
Detected text:
Invoice #12345
Date: 2023‑09‑01
Total: $1,234.56
Thank you for your business!
```

Findet die OCR‑Engine keine Zeichen, ist `result.text` ein leerer String. In diesem Fall prüfen Sie die Bildqualität erneut oder passen ggf. die Eigenschaft `engine.confidence_threshold` an (sofern Ihre Bibliothek das unterstützt).

---

## Umgang mit gängigen Variationen

### Text aus JPEG vs. PNG erkennen

Beide Formate werden unterstützt, aber JPEG‑Kompression kann Artefakte einführen, die die Engine verwirren. Wenn Sie häufig Fehlinterpretationen bemerken, konvertieren Sie das JPEG zunächst zu PNG:

```python
from PIL import Image
Image.open(image_path).save("temp.png", format="PNG")
image = ocr.Image.load("temp.png")
```

### Text aus Bild mit mehreren Sprachen erkennen

Wenn Ihr Dokument Englisch und Spanisch mischt, aktivieren Sie einen mehrsprachigen Modus:

```python
engine.language = ocr.Language.English | ocr.Language.Spanish
```

Die Engine berücksichtigt dann beide Alphabete bei der Erkennung.

### Text aus gescannten PDFs extrahieren

Für PDFs müssen Sie jede Seite zuerst in ein Bild rasterisieren. Bibliotheken wie `pdf2image` machen das unkompliziert:

```python
from pdf2image import convert_from_path

pages = convert_from_path("document.pdf", dpi=300)
for i, page_image in enumerate(pages):
    image = ocr.Image.from_pil(page_image)   # assuming the library accepts a PIL image
    result = engine.recognize(image)
    print(f"Page {i+1} text:")
    print(result.text)
```

---

## Vollständiges funktionierendes Beispiel

Unten finden Sie das komplette Skript, das Sie in eine Datei namens `ocr_demo.py` kopieren können. Es enthält Fehlerbehandlung und einen kleinen Helfer, um die Ausführungszeit zu messen.

```python
import ocr
import time
import sys
from pathlib import Path

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a given image file and return the extracted text.
    Handles auto‑deskew and basic error reporting.
    """
    if not Path(image_path).exists():
        sys.exit(f"❌ Error: File not found – {image_path}")

    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.image_preprocessing.auto_deskew = True

    try:
        image = ocr.Image.load(image_path)
    except Exception as e:
        sys.exit(f"❌ Failed to load image: {e}")

    start = time.time()
    result = engine.recognize(image)
    elapsed = time.time() - start

    if not result.text.strip():
        print("⚠️ No text detected. Try a higher‑resolution image or adjust preprocessing.")
    else:
        print(f"✅ OCR completed in {elapsed:.2f}s")
        print("Detected text:")
        print(result.text)

    return result.text

if __name__ == "__main__":
    # Replace with the path to your JPEG/PNG/TIFF file
    perform_ocr("YOUR_DIRECTORY/skewed_page.jpg")
```

**Erwartete Ausgabe** (bei einem klaren Scan):

```
✅ OCR completed in 0.87s
Detected text:
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

---

## Häufig gestellte Fragen

**F: Kann ich das auf einem headless Server ausführen?**  
A: Absolut. Die Bibliothek funktioniert ohne GUI; stellen Sie nur sicher, dass die notwendigen nativen Binaries (z. B. Tesseract) auf dem Server installiert sind.

**F: Was, wenn das Bild unscharf ist?**  
A: Erwägen Sie, vor `engine.recognize` einen Schärfungsfilter hinzuzufügen. Viele OCR‑Bibliotheken bieten `image_preprocessing.sharpen = True` oder Sie nutzen OpenCVs `cv2.GaussianBlur` in umgekehrter Richtung.

**F: Unterstützt das Skript die Stapelverarbeitung?**  
A: Ja. Wickeln Sie `perform_ocr` in eine Schleife über eine Liste von Dateipfaden ein,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}