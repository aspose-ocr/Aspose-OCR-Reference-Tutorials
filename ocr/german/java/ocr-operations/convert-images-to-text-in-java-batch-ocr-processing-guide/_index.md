---
category: general
date: 2026-08-28
description: Erfahren Sie, wie Sie Text aus PNG-Bildern in Java mit Aspose OCR extrahieren.
  Dieses Tutorial behandelt die Batch-OCR-Verarbeitung, das Lesen von Bildern aus
  einem Ordner und das Filtern von Dateien nach Erweiterung.
draft: false
keywords:
- extract text from png
- read images from folder
- filter files by extension
- how to batch ocr
- aspose ocr java tutorial
lastmod: 2026-08-28
og_description: Erfahren Sie, wie Sie Text aus PNG-Bildern in Java mit Aspose OCR
  extrahieren. Dieses Tutorial behandelt die Batch-OCR-Verarbeitung, das Lesen von
  Bildern aus einem Ordner und das Filtern von Dateien nach Erweiterung.
og_image_alt: 'Developer guide: extract text from png images in Java using Aspose
  OCR'
og_title: Wie man Text aus PNG in Java extrahiert – Batch-OCR-Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Learn how to extract text from png images in Java using Aspose OCR.
    This tutorial covers batch OCR processing, reading images from a folder, and filtering
    files by extension.
  headline: How to extract text from png in Java – batch OCR guide
  type: TechArticle
