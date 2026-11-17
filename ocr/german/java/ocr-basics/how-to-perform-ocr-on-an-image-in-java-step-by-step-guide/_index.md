---
category: general
date: 2026-11-17
description: Erfahren Sie, wie Sie OCR auf einem Bild in Java durchführen und Text
  aus Bildern mit einem einfachen Codebeispiel extrahieren. Enthält Tipps zum Bildlesen
  in Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text image
- read image java
- convert image to text
- image to text java
language: de
lastmod: 2026-11-17
og_description: Wie man OCR auf einem Bild in Java durchführt und Text schnell extrahiert.
  Folgen Sie dieser Anleitung, um ein Bild in Java zu lesen und das Bild in Text zu
  konvertieren, mit einem sofort einsatzbereiten Beispiel.
og_image_alt: Screenshot showing Java code that performs OCR on an image
og_title: Wie man OCR in Java auf einem Bild durchführt – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Learn how to perform OCR on an image in Java and extract text from
    pictures using a simple code example. Includes read image Java tips.
  headline: How to perform OCR on an image in Java – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Java
- Image processing
- Text extraction
title: Wie man OCR in Java auf einem Bild durchführt – Schritt‑für‑Schritt‑Anleitung
url: /de/java/ocr-basics/how-to-perform-ocr-on-an-image-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR auf einem Bild in Java durchführt – Schritt‑für‑Schritt‑Anleitung

Wenn Sie **wie man OCR durchführt** auf ein Bild anwenden müssen, zeigt Ihnen dieses Tutorial eine komplette, ausführbare Lösung in Java. Sie sehen, wie man eine Bilddatei liest, eine OCR‑Engine konfiguriert und den Text extrahiert, den die Engine erkennt.

Die Arbeit mit gescannten Dokumenten, Quittungen oder Screenshots erfordert häufig die Umwandlung des visuellen Inhalts in durchsuchbaren Text. Dieser Leitfaden führt Sie durch jeden Schritt, vom Laden des Bildes bis zum Ausgeben des extrahierten Textes, und behandelt zudem gängige Fallstricke wie nicht unterstützte Dateiformate und null‑Ergebnisse.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

* Java Development Kit (JDK) 8 oder neuer installiert.
* Ein Build‑Tool (Maven oder Gradle), um die OCR‑Bibliothek zu beziehen.
* Eine Bilddatei (JPEG, PNG, BMP), die Sie verarbeiten möchten.

Der Code verwendet die **OCR library from the `com.asprise.ocr` package**, weil sie nur ein einziges JAR benötigt und auf allen gängigen Plattformen funktioniert. Ersetzen Sie sie durch einen anderen Anbieter (Tesseract, Google Vision usw.), indem Sie die Import‑Anweisungen und den Engine‑Initialisierungscode austauschen.

## Schritt 1: OCR‑Abhängigkeit hinzufügen

Wenn Sie Maven verwenden, fügen Sie die folgende Abhängigkeit zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.2.0</version>
</dependency>
```

Für Gradle platzieren Sie diese Zeile in `build.gradle`:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.2.0'
```

Diese Zeilen stellen sicher, dass der **read image Java**‑Code kompiliert und die OCR‑Engine zur Laufzeit verfügbar ist.

## Schritt 2: Bild mit Java lesen

Das Lesen einer Bilddatei ist der erste konkrete Schritt in jedem **extract text image**‑Workflow. Die eingebaute Java‑Klasse `ImageIO` unterstützt die meisten gängigen Formate.

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Loads an image from the supplied path.
 *
 * @param path absolute or relative path to the image file
 * @return a BufferedImage instance, or null if the file cannot be read
 */
private static BufferedImage loadImage(String path) {
    try {
        return ImageIO.read(new File(path));
    } catch (Exception e) {
        System.err.println("Failed to read image: " + e.getMessage());
        return null;
    }
}
```

**Why this matters:** `ImageIO.read` gibt `null` zurück, wenn das Format nicht unterstützt wird oder die Datei beschädigt ist. Die obige Methode protokolliert das Problem und gibt `null` zurück, sodass der nächste Schritt elegant reagieren kann.

## Schritt 3: OCR‑Engine erstellen und konfigurieren

Die OCR‑Engine muss wissen, welche Sprache sie erkennen soll. Das Festlegen der Sprache verbessert die Genauigkeit erheblich, besonders bei nicht‑englischen Dokumenten.

```java
import com.asprise.ocr.Ocr;

/**
 * Instantiates an OCR engine configured for English.
 *
 * @return a ready‑to‑use Ocr object
 */
private static Ocr createEngine() {
    Ocr ocrEngine = new Ocr();
    // The first argument is the language; "eng" is the ISO code for English.
    ocrEngine.startEngine("eng", Ocr.SPEED_FAST);
    return ocrEngine;
}
```

**Why this matters:** Das Starten der Engine ist ein relativ aufwändiger Vorgang, daher sollten Sie sie einmal erstellen und für mehrere Bilder wiederverwenden, wenn Ihre Anwendung Stapel verarbeitet.

## Schritt 4: OCR ausführen und das Bild in Text umwandeln

Jetzt, wo das Bild geladen und die Engine bereit ist, können Sie den Erkennungsschritt ausführen. Dies ist der Kern von **wie man OCR durchführt**.

```java
/**
 * Runs OCR on a BufferedImage and returns the recognized text.
 *
 * @param ocrEngine an initialized Ocr instance
 * @param image     the image to process
 * @return the extracted text, or an empty string if nothing is recognized
 */
