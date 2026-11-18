---
category: general
date: 2026-06-22
description: Führen Sie OCR auf einem Bild mit Python in nur wenigen Zeilen durch.
  Lernen Sie, wie Sie ein Bild für OCR laden, Text aus PNG erkennen und die OCR‑Engine
  effizient nutzen.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- load image for OCR
- use OCR engine
language: de
og_description: Führen Sie OCR schnell mit Python auf Bildern durch. Dieses Tutorial
  zeigt, wie man ein Bild für OCR lädt, Text aus einer PNG-Datei erkennt und die OCR‑Engine
  mit Vertrauen nutzt.
og_title: OCR in Python auf Bild ausführen – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Python in just a few lines. Learn how to
    load image for OCR, recognize text from PNG, and use OCR engine efficiently.
  headline: Perform OCR on Image in Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: OCR auf Bild in Python durchführen – Vollständige Anleitung
url: /de/python-java/general/perform-ocr-on-image-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR in Bildern mit Python durchführen – Vollständige Anleitung

Haben Sie schon einmal **OCR auf Bild**‑Dateien ausführen wollen, aber sind schon bei der ersten Code‑Zeile hängen geblieben? Sie sind nicht allein. In diesem Leitfaden zeigen wir Ihnen genau, wie Sie **ein Bild für OCR laden**, eine leichte **OCR‑Engine** einrichten und schließlich **Text aus PNG** mit nur wenigen Befehlen erkennen.

Wir behandeln alles von der Installation der Bibliothek bis zum Anpassen der Whitelist, sodass nur Ziffern und Großbuchstaben den Scan überstehen. Am Ende haben Sie ein sofort einsatzbereites Skript, das Sie in jedes Projekt einbinden können – ohne Rätsel, ohne überflüssigen Schnickschnack.

## Was Sie lernen werden

- Wie man die **OCR‑Engine** programmgesteuert in Python verwendet.  
- Die genauen Schritte, um **ein Bild für OCR** aus einem lokalen Ordner zu **laden**.  
- Warum und wie man die Erkennung auf einen benutzerdefinierten Zeichensatz beschränkt.  
- Wie man **Text aus PNG** erkennt und das Ergebnis sicher verarbeitet.  

**Voraussetzungen:** Python 3.7+ installiert, ein Terminal, mit dem Sie sich auskennen, und ein Bild (z. B. `serial-number.png`), das Sie auslesen möchten. Keine vorherige OCR‑Erfahrung nötig.

---

## OCR auf Bild ausführen – OCR‑Engine initialisieren

Das Erste, was Sie tun müssen, ist eine Instanz der OCR‑Engine zu erstellen. Denken Sie an die Engine als das Gehirn, das die Pixel analysiert und in Zeichen umwandelt.

```python
import ocr  # Assuming the OCR library is named `ocr`

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Warum das wichtig ist:* Ohne Engine gibt es nichts, das das Bild verarbeitet. Die Klasse `OcrEngine` bündelt das gesamte Heavy‑Lifting – Vorverarbeitung, Segmentierung und Zeichenklassifizierung – in einem einzigen Objekt, das Sie wiederverwenden können.

---

## Bild für OCR laden – PNG‑Datei bereitstellen

Jetzt, wo die Engine existiert, müssen Sie ihr das Bild geben, das Sie lesen wollen. Die Bibliothek erwartet ein `ImageStream`‑Objekt, das Sie direkt aus einem Dateipfad erstellen können.

```python
# Step 2: Load the image to be processed
image_path = "YOUR_DIRECTORY/serial-number.png"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

*Pro‑Tipp:* Halten Sie das Bild in einem hochkontrastiven Format (schwarzer Text auf weißem Hintergrund) und vermeiden Sie Kompressionsartefakte; diese können den OCR‑Algorithmus verwirren.

---

## Zeichen einschränken – Whitelist für Ziffern und Großbuchstaben

Oft interessiert Sie nur ein Teil der Zeichen – zum Beispiel eine Seriennummer, die ausschließlich A‑Z und 0‑9 enthält. Durch das Setzen einer Whitelist sagen Sie der Engine, alles andere zu ignorieren, was die Genauigkeit dramatisch erhöht.

```python
# Step 3: Restrict recognition to digits and uppercase letters
whitelist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
engine.get_settings().set_whitelist(whitelist)
```

*Was passiert im Hintergrund?* Die Engine baut einen Filter, der jedes Glyph, das nicht in der Whitelist steht, vor der finalen Klassifizierungsphase verwirft. Das ist besonders praktisch, wenn das Bild Rauschen oder dekorativen Text enthält, den Sie nicht benötigen.

---

## Text aus PNG erkennen – OCR‑Prozess starten

