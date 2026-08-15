---
category: general
date: 2026-03-26
description: Erfahren Sie, wie Sie ein Bild drehen und OCR in Python durchführen.
  Dieser Leitfaden zeigt außerdem, wie man ein Bild für OCR vorverarbeitet und Text
  aus dem Bild effizient extrahiert.
draft: false
keywords:
- how to rotate image
- how to perform ocr
- preprocess image for ocr
- recognize text from image
- how to extract text from image
language: de
og_description: Wie man ein Bild korrekt dreht und anschließend Text aus dem Bild
  mit Aspose OCR erkennt. Folgen Sie diesem Schritt‑für‑Schritt‑Tutorial, um das Bild
  für OCR vorzubereiten und Text aus dem Bild zu extrahieren.
og_title: Wie man ein Bild dreht und OCR durchführt – Vollständiger Python-Leitfaden
tags:
- Aspose
- Python
- Image Processing
- OCR
title: Wie man ein Bild rotiert und OCR mit Aspose in Python durchführt
url: /de/python-java/general/how-to-rotate-image-and-perform-ocr-with-aspose-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein Bild dreht und OCR mit Aspose in Python durchführt

Haben Sie sich schon einmal gefragt, **wie man ein Bild dreht**, damit eine OCR‑Engine den Text tatsächlich lesen kann? Vielleicht haben Sie ein Formular gescannt, das seitlich gelandet ist, oder eine Kameraaufnahme wurde um 90° im Uhrzeigersinn gedreht. In diesem Fall sieht der Text für das menschliche Auge in Ordnung aus, aber die OCR‑Engine sieht ein Durcheinander. Die gute Nachricht? Es ist ein Kinderspiel, die Orientierung zu korrigieren, den interessierenden Bereich zuzuschneiden und dann den Text zu extrahieren – alles mit wenigen Zeilen Python und den Aspose‑Bibliotheken.

In diesem Tutorial gehen wir den gesamten Workflow durch: vom Laden eines gedrehten TIFFs, Korrigieren seiner Orientierung, **Bild für OCR vorverarbeiten**, bis hin zum **Erkennen von Text aus Bild**. Am Ende wissen Sie **wie man OCR durchführt** auf jedem Bild und können **Text aus Bilddateien** zuverlässig **extrahieren**.

## Was Sie benötigen

- Python 3.8+ (der Code funktioniert mit jeder aktuellen Version)
- `asposeocrjava` und `asposeimaging` Pakete, installiert via `pip`
- Ein Beispielbild, das gedreht werden muss (z. B. `rotated_form.tif`)
- Ein wenig Neugierde für Bildverarbeitung

Keine schweren Frameworks nötig – nur die beiden Aspose‑Pakete und ein bisschen Python‑Logik.

---

## Schritt 1: Aspose‑Pakete installieren (Wie man OCR durchführt)

Bevor wir **Bild drehen** oder **Text aus Bild erkennen** können, benötigen wir die Bibliotheken, die die eigentliche Arbeit erledigen.

```bash
pip install asposeocrjava asposeimaging
```

> **Pro‑Tipp:** Wenn Sie hinter einem Firmen‑Proxy sitzen, fügen Sie `--proxy http://proxy:port` zum Befehl hinzu. Die Pakete sind reine Python‑Wrapper um den Aspose .NET/Java‑Kern, sodass die Installation in der Regel sofort erfolgt.

---

## Schritt 2: Quelldatei laden und drehen – Der Kernschritt „Wie man ein Bild dreht“

```python
from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

# Load the original, incorrectly oriented image
source_image = Image.load("YOUR_DIRECTORY/rotated_form.tif")

# Rotate 90° clockwise – this fixes the orientation for OCR
rotated_image = source_image.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)
```

> **Warum drehen?** Die meisten OCR‑Engines gehen davon aus, dass Text von links nach rechts und von oben nach unten verläuft. Wenn das Bitmap seitlich liegt, liefert die Engine entweder Kauderwelsch oder gar nichts. Das Drehen richtet das Pixelraster an der erwarteten Lesereihenfolge aus und verbessert die Genauigkeit dramatisch.

