---
category: general
date: 2026-07-05
description: Extrahiere Text aus einem Bild mit Python OCR. Erfahre, wie du ein Bild
  für OCR lädst, Text aus einem Bereich liest und Text aus einer Rechnung mit wenigen
  Codezeilen extrahierst.
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: de
og_description: Extrahiere Text aus Bildern mit Python OCR. Dieser Leitfaden zeigt,
  wie man ein Bild für OCR lädt, Text aus einem Bereich liest und Text schnell aus
  einer Rechnung extrahiert.
og_title: Text aus Bild extrahieren – Text aus Region mittels OCR lesen
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Text aus Bild extrahieren – Text aus Region mit OCR lesen
url: /de/python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bild extrahieren – Text aus Region mit OCR lesen

Haben Sie schon einmal **extract text from image** extrahieren müssen, aber nur ein bestimmter Teil ist relevant – zum Beispiel der Gesamtbetrag auf einer Rechnung? Sie sind nicht allein. In vielen real‑world Projekten werden Sie feststellen, dass Sie **read text from region** benötigen, anstatt das gesamte Bild zu verarbeiten. Glücklicherweise können Sie mit ein paar Zeilen Python ein Bild für OCR laden, einen Region‑of‑Interest (ROI) definieren und exakt die Zeichen herausziehen, die Sie brauchen.

In diesem Tutorial gehen wir Schritt für Schritt durch ein vollständiges, ausführbares Beispiel, das zeigt, wie man **load image for OCR**, einen ROI einrichtet und schließlich **extract text from invoice**. Am Ende haben Sie ein sofort einsetzbares Snippet, das mit jeder gängigen OCR‑Bibliothek funktioniert, die region‑basierte Erkennung unterstützt.

---

## Was Sie benötigen

- Python 3.8+ (der Code funktioniert auch mit 3.10)  
- Ein OCR‑Paket, das eine `OcrEngine`‑Klasse bereitstellt (für die Demo verwenden wir ein fiktives `ocr`‑Modul; ersetzen Sie es durch `pytesseract`, `easyocr` oder eine andere Bibliothek, die ROI‑Unterstützung bietet)  
- Ein Beispielbild – z. B. `invoice.png` – das klaren, gedruckten Text enthält  
- Grundlegende Kenntnisse in Python‑Funktionen und -Klassen (kein Deep‑Learning‑Hintergrund nötig)

Wenn Sie das bereits haben, super – lassen Sie uns loslegen. Wenn nicht, holen Sie sich das neueste Python von python.org und installieren Sie das OCR‑Paket via `pip install your-ocr-lib`.

---

![Extract text from image example](extract-text-from-image.png "Extract text from image – region based OCR demo")

*Das Bild oben zeigt die Region (rotes Rechteck), die wir anvisieren, um **extract text from image** zu erhalten.*

---

## Schritt 1: OCR‑Bibliothek installieren und importieren

Stellen Sie zunächst sicher, dass die OCR‑Bibliothek in Ihrer Umgebung verfügbar ist. Das Import‑Muster unten funktioniert für die meisten Pakete, die eine High‑Level `OcrEngine`‑Klasse bereitstellen.

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **Pro‑Tipp:** Wenn Sie `pytesseract` verwenden, müssen Sie die Tesseract‑Binary separat installieren und `pytesseract.pytesseract.tesseract_cmd` auf deren Pfad setzen.

---

## Schritt 2: OCR‑Engine erstellen und Sprache festlegen

Die Erstellung der Engine ist unkompliziert, aber das Festlegen der Sprache verbessert die Genauigkeit erheblich, besonders bei Rechnungen, die Zahlen und englische Wörter enthalten.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

Warum machen wir das? Die OCR‑Engine nutzt Sprachmodelle, um Zeichen vorherzusagen; wenn Sie ihr mitteilen, dass Englisch erwartet wird, reduziert das Fehlinterpretationen wie das Verwechseln von „0“ mit „O“.

---

## Schritt 3: Bild für OCR laden

Jetzt **load image for OCR** wir tatsächlich. Die meisten Bibliotheken akzeptieren einen Dateipfad oder ein Pillow‑Image‑Objekt. Hier benutzen wir den eingebauten Loader der Bibliothek zur Vereinfachung.

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

