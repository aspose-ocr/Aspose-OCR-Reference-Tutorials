---
category: general
date: 2026-07-05
description: Führen Sie OCR auf einem Bild mit Python durch. Lernen Sie, wie Sie ein
  Bild in Text umwandeln, das Bild für OCR laden und kyrillischen Text aus dem Bild
  in wenigen Minuten extrahieren.
draft: false
keywords:
- perform OCR on image
- convert image to text python
- load image for OCR
- extract Cyrillic text from image
- recognize Cyrillic text
language: de
og_description: Führen Sie OCR auf einem Bild in Python durch. Dieser Leitfaden zeigt
  Ihnen, wie Sie ein Bild in Text umwandeln, das Bild für OCR laden und schnell kyrillischen
  Text aus dem Bild extrahieren.
og_title: OCR auf Bild mit Python durchführen – Vollständiges Tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image using Python. Learn how to convert image to text
    python, load image for OCR and extract Cyrillic text from image in minutes.
  headline: Perform OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- Cyrillic
title: OCR auf Bild mit Python durchführen – Vollständige Schritt‑für‑Schritt‑Anleitung
url: /de/python/general/perform-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR auf Bildern mit Python – Vollständige Schritt‑für‑Schritt‑Anleitung

Haben Sie sich jemals gefragt, wie man **OCR auf Bild**‑Dateien durchführt, ohne sie an einen Drittanbieter zu übergeben? Sie sind nicht allein. In vielen Projekten – Passportscanner, Belegdigitalisierer oder Archivierungswerkzeuge – ist das Extrahieren von Rohtext aus einem Bild die erste Hürde.  

In diesem Tutorial gehen wir ein praktisches Beispiel durch, das **image to text python**‑Stil konvertiert, Ihnen zeigt, wie man **load image for OCR** verwendet, und schließlich **extract Cyrillic text from image** mit der Open‑Source‑Bibliothek `aocr` extrahiert. Am Ende können Sie **Cyrillic text** in jedem Bild erkennen, das Sie ihm vorlegen.

> **Was Sie am Ende haben werden:** ein sofort einsatzbereites Skript, klare Erklärungen zu jedem Schritt und Tipps zum Umgang mit häufigen Fallstricken (wie unscharfe Scans oder unerwartete Schriftarten). Keine externen APIs, nur reines Python.

---

## Voraussetzungen

Bevor wir loslegen, stellen Sie sicher, dass Sie Folgendes haben:

- Python 3.8 oder neuer installiert.
- Ein Terminal oder eine Eingabeaufforderung, mit der Sie sich wohlfühlen.
- Das `aocr`‑Paket (installierbar via `pip install aocr`).
- Eine Bilddatei, die kyrillische Zeichen enthält (z. B. ein gescannter russischer Reisepass).  

Falls Ihnen irgendeiner dieser Punkte unbekannt ist, keine Panik – jeder Aufzählungspunkt wird kurz erklärt, während wir fortschreiten.

---

## Schritt 1: OCR auf Bild ausführen – Umgebung einrichten

Das Erste, was wir benötigen, ist eine saubere Python‑Umgebung, in der die OCR‑Bibliothek lebt. Durch die Verwendung einer virtuellen Umgebung werden Abhängigkeiten isoliert und Versionskonflikte vermieden.

```bash
# Create a virtual environment (optional but recommended)
python -m venv ocr-env
# Activate it (Windows)
ocr-env\Scripts\activate
# Activate it (macOS/Linux)
source ocr-env/bin/activate

# Install the aocr library
pip install aocr
```

**Warum?**  
Eine dedizierte Umgebung stellt sicher, dass das `aocr`‑Paket und seine nativen Binärdateien nicht mit anderen Projekten interferieren. Außerdem wird die Reproduzierbarkeit zum Kinderspiel – jemand anderes kann Ihr Repo klonen und denselben `pip install -r requirements.txt`‑Befehl ausführen.

