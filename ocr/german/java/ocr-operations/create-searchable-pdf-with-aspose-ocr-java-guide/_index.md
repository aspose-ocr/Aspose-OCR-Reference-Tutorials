---
category: general
date: 2026-03-26
description: Erstellen Sie ein durchsuchbares PDF mit Aspose.OCR Java – lernen Sie,
  ein Bild zu laden, OCR auszuführen, die Hauptsprache festzulegen, Text aus dem Bild
  zu extrahieren und das OCR‑PDF zu speichern.
draft: false
keywords:
- create searchable pdf
- set primary language
- extract text from image
- load image ocr
- save ocr pdf
language: de
og_description: Erstellen Sie ein durchsuchbares PDF mit Aspose.OCR Java. Schritt‑für‑Schritt‑Anleitung
  zum Laden von Bild‑OCR, Festlegen der Primärsprache, Extrahieren von Text aus dem
  Bild und Speichern des OCR‑PDFs.
og_title: Durchsuchbare PDF mit Aspose.OCR erstellen – Java‑Leitfaden
tags:
- Aspose.OCR
- Java
- PDF
- OCR
title: Erstellen eines durchsuchbaren PDFs mit Aspose.OCR – Java‑Leitfaden
url: /de/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Durchsuchbares PDF mit Aspose.OCR erstellen – Java‑Leitfaden

Haben Sie jemals **ein durchsuchbares PDF** aus einem gescannten Dokument erstellen müssen, wussten aber nicht, wo Sie anfangen sollen? Sie sind nicht allein – viele Entwickler stoßen an diese Hürde, wenn sie zum ersten Mal OCR in Java angehen. Die gute Nachricht ist, dass Aspose.OCR die gesamte Pipeline – vom Laden eines Bildes über das Festlegen der primären Sprache bis hin zum Speichern eines OCR‑aktivierten PDFs – ziemlich unkompliziert macht. In diesem Tutorial führen wir Sie durch ein vollständiges, ausführbares Beispiel, das **Text aus Bild extrahiert**, Ihnen ermöglicht, die **primäre Sprache festzulegen**, und mit einem **OCR‑PDF speichern** endet, das Sie in jedem Reader öffnen können.

Wir werden auch ein paar praktische Tipps behandeln, wie das Aktivieren der GPU‑Beschleunigung für schnellere Verarbeitung und das Handling von Dokumenten mit gemischten Sprachen (Tamil + Englisch in unserem Fall). Am Ende haben Sie ein robustes, produktionsreifes Snippet, das Sie in Ihr Projekt einbinden können.

## Was Sie benötigen

- **Java 17** (oder ein aktuelles JDK; Aspose.OCR unterstützt Java 8+)
- **Aspose.OCR for Java** Bibliothek (von der offiziellen Website herunterladen oder über Maven hinzufügen)
- Eine **Lizenzdatei** (oder die 30‑tägige Testversion)
- Eine Bilddatei, die Text enthält (das Demo verwendet `sample-mixed-tamil-eng.jpg`)

Keine zusätzlichen Frameworks, keine nativen Abhängigkeiten – nur reines Java und die Aspose‑JARs.

---

## Schritt 1: Durchsuchbares PDF erstellen – Projekt einrichten

Bevor wir in den Code eintauchen, stellen wir sicher, dass das Projekt bereit ist, **durchsuchbare PDFs** zu erstellen.

```bash
# Maven dependency (add to pom.xml)
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version -->
</dependency>
```

> **Pro Tipp:** Halten Sie die Versionsnummer aktuell; neuere Releases enthalten oft Leistungsverbesserungen für die GPU‑Nutzung.

Erstellen Sie nun eine einfache Java‑Klasse namens `RecentFeaturesDemo`. Die Klasse enthält die gesamte Logik, die wir benötigen, um **Bild‑OCR zu laden**, Spracheinstellungen zu konfigurieren und schließlich **OCR‑PDF zu speichern**.

