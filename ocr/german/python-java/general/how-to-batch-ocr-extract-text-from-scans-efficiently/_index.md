---
category: general
date: 2026-04-26
description: Wie Sie Ihre Dokumente im Batch OCRen und Text aus Scans in Python extrahieren.
  Lernen Sie die schrittweise Batch‑Verarbeitung mit OcrEngine für JSON‑Ausgabe.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- OCR batch processing
- Python OCR automation
- JSON OCR output
language: de
og_description: Wie Sie Ihre gescannten Dateien stapelweise OCRen und Text aus Scans
  in einem einzigen Skript extrahieren. Vollständiger Code, Tipps und Behandlung von
  Randfällen.
og_title: Wie man Batch-OCR durchführt – Schneller Python-Leitfaden
tags:
- OCR
- Python
- Automation
title: Wie man OCR stapelweise durchführt – Text effizient aus Scans extrahieren
url: /de/python-java/general/how-to-batch-ocr-extract-text-from-scans-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Batch-OCR durchführt – Text effizient aus Scans extrahieren

Haben Sie sich jemals gefragt, **wie man Batch-OCR** auf einen Berg gescannter PDFs anwendet, ohne den Verstand zu verlieren? Sie sind nicht allein – Entwickler fragen ständig, *„Wie kann ich Text aus Scans in einem Durchgang extrahieren?“* Die gute Nachricht ist, dass ein paar Zeilen Python diese lästige Aufgabe in eine reibungslose, automatisierte Pipeline verwandeln können.

In diesem Tutorial führen wir Sie durch eine komplette, sofort einsatzbereite Lösung, die **Text aus Scans extrahiert**, die Ergebnisse als JSON speichert und am Ende einen schnellen Plausibilitäts‑Check bietet. Keine externen Dienste, keine Magie – nur reines Python, die `OcrEngine`‑Klasse und ein wenig Ordner‑Management.

## Was Sie am Ende haben werden

- Ein voll funktionsfähiges Skript, das **Batch-OCR** über beliebige Bild‑Ordner ausführt.
- Klare Erklärungen, *warum* jede Zeile existiert, nicht nur *was* sie tut.
- Tipps zum Umgang mit leeren Ordnern, Nicht‑Bild‑Dateien und großen Stapeln.
- Eine Möglichkeit zu prüfen, dass die JSON‑Ausgabe tatsächlich den extrahierten Text enthält.

### Voraussetzungen (das Minimum)

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | Moderne Syntax & Typ‑Hinweise |
| `OcrEngine` library (or a compatible wrapper) | Kern‑OCR‑Funktionalität |
| A directory with scanned image files (PNG, JPG, TIFF) | Ein Verzeichnis mit gescannten Bilddateien (PNG, JPG, TIFF) – Eingabedaten |
| Write permissions for the output folder | Schreibrechte für den Ausgabeverzeichnis – Speichern der JSON‑Ergebnisse |

Wenn Sie das bereits haben, großartig – lassen Sie uns eintauchen.

![Ablauf der Batch-OCR](image-placeholder.png){alt="Ablauf der Batch-OCR"}

## Schritt 1 – OCR‑Engine initialisieren (Batch-OCR)

Bevor wir irgendetwas verarbeiten können, benötigen wir eine Instanz der OCR‑Engine. Denken Sie an sie als das „Gehirn“, das jedes Bild liest und Text ausgibt. Sie einmal zu initialisieren und über den gesamten Batch hinweg wiederzuverwenden, ist das effizienteste Muster.

```python
# Step 1: Create an OCR engine instance
# The OcrEngine class abstracts the low‑level OCR library (Tesseract, EasyOCR, etc.)
ocr_engine = OcrEngine()
```

> **Warum dieselbe Instanz wiederverwenden?**  
> Für jede Datei eine neue Engine zu erstellen, würde wiederholt schwere Modelle in den Speicher laden und den Batch dramatisch verlangsamen. Eine Instanz hält das Modell im RAM und ermöglicht das Verarbeiten von Tausenden Bildern ohne merkliche Verlangsamung.

## Schritt 2 – Auf Ihren Scan‑Ordner verweisen (Text aus Scans extrahieren)

