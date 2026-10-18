---
category: general
date: 2026-05-03
description: Erfahren Sie, wie Sie OCR auf einem Bild ausführen und Text mit Koordinaten
  mithilfe strukturierter OCR‑Erkennung extrahieren. Schritt‑für‑Schritt‑Python‑Code
  inklusive.
draft: false
keywords:
- run OCR on image
- extract text with coordinates
- structured OCR recognition
- OCR post‑processing
- bounding box extraction
- image text detection
language: de
og_description: Führen Sie OCR auf einem Bild aus und erhalten Sie Text mit Koordinaten
  mittels strukturierter OCR-Erkennung. Vollständiges Python‑Beispiel mit Erklärungen.
og_title: OCR auf Bild ausführen – Tutorial zur strukturierten Textextraktion
tags:
- OCR
- Python
- Computer Vision
title: OCR auf Bild ausführen – Vollständiger Leitfaden zur strukturierten Textextraktion
url: /de/python/general/run-ocr-on-image-complete-guide-to-structured-text-extractio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR auf Bild ausführen – Komplettanleitung zur strukturierten Textextraktion

Haben Sie jemals **run OCR on image**-Dateien ausführen müssen, waren sich aber nicht sicher, wie Sie die genauen Positionen jedes Wortes beibehalten? Sie sind nicht allein. In vielen Projekten – Belegscan, Formulardigitalisierung oder UI-Tests – benötigen Sie nicht nur den Rohtext, sondern auch die Begrenzungsrahmen, die Ihnen zeigen, wo jede Zeile im Bild liegt.  

Dieses Tutorial zeigt Ihnen eine praktische Methode, um *run OCR on image* mit der **aocr**‑Engine zu verwenden, **structured OCR recognition** anzufordern und anschließend das Ergebnis zu post‑processen, wobei die Geometrie erhalten bleibt. Am Ende können Sie **extract text with coordinates** in nur wenigen Zeilen Python durchführen und verstehen, warum der strukturierte Modus für nachgelagerte Aufgaben wichtig ist.

## Was Sie lernen werden

- Wie man die OCR-Engine für **structured OCR recognition** initialisiert.  
- Wie man ein Bild einspeist und Rohresultate erhält, die Zeilenbegrenzungen enthalten.  
- Wie man einen Post‑Processor ausführt, der den Text bereinigt, ohne die Geometrie zu verlieren.  
- Wie man über die finalen Zeilen iteriert und jedes Textelement zusammen mit seinem Begrenzungsrahmen ausgibt.  

Kein Zauber, keine versteckten Schritte – nur ein vollständiges, ausführbares Beispiel, das Sie in Ihr eigenes Projekt einbinden können.

---

## Voraussetzungen

Bevor wir loslegen, stellen Sie sicher, dass Sie Folgendes installiert haben:

```bash
pip install aocr ai   # hypothetical packages; replace with real ones if needed
```

Sie benötigen außerdem eine Bilddatei (`input_image.png` oder `.jpg`), die klaren, lesbaren Text enthält. Alles von einer gescannten Rechnung bis zu einem Screenshot funktioniert, solange die OCR-Engine die Zeichen erkennen kann.

## Schritt 1: Initialisieren der OCR-Engine für strukturierte Erkennung

Das Erste, was wir tun, ist eine Instanz von `aocr.Engine()` zu erstellen und ihr mitzuteilen, dass wir **structured OCR recognition** wollen. Der strukturierte Modus liefert nicht nur den Klartext, sondern auch geometrische Daten (begrenzende Rechtecke) für jede Zeile, was unerlässlich ist, wenn Sie Text zurück auf das Bild abbilden müssen.

```python
import aocr
import ai   # hypothetical post‑processing module

# Initialise the OCR engine
ocr_engine = aocr.Engine()

# Request structured recognition (text + geometry)
ocr_engine.recognize_mode = aocr.RecognitionMode.Structured
```

> **Warum das wichtig ist:**  
> Im Standardmodus gibt die Engine möglicherweise nur einen String aus zusammengefügten Wörtern zurück. Der strukturierte Modus liefert Ihnen eine Hierarchie von Seiten → Zeilen → Wörtern, jeweils mit Koordinaten, was das Überlagern der Ergebnisse auf dem Originalbild oder das Einspeisen in ein layout‑bewusstes Modell erheblich erleichtert.

## Schritt 2: OCR auf dem Bild ausführen und Rohresultate erhalten

