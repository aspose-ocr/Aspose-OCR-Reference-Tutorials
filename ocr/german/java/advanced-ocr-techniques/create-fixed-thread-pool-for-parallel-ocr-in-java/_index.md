---
category: general
date: 2026-05-03
description: Erstelle einen festen Thread‑Pool in Java, um Text schnell aus Bildern
  zu extrahieren. Erfahre, wie man OCR ausführt, Bilder in Text umwandelt und die
  Leistung mit paralleler OCR‑Verarbeitung steigert.
draft: false
keywords:
- create fixed thread pool
- extract text from images
- how to run OCR
- convert image to text
- parallel OCR processing
language: de
og_description: Erstelle einen festen Thread‑Pool in Java, um Text schnell aus Bildern
  zu extrahieren. Erfahre, wie du OCR ausführst, Bilder in Text umwandelst und die
  Leistung mit paralleler OCR‑Verarbeitung steigerst.
og_title: Erstelle einen festen Thread‑Pool für parallele OCR in Java
tags:
- Java
- OCR
- Multithreading
title: Erstelle einen festen Thread‑Pool für parallele OCR in Java
url: /de/java/advanced-ocr-techniques/create-fixed-thread-pool-for-parallel-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Erstelle einen festen Thread-Pool für paralleles OCR in Java

Haben Sie jemals **einen festen Thread-Pool erstellen** müssen, um OCR‑Jobs zu beschleunigen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein. In vielen bildintensiven Projekten ist der Engpass der einstufige OCR‑Aufruf, und die Lösung ist überraschend einfach: Einen Pool von Worker‑Threads starten und sie die Dateien parallel verarbeiten lassen.  

In diesem Tutorial lernen Sie, wie Sie **Text aus Bildern extrahieren** mit Aspose OCR, wie Sie **OCR effizient ausführen** und wie Sie **Bild zu Text konvertieren** können, ohne Ihre CPU zu überlasten. Am Ende haben Sie ein sofort ausführbares Java‑Programm, das **parallele OCR‑Verarbeitung** an einer Handvoll Beispielbilder demonstriert.

## Was Sie bauen werden

Wir stellen eine kleine Konsolen‑App zusammen, die:

* Eine Liste von Bildpfaden (PNG, JPG, TIFF, BMP) einliest.
* **Einen festen Thread-Pool** erstellt, der der Anzahl der CPU‑Kerne entspricht.
* Für jedes Bild eine OCR‑Aufgabe dispatcht.
* Den erkannten Text sammelt und in der Konsole ausgibt.
* Den Executor sauber herunterfährt.

Keine externen Build‑Tools, keine ausgefallenen Frameworks — nur reines Java und die Aspose OCR‑Bibliothek. Wenn Sie Java 8+ und eine ordentliche IDE haben, sind Sie startklar.

## Voraussetzungen

* **Java Development Kit (JDK) 8 oder neuer** – der Code verwendet Lambdas, ältere Versionen lassen sich nicht kompilieren.
* **Aspose OCR für Java** – das JAR von der Aspose‑Website herunterladen oder über Maven einbinden (`com.aspose:aspose-ocr`).
* Ein Ordner mit ein paar Testbildern (der Code verweist auf `YOUR_DIRECTORY`).  
* Grundlegende Kenntnisse der Java‑Parallelität (den Rest erklären wir).

> *Pro‑Tipp:* Wenn Sie Maven verwenden, fügen Sie die Abhängigkeit zu Ihrer `pom.xml` hinzu und lassen Sie die IDE den Klassenpfad verwalten.  

---

## Schritt 1: Die erforderlichen Importe hinzufügen

