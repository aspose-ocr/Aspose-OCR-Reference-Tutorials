---
category: general
date: 2026-02-17
description: Erfahren Sie, wie Sie einen festen Thread‑Pool in Java verwenden, um
  Text aus PNG‑Bildern mit paralleler OCR‑Verarbeitung zu extrahieren und den Executor‑Service
  ordnungsgemäß herunterzufahren.
draft: false
keywords:
- fixed thread pool java
- extract text from png
- parallel ocr processing
- convert scanned pages text
- shut down executor service
language: de
og_description: Entdecken Sie, wie ein fester Thread‑Pool in Java Text aus PNG‑Bildern
  parallel extrahieren, gescannte Seiten konvertieren und den Executor‑Service sicher
  herunterfahren kann.
og_title: Fester Thread‑Pool Java – parallele OCR für PNG
tags:
- java
- ocr
- multithreading
- aspose
title: Fester Thread‑Pool Java – parallele OCR für PNG
url: /de/java/advanced-ocr-techniques/fixed-thread-pool-java-parallel-ocr-for-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Fixed Thread Pool Java – parallele OCR für PNG

Haben Sie sich jemals gefragt, wie man OCR bei einer Menge von PNG‑Dateien mit einem **fixed thread pool java** beschleunigen kann? In diesem Tutorial führen wir Sie durch das **extract text from PNG** von Bildern parallel, **convert scanned pages text** in editierbare Zeichenketten und schließen sicher den **shut down executor service**, sobald die Arbeit erledigt ist.

Wenn Sie schon einmal auf eine ein‑Thread‑Schleife gestoßen sind, die sich über Minuten hinzieht, kennen Sie die Frustration, jede Seite abzuwarten, bevor die nächste überhaupt startet. Die gute Nachricht? Mit ein paar Zeilen Java und Aspose OCR können Sie die Leistung aller CPU‑Kerne nutzen, gescannte Seiten in durchsuchbaren Text verwandeln und Ihre Anwendung reaktionsfähig halten.  

Unten finden Sie ein komplettes, sofort ausführbares Beispiel sowie Erklärungen, warum jedes Teil wichtig ist, häufige Stolperfallen und Tipps, die Sie auf jede OCR‑Bibliothek anwenden können.

---

## Was Sie benötigen

- **Java 17** (oder ein aktuelles JDK) – der Code verwendet die moderne `var`‑Syntax sparsam, funktioniert aber auch mit älteren Versionen.  
- **Aspose.OCR for Java** Bibliothek – Sie können sie von Maven Central beziehen oder eine Testversion von Aspose herunterladen.  
- Ein Satz **PNG**‑Dateien, die Sie verarbeiten möchten – denken Sie an gescannte Quittungen, Buchseiten oder Screenshots.  
- Grundlegende Kenntnisse der Java‑Parallelität – nicht zwingend erforderlich, aber hilfreich.

Das ist alles. Keine externen Dienste, kein Docker, nur reines Java und ein wenig Multithreading‑Magie.

---

## Schritt 1: Aspose OCR‑Abhängigkeit & Lizenz hinzufügen (optional)

Stellen Sie zunächst sicher, dass das Aspose OCR‑JAR in Ihrem Klassenpfad liegt. Wenn Sie Maven verwenden, fügen Sie hinzu:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

Falls Sie keine Lizenz besitzen, läuft die Bibliothek im Evaluierungsmodus; der Code funktioniert genauso. Um eine Lizenz zu laden (empfohlen für die Produktion), legen Sie `Aspose.OCR.lic` in Ihren Ressourcen‑Ordner und verwenden Sie:

