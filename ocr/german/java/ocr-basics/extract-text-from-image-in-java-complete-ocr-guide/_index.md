---
category: general
date: 2026-07-21
description: Extrahiere Text aus einem Bild mit Java‑OCR. Erfahre, wie du PNG in Text
  umwandelst, Text aus PNG liest, ein Bild für OCR lädst und OCR auf ein Bild in nur
  wenigen Schritten durchführst.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: de
lastmod: 2026-07-21
og_description: Extrahiere Text aus einem Bild mit Java. Dieser Leitfaden zeigt, wie
  man PNG in Text umwandelt, Text aus PNG liest, ein Bild für OCR lädt und OCR effizient
  auf ein Bild anwendet.
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: Text aus Bild in Java extrahieren – Schritt‑für‑Schritt OCR‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  headline: Extract Text from Image in Java – Complete OCR Guide
  type: TechArticle
- description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  name: Extract Text from Image in Java – Complete OCR Guide
  steps:
  - name: Low‑Quality Images
    text: 'If the PNG is blurry or has low contrast, OCR accuracy drops. A quick fix
      is to pre‑process the image:'
  - name: Multi‑Language Support
    text: Tess4J can handle many languages. Just download the appropriate `.traineddata`
      file and point `tesseract.setLanguage("spa")` for Spanish, for example.
  - name: Large PDFs or Multi‑Page Images
    text: If you need to **extract text from image** files inside a PDF, split each
      page into PNGs first (using PDFBox) and then feed each PNG to the same OCR routine.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Text aus Bild in Java extrahieren – Vollständiger OCR-Leitfaden
url: /de/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bild in Java extrahieren – Vollständiger OCR-Leitfaden

Haben Sie jemals **Text aus Bild extrahieren** müssen, waren sich aber nicht sicher, welche Java‑Bibliothek Sie wählen sollten? Sie sind nicht allein. Egal, ob Sie Belege digitalisieren, PDFs scannen oder ein durchsuchbares Archiv erstellen, das Herausziehen von Text aus einer PNG ist für viele Entwickler ein tägliches Problem.

In diesem Tutorial führen wir Sie durch eine praktische Lösung, die es Ihnen ermöglicht, **PNG in Text zu konvertieren**, **Text aus PNG zu lesen**, **Bild für OCR zu laden** und **OCR auf Bild auszuführen** – alles mit wenigen Zeilen sauberem Java‑Code. Am Ende haben Sie ein ausführbares Programm, das Sie in jedes Projekt einbinden können.

## Was Sie bauen werden

1. Lädt eine PNG‑Datei von der Festplatte.  
2. Sendet das Bild an eine OCR‑Engine (Tess4J, ein Java‑Wrapper für Tesseract).  
3. Gibt den erkannten Text in der Konsole aus.

Keine externen Dienste, kein Zauber – nur reines Java und eine Open‑Source‑OCR‑Engine.

## Voraussetzungen

- **Java 17** oder neuer (der Code kompiliert auch mit älteren Versionen, aber Java 17 bietet die neuesten Sprachfeatures).  
- **Maven** oder **Gradle** für das Abhängigkeitsmanagement.  
- Ein Beispiel‑PNG mit dem Namen `sample.png`, das in einem Ordner liegt, den Sie referenzieren können (z. B. `src/main/resources`).  
- Grundlegende Vertrautheit mit der `main`‑Methode von Java und der Ausnahmebehandlung.

Falls Ihnen etwas davon unbekannt ist, keine Sorge – jeder Schritt enthält eine kurze Zusammenfassung.

## Schritt 1: Projekt einrichten und die OCR‑Bibliothek hinzufügen

Erstellen Sie zunächst ein neues Maven‑Projekt (oder Gradle, wenn Sie das bevorzugen). Fügen Sie die Tess4J‑Abhängigkeit hinzu, die die Tesseract‑Binärdateien für Sie bereitstellt.

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
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

> **Pro‑Tipp:** Wenn Sie Gradle verwenden, lautet die entsprechende Zeile `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'`.

Durch das Hinzufügen dieser Bibliothek erhalten Sie die Klasse `Tesseract`, die das schwere Heben der **Durchführung von OCR auf Bild**‑Daten übernimmt.

## Schritt 2: Bild für OCR laden

Jetzt müssen wir **Bild für OCR laden**. Tess4J arbeitet mit `java.awt.image.BufferedImage`, also lesen wir die PNG mit `ImageIO`.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class OcrDemo {

    /**
     * Loads a PNG file from the given path and returns a BufferedImage.
     *
     * @param path absolute or relative path to the PNG file
     * @return BufferedImage containing the image data
     * @throws IOException if the file cannot be read
     */
    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image to be recognized
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }
```

Die obige Methode isoliert sauber die **Bild‑für‑OCR‑Laden**‑Logik, wodurch der Rest des Codes leichter zu testen ist. Beachten Sie den Kommentar – er spiegelt das ursprüngliche Snippet wider und erweitert es zur Klarheit.

## Schritt 3: OCR auf Bild ausführen

Mit dem Bild im Speicher können wir nun **OCR auf Bild ausführen**. Die `Tesseract`‑Instanz ist unsere Engine; wir konfigurieren sie, die standardmäßigen englischen Sprachdaten zu verwenden, die mit Tess4J geliefert werden.

```java
    /**
     * Runs OCR on the supplied BufferedImage and returns the extracted text.
     *
     * @param image the image to analyze
     * @return plain text recognized from the image
     * @throws TesseractException if the OCR process fails
     */
    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();

        // Optional: set the datapath if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");

        // Step 4: Run OCR and capture the recognized text
        return tesseract.doOCR(image);
    }
