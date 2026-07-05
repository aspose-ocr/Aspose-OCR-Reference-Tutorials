---
category: general
date: 2026-07-05
description: Wie man ein Bild schnell entneigt. Lernen Sie, das Bild für OCR vorzubereiten,
  die Bildrotation zu korrigieren und den Scan mit Python in Text umzuwandeln.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- convert scan to text
- correct image rotation
language: de
og_description: Wie man ein Bild entneigt und für OCR vorverarbeitet. Dieser Leitfaden
  zeigt, wie man die Bildrotation korrigiert und Text aus einem Bild mit Python extrahiert.
og_title: Wie man ein Bild entzerrt – Schritt-für-Schritt OCR-Vorverarbeitung
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to deskew image quickly. Learn to preprocess image for OCR, correct
    image rotation, and convert scan to text with Python.
  headline: How to Deskew Image – Complete Guide for OCR Preprocessing
  type: TechArticle
tags:
- OCR
- image-processing
- Python
title: Wie man ein Bild begradigt – Vollständiger Leitfaden zur OCR‑Vorverarbeitung
url: /de/python-java/general/how-to-deskew-image-complete-guide-for-ocr-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein Bild deskewt – Vollständiger Leitfaden zur OCR‑Vorverarbeitung

Haben Sie sich schon einmal gefragt, **wie man ein Bild deskewt**, das aussieht, als wäre es von einem schiefen Scanner aufgenommen worden? Sie sind nicht allein. In vielen realen Projekten ist das Erste, was Sie tun müssen, bevor Sie **Text aus Bild extrahieren** können, das Bild zu begradigen.  

In diesem Tutorial gehen wir Schritt für Schritt durch ein praxisnahes End‑to‑End‑Beispiel, das **Bild für OCR vorverarbeitet**, die Rotation korrigiert und schließlich **Scan in Text umwandelt** mithilfe einer Python‑OCR‑Bibliothek. Keine vagen Verweise, nur ein funktionierendes Skript, das Sie kopieren‑einfügen können, plus Tipps zu häufigen Fallstricken.  

## Was Sie erreichen werden

Am Ende dieses Leitfadens können Sie:

* Jedes gescannte JPEG oder PNG, das leicht gekippt ist, laden.  
* Einen Deskew‑Filter und einen Binarisierungsschritt anwenden, um die OCR‑Genauigkeit zu steigern.  
* Die OCR‑Engine ausführen und **Text aus Bild zuverlässig extrahieren**.  
* Verstehen, warum **korrekte Bildrotation** für die nachgelagerte Textextraktion wichtig ist.  

### Voraussetzungen

* Python 3.9+ auf Ihrem Rechner installiert.  
* Ein per pip installierbares OCR‑Paket, das den im Beispiel verwendeten `ocr`‑Namensraum nachahmt (z. B. ein leichter Wrapper um Tesseract).  
* Grundlegende Kenntnisse von Python‑Funktionen und Bildverarbeitungskonzepten.  

Wenn Sie das haben, legen wir los.

![how to deskew image example](deskew_before_after.png){alt="how to deskew image – Vorher und nach Korrektur"}

## Schritt 1: OCR‑Engine einrichten – Wie man ein Bild mit Python deskewt

Zuerst benötigen Sie eine OCR‑Engine, die die Sprache Ihres Dokuments versteht. Das Snippet unten zeigt das minimale Boilerplate, um die Engine zu erstellen und ihr mitzuteilen, dass Sie mit englischem Text arbeiten.

```python
import ocr  # Assume this is a wrapper around your OCR backend

# Create an OCR engine instance and set the language
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH
```

*Warum das wichtig ist:*  Die Spracheinstellung der Engine beeinflusst den Zeichensatz und das Wörterbuch, das sie verwendet. Das Überspringen dieses Schrittes kann dazu führen, dass die OCR häufige Wörter missversteht, besonders nachdem Sie **korrekte Bildrotation** durchgeführt haben.