> **Pro‑Tipp:** Frieren Sie Ihre Abhängigkeiten mit `pip freeze > requirements.txt` ein, damit Sie immer genau wissen, welche Versionen verwendet wurden.

---

## Schritt 2: Bild für OCR laden – Importieren und Datei vorbereiten

Jetzt, wo die Bibliothek bereit ist, müssen wir **load image for OCR**. Die Methode `aocr.Image.from_file` unterstützt die gängigsten Formate (PNG, JPEG, TIFF). So geht's:

```python
import aocr

# Path to the Cyrillic image – replace with your actual file location
image_path = "YOUR_DIRECTORY/rus_passport.png"

# Load the image into an aocr.Image object
cyrillic_image = aocr.Image.from_file(image_path)
```

**Was passiert hier?**  
`aocr.Image.from_file` liest die Binärdaten, dekodiert sie und speichert sie in einem Objekt, das die OCR‑Engine verstehen kann. Wenn die Datei nicht gefunden wird, wirft Python einen `FileNotFoundError`, den Sie später abfangen können, falls Sie eine elegante Fehlerbehandlung benötigen.

> **Randfall:** Einige Scanner geben mehrseitige TIFFs aus. In diesem Szenario müssten Sie die Seiten zuerst aufteilen – `aocr` stellt `Image.from_tiff_pages()` dafür bereit.

---

## Schritt 3: OCR‑Engine konfigurieren – Kyrillische Erkennung erzwingen

Standardmäßig versuchen viele OCR‑Engines, die Sprache zu erraten, was zu fehlerhaften Ausgaben für nicht‑lateinische Schriften führen kann. Um **recognize Cyrillic text** zuverlässig zu ermöglichen, setzen wir die Sprache explizit auf „cyrillic“.

```python
# Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Force the engine to use the Cyrillic recognizer
ocr_engine.language = "cyrillic"
```

**Warum die Sprache erzwingen?**  
Kyrillische Zeichen weisen visuelle Ähnlichkeiten zu lateinischen Buchstaben auf (z. B. „A“ vs. „А“). Der Engine mitzuteilen, dass Kyrillisch erwartet wird, reduziert Fehlinterpretationen drastisch, besonders bei niedrig aufgelösten Scans.

---

## Schritt 4: OCR auf Bild ausführen – Erkennung starten

Mit dem geladenen Bild und der abgestimmten Engine führen wir schließlich **perform OCR on image** aus. Die Methode `recognize` liefert ein `OcrResult`‑Objekt, das den extrahierten Text und Konfidenzwerte enthält.

```python
# Run the OCR process
ocr_result = ocr_engine.recognize(cyrillic_image)

# Print the raw text
print("Cyrillic text:")
print(ocr_result.text)
```

**Was liefert `ocr_result`?**  
- `text`: der reine String der erkannten Zeichen.  
- `confidence`: ein Float (0‑1), der die Gesamtsicherheit angibt.  
- `lines`: eine Liste von Zeilenobjekten, falls Sie granularere Kontrolle benötigen.

> **Häufige Frage:** *Was, wenn der Text verkehrt herum ist?*  
> `aocr` kann Bilder automatisch drehen; setzen Sie einfach `ocr_engine.auto_rotate = True`, bevor Sie `recognize` aufrufen.

---

## Schritt 5: Bild zu Text Python – Ausgabe nachbearbeiten

Der rohe String kann überflüssige Leerzeichen oder Zeilenumbrüche enthalten. Um **convert image to text python**‑Stil zu erhalten, bereinigen wir ihn mit ein paar einfachen Schritten:

```python
import re

# Remove extra whitespace and normalize line breaks
clean_text = re.sub(r'\s+', ' ', ocr_result.text).strip()

print("\nCleaned Cyrillic text:")
print(clean_text)
```

**Warum das Ganze?**  
Bereinigte Ausgaben lassen sich leichter in nachgelagerte Pipelines einspeisen – sei es, um sie in einer Datenbank zu speichern, an eine Übersetzungs‑API zu senden oder reguläre Ausdrücke für Reisepassnummern zu verwenden.

