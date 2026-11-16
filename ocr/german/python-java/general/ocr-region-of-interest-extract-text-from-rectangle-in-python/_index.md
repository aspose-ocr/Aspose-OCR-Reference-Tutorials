---
category: general
date: 2026-05-31
description: Erfahren Sie, wie Sie den OCR‑Bereich von Interesse nutzen, um ein Bild
  für die OCR zu laden und Text aus einem Rechteck zu extrahieren – ideal, um den
  Betrag auf einer Rechnung zu erkennen.
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: de
og_description: Beherrschen Sie den OCR‑Bereich von Interesse, um ein Bild für OCR
  zu laden, Text aus einem Rechteck zu extrahieren und Text aus einer Rechnung in
  einem einzigen Tutorial zu erkennen.
og_title: OCR-Region von Interesse – Schritt‑für‑Schritt Python‑Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  headline: OCR Region of Interest – Extract Text from Rectangle in Python
  type: TechArticle
- description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  name: OCR Region of Interest – Extract Text from Rectangle in Python
  steps:
  - name: Loads an invoice image from disk.
    text: Loads an invoice image from disk.
  - name: Marks a rectangular ROI where the total amount lives.
    text: Marks a rectangular ROI where the total amount lives.
  - name: Runs OCR only inside that ROI.
    text: Runs OCR only inside that ROI.
  - name: Prints the cleaned‑up amount string.
    text: Prints the cleaned‑up amount string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR-Region von Interesse – Text aus einem Rechteck in Python extrahieren
url: /de/python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Region of Interest – Text aus Rechteck in Python extrahieren

Haben Sie sich schon einmal gefragt, wie man **ocr region of interest** einen bestimmten Teil einer gescannten Rechnung ausführt, ohne die gesamte Seite an die Engine zu übergeben? Sie sind nicht der Erste, der auf einem verschwommenen Beleg starrt und sich fragt: „Wie extrahiere ich den Betrag, der irgendwo unten rechts steht?“ Die gute Nachricht ist, dass Sie der OCR‑Bibliothek genau sagen können, wo sie suchen soll, was sowohl die Geschwindigkeit als auch die Genauigkeit erheblich steigert.

In diesem Leitfaden gehen wir Schritt für Schritt durch ein vollständiges, ausführbares Beispiel, das zeigt, wie man **load image for OCR** verwendet, eine **region of interest** definiert und dann **extract text from rectangle** ausführt, um schließlich **recognize text from invoice** zu erledigen und die klassische Frage „wie extrahiere ich den Betrag“ zu beantworten. Keine vagen Verweise – nur konkreter Code, klare Erklärungen und ein paar Pro‑Tipps, die Sie gerne früher gekannt hätten.

---

## Was Sie bauen werden

Am Ende dieses Tutorials haben Sie ein kleines Python‑Skript, das:

1. Ein Rechnungs‑Bild von der Festplatte lädt.  
2. Ein rechteckiges ROI markiert, in dem der Gesamtbetrag steht.  
3. OCR nur innerhalb dieses ROI ausführt.  
4. Den bereinigten Betrag‑String ausgibt.  

All das funktioniert mit jeder OCR‑Bibliothek, die ROI unterstützt – hier verwenden wir das fiktive, aber repräsentative `SimpleOCR`‑Paket, das beliebte Werkzeuge wie Tesseract oder EasyOCR nachahmt. Sie können es problemlos austauschen; die Konzepte bleiben gleich.

---

## Voraussetzungen

- Python 3.8+ installiert (`python --version` sollte ≥3.8 anzeigen).  
- Ein per pip installierbares OCR‑Paket (z. B. `pip install simpleocr`).  
- Ein Rechnungs‑Bild (PNG oder JPEG) in einem Ordner, auf den Sie verweisen können.  
- Grundlegende Kenntnisse von Python‑Funktionen und -Klassen (nichts Besonderes).

Wenn Sie das bereits haben, großartig – lassen Sie uns loslegen. Wenn nicht, holen Sie zuerst das Bild; die restlichen Schritte sind unabhängig vom eigentlichen Dateiinhalt.

---

## Schritt 1: Bild für OCR laden

