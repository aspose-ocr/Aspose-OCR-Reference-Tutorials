---
category: general
date: 2026-03-26
description: Wie man PDF‑Text mit OCR extrahiert. Lernen Sie, PDF als Bild zu laden,
  PDF‑Text zu erkennen und Text aus PDF mit einem einfachen Python‑Beispiel zu extrahieren.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize pdf text
- load pdf as image
- how to use OCR
language: de
og_description: Wie man PDF-Text mit OCR extrahiert. Dieser Leitfaden zeigt, wie man
  ein PDF als Bild lädt, PDF-Text erkennt und Text aus einem PDF in Python extrahiert.
og_title: Wie man PDF-Text mit OCR extrahiert – Vollständiges Tutorial
tags:
- OCR
- Python
- PDF processing
title: Wie man PDF‑Text mit OCR extrahiert – vollständige Schritt‑für‑Schritt‑Anleitung
url: /de/python-java/general/how-to-extract-pdf-text-with-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man PDF‑Text mit OCR extrahiert – vollständige Schritt‑für‑Schritt‑Anleitung

Haben Sie sich schon einmal gefragt, **wie man PDF**‑Dateien extrahiert, die eigentlich nur gescannte Bilder sind? Sie sind nicht allein – viele Entwickler stoßen an diese Grenze, wenn sie durchsuchbaren Inhalt benötigen, aber nur bildbasierte PDFs vorliegen. Die gute Nachricht? Ein paar Zeilen Code und eine solide OCR‑Bibliothek können diese Bild‑PDFs im Handumdrehen in Klartext verwandeln.  

In diesem Tutorial zeigen wir **wie man OCR** verwendet, um ein PDF als Bild zu laden, PDF‑Text zu erkennen und schließlich **Text aus PDF**‑Dokumenten beliebiger Länge zu **extrahieren**. Am Ende haben Sie ein lauffähiges Skript, eine klare Erklärung jedes Schrittes und einige Tipps, um die üblichen Fallstricke zu vermeiden.

## Was Sie benötigen

- Python 3.9 oder neuer (der Code funktioniert auch mit 3.10+)  
- Das Python‑Paket `ocr` (oder jede kompatible OCR‑Bibliothek, die `OcrEngine`, `OcrEngineMode` und `Imaging.Image` bereitstellt)  
- Ein mehrseitiges PDF, das Sie verarbeiten möchten (für das Demo nennen wir es `multi_page.pdf`)  
- Grundlegende Kenntnisse mit virtuellen Umgebungen (optional, aber empfohlen)

> **Pro‑Tipp:** Unter Windows sollten Sie die Anaconda Prompt verwenden; unter macOS/Linux reicht ein einfacher `python -m venv venv && source venv/bin/activate`.

## Schritt 1: Die OCR‑Bibliothek installieren

Zuerst holen Sie sich das OCR‑Paket von PyPI. Das untenstehende Beispiel verwendet ein fiktives `ocr`‑Paket, das die im Code‑Snippet gezeigte API nachbildet, aber die meisten realen Bibliotheken (wie `pytesseract` + `pdf2image`) folgen demselben Muster.

```bash
pip install ocr
```

Falls Sie eine andere Engine benutzen, ersetzen Sie `ocr` durch den entsprechenden Namen (z. B. `pip install pytesseract pdf2image`).

## Schritt 2: Die OCR‑Engine initialisieren

Das Erzeugen einer Engine‑Instanz ist die Grundlage von **wie man PDF**‑Text extrahiert. Denken Sie an die Engine als das Gehirn, das die Pixel jeder PDF‑Seite interpretiert.

```python
import ocr

# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Set the engine to the default mode (fast enough for most PDFs)
ocr_engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)
```

> **Warum das wichtig ist:** `set_engine_mode` lässt Sie Geschwindigkeit gegen Genauigkeit abwägen. `DEFAULT` ist ein ausgewogener Standard; wenn Sie höhere Präzision benötigen, wechseln Sie zu `HIGH_ACCURACY` (sofern die Bibliothek das unterstützt).

## Schritt 3: Das PDF als Bild‑Objekt laden

OCR arbeitet mit Bildern, nicht mit PDF‑Containern, daher müssen wir das PDF zuerst in eine Bilddarstellung konvertieren. Die Methode `Imaging.Image.load` verarbeitet mehrseitige PDFs automatisch.

```python
# Step 3: Load the multi‑page PDF as an image object
pdf_path = "YOUR_DIRECTORY/multi_page.pdf"
pdf_image = ocr.Imaging.Image.load(pdf_path)
```

> **Randfall:** Einige Bibliotheken akzeptieren nur ein einseitiges Bild. In diesem Fall würden Sie jede Seite mit `pdf2image.convert_from_path` in einer Schleife verarbeiten. Unser Aufruf von `load` kapselt das ab und macht **PDF als Bild laden** zu einem Einzeiler.

## Schritt 4: Text auf allen Seiten erkennen

Jetzt kommt der Kern von **PDF‑Text erkennen**. Die Engine scannt jede Seite und liefert eine Liste von Ergebnis‑Objekten – eines pro Seite.

```python
# Step 4: Recognize text on all pages of the PDF
page_results = ocr_engine.recognize_multi_page(pdf_image)
```

Jedes `page_result` enthält Methoden wie `get_text()` (Klartext) und `get_confidence()` (optional: Qualitätsmetrik).  

