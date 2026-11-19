---
category: general
date: 2026-06-16
description: Leer hoe je OCR op afbeeldingsbestanden in Java uitvoert. Deze tutorial
  behandelt het herkennen van tekst uit PNG, het extraheren van tekst uit een afbeelding,
  het converteren van een afbeelding naar tekst, en het laden van een afbeelding voor
  OCR.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: nl
og_description: Voer OCR uit op een afbeelding met Java. Deze gids laat zien hoe je
  tekst uit een PNG herkent, tekst uit een afbeelding extraheert en een afbeelding
  naar tekst converteert met een kant‑klaar voorbeeld.
og_title: Voer OCR uit op afbeelding in Java – Volledige programmeertutorial
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  headline: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  name: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'If `hello.png` contains the phrase “Hello, OCR world!”, the console will
      display something like:'
  - name: 5.1 Dealing with Low‑Resolution Images
    text: 'If the source PNG is blurry, OCR accuracy drops. A quick fix is to upscale
      the image before feeding it to the engine:'
  - name: 5.2 Multi‑Language Documents
    text: 'If you anticipate French or German text, simply add the language codes
      to `setLanguage`:'
  - name: 5.3 Skipping Empty Pages
    text: 'Sometimes a scanned PDF page renders as a blank PNG. Detecting an empty
      image saves processing time:'
  type: HowTo
tags:
- Java
- OCR
- Image Processing
title: Voer OCR uit op een afbeelding in Java – Complete stap‑voor‑stap gids
url: /nl/java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR uitvoeren op afbeelding in Java – Complete stapsgewijze gids

Heb je ooit **perform OCR on image** bestanden moeten verwerken maar wist je niet welke Java‑bibliotheek je moest kiezen? Je bent niet de enige. Of je nu een bonscanner bouwt, een documentarchiver, of gewoon nieuwsgierig bent naar het omzetten van afbeeldingen naar doorzoekbare tekst, leren hoe je **perform OCR on image** met Java kunt doen is een handige vaardigheid.

In deze tutorial lopen we alles door wat je nodig hebt om **perform OCR on image** bestanden te verwerken: de afbeelding laden, de engine configureren, de tekst herkennen en uiteindelijk het resultaat afdrukken. Aan het einde kun je **recognize text from PNG** bestanden, **extract text from image** bronnen, en **convert image to text** met slechts een paar regels code.

## Vereisten

- Java 17 of nieuwer (de code compileert met elke recente JDK)
- Maven geïnstalleerd (of je favoriete build‑tool)
- Basiskennis van Java‑syntaxis
- Een PNG‑bestand dat je wilt testen (we noemen het `hello.png`)

> **Pro tip:** Als je geen PNG bij de hand hebt, maak er dan een door een screenshot van willekeurige tekst te nemen en deze op te slaan als `hello.png` in een map genaamd `resources`.

## Wat we gaan bouwen

Een kleine console‑applicatie genaamd `OcrDemo` die:

1. **Loads image for OCR** – leest een PNG van de schijf.
2. **Performs OCR on image** – gebruikt de Tesseract‑engine via Tess4J.
3. **Extracts text from image** – retourneert een `String` met de herkende inhoud.
4. Drukt het resultaat af naar de console.

Laten we beginnen.

## Stap 1: Het project opzetten en Tess4J toevoegen

Maak eerst een nieuw Maven‑project aan (of Gradle als je dat verkiest). Voeg de Tess4J‑dependency toe, die de populaire Tesseract‑OCR‑engine omsluit.

```xml
<!-- pom.xml -->
<project>
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

> **Waarom Tess4J?** Het wordt actief onderhouden, werkt cross‑platform, en biedt je een nette Java‑API voor **perform OCR on image** taken.

## Stap 2: De afbeelding‑laadlogica voorbereiden

Nu schrijven we een hulpmethode die **load image for OCR**. De methode gebruikt Java’s `ImageIO` om een PNG in te lezen als een `BufferedImage`.

```java
package com.example.ocr;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Utility class responsible for loading images from the file system.
 */
public final class ImageLoader {

    private ImageLoader() { /* utility class */ }

    /**
     * Loads a PNG (or any supported format) from the given path.
     *
     * @param path absolute or relative path to the image file
     * @return BufferedImage instance ready for OCR processing
     * @throws IOException if the file cannot be read
     */
    public static BufferedImage load(String path) throws IOException {
        File imgFile = new File(path);
        if (!imgFile.exists()) {
            throw new IOException("Image file not found: " + path);
        }
        return ImageIO.read(imgFile);
    }
}
```

Merk op dat de methodenaam duidelijk de **load image for OCR** intentie weergeeft, waardoor de code zelf‑documenterend is.

## Stap 3: De OCR‑engine configureren om **Perform OCR on Image** uit te voeren

Met de afbeelding in de hand maken we een `Tesseract`‑instantie, schakelen automatische taaldetectie in, en roepen `doOCR` aan. Dit is de kern van hoe we **perform OCR on image** gegevens verwerken.

```java
package com.example.ocr;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

/**
 * Wrapper around Tess4J that abstracts the OCR workflow.
 */
public final class OcrEngine {

    private final ITesseract tesseract;

