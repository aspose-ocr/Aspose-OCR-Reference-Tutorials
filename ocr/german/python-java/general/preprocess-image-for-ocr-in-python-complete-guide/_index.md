---
category: general
date: 2026-06-25
description: Bild für OCR vorverarbeiten und Text aus gescanntem Dokument mit Python
  erkennen. Schritt‑für‑Schritt‑Tutorial mit vollständigem Code.
draft: false
keywords:
- preprocess image for OCR
- recognize text from scanned document
- Python OCR tutorial
- image deskewing Python
- OCR preprocessing tips
language: de
og_description: Bild für OCR vorverarbeiten und Text aus gescanntem Dokument mit Python
  erkennen. Folgen Sie diesem detaillierten, ausführbaren Tutorial.
og_title: Bild für OCR in Python vorverarbeiten – Vollständiger Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  headline: Preprocess Image for OCR in Python – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  name: Preprocess Image for OCR in Python – Complete Guide
  steps:
  - name: Create an OCR Engine Instance
    text: '```python import ocr # <-- make sure the OCR library is installed'
  - name: Enable Automatic Deskewing and Binarization
    text: '```python # Step 2: Enable automatic deskewing and binarization to improve
      recognition engine.image_preprocessing = ocr.ImagePreProcessingOptions( auto_deskew=True,
      auto_binarize=True ) ```'
  - name: Load the Skewed Image You Want to Process
    text: '```python # Step 3: Load the skewed image you want to process image_path
      = "YOUR_DIRECTORY/skewed_document.jpg" image = ocr.Image.load(image_path) ```'
  - name: Perform OCR on the Pre‑processed Image
    text: '```python # Step 4: Perform OCR on the pre‑processed image result = engine.recognize(image)
      ```'
  - name: Output the Recognized Text
    text: '```python # Step 5: Output the recognized text print("Deskewed & binarized
      text:", result.text) ```'
  - name: 1. Handling Multiple Languages
    text: 'If your document contains both English and French, configure the engine
      before step 1:'
  - name: 2. Fine‑Tuning Binarization Thresholds
    text: 'Automatic binarization works for most cases, but some old photocopies need
      a custom threshold:'
  - name: 3. Extracting Layout Information
    text: 'Sometimes you need more than raw text—you want to know where each paragraph
      lives on the page. Many engines expose a `result.blocks` collection:'
  - name: 4. Processing a Batch of Files
    text: 'If you have a folder full of scanned PDFs converted to JPEGs, wrap the
      whole flow in a loop:'
  - name: 5. Dealing with Low‑Resolution Scans
    text: 'Low‑resolution images (< 150 dpi) often produce fuzzy characters. A quick
      remedy is to upscale using a high‑quality algorithm before feeding the image
      to the OCR engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Bild für OCR in Python vorverarbeiten – Komplettanleitung
url: /de/python-java/general/preprocess-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bild für OCR in Python vorverarbeiten – Vollständiger Leitfaden

Haben Sie sich schon einmal gefragt, wie man **Bild für OCR vorverarbeitet**, damit der Text sauber und zuverlässig herauskommt? Sie sind nicht allein – die meisten Entwickler stoßen auf dasselbe Problem, wenn die gescannte Seite schief ist oder der Kontrast völlig durcheinander ist. Die gute Nachricht: ein paar Zeilen Python können das Durcheinander begradigen, das Bild binarisieren und Ihnen klaren, durchsuchbaren Text zurückgeben.

In diesem Tutorial gehen wir die genauen Schritte durch, um **Bild für OCR vorzuverarbeiten** *und* **Text aus gescannten Dokumenten** zu **erkennen**, wobei wir eine beliebte OCR‑Bibliothek verwenden. Am Ende haben Sie ein sofort ausführbares Skript, verstehen, warum jede Einstellung wichtig ist, und wissen, wie Sie es für knifflige Randfälle anpassen können.

## Was Sie benötigen

- Python 3.8 oder neuer (der Code funktioniert auch mit 3.10+)
- Ein OCR‑Paket, das die Klassen `OcrEngine`, `ImagePreProcessingOptions` und `Image` bereitstellt (z. B. das fiktive `ocr`‑Modul aus dem Beispiel)
- Ein gescanntes oder fotografiertes Dokument, das leicht schief oder kontrastarm ist
- Ihr Lieblings‑IDE oder ein einfacher Terminal – keine schwere GUI nötig

Das war’s. Keine zusätzlichen Binärdateien, kein Docker‑Gymnastik. Lassen Sie uns loslegen.

## Bild für OCR vorverarbeiten – Schritt für Schritt

Unten finden Sie den Kern‑Workflow, aufgeteilt in fünf klare Phasen. Jede Phase enthält **warum** wir sie ausführen, den genauen **Code** und eine kurze **Erklärung**, was im Hintergrund passiert.

