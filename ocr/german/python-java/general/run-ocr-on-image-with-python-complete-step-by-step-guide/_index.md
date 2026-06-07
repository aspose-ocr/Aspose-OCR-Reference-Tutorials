---
category: general
date: 2026-06-06
description: Führen Sie OCR auf einem Bild mit Python aus und sehen Sie sich die Vertrauenswerte
  an. Lernen Sie, wie Sie Wörter mit geringem Vertrauen filtern, Schwellenwerte festlegen
  und Sonderfälle behandeln.
draft: false
keywords:
- run OCR on image
- Python OCR tutorial
- OCR confidence threshold
- low‑confidence word detection
- image text extraction
language: de
og_description: Führen Sie OCR auf einem Bild in Python aus, prüfen Sie die Vertrauenswerte
  und filtern Sie Wörter mit niedriger Sicherheit. Dieses Tutorial führt Sie durch
  ein vollständiges, ausführbares Beispiel.
og_title: OCR auf Bild mit Python ausführen – Vollständige Anleitung
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  headline: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  name: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: Install and Import the OCR Engine
    text: First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box
      for many languages and gives you a confidence score per word.
  - name: Run OCR on the Image
    text: Now we actually **run OCR on image**. The `recognize_image` method from
      the original example is replaced with EasyOCR’s `readtext` call, which returns
      a list of `(bbox, text, confidence)` tuples.
  - name: Summarize Overall Confidence
    text: 'Unlike the earlier snippet that printed a single `confidence` attribute,
      EasyOCR gives a confidence per word. To get an overall sense, we’ll average
      them:'
  - name: List Low‑Confidence Words
    text: Now comes the part that directly answers the “list words whose confidence
      is below the desired threshold” requirement. We’ll set a **OCR confidence threshold**
      of 0.80 (80 %) by default, but you can adjust it.
  - name: Edge Cases & Variations
    text: 1. **Batch Processing** – If you need to **run OCR on image** files in bulk,
      wrap the above logic in a loop that iterates over a directory. 2. **Multiple
      Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine
      will detect both. 3. **Alternative Engines** – Want to try **pyte
  type: HowTo
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`)
      and then feed the PNG/JPEG into the script.
    question: Does this work with PDFs?
  - answer: 'Try image preprocessing: increase contrast, remove background noise,
      or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths`
      parameter you can tweak.'
    question: My confidence numbers are all low—what can I do?
  - answer: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter`
      where each row contains `text`, `confidence`, and bounding‑box coordinates.
    question: Can I export the results to CSV?
  - answer: 'EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed.
      Verify with `torch.cuda.is_available()` before running the script. --- ## Conclusion
      We’ve just **run OCR on image** using Python, inspected the overall confidence,
      and isolated any low‑confidence words that need a {{< /b'
    question: Is there a GPU‑accelerated version?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: OCR auf Bild mit Python ausführen – Vollständige Schritt‑für‑Schritt‑Anleitung
url: /de/python-java/general/run-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR auf Bildern mit Python ausführen – Vollständige Schritt‑für‑Schritt‑Anleitung

Haben Sie schon einmal **OCR auf Bild**‑Dateien ausführen müssen, waren sich aber nicht sicher, wie Sie zuverlässigen Text daraus erhalten? Sie sind nicht allein – vielen Entwicklern geht es genauso, wenn die extrahierten Wörter wackelig aussehen und der Vertrauenswert ein Rätsel bleibt.  

In diesem Leitfaden gehen wir direkt zu einer funktionierenden Lösung: Sie sehen, wie man OCR auf Bild ausführt, das Gesamtergebnis‑Vertrauen ausliest und Wörter mit geringem Vertrauen herausfiltert, die einer manuellen Überprüfung bedürfen. Am Ende haben Sie ein wiederverwendbares Skript, verstehen, warum jede Zeile wichtig ist, und wissen, wie Sie den Vertrauens‑Schwellenwert für Ihre eigenen Projekte anpassen können.

## Was dieses Tutorial behandelt

Wir gehen den gesamten Workflow durch – vom Laden eines Bildes bis zum Ausgeben eines übersichtlichen Berichts über Wörter, die unter einer Vertrauensmarke von 80 % liegen. Dabei besprechen wir:

* Auswahl einer soliden OCR‑Engine (wir verwenden **EasyOCR**, eine beliebte Python‑OCR‑Bibliothek)  
* Interpretation des `confidence`‑Attributs, das jedes OCR‑Ergebnis zurückgibt  
* Filtern von Wörtern mit einem benutzerdefinierten **OCR‑Vertrauens‑Schwellenwert**  
* Erweiterung des Skripts für Batch‑Verarbeitung oder alternative Engines wie **pytesseract**  

Vorkenntnisse in OCR sind nicht nötig, nur Grundkenntnisse in Python und eine funktionierende Umgebung (Python 3.9+ empfohlen).  

Bereit, verschwommene Screenshots in sauberen, durchsuchbaren Text zu verwandeln? Dann legen wir los.

---

## ## Wie man OCR auf Bild mit Python ausführt

Der Kern des Tutorials ist ein dreischrittiger Code‑Abschnitt, der dem bereits gezeigten Code entspricht. Im Folgenden zerlegen wir jede Zeile, erklären das Warum und geben Ihnen anschließend ein vollständiges, copy‑and‑paste‑fertiges Skript.

### Schritt 1: OCR‑Engine installieren und importieren

Stellen Sie zuerst sicher, dass die OCR‑Bibliothek verfügbar ist. **EasyOCR** funktioniert out‑of‑the‑box für viele Sprachen und liefert einen Vertrauenswert pro Wort.

```bash
pip install easyocr
```

```python
import easyocr  # The engine that will run OCR on image files
import os
```

*Warum EasyOCR?* Es bündelt ein Deep‑Learning‑Modell, das auf diversen Datensätzen trainiert wurde, sodass Sie typischerweise höhere Vertrauenswerte erhalten als mit der älteren Tesseract‑Engine, besonders bei Bildern gemischter Qualität.

> **Pro‑Tipp:** Wenn Sie in einer eingeschränkten Umgebung arbeiten (z. B. ein kleiner Docker‑Container), könnte `pytesseract` leichter sein, allerdings verlieren Sie dabei etwas von der modernen Genauigkeit, die EasyOCR bietet.

### Schritt 2: OCR auf das Bild anwenden

Jetzt führen wir tatsächlich **OCR auf Bild** aus. Die `recognize_image`‑Methode aus dem ursprünglichen Beispiel wird durch den EasyOCR‑Aufruf `readtext` ersetzt, der eine Liste von `(bbox, text, confidence)`‑Tupeln zurückgibt.

```python
# Initialize the OCR reader for English (you can add more languages as needed)
reader = easyocr.Reader(['en'])

