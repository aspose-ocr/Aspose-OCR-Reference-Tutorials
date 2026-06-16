---
category: general
date: 2026-03-26
description: Erkennen Sie Text aus Bildern schnell, indem Sie lernen, wie man ein
  Bild für OCR lädt und Daten aus einem bestimmten Bereich extrahiert. Folgen Sie
  diesem praxisorientierten Leitfaden.
draft: false
keywords:
- recognize text from image
- load image for ocr
- OCR region of interest
- extract text from ROI
- Python OCR library
- image preprocessing for OCR
language: de
og_description: Erkenne Text aus einem Bild in Python, indem du ein Bild für OCR lädst,
  einen Interessensbereich definierst und sauberen Text extrahierst. Lerne den kompletten
  Arbeitsablauf.
og_title: Text aus Bild erkennen – Vollständiger Python-OCR-Leitfaden
tags:
- OCR
- Python
- Image Processing
title: Text aus Bild erkennen – Schritt‑für‑Schritt Python OCR‑Tutorial
url: /de/python-java/general/recognize-text-from-image-step-by-step-python-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bild erkennen – Vollständiger Python OCR Leitfaden

Haben Sie schon einmal **Text aus Bild** erkennen müssen, wussten aber nicht, wo Sie anfangen sollen? Vielleicht haben Sie ein gescanntes Formular, einen Kassenbon oder einen Screenshot und möchten nur die Wörter in einem bestimmten Feld extrahieren. Die gute Nachricht: Mit wenigen Zeilen Python können Sie das Bild für OCR laden, sich auf einen einzelnen Bereich konzentrieren und den genauen Text herausziehen – ohne manuelles Kopieren.

In diesem Tutorial gehen wir den gesamten Prozess durch: Bild laden, Region of Interest (ROI) definieren, OCR‑Engine ausführen und das Ergebnis ausgeben. Am Ende können Sie diesen Code‑Snippet in jedes Projekt einbinden, das Text aus einem bestimmten Bildteil extrahieren muss. Keine aufwändigen Bild‑Verarbeitungspipelines, nur sauberer, lesbarer Code, der heute funktioniert.

## Voraussetzungen

- Python 3.8+ installiert  
- Das `ocr`‑Paket (oder eine kompatible OCR‑Bibliothek) – installieren Sie es mit `pip install ocr-lib` (ersetzen Sie den Namen durch das von Ihnen verwendete Paket)  
- Ein PNG/JPEG‑Bild, das das zu lesende Formular enthält  
- Grundlegende Kenntnisse von Python‑Funktionen und -Klassen  

Wenn Sie damit bereits vertraut sind, großartig – Sie können direkt zum nächsten Abschnitt springen. Andernfalls gönnen Sie sich einen kurzen Kaffee und stellen Sie sicher, dass die oben genannten Punkte bereitstehen; die späteren Schritte gehen davon aus, dass sie vorhanden sind.

## Schritt 1: OCR‑Engine‑Instanz erstellen – Kern von „Text aus Bild erkennen“

Das Erste, was wir benötigen, ist ein Objekt, das mit der OCR‑Engine kommunizieren kann. Denken Sie daran als das Gehirn, das später **Text aus Bild** verarbeitet.

```python
import ocr  # Import the OCR library

# Initialize the engine
ocr_engine = ocr.OcrEngine()
```

> **Warum das wichtig ist:** Durch das einmalige Initialisieren der Engine können Sie Einstellungen (wie Sprachpakete) über mehrere Bilder hinweg wiederverwenden, was die Leistung verbessert und den Code übersichtlich hält.

## Schritt 2: Bild für OCR laden – Bild in den Speicher holen

Jetzt **laden wir das Bild für OCR**. Die Bibliothek stellt eine praktische statische Methode bereit, die die Datei einliest und ein Objekt zurückgibt, das die Engine versteht.

```python
# Load the source image (replace the path with your own)
image_path = "YOUR_DIRECTORY/form.png"
ocr_engine.set_image(ocr.Imaging.Image.load(image_path))
```

> **Pro‑Tipp:** Wenn Ihr Bild groß ist, sollten Sie es vor dem Laden verkleinern. Kleinere Bilder beschleunigen die OCR, ohne die Genauigkeit bei den meisten gedruckten Texten zu beeinträchtigen.

## Schritt 3: OCR‑Region of Interest (ROI) definieren

Oft benötigen Sie nicht die gesamte Seite – nur ein bestimmtes Feld, in das der Benutzer Daten eingetragen hat. Das Definieren einer **OCR‑Region of Interest** weist die Engine an, alles andere zu ignorieren, was Rauschen reduziert und die Verarbeitung beschleunigt.

```python
# Define ROI: (left, top, width, height) in pixels
region_of_interest = ocr.Rectangle(120, 340, 560, 90)

# Register the ROI with the engine
ocr_engine.add_region_of_interest(region_of_interest)
```

> **Warum ROI fokussieren?**  
> - **Geschwindigkeit:** Die Engine scannt weniger Pixel.  
> - **Genauigkeit:** Hintergrundgrafiken außerhalb der ROI können die Zeichenerkennung verwirren.  
> - **Einfachheit:** Sie erhalten einen sauberen String, der exakt dem gewünschten Feld entspricht.

