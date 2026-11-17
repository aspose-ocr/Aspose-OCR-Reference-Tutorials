---
category: general
date: 2026-06-28
description: Wie man OCR in Python stapelweise durchführt – Text aus Bildern extrahieren
  und gescannte Seiten mithilfe von Batch‑OCR‑Verarbeitung in Text umwandeln.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: de
og_description: Erfahren Sie, wie Sie OCR in Python stapelweise durchführen, Text
  aus Bildern extrahieren und gescannte Seiten mit effizienter Batch‑OCR‑Verarbeitung
  in Text umwandeln.
og_title: Wie man Batch-OCR in Python durchführt – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR in Python—extract text from images and convert scanned
    pages to text using batch OCR processing.
  headline: How to Batch OCR in Python – Complete Guide to Extract Text from Images
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Wie man OCR in Python stapelweise durchführt – Vollständige Anleitung zum Extrahieren
  von Text aus Bildern
url: /de/python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Batch‑OCR in Python durchführt – Vollständiger Leitfaden zum Extrahieren von Text aus Bildern

Wenn Sie sich fragen, **wie man Batch‑OCR in Python** durchführt, sind Sie hier genau richtig. Dieses Tutorial zeigt Ihnen einen schnellen Weg, **Text aus Bildern zu extrahieren** und **gescannte Seiten in Text zu konvertieren**, indem nur eine OCR‑Engine‑Instanz verwendet wird. Kein mühsames Kopieren‑Einfügen von Datei zu Datei mehr – lassen Sie den Code die schwere Arbeit übernehmen.

Wir gehen Schritt für Schritt durch alles, was Sie benötigen: die Bibliothek installieren, einen ganzen Ordner mit Scans laden, die Batch‑OCR‑Verarbeitung ausführen und die Ergebnisse elegant handhaben. Am Ende haben Sie ein wiederverwendbares Skript, das einen Stapel PNG‑ oder JPEG‑Dateien in durchsuchbare Textdateien verwandelt – und das in Sekunden.

## Was Sie benötigen

Bevor wir loslegen, stellen Sie sicher, dass Sie Folgendes haben:

* Python 3.9+ installiert (der Code funktioniert auch mit 3.8, aber 3.9+ bietet die neuesten Typing‑Features).
* Eine moderne OCR‑Bibliothek – hier verwenden wir **Aspose.OCR for Python via .NET**, die die im Original‑Snippet gezeigte `OcrEngine`‑Klasse bereitstellt.  
  ```bash
  pip install aspose-ocr
  ```
* Einen Ordner mit gescannten Seiten (`page1.png`, `page2.png`, …). Alles, was Pillow öffnen kann, funktioniert, also sind PDFs, TIFFs oder BMPs ebenfalls in Ordnung.
* Ein bisschen Neugier – wenn Sie noch nie Bild‑zu‑Text automatisiert haben, werden Sie gleich sehen, warum Batch‑OCR ein echter Game‑Changer ist.

> **Pro tip:** Wenn Sie lieber eine reine Python‑Bibliothek verwenden, ersetzen Sie `OcrEngine` durch `pytesseract.image_to_string`. Die umgebende Logik bleibt identisch.

## Wie man Batch‑OCR in Python – Schritt‑für‑Schritt‑Anleitung

Unten finden Sie das vollständige, ausführbare Skript. Jede Zeile ist kommentiert, sodass Sie sehen können *warum* jedes Bauteil wichtig ist, nicht nur *was* es tut.

```python
# batch_ocr.py
import os
from aspose.ocr import OcrEngine, Image  # Aspose OCR library
from typing import List

def load_images(folder: str) -> List[Image]:
    """
    Scan a directory and return a list of Aspose.Image objects.
    Supports PNG, JPEG, BMP, and TIFF out of the box.
    """
    supported_ext = {".png", ".jpg", ".jpeg", ".bmp", ".tif", ".tiff"}
    images = []
    for filename in sorted(os.listdir(folder)):
        _, ext = os.path.splitext(filename)
        if ext.lower() in supported_ext:
            path = os.path.join(folder, filename)
            try:
                img = Image.from_file(path)
                images.append(img)
            except Exception as e:
                print(f"⚠️  Could not load {filename}: {e}")
    return images

def batch_ocr_process(images: List[Image]) -> List[str]:
    """
    Perform OCR on the whole batch at once.
    Returns a list of recognized strings, one per image.
    """
    engine = OcrEngine()          # Step 1: create an OCR engine instance
    # The recognize_batch method is optimized for bulk work.
    return engine.recognize_batch(images)

def save_results(texts: List[str], output_folder: str):
    """
    Write each page's text to a separate .txt file.
    """
    os.makedirs(output_folder, exist_ok=True)
    for idx, page_text in enumerate(texts, start=1):
        out_path = os.path.join(output_folder, f"page_{idx}.txt")
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(page_text)
        print(f"✅  Saved page {idx} → {out_path}")

def main():
    # -----------------------------------------------------------------
    # 1️⃣ Load the images you want to process
    # -----------------------------------------------------------------
    image_folder = "YOUR_DIRECTORY"          # <-- replace with your path
    images = load_images(image_folder)

    if not images:
        print("❌  No supported images found. Exiting.")
        return

    # -----------------------------------------------------------------
    # 2️⃣ Perform OCR on the whole batch at once
    # -----------------------------------------------------------------
    print(f"🔎  Running batch OCR on {len(images)} images...")
    page_texts = batch_ocr_process(images)

    # -----------------------------------------------------------------
    # 3️⃣ Output the recognized text for each page
    # -----------------------------------------------------------------
    for i, txt in enumerate(page_texts, start=1):
        print(f"\n--- Page {i} ---")
        print(txt[:200] + ("…" if len(txt) > 200 else ""))  # preview first 200 chars

    # -----------------------------------------------------------------
    # 4️⃣ (Optional) Save each page's text to a file
    # -----------------------------------------------------------------
    save_results(page_texts, "ocr_output")

if __name__ == "__main__":
    main()
```

