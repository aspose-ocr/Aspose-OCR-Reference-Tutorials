---
category: general
date: 2026-07-21
description: Tekst extraheren uit een afbeelding met Java OCR. Leer hoe je PNG naar
  tekst converteert, tekst uit PNG leest, afbeelding laadt voor OCR en OCR op een
  afbeelding uitvoert in slechts een paar stappen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: nl
lastmod: 2026-07-21
og_description: Tekst extraheren uit afbeelding met Java. Deze gids laat zien hoe
  je PNG naar tekst converteert, tekst uit PNG leest, afbeelding laadt voor OCR, en
  efficiënt OCR op een afbeelding uitvoert.
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: Tekst uit afbeelding extraheren in Java – Stapsgewijze OCR‑tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  headline: Extract Text from Image in Java – Complete OCR Guide
  type: TechArticle
- description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  name: Extract Text from Image in Java – Complete OCR Guide
  steps:
  - name: Low‑Quality Images
    text: 'If the PNG is blurry or has low contrast, OCR accuracy drops. A quick fix
      is to pre‑process the image:'
  - name: Multi‑Language Support
    text: Tess4J can handle many languages. Just download the appropriate `.traineddata`
      file and point `tesseract.setLanguage("spa")` for Spanish, for example.
  - name: Large PDFs or Multi‑Page Images
    text: If you need to **extract text from image** files inside a PDF, split each
      page into PNGs first (using PDFBox) and then feed each PNG to the same OCR routine.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Tekst uit afbeelding extraheren in Java – Complete OCR-gids
url: /nl/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst uit afbeelding halen in Java – Complete OCR-gids

Heb je ooit **tekst uit afbeelding** moeten halen maar wist je niet welke Java‑bibliotheek je moest kiezen? Je bent niet de enige. Of je nu bonnen digitaliseert, PDF‑bestanden scant, of een doorzoekbaar archief bouwt, tekst uit een PNG halen is een dagelijks pijnpunt voor veel ontwikkelaars.

In deze tutorial lopen we een praktische oplossing door die je in staat stelt **PNG naar tekst converteren**, **tekst uit PNG lezen**, **afbeelding laden voor OCR**, en **OCR op afbeelding uitvoeren**—alles met een paar regels nette Java‑code. Aan het einde heb je een uitvoerbaar programma dat je in elk project kunt gebruiken.

## Wat je gaat bouwen

We’ll create a small Java console app that:

1. Laadt een PNG‑bestand van de schijf.  
2. Stuur de afbeelding naar een OCR‑engine (Tess4J, een Java‑wrapper voor Tesseract).  
3. Print de herkende tekst naar de console.

Geen externe services, geen magie—alleen pure Java en een open‑source OCR‑engine.

## Vereisten

- **Java 17** of later (de code compileert met oudere versies, maar Java 17 biedt de nieuwste taalfeatures).  
- **Maven** of **Gradle** voor afhankelijkheidsbeheer.  
- Een voorbeeld‑PNG met de naam `sample.png` geplaatst in een map die je kunt refereren (bijv. `src/main/resources`).  
- Basiskennis van Java’s `main`‑methode en exception‑handling.

Als een van deze onbekend klinkt, maak je geen zorgen—elke stap bevat een korte samenvatting.

## Stap 1: Het project opzetten en de OCR‑bibliotheek toevoegen

Maak eerst een nieuw Maven‑project aan (of Gradle als je dat liever hebt). Voeg de Tess4J‑dependency toe, die de Tesseract‑binaries voor je levert.

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Tess4J – Java wrapper for Tesseract OCR -->
        <dependency>
            <groupId>net.sourceforge.tess4j</groupId>
            <artifactId>tess4j</artifactId>
            <version>5.5.1</version>
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** Als je Gradle gebruikt, is de equivalente regel `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'`.

Door deze bibliotheek toe te voegen krijg je de `Tesseract`‑klasse, die het zware werk doet van **OCR op afbeelding uitvoeren** data.

## Stap 2: Afbeelding laden voor OCR

Nu moeten we **afbeelding laden voor OCR**. Tess4J werkt met `java.awt.image.BufferedImage`, dus we lezen de PNG met `ImageIO`.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class OcrDemo {

    /**
     * Loads a PNG file from the given path and returns a BufferedImage.
     *
     * @param path absolute or relative path to the PNG file
     * @return BufferedImage containing the image data
     * @throws IOException if the file cannot be read
     */
    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image to be recognized
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }
```

De bovenstaande methode isoleert duidelijk de **afbeelding laden voor OCR**‑logica, waardoor de rest van de code makkelijker te testen is. Let op de commentaar – deze spiegelt de originele snippet terwijl hij voor duidelijkheid wordt uitgebreid.

## Stap 3: OCR op afbeelding uitvoeren

Met de afbeelding in het geheugen kunnen we nu **OCR op afbeelding uitvoeren**. De `Tesseract`‑instance is onze engine; we configureren deze om de standaard Engelse taaldata te gebruiken die met Tess4J wordt meegeleverd.

```java
    /**
     * Runs OCR on the supplied BufferedImage and returns the extracted text.
     *
     * @param image the image to analyze
     * @return plain text recognized from the image
     * @throws TesseractException if the OCR process fails
     */
    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();

        // Optional: set the datapath if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");

        // Step 4: Run OCR and capture the recognized text
        return tesseract.doOCR(image);
    }
