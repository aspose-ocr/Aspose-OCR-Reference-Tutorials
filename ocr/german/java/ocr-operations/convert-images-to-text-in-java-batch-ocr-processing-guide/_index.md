---
category: general
date: 2026-01-02
description: Bilder mit Java und Aspose OCR in Text umwandeln. Batch‑OCR‑Verarbeitung
  meistern, Bilder aus einem Ordner lesen und Dateien nach Erweiterung filtern.
draft: false
keywords:
- convert images to text
- batch ocr processing
- read images from folder
- extract text from png
- filter files by extension
language: de
og_description: Bilder schnell mit Java in Text umwandeln. Dieses Tutorial behandelt
  die Stapel‑OCR‑Verarbeitung, das Einlesen von Bildern aus einem Ordner und das Filtern
  von Dateien nach Erweiterung.
og_title: Bilder in Text konvertieren in Java – Vollständiger Batch-OCR-Leitfaden
tags:
- OCR
- Java
- Aspose
title: Bilder in Text konvertieren in Java – Leitfaden zur Batch-OCR-Verarbeitung
url: /de/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bilder in Text konvertieren in Java – Batch‑OCR‑Verarbeitungs‑Leitfaden

Haben Sie schon einmal **Bilder in Text umwandeln** müssen, wussten aber nicht, wie Sie Dutzende von Dateien gleichzeitig verarbeiten? Sie sind nicht allein – Entwickler kämpfen ständig damit, Daten aus PNGs, JPGs und anderen Scans zu extrahieren. Die gute Nachricht? Mit Aspose OCR können Sie in wenigen Minuten eine Batch‑OCR‑Verarbeitungspipeline aufsetzen, Bilder aus Ordnerstrukturen lesen und sogar Dateien nach Erweiterung filtern, sodass Sie nur das bearbeiten, was wirklich wichtig ist.

In diesem Tutorial bauen wir ein eigenständiges Java‑Programm, das ein Verzeichnis durchläuft, jedes `.png` oder `.jpg` herauspickt, jedes Bild asynchron an Aspose OCR sendet und den extrahierten Text in der ursprünglichen Reihenfolge ausgibt. Am Ende haben Sie ein wiederverwendbares Snippet, das Sie in jedes Projekt einbinden können, das **Bilder in Text** in großem Umfang konvertieren muss.

---

