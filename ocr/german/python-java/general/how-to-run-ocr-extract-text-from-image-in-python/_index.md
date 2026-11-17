---
category: general
date: 2026-03-26
description: Wie man OCR auf einer PNG‑Datei ausführt und Text aus dem Bild mit einem
  benutzerdefinierten Wörterbuch für verbesserte OCR‑Genauigkeit extrahiert. Lernen
  Sie, das Bild für OCR schnell zu laden.
draft: false
keywords:
- how to run OCR
- extract text from image
- recognize text from png
- improve OCR accuracy
- load image for OCR
language: de
og_description: Wie man OCR auf einer PNG‑Datei ausführt und Text aus dem Bild mit
  benutzerdefiniertem Wörterbuch für verbesserte OCR‑Genauigkeit extrahiert. Schritt‑für‑Schritt‑Anleitung.
og_title: Wie man OCR ausführt – Text aus einem Bild in Python extrahieren
tags:
- OCR
- Python
- Image Processing
title: Wie man OCR ausführt – Text aus Bild in Python extrahieren
url: /de/python-java/general/how-to-run-ocr-extract-text-from-image-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR ausführt – Text aus Bild in Python extrahieren

Haben Sie sich jemals gefragt, **wie man OCR** auf einer gescannten Rechnung oder einem Screenshot ausführt und sauberen, durchsuchbaren Text erhält? Sie sind nicht allein. In vielen Projekten besteht die Engstelle einfach darin, das Bild für OCR zu laden und dann die Engine dazu zu bringen, domänenspezifische Wörter zu verstehen.  

In diesem Tutorial gehen wir Schritt für Schritt durch ein komplettes, sofort ausführbares Beispiel, das **Text aus Bild**‑Dateien extrahiert, Ihnen zeigt, wie Sie **Text aus PNG**‑Assets **erkennen**, und sogar Tricks demonstriert, um **die OCR‑Genauigkeit zu verbessern** mit benutzerdefinierten Wörterbüchern und Sonderzeichen. Am Ende haben Sie ein eigenständiges Skript, das Sie in jede Python‑Codebasis einbinden können.

## Was Sie benötigen

- Python 3.8+ (der Code verwendet Typannotationen, funktioniert aber auch mit früheren 3.x‑Versionen)
- Die `ocr`‑Bibliothek, die mit der OCR‑Engine Ihrer Wahl geliefert wird (installieren Sie sie via `pip install ocr‑engine` – ersetzen Sie den Namen durch das tatsächliche Paket)
- Eine Bilddatei (`input.png`), die Sie verarbeiten möchten
- Optional: eine Klartext‑Datei (`invoice_terms.txt`) mit domänenspezifischen Wörtern, ein Wort pro Zeile

Keine schweren externen Abhängigkeiten, keine Cloud‑API‑Schlüssel, nur eine lokale OCR‑Engine.

---

## Schritt 1: Installieren und Importieren der OCR‑Bibliothek

Zuerst stellen Sie sicher, dass das OCR‑Paket installiert ist. Wenn Sie das hypothetische `ocr-engine`‑Paket verwenden, führen Sie aus:

```bash
pip install ocr-engine
```

Importieren Sie nun die Klassen, die Sie benötigen:

```python
# Step 1: Import the OCR SDK
import ocr
from ocr import Imaging
```

> **Pro‑Tipp:** Wenn Sie in einer virtuellen Umgebung arbeiten, aktivieren Sie diese vor der Installation, um Ihr globales Python sauber zu halten.

## Schritt 2: Erstellen einer OCR‑Engine‑Instanz

Das Erzeugen eines Engine‑Objekts ist der Einstiegspunkt für jede OCR‑Aufgabe. Denken Sie daran wie das Einschalten der Scanner‑Hardware in Software.

```python
# Step 2: Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
```

Warum das wichtig ist: Die Engine hält Konfigurationen wie Sprachpakete, Erkennungsmodi und alle benutzerdefinierten Ressourcen, die Sie später anhängen werden. Ohne sie können Sie **Bild für OCR laden** oder die Erkennungspipeline nicht ausführen.