> **Randfall:** Wenn Sie nicht sicher sind, ob das Bild um 90°, 180° oder 270° gedreht werden muss, können Sie `source_image.width` gegen `source_image.height` prüfen oder die EXIF‑Orientierungstags verwenden. Asposes `rotate_flip`‑Methode unterstützt zudem `ROTATE_180` und `ROTATE_270_CLOCKWISE`.

> **Bildvorschau (optional):**  
> ![Beispiel für Bild drehen](/assets/rotate-demo.png "Bild drehen – Vorher und nachher")

---

## Schritt 3: Interessierenden Bereich zuschneiden – Bild für OCR vorverarbeiten

Oft benötigen Sie nur einen kleinen Teil der Seite – etwa ein Unterschriftsfeld oder einen Zahlenblock. Das Zuschneiden entfernt Rauschen und beschleunigt **wie man OCR durchführt**.

```python
# Define the rectangle that encloses the text you care about
# (x=100, y=200, width=800, height=300) – adjust to your form
roi = Rectangle(100, 200, 800, 300)

# Crop the rotated image to that rectangle
roi_image = rotated_image.crop(roi)
```

> **Warum zuschneiden?** Durch die Reduzierung der Bildgröße wird der Suchraum der OCR‑Engine eingeschränkt, was Fehlalarme reduziert und die Verarbeitungszeit verkürzt. Außerdem hilft es, wenn die Quelldatei Wasserzeichen oder andere Grafiken enthält, die die Engine verwirren könnten.

> **Tipp:** Wenn Sie mehrere Felder haben, wiederholen Sie den Zuschnitt mit verschiedenen Rechtecken und führen OCR für jedes Stück separat aus.

---

## Schritt 4: OCR‑Engine initialisieren – Der Kern von „Wie man OCR durchführt“

```python
# Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

> **Im Hintergrund:** Aspose OCR verwendet eine Kombination aus Tesseract und proprietärer Bildanalyse. Die Engine einmal zu instanziieren und für mehrere Bilder wiederzuverwenden ist effizienter, als jedes Mal ein neues Objekt zu erzeugen.

---

## Schritt 5: Das zugeschnittene Bild übergeben und Text erkennen – Wie man Text aus Bild extrahiert

```python
# Set the cropped image as the input for OCR
ocr_engine.set_image(roi_image)

# Run the recognition process
result = ocr_engine.recognize()

# Extract the plain text
extracted_text = result.get_text()
print(extracted_text)
```

### Erwartete Ausgabe

Enthält das ROI die Phrase „Invoice #12345 – Paid“, sehen Sie etwa Folgendes:

```
Invoice #12345 – Paid
```

Wenn die OCR Schwierigkeiten hat, können zusätzliche Leerzeichen oder falsch erkannte Zeichen auftauchen (z. B. „Invo1ce #I2345 – Pa1d“). Hier kommen **Bild für OCR vorverarbeiten**‑Tricks ins Spiel – etwa Kontrast anpassen oder Binärisierung anwenden. Aspose bietet weitere Filter, die Sie vor Schritt 5 anketten können, aber der Grundablauf funktioniert für die meisten sauberen Scans.

---

## Schritt 6: Optional – OCR‑Einstellungen feinjustieren (Fortgeschrittenes „Wie man OCR durchführt“)

Wenn Sie höhere Genauigkeit für eine bestimmte Sprache benötigen oder bestimmte Zeichen ignorieren wollen, können Sie die Engine anpassen:

```python
# Example: Restrict recognition to English alphanumerics only
ocr_engine.get_recognition_settings().set_recognition_language("en")
ocr_engine.get_recognition_settings().set_characters_blacklist("!@#$%^&*()")
```

> **Wann verwenden:** Nutzen Sie dies, wenn das Dokument viele dekorative Symbole enthält, die Sie nicht benötigen. Das Blacklisting reduziert falsche Erkennungen.

---

## Vollständiges End‑zu‑End‑Skript

Alles zusammengefügt, hier ein sofort ausführbares Skript, das **wie man ein Bild dreht**, **Bild für OCR vorverarbeitet** und schließlich **Text aus Bild erkennt**:

```python
# -*- coding: utf-8 -*-
"""
Complete example: rotate, crop, and OCR an image with Aspose.
Author: Your Name
Date: 2026-03-26
"""