Achten Sie darauf, dass der Pfad auf das richtige Verzeichnis zeigt; ein häufiger Fehler ist das Vergessen des relativen Pfads, wenn das Skript aus einem anderen Arbeitsverzeichnis ausgeführt wird.

---

## Schritt 4: Region of Interest (ROI) definieren

Die Definition des ROI ist das Herzstück von **read text from region**. Stellen Sie sich vor, Sie zeichnen ein Rechteck um den Teil der Rechnung, der den Gesamtbetrag enthält.

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left` und `top` repräsentieren die X‑ bzw. Y‑Koordinaten der oberen linken Ecke des Rechtecks.  
- `width` und `height` bestimmen die Größe des Kastens.  
- Sie können mit verschiedenen Werten experimentieren, indem Sie einen Bildbetrachter verwenden, der Pixelkoordinaten anzeigt.

> **Warum ROI wichtig ist:** Das Ausführen von OCR auf der gesamten Seite verschwendet CPU‑Zyklen und führt oft zu Rauschen durch unrelated text, tables, or graphics. Durch das Fokussieren auf eine Region erhalten Sie sauberere Ergebnisse und schnellere Verarbeitung.

---

## Schritt 5: OCR auf der angegebenen Region ausführen

Mit allem bereit, **extract text from image** wir schließlich – jedoch nur innerhalb des definierten ROI.

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

Die `recognize`‑Methode gibt ein Objekt zurück, das typischerweise den Roh‑String, Confidence‑Scores und manchmal Bounding‑Boxes für jedes Wort enthält. Für unser Beispiel benötigen wir nur den reinen Text.

---

## Schritt 6: Extrahierten Text ausgeben

Lassen Sie uns das Ergebnis ausgeben und sehen, was wir erhalten haben. Dieser Schritt demonstriert **extract text from invoice** in einem real‑world Szenario.

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### Erwartete Ausgabe

```
Text inside ROI:
Total Amount: $1,245.67
```

Verwendet Ihre Rechnung ein anderes Layout, sehen Sie den Text, der innerhalb des Rechtecks liegt – möglicherweise eine Rechnungsnummer, ein Datum oder eine Bestellreferenz.

---

## Schritt 7: Alles in eine wiederverwendbare Funktion verpacken (optional)

Um die Lösung für mehrere Rechnungen wiederverwendbar zu machen, kapseln Sie die Logik in einer Funktion. Das illustriert zudem **ocr on region** als generische Hilfsfunktion.

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

Sie können die Funktion nun mit jeder Rechnung aufrufen:

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

---

## Häufige Stolperfallen & wie man sie vermeidet

| Problem | Warum es passiert | Lösung |
|-------|----------------|-----|
| **Leere Ausgabe** | ROI deckt keinen Text ab (falsche Koordinaten). | Pixelwerte mit einem Bildeditor überprüfen; ein visuelles Debug‑Overlay hinzufügen. |
| **Unsinnige Zeichen** | Niedrige Bildauflösung oder schlechter Kontrast. | Bild vorverarbeiten: in Graustufen konvertieren, Thresholding anwenden (`cv2.threshold`). |
| **Falsche Sprache** | Engine verwendet standardmäßig eine Sprache ohne benötigten Zeichensatz. | Explizit `ocr_engine.language` auf `ENGLISH` oder das passende Locale setzen. |
| **Performance‑Verzögerungen** | Wiederholtes OCR auf großen Bildern. | Bild vor dem Laden verkleinern oder zuerst das ROI ausschneiden und nur das ausschneiden. |

---

## Erweiterung: Mehrere ROIs

Manchmal enthält eine Rechnung mehrere Felder, die Sie benötigen – etwa **extract text from invoice** für sowohl den Gesamtbetrag als auch das Rechnungsdatum. Sie können über eine Liste von Rechtecken iterieren:

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

Dieses Muster hält Ihren Code sauber und ermöglicht es, später weitere Regionen hinzuzufügen.

---

## Fazit

Wir haben gerade einen kompletten End‑to‑End‑Workflow vorgestellt, um **extract text from image** mit Python OCR zu realisieren, wobei der Fokus auf einer spezifischen Region liegt. Durch **loading image for OCR**, das Definieren einer **region of interest** und das Aufrufen der Engine können Sie zuverlässig **read text from region** – ideal, um Beträge aus Rechnungen, Daten aus Quittungen oder andere lokalisierte Informationen zu extrahieren.  

Viel Spaß beim Experimentieren


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Features meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}