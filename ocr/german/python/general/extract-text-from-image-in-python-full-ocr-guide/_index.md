---
category: general
date: 2026-06-25
description: Extrahiere Text aus einem Bild mit Python‑OCR. Lerne, wie man ein Bild
  für OCR lädt, OCR in Python durchführt und einen Beleg in JSON konvertiert – in
  wenigen einfachen Schritten.
draft: false
keywords:
- extract text from image
- load image for OCR
- perform OCR in Python
- convert receipt to JSON
language: de
og_description: Extrahiere Text aus einem Bild mit Python‑OCR. Dieses Tutorial führt
  dich durch das Laden eines Bildes für OCR, die Durchführung von OCR in Python und
  die Umwandlung einer Quittung in JSON.
og_title: Text aus Bild in Python extrahieren – Vollständige OCR-Anleitung
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  headline: Extract Text from Image in Python – Full OCR Guide
  type: TechArticle
- description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  name: Extract Text from Image in Python – Full OCR Guide
  steps:
  - name: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
    text: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
  - name: '**Load an image for OCR** – tell the engine which file to read.'
    text: '**Load an image for OCR** – tell the engine which file to read.'
  - name: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
    text: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
  - name: '**Run the recognition** – actually perform OCR in Python.'
    text: '**Run the recognition** – actually perform OCR in Python.'
  - name: '**Print or store the result** – convert receipt to JSON and see the output.'
    text: '**Print or store the result** – convert receipt to JSON and see the output.'
  - name: Sends the image through a pre‑trained convolutional network.
    text: Sends the image through a pre‑trained convolutional network.
  - name: Decodes the network output into readable characters.
    text: Decodes the network output into readable characters.
  - name: Packages everything into the selected format (JSON in our case).
    text: Packages everything into the selected format (JSON in our case).
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- JSON
title: Text aus Bild in Python extrahieren – Vollständige OCR-Anleitung
url: /de/python/general/extract-text-from-image-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bild in Python extrahieren – Vollständiger OCR‑Leitfaden

Hast du jemals **Text aus einem Bild extrahieren** müssen, wusstest aber nicht, wo du anfangen sollst? In diesem Tutorial führen wir dich Schritt für Schritt durch das **Laden eines Bildes für OCR**, das **Durchführen von OCR in Python** und das **Umwandeln eines Belegs in JSON** – alles mit nur wenigen Code‑Zeilen.

Wenn du schon einmal eine Beleg‑Scanner‑App, einen Ausgaben‑Tracker gebaut hast oder einfach die Dateneingabe automatisieren möchtest, wirst du sehen, warum das Beherrschen dieses Ablaufs ein echter Game‑Changer ist. Am Ende hast du ein funktionierendes Skript, das ein Bild eines Belegs einliest und ein sauberes JSON‑Payload ausgibt, das bereit für nachgelagerte Services ist.

## Was du lernen wirst

Wir decken jeden Schritt von der Installation der `aocr`‑Bibliothek bis hin zur Verarbeitung des Roh‑Ergebnisses ab. Konkret lernst du:

1. **Eine OCR‑Engine‑Instanz erstellen** – der Einstiegspunkt für alle Erkennungsaufgaben.  
2. **Ein Bild für OCR laden** – der Engine mitteilen, welche Datei sie lesen soll.  
3. **Das Export‑Format wählen** – JSON oder XML, wir nehmen JSON, weil es einfacher zu konsumieren ist.  
4. **Die Erkennung ausführen** – OCR in Python tatsächlich durchführen.  
5. **Das Ergebnis ausgeben oder speichern** – Beleg in JSON umwandeln und die Ausgabe sehen.

Vorkenntnisse in OCR sind nicht nötig; du brauchst nur ein einfaches Python‑Setup und eine Bilddatei (einen Beleg, einen Flyer, was immer du möchtest).  

---

![Diagramm, das den Ablauf der Textextraktion aus einem Bild mit Python OCR zeigt](extract-text-from-image-python-ocr.png){alt="Textextraktion aus Bild mit Python OCR"}

## Text aus Bild extrahieren – Schritt‑für‑Schritt Python OCR

Unten findest du das komplette, sofort ausführbare Skript. Kopiere es gern in eine Datei namens `receipt_ocr.py` und führe `python receipt_ocr.py` aus.

```python
# receipt_ocr.py

# 1️⃣ Import the aocr package (make sure it's installed via `pip install aocr`)
import aocr

# 2️⃣ Create an OCR engine instance – this object orchestrates the whole process
engine = aocr.OcrEngine()

# 3️⃣ Load the image you want to process.
#    Replace the path with the location of your receipt or any image.
engine.load_image("YOUR_DIRECTORY/receipt.png")

# 4️⃣ Choose the output format. JSON is handy for APIs and downstream services.
engine.export_format = aocr.ExportFormat.JSON

# 5️⃣ Run the recognition and obtain the raw result.
json_result = engine.recognize()

# 6️⃣ Output the raw JSON string – you can also write it to a file if you prefer.
print(json_result)
```

### Warum das funktioniert

- **Engine‑Instanz** – `aocr.OcrEngine()` kapselt das gesamte schwere Heben (Modell‑Laden, Vorverarbeitung usw.).  
- **Bild laden** – `engine.load_image()` sagt der Bibliothek genau, welches Bitmap sie analysieren soll; du kannst JPEG, PNG oder sogar mehrseitige PDFs einspeisen.  
- **Export‑Format** – Durch Setzen von `engine.export_format` auf `aocr.ExportFormat.JSON` wird das Ergebnis zu einem strukturierten String, perfekt für APIs, die JSON erwarten.  
- **Erkennungsaufruf** – `engine.recognize()` führt die neuronale Netz‑Inference im Hintergrund aus; es liefert einen JSON‑String, der erkannte Textblöcke, Vertrauenswerte und Layout‑Informationen enthält.  

