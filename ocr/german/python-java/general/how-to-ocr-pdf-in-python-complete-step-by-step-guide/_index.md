---
category: general
date: 2026-06-06
description: Wie man PDFs mit Python OCR verarbeitet, Text aus PDFs extrahiert, gescannten
  PDF‑Text konvertiert und die OCR‑Sprache in nur wenigen Zeilen Code ändert.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert scanned pdf text
- perform ocr on pdf
- change ocr language
language: de
og_description: 'Wie man PDFs mit Python OCRt: ein praktischer Leitfaden, der zeigt,
  wie man Text aus PDFs extrahiert, gescannte PDF‑Texte konvertiert und die OCR‑Sprache
  mühelos ändert.'
og_title: Wie man PDFs in Python OCRt – Vollständiges Programmier‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Python, extract text from PDF, convert scanned
    PDF text, and change OCR language in just a few lines of code.
  headline: How to OCR PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Wie man PDFs in Python OCRt – Vollständige Schritt‑für‑Schritt‑Anleitung
url: /de/python-java/general/how-to-ocr-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man PDF in Python OCR‑t – Vollständige Schritt‑für‑Schritt‑Anleitung

Haben Sie sich jemals gefragt, **wie man PDF** Dateien OCR‑t, ohne teure SaaS‑Tools zu bezahlen? Sie sind nicht allein. Egal, ob Sie alte Bücher digitalisieren, Daten aus Rechnungen extrahieren oder einfach durchsuchbaren Text aus einem gescannten Bericht benötigen, das Beherrschen von PDF‑OCR in Python kann Ihnen Stunden manueller Kopierarbeit ersparen.

In diesem Tutorial führen wir Sie durch ein kompaktes, funktionierendes Beispiel, das **Text aus PDF extrahiert**, Ihnen zeigt, wie Sie **gescannte PDF‑Texte** in editierbare Strings umwandeln, und sogar demonstriert, wie Sie **die OCR‑Sprache ändern** können, wenn Ihr Dokument nicht auf Englisch ist. Am Ende haben Sie ein wiederverwendbares Snippet, das Sie in jedes Projekt einbinden können.

## Voraussetzungen & Einrichtung

Bevor wir starten, stellen Sie sicher, dass Sie Folgendes haben:

- Python 3.8+ installiert (der Code funktioniert mit 3.9, 3.10 und neueren Versionen)
- Das `ocr`‑Paket, das die Klasse `OcrEngine` bereitstellt (Sie können es über `pip install ocr-lib` installieren – ersetzen Sie den Namen durch das reale Paket, das Sie verwenden)
- Eine PDF‑Datei, die Sie verarbeiten möchten; für die Demo verwenden wir `high_res_book.pdf`, abgelegt in einem Ordner namens `YOUR_DIRECTORY`

Wenn Sie eine virtuelle Umgebung verwenden (dringend empfohlen), aktivieren Sie sie zuerst:

```bash
python -m venv .venv
source .venv/bin/activate   # on Windows: .venv\Scripts\activate
pip install ocr-lib
```

> **Pro Tipp:** Legen Sie Ihre PDF‑Dateien in einem eigenen `data/`‑Verzeichnis ab, um später Pfad‑bezogene Probleme zu vermeiden.

## Schritt 1: Erstellen einer OCR‑Engine‑Instanz (Wie man PDF OCR‑t – Initialisierung)

Der allererste Schritt, wenn Sie **OCR auf PDF**‑Dateien ausführen möchten, besteht darin, die Engine zu instanziieren. Denken Sie an die Engine als das Gehirn, das jede Seite liest, die Glyphen interpretiert und Ihnen reinen Text zurückgibt.

```python
# Step 1: Create an OCR engine instance
engine = OcrEngine()
```

Warum das wichtig ist: Ohne eine Engine haben Sie keinen Kontext für Spracheinstellungen, Rendering‑Optionen oder PDF‑Verarbeitung. Das `OcrEngine`‑Objekt enthält all diese Vorgaben und lässt Sie später Feinjustierungen vornehmen.

