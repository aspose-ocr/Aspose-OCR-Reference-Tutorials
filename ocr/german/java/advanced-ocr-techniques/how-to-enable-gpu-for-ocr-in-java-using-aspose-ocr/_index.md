---
category: general
date: 2026-08-18
description: Wie man die GPU für OCR in Java aktiviert und schnell Bildtext erkennt,
  Text aus JPG extrahiert, Filter hinzufügt und die Sprache mit Aspose.OCR einstellt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gpu
- recognize image text
- extract text jpg
- how to add filter
- how to set language
language: de
lastmod: 2026-08-18
og_description: Wie man die GPU für OCR in Java aktiviert und sofort Bildtext erkennt,
  Text aus JPG extrahiert, Filter hinzufügt und die Sprache mit Aspose.OCR festlegt.
og_image_alt: Screenshot showing Java code that enables GPU for OCR with Aspose.OCR
og_title: Wie man die GPU für OCR in Java aktiviert – vollständige Aspose.OCR-Anleitung
schemas:
- author: Aspose
  dateModified: '2026-08-18'
  description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  headline: How to enable GPU for OCR in Java using Aspose.OCR
  type: TechArticle
- description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  name: How to enable GPU for OCR in Java using Aspose.OCR
  steps:
  - name: 3.1 Set the OCR language
    text: '```java // Choose the language for recognition – this is the “how to set
      language” step engine.setLanguage(OcrLanguage.ENGLISH); ```'
  - name: 3.2 Add a preprocessing filter
    text: 'Noise, compression artifacts, or uneven lighting can hurt accuracy. Adding
      a denoise filter is the typical **how to add filter** approach:'
  - name: Expected output
    text: '``` Recognized text: The quick brown fox jumps over the lazy dog. ```'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- GPU acceleration
title: Wie man GPU für OCR in Java mit Aspose.OCR aktiviert
url: /de/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GPU für OCR in Java mit Aspose.OCR aktivieren

Wenn Sie **how to enable GPU** für OCR in Java benötigen, führt Sie diese Anleitung Schritt für Schritt durch. Das Aktivieren der GPU‑Beschleunigung ermöglicht es Ihnen, **recognize image text** bis zu mehreren Male schneller zu **recognize**, was besonders wichtig ist, wenn Sie **extract text JPG** Dateien massenhaft verarbeiten müssen. Wir behandeln außerdem **how to add filter**, **how to set language** und wie das Endergebnis abgerufen wird.

Am Ende dieses Tutorials haben Sie ein vollständiges, ausführbares Programm, das:

* Den Aspose.OCR‑Engine mit GPU‑Unterstützung startet.  
* Die OCR‑Sprache konfiguriert (z. B. Englisch).  
* Einen Rauschunterdrückungsfilter anwendet, um die Genauigkeit zu verbessern.  
* Ein JPEG‑Bild lädt, die Erkennung ausführt und den extrahierten Text ausgibt.

> **Voraussetzung:** Java 17 oder höher, Maven und eine Aspose.OCR‑für‑Java‑Lizenz (die kostenlose Testversion funktioniert für Evaluierungen).

![Wie man GPU für OCR in Java aktiviert](/images/ocr-gpu.png){alt="Wie man GPU für OCR in Java aktiviert"}

## Was Sie benötigen

| Item | Reason |
|------|--------|
| **Java Development Kit (JDK) 17+** | Erforderlich, um das Beispiel zu kompilieren und auszuführen. |
| **Maven** | Vereinfacht die Verwaltung von Abhängigkeiten für Aspose.OCR. |
| **Aspose.OCR for Java** | Stellt die Klasse `OcrEngine` und GPU‑Unterstützung bereit. |
| **A sample JPEG image** (`sample.jpg`) | Wird verwendet, um **extract text JPG** zu demonstrieren. |
| **GPU‑compatible hardware** (optional but recommended) | Ermöglicht den Leistungsboost, den wir konfigurieren werden. |

## Schritt 1: Maven‑Projekt einrichten

Erstellen Sie ein neues Maven‑Projekt (oder fügen Sie es zu einem bestehenden hinzu) und binden Sie die Aspose.OCR‑Abhängigkeit ein:

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-gpu-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Aspose.OCR for Java -->
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-ocr</artifactId>
            <version>23.12</version> <!-- Use the latest stable version -->
        </dependency>
    </dependencies>
</project>
```

