---
category: general
date: 2026-01-12
description: Führen Sie OCR schnell auf PNG-Dateien mit Python aus. Erfahren Sie,
  wie Sie Text aus Bildern und Rechnungen extrahieren und Bilder für OCR mit Aspose.OCR
  laden.
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: de
og_description: Führen Sie OCR sofort auf PNG aus. Dieser Leitfaden zeigt, wie man
  Text aus Bild und Rechnung extrahiert, das Bild für OCR lädt und die Ergebnisse
  als JSON und CSV speichert.
og_title: OCR auf PNG ausführen – Vollständiges Python‑Tutorial
tags:
- OCR
- Python
- Image Processing
title: OCR auf PNG ausführen – Vollständiger Python‑Leitfaden zum Extrahieren von
  Text aus Bildern
url: /de/python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR auf PNG ausführen – Vollständiger Python‑Leitfaden zum Extrahieren von Text aus Bildern

Haben Sie jemals **OCR auf PNG**‑Dateien ausführen müssen, waren sich aber nicht sicher, welche Bibliothek saubere, strukturierte Ergebnisse liefert? Sie sind nicht allein. In vielen realen Projekten – denken Sie an Rechnungsautomatisierung oder Beleg‑Scanning – ist der erste Schritt, **Text aus Bild**‑Dateien zu extrahieren, und PNG ist ein gängiges Format, weil es verlustfreie Qualität bewahrt.

In diesem Tutorial führen wir Sie anhand eines praxisnahen Beispiels mit dem Aspose.OCR‑Python‑Paket. Am Ende des Leitfadens wissen Sie, wie Sie **image for OCR laden**, jede Textzeile extrahieren, die Daten in ein übersichtliches JSON‑Objekt umwandeln und sogar in CSV für die Weiterverarbeitung exportieren können. Keine Umschweife, nur eine praktische, sofort einsetzbare Lösung.

## Was Sie lernen werden

- Wie man die Aspose.OCR‑Bibliothek installiert und importiert.  
- Die genauen Schritte, um **OCR auf PNG** auszuführen und das Ergebnisobjekt zu verarbeiten.  
- Methoden, um **Text aus Rechnung**‑Dateien zu extrahieren und die Ausgabe als JSON oder CSV zu formatieren.  
- Tipps zum Umgang mit kontrastarmen Bildern, mehrsprachigen Dokumenten und Vertrauenswerten.  
- Ein vollständiges Copy‑and‑Paste‑Code‑Beispiel, das Sie noch heute ausführen können.

> **Voraussetzung:** Python 3.8+ und Grundkenntnisse in pip. Wenn Sie Aspose noch nie verwendet haben, keine Sorge – dieser Leitfaden deckt alles ab, was Sie für den Einstieg benötigen.

---

## Schritt 1 – Aspose.OCR installieren und Ihre Umgebung vorbereiten

Bevor wir **OCR auf PNG** ausführen können, muss die Bibliothek auf Ihrem System vorhanden sein.

```bash
pip install aspose-ocr
```

> **Pro‑Tipp:** Verwenden Sie eine virtuelle Umgebung (`python -m venv venv`), um Abhängigkeiten zu isolieren. Das verhindert Versionskonflikte, wenn Sie mehrere Projekte gleichzeitig verwalten.

Sobald die Installation abgeschlossen ist, importieren wir die benötigten Module:

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

Hier importieren wir `asposeocr` für die eigentliche Verarbeitung und die eingebaute `json`‑Bibliothek für die spätere Serialisierung.

---

## Schritt 2 – OCR‑Engine erstellen und Sprache festlegen

Die OCR‑Engine ist die Kernkomponente, die tatsächlich die Pixel liest. Für die meisten englischen Rechnungen benötigen Sie das englische Sprachpaket:

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Warum das wichtig ist:** Durch die Angabe der Sprache wird der Zeichensatz eingeschränkt, was die Genauigkeit erhöht und die Verarbeitung beschleunigt. Wenn Sie mehrsprachige Rechnungen verarbeiten müssen, ersetzen Sie einfach `ocr.Language.ENGLISH` durch das passende Enum.

---

## Schritt 3 – Bild für OCR laden

Jetzt **laden wir das Bild für OCR**. Die Methode `Image.load` akzeptiert einen Dateipfad und funktioniert mit PNG, JPEG, BMP und mehr.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **Randfall:** Wenn das PNG ungewöhnlich groß ist (über 5 MB), sollten Sie es zuerst verkleinern, um den Speicherverbrauch im Rahmen zu halten. Pillow kann das in einer einzigen Zeile erledigen:

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

---

## Schritt 4 – OCR auf PNG ausführen und Ergebnis erfassen

Mit der bereitstehenden Engine und dem geladenen Bild ist es Zeit, **OCR auf PNG** auszuführen und das strukturierte Ergebnis abzurufen.

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