- questions:
  - answer: Absolutely. Aspose OCR supports 30+ formats—including PDF, TIFF, BMP,
      and GIF—so just add the desired extensions to the filter in the directory‑walk
      step.
    question: Can I process PDFs or TIFFs as well?
  - answer: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`
      (or any supported language). The language packs are bundled with the library,
      so no extra download is required.
    question: What if I need a language other than English, such as Spanish?
  - answer: Yes. `Files.walk` traverses the entire tree recursively, so every nested
      PNG/J
    question: My folder contains sub‑folders—will they be scanned?
  - answer: Enable streaming mode by calling `ocrEngine.setUseStreaming(true)`. This
      tells the engine to read the image in chunks, dramatically reducing peak memory
      usage.
    question: How do I handle extremely large images that exceed 200 MB?
  - answer: Yes. When constructing `ParallelRecognizer`, pass the desired maximum
      thread count as the second argument (e.g., `new ParallelRecognizer(ocrEngine,
      4)`).
    question: Is there a way to limit the number of concurrent OCR threads?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Wie man Text aus PNG in Java extrahiert – Batch-OCR-Leitfaden
url: /de/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Text aus PNG in Java extrahiert – Batch-OCR-Leitfaden

Wenn Sie jemals **Text aus PNG**‑Dateien extrahieren mussten, aber nicht wussten, wie Sie den Vorgang über ein paar Bilder hinaus skalieren können, sind Sie hier genau richtig. Viele Entwickler beginnen mit einem einzelnen Bild‑OCR‑Aufruf und stoßen schnell an Leistungsgrenzen, sobald der Ordner auf Dutzende oder Hunderte von Dateien anwächst. Mit Aspose OCR für Java können Sie eine robuste Batch‑OCR‑Pipeline aufsetzen, die ein Verzeichnis durchläuft, nur die Bildtypen filtert, die Sie benötigen, die Erkennung parallel ausführt und die Ergebnisse in derselben Reihenfolge wie die Quelldateien zurückgibt. Am Ende dieses Leitfadens haben Sie ein sofort einsetzbares Java‑Snippet, das **Batch‑OCR‑Verarbeitung** zuverlässig und effizient handhabt.

![Beispiel für die Konvertierung von Bildern zu Text](https://example.com/convert-images-to-text.png "Screenshot der Java-Konsolenausgabe, die den konvertierten Text aus PNG-Dateien zeigt")

## Schnelle Antworten
- **Welche Bibliothek übernimmt OCR?** Aspose OCR for Java.
- **Kann ich PNG und JPG zusammen verarbeiten?** Ja – das Beispiel filtert beide Erweiterungen.
- **Ist die OCR-Engine thread‑sicher?** Eine einzelne gemeinsam genutzte `AsposeOCR`‑Instanz ist für gleichzeitige Verwendung sicher.
- **Benötige ich eine Lizenz für Tests?** Ein kostenloser temporärer Schlüssel ist von Aspose verfügbar.
- **Werden Unterordner automatisch gescannt?** `Files.walk` durchläuft den gesamten Baum rekursiv.

## Was bedeutet Text aus PNG extrahieren?

`extract text from png` bezieht sich auf den Vorgang, optische Zeichenerkennung (OCR) auf Portable‑Network‑Graphics‑Dateien anzuwenden, sodass die sichtbaren Zeichen zu durchsuchbaren, editierbaren Zeichenketten werden. Die Aspose‑OCR‑Engine liest Pixeldaten, identifiziert Glyphenformen und gibt Unicode‑Text in einem einzigen Methodenaufruf zurück.

## Warum Aspose OCR für Java verwenden?

Aspose OCR unterstützt **30+ Sprachen**, verarbeitet bis zu **500 Bilder pro Minute** auf einem Standard‑8‑Kern‑Server und kann Dateien bis zu **200 MB** handhaben, ohne das gesamte Bild in den Speicher zu laden. Diese quantifizierten Fähigkeiten bedeuten, dass Sie groß angelegte Batch‑Jobs zuverlässig auf handelsüblicher Hardware ausführen können, ohne Speichergrenzen zu erreichen.

## Voraussetzungen
- Java 17 (oder jede aktuelle LTS‑Version).
- Maven oder Gradle für die Abhängigkeitsverwaltung.
- Ein Verzeichnis, das PNG/JPG‑Bilder enthält, die Sie verarbeiten möchten.
- Grundlegende Kenntnisse von Java‑Streams und dem Paket `java.nio.file`.
- (Optional) Ein temporärer Aspose OCR‑Lizenzschlüssel für die Evaluierung.

> **Pro‑Tipp:** Der kostenlose temporäre Schlüssel läuft nach 30 Tagen ab, bietet Ihnen jedoch vollen API‑Zugriff für Tests.

## Wie behält die Batch‑OCR‑Pipeline die Reihenfolge bei?

`Future<OcrResult>` repräsentiert ein ausstehendes OCR‑Ergebnis, das abgerufen werden kann, sobald die Verarbeitung abgeschlossen ist. Die Pipeline bewahrt die ursprüngliche Dateireihenfolge, indem sie die `Future<OcrResult>`‑Objekte in einer Liste speichert, die die Reihenfolge der Eingabe‑`Path`‑Sammlung spiegelt. Wenn Sie später über die Futures iterieren und `get()` aufrufen, blockiert jeder Aufruf nur für das zugehörige Bild, sodass die Ausgabereihenfolge der Eingabereihenfolge entspricht, ohne zusätzliche Sortierlogik.

## Was ist Aspose OCR für Java?

`AsposeOCR` ist die Kernklasse der Aspose‑OCR‑Bibliothek, die alle Sprachpakete, Erkennungseinstellungen und internen nativen Ressourcen kapselt. Sie ist dafür ausgelegt, einmal pro Anwendungslebensdauer instanziiert und sicher über mehrere Threads hinweg geteilt zu werden. Da sie Sprachdaten nur einmal lädt, reduziert die Wiederverwendung derselben Instanz den Initialisierungsaufwand und verbessert den Durchsatz für Batch‑Operationen.

## Wie man das Projekt einrichtet und Aspose OCR hinzufügt

Zuerst erstellen Sie ein Maven‑ (oder Gradle‑)Projekt und fügen die Aspose‑OCR‑Abhängigkeit zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

> **Warum das wichtig ist:** Durch die Vorab‑Deklaration der Abhängigkeit kann der Compiler `AsposeOCR`, `ParallelRecognizer` und verwandte Klassen sehen. Außerdem wird sichergestellt, dass dieselbe Version auf allen Maschinen verwendet wird, was für reproduzierbare **Batch‑OCR‑Verarbeitung** entscheidend ist.

Aktualisieren Sie Ihre IDE nach Abschluss des Builds; Sie sollten nun die Aspose‑Pakete unter **External Libraries** sehen.

## Wie man die OCR‑Engine initialisiert – eine einzelne Instanz teilen

`AsposeOCR` ist die Haupt‑OCR‑Engine‑Klasse, die von der Aspose‑OCR‑Bibliothek bereitgestellt wird. Wir benötigen nur **eine** OCR‑Engine‑Instanz für den gesamten Durchlauf. Das Teilen über Threads spart Speicher und beschleunigt die Verarbeitung, weil die Engine Sprachpakete nur einmal lädt.

```java
AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");
```

`AsposeOCR` ist thread‑sicher, sodass Sie sie sicher an einen `ParallelRecognizer` übergeben können, der einen Pool von Worker‑Threads verwaltet.

> **Erklärung:** `ParallelRecognizer` kapselt die Engine in einem Thread‑Pool. Wenn Sie viele Dateien einreichen, erhält jede ihren eigenen Worker‑Thread, was echtes Parallelisieren auf Mehrkern‑CPUs ermöglicht.

## Wie man Bilder aus einem Ordner liest – Verzeichnisbaum durchlaufen

`Files.walk` ist eine Java‑NIO‑Methode, die rekursiv einen Dateibaum durchläuft und einen Stream von `Path`‑Objekten zurückgibt. Jetzt müssen wir **Bilder aus dem Ordner lesen** und jedes PNG oder JPG sammeln. Die `Files.walk`‑API macht das zu einem Einzeiler, aber wir fügen einen Filter hinzu, um **Text aus PNG** nur bei Bedarf zu extrahieren.

```java
List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
    .filter(Files::isRegularFile)
    .filter(p -> {
        String lower = p.toString().toLowerCase();
        return lower.endsWith(".png") || lower.endsWith(".jpg");
    })
    .collect(Collectors.toList());
