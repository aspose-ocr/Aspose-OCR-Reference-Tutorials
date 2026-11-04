---
category: general
date: 2026-01-12
description: Erfahren Sie, wie Sie Text aus Bildern erkennen und Text aus PNG-Dateien
  mit Aspose OCR in Java extrahieren. Parallelverarbeitung macht es schnell.
draft: false
keywords:
- recognize text from images
- extract text from png
language: de
og_description: Entdecken Sie den einfachsten Weg, Text aus Bildern in Java zu erkennen
  und Text aus PNG‑Dateien mit Aspose OCR und Parallelverarbeitung zu extrahieren.
og_title: Texte aus Bildern mit Java erkennen – Parallel-OCR-Leitfaden
tags:
- OCR
- Java
- Aspose
title: Texte aus Bildern mit Java erkennen – Parallel-OCR-Tutorial
url: /de/java/advanced-ocr-techniques/recognize-text-from-images-with-java-parallel-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Texterkennung aus Bildern mit Java – Parallel‑OCR‑Tutorial

Haben Sie jemals **Texte aus Bildern erkennen** müssen, waren aber unsicher, wie das geht? Sie sind nicht allein. Egal, ob Sie Rechnungen digitalisieren, Daten aus Screenshots extrahieren oder ein durchsuchbares Archiv erstellen – die Fähigkeit, *Texte aus Bildern zu erkennen*, ist ein echter Wendepunkt.  

In diesem Leitfaden führen wir Sie durch ein vollständiges, sofort ausführbares Java‑Beispiel, das nicht nur **Texte aus Bildern erkennt**, sondern auch zeigt, wie Sie **Text aus PNG**‑Dateien mit Aspose OCRs eingebauter Parallel‑Engine extrahieren können. Keine externen Skripte, keine fehlenden Teile – nur klarer Code und verständliche Erklärungen.

## Was Sie lernen werden

- Aspose OCR in einem Java‑Projekt einrichten  
- Parallelverarbeitung aktivieren, um Batch‑Jobs zu beschleunigen  
- Eine Sammlung von PNG‑Dateien laden und **Text aus PNG** effizient extrahieren  
- Übliche Fallstricke behandeln (große Dateien, leere Ergebnisse, Thread‑Grenzen)  
- Den vollständigen, ausführbaren Quellcode am Ende des Artikels sehen  

Wenn Sie fertig sind, haben Sie eine Copy‑Paste‑Lösung, die Sie an jeden bildbasierten Textextraktions‑Workflow anpassen können.

## Voraussetzungen

Bevor wir beginnen, stellen Sie sicher, dass Sie Folgendes haben:

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| Java 8 oder neuer | Aspose OCRs Java‑API zielt auf Java 8+ ab |
| Maven oder Gradle (zur Abhängigkeitsverwaltung) | Vereinfacht das Hinzufügen der Aspose OCR‑Bibliothek |
| Einige PNG‑Bilder, die Sie verarbeiten möchten | Das Tutorial verwendet `doc1.png`‑`doc4.png` als Beispiele |
| Grundkenntnisse der Java‑Syntax | Der Code ist unkompliziert, Sie müssen ihn jedoch kompilieren und ausführen |

Falls Ihnen etwas fehlt, holen Sie sich das neueste JDK von Oracle oder AdoptOpenJDK und richten Sie ein einfaches Maven‑Projekt ein – nichts Aufwändiges.

![Diagramm zur Texterkennung aus Bildern](image.png){alt="Diagramm zur Texterkennung aus Bildern"}

## Schritt 1 – Aspose OCR zu Ihrem Projekt hinzufügen