---

## Schritt 2: Bild‑OCR laden und Engine initialisieren

Der erste eigentliche Schritt in der Pipeline ist das **Laden von Bild‑OCR**. Damit teilt man Aspose.OCR mit, welche Datei analysiert werden soll.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // 2️⃣ Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable GPU acceleration – speeds up recognition dramatically
        ocrEngine.getEngineSettings().setUseGpu(true);
        // Use all available CPU cores for parallel processing
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);
```

> **Warum das wichtig ist:** Das Aktivieren der GPU (`setUseGpu(true)`) kann die Verarbeitungszeit auf moderner Hardware um bis zu 70 % reduzieren, während parallele Verarbeitung sicherstellt, dass die CPU nicht untätig bleibt, wenn die GPU beschäftigt ist.

---

## Schritt 3: Primäre Sprache festlegen (und eine sekundäre)

Wenn Sie diesen Schritt überspringen, versucht Aspose.OCR die Sprache zu erraten, was langsamer und weniger genau ist. So legen Sie die **primäre Sprache** auf Tamil fest und fügen Englisch als Rückfallback hinzu.

```java
        // 3️⃣ Define languages – primary is Tamil, secondary is English
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English);
```

> **Erklärung:** Die primäre Sprache beeinflusst den Zeichensatz und das Wörterbuch, das während der Erkennung verwendet wird. Das Hinzufügen einer sekundären Sprache ist entscheidend für Dokumente mit gemischten Schriftsystemen (denken Sie an einen Beleg mit sowohl Tamil- als auch Englischtext).  
> **Randfall:** Wenn Ihr Dokument mehr als zwei Sprachen enthält, können Sie `addAdditionalLanguage(...)` für jede zusätzliche Sprache aufrufen.

---

## Schritt 4: Bild vorverarbeiten – Entzerren & Rauschen entfernen

Gescanntes Bild leidet häufig unter Rotation oder Hintergrundrauschen. Die Vorverarbeitung hilft der OCR‑Engine, **Text aus Bild zuverlässiger zu extrahieren**.

```java
        // 4️⃣ Pre‑processing options
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // auto‑rotate tilted pages
                 .setDenoise(true); // suppress speckles and background patterns
```

> **Tipp:** Wenn Sie wissen, dass das Bild bereits sauber ist, können Sie `setDenoise(true)` überspringen, um ein paar Millisekunden zu sparen.

---

## Schritt 5: Bilddatei laden

Jetzt, da die Engine bereit ist, zeigen wir sie auf die Datei, die wir analysieren wollen.

```java
        // 5️⃣ Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

> **Was ist, wenn der Pfad falsch ist?** Aspose.OCR wirft eine klare `FileNotFoundException`. Wickeln Sie den Aufruf in ein try‑catch, wenn Sie eine elegante Fehlerbehandlung benötigen.

---

## Schritt 6: OCR ausführen und Text aus Bild extrahieren

Mit allen Einstellungen ist es Zeit, die Erkennung tatsächlich auszuführen. Dieser Schritt **extrahiert Text aus dem Bild** und bereitet die für die PDF‑Erstellung benötigten Daten vor.

```java
        // 6️⃣ Perform recognition
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Print the raw OCR output – handy for debugging
            System.out.println("Recognized text:");
            System.out.println(recognizedText);
```

Die typische Konsolenausgabe für das Demo‑Bild sieht folgendermaßen aus:

```
வணக்கம் World
This is a mixed language sample.
```

Sie werden feststellen, dass die Tamil‑Zeile korrekt dargestellt wird, gefolgt von Englisch. Das ist die Belohnung für das korrekte **Setzen der primären Sprache**.

---

## Schritt 7: OCR‑PDF speichern – Das letzte Teil

Das letzte Puzzleteil ist das **Speichern des OCR‑PDFs**. Aspose.OCR kann eine unsichtbare Textebene über dem Originalbild einbetten, wodurch das PDF durchsuchbar wird.

