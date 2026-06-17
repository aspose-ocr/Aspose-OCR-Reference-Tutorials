---
category: general
date: 2026-01-12
description: Python OCR‑Tutorial, das zeigt, wie man Tabellentext aus einem Bild extrahiert.
  Lernen Sie, Tabellen aus Bildern zu lesen und ausgewählten Text mit Aspose OCR zu
  extrahieren.
draft: false
keywords:
- python ocr tutorial
- extract table text
- read table from image
- extract selected text
- how to extract table
language: de
og_description: Python-OCR-Tutorial, das Ihnen zeigt, wie Sie Tabellentext aus einem
  Bild extrahieren, Tabellen aus Bildern lesen und ausgewählten Text mit Aspose OCR
  extrahieren.
og_title: 'Python OCR Tutorial: Tabellentext aus Bildern extrahieren'
tags:
- OCR
- Python
- AsposeOCR
title: 'Python-OCR-Tutorial: Tabellentext aus Bildern extrahieren'
url: /de/python-java/general/python-ocr-tutorial-extract-table-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR Tutorial: Tabellentext aus Bildern extrahieren

Haben Sie jemals ein **python ocr tutorial** gebraucht, das Ihnen tatsächlich zeigt, wie man eine Tabelle aus einem gescannten Formular extrahiert? Sie sind nicht allein. Die meisten Tutorials bleiben bei der generischen Textextraktion stehen und lassen Sie rätseln, wie Sie das übersichtliche Datengitter, das Sie benötigen, isolieren können.  

In diesem Leitfaden gehen wir ein reales Szenario durch: das Lesen einer Tabelle aus einem Bild, das Extrahieren nur des ausgewählten Textes, den Sie benötigen, und schließlich das Ausgeben der Ergebnisse. Unterwegs geben wir Tipps, wie man **how to extract table** Daten zuverlässig extrahiert, sodass Sie das Rad nicht jedes Mal neu erfinden müssen.

## Was Sie lernen werden

- Wie man Aspose OCR für Python einrichtet.
- Wie man einen rechteckigen Bereich definiert, der eine Tabelle enthält.
- Die genauen Schritte zum **extract table text** und **read table from image**.
- Tipps zum Umgang mit mehreren Sprachen oder unregelmäßigen Tabellenlayouts.
- Ein vollständiges, ausführbares Skript, das Sie noch heute in Ihr Projekt einbinden können.

**Voraussetzungen**  
- Python 3.8 oder neuer.  
- Grundlegende Vertrautheit mit OCR-Konzepten (keine tiefe Expertise erforderlich).  
- Ein PNG- oder JPEG-Bild, das eine klare Tabelle enthält (wir nennen es `form_with_table.png`).  

Wenn Sie das haben, lassen Sie uns eintauchen – ohne Schnickschnack, nur umsetzbarer Code.

![python ocr tutorial example of table region](table_region_example.png){alt="python ocr tutorial Beispiel, das den Tabellenbereich zeigt"}

## Schritt 1: Aspose OCR installieren und importieren

Zuerst benötigen Sie die Aspose OCR-Bibliothek. Das Paket ist auf PyPI verfügbar, sodass ein einzelner `pip`‑Befehl ausreicht.

```bash
pip install aspose-ocr
```

Jetzt importieren Sie das Modul und alle Hilfsfunktionen, die Sie benötigen.

```python
# Step 1: Import the Aspose OCR package
import asposeocr as ocr
```

*Pro‑Tipp:* Halten Sie Ihre Abhängigkeiten in einer `requirements.txt`‑Datei. Das erleichtert das Reproduzieren der Umgebung enorm.

## Schritt 2: OCR‑Engine initialisieren (Python OCR Tutorial Core)

Das Erstellen der Engine ist das Herzstück jedes **python ocr tutorial**. Hier setzen wir außerdem die Standardsprache auf Englisch – Sie können sie später problemlos ändern.