    public OcrEngine() {
        tesseract = new Tesseract();

        // Use the bundled tessdata folder (you can also point to a custom one)
        tesseract.setDatapath("tessdata");

        // Enable automatic language detection – improves accuracy across multilingual images
        tesseract.setLanguage("eng"); // fallback language
        tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
        tesseract.setPageSegMode(ITesseract.PSM_AUTO);
    }

    /**
     * Performs OCR on the supplied BufferedImage and returns the recognized text.
     *
     * @param image image to be processed
     * @return the text extracted from the image
     * @throws TesseractException if OCR fails
     */
    public String recognize(BufferedImage image) throws TesseractException {
        return tesseract.doOCR(image);
    }
}
```

> **Waarom auto‑detectie inschakelen?** Het laat de engine het beste taalmodel voor de afbeelding kiezen, wat vooral nuttig is wanneer je **convert image to text** van bronnen die Engels en andere scripts combineren.

## Stap 4: Alles samenvoegen – De hoofdapplicatie

Hier is het instappunt dat **recognize text from PNG**, **extract text from image**, en uiteindelijk het resultaat afdrukt. Dit is het volledige, uitvoerbare voorbeeld.

```java
package com.example.ocr;

import net.sourceforge.tess4j.TesseractException;
import java.awt.image.BufferedImage;
import java.io.IOException;

/**
 * Demo application that shows how to perform OCR on image files.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Path to the PNG you want to process
        String imagePath = "resources/hello.png";

        try {
            // Step 1: Load image for OCR
            BufferedImage image = ImageLoader.load(imagePath);

            // Step 2: Create OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Step 3: Perform OCR on image and retrieve the text
            String recognizedText = engine.recognize(image);

            // Step 4: Output the recognized text to the console
            System.out.println("=== Recognized Text ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR processing error: " + e.getMessage());
        }
    }
}
```

### Verwachte output

Als `hello.png` de zin “Hello, OCR world!” bevat, zal de console iets tonen als:

```
=== Recognized Text ===
Hello, OCR world!
```

De exacte output kan iets variëren afhankelijk van de beeldkwaliteit, maar je zou de tekst moeten zien die je in de PNG hebt geplaatst.

## Stap 5: Veelvoorkomende randgevallen afhandelen

### 5.1 Omgaan met lage‑resolutie afbeeldingen

Als de bron‑PNG onscherp is, daalt de OCR‑nauwkeurigheid. Een snelle oplossing is de afbeelding te vergroten voordat je deze aan de engine geeft:

```java
import java.awt.Graphics2D;
import java.awt.RenderingHints;

public static BufferedImage upscale(BufferedImage original, int factor) {
    int width = original.getWidth() * factor;
    int height = original.getHeight() * factor;
    BufferedImage scaled = new BufferedImage(width, height, original.getType());
    Graphics2D g = scaled.createGraphics();
    g.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                       RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g.drawImage(original, 0, 0, width, height, null);
    g.dispose();
    return scaled;
}
```

Roep `upscale(image, 2)` aan vóór `engine.recognize(image)` om de resultaten te verbeteren.

### 5.2 Meertalige documenten

Als je Franse of Duitse tekst verwacht, voeg dan simpelweg de taalcodes toe aan `setLanguage`:

```java
tesseract.setLanguage("eng+fra+deu");
```

De engine zal dan proberen **extract text from image** te gebruiken met de gecombineerde taalmodes.

### 5.3 Lege pagina's overslaan

Soms wordt een gescande PDF‑pagina weergegeven als een lege PNG. Het detecteren van een lege afbeelding bespaart verwerkingstijd:

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## Stap 6: De applicatie verpakken en uitvoeren

1. **Compileer:** `mvn clean compile`
2. **Voer uit:** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

Zorg ervoor dat de `tessdata`‑map (die taalbestanden bevat) naast de gecompileerde JAR staat of specificeer het absolute pad in `OcrEngine`.

## Conclusie

Je hebt nu een solide, productie‑klaar patroon om **perform OCR on image** bestanden te verwerken met Java. Van **loading image for OCR** tot **recognize text from PNG**, we hebben behandeld hoe je **extract text from image**, **convert image to text** kunt doen, en hoe je lastige scenario's zoals lage‑resolutie scans of meertalige inhoud aanpakt.

Volgende stappen die je kunt verkennen:

- **Batchverwerking** – loop over een map met PNG‑bestanden en schrijf elk resultaat naar een `.txt`‑bestand.
- **PDF‑generatie** – embed de geëxtraheerde tekst terug in doorzoekbare PDF‑bestanden.
- **Cloud‑OCR‑services** – vergelijk de lokale Tesseract‑prestaties met API’s zoals Google Vision of Azure Cognitive Services.

Voel je vrij om te experimenteren, de parameters aan te passen, en je bevindingen te delen. Veel plezier met coderen, en moge je afbeeldingen altijd omgezet worden in schone, doorzoekbare tekst! 

![Diagram dat de OCR-werkstroom toont om OCR op afbeelding uit te voeren](https://example.com/ocr-workflow.png "voorbeeld van OCR op afbeelding")

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [tekstafbeelding herkennen met Aspose OCR – Volledige Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Afbeelding naar tekst converteren in Java met Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Tekst extraheren uit afbeelding Java met Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}