---
category: general
date: 2026-03-26
description: Erfahren Sie, wie Sie OCR in Python durchführen und Text aus Bilddateien
  erkennen. Dieser Leitfaden zeigt, wie Sie Text aus PNG extrahieren und Bilder schnell
  in Text umwandeln.
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: de
og_description: Wie führt man OCR in Python durch? Folgen Sie dieser Anleitung, um
  Text aus Bildern zu erkennen, Text aus PNG-Dateien zu extrahieren und Bilder mit
  einer Testlizenz in Text zu konvertieren.
og_title: Wie man OCR in Python durchführt – Komplettes Tutorial
tags:
- OCR
- Python
- Image Processing
title: Wie man OCR in Python durchführt – Vollständiges Schritt‑für‑Schritt‑Tutorial
url: /de/python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR in Python durchführt – Vollständiges Schritt‑für‑Schritt‑Tutorial  

Haben Sie sich jemals gefragt, **wie man OCR** auf einem Bild, das Sie gerade mit Ihrem Handy aufgenommen haben, durchführt? Sie sind nicht allein – Entwickler überall benötigen eine zuverlässige Methode, um Text aus Bilddateien zu erkennen, ohne sich mit komplexen nativen Bibliotheken herumschlagen zu müssen.  

In diesem Tutorial führen wir ein praktisches Beispiel durch, das **wie man OCR durchführt**, **Text aus Bild erkennt** und **Text aus PNG extrahiert** mithilfe eines leichten Python‑Wrappers zeigt. Am Ende können Sie **Bild zu Text konvertieren** mit nur wenigen Codezeilen, und Sie müssen sich keine Sorgen um Lizenzprobleme machen, da wir den integrierten Testmodus verwenden.  

## Was Sie lernen werden  

* Wie man eine Testlizenz für die OCR‑Engine einrichtet (kein Dateipfad erforderlich).  
* Die genaue Reihenfolge der Aufrufe zu **recognize text from image**‑Objekten.  
* Methoden, **extract text from PNG**‑Dateien zu extrahieren und gängige Stolperfallen wie fehlende Schriftarten zu behandeln.  
* Tipps zum Skalieren der Lösung, wenn Sie von einer Test- zu einer Produktionslizenz wechseln.  

**Voraussetzungen** – Sie benötigen Python 3.8+ und das `ocr`‑Paket (installierbar via `pip install ocr`). Keine weiteren externen Werkzeuge sind erforderlich.

---  

