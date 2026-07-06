---
category: general
date: 2026-04-26
description: Wie man OCR auf einem gescannten Formular ausführt, lernt, das Bild zur
  Rauschreduzierung vorzubereiten, und Text schnell aus dem Bild extrahiert.
draft: false
keywords:
- how to run OCR
- how to preprocess image
- extract text from image
- how to extract text
- how to reduce noise
language: de
og_description: Wie man OCR auf gescannten Dokumenten ausführt, Bilder vorverarbeitet,
  Rauschen reduziert und Text effizient extrahiert.
og_title: Wie man OCR ausführt und Bilder vorverarbeitet – Schnellleitfaden
tags:
- OCR
- image processing
- Python
title: Wie man OCR ausführt und Bilder vorverarbeitet – Text aus gescannten Formularen
  extrahieren
url: /de/python-java/general/how-to-run-ocr-and-preprocess-images-extract-text-from-scann/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR ausführt – Ein vollständiger Leitfaden zum Extrahieren von Text aus Bildern

Haben Sie sich schon einmal gefragt, **wie man OCR** auf einem unordentlichen gescannten Formular ausführt und sauberen, durchsuchbaren Text erhält? Sie sind nicht allein. In vielen realen Projekten ist das Rohbild voller Sprenkel, ungleichmäßiger Beleuchtung und anderer Eigenheiten, die ein Standard‑OCR zum Stolpern bringen.  

Die gute Nachricht? Mit nur wenigen Zeilen Python und einer intelligenten Vorverarbeitungspipeline können Sie die Erkennungsgenauigkeit dramatisch steigern, **Rauschen reduzieren** und exakt die Wörter extrahieren, die Sie benötigen. In diesem Tutorial gehen wir jeden Schritt durch – vom Laden des Bildes bis zum Ausgeben des finalen Strings – sodass Sie am Ende ein sofort einsetzbares Snippet haben, das Sie an Rechnungen, Quittungen oder jedes gescannte Dokument anpassen können.

## Was Sie bauen werden

- Eine `OcrEngine`‑Instanz, die mit der zugrunde liegenden OCR‑Bibliothek kommuniziert.  
- Eine Vorverarbeitungskette, die das Bild **binarisiert** und einen **Median‑Blur** anwendet, um Sprenkel zu glätten.  
- Einen einfachen Aufruf von `process()`, der ein Objekt zurückgibt, das `text` enthält, den extrahierten String.  

Am Ende haben Sie ein eigenständiges Skript, das Sie auf jeder Bilddatei ausführen können und sofort den extrahierten Text in der Konsole sehen.

## Voraussetzungen

- Python 3.9+ (die hier verwendete Syntax entspricht der neuesten stabilen Version).  
- Das fiktive `aocr`‑Paket – denken Sie an einen dünnen Wrapper um Tesseract oder jede moderne OCR‑Engine. Installieren Sie es mit `pip install aocr`.  
- Ein gescanntes Bild (`scanned_form.jpg`) in einem Ordner, den Sie referenzieren können.  

Wenn Sie eine echte OCR‑Bibliothek wie `pytesseract` verwenden, können Sie `OcrEngine` durch die entsprechende Klasse ersetzen – alles andere bleibt gleich.

![](how-to-run-ocr-example.png "Beispiel für OCR: Gescanntes Formular und extrahierter Text")

*Alt‑Text: Wie man OCR auf einem gescannten Dokument ausführt und den extrahierten Text anzeigt.*

---

## Schritt 1: Wie man OCR ausführt – Engine initialisieren

