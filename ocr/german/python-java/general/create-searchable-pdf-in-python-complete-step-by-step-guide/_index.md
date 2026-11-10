---
category: general
date: 2026-06-19
description: Erstelle ein durchsuchbares PDF aus einem Bild mit Python‑OCR. Lerne,
  OCR in ein PDF zu konvertieren, Text aus einem Bild zu extrahieren und OCR schnell
  auf ein Bild anzuwenden.
draft: false
keywords:
- create searchable pdf
- convert ocr to pdf
- extract text from image
- convert image to pdf
- perform ocr on image
language: de
og_description: Erstelle ein durchsuchbares PDF aus einem Bild mit Python‑OCR. Dieser
  Leitfaden zeigt, wie man OCR in ein PDF umwandelt, Text aus einem Bild extrahiert
  und OCR auf ein Bild anwendet.
og_title: Erstelle durchsuchbare PDF in Python – Vollständige Programmieranleitung
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  headline: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  name: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  steps:
  - name: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
    text: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
  - name: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
    text: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
  - name: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
    text: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
  type: HowTo
tags:
- OCR
- Python
- PDF
- ImageProcessing
title: Durchsuchbare PDFs in Python erstellen – Vollständige Schritt‑für‑Schritt‑Anleitung
url: /de/python-java/general/create-searchable-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Erstelle durchsuchbare PDFs in Python – Vollständige Schritt‑für‑Schritt‑Anleitung

Hast du schon einmal **durchsuchbare PDFs** aus einem gescannten Beleg erstellen wollen, wusstest aber nicht, wo du anfangen sollst? Du bist nicht allein – vielen Entwicklern stößt man an dieselbe Hürde, wenn sie versuchen, ein Bild von Text in ein PDF zu verwandeln, das man tatsächlich durchsuchen kann.  

In diesem Tutorial gehen wir eine praktische Lösung durch, mit der du **OCR auf Bild** ausführen, das OCR‑Ergebnis in ein **durchsuchbares PDF** umwandeln und sogar den Rohtext extrahieren kannst, falls du ihn für weitere Verarbeitung benötigst. Kein Schnickschnack, nur ein funktionierendes Beispiel, das du noch heute in dein Projekt kopieren‑und‑einfügen kannst.

## Was du lernen wirst

- Wie du eine leichte OCR‑Engine in Python einrichtest  
- Die genauen Schritte, um **OCR in PDF zu konvertieren** und als durchsuchbares Dokument zu speichern  
- Methoden, um **Text aus Bild zu extrahieren** für nachgelagerte Analysen  
- Tipps zum Umgang mit häufigen Stolperfallen wie Bildorientierung und großen Dateien  
- Ein vollständiges, ausführbares Skript, das du an deinen Anwendungsfall anpassen kannst

### Voraussetzungen

- Python 3.8+ auf deinem Rechner installiert  
- Grundlegende Kenntnisse im Umgang mit pip und virtuellen Umgebungen (optional, aber empfohlen)  
- Eine Bilddatei (PNG, JPEG usw.), die klaren, maschinenlesbaren Text enthält  

Wenn du das hast, legen wir los.

## Schritt 1: Installiere die benötigte Bibliothek

Der Code‑Ausschnitt, den du vorher gesehen hast, verwendet ein fiktives `ocr`‑Paket, aber dieselben Ideen gelten für reale Bibliotheken wie **EasyOCR**, **pytesseract** oder **pdfminer.six**. Für diese Anleitung nutzen wir **EasyOCR**, weil es reines Python ist, viele Sprachen unterstützt und eine praktische PDF‑Konvertierungsmethode über einen Hilfs‑Helper bereitstellt.

```bash
pip install easyocr pillow
```

> **Profi‑Tipp:** Installiere innerhalb einer virtuellen Umgebung (`python -m venv venv && source venv/bin/activate`), um deine Abhängigkeiten sauber zu halten.

## Schritt 2: Initialisiere die OCR‑Engine – OCR auf Bild ausführen

Jetzt, wo die Bibliothek bereit ist, erstellen wir eine OCR‑Engine und geben ihr an, mit englischem Text zu arbeiten. Das ist der erste Ort, an dem wir **OCR auf Bild** ausführen.

```python
import easyocr
from PIL import Image
import io

# Create an EasyOCR reader for English
reader = easyocr.Reader(['en'])  # ← performs OCR on image
```

Warum benötigen wir ein dediziertes Reader‑Objekt? EasyOCR lädt Sprachmodelle im Voraus, sodass die Wiederverwendung desselben `reader` für mehrere Bilder weitaus effizienter ist, als ihn jedes Mal neu zu initialisieren.

## Schritt 3: Bild laden – Text aus Bild extrahieren

