---
category: general
date: 2026-06-22
description: Erhalte Bounding‑Box‑Koordinaten aus Bildern mit Python. Lerne, wie man
  Text aus einem Bild mit Python, Aspose OCR und JSON‑Parsing in wenigen Minuten extrahiert.
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: de
og_description: Erhalte Bounding‑Box‑Koordinaten aus Bildern mit Python. Dieser Leitfaden
  zeigt, wie man Text aus Bildern mit Python und Aspose OCR extrahiert und Layoutdaten
  analysiert.
og_title: Erhalte Bounding‑Box‑Koordinaten aus OCR in Python – Vollständiges Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  headline: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  type: TechArticle
- description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  name: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - An active Aspose.OCR for Python
      license or a free trial (the library works without a license but adds a watermark).
      - `pip install aspose-ocr` (the package name on PyPI). - A sample image called
      `invoice.png` placed in a folder you can reference.'
  - name: 1. Convert Bounding Boxes to Simple Rectangles
    text: 'If your downstream tool expects `(x, y, width, height)` instead of eight
      points, add a helper:'
  - name: 2. Handle Multi‑Page PDFs
    text: 'Aspose OCR can accept PDF streams. Replace the image loading line with:'
  - name: 3. Visualize Bounding Boxes
    text: 'If you want to see the boxes drawn on the original image, use Pillow:'
  type: HowTo
- questions:
  - answer: For large documents, consider streaming the JSON or processing page‑by‑page
      to keep memory usage low.
    question: What if the JSON is huge?
  - answer: Low contrast or handwritten text often trips OCR engines. Pre‑process
      the image (increase contrast, binarize) before feeding it to Aspose.
    question: Why are some words missing?
  - answer: Yes—set `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`
      to receive a `"characters"` array with its own `boundingBox`.
    question: Can I get character‑level coordinates?
  - answer: Absolutely. (0, 0) is the top‑left corner of the image.
    question: Is the coordinate system zero‑based?
  type: FAQPage
tags:
- OCR
- Python
- JSON
- Image Processing
title: Bounding-Box-Koordinaten aus OCR in Python erhalten – Komplettanleitung
url: /de/python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bounding‑Box‑Koordinaten aus OCR in Python erhalten – Vollständige Anleitung

Haben Sie jemals **Bounding‑Box‑Koordinaten** für jedes Wort in einer gescannten Rechnung benötigen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein. In vielen Automatisierungsprojekten muss man Text auf einem Bild lokalisieren, um ihn zu markieren, zu schwärzen oder in nachgelagerte Analysen einzuspeisen. Die gute Nachricht? Mit ein paar Zeilen Python und Aspose.OCR können Sie sowohl den Text **als auch** seine exakte Position in einem einzigen Durchlauf erhalten.

In diesem Tutorial führen wir Sie durch ein praxisnahes Beispiel, das zeigt, wie Sie **Text aus Bild python‑style** extrahieren und dann die JSON‑Layout‑Daten durchforsten, um die Bounding‑Boxes zu erhalten. Kein Schnickschnack, nur ein funktionierendes Skript, Erklärungen, warum jeder Schritt wichtig ist, und Tipps, um häufige Fallstricke zu vermeiden.

---

## Was Sie bauen werden

Am Ende dieses Leitfadens haben Sie ein einsatzbereites Python‑Skript, das:

1. Ein Bild (z. B. eine Rechnung im PNG‑Format) in Aspose OCR lädt.  
2. Die Engine so konfiguriert, dass sie JSON‑Layout‑Informationen ausgibt.  
3. Das JSON in ein Python‑Dictionary parst.  
4. Über jedes erkannte Wort iteriert und dessen Text **sowie** seine Bounding‑Box‑Koordinaten ausgibt.

Sie sehen außerdem, wie Sie den Code für mehrseitige PDFs, verschiedene Bildformate und benutzerdefinierte Koordinatensysteme anpassen können.

### Voraussetzungen

