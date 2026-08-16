---
category: general
date: 2026-04-26
description: Wie man OCR aus Bildern mit Python extrahiert – ein Python‑OCR‑Beispiel,
  das zeigt, wie man ein Bild für OCR lädt und Text von einer Quittung extrahiert.
draft: false
keywords:
- how to extract ocr
- python ocr example
- extract text from receipt
- load image for ocr
- how to use OCR
language: de
og_description: wie man OCR aus Bildern mit Python extrahiert. Lernen Sie ein Python-OCR-Beispiel,
  laden Sie ein Bild für OCR und extrahieren Sie Text von einer Quittung in Minuten.
og_title: Wie man OCR in Python extrahiert – Vollständiger Leitfaden
tags:
- OCR
- Python
- Image Processing
title: Wie man OCR in Python extrahiert – Schritt‑für‑Schritt‑Tutorial
url: /de/python-java/general/how-to-extract-ocr-in-python-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in Python extrahiert – Vollständige Anleitung

Haben Sie sich jemals gefragt, **wie man OCR** aus einem verschwommenen Kassenbon oder einer gescannten Rechnung extrahiert? Sie sind nicht allein – Entwickler stoßen ständig an Grenzen, wenn sie sauberen, maschinenlesbaren Text aus Bildern benötigen. Die gute Nachricht? Mit nur wenigen Zeilen Python können Sie ein Bild eines Kassenbons in hochzuverlässigen, durchsuchbaren Text verwandeln.

In diesem Tutorial gehen wir Schritt für Schritt durch ein **python ocr example**, das **wie man Bild für OCR lädt**, die Engine ausführt und nur die Zeichen behält, die einen Vertrauenswert von 85 % überschreiten. Am Ende können Sie **Text aus Kassenbon‑Bildern extrahieren**, ohne durch Dokumentationen zu wühlen oder API‑Parameter zu raten.

## Was Sie benötigen

- Python 3.9 oder neuer (die hier verwendete Syntax funktioniert ab 3.8+)
- Das `aocr`‑Paket (oder jede OCR‑Bibliothek, die eine `OcrEngine`‑Klasse bereitstellt). Installieren Sie es mit:

```bash
pip install aocr
```

- Ein Beispiel‑Kassenbon‑Bild (`receipt.png`) in einem Ordner, den Sie referenzieren können.
- Einen Text‑Editor oder eine IDE – VS Code, PyCharm oder sogar ein einfaches Notebook reichen aus.

Das war’s. Keine schweren Frameworks, keine externen Dienste, nur reines Python.

![High‑confidence OCR result – how to extract ocr from a receipt](/images/ocr-high-confidence.png)

*Bild‑Alt‑Text: how to extract ocr from a receipt using Python OCR*

## Schritt 1 – OCR‑Engine‑Instanz erstellen (how to extract ocr)

Das Erste, was wir tun, ist eine OCR‑Engine zu starten. Denken Sie daran als das Gehirn, das die Pixel für uns liest.

```python
# Step 1: Initialize the OCR engine
from aocr import OcrEngine

ocr_engine = OcrEngine()
```

**Warum?** Durch das Instanziieren von `OcrEngine` erhalten Sie ein frisches Konfigurationsobjekt. Sie können später Sprachmodelle, DPI‑Einstellungen oder Vorverarbeitungsschritte anpassen – alles ohne den Kern der Verarbeitungsschleife zu berühren.

## Schritt 2 – Bild für OCR laden

Als Nächstes zeigen wir der Engine das Bild, das wir analysieren wollen. Hier kommt das Schlüsselwort **load image for ocr** zum Einsatz.

```python
# Step 2: Load the receipt image
image_path = "YOUR_DIRECTORY/receipt.png"
ocr_engine.image = OcrEngine.Image.load(image_path)
```

> **Pro‑Tipp:** Wenn Ihr Bild in einem anderen Verzeichnis liegt, verwenden Sie `os.path.join`, um einen plattformunabhängigen Pfad zu erstellen.

**Warum das Bild auf diese Weise laden?** Der Helfer `Image.load` liest die Datei in ein Format ein, das die Engine versteht, und verarbeitet gängige Formate (PNG, JPEG, TIFF) automatisch. Wird dieser Schritt übersprungen oder rohe Bytes übergeben, löst das einen `ValueError` aus.

## Schritt 3 – OCR‑Prozess ausführen

Jetzt führen wir das OCR tatsächlich aus. Die Methode `process` liefert ein umfangreiches Ergebnisobjekt mit erkannten Symbolen, Vertrauenswerten und Begrenzungsrahmen.

```python
# Step 3: Execute OCR and capture the result
ocr_result = ocr_engine.process()
```

**Was enthält `ocr_result`?** In den meisten Bibliotheken beinhaltet es:

- `text`: den rohen, zusammengefügten String.
- `symbol_confidences`: eine Liste von Tupeln `(char, confidence)`.
- `boxes`: Koordinaten für jedes Zeichen (nützlich für visuelles Debugging).

Der Zugriff auf die Vertrauenswerte pro Zeichen ist für den nächsten Schritt unverzichtbar.

## Schritt 4 – Nur hochzuverlässige Symbole behalten (≥ 85 %)

Ein Kassenbon hat oft Schmierflecken, blassen Druck oder Hintergrundrauschen. Durch das Herausfiltern von Symbolen mit niedriger Zuverlässigkeit verbessern wir die nachfolgende Auswertung erheblich.

```python
# Step 4: Filter out low‑confidence characters
high_confidence_text = ''.join(
    char for char, confidence in ocr_result.symbol_confidences
    if confidence >= 0.85
)
```

