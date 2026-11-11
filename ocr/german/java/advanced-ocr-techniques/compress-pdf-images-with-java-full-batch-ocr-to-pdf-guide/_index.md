---
category: general
date: 2026-07-05
description: Komprimiere PDF‑Bilder beim Konvertieren von PNG zu PDF mit Java. Lerne
  Bildvorverarbeitung für OCR, erkenne Text in JPG und führe Batch‑OCR zu PDF in einem
  einzigen Tutorial durch.
draft: false
keywords:
- compress pdf images
- convert png to pdf
- image preprocessing for ocr
- recognize text jpg
- batch ocr to pdf
language: de
og_description: Komprimiere PDF‑Bilder und konvertiere PNG zu PDF mit Java. Dieser
  Leitfaden behandelt die Bildvorverarbeitung für OCR, die Texterkennung in JPG und
  die Stapel‑OCR zu PDF.
og_title: PDF-Bilder mit Java komprimieren – Vollständiges Batch‑OCR‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  headline: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  type: TechArticle
- description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  name: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints a line for each image, e.g.:'
  - name: What if my server has no GPU?
    text: Just set `gpuSettings.setEnabled(false)`. The rest of the pipeline remains
      unchanged, and you still get multithreaded CPU processing.
  - name: My PDFs are still too large—can I lower the quality further?
    text: Yes. Adjust `options.setImageQuality(70)` or even `50`. Lower values shrink
      size more aggressively but may blur fine glyphs. Test with a representative
      sample.
  - name: How do I handle other image formats (TIFF, BMP)?
    text: 'Add the extensions to the filter lambda:'
  - name: Can I keep the original color images instead of binarizing?
    text: Replace `.addBinarize()` with `.addGrayscale()` in the preprocessor builder
      if you need color retention for downstream analysis.
  type: HowTo
tags:
- ocr
- java
- pdf
- image-processing
title: PDF-Bilder mit Java komprimieren – Vollständige Batch-OCR‑zu‑PDF‑Anleitung
url: /de/java/advanced-ocr-techniques/compress-pdf-images-with-java-full-batch-ocr-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF‑Bilder mit Java komprimieren – Vollständige Batch‑OCR‑zu‑PDF‑Anleitung

Haben Sie jemals **PDF‑Bilder komprimieren** müssen, während Sie einen Ordner mit PNGs in durchsuchbare PDFs umwandeln? Sie sind nicht allein. In vielen Automatisierungspipelines ist der größte Schmerzpunkt, gleichzeitig Bildqualität, OCR‑Genauigkeit und die endgültige PDF‑Größe zu jonglieren.  

In diesem Tutorial führen wir Sie durch eine praktische Lösung, die **PNG zu PDF konvertiert**, **Bildvorverarbeitung für OCR** anwendet und schließlich **PDF‑Bilder komprimiert**, sodass die Ausgabe leicht bleibt. Am Ende wissen Sie, wie Sie **JPG‑Dateien mit Text erkennen**, einen **Batch‑OCR‑zu‑PDF**‑Workflow einrichten und Ihre PDFs ordentlich halten.

## Was Sie lernen werden

- Einrichtung von Aspose OCR für Java und Lizenzierung.
- Konfiguration der Engine für Multithreading, GPU‑Beschleunigung und Rechtschreibkorrektur.
- Aufbau einer wiederverwendbaren **Bildvorverarbeitung für OCR**‑Pipeline (Rauschentfernung, Kontrast, Binarisierung).
- Verwendung von **PdfSaveOptions**, um **PDF‑Bilder zu komprimieren**, ohne die Lesbarkeit zu beeinträchtigen.
- Durchlaufen eines Verzeichnisses, um **PNG zu PDF zu konvertieren** und **JPG‑Dateien mit Text** stapelweise zu erkennen.
- Ein vollständiges, sofort ausführbares Java‑Programm, das Sie in jedes Projekt einbinden können.

> **Voraussetzungen**: Java 8+, Maven oder Gradle, eine Aspose OCR für Java‑Lizenz und ein Ordner mit PNG/JPG‑Bildern, die Sie verarbeiten möchten.

---

## Schritt 1: Aspose OCR‑Lizenz anwenden (unverzichtbar für die Produktion)

Bevor Sie irgendeine OCR‑API aufrufen können, müssen Sie eine gültige Lizenz laden; andernfalls bleiben Sie bei den Einschränkungen der Testversion stecken.

```java
import com.aspose.ocr.*;

public class LicenseSetup {
    public static void loadLicense() throws Exception {
        License license = new License();
        // Point to your license file – keep it out of source control!
        license.setLicense("Aspose.OCR.Java.lic");
    }
}
```

*Warum das wichtig ist*: Eine lizenzierte Engine schaltet GPU‑Unterstützung frei, erhöht die Genauigkeit und entfernt Wasserzeichen, die Ihre PDF‑Dateien sonst aufblähen würden.

