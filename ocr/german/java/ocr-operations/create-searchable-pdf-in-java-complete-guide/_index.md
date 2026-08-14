---
category: general
date: 2026-07-05
description: Erstellen Sie ein durchsuchbares PDF in Java mit Aspose OCR. Erfahren
  Sie, wie Sie Bilder im PDF komprimieren, ein gescanntes Bild in ein PDF konvertieren
  und die Schriftart‑Einbettung im PDF deaktivieren, um kleinere Dateien zu erhalten.
draft: false
keywords:
- create searchable pdf
- compress images in pdf
- convert scanned image to pdf
- disable font embedding pdf
language: de
og_description: Erstellen Sie durchsuchbare PDFs in Java mit Aspose OCR. Dieses Tutorial
  zeigt, wie man Bilder in PDFs komprimiert, gescannte Bilder in PDFs konvertiert
  und das Einbetten von Schriftarten in PDFs deaktiviert.
og_title: Durchsuchbare PDF in Java erstellen – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF in Java using Aspose OCR. Learn how to compress
    images in PDF, convert scanned image to PDF, and disable font embedding PDF for
    smaller files.
  headline: Create Searchable PDF in Java – Complete Guide
  type: TechArticle
tags:
- Java
- OCR
- PDF
title: Durchsuchbare PDF in Java erstellen – Komplettanleitung
url: /de/java/ocr-operations/create-searchable-pdf-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Erstellen durchsuchbarer PDFs in Java – Komplettanleitung

Haben Sie schon einmal **durchsuchbare PDFs** aus einem gescannten Dokument erstellen müssen, wussten aber nicht, *wie*? Sie sind nicht allein. In vielen Projekten ist es ein *Must‑have*, ein TIFF oder JPEG in ein PDF zu verwandeln, das Sie tatsächlich durchsuchen können – besonders wenn Sie außerdem **Bilder im PDF komprimieren** möchten, um die Dateigröße überschaubar zu halten.  

In diesem Tutorial gehen wir Schritt für Schritt durch ein praktisches Beispiel mit Aspose OCR für Java. Am Ende wissen Sie genau, wie Sie **gescannte Bilder in PDF konvertieren**, die Einstellung **Bilder im PDF komprimieren** anpassen und sogar **Schriftart‑Einbettung im PDF deaktivieren**, um ein paar zusätzliche Kilobytes zu sparen. Kein Schnickschnack – nur eine vollständige, lauffähige Lösung, die Sie noch heute in Ihr Projekt übernehmen können.

## Was Sie lernen werden

- Das Aspose OCR‑Engine in einem Java‑Projekt einrichten.  
- OCR auf einem TIFF (oder einem beliebigen Rasterbild) ausführen.  
- `PdfSaveOptions` konfigurieren, um **Bilder im PDF zu komprimieren** und **Schriftart‑Einbettung im PDF zu deaktivieren**.  
- Das Ergebnis als **durchsuchbares PDF** speichern, das Sie sofort indexieren oder durchsuchen können.  

**Voraussetzungen**  
- Java 8 oder neuer installiert.  
- Maven oder Gradle für das Abhängigkeits‑Management (wir zeigen das Maven‑Snippet).  
- Eine gescannte Bilddatei (TIFF, PNG oder JPEG), die verarbeitet werden soll.  

Wenn Sie das haben, legen wir los.

![Erstellen durchsuchbarer PDF‑Workflow – Java OCR zu PDF‑Konvertierung](/images/create-searchable-pdf-workflow.png "Diagramm, das die Schritte zum Erstellen durchsuchbarer PDFs mit Aspose OCR zeigt")

## Schritt 1: Aspose OCR‑Abhängigkeit hinzufügen

Zuerst holen wir die Aspose OCR‑Bibliothek in Ihr Projekt. Mit Maven fügen Sie Folgendes zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Wenn Sie Gradle bevorzugen, lautet das Äquivalent:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro‑Tipp:** Behalten Sie die Aspose‑Release‑Notes im Auge; neuere Versionen bringen häufig Leistungsverbesserungen für die OCR‑Genauigkeit.

## Schritt 2: Die OCR‑Engine initialisieren