private static String extractText(Ocr ocrEngine, BufferedImage image) {
    if (image == null) {
        return "";
    }
    // The third parameter (0) tells the engine to return plain text.
    String result = ocrEngine.recognize(image, 0);
    return result != null ? result.trim() : "";
}
```

**Edge‑case handling:** Wenn das Bild `null` ist, gibt die Methode einen leeren String zurück, anstatt eine `NullPointerException` zu werfen. Das macht den umgebenden Code robuster beim Umgang mit benutzer‑supplierten Dateien.

## Schritt 5: Extrahierten Text anzeigen

Drucken Sie schließlich das Ergebnis in die Konsole oder leiten Sie es an eine andere Komponente weiter (z. B. eine Datenbank oder ein UI‑Widget).

```java
/**
 * Demonstrates the full OCR workflow.
 *
 * @param args command‑line arguments (first argument = path to image)
 */
public static void main(String[] args) {
    if (args.length == 0) {
        System.err.println("Usage: java OcrDemo <path-to-image>");
        return;
    }

    String imagePath = args[0];
    BufferedImage image = loadImage(imagePath);
    Ocr ocrEngine = createEngine();

    String text = extractText(ocrEngine, image);
    System.out.println("=== Recognized Text ===");
    System.out.println(text.isEmpty() ? "(no text detected)" : text);

    // Clean up the OCR engine to free native resources.
    ocrEngine.stopEngine();
}
```

Wenn Sie das Programm mit `java OcrDemo sample.jpg` ausführen, zeigt die Konsole die erkannten Zeichen. Damit ist der **convert image to text**‑Zyklus abgeschlossen.

### Erwartete Ausgabe

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

Enthält das Bild keine lesbaren Zeichen, gibt das Programm `(no text detected)` aus.

## Häufige Variationen und wie man sie anpasst

| Variation | Was ändert sich | Wann zu verwenden |
|-----------|-----------------|-------------------|
| **Andere Sprache** | Ersetzen Sie `"eng"` durch `"spa"` für Spanisch, `"fra"` für Französisch usw. | Dokumente, die in einer anderen Sprache als Englisch verfasst sind |
| **Stapelverarbeitung** | Durchlaufen Sie eine Liste von Dateipfaden, verwenden Sie dieselbe `Ocr`‑Instanz erneut. | Große Mengen gescannter Seiten |
| **Höhere Genauigkeit** | Verwenden Sie `Ocr.SPEED_SLOW` oder aktivieren Sie `ocrEngine.setConfig("tessedit_char_whitelist", "0123456789")` für rein numerische Scans. | Wenn die OCR‑Qualität kritisch ist (z. B. Rechnungsnummern) |
| **Tesseract‑Alternative** | Tauschen Sie den Import zu `net.sourceforge.tess4j.Tesseract` aus und passen Sie den Initialisierungscode an. | Projekte, die bereits von Tesseract abhängen |

## Pro‑Tipps

* **Große Bilder verkleinern** bevor Sie sie an die Engine übergeben; die OCR‑Geschwindigkeit skaliert mit der Pixelanzahl.
* **Vorverarbeiten** Sie das Bild (Graustufen, Kontrastverstärkung) mit Bibliotheken wie OpenCV, wenn die Quelle verrauscht ist.
* **Cache die OCR‑Engine**, wenn Sie sie häufig in kurzer Zeit aufrufen – das Starten und Stoppen der Engine verursacht Overhead.
* **Validieren Sie das Ergebnis** mit regulären Ausdrücken, wenn Sie ein bestimmtes Format erwarten (z. B. Daten, Telefonnummern).

## Fazit

Sie wissen jetzt **wie man OCR durchführt** auf einem Bild in Java, vom Lesen der Datei bis zum Anzeigen des extrahierten Textes. Das Tutorial behandelte die Techniken **read image Java**, **extract text image**, **convert image to text** und **image to text java** und bot praktische Tipps für reale Szenarien.

Von hier aus können Sie:

* Die OCR‑Stufe in einen Web‑Service integrieren, der Uploads entgegennimmt.
* Die Ausgabe mit einem Suchindex für Volltextsuche über gescannte Dokumente kombinieren.
* Erweiterte OCR‑Optionen wie Mehrsprachunterstützung oder benutzerdefinierte Zeichensätze erkunden.

Viel Spaß beim Programmieren und beim Umwandeln von Bildern in durchsuchbaren Text!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden demonstrierten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man OCR in Java verwendet – Text aus Bild mit Rechtschreibkorrektur extrahieren](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/)
- [Bild in Text in Java mit Aspose OCR konvertieren – Vollständige Anleitung](/ocr/english/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/)
- [Wie man GPU für OCR in Java aktiviert – Text aus Bild extrahieren](/ocr/english/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}