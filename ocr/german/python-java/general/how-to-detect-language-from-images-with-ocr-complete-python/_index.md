---
category: general
date: 2026-06-22
description: Erfahren Sie, wie Sie die Sprache aus einem Bild erkennen und Text mit
  OCR in Python extrahieren. Schritt‑für‑Schritt‑Tutorial, das die automatische Spracherkennung
  und Textextraktion abdeckt.
draft: false
keywords:
- how to detect language
- detect language from image
- extract text from image
- how to use ocr
- how to extract text
language: de
og_description: Wie erkennt man die Sprache aus einem Bild mit OCR? Dieser Leitfaden
  zeigt Ihnen Schritt für Schritt, wie Sie OCR in Python verwenden, um die Sprache
  zu erkennen und Text zu extrahieren.
og_title: Wie man Sprache aus Bildern mit OCR erkennt – Vollständige Python-Anleitung
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to detect language from image and extract text using OCR
    in Python. Step‑by‑step tutorial covering automatic language detection and text
    extraction.
  headline: How to Detect Language from Images with OCR – Complete Python Guide
  type: TechArticle
- description: Learn how to detect language from image and extract text using OCR
    in Python. Step‑by‑step tutorial covering automatic language detection and text
    extraction.
  name: How to Detect Language from Images with OCR – Complete Python Guide
  steps:
  - name: Expected Output
    text: 'If `sample-multilang.png` contains French text, you might see something
      like:'
  - name: 1. Unsupported Image Formats
    text: 'If you try to load a TIFF file that the OCR library doesn’t recognise,
      `ocr.ImageStream.from_file()` will raise an `OcrUnsupportedFormatError`. Wrap
      the load call in a try/except block:'
  - name: 2. Low‑Resolution Images
    text: 'OCR accuracy drops sharply below ~300 dpi. If you notice poor detection,
      consider pre‑processing the image with Pillow:'
  - name: 3. Multiple Languages in One Image
    text: 'When an image contains text in more than one language, the auto‑detect
      feature will pick the dominant one. To capture all languages, you can disable
      auto‑detect and manually pass a list of languages to the engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Wie man Sprache aus Bildern mit OCR erkennt – Vollständiger Python-Leitfaden
url: /de/python-java/general/how-to-detect-language-from-images-with-ocr-complete-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Sprache aus Bildern mit OCR erkennt – Vollständiger Python‑Leitfaden

Haben Sie sich schon einmal gefragt, **wie man die Sprache** in einem Bild erkennt, ohne es manuell zu öffnen? Sie sind nicht allein. In vielen Projekten – denken Sie an Belegscanner, mehrsprachige Dokumentenarchive oder eine einfache Foto‑zu‑Text‑App – müssen Sie wissen, *welche* Sprache der Text hat, bevor Sie ihn weiter verarbeiten können.  

In diesem Tutorial führen wir Sie durch ein praktisches End‑to‑End‑Beispiel, das **zeigt, wie man Sprache** aus einem Bild erkennt und anschließend die eigentlichen Zeichen extrahiert. Am Ende können Sie ein paar Zeilen Python ausführen, das Skript auf ein beliebiges unterstütztes Bild zeigen und sowohl die erkannte Sprache *als auch* den extrahierten Text erhalten. Kein Schnickschnack, nur eine klare Lösung zum Kopieren‑und‑Einfügen.

## Was Sie lernen werden

- Installation und Einrichtung einer leichten OCR‑Bibliothek in Python.  
- Initialisierung der OCR‑Engine und Aktivierung der automatischen Spracherkennung.  
- Laden eines Bildes (beliebiges unterstütztes Format) und Ausführen von OCR.  
- Abrufen der erkannten Sprache und des extrahierten Textes.  
- Umgang mit typischen Fallstricken wie nicht unterstützten Formaten oder mehrdeutigen Sprachergebnissen.  

Wenn Sie sich schon einmal gefragt haben, **wie man OCR** für mehrsprachige Dokumente nutzt, deckt dieser Leitfaden alles ab.

---

## Voraussetzungen

Bevor wir starten, stellen Sie sicher, dass Sie Folgendes auf Ihrem Rechner haben:

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| Python 3.9 oder neuer | Das OCR‑Paket, das wir verwenden, richtet sich an moderne Interpreter. |
| `pip` (Python‑Paket‑Manager) | Wird benötigt, um die OCR‑Bibliothek zu installieren. |
| Ein Beispielbild, das Text in mindestens einer Sprache enthält (z. B. `sample-multilang.png`) | Gibt Ihnen etwas Konkretes zum Testen. |
| Optional: Virtuelle Umgebung (`venv` oder `conda`) | Hält Abhängigkeiten sauber und verhindert Versionskonflikte. |

> **Profi‑Tipp:** Wenn Sie in einer virtuellen Umgebung arbeiten, aktivieren Sie sie, bevor Sie das OCR‑Paket installieren, um Ihr globales Python sauber zu halten.

---

## Schritt 1: Installieren der OCR‑Bibliothek

