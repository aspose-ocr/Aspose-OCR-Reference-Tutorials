---
category: general
date: 2026-03-26
description: Lernen Sie, wie man ein Bild begradigt, Text aus einem Bild erkennt und
  eine Bildvorverarbeitungspipeline erstellt, um Rauschen aus dem Scan zu entfernen
  und das gescannte Bild in Text zu konvertieren.
draft: false
keywords:
- how to deskew image
- recognize text from image
- image preprocessing pipeline
- remove noise from scan
- convert scanned image to text
language: de
og_description: Wie man ein Bild begradigt und einen schiefen Scan in durchsuchbaren
  Text umwandelt. Folgen Sie dieser Anleitung, um Text aus einem Bild zu erkennen,
  Rauschen aus dem Scan zu entfernen und das gescannte Bild in Text zu konvertieren.
og_title: Wie man ein Bild entzerrt – Schritt‑für‑Schritt OCR‑Leitfaden
tags:
- OCR
- image-processing
- Python
title: Wie man ein Bild entzerrt – Vollständiger Leitfaden mit OCR
url: /de/python-java/general/how-to-deskew-image-complete-guide-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein Bild entneigt – Vollständiger Leitfaden mit OCR

Haben Sie sich jemals gefragt, **wie man ein Bild entneigt**, das von einem günstigen Scanner stammt? Sie sind nicht allein. Eine schiefe Seite wirkt unprofessionell und, was noch wichtiger ist, die Neigung kann jede OCR‑Engine, die versucht, **Text aus Bild zu erkennen**, durcheinanderbringen.  

In diesem Tutorial führen wir Sie durch eine komplette **Bildvorverarbeitungspipeline**, die ein Scan entneigt, binarisiert und entrauscht, und es dann an eine OCR‑Engine übergibt, sodass Sie **gescanntes Bild in Text umwandeln** können – mit minimalem Aufwand. Kein Zauber, nur reines Python und eine kleine Bibliothek, die die schwere Arbeit übernimmt.

## Was Sie benötigen

- Python 3.9+ (der Code funktioniert mit 3.10 und neuer)
- Das `ocr`‑Paket (Installation via `pip install ocr‑toolkit` – ersetzen Sie es durch den tatsächlichen Bibliotheksnamen)
- Ein gescanntes JPEG oder PNG, das deutlich schief ist (z. B. `skewed_scan.jpg`)
- Ein wenig Neugier, warum jeder Vorverarbeitungsschritt wichtig ist

Das war's. Keine schweren Abhängigkeiten wie OpenCV, es sei denn, Sie möchten später tiefer einsteigen.

## Schritt 1: Das gescannte Bild laden

Der erste Schritt besteht darin, die Datei in den Speicher zu laden. Dieser Schritt ist einfach, aber entscheidend – wenn der Pfad falsch ist, bricht alles andere zusammen.

```python
# Step 1: Load the scanned image
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)
```

> **Warum?**  
> Das Laden des Bildes liefert uns ein manipulierbares Objekt, mit dem `ocr.ImagePreprocessor` arbeiten kann. Das Überspringen dieses Schrittes würde die Pipeline blind für die tatsächlichen Pixeldaten machen.

## Wie man ein Bild entneigt und für OCR vorbereitet

Jetzt, da wir das Bild haben, richten wir es gerade aus. Die Methode `deskew()` schätzt den Neigungswinkel und dreht das Bild wieder horizontal.

```python
# Step 2: Create an image preprocessor and correct the orientation
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()
```

> **Profi‑Tipp:** Wenn Ihre Scans nur leicht abweichen (≤ 3°), ist der Standard‑Algorithmus in der Regel exakt. Bei extremen Winkeln müssen Sie möglicherweise die internen Parameter anpassen – prüfen Sie die Bibliotheks‑Dokumentation für `max_angle`.

## Bild binarisieren – Schwarz‑weiß machen

OCR‑Engines lieben Eingaben mit hohem Kontrast. Die Umwandlung des Bildes in eine binäre (schwarz‑weiße) Darstellung entfernt subtile Abstufungen, die die Zeichenerkennung verwirren können.

```python
# Step 3: Convert the image to a binary (black‑and‑white) representation
preprocessor.binarize(threshold=128)
```

> **Was passiert?**  
> Pixel, die heller als 128 sind, werden weiß; alles andere wird schwarz. Passen Sie den Schwellenwert an, wenn Ihr Scan ungewöhnlich dunkel oder hell ist.

## Rauschen aus dem Scan vor OCR entfernen

Selbst ein perfekt entneigtes Bild kann Sprenkel, Staub oder Kompressionsartefakte enthalten. Diese kleinen Punkte sind der Feind jeder OCR‑Engine.

```python
# Step 4: Reduce noise to improve OCR accuracy
preprocessor.denoise(radius=1)
```

