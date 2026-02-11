---
category: general
date: 2026-01-07
description: Holen Sie OCR-Text aus einem Bild mit Aspose OCR Java. Erfahren Sie,
  wie Sie Text aus einem Bild extrahieren, ein Bild für OCR laden und in wenigen Minuten
  ein Java-OCR-Beispiel ausführen.
draft: false
keywords:
- get OCR text
- extract text image
- java OCR example
- aspose OCR Java
- load image OCR
language: de
og_description: Holen Sie OCR‑Text aus Bildern mit Aspose OCR Java. Dieser Leitfaden
  zeigt ein Java‑OCR‑Beispiel, wie man Text aus einem Bild extrahiert und wie man
  OCR für Bilder effizient verwendet.
og_title: OCR‑Text in Java erhalten – Vollständiges Aspose OCR‑Tutorial
tags:
- OCR
- Java
- Aspose
- Image Processing
title: OCR-Text in Java erhalten – Komplettes Aspose OCR‑Beispiel
url: /de/java/ocr-basics/get-ocr-text-in-java-complete-aspose-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR-Text in Java erhalten – Komplettes Aspose OCR Beispiel

Haben Sie jemals **OCR-Text** aus einem gescannten Dokument erhalten müssen, waren sich aber nicht sicher, welche Bibliothek Sie wählen sollen? Sie sind nicht allein. In vielen realen Projekten – denken Sie an Rechnungsautomatisierung, Belegverarbeitung oder mehrsprachige Formulardigitalisierung – ist das Extrahieren von Text aus Bildern der erste Schritt zur Automatisierung.  

In diesem Tutorial gehen wir ein **java OCR example** durch, das die Aspose OCR for Java Bibliothek verwendet. Am Ende wissen Sie, wie Sie **load image OCR** ausführen, die Engine starten und **extract text image** Daten mit nur wenigen Codezeilen erhalten. Kein Schnickschnack, nur eine praktische Lösung, die Sie in Ihr eigenes Projekt kopieren‑einfügen können.

## Was Sie lernen werden

- Wie man Aspose OCR für Java einrichtet (einschließlich Maven‑Koordinaten).  
- Die genauen Schritte zum **load image OCR** und zum Festlegen einer Sprache.  
- Wie man **get OCR text** als einfachen String erhält und in der Konsole ausgibt.  
- Tipps zum Umgang mit mehrsprachigen Bildern und zur automatischen Spracherkennung.  

*Voraussetzungen*: Java 8 oder neuer, eine Maven‑kompatible IDE (IntelliJ IDEA, Eclipse oder VS Code) und eine gültige Aspose OCR for Java Lizenz (die kostenlose Testversion funktioniert für die Evaluierung).

---

