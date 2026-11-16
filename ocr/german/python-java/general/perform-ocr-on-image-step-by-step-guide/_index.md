---
category: general
date: 2026-03-18
description: Führen Sie OCR auf einem Bild aus, um Text schnell aus dem Bild zu extrahieren.
  Erfahren Sie, wie Sie ein Bild für OCR laden, eine OCR‑Engine erstellen und die
  OCR‑Genauigkeit mit Sprachoptionen verbessern.
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: de
og_description: Führen Sie OCR auf einem Bild mit dieser ausführlichen Anleitung durch.
  Erfahren Sie, wie Sie ein Bild für OCR laden, eine OCR‑Engine erstellen und die
  OCR‑Genauigkeit verbessern, um zuverlässige Textextraktion zu gewährleisten.
og_title: OCR auf Bild ausführen – Vollständiges Programmier‑Tutorial
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: OCR auf Bild ausführen – Schritt‑für‑Schritt‑Anleitung
url: /de/python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR auf Bild ausführen – Komplettes Programmier‑Tutorial

Haben Sie jemals **OCR auf einem Bild ausführen** müssen, waren sich aber nicht sicher, welche Bibliothek Sie wählen oder wie Sie zuverlässige Ergebnisse erhalten? Sie sind nicht allein. In diesem Leitfaden gehen wir Schritt für Schritt durch alles, was Sie benötigen, um **Text aus Bild zu extrahieren**, vom Laden des Bildes bis zum Anpassen der Sprachoptionen, damit Sie **die OCR‑Genauigkeit verbessern** können.

Wir behandeln, wie man **Bild für OCR lädt**, wie man **OCR‑Engine erstellt** und warum jede Einstellung wichtig ist. Am Ende haben Sie ein sofort einsatzbereites Skript, das den erkannten Text ausgibt, und Sie verstehen das „Warum“ hinter jeder Zeile – ohne vage „siehe die Dokumentation“-Abkürzungen. Lassen Sie uns loslegen.

## Was Sie benötigen

- Python 3.8+ (der Code verwendet f‑Strings und Typ‑Hints)
- Das hypothetische `ocr_lib`‑Paket – Installation mit `pip install ocr_lib`
- Eine Bilddatei mit klarem, gedrucktem Text (z. B. `lab_report.png`)
- Ein einfacher Texteditor oder eine IDE (VS Code, PyCharm, oder was Sie mögen)

Wenn Sie das bereits haben, großartig – Sie sind startklar. Wenn nicht, holen Sie sich Python von python.org und führen Sie den Pip‑Befehl aus; das dauert nur eine Minute.

![perform OCR on image example](/images/ocr-example.png)

*Alt‑Text: OCR auf Bild ausführen – Beispielausgabe, die extrahierten Text zeigt.*

## Schritt 1: OCR‑Engine erstellen – Wie man **OCR‑Engine erstellen** in Python

Bevor irgendeine Erkennung stattfinden kann, benötigt die Bibliothek ein Engine‑Objekt, das Konfiguration und Laufzeit‑Zustand hält. Denken Sie an die Engine als das Gehirn hinter der Operation.

```python
# step_1_create_engine.py
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    """
    Initialize and return a fresh OcrEngine instance.
    Creating the engine once and reusing it is more efficient than
    instantiating it inside a loop.
    """
    engine = OcrEngine()
    return engine
```

**Warum das wichtig ist:** Das frühe Instanziieren der Engine ermöglicht es Ihnen, später Sprachoptionen anzuhängen, und es cached interne Modelle für schnellere nachfolgende Aufrufe.

## Schritt 2: Bild für OCR laden – Der korrekte Weg, um **Bild für OCR zu laden**

Jetzt, wo wir eine Engine haben, müssen wir ihr etwas zum Lesen geben. Die Methode `setImageFromFile` akzeptiert einen Dateisystem‑Pfad; der Pfad kann absolut oder relativ zum Arbeitsverzeichnis des Skripts sein.

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**Pro‑Tipp:** Verwenden Sie einen absoluten Pfad oder `os.path.join`, um “Datei nicht gefunden”-Überraschungen zu vermeiden, wenn das Skript aus einem anderen Ordner ausgeführt wird.

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## Schritt 3: OCR‑Genauigkeit verbessern – Anpassen von **language options** um **die OCR‑Genauigkeit verbessern**

Out‑of‑the‑box OCR funktioniert, aber domänenspezifische Vokabulare (wie Labor‑Jargon) bringen es häufig zum Stolpern. Durch das Einspeisen eines benutzerdefinierten Wörterbuchs und einer Blacklist reduzieren Sie Fehlinterpretationen, etwa das Verwechseln von „0“ mit „O“.

```python
# step_3_language_options.py
def configure_language(engine: OcrEngine) -> None:
    """
    Set up language options to help the engine recognize domain‑specific terms
    and ignore characters that are frequently misread.
    """
    language_opts = LanguageOptions()
    # Add terms that appear often in laboratory reports
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    # Blacklist characters that cause confusion
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)
```

