---
category: general
date: 2026-06-25
description: Wie man OCR in Python verwendet – lernen Sie, wie Sie ein Bild für OCR
  laden, Text in einem Bereich erkennen und den Bereichstext schnell extrahieren.
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: de
og_description: Wie man OCR in Python verwendet – Schritt‑für‑Schritt‑Anleitung zum
  Laden eines Bildes, Erkennen von Text in einem bestimmten Bereich und Extrahieren
  der Rechnungsnummer.
og_title: 'Wie man OCR in Python verwendet: Bild laden und Text aus Region extrahieren'
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 'Wie man OCR mit Python nutzt: Bild laden und Text aus einem Bereich extrahieren'
url: /de/python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in Python verwendet: Bild laden und Text eines Bereichs extrahieren

**Wie man OCR in Python verwendet** ist einfacher, als man denkt. Hast du schon einmal eine gescannte Rechnung angesehen und dich gefragt, wie man nur die Rechnungsnummer herausziehen kann, ohne die ganze Seite zu parsen? Du bist nicht allein – viele Entwickler stoßen beim ersten Experimentieren mit optischer Zeichenerkennung auf dieses Problem. In diesem Leitfaden gehen wir Schritt für Schritt durch das Laden eines Bildes für OCR, das Definieren eines Rechtecks, das Erkennen von Text in diesem Bereich und schließlich das Extrahieren des Bereichstextes. Am Ende hast du ein sofort ausführbares Skript, das jedes gewünschte Textstück isoliert.

> *Pro Tipp:* Wenn du mit PDFs arbeitest, konvertiere jede Seite zuerst in ein Bild – die meisten OCR‑Bibliotheken arbeiten am besten mit PNG/JPEG.

## Was du brauchst

- Python 3.8+ (die neueste stabile Version wird empfohlen)  
- Eine OCR‑Bibliothek, die eine `OcrEngine`‑Klasse bereitstellt (z. B. **ocr** von `pip install ocr-lib`)  
- Ein Beispielbild – hier verwenden wir `invoice.png`, das in einem Ordner liegt, den du kontrollierst  
- Grundlegende Kenntnisse über Rechtecke (x, y, Breite, Höhe)  

Keine schweren Abhängigkeiten, keine GPU nötig – nur reine CPU‑Arbeit, was die Portabilität erhöht.

---

## Wie man OCR verwendet: Engine initialisieren (Schritt 1)

Bevor irgendein Text gelesen werden kann, benötigst du eine Instanz der OCR‑Engine. Sie ist das „Gehirn“, das Pixelmuster analysiert.

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Warum das wichtig ist:* Das Initialisieren der Engine lädt Sprachmodelle und setzt Standardkonfigurationen. Wird dieser Schritt übersprungen, wirft das System sofort eine Ausnahme, sobald du `recognize_region` aufrufst.

---

## Bild für OCR laden (Schritt 2)

Jetzt, wo die Engine bereit ist, übergeben wir ihr ein Bild. Die Methode `Image.load` der Bibliothek verarbeitet gängige Formate und normalisiert das Bitmap.

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

Falls die Datei nicht gefunden wird, wirft Python einen `FileNotFoundError`. Stelle sicher, dass der Pfad absolut oder relativ zum Arbeitsverzeichnis deines Skripts ist.  

*Randfall:* Einige OCR‑Engines erwarten ein Graustufen‑Bild. Wenn die Genauigkeit schlecht ist, konvertiere das Bild zuerst:

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

---

## Text im Bereich erkennen (Schritt 3)

Das Definieren des Bereichs ist der Moment, in dem du der Engine sagst, *wo* sie suchen soll. Das `Rectangle` akzeptiert Gleitkommawerte für Sub‑Pixel‑Präzision, was bei hochauflösenden Scans praktisch ist.

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – obere linke Ecke des Rechtecks (in Pixel)  
- **width, height** – Größe des Rechtecks  

Du fragst dich vielleicht, wie du diese Zahlen bekommst. Eine schnelle Methode ist, das Bild in einem Editor (z. B. GIMP oder Paint.NET) zu öffnen und das Auswahlwerkzeug zu benutzen, um die Koordinaten abzulesen.  