---

## Schritt 6: Kyrillischen Text aus Bild extrahieren – Alles zusammenführen

Packen wir alles in eine einzige, wiederverwendbare Funktion. So wird **extract Cyrillic text from image** zu einem Einzeiler in Ihren eigenen Projekten.

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Loads an image, forces Cyrillic OCR, and returns cleaned text.
    """
    # Load image
    img = aocr.Image.from_file(image_path)

    # Configure OCR engine for Cyrillic
    engine = aocr.OcrEngine()
    engine.language = "cyrillic"

    # Recognize text
    result = engine.recognize(img)

    # Clean up the output
    cleaned = re.sub(r'\s+', ' ', result.text).strip()
    return cleaned

# Example usage
if __name__ == "__main__":
    path = "YOUR_DIRECTORY/rus_passport.png"
    print("Extracted text:", extract_cyrillic_text(path))
```

**Erwartetes Ergebnis (Beispiel):**

```
Extracted text: ПАСПОРТ РФ № 1234567890 ИМЯ ФАМИЛИЯ ДАТА РОЖДЕНИЯ 01.01.1990
```

Ist das Bild klar und die Schriftart passt zum OCR‑Modell, erhalten Sie nahezu perfekte Transkription.

---

## Fehlersuche & Tipps

| Problem | Wahrscheinliche Ursache | Lösung |
|---------|--------------------------|--------|
| Verzerrte Zeichen | Falsche Spracheinstellung | Stellen Sie sicher, dass `ocr_engine.language = "cyrillic"` |
| Leere Ausgabe | Bild zu dunkel oder zu niedrige Auflösung | Vorverarbeiten mit `opencv`, um den Kontrast zu erhöhen |
| Falsche Orientierung | Bild um 90° gedreht | Setzen Sie `ocr_engine.auto_rotate = True` |
| Langsame Leistung | Großes Bild ( >5 MP ) | Vor der Erkennung mit `aocr.Image.resize(width=1024)` verkleinern |

---

![perform OCR on image example](ocr_example.png "Beispiel für OCR auf Bild")

*Alt‑Text: „Beispiel für OCR auf Bild, das Python‑Code zeigt, der kyrillischen Text aus einem Reisepass‑Scan extrahiert.“*

---

## Fazit

Wir haben gerade **perform OCR on image**‑Dateien mit reinem Python durchgeführt, gelernt, wie man **load image for OCR** verwendet, die Engine gezwungen hat, **recognize Cyrillic text** zu erkennen, und schließlich **extract Cyrillic text from image** mit einer übersichtlichen Hilfsfunktion extrahiert. Die gesamte Pipeline – vom Installieren von `aocr` bis zum Aufräumen des Ergebnisses – passt in ein paar Dutzend Zeilen Code und lässt sich in jedes Projekt einbinden, das **convert image to text python**‑Stil benötigt.

---

## Was kommt als Nächstes?

- **Batch‑Verarbeitung:** Durchlaufen Sie einen Ordner mit Scans und speichern Sie die Ergebnisse in SQLite.  
- **Spracherkennung:** Kombinieren Sie `langdetect` mit `aocr`, um automatisch zwischen Kyrillisch und Lateinisch zu wechseln.  
- **Erweiterte Vorverarbeitung:** Nutzen Sie `opencv`, um Bilder zu deskewen, zu entrauschen oder zu binarisieren für höhere Genauigkeit.  
- **Integration mit FastAPI:** Stellen Sie die Funktion `extract_cyrillic_text` als REST‑Endpoint für Web‑Apps bereit.

Experimentieren Sie gern – wechseln Sie die Sprache zu „latin“ für englische Reisepässe oder probieren Sie ein anderes OCR‑Backend aus. Die Konzepte bleiben gleich, und der Code ist flexibel genug, um sich anzupassen.

Viel Spaß beim Coden, und mögen Ihre Bilder stets lesbar sein!


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}