# Path to the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "mixed_quality.png")

# Perform OCR – this is the step where we run OCR on image
ocr_results = reader.readtext(image_path, detail=1, paragraph=False)
```

Jeder Eintrag in `ocr_results` sieht folgendermaßen aus:

```python
[
    ((x1, y1, x2, y2, x3, y3, x4, y4), "Detected text", 0.92),
    ...
]
```

Das dritte Element (`0.92` im Beispiel) ist der Vertrauenswert im Bereich von 0 bis 1.

### Schritt 3: Gesamtes Vertrauen zusammenfassen

Im Gegensatz zum vorherigen Snippet, das ein einzelnes `confidence`‑Attribut ausgab, liefert EasyOCR ein Vertrauen pro Wort. Um einen Gesamteindruck zu bekommen, mitteln wir diese Werte:

```python
# Extract just the confidence numbers
confidences = [item[2] for item in ocr_results]

# Compute the mean confidence (overall confidence)
overall_confidence = sum(confidences) / len(confidences) if confidences else 0

print(f"Overall confidence: {overall_confidence:.2%}")
```

*Warum mitteln?* Es gibt Ihnen einen schnellen Gesundheits‑Check – liegt das Gesamtergebnis unter etwa 70 %, sollten Sie das Bild verbessern (bessere Beleuchtung, Vorverarbeitung usw.).

### Schritt 4: Wörter mit geringem Vertrauen auflisten

Jetzt kommt der Teil, der direkt die Anforderung „Liste Wörter, deren Vertrauen unter dem gewünschten Schwellenwert liegt“ erfüllt. Wir setzen standardmäßig einen **OCR‑Vertrauens‑Schwellenwert** von 0.80 (80 %) und können ihn bei Bedarf anpassen.

```python
# Define the confidence threshold – tweak as needed
THRESHOLD = 0.80

