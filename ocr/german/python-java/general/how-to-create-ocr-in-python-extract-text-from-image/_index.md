---
category: general
date: 2026-04-26
description: Wie man OCR schnell und zuverlässig erstellt. Lernen Sie, Text aus einem
  Bild zu extrahieren, ein Bild für OCR zu laden und OCR auf PNG mit einem benutzerdefinierten
  Wörterbuch auszuführen.
draft: false
keywords:
- how to create OCR
- extract text from image
- extract text scanned document
- load image for OCR
- run OCR on png
language: de
og_description: Wie man OCR in Python erstellt und Text aus einem Bild extrahiert.
  Dieser Leitfaden zeigt, wie man ein Bild für OCR lädt, OCR auf PNG ausführt und
  ein benutzerdefiniertes Wörterbuch verwendet.
og_title: Wie man OCR in Python erstellt – Schnelle Textextraktion
tags:
- OCR
- Python
- Image Processing
title: Wie man OCR in Python erstellt – Text aus Bild extrahieren
url: /de/python-java/general/how-to-create-ocr-in-python-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in Python erstellt – Schritt‑für‑Schritt‑Anleitung

Haben Sie sich jemals gefragt, **wie man OCR erstellt**, das Ihre gescannten PDFs, Screenshots oder handschriftlichen Notizen lesen kann? Sie sind nicht allein. In vielen realen Projekten müssen wir *Text aus Bild*-Dateien extrahieren, aber die sofort einsatzbereiten Engines stolpern oft über domänenspezifische Wörter.  

In diesem Tutorial sehen Sie ein vollständiges, ausführbares Beispiel, das ein Bild für OCR lädt, ein benutzerdefiniertes Wörterbuch anwendet und schließlich **OCR auf PNG**‑Dateien ausführt. Am Ende können Sie Text aus jedem Bild extrahieren und die Engine an Ihre eigene Terminologie anpassen.

## Was dieses Tutorial abdeckt

* Installation des kleinen, aber leistungsstarken `aocr`‑Pakets (oder einer kompatiblen Bibliothek).  
* Konfiguration eines **benutzerdefinierten Wörterbuchs**, sodass Begriffe wie `aspocorp` oder `licensekey` erkannt werden.  
* **Laden eines Bildes für OCR**, egal ob es sich um ein PNG, JPEG oder eine gescannte PDF‑Seite handelt.  
* Ausführen des OCR‑Prozesses und Ausgeben des Ergebnisses.  

Keine externen Dokumentationslinks, nur eine eigenständige Lösung, die Sie heute kopieren‑und‑einfügen und ausführen können.

### Voraussetzungen

* Python 3.8 oder neuer (der Code verwendet f‑Strings).  
* Grundlegende Erfahrung mit der Kommandozeile – Sie werden ein paar `pip install`‑Befehle eingeben.  
* Eine Bilddatei (`technical_doc.png` im Beispiel), die an einem Ort liegt, den Sie referenzieren können.  

Wenn Sie diese drei Punkte erfüllen, können Sie loslegen.  

---

## Schritt 1: OCR‑Bibliothek installieren

Zuerst benötigen wir eine OCR‑Engine, die ein programmierbares Konfigurationsobjekt unterstützt. Das `aocr`‑Paket ist ein leichtgewichtiges Wrapper um eine native OCR‑Engine und eignet sich gut für Demonstrationen.

```bash
# Install the library (run once)
pip install aocr
```

> **Pro‑Tipp:** Wenn Sie Windows verwenden und einen Kompilierungsfehler erhalten, versuchen Sie `pip install aocr‑binary`, das vorgefertigte Wheels bereitstellt.

### Warum diese Bibliothek installieren?

`aocr` gibt uns direkten Zugriff auf ein `config`‑Objekt, in das wir ein **benutzerdefiniertes Wörterbuch** einfügen können. Das ist das Geheimrezept, um die Genauigkeit bei Nischenvokabular zu verbessern.

---

## Schritt 2: OCR‑Engine‑Instanz erstellen & ein benutzerdefiniertes Wörterbuch hinzufügen

Jetzt starten wir die Engine und teilen ihr mit, welche Wörter als bekannt behandelt werden sollen.

```python
from aocr import OcrEngine

# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Provide a custom dictionary to improve recognition of domain‑specific terms
ocr_engine.config.custom_dictionary = [
    "aspocorp",      # our company's brand name
    "ocrengine",    # the library name itself
    "licensekey"    # a common field in our contracts
]
```

### Warum ein benutzerdefiniertes Wörterbuch wichtig ist

Standard‑OCR‑Modelle werden auf generischen Korpora trainiert. Wenn das Modell “aspocorp” sieht, könnte es in “aspo corp” aufteilen oder Buchstaben ganz weglassen. Durch das Einspeisen einer benutzerdefinierten Liste biasieren wir den Erkenner auf die exakt benötigte Schreibweise, was den Nachbearbeitungsaufwand drastisch reduziert.

---

## Schritt 3: Das zu verarbeitende Bild laden

Hier laden wir das **Bild für OCR**. Die Methode `Image.load` akzeptiert einen Pfad‑String und bestimmt automatisch den Dateityp.

```python
import aocr

# Step 3: Load the image that contains the text you want to extract
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/technical_doc.png")
```

> **Sonderfall:** Wenn Ihre Quelle ein mehrseitiges PDF ist, konvertieren Sie jede Seite zuerst zu PNG (z. B. mit `pdf2image`) und geben Sie sie einzeln an die Engine weiter.

### Tipps für bessere Bildqualität

* Halten Sie die Auflösung mindestens bei 300 dpi.  
* Stellen Sie sicher, dass das Bild aufrecht ist; rotieren Sie bei Bedarf mit `Pillow`.  
* Konvertieren Sie farbige Scans in Graustufen, um Rauschen zu reduzieren.