```

> **Warum wir hier filtern:** Durch `filter` können wir **Dateien nach Erweiterung** frühzeitig herausfiltern, was unnötige I/O später reduziert. Außerdem bleibt der Code lesbar – keine komplexen Regexes nötig.

## Wie man OCR‑Jobs asynchron einreicht

`recognizeAsync` übergibt ein Bild an die OCR‑Engine zur asynchronen Verarbeitung und gibt ein `Future<OcrResult>` zurück, das das ausstehende Ergebnis repräsentiert. Mit der fertigen Dateiliste schieben wir jeden Pfad zum `ParallelRecognizer`. Die Methode `recognizeAsync` liefert ein `Future<OcrResult>`, das wir für die spätere Abfrage speichern.

```java
ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine, Runtime.getRuntime().availableProcessors());
List<Future<OcrResult>> futures = new ArrayList<>();

for (Path imagePath : imagePaths) {
    futures.add(recognizer.recognizeAsync(imagePath));
}
```

> **Was im Hintergrund passiert:** Jeder Aufruf enqueued eine Aufgabe in den internen Executor‑Service des Recognizers. Die Aufgaben laufen parallel, sodass ein Ordner mit 100 Bildern in einem Bruchteil der Zeit verarbeitet wird, die eine ein‑Thread‑Schleife benötigen würde.

## Wie man Ergebnisse abruft und dabei die Dateireihenfolge beibehält

`Future<OcrResult>` enthält das Ergebnis einer asynchronen OCR‑Aufgabe und bietet eine `get()`‑Methode, um den erkannten Text zu erhalten. Da wir die Futures in derselben Reihenfolge wie `imagePaths` gespeichert haben, können wir einfach über die Liste iterieren und `get()` aufrufen. Der Aufruf blockiert nur, bis das jeweilige Bild fertig ist, wodurch die Reihenfolge ohne zusätzlichen Aufwand erhalten bleibt.

```java
for (int i = 0; i < futures.size(); i++) {
    try {
        OcrResult result = futures.get(i).get();
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println("Text: " + result.getText());
    } catch (Exception e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**Beispielhafte Konsolenausgabe** (gekürzt für Übersicht):

```
File: invoice1.png
Text: Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...
```

> **Umgang mit Randfällen:** Wenn ein bestimmtes Bild eine Ausnahme wirft (beschädigte Datei, nicht unterstütztes Format), fangen wir sie ab und verarbeiten den Rest weiter – ein essentielles Vorgehen für zuverlässige **Batch‑OCR‑Verarbeitung**‑Pipelines.

## Wie man Ressourcen bereinigt – den Recognizer herunterfährt

`ParallelRecognizer.shutdown()` stoppt den internen Thread‑Pool und stellt sicher, dass alle OCR‑Aufgaben abgeschlossen sind, bevor die Anwendung beendet wird. Vergessen Sie nie, den internen Thread‑Pool herunterzufahren; sonst kann Ihre JVM beim Beenden hängen bleiben.

```java
recognizer.shutdown();
```

Das war's! Das Programm durchläuft nun jedes Verzeichnis, filtert PNG/JPG‑Dateien, führt OCR parallel aus und gibt die Ergebnisse in der ursprünglichen Reihenfolge aus.

---

## Vollständiges funktionierendes Beispiel (Copy‑and‑Paste)

Unten finden Sie die komplette, sofort ausführbare Java‑Klasse. Ersetzen Sie `"YOUR_DIRECTORY"` durch den Pfad zu Ihrem Bildordner und führen Sie sie in Ihrer IDE oder über die Befehlszeile aus.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

public class BatchOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine (single shared instance)
        AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");

        // Create a parallel recognizer that uses a thread pool
        ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine,
                Runtime.getRuntime().availableProcessors());

        // Walk the directory and collect PNG/JPG files
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(Files::isRegularFile)
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        // Submit OCR jobs asynchronously
        List<Future<OcrResult>> futures = new ArrayList<>();
        for (Path imagePath : imagePaths) {
            futures.add(recognizer.recognizeAsync(imagePath));
        }

        // Retrieve results in the original order
        for (int i = 0; i < futures.size(); i++) {
            try {
                OcrResult result = futures.get(i).get();
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println("Text: " + result.getText());
            } catch (Exception e) {
                System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Clean up the recognizer's thread pool
        recognizer.shutdown();
    }
}
```

Führen Sie die Klasse aus, beobachten Sie, wie die Konsole mit extrahierten Zeichenketten gefüllt wird, und freuen Sie sich darüber, dass Sie gerade **Bilder in Text konvertiert** haben, ohne eine einzige Schleife zu schreiben, die bei I/O blockiert.

---

## Häufig gestellte Fragen (FAQs)

**F: Kann ich auch PDFs oder TIFFs verarbeiten?**  
A: Absolut. Aspose OCR unterstützt 30+ Formate – darunter PDF, TIFF, BMP und GIF – sodass Sie einfach die gewünschten Erweiterungen zum Filter im Verzeichnis‑Walk‑Schritt hinzufügen können.

**F: Was, wenn ich eine andere Sprache als Englisch benötige, z. B. Spanisch?**  
A: Ändern Sie `RecognitionLanguage.ENGLISH` zu `RecognitionLanguage.SPANISH` (oder einer anderen unterstützten Sprache). Die Sprachpakete sind mit der Bibliothek gebündelt, ein zusätzlicher Download ist nicht nötig.

**F: Mein Ordner enthält Unterordner – werden diese gescannt?**  
A: Ja. `Files.walk` durchläuft den gesamten Baum rekursiv, sodass jede verschachtelte PNG/J

**F: Wie gehe ich mit extrem großen Bildern um, die 200 MB überschreiten?**  
A: Aktivieren Sie den Streaming‑Modus, indem Sie `ocrEngine.setUseStreaming(true)` aufrufen. Dadurch liest die Engine das Bild in Teilen, was den Spitzen‑Speicherverbrauch drastisch reduziert.

**F: Gibt es eine Möglichkeit, die Anzahl gleichzeitiger OCR‑Threads zu begrenzen?**  
A: Ja. Beim Erzeugen von `ParallelRecognizer` übergeben Sie die gewünschte maximale Thread‑Anzahl als zweiten Parameter (z. B. `new ParallelRecognizer(ocrEngine, 4)`).

---

**Zuletzt aktualisiert:** 2026-08-28  
**Getestet mit:** Aspose OCR für Java 24.10  
**Autor:** Aspose  






```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```

```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```

```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```

```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

## Verwandte Tutorials

- [Bilder in Text konvertieren in Java Batch-OCR-Verarbeitungsleitfaden](/ocr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/)
- [Text aus Bild in Java lesen – vollständiger Aspose-OCR-Leitfaden](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Text aus Bildern extrahieren mit Aspose.OCR – erlaubte Zeichen](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}