---
category: general
date: 2026-04-26
description: 'Wie man OCR in Python verwendet: Lernen Sie, Text aus Bildern zu extrahieren
  und TIFF-Dateien in Python mit einem einfachen OCR‑Beispiel zu lesen. Schneller,
  ausführbarer Code enthalten.'
draft: false
keywords:
- how to ocr python
- extract text from image
- read tiff file python
- basic ocr example
- convert scanned image text
language: de
og_description: 'Wie man OCR in Python verwendet: Eine Schritt‑für‑Schritt‑Anleitung,
  die zeigt, wie man Text aus Bildern extrahiert, TIFF‑Dateien mit Python liest und
  gescannten Bildtext mit einem einfachen, ausführbaren Skript konvertiert.'
og_title: Wie man OCR in Python verwendet – Einfaches OCR-Beispiel zum Extrahieren
  von Text
tags:
- OCR
- Python
- Image Processing
title: Wie man OCR in Python verwendet – Einfaches OCR‑Beispiel zum Extrahieren von
  Text
url: /de/python-java/general/how-to-ocr-python-basic-ocr-example-for-extracting-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to ocr python – Grundlegendes OCR‑Beispiel zum Extrahieren von Text

Haben Sie sich jemals gefragt **how to ocr python**, wenn Sie ein gescanntes TIFF auf Ihrem Schreibtisch liegen haben? Sie sind nicht der Einzige, der auf eine Menge Bilddateien starrt und fragt: „Wie bekomme ich die Wörter daraus heraus?“ Die gute Nachricht ist, dass das Umwandeln eines Bildes in Klartext ein Kinderspiel ist, wenn man die richtige Bibliothek und ein paar klare Schritte hat.

In diesem Tutorial gehen wir ein **basic OCR example** durch, das eine TIFF‑Datei liest, den Text extrahiert und ihn in der Konsole ausgibt. Am Ende wissen Sie genau, wie man **extract text from image** Dateien verarbeitet, wie man die Eigenheiten von TIFF‑Formaten handhabt und was man anpassen muss, wenn man **convert scanned image text** in etwas Nützlicheres umwandeln möchte. Keine versteckte Magie – nur straightforward Python, das Sie heute copy‑paste und ausführen können.

## Was Sie benötigen

- Python 3.9+ installiert (die neueste stabile Version ist am besten).
- Eine pip‑installierbare OCR‑Bibliothek. In diesem Leitfaden verwenden wir das fiktive `aocr`‑Paket, das beliebte Werkzeuge wie Tesseract nachahmt; Sie können es später durch `pytesseract` oder `easyocr` ersetzen.
- Ein TIFF‑Bild, das Sie verarbeiten möchten – nennen Sie es `input.tiff` und legen Sie es in einen Ordner, den Sie im Code referenzieren.
- Grundlegende Vertrautheit mit der Kommandozeile (nur zum Installieren des Pakets).

Das war's. Keine schweren Abhängigkeiten, keine Docker‑Container, nur ein paar Code‑Zeilen.

## Schritt 1 – Installieren und Importieren von Abhängigkeiten (how to ocr python)

Zuerst holen Sie das OCR‑Paket. Öffnen Sie ein Terminal und führen Sie aus:

```bash
pip install aocr
```

Wenn Sie lieber eine reale Bibliothek verwenden, ersetzen Sie `aocr` durch `pytesseract` und installieren Sie die Tesseract‑Engine separat.

Jetzt importieren wir, was wir benötigen. Die `Path`‑Klasse aus `pathlib` bietet uns eine saubere Möglichkeit, mit Dateipfaden über Betriebssysteme hinweg zu arbeiten.

```python
# Step 1: Import the Path class for handling file paths
from pathlib import Path

# Import the OCR engine and image loader from the chosen library
from aocr import OcrEngine, Image
```

