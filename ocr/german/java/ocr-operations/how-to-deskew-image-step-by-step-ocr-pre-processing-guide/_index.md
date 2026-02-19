---
category: general
date: 2026-02-19
description: Erfahren Sie, wie Sie ein Bild entzerren und Rauschen für OCR entfernen.
  Dieses Tutorial zeigt, wie man Textbilder erkennt, die Bildrotation korrigiert und
  die Bildvorverarbeitung für OCR mit Aspose OCR durchführt.
draft: false
keywords:
- how to deskew image
- recognize text image
- how to remove noise
- correct image rotation
- preprocess image ocr
language: de
og_description: Wie man ein Bild entzerrt und Rauschen entfernt, damit Sie Textbilder
  schnell erkennen können. Folgen Sie dieser Anleitung, um die Bildrotation zu korrigieren
  und die Bild‑OCR mit Aspose vorzubereiten.
og_title: Wie man ein Bild entzerrt – Vollständiges OCR-Vorverarbeitungs‑Tutorial
tags:
- OCR
- Java
- Image Processing
title: Wie man ein Bild entzerrt — Schritt‑für‑Schritt OCR‑Vorverarbeitungs‑Leitfaden
url: /de/java/ocr-operations/how-to-deskew-image-step-by-step-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein Bild deskew — Komplettes OCR‑Vorverarbeitungs‑Tutorial

Haben Sie sich schon einmal gefragt, **wie man Bilddateien deskew** kann, bevor man sie an eine OCR‑Engine übergibt? Vielleicht haben Sie einen Stapel Belege gescannt und die Seiten sehen ein wenig schief aus, oder der Scan ist mit zufälligen Punkten übersät. Das ist ein häufiges Problem – schiefe, verrauschte Bilder lassen die Texterkennung stolpern.  

Die gute Nachricht? Sie können das Bild (Bildrotation korrigieren) und das Rauschen (wie man Rauschen entfernt) mit nur wenigen Zeilen Java mithilfe von Aspose.OCR begradigen und entrauschen. In diesem Leitfaden gehen wir den gesamten Ablauf durch: vom Laden eines verrauschten‑rotierten PNGs, über das Anwenden von Deskew + Median‑Denoise, bis hin zum **recognize text image** und dem Ausgeben des Ergebnisses. Am Ende haben Sie ein wiederverwendbares Snippet, das Sie in jedes Java‑Projekt einbinden können.

## Was Sie benötigen

- **Java 17** oder neuer (der Code kompiliert auch mit älteren Versionen, aber 17 ist der optimale Punkt).  
- **Aspose.OCR für Java** – Sie können das neueste JAR von Maven Central holen (`com.aspose:aspose-ocr`).  
- Eine Bilddatei, die sowohl rotiert als auch verrauscht ist (z. B. `noisy-rotated.png`).  
- Eine einfache IDE (IntelliJ, Eclipse oder sogar VS Code).  

Keine ausgefallenen Build‑Tools nötig; ein einfacher `javac` + `java`‑Durchlauf reicht aus.

---

## Schritt 1 – Instanz des OCR‑Engines erstellen  

Das Erste, was Sie tun, ist ein `OcrEngine` zu erzeugen. Denken Sie daran als das Gehirn, das später die Zeichen für Sie liest.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Pro‑Tipp:** Halten Sie die Engine als Singleton, wenn Sie viele Bilder verarbeiten; sie nutzt interne Puffer wieder und beschleunigt den Vorgang.

## Schritt 2 – Deskew und Median‑Denoise aktivieren (Wie man Rauschen entfernt)

Jetzt sagen wir der Engine, **die Bildrotation zu korrigieren** und **wie man Rauschen entfernt**. Beide Filter sind optional, zusammen verbessern sie die Genauigkeit dramatisch.

```java
        // Turn on preprocessing filters
        ocrEngine.getPreprocessing().setDeskew(true);          // fixes rotation
        ocrEngine.getPreprocessing().setMedianDenoise(true);   // smooths out speckles
```

Warum Median‑Denoise? Es bewahrt Kanten (die Linien, die Zeichen definieren), während isolierte Pixel gelöscht werden – genau das, was Sie für saubere OCR benötigen.

## Schritt 3 – Das zu verarbeitende Bild laden  

Hier zeigen wir der Engine die Datei, die gereinigt werden muss. `ImageStream.fromFile` liest das PNG in den Speicher.

```java
        // Load the noisy‑rotated image
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/noisy-rotated.png"));
```

