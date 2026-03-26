---
category: general
date: 2026-03-26
description: Erfahren Sie, wie Sie OCR in Python durchführen und Text einfach aus
  Bildern extrahieren, Text aus Scans lesen oder Text aus Rechnungen mit einer einfachen
  OcrEngine extrahieren.
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from scan
- extract text from invoice
- how to use OCR
language: de
og_description: Wie führt man OCR in Python durch? Dieser Leitfaden zeigt Ihnen, wie
  Sie Text aus Bildern extrahieren, Text aus Scans lesen und Text aus Rechnungen in
  Minuten extrahieren.
og_title: Wie man OCR in Python durchführt – Text schnell extrahieren
tags:
- OCR
- Python
- Image Processing
title: Wie man OCR in Python durchführt – Text schnell extrahieren
url: /de/python/general/how-to-perform-ocr-in-python-extract-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in Python durchführt – Text schnell extrahieren

Haben Sie sich jemals gefragt, **wie man OCR** auf einem gescannten Beleg oder einer verschwommenen PDF durchführt? Sie sind nicht allein. In vielen Projekten taucht das Bedürfnis, **Text aus Bild zu extrahieren**, früher oder später auf, und der übliche Ansatz „alles von Hand tippen“ ist einfach nicht skalierbar.  

In diesem Tutorial sehen Sie ein vollständiges, sofort ausführbares Beispiel, das **zeigt, wie man OCR** verwendet, um Text aus einem Scan zu lesen, Daten aus einer Rechnung zu extrahieren und sogar die automatische Schräglagenkorrektur zu handhaben – alles mit nur wenigen Zeilen Python.

## Was Sie lernen werden

* Die genauen Abhängigkeiten und Importe, die benötigt werden.
* Wie man eine `OcrEngine`‑Instanz erstellt und konfiguriert.
* Möglichkeiten, **Text aus Bild zu extrahieren**, **Text aus Scan zu lesen** und **Text aus Rechnung zu extrahieren** mit derselben Engine zu nutzen.
* Häufige Fallstricke (falsche Sprache, fehlende Dateien, große Bilder) und wie man sie vermeidet.
* Erwartete Ausgabe, damit Sie überprüfen können, ob das OCR erfolgreich war.

Keine externen Dokumentationslinks sind nötig – alles ist in sich geschlossen, sodass Sie den Code kopieren‑einfügen und die Ergebnisse sofort sehen können.

## Voraussetzungen

Bevor wir loslegen, stellen Sie sicher, dass Sie Folgendes haben:

* Python 3.8+ installiert (das `ocr`‑Paket funktioniert mit jeder aktuellen Version).
* Die `ocr`‑Bibliothek verfügbar (`pip install ocr‑engine` – ersetzen Sie den Namen durch den tatsächlichen Paketnamen, falls abweichend).
* Eine Bilddatei, die Sie verarbeiten möchten – für die Demo verwenden wir `invoice.png` in einem Ordner namens `YOUR_DIRECTORY`.

Das war’s. Wenn Sie das bereits haben, können Sie loslegen.

## Schritt 1: Installieren und importieren des OCR‑Moduls

Zuerst das Wichtigste: Wir benötigen die OCR‑Bibliothek. Wenn Sie sie noch nicht installiert haben, führen Sie den folgenden Befehl in Ihrem Terminal aus:

```bash
pip install ocr-engine
```

Jetzt importieren wir das Modul in unser Skript.

```python
# Step 1: Import the OCR module
import ocr
```

> **Pro Tipp:** Halten Sie Ihre virtuelle Umgebung sauber; das verhindert Versionskonflikte, wenn Sie später weitere Bild‑Verarbeitungs‑Pakete hinzufügen.

## Schritt 2: Erstellen und konfigurieren der OCR‑Engine

Die Engine zu erstellen ist so einfach wie den Konstruktor aufzurufen, aber die eigentliche Stärke liegt in der korrekten Konfiguration. Wir setzen die Sprache auf Englisch und aktivieren die automatische Schräglagenkorrektur, was bei gescannten Rechnungen, die nicht perfekt ausgerichtet sind, unerlässlich ist.

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Step 3: Configure the engine – set language and enable automatic skew correction
engine.language = ocr.Language.English   # any supported language, e.g., Spanish, French
engine.auto_skew = True                 # fixes tilted scans automatically
```

Warum `auto_skew` aktivieren? Viele Scanner erzeugen Bilder, die um einige Grad gedreht sind. Ohne Korrektur könnte die Engine Zeichen übersehen und eine perfekt lesbare Rechnung in Kauderwelsch verwandeln.

## Schritt 3: OCR auf Ihrem Zielbild ausführen

Jetzt übergeben wir die Bilddatei an die Engine. Die Methode `recognize_image` gibt ein Objekt zurück, das den Rohtext sowie Konfidenzwerte enthält (falls die Bibliothek diese bereitstellt).

```python
# Step 4: Perform OCR on the target image
ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

Wenn Sie ein **read text from scan**‑Szenario haben, ersetzen Sie einfach den Pfad durch das gescannte PDF, das in PNG oder JPEG konvertiert wurde. Der gleiche Aufruf funktioniert für jedes Bildformat, das die zugrunde liegende Bibliothek unterstützt.

## Schritt 4: Untersuchen und verwenden des extrahierten Textes

Lassen Sie uns die rohe OCR‑Ausgabe ausgeben. In einer realen Rechnungsverarbeitungspipeline würden Sie diesen String wahrscheinlich parsen, Positionen, Summen und Daten extrahieren, aber für den Moment bestätigt ein kurzer Blick, dass das OCR erfolgreich war.