**Warum 85 %?** Empirisch bietet ein Schwellenwert um 0,85 ein gutes Gleichgewicht zwischen Recall und Precision für die meisten gedruckten Kassenbons. Wenn Ihnen Zahlen fehlen, senken Sie den Schwellenwert; wenn Sie Kauderwelsch erhalten, erhöhen Sie ihn.

## Schritt 5 – Hochzuverlässigen extrahierten Text ausgeben

Abschließend geben wir die bereinigte Zeichenkette aus (oder speichern sie). Das ist der Kern unseres **extract text from receipt**‑Workflows.

```python
# Step 5: Show the cleaned result
print("High‑confidence text:", high_confidence_text)
```

Typische Ausgabe sieht so aus:

```
High‑confidence text: Store XYZ
Date: 2024‑04‑22
Total: $23.45
```

Sie können diesen String nun an einen CSV‑Writer, eine Datenbank oder irgendeine nachgelagerte Analyse‑Pipeline weitergeben.

## Vollständiges, sofort ausführbares Skript

Unten finden Sie das komplette Code‑Snippet, das Sie in `ocr_receipt.py` kopieren und sofort ausführen können.

```python
# ocr_receipt.py
# A complete python ocr example that extracts high‑confidence text from a receipt.

from aocr import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the image you want to analyze
    image_path = "YOUR_DIRECTORY/receipt.png"
    ocr_engine.image = OcrEngine.Image.load(image_path)

    # 3️⃣ Run the OCR process
    ocr_result = ocr_engine.process()

    # 4️⃣ Keep only symbols with confidence ≥ 85%
    high_confidence_text = ''.join(
        char for char, confidence in ocr_result.symbol_confidences
        if confidence >= 0.85
    )

    # 5️⃣ Output the result
    print("High‑confidence text:", high_confidence_text)

if __name__ == "__main__":
    main()
```

Speichern Sie die Datei, stellen Sie sicher, dass `receipt.png` existiert, und führen Sie aus:

```bash
python ocr_receipt.py
```

Sie sollten den bereinigten Kassenbon‑Text in der Konsole sehen.

## Randfälle & Was‑wenn‑Szenarien

| Situation | Empfohlene Lösung |
|-----------|-------------------|
| **Sehr niedrige Zuverlässigkeit überall** | Bild vorverarbeiten: Kontrast erhöhen, in Graustufen konvertieren oder einen Rauschfilter anwenden (`cv2.GaussianBlur`). |
| **Nicht‑lateinische Zeichen** | Ein Sprachmodell an `OcrEngine` übergeben (z. B. `ocr_engine.language = "spa"` für Spanisch). |
| **Mehrere Kassenbons in einem Bild** | OCR auf das gesamte Bild anwenden, dann das Ergebnis mit regulären Ausdrücken splitten, die `\n\n+` (doppelte Zeilenumbrüche) erkennen. |
| **Roh‑OCR‑Text ebenfalls benötigen** | `ocr_result.text` neben der gefilterten Version für Debugging behalten. |

Diese Varianten stellen sicher, dass Ihr **how to use OCR**‑Wissen über den einfachsten Anwendungsfall hinaus skaliert.

## Häufige Stolperfallen (und wie man sie vermeidet)

- **Vergessen, die Bibliothek zu installieren** – `pip install aocr` muss erfolgreich abgeschlossen sein, bevor Sie importieren.
- **Falscher Pfad‑Separator** unter Windows (`\` vs `/`). Verwenden Sie `os.path.join`.
- **Hard‑codierter Vertrauensschwellenwert** ohne Test – führen Sie immer einen kurzen visuellen Check an ein paar Kassenbons durch.
- **Unicode‑Normalisierung ignorieren** – manche Kassenbons enthalten spezielle Bindestriche; führen Sie `unicodedata.normalize('NFKC', text)` aus, wenn Sie die Ausgabe speichern wollen.

## Nächste Schritte – über die Grundlagen hinaus

Jetzt, wo Sie **wie man OCR**‑Daten aus einem einzelnen Kassenbon extrahiert, möchten Sie vielleicht:

1. **Stapelverarbeitung eines Ordners mit Kassenbons** – über alle PNG/JPG‑Dateien iterieren und jedes Ergebnis in eine CSV schreiben.
2. **Integration in eine Datenbank** – `high_confidence_text` in SQLite für schnelle Abfragen speichern.
3. **Natürliche Sprachverarbeitung anwenden** – mit Regex oder `dateutil` Daten, Summen und Steuerbeträge extrahieren.
4. **Alternative Bibliotheken testen** – `pytesseract`, `easyocr` oder Cloud‑Dienste (Google Vision, Azure OCR), wenn Sie mehrsprachige Unterstützung oder höhere Genauigkeit benötigen.

Jedes dieser Themen greift natürlich unsere sekundären Schlüsselwörter auf: *python ocr example*, *extract text from receipt*, *load image for ocr* und *how to use OCR*.

## Fazit

Wir haben ein komplettes **python ocr example** durchgearbeitet, das **wie man OCR**‑Text aus einem Kassenbon‑Bild extrahiert, niedrig‑zuverlässige Symbole filtert und saubere Ergebnisse ausgibt. Die Schritte sind einfach, der Code ist eigenständig und der Ansatz flexibel genug, um in größere Projekte zu integrieren.

Probieren Sie es mit Ihren eigenen Kassenbons, passen Sie den Vertrauensschwellenwert an und skalieren Sie anschließend zur Stapelverarbeitung. Wenn Sie auf Eigenheiten stoßen – etwa ein schwaches Logo oder eine ungewöhnliche Schriftart – denken Sie an die oben genannten Randfall‑Tipps. Viel Spaß beim Coden und mögen Ihre OCR‑Pipelines stets präzise sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}