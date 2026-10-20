---
category: general
date: 2026-03-26
description: Erstellen Sie ein ROI-Polygon, um OCR im ausgewählten Bereich auszuführen.
  Erfahren Sie, wie Sie mehrere Regionen definieren, registrieren und Text mit einer
  Python-OCR-Engine extrahieren.
draft: false
keywords:
- create roi polygon
- ocr on selected area
- region of interest
- ocr engine
- python ocr example
language: de
og_description: Erstelle ein ROI-Polygon und führe OCR im ausgewählten Bereich mit
  einer Python-Engine aus. Vollständiger Code, Erklärungen und Tipps inklusive.
og_title: ROI-Polygon erstellen – Schnelle OCR im ausgewählten Bereich
tags:
- OCR
- Python
- Image Processing
title: ROI‑Polygon erstellen – Schritt‑für‑Schritt‑Anleitung für OCR im ausgewählten
  Bereich
url: /de/python-java/general/create-roi-polygon-step-by-step-guide-for-ocr-on-selected-ar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ROI-Polygon erstellen – Vollständiges Tutorial für OCR im ausgewählten Bereich

Haben Sie schon einmal **ROI-Polygon erstellen** müssen, um OCR nur auf den Teil eines Bildes anzuwenden, der relevant ist? Vielleicht scannen Sie Quittungen und nur die Gesamtsummen sind wichtig, oder Sie haben ein Formular, bei dem nur das Unterschriftsfeld gelesen werden muss. In solchen Fällen spart **ocr on selected area** Zeit und erhöht die Genauigkeit.  

In diesem Leitfaden führen wir Sie durch alles, was Sie benötigen: vom Definieren zweier Polygone, über die Registrierung bei einer OCR-Engine, bis zum Abrufen des erkannten Textes in einem einzigen Aufruf. Am Ende haben Sie ein einsatzbereites Skript und ein fundiertes Verständnis dafür, warum das Fokussieren auf Interessensregionen wichtig ist.

## Was Sie lernen werden

- Wie man **ROI-Polygon**-Objekte mit einer typischen OCR-Bibliothek **erstellt**.
- Der Unterschied zwischen der Definition einer einzelnen Region und mehreren.
- Wie man diese Regionen bei der Engine registriert, sodass `ocr on selected area` ausgeführt wird.
- Erwartete Ausgabe und wie man häufige Fallstricke behebt (z. B. überlappende ROIs, leere Ergebnisse).

### Voraussetzungen

- Python 3.8+ installiert.
- Eine OCR-Bibliothek, die die Methoden `Polygon`, `Point` und `add_region_of_interest` bereitstellt (das Beispiel verwendet ein fiktives `ocr`‑Modul; ersetzen Sie es durch Ihr tatsächliches SDK, z. B. Tesseract‑Python‑Wrapper oder EasyOCR).
- Eine Beispielbilddatei (`sample.png`), die Text innerhalb der unten gezeigten Koordinaten enthält.

> **Pro‑Tipp:** Wenn Sie eine echte Bibliothek verwenden, stellen Sie sicher, dass das Bild im gleichen Koordinatenraum geladen wird (Ursprung oben links, X steigt nach rechts, Y steigt nach unten).  

---  

## Schritt 1: Das OCR‑Modul importieren und Ihr Bild laden

Zuerst das OCR‑Paket in den Gültigkeitsbereich holen und das Bild einlesen, das Sie verarbeiten möchten.  

```python
import ocr  # Replace with your actual OCR library import
from pathlib import Path

# Load the image – adjust the path as needed
image_path = Path("sample.png")
ocr_engine = ocr.Engine(image_path)
```

*Warum das wichtig ist:* Die Engine benötigt die Bilddaten, bevor Sie ein **ROI‑Polygon** anhängen können. Einige Bibliotheken erlauben es, das Bild später zu übergeben, aber eine frühe Initialisierung hält den Arbeitsablauf übersichtlich.

