---
category: general
date: 2026-06-16
description: Definieren Sie den Interessensbereich (ROI) in der OCR, um spanischen
  Text von Ausweisen zu extrahieren. Erfahren Sie, wie Sie das Bild für die OCR laden
  und den ROI effizient festlegen.
draft: false
keywords:
- define region of interest
- load image for ocr
- how to specify roi
- extract id card text
- extract spanish text image
language: de
og_description: Definieren Sie den Bereich von Interesse (ROI) in der OCR, um spanischen
  Text von Ausweisen zu extrahieren. Schritt‑für‑Schritt‑Anleitung zum Laden von Bildern
  und Festlegen des ROI.
og_title: Region von Interesse in OCR definieren – Komplettes Python‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Define region of interest in OCR to extract Spanish text from ID cards.
    Learn how to load image for OCR and specify ROI efficiently.
  headline: Define region of interest in OCR – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Region von Interesse im OCR definieren – Vollständiges Python‑Tutorial
url: /de/python-java/general/define-region-of-interest-in-ocr-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definieren des Interessengebiets in OCR – Vollständiges Python‑Tutorial

Haben Sie sich jemals gefragt, wie man **define region of interest in OCR** definiert, damit Sie nur den Teil eines Bildes lesen, den Sie tatsächlich benötigen? In diesem Tutorial führen wir Sie genau durch diesen Prozess und zeigen Ihnen, wie Sie **load image for OCR** ausführen und spanischen Text von einem Ausweis in nur wenigen Zeilen Python extrahieren.

Wenn Sie schon einmal auf einen verrauschten Scan gestarrt haben und dachten: „Es muss einen saubereren Weg geben, das Namensfeld zu erfassen“, dann sind Sie hier genau richtig. Am Ende können Sie den Text des Ausweises, der Sie interessiert, extrahieren, ohne von Hintergrundgeräuschen abgelenkt zu werden.

## Was Sie lernen werden

- Warum Sie **define region of interest** vor dem Ausführen von OCR definieren sollten.  
- Die genauen Schritte, um **load image for OCR** mit einem beliebten Python‑OCR‑Wrapper zu verwenden.  
- Wie man **how to specify ROI** mit Pixelkoordinaten angibt.  
- Möglichkeiten, **extract id card text** zuverlässig zu extrahieren, selbst wenn die Ausgangssprache Spanisch ist.  
- Tipps zum Umgang mit Randfällen wie gedrehten Karten oder Scans mit geringem Kontrast.  

Keine vorherige OCR‑Meisterschaft ist erforderlich – nur eine funktionierende Python 3‑Umgebung und ein JPEG eines Ausweises, den Sie testen möchten.

![Define region of interest illustration](placeholder.png){alt="Beispiel für das Definieren des Interessengebiets, das ein hervorgehobenes Rechteck auf einem Ausweisbild zeigt"}

## Schritt 1: Installieren und Importieren der OCR‑Bibliothek

Zuerst benötigen Sie eine Bibliothek, die eine `OcrEngine`‑Klasse bereitstellt, ähnlich dem Snippet, das Sie gesehen haben. Für diese Anleitung verwenden wir das fiktive `ocr`‑Paket, aber dieselben Konzepte gelten für `pytesseract`, `easyocr` oder jeden Wrapper, der Ihnen erlaubt, eine Sprache und eine ROI festzulegen.

```bash
pip install ocr   # Replace with the actual package name you use
```

```python
# Import the library and any helper classes
import ocr
from ocr import Rectangle, Image
```

*Pro‑Tipp:* Wenn Sie `pytesseract` verwenden, wird die `Rectangle`‑Klasse zu einem einfachen Tupel `(left, top, width, height)`. Der Rest des Ablaufs bleibt identisch.

## Schritt 2: Bild für OCR laden

Jetzt **load image for OCR**. Die Engine erwartet ein `ocr.Image`‑Objekt, also verweisen wir auf die Datei, die den Ausweis enthält. Stellen Sie sicher, dass der Pfad absolut oder relativ zum Arbeitsverzeichnis Ihres Skripts ist.

```python
# Create the OCR engine instance
engine = ocr.OcrEngine()

# Tell the engine which language we’re interested in – Spanish in this case
engine.language = ocr.Language.SPANISH

# Load the source image that contains the text to be recognized
engine.image = Image.load_from_file("YOUR_DIRECTORY/id-card.jpg")
```

Wenn das Bild sehr groß ist, sollten Sie es zuerst verkleinern; OCR‑Engines arbeiten schneller mit Bildern, die weniger als 1500 px in der Breite haben.

## Schritt 3: Wie man ROI angibt (Define Region of Interest)

Hier ist das Herzstück des Tutorials: **how to specify ROI**. Ein Interessengebiet ist einfach ein Rechteck, das der OCR‑Engine sagt: „Nur innerhalb dieser Pixelgrenzen schauen.“ Stellen Sie sich das vor, als würden Sie ein Kästchen um das Namensfeld auf einem Ausweis zeichnen.

```python
# Define the region of interest – left, top, width, height (all in pixels)
engine.region_of_interest = Rectangle(
    left=120,   # X‑coordinate of the left edge
    top=80,     # Y‑coordinate of the top edge
    width=340,  # Width of the box
    height=200  # Height of the box
)
```

Warum diese Zahlen? In unserem Beispielbild befindet sich der Name etwa 120 px vom linken Rand und 80 px vom oberen Rand. Passen Sie sie an das Layout der Karten an, die Sie verarbeiten.  

*Randfall:* Wenn die Karte um 90° gedreht ist, tauschen Sie `width` und `height` aus und passen `left`/`top` entsprechend an, oder drehen Sie das Bild vorab mit Pillow, bevor Sie es an die Engine übergeben.

