---
category: general
date: 2026-06-06
description: Wie man OCR in Java durchführt – Text schnell aus einem Bild extrahieren,
  Bild in Text umwandeln und Text aus einer JPG lesen, mit einem einfachen Codebeispiel.
draft: false
keywords:
- how to perform OCR
- ocr in java
- extract text from image
- convert image to text
- read text from jpg
language: de
og_description: Wie man OCR in Java durchführt – lernen Sie, wie Sie Text aus einem
  Bild extrahieren, ein Bild in Text umwandeln und Text aus einer JPG lesen, mit einem
  sofort einsatzbereiten Beispiel.
og_title: Wie man OCR in Java durchführt – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  headline: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  type: TechArticle
- description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  name: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  steps:
  - name: What You’ll Learn
    text: '- Install an OCR library (yes, **ocr in java** is easier than you think).
      - Create and configure an OCR engine instance. - Load a JPG (or any image) and
      set the language. - Process the image and **extract text from image** files.
      - Print the recognized string to the console.'
  - name: Expected Output
    text: 'If `input.jpg` contains the Mongolian phrase “Сайн байна уу?” the console
      will show:'
  - name: 'Pro Tip: Batch Processing'
    text: 'If you need to **extract text from image** files in bulk, wrap the core
      logic in a loop:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Wie man OCR in Java durchführt – Vollständige Anleitung zum Extrahieren von
  Text aus Bildern
url: /de/java/ocr-basics/how-to-perform-ocr-in-java-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR in Java durchführen – Vollständige Anleitung zum Extrahieren von Text aus Bildern

Haben Sie sich jemals gefragt, **how to perform OCR** auf einem Bild, das Sie mit Ihrem Handy aufgenommen haben? Sie sind nicht allein. Egal, ob Sie eine Beleg‑Scann‑App bauen oder einfach Text aus einem gescannten PDF ziehen müssen, **how to perform OCR** in Java ist eine Fähigkeit, die sich schnell auszahlt. In diesem Tutorial gehen wir ein praktisches Beispiel durch, das **extract text from image**‑Dateien **converts image to text** und Ihnen sogar zeigt, wie Sie **read text from jpg** mit nur wenigen Codezeilen lesen können.

> *Pro Tipp:* Der gleiche Ansatz funktioniert für PNG, BMP oder jedes Format, das die OCR‑Engine unterstützt – einfach den Dateinamen austauschen.

## OCR in Java durchführen – Überblick

Optical Character Recognition (OCR) ist die Technologie, die Bilder von Buchstaben in echten, durchsuchbaren Text verwandelt. Im Java‑Ökosystem gibt es mehrere Bibliotheken – Tesseract, Asprise und kommerzielle SDKs – die alle einen ähnlichen Workflow bieten: Bild laden, der Engine die erwartete Sprache mitteilen, die Erkennung ausführen und das Ergebnis holen. Im Folgenden verwenden wir eine generische `OcrEngine`‑Klasse, um das Beispiel klar zu halten, aber Sie können sie durch jede konkrete Implementierung ersetzen, die dasselbe Muster folgt.

### Was Sie lernen werden

- Installieren Sie eine OCR‑Bibliothek (ja, **ocr in java** ist einfacher als Sie denken).
- Erstellen und konfigurieren Sie eine OCR‑Engine‑Instanz.
- Laden Sie ein JPG (oder ein beliebiges Bild) und setzen Sie die Sprache.
- Verarbeiten Sie das Bild und **extract text from image**‑Dateien.
- Geben Sie die erkannte Zeichenkette in der Konsole aus.

Am Ende haben Sie ein eigenständiges Java‑Programm, das Sie in jedes Projekt einbinden und sofort ausführen können.

![Beispiel für OCR durchführen](ocr-example.png "Illustration zum Durchführen von OCR in Java")

## Schritt 1 – Installieren und Importieren einer OCR‑Bibliothek (ocr in java)

