---
category: general
date: 2026-03-26
description: 'Python-OCR-Tutorial: Erfahren Sie, wie Sie Text aus einem Bild extrahieren,
  ein Bild für OCR laden und Text von einem Beleg mit Aspose OCR in nur wenigen Schritten
  erkennen.'
draft: false
keywords:
- python ocr tutorial
- extract text from image
- load image for ocr
- perform ocr in python
- recognize text from receipt
language: de
og_description: 'Python OCR‑Tutorial: Lernen Sie schnell, Text aus Bildern zu extrahieren,
  Bilder für OCR zu laden und Text von Quittungen mit Aspise OCR zu erkennen.'
og_title: Python OCR‑Tutorial – Text aus Bild extrahieren
tags:
- OCR
- Aspose
- Python
title: Python OCR‑Tutorial – Text aus Bild extrahieren mit Aspose
url: /de/python-java/general/python-ocr-tutorial-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR‑Tutorial – Text aus Bild extrahieren mit Aspose

Haben Sie sich jemals gefragt, wie man den Text aus einem verschwommenen Kassenbon oder einem gescannten Formular extrahiert, ohne Stunden damit zu verbringen, benutzerdefinierte Regexes zu schreiben? Sie sind nicht allein. In diesem **python ocr tutorial** führen wir Sie durch das Laden eines Bildes für OCR, das Durchführen von OCR in Python und schließlich das Erkennen von Text aus Kassenbon‑Dateien mithilfe der Aspose OCR‑Bibliothek.  

Am Ende dieses Leitfadens haben Sie ein sofort einsatzbereites Skript, das jedes unterstützte Bildformat einliest, den Textinhalt extrahiert und ihn in der Konsole ausgibt. Keine externen Dienste, keine API‑Schlüssel — nur reines Python und eine leistungsstarke OCR‑Engine.  

## Was Sie benötigen

- Python 3.8 oder neuer (der Code verwendet Typ‑Hints, daher ist ein aktueller Interpreter empfehlenswert)  
- `asposeocrjava`‑Paket installiert via `pip install aspose-ocr`  
- Ein Beispielbild – zum Beispiel `receipt_noisy.jpg`, das einen typischen Kassenbon enthält  
- (Optional) Eine virtuelle Umgebung, um Abhängigkeiten sauber zu halten  

Wenn Sie diese Punkte abgehakt haben, können wir direkt zum Code springen.  

## Schritt 1: Aspose OCR‑Klassen installieren und importieren

Zuerst stellen Sie sicher, dass das Aspose OCR‑Paket verfügbar ist. Dann importieren Sie die Klassen, die wir benötigen.

```python
# Install the package (run once)
# pip install aspose-ocr

# Import the required Aspose OCR modules
import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult
```

**Warum das wichtig ist:** Das Importieren nur der benötigten Symbole hält den Namensraum sauber und signalisiert dem Interpreter, welche Teile der Bibliothek wir tatsächlich verwenden. Es verkürzt außerdem spätere Code‑Zeilen und macht das Tutorial leichter nachvollziehbar.

> **Pro‑Tipp:** Wenn Sie ein Jupyter‑Notebook verwenden, setzen Sie ein `!` vor die Installationszeile, um sie in‑Zelle auszuführen.

## Schritt 2: OCR‑Engine erstellen und Deep‑Learning‑Modus aktivieren

Aspose bietet mehrere Engine‑Modi. Für die meisten realen Kassenbons liefert das Deep‑Learning‑Modell die höchste Genauigkeit, besonders bei verrauschten Scans.

```python
# Initialise the OCR engine
ocr_engine = OcrEngine()

# Switch to deep‑learning mode for better accuracy on complex images
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
```

**Warum Deep‑Learning?** Traditionelle regelbasierte OCR kann bei kontrastarmen oder verzerrten Zeichen scheitern. Das Deep‑Learning‑Modell, das auf Millionen von Glyphen trainiert wurde, passt sich besser an Variationen an — genau das, was Sie benötigen, wenn Sie *perform OCR in Python* auf Kassenbons ausführen, die mit einer Handykamera aufgenommen wurden.

## Schritt 3: Bild für OCR laden

Jetzt **load image for OCR** wir tatsächlich. Aspose.Imaging unterstützt PNG, JPEG, BMP, TIFF und mehr, sodass Sie praktisch jedes Bild eines Dokuments verwenden können.

```python
# Load the image (replace the path with your own file)
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/receipt_noisy.jpg")

# Attach the image to the OCR engine
ocr_engine.set_image(input_image)
```

**Häufiges Stolper‑Problem:** Wenn Sie das Bild nicht auf die Engine setzen, führt das zur `NullReferenceException` zur Laufzeit. Rufen Sie immer `set_image` nach dem Laden der Datei auf.

## Schritt 4: OCR ausführen und Text extrahieren

Mit der vorbereiteten Engine und dem angehängten Bild können wir endlich **perform OCR in Python** und das textuelle Ergebnis abrufen.

```python
# Run the recognition process
ocr_result: OcrResult = ocr_engine.recognize()

# Extract plain text from the result object
recognized_text = ocr_result.get_text()
```

Die Methode `recognize()` gibt ein `OcrResult`‑Objekt zurück, das nicht nur den Rohtext, sondern auch Konfidenzwerte, Begrenzungsrahmen und Sprachinformationen enthält. Für den schnellen **extract text from image**‑Anwendungsfall benötigen wir nur `get_text()`.