Das Objekt `ocr_result` enthält eine Sammlung von `OcrRegion`‑Elementen, jedes mit dem erkannten Text und einem Vertrauenswert (0‑100). Hier erhalten Sie die granularen Daten, die zum **Extrahieren von Text aus Rechnung**‑Zeilen nötig sind.

---

## Schritt 5 – Ergebnis in JSON konvertieren und hübsch ausgeben

Die meisten nachgelagerten Systeme lieben JSON, also wandeln wir die OCR‑Ausgabe in einen schön formatierten String um.

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### Sample Output

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

Beachten Sie, dass jede Zeile eine Vertrauensmetrik enthält – perfekt, um Einträge mit niedriger Sicherheit herauszufiltern, wenn Sie **Text aus Rechnung** automatisch extrahieren möchten.

---

## Schritt 6 – OCR‑Daten als CSV speichern (eine Zeile pro Text + Vertrauenswert)

CSV ist ideal für Tabellenkalkulationen oder schnelle Datenimporte. Aspose bietet einen Einzeiler, um alles in eine CSV‑Datei zu schreiben.

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

Die erzeugte CSV‑Datei sieht folgendermaßen aus:

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

Sie können sie jetzt in Excel, Google Sheets öffnen oder in eine Datenbank einspielen.

---

## Bonus – Umgang mit Text niedriger Sicherheit und mehrseitigen PDFs

### Filtern nach Vertrauenswert

Wenn Sie nur Zeilen mit hoher Sicherheit möchten, filtern Sie das JSON, bevor Sie es schreiben:

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### Mehrseitige Dokumente

Aspose.OCR erstellt automatisch einen neuen `page`‑Eintrag für jede Seite in einem mehrseitigen PNG oder PDF. Durchlaufen Sie `ocr_data["pages"]`, um alle zu verarbeiten – kein zusätzlicher Code nötig.

---

## Vollständiges funktionierendes Beispiel

Unten finden Sie das **complete script**, das Sie sofort kopieren, einfügen und ausführen können. Ersetzen Sie `YOUR_DIRECTORY` durch den Ordner, der Ihre PNG‑Datei enthält.

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

Führen Sie das Skript mit `python run_ocr.py` aus und Sie sehen die JSON‑Ausgabe in der Konsole, eine CSV‑Datei auf der Festplatte und eine gefilterte Liste von Einträgen mit hoher Sicherheit.

---

## Häufig gestellte Fragen

**F: Kann ich das verwenden, um Text aus einem gescannten Beleg statt einer Rechnung zu extrahieren?**  
A: Absolut. Der gleiche Arbeitsablauf gilt – zeigen Sie einfach `image_path` auf Ihr Beleg‑PNG. Wenn der Beleg eine andere Sprache verwendet, wechseln Sie `engine.language` entsprechend.

**F: Was ist, wenn mein PNG gedrehten Text enthält?**  
A: Aspose.OCR erkennt die Ausrichtung automatisch, aber bei hartnäckigen Fällen können Sie das Bild mit Pillow manuell drehen, bevor Sie es an die Engine übergeben.

**F: Benötige ich eine kostenpflichtige Lizenz für Aspose.OCR?**  
A: Die Bibliothek bietet einen kostenlosen Evaluierungsmodus mit Wasserzeichen im Ergebnis. Für den Produktionseinsatz benötigen Sie eine Lizenz, die Sie auf der Aspose‑Website erhalten können.

---

## Fazit

Wir haben alles behandelt, was Sie benötigen, um **OCR auf PNG**‑Dateien mit Python auszuführen: Installation des SDK, Laden des Bildes, Extrahieren strukturierten Textes und Speichern des Ergebnisses als JSON oder CSV. Egal, ob Sie **Text aus Bild** für ein einfaches Skript oder **Text aus Rechnung** für eine automatisierte Buchhaltungspipeline extrahieren möchten, die obigen Schritte bieten Ihnen eine solide, produktionsbereite Grundlage.

Als Nächstes könnten Sie folgendes erkunden:

- Integration der CSV‑Ausgabe in eine Datenbank für die massenhafte Rechnungsablage.  
- Hinzufügen einer Nachbearbeitung mit regulären Ausdrücken, um Daten, Beträge oder Steuer‑IDs zu extrahieren.  
- Nutzung der Funktion `ocr_engine.recognize_barcode`, falls Ihre Rechnungen QR‑Codes enthalten.

Probieren Sie es aus, passen Sie die Vertrauens‑Schwellenwerte an und sehen Sie, wie Ihr Dokumenten‑Verarbeitungs‑Workflow zum Kinderspiel wird. Haben Sie weitere Fragen oder ein cooles Anwendungsbeispiel? Hinterlassen Sie unten einen Kommentar – happy OCRing!

![run OCR on PNG example](run-ocr-on-png.png "run OCR on PNG – visual example of OCR result")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}