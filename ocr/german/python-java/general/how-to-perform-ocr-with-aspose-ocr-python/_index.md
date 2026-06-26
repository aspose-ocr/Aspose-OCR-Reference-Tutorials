---
category: general
date: 2026-06-25
description: Wie man OCR mit Aspose OCR Python durchführt – lernen Sie, Bild‑OCR zu
  laden, Bild‑OCR zu verarbeiten und JSON‑Ergebnisse in Minuten zu extrahieren.
draft: false
keywords:
- how to perform OCR
- aspose OCR python
- load image OCR
- process image OCR
language: de
og_description: Wie man OCR mit Aspose OCR Python durchführt. Folgen Sie dieser Anleitung,
  um Bild‑OCR zu laden, Bild‑OCR zu verarbeiten und die JSON‑Ausgabe mühelos zu analysieren.
og_title: Wie man OCR mit Aspose OCR in Python durchführt
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to perform OCR with Aspose OCR Python – learn to load image OCR,
    process image OCR, and extract JSON results in minutes.
  headline: How to Perform OCR with Aspose OCR Python
  type: TechArticle
- description: How to perform OCR with Aspose OCR Python – learn to load image OCR,
    process image OCR, and extract JSON results in minutes.
  name: How to Perform OCR with Aspose OCR Python
  steps:
  - name: Creating an OCR engine instance.
    text: Creating an OCR engine instance.
  - name: Loading an image for OCR.
    text: Loading an image for OCR.
  - name: Processing the image OCR.
    text: Processing the image OCR.
  - name: Converting the result to JSON.
    text: Converting the result to JSON.
  - name: Parsing and printing useful information.
    text: Parsing and printing useful information.
  - name: '**File format matters** – While TIFF works great for scanned documents,
      PNG is often better for screenshots, and JPEG for photographs.'
    text: '**File format matters** – While TIFF works great for scanned documents,
      PNG is often better for screenshots, and JPEG for photographs.'
  - name: '**Resolution** – Aspose OCR performs best with 300 dpi or higher. If you
      see low confidence scores, consider up‑sampling the image before loading.'
    text: '**Resolution** – Aspose OCR performs best with 300 dpi or higher. If you
      see low confidence scores, consider up‑sampling the image before loading.'
  - name: '**Multi‑page files** – If your TIFF contains several pages, `image = ocr.Image.load(path)`
      will give you a stack; you can iterate with `for page in image.pages:` and call
      `engine.recognize(page)` for each.'
    text: '**Multi‑page files** – If your TIFF contains several pages, `image = ocr.Image.load(path)`
      will give you a stack; you can iterate with `for page in image.pages:` and call
      `engine.recognize(page)` for each.'
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: Wie man OCR mit Aspose OCR Python durchführt
url: /de/python-java/general/how-to-perform-ocr-with-aspose-ocr-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR mit Aspose OCR Python durchführt

Haben Sie sich jemals gefragt, **wie man OCR** auf einer Quittung, Rechnung oder einem beliebigen gescannten Dokument mit Python durchführt? Sie sind nicht allein. In vielen realen Projekten ist das Extrahieren von Text aus Bildern der erste Schritt zu Automatisierung, Analytik oder Archivierung.  

Die gute Nachricht? Mit **Aspose OCR Python** können Sie Bild‑OCR laden, Bild‑OCR verarbeiten und ein übersichtliches JSON‑Payload in nur wenigen Code‑Zeilen erhalten. Im Folgenden sehen Sie ein vollständiges, sofort ausführbares Skript sowie die Begründung hinter jedem Schritt, damit Sie wirklich verstehen, *warum* der Code so aussieht, wie er ist.

## Was dieses Tutorial abdeckt

- Einrichten der Aspose OCR Engine in Python  
- **Load image OCR** korrekt laden, gängige Formate wie TIFF, PNG und JPEG behandeln  
- **Process image OCR** verarbeiten und das Ergebnis in JSON konvertieren  
- Das JSON parsen, um nützliche Informationen zu erhalten (Wörter, Vertrauenswerte usw.)  
- Tipps zur Fehlersuche, zum Umgang mit Randfällen und Ideen für die nächsten Schritte  

Vorkenntnisse mit Aspose sind nicht erforderlich; Sie benötigen lediglich eine funktionierende Python 3‑Umgebung und eine Bilddatei, die Sie einlesen möchten.