Das Erste, was jeder OCR‑Workflow benötigt, ist ein Bitmap, das gelesen werden kann. Die meisten Bibliotheken stellen eine einfache `load_image`‑Methode bereit, die einen Dateipfad akzeptiert. So geht's mit unserer `SimpleOCR`‑Engine:

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Pro‑Tipp:** Verwenden Sie absolute Pfade oder `os.path.join`, um „Datei nicht gefunden“-Überraschungen zu vermeiden, wenn das Skript aus einem anderen Arbeitsverzeichnis ausgeführt wird.

---

## Schritt 2: OCR Region of Interest definieren

Anstatt die Engine die gesamte Seite scannen zu lassen, sagen wir ihr *genau*, wo der Betrag steht. Das ist der **ocr region of interest**‑Schritt und der Schlüssel zu zuverlässiger Extraktion, besonders wenn das Dokument laute Kopf‑ oder Fußzeilen enthält.

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

Warum diese Zahlen? `x` und `y` sind Pixel‑Offsets vom oberen linken Eckpunkt, während `width` und `height` die Größe des Kastens beschreiben. Wenn Sie unsicher sind, öffnen Sie das Bild in einem beliebigen Editor, aktivieren Sie ein Lineal und notieren Sie die Koordinaten. Viele IDEs zeigen sogar die Cursor‑Position beim Überfahren an.

---

## Schritt 3: Text aus Rechteck extrahieren

Jetzt, wo das ROI gesetzt ist, bitten wir die Engine, **recognize text from invoice** zu erledigen, jedoch nur innerhalb des gerade hinzugefügten Rechtecks. Der Aufruf liefert ein Ergebnis‑Objekt, das typischerweise den Roh‑String, Vertrauenswerte und manchmal Begrenzungsrahmen enthält.

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

Im Hintergrund iteriert `recognize()` über jedes ROI, schneidet diesen Ausschnitt zu, führt das OCR‑Modell aus und fügt die Ergebnisse zusammen. Deshalb kann das Definieren eines engen **extract text from rectangle**‑Bereichs Sekunden bei Batch‑Jobs einsparen.

---

## Schritt 4: Wie man Betrag extrahiert – Ausgabe bereinigen

OCR ist nicht perfekt; Sie erhalten häufig überflüssige Leerzeichen, Zeilenumbrüche oder sogar falsch gelesene Zeichen (z. B. „S“ statt „5“). Ein kurzer `strip()` und ein kleiner Regex erledigen das meist für Geldbeträge.

```python
# Step 4: Clean and display the recognized amount
import re

raw_amount = ocr_result.text.strip()
# Simple regex to keep digits, commas, periods, and optional currency symbols
clean_amount = re.search(r'[\d,.]+', raw_amount)
if clean_amount:
    print("Amount:", clean_amount.group())
else:
    print("Could not locate a numeric amount in the ROI.")
```

> **Warum das wichtig ist:** Wenn Sie den Betrag in eine Datenbank oder ein Zahlungsgateway einspeisen wollen, benötigen Sie ein vorhersehbares Format. Das Entfernen von Leerzeichen und das Filtern nicht‑numerischer Zeichen verhindert nachgelagerte Fehler.

---

## Schritt 5: Text aus Rechnung erkennen – Vollständiges Skript

Alles zusammengeführt, hier das komplette, sofort ausführbare Skript. Speichern Sie es als `extract_amount.py` und führen Sie `python extract_amount.py` aus.

```python
# extract_amount.py
import re
from simpleocr import OcrEngine, Rectangle

def main():
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load the invoice image (adjust the path)
    ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

    # Define ROI where the amount is located
    amount_region = Rectangle(120, 340, 200, 40)
    ocr_engine.add_roi(amount_region)

    # Run OCR on the ROI
    ocr_result = ocr_engine.recognize()

    # Clean and print the amount
    raw_amount = ocr_result.text.strip()
    match = re.search(r'[\d,.]+', raw_amount)
    if match:
        print("Amount:", match.group())
    else:
        print("Could not locate a numeric amount in the ROI.")

if __name__ == "__main__":
    main()
```

### Erwartete Ausgabe

