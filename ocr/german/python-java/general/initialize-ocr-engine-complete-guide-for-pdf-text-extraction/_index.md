---
category: general
date: 2026-06-25
description: Initialisiere die OCR‑Engine in Python, um Text aus mehrseitigen PDFs
  mithilfe benutzerdefinierter Wörterbücher, Spracheinstellungen und Regionsauswahl
  zu extrahieren.
draft: false
keywords:
- initialize OCR engine
- configure OCR language
- OCR image preprocessing
- OCR custom dictionary
- recognize multi-page PDF
language: de
og_description: Initialisiere die OCR-Engine in Python, um vietnamesische PDFs zuverlässig
  zu lesen, konfiguriere Sprache, Vorverarbeitung und benutzerdefiniertes Wörterbuch
  für genaue Ergebnisse.
og_title: OCR-Engine initialisieren – Schritt‑für‑Schritt‑Anleitung zur PDF‑Extraktion
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Initialize OCR engine in Python to extract text from multi‑page PDFs
    using custom dictionaries, language settings, and region targeting.
  headline: Initialize OCR Engine – Complete Guide for PDF Text Extraction
  type: TechArticle
- description: Initialize OCR engine in Python to extract text from multi‑page PDFs
    using custom dictionaries, language settings, and region targeting.
  name: Initialize OCR Engine – Complete Guide for PDF Text Extraction
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed. - An OCR library that exposes an `OcrEngine` class
      (the sample uses a hypothetical `ocr` package; replace with your actual SDK).
      - A sample multi‑page PDF (`sample.pdf`) placed in a known directory. - Basic
      familiarity with Python dictionaries and loops.'
  - name: Pro tip
    text: If you ever need to support multiple languages in the same run, you can
      switch `ocr_engine.language` on the fly before processing each page. Just remember
      to re‑initialize any heavy models if the SDK requires it.
  - name: Expected Output
    text: 'Running the script against a three‑page invoice PDF might produce:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: OCR-Engine initialisieren – Vollständiger Leitfaden zur PDF-Text-Extraktion
url: /de/python-java/general/initialize-ocr-engine-complete-guide-for-pdf-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR-Engine initialisieren – Vollständige Anleitung zur PDF-Text-Extraktion

Haben Sie schon einmal **eine OCR-Engine** für einen Stapel vietnamesischer Rechnungen initialisieren müssen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein. In vielen realen Projekten ist das erste Hindernis, die OCR‑Bibliothek mit Ihren PDFs zum Laufen zu bringen, besonders wenn Sie Sprache, Vorverarbeitung oder ein benutzerdefiniertes Wörterbuch anpassen müssen.  

In diesem Leitfaden gehen wir Schritt für Schritt durch ein vollständiges, ausführbares Beispiel, das zeigt, wie Sie **die OCR-Engine initialisieren**, die Sprache konfigurieren, intelligente Bild‑Vorverarbeitung aktivieren, ein benutzerdefiniertes Wörterbuch hinzufügen und schließlich strukturierte Daten aus jeder Seite eines mehrseitigen PDFs extrahieren. Am Ende haben Sie ein eigenständiges Skript, das Sie in Ihr eigenes Projekt einbinden können – ohne fehlende Teile, ohne „siehe Dokumentation“-Abkürzungen.

## Was Sie lernen werden

- Wie man **die OCR-Engine** mit Unterstützung der vietnamesischen Sprache **initialisiert**.  
- Warum **die OCR‑Sprache konfigurieren** für die Genauigkeit wichtig ist.  
- Verwendung von **OCR‑Bild‑Vorverarbeitungs‑Optionen** wie Auto‑Deskew und Auto‑Binarize.  
- Hinzufügen eines **OCR‑benutzerdefinierten Wörterbuchs**, um die Erkennung domänenspezifischer Begriffe zu verbessern.  
- **Mehrseitige PDF‑Dateien erkennen** und einen bestimmten Bereich (z. B. Gesamtbetrag) extrahieren.  
- Die rohen Ergebnisse in eine saubere JSON‑ähnliche Struktur für nachgelagerte Verarbeitung umwandeln.

### Voraussetzungen

- Python 3.8+ installiert.  
- Eine OCR‑Bibliothek, die eine `OcrEngine`‑Klasse bereitstellt (das Beispiel verwendet ein hypothetisches `ocr`‑Package; ersetzen Sie es durch Ihr tatsächliches SDK).  
- Ein Beispiel‑Mehrseiten‑PDF (`sample.pdf`) in einem bekannten Verzeichnis.  
- Grundlegende Kenntnisse von Python‑Dictionaries und Schleifen.

Wenn Sie das haben, legen wir los.

---

## Schritt 1: Wie man die OCR‑Engine in Python initialisiert

Das allererste, was Sie tun müssen, ist **die OCR‑Engine zu initialisieren**. Denken Sie daran wie das Einschalten einer Maschine und das Angeben der Sprache, die Sie ihr zufüttern werden.

