---
category: general
date: 2026-05-25
description: Text aus Bild in Java mit OCR extrahieren. Erfahren Sie, wie Sie ein
  Bild für OCR laden, Text aus einem Foto erkennen und den Text aus OCR mit einem
  einfachen Codebeispiel erhalten.
draft: false
keywords:
- extract text from image
- get text from ocr
- recognize text from photo
- java image to text
- load image for ocr
language: de
og_description: Extrahiere Text aus Bildern in Java mit einer Schritt‑für‑Schritt‑Anleitung.
  Lerne, wie man ein Bild für OCR lädt, Text aus einem Foto erkennt und Text effizient
  aus OCR erhält.
og_title: Text aus Bild in Java extrahieren – Text per OCR erhalten
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  headline: Extract Text from Image in Java – Get Text from OCR
  type: TechArticle
- description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  name: Extract Text from Image in Java – Get Text from OCR
  steps:
  - name: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
    text: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
  - name: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
    text: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
  - name: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
    text: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
  - name: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
    text: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
  - name: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
    text: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Text aus Bild in Java extrahieren – Text aus OCR erhalten
url: /de/java/ocr-basics/extract-text-from-image-in-java-get-text-from-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bild in Java – Text aus OCR erhalten

Haben Sie jemals **extract text from image** extrahieren müssen, waren sich aber nicht sicher, welche Java‑Bibliothek Sie wählen sollen? Sie sind nicht allein. Egal, ob Sie Belege digitalisieren, Seriennummern aus Produktfotos extrahieren oder einfach nur an einem lustigen Nebenprojekt spielen, ein Bild in editierbaren Text zu verwandeln, ist ein häufiges Hindernis.

In diesem Tutorial führen wir Sie durch ein komplettes, sofort ausführbares Beispiel, das zeigt, wie Sie **load image for OCR** konfigurieren, die Engine einstellen und schließlich **recognize text from photo**, sodass Sie **get text from OCR** mit nur wenigen Codezeilen erhalten können. Keine vagen Verweise – alles, was Sie brauchen, ist hier.

## Was Sie lernen werden

* Wie man eine leichte OCR‑Engine in Java einrichtet.  
* Die genauen Schritte zum **load image for OCR** und zum Umgang mit verschiedenen Dateipfaden.  
* Warum die Konfiguration der Sprache wichtig ist, wenn Sie **extract text from image** extrahieren möchten, das nicht Englisch ist.  
* Wie man das Ergebnis sicher ausgibt und was zu tun ist, wenn die Engine nichts zurückgibt.  
* Eine Handvoll Pro‑Tipps, um die häufigsten Fallstricke zu vermeiden.

Am Ende dieses Leitfadens haben Sie ein eigenständiges Programm, das ein JPEG (oder PNG) mit ukrainischen Zeichen liest und die erkannte Zeichenkette in der Konsole ausgibt. Sie können die Sprache oder das Bild problemlos austauschen – alles ist modular.

![Flussdiagramm des Prozesses zum Extrahieren von Text aus Bild in Java](/images/extract-text-from-image-java.png)

*Alt text: Flussdiagramm des Prozesses zum Extrahieren von Text aus Bild in Java.*

## Voraussetzungen

* **Java Development Kit (JDK) 11+** – Der Code verwendet das moderne Modulsystem, aber ältere Versionen funktionieren mit kleinen Anpassungen.  
* **Maven oder Gradle** – um die OCR‑Bibliothek zu beziehen (wir verwenden **Asprise OCR** als leichte, kostenlos‑für‑Entwicklungs‑Option).  
* Eine Beispielbilddatei (z. B. `ukrainian_sign.jpg`) an einem Ort, den Ihr Programm lesen kann.  
* Grundlegende Vertrautheit mit der `main`‑Methode von Java und Ausnahmebehandlung.

Wenn Sie diese haben, können Sie loslegen. Andernfalls holen Sie sich das JDK von Oracle oder AdoptOpenJDK und richten ein einfaches Maven‑Projekt ein – nichts Aufwändiges.

## Schritt 1: OCR‑Abhängigkeit hinzufügen

