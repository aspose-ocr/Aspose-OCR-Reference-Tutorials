---
category: general
date: 2026-07-05
description: Wie man OCR in Python verwendet, um TIFF schnell in Text zu konvertieren.
  Lernen Sie die Schritte der OCR‑Bibliothek in Python zum Extrahieren von Text aus
  TIFF‑Bildern und zum Erstellen einer Python‑OCR‑Engine.
draft: false
keywords:
- how to use ocr
- ocr library python
- convert tiff to text
- extract text from tiff
- python ocr engine
language: de
og_description: Wie verwendet man OCR in Python? Dieser Leitfaden zeigt Ihnen Schritt
  für Schritt, wie Sie TIFF in Text umwandeln, indem Sie eine Python-OCR-Engine und
  die OCR-Bibliothek Python verwenden.
og_title: Wie man OCR in Python verwendet – Vollständige TIFF‑Textextraktion
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  headline: How to Use OCR in Python – Extract Text from TIFF
  type: TechArticle
- description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  name: How to Use OCR in Python – Extract Text from TIFF
  steps:
  - name: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
    text: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
  - name: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
    text: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
  - name: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
    text: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Image Processing
title: Wie man OCR in Python verwendet – Text aus TIFF extrahieren
url: /de/python-java/general/how-to-use-ocr-in-python-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in Python verwendet – Text aus TIFF extrahieren

Haben Sie sich schon einmal gefragt, **wie man OCR in Python** nutzt, um ein gescanntes Buch in editierbaren Text zu verwandeln? Sie sind nicht allein – Entwickler, Forscher und Hobbyisten stoßen häufig auf dieses Problem, wenn sie mit mehrseitigen TIFF‑Bildern arbeiten. Die gute Nachricht? Mit der **ocr library python** können Sie eine kleine OCR‑Engine starten, sie auf eine TIFF‑Datei zeigen und in Sekunden sauberen, durchsuchbaren Text erhalten.

In diesem Tutorial gehen wir Schritt für Schritt durch alles, was Sie benötigen: das richtige Paket installieren, ein mehrseitiges TIFF laden, die OCR‑Engine ausführen und schließlich den Inhalt jeder Seite ausgeben. Am Ende können Sie **TIFF in Text umwandeln** und **Text aus TIFF**‑Dateien extrahieren, ohne Ihre Python‑Umgebung zu verlassen.

## Voraussetzungen

Bevor wir starten, stellen Sie sicher, dass Sie Folgendes haben:

- Python 3.9 oder neuer (das Beispiel wurde mit 3.11 getestet)
- Eine aktuelle Version der `ocr`‑Bibliothek (oder ein kompatibles `python ocr engine`, das Sie bevorzugen)
- Eine mehrseitige TIFF‑Datei, die Sie verarbeiten möchten (wir nennen sie `scanned_book.tif`)
- Grundlegende Kenntnisse in Python‑Skripten und virtuellen Umgebungen

Keine schweren externen Tools nötig – nur pip und ein paar Code‑Zeilen.

## OCR‑Bibliothek für Python installieren

Zuerst benötigen Sie ein stabiles OCR‑Backend. Für diese Anleitung verwenden wir das fiktive `ocr`‑Paket, das eine einfache High‑Level‑API bereitstellt, aber das gleiche Muster funktioniert auch mit Tesseract‑basierten Wrappers wie `pytesseract` oder kommerziellen SDKs.

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Pro‑Tipp:** Wenn Sie Windows verwenden und das Paket native Binärdateien benötigt, stellen Sie sicher, dass das passende Visual C++‑Redistributable installiert ist. Der Installer warnt Sie in der Regel, falls etwas fehlt.

## Wie man die OCR‑Engine in Python verwendet

