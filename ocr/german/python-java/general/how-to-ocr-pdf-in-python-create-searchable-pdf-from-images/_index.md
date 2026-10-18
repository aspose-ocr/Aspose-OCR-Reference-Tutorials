---
category: general
date: 2026-06-06
description: Wie man PDFs OCRt und durchsuchbare PDF-Dateien aus Bildern mit Python
  erstellt. Lernen Sie, durchsuchbaren Text hinzuzufügen und Bilder in PDF/A in wenigen
  Minuten zu konvertieren.
draft: false
keywords:
- how to ocr pdf
- create searchable pdf
- add searchable text
- ocr image to pdf
- convert image to pdf/a
language: de
og_description: Wie man PDF Schritt für Schritt OCRt. Lernen Sie, durchsuchbaren Text
  hinzuzufügen und Bilder mit einem einfachen Python‑Skript in PDF/A zu konvertieren.
og_title: Wie man PDFs OCRt – Schnellleitfaden zur Erstellung durchsuchbarer PDFs
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  headline: How to OCR PDF in Python – Create Searchable PDF from Images
  type: TechArticle
- description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  name: How to OCR PDF in Python – Create Searchable PDF from Images
  steps:
  - name: Why this matters
    text: '- **Preserving graphics** means the visual layout (tables, logos, stamps)
      stays exactly as the scanner captured it. - The `result` object typically contains
      a hidden text layer that we’ll later embed into the PDF. - Using `recognize_image`
      instead of `recognize_pdf` avoids an extra conversion step, '
  - name: Why this matters
    text: '- **Searchable PDF**: The output file contains a hidden, selectable text
      layer. You can now Ctrl + F through the document. - **PDF/A compliance**: Some
      organizations (legal, finance) require PDF/A for audit trails; this step satisfies
      that rule automatically. - The method also **adds searchable text'
  - name: Expected output
    text: 'When you run the script, the console prints:'
  type: HowTo
tags:
- OCR
- PDF
- Python
- Automation
title: Wie man PDFs in Python OCRt – Durchsuchbare PDFs aus Bildern erstellen
url: /de/python-java/general/how-to-ocr-pdf-in-python-create-searchable-pdf-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man PDF OCR‑t – Gescannte Bilder in durchsuchbare PDFs umwandelt

Haben Sie sich schon einmal gefragt, **wie man PDF OCR‑t**, wenn Sie nur ein gescanntes Bild einer Rechnung oder eines Belegs haben? Sie sind nicht allein. In vielen Büros kommen eingehende Unterlagen als flache PNG‑ oder JPEG‑Dateien, und der nächste Schritt – diese Inhalte durchsuchbar zu machen – fühlt sich wie eine Black‑Box an.  

Die gute Nachricht? Mit nur wenigen Zeilen Python können Sie **durchsuchbare PDF**‑Dateien **erstellen**, **durchsuchbaren Text hinzufügen** und sogar **Bild zu PDF/A konvertieren** für die Langzeitarchivierung. In diesem Tutorial gehen wir jeden Schritt durch, erklären, warum er wichtig ist, und geben Ihnen ein sofort einsatzbereites Skript, das Sie in jedes Projekt einbinden können.

> **Pro‑Tipp:** Der gleiche Ansatz funktioniert für mehrseitige Scans; einfach über die Dateien iterieren und die Engine erledigt den Rest.

---

## Was Sie benötigen

Bevor wir starten, stellen Sie sicher, dass Sie Folgendes auf Ihrem Rechner haben:

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| Python 3.9 oder neuer | Moderne Syntax und bessere Bibliotheksunterstützung |
| `pdfium`‑basierte OCR‑Engine (z. B. `pdfocr` oder ein kommerzielles SDK) | Handhabt sowohl Bild‑Erkennung als auch PDF/A‑Erstellung |
| Eine Bilddatei (PNG, JPEG, TIFF), die Sie in ein durchsuchbares PDF umwandeln möchten | Die Quelle des Textes |
| Schreibrechte für den Zielordner | Damit das Skript das neue PDF speichern kann |

Falls Sie das OCR‑SDK noch nicht installiert haben, führen Sie aus:

```bash
pip install pdfocr   # replace with your vendor's package name
```

Das war’s – keine komplexen Systemabhängigkeiten, nur ein pip‑Install.

---

## Wie man PDF OCR‑t – Überblick

Auf hoher Ebene besteht der Prozess aus drei einfachen Aktionen:

1. **Erkennen** des Textes im Bild, während die ursprüngliche Grafik erhalten bleibt.  
2. **Exportieren** des OCR‑Ergebnisses zusammen mit dem Originalbild als **durchsuchbares PDF/A** (die archivfreundliche PDF‑Variante).  
3. **Validieren**, dass die resultierende Datei auswählbaren, durchsuchbaren Text über dem Originalbild enthält.

Im Folgenden sehen Sie jeden Schritt im Code, mit Erklärungen zum *Warum* hinter den Befehlen.

---

## Schritt 1: Text aus dem Bild erkennen