### Erwartete Ausgabe

Das Ausführen des Skripts in einem Ordner mit drei PNG‑Scans liefert etwa Folgendes:

```
🔎  Running batch OCR on 3 images...

--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit…

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore…

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco…
✅  Saved page 1 → ocr_output/page_1.txt
✅  Saved page 2 → ocr_output/page_2.txt
✅  Saved page 3 → ocr_output/page_3.txt
```

Die Vorschau zeigt die ersten 200 Zeichen jeder Seite, und der komplette Text befindet sich im Verzeichnis `ocr_output`.

## Text aus Bildern mit einer einzigen Engine extrahieren

Warum erstellen wir **eine** `OcrEngine` und verwenden sie mehrfach? Das Instanziieren der Engine kann teuer sein, weil Sprachpakete und native DLLs geladen werden. Wenn Sie dieselbe Instanz über das Batch hinweg teilen, erhalten Sie:

* **Speicher sparen** – nur ein Satz Ressourcen liegt im RAM.
* **Geschwindigkeit erhöhen** – die Engine bleibt „warm“ und vermeidet wiederholte Initialisierungen.
* **Konsistenz wahren** – dieselben Erkennungseinstellungen gelten für jede Seite, was entscheidend ist, wenn Sie **Text aus Bildern** extrahieren wollen, die das gleiche Layout teilen.

Falls Sie die Erkennung anpassen müssen (z. B. Rechtschreibprüfung aktivieren oder die Sprache ändern), tun Sie dies *vor* dem Aufruf von `recognize_batch`. Alle nachfolgenden Seiten übernehmen diese Einstellungen automatisch.

## Gescannte Seiten effizient in Text konvertieren

Der Kern des Problems – **gescannte Seiten in Text konvertieren** – wird durch `engine.recognize_batch(images)` gelöst. Im Hintergrund verarbeitet die Bibliothek jedes Bild in einem Thread‑Pool, sodass Sie auf Mehrkern‑Maschinen nahezu lineare Skalierung erhalten. Ein paar Dinge, die Sie beachten sollten:

* **Bildqualität ist entscheidend** – 300 dpi oder höher liefert die besten Ergebnisse. Wenn Ihre Scans eine niedrige Auflösung haben, überlegen Sie, sie mit Pillow hochzuskalieren, bevor Sie sie an die Engine übergeben.
* **Farbe vs. Graustufen** – OCR‑Engines arbeiten meist schneller mit 8‑Bit‑Graustufen. Sie können einen Vorverarbeitungsschritt hinzufügen:
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **Sprachunterstützung** – Aspose.OCR unterstützt über 40 Sprachen. Setzen Sie `engine.language = "eng"` oder `"fra"` vor dem Batch‑Aufruf, wenn Sie nicht mit Englisch arbeiten.

## Best Practices für Batch‑OCR‑Verarbeitung

Obwohl der obige Code bereits kompakt ist, erfordert produktionsreifes Batch‑OCR häufig ein paar zusätzliche Schutzmaßnahmen:

| Problem | Empfohlener Ansatz |
|---------|--------------------|
| **Große Batches ( > 500 Dateien )** | In Stücke von 100–200 Bildern aufteilen, um den Speicherverbrauch moderat zu halten. |
| **Beschädigte oder nicht unterstützte Dateien** | Der `load_images`‑Helper fängt bereits Ausnahmen ab und protokolliert eine Warnung; Sie können zusätzlich ein Fallback implementieren, das fehlerhafte Dateien überspringt oder verschiebt. |
| **Fortschrittsüberwachung** | `recognize_batch` in einer Schleife einbetten, die nach jedem Bild einen Yield ausgibt, falls die Bibliothek per‑Bild‑Callbacks bereitstellt. |
| **Nachbearbeitung** | Eine Rechtschreibprüfung oder Regex‑Bereinigung auf die resultierenden Strings anwenden, um die spätere Durchsuchbarkeit zu verbessern. |
| **Parallelität** | Bei einer Multi‑Node‑Umgebung Ordner auf mehrere Worker verteilen und die `.txt`‑Ausgaben am Ende zusammenführen. |

Diese Tipps helfen Ihnen, **Batch‑OCR‑Verarbeitung** von wenigen Seiten auf tausende zu skalieren, ohne dass Ihr Skript abstürzt.

## Häufig gestellte Fragen

**F: Kann ich das direkt mit PDFs verwenden?**  
A: Absolut. Konvertieren Sie jede PDF‑Seite zuerst in ein Bild (z. B. mit `pdf2image`) und übergeben Sie die resultierende Liste an `recognize_batch`. Der Rest der Pipeline bleibt unverändert.

## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}