## Schritt 5: Erkannten Text anzeigen

Sehen wir uns an, was die Engine tatsächlich vom Kassenbon gelesen hat.

```python
print("Recognized text:\n", recognized_text)
```

Typische Ausgabe sieht so aus:

```
Recognized text:
   Store XYZ
   04/26/2026  14:32
   Item A   2.99
   Item B   5.49
   TOTAL    8.48
   THANK YOU!
```

Wenn die Ausgabe unleserliche Zeichen enthält, sollten Sie das Bild vorab bearbeiten (z. B. den Kontrast erhöhen oder einen Deskew‑Filter anwenden), bevor Sie es in die OCR‑Engine laden. Aspose.Imaging bietet eine komplette Palette an Bild‑Verbesserungs‑Tools, die Sie kombinieren können.

## Handling Edge Cases & Tips for Better Accuracy

### 1. Umgang mit extrem verrauschten Kassenbons
Wenn der Kassenbon stark verschmiert ist, können Sie zum schnelleren, aber weniger genauen Durchlauf in den `OcrEngineMode.HIGH_SPEED`‑Modus wechseln und anschließend einen zweiten Durchlauf im `DEEP_LEARNING`‑Modus auf dem bereinigten Bild ausführen.

```python
ocr_engine.set_engine_mode(OcrEngineMode.HIGH_SPEED)
# ... run first pass, then...
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
# ... run second pass on the same image
```

### 2. Sprache festlegen
Standardmäßig versucht Aspose, die Sprache automatisch zu erkennen. Für englische Kassenbons können Sie sie festlegen:

```python
ocr_engine.set_language("eng")
```

### 3. Speicherverwaltung
Beim Verarbeiten vieler Bilder in einer Schleife sollten Sie Ressourcen explizit freigeben:

```python
input_image.dispose()
ocr_engine.dispose()
```

### 4. OCR‑Ergebnisse in einer Datei speichern
Manchmal müssen Sie den extrahierten Text für spätere Analysen persistieren.

```python
with open("receipt_output.txt", "w", encoding="utf-8") as f:
    f.write(recognized_text)
```

## Vollständiges funktionierendes Beispiel

Unten finden Sie das komplette Skript, das alles zusammenführt. Kopieren Sie es in eine Datei namens `receipt_ocr.py`, passen Sie den Bildpfad an und führen Sie `python receipt_ocr.py` aus.

```python
# receipt_ocr.py
# -------------------------------------------------
# Complete Python OCR tutorial using Aspose OCR
# -------------------------------------------------

# 1️⃣ Install the package (run once):
# pip install aspose-ocr

import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult

def main():
    # 2️⃣ Initialise engine in deep‑learning mode
    engine = OcrEngine()
    engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)

    # 3️⃣ Load your receipt image
    image_path = "YOUR_DIRECTORY/receipt_noisy.jpg"   # <-- change this
    img = ocr.Imaging.Image.load(image_path)
    engine.set_image(img)

    # 4️⃣ Recognise text
    result: OcrResult = engine.recognize()
    text = result.get_text()

    # 5️⃣ Output the result
    print("=== Recognized text from receipt ===")
    print(text)

    # Optional: write to a file
    with open("receipt_output.txt", "w", encoding="utf-8") as out_file:
        out_file.write(text)

    # Clean up resources
    img.dispose()
    engine.dispose()

if __name__ == "__main__":
    main()
```

Das Ausführen des Skripts sollte den Inhalt des Kassenbons in Ihrer Konsole anzeigen und zudem `receipt_output.txt` mit denselben Daten erzeugen.

![Python OCR‑Tutorial – Beispiel für Kassenbon‑Ausgabe](https://example.com/receipt_output.png "python ocr tutorial beispiel")

*Bild‑Alt‑Text:* **python ocr tutorial – sample receipt output**

## Zusammenfassung & nächste Schritte

Wir haben gerade ein **python ocr tutorial** durchlaufen, das zeigt, wie man **load image for OCR**, **perform OCR in Python** und schließlich **recognize text from receipt**‑Dateien mit Aspose verwendet. Die wichtigsten Erkenntnisse sind:

- Wählen Sie den richtigen Engine‑Modus (Deep‑Learning für Genauigkeit)  
- Hängen Sie das Bild immer an, bevor Sie `recognize()` aufrufen  
- Nutzen Sie das `OcrResult`‑Objekt, um sauberen Text zu extrahieren, und speichern oder verarbeiten Sie ihn nach Bedarf  

Was kommt als Nächstes? Erwägen Sie, Aspose Imaging‑Filter zu verketten, um kontrastarme Scans zu verbessern, oder integrieren Sie das Skript in eine Flask‑API, sodass Sie Kassenbons über ein Web‑Formular hochladen können. Sie könnten auch das Exportieren der OCR‑Daten nach CSV für die Buchhaltungsautomatisierung untersuchen.

Haben Sie Fragen zum Umgang mit mehrseitigen PDFs oder nicht‑lateinischen Skripten? Hinterlassen Sie einen Kommentar — ich helfe gern!  

**Bereit, Ihre Dokumenten‑Automatisierung auf das nächste Level zu heben?** Schnappen Sie sich den Code, experimentieren Sie mit verschiedenen Bildern, und lassen Sie die OCR‑Engine die schwere Arbeit übernehmen. Viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}