---

## Schritt 2: OCR‑Engine konfigurieren – Threads, GPU und Rechtschreibkorrektur

Eine schnelle OCR‑Engine ist das Rückgrat jedes **Batch‑OCR‑zu‑PDF**‑Jobs. Wir starten so viele Threads, wie die CPU des Hosts bewältigen kann, aktivieren die GPU‑Beschleunigung (falls Sie eine kompatible Karte besitzen) und schärfen die Rechtschreibkorrektur, um OCR‑Fehler zu bereinigen.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.GPUSettings;
import com.aspose.ocr.spell.SpellCorrectionOptions;

public class EngineConfig {
    public static OcrEngine createEngine() {
        OcrEngine ocrEngine = new OcrEngine();

        // Use all available logical processors
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Enable GPU – huge speedup for large batches
        GPUSettings gpu = new GPUSettings();
        gpu.setEnabled(true);
        ocrEngine.setGpuSettings(gpu);

        // Light spell correction: fix common typos without over‑correcting
        SpellCorrectionOptions spellOpts = new SpellCorrectionOptions();
        spellOpts.setMaxEditDistance(1);
        ocrEngine.getSpellCorrection().setOptions(spellOpts);

        return ocrEngine;
    }
}
```

*Pro‑Tipp*: Wenn Sie auf einem headless Server ohne GPU laufen, setzen Sie einfach `gpu.setEnabled(false)` – der Code funktioniert weiterhin, nur etwas langsamer.

---

## Schritt 3: Bildvorverarbeitungspipeline aufbauen

Rohscans leiden häufig unter Rauschen, geringem Kontrast oder ungleichmäßiger Beleuchtung. **Bildvorverarbeitung für OCR** verbessert die Erkennungsraten dramatisch, besonders bei **JPG‑Dateien mit Text**.

```java
import com.aspose.ocr.*;

public class PreprocessorSetup {
    public static ImagePreprocessor createPreprocessor() {
        return new ImagePreprocessor.Builder()
                .addDenoise(0.7)      // Reduce grain while preserving edges
                .addContrast(1.15)    // Boost contrast for clearer glyphs
                .addBinarize()        // Convert to black‑and‑white for OCR
                .build();
    }
}
```

*Warum wir das so verketten*: Das Rauschentfernen zuerst verhindert, dass der Binärisierer die Störpunkte verstärkt; anschließend sorgt der Kontrast dafür, dass die Zeichen hervorstechen; schließlich liefert die Binarisierung dem OCR‑Engine ein sauberes Binärbild.

---

## Schritt 4: PDF‑Speicheroptionen vorbereiten – **PDF‑Bilder effizient komprimieren**

Aspose ermöglicht feine Einstellungen der PDF‑Ausgabe. Wir aktivieren die Bildkompression und setzen einen Qualitätswert, der Größe und Lesbarkeit ausbalanciert.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOptions {
    public static PdfSaveOptions createOptions() {
        PdfSaveOptions options = new PdfSaveOptions();
        options.setCompressImages(true);   // This is the key to compress PDF images
        options.setImageQuality(90);       // 90% retains sharp text while shrinking file size
        return options;
    }
}
```

*Ergebnis*: Jede durchsuchbare PDF ist merklich kleiner – ideal für Archivierung oder Versand per E‑Mail.

---

## Schritt 5: Ordner verarbeiten – **PNG zu PDF konvertieren** und **JPG‑Dateien mit Text** in einer Schleife erkennen

