---
category: general
date: 2026-06-19
description: Wie man PDFs mit OCR in Python extrahiert – Schritt‑für‑Schritt‑Tutorial
  zur Textextraktion aus PDFs, Texterkennung aus Bildern und ein OCR‑Python‑Beispiel.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize text from image
- ocr python example
- read pdf with ocr
language: de
og_description: Wie man PDFs mit OCR in Python extrahiert. Lernen Sie, Text aus PDFs
  zu extrahieren, Text aus Bildern zu erkennen, und sehen Sie ein komplettes OCR-Python-Beispiel.
og_title: Wie man PDF-Text mit OCR in Python extrahiert – Vollständiges Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  headline: How to Extract PDF Text with OCR in Python – Complete Guide
  type: TechArticle
- description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  name: How to Extract PDF Text with OCR in Python – Complete Guide
  steps:
  - name: – Install the Required Packages
    text: First, we need an OCR engine. The example below uses the popular **ocr**
      package (a thin wrapper around Tesseract). If you prefer a different backend,
      the concepts stay the same.
  - name: – Initialize the OCR Engine and Set Language
    text: Now we spin up the engine and tell it to look for English characters. You
      can swap `ocr.Language.English` for any supported language code.
  - name: – Load a PDF Page as an Image
    text: OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper
      renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based
      indexing).
  - name: – Recognize Text from the Rendered Image
    text: Here’s the heart of the **ocr python example**. The engine processes the
      bitmap and returns an object containing the extracted string.
  - name: – Print or Store the Extracted Text
    text: Finally, we output the result. In a real application you’d probably write
      to a file or a database.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Wie man PDF‑Text mit OCR in Python extrahiert – Komplettanleitung
url: /de/python-java/general/how-to-extract-pdf-text-with-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man PDF-Text mit OCR in Python – Vollständige Anleitung

Haben Sie sich jemals gefragt, **wie man PDF**‑Inhalte extrahiert, wenn die Datei nur ein gescanntes Bild ist? Sie sind nicht allein. In vielen realen Projekten – denken Sie an Verträge, Rechnungen oder historische Archive – enthält das erhaltene PDF keinen auswählbaren Text. Die gute Nachricht? Ein paar Zeilen Python können diese rein bildbasierten Seiten in durchsuchbaren, editierbaren Text verwandeln.

In diesem Tutorial führen wir Sie durch ein praktisches **OCR Python Beispiel**, das ein PDF einliest, die erste Seite als Bild rendert und dann **Text aus PDF** mithilfe einer OCR‑Engine extrahiert. Am Ende wissen Sie genau, wie man **PDF mit OCR liest**, warum jeder Schritt wichtig ist und wie Sie den Code für mehrseitige Dokumente oder verschiedene Sprachen anpassen können.

## Was Sie lernen werden

- Eine zuverlässige OCR‑Bibliothek für Python installieren und einrichten.
- PDF‑Seiten in für OCR geeignete Bilder konvertieren.
- **Text aus Bild erkennen** und saubere Unicode‑Zeichenketten abrufen.
- Häufige Stolperfallen (PDFs mit niedriger Auflösung, gedrehte Seiten) und wie man sie vermeidet.
- Das Skript erweitern, um mehrere Seiten oder Batch‑Verarbeitung zu unterstützen.

**Voraussetzungen**: Python 3.8+, pip und ein grundlegendes Verständnis von virtuellen Umgebungen. Keine vorherige OCR‑Erfahrung erforderlich – einfach mitmachen.

---

## ## Wie man PDF-Text mit OCR in Python extrahiert

Dieser H2‑Header enthält unser Haupt‑Keyword genau dort, wo Suchmaschinen es lieben. Lassen Sie uns direkt in den Code eintauchen.

### Schritt 1 – Erforderliche Pakete installieren