Zuerst teilen Sie Maven (oder Gradle) mit, die Aspose OCR‑Bibliothek zu holen. Fügen Sie in einer `pom.xml`‑Datei Folgendes hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Falls Sie Gradle bevorzugen, ist das Äquivalent:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Profi‑Tipp:** Prüfen Sie das [Aspose OCR Maven‑Repository](https://repo.aspose.com/repo) auf die neueste Version. Die Bibliothek aktuell zu halten, stellt sicher, dass Sie die neuesten OCR‑Verbesserungen und Fehlerbehebungen erhalten.

## Schritt 2 – Parallelverarbeitung aktivieren (das Geheimrezept)

Aspose OCR kann die Arbeitslast auf mehrere CPU‑Kerne verteilen. So bleibt die **Texterkennung aus Bildern**‑Operation schnell, selbst wenn Sie Dutzende von PNG‑Dateien haben.

```java
// Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Configure parallel options – up to 4 cores in this demo
ParallelOptions parallelOptions = new ParallelOptions();
parallelOptions.setMaxDegreeOfParallelism(4); // Adjust based on your machine
ocrEngine.setParallelOptions(parallelOptions);
```

Warum ein Limit setzen? Das Überbuchen von Threads kann andere Prozesse, insbesondere auf gemeinsam genutzten Servern, ausbremsen. Vier Kerne sind ein sicherer Standard für die meisten Desktops; erhöhen Sie den Wert, wenn Ihre Hardware mehr bewältigen kann.

## Schritt 3 – Liste der PNG‑Dateien vorbereiten

Das Tutorial konzentriert sich auf **Text aus PNG**‑Dateien zu extrahieren, aber derselbe Code funktioniert für JPEG, BMP usw. Legen Sie Ihre Bilder in einen Ordner und referenzieren Sie sie wie folgt:

```java
String[] imageFiles = {
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
};
```

> **Hinweis:** Ersetzen Sie `YOUR_DIRECTORY` durch den absoluten oder relativen Pfad, in dem die PNG‑Dateien liegen. Wenn Sie einen dynamischen Ordner verarbeiten müssen, können Sie `Files.list(Paths.get("YOUR_DIRECTORY"))` verwenden, um das Array automatisch zu erstellen.

## Schritt 4 – OCR für jedes Bild ausführen (die Engine übernimmt die schwere Arbeit)

Obwohl wir Parallelität aktiviert haben, iterieren wir weiterhin über das Dateiarrray. Aspose OCR verteilt die Erkennungsarbeit intern über die von uns konfigurierten Threads.

```java
for (String imagePath : imageFiles) {
    // Load the image into the engine
    ocrEngine.setImage(imagePath);
    
    // Perform recognition
    OcrResult result = ocrEngine.recognize();
    
    // Guard against empty results
    String text = result.getText();
    if (text == null || text.isEmpty()) {
        System.out.println("[" + imagePath + "] => No text found.");
        continue;
    }
    
    // Print a short preview (first 50 characters)
    System.out.println("[" + imagePath + "] => " +
        text.substring(0, Math.min(50, text.length())) + "...");
}
```

### Warum eine Schleife und kein Parallel‑Stream?

Aspose OCR teilt die Bildverarbeitung bereits intern basierend auf `ParallelOptions`. Das Einwickeln des Aufrufs in einen externen Parallel‑Stream würde die Arbeit doppelt verarbeiten und könnte die Leistung tatsächlich verschlechtern. Vertrauen Sie darauf, dass die Bibliothek die Threads verwaltet.

## Schritt 5 – Randfälle & praktische Tipps

| Situation | Was zu tun ist |
|-----------|----------------|
| **Großes PNG ( > 10 MB )** | Erhöhen Sie den JVM‑Heap (`-Xmx2g`) oder verkleinern Sie das Bild, bevor Sie es an die Engine übergeben. |
| **Gemischte Bildformate** | Verwenden Sie `ocrEngine.setImage(new File(imagePath))` – die Engine erkennt das Format automatisch. |
| **Vollständigen Text benötigen, nicht nur eine Vorschau** | Speichern Sie `result.getText()` in einem `StringBuilder` oder schreiben Sie es in eine Datei für die spätere Analyse. |
| **Ausführung auf einem CI‑Server ohne GUI** | Keine zusätzlichen Schritte – Aspose OCR ist vollständig headless. |
| **Lizenzablauf** | Registrieren Sie eine temporäre Lizenz mit `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`, um Evaluations‑Wasserzeichen zu vermeiden. |

## Vollständiges funktionierendes Beispiel

Unten finden Sie die komplette Java‑Klasse, die Sie kopieren, einfügen und ausführen können. Sie enthält alle besprochenen Teile sowie einige Kommentare zur Klarheit.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.parallel.*;

public class ParallelOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create and initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable parallel processing (up to 4 CPU cores)
        ParallelOptions parallelOptions = new ParallelOptions();
        parallelOptions.setMaxDegreeOfParallelism(4); // Adjust as needed
        ocrEngine.setParallelOptions(parallelOptions);

        // Step 3: Define the PNG files to be processed
        String[] imageFiles = {
            "YOUR_DIRECTORY/doc1.png",
            "YOUR_DIRECTORY/doc2.png",
            "YOUR_DIRECTORY/doc3.png",
            "YOUR_DIRECTORY/doc4.png"
        };

        // Step 4: Recognize text from each image (engine handles parallelism internally)
        for (String imagePath : imageFiles) {
            // Load the image
            ocrEngine.setImage(imagePath);

            // Perform OCR
            OcrResult result = ocrEngine.recognize();

            // Extract the recognized text
            String text = result.getText();

            // Guard against empty results
            if (text == null || text.isEmpty()) {
                System.out.println("[" + imagePath + "] => No text found.");
                continue;
            }

            // Step 5: Output a short preview (first 50 characters)
            System.out.println("[" + imagePath + "] => " +
                text.substring(0, Math.min(50, text.length())) + "...");
        }
    }
}
```

### Erwartete Ausgabe

Wenn `doc1.png` den Satz „Invoice #12345 – Total $250.00“ enthält, sehen Sie etwa Folgendes:

```
[YOUR_DIRECTORY/doc1.png] => Invoice #12345 – Total $250.00...
[YOUR_DIRECTORY/doc2.png] => No text found.
[YOUR_DIRECTORY/doc3.png] => Customer Name: John Doe...
[YOUR_DIRECTORY/doc4.png] => ...
```

Die Vorschau wird nach 50 Zeichen abgeschnitten, aber die vollständige Zeichenkette befindet sich in `result.getText()` für jede nachgelagerte Verarbeitung, die Sie benötigen.

## Fazit

Sie haben nun ein solides, produktionsreifes Muster, um **Texte aus Bildern** mit Aspose OCR in Java zu **erkennen**, und Sie haben genau gesehen, wie Sie **Text aus PNG**‑Dateien mit parallelen Geschwindigkeitssteigerungen **extrahieren** können. Die wichtigsten Schritte – Engine‑Einrichtung, Parallel‑Konfiguration, Bildlisten‑Vorbereitung und Ergebnis‑Verarbeitung – sind alle abgedeckt, zusammen mit einigen praktischen Tipps, um häufige Probleme zu vermeiden.

Was kommt als Nächstes? Versuchen Sie, die PNG‑Liste durch einen dynamischen Verzeichnisscan zu ersetzen, leiten Sie die OCR‑Ausgabe in einen Suchindex wie Elasticsearch, oder experimentieren Sie mit sprachspezifischen OCR‑Einstellungen (`ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH)`). Der Himmel ist die Grenze, sobald Sie den Kern‑Workflow gemeistert haben.

Wenn Sie auf Eigenheiten gestoßen sind oder Ideen haben, dieses Tutorial zu erweitern, hinterlassen Sie unten einen Kommentar. Viel Spaß beim Programmieren und beim Umwandeln dieser hartnäckigen Bilder in durchsuchbaren Text!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}