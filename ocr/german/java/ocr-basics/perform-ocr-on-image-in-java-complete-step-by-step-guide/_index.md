---
category: general
date: 2026-06-16
description: Lernen Sie, wie Sie OCR auf Bilddateien in Java durchführen. Dieses Tutorial
  behandelt das Erkennen von Text aus PNG, das Extrahieren von Text aus Bildern, das
  Konvertieren von Bildern zu Text und das Laden von Bildern für OCR.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: de
og_description: Führen Sie OCR auf Bildern mit Java durch. Dieser Leitfaden zeigt,
  wie man Text aus PNG erkennt, Text aus einem Bild extrahiert und ein Bild in Text
  umwandelt, mit einem sofort einsatzbereiten Beispiel.
og_title: OCR auf Bild in Java ausführen – Vollständiges Programmier‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  headline: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  name: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'If `hello.png` contains the phrase “Hello, OCR world!”, the console will
      display something like:'
  - name: 5.1 Dealing with Low‑Resolution Images
    text: 'If the source PNG is blurry, OCR accuracy drops. A quick fix is to upscale
      the image before feeding it to the engine:'
  - name: 5.2 Multi‑Language Documents
    text: 'If you anticipate French or German text, simply add the language codes
      to `setLanguage`:'
  - name: 5.3 Skipping Empty Pages
    text: 'Sometimes a scanned PDF page renders as a blank PNG. Detecting an empty
      image saves processing time:'
  type: HowTo
tags:
- Java
- OCR
- Image Processing
title: OCR auf Bild in Java durchführen – Vollständige Schritt‑für‑Schritt‑Anleitung
url: /de/java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Durchführen von OCR auf Bild in Java – Vollständige Schritt‑für‑Schritt‑Anleitung

Haben Sie jemals **perform OCR on image** Dateien durchführen müssen, waren sich aber nicht sicher, welche Java‑Bibliothek Sie wählen sollten? Sie sind nicht allein. Egal, ob Sie einen Belegscanner, ein Dokumentenarchiv erstellen oder einfach nur neugierig darauf sind, Bilder in durchsuchbaren Text zu verwandeln – das Erlernen, wie man **perform OCR on image** mit Java durchführt, ist eine nützliche Fähigkeit.

In diesem Tutorial gehen wir alles durch, was Sie benötigen, um **perform OCR on image** Dateien zu bearbeiten: das Laden des Bildes, das Konfigurieren der Engine, das Erkennen des Textes und schließlich das Ausgeben des Ergebnisses. Am Ende können Sie **recognize text from PNG** Dateien, **extract text from image** Quellen und **convert image to text** mit nur wenigen Code‑Zeilen.

## Voraussetzungen

- Java 17 oder neuer (der Code kompiliert mit jedem aktuellen JDK)
- Maven installiert (oder Ihr bevorzugtes Build‑Tool)
- Grundlegende Vertrautheit mit der Java‑Syntax
- Eine PNG‑Datei, die Sie testen möchten (wir nennen sie `hello.png`)

> **Pro‑Tipp:** Wenn Sie keine PNG‑Datei zur Hand haben, erstellen Sie eine, indem Sie einen Screenshot von beliebigem Text machen und ihn als `hello.png` in einem Ordner namens `resources` speichern.

## Was wir bauen werden

Eine kleine Konsolenanwendung namens `OcrDemo`, die:

1. **Loads image for OCR** – liest ein PNG von der Festplatte.
2. **Performs OCR on image** – verwendet die Tesseract‑Engine über Tess4J.
3. **Extracts text from image** – gibt einen `String` mit dem erkannten Inhalt zurück.
4. Gibt das Ergebnis in der Konsole aus.

Lassen Sie uns eintauchen.

## Schritt 1: Projekt einrichten und Tess4J hinzufügen