```python
# Step 5: Display the raw extracted text
print("Raw OCR text:\n", ocr_result.text)
```

**Erwartete Ausgabe (gekürzt für die Übersicht):**

```
Raw OCR text:
 Invoice #12345
 Date: 2026‑03‑01
 Bill To: Acme Corp.
 Item          Qty   Price   Total
 ------------------------------------------------
 Widget A      10    5.00    50.00
 Widget B      5     12.00   60.00
 ------------------------------------------------
 Subtotal:                     110.00
 Tax (5%):                     5.50
 Grand Total:                  115.50
```

Wenn die Ausgabe unleserlich aussieht, prüfen Sie, ob das Bild klar ist und ob `engine.language` mit der Sprache des Dokuments übereinstimmt.

## Schritt 5: Umgang mit häufigen Sonderfällen

### Große Bilder

Die Verarbeitung eines 5000 × 5000 Pixel‑Scans kann speicherintensiv sein. Eine schnelle Möglichkeit, dies zu mildern, besteht darin, das Bild vor dem Senden an die Engine zu verkleinern:

```python
from PIL import Image

def load_and_resize(path, max_dim=2000):
    img = Image.open(path)
    img.thumbnail((max_dim, max_dim), Image.ANTIALIAS)
    return img

scaled_image = load_and_resize("YOUR_DIRECTORY/invoice.png")
ocr_result = engine.recognize_image(scaled_image)
```

### Mehrere Sprachen

Wenn Sie **Text aus Bild** extrahieren müssen, das sowohl Englisch als auch Spanisch enthält, können Sie eine Sprachliste festlegen:

```python
engine.language = [ocr.Language.English, ocr.Language.Spanish]
```

Die Engine wird versuchen, Zeichen aus beiden Sprachsätzen zu erkennen.

### Fehlerbehandlung

Nehmen Sie nie an, dass die Datei existiert. Umhüllen Sie den Aufruf mit einem try‑except‑Block, um eine freundliche Meldung auszugeben:

```python
try:
    ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
    print("OCR succeeded!")
except FileNotFoundError:
    print("Error: The image file was not found. Check the path and try again.")
except ocr.OcrError as e:
    print(f"OCR failed with error: {e}")
```

## Visuelle Referenz

Unten sehen Sie einen Screenshot der Beispielrechnung, die wir in der Demo verwendet haben. Beachten Sie die leichte Neigung – genau das, was `auto_skew` korrigiert.

![wie man OCR auf einer Rechnung anwendet – Bild zeigt automatische Schräglagenkorrektur](/images/ocr-example.png)

*Alt-Text:* wie man OCR auf einer Rechnung anwendet – Bild zeigt automatische Schräglagenkorrektur.

## Vollständiges, ausführbares Beispiel

Wenn wir alles zusammenfügen, erhalten Sie ein einzelnes Skript, das Sie von der Befehlszeile aus ausführen können. Es deckt Installation, Konfiguration, Fehlerbehandlung und einen einfachen Nachbearbeitungsschritt ab, der den extrahierten Text in eine Datei namens `output.txt` schreibt.

```python
# full_ocr_demo.py
# -------------------------------------------------
# Demonstrates how to perform OCR, extract text from image,
# read text from scan, and extract text from invoice.
# -------------------------------------------------

import ocr
from pathlib import Path

def main(image_path: str, output_path: str = "output.txt"):
    # Create and configure the engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.auto_skew = True

    # Verify the image exists
    if not Path(image_path).is_file():
        print(f"❌  Image not found: {image_path}")
        return

    # Run OCR
    try:
        result = engine.recognize_image(image_path)
    except ocr.OcrError as err:
        print(f"❌  OCR failed: {err}")
        return

    # Output the raw text
    print("✅  OCR completed. Raw text:")
    print(result.text)

    # Save to a text file for later processing
    Path(output_path).write_text(result.text, encoding="utf-8")
    print(f"💾  Text saved to {output_path}")

if __name__ == "__main__":
    # Replace with your actual file location
    main("YOUR_DIRECTORY/invoice.png")
```

Das Ausführen von `python full_ocr_demo.py` gibt den extrahierten Text in der Konsole aus und speichert ihn in `output.txt`. Von dort aus können Sie reguläre Ausdrücke, CSV‑Writer oder jede andere Logik anwenden, die Sie für die Automatisierung von **Text aus Rechnung extrahieren** benötigen.

## Fazit

Sie haben nun eine solide End‑zu‑End‑Lösung für **wie man OCR** in Python durchführt. Durch das Erstellen einer `OcrEngine`, das Konfigurieren von Sprache und Schräglagenkorrektur und das Behandeln einiger praktischer Sonderfälle können Sie zuverlässig **Text aus Bild extrahieren**, **Text aus Scan lesen** und **Text aus Rechnung extrahieren**, ohne in verstreuter Dokumentation zu suchen.

Was kommt als Nächstes? Versuchen Sie, eine Stapel von Dateien in einer Schleife zu verarbeiten, experimentieren Sie mit verschiedenen Sprachen oder verbinden Sie die Ausgabe mit einer PDF‑Generierungsbibliothek, um durchsuchbare PDFs zu erstellen. Der Himmel ist die Grenze, und der Code, den Sie gerade gesehen haben, ist ein robustes Sprungbrett.

Haben Sie Fragen zu einem bestimmten Dateiformat oder benötigen Hilfe beim Anpassen von Konfidenzschwellen? Hinterlassen Sie unten einen Kommentar – ich helfe Ihnen gerne, Ihre OCR‑Pipeline zu optimieren!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}