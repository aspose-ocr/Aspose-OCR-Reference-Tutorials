---
category: general
date: 2026-03-18
description: Führen Sie OCR schnell auf einem Bild mit Python aus. Lernen Sie, wie
  Sie Text aus PNG erkennen, ein Bild für OCR laden und Wörter aus dem Bild extrahieren
  – in einer Schritt‑für‑Schritt‑Anleitung.
draft: false
keywords:
- run OCR on image
- recognize text from png
- python OCR example
- extract words from image
- load image for OCR
language: de
og_description: Führen Sie OCR auf einem Bild mit Python aus. Dieses Tutorial zeigt,
  wie man Text aus einer PNG erkennt, das Bild für OCR lädt und Wörter aus dem Bild
  extrahiert, inklusive eines vollständigen Codebeispiels.
og_title: OCR auf Bild ausführen – Python‑Leitfaden
tags:
- OCR
- Python
- Image Processing
title: OCR auf Bild ausführen – Komplettes Python-OCR-Beispiel
url: /de/python-java/general/run-ocr-on-image-complete-python-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR auf Bild ausführen – Komplettes Python OCR Beispiel

Haben Sie jemals **run OCR on image** Dateien ausführen müssen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein; viele Entwickler stoßen an diese Grenze, wenn sie zum ersten Mal die Textextraktion aus gescannten Dokumenten angehen. In diesem Tutorial gehen wir ein **Python OCR example** durch, das Ihnen ermöglicht, **recognize text from PNG** Dateien, **load image for OCR**, und **extract words from image** mit Vertrauenswerten – alles in nur wenigen Codezeilen.

Wir behandeln alles, was Sie benötigen: die erforderliche Bibliothek, wie Sie die Engine einrichten, warum jeder Schritt wichtig ist und wie die Ausgabe aussieht. Am Ende können Sie diesen Code‑Snippet in Ihr eigenes Projekt einfügen und sofort Text aus jedem Bild extrahieren. Kein Schnickschnack, nur eine praktische, ausführbare Lösung.

## Was Sie benötigen

- Python 3.8 oder neuer installiert  
- Das `ocrengine`‑Paket (oder jede Bibliothek, die eine `OcrEngine`‑Klasse bereitstellt). Sie können es über `pip install ocrengine` installieren – passen Sie den Namen an, falls Sie eine andere OCR‑Bibliothek wie `pytesseract` verwenden.  
- Eine Bilddatei (PNG, JPG usw.), die Sie verarbeiten möchten – für diese Anleitung verwenden wir `invoice.png`.  

Das war’s. Keine schweren Abhängigkeiten, keine externen Dienste, nur reines Python.

![run OCR on image example – gescannte Rechnung](/images/run-ocr-on-image.png)

*Alt-Text: run OCR on image example – gescannte Rechnung*

## Schritt 1 – OCR‑Bibliothek installieren und importieren

Zuerst einmal holen wir die OCR‑Engine in unsere Umgebung und importieren sie. Wenn Sie das hypothetische `ocrengine`‑Paket verwenden, sieht der Import folgendermaßen aus:

```python
# Install the package (run once in your terminal)
# pip install ocrengine

# Import the OCR engine class
from ocrengine import OcrEngine
```

**Warum das wichtig ist:** Das Importieren der richtigen Klasse gibt Ihnen Zugriff auf die Methoden, die wir später aufrufen, wie `setImageFromFile` und `recognize`. Wenn Sie diesen Schritt überspringen, wirft Python einen `ModuleNotFoundError` und Sie stecken fest, bevor Sie überhaupt ein Bild laden.

## Schritt 2 – OCR‑Engine‑Instanz erstellen