## Schritt 2: Erkennen der Sprache festlegen (OCR‑Sprache ändern)

Die meisten OCR‑Bibliotheken verwenden standardmäßig Englisch, aber was, wenn Ihr Dokument auf Französisch, Deutsch oder sogar Japanisch ist? Die Sprache zu ändern ist so einfach wie ein Aufruf von `set_recognition_language`. Das erfüllt die Anforderung **change OCR language** und sorgt für höhere Genauigkeit.

```python
# Step 2: Set the recognition language to English (or any supported language)
engine.set_recognition_language(ocr.Language.ENGLISH)   # swap ENGLISH for FRANCAIS, etc.
```

> **Warum Sie das benötigen könnten:** Ein mehrsprachiges Archiv enthält häufig gemischte Sprachseiten. Das Umschalten der Sprache on‑the‑fly verhindert Fehlinterpretationen von Zeichen wie „ß“ oder „ñ“.

## Schritt 3: PDF‑Render‑Optionen konfigurieren (gescannte PDF‑Texte effektiv konvertieren)

Bei gescannten PDFs beeinflussen Auflösung und Farbraum die OCR‑Qualität stark. Das Rendern mit 300 DPI in Graustufen ist für die meisten Dokumente ein guter Kompromiss – hoch genug, um Details zu erfassen, aber niedrig genug, um den Speicherverbrauch im Rahmen zu halten.

```python
# Step 3: Configure PDF rendering options (300 DPI, grayscale)
engine.pdf_render_options() \
      .set_dpi(300) \
      .set_color_mode("grayscale")
```

Die verketteten Aufrufe sehen vielleicht fancy aus, sind aber nur eine fluente API, die jedes Mal dasselbe Options‑Objekt zurückgibt. Wenn Sie Farbe benötigen (z. B. für farbige Diagramme), ersetzen Sie `"grayscale"` durch `"color"`.

## Schritt 4: PDF erkennen und Text der ersten Seite extrahieren (Text aus PDF extrahieren)

Jetzt kommt der Kern von **how to OCR PDF**: Der Engine einen Dateipfad übergeben und den erkannten Text herausziehen. Die Methode liefert eine Liste von Seitenergebnissen; jedes Ergebnis enthält ein `text`‑Attribut.

```python
# Step 4: Recognize the PDF and print the text of the first page
results = engine.recognize_pdf("YOUR_DIRECTORY/high_res_book.pdf")
print(results[0].text)   # Text from the first page
```

Wenn Sie das gesamte Dokument benötigen, iterieren Sie über `results`:

```python
for i, page in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(page.text)
```

### Was tun, wenn das PDF verschlüsselt ist?

Einige PDFs sind passwortgeschützt. In diesem Fall können Sie das Passwort an `recognize_pdf` übergeben:

```python
results = engine.recognize_pdf(
    "YOUR_DIRECTORY/secure_doc.pdf",
    password="mySecret123"
)
```

Die Engine entschlüsselt on‑the‑fly, bevor sie das OCR ausführt – keine zusätzlichen Schritte nötig.

## Schritt 5: Nachbearbeitung des extrahierten Textes (Feinabstimmung des Textes aus PDF)

Roh‑OCR‑Ausgaben enthalten häufig Zeilenumbrüche, überflüssige Leerzeichen oder gelegentlich falsch erkannte Zeichen. Eine schnelle Aufräum‑Routine macht den extrahierten String bereit für nachgelagerte Verarbeitung (Suchindizierung, Datenbankspeicherung usw.).

```python
import re

def clean_ocr_text(raw: str) -> str:
    # Remove multiple spaces and line breaks
    text = re.sub(r'\s+', ' ', raw)
    # Strip leading/trailing whitespace
    return text.strip()

clean_text = clean_ocr_text(results[0].text)
print(clean_text)
```

Sie können nun sicher **text from PDF** extrahieren und in jede NLP‑Pipeline, Suchmaschine oder einfache `open(...).write()`‑Operation einspeisen.