## Schritt 2: Das erste ROI‑Polygon definieren

Jetzt erstellen wir die erste Interessensregion. Stellen Sie sich das vor wie das Zeichnen eines Rechtecks um eine Tabellenüberschrift.  

```python
# Step 2: Define the first ROI polygon
first_roi = ocr.Polygon([
    ocr.Point(50, 20),   # top‑left
    ocr.Point(200, 20),  # top‑right
    ocr.Point(200, 80),  # bottom‑right
    ocr.Point(50, 80)    # bottom‑left
])
```

*Erklärung:*  
- `ocr.Point(x, y)` verwendet Pixelkoordinaten.  
- Die Liste der Punkte ist im Uhrzeigersinn geordnet, wie die meisten Engines erwarten.  
- Sie können beliebig viele Punkte hinzufügen, um unregelmäßige Formen zu erstellen; ein Rechteck ist nur ein Spezialfall.

## Schritt 3: Zusätzliche ROI‑Polygone definieren (optional)

Sie müssen nicht bei einem aufhören. Hier ist ein zweites Polygon, das ein Unterschriftsfeld weiter unten auf der Seite erfasst.  

```python
# Step 3: Define the second ROI polygon
second_roi = ocr.Polygon([
    ocr.Point(300, 150),
    ocr.Point(480, 150),
    ocr.Point(480, 210),
    ocr.Point(300, 210)
])
```

*Warum mehr hinzufügen?* Das Ausführen von **ocr on selected area** für mehrere Zonen ermöglicht das Extrahieren verschiedener Datenstücke in einem einzigen Durchlauf, was weitaus schneller ist, als jeden Ausschnitt separat zuzuschneiden und zu verarbeiten.

## Schritt 4: Die ROIs bei der OCR‑Engine registrieren

Wenn die Polygone bereit sind, teilen Sie der Engine mit, welche Bereiche sie untersuchen soll.  

```python
# Step 4: Register the ROIs
ocr_engine.add_region_of_interest(first_roi)
ocr_engine.add_region_of_interest(second_roi)
```

*Wichtiger Hinweis:* Einige SDKs erfordern, dass Sie vor dem Hinzufügen neuer Regionen die Methode `clear_regions()` aufrufen, wenn Sie die Engine für ein weiteres Bild wiederverwenden.

## Schritt 5: OCR ausführen und den Text abrufen

Zum Schluss starten Sie die Erkennung. Die Engine schaut nur innerhalb der gerade hinzugefügten Polygone.  

```python
# Step 5: Perform OCR on the defined regions
recognized_text = ocr_engine.recognize().get_text()
print("=== Recognized Text ===")
print(recognized_text)
```

**Erwartete Ausgabe** (angenommen, `sample.png` enthält die Wörter „Invoice Total: $123.45“ im ersten ROI und „Signature: John Doe“ im zweiten):

```
=== Recognized Text ===
Invoice Total: $123.45
Signature: John Doe
```

Wenn die Ausgabe leer ist, überprüfen Sie, ob die Koordinaten tatsächlich Text überschneiden und ob die Bildauflösung zum Koordinatensystem passt.

## Randfälle & häufige Stolperfallen  

| Situation                               | What to Watch For                               | Fix / Work‑around                              |
|----------------------------------------|--------------------------------------------------|-----------------------------------------------|
| **Überlappende ROIs**                    | Text kann doppelt zurückgegeben werden.                     | Polygone disjunkt halten oder die Ausgabe deduplizieren. |
| **ROI außerhalb der Bildgrenzen**           | Engine kann einen Fehler auslösen oder nichts zurückgeben.    | Koordinaten auf `0 ≤ x < width`, `0 ≤ y < height` begrenzen. |
| **Sehr kleines ROI**                     | Die OCR‑Genauigkeit sinkt wegen unzureichender Pixel. | Polygon um ein paar Pixel erweitern oder das Bild zuerst hochskalieren. |
| **Nicht‑rechteckige Form**               | Einige Engines unterstützen nur konvexe Polygone.      | Komplexe Formen in mehrere konvexe ROIs aufteilen. |
| **Ändernde Bildgröße**                | Hartkodierte Koordinaten werden ungültig.           | ROI‑Koordinaten relativ zu den Bildabmessungen berechnen (z. B. Prozentsätze). |