Mit der vorbereiteten Engine und dem geladenen Bild können Sie endlich **OCR auf Bild** ausführen. Der Aufruf `recognize()` führt die gesamte Pipeline aus und liefert ein Ergebnis‑Objekt zurück.

```python
# Step 4: Perform OCR on the image
result = engine.recognize()
```

Wenn Sie an der Performance interessiert sind: Die Methode beendet sich typischerweise nach wenigen hundert Millisekunden für ein 300 × 200 px PNG auf einem modernen Laptop.

---

## Ausgabe und Verifizierung – Erkannten Text erhalten

Der letzte Schritt besteht darin, den Klartext aus dem Ergebnis‑Objekt zu extrahieren. Alles, was nicht zur Whitelist passt, wird automatisch verworfen, sodass Sie einen sauberen String für die weitere Verarbeitung erhalten.

```python
# Step 5: Output the recognized text (characters outside the whitelist are ignored)
recognized_text = result.get_text()
print(recognized_text)
```

*Typische Ausgabe:* `AB12C3D4E5` (vorausgesetzt, das Bild enthielt genau diese Seriennummer).  

Ist die Ausgabe leer oder unleserlich, prüfen Sie die Bildqualität und die Whitelist; ein häufiger Stolperstein ist das versehentliche Weglassen benötigter Zeichen.

---

## Sonderfälle & häufige Fallen

| Situation | Was zu prüfen ist | Empfohlene Lösung |
|-----------|-------------------|-------------------|
| **Datei nicht gefunden** | Tippfehler im Pfad oder fehlende Datei | Verwenden Sie `os.path.abspath`, um den vollständigen Pfad vor dem Aufruf von `set_image` zu prüfen. |
| **Bild mit geringem Kontrast** | Text verschmilzt mit dem Hintergrund | Wenden Sie einen einfachen Schwellenwert (`Pillow` oder `OpenCV`) an, bevor Sie das Bild an die Engine übergeben. |
| **Unerwartete Zeichen** | Whitelist zu restriktiv | Ergänzen Sie die fehlenden Zeichen in der Whitelist‑Zeichenkette. |
| **Große Bilder** | Langsame Erkennung | Skalieren Sie das Bild auf maximal 1024 px Breite; die OCR‑Qualität bleibt meist hoch. |

---

## Komplettes Skript – Bereit zum Ausführen

Unten finden Sie das vollständige, eigenständige Skript, das alle Bausteine zusammenführt. Speichern Sie es als `ocr_demo.py`, ersetzen Sie `YOUR_DIRECTORY` durch den tatsächlichen Ordner und führen Sie `python ocr_demo.py` aus.

```python
import ocr
import os

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a PNG image and return the recognized text.
    Only uppercase letters and digits are allowed.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Load the PNG image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # Whitelist: A-Z and 0-9
    engine.get_settings().set_whitelist("ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

    # Run recognition
    result = engine.recognize()

    # Return clean text
    return result.get_text()

if __name__ == "__main__":
    # Adjust the path to point to your PNG file
    png_path = "YOUR_DIRECTORY/serial-number.png"
    try:
        text = perform_ocr(png_path)
        print("Recognized text:", text)
    except Exception as e:
        print("Error during OCR:", e)
```

*Erwartete Konsolenausgabe* (wenn das PNG `SN12345` enthält):

```
Recognized text: SN12345
```

---

## Fazit

Sie wissen jetzt genau, wie Sie **OCR auf Bild**‑Dateien in Python durchführen, von **Bild für OCR laden** über **Text aus PNG erkennen** bis hin zur Extraktion eines sauberen Ergebnisses mithilfe einer anpassbaren **OCR‑Engine**. Der Ansatz ist unkompliziert, erweiterbar und funktioniert out‑of‑the‑box für die meisten Seriennummer‑Scans.

Was kommt als Nächstes? Probieren Sie, die Whitelist auf Kleinbuchstaben umzustellen, experimentieren Sie mit anderen Bildformaten (JPEG, BMP) oder integrieren Sie das Skript in eine Batch‑Verarbeitungspipeline. Das gleiche Muster – Engine → Bild → Einstellungen → Erkennen → Ausgabe – gilt für praktisch jede OCR‑Aufgabe, der Sie begegnen.

Haben Sie Fragen oder ein kniffliges Bild, das sich weigert zu kooperieren? Hinterlassen Sie einen Kommentar unten, und happy coding! 

![Diagramm, das die Schritte zur Durchführung von OCR auf Bild mit Python veranschaulicht](https://example.com/ocr-flow.png "Diagramm, das zeigt, wie man OCR auf Bild mit einer Python‑OCR‑Engine durchführt")


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Bild zu Text konvertieren – OCR auf Bild von URL ausführen](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Wie man AspOCR verwendet: Bild‑OCR‑Filter für .NET vorverarbeiten](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Wie man Text aus Bild extrahiert, indem man Rechtecke für OCR vorbereitet](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}