Zuerst ein neues Maven‑Projekt erstellen (oder Gradle, wenn Sie das bevorzugen). Die Tess4J‑Abhängigkeit hinzufügen, die die beliebte Tesseract‑OCR‑Engine einbindet.

```xml
<!-- pom.xml -->
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>ocr-demo</artifactId>
  <version>1.0.0</version>
  <properties>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
  </properties>

  <dependencies>
    <!-- Tess4J – Java wrapper for Tesseract OCR -->
    <dependency>
      <groupId>net.sourceforge.tess4j</groupId>
      <artifactId>tess4j</artifactId>
      <version>5.5.1</version>
    </dependency>
  </dependencies>
</project>
```

> **Warum Tess4J?** Es wird aktiv gepflegt, funktioniert plattformübergreifend und bietet Ihnen eine saubere Java‑API für **perform OCR on image** Aufgaben.

## Schritt 2: Bild‑Lade‑Logik vorbereiten

Jetzt schreiben wir eine Hilfsmethode, die **load image for OCR**. Die Methode nutzt Java’s `ImageIO`, um ein PNG in ein `BufferedImage` zu lesen.

```java
package com.example.ocr;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Utility class responsible for loading images from the file system.
 */
public final class ImageLoader {

    private ImageLoader() { /* utility class */ }

    /**
     * Loads a PNG (or any supported format) from the given path.
     *
     * @param path absolute or relative path to the image file
     * @return BufferedImage instance ready for OCR processing
     * @throws IOException if the file cannot be read
     */
    public static BufferedImage load(String path) throws IOException {
        File imgFile = new File(path);
        if (!imgFile.exists()) {
            throw new IOException("Image file not found: " + path);
        }
        return ImageIO.read(imgFile);
    }
}
```

Beachten Sie, dass der Methodenname eindeutig die Absicht **load image for OCR** widerspiegelt, wodurch der Code selbstdokumentierend ist.

## Schritt 3: OCR‑Engine konfigurieren für **Perform OCR on Image**

Mit dem Bild in der Hand erstellen wir eine `Tesseract`‑Instanz, aktivieren die automatische Spracherkennung und rufen `doOCR` auf. Das ist der Kern, wie wir **perform OCR on image** Daten verarbeiten.

```java
package com.example.ocr;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

/**
 * Wrapper around Tess4J that abstracts the OCR workflow.
 */
public final class OcrEngine {

    private final ITesseract tesseract;

    public OcrEngine() {
        tesseract = new Tesseract();

        // Use the bundled tessdata folder (you can also point to a custom one)
        tesseract.setDatapath("tessdata");

        // Enable automatic language detection – improves accuracy across multilingual images
        tesseract.setLanguage("eng"); // fallback language
        tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
        tesseract.setPageSegMode(ITesseract.PSM_AUTO);
    }

    /**
     * Performs OCR on the supplied BufferedImage and returns the recognized text.
     *
     * @param image image to be processed
     * @return the text extracted from the image
     * @throws TesseractException if OCR fails
     */
    public String recognize(BufferedImage image) throws TesseractException {
        return tesseract.doOCR(image);
    }
}
```

> **Warum Auto‑Detect aktivieren?** Es lässt die Engine das beste Sprachmodell für das Bild auswählen, was besonders nützlich ist, wenn Sie **convert image to text** aus Quellen durchführen, die Englisch und andere Schriften mischen.

## Schritt 4: Alles zusammenführen – Die Hauptanwendung

Hier ist der Einstiegspunkt, der **recognize text from PNG**, **extract text from image** ausführt und schließlich das Ergebnis ausgibt. Dies ist das vollständige, ausführbare Beispiel.

```java
package com.example.ocr;

import net.sourceforge.tess4j.TesseractException;
import java.awt.image.BufferedImage;
import java.io.IOException;

/**
 * Demo application that shows how to perform OCR on image files.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Path to the PNG you want to process
        String imagePath = "resources/hello.png";

        try {
            // Step 1: Load image for OCR
            BufferedImage image = ImageLoader.load(imagePath);

            // Step 2: Create OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Step 3: Perform OCR on image and retrieve the text
            String recognizedText = engine.recognize(image);

            // Step 4: Output the recognized text to the console
            System.out.println("=== Recognized Text ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR processing error: " + e.getMessage());
        }
    }
}
```

