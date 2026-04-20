---
category: general
date: 2026-03-18
description: Wie man OCR verwendet, um Text aus Bildern zu extrahieren – ein kurzer
  Leitfaden zum Erkennen von Text aus PNG-Dateien und zum Laden von Bildern für OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- how to extract text
- load image for OCR
language: de
og_description: Wie man OCR verwendet, um Text aus Bildern zu extrahieren – lernen
  Sie, Text aus PNG zu erkennen, ein Bild für OCR zu laden und Text mit einem einfachen
  Python‑Skript zu extrahieren.
og_title: 'Wie man OCR verwendet: Text aus Bildern in Python extrahieren'
tags:
- OCR
- Python
- Image Processing
title: 'Wie man OCR verwendet: Text aus Bildern in Python extrahieren'
url: /de/python-java/general/how-to-use-ocr-extract-text-from-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR verwendet: Text aus Bildern in Python extrahieren

Haben Sie sich jemals gefragt, **wie man OCR verwendet**, wenn Sie einen unordentlichen Screenshot oder einen gescannten Beleg haben? Sie sind nicht allein – Entwickler müssen ständig lesbaren Text aus Bildern extrahieren, insbesondere PNGs, die von mobilen Apps oder Web‑Uploads stammen. In diesem Tutorial führen wir Sie durch ein vollständiges, ausführbares Beispiel, das zeigt, wie Sie **Text aus Bilddateien extrahieren**, **Text aus PNG‑Assets erkennen** und sogar **Bild für OCR laden** mit nur wenigen Zeilen Python.

Wir behandeln alles, von der Installation der richtigen Bibliothek bis zur Verarbeitung mehrsprachiger Dokumente, sodass Sie am Ende genau wissen, *wie man Text extrahiert* aus jedem Bild, das Sie dem Engine zuführen. Keine vagen Verweise, nur eine klare, Schritt‑für‑Schritt‑Lösung, die Sie kopieren‑einfügen und ausführen können.

## Was Sie lernen werden

1. Richten Sie eine leichte OCR‑Engine ein (keine schweren Abhängigkeiten erforderlich).  
2. Laden Sie eine Bilddatei – speziell ein PNG – in die Engine.  
3. Aktivieren Sie die automatische Spracherkennung, damit die Engine mehrsprachige Inhalte verarbeiten kann.  
4. Führen Sie den Erkennungsprozess aus und holen Sie das Klartext‑Ergebnis ab.  
5. Passen Sie den Workflow für Randfälle wie fehlende Dateien oder nicht unterstützte Formate an.

Wenn Sie mit grundlegenden Python-Kenntnissen vertraut sind, sind Sie startklar. Vorherige OCR‑Erfahrung ist nicht nötig, obwohl ein kurzer Blick in die Dokumentation der Bibliothek nie schadet.

---

![Wie man OCR auf ein PNG‑Bild anwendet](placeholder.png "Wie man OCR auf ein PNG‑Bild anwendet – Schritt‑für‑Schritt‑Anleitung")

## Wie man OCR verwendet – Bild laden und Text erkennen {#how-to-use-ocr}

### Schritt 1: OCR‑Bibliothek installieren

Zunächst benötigen Sie ein Python‑Paket, das eine `OcrEngine`‑Klasse bereitstellt. Für dieses Tutorial verwenden wir das fiktive, aber anschauliche **SimpleOCR**‑Paket, das Sie über pip installieren können:

```bash
pip install simple-ocr
```

> **Pro‑Tipp:** Wenn Sie in einer virtuellen Umgebung arbeiten (dringend empfohlen), aktivieren Sie diese, bevor Sie den Installationsbefehl ausführen. So bleiben Ihre Projektabhängigkeiten übersichtlich.

### Schritt 2: Engine importieren und eine Instanz erstellen

Die Engine zu erstellen ist so einfach wie den Konstruktor aufzurufen. Betrachten Sie die Engine als das „Gehirn“, das später das Bild verarbeitet, das Sie ihr übergeben.

```python
# Step 2: Import and instantiate the OCR engine
from simple_ocr import OcrEngine

# Create a fresh engine instance – this allocates internal buffers
engine = OcrEngine()
```

