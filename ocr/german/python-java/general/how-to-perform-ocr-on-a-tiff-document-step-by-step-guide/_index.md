---
category: general
date: 2026-01-12
description: Wie man OCR schnell und genau durchführt. Lernen Sie, OCR auf Dokumenten
  auszuführen, Text aus TIFF zu extrahieren, ein Bild für OCR zu laden und die OCR‑Sprache
  in Python festzulegen.
draft: false
keywords:
- how to perform ocr
- run ocr on document
- extract text from tiff
- load image for ocr
- set OCR language
language: de
og_description: Wie man OCR in Python durchführt. Dieses Tutorial zeigt Ihnen, wie
  Sie OCR auf Dokumenten ausführen, Text aus TIFF extrahieren, ein Bild für OCR laden
  und die OCR‑Sprache einstellen.
og_title: Wie man OCR auf einem TIFF-Dokument durchführt – Komplettanleitung
tags:
- OCR
- Python
- Image Processing
title: Wie man OCR auf einem TIFF-Dokument durchführt – Schritt‑für‑Schritt‑Anleitung
url: /de/python-java/general/how-to-perform-ocr-on-a-tiff-document-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR auf einem TIFF-Dokument durchführt – Vollständige Anleitung

Haben Sie sich jemals gefragt, **wie man OCR** auf einer gescannten TIFF-Datei durchführt, ohne Stunden damit zu verbringen, die richtige Bibliothek zu suchen? Sie sind nicht allein. Viele Entwickler stoßen an ihre Grenzen, wenn sie Text aus TIFF‑Bildern extrahieren müssen, besonders wenn Leistung und Spracheinstellungen wichtig sind.

In diesem Tutorial führen wir Sie durch alles, was Sie wissen müssen: von der Installation des OCR‑Pakets, dem Laden des Bildes für OCR, dem Einstellen der OCR‑Sprache, bis hin zum **Ausführen von OCR auf dem Dokument** und dem Extrahieren von sauberem Text. Am Ende haben Sie ein einsatzbereites Skript, das Sie in jedes Projekt einbinden können.

> **Profi‑Tipp:** Während das Beispiel ein generisches `ocr`‑Modul verwendet, gelten dieselben Konzepte für Tesseract, EasyOCR oder jede moderne OCR‑Engine, die eine Python‑API bereitstellt.

---

## Was Sie benötigen

- Python 3.8+ (jede aktuelle Version funktioniert)
- Eine OCR‑Bibliothek, die eine `OcrEngine`‑Klasse bereitstellt (das Beispiel verwendet ein fiktives `ocr`‑Paket; ersetzen Sie es durch Ihr echtes)
- Eine mehrseitige TIFF‑Datei, die Sie verarbeiten möchten (wir nennen sie `big_document.tif`)
- Ein Rechner mit mindestens 4 CPU‑Kernen, falls Sie die Thread‑Anzahl festlegen wollen

Keine externen Dienste, keine Cloud‑Schlüssel – nur lokaler Code, der in Sekunden läuft.

![Beispiel für OCR‑Ausführung](/images/ocr-example.png "Wie man OCR auf einem TIFF-Dokument durchführt")

*Bildbeschreibung: Wie man OCR auf einem TIFF-Dokument durchführt – Vorschau des extrahierten Textes.*

---

## Schritt 1: Installieren und Importieren der OCR‑Bibliothek

Zuerst: Holen Sie sich die Bibliothek auf Ihren Rechner. Die meisten OCR‑Pakete sind auf PyPI, sodass ein einfacher `pip install` ausreicht.

```bash
pip install ocr‑engine   # replace with the actual package name, e.g., pytesseract
```

Jetzt importieren Sie die Klassen, die Sie benötigen. Wenn Sie Tesseract verwenden, sieht die Import‑Zeile anders aus, aber der Rest des Codes bleibt gleich.

```python
# Step 1: Import the OCR engine and image helper
import ocr                       # fictional package – swap with your real one
from ocr import OcrEngine, Image
```

*Warum das wichtig ist:* Das frühe Importieren der richtigen Symbole verhindert später Namenskonflikte und macht das Skript leichter lesbar.

---

## Schritt 2: Erstellen und Konfigurieren der OCR‑Engine (OCR‑Sprache festlegen)

Das Konfigurieren der Engine ist der Ort, an dem Sie **die OCR‑Sprache festlegen** für eine genaue Erkennung. Englisch ist die Vorgabe, aber Sie können mit einer einzigen Zeile zu Französisch, Deutsch oder sogar zum mehrsprachigen Modus wechseln.

```python
# Step 2: Initialize the engine and set language
ocr_engine = OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # set OCR language to English
ocr_engine.set_thread_count(4)               # limit processing to 4 CPU cores
ocr_engine.set_memory_limit(512 * 1024 * 1024)  # 512 MB internal buffer
```

> **Warum 4 Threads?** Die meisten modernen Laptops haben mindestens vier Kerne, und das Begrenzen der Thread‑Anzahl verhindert, dass der OCR‑Prozess die gesamte Maschine beansprucht – besonders nützlich, wenn das Skript auf einem gemeinsam genutzten Server läuft.

Wenn Sie eine andere Sprache benötigen, ersetzen Sie einfach `ocr.Language.ENGLISH` durch `ocr.Language.FRENCH`, `ocr.Language.SPANISH` usw.

---

## Schritt 3: Bild für OCR laden (Load Image for OCR)

Jetzt **laden wir das Bild für OCR**. Die Methode `Image.load` liest die TIFF‑Datei in den Speicher und verarbeitet mehrseitige Dokumente automatisch.