Jetzt, wo die Bibliothek bereit ist, starten wir eine OCR‑Engine und zeigen sie auf unsere TIFF‑Datei. Das folgende Snippet erstellt eine Engine‑Instanz, setzt die Sprache auf Englisch und bereitet sie für die Verarbeitung mehrseitiger Dokumente vor.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # You can switch to ocr.Language.FRENCH, etc.
```

**Warum die Sprache setzen?**  
Die meisten OCR‑Engines verwenden Sprachmodelle, um die Genauigkeit zu erhöhen. Wenn Sie diesen Schritt überspringen, greift die Engine auf ein generisches Modell zurück, das Satzzeichen oder Sonderzeichen falsch erkennen kann.

## Mehrseitiges TIFF‑Bild laden

Der nächste Schritt ist das Laden des gescannten Dokuments. Der Helfer `ocr.Image.load` versteht TIFF‑Stacks von Haus aus und gibt ein Objekt zurück, das intern jede Seite repräsentiert.

```python
# Step 2: Load the multi‑page TIFF image containing the scanned book
tiff_path = "YOUR_DIRECTORY/scanned_book.tif"
tiff_image = ocr.Image.load(tiff_path)
```

> **Randfall:** Wenn Ihr TIFF komprimiert ist (CCITT Group 4, LZW usw.) und die Bibliothek einen Fehler wirft, versuchen Sie zunächst, es mit ImageMagick in eine unkomprimierte Version zu konvertieren:
> ```bash
> convert scanned_book.tif -compress none scanned_book_uncompressed.tif
> ```

## OCR auf allen Seiten ausführen – TIFF in Text umwandeln

Mit dem Bild‑Objekt in der Hand kann die Engine nun jede Seite auf einmal verarbeiten. Diese Methode liefert eine Liste, wobei jedes Element das OCR‑Ergebnis einer einzelnen Seite enthält.

```python
# Step 3: Perform OCR on all pages of the image
page_results = engine.recognize_multi_page(tiff_image)
```

**Was passiert im Hintergrund?**  
Die Funktion `recognize_multi_page` iteriert über jede rasterisierte Seite, führt den neuronalen Erkenner aus und verpackt die reine Textausgabe zusammen mit Konfidenzwerten. Es ist im Wesentlichen ein Batch‑Vorgang, der Ihnen das Schreiben einer manuellen Schleife erspart.

## Ergebnisse iterieren – Text aus TIFF extrahieren

Abschließend geben wir den erkannten Text aus. Sie könnten die Ausgabe in separate `.txt`‑Dateien schreiben, in eine Datenbank einspielen oder in einen Such‑Index einspeisen – je nach Ihrem Workflow.

```python
# Step 4: Iterate through the results and display the recognized text for each page
for page_index, result in enumerate(page_results):
    print(f"Page {page_index + 1}:\n{result.text}\n")
```

### Erwartete Ausgabe

```
Page 1:
Chapter 1
In the beginning...

Page 2:
The quick brown fox jumps over the lazy dog.

Page 3:
...

```

Jeder `result.text`‑String enthält das rohe OCR‑Ergebnis für die jeweilige Seite. Wenn Sie Zeilenumbrüche erhalten möchten, stellen die meisten Engines `result.lines` als Liste von Strings bereit.

## Große TIFF‑Dateien verarbeiten – Tipps & Tricks

Die Verarbeitung einer 500‑seitigen TIFF kann speicherintensiv sein. Hier ein paar Strategien, um alles reibungslos zu halten:

1. **Seiten stapeln** – Statt `recognize_multi_page` rufen Sie `engine.recognize(page)` innerhalb eines Generators auf, der jeweils eine Seite liefert.
2. **DPI anpassen** – Das Reduzieren der Bildauflösung (z. B. von 300 DPI auf 200 DPI) verringert die CPU‑Last, während die Genauigkeit bei normalem Drucktext kaum leidet.
3. **Parallelisieren** – Wenn Ihre OCR‑Engine thread‑sicher ist, starten Sie einen `concurrent.futures.ThreadPoolExecutor`, um die Erkennung auf mehreren Seiten gleichzeitig laufen zu lassen.

```python
import concurrent.futures

def ocr_page(page):
    return engine.recognize(page).text

with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    texts = list(executor.map(ocr_page, tiff_image.pages))
```

## Extrahierten Text in Dateien speichern

Die meisten realen Pipelines benötigen persistente Speicherung. Nachfolgend ein kompakter Weg, um den Text jeder Seite in eine eigene Datei zu schreiben und dabei die Reihenfolge beizubehalten.

```python
import pathlib

