---
category: general
date: 2026-06-25
description: PDF-Text mit OCR in Python extrahieren. Lernen Sie, wie Sie PDF in Text
  umwandeln, mit einem klaren Python‑OCR‑Beispiel, und erhalten Sie schnell zuverlässige
  Ergebnisse.
draft: false
keywords:
- extract pdf text OCR
- convert pdf to text
- python ocr example
- Aspose OCR Python
- multi‑page PDF OCR
language: de
og_description: PDF-Text mit OCR in Python extrahieren. Dieser Leitfaden zeigt ein
  Python‑OCR‑Beispiel, das PDFs in Text umwandelt und mehrseitige Dokumente mühelos
  verarbeitet.
og_title: PDF-Text per OCR in Python extrahieren – Vollständiges Programmier‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract PDF text OCR using Python. Learn how to convert PDF to text
    with a clear python OCR example and get reliable results fast.
  headline: Extract PDF Text OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: PDF-Text mit OCR in Python extrahieren – Vollständige Schritt‑für‑Schritt‑Anleitung
url: /de/python-java/general/extract-pdf-text-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF‑Text‑OCR in Python extrahieren – Vollständige Schritt‑für‑Schritt‑Anleitung

Haben Sie schon einmal **PDF‑Text‑OCR extrahieren** müssen, waren sich aber nicht sicher, welche Bibliothek mehrseitige PDFs ohne Kopfschmerzen verarbeiten kann? Sie sind nicht allein. In vielen realen Projekten – denken Sie an Rechtsverträge, gescannte Rechnungen oder archivierte Berichte – ist das Erhalten von sauberem, durchsuchbarem Text aus einem PDF eine unverzichtbare Fähigkeit.

In diesem Tutorial gehen wir einen **Python‑OCR‑Beispiel** durch, das **PDF in Text konvertiert** mithilfe von Aspose.OCR. Am Ende haben Sie ein sofort einsatzbereites Skript, das den Text jeder Seite extrahiert, eine Vorschau anzeigt und das gesamte Dokument als einzelne `.txt`‑Datei speichert. Kein Schnickschnack, nur eine praktische Lösung, die Sie noch heute in Ihren Code integrieren können.

## Was Sie lernen werden

- Wie Sie das Aspose‑OCR‑Modul für Python installieren und importieren.  
- Wie Sie eine OCR‑Engine‑Instanz erstellen und **PDF‑Text‑OCR extrahieren** auf einem mehrseitigen PDF ausführen.  
- Wie Sie durch die Ergebnisse jeder Seite iterieren, eine Vorschau anzeigen und die komplette Ausgabe auf die Festplatte schreiben.  
- Tipps zum Umgang mit häufigen Fallstricken wie leeren Seiten oder Unicode‑Zeichen.  

> **Voraussetzungen:** Python 3.8+ installiert, Grundkenntnisse im Umgang mit pip und eine PDF‑Datei, die Sie verarbeiten möchten. Keine vorherige OCR‑Erfahrung erforderlich.

---

![Extract PDF Text OCR workflow diagram](extract-pdf-text-ocr.png "Diagramm des PDF‑Text‑OCR‑Prozesses")

*Alt‑Text: Diagramm, das den PDF‑Text‑OCR‑Workflow in Python veranschaulicht.*

## Schritt 1: Aspose OCR für Python installieren

Bevor irgendein Code ausgeführt wird, benötigen Sie das Aspose.OCR‑Paket. Es wird über PyPI verteilt, sodass ein einziger pip‑Befehl ausreicht.

```bash
pip install aspose-ocr
```

> **Pro‑Tipp:** Wenn Sie in einer virtuellen Umgebung arbeiten (dringend empfohlen), aktivieren Sie diese zuerst, um Abhängigkeiten isoliert zu halten.

## Schritt 2: Modul importieren und OCR‑Engine erstellen

Jetzt, wo die Bibliothek verfügbar ist, importieren Sie sie und erzeugen ein `OcrEngine`. Denken Sie an die Engine als das Gehirn, das die schwere Arbeit erledigt – Zeichen erkennen, Seitenlayouts verarbeiten und saubere Unicode‑Strings zurückgeben.