Falls Ihr Bild auf einem entfernten Server liegt, übergeben Sie einfach einen `InputStream` – Aspose verarbeitet das problemlos.

## Schritt 4 – OCR ausführen und den erkannten Text erfassen  

Mit aktivierter Vorverarbeitung liest die Engine nun das korrigierte Bild. Der Aufruf `recognize()` liefert ein `RecognitionResult`, das den extrahierten String enthält.

```java
        // Perform OCR – the engine automatically applies deskew & denoise first
        String recognizedText = ocrEngine.recognize().getText();

        // Show the output
        System.out.println("=== Recognized Text ===");
        System.out.println(recognizedText);
    }
}
```

Sie sollten sauberen, lesbaren Text in der Konsole sehen, selbst wenn das Originalbild schief und körnig war.

## Schritt 5 – Ergebnis überprüfen (Was zu erwarten ist)

Wenn alles funktioniert, gibt die Konsole etwa Folgendes aus:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑02‑15
Total: $1,234.56
```

Falls die Ausgabe noch verzerrte Zeichen enthält, prüfen Sie:

- Die Bildauflösung (≥ 300 dpi ist ideal).  
- Ob der Dateipfad korrekt ist.  
- Ob zusätzliche Filter (z. B. `setContrastStretch`) helfen könnten.

---

## Optional: Visuelle Bestätigung mit einem Beispielbild  

Unten sehen Sie eine kleine Vorschau eines rotierten, verrauschten Belegs. Beachten Sie die Neigung – unser Code wird sie für Sie begradigen.

![how to deskew image example](deskew-demo.png "how to deskew image")

*Alt‑Text: how to deskew image – Vorher und Nachher der Verarbeitung.*

---

## Häufig gestellte Fragen

### Funktioniert das mit PDFs oder nur mit PNG/JPEG?  
Aspose.OCR kann PDFs direkt lesen; ersetzen Sie einfach `ImageStream.fromFile` durch `ImageStream.fromPdf`. Die gleichen Vorverarbeitungs‑Flags gelten, sodass Sie weiterhin **how to deskew image** und **how to remove noise** erhalten.

### Was, wenn ich die ursprüngliche Orientierung für spätere Schritte behalten muss?  
Sie können das Bild vor der Vorverarbeitung klonen:

```java
Image original = ocrEngine.getImage().clone();
ocrEngine.getPreprocessing().apply(); // modifies the internal copy
// Use original later if needed
```

### Kann ich den Deskew‑Winkel manuell ändern?  
Ja – `setDeskewAngle(double degrees)` lässt Sie den Auto‑Detect‑Algorithmus überschreiben. Nützlich, wenn die automatische Erkennung bei extremen Rotationen versagt.

### Wie unterscheidet sich Median‑Denoise von Gaussian Blur?  
Median‑Filter ersetzen jedes Pixel durch den Median seiner Nachbarn, wodurch Kanten erhalten bleiben. Gaussian Blur glättet alles, was die Striche von Zeichen verwischen kann – daher ist Median die sicherere Wahl für OCR.

---

## Fazit  

In diesem Tutorial haben wir **how to deskew image** Dateien behandelt, **how to remove noise** demonstriert und gezeigt, wie man **recognize text image** mit den integrierten Vorverarbeitungsfunktionen von Aspose OCR verwendet. Durch das Aktivieren von `setDeskew(true)` und `setMedianDenoise(true)` korrigieren Sie automatisch **image rotation** und entfernen Sprenkel, wodurch ein unordentlicher Scan in einen sauberen Textstring verwandelt wird.  

Probieren Sie gern aus: verschiedene Denoise‑Strategien, PDFs einspeisen oder mehrere Bilder in einer Schleife verarbeiten. Das gleiche Muster – Engine → Vorverarbeitung → Erkennung – gilt für jedes Szenario und bildet eine solide Basis für jede OCR‑Pipeline.

**Nächste Schritte**, die Sie erkunden könnten:

- **Batch‑Verarbeitung** – über ein Verzeichnis von Bildern iterieren und jedes Ergebnis in eine `.txt`‑Datei schreiben.  
- **Sprachpakete** – ein spezifisches Sprachwörterbuch laden, um die Genauigkeit für nicht‑englischen Text zu steigern.  
- **Erweiterte Filter** – wie `setContrastStretch` oder `setBinarization` für Scans mit geringem Kontrast.  

Haben Sie weitere Fragen? Hinterlassen Sie einen Kommentar, und happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}