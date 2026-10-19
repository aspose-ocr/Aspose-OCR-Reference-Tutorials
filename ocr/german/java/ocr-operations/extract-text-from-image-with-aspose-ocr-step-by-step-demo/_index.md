---
category: general
date: 2026-02-14
description: Extrahieren Sie Text aus einem Bild mit Aspose OCR. Erfahren Sie, wie
  Sie ein Bild für OCR laden, Text aus einem Rechteck auslesen und diesem Aspose OCR‑Tutorial
  in wenigen Minuten folgen.
draft: false
keywords:
- extract text from image
- load image for ocr
- read text from rectangle
- aspose ocr tutorial
language: de
og_description: Extrahiere Text aus einem Bild sofort. Dieser Leitfaden zeigt, wie
  man ein Bild für OCR lädt, Text aus einem Rechteck liest und ein Aspose‑OCR‑Tutorial
  abschließt.
og_title: Text aus Bild mit Aspose OCR extrahieren – Schnellleitfaden
tags:
- Aspose
- OCR
- Java
title: Text aus Bild mit Aspose OCR extrahieren – Schritt‑für‑Schritt‑Demo
url: /de/java/ocr-operations/extract-text-from-image-with-aspose-ocr-step-by-step-demo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bild mit Aspose OCR extrahieren – Schritt‑für‑Schritt Demo

Haben Sie schon einmal **Text aus einem Bild extrahieren** müssen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein – viele Entwickler stoßen an diese Hürde, wenn sie zum ersten Mal Quittungs‑Scanning oder ID‑Verifizierung angehen. Die gute Nachricht? Mit Aspose OCR können Sie ein Bild laden, den genauen Bereich definieren, in dem sich der Text befindet, und die Zeichen in wenigen Zeilen herausziehen.

In diesem **aspose ocr tutorial** gehen wir alles durch, was Sie benötigen: das Laden des Bildes für OCR, das Setzen eines Rechtecks, das der Engine sagt, wo sie suchen soll, und schließlich das Lesen des extrahierten Textes. Am Ende haben Sie ein lauffähiges Java‑Programm, das den ROI‑Text in die Konsole ausgibt – keine Geheimnisse, nur eine klare, funktionierende Lösung.

## Was Sie benötigen

Bevor wir starten, stellen Sie sicher, dass Sie die Grundlagen abgedeckt haben:

| Voraussetzung | Warum es wichtig ist |
|--------------|----------------------|
| **Java JDK 8+** | Aspose OCR wird als Java‑Bibliothek bereitgestellt; jedes moderne JDK ist geeignet. |
| **Aspose.OCR for Java** (Download von der Aspose‑Website oder per Maven hinzufügen) | Stellt die Klassen `OcrEngine`, `ImageStream` und weitere bereit. |
| **Eine Bilddatei** (z. B. `receipt.jpg`), die druckbaren Text enthält | Wir zeigen der Engine ein Rechteck innerhalb dieser Datei. |
| **IDE oder Editor** (IntelliJ, Eclipse, VS Code…) | Hilft Ihnen, das Beispiel schnell zu kompilieren und auszuführen. |

Wenn Sie Maven verwenden, fügen Sie diese Abhängigkeit zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check Aspose for the latest version -->
</dependency>
```

> **Profi‑Tipp:** Die Versionsnummer oben ist Stand Februar 2026. Ein Update auf die neueste Version sorgt für Bug‑Fixes und Leistungsverbesserungen.

## Schritt 1 – OCR‑Engine initialisieren

Zuerst benötigen Sie eine Instanz von `OcrEngine`. Denken Sie daran wie an das Gehirn, das die Pixel analysiert.

```java
// Step 1: Create the OCR engine object
OcrEngine ocrEngine = new OcrEngine();
```

Warum auf diese Weise erstellen? Aspose trennt die Engine (die die Konfiguration hält) von den Bilddaten, sodass Sie dieselbe Engine bei Bedarf für mehrere Bilder wiederverwenden können.

## Schritt 2 – Bild für OCR laden

Jetzt **laden wir das Bild für OCR**. Der Helfer `ImageStream.fromFile` liest die Datei in einen Stream, den Aspose versteht.

```java
// Step 2: Load the target image (replace with your own path)
String imagePath = "YOUR_DIRECTORY/receipt.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

Kann die Datei nicht gefunden werden, wirft die Engine eine Ausnahme; in Produktionscode sollten Sie das daher in einen try‑catch‑Block einbetten. Für dieses Demo lassen wir die Ausnahme weiterreichen – das hält das Beispiel übersichtlich.

## Schritt 3 – Rechteck definieren (Text aus Rechteck lesen)

Hier kommt der **read text from rectangle**‑Teil zum Tragen. Sie geben der Engine exakt an, wo sie suchen soll, was die Verarbeitung beschleunigt und Fehlalarme reduziert.

```java
// Step 3: Create a rectangle that covers the area with the receipt total
// Parameters: x, y, width, height (all in pixels)
Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);
```

> **Warum ein Rechteck?**  
> Die meisten Dokumente haben vorhersehbare Layouts – denken Sie an eine Quittung, bei der der Betrag immer am unteren Rand steht. Durch Fokussierung auf diesen Ausschnitt ignoriert die OCR‑Engine irrelevante Grafiken und erhöht die Genauigkeit.