Zuerst bringen wir die Klassen, die wir benötigen, in den Gültigkeitsbereich. Das ist nicht nur Boilerplate; jeder Import sagt der JVM, wo die OCR‑Engine, Bild‑Utilities und die Concurrency‑Tools zu finden sind, die uns **einen festen Thread-Pool erstellen** lassen.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;
```

* `com.aspose.ocr.*` – die Kern‑OCR‑API.  
* `java.util.*` – Collections zum Speichern von Bildpfaden und Ergebnissen.  
* `java.util.concurrent.*` – das Concurrency‑Paket, das `ExecutorService` und `Future` bereitstellt.

---

## Schritt 2: Die zu verarbeitenden Bilder definieren

Als Nächstes listen wir die Dateien auf, aus denen wir **Text aus Bildern extrahieren** wollen. `Arrays.asList` hält den Code kompakt und ermöglicht es, Ihr eigenes Verzeichnis einzusetzen, ohne die übrige Logik zu ändern.

```java
List<String> imagePaths = Arrays.asList(
        "YOUR_DIRECTORY/image1.png",
        "YOUR_DIRECTORY/image2.jpg",
        "YOUR_DIRECTORY/image3.tif",
        "YOUR_DIRECTORY/image4.bmp"
);
```

Fügen Sie gern weitere Einträge hinzu; der Thread‑Pool skaliert automatisch basierend auf der Anzahl Ihrer CPU‑Kerne.

---

## Schritt 3: **Einen festen Thread-Pool erstellen**, passend zu den CPU‑Kernen

Hier kommt das Herzstück des Tutorials. Wir fragen die Laufzeit, wie viele Kerne verfügbar sind, und lassen die `Executors`‑Factory uns einen Pool exakt dieser Größe geben. Warum fest? Weil eine vorhersehbare Thread‑Anzahl das gefürchtete „Thread‑Explodieren“ verhindert, das das Betriebssystem mit Ressourcen ersticken kann.

```java
int coreCount = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(coreCount);
```

* `availableProcessors()` liefert die logische Kernanzahl (inklusive Hyper‑Threads).  
* `newFixedThreadPool(coreCount)` garantiert, dass wir nie die Kapazität der CPU überschreiten – der sicherste Weg, **OCR parallel auszuführen**.

---

## Schritt 4: Für jedes Bild eine OCR‑Aufgabe einreichen

Jetzt verwandeln wir jeden Dateipfad in ein `Callable`, das **OCR ausführt**, den Text erkennt und das Ergebnis zurückgibt. Beachten Sie, dass wir innerhalb des Lambdas eine frische `OcrEngine` instanziieren — das verhindert das thread‑unsichere Teilen von Engine‑Zuständen.

```java
List<Future<String>> ocrResults = new ArrayList<>();
for (String path : imagePaths) {
    ocrResults.add(executor.submit(() -> {
        OcrEngine engine = new OcrEngine();          // fresh engine per task
        engine.setImage(ImageStream.fromFile(path));
        engine.getLanguage().setEnglish(true);
        return engine.recognize() ? engine.getText()
                                   : "Failed: " + path;
    }));
}
```

* Jeder `submit`‑Aufruf übergibt das Lambda an den Pool, der es einem freien Thread zuweist.  
* Die `Future<String>`‑Objekte ermöglichen es uns, den erkannten Text später abzurufen und bei Bedarf die Reihenfolge beizubehalten.

---

## Schritt 5: Den erkannten Text abrufen und anzeigen

Sobald alle Aufgaben in die Warteschlange gestellt sind, iterieren wir einfach über die `Future`‑Liste und rufen `get()` auf, um zu blockieren, bis jeder OCR‑Job fertig ist. Hier wird der **Bild‑zu‑Text‑Konvertierung**‑Schritt sichtbar: Der Aufruf `engine.getText()` liefert den rohen String.

```java
for (Future<String> result : ocrResults) {
    System.out.println("OCR result:\n" + result.get());
}
```

Typische Konsolenausgabe sieht so aus:

```
OCR result:
Hello world!
OCR result:
Invoice #12345
Date: 2026‑04‑30
...
```

Scheitert eine Datei (z. B. weil sie beschädigt ist), sehen Sie eine Zeile, die mit `Failed:` beginnt, gefolgt vom Pfad — praktisch für schnelles Debugging.

---

## Schritt 6: Den Executor Service bereinigen

Vergessen Sie nie, den Pool herunterzufahren; sonst bleibt die JVM eventuell aktiv, weil sie denkt, es gäbe noch Arbeit. Ein geordneter Shutdown lässt laufende Aufgaben beenden, bevor der Prozess endet.

```java
executor.shutdown();
```

Sie können auch `awaitTermination` aufrufen, wenn Sie ein Timeout erzwingen wollen, aber für die meisten Kommandozeilen‑Utilities reicht ein einfaches `shutdown()` aus.

---

## Vollständiges funktionierendes Beispiel

Unten finden Sie das komplette, sofort ausführbare Programm. Kopieren Sie es in eine Datei namens `ParallelOcrTutorial.java`, passen Sie die Bildpfade an und führen Sie `javac` + `java` wie gewohnt aus.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Define the images to be processed
        List<String> imagePaths = Arrays.asList(
                "YOUR_DIRECTORY/image1.png",
                "YOUR_DIRECTORY/image2.jpg",
                "YOUR_DIRECTORY/image3.tif",
                "YOUR_DIRECTORY/image4.bmp"
        );

        // Step 3: Create a fixed‑size thread pool matching the CPU cores
        int coreCount = Runtime.getRuntime().availableProcessors();
        ExecutorService executor = Executors.newFixedThreadPool(coreCount);

        // Step 4: Submit an OCR task for each image
        List<Future<String>> ocrResults = new ArrayList<>();
        for (String path : imagePaths) {
            ocrResults.add(executor.submit(() -> {
                OcrEngine engine = new OcrEngine();          // fresh engine per task
                engine.setImage(ImageStream.fromFile(path));
                engine.getLanguage().setEnglish(true);
                return engine.recognize() ? engine.getText()
                                           : "Failed: " + path;
            }));
        }

        // Step 5: Retrieve and display the recognized text
        for (Future<String> result : ocrResults) {
            System.out.println("OCR result:\n" + result.get());
        }

        // Step 6: Clean up the executor service
        executor.shutdown();
    }
}
```

**Erwartetes Ergebnis:** Der Textinhalt jedes Bildes wird in der Konsole ausgegeben, in derselben Reihenfolge wie die `imagePaths`‑Liste. Kann ein Bild nicht verarbeitet werden, erscheint stattdessen ein Fehlermeldungshinweis.

---

## Häufige Fragen & Sonderfälle

### Was ist, wenn ich mehr Bilder als Threads habe?

Der feste Thread‑Pool wird die überschüssigen Aufgaben automatisch in die Warteschlange stellen. Sobald ein Thread seinen aktuellen OCR‑Job beendet, übernimmt er die nächste Aufgabe. Dieses Warteschlangen‑Verhalten ist das Wesen der **parallelen OCR‑Verarbeitung** — Sie erhalten maximalen Durchsatz, ohne die CPU zu überlasten.

### Kann ich die Sprache ändern?

Absolut. Ersetzen Sie `engine.getLanguage().setEnglish(true);` durch das passende Sprach‑Flag, z. B. `setFrench(true)` oder aktivieren Sie mehrere Sprachen, indem Sie mehrere Setter vor `recognize()` aufrufen.

### Wie gehe ich mit sehr großen Bildern um?

Große Dateien können pro Thread viel Speicher verbrauchen. Wenn Sie `OutOfMemoryError` bemerken, sollten Sie das Bild vor dem Einspeisen in die Engine verkleinern oder den Heap mit `-Xmx` vergrößern. Ein weiterer Ansatz ist die Verwendung eines **cached thread pool** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}