Zuerst lassen wir die OCR‑Engine die Pixel lesen und ein Ergebnis‑Objekt zurückgeben, das sowohl das Rohbild als auch den extrahierten Text enthält. Denken Sie daran, dass die Engine das Dokument für Sie „liest“.

```python
# Step 1: Recognize text from the image and keep the original graphics
result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

### Warum das wichtig ist

- **Grafiken erhalten** bedeutet, dass das visuelle Layout (Tabellen, Logos, Stempel) exakt so bleibt, wie der Scanner es erfasst hat.  
- Das `result`‑Objekt enthält typischerweise eine versteckte Textebene, die wir später in das PDF einbetten.  
- Die Verwendung von `recognize_image` statt `recognize_pdf` vermeidet einen zusätzlichen Konvertierungsschritt, was die Verarbeitung von Einzelseiten‑Bildern beschleunigt.

#### Häufige Varianten

- Wenn Sie ein **mehrseitiges TIFF** haben, übergeben Sie den Dateipfad direkt; die meisten Engines behandeln jede Seite als separates Bild.  
- Für PDFs, die bereits Bilder enthalten, können Sie `engine.recognize_pdf("file.pdf")` aufrufen und diesen Schritt komplett überspringen.

---

## Schritt 2: OCR‑Ergebnis als durchsuchbares PDF/A exportieren

Jetzt nehmen wir das `result` aus Schritt 1 und lassen die Engine eine neue Datei schreiben. Das Schlüssel‑Flag hier ist *PDF/A* – die ISO‑Standard‑Version von PDF, die für die Langzeit‑Aufbewahrung konzipiert ist.

```python
# Step 2: Export the OCR result together with the original image as a searchable PDF/A
result.save_as_pdfa("YOUR_DIRECTORY/invoice_searchable.pdf")
```

### Warum das wichtig ist

- **Durchsuchbares PDF**: Die Ausgabedatei enthält eine versteckte, auswählbare Textebene. Sie können jetzt mit Strg + F das Dokument durchsuchen.  
- **PDF/A‑Konformität**: Einige Organisationen (Recht, Finanzen) verlangen PDF/A für Prüfpfade; dieser Schritt erfüllt diese Anforderung automatisch.  
- Die Methode **fügt durchsuchbaren Text hinzu**, ohne das Bild zu flatten, sodass die visuelle Treue perfekt bleibt.

#### Sonderfall: Stattdessen ein normales PDF?

Wenn Ihnen PDF/A egal ist, ersetzen Sie `save_as_pdfa` durch `save_as_pdf`. Der Rest des Workflows bleibt unverändert.

---

## Schritt 3: Das durchsuchbare PDF überprüfen

Ein kurzer Plausibilitäts‑Check erspart Ihnen später mysteriöse Fehler. Öffnen Sie die erzeugte Datei in einem beliebigen PDF‑Viewer, versuchen Sie ein Wort zu markieren und nutzen Sie die Suchfunktion.

```python
# Step 3: The file "invoice_searchable.pdf" now contains selectable text layered over the original invoice image
import subprocess, os

pdf_path = "YOUR_DIRECTORY/invoice_searchable.pdf"
if os.path.exists(pdf_path):
    print(f"✅ PDF created successfully: {pdf_path}")
    # Optionally open the file (works on macOS, Windows, Linux with appropriate commands)
    subprocess.run(["open", pdf_path] if os.name == "posix" else ["start", pdf_path], shell=True)
else:
    print("❌ Something went wrong – PDF not found.")
```

### Erwartete Ausgabe

Wenn Sie das Skript ausführen, gibt die Konsole Folgendes aus:

```
✅ PDF created successfully: YOUR_DIRECTORY/invoice_searchable.pdf
```

Beim Öffnen der Datei sollten Sie das Original‑Rechnungsbild mit einer schwachen, unsichtbaren Textebene sehen. Markieren Sie ein beliebiges Wort – es ist auswählbar – **das ist der durchsuchbare Text**, den Sie gerade hinzugefügt haben.

---

## Durchsuchbaren Text zu bestehenden PDFs hinzufügen (Bonus)

Manchmal haben Sie bereits ein PDF, dem Sie **durchsuchbaren Text** hinzufügen müssen. Die gleiche Engine kann OCR‑Ergebnisse über ein bestehendes PDF legen:

```python
# Bonus: Add searchable text to an existing PDF file
existing_pdf = engine.load_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result = engine.recognize_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result.apply_to(existing_pdf).save_as_pdfa("YOUR_DIRECTORY/old_scanned_searchable.pdf")
```

Hier kombiniert `apply_to` die versteckte Ebene mit den Originalseiten, sodass Sie **durchsuchbare PDFs** erstellen können, ohne erneut zu scannen.

---

## Häufige Stolperfallen und Tipps

| Stolperfalle | Wie man sie vermeidet |
|--------------|----------------------|
| **Niedrigauflösende Quellbilder** (< 150 dpi) | Hochskalieren oder um einen Scan mit höherer Auflösung bitten; die OCR‑Genauigkeit sinkt dramatisch unter 150 dpi. |
| **Fehlende Sprachdaten** | Installieren Sie die passenden Sprachpakete für Ihre OCR‑Engine (`pip install pdfocr[eng,spa]`). |
| **Ausgabeordner nicht beschreibbar** | Skript mit ausreichenden Rechten ausführen oder ein anderes Verzeichnis wählen. |
| **PDF/A‑Validierung schlägt fehl** | Stellen Sie sicher, dass Sie keine nicht unterstützten Schriften oder JavaScript einbetten; die meisten SDKs erledigen das automatisch, wenn Sie `save_as_pdfa` verwenden. |

---

## Komplettes Skript – Ein‑Datei‑Lösung

Unten finden Sie ein eigenständiges Skript, das alles zusammenführt. Kopieren‑Sie es, ersetzen Sie die Platzhalter‑Pfade, und Sie können **Bild zu PDF/A** in Sekundenschnelle konvertieren.

```python
#!/usr/bin/env python3
"""
How to OCR PDF – Complete script to create a searchable PDF/A from an image.
Works with any OCR engine exposing `recognize_image` and `save_as_pdfa`.
"""