## Bonus: Stapelverarbeitung mehrerer PDFs (Skalierung von OCR auf PDF)

Wenn Sie einen Ordner voller gescannter PDFs haben, verpacken Sie die Logik in einer Schleife:

```python
import pathlib

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    print(f"Processing {pdf_path.name} …")
    pages = engine.recognize_pdf(str(pdf_path))
    full_text = "\n".join(page.text for page in pages)
    cleaned = clean_ocr_text(full_text)

    # Save the extracted text alongside the PDF
    txt_path = pdf_path.with_suffix(".txt")
    txt_path.write_text(cleaned, encoding="utf-8")
    print(f"Saved extracted text to {txt_path.name}")
```

Dieses Snippet zeigt, wie Sie **perform OCR on PDF**‑Dateien in großen Mengen verarbeiten – ein häufiger Bedarf bei Digitalisierungsprojekten.

## Erwartete Ausgabe

Das Ausführen des Ein‑Seiten‑Beispiels (Schritt 4) sollte etwa Folgendes ausgeben:

```
In the beginning God created the heavens and the earth. Now the earth was formless …
```

Wenn Sie ein mehrseitiges Buch verarbeitet haben, zeigt die Konsole den bereinigten Text jeder Seite, und das Batch‑Skript legt neben jeder PDF eine `.txt`‑Datei an.

## Häufige Fallstricke & wie man sie vermeidet

| Problem | Symptome | Lösung |
|-------|----------|-----|
| Low‑resolution source PDF | Verzerrte Zeichen, fehlende Wörter | DPI erhöhen (`set_dpi(400)` oder höher) |
| Wrong language set | Viele unbekannte Symbole, besonders bei Akzentzeichen | `engine.set_recognition_language(ocr.Language.FRENCH)` oder das passende Enum verwenden |
| Large PDF causing memory error | `MemoryError` oder Absturz nach einigen Seiten | Seiten in Chunks verarbeiten (`engine.recognize_pdf(..., max_pages=10)`) |
| Missing fonts in the PDF | Leere Ausgabe für bestimmte Seiten | Sicherstellen, dass das PDF tatsächlich Rasterbilder enthält; manche PDFs sind nur Vektor‑ und benötigen andere Handhabung |

## Bildillustration

Unten sehen Sie eine schnelle Visualisierung des Workflows. Der Alt‑Text ist bewusst SEO‑freundlich.

![how to ocr pdf workflow diagram showing engine initialization, language setting, rendering options, recognition, and text extraction](/images/ocr-workflow.png)

*Das Diagramm ist nicht erforderlich, damit der Code läuft, hilft aber visuellen Lernenden zu verstehen, wo jeder Schritt einzuordnen ist.*

## Fazit

Wir haben **how to OCR PDF**‑Dateien in Python von Anfang bis Ende behandelt: Erstellung einer OCR‑Engine, **changing OCR language**, Konfiguration des Renderings zum **convert scanned PDF text** und schließlich **extracting text from PDF** für die weitere Nutzung. Das komplette, ausführbare Beispiel kann in jedes Projekt übernommen werden, und das optionale Batch‑Skript zeigt, wie Sie die Lösung skalieren.

Als Nächstes könnten Sie folgendes erkunden:

- Hinzufügen von **perform OCR on PDF** für mehrsprachige Archive, indem Sie über eine Sprachliste iterieren.
- Integration des extrahierten Textes in Elasticsearch für Volltextsuche.
- Nutzung von OCR, um durchsuchbare PDFs zu erstellen, indem Sie die Textebene wieder in die Originaldatei einbetten (viele Bibliotheken bieten eine `save_as_searchable_pdf`‑Methode).

Fühlen Sie sich frei zu experimentieren, DPI‑Einstellungen zu justieren oder zu einem anderen OCR‑Backend zu wechseln. Die Grundlagen bleiben gleich, und Sie haben nun ein solides Fundament, auf dem Sie aufbauen können.

Viel Spaß beim Coden, und mögen Ihre gescannten Dokumente endlich durchsuchbar werden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält komplette, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Features zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}