Warum erstellen wir jedes Mal eine neue Instanz? Isolation. Eine frische Engine stellt sicher, dass kein Restzustand eines vorherigen Laufs die aktuelle Erkennung kontaminiert, was besonders wichtig ist, wenn Sie viele Dateien stapelweise verarbeiten.

### Schritt 3: Bild laden, das Sie verarbeiten möchten

Jetzt **laden wir das Bild für OCR**. Die Methode `setImageFromFile` akzeptiert einen Pfad zu einem beliebigen Rasterbild; wir zeigen sie auf ein PNG namens `mixed_doc.png`.

```python
# Step 3: Load the PNG image you want to read
image_path = "YOUR_DIRECTORY/mixed_doc.png"
engine.setImageFromFile(image_path)
```

Wenn die Datei nicht gefunden wird, wirft `SimpleOCR` einen klaren `FileNotFoundError`. Sie können ihn abfangen, um eine benutzerfreundliche Fehlermeldung auszugeben:

```python
try:
    engine.setImageFromFile(image_path)
except FileNotFoundError:
    print(f"❗️ Unable to locate '{image_path}'. Check the path and try again.")
    raise
```

### Schritt 4: Automatische Spracherkennung aktivieren

Die meisten modernen OCR‑Engines werden mit Sprachpaketen geliefert. Durch Übergabe von `"multilingual"` teilen wir der Engine mit, den Text zu analysieren und automatisch das richtige Sprachmodell auszuwählen. Das ist besonders praktisch, wenn Ihr PNG beispielsweise eine Mischung aus Englisch und Spanisch enthält.

```python
# Step 4: Turn on auto‑language detection (covers all installed packs)
engine.setLanguage("multilingual")
```

Wenn Sie die Sprache im Voraus kennen, können Sie `"multilingual"` durch ein spezifisches Locale wie `"eng"` oder `"spa"` ersetzen, um die Verarbeitung zu beschleunigen.

### Schritt 5: Erkennungsprozess ausführen

Hier findet die eigentliche Arbeit statt. `recognize()` scannt das Bild, wendet Segmentierung an, führt das neuronale Netz aus und erstellt intern einen Textpuffer.

```python
# Step 5: Execute OCR – this may take a moment for large images
engine.recognize()
```

Im Hintergrund führt die Engine aus:

- **Vorverarbeitung** (Entzerrung, Binarisierung)  
- **Layout‑Analyse** (Erkennung von Spalten, Tabellen)  
- **Zeichenklassifizierung** (unter Verwendung eines Deep‑Learning‑Modells)  

All das ist abstrahiert, weshalb Sie nur eine Zeile benötigen.

### Schritt 6: Erkannten Text abrufen und ausgeben

Schließlich holen wir das Ergebnisobjekt und extrahieren die reine Zeichenkette. Das ist der Teil, in dem Sie tatsächlich **Text aus Bild extrahieren**.

```python
# Step 6: Get the OCR result and display the plain text
result = engine.getResult()
text = result.getText()
print("📝 Recognized Text:\n")
print(text)
```

**Erwartete Ausgabe** (gekürzt für die Kürze):

```
📝 Recognized Text:

Invoice #12345
Date: 2026‑03‑15
Total: $89.99
Thank you for your purchase!
```

Wenn das Bild keine erkennbaren Zeichen enthält, ist `text` eine leere Zeichenkette. Sie können dem vorbeugen:

```python
if not text.strip():
    print("⚠️ No text detected – try a higher‑resolution image or adjust preprocessing.")
```

---

## Text aus Bild extrahieren – Umgang mit gängigen Randfällen

### Mehrere Sprachen in einer Datei

Wenn ein Dokument mehrere Sprachen mischt, erledigt die Einstellung `"multilingual"` in der Regel das Richtige. Wenn Sie jedoch Fehlinterpretationen bemerken, können Sie manuell eine Ausweichliste angeben:

```python
engine.setLanguage(["eng", "spa", "fra"])  # English, Spanish, French
```

### Nicht‑PNG‑Formate

Obwohl unser Fokus **Text aus PNG erkennen** ist, akzeptiert `SimpleOCR` auch JPEG, BMP und TIFF. Ändern Sie einfach die Dateierweiterung in `setImageFromFile`. Für TIFF‑Stacks müssen Sie möglicherweise eine bestimmte Seite auswählen:

```python
engine.setImageFromFile("scanned.tif", page=0)  # first page only
```

### Große Dateien und Speicherverbrauch

Wenn Sie Gigapixel‑Scans verarbeiten, sollten Sie vor dem OCR eine Größenanpassung in Betracht ziehen:

```python
from PIL import Image

with Image.open(image_path) as img:
    img.thumbnail((2000, 2000))  # keep aspect ratio, max 2000px
    img.save("temp_resized.png")
engine.setImageFromFile("temp_resized.png")
```

Das Ändern der Größe reduziert den Speicherbedarf, während genügend Details für eine genaue Erkennung erhalten bleiben.

### Fehlgeschlagene Ladevorgänge debuggen

Manchmal sieht ein Bild für das Auge in Ordnung aus, ist aber intern beschädigt. Aktivieren Sie ausführliches Logging, um zu sehen, was die Engine erkennt:

```python
engine.enableDebug(True)   # prints internal steps to stdout
engine.recognize()
```

---

## Komplettes, sofort ausführbares Skript

Unten finden Sie das vollständige Programm, das alle Teile zusammenfügt. Kopieren Sie es in eine Datei namens `ocr_demo.py`, passen Sie den Platzhalter `YOUR_DIRECTORY` an und führen Sie `python ocr_demo.py` aus.

```python
# ocr_demo.py
# Full example showing how to use OCR to extract text from a PNG image.
# Requires: pip install simple-ocr pillow

from simple_ocr import OcrEngine
import os
from PIL import Image

def main():
    # 1️⃣ Create the OCR engine
    engine = OcrEngine()

    # 2️⃣ Define the image path – change this to your actual file location
    image_path = os.path.join("YOUR_DIRECTORY", "mixed_doc.png")

    # 3️⃣ Load the image (with a safety net for missing files)
    try:
        engine.setImageFromFile(image_path)
    except FileNotFoundError:
        print(f"❗️ Cannot find image at '{image_path}'. Exiting.")
        return

    # Optional: resize large images to keep memory usage low
    # (uncomment if you deal with huge scans)
    # with Image.open(image_path) as img:
    #     img.thumbnail((2000, 2000))
    #     resized_path = "temp_resized.png"
    #     img.save(resized_path)
    #     engine.setImageFromFile(resized_path)

    # 4️⃣ Enable automatic language detection (covers all installed packs)
    engine.setLanguage("multilingual")

    # 5️⃣ Run the OCR engine
    engine.recognize()

    # 6️⃣ Retrieve and print the recognized text
    result = engine.getResult()
    text = result.getText()

    if text.strip():
        print("\n📝 Recognized Text:\n")
        print(text)
    else:
        print("⚠️ No recognizable text found. Try a clearer image or adjust preprocessing.")

if __name__ == "__main__":
    main()
```

Das Ausführen dieses Skripts sollte die Klartext‑Version dessen ausgeben, was in `mixed_doc.png` enthalten ist. Sie können die Datei gern durch ein anderes Bild ersetzen – **wie man Text extrahiert** funktioniert auf dieselbe Weise.

---

## Fazit

Wir haben gerade **wie man OCR verwendet** in Python durchlaufen, um **Text aus Bilddateien zu extrahieren**, wobei wir uns speziell auf **Text aus PNG‑Assets erkennen** und die praktischen Schritte zum **Bild für OCR laden** konzentriert haben. Das obige Snippet ist eine eigenständige Lösung: Paket installieren, Datei übergeben, mehrsprachige Erkennung aktivieren, Engine ausführen und das Ergebnis holen.

Von hier aus könnten Sie:

- Das Skript in einen Web‑Service integrieren, der Benutzer‑Uploads akzeptiert.  
- Einen Ordner mit PDFs, die in PNGs konvertiert wurden, stapelweise verarbeiten.  
- Nachbearbeitung hinzufügen (z. B. Regex‑Bereinigung, Rechtschreibprüfung), um die Genauigkeit zu verbessern.

Denken Sie daran, die OCR‑Qualität hängt von Bildklarheit, richtigen Sprachpaketen und manchmal ein wenig Vorverarbeitung ab – also experimentieren Sie

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}