Bevor Sie eine einzige Zeile Java schreiben, benötigen Sie eine Bibliothek, die die eigentliche schwere Arbeit übernimmt. Wenn Sie Maven verwenden, fügen Sie eine Abhängigkeit wie diese hinzu (ersetzen Sie `com.example.ocr` durch die echte Group‑ID Ihres gewählten SDKs):

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>ocr-sdk</artifactId>
    <version>1.4.2</version>
</dependency>
```

Wenn Sie Gradle bevorzugen:

```gradle
implementation 'com.example:ocr-sdk:1.4.2'
```

Sobald das JAR in Ihrem Klassenpfad ist, importieren Sie die Klassen, die Sie benötigen:

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;
```

> **Warum das wichtig ist:** Das Importieren der richtigen Klassen verhindert „cannot find symbol“-Fehler und macht Ihre IDE glücklich – nichts ist frustrierender als ein fehlender Import, wenn Sie versuchen, **convert image to text** zu erledigen.

## Schritt 2 – Erstellen der OCR‑Engine‑Instanz (how to perform OCR)

Jetzt, wo die Bibliothek bereit ist, starten Sie die Engine. Denken Sie an die Engine als das Gehirn, das die Pixel betrachtet und die Buchstaben errät.

```java
// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

Das Erzeugen der Engine ist in der Regel günstig; die meisten SDKs allokieren interne Puffer erst bei Bedarf, sodass Sie dieselbe Instanz sicher für viele Bilder wiederverwenden können, wenn Sie einen Stapel verarbeiten.

## Schritt 3 – Bild laden und Sprache setzen (extract text from image)

Der nächste Schritt besteht darin, der Engine etwas zum Lesen zu geben. Hier laden wir ein JPEG von der Festplatte und teilen der OCR‑Engine mit, dass der Text in Mongolisch (ISO 639‑2‑Code „mon“) vorliegt. Sie können den Pfad oder den Sprachcode an Ihren Anwendungsfall anpassen.

```java
// Step 3: Load the image you want to recognize
ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/input.jpg"));