## Vollständiges funktionierendes Beispiel  

Unten finden Sie das komplette Skript, das Sie kopieren‑und‑einfügen und ausführen können (ersetzen Sie `ocr` durch Ihre tatsächliche Bibliothek).  

```python
import ocr                      # <- your OCR library
from pathlib import Path

# -------------------------------------------------
# Configuration
# -------------------------------------------------
IMAGE_PATH = Path("sample.png")

# -------------------------------------------------
# Initialize OCR engine with the image
# -------------------------------------------------
engine = ocr.Engine(IMAGE_PATH)

# -------------------------------------------------
# Define ROI polygons
# -------------------------------------------------
first_roi = ocr.Polygon([
    ocr.Point(50, 20), ocr.Point(200, 20),
    ocr.Point(200, 80), ocr.Point(50, 80)
])

second_roi = ocr.Polygon([
    ocr.Point(300, 150), ocr.Point(480, 150),
    ocr.Point(480, 210), ocr.Point(300, 210)
])

# -------------------------------------------------
# Register ROIs
# -------------------------------------------------
engine.add_region_of_interest(first_roi)
engine.add_region_of_interest(second_roi)

# -------------------------------------------------
# Run OCR on the selected areas
# -------------------------------------------------
result = engine.recognize().get_text()

print("=== Recognized Text ===")
print(result)
```

Führen Sie es mit `python ocr_roi_example.py` aus und Sie sollten die extrahierten Zeichenketten aus den beiden definierten Zonen sehen.

## Nächste Schritte  

- **Dynamische ROI‑Erzeugung:** Statt hartkodierter Koordinaten Bildverarbeitung (z. B. OpenCV‑Konturenerkennung) verwenden, um Tabellen oder Felder automatisch zu lokalisieren.  
- **Nachbearbeitung:** Leerzeichen entfernen, Regexes anwenden oder Zahlen in passende Datentypen konvertieren.  
- **Batch‑Verarbeitung:** Durchlaufen eines Ordners mit Bildern, wobei dieselben ROI‑Definitionen wiederverwendet werden, wenn das Layout konsistent ist.  

Wenn Sie neugierig auf **ocr on selected area** für komplexere Dokumente sind – denken Sie an mehrseitige PDFs oder gescannte Formulare – schauen Sie sich Bibliotheken an, die eine seitenweise ROI‑Registrierung unterstützen.  

---  

### Visuelle Übersicht  

![Diagramm, das zwei ROI-Polygone auf einem Beispielbild zeigt](roi_diagram.png){alt="Beispiel für das Erstellen von ROI-Polygonen, das zwei ausgewählte Bereiche zeigt"}

---  

## Fazit  

Wir haben gerade **ROI-Polygon**-Objekte erstellt, sie bei einer OCR‑Engine registriert und `ocr on selected area` in einem sauberen, reproduzierbaren Skript ausgeführt. Indem Sie die Engine auf die für Sie relevanten Zonen beschränken, reduzieren Sie die Verarbeitungszeit, verbessern die Genauigkeit und vereinfachen die nachgelagerte Datenverarbeitung erheblich.  

Probieren Sie es mit Ihren eigenen Bildern aus – passen Sie die Koordinaten an, fügen Sie weitere Polygone hinzu oder verbinden Sie die Ausgabe mit einer Datenbank. Der Himmel ist die Grenze, sobald Sie regionenbasiertes OCR beherrschen.  

Haben Sie Fragen oder möchten Sie einen interessanten Anwendungsfall teilen? Hinterlassen Sie unten einen Kommentar, und viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}