```python
# Step 2: Create an OCR engine and set the default language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

Warum die Sprache festlegen? Die OCR‑Genauigkeit kann stark steigen, wenn die Engine weiß, welche Zeichen zu erwarten sind. Wenn Sie mit mehrsprachigen Formularen arbeiten, können Sie entweder eine Liste von Sprachen festlegen oder pro Region überschreiben (siehe später).

## Schritt 3: Bild laden

Aspose OCR funktioniert mit den meisten gängigen Bildformaten. Zeigen Sie einfach auf den Dateipfad, und Sie erhalten ein `Image`‑Objekt, das bereit zur Verarbeitung ist.

```python
# Step 3: Load the image that contains the form with the table
image_page = ocr.Image.load("YOUR_DIRECTORY/form_with_table.png")
```

*Sonderfall:* Große Bilder (über 5 MB) können die Verarbeitung verlangsamen. Erwägen Sie, sie vor der OCR zu verkleinern oder zu komprimieren, falls die Leistung ein Problem darstellt.

## Schritt 4: Tabellenbereich definieren (Read Table from Image)

Jetzt kommt der spaßige Teil: der Engine mitteilen, *wo* die Tabelle liegt. Sie übergeben ein `OcrRegion` mit einem `Rectangle` (x, y, Breite, Höhe). Die Koordinaten basieren auf Pixeln, sodass Sie ein wenig experimentieren müssen.

```python
# Step 4: Define the rectangular area where the table is located
# (x, y, width, height) – adjust these values for your image
table_region = ocr.OcrRegion(
    image_page,
    ocr.Rectangle(120, 340, 800, 450)
)

# Optional: override language for this specific region
table_region.language = ocr.Language.ENGLISH
```

Warum einen Bereich verwenden? Durch die Begrenzung der OCR auf den Tabellenbereich **extract selected text** wir schneller und vermeiden Rauschen von umliegenden Beschriftungen oder Grafiken. Außerdem verbessert es die Genauigkeit, da sich die Engine auf ein einheitliches Layout konzentrieren kann.

## Schritt 5: OCR im definierten Bereich ausführen

Mit dem gesetzten Bereich rufen wir `process_region` auf. Die Methode gibt ein `OcrResult`‑Objekt zurück, das den Rohtext, Konfidenzwerte und sogar Begrenzungsrahmen enthält, falls Sie diese später benötigen.

```python
# Step 5: Run OCR only on the defined region
region_result = ocr_engine.process_region(table_region)
```

Wenn Sie mehrere Tabellen extrahieren müssen, wiederholen Sie einfach die Schritte 4‑5 mit unterschiedlichen Rechtecken.

## Schritt 6: Extrahierten Tabellentext ausgeben

Zum Schluss geben Sie die textuelle Darstellung der Tabelle aus – oder speichern sie. Aspose OCR liefert Klartext mit Zeilenumbrüchen, die in der Regel den Zeilen entsprechen, was die Nachbearbeitung einfach macht.

```python
# Step 6: Output the extracted table text
print("Table text:\n", region_result.text)
```

**Erwartete Ausgabe** (Beispiel):

```
Table text:
 Item        Qty   Price
 Apple       10    $1.20
 Banana      5     $0.80
 Orange      8     $1.00
```

Sie können diesen String jetzt in `csv`‑Parser, pandas‑DataFrames oder jede nachgelagerte Analyse‑Pipeline einspeisen.

## Vollständiges funktionierendes Beispiel

Alles zusammengeführt, hier das komplette Skript, das Sie sofort ausführen können. Ersetzen Sie `YOUR_DIRECTORY/form_with_table.png` durch den tatsächlichen Pfad zu Ihrem Bild.

```python
# -*- coding: utf-8 -*-
"""
Python OCR Tutorial: Extract Table Text from Images
---------------------------------------------------
A self‑contained example that demonstrates how to read a table from an image
using Aspose OCR for Python.
"""

# Install the library first:
# pip install aspose-ocr

import asposeocr as ocr