## Voraussetzungen

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| Python 3.8+ | Die Wheels von Aspose OCR zielen auf moderne Interpreter ab |
| `aspose-ocr` Paket (`pip install aspose-ocr`) | Die Kernbibliothek, die die schwere Arbeit erledigt |
| Ein Beispielbild (z. B. `receipt.tif`) | Wir benötigen etwas, das in die Engine eingespeist wird |
| Grundkenntnisse in `json` | Wir werden die OCR‑Ausgabe in ein Python‑Dict parsen |

> **Profi‑Tipp:** Wenn Sie Windows verwenden, führen Sie die Eingabeaufforderung als Administrator aus, wenn Sie das Paket installieren, um Berechtigungsprobleme zu vermeiden.

---

## Wie man OCR mit Aspose OCR Python durchführt

Im Folgenden finden Sie das **vollständige Skript**, das Sie in eine Datei namens `ocr_demo.py` kopieren können. Es enthält alles – von den Imports bis zur finalen Ausgabe – sodass Sie es sofort ausführen können.

```python
#!/usr/bin/env python3
"""
How to Perform OCR with Aspose OCR Python

This script demonstrates:
1. Creating an OCR engine instance.
2. Loading an image for OCR.
3. Processing the image OCR.
4. Converting the result to JSON.
5. Parsing and printing useful information.
"""

import json
import aspose.ocr as ocr
import os
import sys

# ----------------------------------------------------------------------
# Step 1: Create an OCR engine instance
# ----------------------------------------------------------------------
# The engine holds configuration (language, recognition mode, etc.).
# For most cases the defaults work fine, but you can tweak them later.
engine = ocr.OcrEngine()

# ----------------------------------------------------------------------
# Step 2: Load image OCR
# ----------------------------------------------------------------------
# Aspose can read many formats; here we use a TIFF because receipts often
# come as multi‑page scans. Adjust the path to point at your own file.
image_path = os.path.join("YOUR_DIRECTORY", "receipt.tif")
if not os.path.isfile(image_path):
    sys.stderr.write(f"❌ Image not found: {image_path}\n")
    sys.exit(1)

# The Image.load method decodes the file into an in‑memory object.
image = ocr.Image.load(image_path)

# ----------------------------------------------------------------------
# Step 3: Process image OCR
# ----------------------------------------------------------------------
# The recognize() call runs the OCR engine on the supplied image.
# It returns an OcrResult object that we can later serialize.
result = engine.recognize(image)

# ----------------------------------------------------------------------
# Step 4: Convert the recognition result to JSON
# ----------------------------------------------------------------------
# Aspose gives us a handy to_json() method; we then feed the string
# into Python's json module for a native dict.
json_payload = result.to_json()
parsed = json.loads(json_payload)

# ----------------------------------------------------------------------
# Step 5: Inspect the parsed data
# ----------------------------------------------------------------------
# The structure contains keys like "words", "lines", and "pages".
# We'll print a few samples to prove it works.
print("\n🔎 JSON keys:", list(parsed.keys()))
if parsed.get("words"):
    print("First word entry:", parsed["words"][0])
else:
    print("⚠️ No words detected – check image quality or language settings.")
```

### Erwartete Ausgabe

Wenn Sie `python ocr_demo.py` ausführen (vorausgesetzt, das Bild existiert und ist lesbar), sollten Sie etwas Ähnliches sehen:

```
🔎 JSON keys: ['pages', 'lines', 'words', 'language', 'confidence']
First word entry: {'text': 'Total', 'confidence': 0.98, 'rectangle': {...}}
```

Der genaue Inhalt variiert je nach Quellbild, aber das Vorhandensein des `"words"`‑Arrays bestätigt, dass **process image OCR** erfolgreich war.

---

## Load Image OCR – Tipps & häufige Fallstricke

1. **Dateiformat ist wichtig** – Während TIFF hervorragend für gescannte Dokumente funktioniert, ist PNG oft besser für Screenshots und JPEG für Fotografien.  
2. **Auflösung** – Aspose OCR liefert die besten Ergebnisse bei 300 dpi oder höher. Wenn Sie niedrige Vertrauenswerte sehen, sollten Sie das Bild vor dem Laden hochskalieren.  
3. **Mehrseitige Dateien** – Wenn Ihr TIFF mehrere Seiten enthält, liefert `image = ocr.Image.load(path)` einen Stapel; Sie können mit `for page in image.pages:` iterieren und `engine.recognize(page)` für jede Seite aufrufen.

> **Warum dieser Schritt entscheidend ist:** Das korrekte Laden des Bildes stellt sicher, dass die OCR‑Engine saubere Pixeldaten erhält. Ein beschädigtes oder nicht unterstütztes Format führt dazu, dass `engine.recognize` eine Ausnahme wirft und Ihre Pipeline stoppt.

