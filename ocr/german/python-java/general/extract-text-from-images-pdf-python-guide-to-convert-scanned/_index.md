---
category: general
date: 2026-06-06
description: Extrahiere Text aus Bild‑PDFs mit Python OCR. Lerne, wie du gescannte
  Dokumente schnell in Text umwandeln kannst, mit asynchroner Batch‑Erkennung.
draft: false
keywords:
- extract text from images pdf
- convert scanned documents to text
- python ocr batch processing
- asynchronous OCR python
- image to text conversion
language: de
og_description: Extrahiere Text aus Bild‑PDFs mit Python. Diese Schritt‑für‑Schritt-Anleitung
  zeigt, wie man gescannte Dokumente mit asynchroner OCR in Text umwandelt.
og_title: Text aus Bild‑PDFs extrahieren – Python OCR‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from images pdf using Python OCR. Learn how to convert
    scanned documents to text quickly with async batch recognition.
  headline: Extract Text from Images PDF – Python Guide to Convert Scanned Documents
    to Text
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Text aus Bild‑PDFs extrahieren – Python‑Leitfaden zum Konvertieren gescannter
  Dokumente in Text
url: /de/python-java/general/extract-text-from-images-pdf-python-guide-to-convert-scanned/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bild‑PDFs extrahieren – Python‑Leitfaden zum Konvertieren gescannter Dokumente in Text

Haben Sie jemals **Text aus Bild‑PDFs extrahieren** müssen, ohne stundenlang abzutippen? In diesem Leitfaden zeigen wir Ihnen, wie Sie **gescannte Dokumente in Text konvertieren** können, indem Sie einen einfachen asynchronen OCR‑Workflow in Python verwenden.  

Wenn Sie jemals auf einen Stapel gescannter PDFs gestarrt haben und dachten: „Da muss es doch einen schnelleren Weg geben“, dann sind Sie hier genau richtig. Wir gehen jede Codezeile durch, erklären, warum jedes Teil wichtig ist, und behandeln sogar einige Randfälle, auf die Sie stoßen könnten.

## Was Sie lernen werden

- Wie man eine OCR‑Engine startet und die Erkennungssprache festlegt.  
- Die Funktionsweise, eine gemischte Liste aus PNGs und PDFs an einen Batch‑Recognizer zu übergeben.  
- Wie man den OCR‑Job asynchron ausführt, damit Ihre Anwendung reaktionsfähig bleibt.  
- Wie man die Ergebnisse abruft, sie den Quelldateien zuordnet und eine saubere Ausgabe druckt.  

**Voraussetzungen**: Python 3.8+, ein grundlegendes Verständnis von `asyncio` oder `concurrent.futures` und eine OCR‑Bibliothek, die eine `OcrEngine`‑Klasse ähnlich der im Beispiel bereitstellt (z. B. Aspose.OCR, Tesseract‑Wrapper oder ein benutzerdefinierter Wrapper). Keine aufwändige Einrichtung nötig – einfach die Bibliothek installieren und Sie können loslegen.