Ihre Scans befinden sich irgendwo auf der Festplatte. Lassen Sie uns dem Skript mitteilen, wo sie zu finden sind. Die Verwendung absoluter Pfade vermeidet „Datei nicht gefunden“-Überraschungen, wenn das Skript aus einem anderen Arbeitsverzeichnis gestartet wird.

```python
import os

# Step 2: Specify the folder that contains scanned images
# Replace YOUR_DIRECTORY with the actual base path on your machine.
input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
```

> **Pro‑Tipp:**  
> Unter Windows funktionieren Vorwärtsschrägstriche (`/`) problemlos mit `os.path.abspath`, sodass Sie Backslashes nicht escapen müssen.

## Schritt 3 – Zielort für die JSON‑Ergebnisse festlegen

Sie möchten wahrscheinlich einen übersichtlichen Ordner für die OCR‑Ergebnisse. Die Trennung von Ausgabe und Quelle erleichtert das spätere Aufräumen oder das Einspeisen des JSON in eine andere Pipeline.

```python
# Step 3: Specify where the JSON results should be saved
output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
os.makedirs(output_dir, exist_ok=True)   # Ensure the folder exists
```

> **Warum den Ordner programmgesteuert erstellen?**  
> Es garantiert, dass das Skript nicht abstürzt, wenn das Verzeichnis fehlt, und `exist_ok=True` macht die Operation idempotent – das Skript kann mehrmals ohne Fehler ausgeführt werden.

## Schritt 4 – Batch‑Prozess ausführen (Batch-OCR)

Jetzt zum Kern der Sache: `ocr_engine` anweisen, jede Datei in `input_dir` zu durchlaufen, OCR auszuführen und JSON in `output_dir` zu schreiben. Das Flag `format="json"` weist die Engine an, das Ergebnis in einer strukturierten Form zu serialisieren, die nachgelagerte Werkzeuge lieben.

```python
# Step 4: Run batch processing to convert all scans to JSON format
ocr_engine.batch_process(
    input_folder=input_dir,
    output_folder=output_dir,
    format="json"
)
```

### Was passiert im Hintergrund?

1. **Datei‑Erkennung** – Die Engine scannt `input_folder` rekursiv und ignoriert versteckte Dateien.
2. **Datei‑Validierung** – Nur unterstützte Bild‑Erweiterungen (`.png`, `.jpg`, `.tif` usw.) werden an das OCR‑Modell übergeben.
3. **OCR‑Ausführung** – Jedes Bild wird an die OCR‑Engine gesendet; Text, Konfidenz‑Scores und Layout‑Daten werden erfasst.
4. **JSON‑Serialisierung** – Das Ergebnis wird in eine Datei mit demselben Basisnamen, aber der Erweiterung `.json`, im `output_folder` geschrieben.

> **Umgang mit Sonderfällen:**  
> - **Leerer Ordner:** Die Engine protokolliert „No files found“ und beendet sich ohne Absturz.  
> - **Beschädigtes Bild:** Sie überspringt die Datei, zeichnet einen Fehlereintrag in `batch_errors.log` auf und fährt fort.  
> - **Großer Batch (10 k+ Dateien):** Der Speicherverbrauch bleibt gering, da jedes Bild unabhängig verarbeitet wird.

## Schritt 5 – Abschluss der Konvertierung bestätigen

Eine einfache `print`‑Anweisung liefert sofortiges Feedback in der Konsole. Für Produktions‑Pipelines könnten Sie dies durch einen Logging‑Aufruf oder eine E‑Mail‑Benachrichtigung ersetzen.

```python
# Step 5: Inform the user that the batch conversion has finished
print("Batch conversion complete.")
```

Wenn Sie diese Zeile sehen, können Sie den `json_output`‑Ordner sicher inspizieren. Jede JSON‑Datei wird ungefähr so aussehen:

```json
{
  "file_name": "invoice_001.png",
  "text": "Invoice #001\nDate: 2024‑12‑01\nTotal: $1,234.56",
  "confidence": 0.97,
  "layout": [
    {"line": 1, "bbox": [10, 20, 200, 40]},
    {"line": 2, "bbox": [10, 50, 180, 70]},
    {"line": 3, "bbox": [10, 80, 150, 100]}
  ]
}
```

Sie können diese JSON‑Dateien nun in eine Datenbank, einen Suchindex oder ein beliebiges nachgelagertes Analyse‑Tool einspeisen.