## Schritt 2: Das gescannte Bild laden, das Sie begradigen möchten

Jetzt bringen wir die Datei in den Speicher. Ersetzen Sie `"YOUR_DIRECTORY/skewed_scan.jpg"` durch den Pfad zu Ihrem eigenen Bild.

```python
# Load the raw scanned image
raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")
```

Falls das Bild bereits in einem NumPy‑Array oder einem OpenCV `Mat` vorliegt, können Sie den Loader entsprechend anpassen – entscheidend ist, dass das Objekt die später verwendete Methode `apply_filter` bereitstellt.

## Schritt 3: Bild für OCR vorverarbeiten – Deskew und Binarisieren

Hier passiert die Magie. Wir verketten zwei Filter:

1. **Deskew** – erkennt automatisch die dominante Textgrundlinie und dreht das Bild wieder horizontal.  
2. **Binarisieren (Otsu)** – wandelt das Bild in reines Schwarz‑weiß um, was die Erkennungsraten dramatisch verbessert.

```python
# Preprocess: deskew then binarize
preprocessed_image = (
    raw_image
    .apply_filter(ocr.Filter.deskew())          # <-- how to deskew image
    .apply_filter(ocr.Filter.binarize_otsu())  # improves OCR reliability
)
```

*Pro‑Tipp:*  Wenn der Text nach der Binarisierung noch unscharf wirkt, versuchen Sie, den Kontrast anzupassen oder ein anderes Schwellenwertverfahren zu verwenden. Das Modul `ocr.Filter` enthält häufig `adaptive_threshold()` für schwierigere Fälle.

## Schritt 4: OCR ausführen – Text aus Bild extrahieren

Mit einer sauberen, begradigten Leinwand übergeben wir das Bild an die Engine. Das Ergebnis‑Objekt enthält den erkannten String, Vertrauenswerte und sogar Begrenzungsrahmen, falls Sie diese später benötigen.

```python
# Perform recognition on the preprocessed image
recognition_result = engine.recognize(preprocessed_image)

# Print the raw text output
print(recognition_result.text)
```

Typische Ausgabe sieht so aus:

```
Invoice #12345
Date: 2026-07-01
Total: $1,250.00
Thank you for your business!
```

Sie sehen, wie die Zeilenumbrüche perfekt ausgerichtet sind? Das ist der Nutzen von **korrekter Bildrotation** – die OCR muss die Zeilenorientierung nicht mehr erraten.

## Schritt 5: Alles zusammenführen – Ein‑Datei‑Skript zum Konvertieren von Scans in Text

Unten finden Sie das vollständige, ausführbare Skript, das alle besprochenen Teile kombiniert. Speichern Sie es als `deskew_ocr.py` und führen Sie `python deskew_ocr.py` aus.

