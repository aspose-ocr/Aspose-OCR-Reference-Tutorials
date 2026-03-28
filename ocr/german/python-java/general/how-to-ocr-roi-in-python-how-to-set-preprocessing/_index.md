---
category: general
date: 2026-03-28
description: Wie man ROI in Python OCR durchführt – Erfahren Sie, wie Sie Vorverarbeitungsoptionen
  einstellen, um aus bestimmten Bildbereichen genaue Texterkennung zu erhalten.
draft: false
keywords:
- how to OCR ROI
- how to set preprocessing
- Aspose OCR Python
- ROI extraction
- image preprocessing OCR
language: de
og_description: Wie man ROI in Python OCRt – Dieser Leitfaden zeigt, wie man die Vorverarbeitung
  einstellt, um zuverlässige Textextraktion aus definierten Bildbereichen zu ermöglichen.
og_title: Wie man ROI in Python OCRt – Wie man die Vorverarbeitung einstellt
tags:
- OCR
- Python
- Aspose
title: Wie man ROI in Python OCRt – Wie man die Vorverarbeitung einstellt
url: /de/python-java/general/how-to-ocr-roi-in-python-how-to-set-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ROI in Python OCRt – Wie man die Vorverarbeitung einstellt

Haben Sie sich jemals gefragt, **wie man ROI OCRt** in einem verrauschten Rechnungsbild, ohne die gesamte Seite in den Speicher zu laden? Sie sind nicht allein. In vielen realen Projekten benötigen wir nur ein paar Felder – Kundenname, Adresse, Summen – sodass das Scannen des gesamten Dokuments übertrieben ist.  

Die gute Nachricht? Mit Aspose OCR können Sie der Engine genau **sagen, wo sie suchen soll** und ihr sogar mitteilen, das Bild zuerst zu bereinigen. In diesem Tutorial gehen wir Schritt für Schritt durch **wie man die Vorverarbeitung** einstellt, Regions of Interest (ROIs) definiert und sauberen Text in nur wenigen Zeilen Python extrahiert.

Am Ende dieses Leitfadens haben Sie ein sofort ausführbares Skript, das spezifische Blöcke aus jeder Rechnung, Quittung oder jedem Formular extrahiert. Keine zusätzlichen Werkzeuge nötig, nur Aspose OCR und ein wenig Python‑Logik.

---

## Was Sie benötigen

- **Python 3.8+** (der Code funktioniert mit jeder aktuellen Version)  
- **Aspose OCR for Python via .NET** – Installation mit `pip install aspose-ocr`  
- Ein Beispielbild (z. B. `invoice.png`) in einem Ordner, den Sie referenzieren können  
- Grundlegende Kenntnisse von Python‑Funktionen und objektorientierter Syntax  

Wenn Sie das bereits haben, großartig – lassen Sie uns direkt zum Code springen.

---

![Wie man ROI OCRt Diagramm](ocr-roi.png "Wie man ROI OCRt Beispiel")

*Alt‑Text: Diagramm, das zeigt, wie man ROI OCRt, mit ROI‑Boxen auf einem Rechnungsbild*

---

## Schritt 1 – Initialisieren der OCR‑Engine (Wie man ROI OCRt)

Bevor wir der Engine *sagen* können, **wo** sie suchen soll, benötigen wir eine Instanz des OCR‑Processors. Dieses Objekt hält alle Konfigurationen und führt den Erkennungsdurchlauf aus.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the engine – this is the entry point for all OCR work
ocr_engine = aocr.OcrEngine()
```

*Warum das wichtig ist*: Die Klasse `OcrEngine` übernimmt die schwere Arbeit (Schrifterkennung, Layout‑Analyse usw.). Durch das Erstellen einer einzigen Engine vermeiden Sie das erneute Initialisieren ressourcenintensiver Komponenten für jedes Bild, was die Leistung flott hält.

---

## Schritt 2 – Laden Ihres Quellbildes (Wie man ROI OCRt)

Aspose Storage macht das Laden von Bildern mühelos. Geben Sie den Dateipfad an, und Sie erhalten ein `Image`‑Objekt, das bereit zur Verarbeitung ist.

```python
# Replace YOUR_DIRECTORY with the actual path where invoice.png lives
source_image = storage.Image.load("YOUR_DIRECTORY/invoice.png")
```

*Hinweis*: Wenn Sie mit Streams arbeiten (z. B. Bilder, die über eine Web‑API hochgeladen werden), können Sie ein `BytesIO`‑Objekt an `Image.load` übergeben statt eines Dateipfads.

---

## Schritt 3 – Definieren der Regions of Interest (ROIs)

Jetzt beantworten wir die Kernfrage **wie man ROI OCRt**: Wir teilen der Engine die genauen Rechtecke mit, die die gewünschten Daten enthalten. Jede ROI wird durch ihre linke obere Ecke (`x`, `y`) und ihre Größe (`width`, `height`) definiert.

```python
from aspose.ocr import Roi

