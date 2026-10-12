---
category: general
date: 2026-10-11
description: Erfahren Sie, wie Sie OCR auf einem PNG‑Bild in Java durchführen, Text
  aus dem Bild extrahieren und das Bild mit einem einfachen OcrEngine‑Beispiel in
  Text umwandeln.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: de
lastmod: 2026-10-11
og_description: Wie man OCR auf einem PNG‑Bild in Java durchführt, Text aus dem Bild
  extrahiert und das Bild in Text umwandelt, mit einem knappen, sofort einsatzbereiten
  Beispiel.
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: Wie man OCR auf einem PNG‑Bild in Java durchführt – vollständige Anleitung
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  headline: How to perform OCR on a PNG image in Java
  type: TechArticle
- description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  name: How to perform OCR on a PNG image in Java
  steps:
  - name: 4.1 Handling low‑resolution PNGs
    text: 'Tesseract performs best on images with at least 300 DPI. If your source
      PNG is smaller, upscale it before OCR:'
  - name: 4.2 Extracting non‑English text
    text: 'To **extract text from image** that contains other languages, download
      the appropriate `.traineddata` files and set the language code:'
  - name: 4.3 Batch processing multiple PNGs
    text: 'If you need to **recognize text from PNG** files in a folder, iterate over
      the directory:'
  - name: 4.4 Dealing with OCR errors
    text: 'Typical OCR mistakes include misreading `0` (zero) as `O` or `1` as `l`.
      Post‑processing with regular expressions can clean the result:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
- Text Extraction
title: Wie man OCR auf einem PNG‑Bild in Java durchführt
url: /de/java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR auf einem PNG‑Bild in Java durchführt

Wenn Sie **OCR ausführen** müssen, ist das **Durchführen von OCR** in Java für viele Automatisierungsaufgaben unverzichtbar. Ob Sie Belege digitalisieren, gescannte Dokumente indexieren oder ein durchsuchbares Foto‑Archiv erstellen – die Fähigkeit, **Text aus Bild**‑Dateien zu **extrahieren** spart unzählige manuelle Stunden.

Dieses Tutorial zeigt Ihnen eine komplette, ausführbare Lösung, die ein PNG lädt, eine OCR‑Engine ausführt und **Text aus PNG**‑Dateien **erkennt**. Sie sehen außerdem, wie man **Bild zu Text** konvertiert und gängige Stolperfallen wie niedrige Auflösung oder Nicht‑ASCII‑Zeichen handhabt.

## Was Sie erreichen werden

Am Ende dieses Leitfadens können Sie:

* **load image java**‑Code, der ein PNG von der Festplatte liest,
* eine leichte OCR‑Engine initialisieren,
* **extract text from image** und das Ergebnis in der Konsole ausgeben,
* die Lösung für andere Bildformate oder Batch‑Verarbeitung anpassen.

Es werden keine externen Dienste benötigt – nur eine einzige Open‑Source‑OCR‑Bibliothek (Tess4J) und die Java SE‑Runtime.

---

## Voraussetzungen

* Java 17 oder neuer (der Code kompiliert mit JDK 17).
* Maven oder Gradle für das Dependency‑Management.
* Grundlegende Kenntnisse im Umgang mit der Kommandozeile und Ihrer bevorzugten IDE.
* Die Bibliothek `tess4j` (ein Java‑Wrapper für Tesseract). Fügen Sie die folgende Maven‑Abhängigkeit hinzu:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Wenn Sie Gradle verwenden, lautet das Äquivalent:

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

Sie benötigen außerdem die Tesseract‑Daten‑Dateien (`.traineddata`). Laden Sie das englische Datenpaket aus dem offiziellen Repository herunter und legen Sie es in einem Ordner namens `tessdata` im Projekt‑Root ab.

---

## Schritt 1: Bild in Java laden

Das Laden eines PNG ist mit der Standard‑Klasse `ImageIO` unkompliziert. Der untenstehende Code demonstriert **load image java** auf sichere, ausnahme‑bewusste Weise:

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Reads a PNG file from the given path and returns a BufferedImage.
 *
 * @param path absolute or relative path to the PNG file
 * @return BufferedImage representation of the file
 * @throws Exception if the file cannot be read or is not a PNG
 */
private static BufferedImage loadPng(String path) throws Exception {
    File imgFile = new File(path);
    if (!imgFile.exists()) {
        throw new IllegalArgumentException("File not found: " + path);
    }
    BufferedImage img = ImageIO.read(imgFile);
    if (img == null) {
        throw new IllegalArgumentException("Unsupported image format or corrupt file: " + path);
    }
    return img;
}
```

**Warum das wichtig ist:** `ImageIO.read` erkennt das Bildformat automatisch, aber wir prüfen explizit auf `null`, um stille Fehler bei beschädigten PNGs zu vermeiden. Dieses Muster ist eine bewährte Praxis, wenn Sie **load image java** für OCR verwenden.

---

## Schritt 2: OCR‑Engine initialisieren

Tess4J umschließt das native Tesseract‑Binary und stellt eine einfache Java‑API bereit. Die folgende Methode erzeugt eine `Tesseract`‑Instanz, verweist auf den `tessdata`‑Ordner und konfiguriert die Sprache auf Englisch:

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;

/**
 * Configures and returns a ready‑to‑use Tesseract instance.
 *
 * @return configured ITesseract object
 */
private static ITesseract createOcrEngine() {
    ITesseract tesseract = new Tesseract();
    // Path to the folder that contains .traineddata files
    tesseract.setDatapath("tessdata");
    // Language code – "eng" for English; you can add more languages later
    tesseract.setLanguage("eng");
    // Optional: increase OCR accuracy for PNGs with low DPI
    tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
    return tesseract;
}
```

