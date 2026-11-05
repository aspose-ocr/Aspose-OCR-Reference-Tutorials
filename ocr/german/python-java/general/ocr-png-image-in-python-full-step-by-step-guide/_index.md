---
category: general
date: 2026-06-06
description: OCR PNG‑Bild mit Python – lernen Sie, wie man Text aus einem Bild extrahiert,
  ein Python‑OCR‑Beispiel ausführt und sogar antiken griechischen Text leicht liest.
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: de
og_description: OCR-PNG-Bild in Python erklärt. Dieser Leitfaden zeigt, wie man Text
  aus einem Bild extrahiert, ein Python-OCR-Beispiel ausführt und antikes Griechisch
  mühelos liest.
og_title: OCR PNG‑Bild in Python – Vollständiges Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR‑PNG‑Bild in Python – Vollständige Schritt‑für‑Schritt‑Anleitung
url: /de/python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR PNG Bild in Python – Vollständige Schritt‑für‑Schritt-Anleitung

Haben Sie sich jemals gefragt, wie man **OCR PNG image** Dateien direkt aus einem Python‑Skript heraus verarbeitet? Vielleicht haben Sie einen Ordner voller gescannter antiker Manuskripte und müssen **extract text from image** Dateien extrahieren, ohne alles von Hand abzutippen. Die gute Nachricht: Sie benötigen keinen Doktortitel in Computer Vision – nur ein paar Zeilen Code und die richtige Bibliothek, und Sie können antikes Griechisch in Sekunden lesen.

In diesem Tutorial gehen wir ein **python OCR example** durch, das Text aus einer PNG erkennt, die Sprache auf Griechisch polytonisch setzt und das Ergebnis ausgibt. Am Ende wissen Sie genau, wie man **recognize image text** durchführt, gängige Fallstricke behandelt und das Skript für andere Sprachen oder Bildformate anpasst.

## Was Sie lernen werden

- Installieren und konfigurieren Sie eine Python OCR‑Bibliothek (pytesseract + Tesseract OCR)
- Erstellen Sie eine OCR‑Engine‑Instanz und laden Sie eine PNG‑Datei
- Setzen Sie die Erkennungssprache auf Griechisch polytonisch, damit Sie **read ancient greek** können
- Geben Sie den erkannten Text aus und beheben Sie typische Probleme
- Erweitern Sie das Skript, um mehrere PNGs stapelweise zu verarbeiten oder zu einer anderen Sprache zu wechseln

### Voraussetzungen

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| Python 3.8+ | Moderne Syntax und Typ‑Hinweise |
| `pytesseract`‑Paket | Dünner Wrapper um die Tesseract‑Engine |
| Tesseract OCR‑Binärdateien (≥ 5.0) | Die eigentliche Engine, die die schwere Arbeit leistet |
| Griechische Sprachdaten (`grc.traineddata`) | Benötigt, um **read ancient greek** korrekt zu lesen |
| Ein PNG‑Bild, das Sie analysieren möchten (z. B. `ancient_greek.png`) | Unser Ziel für die **ocr png image** Demo |

Sie können die Python‑Seite installieren mit:

```bash
pip install pytesseract Pillow
```

Und unter Ubuntu/macOS würden Sie die Engine selbst hinzufügen:

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

Vergessen Sie nicht, die griechischen polytonischen Trainingsdaten herunterzuladen:

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

*(Der Pfad kann abweichen; passen Sie `TESSDATA_PREFIX` bei Bedarf an.)*

## OCR PNG Bild: Engine‑Instanz erstellen

Das erste, was wir benötigen, ist ein Objekt, das mit Tesseract kommuniziert. In `pytesseract` wird die Engine über Funktionen auf Modulebene angesprochen, aber zur Klarheit verpacken wir sie in einer kleinen Klasse. Das spiegelt das „engine“-Konzept wider, das Sie im ursprünglichen Snippet gesehen haben.

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**Warum ein Wrapper?**  
- Behält die öffentliche API identisch zum Ausgangssnippet bei, wodurch die Migration problemlos verläuft.  
- Ermöglicht es uns, später Logging oder Fehlerbehandlung hinzuzufügen, ohne den Hauptablauf zu berühren.  
- Demonstriert gute OOP‑Praxis – etwas, das erfahrene Entwickler zu schätzen wissen.

## Text aus Bild extrahieren: Sprache auf Griechisch polytonisch setzen

Jetzt, da wir eine Engine haben, müssen wir ihr mitteilen, welche Sprache erwartet wird. Griechisch polytonisch verwendet Diakritika, die in den Standard‑„greek“-Daten nicht enthalten sind, daher verweisen wir Tesseract auf die `grc`‑Trainingsdatei.

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

Wenn Sie jemals **extract text from image** Dateien in einer anderen Sprache extrahieren möchten, ersetzen Sie einfach `"grc"` durch `"eng"` für Englisch, `"fra"` für Französisch usw. Die gleiche Zeile funktioniert für jede installierte Sprache.