- Python 3.8+ auf Ihrem Rechner installiert.  
- Eine aktive Aspose.OCR‑für‑Python‑Lizenz oder ein kostenloser Test (die Bibliothek funktioniert ohne Lizenz, fügt jedoch ein Wasserzeichen hinzu).  
- `pip install aspose-ocr` (der Paketname auf PyPI).  
- Ein Beispielbild namens `invoice.png` in einem Ordner, den Sie referenzieren können.

Das war’s – keine schweren Frameworks, keine externen Dienste. Lassen Sie uns loslegen.

---

## Schritt 1: Installieren und Importieren der benötigten Bibliotheken

Stellen Sie zunächst sicher, dass das Aspose OCR‑Paket und das eingebaute `json`‑Modul verfügbar sind. Das `json`‑Modul ist Teil von Python, daher müssen wir nur Aspose installieren.

```bash
pip install aspose-ocr
```

Importieren Sie sie nun in Ihrem Skript:

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **Warum das wichtig ist:** Durch das Importieren von `aspose.ocr` erhalten Sie Zugriff auf die Hochleistungs‑OCR‑Engine, während `json` Ihnen ermöglicht, den rohen Layout‑String in ein natives Python‑Dictionary zu verwandeln, das leicht zu traversieren ist.

---

## Schritt 2: Erstellen der OCR‑Engine und Laden Ihres Bildes

Die Engine ist das Herzstück des Prozesses. Sie instanziieren sie und geben ihr dann das Bild, das Sie scannen möchten.

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **Pro‑Tipp:** Ersetzen Sie `"YOUR_DIRECTORY/invoice.png"` durch einen absoluten oder relativen Pfad, der auf Ihre tatsächliche Datei zeigt. Wenn die Datei nicht gefunden wird, wirft Aspose einen `FileNotFoundError`, also prüfen Sie die Schreibweise sorgfältig.

---

## Schritt 3: Konfigurieren der Engine für die Ausgabe von JSON‑Layout‑Daten

Aspose OCR kann reinen Text, OCR‑nur JSON oder ein vollständiges Layout‑JSON zurückgeben, das Koordinaten für Wörter, Zeilen und sogar einzelne Zeichen enthält. Für **Bounding‑Box‑Koordinaten** benötigen wir das Layout‑JSON.

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **Warum JSON?** JSON ist sprachunabhängig, menschenlesbar und lässt sich sauber in Python‑Dictionaries abbilden. Das Layout‑JSON enthält ein `"words"`‑Array, wobei jeder Eintrag den Text und ein `boundingBox`‑Array mit acht Zahlen (die vier Eckpunkte) hält.

---

## Schritt 4: Erkennung ausführen und den rohen JSON‑String holen

Jetzt führen wir die OCR tatsächlich aus. Die Methode `recognize()` liefert ein `OcrResult`‑Objekt, aus dem wir den JSON‑String extrahieren können.

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

Wenn Sie `layout_json` ausgeben, sehen Sie etwa Folgendes:

```json
{
  "words": [
    {
      "text": "Invoice",
      "boundingBox": [12, 34, 112, 34, 112, 58, 12, 58]
    },
    {
      "text": "#12345",
      "boundingBox": [130, 34, 210, 34, 210, 58, 130, 58]
    }
    // ... more words ...
  ]
}
```

> **Randfall:** Einige Bilder können leere `"words"`‑Arrays erzeugen, wenn die OCR‑Engine keinen Text erkennen kann. In diesem Fall prüfen Sie die Bildqualität (Kontrast, Auflösung), bevor Sie fortfahren.

---

## Schritt 5: Das JSON in ein Python‑Dictionary parsen

Die Arbeit mit nativen Python‑Strukturen ist weitaus einfacher als das Herumspielen mit Strings. Verwenden Sie die Funktion `json.loads()`, um den String zu konvertieren.

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

Jetzt ist `layout_data["words"]` eine Liste von Dictionaries, jedes repräsentiert ein Wort und seine Bounding‑Box.

---

## Schritt 6: Über Wörter iterieren und **Bounding‑Box‑Koordinaten** erhalten