**Randfall:** Überschreitet das Rechteck die Bildgrenzen, schneidet Aspose es stillschweigend ab, wobei Daten verloren gehen. Eine kurze Plausibilitätsprüfung kann das verhindern:

```java
if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
    regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
    throw new IllegalArgumentException("ROI exceeds image dimensions.");
}
```

## Schritt 4 – Bild verarbeiten

Nachdem alles eingestellt ist, lassen wir die Engine ihre Magie wirken.

```java
// Step 4: Run OCR on the defined ROI
OcrResult ocrResult = ocrEngine.process();
```

Der Aufruf `process()` liefert ein `OcrResult`‑Objekt, das den extrahierten Text, Vertrauenswerte und sogar die Begrenzungsrahmen für jedes Wort enthält, falls Sie diese später benötigen.

## Schritt 5 – Extrahierten Text ausgeben

Zum Schluss geben wir das Ergebnis aus. In einer echten Anwendung würden Sie es vielleicht in einer Datenbank speichern oder an einen anderen Service weiterleiten, aber für dieses Tutorial reicht die Konsolenausgabe aus.

```java
// Step 5: Display the recognized text
System.out.println("ROI text:");
System.out.println(ocrResult.getText());
```

**Erwartete Ausgabe** (angenommen, das Rechteck hat den Gesamtbetrag auf einer Quittung erfasst):

```
ROI text:
$12.34
```

Ist das ROI leer oder das Bild unscharf, erhalten Sie einen leeren String oder wirre Zeichen. Passen Sie das Rechteck an, verbessern Sie die Bildqualität oder aktivieren Sie Asposes Vorverarbeitungsoptionen (z. B. `setAutoSkewCorrection(true)`).

## Vollständiges funktionierendes Beispiel

Unten finden Sie das komplette, sofort ausführbare Programm. Kopieren Sie es in eine Datei namens `RoiDemo.java`, passen Sie den Bildpfad an und führen Sie `javac RoiDemo.java && java RoiDemo` aus.

```java
import com.aspose.ocr.*;
import java.awt.Rectangle;

/**
 * Demo: Extract text from a specific rectangle (ROI) in an image using Aspose OCR.
 * Adjust the rectangle coordinates to match the area you want to read.
 */
public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        // Replace YOUR_DIRECTORY with the actual folder containing receipt.jpg
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.jpg"));

        // Step 3: Define the region of interest where text is expected
        // (x, y, width, height) in pixels
        Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
        ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);

        // Optional sanity check – ensures ROI fits inside the image
        if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
            regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
            throw new IllegalArgumentException("ROI exceeds image dimensions.");
        }

        // Step 4: Perform OCR on the defined ROI
        OcrResult ocrResult = ocrEngine.process();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(ocrResult.getText());
    }
}
```

> **Ergebnisüberprüfung:** Nach dem Ausführen vergleichen Sie die Konsolenausgabe mit dem tatsächlichen Text im Rechteck. Stimmen sie überein, haben Sie erfolgreich **extract text from image** mit Aspose OCR umgesetzt.

## Häufige Fragen & Tipps

### Was, wenn ich mehrere ROIs im selben Bild verarbeiten muss?
Erstellen Sie für jeden Bereich ein neues `Rectangle`, rufen Sie `setRegionOfInterest` erneut auf und führen Sie `process()` erneut aus. Die Engine nutzt dieselben Bilddaten, sodass die Performance erhalten bleibt.

### Wie geht Aspose mit verschiedenen Sprachen oder Schriftarten um?
Sie können das Sprachmodell über `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.English)` wechseln. Für nicht‑lateinische Schriften laden Sie das passende Sprachpaket (auf der Aspose‑Download‑Seite verfügbar).

### Unterstützt die Bibliothek PDF‑Eingaben?
Ja – Aspose OCR kann PDF‑Streams direkt verarbeiten. Ersetzen Sie einfach `ImageStream.fromFile` durch `ImageStream.fromPdfFile("doc.pdf")` und geben Sie optional die Seitenzahl an.

### Kann ich die Genauigkeit bei minderwertigen Scans verbessern?
Aktivieren Sie die Vorverarbeitung:

```java
ocrEngine.getEngineOptions().setAutoSkewCorrection(true);
ocrEngine.getEngineOptions().setBinarizationMethod(BinarizationMethod.Otsu);
```

Diese Optionen entfernen Rauschen und richten den Text aus, bevor die Erkennung erfolgt.

## Fazit

Wir haben gerade ein komplettes **aspose ocr tutorial** durchlaufen, das zeigt, wie man **extract text from image**, **load image for OCR** und **read text from rectangle** mit Java verwendet. Die wichtigsten Schritte sind: Engine initialisieren, Bild übergeben, Region of Interest festlegen, verarbeiten und schließlich das Ergebnis ausgeben.

Von hier aus können Sie:

* **Batch‑Verarbeitung** – über einen Ordner mit Quittungen iterieren und jeden Betrag in einer Datenbank speichern.  
* **Dynamische ROI‑Erkennung** – Bildverarbeitungs‑Bibliotheken (OpenCV) nutzen, um Textblöcke automatisch zu lokalisieren.  
* **Nachbearbeitung** – Regex oder Fuzzy‑Matching anwenden, um OCR‑Eigenheiten zu bereinigen.

Probieren Sie diese Ideen aus, passen Sie das Rechteck an Ihre eigenen Dokumente an, und Sie haben in kürzester Zeit eine robuste Text‑Extraktions‑Pipeline. Viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}