### Schritt 1: Eine OCR‑Engine‑Instanz erstellen

```python
import ocr  # <-- make sure the OCR library is installed

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Warum das wichtig ist:*  
Das Objekt `OcrEngine` ist das Gehirn der Operation. Es hält Konfigurationen wie Sprachpakete, Vertrauensschwellen und – am wichtigsten für uns – Bild‑Vorverarbeitungs‑Flags. Durch die Instanziierung erhalten wir eine saubere Basis, um die nachfolgenden Tricks zu aktivieren.

### Schritt 2: Automatisches Deskewing und Binarisierung aktivieren

```python
# Step 2: Enable automatic deskewing and binarization to improve recognition
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
```

*Warum das wichtig ist:*  
- **Deskewing** dreht das Bild, sodass Textzeilen horizontal werden. OCR‑Engines haben Schwierigkeiten, wenn die Grundlinie um mehr als ein paar Grad geneigt ist.  
- **Binarisierung** wandelt das Bild in reines Schwarz‑Weiß um und entfernt Hintergrundrauschen, das Zeichenklassifikatoren verwirren kann.  
Beide Optionen sind in vielen modernen Bibliotheken *automatisch*, aber Sie müssen sie trotzdem einschalten – daher die explizite Zuweisung.

> **Pro‑Tipp:** Wenn Ihre Quellbilder bereits perfekt ausgerichtet sind, können Sie `auto_deskew=False` setzen, um ein Millisekunde Verarbeitungszeit zu sparen.

### Schritt 3: Das schiefe Bild laden, das Sie verarbeiten möchten

```python
# Step 3: Load the skewed image you want to process
image_path = "YOUR_DIRECTORY/skewed_document.jpg"
image = ocr.Image.load(image_path)
```

*Warum das wichtig ist:*  
Die Methode `Image.load` liest die Datei in den Speicher und verpackt sie in ein Objekt, das die OCR‑Engine versteht. Sie extrahiert außerdem Metadaten wie DPI, die den Standard‑Skalierungsfaktor für das Deskewing beeinflussen können.

> **Randfall:** Handelt es sich bei dem Bild um ein mehrseitiges TIFF, müssen Sie über jede Seite iterieren oder einen Helfer wie `ocr.MultiPageImage.load` verwenden. Die gleichen Vorverarbeitungseinstellungen gelten für jede Seite.

### Schritt 4: OCR auf dem vorverarbeiteten Bild ausführen

```python
# Step 4: Perform OCR on the pre‑processed image
result = engine.recognize(image)
```

*Warum das wichtig ist:*  
An diesem Punkt wendet die Engine die zuvor aktivierten Deskew‑ und Binarisierungsschritte an und führt dann ihr neuronales Netzwerk (oder die klassische Tesseract‑ähnliche Pipeline) auf dem bereinigten Bitmap aus. Das zurückgegebene `result`‑Objekt enthält typischerweise den Klartext, Vertrauenswerte und manchmal Positionsdaten für jedes Wort.

> **Was tun, wenn der Text immer noch verzerrt ist?**  
Überprüfen Sie die Bildauflösung: OCR funktioniert am besten bei 300 dpi oder höher. Wenn Ihre Quelle niedriger ist, sollten Sie vor dem Laden hochskalieren oder das Original‑Scan vom Dokumenten‑Ersteller anfordern.

### Schritt 5: Den erkannten Text ausgeben

```python
# Step 5: Output the recognized text
print("Deskewed & binarized text:", result.text)
```

*Warum das wichtig ist:*  
`result.text` ist eine reine Zeichenkette, die alles enthält, was die Engine lesen konnte. Das Ausgeben ist praktisch für schnelles Debugging; in einer echten Anwendung würden Sie es wahrscheinlich in eine `.txt`‑Datei, eine Datenbank oder in eine nachgelagerte NLP‑Pipeline schreiben.

---

## Text aus gescanntem Dokument erkennen – Mehr als die Grundlagen

Jetzt, wo die Grundpipeline funktioniert, schauen wir uns ein paar gängige Variationen an, denen Sie begegnen können, wenn Sie **Text aus gescannten Dokumenten** in der Praxis **erkennen**.

### 1. Umgang mit mehreren Sprachen

Enthält Ihr Dokument sowohl Englisch als auch Französisch, konfigurieren Sie die Engine vor Schritt 1:

```python
engine = ocr.OcrEngine(languages=["eng", "fra"])
```

Die meisten OCR‑Engines akzeptieren ISO‑639‑2‑Codes; das Laden zusätzlicher Sprachpakete verursacht einen kleinen Overhead, verbessert jedoch die Genauigkeit bei mehrsprachigen Seiten dramatisch.

### 2. Feinabstimmung der Binarisierungsschwelle

Automatische Binarisierung funktioniert in den meisten Fällen, aber einige alte Fotokopien benötigen eine benutzerdefinierte Schwelle:

```python
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=False,          # turn off auto
    binarization_threshold=180   # manual threshold (0‑255)
)
```

Experimentieren Sie mit Werten zwischen 120 und 220, bis der Hintergrund verschwindet, ohne schwache Zeichen zu löschen.

### 3. Extrahieren von Layout‑Informationen

Manchmal benötigen Sie mehr als reinen Text – Sie wollen wissen, wo jeder Absatz auf der Seite liegt. Viele Engines stellen eine `result.blocks`‑Sammlung bereit:

```python
for block in result.blocks:
    print(f"Block at ({block.x}, {block.y}) size {block.width}x{block.height}")
    print(block.text)
