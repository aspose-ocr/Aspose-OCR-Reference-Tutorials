---
category: general
date: 2026-03-26
description: Erfahren Sie, wie Sie OCR für arabische PNG‑Bilder ausführen und arabischen
  Text schnell extrahieren. Dieser Leitfaden zeigt die Umwandlung von Bild zu Text
  mit Schritt‑für‑Schritt‑Python‑Code.
draft: false
keywords:
- how to run ocr
- extract arabic text
- recognize arabic text
- convert image to text
- extract text from png
language: de
og_description: Wie führt man OCR bei arabischen PNG‑Bildern durch? Folgen Sie dieser
  umfassenden Anleitung, um arabischen Text zu extrahieren, arabischen Text zu erkennen
  und das Bild mit Python in Text zu konvertieren.
og_title: Wie man OCR auf arabischen PNGs ausführt – Text aus dem Bild extrahieren
tags:
- OCR
- Python
- Arabic
title: Wie man OCR auf arabischen PNGs ausführt – Text aus Bild extrahieren
url: /de/python-java/general/how-to-run-ocr-on-arabic-png-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR auf arabischem PNG ausführt – Text aus Bild extrahieren

Haben Sie sich schon einmal gefragt, **wie man OCR** auf einem Bild mit arabischer Schrift ausführt? Vielleicht haben Sie einen gescannten Beleg, ein historisches Manuskript oder einfach einen Screenshot eines Social‑Media‑Posts und benötigen den Text in einem durchsuchbaren Format. Sie sind nicht allein – Entwickler weltweit stoßen bei rechts‑nach‑links‑Sprachen auf dieses Problem.

In diesem Tutorial gehen wir Schritt für Schritt durch ein vollständiges, ausführbares Beispiel, das **zeigt, wie man OCR** auf einer PNG‑Datei ausführt, arabischen Text extrahiert und das Ergebnis in der Konsole ausgibt. Keine vagen „siehe die Docs“-Links; nur Code, den Sie copy‑pasten können, plus Erklärungen, warum jede Zeile wichtig ist. Am Ende können Sie **Bild zu Text** zuverlässig umwandeln, selbst wenn die Quelle ein kniffliges arabisches PNG ist.

> **Was Sie lernen werden**
> - Ein Python‑OCR‑Engine für Arabisch einrichten  
> - Ein PNG‑Bild laden und gängige Stolperfallen behandeln  
> - Arabischen Text erkennen und die Ausgabe prüfen  
> - Tipps zum **Extrahieren arabischen Textes** aus Bildern unterschiedlicher Qualität  

Bevor wir loslegen, stellen Sie sicher, dass Python 3.8+ installiert ist und Sie eine aktuelle Version der `ocr`‑Bibliothek (die im Code‑Snippet verwendete) besitzen. Wenn Sie eine virtuelle Umgebung nutzen, aktivieren Sie sie jetzt – so bleiben Abhängigkeiten übersichtlich.

## Voraussetzungen

- Python 3.8 oder neuer  
- `ocr`‑Paket (`pip install ocr‑engine` – ersetzen Sie dies durch den tatsächlichen Paketnamen)  
- Ein arabisches PNG‑Bild (`arabic_doc.png`), das Sie referenzieren können  
- Grundlegende Kenntnisse von Python‑Funktionen und -Klassen  

Das war’s. Keine schweren Frameworks, keine Docker‑Container – nur reines Python.

## Schritt 1: OCR‑Bibliothek installieren und importieren

Zuerst das Wichtigste. Wir benötigen die OCR‑Engine selbst. Die Bibliothek, die wir verwenden, stellt eine `OcrEngine`‑Klasse mit einer unkomplizierten API bereit.

```python
# Install the library (run once in your terminal)
# pip install ocr-engine   # <-- replace with the correct package name

# Import the necessary classes
import ocr
from ocr import Imaging
```

*Warum `Imaging` separat importieren?* Das `Imaging`‑Untermodul liefert uns die praktische Methode `Image.load`, die PNG, JPEG und TIFF sofort versteht. Würden Sie diesen Schritt überspringen, müssten Sie Roh‑Bytes selbst verarbeiten – das ist für die meisten Anwendungsfälle unnötig.