**Warum das hilft:** Das Wörterbuch teilt dem OCR‑Modell mit, dass „HPLC“ ein gültiges Token ist, wodurch verhindert wird, dass das Wort in Unsinn zerlegt wird. Die Blacklist weist das Modell an, mehrdeutige Symbole als Rauschen zu behandeln, was die **OCR‑Genauigkeit verbessert**.

## Schritt 4: OCR auf Bild ausführen – Der Kernaufruf **OCR auf Bild ausführen**

Mit der vorbereiteten Engine und dem angehängten Bild ist es Zeit, den Text tatsächlich zu erkennen. Dieser Schritt gibt ein `OcrResult`‑Objekt zurück, das Sie nach Rohtext, Konfidenz‑Scores oder Begrenzungsrahmen abfragen können.

```python
# step_4_recognize.py
def recognize_text(engine: OcrEngine) -> OcrResult:
    """
    Run the OCR process. This may take a few seconds depending on image size.
    Returns an OcrResult that contains the extracted string and metadata.
    """
    result = engine.recognize()
    return result
```

Wenn das Bild unscharf ist, sehen Sie niedrigere Konfidenz‑Zahlen im Ergebnis. Das ist ein Hinweis, das Bild vorzuverarbeiten (z. B. Kontrast erhöhen), bevor Sie es an die Engine übergeben.

## Schritt 5: Text aus Bild extrahieren – Die endgültige Zeichenkette holen

Schließlich fragen wir das `OcrResult` nach seiner textuellen Darstellung. Die Methode `getText()` liefert einen Klartext‑String, der bereit für nachgelagerte Verarbeitung ist (Speichern in einer Datei, Einspeisen in eine Datenbank usw.).

```python
# step_5_output.py
def print_result(result: OcrResult) -> None:
    """
    Output the recognized text to the console.
    You could also write it to a file with open('output.txt', 'w') …
    """
    extracted = result.getText()
    print("=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===")
```

**Erwartete Ausgabe:** Angenommen, `lab_report.png` enthält eine einfache Tabelle, dann könnte das Ergebnis etwa so aussehen:

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

Damit ist der Teil **Text aus Bild extrahieren** abgeschlossen.

## Vollständiges funktionierendes Beispiel – Alles zusammenführen

Unten finden Sie ein einzelnes Skript, das die Bausteine aus den vorherigen Abschnitten zusammensetzt. Sie können es in `run_ocr.py` kopieren und mit `python run_ocr.py` ausführen.

```python
# run_ocr.py
import os
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    engine = OcrEngine()
    return engine

def load_image(engine: OcrEngine, image_path: str) -> None:
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")
    engine.setImageFromFile(image_path)

def configure_language(engine: OcrEngine) -> None:
    language_opts = LanguageOptions()
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)

def recognize_text(engine: OcrEngine) -> OcrResult:
    return engine.recognize()

def print_result(result: OcrResult) -> None:
    extracted = result.getText()
    print("\n=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===\n")

def main() -> None:
    # 1️⃣ Create the OCR engine
    ocr_engine = build_engine()

    # 2️⃣ Load the image you want to process
    image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
    load_image(ocr_engine, image_file)

    # 3️⃣ Apply language tweaks to **improve OCR accuracy**
    configure_language(ocr_engine)

    # 4️⃣ **Perform OCR on image** – this is the heavy lifting
    ocr_result = recognize_text(ocr_engine)

    # 5️⃣ **Extract text from image** and show it
    print_result(ocr_result)

if __name__ == "__main__":
    main()
```

### Schnelle Prüfliste

| ✅ | Element |
|---|------|
| ✔️ | Engine ist erstellt (`create OCR engine`) |
| ✔️ | Bild ist geladen (`load image for OCR`) |
| ✔️ | Sprachoptionen sind gesetzt (`improve OCR accuracy`) |
| ✔️ | OCR wird ausgeführt (`perform OCR on image`) |
| ✔️ | Text wird extrahiert (`extract text from image`) |

Führen Sie das Skript aus und beobachten Sie die Konsole. Wenn Sie den Block „OCR Output“ mit dem Inhalt Ihres Berichts sehen, haben Sie erfolgreich **OCR auf Bild ausgeführt**.

## Häufige Fallstricke & wie man sie vermeidet

| Problem | Warum es passiert | Lösung |
|-------|----------------|-----|
| **Blurry input** | Das OCR‑Modell kann Zeichen nicht unterscheiden | Vorverarbeitung mit OpenCV: `cv2.GaussianBlur` oder DPI erhöhen |
| **Wrong language** | Die Standardsprache ist möglicherweise nicht Englisch | `engine.setLanguage("eng")` vor `recognize()` aufrufen |
| **Missing dictionary terms** | Domänenspezifische Wörter werden verzerrt | Sie über `setDictionary` hinzufügen, wie in Schritt 3 gezeigt |
| **Blacklisted characters cause** |  |  |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}