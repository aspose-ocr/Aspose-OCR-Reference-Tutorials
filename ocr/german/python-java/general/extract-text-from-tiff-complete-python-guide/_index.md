---
category: general
date: 2026-06-16
description: Extrahiere Text aus TIFF‑Dateien mit Python‑OCR. Lerne, wie du TIFF Schritt
  für Schritt in Text umwandelst und mehrseitige Dokumente mühelos verarbeitest.
draft: false
keywords:
- extract text from tiff
- convert tiff to text
- Python OCR multi‑page TIFF
- OCR language settings
- OCR engine Python
language: de
og_description: Extrahiere Text aus TIFF‑Dateien mit Python‑OCR. Befolge diese Anleitung,
  um TIFF in Text zu konvertieren, mehrseitige Scans zu verarbeiten und saubere Ergebnisse
  zu erhalten.
og_title: Text aus TIFF extrahieren – Vollständiger Python-Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  headline: Extract Text from TIFF – Complete Python Guide
  type: TechArticle
- description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  name: Extract Text from TIFF – Complete Python Guide
  steps:
  - name: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
    text: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
  - name: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
    text: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
  - name: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
    text: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
  - name: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
    text: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Text extraction
title: Text aus TIFF extrahieren – Vollständiger Python‑Leitfaden
url: /de/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus TIFF extrahieren – Vollständiger Python‑Leitfaden

Haben Sie jemals **Text aus TIFF**‑Bildern extrahieren müssen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein – viele Entwickler stoßen auf dieses Problem, wenn sie mit gescannten Archiven oder Legacy‑Dokumenten arbeiten. Die gute Nachricht? Mit ein paar Zeilen Python können Sie **TIFF in Text** umwandeln – und das im Handumdrehen, selbst wenn die Datei Dutzende von Seiten enthält.

In diesem Tutorial gehen wir ein konkretes Beispiel durch: Laden einer mehrseitigen TIFF, Festlegen der OCR‑Sprache auf Französisch und Auslesen des erkannten Textes jeder Seite. Am Ende haben Sie ein sofort einsatzbereites Skript, verstehen, warum jeder Schritt wichtig ist, und wissen, wie Sie es für andere Sprachen oder Bildformate anpassen können.

## Voraussetzungen

Bevor wir starten, stellen Sie sicher, dass Sie folgendes haben:

- Python 3.8 oder neuer installiert.
- Das `ocr`‑Paket (oder eine kompatible OCR‑Bibliothek, die eine `OcrEngine`‑Klasse bereitstellt). Installieren Sie es mit `pip install ocr-lib` – ersetzen Sie den Namen durch das tatsächlich verwendete Paket.
- Eine mehrseitige TIFF‑Datei (z. B. `french-scans.tif`), die Sie verarbeiten möchten.
- Grundlegende Erfahrung mit Python‑Skripting.

Keine schweren Abhängigkeiten, keine externen Dienste – nur reines Python und eine OCR‑Engine.

---

## Schritt 1: OCR‑Engine einrichten, um **Text aus TIFF** zu extrahieren

Zuerst benötigen wir eine Instanz der OCR‑Engine und müssen ihr mitteilen, welche Sprache verwendet werden soll. In unserem Fall ist das Ausgangsmaterial Französisch, also setzen wir die Sprache entsprechend.

```python
import ocr  # Replace with the actual import if your OCR library uses a different name

# Create the OCR engine
engine = ocr.OcrEngine()

# Tell the engine to look for French characters
engine.language = ocr.Language.FRENCH
```

**Warum das wichtig ist:**  
Die Spracheinstellung verbessert die Genauigkeit erheblich. Französische Zeichen wie „é“ oder „ç“ würden bei einer englischen Voreinstellung als generische Symbole gelesen werden. Durch die explizite Auswahl von Französisch geben wir der Engine die richtige Zeichentabelle.

> **Pro‑Tipp:** Wenn Sie Dokumente in mehreren Sprachen verarbeiten, können Sie `engine.language` vor jedem `recognize()`‑Aufruf dynamisch ändern.

---

## Schritt 2: Laden Sie die mehrseitige TIFF, die Sie **TIFF in Text** umwandeln möchten