Eine OCR‑Engine zu erstellen ist so einfach wie das Instanziieren von `OcrEngine`. Dieses Objekt übernimmt alles von der Bild‑Ladung bis zur Textextraktion.

```java
import com.aspose.ocr.OcrEngine;

// ...

// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

Warum benötigen wir eine dedizierte Engine? Aspose trennt das schwere Heben (Bildvorverarbeitung, Sprachmodelle) vom Rest Ihrer Anwendung, sodass Sie dieselbe `engine` über mehrere Dateien hinweg wiederverwenden können, ohne schwere Ressourcen neu zu initialisieren.

## Schritt 3: OCR auf dem gescannten Bild ausführen

Jetzt übergeben wir der Engine eine gescannte Datei. Die Methode `recognizeImage` liefert ein `RecognitionResult`, das den extrahierten Text und Layout‑Informationen enthält.

```java
import com.aspose.ocr.RecognitionResult;

// ...

// Step 3: Perform OCR on the source image
String sourcePath = "YOUR_DIRECTORY/document_scan.tif"; // could be .png or .jpg too
RecognitionResult result = engine.recognizeImage(sourcePath);
```

> **Was, wenn das Bild kein TIFF ist?**  
> Aspose OCR erkennt automatisch gängige Rasterformate, sodass Sie es einfach auf ein JPEG, PNG oder BMP zeigen können, ohne den Code zu ändern.

## Schritt 4: PDF‑Speicheroptionen konfigurieren (Bilder komprimieren & Schriftart‑Einbettung deaktivieren)

Hier kommen die sekundären Schlüsselwörter ins Spiel. Wir sagen Aspose, **Bilder im PDF zu komprimieren** und **Schriftart‑Einbettung im PDF zu deaktivieren**. Beide Einstellungen reduzieren die endgültige Dateigröße – praktisch, wenn Sie Dutzende Dokumente ausliefern.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

// ...

// Step 4: Set up PDF save options
PdfSaveOptions pdfOpts = new PdfSaveOptions();

// Reduce PDF size by compressing images
pdfOpts.setCompressImages(true);
pdfOpts.setImageQuality(80); // 0‑100, 80 is a good balance

// Prevent fonts from being embedded – saves a few KB per page
pdfOpts.setEmbedFonts(false);
```

**Warum Bilder komprimieren?**  
Gescannte Seiten sind oft hochauflösend; eine Komprimierung auf 80 % Qualität kann ein 10‑seitiges PDF von 12 MB auf unter 3 MB schrumpfen lassen, ohne merklichen visuellen Qualitätsverlust.

**Warum Schriftart‑Einbettung deaktivieren?**  
Verwendet die OCR‑Engine Standardsystem‑Schriften (wie Arial oder Times New Roman), ist das Einbetten überflüssig. Das Ausschalten reduziert die Dateigröße weiter, besonders bei großen Stapeln.

## Schritt 5: OCR‑Ergebnis als durchsuchbares PDF speichern

Der letzte Schritt fügt alles zusammen: das Rohbild, die extrahierte Textebene und die gerade gesetzten PDF‑Optionen.

```java
// Step 5: Save the OCR result as a searchable PDF
String outputPath = "YOUR_DIRECTORY/document.pdf";
engine.saveAsSearchablePdf(outputPath, pdfOpts);

System.out.println("Searchable PDF created at: " + outputPath);
```

Wenn Sie `document.pdf` in Adobe Reader oder einem modernen Viewer öffnen, sehen Sie das ursprüngliche gescannte Bild **plus** eine unsichtbare Textebene. Gibt man ein Wort in das Suchfeld ein, wird es hervorgehoben – genau das, was „durchsuchbares PDF erstellen“ verspricht.

### Erwartete Ausgabe

Ein Lauf des Programms mit einem gültigen TIFF liefert etwa Folgendes:

```
Searchable PDF created at: YOUR_DIRECTORY/document.pdf
```

Öffnen Sie das PDF, drücken Sie `Strg+F`, tippen Sie ein Wort, das auf der gescannten Seite vorkommt, und sehen Sie, wie es zur richtigen Stelle springt. Das ist das Markenzeichen eines erfolgreichen **create searchable pdf**‑Workflows.

