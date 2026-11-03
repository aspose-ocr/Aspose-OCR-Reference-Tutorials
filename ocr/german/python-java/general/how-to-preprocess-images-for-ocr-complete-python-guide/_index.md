---
category: general
date: 2026-06-06
description: Wie man Bilder für OCR mit Python vorverarbeitet. Lernen Sie, wie man
  ein Bild mit Otsu binarisiert, gescannte Dokumente entneigt und die OCR‑Genauigkeit
  für deutschen Text verbessert.
draft: false
keywords:
- how to preprocess images for OCR
- binarize image using otsu
- how to deskew scanned documents
- how to improve OCR accuracy
- extract text from german image
language: de
og_description: Wie man Bilder für OCR in Python vorverarbeitet. Dieses Tutorial zeigt,
  wie man Bilder mit Otsu binarisiert, gescannte Dokumente entneigt und die OCR‑Genauigkeit
  für deutsche Bilder verbessert.
og_title: Wie man Bilder für OCR vorverarbeitet – Vollständiger Python-Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  headline: How to Preprocess Images for OCR – Complete Python Guide
  type: TechArticle
- description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  name: How to Preprocess Images for OCR – Complete Python Guide
  steps:
  - name: How to Deskew Scanned Documents
    text: The `deskew` call above is the concrete answer to **how to deskew scanned
      documents**. Internally it estimates the dominant text line angle via Hough
      transform and rotates the image back. If your documents are rotated more than
      5°, bump `max_angle` up, but beware of over‑rotation artifacts.
  - name: Binarize Image Using Otsu
    text: The `binarize(method="otsu")` line directly answers the query **binarize
      image using otsu**. Otsu’s algorithm computes a threshold that minimizes intra‑class
      variance, which is perfect for documents with bimodal histograms (dark text
      vs. light background).
  - name: Expected Output
    text: 'Assuming the sample scan contains the sentence “Die schnelle braune Füchsin
      springt über den faulen Hund.” you should see something like:'
  type: HowTo
tags:
- OCR
- image preprocessing
- Python
- German language
title: Wie man Bilder für OCR vorverarbeitet – Vollständiger Python‑Leitfaden
url: /de/python-java/general/how-to-preprocess-images-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Bilder für OCR vorverarbeitet – Vollständiger Python‑Leitfaden

Haben Sie sich jemals gefragt **wie man Bilder für OCR vorverarbeitet**, damit der Text kristallklar herauskommt? Sie sind nicht allein. Gescannte Dokumente – besonders verrauschte deutsche Seiten – können für jede OCR‑Engine ein Albtraum sein. Die gute Nachricht? Ein paar clevere Vorverarbeitungsschritte können einen unscharfen, gesprenkelten Scan in ein sauberes, maschinenlesbares Bild verwandeln.

In diesem Tutorial führen wir Sie durch ein praktisches Beispiel, das **zeigt, wie man Bilder für OCR vorverarbeitet** mit Python. Sie lernen, **ein Bild mit Otsu zu binarisieren**, **wie man gescannte Dokumente entzerrt**, und insgesamt **wie man die OCR‑Genauigkeit verbessert**, wenn Sie **Text aus deutschen Bilddateien extrahieren** müssen. Kein Schnickschnack, nur ein funktionierendes Skript, das Sie noch heute kopieren‑und‑einfügen können.

## Was Sie benötigen

- **Python 3.9+** (jede aktuelle Version funktioniert)
- Eine OCR‑Bibliothek, die eine `OcrEngine`‑Klasse bereitstellt – für das Demo gehen wir von einem generischen `ocr`‑Paket aus. Installieren Sie es mit `pip install ocr-lib`.
- Ein verrauschter deutscher Scan (`noisy_german_scan.tif`), den Sie testen möchten.
- Grundlegendes Verständnis von Python‑Funktionen (wenn Sie schon einmal ein `def` geschrieben haben, sind Sie bereit).

> **Pro‑Tipp:** Wenn Sie ein anderes OCR‑SDK verwenden (z. B. Tesseract via `pytesseract`), bleiben die Konzepte gleich – passen Sie nur die Methodennamen an.

## Überblick über die Lösung

1. **Eine OCR‑Engine‑Instanz erstellen.**  
2. **Die Erkennungssprache auf Deutsch setzen.**  
3. **Eine benutzerdefinierte Vorverarbeitungspipeline bauen**, die Entzerren, Entrauschen, Binarisierung (Otsu) und Kontraststreckung umfasst.  
4. **Die Pipeline an die Engine anhängen**, sodass jedes Bild automatisch durch sie läuft.  
5. **Die OCR** auf einem verrauschten deutschen Scan ausführen.  
6. **Den extrahierten Text ausgeben**, um das Ergebnis zu prüfen.