Lassen wir das Bild in den Speicher laden. Dieser Schritt ist später der Ort, an dem wir **Text aus Bild extrahieren**, aber zunächst laden wir es nur.

```python
# Replace with the path to your receipt or scanned document
image_path = "YOUR_DIRECTORY/receipt.png"

# Open the image with Pillow (helps with format handling)
pil_image = Image.open(image_path).convert("RGB")
```

Falls dein Bild verkehrt herum oder schief ist, solltest du Pillow‑Methoden wie `rotate` oder `transpose` verwenden, bevor du es an die OCR‑Engine übergibst. Ein kurzer visueller Check kann dir später Stunden an Fehlersuche ersparen.

## Schritt 4: OCR‑Engine ausführen und Ergebnisse erfassen

Hier kommt der Kern des Prozesses – das Bild an die OCR‑Engine senden und strukturierte Daten zurückbekommen.

```python
# EasyOCR returns a list of (bbox, text, confidence) tuples
ocr_result = reader.readtext(image_path, detail=1, paragraph=True)
```

Das Flag `detail=1` liefert uns Begrenzungsrahmen, die wir später benötigen, wenn wir **OCR in PDF konvertieren**. Wenn du nur an den rohen Zeichenketten interessiert bist, setze `detail=0`.

## Schritt 5: OCR‑Ergebnis in ein durchsuchbares PDF konvertieren – OCR in PDF konvertieren

EasyOCR bietet keinen direkten PDF‑Writer, aber wir können das PDF selbst zusammenstellen, indem wir Pillow und die Bibliothek `reportlab` verwenden. Um das Tutorial leichtgewichtig zu halten, nutzen wir `fpdf2`, das uns erlaubt, das Originalbild einzubetten und unsichtbaren Text darüber zu legen.

```bash
pip install fpdf2
```

```python
from fpdf import FPDF

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        # Set invisible text style
        self.set_text_color(255, 255, 255)   # white on white background
        self.set_font("Helvetica", size=12)

        for bbox, text, conf in ocr_data:
            # bbox = [(x1,y1), (x2,y2), (x3,y3), (x4,y4)]
            x_min = min(point[0] for point in bbox)
            y_min = min(point[1] for point in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

# Create PDF instance with the original image as background
pdf = SearchablePDF(image_path)

# Add invisible OCR text on top of the image
pdf.add_ocr_text(ocr_result)

# Save the searchable PDF
output_path = "YOUR_DIRECTORY/receipt_searchable.pdf"
pdf.output(output_path)
```

Was ist gerade passiert? Wir haben das gescannte Bild als sichtbare Ebene platziert und dann die erkannten Wörter darüber geschrieben, wobei wir weißen Text verwenden, der mit dem weißen Hintergrund verschmilzt. Suchwerkzeuge lesen trotzdem die verborgene Ebene, sodass das PDF **durchsuchbar** wird, ohne das visuelle Erscheinungsbild zu verändern.

## Schritt 6: PDF‑Bytes speichern – Bild in PDF konvertieren

Wenn du das PDF lieber im Speicher halten möchtest (z. B. zum Versand über eine API), kannst du die Bytes erfassen, anstatt direkt auf die Festplatte zu schreiben.

```python
pdf_bytes = pdf.output(dest='S').encode('latin1')  # returns a byte string

# Example: write bytes to a file (same as Step 5 but shows the conversion)
with open(output_path, "wb") as f:
    f.write(pdf_bytes)
```

Diese Zeile demonstriert den klassischen **Bild‑zu‑PDF konvertieren**‑Workflow: Du startest mit einem Bild, führst OCR aus, überlagerst Text und erzeugst schließlich einen PDF‑Stream.

## Schritt 7: Ergebnis prüfen – Schnell‑Checks

Nachdem du das Skript ausgeführt hast, öffne `receipt_searchable.pdf` in einem beliebigen PDF‑Betrachter und teste das Suchfeld (Strg + F). Gib ein Wort ein, von dem du weißt, dass es im Beleg vorkommt – wenn es zur richtigen Stelle springt, hast du erfolgreich **durchsuchbare PDFs erstellt**!  

Falls die Suche fehlschlägt, prüfe:

1. Die OCR‑Vertrauenswerte (`conf`‑Werte). Niedrige Werte können auf ein unscharfes Bild hinweisen.  
2. Die Koordinaten der Begrenzungsrahmen – manchmal meldet EasyOCR sie in einer anderen Orientierung.  
3. Ob der PDF‑Betrachter nicht im „nur‑Bild“-Modus ist (selten, aber manche Viewer haben diese Option).

## Vollständiges funktionierendes Skript