## Schritt 3: Laden des Bildes, das Sie erkennen möchten

Hier **laden wir das Bild für OCR**. Die Methode `Imaging.Image.load()` liest die Datei und konvertiert sie in das interne Bitmap‑Format, das die Engine erwartet.

```python
# Step 3: Load the PNG image you want to process
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Imaging.Image.load(image_path))
```

Wenn Sie ein JPEG oder TIFF haben, funktioniert dieselbe Methode – ändern Sie einfach die Dateierweiterung. Die Engine erkennt das Format automatisch.

> **Randfall:** Sehr große Bilder (über 5 MP) können Speicherspitzen verursachen. Skalieren Sie das Bild ggf. mit Pillow herunter, bevor Sie es laden, falls Sie Leistungsprobleme bemerken.

## Schritt 4: Bereitstellung eines benutzerdefinierten Wörterbuchs zur Steigerung der Genauigkeit

Die meisten OCR‑Engines werden mit generischen Sprachmodellen ausgeliefert. Für Rechnungen, Quittungen oder juristische Dokumente werden häufig Wörter übersehen. Das Bereitstellen einer eigenen Wortliste sagt der Engine: „Diese Begriffe sind gültig, behandle sie als korrekt“.

```python
# Step 4: Attach a custom dictionary (one word per line)
custom_dict_path = "YOUR_DIRECTORY/invoice_terms.txt"
ocr_engine.set_custom_dictionary(custom_dict_path)
```

Typische Einträge könnten sein:

```
VAT
InvoiceNumber
Øre
ß
Ħ
```

Das Hinzufügen dieser Einträge verbessert die **Verbesserung der OCR‑Genauigkeit**‑Metrik dramatisch – besonders für Nicht‑ASCII‑Symbole.

## Schritt 5: Hinzufügen von Sonderzeichen, die nicht im Standardsatz enthalten sind

Wenn Ihre Domäne Symbole wie das Euro‑Zeichen (€) oder das skandinavische Ø verwendet, können Sie diese explizit hinzufügen:

```python
# Step 5: Register additional characters
ocr_engine.add_custom_characters("ØßĦ")
```

Die Engine wird diese Glyphen nun während der Erkennungsphase als gültig behandeln, wodurch die Wahrscheinlichkeit von „Müll“-Ausgaben sinkt.

## Schritt 6: Ausführen des OCR‑Prozesses und Abrufen des Textes

Zum Schluss rufen Sie den Erkenner auf und holen das Klartext‑Ergebnis. Der Aufruf `recognize()` liefert ein reichhaltiges Objekt; für die meisten Anwendungsfälle benötigen wir nur den rohen String.

```python
# Step 6: Execute OCR and print the result
result = ocr_engine.recognize()
print("=== Recognized Text ===")
print(result.get_text())
```

**Erwartete Ausgabe** (gekürzt zur Übersicht):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total: €1,250.00
VAT: 25%
...
```

Wenn die Ausgabe unleserlich erscheint, prüfen Sie, ob Ihr benutzerdefiniertes Wörterbuch und die Sonderzeichen korrekt geladen wurden.

---

## Visueller Überblick

![Diagramm zur Ausführung von OCR](ocr-workflow.png){alt="Diagramm zur Ausführung von OCR"}

Das obige Diagramm veranschaulicht den Ablauf vom Laden eines Bildes bis zum Erhalt von sauberem Text und hebt hervor, wo Sie benutzerdefinierte Wörterbücher und Zeichensätze einbinden können.

---

## Häufige Fragen & Stolperfallen

### Funktioniert das mit mehrseitigen PDFs?

Ja – konvertieren Sie einfach jede Seite zu einer PNG (mit `pdf2image` oder ähnlichem) und geben Sie sie nacheinander an dieselbe `ocr_engine`‑Instanz weiter. Die Engine verarbeitet jedes Bild unabhängig, sodass Sie eine Liste von Zeichenketten erhalten, die Sie zusammenfügen können.

### Was, wenn das Bild gedreht ist?

Die meisten modernen OCR‑Engines erkennen die Orientierung automatisch, Sie können jedoch eine Drehung erzwingen mit:

```python
ocr_engine.set_image(Imaging.Image.load(image_path).rotate(90))
```

### Wie geht man mit anderen Sprachen als Englisch um?

Tauschen Sie das Sprachmodell aus, bevor Sie das Bild laden:

```python
ocr_engine.set_language("de")  # German
```

Stellen Sie sicher, dass das entsprechende Sprachpaket installiert ist.

---

## Vollständiges Skript – Bereit zum Kopieren & Einfügen

Unten finden Sie das gesamte Programm, das nach dem Ersetzen der Platzhalter‑Pfade sofort ausführbar ist.

```python
#!/usr/bin/env python3
"""
How to Run OCR – Complete example that extracts text from a PNG,
uses a custom dictionary, and adds special characters for better accuracy.
"""