![Text aus Bild‑PDFs extrahieren](https://example.com/placeholder.png "Screenshot der OCR‑Ausgabe – Text aus Bild‑PDFs extrahieren")

## Text aus Bild‑PDFs extrahieren – Einrichtung der OCR‑Engine

Das Erste, was Sie benötigen, ist eine OCR‑Engine‑Instanz, die für die Sprache Ihrer Dokumente konfiguriert ist. In unserem Fall verwenden wir Französisch, aber Sie können sie durch jede unterstützte Sprache ersetzen.

```python
# Import the OCR library – replace with your actual import
from ocr import OcrEngine, Language

# Step 1: Create and configure the OCR engine
engine = OcrEngine()
engine.set_recognition_language(Language.FRENCH)   # Change to Language.ENGLISH, etc.
```

**Warum das wichtig ist**: Die Festlegung der Sprache im Voraus verbessert die Genauigkeit erheblich. Die Engine nutzt sprachspezifische Wörterbücher und Zeichenmodelle; die falsche Sprache zu verwenden ist eine häufige Ursache für fehlerhafte Ausgaben.

## Dateiliste vorbereiten – Bilder und PDFs zusammen

Unser Batch‑Recognizer kann sowohl Rasterbilder (`.png`, `.jpg`) als auch PDF‑Container verarbeiten. Geben Sie einfach eine einfache Python‑Liste von Dateipfaden ein.

```python
# Step 2: Define the files to be processed (use your own directory)
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.pdf"
]
```

**Tipp**: Halten Sie die Liste flach; die Engine wird intern jede PDF‑Seite in Bilder entpacken, bevor sie erkannt wird. Wenn Sie tausende Dateien haben, sollten Sie die Liste in kleinere Batches aufteilen, um Speicher‑Spitzen zu vermeiden.

## Asynchrone Batch‑Erkennung starten

Anstatt den Haupt‑Thread zu blockieren, starten wir den OCR‑Job im Hintergrund. Die Methode gibt ein `Future` zurück, das schließlich eine Liste von `OcrResult`‑Objekten enthält.

```python
# Step 3: Start asynchronous batch recognition
future = engine.recognize_batch_async(files)   # returns a Future[List[OcrResult]]
```

**Wie es funktioniert**: Unter der Haube startet die Engine einen Thread‑Pool (oder eine async‑Aufgabe, je nach Implementierung). Das ermöglicht Ihnen, andere Arbeiten fortzusetzen – z. B. eine UI zu aktualisieren, weitere Dateien zu holen oder den Fortschritt zu protokollieren – während die schwere Arbeit im Hintergrund läuft.

## Etwas Nützliches tun, während OCR läuft

Ein häufiger Fehler ist, untätig zu warten und das Future in einer engen Schleife abzufragen. Stattdessen können Sie beliebige andere Arbeiten ausführen. Zur Demonstration geben wir einfach eine Statuszeile aus.

```python
# Step 4: Perform other work while OCR runs
print("Batch started – doing other work...")
# Imagine you could be uploading files, sending heartbeats, etc.
```

## Ergebnisse sammeln, sobald das Future abgeschlossen ist

Wenn Sie bereit sind, die OCR‑Ausgabe zu sammeln, verwenden Sie `as_completed` aus `concurrent.futures`. Dieses Muster funktioniert sowohl bei einem einzelnen Future als auch bei vielen.

```python
from concurrent.futures import as_completed

# Step 5: Wait for the batch to finish and retrieve the results
for completed in as_completed([future]):
    ocr_results = completed.result()   # List[OcrResult] in the same order as `files`
    for path, result in zip(files, ocr_results):
        print(f"{path} →\n{result.text}\n")
```

**Was Sie sehen werden**: Jeder Dateipfad gefolgt von der extrahierten Klartext‑Darstellung. Für PDFs enthält `result.text` den zusammengefügten Text aller Seiten.

### Erwartete Ausgabe (Beispiel)

```
YOUR_DIRECTORY/doc1.png →
Bonjour, ceci est un test d’OCR.

YOUR_DIRECTORY/doc2.png →
Le texte de la deuxième image apparaît ici.

YOUR_DIRECTORY/doc3.pdf →
Page 1 du PDF : Lorem ipsum dolor sit amet…
Page 2 du PDF : Consectetur adipiscing elit…
```

Falls Sie fehlende Zeichen bemerken, prüfen Sie, ob die eingestellte Sprache mit der Dokumentensprache übereinstimmt, und erwägen Sie, die Bilder vorzuverarbeiten (Entzerrung, Kontrast erhöhen), bevor Sie sie an die Engine übergeben.

## Umgang mit Randfällen und häufigen Stolperfallen

| Situation | Vorgehensweise |
|-----------|----------------|
| **Gemischte Sprachen** | Führen Sie zuerst einen Sprach‑Erkennungsschritt durch und erstellen Sie dann separate Engines pro Sprache. |
| **Große PDFs (> 100 MB)** | Teilen Sie das PDF in einzelne Seiten auf der Festplatte (z. B. mit `PyPDF2`) und geben Sie sie als separate Einträge ein. |
| **Nicht‑lateinische Schriften** | Stellen Sie sicher, dass die OCR‑Bibliothek das benötigte Sprachpaket enthält; einige Bibliotheken erfordern das Herunterladen zusätzlicher Datendateien. |
| **Leistungsengpass** | Erhöhen Sie die Thread‑Pool‑Größe (`engine.set_thread_pool_size(8)`) oder wechseln Sie zu einem GPU‑beschleunigten Backend, falls verfügbar. |
| **Fehlender Text in niedrigauflösenden Bildern** | Vorverarbeiten mit OpenCV: `cv2.resize`, `cv2.threshold` und `cv2.medianBlur`, um die Lesbarkeit zu verbessern. |

## Vollständiges funktionierendes Beispiel (Copy‑Paste‑bereit)

```python
# ------------------------------------------------------------
# Full script: extract text from images pdf – async OCR batch
# ------------------------------------------------------------
import os
from concurrent.futures import as_completed
# Replace the import below with the actual OCR library you use
from ocr import OcrEngine, Language, OcrResult

def main():
    # 1️⃣ Initialize OCR engine
    engine = OcrEngine()
    engine.set_recognition_language(Language.FRENCH)   # Change as needed

    # 2️⃣ Build list of files (images + PDFs)
    base_dir = "YOUR_DIRECTORY"
    files = [
        os.path.join(base_dir, "doc1.png"),
        os.path.join(base_dir, "doc2.png"),
        os.path.join(base_dir, "doc3.pdf")
    ]

    # 3️⃣ Launch async batch recognition
    future = engine.recognize_batch_async(files)

    # 4️⃣ Do other work – here we just print a placeholder
    print("Batch started – doing other work...")

    # 5️⃣ Retrieve results when ready
    for completed in as_completed([future]):
        ocr_results = completed.result()   # List[OcrResult]
        for path, result in zip(files, ocr_results):
            print(f"{path} →\n{result.text}\n")

if __name__ == "__main__":
    main()
```

Speichern Sie dies als `extract_text_async.py`, ersetzen Sie `YOUR_DIRECTORY` durch den Pfad zu Ihren Dateien, installieren Sie das OCR‑Paket (`pip install your-ocr-lib`) und führen Sie `python extract_text_async.py` aus. Sie sollten die zuvor gezeigte Konsolenausgabe sehen.

## Nächste Schritte – über die Grundextraktion hinaus

- **Nachbearbeitung**: Entfernen Sie überflüssige Leerzeichen, normalisieren Sie Unicode (`unicodedata.normalize`) oder führen Sie eine Rechtschreibprüfung durch, um OCR‑Rauschen zu bereinigen.  
- **Strukturierte Ausgabe**: Exportieren Sie die Ergebnisse nach CSV, JSON oder direkt in eine Datenbank für nachgelagerte Suche.  
- **Parallele Batches**: Wenn Sie Hunderte von Dateien haben, starten Sie mehrere Futures und verwenden Sie eine Warteschlange, um die CPU auszulasten, ohne den Speicher zu überlasten.  
- **Integration in Web‑Frameworks**: Binden Sie dieses Skript in einen Flask‑ oder FastAPI‑Endpoint ein, um OCR‑On‑Demand als Service bereitzustellen.

---

### TL;DR

Sie wissen jetzt, wie man **Text aus Bild‑PDFs extrahiert** mit einem minimalen Python‑Skript, das OCR asynchron ausführt, sodass Sie **gescannte Dokumente in Text konvertieren** können, während Ihr Programm reaktionsfähig bleibt. Experimentieren Sie mit den Spracheinstellungen, Batch‑Größen und Vorverarbeitungstricks, um jede noch so kleine Zeichen‑Genauigkeit herauszuholen.

Haben Sie eine Variante, die Sie teilen möchten – vielleicht OCR für handgeschriebene Notizen oder einen cloud‑basierten Dienst? Hinterlassen Sie einen Kommentar und viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Text aus Bild mit Aspose OCR extrahieren – Schritt‑für‑Schritt‑Leitfaden](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Text aus Bildern mit OCR‑Operation in Ordnern extrahieren](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Text aus Bildern mit Aspose.OCR extrahieren – Erlaubte Zeichen](/ocr/english/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}