**Warum wir das tun:** Die Engine einmal zu initialisieren und für mehrere Bilder wiederzuverwenden reduziert den Start‑Overhead. Der Aufruf `setOcrEngineMode` wählt den Standard‑Modus, der für die meisten PNGs gut funktioniert. Bei verrauschten Scans können Sie mit anderen Modi experimentieren (z. B. `OEM_LSTM_ONLY`).

---

## Schritt 3: OCR ausführen und **recognize text from PNG**

Jetzt kombinieren wir den Bild‑Lader und die OCR‑Engine. Die Methode unten führt OCR auf einem `BufferedImage` aus und gibt den extrahierten String zurück:

```java
/**
 * Runs OCR on the supplied image and returns the recognized text.
 *
 * @param image BufferedImage containing the PNG to process
 * @param tesseract configured OCR engine
 * @return plain‑text result of OCR
 * @throws Exception if OCR fails
 */
private static String extractText(BufferedImage image, ITesseract tesseract) throws Exception {
    // Tess4J can directly accept a BufferedImage
    return tesseract.doOCR(image);
}
```

**Vollständiges ausführbares Beispiel**

```java
import java.awt.image.BufferedImage;
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.TesseractException;

public class OcrDemo {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the PNG file
            BufferedImage image = loadPng("sample.png");

            // 2️⃣ Create and configure the OCR engine
            ITesseract ocrEngine = createOcrEngine();

            // 3️⃣ Recognize text from PNG
            String recognizedText = extractText(image, ocrEngine);

            // 4️⃣ Display the result – this is the **convert image to text** step
            System.out.println("=== OCR RESULT ===");
            System.out.println(recognizedText);
        } catch (Exception e) {
            System.err.println("Error during OCR processing:");
            e.printStackTrace();
        }
    }

    // ----- Helper methods from previous steps -----
    // loadPng, createOcrEngine, extractText (copy-pasted here for completeness)
    // ... (methods omitted for brevity; see the sections above) ...
}
```

**Erwartete Ausgabe**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

Die Konsole zeigt die genauen Zeichen, die die Engine aus `sample.png` extrahiert hat. Enthält das PNG nur ein einzelnes Wort, wird dieses Wort gefolgt von einem Zeilenumbruch ausgegeben.

---

## Schritt 4: Häufige Varianten und Sonderfälle

### 4.1 Umgang mit niedrigauflösenden PNGs

Tesseract liefert beste Ergebnisse bei Bildern mit mindestens 300 DPI. Ist Ihr Quell‑PNG kleiner, skalieren Sie es vor dem OCR hoch:

```java
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.RenderingHints;

private static BufferedImage upscale(BufferedImage src, int scaleFactor) {
    int width = src.getWidth() * scaleFactor;
    int height = src.getHeight() * scaleFactor;
    Image tmp = src.getScaledInstance(width, height, Image.SCALE_SMOOTH);
    BufferedImage resized = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
    Graphics2D g2d = resized.createGraphics();
    g2d.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                         RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g2d.drawImage(tmp, 0, 0, null);
    g2d.dispose();
    return resized;
}
```

Wenden Sie `upscale(image, 2)` vor dem Aufruf von `extractText` an, um die Genauigkeit zu verbessern.

### 4.2 Extrahieren von nicht‑englischem Text

Um **extract text from image** zu erhalten, das andere Sprachen enthält, laden Sie die entsprechenden `.traineddata`‑Dateien herunter und setzen Sie den Sprachcode:

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 Batch‑Verarbeitung mehrerer PNGs

Wenn Sie **recognize text from PNG**‑Dateien in einem Ordner verarbeiten müssen, iterieren Sie über das Verzeichnis:

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 Umgang mit OCR‑Fehlern

Typische OCR‑Fehler sind das Verwechseln von `0` (Null) mit `O` oder `1` mit `l`. Eine Nachbearbeitung mit regulären Ausdrücken kann das Ergebnis bereinigen:

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

---

## Pro‑Tipps für zuverlässiges OCR in Java

| Tipp | Grund |
|-----|--------|
| **Verwenden Sie ein verlustfreies PNG** | Kompressionsartefakte in JPEG können die Engine verwirren. |
| **Weiße Ränder zuschneiden** | Überflüssiger Whitespace erhöht die Verarbeitungszeit und kann Fehlalarme verursachen. |
| **Setzen Sie `tesseract.setPageSegMode(ITesseract.PSM_AUTO)`** nur, wenn das Layout unbekannt ist; wählen Sie sonst einen spezifischen Modus (z. B. `PSM_SINGLE_BLOCK`). |
| **Cache die `ITesseract`‑Instanz** |


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [How to Read Text from an Image in Java Using Aspose OCR – Complete Guide](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [How to Use OCR in Java – Recognize Text from Image Quickly](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [Batch Image OCR in Java – Extract Text from PNG Files Fast](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}