Im Folgenden zerlegen wir jeden Schritt, erklären **warum** er wichtig ist und zeigen den genauen Code, den Sie benötigen.

![wie man Bilder für OCR vorverarbeitet Beispiel](image.png "wie man Bilder für OCR vorverarbeitet Beispiel")

## Schritt 1: OCR‑Engine‑Instanz erstellen

Zuerst einmal – ohne Engine passiert nichts. Das `OcrEngine`‑Objekt ist der Einstiegspunkt, der alle nachfolgenden Verarbeitungsschritte koordiniert.

```python
# Step 1: Initialize the OCR engine
from ocr import OcrEngine, Language

ocr_engine = OcrEngine()
```

*Warum das wichtig ist:* Das Initialisieren der Engine richtet interne Ressourcen (wie Sprachmodelle) ein und gibt Ihnen eine saubere Basis, um später eine eigene Pipeline anzuhängen.

## Schritt 2: Erkennungs­sprache auf Deutsch setzen

Die OCR‑Genauigkeit ist stark sprachabhängig. Wenn Sie der Engine mitteilen, dass Deutsch erwartet wird, aktivieren Sie den richtigen Zeichensatz und das passende Sprachmodell.

```python
# Step 2: Tell the engine we’re working with German text
ocr_engine.set_recognition_language(Language.GERMAN)
```

Wenn Sie das überspringen, könnte die Engine standardmäßig Englisch verwenden und Umlaute (ä, ö, ü) sowie das ß‑Zeichen falsch erkennen – ein häufiger Stolperstein bei deutschen Scans.

## Schritt 3: Benutzerdefinierte Vorverarbeitungspipeline erstellen

Dies ist das Herzstück von **wie man Bilder für OCR vorverarbeitet**. Wir verketten vier Transformationen:

| Transformation | Was es macht | Warum es hilft |
|----------------|--------------|----------------|
| **Deskew** | Dreht das Bild wieder horizontal (max 5°) | Scans sind selten perfekt ausgerichtet; das Entzerren entfernt die Schräglage, die die Zeichensegmentierung verwirrt. |
| **Denoise** | Reduziert zufällige Punkte (Stärke 0.7) | Rauschen erzeugt falsche Kanten, die die OCR‑Engine als Zeichen interpretieren könnte. |
| **Binarize (Otsu)** | Wandelt mit Otsus Methode in Schwarz‑Weiß um | Ein sauberes Binärbild liefert der Engine einen starken Kontrast zwischen Vordergrund (Text) und Hintergrund. |
| **Contrast Stretch** | Erweitert den Dynamikbereich | Verbessert die Lesbarkeit schwacher Striche, besonders bei alten Dokumenten. |

```python
# Step 3: Assemble the preprocessing pipeline
preprocessing_pipeline = (
    ocr_engine.preprocessing()
               .deskew(max_angle=5)          # auto‑deskew up to 5°
               .denoise(strength=0.7)       # medium denoise
               .binarize(method="otsu")      # **binarize image using Otsu**
               .contrast(stretch=True)      # auto contrast stretch
)

# Explanation:
# - `deskew` corrects rotation; 5° is a safe ceiling for most scans.
# - `denoise` with 0.7 balances smoothing without erasing thin characters.
# - `binarize` with method "otsu" automatically selects the optimal threshold.
# - `contrast` stretch brightens faint ink while keeping dark ink dark.
```

### Wie man gescannte Dokumente entzerrt

Der Aufruf `deskew` oben ist die konkrete Antwort auf **wie man gescannte Dokumente entzerrt**. Intern schätzt er den dominanten Textzeilenwinkel mittels Hough‑Transformation und rotiert das Bild zurück. Wenn Ihre Dokumente um mehr als 5° gedreht sind, erhöhen Sie `max_angle`, achten Sie jedoch auf mögliche Über‑Rotationsartefakte.

### Bild mit Otsu binarisieren

Die Zeile `binarize(method="otsu")` beantwortet direkt die Frage **binarize image using otsu**. Otsus Algorithmus berechnet einen Schwellenwert, der die intra‑Klassen‑Varianz minimiert – ideal für Dokumente mit bimodalen Histogrammen (dunkler Text vs. heller Hintergrund).

## Schritt 4: Pipeline an die Engine anhängen

Jetzt weisen wir die OCR‑Engine an, jedes eingehende Bild durch die gerade erstellte Pipeline zu schicken.

```python
# Step 4: Register the custom pipeline
ocr_engine.set_preprocessing(preprocessing_pipeline)
```