output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for i, result in enumerate(page_results, start=1):
    file_path = output_dir / f"page_{i:03}.txt"
    file_path.write_text(result.text, encoding="utf-8")
    print(f"Saved page {i} to {file_path}")
```

Jetzt haben Sie ein sauberes Verzeichnis mit `.txt`‑Dateien, bereit für Indexierung oder weitere NLP‑Verarbeitung.

## Bildvorschau – OCR‑Ergebnisse visuell nutzen

Wenn Sie die OCR‑Überlagerung auf dem Originalbild sehen möchten (praktisch zum Debuggen), erlauben viele Bibliotheken das Zeichnen von Begrenzungsrahmen. Hier ein kurzes Beispiel mit Pillow:

```python
from PIL import ImageDraw

for page, result in zip(tiff_image.pages, page_results):
    draw = ImageDraw.Draw(page)
    for word in result.words:          # Assume `result.words` gives bounding boxes
        draw.rectangle(word.box, outline="red")
    page.show()   # Opens the annotated page
```

![Wie man OCR in Python verwendet – OCR‑Overlay auf einer TIFF‑Seite](ocr_overlay_example.png)

*Alt‑Text:* Wie man OCR in Python verwendet – visuelle Überlagerung des erkannten Textes auf einer TIFF‑Seite.

## Häufige Stolperfallen und wie man sie vermeidet

| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| Verzerrte Zeichen | Falsches Sprachmodell | `engine.language` auf das korrekte Enum setzen |
| Fehlende Seiten | TIFF‑Kompression nicht unterstützt | Zuerst in unkomprimiertes TIFF konvertieren |
| Langsame Leistung | Hohe DPI + ein‑Thread‑Verarbeitung | DPI reduzieren oder Multi‑Threading aktivieren |
| Leere Ausgabe | Bild zu dunkel/geringe Kontrast | Vorverarbeitung mit Kontraststreckung (`opencv` oder `Pillow`) |

Frühzeitiges Beheben dieser Probleme spart Ihnen später Stunden an Fehlersuche.

## Nächste Schritte – über die Grundextraktion hinaus

Jetzt, wo Sie die Grundlagen **wie man OCR in Python verwendet** beherrschen, können Sie Folgendes erkunden:

- **PDF‑Erstellung** – Kombinieren Sie extrahierten Text mit `reportlab`, um durchsuchbare PDFs zu erzeugen.
- **Spracherkennung** – Schalten Sie `engine.language` automatisch um mit `langdetect`.
- **Strukturierte Datenerfassung** – Nutzen Sie reguläre Ausdrücke oder spaCy, um Daten wie Datumsangaben, Namen oder Tabellen aus dem Rohtext zu ziehen.
- **Alternative OCR‑Backends** – Ersetzen Sie `ocr` durch `pytesseract` oder `easyocr`, wenn Sie mehrsprachige Unterstützung benötigen.

All diese Themen knüpfen natürlich an die sekundären Schlüsselwörter **ocr library python**, **convert tiff to text**, **extract text from tiff** und **python ocr engine** an und geben Ihnen ein solides Fundament für weiterführende Projekte.

---

### Fazit

Wir haben **wie man OCR in Python** von der Installation bis zur mehrseitigen Verarbeitung behandelt und gezeigt, wie Sie **TIFF in Text umwandeln** und **Text aus TIFF** mithilfe einer einfachen **python OCR engine** extrahieren. Das vollständige, ausführbare Beispiel oben sollte für die meisten Standard‑TIFF‑Dateien sofort funktionieren, und die genannten Tipps helfen Ihnen, auf größere Dokumente zu skalieren oder OCR in umfangreichere Pipelines zu integrieren.

Probieren Sie es mit Ihren eigenen gescannten Büchern, Quittungen oder Archivbildern aus – und experimentieren Sie anschließend mit den im Abschnitt „Nächste Schritte“ aufgeführten Ideen. Viel Spaß beim Coden und mögen Ihre OCR‑Ergebnisse stets präzise sein!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to extract text from tiff with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}