```java
            // 7️⃣ (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Öffnen Sie `searchable.pdf` in Adobe Reader, drücken Sie **Strg + F**, und Sie können sowohl nach tamilischen als auch nach englischen Wörtern suchen – genau das, was ein **Durchsuchbares‑PDF‑Erstellungs‑Workflow** verspricht.

---

## Vollständiges funktionierendes Beispiel (Copy‑Paste)

Unten finden Sie das vollständige Programm, das Sie unverändert kompilieren und ausführen können. Ersetzen Sie die Platzhalter‑Pfade durch Ihre eigenen Verzeichnisse.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineSettings().setUseGpu(true);                     // enable CUDA GPU acceleration
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);     // use multiple CPU cores
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);      // primary language
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English); // secondary language
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // correct image rotation
                 .setDenoise(true); // reduce background noise

        // Step 3: Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Run OCR and obtain the plain‑text result
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Step 5: (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("Recognized text:");
            System.out.println(recognizedText);
            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Führen Sie es aus mit:

```bash
javac -cp "path/to/aspose-ocr.jar" RecentFeaturesDemo.java
java -cp ".:path/to/aspose-ocr.jar" RecentFeaturesDemo
```

Sie sollten den extrahierten Text in der Konsole sehen, gefolgt von einer Bestätigung, dass das **durchsuchbare PDF** auf die Festplatte geschrieben wurde.

---

## Häufige Fragen & Randfälle

### Was, wenn ich **Bild‑OCR laden** aus einem Byte‑Array benötige?

Sie können `ImageStream.fromFile(imagePath)` durch `ImageStream.fromBytes(byteArray)` ersetzen. Das ist praktisch, wenn das Bild aus einer Datenbank oder einem Webservice stammt.

### Wie gehe ich mit PDFs um, die bereits Bilder enthalten?

Aspose.OCR kann direkt auf PDF‑Seiten arbeiten: `ocrEngine.setDocument(PdfDocument.fromFile("input.pdf"))`. Die Engine rastert jede Seite intern, bevor die Erkennung erfolgt.

### Meine GPU wird nicht erkannt – sollte ich `setUseGpu(true)` beibehalten?

Wenn `setUseGpu(true)` fehlschlägt, fällt Aspose.OCR automatisch auf die CPU zurück. Sie können `ocrEngine.getEngineSettings().isGpuAvailable()` prüfen, bevor Sie es aktivieren.

### Kann ich **OCR‑PDF speichern** mit benutzerdefinierten Metadaten?

Ja. Nach der Erkennung verwenden Sie `ocrEngine.getPdfSaveOptions().setTitle("My Document")` oder `setAuthor("John Doe")`, bevor Sie `save` aufrufen.

---

## Leistungstipps für große Stapel

- **Batchverarbeitung:** Verwenden Sie dieselbe `OcrEngine`‑Instanz für mehrere Bilder. Rufen Sie nur `ocrEngine.clear()` zwischen den Durchläufen auf.
- **Thread‑Pool:** Packen Sie jede Bildaufgabe in ein `Callable` und übergeben Sie sie an einen `ExecutorService`. Da wir parallele Verarbeitung aktiviert haben, profitiert jeder Thread von der Multi‑Core‑Nutzung.
- **Speichermanagement:** Bei Gigapixel‑Bildern sollten Sie eine Down‑Sampling‑Rate mit `ocrEngine.getPreprocessingSettings().setResizeFactor(0.5)` in Betracht ziehen, um den RAM‑Verbrauch im Rahmen zu halten.

---

## Fazit

Wir haben gerade einen vollständigen **Durchsuchbares‑PDF‑Erstellungs‑Workflow** mit Aspose.OCR für Java durchgegangen. Beginnend mit **Bild‑OCR laden**, haben wir

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}