> **Warum Rauschen entfernen?**  
> Rauschen erzeugt falsche Kanten, die die OCR‑Engine als Zeichen interpretieren könnte. Ein kleiner Radius reicht für die meisten Scans; erhöhen Sie ihn bei stark körnigen Dokumenten.

## Bildvorverarbeitungspipeline anwenden

Alle Konfigurationen sind gesetzt – jetzt führen wir die Pipeline auf dem Originalbild aus.

```python
# Step 5: Apply the preprocessing pipeline to the loaded image
processed_image = preprocessor.apply(original_image)
```

> **Ergebnis:** `processed_image` ist ein bereinigtes, gerades, hochkontrastiertes Bitmap, bereit für die Textextraktion.

## Text aus Bild mit OCR‑Engine erkennen

Zeit, den Text tatsächlich zu lesen. Wir initialisieren die OCR‑Engine, übergeben ihr unser aufbereitetes Bild und fragen nach dem Roh‑String.

```python
# Step 6: Initialise the OCR engine and provide the processed image
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# Step 7: Recognise text and output the result
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Erwartete Ausgabe** (Beispiel):

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Wenn Sie unleserliche Zeichen sehen, überprüfen Sie den Entneigungs‑Schritt erneut oder experimentieren Sie mit einem anderen `threshold`‑Wert.

## Aufbau einer Bildvorverarbeitungspipeline – Vollständiges Skript

Alles zusammengefügt, hier ein einzelnes, ausführbares Skript, das Sie in eine `.py`‑Datei einfügen und ausführen können:

```python
import ocr  # Replace with the actual import path of your OCR library

# -------------------------------------------------
# 1️⃣ Load the scanned image
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)

# -------------------------------------------------
# 2️⃣ Deskew – how to deskew image
# -------------------------------------------------
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()

# -------------------------------------------------
# 3️⃣ Binarize – convert to black‑and‑white
# -------------------------------------------------
preprocessor.binarize(threshold=128)

# -------------------------------------------------
# 4️⃣ Denoise – remove noise from scan
# -------------------------------------------------
preprocessor.denoise(radius=1)

# -------------------------------------------------
# 5️⃣ Apply the pipeline
# -------------------------------------------------
processed_image = preprocessor.apply(original_image)

# -------------------------------------------------
# 6️⃣ OCR – recognize text from image
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# -------------------------------------------------
# 7️⃣ Output – convert scanned image to text
# -------------------------------------------------
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Tipp:** Packen Sie das Ganze in eine Funktion (`def ocr_from_file(path): …`), wenn Sie viele Dateien stapelweise verarbeiten möchten.

## Häufige Fragen & Sonderfälle

- **Was, wenn das Bild bereits gerade ist?**  
  Die Methode `deskew()` erkennt einen nahezu Null‑Winkel und lässt das Bild unverändert, sodass Sie sie sicher auf jede Datei anwenden können.

- **Mein Scan ist in Farbe – soll ich sie behalten?**  
  Farbe liefert für die meisten OCR‑Aufgaben keinen Mehrwert. Die Binarisierung entfernt sie, beschleunigt die Verarbeitung und reduziert den Speicherverbrauch.

- **Kann ich mehrere Vorverarbeitungsschritte verketten?**  
  Absolut. Die Klasse `ImagePreprocessor` ist für Pipelines konzipiert; Sie können `sharpen()`, `contrast_enhance()` oder benutzerdefinierte Filter hinzufügen, bevor Sie `apply()` aufrufen.

- **Die OCR‑Ausgabe enthält unerwünschte Zeilenumbrüche – wie behebe ich das?**  
  Verarbeiten Sie den String nach mit `text.replace("\n", " ").strip()` oder verwenden Sie eine fortgeschrittenere Layout‑Analyse‑Bibliothek wie Tesserats `--psm`‑Modi.

## Nächste Schritte

Jetzt, da Sie wissen, **wie man ein Bild entneigt** und eine solide **Bildvorverarbeitungspipeline** haben, könnten Sie folgendes erkunden:

- Die Integration von **Text aus Bild erkennen** in eine Flask‑API für sofortige Dokument‑Uploads.
- Die Nutzung der Pipeline zum **Rauschen aus Scan entfernen** bei historischen Dokumenten, bei denen die Erhaltung entscheidend ist.
- Das Hochskalieren, um tausende Seiten stapelweise zu verarbeiten und ein durchsuchbares PDF mit `pdfminer` oder `PyMuPDF` auszugeben.

Fühlen Sie sich frei, mit verschiedenen Schwellenwerten, Entrausch‑Radien zu experimentieren oder sogar das OCR‑Backend gegen Tesseract auszutauschen, wenn Sie mehrsprachige Unterstützung benötigen. Die Grundlagen bleiben gleich: gerade ausrichten, säubern, dann lesen.

---

*Viel Spaß beim Coden! Wenn Sie auf Probleme stoßen, hinterlassen Sie unten einen Kommentar – ich helfe Ihnen gern, die Pipeline zu optimieren.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}