Bevor die Engine irgendetwas lesen kann, müssen wir eine Instanz erstellen. Denken Sie an die `OcrEngine` als das Gehirn, das später die visuellen Daten interpretiert.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()
```

> **Warum das wichtig ist:** Das Instanziieren der Engine richtet interne Modelle ein, lädt Sprachpakete und bereitet die Laufzeitumgebung vor. Das Überspringen dieses Schrittes führt meist zu einem `NoneType`‑Fehler, wenn Sie später `process()` aufrufen.

---

## Schritt 2: Wie man Bild vorverarbeitet – Gescanntes Formular laden

Jetzt, wo das Gehirn bereit ist, füttern wir es mit einem Bild. Das Bild kann jedes von `aocr.Image` unterstützte Format sein.

```python
# Step 2: Load the image you want to recognize
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/scanned_form.jpg")
```

> **Pro‑Tipp:** Verwenden Sie während der Entwicklung absolute Pfade, um „Datei nicht gefunden“-Überraschungen zu vermeiden, wenn das Skript aus einem anderen Arbeitsverzeichnis ausgeführt wird.

---

## Schritt 3: Wie man Rauschen reduziert – Binarisierung & Median‑Blur anwenden

Roh‑Scans enthalten oft lose Punkte, ungleichmäßigen Hintergrund oder schwache Schatten. Zwei klassische Tricks – **Binarisierung** und **Median‑Blur** – säubern das Bild, ohne die Kanten zu verlieren, die Zeichen definieren.

```python
# Step 3: Pre‑process the image to improve recognition accuracy
# • Binarize converts the image to black‑and‑white using a threshold
# • Median blur reduces noise while preserving edges
ocr_engine.image = ocr_engine.image.apply_filters(
    aocr.ImageFilters.binarize(threshold=180),
    aocr.ImageFilters.median_blur(radius=2)
)
```

### Tiefer einsteigen

- **Binarisierung**: Der Wert `threshold=180` sagt dem Algorithmus: „Alles, was heller als 180 ist, wird weiß; alles andere wird schwarz.“ Passen Sie diese Zahl an, wenn Ihr Scan zu dunkel oder zu hell ist.  
- **Median‑Blur**: Ein Radius von `2` bedeutet, dass der Filter ein 5×5‑Pixel‑Fenster betrachtet und das zentrale Pixel durch den Medianwert ersetzt. Das glättet isolierte Sprenkel, während die Striche der Buchstaben erhalten bleiben.

> **Randfall:** Wenn Ihr Dokument farbige Markierungen enthält, kann ein einfacher binärer Schwellenwert diese entfernen. In diesem Szenario sollten Sie stattdessen `aocr.ImageFilters.adaptive_threshold()` verwenden – dieser passt den Schwellenwert lokal über das Bild hinweg an.

---

## Schritt 4: Wie man Text extrahiert – OCR‑Prozess ausführen

Mit einem bereinigten Bild lassen wir schließlich die Engine ihre Magie wirken.

```python
# Step 4: Run the OCR process on the prepared image
ocr_result = ocr_engine.process()
```

> **Was im Hintergrund passiert:** Die Engine läuft ein neuronales Netzwerk (oder einen klassischen Muster‑Matcher) über die Pixelmatrix, übersetzt jedes erkannte Glyph in Unicode‑Zeichen und fügt sie zu Zeilen und Absätzen zusammen.

---

## Schritt 5: Wie man Text extrahiert – Ergebnis ausgeben

Das Objekt `ocr_result` stellt ein praktisches Attribut `text` bereit. Schauen wir, was wir erhalten haben.

```python
# Step 5: Print the extracted text
print(ocr_result.text)
```

### Erwartete Ausgabe

Wenn das gescannte Formular enthält:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Sollten Sie etwas Ähnliches sehen:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Beachten Sie, wie der Vorverarbeitungsschritt lose Punkte eliminiert hat, die zuvor „Amount“ zu „Am0unt“ machten. Das ist die Kraft, **Rauschen zu reduzieren** bevor OCR angewendet wird.

---

## Häufige Fallstricke & wie man sie behebt

| Symptom | Wahrscheinliche Ursache | Schnelle Lösung |
|---------|--------------------------|-----------------|
| Verzerrte Zeichen (z. B. “@#%”) | Bild zu dunkel oder zu hell | `threshold` in `binarize()` anpassen; `adaptive_threshold` probieren. |
| Fehlende Wörter | Rauschen noch vorhanden | `radius` für `median_blur` erhöhen oder einen `gaussian_blur`‑Filter hinzufügen. |
| Falsche Sprache (z. B. englische Buchstaben werden zu Chinesisch) | Falsches Sprachpaket geladen | Beim Erstellen von `OcrEngine()` `language="eng"` übergeben, falls die Bibliothek das unterstützt. |
| Langsame Verarbeitung bei großen Dateien | Hohe Auflösung | Bild zuerst verkleinern: `aocr.ImageFilters.resize(width=1200)` vor der Binarisierung. |

---

## Weiterführendes – Nächste Schritte und verwandte Themen

- **Stapelverarbeitung**: Packen Sie die obige Logik in eine Schleife, um Dutzende von Dateien automatisch zu verarbeiten.  
- **Strukturierte Ausgabe**: Verwenden Sie reguläre Ausdrücke auf `ocr_result.text`, um Felder wie Datum oder Betrag herauszuziehen.  
- **Alternative Bibliotheken**: Ersetzen Sie `aocr` durch `pytesseract` – der Code ändert sich nur beim Initialisieren der Engine.  
- **Wie man Bilder für PDFs vorverarbeitet**: Konvertieren Sie jede PDF‑Seite in ein Bild und wenden Sie dann dieselbe Pipeline an.  

Diese Erweiterungen ermöglichen es Ihnen, die Lösung von einem einzelnen Formular zu einer unternehmensweiten Dokumenten‑Ingest‑Pipeline zu skalieren.

---

## Fazit

Wir haben **wie man OCR ausführt** von Anfang bis Ende behandelt, gezeigt, **wie man Bild vorverarbeitet**, um **Rauschen zu reduzieren**, und demonstriert, **wie man Text aus einem Bild extrahiert** mit einem sauberen, reproduzierbaren Skript. Die zentrale Erkenntnis? Ein paar einfache Filter – Binarisierung und Median‑Blur – können einen verrauschten Scan in eine zuverlässige Datenquelle verwandeln und Ihnen Stunden manueller Nachbearbeitung ersparen.

Probieren Sie das Skript mit Ihren eigenen Dokumenten, justieren Sie die Schwellenwerte und beobachten Sie, wie die Genauigkeit steigt. Wenn Sie bereit sind, erkunden Sie die Stapelverarbeitung oder integrieren Sie die Ausgabe in eine Datenbank für durchsuchbare Archive. Viel Spaß beim Programmieren, und möge Ihre OCR immer treffsicher sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}