// Step 3b: Specify the language (e.g., English = "eng", Mongolian = "mon")
ocrEngine.getSettings().setLanguage("mon");
```

> **Hinweis:** Wenn Sie keine Sprache setzen, verwendet die Engine standardmäßig Englisch, was die Genauigkeit drastisch senken kann, wenn der Text tatsächlich kyrillisch oder in einer anderen Schrift ist. Geben Sie immer die korrekte Sprache an, wenn Sie können.

## Schritt 4 – Bild verarbeiten und Ergebnis holen (convert image to text)

Mit Bild und Sprache im Hintergrund fordern Sie die Engine auf, ihre Magie zu wirken. Der Aufruf `process()` führt den OCR‑Algorithmus aus und liefert ein `OcrResult`‑Objekt, das die erkannte Zeichenkette und Konfidenzwerte enthält.

```java
// Step 4: Process the image and obtain the recognition result
OcrResult ocrResult = ocrEngine.process();
```

Im Hintergrund kann die Engine Vorverarbeitungsschritte durchführen – Entzerrung, Binarisierung, Rauschunterdrückung – sodass Sie diese Schritte nicht selbst schreiben müssen. Deshalb machen die meisten modernen OCR‑Bibliotheken Freude bei **convert image to text**‑Aufgaben.

## Schritt 5 – Extrahierten Text ausgeben (read text from jpg)

Zum Schluss holen Sie den Klartext aus dem Ergebnis und machen etwas Nützliches damit. Für diese Demo geben wir ihn einfach in der Konsole aus, aber Sie könnten ihn in eine Datei schreiben, in einen Suchindex einspeisen oder an einen anderen Service weitergeben.

```java
// Step 5: Output the extracted text
System.out.println(ocrResult.getText());
```

Diese Zeile beweist allein, dass Sie erfolgreich **read text from jpg** (oder ein beliebiges unterstütztes Format) gelesen haben. Wenn die Ausgabe wirr aussieht, prüfen Sie den Sprachcode und die Bildqualität erneut.

## Vollständiges funktionierendes Beispiel (Alle Schritte kombiniert)

Unten finden Sie eine komplette, sofort ausführbare Java‑Klasse, die alle Bausteine zusammenführt. Kopieren Sie sie in eine Datei namens `OcrDemo.java`, passen Sie den Bildpfad und die Sprache an und führen Sie `javac OcrDemo.java && java OcrDemo` aus.

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to perform OCR in Java using a generic OCR SDK.
 * This example loads a JPG, sets the language to Mongolian, and prints
 * the recognized text to the console.
 *
 * Replace the import package with the actual library you are using.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Validate command‑line arguments
        if (args.length < 2) {
            System.err.println("Usage: java OcrDemo <image-path> <language-code>");
            System.exit(1);
        }

        String imagePath = args[0];   // e.g., "input.jpg"
        String language = args[1];    // e.g., "mon" for Mongolian

        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image
        ocrEngine.setImage(new OcrInputImage(imagePath));

        // Step 3: Set the language (ISO‑639‑2)
        ocrEngine.getSettings().setLanguage(language);

        // Step 4: Run the recognition
        OcrResult result = ocrEngine.process();

        // Step 5: Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### Erwartete Ausgabe

Enthält `input.jpg` den mongolischen Satz „Сайн байна уу?“, zeigt die Konsole:

```
=== Recognized Text ===
Сайн байна уу?
```

Ist das Bild unscharf oder ist der Sprachcode falsch, sehen Sie verzerrte Zeichen oder einen leeren String – häufige Stolperfallen, die wir im Folgenden besprechen.

## Häufige Probleme und deren Behebung

| Symptom | Wahrscheinliche Ursache | Lösung |
|---------|--------------------------|--------|
| Verzerrte kyrillische Zeichen | Falscher Sprachcode (Standard ist Englisch) | Setzen Sie `ocrEngine.getSettings().setLanguage("mon")` oder den entsprechenden Code. |
| Keine Ausgabe | Bildpfad falsch oder Datei nicht lesbar | Überprüfen Sie den Pfad, stellen Sie sicher, dass die Datei existiert, und dass der Prozess Leseberechtigungen hat. |
| Niedrige Genauigkeit (<70 %) | Bild hat geringen Kontrast oder ist gedreht | Bild vorverarbeiten: Kontrast erhöhen, entzerren oder in Graustufen konvertieren, bevor Sie es an die Engine übergeben. |
| `OutOfMemoryError` bei großen PDFs | Viele hochauflösende Seiten gleichzeitig laden | Seiten einzeln verarbeiten oder Bilder vor dem OCR verkleinern. |

### Pro Tipp: Stapelverarbeitung

Wenn Sie **extract text from image**‑Dateien in großen Mengen benötigen, verpacken Sie die Kernlogik in einer Schleife:

```java
for (File img : new File("batchFolder").listFiles()) {
    ocrEngine.setImage(new OcrInputImage(img.getAbsolutePath()));
    OcrResult r = ocrEngine.process();
    System.out.println(r.getText());
}
```

Dieses Snippet zeigt, wie einfach es ist, von einem einzelnen JPG zu einem ganzen Ordner von Scans zu skalieren.

## Weiterführend – Was Sie als Nächstes erkunden können?

- **Sprachpakete:** Die meisten OCR‑SDKs erlauben das Herunterladen zusätzlicher Sprachdatendateien. Das Hinzufügen eines neuen Pakets ermöglicht Ihnen **convert image to text** für Sprachen jenseits von Englisch und Mongolisch.
- **PDF‑OCR:** Kombinieren Sie diesen Code mit Apache PDFBox, um

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält komplette, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Text aus Bildern extrahieren – OCR‑Grundlagen mit Aspose.OCR für Java](/ocr/english/java/ocr-basics/)
- [Bild in Text umwandeln in Java mit Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Wie man Bildtext mit Sprache OCR‑t – Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}