![Convert images to text example](https://example.com/convert-images-to-text.png "Screenshot der Java‑Konsolenausgabe, die konvertierten Text aus PNG‑Dateien zeigt")

## Was Sie bauen werden

- Eine einzelne `AsposeOCR`‑Engine, die über Threads hinweg geteilt wird (effizient und thread‑sicher).  
- Ein `ParallelRecognizer`, der OCR‑Jobs parallel ausführt – perfekt für **Batch‑OCR‑Verarbeitung**.  
- Logik, die **Bilder aus Ordnern liest** mittels `java.nio.file.Files`.  
- Einfache Filter, um **Text aus PNG**‑Dateien zu extrahieren, während JPGs ebenfalls unterstützt werden.  
- Sauberes Herunterfahren des internen Thread‑Pools, um Ressourcen‑Lecks zu vermeiden.

### Voraussetzungen

- Java 17 (oder jede aktuelle LTS‑Version).  
- Maven oder Gradle, um die Aspose‑OCR‑Bibliothek zu beziehen.  
- Ein Ordner voller PNG/JPG‑Bilder, die Sie verarbeiten möchten.  
- Grundlegende Kenntnisse von Java‑Streams – nichts Besonderes erforderlich.

> **Pro‑Tipp:** Wenn Sie noch keine Lizenz haben, bietet Aspose einen kostenlosen temporären Schlüssel für Testzwecke an.

---

## Schritt 1 – Projekt einrichten und Aspose OCR hinzufügen

Erstellen Sie zunächst ein neues Maven‑Projekt (oder Gradle, wie Sie möchten). Fügen Sie die Aspose‑OCR‑Abhängigkeit zu `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **Warum das wichtig ist:** Die Deklaration der Abhängigkeit zu Beginn stellt sicher, dass der Compiler `AsposeOCR`, `ParallelRecognizer` und verwandte Klassen erkennt. Außerdem wird garantiert, dass dieselbe Version auf allen Maschinen verwendet wird – entscheidend für reproduzierbare **Batch‑OCR‑Verarbeitung**.

Nachdem der Build abgeschlossen ist, aktualisieren Sie Ihre IDE und Sie sollten die Aspose‑Pakete unter `External Libraries` sehen.

---

## Schritt 2 – Bilder in Text konvertieren – OCR‑Engine initialisieren

Wir benötigen nur **eine** OCR‑Engine‑Instanz für den gesamten Durchlauf. Das Teilen über Threads hinweg spart Speicher und beschleunigt die Verarbeitung, weil die Engine Sprachpakete nur einmal lädt.

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

> **Erklärung:** `ParallelRecognizer` kapselt die Engine in einen Thread‑Pool. Wenn Sie viele Dateien einreichen, erhält jede ihren eigenen Worker‑Thread, was echtes Parallelisieren auf Mehrkern‑CPUs ermöglicht.

---

## Schritt 3 – Bilder aus Ordner lesen – Verzeichnisbaum durchlaufen

Jetzt müssen wir **Bilder aus Ordnern lesen** und jedes PNG oder JPG sammeln. Die API `Files.walk` macht das zu einem Einzeiler, aber wir fügen einen Filter hinzu, um **Text aus PNG**‑Dateien nur bei Bedarf zu extrahieren.

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

> **Warum wir hier filtern:** Durch `filter` können wir **Dateien nach Erweiterung filtern** bereits frühzeitig, was später unnötige I/O‑Operationen reduziert. Außerdem bleibt der Code lesbar – keine komplexen Regexes nötig.

---

## Schritt 4 – Batch‑OCR‑Verarbeitung – Jobs asynchron einreichen

Mit der fertigen Dateiliste übergeben wir jeden Pfad an den `ParallelRecognizer`. Die Methode `recognizeAsync` liefert ein `Future<OcrResult>`, das wir für die spätere Abfrage speichern.

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

> **Was im Hintergrund passiert:** Jeder Aufruf legt eine Aufgabe in den internen Executor‑Service des Recognizers. Die Aufgaben laufen parallel, sodass ein Ordner mit 100 Bildern in einem Bruchteil der Zeit verarbeitet wird, die eine einstufige Schleife benötigen würde.

---

## Schritt 5 – Ergebnisse in ursprünglicher Reihenfolge abrufen – Dateisequenz erhalten

Da wir die Futures in derselben Reihenfolge wie `imagePaths` gespeichert haben, können wir einfach über die Liste iterieren und `get()` aufrufen. Der Aufruf blockiert nur, bis das jeweilige Bild fertig ist, wodurch die Reihenfolge ohne zusätzlichen Aufwand erhalten bleibt.

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

**Beispielhafte Konsolenausgabe** (gekürzt):

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

> **Umgang mit Sonderfällen:** Wenn ein bestimmtes Bild eine Ausnahme wirft (beschädigte Datei, nicht unterstütztes Format), fangen wir sie ab und verarbeiten den Rest weiter – ein essentielles Vorgehen für zuverlässige **Batch‑OCR‑Verarbeitung**‑Pipelines.

---

## Schritt 6 – Aufräumen – Recognizer herunterfahren

Vergessen Sie nie, den internen Thread‑Pool zu schließen; sonst kann Ihre JVM beim Beenden hängen bleiben.

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

Damit ist alles erledigt! Das Programm durchläuft nun jedes Verzeichnis, filtert PNG/JPG‑Dateien, führt OCR parallel aus und gibt die Ergebnisse aus.

---

## Vollständiges funktionierendes Beispiel

Unten finden Sie die komplette, copy‑and‑paste‑bereite Java‑Klasse. Ersetzen Sie `"YOUR_DIRECTORY"` durch den Pfad zu Ihrem Bildordner und führen Sie sie in Ihrer IDE oder über die Kommandozeile aus.

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

Starten Sie die Klasse, beobachten Sie, wie die Konsole mit extrahierten Zeichenketten gefüllt wird, und freuen Sie sich darüber, dass Sie gerade **Bilder in Text** konvertiert haben, ohne eine einzige blockierende I/O‑Schleife zu schreiben.

---

## Häufig gestellte Fragen (FAQs)

**F: Kann ich auch PDFs oder TIFFs verarbeiten?**  
A: Absolut. Aspose OCR unterstützt viele Formate – fügen Sie einfach die entsprechenden Dateierweiterungen zum Filter in Schritt 2 hinzu.

**F: Was, wenn ich eine andere Sprache, z. B. Spanisch, benötige?**  
A: Ändern Sie `RecognitionLanguage.ENGLISH` zu `RecognitionLanguage.SPANISH`. Stellen Sie sicher, dass das Sprachpaket installiert ist (Aspose liefert die meisten gängigen Sprachen out‑of‑the‑box).

**F: Mein Ordner enthält Unterordner – werden diese gescannt?**  
A: Ja. `Files.walk` traversiert den gesamten Baum rekursiv, sodass jedes verschachtelte PNG/J

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}