## Häufige Stolperfallen & wie man sie vermeidet

| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| **Leeres PDF** | `PdfSaveOptions` nicht an `saveAsSearchablePdf` übergeben. | Stellen Sie sicher, dass Sie die Überladung verwenden, die `PdfSaveOptions` akzeptiert. |
| **Kauderwelsch‑Zeichen** | OCR‑Sprache nicht gesetzt (Standard ist Englisch). | Verwenden Sie `engine.getLanguage().setLanguage(OcrLanguage.FRENCH);` vor `recognizeImage`. |
| **Riesige Dateigröße** | `setCompressImages(false)` oder `setEmbedFonts(true)`. | Lassen Sie beide Flags wie oben gezeigt auf `true`/`false`. |
| **Bildverzerrung** | `setImageQuality` zu niedrig eingestellt (<50). | Bleiben Sie bei 70‑90 für ein gutes Gleichgewicht. |

## Erweiterung des Beispiels

Jetzt, wo Sie **gescannte Bilder in PDF konvertieren** und die Größe steuern können, möchten Sie vielleicht:

- **Stapelverarbeitung** eines Ordners mit Scans mittels einer einfachen `for(File f : folder.listFiles())`‑Schleife.  
- **Wasserzeichen** hinzufügen mit Aspose PDF (`PdfDocument.addWatermarkText`).  
- Den OCR‑Text in eine **plain .txt**‑Datei exportieren für Indexierungssysteme (`result.getText().writeToFile("doc.txt")`).  

All diese Erweiterungen nutzen dieselbe `OcrEngine`‑Instanz und halten den Speicherverbrauch gering.

## Vollständiger, lauffähiger Code

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Perform OCR on the source image
        String source = "YOUR_DIRECTORY/document_scan.tif";
        RecognitionResult result = engine.recognizeImage(source);

        // Step 3: Configure PDF save options (compress images & disable fonts)
        PdfSaveOptions pdfOpts = new PdfSaveOptions();
        pdfOpts.setCompressImages(true);      // Reduce PDF size by compressing images
        pdfOpts.setImageQuality(80);          // Image quality (0‑100)
        pdfOpts.setEmbedFonts(false);         // Do not embed fonts to keep file size small

        // Step 4: Save the OCR result as a searchable PDF
        String output = "YOUR_DIRECTORY/document.pdf";
        engine.saveAsSearchablePdf(output, pdfOpts);

        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF created at: " + output);
    }
}
```

Kopieren Sie das in Ihre IDE, ersetzen Sie `YOUR_DIRECTORY` durch einen echten Pfad und starten Sie das Programm. Wenn alles korrekt eingerichtet ist, erhalten Sie ein **durchsuchbares PDF**, das dank Bildkomprimierung und deaktivierter Schriftart‑Einbettung zudem leichtgewichtig ist.

## Fazit

Wir haben alles behandelt, was Sie benötigen, um **durchsuchbare PDFs** in Java mit Aspose OCR zu erstellen. Vom Initialisieren der Engine, über die OCR‑Ausführung, das Anpassen von **Bilder im PDF komprimieren** und **Schriftart‑Einbettung im PDF deaktivieren**, bis hin zum Speichern eines durchsuchbaren Dokuments – jeder Schritt wurde mit dem *Warum* dahinter erklärt.  

Bereit für die nächste Herausforderung? Probieren Sie OCR‑Sprachpakete, Stapel‑Verarbeitung ganzer Ordner oder das Hinzufügen von Anmerkungen zu PDFs. Die Grundlagen, die Sie gerade gemeistert haben, machen diese Erweiterungen zum Kinderspiel.

Haben Sie Fragen oder möchten Ihre eigenen Tricks teilen? Hinterlassen Sie einen Kommentar unten, und happy coding!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [PDF‑Text erkennen – OCR‑Operationen mit Aspose.OCR für Java](/ocr/english/java/ocr-operations/)
- [OCR‑Erkennung von PDF‑Dokumenten in Aspose.OCR für Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Wie man PDF in .NET mit Aspose.OCR OCR‑verarbeitet](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}