```java
// Load the Aspose OCR license (optional)
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

> **Pro‑Tipp:** Halten Sie die Lizenzdatei außerhalb der Versionskontrolle, um eine versehentliche Veröffentlichung zu vermeiden.

---

## Schritt 2: Eine thread‑sichere `OcrEngine`‑Instanz erstellen

Aspose OCRs `OcrEngine` ist thread‑sicher, solange Sie dieselbe Instanz über mehrere Aufgaben hinweg wiederverwenden. Das einmalige Erzeugen spart Speicher und vermeidet den Overhead, die Engine für jedes Bild neu zu initialisieren.

```java
// One shared OcrEngine for all threads
OcrEngine ocrEngine = new OcrEngine();
```

Warum wiederverwenden? Stellen Sie sich die Engine als schwergewichtigen Arbeiter vor, der Sprachmodelle in den Speicher lädt. Für jedes Bild eine neue Engine zu starten, wäre wie für jede kleine Aufgabe einen neuen Spezialisten einzustellen – kostenintensiv und unnötig.

---

## Schritt 3: Einen Fixed Thread Pool Java einrichten

Jetzt kommt der Star der Show: ein **fixed thread pool java**. Wir dimensionieren ihn nach der Anzahl logischer Prozessoren, sodass jeder Kern Arbeit bekommt, ohne zu überlasten.

```java
// Determine available processors and create a fixed pool
int threadCount = Runtime.getRuntime().availableProcessors();
ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);
```

Die Verwendung eines *fixed*‑Pools (statt eines cached) liefert vorhersehbaren Ressourcenverbrauch und verhindert die gefürchteten „Out‑of‑Memory“-Spitzen, wenn Hunderte von Bildern gleichzeitig ankommen.

---

## Schritt 4: Die PNG‑Dateien auflisten, die Sie verarbeiten möchten (Extract Text from PNG)

Sammeln Sie die Pfade zu den Bildern, die Sie OCR‑verarbeiten wollen. In einem echten Projekt würden Sie wahrscheinlich ein Verzeichnis scannen oder aus einer Datenbank lesen; hier kodieren wir ein paar Beispiele fest ein.

```java
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png"
);
```

> **Hinweis:** Die Dateierweiterung **png** ist wichtig, weil Aspose OCR das Format automatisch erkennt, aber Sie könnten auch JPEG oder TIFF verwenden.

---

## Schritt 5: OCR‑Aufgaben einreichen – Parallel OCR Processing

Jedes Bild wird zu einem Callable, das den erkannten Text zurückgibt. Da die `OcrEngine` geteilt wird, müssen wir nur den Dateipfad an die Aufgabe übergeben.

```java
List<Future<String>> ocrFutures = new ArrayList<>();

for (String imagePath : imageFiles) {
    ocrFutures.add(threadPool.submit(() -> {
        // Prepare input for this image
        OcrInput input = new OcrInput();
        input.add(imagePath);

        // Perform OCR using the shared engine
        OcrResult result = ocrEngine.recognize(input);

        // Return the plain text
        return result.getText();
    }));
}
```

Warum in ein `Future` verpacken? Es ermöglicht, alle Jobs sofort zu starten und später die Ergebnisse in der Reihenfolge zu sammeln, in der sie eingereicht wurden – perfekt, um die Seitenreihenfolge beim **convert scanned pages text** zurück in ein Dokument zu bewahren.

---

## Schritt 6: Ergebnisse abrufen und anzeigen (Convert Scanned Pages Text)

Jetzt warten wir auf jedes `Future`, bis es fertig ist, und geben die Ausgabe aus. Der Aufruf `get()` blockiert nur, bis die jeweilige Aufgabe abgeschlossen ist, nicht das gesamte Pool.

```java
for (Future<String> future : ocrFutures) {
    System.out.println("----");
    System.out.println(future.get()); // prints OCR result for one PNG
}
```

Typische Konsolenausgabe sieht so aus:

```
----
The quick brown fox jumps over the lazy dog.
----
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----
Page 3 content goes here…
```

Wenn Sie die Ergebnisse lieber in Dateien schreiben möchten, ersetzen Sie `System.out.println` durch einen Aufruf von `Files.writeString`.

---

## Schritt 7: Executor Service sauber herunterfahren

Wenn jede Aufgabe erledigt ist, ist es entscheidend, den **shut down executor service** auszuführen; andernfalls könnte Ihre JVM nicht‑Daemon‑Threads am Leben erhalten, was einen sauberen Exit verhindert.

```java
threadPool.shutdown();               // No new tasks accepted
if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
    threadPool.shutdownNow();        // Force shutdown after timeout
}
```

Das Muster `awaitTermination` gibt dem Pool die Chance, laufende Arbeiten abzuschließen, bevor wir ihn zwangsweise beenden. Dieses Vorgehen zu ignorieren, ist eine häufige Ursache für Speicherlecks in langlebigen Anwendungen.

---

## Vollständiges funktionierendes Beispiel

Alles zusammengefügt, hier das komplette Programm, das Sie in `ParallelBatchDemo.java` kopieren und ausführen können:

```java
import com.aspose.ocr.*;

import java.util.*;
import java.util.concurrent.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license (optional)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // 2️⃣ Shared, thread‑safe OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Fixed thread pool java – one thread per core
        int threadCount = Runtime.getRuntime().availableProcessors();
        ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);

        // 4️⃣ Files to process – extract text from png
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png"
        );

        // 5️⃣ Submit tasks – parallel OCR processing
        List<Future<String>> ocrFutures = new ArrayList<>();
        for (String imagePath : imageFiles) {
            ocrFutures.add(threadPool.submit(() -> {
                OcrInput input = new OcrInput();
                input.add(imagePath);
                OcrResult result = ocrEngine.recognize(input);
                return result.getText();
            }));
        }

        // 6️⃣ Retrieve and print – convert scanned pages text
        for (Future<String> future : ocrFutures) {
            System.out.println("----");
            System.out.println(future.get());
        }

        // 7️⃣ Shut down executor service cleanly
        threadPool.shutdown();
        if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
            threadPool.shutdownNow();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}