## Schritt 4: OCR innerhalb der ROI ausführen

Mit definierter ROI ignoriert die Engine alles außerhalb des Rechtecks. Das beschleunigt nicht nur die Verarbeitung, sondern reduziert auch Fehlalarme, die durch Hintergrundgrafiken verursacht werden.

```python
# Run OCR only inside the defined ROI
roi_result = engine.recognize()
```

Der Aufruf `recognize()` gibt ein Objekt zurück, das den erkannten Text, Vertrauenswerte und Begrenzungsrahmen für jedes Wort enthält.

## Schritt 5: ID‑Kartentext extrahieren (und spanische Ausgabe überprüfen)

Schließlich **extract id card text** aus dem ROI‑Ergebnis und geben es aus. Da wir die Sprache zuvor auf Spanisch gesetzt haben, verwendet die OCR‑Engine sprachspezifische Wörterbücher, was die Genauigkeit für Zeichen wie „ñ“ oder „á“ verbessert.

```python
# Output the recognized text from the ROI
print("ROI text:", roi_result.text)
```

### Erwartete Ausgabe

```
ROI text: JUAN PÉREZ GARCÍA
```

Wenn Sie unleserliche Zeichen sehen, prüfen Sie, ob das Bild wirklich Spanisch ist und ob die Sprachdatendateien der OCR‑Bibliothek installiert sind.

## Häufige Fallstricke & wie man sie vermeidet

| Symptom | Wahrscheinliche Ursache | Lösung |
|---------|--------------------------|--------|
| Leere Zeichenkette zurückgegeben | ROI schneidet keinen Text | Koordinaten mit einem Bildbetrachter überprüfen; `engine.debug_draw_roi()` verwenden, falls verfügbar. |
| Viele fehlerhafte Zeichen | Falsches Sprachpaket | Spanische Sprachdaten neu installieren oder zu `ocr.Language.AUTO` wechseln. |
| Niedrige Vertrauenswerte | Bild ist unscharf oder hat geringen Kontrast | Mit OpenCV vorverarbeiten – `cv2.GaussianBlur` und `cv2.threshold` anwenden. |
| OCR läuft auf dem gesamten Bild trotz ROI | Verwendung einer älteren Bibliotheksversion | Auf das neueste `ocr`‑Paket aktualisieren; ältere Versionen ignorierten ROI. |

## Erweiterung des Beispiels: Mehrere ROIs

Manchmal müssen Sie mehr als ein Feld extrahieren (z. B. Name und Ausweisnummer). Das Muster bleibt gleich: Ändern Sie `engine.region_of_interest` und rufen Sie `recognize()` erneut auf.

```python
# ROI for the ID number (different coordinates)
engine.region_of_interest = Rectangle(120, 300, 340, 80)
id_result = engine.recognize()
print("ID Number:", id_result.text)
```

Sie können auch eine Liste von Rechtecken stapelweise verarbeiten, falls die Bibliothek dies unterstützt, was einen zusätzlichen Durchlauf zur OCR‑Engine spart.

## Vollständiges funktionierendes Skript

Wenn wir alles zusammenfügen, erhalten Sie ein sofort ausführbares Skript, das **defines region of interest**, **loads image for OCR** und **extracts Spanish text** von einem Ausweis.

```python
import ocr
from ocr import Rectangle, Image

def extract_name_from_id(image_path):
    """
    Loads an image, defines a ROI around the name field,
    runs OCR in Spanish, and returns the recognized text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.SPANISH
    engine.image = Image.load_from_file(image_path)

    # Adjust these numbers to match your card layout
    engine.region_of_interest = Rectangle(left=120, top=80, width=340, height=200)

    result = engine.recognize()
    return result.text.strip()

if __name__ == "__main__":
    name = extract_name_from_id("YOUR_DIRECTORY/id-card.jpg")
    print("Extracted Name:", name)
```

Führen Sie das Skript aus und Sie sollten den Namen in der Konsole sehen. Ändern Sie die Rechteckwerte, um andere Felder anzusteuern, und Sie haben ein wiederverwendbares Werkzeug für jedes Dokument vom Typ Ausweis.

## Nächste Schritte

- **Batch‑Verarbeitung:** Durchlaufen Sie einen Ordner mit Ausweisen und speichern Sie jeden extrahierten Namen in einer CSV‑Datei.  
- **Spracherkennung:** Lassen Sie den Benutzer die Sprache dynamisch auswählen; `ocr.Language.AUTO` kann nützlich sein.  
- **Nachbearbeitung:** Regex‑Muster anwenden, um häufige OCR‑Fehler zu bereinigen (z. B. “0” durch “O” ersetzen, wenn es in Namen vorkommt).  

Durch das Beherrschen, wie man **define region of interest** einsetzt, haben Sie eine leistungsstarke Methode entdeckt, **extract id card text** schnell und exakt zu extrahieren, besonders bei spanischsprachigen Dokumenten.

---

### TL;DR

Wir haben Ihnen gezeigt, wie man **define region of interest in OCR**, **load image for OCR** und **how to specify ROI** verwendet, um **extract spanish text image** von einem Ausweis zu extrahieren. Das vollständige Beispiel läuft in weniger als einer Minute und lässt sich mit wenigen Koordinatenanpassungen an jedes Layout anpassen. Probieren Sie es aus, justieren Sie das Rechteck und sehen Sie, wie die OCR wie ein Laser fokussiert.

Viel Spaß beim Programmieren!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man Text aus einem Bild extrahiert, indem man Rechtecke in OCR vorbereitet](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Bildtext in C# mit Sprachauswahl mittels Aspose.OCR extrahieren](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Text aus Bild extrahieren – OCR‑Optimierung mit Aspose.OCR für .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}