# Each tuple is (x, y, width, height) in pixels
regions_of_interest = [
    Roi(50, 120, 400, 60),   # Customer name block
    Roi(50, 200, 400, 80)    # Address block
]
```

*Warum ROIs verwenden?*  
- **Geschwindigkeit** – Die Engine überspringt irrelevante Bildbereiche.  
- **Genauigkeit** – Durch Fokussierung auf einen kleinen Bereich kann äußeres Rauschen den Erkenner nicht verwirren.  
- **Flexibilität** – Sie können beliebig viele ROIs hinzufügen; die Engine gibt eine Ergebnisliste in derselben Reihenfolge zurück.

---

## Schritt 4 – Wie man die Vorverarbeitung für bessere OCR‑Genauigkeit einstellt

Bilder, die direkt von Scannern oder Handys kommen, leiden häufig unter Schräglage, geringem Kontrast oder ungleichmäßiger Beleuchtung. Aspose OCR bietet ein `PreprocessingOptions`‑Objekt, mit dem Sie gängige Korrekturen vor der Erkennung aktivieren können.

```python
from aspose.ocr import PreprocessingOptions

preprocessing_options = PreprocessingOptions()
preprocessing_options.deskew = True          # Auto‑rotate tilted text
preprocessing_options.binarize = True        # Convert to black‑white for clarity
preprocessing_options.contrast = 1.5         # Boost contrast (1.0 = no change)
```

*Wie das hilft*:  
- **Deskew** entfernt die Schräglage, die Zeichenformen mehrdeutig macht.  
- **Binarize** reduziert Farbrauschen und liefert der OCR‑Engine ein sauberes Binärbild.  
- **Contrast** verstärkt schwache Striche, was besonders bei verblassten Quittungen nützlich ist.

Sie können mit diesen Flags experimentieren – schalten Sie eines aus und prüfen Sie, ob sich die Ausgabe ändert. Das ist der Kern von **wie man die Vorverarbeitung** effektiv einsetzt.

---

## Schritt 5 – OCR nur innerhalb der definierten ROIs ausführen

Mit Engine, Bild, ROIs und Vorverarbeitung ist es Zeit, `recognize` aufzurufen. Die Methode liefert ein `OcrResult`‑Objekt, das eine `regions`‑Sammlung enthält – jeder Eintrag entspricht der Reihenfolge der übergebenen ROIs.

```python
ocr_result = ocr_engine.recognize(
    source_image,
    rois=regions_of_interest,
    preprocessing=preprocessing_options
)
```

*Im Hintergrund*: Die Engine schneidet jede ROI zu, wendet die Vorverarbeitungspipeline an und führt das Erkennungsmodell auf dem bereinigten Ausschnitt aus. Da wir eine Liste übergeben haben, bleibt die Reihenfolge erhalten, was die Nachbearbeitung unkompliziert macht.

---

## Schritt 6 – Ausgelesenen Text lesen und verwenden (Wie man ROI OCRt)

Zum Schluss iterieren Sie über die `regions`‑Liste und geben die erkannten Zeichenketten aus – oder speichern sie. Das `Region`‑Objekt stellt eine `text`‑Eigenschaft bereit, die das Unicode‑Ergebnis enthält.

```python
for idx, region in enumerate(ocr_result.regions, start=1):
    print(f"Region {idx} text:")
    print(region.text)
    print("-" * 40)