```

Das ist unbezahlbar, um Tabellen wiederherzustellen oder die Spaltenreihenfolge zu erhalten.

### 4. Verarbeitung einer Stapeldatei

Haben Sie einen Ordner voller gescannter PDFs, die in JPEGs konvertiert wurden, verpacken Sie den gesamten Ablauf in eine Schleife:

```python
import pathlib

folder = pathlib.Path("YOUR_DIRECTORY")
for img_file in folder.glob("*.jpg"):
    img = ocr.Image.load(str(img_file))
    txt = engine.recognize(img).text
    (folder / f"{img_file.stem}.txt").write_text(txt, encoding="utf-8")
    print(f"Processed {img_file.name}")
```

Die Schleife verwendet dieselbe `engine`‑Instanz, was effizienter ist, als sie für jede Datei neu zu erstellen.

### 5. Umgang mit niedrigauflösenden Scans

Niedrigauflösende Bilder (< 150 dpi) erzeugen häufig unscharfe Zeichen. Eine schnelle Lösung ist, vor dem Übergeben an die OCR‑Engine mit einem hochwertigen Algorithmus hochzuskalieren:

```python
from PIL import Image as PilImage

pil_img = PilImage.open("low_res.jpg")
upscaled = pil_img.resize((pil_img.width * 2, pil_img.height * 2), PilImage.LANCZOS)
upscaled.save("upscaled.jpg")
image = ocr.Image.load("upscaled.jpg")
```

Hochskalieren erzeugt nicht magisch Details, aber die Binarisierung kann mit schärferen Kanten arbeiten und so einen modesten Schub geben.

---

## Erwartete Ausgabe

Das Ausführen des ursprünglichen Fünf‑Schritte‑Skripts auf einem mäßig schiefen Scan mit 300 dpi sollte etwa Folgendes ausgeben:

```
Deskewed & binarized text: 
Dear Customer,

Thank you for your recent purchase. Please find your receipt attached.

Best regards,
Acme Corp.
```

Wenn Sie verzerrte Zeichen sehen, überprüfen Sie die Vorverarbeitungs‑Flags, die Bildauflösung und die Sprachkonfiguration.

---

## Fazit

Wir haben alles behandelt, was Sie benötigen, um **Bild für OCR vorzuverarbeiten** und **Text aus gescannten Dokumenten** mit Python zu **erkennen**. Beginnend mit einer frischen Engine‑Instanz haben wir automatisches Deskewing und Binarisierung aktiviert, ein schiefes Bild geladen, die Erkennung ausgeführt und den sauberen Text ausgegeben. Unterwegs haben wir Mehrsprachigkeit, manuelle Schwellenwerte, Layout‑Extraktion, Batch‑Verarbeitung und Low‑Resolution‑Work‑arounds erkundet.

Probieren Sie das Skript an Ihren eigenen Scans aus – vielleicht ein Stapel Quittungen, ein handschriftliches Formular oder ein altes Zeitungsstück. Sobald Sie sich sicher fühlen, können Sie PDF‑Erstellung hinzufügen oder die Ausgabe in einen Such‑Index einspeisen. Der Himmel ist das Limit.

**Bereit für die nächste Herausforderung?** Schauen Sie sich unsere Tutorials zu *„Tabellen aus gescannten PDFs mit Python extrahieren“* und *„Benutzerdefinierte OCR‑Modelle mit TensorFlow trainieren“* an, um Ihre Dokument‑Automatisierungs‑Toolbox weiter auszubauen.

Viel Spaß beim Coden, und möge Ihre OCR stets scharf sein!


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Text aus Bild mit Aspose OCR extrahieren – Schritt‑für‑Schritt‑Anleitung](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Text aus Bild extrahieren – OCR‑Optimierung mit Aspose.OCR für .NET](/ocr/english/net/ocr-optimization/)
- [Wie man AspOCR verwendet: Bild‑OCR‑Filter vorverarbeiten für .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}