> **Tipp:** Wenn Sie nur die erste Seite benötigen, rufen Sie `recognize(pdf_image[0])` anstelle des Mehrseiten‑Hilfsprogramms auf.

## Schritt 5: Ergebnisse durchlaufen und extrahierten Text ausgeben

Abschließend iterieren wir über die Ergebnisse und geben den Text jeder Seite aus. Damit ist der **Text aus PDF**‑Workflow abgeschlossen.

```python
# Step 5: Print extracted text page by page
for index, page_result in enumerate(page_results):
    print(f"--- Page {index + 1} ---")
    print(page_result.get_text())
    # Optional: show confidence score
    # print(f"Confidence: {page_result.get_confidence():.2f}%")
```

### Erwartete Ausgabe

Enthält `multi_page.pdf` drei Seiten mit den Wörtern „Hello“, „World“ und „Python“, sehen Sie:

```
--- Page 1 ---
Hello
--- Page 2 ---
World
--- Page 3 ---
Python
```

Das war’s – Ihr PDF ist jetzt vollständig durchsuchbar und der Text steht für nachgelagerte Verarbeitung bereit (Indexierung, Sentiment‑Analyse, was auch immer).

## Schritt 6: Häufige Fallstricke behandeln

| Problem | Warum es passiert | Schnell‑Lösung |
|-------|----------------|-----------|
| **Leere Ausgabe** | PDF‑Seiten wurden mit niedriger DPI gescannt, sodass Zeichen nicht unterscheidbar sind. | Bild vor OCR hochskalieren: `pdf_image = pdf_image.resize(300)` (300 DPI ist ein guter Wert). |
| **Unsinnige Zeichen** | Nicht‑lateinische Alphabete benötigen Sprachpakete. | Passendes Sprachmodell laden: `ocr_engine.load_language('spa')` für Spanisch usw. |
| **Speicherexplosion bei riesigen PDFs** | Das Laden aller Seiten auf einmal verbraucht RAM. | Seiten in Batches verarbeiten: `for img in pdf_image.split(batch=10): …` (Pseudo‑Code). |
| **Langsame Performance** | `DEFAULT` bei einem massiven Dokument kann träge sein. | Auf `FAST`‑Modus umschalten oder OCR parallel mit `concurrent.futures` ausführen. |

## Bonus: Extrahierten Text in einer Datei speichern

Die meisten realen Pipelines benötigen den Text persistent. Hier ein kleiner Helfer, der alles in `output.txt` schreibt.

```python
output_path = "YOUR_DIRECTORY/output.txt"

with open(output_path, "w", encoding="utf-8") as f:
    for idx, result in enumerate(page_results):
        f.write(f"--- Page {idx + 1} ---\n")
        f.write(result.get_text() + "\n\n")
print(f"All text saved to {output_path}")
```

Jetzt können Sie `output.txt` in eine Suchmaschine, eine Datenbank oder ein beliebiges NLP‑Modell einspeisen.

## Alles zusammen – Vollständiges Skript

Unten finden Sie das komplette, sofort ausführbare Programm. Kopieren, Pfade anpassen und los geht’s.

```python
# -*- coding: utf-8 -*-
"""
How to extract PDF text with OCR – end‑to‑end example.

Prerequisites:
    pip install ocr
"""

import ocr

def extract_text_from_pdf(pdf_path: str):
    """
    Load a PDF, run OCR on every page, and return a list of strings.
    """
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)

    # Load PDF as image (multi‑page support)
    pdf_image = ocr.Imaging.Image.load(pdf_path)

    # Recognize text on all pages
    results = engine.recognize_multi_page(pdf_image)

    # Collect plain text
    texts = [res.get_text() for res in results]
    return texts

def main():
    pdf_file = "YOUR_DIRECTORY/multi_page.pdf"
    texts = extract_text_from_pdf(pdf_file)

    # Print and optionally save
    for i, txt in enumerate(texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()

    # Save to file
    out_path = "YOUR_DIRECTORY/extracted_text.txt"
    with open(out_path, "w", encoding="utf-8") as out_f:
        for i, txt in enumerate(texts, start=1):
            out_f.write(f"--- Page {i} ---\n{txt}\n\n")
    print(f"Extracted text stored in {out_path}")

if __name__ == "__main__":
    main()
```

Ausführen:

```bash
python extract_pdf_ocr.py
```

Sie sollten den Inhalt jeder Seite in der Konsole sehen, gefolgt von einer Bestätigung, dass die Datei `extracted_text.txt` erstellt wurde.

## Fazit

Wir haben **wie man PDF**‑Text aus bildbasierten Dokumenten mit einer OCR‑Engine extrahiert – von der Installation der Bibliothek über die Verarbeitung mehrseitiger Ergebnisse bis hin zum Speichern der Ausgabe. Sie wissen jetzt **wie man OCR verwendet**, wie man **PDF als Bild lädt** und wie man **PDF‑Text zuverlässig erkennt**.  

Nächste Schritte? Wechseln Sie den Standard‑Engine‑Modus zu einer hochpräzisen Einstellung, experimentieren Sie mit Sprachpaketen für mehrsprachige PDFs oder leiten Sie den extrahierten Text in einen Volltext‑Suchindex wie Elasticsearch weiter. Der Himmel ist das Limit, sobald Sie die Grundlagen des Text‑Extrahierens aus PDF‑Dateien beherrschen.

---

![how to extract pdf example](images/ocr_flowchart.png){alt="Wie man den PDF‑Arbeitsablauf extrahiert"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}