```python
import ocr  # Replace with your actual OCR package

# Create the engine instance
ocr_engine = ocr.OcrEngine()

# Set the language to Vietnamese – this tells the engine which character set to expect
ocr_engine.language = ocr.Language.Vietnamese
```

> **Warum das wichtig ist:**  
> Die meisten OCR‑Engines werden mit generischen Sprachpaketen ausgeliefert. Durch das explizite Setzen von `ocr_engine.language` verhindern Sie, dass die Engine falsche Zeichen errät, was die Fehlerrate bei diakritischen Zeichen im Vietnamesischen drastisch reduziert.

### Pro‑Tipp
Falls Sie mehrere Sprachen im selben Durchlauf unterstützen müssen, können Sie `ocr_engine.language` on the fly vor der Verarbeitung jeder Seite umschalten. Denken Sie nur daran, schwere Modelle neu zu initialisieren, falls das SDK dies erfordert.

---

## Schritt 2: OCR‑Bild‑Vorverarbeitungs‑Optionen aktivieren

Roh‑Scans sind selten perfekt. Schiefe Seiten, ungleichmäßige Beleuchtung oder geringer Kontrast können selbst die besten Erkenner aus dem Konzept bringen. Deshalb **konfigurieren wir die OCR‑Bild‑Vorverarbeitung** gleich nach der Initialisierung.

```python
ocr_engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,      # Auto‑rotate to correct tilt
    auto_binarize=True    # Convert to black‑and‑white for sharper edges
)
```

Diese beiden Flags reichen oft aus, um die meisten gescannten Rechnungen zu säubern. Wenn Ihre Quell‑PDFs bereits von hoher Qualität sind, können Sie sie deaktivieren, um ein paar Millisekunden pro Seite zu sparen.

---

## Schritt 3: Ein OCR‑benutzerdefiniertes Wörterbuch hinzufügen

Domänenspezifische Begriffe – wie Bestellcodes, Produkt‑IDs oder juristische Abkürzungen – erscheinen selten in generischen Sprachmodellen. Durch das Einbinden eines **OCR‑benutzerdefinierten Wörterbuchs** geben Sie der Engine ein Spickzettel.

```python
ocr_engine.custom_dictionary = ["MãĐơnHàng", "KháchHàng", "SốTiền"]
```

> **Was passiert im Hintergrund?**  
> Die Engine erhöht die Confidence‑Scores für jedes Wort, das in dieser Liste vorkommt, sodass es viel weniger wahrscheinlich ist, als etwas anderes missinterpretiert zu werden.

---

## Schritt 4: Mehrseitige PDF‑Datei erkennen – gesamten Text auf einmal holen

Jetzt, wo die Engine vollständig konfiguriert ist, können wir **mehrseitige PDF‑Dateien erkennen**. Die Methode `recognize_multi_page` liefert eine Liste, bei der jedes Element eine einzelne, bereits OCR‑verarbeitete Seite repräsentiert.

```python
pdf_path = "YOUR_DIRECTORY/sample.pdf"
pages = ocr_engine.recognize_multi_page(pdf_path)
```

Falls Sie mit riesigen PDFs (Hunderte Seiten) arbeiten, sollten Sie sie in Chunks verarbeiten, um den Speicherverbrauch gering zu halten. Das SDK bietet hierfür meist eine Streaming‑API.

---

## Schritt 5: Einen bestimmten Bereich aus jeder Seite extrahieren

Die meisten Rechnungen besitzen ein Feld „Gesamtbetrag“, das an derselben Stelle auf jeder Seite zu finden ist. Statt den gesamten Seiten‑Text zu parsen, können wir die Engine anweisen, sich auf ein Rechteck zu konzentrieren.

```python
from ocr import Rectangle  # Adjust import based on your SDK

for page_index, page in enumerate(pages, start=1):
    # Define the rectangle (x, y, width, height) that encloses the total amount
    total_region = Rectangle(400, 650, 200, 50)

    # Run OCR only on that region
    region_result = ocr_engine.recognize_region(page.image, total_region)
```

> **Warum ein Ziel‑Region wählen?**  
> Die Beschränkung der OCR auf einen kleinen Bereich beschleunigt die Verarbeitung und reduziert Fehlalarme, besonders wenn der Rest der Seite verrauscht ist.

---

## Schritt 6: Ein JSON‑ähnliches Dictionary für jede Seite zusammenstellen

Der rohe Text ist nützlich, aber nachgelagerte Systeme erwarten meist strukturierte Daten. Im Folgenden bauen wir ein sauberes Dictionary, das die Seitennummer, den gesamten Seitentext, den extrahierten Gesamtbetrag und eine Liste aller erkannten Wörter mit Confidence‑Scores enthält.

```python
    page_output = {
        "page": page_index,
        "full_text": page.text,
        "total_amount": region_result.text,
        "words": [
            {"text": word.text, "conf": word.confidence}
            for word in page.words
        ]
    }

    # Step 7: Output the result for the current page
    print(page_output)
```