Zuerst benötigen wir eine OCR‑Engine. Das untenstehende Beispiel verwendet das beliebte **ocr**‑Paket (ein dünner Wrapper um Tesseract). Wenn Sie ein anderes Backend bevorzugen, bleiben die Konzepte gleich.

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR wrapper and Pillow for image handling
pip install ocr pillow
```

> **Pro‑Tipp:** Unter Linux benötigen Sie außerdem das Tesseract‑Binary: `sudo apt-get install tesseract-ocr`. macOS‑Benutzer können es über Homebrew holen: `brew install tesseract`.

### Schritt 2 – OCR‑Engine initialisieren und Sprache festlegen

Jetzt starten wir die Engine und weisen sie an, nach englischen Zeichen zu suchen. Sie können `ocr.Language.English` durch jeden unterstützten Sprachcode ersetzen.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
```

**Warum das wichtig ist:** Die Angabe der Sprache verbessert die Genauigkeit erheblich, da die Engine sprachspezifische Wörterbücher und Zeichenmodelle anwenden kann.

### Schritt 3 – PDF‑Seite als Bild laden

OCR arbeitet mit Rasterbildern, nicht mit PDF‑Objekten. Der Helfer `ocr.Image.from_pdf` rendert die ausgewählte Seite in ein Bitmap. Passen Sie `page_number` für andere Seiten an (0‑basierte Indexierung).

```python
# Step 2: Load the first page of the PDF as an image
pdf_file_path = "YOUR_DIRECTORY/contract.pdf"
page_image = ocr.Image.from_pdf(pdf_file_path, page_number=1)
```

> **Randfall:** Wenn das PDF Vektorgrafiken statt gescannter Bilder enthält, erhalten Sie möglicherweise ein scharfes Rendering. Bei niedrig aufgelösten Scans sollten Sie die DPI erhöhen: `ocr.Image.from_pdf(..., dpi=300)`.

### Schritt 4 – Text aus dem gerenderten Bild erkennen

Hier ist das Herzstück des **ocr python example**. Die Engine verarbeitet das Bitmap und gibt ein Objekt zurück, das die extrahierte Zeichenkette enthält.

```python
# Step 3: Recognize text from the rendered page image
ocr_result = ocr_engine.recognize(page_image)
```

Das Attribut `ocr_result.text` enthält die reine Textausgabe und bewahrt, wo möglich, Zeilenumbrüche.

### Schritt 5 – Extrahierten Text ausgeben oder speichern

Abschließend geben wir das Ergebnis aus. In einer realen Anwendung würden Sie es wahrscheinlich in eine Datei oder Datenbank schreiben.

```python
# Step 4: Print the extracted text
print(ocr_result.text)
```

Das Ausführen des Skripts sollte etwa Folgendes anzeigen:

```
THIS AGREEMENT is made on the 1st day of January 2024...
```

Das ist ein vollständiger **extract text from pdf**‑Workflow mit OCR.

---

## ## Text aus Bild erkennen – Genauigkeit optimieren

Wenn Sie nur an **recognize text from image** interessiert sind (z. B. ein JPEG eines Belegs), können Sie den PDF‑Konvertierungsschritt überspringen:

```python
image_path = "receipt.jpg"
page_image = ocr.Image.from_file(image_path)   # Directly load an image
ocr_result = ocr_engine.recognize(page_image)
print(ocr_result.text)
```

**Tipps für bessere Ergebnisse:**

- **Vorverarbeiten** des Bildes: in Graustufen konvertieren, Schwellenwert anwenden oder entzerren. Pillow macht das einfach.
- **DPI erhöhen** beim PDF‑Rendering: höhere Auflösung liefert der OCR‑Engine mehr Details.
- **OCR‑Engine‑Konfiguration aktivieren** für Seitensegmentierung (`ocr_engine.config = "--psm 6"` für einheitliche Blöcke).

---

## ## PDF mit OCR lesen – Mehrere Seiten verarbeiten

Die meisten Verträge erstrecken sich über mehrere Seiten. Das Durchlaufen jeder Seite ist unkompliziert:

```python
def extract_all_pages(pdf_path):
    all_text = []
    for i in range(ocr.Image.pdf_page_count(pdf_path)):
        img = ocr.Image.from_pdf(pdf_path, page_number=i)
        result = ocr_engine.recognize(img)
        all_text.append(result.text)
    return "\n--- PAGE BREAK ---\n".join(all_text)

full_text = extract_all_pages("YOUR_DIRECTORY/contract.pdf")
print(full_text)
```