*Warum das wichtig ist:* Ohne Registrierung würde die Engine den Rohscan verarbeiten und all die von uns konfigurierten Bereinigungen ignorieren. Dieser Schritt stellt sicher, dass **wie man die OCR‑Genauigkeit verbessert**, indem dieselbe Vorverarbeitung konsequent angewendet wird.

## Schritt 5: Text aus einem verrauschten deutschen Scan erkennen

Jetzt wird alles zusammengeführt. Wir geben der Engine ein verrauschtes deutsches Bild und lassen sie die schwere Arbeit erledigen.

```python
# Step 5: Run OCR on the target file
image_path = "YOUR_DIRECTORY/noisy_german_scan.tif"
recognition_result = ocr_engine.recognize_image(image_path)
```

Wenn Sie an der Performance interessiert sind, können Sie den Aufruf zeitlich messen:

```python
import time
start = time.time()
result = ocr_engine.recognize_image(image_path)
print(f"OCR took {time.time() - start:.2f}s")
```

## Schritt 6: Erkannten Text ausgeben

Abschließend drucken wir die extrahierte Zeichenkette. Das ist die direkte Antwort auf **extract text from german image**.

```python
# Step 6: Display the OCR output
print("=== Recognized German Text ===")
print(recognition_result.text)
```

### Erwartete Ausgabe

Angenommen, der Beispiel‑Scan enthält den Satz „Die schnelle braune Füchsin springt über den faulen Hund.“ sollten Sie etwa Folgendes sehen:

```
=== Recognized German Text ===
Die schnelle braune Füchsin springt über den faulen Hund.
```

Wenn die Ausgabe noch verzerrte Zeichen enthält, überlegen Sie, die `denoise`‑Stärke anzupassen oder den `max_angle` für das Entzerren zu erhöhen.

## Häufige Fallstricke & wie man sie behebt

- **Fehlendes Sprachmodell:** Das Vergessen von `set_recognition_language(Language.GERMAN)` führt häufig zu fehlenden Umlauten. Prüfen Sie den Aufruf doppelt.
- **Über‑Entrauschen:** Eine Stärke über 0.9 kann dünne Striche, besonders in älteren Schriften, löschen. Bleiben Sie bei 0.5‑0.7 für die meisten Fälle.
- **Falsches Dateiformat:** Einige OCR‑Engines kommen mit mehrseitigen TIFFs nicht klar. Wenn Sie ein mehrseitiges Dokument haben, teilen Sie es zuerst in Einzelseiten‑Dateien auf.
- **Reihenfolge der Pipeline:** Die gezeigte Reihenfolge (Entzerren → Entrauschen → Binarisieren → Kontrast) ist bewusst gewählt. Binarisieren vor dem Entrauschen kann das Rauschen festsetzen; immer zuerst entrauschen.

## Pipeline erweitern (Was kommt als Nächstes?)

Jetzt, wo Sie eine solide Basis haben, könnten Sie Folgendes hinzufügen:

- **Ein morphologisches Öffnen** einbauen, um kleine Flecken zu säubern (`.morph_open(kernel=3)`).
- **Ein Sprachmodell integrieren** für die Nachbearbeitungskorrektur (`ocr_engine.apply_spellcheck()`).
- **Batch‑Verarbeitung parallelisieren** für große Datensätze mittels `concurrent.futures`.

All das sind natürliche Erweiterungen, die die Kernidee von **wie man Bilder für OCR vorverarbeitet** beibehalten und gleichzeitig **wie man die OCR‑Genauigkeit verbessert** weiter steigern.

## Fazit

Wir haben gerade **wie man Bilder für OCR vorverarbeitet** von Anfang bis Ende behandelt: Engine erstellen, deutsche Sprache setzen, eine Pipeline bauen, die **Bild mit Otsu binarisiert**, **wie man gescannte Dokumente entzerrt**, und schließlich **Text aus deutschem Bild extrahiert** mit höherer Zuverlässigkeit. Wenn Sie die sechs Schritte oben befolgen, werden Sie einen spürbaren Sprung in der Erkennungsqualität sehen – keine endlosen manuellen Korrekturen mehr.

Probieren Sie das Skript mit Ihren eigenen Scans aus, experimentieren Sie mit den Parametern und lassen Sie die Ergebnisse für sich sprechen. Haben Sie Fragen zu einer bestimmten Vorverarbeitungs‑Optimierung? Hinterlassen Sie einen Kommentar, und wir tauchen gemeinsam tiefer ein.

Viel Spaß beim Coden, und möge Ihre OCR stets präzise sein!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Bildtext in C# extrahieren mit Sprachauswahl mittels Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Wie man Schwellenwert im OCR‑Bilderkennung festlegt](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Wie man ein Bild OCR‑t – OCR auf Bild ausführen in OCR‑Bilderkennung](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}