# Install the OCR package first:
# pip install ocr-engine

import ocr
from ocr import Imaging

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = ocr.OcrEngine()

    # 2️⃣ Load the image you want to recognize
    image_path = "YOUR_DIRECTORY/input.png"      # <-- change this
    ocr_engine.set_image(Imaging.Image.load(image_path))

    # 3️⃣ Provide a custom dictionary (optional but recommended)
    dict_path = "YOUR_DIRECTORY/invoice_terms.txt"   # one word per line
    ocr_engine.set_custom_dictionary(dict_path)

    # 4️⃣ Add any special characters not covered by the default set
    ocr_engine.add_custom_characters("ØßĦ")   # e.g., currency symbols

    # 5️⃣ Run the OCR process
    result = ocr_engine.recognize()

    # 6️⃣ Output the recognized text
    print("=== Recognized Text ===")
    print(result.get_text())

if __name__ == "__main__":
    main()
```

Führen Sie es aus mit:

```bash
python run_ocr.py
```

Sie sollten den extrahierten Text in der Konsole ausgegeben sehen. Von dort aus können Sie ihn in eine Datei schreiben, in eine Datenbank einspeisen oder an nachgelagerte NLP‑Pipelines weitergeben.

---

## Zusammenfassung & nächste Schritte

Wir haben behandelt, **wie man OCR** auf einer PNG ausführt, **wie man Text aus Bild** extrahiert und praktische Wege gezeigt, **Text aus PNG** zu **erkennen**, während wir **die OCR‑Genauigkeit** mit Wörterbüchern und benutzerdefinierten Zeichen verbessern.  

Als Nächstes überlegen Sie:

- **Batch‑Verarbeitung:** Durchlaufen Sie ein Verzeichnis mit Bildern.
- **Nachbearbeitung:** Verwenden Sie Regex, um Rechnungsnummern oder Daten herauszuziehen.
- **Integration:** Binden Sie das Skript in eine Flask‑API für On‑Demand‑OCR‑Dienste ein.

Wenn Sie neugierig auf weiterführende Themen sind, schauen Sie sich Tutorials zu **Bild für OCR laden** mit OpenCV‑Vorverarbeitung an oder tauchen Sie ein in Deep‑Learning‑basierte OCR‑Modelle wie Tesseract 4+ mit LSTM‑Schichten.

---

### Weiter experimentieren!

Versuchen Sie, die `invoice_terms.txt` durch eine Liste medizinischer Fachbegriffe zu ersetzen, fügen Sie griechische Zeichen hinzu oder geben Sie der Engine ein Bild mit niedriger Auflösung, um zu sehen, wie weit die Genauigkeit noch reicht. Je mehr Sie herumprobieren, desto besser verstehen Sie die Kompromisse zwischen Vorverarbeitung, benutzerdefinierten Vokabularen und Engine‑Einstellungen.

Viel Spaß beim Coden und möge Ihr OCR‑Ergebnis stets klar und präzise sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}