## Schritt 4: OCR‑Prozess ausführen – Der entscheidende Moment

Nachdem alles eingerichtet ist, **erkennen wir Text aus dem Bild** innerhalb der definierten ROI.

```python
# Execute OCR on the specified region
ocr_result = ocr_engine.recognize()
```

Falls die Engine mehrere Regionen unterstützt, enthält `ocr_result` eine Liste; in unserem Ein‑ROI‑Fall ist es ein einfaches Objekt mit einer `get_text()`‑Methode.

## Schritt 5: Text extrahieren und ausgeben – Das Endergebnis erhalten

Jetzt holen wir den reinen String aus dem Ergebnisobjekt und geben ihn aus. Hier können Sie die Ausgabe in eine Datenbank, eine CSV‑Datei oder jede nachgelagerte Logik einbinden.

```python
# Retrieve the recognized text
extracted_text = ocr_result.get_text()

# Show the result
print("Text inside ROI:\n", extracted_text)
```

**Erwartete Ausgabe** (Beispiel für ein ausgefülltes Namensfeld):

```
Text inside ROI:
 John Doe
```

Falls die OCR‑Engine zusätzliche Leerzeichen oder Zeilenumbrüche zurückgibt, können Sie diese mit `.strip()` oder einem regulären Ausdruck bereinigen.

## Häufige Sonderfälle behandeln

| Situation                              | Was zu tun ist                                                               |
|----------------------------------------|------------------------------------------------------------------------------|
| **Low‑resolution image**               | Vor dem Laden mit `Pillow` (`Image.resize`) hochskalieren.                  |
| **Skewed or rotated text**             | Rotationskorrektur anwenden (`ocr.Imaging.Image.rotate`).                  |
| **Multiple languages**                | Sprachpaket auf der Engine setzen: `ocr_engine.set_language('eng+spa')`.   |
| **No ROI defined**                     | `add_region_of_interest` überspringen; die Engine verarbeitet das gesamte Bild. |
| **Unexpected characters (e.g., commas)** | Zeichenkette nachbearbeiten: `extracted_text.replace(',', '')`.            |

Diese Tipps halten Ihre **load image for OCR**‑Pipeline robust, selbst wenn das Ausgangsmaterial nicht perfekt ist.

## Vollständiges Beispiel – Kopieren, Einfügen, Ausführen

Unten finden Sie das komplette Skript, das Sie in eine `.py`‑Datei einfügen und ausführen können. Es enthält alle Importe, Fehlerbehandlung und einen kleinen Helfer, der prüft, ob das Bild existiert.

```python
import os
import ocr

def recognize_text_from_image(image_path: str,
                              roi: tuple = (120, 340, 560, 90)):
    """
    Recognize text from a specific region of an image.

    Parameters
    ----------
    image_path : str
        Full path to the image file.
    roi : tuple
        (left, top, width, height) defining the region of interest.

    Returns
    -------
    str
        The extracted text, stripped of surrounding whitespace.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Step 1 – create engine
    engine = ocr.OcrEngine()

    # Step 2 – load image for OCR
    engine.set_image(ocr.Imaging.Image.load(image_path))

    # Step 3 – define ROI
    left, top, width, height = roi
    engine.add_region_of_interest(ocr.Rectangle(left, top, width, height))

    # Step 4 – run OCR
    result = engine.recognize()

    # Step 5 – extract text
    text = result.get_text().strip()
    return text


if __name__ == "__main__":
    # Adjust the path to point at your form image
    img_path = "YOUR_DIRECTORY/form.png"

    try:
        roi_text = recognize_text_from_image(img_path)
        print("Text inside ROI:\n", roi_text)
    except Exception as e:
        print("OCR failed:", e)
```

Wenn Sie dieses Skript ausführen, wird die bereinigte Zeichenkette aus der ROI ausgegeben, sodass Sie sofort nutzbare Daten erhalten.

## Fazit

Sie haben nun eine klare, durchgängige Methode, **Text aus Bild** zu erkennen, indem Sie zuerst **load image for OCR**, eine präzise **OCR region of interest** definieren und schließlich den sauberen Text extrahieren. Der Ansatz funktioniert mit jeder Python‑OCR‑Bibliothek, die dem gezeigten Muster folgt, und lässt sich leicht erweitern, um mehrere ROIs, verschiedene Sprachen oder Vorverarbeitungsschritte zu unterstützen.

Als Nächstes könnten Sie erkunden:

- **image preprocessing for OCR** (Schwellwertsetzung, Rauschunterdrückung), um die Genauigkeit bei verrauschten Scans zu steigern.  
- Das Ergebnis **extract text from ROI** nutzen, um ein pandas DataFrame für die Massenanalyse zu füllen.  
- Auf einen cloud‑basierten OCR‑Dienst (Google Vision, Azure Computer Vision) umsteigen, wenn Sie höhere Zuverlässigkeit im großen Maßstab benötigen.

Probieren Sie es aus, passen Sie die Rechteckkoordinaten an Ihre eigenen Formulare an und lassen Sie die Automatisierung für Sie arbeiten. Viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}