from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

def ocr_rotated_image(
    input_path: str,
    output_path: str = None,
    crop_rect: Rectangle = Rectangle(100, 200, 800, 300)
) -> str:
    """
    Loads an image, rotates it 90° clockwise, crops the region of interest,
    runs OCR, and returns the extracted text.

    Parameters
    ----------
    input_path : str
        Path to the original (possibly rotated) image file.
    output_path : str, optional
        If provided, saves the processed (rotated + cropped) image for inspection.
    crop_rect : Rectangle, optional
        Rectangle defining the ROI. Adjust to match your document layout.

    Returns
    -------
    str
        The plain text extracted from the ROI.
    """
    # Load and rotate
    src = Image.load(input_path)
    rotated = src.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)

    # Crop to region of interest
    roi = rotated.crop(crop_rect)

    # Optionally save the processed image for debugging
    if output_path:
        roi.save(output_path)

    # OCR
    engine = OcrEngine()
    engine.set_image(roi)
    result = engine.recognize()
    return result.get_text()

if __name__ == "__main__":
    text = ocr_rotated_image(
        "YOUR_DIRECTORY/rotated_form.tif",
        output_path="processed_roi.png"
    )
    print("=== Extracted Text ===")
    print(text)
```

Beim Ausführen dieses Skripts wird der erkannte Text in der Konsole ausgegeben und ein Bild des verarbeiteten ROI als `processed_roi.png` gespeichert. Sie können dieses PNG öffnen, um zu prüfen, ob Drehung und Zuschnitt wie erwartet funktioniert haben.

---

## Häufige Fragen & Stolperfallen

| Frage | Antwort |
|----------|--------|
| **Was, wenn das Bild bereits korrekt ausgerichtet ist?** | Der Drehschritt ist idempotent – das Drehen eines korrekt ausgerichteten Bildes um 90° würde es natürlich zerstören, also sollten Sie `source_image.width` gegen `height` prüfen oder EXIF‑Orientierungsdaten nutzen, bevor Sie `rotate_flip` aufrufen. |
| **Meine OCR‑Ausgabe enthält zusätzliche Zeilenumbrüche.** | Verwenden Sie `result.get_text().replace("\n", " ").strip()`, um aufzuräumen, oder aktivieren Sie `ocr_engine.get_recognition_settings().set_remove_line_breaks(True)`. |
| **Kann ich PDFs direkt verarbeiten?** | Ja – Aspose Imaging kann PDF‑Seiten als Bilder laden (`Image.load("file.pdf")`), danach folgen dieselben Dreh‑ und OCR‑Schritte. |
| **Gibt es eine Möglichkeit, viele Dateien stapelweise zu verarbeiten?** | Verpacken Sie `ocr_rotated_image` in eine Schleife über ein Verzeichnis oder nutzen Sie Python’s `concurrent.futures`, um parallel zu arbeiten. |
| **Wie gehe ich mit anderen Sprachen als Englisch um?** | Setzen Sie die Erkennungssprache via `ocr_engine.get_recognition_settings().set_recognition_language("fr")` für Französisch usw. |

---

## Fazit

Wir haben behandelt, **wie man ein Bild korrekt dreht**, **Bild für OCR vorverarbeitet** durch Zuschneiden und schließlich **wie man OCR durchführt**, um **Text aus Bild** zu **extrahieren** mit den Python‑Bibliotheken von Aspose. Das vollständige Skript demonstriert einen praktischen, produktionsreifen Workflow, den Sie in jede Automatisierungspipeline einbinden können.

Wenn Sie weitergehen möchten, probieren Sie:

- **Bildverbesserung** (Kontrast, Binärisierung) vor OCR
- **Mehrere ROI‑Extraktionen** für Formulare mit mehreren Feldern
- **Batch‑Verarbeitung** ganzer Ordner gescannter Dokumente
- **Integration** in nachgelagerte Systeme (z. B. Extrahierte Daten in eine Datenbank einspielen)

Passen Sie den Code gern an Ihren Anwendungsfall an und viel Spaß beim Coden! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}