```python
#!/usr/bin/env python3
"""
Complete example: how to deskew image, preprocess it for OCR,
and extract text from a scanned document.
"""

import ocr  # Replace with your actual OCR library import

def main():
    # 1️⃣ Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # 2️⃣ Load the image (change path as needed)
    raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")

    # 3️⃣ Preprocess – deskew then binarize
    preprocessed = (
        raw_image
        .apply_filter(ocr.Filter.deskew())          # how to deskew image
        .apply_filter(ocr.Filter.binarize_otsu())  # preprocess image for OCR
    )

    # 4️⃣ Recognize text
    result = engine.recognize(preprocessed)

    # 5️⃣ Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

### Warum das funktioniert

* **Deskew zuerst** – das Bild vor der Binarisierung zu drehen sorgt dafür, dass der Schwellenwert‑Algorithmus auf einer ebenen Horizontlinie arbeitet.  
* **Binarisieren nach Deskew** – Otsus Methode geht von einem bimodalen Histogramm aus; eine gekippte Seite würde diese Annahme zerstören.  
* **Englisches Sprachmodell** – teilt der OCR mit, welche Zeichen zu erwarten sind, und reduziert Fehlalarme.  

Wenn Sie andere Sprachen verarbeiten müssen, tauschen Sie einfach `ocr.Language.ENGLISH` gegen das passende Enum aus.

## Häufige Fragen & Sonderfälle

| Frage | Antwort |
|----------|--------|
| *Was, wenn der Scan verkehrt herum ist?* | Der `deskew()`‑Filter erkennt in der Regel auch eine 180°‑Drehung. Falls er scheitert, rufen Sie `apply_filter(ocr.Filter.rotate(180))` vor dem Deskew‑Vorgang auf. |
| *Mein Dokument enthält farbige Grafiken – wird die Binarisierung sie entfernen?* | Ja. Für gemischte Inhalte sollten Sie nur `ocr.Filter.deskew()` verwenden und anschließend die OCR auf dem Farbbild ausführen. Sie können weiterhin Text extrahieren und gleichzeitig die Grafiken erhalten. |
| *Kann ich eine Stapelverarbeitung von Dateien durchführen?* | Verpacken Sie die Logik in einer Schleife, lesen Sie jeden Dateipfad aus einer Liste und speichern Sie jedes `result.text` in einer separaten `.txt`‑Datei. |
| *Wie kann ich die Genauigkeit bei niedrig aufgelösten Scans verbessern?* | Skalieren Sie das Bild mit einem bikubischen Filter **vor** dem Deskew‑Schritt hoch und wenden Sie anschließend einen Schärfungsfilter an. Mehr Pixel geben der OCR‑Engine bessere Anhaltspunkte. |

## Bonus: Visuelle Überprüfung des Deskew

Wenn Sie das Vorher‑und‑Nachher‑Bild nebeneinander sehen möchten, fügen Sie einen kurzen Matplotlib‑Snippet hinzu:

```python
import matplotlib.pyplot as plt

def show_comparison(original, processed):
    fig, axs = plt.subplots(1, 2, figsize=(10, 4))
    axs[0].imshow(original.to_numpy(), cmap='gray')
    axs[0].set_title('Original')
    axs[0].axis('off')

    axs[1].imshow(processed.to_numpy(), cmap='gray')
    axs[1].set_title('Deskewed & Binarized')
    axs[1].axis('off')
    plt.show()

show_comparison(raw_image, preprocessed)
```

Die korrigierte Ausrichtung zu sehen, kann beruhigend wirken, besonders wenn Sie eine knifflige Stapelverarbeitung von Scans debuggen.

## Fazit

Wir haben behandelt, **wie man ein Bild deskewt**, warum **Bild für OCR vorverarbeiten** essenziell ist und wie man **Text aus Bild extrahiert**, um schließlich **Scan in Text umzuwandeln**. Der Workflow – Laden → Deskew → Binarisieren → Erkennen – stellt sicher, dass die OCR eine saubere, gerade Seite sieht, was zu höherer Genauigkeit und weniger manuellen Korrekturen führt.

Was kommt als Nächstes auf Ihrer OCR‑Reise? Probieren Sie folgendes aus:

* Unterschiedliche Sprachpakete (`ocr.Language.FRENCH` usw.).  
* Einen Layout‑Analyse‑Schritt hinzufügen, um Spalten oder Tabellen zu erkennen.  
* Die OCR‑Ergebnisse in durchsuchbare PDFs exportieren mithilfe einer PDF‑Bibliothek.

Hinterlassen Sie gern einen Kommentar, falls Sie auf ein Problem stoßen, oder teilen Sie Ihre eigenen Optimierungen für besonders hartnäckige Scans. Viel Spaß beim Coden, und mögen Ihre Bilder immer perfekt ausgerichtet sein!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man AspOCR verwendet: Bild‑OCR‑Filter für .NET vorverarbeiten](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Bildtext in C# mit Sprachauswahl mittels Aspose.OCR extrahieren](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Wie man ein Bild OCRt – OCR auf Bild in der Bild‑ und Zeichenerkennung durchführen](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}