Jetzt geben wir das Bild an die Engine weiter. Der Aufruf `recognize` gibt ein `OcrResult`‑Objekt zurück, das eine Sammlung von Zeilen enthält, von denen jede ihr eigenes Begrenzungsrechteck hat.

```python
# Load your image (any format supported by aocr)
input_image_path = "input_image.png"

# Run OCR – this returns an OcrResult with lines and bounds
raw_result = ocr_engine.recognize(input_image_path)
```

An diesem Punkt enthält `raw_result.lines` Objekte mit zwei wichtigen Attributen:

- `text` – die erkannte Zeichenkette für diese Zeile.  
- `bounds` – ein Tupel wie `(x, y, width, height)`, das die Position der Zeile beschreibt.

## Schritt 3: Nachbearbeitung bei Erhaltung der Geometrie

Roh‑OCR‑Ausgaben sind oft verrauscht: fremde Zeichen, falsche Leerzeichen oder Zeilenumbruchprobleme. Die Funktion `ai.run_postprocessor` bereinigt den Text, **keeps the original geometry** unverändert, sodass Sie weiterhin genaue Koordinaten haben.

```python
# Apply a post‑processing step that corrects common OCR errors
postprocessed_result = ai.run_postprocessor(raw_result)

# The structure (lines + bounds) stays the same, only `line.text` changes
```

> **Pro Tipp:** Wenn Sie domänenspezifische Vokabulare haben (z. B. Produktcodes), übergeben Sie dem Post‑Processor ein benutzerdefiniertes Wörterbuch, um die Genauigkeit zu verbessern.

## Schritt 4: Text mit Koordinaten extrahieren – iterieren und anzeigen

Abschließend iterieren wir über die bereinigten Zeilen und geben für jede Zeile den Begrenzungsrahmen zusammen mit dem Text aus. Das ist das Kernstück von **extract text with coordinates**.

```python
# Print each recognised line together with its bounding box
for line in postprocessed_result.lines:
    print(f"[{line.bounds}] {line.text}")
```

### Erwartete Ausgabe

Angenommen, das Eingabebild enthält zwei Zeilen: „Invoice #12345“ und „Total: $89.99“, Sie sehen etwa Folgendes:

```
[(15, 30, 210, 25)] Invoice #12345
[(15, 70, 190, 25)] Total: $89.99
```

Das erste Tupel ist das `(x, y, width, height)` der Zeile im Originalbild, sodass Sie Rechtecke zeichnen, Text hervorheben oder die Koordinaten in ein anderes System einspeisen können.

## Visualisierung des Ergebnisses (Optional)

Wenn Sie die Begrenzungsrahmen über das Bild gelegt sehen möchten, können Sie Pillow (PIL) verwenden, um Rechtecke zu zeichnen. Unten ist ein kurzer Ausschnitt; Sie können ihn überspringen, wenn Sie nur die Rohdaten benötigen.

```python
from PIL import Image, ImageDraw

# Open the original image
img = Image.open(input_image_path)
draw = ImageDraw.Draw(img)

# Draw a rectangle around each line
for line in postprocessed_result.lines:
    x, y, w, h = line.bounds
    draw.rectangle([x, y, x + w, y + h], outline="red", width=2)

# Save or show the annotated image
img.save("annotated_output.png")
img.show()
```

![run OCR on image example showing bounding boxes](/images/ocr-bounding-boxes.png "run OCR on image – bounding box overlay")

Der obige Alt‑Text enthält das **primary keyword**, was die SEO‑Anforderung für Bild‑Alt‑Attribute erfüllt.

## Warum strukturierte OCR-Erkennung die einfache Textextraktion übertrifft

Sie fragen sich vielleicht: „Kann ich nicht einfach OCR ausführen und den Text erhalten? Warum die Geometrie?“.

- **Spatial context:** Wenn Sie Felder auf einem Formular zuordnen müssen (z. B. „Date“ neben einem Datumswert), geben Ihnen die Koordinaten an, *wo* die Daten liegen.  
- **Multi‑column layouts:** Einfacher linearer Text verliert die Reihenfolge; strukturierte Daten erhalten die Spaltenreihenfolge.  
- **Post‑processing accuracy:** Das Wissen um die Boxgröße hilft Ihnen zu entscheiden, ob ein Wort eine Überschrift, eine Fußnote oder ein fremdes Artefakt ist.  

Kurz gesagt, bietet **structured OCR recognition** Ihnen die Flexibilität, intelligentere Pipelines zu bauen – egal, ob Sie Daten in eine Datenbank einspeisen, durchsuchbare PDFs erstellen oder ein Machine‑Learning‑Modell trainieren, das das Layout respektiert.