---

## Schritt 4: OCR‑Prozess auf der PNG‑Datei ausführen

Mit der konfigurierten Engine und dem geladenen Bild führen wir schließlich **OCR auf PNG** aus.

```python
# Step 4: Run the OCR process
ocr_result = ocr_engine.process()
```

Der Aufruf `process()` gibt ein Objekt zurück, das den erkannten Text, Konfidenzwerte und Begrenzungsrahmen für jedes Wort enthält.

---

## Schritt 5: Erkannten Text ausgeben

Der einfachste Weg, zu sehen, was die Engine gefunden hat, ist das Ausdrucken des Attributs `text`.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### Erwartete Ausgabe

Wenn `technical_doc.png` den Satz *„The Aspocorp licensekey expires on 2025‑12‑31.“* enthält, sollte die Konsole anzeigen:

```
The Aspocorp licensekey expires on 2025-12-31.
```

Beachten Sie, wie das benutzerdefinierte Wörterbuch den Markennamen unverändert ließ – etwas, das ein Standard‑OCR möglicherweise verzerrt hätte.

---

## Vollständiges funktionierendes Beispiel (Kopieren‑und‑Einfügen bereit)

Unten finden Sie das gesamte Skript, bereit zum Speichern als `run_ocr.py`. Ersetzen Sie einfach den Platzhalter‑Pfad durch den Speicherort Ihres Bildes.

```python
# run_ocr.py
# -------------------------------------------------
# Complete example showing how to create OCR,
# load an image, apply a custom dictionary,
# and extract text from a PNG file.
# -------------------------------------------------

from aocr import OcrEngine
import aocr

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Add domain‑specific words
    ocr_engine.config.custom_dictionary = [
        "aspocorp",
        "ocrengine",
        "licensekey"
    ]

    # 3️⃣ Load the image you want to process
    #    (Make sure the path points to a real file)
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    ocr_engine.image = aocr.Image.load(image_path)

    # 4️⃣ Run the OCR engine
    ocr_result = ocr_engine.process()

    # 5️⃣ Print the extracted text
    print("=== Extracted Text ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

Führen Sie es im Terminal aus:

```bash
python run_ocr.py
```

Sie sollten den extrahierten Text in der Konsole sehen, genau wie im vorherigen Beispiel gezeigt.

---

## Häufig gestellte Fragen (FAQ)

| Frage | Antwort |
|----------|--------|
| **Kann ich Text aus einem gescannten PDF extrahieren?** | Ja. Konvertieren Sie jede Seite zuerst zu PNG (oder TIFF) und geben Sie die Bilder dann an dasselbe Skript weiter. |
| **Was, wenn mein Bild ein JPEG statt eines PNG ist?** | Die Methode `Image.load` unterstützt JPEG, BMP, TIFF und PNG von Haus aus. Ändern Sie einfach die Dateierweiterung. |
| **Wie verbessere ich die Genauigkeit bei Scans mit geringem Kontrast?** | Vorbearbeiten mit `Pillow` – Kontrast erhöhen, Binärisierung anwenden oder `opencv` zum Entzerren nutzen. |
| **Gibt es eine Möglichkeit, Konfidenzwerte für jedes Wort zu erhalten?** | `ocr_result` enthält `words` – jedes Wort hat ein `confidence`‑Attribut, über das Sie iterieren können. |
| **Kann ich das auf einem headless Server ausführen?** | Absolut. `aocr` hat keine GUI‑Abhängigkeiten und ist damit perfekt für CI‑Pipelines. |

---

## Nächste Schritte & verwandte Themen

Jetzt, da Sie wissen, **wie man OCR erstellt** und **Text aus Bilddateien extrahiert**, sollten Sie folgende Themen erkunden:

* **Pre‑Processing‑Techniken** – `load image for OCR` ist nur der erste Schritt; verwenden Sie `opencv`, um Rauschen zu entfernen oder zu schärfen.  
* **Batch‑Verarbeitung** – iterieren Sie über ein Verzeichnis von PNGs, um ein durchsuchbares Archiv zu erzeugen.  
* **Mehrsprachige Unterstützung** – fügen Sie Sprachpakete zur Engine hinzu, wenn Sie französische oder deutsche Dokumente lesen müssen.  
* **Integration mit Elasticsearch** – indexieren Sie den extrahierten Text für Volltextsuche über gescannte Assets.  

Jede dieser Erweiterungen baut auf dem Kernmuster auf, das wir gerade behandelt haben, sodass der Übergang mühelos sein wird.

---

## Abschluss

In wenigen Minuten haben wir beantwortet, **wie man OCR erstellt**, das zuverlässig **Text aus Bilddateien** extrahiert, insbesondere PNGs, und wir haben Ihnen gezeigt, wie man **Bild für OCR lädt**, ein **benutzerdefiniertes Wörterbuch** anwendet und **OCR auf PNG** ausführt – ganz ohne externe Dienste.  

Probieren Sie das Skript aus, passen Sie das Wörterbuch an Ihren eigenen Jargon an, und Sie haben eine solide Grundlage für jedes Dokument‑Digitalisierungsprojekt.  

Wenn Sie auf Probleme stoßen, hinterlassen Sie unten einen Kommentar – ich helfe gern. Und vergessen Sie nicht, Ihre Erfolgsgeschichten zu teilen; die Community lernt am besten aus Praxisbeispielen.  

**Bereit, Ihre Papierarbeit zu automatisieren?** Holen Sie sich den Code, passen Sie ihn an und beginnen Sie noch heute damit, Pixel in durchsuchbaren Text zu verwandeln!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}