---

## Process Image OCR – Erweiterte Optionen

Aspose OCR stellt mehrere Eigenschaften am `OcrEngine`‑Objekt bereit:

| Eigenschaft | Anwendungsfall |
|-------------|----------------|
| `engine.language = ocr.Language.English` | Erzwingt Englisch, wenn das Bild gemischte Skripte enthält |
| `engine.recognition_mode = ocr.RecognitionMode.TextDetection` | Schneller, aber weniger genau; gut für schnelle Vorschauen |
| `engine.auto_rotate = True` | Korrigiert automatisch gedrehte Seiten (praktisch für Quittungen) |

Sie können diese vor Schritt 3 setzen, um die **process image OCR**‑Phase fein abzustimmen. Zum Beispiel:

```python
engine.language = ocr.Language.English
engine.auto_rotate = True
```

---

## Verständnis der Aspose OCR Python Ausgabe

Das JSON‑Payload folgt einem vorhersehbaren Schema:

- **pages** – Liste von Seitenobjekten, jeweils mit Abmessungen und Rotationsinformationen.  
- **lines** – Gruppierte Wörter, die dieselbe Grundlinie teilen. Nützlich zum Wiederaufbau von Absätzen.  
- **words** – Einzelne Wortobjekte mit `text`, `confidence` und einem `rectangle` mit Koordinaten.  
- **language** – Erkannter Sprachcode (z. B. "en").  
- **confidence** – Gesamtes Vertrauen für das gesamte Dokument.

Dieses Strukturwissen ermöglicht es Ihnen, exakt das zu extrahieren, was Sie benötigen. Beispielsweise könnten Sie alle Wörter mit einem Vertrauen < 0,9 (potenzielle OCR‑Fehler) hinzufügen:

```python
low_confidence = [w for w in parsed["words"] if w["confidence"] < 0.9]
print("Potentially mis‑read words:", low_confidence)
```

---

## Randfälle & wie man sie handhabt

| Situation | Empfohlene Vorgehensweise |
|-----------|---------------------------|
| **Leeres Ergebnis** (keine Wörter) | Bildqualität überprüfen, sicherstellen, dass die richtige Sprache eingestellt ist, und ggf. DPI erhöhen. |
| **Mehrseitige PDFs** | PDF‑Seiten zuerst in Bilder konvertieren (z. B. mit `pdf2image`) und dann jede Seite an die OCR‑Engine übergeben. |
| **Nicht‑lateinische Skripte** | Zusätzliche Sprachpakete installieren via `engine.add_language(ocr.Language.ChineseSimplified)`. |
| **Große Dateien** | In Teilen verarbeiten; dieselbe `OcrEngine`‑Instanz wiederverwenden, um übermäßige Speicherzuweisung zu vermeiden. |

---

## Vollständiges funktionierendes Beispiel (Alle Schritte kombiniert)

Im Folgenden finden Sie eine kompakte Version, die Sie in ein Jupyter‑Notebook oder ein Skript einfügen können. Sie enthält Fehlerbehandlung, optionale Einstellungen und gibt eine übersichtliche Zusammenfassung aus.

```python
import json, os, sys, aspose.ocr as ocr

def perform_ocr(image_path: str):
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Create engine and tweak settings (optional)
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English   # ensures English detection
    engine.auto_rotate = True                # correct rotated scans

    # Load and recognize
    image = ocr.Image.load(image_path)
    result = engine.recognize(image)

    # Convert to JSON and parse
    parsed = json.loads(result.to_json())
    return parsed

if __name__ == "__main__":
    img = os.path.join("YOUR_DIRECTORY", "receipt.tif")
    try:
        data = perform_ocr(img)
        print("\n🔎 JSON keys:", list(data.keys()))
        print("First word:", data["words"][0] if data.get("words") else "No words")
    except Exception as exc:
        sys.stderr.write(f"❗ OCR failed: {exc}\n")
```

Das Ausführen dieses Codes liefert dieselbe prägnante Ausgabe wie zuvor,

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Text aus Bild mit Aspose OCR extrahieren – Schritt‑für‑Schritt‑Anleitung](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Wie man Aspose OCR für JSON‑Ergebnis in der Bild­erkennung verwendet](/ocr/english/net/text-recognition/get-result-as-json/)
- [Wie man Bild‑Textextraktion aus einem Stream mit Aspose OCR durchführt](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}