Eine TIFF kann mehrere Frames enthalten – denken Sie an jeden Frame als separate Seite. Die OCR‑Bibliothek abstrahiert das für uns, sodass wir einfach den Dateipfad angeben.

```python
# Path to your multi‑page TIFF
tiff_path = "YOUR_DIRECTORY/french-scans.tif"

# Load the file; the engine now knows how many pages it contains
engine.load_from_file(tiff_path)
```

**Hinweis zu Randfällen:**  
Ist der Dateipfad falsch oder ist die TIFF beschädigt, wirft die Methode `load_from_file` eine Ausnahme. Packen Sie sie in einen `try/except`‑Block für Produktionscode:

```python
try:
    engine.load_from_file(tiff_path)
except Exception as e:
    print(f"Failed to load TIFF: {e}")
    raise
```

---

## Schritt 3: OCR auf das gesamte Dokument anwenden – Der Kern von **Text aus TIFF extrahieren**

Jetzt lässt die Engine ihre Magie wirken. Der Aufruf `recognize()` verarbeitet jede Seite in einem Durchlauf und liefert ein umfangreiches Ergebnisobjekt.

```python
# Perform OCR on all pages at once
multi_result = engine.recognize()
```

**Was im Hintergrund passiert:**  
Die Engine iteriert über jeden Frame, wendet Vorverarbeitung (Entzerrung, Binarisierung) an, führt das neuronale Netzwerk aus und aggregiert die Ausgabe. Da wir `recognize()` nur einmal aufrufen, kann die Bibliothek Ressourcen zwischen den Seiten teilen, was schneller ist als ein manuelles Durchlaufen.

---

## Schritt 4: Den erkannten Text aus dem JSON‑Ergebnis ziehen – **TIFF in Text** Seite für Seite

Das Ergebnisobjekt kann in JSON serialisiert werden. In diesem JSON finden Sie ein `pages`‑Array, das jeweils ein Feld `text` enthält.

```python
# Convert the result to a Python dict (JSON-like)
result_dict = multi_result.to_json()

# Extract the list of pages
pages = result_dict["pages"]
```

Jetzt haben wir eine saubere Python‑Liste, bei der jedes Element dem OCR‑Ausgabe‑Text einer Seite entspricht.

---

## Schritt 5: Den Text jeder Seite ausgeben oder speichern – Der letzte Schritt von **Text aus TIFF extrahieren**

Lassen Sie uns über die Seiten iterieren und den extrahierten Text anzeigen. Sie können den Text auch in separate `.txt`‑Dateien schreiben, wenn Ihnen das lieber ist.

```python
for i, page in enumerate(pages, start=1):
    print(f"--- Page {i} ---")
    print(page["text"])
    print()  # Blank line for readability
```

### Erwartete Ausgabe (Beispiel)

```
--- Page 1 ---
Bonjour, ceci est un exemple de texte extrait d'une image TIFF.

--- Page 2 ---
Le deuxième page contient davantage d'informations en français.
```

Wenn die OCR erfolgreich war, sehen Sie einen sauberen Block französischer Sätze pro Seite. Sollten Sie unleserliche Zeichen bemerken, prüfen Sie die Spracheinstellung oder erhöhen Sie die Bildauflösung vor der OCR.

---

## Häufige Stolperfallen beim **TIFF in Text** umwandeln

| Problem | Warum es passiert | Schnelle Lösung |
|---------|-------------------|-----------------|
| **Leeres `pages`‑Array** | Die TIFF wurde nicht korrekt geladen oder enthält keine Frames. | Pfad prüfen und sicherstellen, dass die TIFF nicht ein einseitiges PNG im TIFF‑Format ist. |
| **Unsinnige Zeichen** | Sprachmismatch oder niedrige Bildqualität. | Richtige `engine.language` setzen und das Bild vorverarbeiten (z. B. DPI erhöhen). |
| **Speicherexplosion bei riesigen TIFFs** | Alle Seiten gleichzeitig laden verbraucht RAM. | In Teilen verarbeiten: Einzelnen Frame laden, erkennen, dann verwerfen, bevor der nächste geladen wird. |
| **Unicode‑Fehler beim Ausgeben** | Konsolen‑Encoding unterstützt keine Akzentzeichen. | `print(page["text"].encode('utf-8').decode('utf-8'))` verwenden oder das Terminal auf UTF‑8 konfigurieren. |