Zuerst teilen Sie Ihrem Build‑Tool mit, die OCR‑Engine zu holen. Für Maven fügen Sie das in `pom.xml` ein:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.0.2</version>
</dependency>
```

Wenn Sie Gradle bevorzugen, ist das Äquivalent:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.0.2'
```

Diese Koordinaten holen ein kompaktes JAR, das `OcrEngine`, `OcrLanguage` und die Hilfsklassen enthält, die wir verwenden werden. Für grundlegende lateinische und kyrillische Skripte sind keine zusätzlichen nativen Binärdateien erforderlich.

## Schritt 2: Eine Java‑Klasse zum **Extract Text from Image** erstellen

Jetzt schreiben wir das eigentliche Programm. Speichern Sie das Folgende als `ExtractTextDemo.java` in `src/main/java/com/example/ocr/`.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;

/**
 * Demonstrates how to extract text from image using Asprise OCR.
 * The example loads a JPEG, sets the language to Ukrainian,
 * runs recognition, and prints the result.
 */
public class ExtractTextDemo {

    public static void main(String[] args) {
        // ---- 1️⃣  Initialize the OCR engine ---------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---- 2️⃣  Configure the engine to recognize Ukrainian text -----------
        // This is crucial if your image contains non‑Latin characters.
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.UKRAINIAN);

        // ---- 3️⃣  Load the image that contains Ukrainian characters ----------
        // Replace the path with the location of your own picture.
        String imagePath = "YOUR_DIRECTORY/ukrainian_sign.jpg";
        try {
            ocrEngine.getImage().loadFromFile(imagePath);
        } catch (Exception e) {
            System.err.println("Failed to load image: " + e.getMessage());
            return;
        }

        // ---- 4️⃣  Perform OCR recognition and obtain the extracted text -------
        String recognizedText;
        try {
            recognizedText = ocrEngine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Recognition error: " + e.getMessage());
            return;
        }