![Flussdiagramm, das zeigt, wie man OCR-Text aus einem Bild mit Aspose OCR Java erhält](https://example.com/ocr-flowchart.png "OCR-Text Flussdiagramm")

## Schritt 1 – Aspose OCR‑Abhängigkeit hinzufügen (Load Image OCR)

Zuerst teilen Sie Maven mit, die Aspose OCR‑Bibliothek zu holen. Öffnen Sie Ihre `pom.xml` und fügen Sie den folgenden `<dependency>`‑Block innerhalb von `<dependencies>` ein:

```xml
<!-- Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version available -->
</dependency>
```

> **Pro‑Tipp**: Wenn Sie Gradle verwenden, lautet das Äquivalent `implementation 'com.aspose:aspose-ocr:23.9'`. Das Hinzufügen der Abhängigkeit ist der günstigste Weg, **load image OCR**‑Funktionen in Ihr Projekt zu integrieren.

## Schritt 2 – OCR‑Engine erstellen und Ihr Bild laden

Jetzt schreiben wir eine kleine Java‑Klasse, die eine `OcrEngine`‑Instanz erstellt, sie auf eine Bilddatei zeigt und der Engine mitteilt, welche Sprache erkannt werden soll. Die Sprache wird durch ihren ISO‑639‑2‑Code identifiziert (z. B. `"tam"` für Tamil).

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {

    public static void main(String[] args) throws Exception {
        // 2️⃣ Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Load the image you want to process – this is the "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // 2️⃣ Choose the language (ISO‑639‑2). Change "tam" to any supported code.
        engine.getEngineOptions().setLanguage("tam");
        // If you prefer automatic detection, uncomment the next line:
        // engine.getEngineOptions().setAutoDetectLanguage(true);
```

### Warum die Sprache explizit festlegen?

Die Angabe der Sprache reduziert Fehlalarme und beschleunigt die Erkennung. Für mehrsprachige PDFs können Sie über ein Array von Sprachcodes iterieren oder zur Bequemlichkeit die automatische Erkennung aktivieren.

## Schritt 3 – OCR‑Prozess ausführen und **Get OCR Text**

Mit der konfigurierten Engine führt die nächste Zeile tatsächlich die Erkennung aus. Das Ergebnisobjekt enthält den extrahierten String und zusätzliche Metadaten.

```java
        // 3️⃣ Perform OCR – this is where we finally **get OCR text**
        OcrResult result = engine.recognize();

        // 3️⃣ Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

Wenn Sie `LanguageExample` ausführen, sollten Sie etwa Folgendes sehen:

```
=== Extracted Text ===
தமிழ் உரை இங்கு வருகிறது...
```

Wenn Sie `setAutoDetectLanguage(true)` verwendet haben, versucht die Engine, die Sprache für Sie zu erraten, was praktisch ist, wenn Sie mit unbekannten Dokumenten arbeiten.

## Schritt 4 – Umgang mit gängigen Randfällen (Extract Text Image Variations)

### Umgang mit niedrig aufgelösten Bildern

Die OCR‑Genauigkeit sinkt stark unter 300 dpi. Wenn Ihr Quellbild eine niedrige Auflösung hat, sollten Sie es zuerst hochskalieren:

```java
engine.getEngineOptions().setResolution(300); // forces 300 DPI
```

### Hintergrundrauschen entfernen

Manchmal enthalten gescannte Formulare Punkte, die die Engine verwirren. Sie können die Vorverarbeitung aktivieren:

```java
engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);
```

### Text aus bestimmten Bereichen extrahieren

Wenn Sie nur Text aus einem bestimmten Rechteck benötigen (z. B. einer Tabellenzelle), setzen Sie ein `Rectangle`, bevor Sie `recognize()` aufrufen:

```java
engine.setRegion(new Rectangle(50, 100, 400, 200));
```

Diese Anpassungen machen Ihr **java OCR example** robust genug für Produktionslasten.

## Schritt 5 – Ausgabe überprüfen (Was sollten Sie erwarten?)

Ein erfolgreicher Durchlauf gibt die reine Textversion des Bildes aus. Bei mehrsprachigen Bildern können Sie gemischte Schriften sehen:

```
Hello World
こんにちは世界
مرحبا بالعالم
```

Wenn die Ausgabe leer oder unleserlich ist, überprüfen Sie Folgendes:

1. Den Dateipfad in `setImage` (ist er korrekt?).  
2. Der Sprachcode stimmt mit der Schrift im Bild überein.  
3. Die Bildqualität (Kontrast, DPI) ist ausreichend.

## Vollständiges funktionierendes Beispiel (Kopier‑Einfügen bereit)

Unten finden Sie die gesamte Datei, bereit zum Kompilieren und Ausführen. Ersetzen Sie `YOUR_DIRECTORY/multilingual.png` durch den tatsächlichen Pfad zu Ihrem Testbild.

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {
    public static void main(String[] args) throws Exception {
        // Initialize OCR engine
        OcrEngine engine = new OcrEngine();

        // Load the image – this is the core "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // Set language (ISO‑639‑2). For Tamil use "tam". Change as needed.
        engine.getEngineOptions().setLanguage("tam");
        // Uncomment for auto‑detect:
        // engine.getEngineOptions().setAutoDetectLanguage(true);

        // Optional: improve accuracy on low‑res images
        // engine.getEngineOptions().setResolution(300);
        // engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);

        // Perform OCR and retrieve text
        OcrResult result = engine.recognize();

        // Print the extracted text – this is how we **get OCR text**
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

Kompilieren und ausführen:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.LanguageExample"
```

Sie sollten nun den extrahierten Inhalt in Ihrer Konsole sehen.

---

## Fazit

Wir haben Ihnen gerade **wie man OCR-Text** aus einem Bild mit Aspose OCR für Java erhält, gezeigt. Durch das Befolgen dieses **java OCR example** können Sie **extract text image**‑Daten **load image OCR** extrahieren und sogar die Engine für mehrsprachige oder verrauschte Eingaben anpassen.  

Von hier aus könnten Sie:

- Den OCR‑Schritt in einen größeren Workflow integrieren (z. B. den Text in einer Datenbank speichern).  
- Mit einer Übersetzungs‑API kombinieren, um mehrsprachige Scans in eine einzige Sprache zu überführen.  
- Mit anderen Aspose OCR‑Funktionen experimentieren, wie PDF‑Konvertierung oder Barcode‑Erkennung.  

Probieren Sie es aus, brechen Sie ein paar Dinge und verfeinern Sie dann die Einstellungen, bis die Ausgabe perfekt ist. Viel Spaß beim Programmieren, und möge Ihr OCR stets kristallklar sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}