---

## Das Skript erweitern: Von **Text aus TIFF extrahieren** zu Batch‑Verarbeitung

Jetzt, wo Sie eine solide Basis haben, können Sie folgende Schritte in Betracht ziehen:

1. **Batch‑Konvertierung** – Packen Sie den gesamten Ablauf in eine Funktion `def ocr_tiff(path):` und iterieren Sie über ein Verzeichnis mit TIFF‑Dateien.
2. **Ausgabe in Dateien** – Statt zu drucken, schreiben Sie den Text jeder Seite in `page_{i}.txt` oder fassen alles in einem einzigen Dokument zusammen.
3. **Alternative OCR‑Engines** – Für höhere Genauigkeit können Sie `ocr.OcrEngine()` durch Tesseract (`pytesseract`) oder Azure Cognitive Services ersetzen – die Logik zum **Text aus TIFF extrahieren** bleibt gleich.
4. **Nachbearbeitung** – Rechtschreibprüfung, Spracherkennung oder Regex‑Bereinigung ausführen, um das rohe OCR‑Ergebnis zu säubern.

---

## Vollständiges, sofort ausführbares Skript

Unten finden Sie den kompletten Code, bereit zum Kopieren und Einfügen. Er enthält grundlegende Fehlerbehandlung und optionales Speichern des Textes jeder Seite in separate Dateien.

```python
import ocr  # Adjust import based on your OCR library
import os

def extract_text_from_tiff(tiff_path: str, output_dir: str = None) -> list:
    """
    Loads a multi‑page TIFF, runs OCR, and returns a list of strings,
    one per page. Optionally saves each page to a .txt file.
    """
    # Initialize engine and set language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.FRENCH

    # Load the TIFF file
    try:
        engine.load_from_file(tiff_path)
    except Exception as e:
        raise RuntimeError(f"Unable to load {tiff_path}: {e}")

    # Run OCR on all pages
    multi_result = engine.recognize()

    # Parse JSON result
    pages = multi_result.to_json()["pages"]
    texts = [page["text"] for page in pages]

    # If an output directory is provided, write each page to a file
    if output_dir:
        os.makedirs(output_dir, exist_ok=True)
        for i, text in enumerate(texts, start=1):
            file_path = os.path.join(output_dir, f"page_{i}.txt")
            with open(file_path, "w", encoding="utf-8") as f:
                f.write(text)

    return texts

if __name__ == "__main__":
    # Example usage – replace with your actual TIFF path
    tiff_file = "YOUR_DIRECTORY/french-scans.tif"
    # Optional: where to store per‑page text files
    out_folder = "extracted_pages"

    page_texts = extract_text_from_tiff(tiff_file, out_folder)

    for i, txt in enumerate(page_texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()
```

Führen Sie dieses Skript aus, setzen Sie `tiff_file` auf Ihr Dokument und beobachten Sie, wie die Konsole mit sauberen französischen Sätzen gefüllt wird. Wenn Sie `out_folder` angegeben haben, finden Sie außerdem eine Reihe von `page_#.txt`‑Dateien, die für nachgelagerte Verarbeitung bereitstehen.

---

## Fazit

Wir haben **Text aus TIFF**‑Dateien mithilfe eines einfachen Python‑OCR‑Workflows extrahiert und Sie wissen jetzt, wie Sie **TIFF in Text** zuverlässig umwandeln. Vom Initialisieren der Engine mit der richtigen Sprache bis zum Durchlaufen des JSON‑Ergebnisses jeder Seite wurde jeder Schritt mit dem zugrunde liegenden „Warum“ erklärt, sodass Sie das Muster auf andere Sprachen, Bildformate oder größere Batch‑Jobs anpassen können.

Was kommt als Nächstes? Tauschen Sie das OCR‑Backend gegen Tesseract aus, experimentieren Sie mit verschiedenen Sprachpaketen oder integrieren Sie die Ausgabe in eine durchsuchbare Datenbank. Der Himmel ist die Grenze, wenn Sie gescannte Bilder zuverlässig in durchsuchbaren Text verwandeln können.

Hinterlassen Sie gern einen Kommentar, falls Sie auf Probleme stoßen oder Ideen für weitere Verbesserungen haben. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}