```

**Erwartete Ausgabe (Beispiel)**:

```
Region 1 text:
John Doe
----------------------------------------
Region 2 text:
123 Maple Street
Springfield, IL 62704
----------------------------------------
```

Wenn der Text wirr aussieht, prüfen Sie erneut **wie man die Vorverarbeitung** einstellt: Vielleicht den `contrast` erhöhen oder `binarize` für farbige Logos deaktivieren.

---

## Häufige Stolperfallen und Profi‑Tipps

| Problem | Warum es passiert | Lösung (Wie man die Vorverarbeitung einstellt) |
|---------|-------------------|-----------------------------------------------|
| Schräger Text erscheint als Kauderwelsch | `deskew` deaktiviert oder Bild zu stark gedreht | `preprocessing_options.deskew = True` aktivieren |
| Zahlen werden zu Punkten oder Streifen | Niedriger Kontrast oder aggressive Binärisierung | `contrast` senken (z. B. `1.2`) oder `binarize = False` setzen |
| ROI‑Koordinaten weichen um ein paar Pixel ab | Unterschiedliche DPI oder Scanner‑Skalierung | Werkzeug (z. B. Paint.NET) nutzen, um exakte Pixelpositionen zu messen, oder kleinen Rand (`+5` Pixel) zu jeder ROI hinzufügen |
| Leeres Ergebnis für eine Region | ROI liegt außerhalb der Bildgrenzen | Bildabmessungen prüfen: `source_image.width`, `source_image.height` |

---

## Erweiterung der Lösung (Wie man ROI OCRt in verschiedenen Szenarien)

- **Dynamische ROIs**: Haben Ihre Rechnungen variable Layouts, können Sie zuerst ein schnelles Vollseiten‑OCR ausführen, um Schlüsselwörter („Customer:“, „Address:“) zu finden, und dann die ROIs on‑the‑fly berechnen.  
- **Batch‑Verarbeitung**: Packen Sie die obigen Schritte in eine Funktion und iterieren Sie über einen Ordner mit Bildern. Denken Sie daran, dieselbe `ocr_engine`‑Instanz wiederzuverwenden, um den Speicherverbrauch gering zu halten.  
- **Export nach JSON**: Statt zu drucken, bauen Sie ein Dictionary und schreiben es mit `json.dumps`; das erleichtert die nachgelagerte Integration (z. B. in ein ERP‑System).

```python
import json

def extract_invoice_fields(image_path):
    img = storage.Image.load(image_path)
    result = ocr_engine.recognize(
        img,
        rois=regions_of_interest,
        preprocessing=preprocessing_options
    )
    data = {f"field_{i+1}": r.text.strip() for i, r in enumerate(result.regions)}
    return data

print(json.dumps(extract_invoice_fields("invoice.png"), indent=2))
```

---

## Fazit

Sie haben nun ein vollständiges, ausführbares Beispiel, das **zeigt, wie man ROI OCRt** in Python, während Sie **die Vorverarbeitung** für optimale Genauigkeit beherrschen. Indem Sie die Engine auf die genauen Rechtecke beschränken, die Sie benötigen, und das Bild vorher bereinigen, erhalten Sie schnellere, sauberere Ergebnisse – perfekt für Rechnungsautomatisierung, Formulardigitalisierung oder jedes Szenario, bei dem nur ein Ausschnitt der Seite relevant ist.

Bereit für den nächsten Schritt? Passen Sie die ROI‑Koordinaten für einen anderen Dokumenttyp an oder experimentieren Sie mit zusätzlichen Vorverarbeitungs‑Flags wie `sharpen` oder `noise_reduction`. Die Flexibilität von Aspose OCR ermöglicht es Ihnen, die Pipeline an praktisch jede Bildqualität anzupassen.

Wenn Sie auf ein Problem stoßen, prüfen Sie die Konsolenausgabe auf leere Regionen und überarbeiten Sie die Vorverarbeitungseinstellungen. Viel Spaß beim Coden, und möge Ihre OCR stets präzise sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}