```
Amount: 1,245.67
```

Wenn das ROI falsch ausgerichtet ist, sehen Sie möglicherweise etwas wie `Amount: 1245.6S` – beachten Sie das überflüssige „S“. Passen Sie die Rechteck‑Koordinaten an und wiederholen Sie den Vorgang, bis die Ausgabe sauber aussieht.

---

## Häufige Fallstricke & Randfälle

| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| **ROI zu klein** | Der Betragstext wird abgeschnitten, was zu teilweiser Erkennung führt. | Erweitern Sie `width`/`height` um ca. 10‑20 % und testen Sie erneut. |
| **Falsche DPI** | Scans mit niedriger Auflösung (≤150 dpi) verringern die OCR‑Genauigkeit. | Resampeln Sie das Bild auf 300 dpi vor dem Laden oder bitten Sie den Scanner um höhere DPI. |
| **Mehrere Währungen** | Der Regex wählt die erste Zahlenfolge, die möglicherweise eine Rechnungsnummer ist. | Verfeinern Sie den Regex, um nach Währungssymbolen (`$`, `€`, `£`) vor den Ziffern zu suchen. |
| **Gedrehte Rechnungen** | OCR‑Engines gehen von aufrechtem Text aus; gedrehte Seiten brechen die Erkennung. | Wenden Sie eine Rotationskorrektur (`ocr_engine.rotate(90)`) an, bevor Sie die ROI hinzufügen. |
| **Rauschen im Hintergrund** | Schatten oder Stempel verwirren das Modell. | Vorverarbeiten mit einem einfachen Schwellenwert (`cv2.threshold`) oder einen Rauschfilter verwenden. |

---

## Pro‑Tipps für reale Projekte

- **Stapelverarbeitung:** Durchlaufen Sie einen Ordner mit Rechnungen, berechnen Sie das ROI dynamisch (z. B. basierend auf Vorlagenerkennung) und speichern Sie die Ergebnisse in einer CSV‑Datei.  
- **Vorlagenabgleich:** Wenn Sie mehrere Rechnungs‑Layouts bearbeiten, führen Sie eine JSON‑Map `template_id → ROI‑Koordinaten` ein. Wechseln Sie das ROI basierend auf einem schnellen Layout‑Klassifikator.  
- **Parallele Ausführung:** Nutzen Sie `concurrent.futures.ThreadPoolExecutor`, um mehrere OCR‑Instanzen gleichzeitig laufen zu lassen – ideal für hochvolumige Back‑Office‑Pipelines.  
- **Vertrauensfilterung:** Die meisten OCR‑Ergebnisse enthalten einen Confidence‑Score. Verwerfen Sie Ergebnisse unter einem Schwellenwert (z. B. 85 %) und markieren Sie sie zur manuellen Prüfung.

---

## Fazit

Wir haben alles behandelt, was Sie benötigen, um **ocr region of interest**, **load image for OCR**, **extract text from rectangle** und schließlich **recognize text from invoice** zu nutzen, um die klassische **how to extract amount**‑Frage zu beantworten. Das Skript ist kompakt, aber flexibel genug, um sich an verschiedene Dokumentformate, Sprachen und OCR‑Back‑Ends anzupassen.

Jetzt, wo Sie die Grundlagen beherrschen, überlegen Sie, den Workflow zu erweitern: Barcode‑Scanning hinzufügen, mit einem PDF‑Parser integrieren oder den extrahierten Betrag an eine Buchhaltungs‑API senden. Der Himmel ist die Grenze, und mit einem gut definierten ROI erhalten Sie stets schnellere, sauberere Ergebnisse.

Wenn Sie auf ein Problem stoßen, hinterlassen Sie unten einen Kommentar – happy OCRing!

![Beispiel für OCR Region of Interest](https://example.com/ocr_roi_example.png "Beispiel für OCR Region of Interest")


## Was sollten Sie als Nächstes lernen?

- [Wie man Text aus Bild extrahiert, indem man Rechtecke für OCR vorbereitet](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Text aus Bild Java mit Aspose.OCR Detect Areas Mode extrahieren](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Text aus Bild – OCR‑Optimierung mit Aspose.OCR für .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}