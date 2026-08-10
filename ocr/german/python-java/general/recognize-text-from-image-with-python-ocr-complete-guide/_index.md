---
category: general
date: 2026-06-16
description: Texterkennung aus Bildern mit einer Python‑OCR‑Engine – lernen Sie, wie
  Sie Text von Quittungen extrahieren und die OCR‑Genauigkeit in Minuten verbessern.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- improve ocr accuracy
- python ocr tutorial
- image preprocessing for OCR
language: de
og_description: Erkenne Text aus Bildern schnell. Dieser Leitfaden zeigt, wie man
  Text von Quittungen extrahiert und die OCR‑Genauigkeit mit Python verbessert.
og_title: Text aus Bild mit Python OCR erkennen – Komplettanleitung
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text from image using a Python OCR engine – learn how to
    extract text from receipt and improve OCR accuracy in minutes.
  headline: recognize text from image with Python OCR – Complete Guide
  type: TechArticle
- description: recognize text from image using a Python OCR engine – learn how to
    extract text from receipt and improve OCR accuracy in minutes.
  name: recognize text from image with Python OCR – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - Basic familiarity with pip and
      virtual environments. - A sample receipt image (JPEG or PNG) that you want to
      process. - The `ocr` package (the example uses a fictional `ocr` module for
      illustration; replace it with `pytesseract`, `easyocr`, or any library t'
  - name: Expected Output
    text: 'Running the script on a typical grocery receipt yields something like:'
  - name: H3 – Crop to the Receipt Region
    text: 'If your image contains a lot of background (e.g., a photo of a desk), crop
      it first:'
  - name: H3 – Use a Custom Language Pack
    text: 'For receipts that contain foreign characters (e.g., “€” or “¥”), load the
      appropriate language data:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Text aus Bild mit Python OCR erkennen – Komplettanleitung
url: /de/python-java/general/recognize-text-from-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bild mit Python OCR – Komplettanleitung

Haben Sie jemals **Text aus Bild erkennen** müssen, aber die Ergebnisse sahen wie Kauderwelsch aus? Sie sind nicht allein. In vielen Kleinunternehmens‑Szenarien – denken Sie an das Scannen von Quittungen, das Digitalisieren von Rechnungen oder das Auslesen von Daten aus Ausweisen – ist ein sauberes, zuverlässiges Ergebnis der Unterschied zwischen einem reibungslosen Arbeitsablauf und einem Ärgernis.

In diesem Tutorial führen wir Sie durch eine praktische Methode, **Text aus Bild zu erkennen** mit einer leichtgewichtigen Python‑OCR‑Bibliothek. Wir zeigen Ihnen außerdem genau, wie Sie **Text aus Quittungen** extrahieren können und teilen Tricks, um **die OCR‑Genauigkeit zu verbessern**, ohne teure Software zu kaufen. Bereit? Dann legen wir los.

## Was Sie bauen werden

Am Ende dieses Leitfadens haben Sie ein sofort ausführbares Skript, das:

1. Eine OCR‑Engine instanziiert.  
2. Intelligente Vorverarbeitung aktiviert (deskew, despeckle, binarization).  
3. Ein verrauschtes Quittungs‑Bild lädt.  
4. Die Erkennungspipeline automatisch ausführt.  
5. Sauberen, durchsuchbaren Text in der Konsole ausgibt.

Keine externen Dienste, keine versteckten API‑Schlüssel – nur reiner Python‑Code, den Sie an jedes Projekt anpassen können.

### Voraussetzungen

- Python 3.8+ auf Ihrem Rechner installiert.  
- Grundlegende Kenntnisse im Umgang mit pip und virtuellen Umgebungen.  
- Ein Beispiel‑Quittungs‑Bild (JPEG oder PNG), das Sie verarbeiten möchten.  
- Das `ocr`‑Paket (das Beispiel verwendet ein fiktives `ocr`‑Modul zur Veranschaulichung; ersetzen Sie es durch `pytesseract`, `easyocr` oder eine andere Bibliothek mit einer ähnlichen API).

> **Profi‑Tipp:** Wenn Sie auf fehlende Abhängigkeiten stoßen, installieren Sie diese mit `pip install ocr` (oder dem tatsächlichen Paketnamen), bevor Sie fortfahren.

## Schritt 1 – Text aus Bild erkennen: Engine einrichten

Zuerst das Wichtigste. Wir benötigen ein Objekt, das Pixel‑Daten lesen und in Zeichen umwandeln kann. Betrachten Sie die Engine als das Gehirn des Vorgangs; alles andere liefert ihr Informationen.

```python
import ocr  # Replace with your actual OCR library import

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

Warum die Engine manuell erstellen? Einige Bibliotheken erlauben einen Aufruf einer einzigen Funktion, aber eine explizite Instanz gibt Ihnen eine feinkörnige Kontrolle über die Vorverarbeitung – genau das, was wir später benötigen, um **die OCR‑Genauigkeit zu verbessern**.

## Schritt 2 – Text aus Quittung extrahieren: Vorverarbeitung aktivieren

Eine mit dem Handy gescannte Quittung ist selten perfekt. Sie kann leicht geneigt sein, Staubflecken enthalten oder unter ungleichmäßiger Beleuchtung leiden. Das Aktivieren der Vorverarbeitung übernimmt die schwere Arbeit, bevor die Engine überhaupt die Buchstaben betrachtet.

```python
# Step 2: Enable preprocessing to improve recognition quality
preprocess = engine.preprocessing
preprocess.deskew = True        # Auto‑rotate slightly tilted pages
preprocess.despeckle = True     # Remove isolated noise pixels
preprocess.binarization = True  # Convert image to pure black‑white
```

*Deskew* richtet die Seite gerade, *despeckle* entfernt störende Punkte, und *binarization* zwingt jeden Pixel, entweder schwarz oder weiß zu sein. Diese drei Flags allein können die **OCR‑Genauigkeit** bei verrauschten Quittungen um 20‑30 % **verbessern**.

## Schritt 3 – Bild laden, das Sie erkennen möchten

Jetzt richten wir die Engine auf die eigentliche Datei. Der Pfad kann absolut oder relativ sein; stellen Sie einfach sicher, dass das Bild existiert.

```python
# Step 3: Load the scanned receipt image
engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/receipt-noisy.jpg")
```

Falls Sie sich fragen, ob die Engine PDFs oder mehrseitige TIFFs unterstützt, tun dies die meisten modernen Bibliotheken – prüfen Sie einfach die Dokumentation. Für ein einseitiges JPEG reicht die obige Zeile aus.

## Schritt 4 – OCR ausführen – Die Engine erledigt den Rest

Mit konfigurierter Vorverarbeitung und geladenem Bild erledigt der nächste Aufruf alles: Es führt die Vorverarbeitung durch, läuft den Erkennungsalgorithmus und gibt ein Ergebnis‑Objekt zurück.

```python
# Step 4: Run OCR – the configured preprocessing is applied automatically
ocr_result = engine.recognize()
```

Im Hintergrund kann die Engine Tesseract, ein neuronales Netzwerk oder eine proprietäre Engine verwenden. Sie müssen die Interna nicht kennen; Sie erhalten einfach ein sauberes Ergebnis.

## Schritt 5 – Erkannten Text ausgeben

Schließlich extrahieren wir den Klartext aus dem Ergebnis und geben ihn aus. In einer echten Anwendung könnten Sie ihn in eine Datenbank, eine CSV‑Datei schreiben oder sogar in eine nachgelagerte Analyse‑Pipeline einspeisen.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### Erwartete Ausgabe

Das Ausführen des Skripts auf einer typischen Supermarkt‑Quittung liefert etwa Folgendes:

```
WALMART STORE #1234
123 Main St.
Anytown, USA

Date: 06/15/2026   Time: 14:32
Cashier: J. Doe

Item                Qty   Price
---------------------------------
Milk                1     2.99
Bread               2     5.48
Eggs                1     3.20
---------------------------------
Subtotal                    11.67
Tax                         0.93
Total                       12.60
```

Wenn die Ausgabe unleserlich erscheint, prüfen Sie, ob die Vorverarbeitungs‑Flags aktiviert sind und das Bild nicht zu dunkel ist. Das Anpassen des Binarisierungs‑Schwellwerts (einige Bibliotheken erlauben das Setzen eines eigenen Werts) kann die **OCR‑Genauigkeit** weiter **verbessern**.

## Fortgeschritten: Feinabstimmung zum schnelleren Extrahieren von Text aus Quittungen

Während der Fünf‑Schritte‑Ablauf für die meisten Fälle funktioniert, möchten Sie vielleicht die Verarbeitung beschleunigen, wenn Sie nachts Hunderte von Quittungen verarbeiten. Hier sind ein paar optionale Optimierungen:

### H3 – Auf den Quittungsbereich zuschneiden

Falls Ihr Bild viel Hintergrund enthält (z. B. ein Foto eines Schreibtisches), schneiden Sie es zuerst zu:

```python
engine.image = engine.image.crop((50, 200, 800, 1200))  # left, top, right, bottom
```

### H3 – Eigenes Sprachpaket verwenden

Für Quittungen, die Fremdzeichen enthalten (z. B. „€“ oder „¥“), laden Sie die entsprechenden Sprachdaten:

```python
engine.set_language('eng+deu+fra')  # English, German, French
```

Beide Tricks helfen der Engine, **Text aus Bild** zuverlässiger zu **erkennen**, besonders wenn das Ausgangsmaterial variiert.

## Häufige Fallstricke und wie man sie vermeidet

- **Fehlende Schriftarten:** Einige OCR‑Engines benötigen die Schriftdateien für spezialisierte Quittungs‑Schriften. Installieren Sie die entsprechenden Sprachpakete.  
- **Zu viel Rauschen:** Selbst bei `despeckle=True` können extrem körnige Scans die Engine verwirren. Ein schneller manueller Filter in Pillow (`Image.filter(ImageFilter.MedianFilter)`) kann helfen.  
- **Falsche DPI:** OCR‑Engines gehen von etwa 300 dpi aus. Wenn Ihr Bild niedriger ist, skalieren Sie es zuerst: `engine.image = engine.image.resize((width*2, height*2))`.

Das direkte Beheben dieser Probleme **verbessert die OCR‑Genauigkeit**, ohne auf teure Drittanbieter‑Dienste zurückzugreifen.

## Vollständiges Skript – Bereit zum Ausführen

Unten finden Sie das vollständige, ausführbare Python‑Programm, das alles, was wir besprochen haben, integriert. Speichern Sie es als `receipt_ocr.py` und führen Sie `python receipt_ocr.py` aus.

```python
import ocr  # Replace with the actual library you use

def main():
    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Enable preprocessing steps
    preprocess = engine.preprocessing
    preprocess.deskew = True
    preprocess.despeckle = True
    preprocess.binarization = True

    # Load the receipt image (change the path to your file)
    engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/receipt-noisy.jpg")

    # Optional: crop out unnecessary background
    # engine.image = engine.image.crop((50, 200, 800, 1200))

    # Run the recognition pipeline
    result = engine.recognize()

    # Print the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

Das Ausführen dieses Skripts wird **Text aus Bild erkennen** und einen schön formatierten Block von Quittungsdaten ausgeben. Passen Sie gerne die Zuschneide‑Koordinaten, Spracheinstellungen oder Vorverarbeitungs‑Flags an Ihre eigenen Quittungs‑Layouts an.

## Fazit

Wir haben gerade einen einfachen Weg gezeigt, **Text aus Bild** mit Python zu **erkennen**, demonstriert, wie man **Text aus Quittungen** extrahiert, und mehrere praktische Tipps vorgestellt, um **die OCR‑Genauigkeit zu verbessern**. Die Kernidee ist simpel: Eine OCR‑Engine einrichten, intelligente Vorverarbeitung aktivieren, ihr ein sauberes Bild zuführen und die Bibliothek die schwere Arbeit erledigen lassen.

Nächste Schritte? Versuchen Sie, einen Stapel von Quittungen in einer Schleife zu verarbeiten, jedes Ergebnis in einer CSV zu speichern oder die Ausgabe in ein Buchhaltungssystem zu integrieren. Sie können auch mit Deep‑Learning‑basierten OCR‑Bibliotheken wie `easyocr` experimentieren, um noch höhere Genauigkeit bei komplexen Schriften zu erreichen.

Haben Sie Fragen zu einem bestimmten Quittungsformat oder möchten Sie wissen, wie man mehrseitige PDFs verarbeitet? Hinterlassen Sie unten einen Kommentar, und viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Text aus Bild extrahieren mit Aspose OCR – Schritt‑für‑Schritt‑Anleitung](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Wie man Text aus Bild extrahiert, indem man Rechtecke in OCR vorbereitet](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Text aus Bild extrahieren – OCR‑Optimierung mit Aspose.OCR für .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}