> **Profi‑Tipp:** Halten Sie die Versionsnummer aktuell; neuere Releases verbessern die GPU‑Verarbeitung und fügen Sprachpakete hinzu.

## Schritt 2: OCR‑Engine initialisieren und **how to enable GPU**

Das Herzstück der Lösung ist die `OcrEngine`. Die Instanziierung ist einfach, aber Sie müssen die GPU‑Beschleunigung explizit aktivieren:

```java
import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2.2: Enable GPU acceleration (this is the “how to enable GPU” part)
        engine.setUseGpu(true); // <-- GPU is now active

        // Step 2.3: Configure language and preprocessing filter (covered later)
```

**Warum GPU aktivieren?**  
Wenn `setUseGpu(true)` aufgerufen wird, lagert Aspose.OCR schwere Bildverarbeitungs‑Kernels an die Grafikkarte aus. Auf einer modernen NVIDIA/AMD‑GPU kann die Erkennungsgeschwindigkeit von ~200 ms pro Seite auf < 80 ms steigen, was die Gesamtverarbeitungszeit für große Stapel dramatisch reduziert.

## Schritt 3: **how to set language** und **how to add filter**

### 3.1 OCR‑Sprache festlegen

```java
        // Choose the language for recognition – this is the “how to set language” step
        engine.setLanguage(OcrLanguage.ENGLISH);
```

Aspose.OCR wird mit Sprachpaketen für über 100 Sprachen geliefert. Ersetzen Sie `ENGLISH` durch `FRENCH`, `CHINESE_SIMPLIFIED` usw., um Ihr Ausgangsmaterial zu entsprechen.

### 3.2 Vorverarbeitungsfilter hinzufügen

Rauschen, Kompressionsartefakte oder ungleichmäßige Beleuchtung können die Genauigkeit beeinträchtigen. Das Hinzufügen eines Rauschunterdrückungsfilters ist der typische **how to add filter** Ansatz:

```java
        // Add a denoising filter to improve OCR quality – “how to add filter”
        engine.addPreprocessFilter(FilterType.DENOISE);
```

Weitere nützliche Filter sind `FilterType.CONTRAST`, `FilterType.BRIGHTNESS` und `FilterType.BINARIZE`. Sie können mehrere Filter verketten, indem Sie `addPreprocessFilter` wiederholt aufrufen.

## Schritt 4: Bild laden – **extract text JPG**

Jetzt zeigen wir die Engine auf die JPEG‑Datei, die wir verarbeiten wollen:

```java
        // Load the JPEG image – this demonstrates “extract text JPG”
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

Ersetzen Sie `YOUR_DIRECTORY` durch den tatsächlichen Pfad, in dem sich `sample.jpg` befindet. Aspose.OCR unterstützt außerdem PNG, BMP, TIFF und PDF; derselbe Aufruf funktioniert für diese Formate.

## Schritt 5: OCR ausführen und **recognize image text**

Mit der konfigurierten Engine rufen Sie die Erkennungsroutine auf:

```java
        // Run the OCR operation – “recognize image text”
        engine.recognize();

        // Retrieve the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);
    }
}
```

Die Methode `recognize()` verarbeitet das Bild auf der GPU (falls aktiviert) und füllt den internen Textpuffer. `getText()` liefert einen Klartext‑`String` zurück, den Sie in eine Datei, eine Datenbank schreiben oder an nachgelagerte NLP‑Pipelines weitergeben können.

### Erwartete Ausgabe

```
Recognized text: The quick brown fox jumps over the lazy dog.
```

Enthält das Bild mehrere Zeilen, enthält der zurückgegebene String Zeilenumbrüche (`\n`), die das ursprüngliche Layout beibehalten.

## Schritt 6: GPU‑Nutzung überprüfen (optional)

Um zu bestätigen, dass die GPU tatsächlich verwendet wird, aktivieren Sie das Aspose‑Logging:

```java
        // Enable diagnostic logging (optional)
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
```

Untersuchen Sie `ocr-debug.log` nach einem Lauf; Sie sollten Einträge wie `GPU device: NVIDIA GeForce RTX 3080` und `Processing time (GPU): 78 ms` sehen. Wenn das Protokoll **CPU** erwähnt, überprüfen Sie Ihre Treiberinstallation und ob der Aufruf `setUseGpu(true)` vorhanden ist.

## Häufige Fallstricke und wie man sie vermeidet

| Symptom | Likely cause | Fix |
|---------|--------------|-----|
| **`java.lang.UnsatisfiedLinkError: no aspose_ocr_native`** | Fehlende native GPU‑Bibliotheken | Installieren Sie den neuesten GPU‑Treiber und stellen Sie sicher, dass die nativen `aspose-ocr`‑Binärdateien im `java.library.path` liegen. |
| **Poor accuracy on dark images** | Kein Vorverarbeitungsfilter | Fügen Sie `engine.addPreprocessFilter(FilterType.BRIGHTNESS)` hinzu oder erhöhen Sie `FilterType.CONTRAST`. |
| **`OutOfMemoryError` on large batches** | GPU‑Speicherauslastung | Verarbeiten Sie Bilder in kleineren Stapeln oder deaktivieren Sie die GPU (`engine.setUseGpu(false)`) für sehr große Auflösungen. |
| **Incorrect language output** | Falsche Sprache eingestellt | Verifizieren Sie, dass `engine.setLanguage(OcrLanguage.YOUR_LANGUAGE)` mit dem Quelltext übereinstimmt. |

## Vollständiges, ausführbares Beispiel

Unten finden Sie die vollständige Java‑Klasse, die Sie in `src/main/java/com/example/HelloWorldOcr.java` kopieren können. Sie enthält alle Schritte, Fehlerbehandlung und optionales Logging.

```java
package com.example;