Das Ausführen des Skripts erzeugt eine Reihe von Dictionaries – eines pro Seite – die etwa so aussehen:

```json
{
  "page": 1,
  "full_text": "....",
  "total_amount": "1,250,000 VND",
  "words": [
    {"text": "MãĐơnHàng", "conf": 0.98},
    {"text": "KháchHàng", "conf": 0.96},
    ...
  ]
}
```

Sie können die Ausgabe leicht in eine Datei umleiten (`> results.jsonl`) für eine spätere Batch‑Verarbeitung.

---

## Vollständiges funktionierendes Beispiel

Alles zusammengeführt, hier das komplette Skript, das Sie kopieren und ausführen können:

```python
import ocr
from ocr import Rectangle

# -------------------------------------------------
# 1️⃣ Initialize the OCR engine and configure it
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.Vietnamese
ocr_engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
ocr_engine.custom_dictionary = ["MãĐơnHàng", "KháchHàng", "SốTiền"]

# -------------------------------------------------
# 2️⃣ Recognize all pages of a multi‑page PDF
# -------------------------------------------------
pdf_path = "YOUR_DIRECTORY/sample.pdf"
pages = ocr_engine.recognize_multi_page(pdf_path)

# -------------------------------------------------
# 3️⃣ Iterate through each page, extract region, and build output
# -------------------------------------------------
for page_index, page in enumerate(pages, start=1):
    total_region = Rectangle(400, 650, 200, 50)          # region of interest
    region_result = ocr_engine.recognize_region(page.image, total_region)

    page_output = {
        "page": page_index,
        "full_text": page.text,
        "total_amount": region_result.text,
        "words": [
            {"text": word.text, "conf": word.confidence}
            for word in page.words
        ]
    }

    print(page_output)   # Replace with logging or file write as needed
```

### Erwartete Ausgabe

Das Ausführen des Skripts gegen ein dreiseitiges Rechnungs‑PDF könnte folgendes Ergebnis liefern:

```
{'page': 1, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.99}, ...]}
{'page': 2, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.98}, ...]}
{'page': 3, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.97}, ...]}
```

Leiten Sie die Ausgabe gern an `jq` oder einen anderen JSON‑Parser weiter, um die Struktur zu prüfen.

---

## Häufige Fragen & Randfälle

| Frage | Antwort |
|----------|--------|
| **Was, wenn mein PDF passwortgeschützt ist?** | Die meisten SDKs erlauben das Übergeben eines `password`‑Arguments an `recognize_multi_page`. Einfach `password="mySecret"` zum Aufruf hinzufügen. |
| **Meine Scans sind in Graustufen, nicht Schwarz‑Weiß.** | Die Option `auto_binarize` kümmert sich darum, Sie können aber auch vorher mit `Pillow` manuell konvertieren, bevor Sie das Bild an `recognize_region` übergeben. |
| **Der Gesamtbetrag erscheint manchmal an einer anderen Koordinate.** | Berechnen Sie das Rechteck dynamisch (z. B. via Template‑Matching) oder führen Sie eine Vollseiten‑OCR aus und suchen Sie den Text anschließend mit einem Regex wie `r'\d{1,3}(,\d{3})* VND'`. |
| **Die Performance ist bei 500‑seitigen PDFs langsam.** | Stapeln Sie die Seiten: Verarbeiten Sie 50 Seiten, schreiben Sie die Ergebnisse, dann leeren Sie die `pages`‑Liste, um Speicher freizugeben. Deaktivieren Sie außerdem `auto_deskew`, wenn Ihre Scans bereits gerade sind. |
| **Wie gehe ich später mit anderen Sprachen um?** | Ändern Sie einfach `ocr_engine.language = ocr.Language.English` (oder ein beliebiges unterstütztes Enum), bevor Sie `recognize_multi_page` aufrufen. Der Rest der Pipeline bleibt unverändert. |

---

## Tipps für produktionsreife Deployments

1. **Fehlerbehandlung** – Umschließen Sie OCR‑Aufrufe mit `try/except`‑Blöcken; protokollieren Sie den Seiten‑Index bei einem Fehlschlag, damit Sie später nacharbeiten können.  
2. **Logging** – Verwenden Sie das Python‑`logging`‑Modul anstelle von `print` für flexible Verbosität.  
3. **Parallelität** – Wenn Ihre OCR‑Bibliothek thread‑sicher ist, starten Sie einen `ThreadPoolExecutor`, um Seiten gleichzeitig zu verarbeiten.  
4. **Konfigurationsdatei** – Speichern Sie Sprache, Wörterbuch und Rechteckkoordinaten in einer JSON/YAML‑Datei; das macht das Skript wiederverwendbar für verschiedene Projekte.  
5. **Testing** – Erstellen Sie ein kleines Test‑Suite mit bekannten PDFs und prüfen Sie, ob der extrahierte `total_amount` den erwarteten Werten entspricht.  

---

## Fazit

Sie haben gerade gelernt **

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}