Hier ist der Kern unseres Tutorials: Durch jedes Wort schleifen, den Text extrahieren und die Koordinaten ausgeben. Genau hier **erhalten wir Bounding‑Box‑Koordinaten**.

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**Beispielausgabe** (Ihre Zahlen werden je nach Bild variieren):

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **Warum das Acht‑Punkte‑Format?** Die vier Ecken (oben‑links, oben‑rechts, unten‑rechts, unten‑links) erlauben es, ein Polygon um das Wort zu zeichnen, selbst wenn der Text schräg steht. Wenn Sie nur ein einfaches Rechteck benötigen, können Sie `x_min = min(x1, x2, x3, x4)`, `y_min = min(y1, y2, y3, y4)`, `width = max(x…) - x_min` und `height = max(y…) - y_min` berechnen.

---

## Optionale Erweiterungen

### 1. Bounding‑Boxes in einfache Rechtecke umwandeln

Falls Ihr nachgelagertes Tool `(x, y, width, height)` statt acht Punkten erwartet, fügen Sie einen Helfer hinzu:

```python
def box_to_rect(box):
    xs = box[0::2]  # extract x coordinates
    ys = box[1::2]  # extract y coordinates
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min, x_max - x_min, y_max - y_min)

for word in layout_data["words"]:
    rect = box_to_rect(word["boundingBox"])
    print(f"'{word['text']}' rectangle {rect}")
```

### 2. Mehrseitige PDFs verarbeiten

Aspose OCR kann PDF‑Streams akzeptieren. Ersetzen Sie die Zeile zum Laden des Bildes durch:

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

Iterieren Sie `set_page_number` für jede Seite und sammeln Sie die Koordinaten pro Seite.

### 3. Bounding‑Boxes visualisieren

Wenn Sie die Boxen auf dem Originalbild sehen möchten, verwenden Sie Pillow:

```python
from PIL import Image, ImageDraw

img = Image.open("YOUR_DIRECTORY/invoice.png")
draw = ImageDraw.Draw(img)

for word in layout_data["words"]:
    box = word["boundingBox"]
    # Pillow expects a list of tuples [(x1,y1), (x2,y2), ...]
    polygon = [(box[i], box[i+1]) for i in range(0, len(box), 2)]
    draw.line(polygon + [polygon[0]], fill="red", width=2)

img.show()
```

Jetzt sehen Sie rote Umrandungen um jedes erkannte Wort – perfekt zum Debuggen oder für UI‑Overlays.

---

## Häufige Fragen & Stolperfallen

- **Was tun, wenn das JSON riesig ist?** Bei großen Dokumenten sollten Sie das JSON streamen oder seitenweise verarbeiten, um den Speicherverbrauch gering zu halten.  
- **Warum fehlen einige Wörter?** Niedriger Kontrast oder handschriftlicher Text bringen OCR‑Engines häufig aus dem Tritt. Vorverarbeiten Sie das Bild (Kontrast erhöhen, binarisieren), bevor Sie es an Aspose übergeben.  
- **Kann ich Koordinaten auf Zeichenebene erhalten?** Ja – setzen Sie `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`, um ein `"characters"`‑Array mit eigenen `boundingBox`‑Werten zu erhalten.  
- **Ist das Koordinatensystem nullbasiert?** Ja. (0, 0) ist die obere linke Ecke des Bildes.

---

## Vollständiges Skript – Zum Kopieren & Ausführen bereit

Unten finden Sie das komplette, lauffähige Beispiel, das alle Schritte kombiniert. Speichern Sie es als `extract_bboxes.py` und führen Sie `python extract_bboxes.py` aus.

```python
import aspose.ocr as ocr
import json

# -------------------------
# 1️⃣ Initialize OCR engine
# -------------------------
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))

# -------------------------------------------------
# 2️⃣ Ask for JSON layout output (contains bounding boxes)
# -------------------------------------------------
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)

# -------------------------
# 3️⃣ Run recognition
# -------------------------
result = engine.recognize()
layout_json = result.get_json()

# -------------------------
# 4️⃣ Parse JSON
# -------------------------
layout_data = json.loads(layout_json)

# -------------------------
# 5️⃣ Helper to turn 8‑point box into rectangle (optional)
# -------------------------
def box_to_rect(box):
    xs = box[0::2]
    ys = box[1::2]
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}