Jetzt, wo die Bibliothek bereit ist, benötigen wir ein Engine‑Objekt, das die Konfiguration und den Zustand für den Erkennungsprozess hält.

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()
```

*Pro‑Tipp:* Einige OCR‑Engines erlauben es Ihnen, Sprachmodelle oder DPI‑Einstellungen an diesem Punkt anzupassen. Für ein einfaches **python OCR example** funktionieren die Standardwerte, aber wenn Sie mit niedrig aufgelösten Scans arbeiten, sollten Sie sie hier anpassen.

## Schritt 3 – Bild laden, das Sie verarbeiten möchten

Der nächste logische Schritt ist **load image for OCR**. Sie geben der Engine den Dateipfad der PNG (oder eines anderen unterstützten Formats) an, die Sie analysieren möchten.

```python
# Step 3: Load the image you want to process
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice.png")
```

**Was passiert im Hintergrund?** Die Engine liest die Pixeldaten, konvertiert sie in ein Format, das der Erkennungsalgorithmus verstehen kann, und speichert sie intern. Wenn der Dateipfad falsch ist, erhalten Sie einen `FileNotFoundError`, also überprüfen Sie, ob das Bild existiert.

## Schritt 4 – Erkennungsalgorithmus ausführen

Nachdem das Bild geladen ist, führen wir endlich **run OCR on image** aus, um den Textinhalt zu extrahieren.

```python
# Step 4: Run the recognition algorithm to obtain results
ocr_result = ocr_engine.recognize()
```

An diesem Punkt scannt die Engine das Bitmap, wendet Mustererkennung an und gibt ein Objekt zurück, das jedes erkannte Wort, jede Zeile und die Vertrauensmetrik enthält.

## Schritt 5 – Über erkannte Wörter iterieren und Vertrauen anzeigen

Der nützlichste Teil jedes OCR‑Workflows ist das Anzeigen **the confidence** für jedes extrahierte Token. Es zeigt Ihnen, wie sicher die Engine bei jedem Wort ist, sodass Sie bei Bedarf Ergebnisse mit niedrigem Vertrauen herausfiltern können.

```python
# Step 5: Iterate over each recognized word and display its text with confidence
for recognized_word in ocr_result.getWords():
    word_text = recognized_word.getText()
    confidence = recognized_word.getConfidence()   # 0‑100%
    print(f"Word: '{word_text}' – confidence: {confidence}%")
```

**Erwartete Ausgabe** (Beispiel):

```
Word: 'Invoice' – confidence: 98%
Word: 'Number' – confidence: 95%
Word: ':' – confidence: 92%
Word: '2023-07-15' – confidence: 97%
Word: 'Total' – confidence: 96%
Word: ':' – confidence: 93%
Word: '$' – confidence: 88%
Word: '1,250.00' – confidence: 94%
```

Sie können jetzt genau sehen **what words were extracted from the image** und wie zuverlässig jede Erkennung ist. Das ist das Kernstück jeder **extract words from image**‑Pipeline.

## Umgang mit häufigen Randfällen

### Was, wenn das Bild Graustufen ist?

Einige OCR‑Engines funktionieren besser mit Farbbildern. Wenn Sie durchgehend niedriges Vertrauen feststellen, versuchen Sie, die PNG in eine höher kontrastierende Schwarz‑Weiß‑Version zu konvertieren, bevor Sie sie an die Engine übergeben. Pillow kann helfen:

```python
from PIL import Image, ImageOps

img = Image.open("YOUR_DIRECTORY/invoice.png")
bw = ImageOps.grayscale(img).point(lambda x: 0 if x < 128 else 255, '1')
bw.save("YOUR_DIRECTORY/invoice_bw.png")
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice_bw.png")
```

### Umgang mit mehreren Sprachen

Wenn Ihr Dokument sowohl Englisch als auch Spanisch enthält, möchten Sie **recognize text from PNG** mit einem mehrsprachigen Modell verwenden. Die meisten Engines erlauben es, die Sprachliste während der Initialisierung festzulegen:

```python
ocr_engine = OcrEngine(languages=["eng", "spa"])
```

### Filtern von Low‑Confidence‑Wörtern

Manchmal benötigen Sie nur Wörter mit einem Vertrauen von über, sagen wir, 90 %. Ein schneller Filter sieht so aus:

```python
high_confidence_words = [
    w.getText()
    for w in ocr_result.getWords()
    if w.getConfidence() >= 90
]
print(high_confidence_words)
```

## Vollständiges, sofort ausführbares Skript

Wenn wir alles zusammenfügen, erhalten Sie ein einzelnes Skript, das Sie kopieren‑und‑einfügen und sofort ausführen können (ersetzen Sie lediglich den Pfad zu Ihrer PNG).

```python
# run_ocr_on_image.py
# -------------------------------------------------
# Complete Python OCR example: load image for OCR,
# run OCR on image, and extract words from image.
# -------------------------------------------------