## Häufig gestellte Fragen (und schnelle Antworten)

**F: Was, wenn ich PDFs statt Bildern verarbeiten muss?**  
A: Konvertieren Sie jede PDF‑Seite zuerst in ein Bild (z. B. mit `pdf2image`) und legen Sie die resultierenden PNG/JPG‑Dateien in `input_dir` ab. Die Batch‑OCR‑Logik bleibt unverändert.

**F: Kann ich das Ausgabeformat zu einfachem Text ändern?**  
A: Absolut. Ersetzen Sie `format="json"` durch `format="txt"` und die Engine schreibt eine `.txt`‑Datei, die nur den extrahierten Text enthält.

**F: Meine Scans befinden sich in mehreren Unterordnern – wird das Skript rekursiv arbeiten?**  
A: Ja. `batch_process` durchläuft standardmäßig den Verzeichnisbaum. Wenn Sie eine flache Ausgabe wünschen, setzen Sie `flatten=True` (falls die Bibliothek das unterstützt) oder verarbeiten Sie die JSON‑Dateinamen nachträglich.

**F: Wie gehe ich mit nicht‑lateinischen Schriften um?**  
A: Initialisieren Sie `OcrEngine` mit einem Sprachparameter, z. B. `OcrEngine(lang="spa+eng")`. Die Batch‑Schleife selbst benötigt keine Änderungen.

## Pro‑Tipps & häufige Fallstricke

- **Batch‑Größe ist wichtig:** Wenn Sie CPU‑Spitzen bemerken, drosseln Sie den Prozess mit einem einfachen `time.sleep(0.1)` zwischen den Dateien.
- **Logging:** Ersetzen Sie den `print`‑Aufruf durch das Python‑`logging`‑Modul, um Zeitstempel und Fehlerebenen zu erfassen.
- **Dateinamen‑Kollisionen:** Wenn zwei Scans denselben Basisnamen haben, aber in unterschiedlichen Unterordnern liegen, überschreiben die JSON‑Dateien einander. Hängen Sie einen Hash des relativen Pfads an den Ausgabename an, um dies zu vermeiden.
- **Speicher‑Lecks:** Einige OCR‑Back‑Ends behalten native Ressourcen bei. Rufen Sie `ocr_engine.close()` am Ende Ihres Skripts auf, falls die Bibliothek eine Aufräummethode bereitstellt.

## Vollständiges Skript – bereit zum Kopieren & Einfügen

```python
import os
from ocr_engine import OcrEngine   # Replace with the actual import path

def main():
    # Step 1: Initialize the OCR engine (how to batch OCR)
    ocr_engine = OcrEngine()

    # Step 2: Directory with scanned images (extract text from scans)
    input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
    if not os.path.isdir(input_dir):
        raise FileNotFoundError(f"Input folder not found: {input_dir}")

    # Step 3: Destination for JSON results
    output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
    os.makedirs(output_dir, exist_ok=True)

    # Step 4: Run the batch OCR process
    ocr_engine.batch_process(
        input_folder=input_dir,
        output_folder=output_dir,
        format="json"
    )

    # Step 5: Confirmation message
    print("Batch conversion complete.")

if __name__ == "__main__":
    main()
```

**Erwartete Konsolenausgabe**

```
Scanning folder: /home/user/YOUR_DIRECTORY/scans/
Found 42 image files.
Processing file 1/42: invoice_001.png … done.
Processing file 2/42: receipt_2024-03.jpg … done.
…
Batch conversion complete.
```

Sie können das JSON überprüfen, indem Sie eine Datei in `json_output` mit einem Texteditor öffnen oder sie in Python laden:

```python
import json, pathlib

sample = pathlib.Path(output_dir) / "invoice_001.json"
data = json.loads(sample.read_text())
print(data["text"])
```

Sie sollten den rohen, OCR‑extrahierten Text in der Konsole sehen.

## Fazit

Wir haben gerade **wie man Batch-OCR** für ein ganzes Verzeichnis gescannter Bilder durchführt und **Text aus Scans** in saubere, maschinenlesbare JSON‑Dateien extrahiert. Der Ansatz ist bewusst einfach: Die Engine einmal einrichten, auf einen Ordner zeigen und die Bibliothek die schwere Arbeit erledigen lassen. Von hier aus können Sie:

- Das JSON einbinden

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}