print("\nLow‑confidence words:")
low_confidence_found = False
for bbox, text, conf in ocr_results:
    if conf < THRESHOLD:
        low_confidence_found = True
        print(f"  • '{text}' ({conf:.2%})")
if not low_confidence_found:
    print("  All words meet the confidence threshold.")
```

Die Schleife gibt jedes Wort aus, das den Cut‑off nicht erreicht hat, zusammen mit seinem prozentualen Vertrauenswert. Das ist das exakte Gegenstück zur ursprünglichen `for recognized_word in recognition_result.words`‑Schleife, funktioniert aber mit dem Ausgabeformat von EasyOCR.

---

## ## Verständnis von OCR‑Vertrauens‑Scores

Vertrauen ist keine magische Zahl; es ist die Schätzung des Modells, wie sicher es sich bei einer bestimmten Transkription ist. Beachten Sie Folgendes:

| Situation | Typisches Vertrauen | Was zu tun ist |
|-----------|-------------------|------------|
| Klarer, hochauflösender Scan | 0.95 – 1.00 | Keine zusätzlichen Schritte nötig |
| Leichte Unschärfe oder ungleichmäßige Beleuchtung | 0.80 – 0.94 | Leichte Vorverarbeitung (Kontrast erhöhen) |
| Starke Geräusche, gedrehter Text | < 0.70 | Bildvorverarbeitung (Deskew, Denoise) oder andere OCR‑Engine verwenden |

> **Achtung:** Einige Sprachen (z. B. kursive Handschrift) erzeugen naturgemäß niedrigere Werte. Passen Sie den Schwellenwert entsprechend an.

### Randfälle & Varianten

1. **Batch‑Verarbeitung** – Wenn Sie **OCR auf Bild**‑Dateien in großen Mengen ausführen müssen, verpacken Sie die obige Logik in eine Schleife, die ein Verzeichnis durchläuft.  
2. **Mehrere Sprachen** – Übergeben Sie eine Liste wie `['en', 'fr']` an `easyocr.Reader` und die Engine erkennt beide.  
3. **Alternative Engines** – Möchten Sie **pytesseract** testen? Ersetzen Sie den Reader‑Block durch:

   ```python
   import pytesseract
   from PIL import Image

   img = Image.open(image_path)
   raw_text = pytesseract.image_to_string(img, output_type=pytesseract.Output.DICT)
   # raw_text['text'] contains the full string,
   # raw_text['conf'] holds per‑character confidence.
   ```

   Anschließend müssen Sie die Vertrauenswerte pro Zeichen zu Wort‑Vertrauenswerten aggregieren – etwas mehr Aufwand, aber machbar.

4. **Vorverarbeitungs‑Tricks** – Das Anwenden von OpenCV‑Filtern (`cv2.threshold`, `cv2.GaussianBlur`) kann das Vertrauen bei verrauschten Scans erhöhen.  

---

## ## Vollständiges, sofort ausführbares Skript

Unten finden Sie die komplette Python‑Datei, die Sie in Ihr Projekt einbinden können. Speichern Sie sie als `ocr_report.py` und führen Sie `python ocr_report.py` aus. Achten Sie darauf, dass der Bildpfad auf eine reale Datei zeigt.

```python
#!/usr/bin/env python3
"""
run_ocr_on_image.py

A self‑contained script that:
  1. Runs OCR on an image using EasyOCR.
  2. Prints the overall confidence.
  3. Lists any words whose confidence falls below a configurable threshold.

Author: Your Name
Date: 2026‑06‑06
"""

