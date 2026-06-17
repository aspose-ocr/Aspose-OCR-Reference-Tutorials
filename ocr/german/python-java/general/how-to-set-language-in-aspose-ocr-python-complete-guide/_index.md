---
category: general
date: 2026-01-12
description: Wie man die Sprache in Aspose OCR Python festlegt und Text aus einem
  Bild mit einem benutzerdefinierten Wörterbuch extrahiert. Schritt‑für‑Schritt‑Tutorial
  für Entwickler.
draft: false
keywords:
- how to set language
- extract text from image
- how to extract text
- how to add dictionary
- how to process image
language: de
og_description: Wie man die Sprache in Aspose OCR Python einstellt und Text aus einem
  Bild mit einem benutzerdefinierten Wörterbuch extrahiert. Lernen Sie den vollständigen
  Workflow in Minuten.
og_title: Wie man die Sprache in Aspose OCR Python einstellt – Komplettanleitung
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Wie man die Sprache in Aspose OCR Python einstellt – Komplettanleitung
url: /de/python-java/general/how-to-set-language-in-aspose-ocr-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man die Sprache in Aspose OCR Python festlegt – Vollständige Anleitung

Haben Sie sich jemals gefragt, **wie man die Sprache** festlegt, wenn man Aspose OCR in Python verwendet? Sie sind nicht allein – viele Entwickler stoßen auf dieses Problem, wenn das standardmäßige englische Modell Produktcodes, Seriennummern oder mehrsprachigen Text nicht erkennt. Die gute Nachricht ist, dass die Lösung sowohl einfach als auch leistungsstark ist. In diesem Tutorial führen wir Sie durch die Konfiguration der Sprache, das Hinzufügen eines benutzerdefinierten Wörterbuchs, das Extrahieren von Text aus einem Bild und schließlich die Bildverarbeitung für die besten OCR-Ergebnisse.

Wir behandeln alles, was Sie wissen müssen: von der Installation der Bibliothek bis zum Ausführen eines vollständigen Beispiels, das den extrahierten Text ausgibt. Am Ende können Sie **Text aus Bild**-Dateien mit Zuversicht extrahieren, selbst wenn der Inhalt ungewöhnliche Codes oder gemischte Sprachen enthält.

## Voraussetzungen

* Python 3.8+ installiert (der Code verwendet f‑Strings, daher funktionieren ältere Versionen nicht).
* Eine aktive Aspose OCR for Python Lizenz oder ein kostenloser Testschlüssel.
* Das `asposeocr`‑Paket installiert via `pip install asposeocr`.
* Ein Beispielbild (`product_label.png`), das den Text enthält, den Sie lesen möchten.

Wenn Sie diese Komponenten bereits haben, großartig – lassen Sie uns weitermachen. Wenn nicht, holen Sie sich die kostenlose Testversion von Asposes Website und führen Sie den Installationsbefehl aus; das dauert nur eine Minute.

## Schritt 1: Importieren des Aspose OCR‑Moduls

Das Erste, was Sie tun müssen, ist, die OCR‑Klassen in Ihr Skript zu importieren. Dies ist die Grundlage für **wie man die Sprache festlegt** später.

```python
# Step 1: Import the Aspose OCR module
import asposeocr as ocr
```

> **Pro Tipp:** Halten Sie Ihre Importe am Anfang der Datei. Das macht das Skript leichter zu überblicken, besonders wenn Sie später zurückkehren.

## Schritt 2: Wie man die Sprache festlegt

Standardmäßig geht Aspose OCR von Englisch aus. Wenn Ihr Bild Französisch, Deutsch oder eine andere Sprache enthält, müssen Sie der Engine mitteilen, welche Sprache verwendet werden soll. Hier kommt das Haupt‑Schlüsselwort zum Einsatz.

```python
# Step 2: Create an OCR engine and set the recognition language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # change to ocr.Language.FRENCH, etc.
```

Warum ist das wichtig? OCR‑Engines basieren auf sprachspezifischen Zeichenmodellen. Die Angabe der richtigen Sprache verbessert die Genauigkeit erheblich – besonders bei Akzentzeichen oder sprachspezifischen Ligaturen.

> **Hinweis:** Wenn Sie mehrere Sprachen gleichzeitig unterstützen müssen, können Sie eine Liste übergeben, z. B. `ocr.Language.ENGLISH | ocr.Language.SPANISH`.

## Schritt 3: Wie man ein Wörterbuch hinzufügt (benutzerdefinierte Wörter)

Manchmal liest die OCR‑Engine Produktcodes wie „AB‑1234“ falsch. Sie können das Vertrauen erhöhen, indem Sie ein benutzerdefiniertes Wörterbuch bereitstellen. Das beantwortet direkt **wie man ein Wörterbuch hinzufügt** in Aspose OCR.

```python
# Step 3: Supply product codes that must be recognized with higher confidence
ocr_engine.set_user_defined_words(["AB-1234", "ZX-9876", "SKU-001"])
```