*Warum nicht einfach die ganze Seite OCR‑en?* Das Einschränken des Bereichs reduziert Rauschen, beschleunigt die Verarbeitung und verbessert die Genauigkeit für kleine Felder wie Rechnungsnummern erheblich.

---

## Wie man den Text des Bereichs extrahiert (Schritt 4)

Nachdem der Bereich festgelegt ist, lässt du die Engine nur diesen Ausschnitt erkennen. Das Ergebnisobjekt enthält den Rohtext und die Vertrauenswerte.

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

Falls die OCR‑Engine mehrere Sprachen unterstützt, kannst du einen optionalen Sprachcode übergeben:

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*Häufiger Stolperstein:* Manche Engines geben eine Liste von Wörtern statt eines einzelnen Strings zurück. In solchen Fällen musst du sie zusammenfügen:

```python
text = " ".join(region_result.words)
```

---

## Extrahierte Rechnungsnummer ausgeben (Schritt 5)

Zum Schluss gibst du den extrahierten Text aus – oder speicherst ihn. Du kannst den String zudem nachbearbeiten, um überflüssige Leerzeichen oder nicht‑numerische Zeichen zu entfernen.

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

Wenn du das Skript mit einem korrekt ausgerichteten Rechteck ausführst, sollte etwa Folgendes erscheinen:

```
Invoice number: 20231578
```

Falls du nur Kauderwelsch bekommst, prüfe die Rechteckkoordinaten erneut oder erhöhe die Bildauflösung.

---

## Vollständiges funktionierendes Beispiel

Alles zusammengeführt, hier ein eigenständiges Skript, das du kopieren und ausführen kannst:

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

Speichere die Datei als `extract_invoice.py`, ersetze `YOUR_DIRECTORY` durch den tatsächlichen Ordner und führe sie aus:

```bash
python extract_invoice.py
```

Du solltest die Rechnungsnummer in der Konsole sehen.

---

## Häufig gestellte Fragen

**F: Was, wenn die Rechnungsnummer in einer ausgefallenen Schriftart gedruckt ist?**  
A: Die meisten modernen OCR‑Engines unterstützen eine breite Palette von Schriftarten, aber du kannst die Genauigkeit steigern, indem du ein benutzerdefiniertes Sprachmodell trainierst oder das Bild vorverarbeitest (z. B. einen Schwellenwert‑Filter anwenden).

**F: Kann ich mehrere Felder gleichzeitig extrahieren?**  
A: Absolut. Definiere eine Liste von `Rectangle`‑Objekten – eines pro Feld – und iteriere darüber, wobei du jedes Ergebnis in einem Dictionary speicherst.

**F: Funktioniert das bei mehrseitigen PDFs?**  
A: Konvertiere jede Seite zuerst in ein Bild (mit `pdf2image` oder ähnlichem) und wende dann dieselbe bereichsbasierte Extraktion pro Seite an.

---

## Fazit

In diesem Tutorial haben wir behandelt, **wie man OCR** in Python verwendet, um ein Bild zu laden, Text in einem bestimmten Bereich zu erkennen und den Text dieses Bereichs zu extrahieren – ideal, um Rechnungsnummern, Auftrags‑IDs oder andere kleine Datenfragmente aus gescannten Dokumenten zu holen. Durch das Isolieren des Interessensbereichs gewinnst du Geschwindigkeit, Genauigkeit und weniger Nachbearbeitung.

Bereit für den nächsten Schritt? Versuche, das Skript zu erweitern, sodass **Bild für OCR laden** aus einem Ordner mit Stapel‑Rechnungen erfolgt, oder experimentiere mit **Text im Bereich erkennen** für andere Felder wie Datum und Gesamtsumme. Das gleiche Muster gilt – nur die Rechteckkoordinaten ändern.

Falls du auf Probleme gestoßen bist oder Verbesserungsvorschläge hast, hinterlasse unten einen Kommentar. Viel Spaß beim Coden und möge deine OCR‑Pipeline stets präzise sein!

## Was du als Nächstes lernen solltest

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um dir zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in deinen eigenen Projekten zu erkunden.

- [Text aus Bild mit Aspose OCR extrahieren – Schritt‑für‑Schritt‑Anleitung](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Text aus Bild extrahieren, indem Rechtecke in OCR vorbereitet werden](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Wie man AspOCR verwendet: Bild‑OCR‑Filter für .NET vorverarbeiten](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}