        // ---- 5️⃣  Output the recognized text to the console -------------------
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### Warum diese Struktur funktioniert

* **Separate numbered blocks** machen den Ablauf leicht nachvollziehbar, besonders wenn Sie nach dem Ort suchen, an dem **load image for OCR** oder **recognize text from photo** durchgeführt wird.  
* Das `try/catch` rund um das Laden des Bildes und die Erkennung stellt sicher, dass das Programm graceful fehlschlägt – nützlich, wenn der Dateipfad falsch ist oder die OCR‑Engine die Sprachdaten nicht findet.  
* Das frühe Setzen der Sprache (Schritt 2) verbessert die Genauigkeit für nicht‑englische Skripte erheblich. Wenn Sie später **java image to text** für andere Sprachen benötigen, tauschen Sie einfach `OcrLanguage.UKRAINIAN` gegen `OcrLanguage.ENGLISH`, `FRENCH` usw.

## Schritt 3: Das Programm bauen und ausführen

Aus dem Projektstammverzeichnis führen Sie aus:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ExtractTextDemo"
```

Oder, wenn Sie Gradle verwenden:

```bash
./gradlew run --args="com.example.ocr.ExtractTextDemo"
```

Angenommen, `ukrainian_sign.jpg` enthält den Text *«Ласкаво просимо»* (Ukrainisch für „Willkommen“), Sie sollten etwas Ähnliches sehen:

```
=== OCR Result ===
Ласкаво просимо
```

Diese Ausgabe bestätigt, dass Sie erfolgreich **extract text from image** und **get text from OCR** in einem einzigen Durchlauf durchgeführt haben.

## Schritt 4: Workflow anpassen – Von **Java Image to Text** in realen Projekten

Obwohl das Demo minimal ist, benötigen reale Anwendungen oft etwas mehr:

| Szenario | Was anzupassen | Grund |
|----------|----------------|--------|
| **Batch processing** | Durchlaufen Sie eine `List<Path>` und speichern jedes Ergebnis in einer Datenbank. | Reduziert manuelle Arbeit, wenn Sie Hunderte von Fotos haben. |
| **Different image formats** | Verwenden Sie `ImageIO.read(new File(path))` zur Vorverarbeitung und übergeben dann das `BufferedImage` an `ocrEngine.getImage().loadFromBufferedImage(bufImg)`. | Verarbeitet PNG, BMP oder sogar PDFs nach Konvertierung. |
| **Performance tuning** | Rufen Sie `ocrEngine.getEngineOptions().setSpeed(OcrEngine.Speed.FAST)` auf, wenn Ihnen eine leicht geringere Genauigkeit recht ist. | Beschleunigt die Erkennung auf schwacher Hardware. |
| **Post‑processing** | Entfernen Sie Leerzeichen, ersetzen häufige OCR‑Fehlinterpretationen (`0` → `O`, `1` → `I`). | Verbessert die Datenqualität nachgelagert. |

Diese Varianten erhalten die Kernidee – **recognize text from photo** – unverändert, geben Ihnen jedoch Flexibilität für Produktionslasten.

## Häufige Fallstricke & Pro‑Tipps

1. **Wrong language setting** – Wenn Sie Schritt 2 vergessen, verwendet die Engine standardmäßig Englisch und verwandelt kyrillische Zeichen in Kauderwelsch. Überprüfen Sie den Sprachcode immer doppelt.  
2. **Image quality matters** – Niedrigauflösende oder verschwommene Fotos verringern die Genauigkeit. Vorverarbeiten mit Kontrastverstärkung oder Binarisierung, falls nötig.  
3. **File path quirks** – Unter Windows müssen Backslashes escaped werden (`C:\\images\\file.jpg`). Die Verwendung von `Path.of(...)` aus `java.nio.file` umgeht das.  
4. **Memory leaks** – `OcrEngine` hält native Ressourcen. Rufen Sie `ocrEngine.dispose()` auf, wenn Sie fertig sind, besonders in langlaufenden Diensten.  
5. **Thread safety** – Die Engine ist nicht von Haus aus thread‑sicher. Erstellen Sie pro Thread eine separate Instanz oder synchronisieren Sie den Zugriff.

## Vollständiges funktionierendes Beispiel (Alles‑in‑einem)

Unten finden Sie eine einzelne Datei, die Sie in jede IDE kopieren und einfügen können. Sie enthält den Aufruf `dispose()` und eine kleine Hilfsmethode, um den Code etwas sauberer zu machen.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;
import java.nio.file.Path;

/**
 * Complete, runnable demo that extracts text from an image using Java OCR.
 */
public class FullDemo {

    public static void main(String[] args) {
        // Path to the image – change this to your own file.
        Path imgPath = Path.of("YOUR_DIRECTORY/ukrainian_sign.jpg");

        // Run the OCR workflow and capture the output.
        String result = extractTextFromImage(imgPath, OcrLanguage.UKRAINIAN);
        if (result != null) {
            System.out.println("=== OCR Result ===");
            System.out.println(result);
        }
    }

    /**
     * Core method that encapsulates the 5‑step OCR process.
     *
     * @param imagePath Path to the image file.
     * @param language  Desired OCR language.
     * @return Recognized text, or {@code null} if something went wrong.
     */
    private static String extractTextFromImage(Path imagePath, OcrLanguage language) {
        OcrEngine engine = new OcrEngine();
        try {
            // 1️⃣ Set language
            engine.getEngineOptions().setLanguage(language);

            // 2️⃣ Load image
            engine.getImage().loadFromFile(imagePath.toString());

            // 3️⃣ Recognize and return text
            return engine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Error during OCR: " + e.getMessage());
            return null;
        } finally {
            // 4️⃣ Release native resources
            engine.dispose();
        }
    }
}
```

Das Ausführen dieses Programms liefert die gleiche Konsolenausgabe wie zuvor gezeigt. Sie können `OcrLanguage.UKRAINIAN` gerne durch `OcrLanguage.ENGLISH` oder eine andere unterstützte Sprache ersetzen, um zu sehen, wie die Engine reagiert.

## Fazit

Wir haben alles durchgegangen, was Sie benötigen, um **extract text from image** mit Java zu verwenden: vom Hinzufügen der OCR‑Abhängigkeit bis zum **load image for OCR**,

## Verwandte Tutorials

- [Textbild mit Aspose OCR erkennen – Vollständiges Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Wie man Bildtext mit Sprache mittels Aspose.OCR OCRt](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Bild in Text in Java konvertieren mit Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}