## Bildtext erkennen: OCR auf einer PNG ausführen

Mit der eingestellten Sprache übergeben wir die PNG an die Engine. Das ursprüngliche Beispiel verwendete einen fest codierten Pfad; wir machen es etwas flexibler, indem wir `Path`‑Objekte verwenden.

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**Tipps & Sonderfälle**

- **File not found** – wickeln Sie den Aufruf in ein `try/except FileNotFoundError`, um eine freundliche Meldung auszugeben.
- **Low‑resolution PNG** – erwägen Sie eine Vorverarbeitung (z. B. Skalierung, Binarisierung) mit Pillow vor dem OCR.
- **Non‑Greek text** – Tesseract wird weiterhin versuchen zu dekodieren, aber die Genauigkeit sinkt stark. Stimmen Sie immer die Sprache ab.

## Erkannten Text ausgeben

Schließlich geben wir das Ergebnis aus. In einem echten Projekt könnten Sie es in eine Datenbank, eine CSV‑Datei schreiben oder sogar in eine Übersetzungspipeline einspeisen.

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

Wenn Sie das Skript gegen einen klaren Scan einer antiken griechischen Inschrift ausführen, sollten Sie etwas Ähnliches sehen:

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

Wenn die Ausgabe unleserlich aussieht, überprüfen Sie, ob die **greek.traineddata**‑Datei im richtigen Ordner liegt und das PNG nicht zu verrauscht ist.

## Vollständiges funktionierendes Beispiel (Alle Schritte in einem Skript)

Unten finden Sie das vollständige, sofort ausführbare Programm. Speichern Sie es als `ocr_greek.py` und führen Sie `python ocr_greek.py` aus.

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**Erwartete Ausgabe** (gekürzt für die Kürze):

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

Wenn Sie die korrekten griechischen Zeichen sehen, herzlichen Glückwunsch – Sie haben erfolgreich eine **ocr png image**‑Operation in Python durchgeführt!

## Häufige Fragen & Profi‑Tipps

### Wie verbessere ich die Genauigkeit bei einem verrauschten PNG?

- Konvertieren Sie das Bild in Graustufen: `img = img.convert('L')`
- Wenden Sie einen binären Schwellenwert an: `img = img.point(lambda x: 0 if x < 128 else 255, '1')`
- Skalieren Sie hoch mit `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`

Diese Schritte verwandeln oft ein **recognize image text**‑Alptraum in ein sauberes Ergebnis.

### Kann ich einen ganzen Ordner von PNGs verarbeiten?

Absolut. Verpacken Sie den Aufruf von `recognize_image` in eine `for`‑Schleife über `Path.glob("*.png")`. Speichern Sie jedes Ergebnis in einem Wörterbuch oder schreiben Sie es in eine CSV für spätere Analysen.

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### Was, wenn ich nur Zahlen extrahieren muss?

Geben Sie einen benutzerdefinierten **config**‑String an `image_to_string` weiter:

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

Auf diese Weise können Sie **extract text from image** Dateien extrahieren, die Tabellen, Seriennummern oder Zeitstempel enthalten.

### Gibt es eine Möglichkeit, Vertrauenswerte zu erhalten?

Ja – verwenden Sie `pytesseract.image_to_data`, das ein TSV mit dem Vertrauenswert pro Wort zurückgibt. Sie können Tokens mit niedrigem Vertrauenswert herausfiltern, bevor Sie den endgültigen String zusammenstellen.

## Das Tutorial erweitern

Jetzt, da Sie die Grundlagen beherrscht haben, sollten Sie diese verwandten Themen erkunden:

- **Batch OCR with multiprocessing** – beschleunigt große Korpora von PNGs.
- **Hybrid OCR + NLP pipelines** – übersetzt automatisch das extrahierte antike Griechisch in modernes Englisch.
- **Alternative engines** – probieren Sie `easyocr` oder `opencv`‑basierte Methoden für spezifische Anwendungsfälle.
- **Cloud OCR services** – Google Vision, Azure Computer Vision oder AWS Textract für serverloses Skalieren.

Jedes dieser Themen baut auf dem Kern‑**python ocr example** auf, das wir gerade behandelt haben, sodass Sie sich beim tieferen Eintauchen wohlfühlen.

## Fazit

Wir haben ein einfaches Snippet genommen und in einen robusten **ocr png image**‑Workflow in Python verwandelt. Durch das Erstellen einer `OcrEngine`, das Setzen der Sprache auf Griechisch polytonisch, das Einspeisen einer PNG und das Ausgeben des Ergebnisses wissen Sie jetzt, wie man **extract text from image** Dateien, **recognize image text** und sogar **read ancient greek** verarbeitet.

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Text aus Bild mit Aspose OCR extrahieren – Schritt‑für‑Schritt‑Anleitung](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Wie man den Schwellenwert in OCR‑Bilderkennung einstellt](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Textbild mit Aspose OCR für mehrere Sprachen erkennen](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}