Die Engine behandelt diese Wörter als „bekannt“ und bevorzugt sie gegenüber ähnlich aussehenden Zeichen. Das ist besonders praktisch für SKU‑Nummern, Seriencodes oder Markennamen, die nicht zu einer natürlichen Sprache gehören.

## Schritt 4: Wie man ein Bild verarbeitet

Jetzt, wo die Engine konfiguriert ist, müssen Sie das Bild laden, das Sie analysieren möchten. Das behandelt **wie man ein Bild verarbeitet** auf eine saubere, wiederholbare Weise.

```python
# Step 4: Load the image containing the product label
image = ocr.Image.load("YOUR_DIRECTORY/product_label.png")
```

Wenn Sie mit PDFs arbeiten, können Sie jede Seite zuerst in ein Bild konvertieren – Aspose OCR unterstützt das von Haus aus.

## Schritt 5: Wie man Text aus einem Bild extrahiert

Wenn alles eingestellt ist, ist der letzte Schritt, die OCR auszuführen und den Text abzurufen. Das ist der Kern von **wie man Text extrahiert** aus einem Bild.

```python
# Step 5: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)

# Step 6: Print the extracted text
print(ocr_result.text)
```

Wenn Sie das Skript ausführen, sollten Sie etwas Ähnliches sehen:

```
Product: AB-1234
Batch: ZX-9876
SKU: SKU-001
```

Wenn die Ausgabe unleserlich erscheint, überprüfen Sie, ob Sie die richtige Sprache eingestellt haben und ob Ihr benutzerdefiniertes Wörterbuch die genauen erwarteten Zeichenketten enthält.

## Vollständiges funktionierendes Beispiel

Wenn wir alles zusammenfügen, finden Sie hier das vollständige Skript, das Sie in eine Datei namens `extract_label.py` kopieren können. Ersetzen Sie `YOUR_DIRECTORY` durch den tatsächlichen Pfad zu Ihrem Bild.

```python
import asposeocr as ocr

# Create OCR engine and set language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # Change if needed

# Add custom dictionary entries
ocr_engine.set_user_defined_words(["AB-1234", "ZX-9876", "SKU-001"])

# Load the target image
image = ocr.Image.load("YOUR_DIRECTORY/product_label.png")

# Perform OCR
ocr_result = ocr_engine.process(image)

# Output the result
print("=== OCR Extraction Result ===")
print(ocr_result.text)
```

### Erwartete Ausgabe

```
=== OCR Extraction Result ===
Product: AB-1234
Batch: ZX-9876
SKU: SKU-001
```

Wenn Sie die genauen Codes sehen, die Sie dem Wörterbuch hinzugefügt haben, haben Sie erfolgreich **wie man die Sprache festlegt**, **wie man ein Wörterbuch hinzufügt** und **wie man Text aus einem Bild extrahiert** mit Aspose OCR gemeistert.

## Umgang mit häufigen Randfällen

| Situation | Was zu tun ist |
|-----------|----------------|
| **Bild ist unscharf** | Vorverarbeiten mit `ocr.Image.apply_filter()`, um das Bild zu schärfen, bevor `process()` aufgerufen wird. |
| **Mehrere Sprachen in einem Bild** | Setzen Sie `ocr_engine.language = ocr.Language.ENGLISH | ocr.Language.SPANISH`. |
| **Große PDFs** | Durchlaufen Sie jede Seite, konvertieren Sie sie zu `ocr.Image` und rufen Sie `process()` pro Seite auf. |
| **Unerwartete Zeichen** | Fügen Sie sie der Liste benutzerdefinierter Wörter hinzu; Aspose OCR behandelt sie als hochzuverlässige Token. |

## Visuelle Referenz

![how to set language in Aspose OCR Beispiel](image.png "Screenshot, der zeigt, wie man die Sprache in Aspose OCR Python Beispiel festlegt")

*Alt-Text:* **how to set language** Screenshot, die die Zuweisung der Spracheigenschaft in einer Python‑IDE veranschaulicht.

## Fazit

Sie wissen jetzt, **wie man die Sprache** in Aspose OCR Python festlegt, wie man **Wörterbuch**‑Einträge hinzufügt und die genauen Schritte, um **Text aus Bild** zu **extrahieren** und **Bild**‑Dateien für optimale Ergebnisse zu **verarbeiten**. Das obige vollständige Beispiel kann in jedes Projekt eingefügt, für verschiedene Sprachen angepasst und erweitert werden, um Stapelverarbeitung oder PDF‑Eingaben zu handhaben.

Bereit für die nächste Herausforderung? Versuchen Sie, `ocr.Language.ENGLISH` durch `ocr.Language.FRENCH` zu ersetzen und beobachten Sie die Genauigkeitssteigerung bei französischsprachigen Etiketten. Oder experimentieren Sie mit der Methode `set_user_defined_words`, um einen gesamten Produktkatalog einzubeziehen – Ihre OCR‑Engine wird jeden Eintrag als hochzuverlässige Übereinstimmung behandeln.

Viel Spaß beim Programmieren, und mögen Ihre OCR‑Ergebnisse stets kristallklar sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}