import os
import easyocr

# --------------------------- Configuration --------------------------- #
IMAGE_DIR = "YOUR_DIRECTORY"          # <-- Change to your folder
IMAGE_NAME = "mixed_quality.png"      # <-- Change to your file name
THRESHOLD = 0.80                       # Confidence threshold (0‑1)

# --------------------------- Helper Functions ----------------------- #
def load_image_path():
    """Construct the absolute path to the target image."""
    return os.path.join(IMAGE_DIR, IMAGE_NAME)

def run_ocr(image_path):
    """Run OCR on the image and return detailed results."""
    reader = easyocr.Reader(['en'])
    return reader.readtext(image_path, detail=1, paragraph=False)

def compute_overall_confidence(results):
    """Return the mean confidence across all detected words."""
    if not results:
        return 0.0
    confidences = [item[2] for item in results]
    return sum(confidences) / len(confidences)

def report_low_confidence_words(results, threshold):
    """Print words whose confidence is below the given threshold."""
    low_conf = [(text, conf) for _, text, conf in results if conf < threshold]
    if not low_conf:
        print("All words meet the confidence threshold.")
    else:
        for text, conf in low_conf:
            print(f"Low‑confidence word: '{text}' ({conf:.2%})")

# --------------------------- Main Execution ------------------------ #
def main():
    image_path = load_image_path()
    if not os.path.isfile(image_path):
        print(f"❌ Image not found: {image_path}")
        return

    # Step 1: Run OCR on image
    ocr_results = run_ocr(image_path)

    # Step 2: Show overall confidence
    overall = compute_overall_confidence(ocr_results)
    print(f"Overall confidence: {overall:.2%}")

    # Step 3: List low‑confidence words
    print("\n--- Low‑confidence words (threshold: {0:.0%}) ---".format(THRESHOLD))
    report_low_confidence_words(ocr_results, THRESHOLD)

if __name__ == "__main__":
    main()
```

**Erwartete Ausgabe** (Ihre Zahlen werden abweichen):

```
Overall confidence: 78.45%

--- Low‑confidence words (threshold: 80%) ---
Low‑confidence word: 'recgnition' (62.13%)
Low‑confidence word: 'imgae' (57.90%)
```

Wenn jedes Wort die 80 %-Marke überschreitet, sehen Sie stattdessen die freundliche Meldung „All words meet the confidence threshold.“.

---

## ## Häufig gestellte Fragen (FAQ)

**F: Funktioniert das mit PDFs?**  
A: Nicht direkt. Konvertieren Sie jede PDF‑Seite zuerst in ein Bild (z. B. mit `pdf2image`) und übergeben Sie dann das PNG/JPEG an das Skript.

**F: Meine Vertrauenszahlen sind alle niedrig – was kann ich tun?**  
A: Probieren Sie Bildvorverarbeitung: Kontrast erhöhen, Hintergrundrauschen entfernen oder das Bild horizontal ausrichten. EasyOCR akzeptiert außerdem einen Parameter `contrast_ths`, den Sie anpassen können.

**F: Kann ich die Ergebnisse als CSV exportieren?**  
A: Auf jeden Fall. Schreiben Sie nach der Low‑Confidence‑Schleife `ocr_results` mit einem `csv.DictWriter`, wobei jede Zeile `text`, `confidence` und die Bounding‑Box‑Koordinaten enthält.

**F: Gibt es eine GPU‑beschleunigte Version?**  
A: EasyOCR nutzt automatisch CUDA, wenn eine kompatible GPU und PyTorch installiert sind. Prüfen Sie mit `torch.cuda.is_available()` vor dem Skriptlauf.

---

## Fazit

Wir haben gerade **OCR auf Bild** mit Python ausgeführt, das Gesamtergebnis‑Vertrauen geprüft und Wörter mit geringem Vertrauen isoliert, die einer manuellen Nachbearbeitung bedürfen.

## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}