### Erwartete Ausgabe

Wenn `hello.png` den Satz „Hello, OCR world!“ enthält, zeigt die Konsole etwa Folgendes:

```
=== Recognized Text ===
Hello, OCR world!
```

Die genaue Ausgabe kann je nach Bildqualität leicht variieren, aber Sie sollten den in das PNG eingefügten Text sehen.

## Schritt 5: Häufige Randfälle behandeln

### 5.1 Umgang mit niedrig aufgelösten Bildern

Wenn das Quell‑PNG unscharf ist, sinkt die OCR‑Genauigkeit. Eine schnelle Lösung ist, das Bild vor dem Übergeben an die Engine zu vergrößern:

```java
import java.awt.Graphics2D;
import java.awt.RenderingHints;

public static BufferedImage upscale(BufferedImage original, int factor) {
    int width = original.getWidth() * factor;
    int height = original.getHeight() * factor;
    BufferedImage scaled = new BufferedImage(width, height, original.getType());
    Graphics2D g = scaled.createGraphics();
    g.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                       RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g.drawImage(original, 0, 0, width, height, null);
    g.dispose();
    return scaled;
}
```

Rufen Sie `upscale(image, 2)` vor `engine.recognize(image)` auf, um die Ergebnisse zu verbessern.

### 5.2 Mehrsprachige Dokumente

Wenn Sie französischen oder deutschen Text erwarten, fügen Sie einfach die Sprachcodes zu `setLanguage` hinzu:

```java
tesseract.setLanguage("eng+fra+deu");
```

Die Engine wird dann versuchen, **extract text from image** mit den kombinierten Sprachmodellen zu verarbeiten.

### 5.3 Leere Seiten überspringen

Manchmal wird eine gescannte PDF‑Seite als leeres PNG gerendert. Das Erkennen eines leeren Bildes spart Verarbeitungszeit:

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## Schritt 6: Anwendung paketieren und ausführen

1. **Kompilieren:** `mvn clean compile`
2. **Ausführen:** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

Stellen Sie sicher, dass der Ordner `tessdata` (enthält Sprachdateien) neben dem kompilierten JAR liegt oder geben Sie seinen absoluten Pfad in `OcrEngine` an.

## Fazit

Sie haben nun ein solides, produktionsreifes Muster, um **perform OCR on image** Dateien mit Java zu bearbeiten. Von **loading image for OCR** bis **recognize text from PNG** haben wir gezeigt, wie man **extract text from image**, **convert image to text** durchführt und knifflige Szenarien wie niedrig aufgelöste Scans oder mehrsprachige Inhalte handhabt.

Als Nächstes könnten Sie erkunden:

- **Batch processing** – über ein Verzeichnis von PNGs iterieren und jedes Ergebnis in einer `.txt`‑Datei speichern.
- **PDF generation** – den extrahierten Text wieder in durchsuchbare PDFs einbetten.
- **Cloud OCR services** – die lokale Tesseract‑Leistung mit APIs wie Google Vision oder Azure Cognitive Services vergleichen.

Fühlen Sie sich frei zu experimentieren, die Parameter anzupassen und Ihre Ergebnisse zu teilen. Viel Spaß beim Coden, und mögen Ihre Bilder stets in sauberen, durchsuchbaren Text verwandelt werden! 

![Diagram showing the OCR workflow to perform OCR on image](https://example.com/ocr-workflow.png "perform OCR on image example")


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Text aus Bild mit Aspose OCR erkennen – Vollständiges Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Bild in Text konvertieren in Java mit Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Text aus Bild in Java extrahieren mit Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}