Jetzt fügen wir alles zusammen. Die Schleife durchläuft ein Eingabeverzeichnis, führt OCR für jedes PNG oder JPG aus und schreibt eine durchsuchbare PDF in einen Ausgabepfad. Der PDF‑Name spiegelt den Namen der Quellbilddatei wider.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.PdfSaveOptions;
import java.io.File;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license
        LicenseSetup.loadLicense();

        // 2️⃣ Engine & preprocessing
        OcrEngine ocrEngine = EngineConfig.createEngine();
        ocrEngine.setPreprocessor(PreprocessorSetup.createPreprocessor());

        // 3️⃣ PDF options (compress PDF images)
        PdfSaveOptions pdfOptions = PdfOptions.createOptions();

        // 4️⃣ Define input / output folders
        File inputFolder = new File("YOUR_DIRECTORY/input");
        File outputFolder = new File("YOUR_DIRECTORY/output");
        if (!outputFolder.exists()) outputFolder.mkdirs();

        // 5️⃣ Filter PNG & JPG files
        File[] imageFiles = inputFolder.listFiles((dir, name) ->
                name.toLowerCase().endsWith(".png") || name.toLowerCase().endsWith(".jpg"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG or JPG files found in the input folder.");
            return;
        }

        // 6️⃣ Process each file
        for (File image : imageFiles) {
            // Recognize text – works for both PNG and JPG
            ocrEngine.recognizeImage(image.getAbsolutePath());

            // Build output PDF path (same base name)
            String pdfPath = outputFolder.getAbsolutePath() + File.separator +
                    image.getName().replaceAll("\\.(png|jpg)$", ".pdf");

            // Save as searchable PDF – this step also compresses images
            ocrEngine.saveAsSearchablePdf(pdfPath, pdfOptions);

            System.out.println("✅ Processed: " + image.getName() + " → " + pdfPath);
        }

        System.out.println("🎉 All files have been converted and compressed!");
    }
}
```

### Erwartete Ausgabe

Beim Ausführen des Programms wird für jedes Bild eine Zeile ausgegeben, z. B.:

```
✅ Processed: invoice1.png → /output/invoice1.pdf
✅ Processed: receipt23.jpg → /output/receipt23.pdf
🎉 All files have been converted and compressed!
```

Öffnen Sie eine der erzeugten PDFs in einem Viewer und Sie sehen auswählbaren, durchsuchbaren Text, während die Dateigröße typischerweise **30‑50 % kleiner** ist als bei einer nicht komprimierten Gegenstück‑PDF.

---

## Häufige Fragen & Sonderfälle

### Was, wenn mein Server keine GPU hat?
Setzen Sie einfach `gpuSettings.setEnabled(false)`. Der Rest der Pipeline bleibt unverändert, und Sie erhalten weiterhin eine mehr‑threadige CPU‑Verarbeitung.

### Meine PDFs sind immer noch zu groß – kann ich die Qualität weiter senken?
Ja. Passen Sie `options.setImageQuality(70)` oder sogar `50` an. Niedrigere Werte reduzieren die Größe aggressiver, können jedoch feine Glyphen verwischen. Testen Sie mit einer repräsentativen Stichprobe.

### Wie gehe ich mit anderen Bildformaten (TIFF, BMP) um?
Fügen Sie die Erweiterungen zur Filter‑Lambda hinzu:

```java
name.toLowerCase().endsWith(".png") ||
name.toLowerCase().endsWith(".jpg") ||
name.toLowerCase().endsWith(".tif") ||
name.toLowerCase().endsWith(".bmp")
```

Die gleiche Vorverarbeitungspipeline funktioniert für die meisten Rasterformate.

### Kann ich die Original‑Farbbilder behalten statt zu binarisieren?
Ersetzen Sie `.addBinarize()` durch `.addGrayscale()` im Preprocessor‑Builder, falls Sie Farbinformationen für nachgelagerte Analysen benötigen.

---

## Pro‑Tipps für produktionsreife Batch‑OCR

- **Speichermanagement**: Wiederverwenden einer einzelnen `OcrEngine`‑Instanz (wie gezeigt), um den Overhead von Erzeugung/Zerstörung pro Bild zu vermeiden.
- **Fehlerbehandlung**: Umschließen Sie den pro‑Datei‑Block mit einem `try/catch`, um Fehler zu protokollieren, ohne den gesamten Batch abzubrechen.
- **Logging**: Verwenden Sie ein richtiges Logging‑Framework (SLF4J, Log4j) anstelle von `System.out.println` für skalierbare Lösungen.
- **Parallelität**: Bei riesigen Ordnern können Sie Unterverzeichnisse in parallelen Streams verarbeiten, achten Sie jedoch auf GPU‑Konkurrenz.
- **Sicherheit**: Lagern Sie die Lizenzdatei außerhalb des Repositories und schützen Sie sie mit Dateisystem‑Berechtigungen.

---

## Fazit

Wir haben gezeigt, wie man **PDF‑Bilder komprimiert**, während man eine **Batch‑OCR‑zu‑PDF**‑Konvertierung durchführt, die **PNG zu PDF** konvertiert, **JPG‑Dateien mit Text** erkennt und eine robuste **Bildvorverarbeitung für OCR**‑Pipeline anwendet. Das vollständige Java‑Programm ist eigenständig, läuft auf jeder modernen JDK und erzeugt leichte, durchsuchbare PDFs, die sich zum Archivieren oder für nachgelagerte Analysen eignen.

Nächste Schritte? Experimentieren Sie mit verschiedenen Vorverarbeitungsparametern, probieren Sie OCR‑Sprachen neben Englisch aus oder integrieren Sie den Workflow in einen Spring‑Boot‑Microservice, der ein Verzeichnis überwacht und Dateien on‑the‑fly verarbeitet. Die Kernkonzepte – Lizenz laden, Engine konfigurieren, Vorverarbeitung und PDF‑Kompression – bleiben gleich und bieten Ihnen ein solides Fundament für jedes OCR‑getriebene Projekt.

Haben Sie Fragen oder möchten eigene Optimierungen teilen? Hinterlassen Sie einen Kommentar unten, und happy coding!

![Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output](alt="Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output")

## Was Sie als Nächstes lernen sollten


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie zusätzliche API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}