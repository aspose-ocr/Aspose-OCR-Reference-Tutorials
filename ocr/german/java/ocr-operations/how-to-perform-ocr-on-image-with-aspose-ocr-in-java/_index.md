---
category: general
date: 2026-09-10
description: Führen Sie OCR auf Bildern mit Aspose OCR Java durch. Lernen Sie, Text
  aus JPEGs zu erkennen, Text aus Bildern zu extrahieren und Bilder effizient in Text
  umzuwandeln.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- recognize text from JPEG
- extract text from image
- convert image to text
- load image for OCR
language: de
lastmod: 2026-09-10
og_description: Führen Sie OCR auf einem Bild mit Aspose OCR Java durch. Dieses Tutorial
  zeigt, wie man Text aus JPEG erkennt, Text aus einem Bild extrahiert und das Bild
  in Text umwandelt – in wenigen Codezeilen.
og_image_alt: Screenshot of Java code that performs OCR on an image using Aspose OCR
og_title: OCR auf Bild mit Aspose OCR – Java‑Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  headline: How to perform OCR on image with Aspose OCR in Java
  type: TechArticle
- description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  name: How to perform OCR on image with Aspose OCR in Java
  steps:
  - name: Prerequisites
    text: '* Java Development Kit (JDK) 8 or later. * Maven or Gradle to manage dependencies
      (the example uses Maven). * A valid Aspose OCR for Java license (or a temporary
      evaluation key). * An image file named `sample.jpg` placed in a known directory.'
  - name: Load image for OCR
    text: '```java // Step 1: Load the image you want to process String imagePath
      = "YOUR_DIRECTORY/sample.jpg"; ImageStream imageStream = ImageStream.fromFile(imagePath);
      ```'
  - name: Create and configure the OCR engine
    text: '```java // Step 2: Create an OCR engine instance OcrEngine engine = new
      OcrEngine();'
  - name: Recognize text from JPEG
    text: '```java // Step 3: Attach the image to the engine engine.setImage(imageStream);'
  - name: Extract text from image and output
    text: '```java // Step 5: Output the recognized text System.out.println("=== Recognized
      Text ==="); System.out.println(result.getText()); ```'
  - name: Expected output
    text: 'Assuming `sample.jpg` contains the text “Hello World”, the console will
      display:'
  type: HowTo
tags:
- OCR
- Java
- Aspose
title: Wie man OCR auf einem Bild mit Aspose OCR in Java ausführt
url: /de/java/ocr-operations/how-to-perform-ocr-on-image-with-aspose-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man OCR auf Bildern mit Aspose OCR in Java durchführt

Wenn Sie **OCR auf Bild**-Dateien in einer Java-Anwendung durchführen müssen, bietet dieser Leitfaden eine vollständige, sofort einsatzbereite Lösung. Sie sehen, wie man **Text aus JPEG**-Dateien **erkennt**, **Text aus Bild**-Daten **extrahiert** und **Bild in Text umwandelt** mithilfe der modernen API von Aspose OCR.

Das Tutorial führt Sie durch jeden erforderlichen Schritt – vom Laden des Bildes bis zum Ausgeben des erkannten Textes – sodass Sie OCR-Funktionalität integrieren können, ohne nach zusätzlichen Ressourcen zu suchen. Keine externen Werkzeuge sind erforderlich, außer der Aspose OCR für Java Bibliothek.

## Was Sie erreichen werden

* **Ein Bild für OCR laden** direkt aus dem Dateisystem.  
* Aktivieren Sie die Vorverarbeitung von Aspose OCR (z. B. Rauschunterdrückung), um die Genauigkeit zu verbessern.  
* **Text aus JPEG erkennen** und andere Rasterformate.  
* **Text aus Bild extrahieren** und in die Konsole ausgeben.  
* Verstehen Sie, wie man **Bild in Text umwandelt** in einem produktionsbereiten Codebeispiel.

### Voraussetzungen

* Java Development Kit (JDK) 8 oder höher.  
* Maven oder Gradle zur Verwaltung von Abhängigkeiten (das Beispiel verwendet Maven).  
* Eine gültige Aspose OCR für Java Lizenz (oder ein temporärer Evaluierungsschlüssel).  
* Eine Bilddatei namens `sample.jpg`, die in einem bekannten Verzeichnis abgelegt ist.

> **Pro Tipp:** Verwenden Sie hochauflösende JPEGs (300 dpi oder höher) für die besten Erkennungsraten.  

## Schritt 1: Aspose OCR zu Ihrem Projekt hinzufügen

Wenn Sie Abhängigkeiten mit Maven verwalten, fügen Sie das folgende Snippet in Ihre `pom.xml` ein:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version>
</dependency>
```

Für Gradle fügen Sie hinzu:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Diese Koordinaten holen die neueste stabile Aspose OCR Bibliothek, die die später verwendeten Vorverarbeitungsfunktionen enthält.

## OCR auf Bild ausführen – Schritt für Schritt

Die folgenden Abschnitte zerlegen das komplette Programm. Jeder Block ist ein eigenständiges Stück, das Sie kopieren, einfügen und ausführen können.

### Bild für OCR laden

```java
// Step 1: Load the image you want to process
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ImageStream imageStream = ImageStream.fromFile(imagePath);
```

*Warum das wichtig ist:*  
`ImageStream.fromFile` liest die Rohbytes des JPEG und bereitet sie für die OCR-Engine vor. Die Methode funktioniert mit jedem von Aspose OCR unterstützten Rasterformat, sodass Sie das JPEG ohne Codeänderungen durch PNG oder BMP ersetzen können.

### OCR-Engine erstellen und konfigurieren

```java
// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();