Diese Funktion **reads PDF with OCR**, fügt die Ausgabe zusammen und fügt einen klaren Seitenumbruch‑Marker ein. Sie können `full_text` dann in einen Suchindex einspeisen oder als `.txt`‑Datei speichern.

---

## ## Häufige Fallstricke und wie man sie behebt

| Symptom | Wahrscheinliche Ursache | Lösung |
|---------|--------------------------|--------|
| Verzerrte Zeichen, viele `?` | Falsche Sprache oder fehlende Sprachdaten-Dateien | Installieren Sie das richtige Tesseract‑Sprachpaket (`tesseract-ocr-<lang>`) und setzen Sie `ocr_engine.language`. |
| Fehlende Zeilen oder abgeschnittene Wörter | Niedrige DPI (unter 150) | Rendern Sie das PDF mit 300 DPI oder höher (`dpi=300`). |
| Text ist gedreht oder verkehrt herum | Gescannte Seite nicht aufrecht | Verwenden Sie `ocr.Image.deskew(page_image)` vor der Erkennung. |
| Langsame Verarbeitung bei großen PDFs | Seiten werden sequenziell in einem einzelnen Thread verarbeitet | Parallelisieren Sie mit `concurrent.futures.ThreadPoolExecutor`. |

---

## ## Das OCR‑Python‑Beispiel erweitern

- **Export nach PDF/A**: Nach der Extraktion können Sie den Text mit `reportlab` oder `pypdf2` wieder in ein durchsuchbares PDF einbetten.
- **Spracherkennung**: Verwenden Sie `langdetect` auf dem OCR‑Output, um `ocr_engine.language` dynamisch zu wechseln.
- **Batch‑Verarbeitung**: Durchlaufen Sie ein Verzeichnis mit `os.listdir` und wenden Sie `extract_all_pages` auf jede Datei an.

---

## ## Erwartete Ausgabe und Verifizierung

Wenn Sie das Skript gegen einen klaren Scan in englischer Sprache ausführen, sollten Sie einen sauberen Textblock mit korrekter Interpunktion sehen. Überprüfen Sie dies durch:

1. Einige Zeilen mit dem Original‑Scan vergleichen.  
2. Eine einfache Wortzählung ausführen (`len(ocr_result.text.split())`), um sicherzustellen, dass die Ausgabe nicht leer ist.  
3. Optional das Ergebnis in einen Rechtschreibprüfer wie `pyspellchecker` einspeisen, um OCR‑Fehler zu erkennen.

---

## Fazit

Wir haben **wie man PDF**‑Inhalte extrahiert, wenn herkömmliches Parsen scheitert, ein vollständiges **ocr python example** demonstriert und erklärt, wie man **recognize text from image** und **read PDF with OCR** sowohl für einseitige als auch mehrseitige Szenarien durchführt. Mit den obigen Code‑Snippets können Sie nun jedes gescannte PDF in durchsuchbaren, editierbaren Text verwandeln – kein manuelles Abtippen mehr.

Nächste Schritte? Versuchen Sie, die Sprache zu Spanisch zu wechseln (`ocr.Language.Spanish`) oder experimentieren Sie mit Bild‑Vorverarbeitungstechniken, um die Genauigkeit zu erhöhen. Wenn Sie ein Dokumenten‑Management‑System bauen, denken Sie darüber nach, den extrahierten Text mit Elasticsearch für blitzschnelle Suche zu indexieren.

Haben Sie Fragen oder stoßen Sie auf ein eigenartiges PDF? Hinterlassen Sie einen Kommentar und happy coding!  

![Wie man PDF mit OCR in Python extrahiert](image.png "Wie man PDF mit OCR in Python extrahiert")

## Was Sie als Nächstes lernen sollten?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Text aus Bild mit Aspose OCR extrahieren – Schritt‑für‑Schritt‑Anleitung](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [PDF‑Text erkennen – OCR‑Operationen mit Aspose.OCR für Java](/ocr/english/java/ocr-operations/)
- [Bildtext in C# mit Sprachauswahl mithilfe von Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}