def extract_table(image_path, rect):
    """
    Extracts text from a rectangular region that contains a table.

    :param image_path: Path to the PNG/JPEG image.
    :param rect: Tuple (x, y, width, height) defining the table region.
    :return: Plain‑text representation of the table.
    """
    # Initialise OCR engine with English language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Load the image
    img = ocr.Image.load(image_path)

    # Define the region (override language if needed)
    region = ocr.OcrRegion(img, ocr.Rectangle(*rect))
    region.language = ocr.Language.ENGLISH  # optional per‑region override

    # Process only this region
    result = engine.process_region(region)

    return result.text

if __name__ == "__main__":
    # Adjust these coordinates to match your table location
    table_rect = (120, 340, 800, 450)   # x, y, width, height

    # Path to your image file
    img_file = "YOUR_DIRECTORY/form_with_table.png"

    extracted_text = extract_table(img_file, table_rect)
    print("=== Extracted Table Text ===")
    print(extracted_text)
```

Führen Sie das Skript mit `python extract_table.py` aus. Wenn alles passt, wird die Tabelle in Ihrer Konsole ausgegeben.

## Häufige Fragen & Sonderfall‑Behandlung

**Was, wenn die Tabelle nicht perfekt rechteckig ist?**  
Sie können die Tabelle in mehrere überlappende Bereiche aufteilen oder ein größeres Rechteck verwenden, das den gesamten Bereich abdeckt, und anschließend den Text nachbearbeiten (z. B. anhand von Zeilenumbrüchen splitten).

**Kann ich nur bestimmte Spalten extrahieren?**  
Nachdem Sie den vollständigen Tabellentext haben, verwenden Sie Python‑`csv` oder `pandas`, um die gewünschten Spalten herauszuschneiden. Der OCR‑Schritt selbst gibt alles innerhalb des Rechtecks zurück.

**Wie arbeite ich mit nicht‑englischen Tabellen?**  
Setzen Sie `ocr_engine.language` (oder `region.language`) auf das passende Enum, z. B. `ocr.Language.FRENCH` oder kombinieren Sie mehrere Sprachen mit `ocr.Language.ENGLISH | ocr.Language.SPANISH`.

**Gibt es eine Möglichkeit, Begrenzungsrahmen für jede Zelle zu erhalten?**  
Aspose OCR kann `region_result.words` zurückgeben, wobei jedes Wort einen Begrenzungsrahmen enthält. Sie müssten diese Rahmen zurück zu einem Raster zuordnen – nützlich für fortgeschrittene Layout‑Analysen.

## Tipps für bessere Genauigkeit

- **Clean the image**: Binarisieren oder den Kontrast erhöhen, bevor Sie das Bild an OCR übergeben. Bibliotheken wie Pillow können helfen.
- **Avoid compression artifacts**: Speichern Sie Scans nach Möglichkeit als PNG.
- **Mind DPI**: 300 dpi ist ein optimaler Wert; niedrigere Werte können zu fehlenden Zeichen führen.
- **Test different rectangle sizes**: Etwas größere Rechtecke erfassen oft lose Zeichen, die zur Tabelle gehören.

## Nächste Schritte

Jetzt, da Sie **how to extract table** Daten mit Aspose OCR gemeistert haben, könnten Sie folgendes erkunden:

- Den extrahierten Text mit Pythons `csv`‑Modul in eine CSV‑Datei umwandeln.
- Die Daten in ein **pandas**‑DataFrame für Analysen einspeisen.
- OCR zum Lesen handschriftlicher Formulare verwenden (erfordert eine andere Engine oder zusätzliches Training).
- Die Stapelverarbeitung von Dutzenden gescannter Formulare automatisieren mittels einer einfachen `for`‑Schleife.

Jede dieser Erweiterungen baut auf den Kernkonzepten dieses **python ocr tutorial** auf, sodass Sie gut gerüstet sind, um zu skalieren.

---

*Viel Spaß beim Coden! Wenn Sie auf Probleme stoßen, hinterlassen Sie unten einen Kommentar – ich helfe Ihnen gerne, die Extraktion zu optimieren.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}