// Enable preprocessing to improve accuracy (e.g., denoising)
engine.getPreprocessing().setDenoise(true);
```

*Warum das wichtig ist:*  
Instanziieren von `OcrEngine` reserviert die Kern-Erkennungs-Engine. Das Aktivieren des **denoise**-Flags entfernt visuelles Rauschen, das häufig die Zeichenerkennung beeinträchtigt, insbesondere bei gescannten JPEGs.

### Text aus JPEG erkennen

```java
// Step 3: Attach the image to the engine
engine.setImage(imageStream);

// Step 4: Perform OCR recognition
OcrResult result = engine.recognize();
```

*Warum das wichtig ist:*  
`engine.setImage` bindet die Bilddaten an die OCR-Pipeline. `engine.recognize()` führt den gesamten Erkennungsprozess aus und gibt ein `OcrResult` zurück, das den extrahierten Text und Konfidenzmetriken enthält.

### Text aus Bild extrahieren und ausgeben

```java
// Step 5: Output the recognized text
System.out.println("=== Recognized Text ===");
System.out.println(result.getText());
```

*Warum das wichtig ist:*  
`result.getText()` liefert die reine Textdarstellung des Bildinhalts. Die Ausgabe in die Konsole demonstriert, dass **Bild in Text umwandeln** erfolgreich war, und Sie können diesen String in Dateien, Datenbanken oder nachgelagerte Dienste weiterleiten.

## Vollständiges, ausführbares Beispiel

Unten finden Sie die vollständige Java-Klasse, die alle Schritte integriert. Ersetzen Sie `YOUR_DIRECTORY` durch den absoluten Pfad zu Ihrer JPEG-Datei.

```java
import com.aspose.ocr.*;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the image for OCR
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ImageStream imageStream = ImageStream.fromFile(imagePath);

        // Create and configure the OCR engine
        OcrEngine engine = new OcrEngine();
        engine.getPreprocessing().setDenoise(true); // improve accuracy

        // Attach the image and run recognition
        engine.setImage(imageStream);
        OcrResult result = engine.recognize();

        // Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### Erwartete Ausgabe

Angenommen, `sample.jpg` enthält den Text „Hello World“, dann wird die Konsole Folgendes anzeigen:

```
=== Recognized Text ===
Hello World
```

Wenn das Bild mehrere Zeilen enthält, wird jede Zeile in der Ausgabe in einer eigenen Zeile erscheinen.

## Häufige Variationen und Randfälle

| Situation                                 | Empfohlene Anpassung |
|-------------------------------------------|----------------------|
| **Niedrigauflösendes JPEG** (≤150 dpi)    | Erhöhen Sie `engine.getPreprocessing().setUpsample(true);`, damit Aspose das Bild vor der Erkennung hochskaliert. |
| **Farbiger Hintergrund** (z. B. gescannte Formulare) | Aktivieren Sie `engine.getPreprocessing().setBinarize(true);`, um das Bild in Schwarz‑Weiß zu konvertieren. |
| **Nicht‑lateinisches Skript** (z. B. Kyrillisch) | Setzen Sie die Sprache: `engine.getLanguage().setLanguage(OcrLanguage.RUSSIAN);`. |
| **Große Stapelverarbeitung**             | Verwenden Sie eine einzelne `OcrEngine`-Instanz für mehrere Bilder, um den Startaufwand zu reduzieren. |
| **Benötigen von Konfidenzwerten**        | Greifen Sie auf `result.getConfidence()` zu, um Konfidenzwerte pro Zeichen zu erhalten. |

Diese Anpassungen zeigen, wie Sie **Bild für OCR laden** unter verschiedenen Bedingungen, während Sie dennoch **OCR auf Bild zuverlässig ausführen**.

## Leistungsüberlegungen

* **Speichernutzung:** Jeder `ImageStream` hält das gesamte Bild im Speicher. Bei sehr großen Dateien (z. B. >10 MB) sollten Sie das Bild in Teilen mit `ImageStream.fromByteArray` streamen.  
* **Thread‑Sicherheit:** `OcrEngine` ist *nicht* thread‑sicher. Erstellen Sie für jeden Thread eine separate Instanz, wenn Sie OCR‑Aufgaben parallelisieren möchten.  
* **Lizenzmodus:** Der Evaluierungsmodus begrenzt die Anzahl der pro Sitzung verarbeiteten Seiten. Setzen Sie eine lizenzierte Version für Produktionslasten ein.  

## Fazit

Sie wissen jetzt, wie man **OCR auf Bild**-Dateien in Java mit Aspose OCR durchführt. Das Tutorial behandelte das Laden eines Bildes, das Aktivieren der Vorverarbeitung, das Erkennen von Text aus JPEG, das Extrahieren des Textes und das Umwandeln des Bildes in Text – alles in einem einzigen, kompakten Programm.

Ab hier können Sie verwandte Themen erkunden, wie **Text aus JPEG in großen Mengen erkennen**, die Ausgabe in einen Suchindex integrieren oder OCR mit Natural‑Language‑Processing kombinieren, um intelligentere Dokumenten‑Pipelines zu erstellen. Experimentieren Sie mit den Vorverarbeitungsoptionen, um die beste Genauigkeit für Ihre spezifischen Bildquellen zu erreichen.

--- 

*Bild, das die Codeausgabe veranschaulicht*  
![perform OCR on image Java example](image-placeholder.png){alt="OCR auf Bild mit Aspose OCR Java ausführen"}

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Text aus Bild mit Aspose OCR erkennen – Vollständiges Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Wie man Bildtext mit Sprache mittels Aspose.OCR OCR durchführt](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Bild OCR in Java mit Aspose OCR vorverarbeiten – Genauigkeit steigern & Text extrahieren](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}