```

Hier haben wir die ursprünglichen „Schritt 1“ und „Schritt 4“ zu einer einzigen Methode zusammengeführt, weil das `Tesseract`‑Objekt günstig zu erstellen ist und wir den Code kompakt halten wollen. Der Kommentar verweist weiterhin auf die ursprünglichen Schritte zur Nachvollziehbarkeit.

## Schritt 4: Alles zusammenführen – Main‑Methode

Zum Schluss fügen wir alles in `main` zusammen. Hier werden Sie **Text aus PNG lesen** und das Ergebnis in der Konsole ausgeben.

```java
    public static void main(String[] args) {
        // Adjust the path to point at your PNG file
        String imagePath = "src/main/resources/sample.png";

        try {
            // Load the PNG image
            BufferedImage image = loadImage(imagePath);

            // Extract text from the image
            String recognizedText = extractText(image);

            // Step 5: Display the extracted text
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR error: " + e.getMessage());
        }
    }
}
```

Wenn Sie `mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"` ausführen (oder das Gradle‑Äquivalent), sollten Sie etwa Folgendes sehen:

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

Diese Ausgabe beweist, dass Sie erfolgreich **Text aus Bild extrahieren**, **PNG in Text konvertieren** und **Text aus PNG lesen** in einem einzigen, übersichtlichen Programm.

## Umgang mit häufigen Sonderfällen

### Bilder mit niedriger Qualität

Wenn die PNG unscharf ist oder wenig Kontrast hat, sinkt die OCR‑Genauigkeit. Eine schnelle Lösung ist die Vorverarbeitung des Bildes:

```java
// Example: Convert to grayscale and apply a binary threshold
BufferedImage gray = new BufferedImage(
        image.getWidth(), image.getHeight(),
        BufferedImage.TYPE_BYTE_GRAY);
Graphics2D g = gray.createGraphics();
g.drawImage(image, 0, 0, null);
g.dispose();

// Simple binary threshold
for (int y = 0; y < gray.getHeight(); y++) {
    for (int x = 0; x < gray.getWidth(); x++) {
        int rgb = gray.getRGB(x, y) & 0xFF;
        int binary = rgb < 128 ? 0x000000 : 0xFFFFFF;
        gray.setRGB(x, y, binary);
    }
}
String text = extractText(gray);
```

### Mehrsprachige Unterstützung

Tess4J kann viele Sprachen verarbeiten. Laden Sie einfach die passende `.traineddata`‑Datei herunter und setzen Sie `tesseract.setLanguage("spa")` für Spanisch, zum Beispiel.

### Große PDFs oder mehrseitige Bilder

Wenn Sie **Text aus Bild**‑Dateien innerhalb eines PDFs extrahieren müssen, teilen Sie zunächst jede Seite in PNGs (mit PDFBox) und übergeben dann jedes PNG an dieselbe OCR‑Routine.

## Vollständiges funktionierendes Beispiel (Gesamter Code an einem Ort)

Unten finden Sie die komplette, sofort ausführbare Java‑Klasse. Kopieren Sie sie nach `src/main/java/com/example/ocrdemo/OcrDemo.java` und Sie können loslegen.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Demonstrates how to extract text from image (PNG) using Java and Tess4J.
 */
public class OcrDemo {

    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image for OCR
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }

    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();
        // Uncomment and set if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");
        // Step 4: Perform OCR on image
        return tesseract.doOCR(image);
    }

    public static void main(String[] args) {
        // Path to the PNG you want to convert to text
        String imagePath = "src/main/resources/sample.png";

        try {
            BufferedImage image = loadImage(imagePath);
            String recognizedText = extractText(image);
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("Error during OCR: " + e.getMessage());
        }
    }
}
```

Das Ausführen der Klasse gibt das OCR‑Ergebnis aus und bestätigt, dass Sie erfolgreich **OCR auf Bild ausgeführt** haben und Ihre PNG in editierbaren Text umgewandelt haben.

## Zusammenfassung & nächste Schritte

Wir haben mit **Text aus Bild extrahieren** unter Verwendung einer leichten Java‑Umgebung begonnen. Sie wissen jetzt, wie man **Bild für OCR lädt**, **OCR auf Bild ausführt** und **Text aus PNG liest** – wesentliche Bausteine für jede Dokument‑Digitalisierungspipeline.

Möchten Sie weitergehen? Probieren Sie diese Ideen aus:

- **Batch‑Verarbeitung:** Durchlaufen Sie ein Verzeichnis mit PNGs und schreiben Sie jedes Ergebnis in eine `.txt`‑Datei.  
- **Integration mit einer Datenbank:** Speichern Sie extrahierte Zeichenketten zusammen mit Metadaten für durchsuchbare Archive.  
- **Kombination mit NLP:** Führen Sie die OCR‑Ausgabe in ein Sentiment‑Analyse‑Modell ein, um schnelle Einblicke zu erhalten.

Jede dieser Erweiterungen baut auf denselben Kernkonzepten auf, die wir behandelt haben, sodass Sie bereit zum Experimentieren sind.

---

*Viel Spaß beim Coden! Wenn Sie auf Probleme stoßen*

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Text aus Bild in Java mit Aspose.OCR Detect Areas Mode extrahieren](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Bild zu Text Java: Bild mit Aspose.OCR in Text konvertieren](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Wie man Bildtext mit Sprache mittels Aspose.OCR OCR‑t](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}