---
category: general
date: 2026-03-28
description: Führen Sie OCR auf einem Bild durch und erhalten Sie bereinigten Text
  mit Koordinaten der Begrenzungsrahmen. Lernen Sie, wie man OCR extrahiert, OCR bereinigt
  und die Ergebnisse Schritt für Schritt anzeigt.
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: de
og_description: Führen Sie OCR auf einem Bild aus, bereinigen Sie die Ausgabe und
  zeigen Sie die Koordinaten der Begrenzungsrahmen in einer kurzen Anleitung.
og_title: OCR auf Bild ausführen – Saubere Ergebnisse und Begrenzungsrahmen
tags:
- OCR
- Computer Vision
- Python
title: OCR auf Bild ausführen – Ergebnisse bereinigen und Bounding‑Box‑Koordinaten
  anzeigen
url: /de/python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR auf Bild ausführen – Ergebnisse bereinigen und Begrenzungsbox‑Koordinaten anzeigen

Haben Sie jemals **OCR auf Bild**‑Dateien ausführen müssen, aber immer wieder unordentlichen Text erhalten und nicht sicher sein können, wo jedes Wort im Bild liegt? Sie sind nicht allein. In vielen Projekten – Rechnungsdigitalisierung, Belegscan oder einfache Textextraktion – ist die Roh‑OCR‑Ausgabe nur das erste Hindernis. Die gute Nachricht? Sie können diese Ausgabe bereinigen und sofort die Begrenzungsbox‑Koordinaten jeder Region sehen, ohne eine Menge Boiler‑Plate‑Code zu schreiben.

In diesem Leitfaden gehen wir Schritt für Schritt durch **how to extract OCR**, führen einen **how to clean OCR**‑Post‑Processor aus und zeigen schließlich **display bounding box coordinates** für jede bereinigte Region. Am Ende haben Sie ein einzelnes, ausführbares Skript, das ein unscharfes Foto in sauberen, strukturierten Text verwandelt, bereit für die nachgelagerte Verarbeitung.

## Was Sie benötigen

- Python 3.9+ (die unten gezeigte Syntax funktioniert ab 3.8)
- Eine OCR‑Engine, die `recognize(..., return_structured=True)` unterstützt – zum Beispiel die fiktive `engine`‑Bibliothek im Beispiel. Ersetzen Sie sie durch Tesseract, EasyOCR oder ein beliebiges SDK, das Regionsdaten zurückgibt.
- Grundlegende Kenntnisse von Python‑Funktionen und Schleifen
- Eine Bilddatei, die Sie scannen möchten (PNG, JPG usw.)

> **Profi‑Tipp:** Wenn Sie Tesseract verwenden, liefert die Funktion `pytesseract.image_to_data` bereits Begrenzungsboxen. Sie können das Ergebnis in einen kleinen Adapter einbinden, der die unten gezeigte `engine.recognize`‑API nachahmt.

---

![perform OCR on image example](image-placeholder.png "perform OCR on image example")

*Alt text: Diagramm, das zeigt, wie OCR auf Bild ausgeführt wird und Begrenzungsbox‑Koordinaten visualisiert werden*

## Schritt 1 – OCR auf Bild ausführen und strukturierte Regionen erhalten

Der erste Schritt besteht darin, die OCR‑Engine zu bitten, nicht nur reinen Text, sondern eine strukturierte Liste von Textregionen zurückzugeben. Diese Liste enthält die Rohzeichenkette und das Rechteck, das sie umschließt.

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**Warum das wichtig ist:**  
Wenn Sie nur nach reinem Text fragen, verlieren Sie den räumlichen Kontext. Strukturierte Daten ermöglichen es Ihnen später, **display bounding box coordinates** anzuzeigen, Text mit Tabellen auszurichten oder präzise Positionen an ein nachgelagertes Modell zu übergeben.

## Schritt 2 – OCR‑Ausgabe mit einem Post‑Processor bereinigen

OCR‑Engines erkennen Zeichen gut, lassen jedoch oft überflüssige Leerzeichen, Zeilenumbruch‑Artefakte oder falsch erkannte Symbole zurück. Ein Post‑Processor normalisiert den Text, behebt häufige OCR‑Fehler und entfernt überflüssige Leerzeichen.

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

Wenn Sie Ihren eigenen Cleaner bauen, sollten Sie berücksichtigen:

- Entfernen von Nicht‑ASCII‑Zeichen (`re.sub(r'[^\x00-\x7F]+',' ', text)`)
- Zusammenführen mehrerer Leerzeichen zu einem einzigen
- Anwenden eines Rechtschreibprüfers wie `pyspellchecker` für offensichtliche Tippfehler

**Warum das wichtig ist:**  
Ein bereinigter String macht Suche, Indexierung und nachgelagerte NLP‑Pipelines deutlich zuverlässiger. Mit anderen Worten, **how to clean OCR** ist oft der Unterschied zwischen einem nutzbaren Datensatz und einem Kopfschmerz.

## Schritt 3 – Begrenzungsbox‑Koordinaten für jede bereinigte Region anzeigen

Jetzt, wo der Text bereinigt ist, iterieren wir über jede Region, geben ihr Rechteck und den bereinigten String aus. Das ist der Teil, in dem wir schließlich **display bounding box coordinates** anzeigen.

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**Beispielausgabe**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

Sie können diese Koordinaten nun in eine Zeichenbibliothek (z. B. OpenCV) einspeisen, um Boxen über das Originalbild zu legen, oder sie in einer Datenbank für spätere Abfragen speichern.

## Vollständiges, sofort ausführbares Skript

Unten finden Sie das vollständige Programm, das alle drei Schritte verbindet. Ersetzen Sie die Platzhalter‑`engine`‑Aufrufe durch Ihr tatsächliches OCR‑SDK.

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### So führen Sie das Skript aus

```bash
python perform_ocr.py sample_invoice.jpg
```

Sie sollten eine Liste von Begrenzungsboxen zusammen mit bereinigtem Text sehen, genau wie in der obigen Beispielausgabe.

## Häufig gestellte Fragen & Sonderfälle

| Frage | Antwort |
|----------|--------|
| **Was ist, wenn die OCR‑Engine `return_structured` nicht unterstützt?** | Schreiben Sie einen dünnen Wrapper, der die Rohausgabe der Engine (in der Regel eine Liste von Wörtern mit Koordinaten) in Objekte mit den Attributen `text` und `bounding_box` konvertiert. |
| **Kann ich Konfidenzwerte erhalten?** | Viele SDKs stellen eine Konfidenzmetrik pro Region bereit. Hängen Sie sie an die Print‑Anweisung an: `print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")`. |
| **Wie gehe ich mit gedrehtem Text um?** | Vorverarbeiten Sie das Bild mit OpenCVs `cv2.minAreaRect`, um es vor dem Aufruf von `recognize` zu entzerren. |
| **Was ist, wenn ich die Ausgabe im JSON‑Format benötige?** | Serialisieren Sie `processed_result.regions` mit `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)`. |
| **Gibt es eine Möglichkeit, die Boxen zu visualisieren?** | Verwenden Sie OpenCV: `cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)` innerhalb der Schleife und dann `cv2.imwrite("annotated.jpg", img)`. |

## Fazit

Sie haben gerade **how to perform OCR on image** gelernt, die Rohausgabe bereinigt und **display bounding box coordinates** für jede Region angezeigt. Der dreistufige Ablauf – erkennen → nachbearbeiten → iterieren – ist ein wiederverwendbares Muster, das Sie in jedes Python‑Projekt einbinden können, das zuverlässige Textextraktion benötigt.

### Was kommt als Nächstes?

- **Untersuchen Sie verschiedene OCR‑Back‑ends** (Tesseract, EasyOCR, Google Vision) und vergleichen Sie die Genauigkeit.
- **Integrieren Sie eine Datenbank**, um Regionsdaten für durchsuchbare Archive zu speichern.
- **Fügen Sie Spracherkennung hinzu**, um jede Region durch den passenden Rechtschreibprüfer zu leiten.
- **Boxen über das Originalbild legen** zur visuellen Überprüfung (siehe das OpenCV‑Snippet oben).

Wenn Sie auf Eigenheiten stoßen, denken Sie daran, dass der größte Gewinn aus einem soliden Nachbearbeitungsschritt resultiert; ein bereinigter String ist viel einfacher zu verarbeiten als ein Rohdump von Zeichen.

Viel Spaß beim Coden, und mögen Ihre OCR‑Pipelines stets ordentlich sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}