![Beispiel für OCR durchführen](https://example.com/ocr-demo.png "wie man OCR in Python durchführt – erkannter Text angezeigt")  

*Bild‑Alt‑Text: wie man OCR in Python durchführt – Beispielausgabe*  

## Schritt 1 – Testlizenz aktivieren (kein Dateipfad erforderlich)  

Bevor die Engine etwas lesen kann, benötigt sie eine gültige Lizenz. Der Testmodus ist perfekt für Experimente und kleine Projekte.

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*Warum das wichtig ist:* Das Lizenzobjekt teilt der OCR‑Bibliothek mit, dass Sie in einer Sandbox arbeiten. Wenn Sie diesen Schritt überspringen, wirft die Engine sofort einen `LicenseError`, sobald Sie `recognize()` aufrufen.  

**Pro‑Tipp:** Wenn Sie zu einer kostenpflichtigen Lizenz wechseln, ersetzen Sie die beiden Zeilen oben durch `ocr.License("path/to/your/license.key").apply()`.

## Schritt 2 – OCR‑Engine‑Instanz erstellen  

Jetzt, da der Test aktiv ist, instanziieren wir die Haupt‑Engine. Denken Sie daran als das „Gehirn“, das das Bild betrachtet und entscheidet, welche Zeichen wo sind.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*Warum das wichtig ist:* Der `OcrEngine` enthält Konfigurationen wie Sprachpakete und DPI‑Einstellungen. Sie können diese später anpassen, aber die Vorgabe funktioniert für die meisten rein englischen PNGs.

## Schritt 3 – Laden Sie das PNG, das Sie verarbeiten möchten  

Hier führen wir **recognize text from image** aus. Die Methode `ocr.Imaging.Image.load()` unterstützt PNG, JPEG, BMP und einige weitere Formate.

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*Randfall:* Wenn Ihr PNG eine indizierte Palette verwendet (häufig bei Screenshots), konvertiert der Loader es automatisch in einen 24‑Bit‑RGB‑Puffer. Diese Konvertierung kann einen kleinen Leistungseinbruch bedeuten, garantiert aber genaue OCR‑Ergebnisse.

## Schritt 4 – OCR ausführen und Text holen  

Schließlich lassen wir die Engine ihre Arbeit tun und holen dann das Klartext‑Ergebnis.

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**Erwartete Ausgabe** (Beispiel für ein einfaches Bild mit dem Text „Hello World“):

```
Hello World
```

Wenn das Bild mehrere Zeilen enthält, bewahrt die Ausgabe Zeilenumbrüche, was das Weiterleiten an nachgelagerte Prozesse wie CSV‑Parser oder NLP‑Pipelines erleichtert.

## Optional: Feinabstimmung für bessere Genauigkeit  

* **Sprachpakete:** `ocr_engine.set_language("eng")` (Standard) oder `"fra"` für Französisch.  
* **DPI‑Skalierung:** `ocr_engine.set_dpi(300)` kann Ergebnisse bei niedrigauflösenden Scans verbessern.  
* **Vorverarbeitung:** Das Anwenden eines binären Schwellenwerts (`ocr.Imaging.Image.threshold()`) vor `set_image` liefert häufig saubereren Text bei verrauschten Hintergründen.  

Diese Anpassungen sind nützlich, wenn Sie von einer schnellen Demo zu einer produktionsreifen **ocr tutorial python** wechseln, die täglich Hunderte von Dateien verarbeitet.

## Vollständiges Skript – Bereit zum Kopieren & Einfügen  

Unten finden Sie das komplette, ausführbare Skript, das alle oben genannten Schritte kombiniert. Speichern Sie es als `run_ocr.py` und ersetzen Sie `YOUR_DIRECTORY/sample1.png` durch den Pfad zu Ihrem eigenen PNG.

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

Führen Sie es über die Befehlszeile aus:

```bash
python run_ocr.py
```

Sie sollten den extrahierten Text in der Konsole ausgegeben sehen. Wenn Sie eine leere Zeichenkette erhalten, überprüfen Sie, ob das Bild tatsächlich klaren, hochkontrastierten Text enthält und ob die Testlizenz ohne Fehler angewendet wurde.

## Häufige Fragen & Stolperfallen  

* **„Funktioniert das mit JPEG?“** – Absolut. Die Methode `load()` erkennt das Format automatisch, sodass Sie PNG durch JPEG ersetzen können, ohne den Code zu ändern.  
* **„Was ist, wenn das Bild gedreht ist?“** – Die Engine kann die Orientierung automatisch erkennen, aber für beste Ergebnisse können Sie das Bild vor `set_image` mit `input_image.rotate(90)` vorab drehen.  
* **„Kann ich mehrere Bilder in einer Schleife verarbeiten?“** – Ja. Verschieben Sie einfach das Laden und die Aufrufe von `recognize()` in eine `for`‑Schleife; dieselbe `ocr_engine`‑Instanz kann wiederverwendet werden, was einen kleinen Overhead spart.  

## Nächste Schritte – Von der Demo zur Produktion  

Jetzt, da Sie **wie man OCR durchführt** kennen, denken Sie über diese weiterführenden Themen nach:

* **Batch‑Verarbeitung** – Kombinieren Sie dieses Skript mit `os.listdir()`, um **extract text from PNG**‑Dateien stapelweise zu verarbeiten.  
* **Integration mit PDF** – Verwenden Sie `pdf2image`, um PDF‑Seiten in PNG zu konvertieren und dann in dieselbe Pipeline einzuspeisen.  
* **Nachbearbeitung** – Wenden Sie Regex oder Fuzzy‑Matching an, um häufige OCR‑Fehler zu bereinigen (z. B. „0“ vs „O“).  

Jeder dieser Punkte baut auf der Kernidee **convert image to text** auf und erweitert die Nützlichkeit Ihres OCR‑Workflows.

---  

### TL;DR  

Wir haben alles behandelt, was Sie wissen müssen, um **wie man OCR** in Python durchzuführen: Testlizenz aktivieren, Engine erstellen, PNG laden, Erkennung ausführen und das Ergebnis ausgeben. Mit nur wenigen Zeilen können Sie **recognize text from image**, **extract text from PNG** und **convert image to text** für jede nachgelagerte Anwendung.  

Probieren Sie es aus, passen Sie DPI‑ oder Spracheinstellungen an und lassen Sie die Engine die schwere Arbeit übernehmen. Viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}