```python
# Step 2: Import the Aspose OCR module and create an engine
import aspose.ocr as ocr

engine = ocr.OcrEngine()
```

> **Warum das wichtig ist:** Die Engine einmal zu instanziieren und über alle Seiten hinweg wiederzuverwenden, ist deutlich effizienter, als für jede Seite eine neue Engine zu erstellen. Außerdem sorgt es für konsistente Einstellungen im gesamten Dokument.

## Schritt 3: Alle Seiten eines PDFs erkennen (Mehrseitige OCR)

Die Methode `recognize_multi_page` von Aspose.OCR akzeptiert einen Dateipfad und gibt eine Liste von `OcrResult`‑Objekten zurück – eines pro Seite. Das ist das Kernstück unserer **PDF‑in‑Text‑Konvertierung**.

```python
# Step 3: Run OCR on every page of the PDF
pdf_path = "YOUR_DIRECTORY/contract.pdf"   # replace with your actual file
pdf_pages = engine.recognize_multi_page(pdf_path)  # returns List[OcrResult]
```

> **Randfall:** Wenn das PDF passwortgeschützt ist, müssen Sie das Passwort über `engine.set_password("your_password")` bereitstellen, bevor Sie `recognize_multi_page` aufrufen.

## Schritt 4: Ergebnisse iterieren und eine Vorschau anzeigen

Eine kurze Vorschau hilft Ihnen zu überprüfen, ob die OCR tatsächlich Text erkennt. Wir geben die ersten 200 Zeichen jeder Seite aus, Sie können den Slice nach Bedarf anpassen.

```python
# Step 4: Display a short preview of each page’s extracted text
for page_number, page_result in enumerate(pdf_pages, start=1):
    print(f"--- Page {page_number} ---")
    # Show the first 200 characters of the page's OCR text
    print(page_result.text[:200])
    print()  # blank line for readability
```

**Beispielausgabe**

```
--- Page 1 ---
This Agreement is made on the 1st day of January 2025 between ...

--- Page 2 ---
WHEREAS, the Parties desire to enter into a collaborative ...

--- Page 3 ---
IN WITNESS WHEREOF, the Parties have executed this Agreement ...
```

Oben wird nur ein Ausschnitt gezeigt, aber der vollständige Text befindet sich in `page_result.text`.

## Schritt 5: Alle Seiten zu einer einzigen Textdatei kombinieren (optional)

Die meisten nachgelagerten Workflows – Suchindizierung, Datenanalyse oder einfaches Archivieren – bevorzugen eine einzelne `.txt`‑Datei. Lassen Sie uns die Seiten zusammenfügen und schreiben.

```python
# Step 5: Save the complete OCR output to a .txt file
output_path = "YOUR_DIRECTORY/contract_extracted.txt"

with open(output_path, "w", encoding="utf-8") as out_file:
    for page_result in pdf_pages:
        out_file.write(page_result.text)
        out_file.write("\n\n")  # separate pages with a blank line
print(f"All pages saved to {output_path}")
```

> **Warum das funktioniert:** Die Verwendung von UTF‑8 stellt sicher, dass Sie keine Sonderzeichen wie Akzente oder Symbole verlieren, die häufig in juristischen Dokumenten vorkommen.

## Schritt 6: Umgang mit häufigen Fallstricken

| Problem | Symptom | Lösung |
|---------|---------|--------|
| Leere Seiten in der Ausgabe | `page_result.text` ist leer | Prüfen Sie, ob das Quell‑PDF tatsächlich gescannte Bilder enthält; manche PDFs sind bereits textbasiert und benötigen einen anderen Ansatz (z. B. PDF‑Textextraktions‑Bibliotheken). |
| Verzerrte Zeichen | Seltsame Symbole anstelle von Buchstaben | Stellen Sie sicher, dass die Sprache der OCR‑Engine korrekt gesetzt ist: `engine.language = ocr.Language.English` (oder eine andere Sprache). |
| Große PDFs dauern zu lange | Skript scheint bei einer Seite zu hängen | Aktivieren Sie Multithreading: `engine.recognize_multi_page(pdf_path, ocr.RecognizeOptions(parallel=True))`. |
| Speicherfehler bei riesigen Dateien | `MemoryError` wird ausgelöst | Verarbeiten Sie das PDF in Teilen (z. B. 50 Seiten gleichzeitig) oder erhöhen Sie das Python‑Speicherlimit. |