---

## Bild für OCR mit aocr laden

Falls du dich fragst, ob das Bild einer speziellen Vorverarbeitung bedarf, lautet die kurze Antwort **nein** – `aocr` übernimmt die meisten gängigen Fälle (Kontrastanpassung, Entzerrung) automatisch. Du kannst jedoch die Genauigkeit erhöhen, indem du:

- Sicherstellst, dass das Bild mindestens 300 dpi hat.  
- Irrelevante Ränder abschneidest.  
- Vor dem Laden in Graustufen konvertierst (optional, `engine.load_image()` erledigt das für dich).

```python
# Optional preprocessing example using Pillow
from PIL import Image, ImageOps

original = Image.open("YOUR_DIRECTORY/receipt.png")
# Convert to grayscale and increase contrast
processed = ImageOps.autocontrast(original.convert("L"))
processed.save("processed_receipt.png")
engine.load_image("processed_receipt.png")
```

*Pro‑Tipp:* Wenn der Beleg viel Rauschen enthält, kann der zusätzliche Schritt oben die **perform OCR in Python**‑Genauigkeit merklich steigern.

---

## Export‑Format wählen und Beleg in JSON umwandeln

Vielleicht fragst du dich: „Warum nicht einfach Nur‑Text?“ Weil JSON die hierarchische Struktur (Zeilen, Wörter, Begrenzungsrahmen) bewahrt. Das macht es viel einfacher, Felder wie *Gesamtbetrag* oder *Datum* später zuzuordnen.

```python
engine.export_format = aocr.ExportFormat.JSON   # Switch to XML with aocr.ExportFormat.XML if needed
```

Wenn du das Skript ausführst, sieht `json_result` etwa so aus (gekürzt zur Übersicht):

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "bbox": [12, 34, 210, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.96,
          "bbox": [15, 400, 190, 420]
        }
      ]
    }
  ]
}
```

Jetzt hast du ein **convert receipt to JSON**‑Payload, das du direkt in eine Datenbank, einen REST‑Endpoint oder ein Machine‑Learning‑Modell einspeisen kannst.

---

## Erkennung ausführen und Ergebnisse abrufen

Der letzte Schritt – das eigentliche OCR – ist so einfach wie ein Aufruf von `recognize()`. Im Hintergrund erledigt die Bibliothek:

1. Das Bild durch ein vortrainiertes Convolutional‑Network zu schicken.  
2. Die Netzwerk‑Ausgabe in lesbare Zeichen zu decodieren.  
3. Alles in das gewählte Format (JSON in unserem Fall) zu verpacken.  

```python
json_result = engine.recognize()
print(json_result)   # <-- This prints the JSON string to stdout
```

Möchtest du die Ausgabe lieber speichern statt auszugeben, schreibe sie einfach in eine Datei:

```python
with open("receipt_output.json", "w", encoding="utf-8") as f:
    f.write(json_result)
```

*Randfall:* Einige Belege enthalten Nicht‑ASCII‑Zeichen (z. B. „€“). Öffne die Datei mit UTF‑8‑Kodierung, wie oben gezeigt, um verzerrten Text zu vermeiden.

---

## Vollständiges Beispiel (Alle Schritte in einem Skript)

Alles zusammengeführt, hier das finale Skript, das du von Anfang bis Ende ausführen kannst:

```python
import aocr
from PIL import Image, ImageOps

# Create engine
engine = aocr.OcrEngine()

# Optional: preprocess image for better accuracy
raw = Image.open("YOUR_DIRECTORY/receipt.png")
processed = ImageOps.autocontrast(raw.convert("L"))
processed.save("processed_receipt.png")

# Load the (processed) image
engine.load_image("processed_receipt.png")

# Choose JSON output
engine.export_format = aocr.ExportFormat.JSON

# Run OCR
json_result = engine.recognize()

# Save result
with open("receipt_output.json", "w", encoding="utf-8") as out_file:
    out_file.write(json_result)

print("OCR complete! JSON saved to receipt_output.json")
```

Starte es mit:

```bash
python receipt_ocr.py
```

Du solltest eine Bestätigungszeile sehen und im selben Ordner eine Datei `receipt_output.json`, die die strukturierten Daten enthält.

---

## Fazit

Du weißt jetzt, **wie man Text aus einem Bild extrahiert** mit Python, **wie man ein Bild für OCR lädt**, **wie man OCR in Python durchführt** und **wie man einen Beleg in JSON umwandelt** für nachgelagerte Verwendungen. Dieser End‑to‑End‑Flow ist leichtgewichtig, benötigt nur das `aocr`‑Package und lässt sich in jede Automatisierungspipeline einbinden.

Was kommt als Nächstes? Probiere das Export‑Format zu XML zu wechseln, experimentiere mit verschiedenen Bild‑Vorverarbeitungstechniken oder baue eine kleine Flask‑API, die einen hochgeladenen Beleg entgegennimmt und sofort das JSON‑Payload zurückgibt. Der Himmel ist die Grenze, sobald du die Grundlagen beherrschst.

Fragen oder Probleme? Hinterlasse einen Kommentar unten, und happy coding!

## Was du als Nächstes lernen solltest


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um dir zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in deinen eigenen Projekten zu erkunden.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}