```

Hier hebben we de originele “Stap 1” en “Stap 4” samengevoegd tot één methode, omdat het `Tesseract`‑object goedkoop is om te maken en we de code compact willen houden. De commentaar verwijst nog steeds naar de originele stappen voor traceerbaarheid.

## Stap 4: Alles samenvoegen – Main‑methode

Tot slot brengen we alles samen in `main`. Hier ga je **tekst uit PNG lezen** en zie je het resultaat naar de console geprint.

```java
    public static void main(String[] args) {
        // Adjust the path to point at your PNG file
        String imagePath = "src/main/resources/sample.png";

        try {
            // Load the PNG image
            BufferedImage image = loadImage(imagePath);

            // Extract text from the image
            String recognizedText = extractText(image);

            // Step 5: Display the extracted text
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR error: " + e.getMessage());
        }
    }
}
```

Wanneer je `mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"` uitvoert (of het Gradle‑equivalent), zou je iets moeten zien als:

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

Die output bewijst dat je succesvol **tekst uit afbeelding hebt gehaald**, **PNG naar tekst hebt geconverteerd**, en **tekst uit PNG hebt gelezen** in één net programma.

## Veelvoorkomende randgevallen afhandelen

### Lage‑kwaliteit afbeeldingen

Als de PNG onscherp is of een laag contrast heeft, daalt de OCR‑nauwkeurigheid. Een snelle oplossing is om de afbeelding voor te verwerken:

```java
// Example: Convert to grayscale and apply a binary threshold
BufferedImage gray = new BufferedImage(
        image.getWidth(), image.getHeight(),
        BufferedImage.TYPE_BYTE_GRAY);
Graphics2D g = gray.createGraphics();
g.drawImage(image, 0, 0, null);
g.dispose();

// Simple binary threshold
for (int y = 0; y < gray.getHeight(); y++) {
    for (int x = 0; x < gray.getWidth(); x++) {
        int rgb = gray.getRGB(x, y) & 0xFF;
        int binary = rgb < 128 ? 0x000000 : 0xFFFFFF;
        gray.setRGB(x, y, binary);
    }
}
String text = extractText(gray);
```

### Meertalige ondersteuning

Tess4J kan veel talen aan. Download gewoon het juiste `.traineddata`‑bestand en stel `tesseract.setLanguage("spa")` in voor Spaans, bijvoorbeeld.

### Grote PDF‑s of meer‑pagina afbeeldingen

Als je **tekst uit afbeelding**‑bestanden binnen een PDF moet halen, splits dan eerst elke pagina in PNG‑s (met PDFBox) en voer vervolgens elke PNG in dezelfde OCR‑routine.

## Volledig werkend voorbeeld (Alle code op één plek)

Hieronder staat de volledige, klaar‑om‑te‑runnen Java‑klasse. Kopieer‑en‑plak deze in `src/main/java/com/example/ocrdemo/OcrDemo.java` en je bent klaar om te gaan.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Demonstrates how to extract text from image (PNG) using Java and Tess4J.
 */
public class OcrDemo {

    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image for OCR
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }

    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();
        // Uncomment and set if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");
        // Step 4: Perform OCR on image
        return tesseract.doOCR(image);
    }

    public static void main(String[] args) {
        // Path to the PNG you want to convert to text
        String imagePath = "src/main/resources/sample.png";

        try {
            BufferedImage image = loadImage(imagePath);
            String recognizedText = extractText(image);
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("Error during OCR: " + e.getMessage());
        }
    }
}
```

Het uitvoeren van de klasse print het OCR‑resultaat, wat bevestigt dat je succesvol **OCR op afbeelding hebt uitgevoerd** en je PNG hebt omgezet naar bewerkbare tekst.

## Samenvatting & volgende stappen

We begonnen met **tekst uit afbeelding halen** met een lichte Java‑opzet. Je weet nu hoe je **afbeelding laden voor OCR**, **OCR op afbeelding uitvoeren**, en **tekst uit PNG lezen**—essentiële bouwstenen voor elke document‑digitaliserings‑pipeline.

Wil je verder gaan? Probeer deze ideeën:

- **Batchverwerking:** Loop over een map met PNG‑s en schrijf elk resultaat naar een `.txt`‑bestand.  
- **Integreren met een database:** Sla geëxtraheerde strings op naast metadata voor doorzoekbare archieven.  
- **Combineren met NLP:** Voer de OCR‑output in een sentiment‑analyse model voor snelle inzichten.  

Elk van die uitbreidingen bouwt voort op dezelfde kernconcepten die we hebben behandeld, dus je bent klaar om te experimenteren.

---

*Veel plezier met coderen! Als je ergens tegenaan loopt

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Tekst uit afbeelding halen Java met Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [afbeelding naar tekst java: Afbeelding naar tekst converteren met Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Hoe OCR‑tekst van afbeelding met taal gebruiken met Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}