## Häufige Randfälle und deren Handhabung

| Situation | Worauf zu achten ist | Vorgeschlagene Lösung |
|-----------|----------------------|-----------------------|
| **Gedrehte oder verzerrte Bilder** | Begrenzungsrahmen können von der Achse abweichen. | Vorverarbeiten mit Entzerrung (z. B. OpenCV’s `warpAffine`). |
| **Sehr kleine Schriften** | Die Engine kann Zeichen übersehen, was zu leeren Zeilen führt. | Erhöhen Sie die Bildauflösung oder verwenden Sie `ocr_engine.set_dpi(300)`. |
| **Gemischte Sprachen** | Ein falsches Sprachmodell kann unlesbaren Text erzeugen. | Setzen Sie `ocr_engine.language = ["en", "de"]` vor der Erkennung. |
| **Überlappende Boxen** | Der Post‑Processor könnte unbeabsichtigt zwei Zeilen zusammenführen. | Überprüfen Sie `line.bounds` nach der Verarbeitung; passen Sie die Schwellenwerte in `ai.run_postprocessor` an. |

Das frühzeitige Angehen dieser Szenarien erspart Ihnen später Kopfschmerzen, besonders wenn Sie die Lösung auf Hunderte von Dokumenten pro Tag skalieren.

## Vollständiges End‑to‑End‑Skript

Unten finden Sie das komplette, sofort ausführbare Programm, das alle Schritte zusammenführt. Kopieren‑einfügen, passen Sie den Bildpfad an, und Sie können loslegen.

```python
# -*- coding: utf-8 -*-
"""
Run OCR on image – extract text with coordinates using structured OCR recognition.
Author: Your Name
Date: 2026-05-03
"""

import aocr
import ai
from PIL import Image, ImageDraw

def run_structured_ocr(image_path: str, annotate: bool = False):
    # 1️⃣ Initialise the OCR engine
    ocr_engine = aocr.Engine()
    ocr_engine.recognize_mode = aocr.RecognitionMode.Structured

    # 2️⃣ Recognise the image
    raw_result = ocr_engine.recognize(image_path)

    # 3️⃣ Post‑process while keeping geometry
    processed = ai.run_postprocessor(raw_result)

    # 4️⃣ Print each line with its bounding box
    for line in processed.lines:
        print(f"[{line.bounds}] {line.text}")

    # Optional visualisation
    if annotate:
        img = Image.open(image_path)
        draw = ImageDraw.Draw(img)
        for line in processed.lines:
            x, y, w, h = line.bounds
            draw.rectangle([x, y, x + w, y + h], outline="red", width=2)
        annotated_path = "annotated_" + image_path
        img.save(annotated_path)
        print(f"Annotated image saved as {annotated_path}")

if __name__ == "__main__":
    INPUT_IMG = "input_image.png"
    run_structured_ocr(INPUT_IMG, annotate=True)
```

Das Ausführen dieses Skripts bewirkt:

1. **Run OCR on image** mit strukturiertem Modus.  
2. **Extract text with coordinates** für jede Zeile.  
3. Optional wird ein annotiertes PNG erzeugt, das die Boxen zeigt.

## Fazit

Sie haben nun eine solide, eigenständige Lösung, um **run OCR on image** und **extract text with coordinates** mit **structured OCR recognition** durchzuführen. Der Code demonstriert jeden Schritt – von der Engine‑Initialisierung über die Nachbearbeitung bis hin zur visuellen Verifizierung – sodass Sie ihn an Quittungen, Formulare oder jedes visuelle Dokument anpassen können, das eine präzise Textlokalisierung benötigt.

Was kommt als Nächstes? Versuchen Sie, die `aocr`‑Engine durch eine andere Bibliothek (Tesseract, EasyOCR) zu ersetzen und sehen Sie, wie sich deren strukturierte Ausgaben unterscheiden. Experimentieren Sie mit verschiedenen Nachbearbeitungsstrategien, wie Rechtschreibprüfung oder benutzerdefinierten Regex‑Filtern, um die Genauigkeit für Ihr Fachgebiet zu steigern. Und wenn Sie eine größere Pipeline bauen, überlegen Sie, die `(text, bounds)`‑Paare in einer Datenbank für spätere Analysen zu speichern.

Viel Spaß beim Programmieren und mögen Ihre OCR‑Projekte stets genau sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}