# Install the library first:
# pip install ocrengine pillow   # pillow only needed for optional preprocessing

from ocrengine import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the target PNG (replace with your own file)
    image_path = "YOUR_DIRECTORY/invoice.png"
    ocr_engine.setImageFromFile(image_path)

    # 3️⃣ Run recognition
    ocr_result = ocr_engine.recognize()

    # 4️⃣ Print each word with its confidence
    print("\n--- OCR Results ---")
    for word in ocr_result.getWords():
        text = word.getText()
        conf = word.getConfidence()
        print(f"Word: '{text}' – confidence: {conf}%")

if __name__ == "__main__":
    main()
```

Führen Sie es aus mit:

```bash
python run_ocr_on_image.py
```

Sie sollten die Liste der Wörter und Vertrauensprozentsätze in der Konsole ausgegeben sehen, genau wie zuvor gezeigt.

## Häufig gestellte Fragen

**Funktioniert das mit JPG‑ oder TIFF‑Dateien?**  
Absolut. Die `setImageFromFile`‑Methode akzeptiert jedes Format, das die zugrunde liegende Bibliothek dekodieren kann, sodass Sie **run OCR on image**‑Dateien vom Typ JPG, TIFF, BMP usw. verwenden können.

**Kann ich mehrere Bilder in einer Schleife verarbeiten?**  
Natürlich. Packen Sie die Lade‑ und Erkennungsschritte in eine `for`‑Schleife über eine Liste von Dateipfaden. Denken Sie nur daran, die Engine neu zu initialisieren, falls die Bibliothek für jedes Bild eine neue Instanz erfordert.

**Was, wenn ich den Text als einzelnen String statt pro Wort benötige?**  
Die meisten OCR‑Ergebnisobjekte stellen eine `getText()`‑Methode bereit, die das gesamte Dokument zurückgibt. Beispiel:

```python
full_text = ocr_result.getText()
print(full_text)
```

## Nächste Schritte und verwandte Themen

Jetzt, da Sie wissen, wie man **run OCR on image** ausführt, sollten Sie Folgendes erkunden:

- **Post‑processing**: Verwenden Sie reguläre Ausdrücke, um Daten, Beträge oder IDs, die aus Rechnungen extrahiert wurden, zu bereinigen.  
- **Batch processing**: Kombinieren Sie das Skript mit `os.listdir()`, um ganze Ordner gescannter Dokumente zu verarbeiten.  
- **Alternative libraries**: `pytesseract` ist eine beliebte Open‑Source‑Option; der Workflow ist ähnlich – ersetzen Sie einfach die Engine‑Aufrufe.  
- **Exporting results**: Schreiben Sie die extrahierten Wörter und Vertrauenswerte in eine CSV für nachgelagerte Analysen.  

Jede dieser Erweiterungen baut direkt auf dem hier gelegten Fundament auf und ermöglicht es Ihnen, rohe OCR‑Daten in verwertbare Informationen zu verwandeln.

---

### TL;DR

Wir haben ein prägnantes **python OCR example** gezeigt, das demonstriert, wie man **load image for OCR**, **run OCR on image** und **extract words from image** ausführt, während das Vertrauen gemeldet wird. Das vollständige Skript ist bereit zum Ausführen, und Sie haben nun das Wissen, es an jedes Projekt anzupassen, das **recognize text from PNG** (oder andere Formate) benötigt. Probieren Sie es aus, passen Sie die Vertrauensschwellen an und sehen Sie, wie Ihre Anwendungen innerhalb weniger Minuten text‑bewusst werden. Viel Spaß beim Programmieren!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}