import os
import subprocess

# ----------------------------------------------------------------------
# CONFIGURATION – change these paths to match your environment
# ----------------------------------------------------------------------
INPUT_IMAGE = "YOUR_DIRECTORY/invoice.png"
OUTPUT_PDF  = "YOUR_DIRECTORY/invoice_searchable.pdf"

# ----------------------------------------------------------------------
# INITIALIZE THE OCR ENGINE (replace with your SDK's init call)
# ----------------------------------------------------------------------
# Example for a fictional `pdfocr` package:
# from pdfocr import Engine
# engine = Engine(api_key="YOUR_API_KEY")
# If you use a different library, adjust the import and init accordingly.
engine = Engine()  # placeholder – insert real initialization here

def main():
    # Step 1 – Recognize the image
    print(f"🔎 Recognizing text from {INPUT_IMAGE} …")
    result = engine.recognize_image(INPUT_IMAGE)

    # Step 2 – Save as searchable PDF/A
    print(f"💾 Saving searchable PDF/A to {OUTPUT_PDF} …")
    result.save_as_pdfa(OUTPUT_PDF)

    # Step 3 – Verify the file exists
    if os.path.isfile(OUTPUT_PDF):
        print("✅ Success! Searchable PDF/A created.")
        # Open the file for a quick visual check (optional)
        try:
            if os.name == "posix":
                subprocess.run(["open", OUTPUT_PDF])
            else:
                subprocess.run(["start", OUTPUT_PDF], shell=True)
        except Exception:
            pass
    else:
        print("❌ Error: PDF not created.")

if __name__ == "__main__":
    main()
```

**Was dieses Skript macht:**  
1. Lädt die OCR‑Engine.  
2. Liest das ausgewählte Bild und extrahiert den Text.  
3. Schreibt ein **durchsuchbares PDF/A**, das Sie sofort verteilen oder archivieren können.  

Sie können die `main`‑Logik leicht in eine Funktion verpacken, die einen ganzen Ordner verarbeitet – einfach über `os.listdir()` iterieren und die drei Schritte für jede Datei wiederholen.

---

## Nächste Schritte & verwandte Themen

Jetzt, wo Sie **wie man PDF OCR‑t** beherrschen, können Sie folgende weiterführende Ideen erkunden:

- **Batch‑Verarbeitung:** Nutzen Sie `concurrent.futures`, um Dutzende Rechnungen parallel zu OCR‑en.  
- **Metadaten‑Injection:** Fügen Sie Erstellungsdaten oder Rechnungsnummern zu den PDF‑Metadaten hinzu, um die Indexierung zu erleichtern.  
- **Hybrid‑PDFs:** Kombinieren Sie durchsuchbaren Text mit eingebetteten Originalbildern für einen „digitalen Zwilling“ des Papierdokuments.  
- **Alternative Ausgaben:** Exportieren Sie nach **DOCX** oder **HTML**, wenn nachgelagerte Systeme editierbare Formate benötigen.

Jeder dieser Punkte baut auf den Kernkonzepten auf, die Sie gerade gelernt haben – erkennen, exportieren, verifizieren.

---

## Fazit

Kurz gesagt, Sie wissen jetzt **wie man PDF OCR‑t**, indem Sie ein einfaches Bild mit nur drei Zeilen Python in ein **durchsuchbares PDF/A** verwandeln. Das Skript übernimmt die schwere Arbeit, bewahrt die Originalgrafiken und liefert ein normkonformes Dokument, das Sie durchsuchen, archivieren oder teilen können.  

Probieren Sie es mit Ihren eigenen Rechnungen, Belegen oder gescannten Verträgen aus. Wenn Sie auf Probleme stoßen, hinterlassen Sie einen Kommentar unten oder schauen Sie in die offizielle Dokumentation des SDK – dort finden Sie meist weitere Beispiele. Viel Spaß beim Coden und genießen Sie die neue Möglichkeit, jedes Bild sofort durchsuchbar zu machen! 

![How to OCR PDF example showing original image and searchable PDF overlay](placeholder.png "How to OCR PDF example")

## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}