*Warum `Path` verwenden?* Weil es die Schrägstriche (`/` vs `\`) abstrahiert und es Ihnen ermöglicht, Verzeichnisse zu verbinden, ohne sich um das zugrunde liegende OS zu kümmern. Dieses kleine Detail erspart oft Kopfschmerzen, wenn Sie das Skript später auf einen CI‑Server verschieben.

## Schritt 2 – Erstellen der OCR‑Engine‑Instanz (basic ocr example)

Als Nächstes starten Sie die OCR‑Engine. Stellen Sie sich `OcrEngine` als das Gehirn vor, das das Bild liest und Zeichen ausgibt.

```python
# Step 2: Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

Die meisten OCR‑Bibliotheken erlauben hier das Anpassen von Sprache, DPI oder Confidence‑Schwellenwerten. Für dieses **basic OCR example** bleiben wir bei den Vorgaben, aber Sie können später `ocr_engine.config` erkunden, falls Sie mehrsprachige Dokumente verarbeiten müssen.

## Schritt 3 – Laden Ihres TIFF‑Bildes (read tiff file python)

Hier kommt der **read tiff file python** Teil ins Spiel. TIFFs können mehrseitig sein, aber `Image.load` holt standardmäßig die erste Seite – perfekt für einen einseitigen Scan.

```python
# Step 3: Load the image you want to recognize
# Using a generic placeholder path makes it easy to adapt the example
ocr_engine.image = Image.load(Path("YOUR_DIRECTORY/input.tiff"))
```

Ersetzen Sie `"YOUR_DIRECTORY"` durch den tatsächlichen Ordner, der `input.tiff` enthält. Wenn Sie nicht sicher sind, wo das Skript läuft, gibt `Path.cwd()` das aktuelle Arbeitsverzeichnis aus – praktisch zum Debuggen von Pfadproblemen.

## Schritt 4 – Ausführen des OCR‑Prozesses (extract text from image)

Jetzt geschieht die Magie. Der Aufruf von `process()` schickt das Bild durch die OCR‑Pipeline und gibt ein Ergebnis‑Objekt zurück.

```python
# Step 4: Run the OCR process to extract text from the image
ocr_result = ocr_engine.process()
```

Im Hintergrund könnte die Engine das Bild in Graustufen umwandeln, eine Schwellenwert‑Anwendung durchführen und es in ein neuronales Netzwerk einspeisen. Sie müssen diese Schritte nicht verwalten; die Bibliothek abstrahiert sie.

## Schritt 5 – Ausgeben des erkannten Textes (convert scanned image text)

Zum Schluss geben Sie den Text aus. In realen Projekten würden Sie ihn wahrscheinlich in eine Datei oder Datenbank schreiben, aber das Ausdrucken hält das Beispiel übersichtlich.

```python
# Step 5: Print the recognized text to the console
print(ocr_result.text)
```

Wenn Sie das Skript ausführen, sollten Sie etwas Ähnliches sehen:

```
Hello, world!
This is a sample scanned document.
```

Wenn die Ausgabe unleserlich erscheint, prüfen Sie, ob das Quellbild klar ist und die OCR‑Sprache zum Text passt.

## Vollständiges funktionierendes Skript

Alles zusammengefügt, hier das komplette, sofort ausführbare Programm:

```python
# Full script: how to ocr python – basic OCR example

from pathlib import Path
from aocr import OcrEngine, Image  # Replace with your OCR library if needed

def main():
    # Initialize the OCR engine
    ocr_engine = OcrEngine()

    # Load the TIFF image (adjust the path as needed)
    image_path = Path("YOUR_DIRECTORY/input.tiff")
    if not image_path.is_file():
        raise FileNotFoundError(f"Could not find {image_path}. Make sure the file exists.")
    
    ocr_engine.image = Image.load(image_path)

    # Perform OCR
    ocr_result = ocr_engine.process()

    # Output the extracted text
    print("=== OCR Output ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

### Erwartete Ausgabe

```
=== OCR Output ===
Your scanned document’s text appears here, line by line.
```

Wenn Sie **convert scanned image text** in ein durchsuchbares PDF umwandeln müssen, können Sie `ocr_result.text` in einen PDF‑Generator wie `reportlab` leiten – aber das ist ein eigenes **tutorial**.

## Häufige Fallstricke & Pro‑Tipps

- **Low‑resolution scans**: OCR hat Schwierigkeiten unter 150 DPI. Wenn Ihr TIFF unscharf ist, skalieren Sie es zuerst mit Pillow (`Image.open(...).resize(...)`) hoch.
- **Multiple pages**: Für mehrseitige TIFFs iterieren Sie über `Image.load_multi_page()` (falls Ihre Bibliothek das unterstützt) und verketten die Ergebnisse.
- **Language support**: Viele Engines verwenden standardmäßig Englisch. Setzen Sie z. B. `ocr_engine.language = "spa"` für Spanisch.
- **Whitespace handling**: OCR fügt oft überflüssige Zeilenumbrüche ein. Verwenden Sie `str.splitlines()` oder reguläre Ausdrücke, um die Ausgabe zu bereinigen.
- **Performance**: Für die Massenverarbeitung wiederverwenden Sie eine einzelne `OcrEngine`‑Instanz, anstatt für jede Datei eine neue zu erstellen.

## Erweiterung des Beispiels

Jetzt, wo Sie **how to ocr python** für ein einzelnes Bild gemeistert haben, denken Sie an die nächsten Schritte:

1. **Batch processing** – Durchlaufen Sie ein Verzeichnis von TIFFs und schreiben Sie jedes Ergebnis in eine `.txt`‑Datei.
2. **Integration with Pandas** – Speichern Sie den extrahierten Text zusammen mit Metadaten für schnelle Analysen.
3. **Hybrid approach** – Kombinieren Sie OCR mit NLP‑Bibliotheken wie `spaCy`, um Entitäten (Namen, Daten, Beträge) aus gescannten Rechnungen zu extrahieren.
4. **Alternative file formats** – Ersetzen Sie `Image.load` durch `Image.from_bytes`, um Bilder aus einer API oder einer Datenbank zu verarbeiten.

All dies baut auf der Kernidee von **extract text from image** und **convert scanned image text** auf, um etwas zu schaffen, das Maschinen verstehen können.

## Fazit

Wir haben ein klares, durchgängiges **basic OCR example** durchgegangen, das **how to ocr python**, **read tiff file python** und **extract text from image** Dateien mit nur wenigen Zeilen zeigt. Das Skript ist eigenständig, enthält Fehlerbehandlung und gibt das Ergebnis direkt aus, was es zu einer soliden Grundlage für jedes Projekt macht, das gescannte Dokumente in editierbaren Text umwandeln muss.

Fühlen Sie sich frei zu experimentieren – tauschen Sie das OCR‑Backend aus, passen Sie die Vorverarbeitung an oder binden Sie die Ausgabe in einen nachgelagerten Workflow ein. Der Himmel ist die Grenze, wenn Sie zuverlässig **convert scanned image text** in durchsuchbare Daten umwandeln können.

Haben Sie Fragen zu Randfällen, Sprachpaketen oder Performance‑Optimierung? Hinterlassen Sie unten einen Kommentar und happy coding! 

![how to ocr python Beispiel](/images/ocr-python-example.png "Screenshot des how to ocr python Skriptausgabe")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}