## Schritt 2: OCR‑Engine‑Instanz erstellen

Jetzt erzeugen wir eine Instanz der Engine. Denken Sie an dieses Objekt als das „Gehirn“, das das Bild verarbeitet.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

> **Pro‑Tipp:** Wenn Sie viele Bilder hintereinander verarbeiten wollen, verwenden Sie dieselbe `ocr_engine`‑Instanz wieder. Sie cached die Sprachmodelle, was nachfolgende Erkennungen beschleunigt.

## Schritt 3: Sprache auf Arabisch setzen

Arabisch ist nicht Latein; es hat ein eigenes Zeichenset, eine rechts‑nach‑links‑Richtung und kontextabhängige Formen. Deshalb müssen wir der Engine explizit mitteilen, welches Sprachmodell geladen werden soll.

```python
# Step 3: Set the language to Arabic (language code "ar")
ocr_engine.set_language("ar")
```

Vergessen Sie diese Zeile, verwendet die Engine standardmäßig Englisch und liefert verstümmelte Ausgabe – etwas, das ich viel zu oft gesehen habe.

## Schritt 4: Ihr PNG‑Bild laden

Hier beginnt der eigentliche **Bild‑zu‑Text**‑Teil. Wir laden die PNG‑Datei, die den arabischen Text enthält.

```python
# Step 4: Load the image that contains the Arabic text
image_path = "YOUR_DIRECTORY/arabic_doc.png"   # replace with your actual path
ocr_engine.set_image(Imaging.Image.load(image_path))
```

### Häufige Randfälle

| Problem | Symptom | Lösung |
|---------|---------|--------|
| Bild ist zu dunkel | Ausgabe enthält viele Lücken | Vorverarbeiten mit Pillow (`ImageEnhance.Brightness`) |
| PNG hat einen Alpha‑Kanal | Manche OCR‑Engines lesen transparente Pixel falsch | Vor dem Laden in RGB konvertieren (`image.convert("RGB")`) |
| Text ist gedreht | Erkanntes Ergebnis ist verkehrt herum | Bild rotieren (`image.rotate(90, expand=True)`) bevor es an die Engine übergeben wird |

## Schritt 5: Erkennungsprozess starten

Jetzt, wo alles bereit ist, lassen wir die Engine ihre Arbeit tun.

```python
# Step 5: Run the recognition process
ocr_result = ocr_engine.recognize()
```

Die Methode `recognize` liefert ein Objekt, das den rohen Unicode‑String, Vertrauenswerte und Begrenzungsrahmen enthält. Für die meisten Entwickler reicht der reine Text aus.

## Schritt 6: Erkannten arabischen Text ausgeben

Jetzt drucken wir das Ergebnis. In einer echten Anwendung würden Sie es vielleicht in eine Datei, eine Datenbank oder an eine Übersetzungs‑API weitergeben.

```python
# Step 6: Output the recognized text
print(ocr_result.get_text())
```

Wenn Sie das Skript ausführen, sollten die arabischen Zeichen in Ihrer Konsole erscheinen (stellen Sie sicher, dass Ihr Terminal Unicode unterstützt). Wenn Sie Fragezeichen oder leere Zeichenketten sehen, prüfen Sie die Spracheinstellung und die Bildqualität erneut.

### Erwartete Ausgabe

```
هذا نص عربي من صورة PNG تم استخراجها باستخدام OCR.
```

Sieht die Ausgabe ähnlich aus wie oben, herzlichen Glückwunsch – Sie haben erfolgreich **arabischen Text aus einem PNG extrahiert**!

## Vollständiges funktionierendes Beispiel

Unten finden Sie das gesamte Skript, bereit zum Kopieren und Einfügen. Ersetzen Sie `YOUR_DIRECTORY/arabic_doc.png` durch den Pfad zu Ihrer eigenen Datei.

```python
import ocr
from ocr import Imaging

def main():
    # Create OCR engine
    ocr_engine = ocr.OcrEngine()
    
    # Set Arabic language
    ocr_engine.set_language("ar")
    
    # Load the PNG image
    image_path = "YOUR_DIRECTORY/arabic_doc.png"
    ocr_engine.set_image(Imaging.Image.load(image_path))
    
    # Recognize text
    ocr_result = ocr_engine.recognize()
    
    # Print the extracted Arabic text
    print(ocr_result.get_text())

if __name__ == "__main__":
    main()
```