Alles zusammengefügt, hier die komplette, sofort ausführbare Python‑Datei:

```python
# searchable_pdf.py
import easyocr
from PIL import Image
from fpdf import FPDF

# ---------- Configuration ----------
IMAGE_PATH = "YOUR_DIRECTORY/receipt.png"
OUTPUT_PDF = "YOUR_DIRECTORY/receipt_searchable.pdf"
# ----------------------------------

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        # Fit the image to the page size
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        self.set_text_color(255, 255, 255)   # invisible white text
        self.set_font("Helvetica", size=12)
        for bbox, text, conf in ocr_data:
            x_min = min(p[0] for p in bbox)
            y_min = min(p[1] for p in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

def main():
    # 1️⃣ Initialize OCR engine – perform OCR on image
    reader = easyocr.Reader(['en'])

    # 2️⃣ Load the image – extract text from image later
    pil_image = Image.open(IMAGE_PATH).convert("RGB")

    # 3️⃣ Run OCR and capture results
    ocr_result = reader.readtext(IMAGE_PATH, detail=1, paragraph=True)

    # 4️⃣ Convert OCR result to searchable PDF – convert OCR to PDF
    pdf = SearchablePDF(IMAGE_PATH)
    pdf.add_ocr_text(ocr_result)

    # 5️⃣ Save the PDF – convert image to PDF (or keep bytes in memory)
    pdf.output(OUTPUT_PDF)
    print(f"✅ Searchable PDF saved to {OUTPUT_PDF}")

if __name__ == "__main__":
    main()
```

Speichere sie als `searchable_pdf.py`, ersetze die Platzhalter `YOUR_DIRECTORY` durch echte Pfade und führe sie aus:

```bash
python searchable_pdf.py
```

Du solltest eine Bestätigungsnachricht sehen und ein brandneues durchsuchbares PDF in deinem Ordner liegen haben.

## Häufige Fragen & Sonderfälle

**Was, wenn das Bild farbig ist?**  
EasyOCR funktioniert sowohl mit Graustufen‑ als auch mit Farbbildern, aber das Konvertieren zu Graustufen (`pil_image.convert("L")`) kann die Genauigkeit bei verrauschten Scans manchmal verbessern.

**Kann ich mehrseitige PDFs verarbeiten?**  
Ja – iteriere über jedes Seitenbild, führe die OCR‑Schritte aus und füge jede Seite zum selben `FPDF`‑Objekt hinzu. Denk daran, den Cursor für jedes neue Bild zurückzusetzen (`self.add_page()`).

**Gibt es eine Möglichkeit, die originale Textebene statt unsichtbarem weißem Text zu behalten?**  
Wenn du ein echtes „Text‑unter‑Bild“‑PDF (z. B. für Barrierefreiheit) benötigst, erwäge `pdfminer` oder `pikepdf`, um eine versteckte Textebene mit korrekten PDF‑Tags einzubetten. Das ist fortgeschrittener, aber das Prinzip bleibt gleich: Hintergrundbild + überlagerter Text.

**Was, wenn die OCR‑Vertrauenswerte niedrig sind?**  
Du kannst Wörter mit geringer Vertrauenswürdigkeit herausfiltern:

```python
filtered = [item for item in ocr_result if item[2] > 0.8]  # keep >80% confidence
pdf.add_ocr_text(filtered)
```

## Fazit – Was wir erreicht haben

Wir begannen mit einem einfachen Bild eines Belegs, **OCR auf Bild** ausgeführt, die erkannten Zeichenketten extrahiert und schließlich **durchsuchbare PDFs erstellt**, die sich wie professionell gescannte Dokumente verhalten. Der Prozess deckte jedes sekundäre Schlüsselwort ab – **OCR in PDF konvertieren**, **Text aus Bild extrahieren**, **Bild in PDF konvertieren** und **OCR auf Bild ausführen** – sodass du jetzt ein wiederverwendbares Werkzeugset für jedes ähnliche Projekt hast.

### Nächste Schritte

- Experimentiere mit anderen Sprachen, indem du ihre ISO‑Codes an `easyocr.Reader(['en', 'es'])` übergibst.  
- Tausche EasyOCR gegen Tesseract aus, wenn du eine vollständig offline‑Lösung brauchst; der Rest der Pipeline bleibt gleich.  
- Füge eine Visualisierung der OCR‑Vertrauenswerte hinzu (Zeichne Begrenzungsrahmen ins Bild), um problematische Scans zu debuggen.  

Hast du eine eigene Variante, die du teilen möchtest? Hinterlasse einen Kommentar, forke das Repository.

## Was solltest du als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit du weitere API‑Funktionen meistern und alternative Implementierungsansätze in deinen eigenen Projekten erkunden kannst.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}