## Vollständiges Skript – Bereit zum Ausführen

Alles zusammengefügt, hier das komplette, eigenständige Skript, das Sie in eine Datei namens `extract_pdf_text_ocr.py` kopieren können.

```python
# extract_pdf_text_ocr.py
# Complete python ocr example that extracts PDF text using Aspose OCR.

import aspose.ocr as ocr

def main():
    # 1️⃣ Install the library via `pip install aspose-ocr` before running.
    # 2️⃣ Set the path to your PDF.
    pdf_path = "YOUR_DIRECTORY/contract.pdf"
    output_path = "YOUR_DIRECTORY/contract_extracted.txt"

    # 3️⃣ Create the OCR engine.
    engine = ocr.OcrEngine()
    # Optional: set language for better accuracy.
    # engine.language = ocr.Language.English

    # 4️⃣ Perform multi‑page OCR.
    pdf_pages = engine.recognize_multi_page(pdf_path)

    # 5️⃣ Show a preview of each page.
    for page_number, page_result in enumerate(pdf_pages, start=1):
        print(f"--- Page {page_number} ---")
        print(page_result.text[:200])
        print()

    # 6️⃣ Write the full text to a file.
    with open(output_path, "w", encoding="utf-8") as out_file:
        for page_result in pdf_pages:
            out_file.write(page_result.text)
            out_file.write("\n\n")
    print(f"✅ All pages saved to {output_path}")

if __name__ == "__main__":
    main()
```

Führen Sie es im Terminal aus:

```bash
python extract_pdf_text_ocr.py
```

Sie sollten die Seitenvorschauen in der Konsole sehen, gefolgt von einer Bestätigung, dass der gesamte Text gespeichert wurde.

## Zusammenfassung & nächste Schritte

Wir haben gerade gezeigt, wie man **PDF‑Text‑OCR extrahiert** mit einem prägnanten **Python‑OCR‑Beispiel**, das **PDF in Text konvertiert**. Die Kernschritte – installieren, importieren, Engine erstellen, `recognize_multi_page` ausführen, Vorschau anzeigen und speichern – decken den gängigsten Workflow für gescannte PDFs ab.

**Was kommt als Nächstes?**  

- **Genauigkeit feinabstimmen**: Spielen Sie mit `engine.recognize_multi_page(..., RecognizeOptions(...))`, um DPI anzupassen oder Sprachpakete zu nutzen.  
- **Nachbearbeitung**: Entfernen Sie überflüssige Leerzeichen, führen Sie eine Rechtschreibprüfung durch oder leiten Sie den Text in eine Natural‑Language‑Pipeline weiter.  
- **Batch‑Verarbeitung**: Durchlaufen Sie einen Ordner mit PDFs, um ein durchsuchbares Archiv aufzubauen.  

Wenn Sie Probleme haben, prüfen Sie, ob das PDF tatsächlich Rasterbilder enthält (OCR funktioniert nur auf Bildern, nicht auf eingebettetem Text). Für bereits textbasierte PDFs sollten Sie Bibliotheken wie `pdfminer.six` oder `PyMuPDF` in Betracht ziehen.

---

**Viel Spaß beim Coden!** Wenn Ihnen diese Anleitung geholfen hat, **PDF‑Text‑OCR zu extrahieren** für Ihr Projekt, teilen Sie Ihre Ergebnisse in den Kommentaren oder öffnen Sie ein Issue auf der Aspose OCR GitHub‑Seite für Feature‑Wünsche. Experimentieren Sie weiter, und Sie werden bald eine robuste Pipeline haben, die jedes gescannte PDF in durchsuchbaren, editierbaren Text verwandelt.

## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Text aus Bild mit Aspose OCR extrahieren – Schritt‑für‑Schritt‑Anleitung](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Text aus Bildern extrahieren – OCR‑Grundlagen mit Aspose.OCR für Java](/ocr/english/java/ocr-basics/)
- [Wie man Bildtext mit Sprache mittels Aspose.OCR OCR‑durchführt](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}