```python
# Step 3: Load the TIFF image you want to process
image_path = "YOUR_DIRECTORY/big_document.tif"
image = Image.load(image_path)   # load image for OCR
```

*Randfall:* Wenn die Datei sehr groß ist, könnte Ihnen der Arbeitsspeicher ausgehen. In diesem Fall sollten Sie erwägen, Seite für Seite mit `Image.load_page(page_number)` zu laden (sofern die Bibliothek das unterstützt).

---

## Schritt 4: OCR auf Dokument ausführen

Mit der bereitstehenden Engine und dem geladenen Bild ist es Zeit, **OCR auf dem Dokument auszuführen**. Die Methode `process` übernimmt die schwere Arbeit und gibt ein Ergebnisobjekt zurück.

```python
# Step 4: Execute OCR
ocr_result = ocr_engine.process(image)
```

Im Hintergrund teilt die Engine das Bild in Textblöcke, führt das Erkennungsmodell aus und fügt die Ergebnisse zusammen. Der Aufruf ist blockierend, das heißt, das Skript wartet, bis das gesamte TIFF verarbeitet ist – ideal für Batch‑Jobs.

---

## Schritt 5: Text aus TIFF extrahieren und Ausgabe überprüfen

Abschließend **extrahieren wir Text aus dem TIFF**, indem wir auf das Attribut `text` des Ergebnisses zugreifen. Lassen Sie uns die ersten 200 Zeichen als schnelle Plausibilitätsprüfung ausgeben.

```python
# Step 5: Show a preview of the recognized text
preview = ocr_result.text[:200]   # first 200 characters
print("Preview of OCR output:\n", preview)
```

**Erwartete Ausgabe (Beispiel):**

```
Preview of OCR output:
 In the United States, the Constitution guarantees the ...
```

Wenn Sie den gesamten Text benötigen, verwenden Sie einfach `ocr_result.text`. Für die Weiterverarbeitung möchten Sie ihn vielleicht in eine `.txt`‑Datei schreiben:

```python
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(ocr_result.text)
```

---

## Vollständiges funktionierendes Beispiel

Alles zusammengefügt, hier ein einsatzbereites Skript. Ersetzen Sie den Platzhalter‑Paketnamen durch den, den Sie tatsächlich installiert haben.

```python
# -*- coding: utf-8 -*-
"""
How to Perform OCR on a TIFF Document – Complete Example
"""

# Install the OCR library first:
# pip install ocr-engine   # adjust to your actual package

import ocr
from ocr import OcrEngine, Image

def main():
    # 1️⃣ Initialize and configure the engine
    engine = OcrEngine()
    engine.language = ocr.Language.ENGLISH
    engine.set_thread_count(4)
    engine.set_memory_limit(512 * 1024 * 1024)

    # 2️⃣ Load the TIFF image
    img_path = "YOUR_DIRECTORY/big_document.tif"
    img = Image.load(img_path)

    # 3️⃣ Run OCR on the loaded image
    result = engine.process(img)

    # 4️⃣ Show a short preview and save the full text
    print("First 200 chars of OCR output:")
    print(result.text[:200])

    with open("extracted_text.txt", "w", encoding="utf-8") as out_file:
        out_file.write(result.text)

    print("\n✅ Extraction complete – see 'extracted_text.txt' for full output.")

if __name__ == "__main__":
    main()
```

Führen Sie das Skript aus mit:

```bash
python ocr_tiff_example.py
```

Sie sollten eine Vorschau in der Konsole sehen und eine Datei namens `extracted_text.txt`, die die vollständige Transkription enthält.

---

## Häufige Fragen & Randfälle

- **Was ist, wenn das TIFF mehrere Seiten enthält?**  
  Die meisten OCR‑Engines behandeln jede Seite intern als separates Bild. `ocr_result.text` enthält einen Zeilenumbruch zwischen den Seiten. Wenn Sie eine pro‑Seite‑Verarbeitung benötigen, iterieren Sie mit `Image.load_page(page_number)`.

- **Kann ich stattdessen ein PNG oder JPEG verarbeiten?**  
  Absolut. Die Methode `Image.load` akzeptiert in der Regel jedes von Pillow oder der zugrunde liegenden Bibliothek unterstützte Format. Ändern Sie einfach die Dateierweiterung.

- **Mein Text ist verzerrt – sollte ich die Sprache ändern?**  
  Ja. Der Schritt **set OCR language** ist entscheidend für Nicht‑Englisch‑Dokumente. Stellen Sie sicher, dass das Sprachpaket installiert ist (z. B. `tesseract‑lang‑fra` für Französisch).

- **Läuft der Speicher aus?**  
  Reduzieren Sie `set_memory_limit` oder verarbeiten Sie Seiten einzeln. Einige Engines erlauben zudem das Herunterskalieren des Bildes vor der Erkennung.

---

## Fazit

Damit haben Sie – ein kompakter, voll funktionsfähiger Leitfaden, wie man **OCR** auf einer TIFF‑Datei mit Python durchführt. Wir haben alles behandelt, von der Installation der Bibliothek, der Konfiguration der Engine (einschließlich **set OCR language**), **load image for OCR**, **run OCR on document** und schließlich **extract text from tiff**.

Fühlen Sie sich frei zu experimentieren: Passen Sie die Thread‑Anzahl an, wechseln Sie die Sprache oder leiten Sie die OCR‑Ausgabe in eine Natural‑Language‑Pipeline weiter. Der Himmel ist die Grenze, sobald Sie die Grundlagen beherrschen.

Haben Sie weitere Fragen? Hinterlassen Sie unten einen Kommentar, und viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}