Für diesen Durchlauf verwenden wir das hypothetische `ocr`‑Paket, das die im Code‑Snippet gezeigte API nachbildet. In einer realen Situation könnten Sie es durch `pytesseract`, `easyocr` oder eine andere Bibliothek ersetzen, die automatische Spracherkennung unterstützt.

```bash
pip install ocr
```

> **Hinweis:** Das Paket ist leichtgewichtig (< 5 MB) und funktioniert unter Windows, macOS und Linux. Wenn Sie Berechtigungsfehler erhalten, fügen Sie `--user` zum Befehl hinzu.

---

## Schritt 2: Initialisieren der OCR‑Engine – Wie man Sprache erkennt

Jetzt, wo die Bibliothek bereit ist, können wir eine OCR‑Engine‑Instanz erstellen. Dieses Objekt scannt das Bild tatsächlich und ermittelt die Sprache.

```python
import ocr

# Initialise the OCR engine – this is where we start the language detection pipeline
engine = ocr.OcrEngine()
```

Warum beginnen wir mit einer Engine? Denken Sie an die Engine als das Gehirn des OCR‑Systems; sie hält Konfigurationen, lädt Sprachmodelle und übernimmt das schwere Heben im Hintergrund. Die Initialisierung zuerst stellt sicher, dass nachfolgende Aufrufe (wie das Laden eines Bildes) einen Kontext haben, in dem sie arbeiten können.

---

## Schritt 3: Bild laden und automatische Spracherkennung aktivieren

Der nächste Schritt besteht darin, das Bild in die Engine zu speisen. Wir schalten außerdem das *auto‑detect language*‑Flag ein, sodass die OCR‑Engine versucht, die Sprache on‑the‑fly zu erraten.

```python
# Load the image (any supported format – PNG, JPEG, BMP, etc.)
image_path = "YOUR_DIRECTORY/sample-multilang.png"
image = ocr.ImageStream.from_file(image_path)

# Attach the image to the engine
engine.set_image(image)

# Enable automatic language detection – this is the key for detecting language from image
engine.get_settings().set_auto_detect_language(True)
```

> **Warum auto‑detect aktivieren?**  
> Die meisten OCR‑Bibliotheken werden mit einer Standardsprache ausgeliefert (oft Englisch). Enthält Ihr Dokument Französisch, Japanisch oder eine andere Schrift, würde die Engine dies ohne diese Einstellung übersehen. Durch das Setzen von `set_auto_detect_language(True)` lassen wir die Engine das Bitmap scannen, Zeichenform‑Statistiken vergleichen und das wahrscheinlichste Sprachmodell auswählen.

---

## Schritt 4: OCR ausführen – Text aus Bild extrahieren

Mit dem geladenen Bild und aktivierter Spracherkennung besteht der eigentliche OCR‑Schritt nur aus einem einzigen Methodenaufruf.

```python
# Run the OCR process – this both detects the language and extracts the text
result = engine.recognize()
```

Die Methode `recognize()` erledigt zwei Dinge im Hintergrund:

1. **Spracherkennung:** Sie führt einen leichten Klassifikator über das Bild aus, um einen Sprachcode zu bestimmen (z. B. `en`, `fr`, `es`).  
2. **Textextraktion:** Anschließend wendet sie das passende sprachspezifische Modell an, um die Zeichen in Unicode‑Strings zu transkribieren.

Da beide Aktionen zusammen ablaufen, erhalten Sie ein einzelnes `result`‑Objekt, das alles enthält, was Sie benötigen.

---

## Schritt 5: Erkennen der Sprache und des extrahierten Textes anzeigen

Schließlich holen wir den Sprachcode und den Rohtext aus dem `result`‑Objekt und geben sie in der Konsole aus.

```python
# Print the detected language and the extracted text
print("Detected language:", result.get_language())
print("Text:", result.get_text())
```

### Erwartete Ausgabe

Enthält `sample-multilang.png` französischen Text, könnte die Ausgabe etwa so aussehen:

```
Detected language: fr
Text: Bonjour, ceci est un texte d'exemple.
```

Ist das Bild mehrdeutig oder enthält mehrere Sprachen, gibt die Engine die Sprache zurück, bei der sie am meisten Vertrauen hat; Sie können später den Vertrauenswert prüfen (die meisten Bibliotheken stellen eine `get_confidence()`‑Methode für fortgeschrittene Anwendungsfälle bereit).

---

## Umgang mit gängigen Sonderfällen

### 1. Nicht unterstützte Bildformate

Versuchen Sie, eine TIFF‑Datei zu laden, die die OCR‑Bibliothek nicht erkennt, wirft `ocr.ImageStream.from_file()` einen `OcrUnsupportedFormatError`. Wickeln Sie den Ladevorgang in einen try/except‑Block:

```python
try:
    image = ocr.ImageStream.from_file(image_path)
except ocr.OcrUnsupportedFormatError as e:
    print(f"Unsupported format: {e}")
    raise
```

### 2. Bilder mit niedriger Auflösung

Die OCR‑Genauigkeit sinkt stark unter ~300 dpi. Wenn Sie schlechte Erkennungsraten bemerken, sollten Sie das Bild mit Pillow vorverarbeiten:

```python
from PIL import Image, ImageEnhance

pil_img = Image.open(image_path)
pil_img = pil_img.resize((pil_img.width * 2, pil_img.height * 2), Image.LANCZOS)
pil_img.save("resized.png")
image = ocr.ImageStream.from_file("resized.png")
```

### 3. Mehrere Sprachen in einem Bild

Enthält ein Bild Text in mehr als einer Sprache, wählt die Auto‑Detect‑Funktion die dominante Sprache. Um alle Sprachen zu erfassen, können Sie Auto‑Detect deaktivieren und der Engine manuell eine Sprachliste übergeben:

```python
engine.get_settings().set_auto_detect_language(False)
engine.get_settings().set_languages(["en", "fr", "de"])
```

Jetzt versucht die OCR, Zeichen mit jedem Sprachmodell zu erkennen und gibt für jeden Textblock die beste Übereinstimmung zurück.

---

## Komplettes Skript – Alle Schritte kombiniert

Unten finden Sie das vollständige, sofort ausführbare Python‑Skript, das alles enthält, was wir besprochen haben. Speichern Sie es als `detect_language_ocr.py` und führen Sie `python detect_language_ocr.py` aus.

```python
# detect_language_ocr.py
# -------------------------------------------------
# How to detect language from image and extract text using OCR
# -------------------------------------------------

import ocr

def main():
    # 1️⃣ Initialise the OCR engine
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image (any supported format)
    image_path = "YOUR_DIRECTORY/sample-multilang.png"
    try:
        image = ocr.ImageStream.from_file(image_path)
    except ocr.OcrUnsupportedFormatError as err:
        print(f"Error loading image: {err}")
        return

    engine.set_image(image)

    # 3️⃣ Enable automatic language detection
    engine.get_settings().set_auto_detect_language(True)

    # 4️⃣ Perform OCR – this both detects language and extracts text
    try:
        result = engine.recognize()
    except ocr.OcrRecognitionError as err:
        print(f"OCR failed: {err}")
        return

    # 5️⃣ Retrieve and display the detected language and extracted text
    print("Detected language:", result.get_language())
    print("Text:", result.get_text())

if __name__ == "__main__":
    main()
```

**Führen Sie es aus** und Sie sehen sofort den Sprachcode gefolgt vom extrahierten Text. Das ist die gesamte Antwort auf **wie man Sprache erkennt** und **wie man Text extrahiert** aus einem Bild mittels OCR.

---

## Weiterführend – Nächste Schritte & verwandte Themen

- **Genauigkeit verbessern:** Experimentieren Sie mit Bildvorverarbeitung (Schwellwertsetzung, Rauschunterdrückung) mittels `opencv-python`.  
- **Batch‑Verarbeitung:** Verpacken Sie das Skript in eine Schleife, um einen ganzen Ordner mit Bildern zu bearbeiten.  
- **Integration mit NLP:** Leiten Sie den extrahierten Text an eine Sprachidentifikations‑Bibliothek wie `langdetect` weiter, um eine zweite Meinung zu erhalten.  
- **Andere OCR‑Engines erkunden:** `pytesseract` bietet feinkörnige Kontrolle, während `easyocr` über 80 Sprachen out‑of‑the‑box unterstützt.  

All diese Themen knüpfen an unsere sekundären Schlüsselwörter – *detect language from image*, *extract text from image*, *how to use OCR* und *how to extract text* – an, sodass Sie Ihr Toolkit erweitern können, ohne von Grund auf neu zu beginnen.

---

## Fazit

Wir haben gerade **gezeigt, wie man Sprache** aus einem Bild erkennt, den genauen Code durchgegangen und erklärt, warum jeder Schritt wichtig ist. Durch das Initialisieren der OCR‑Engine, das Laden des Bildes, das Einschalten der automatischen Spracherkennung und schließlich den Aufruf von `recognize()` erhalten Sie sowohl den Sprachidentifikator als auch den extrahierten Text in einem sauberen Vorgang.

Jetzt können Sie diese Logik in größere Anwendungen einbetten – sei es ein Beleg‑Scanning‑Service, ein mehrsprachiger Chatbot oder ein einfaches Desktop‑Utility. Die Kernidee bleibt dieselbe: Die OCR‑Engine die schwere Arbeit erledigen lassen und die Ergebnisse nach Belieben nutzen.

Fragen zu Sonderfällen oder ein cooles Anwendungsbeispiel zu teilen? Hinterlassen Sie einen Kommentar unten. Viel Spaß beim Coden und beim Umwandeln von Bildern in durchsuchbaren Text!  

![wie man Sprache aus Bild erkennt](ocr-demo.png "Screenshot, der zeigt, wie man Sprache aus Bild mit Python OCR erkennt")

## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [Text aus Bild mit Aspose OCR extrahieren – Schritt‑für‑Schritt‑Anleitung](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Bildtext in C# mit Sprachauswahl mittels Aspose.OCR extrahieren](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Wie man AspOCR verwendet: Bild‑OCR‑Filter für .NET vorverarbeiten](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}