import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // -------------------------------------------------
        // 1️⃣ Enable GPU acceleration – how to enable GPU
        // -------------------------------------------------
        engine.setUseGpu(true);

        // -------------------------------------------------
        // 2️⃣ Set language – how to set language
        // -------------------------------------------------
        engine.setLanguage(OcrLanguage.ENGLISH); // Change if needed

        // -------------------------------------------------
        // 3️⃣ Add preprocessing filter – how to add filter
        // -------------------------------------------------
        engine.addPreprocessFilter(FilterType.DENOISE);
        // Optional: engine.addPreprocessFilter(FilterType.CONTRAST);

        // -------------------------------------------------
        // 4️⃣ Load the JPEG image – extract text JPG
        // -------------------------------------------------
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        engine.setImage(ImageStream.fromFile(imagePath));

        // -------------------------------------------------
        // 5️⃣ Perform OCR – recognize image text
        // -------------------------------------------------
        engine.recognize();

        // Retrieve and display the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);

        // -------------------------------------------------
        // 6️⃣ Optional: write output to a file
        // -------------------------------------------------
        java.nio.file.Files.writeString(
                java.nio.file.Paths.get("output.txt"),
                text,
                java.nio.charset.StandardCharsets.UTF_8
        );

        // -------------------------------------------------
        // 7️⃣ Optional: enable debug logging to verify GPU usage
        // -------------------------------------------------
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
    }
}
```

**Programm ausführen**

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HelloWorldOcr
```

Sie sollten den erkannten Text in der Konsole ausgegeben und in `output.txt` gespeichert sehen. Die Datei `ocr-debug.log` bestätigt die GPU‑Nutzung.

## Fazit

In diesem Tutorial haben wir **how to enable GPU** für Aspose.OCR in Java demonstriert, wie man **recognize image text**, **extract text JPG**, **how to add filter** und **how to set language** verwendet – alles in einem einzigen, eigenständigen Programm. Durch das Aktivieren der GPU erhalten Sie einen erheblichen Geschwindigkeitsvorteil, während Filter und Spracheinstellungen eine hohe Genauigkeit über verschiedene Bildquellen hinweg gewährleisten.

**Nächste Schritte**

* Experimentieren Sie mit zusätzlichen Filtern wie `FilterType.BINARIZE` für gescannte Dokumente.  
* Wechseln Sie zu anderen Sprachen (`OcrLanguage.SPANISH`, `OcrLanguage.CHINESE_SIMPLIFIED`), um die mehrsprachige Unterstützung zu erweitern.  
* Kombinieren Sie diese OCR‑Pipeline mit Apache PDFBox, um Text direkt aus PDF‑Seiten zu extrahieren.

Passen Sie den Code gern für die Stapelverarbeitung an, integrieren Sie ihn in einen Spring‑Boot‑Service oder binden Sie ihn an eine Nachrichtenwarteschlange für Echtzeit‑OCR‑Workloads ein. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to Read Text from an Image in Java Using Aspose OCR – Complete Guide](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Preprocess Image OCR in Java with Aspose OCR – Boost Accuracy & Extract Text](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}