Führen Sie es mit `python run_ocr.py` (oder wie auch immer Sie die Datei genannt haben) aus. Wenn alles korrekt installiert ist, wird der arabische Satz in der Konsole angezeigt.

## OCR auf verschiedenen Bildformaten ausführen

Der gleiche Code funktioniert für JPEG, TIFF oder BMP – einfach die Dateierweiterung ändern. Die Methode `Image.load` erkennt das Format automatisch, sodass Sie **Bild zu Text** ohne zusätzlichen Code umwandeln können.

```python
# Example for a JPEG file
ocr_engine.set_image(Imaging.Image.load("sample.jpg"))
```

Denken Sie daran, dass die Qualität des Quellbildes die Genauigkeit des **arabischen Text erkennen**‑Schritts stark beeinflusst. Hochauflösende, wenig komprimierte Bilder liefern die besten Ergebnisse.

## Text aus PNG extrahieren: Tipps für höhere Genauigkeit

1. **DPI ist wichtig** – Zielwert mindestens 300 dpi. Niedrigere DPI führen häufig zu fehlenden Zeichen.  
2. **Kontrast ist König** – Nutzen Sie Bildverarbeitungs‑Tools (z. B. OpenCV), um den Kontrast vor dem OCR zu erhöhen.  
3. **Rauschunterdrückung** – Kleine Punkte können das Modell verwirren; Median‑Filterung hilft.  

Hier ein kurzer Snippet mit Pillow, um ein PNG vor dem OCR zu verbessern:

```python
from PIL import Image, ImageEnhance, ImageFilter

def preprocess_png(path):
    img = Image.open(path).convert("L")          # grayscale
    img = ImageEnhance.Contrast(img).enhance(2)  # boost contrast
    img = img.filter(ImageFilter.MedianFilter()) # denoise
    return img

# Use the preprocessed image
prepped = preprocess_png("arabic_doc.png")
ocr_engine.set_image(Imaging.Image.from_pil(prepped))
```

## Häufig gestellte Fragen

**F: Funktioniert das auch mit anderen rechts‑nach‑links‑Sprachen außer Arabisch?**  
A: Absolut. Ändern Sie einfach den Sprachcode (`"ar"` → `"he"` für Hebräisch, `"fa"` für Persisch) und die Engine lädt das passende Modell.

**F: Was, wenn ich Text aus mehreren PNGs in einem Ordner extrahieren muss?**  
A: Durchlaufen Sie die Dateien, verwenden Sie dieselbe `ocr_engine`‑Instanz und sammeln Sie die Ergebnisse in einer Liste oder schreiben Sie jede in eine separate `.txt`‑Datei.

**F: Kann ich Vertrauenswerte für jedes Wort erhalten?**  
A: Ja. `ocr_result` stellt häufig eine Methode `get_confidences()` bereit. Kombinieren Sie jeden Vertrauenswert mit dem zugehörigen Wort für Qualitätskontrolle.

## Nächste Schritte

Jetzt, wo Sie **wissen, wie man OCR** auf arabischen PNGs ausführt, können Sie folgende Ideen umsetzen:

- **Batch‑Verarbeitung:** Kombinieren Sie das Skript mit `os.listdir`, um **arabischen Text** aus einem gesamten Verzeichnis zu **extrahieren**.  
- **Nachbearbeitung:** Nutzen Sie die Bibliotheken `arabic_reshaper` und `python-bidi`, um rechts‑nach‑links‑Ausgaben korrekt in PDFs darzustellen.  
- **Integration:** Füttern Sie den extrahierten Text in einen Such‑Index (z. B. Elasticsearch), um gescannte Dokumente durchsuchbar zu machen.  

All diese Themen bauen auf den hier behandelten Grundlagen auf und helfen Ihnen, ein einfaches **Bild‑zu‑Text**‑Skript in eine produktionsreife Pipeline zu verwandeln.

---

![wie man OCR auf arabischem PNG ausführt]()

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}