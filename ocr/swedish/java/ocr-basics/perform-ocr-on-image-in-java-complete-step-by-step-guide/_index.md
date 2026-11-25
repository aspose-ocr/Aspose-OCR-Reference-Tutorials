---
category: general
date: 2026-06-16
description: Lär dig hur du utför OCR på bildfiler i Java. Denna handledning täcker
  att känna igen text från PNG, extrahera text från bild, konvertera bild till text
  och ladda bild för OCR.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: sv
og_description: Utför OCR på bild med Java. Denna guide visar hur man känner igen
  text från PNG, extraherar text från bild och konverterar bild till text med ett
  färdigt exempel som kan köras direkt.
og_title: Utför OCR på bild i Java – Fullständig programmeringshandledning
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
title: Utför OCR på bild i Java – Komplett steg‑för‑steg‑guide
url: /sv/java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utför OCR på bild i Java – Komplett steg‑för‑steg guide

Har du någonsin behövt **utföra OCR på bild**-filer men varit osäker på vilket Java‑bibliotek du ska välja? Du är inte ensam. Oavsett om du bygger en kvittescanner, ett dokumentarkiv eller bara är nyfiken på att omvandla bilder till sökbar text, är det en praktisk färdighet att lära sig hur man **utför OCR på bild** med Java.

I den här handledningen går vi igenom allt du behöver för att **utföra OCR på bild**-filer: ladda bilden, konfigurera motorn, känna igen texten och slutligen skriva ut resultatet. När du är klar kommer du kunna **igenkänna text från PNG**‑filer, **extrahera text från bild**‑källor och **konvertera bild till text** med bara några rader kod.

## Förutsättningar

- Java 17 eller nyare (koden kompileras med vilken recent JDK som helst)
- Maven installerat (eller ditt föredragna byggverktyg)
- Grundläggande kunskap om Java‑syntax
- En PNG‑fil du vill testa (vi kallar den `hello.png`)

> **Proffstips:** Om du inte har en PNG till hands, skapa en genom att ta en skärmbild av någon text och spara den som `hello.png` i en mapp som heter `resources`.

## Vad vi kommer att bygga

En liten konsolapplikation med namnet `OcrDemo` som:

1. **Laddar bild för OCR** – läser en PNG från disk.
2. **Utför OCR på bild** – använder Tesseract‑motorn via Tess4J.
3. **Extraherar text från bild** – returnerar en `String` med den igenkända innehållet.
4. Skriver ut resultatet till konsolen.

Låt oss dyka ner.

## Steg 1: Ställ in projektet och lägg till Tess4J

Först, skapa ett nytt Maven‑projekt (eller Gradle om du föredrar). Lägg till Tess4J‑beroendet, som omsluter den populära Tesseract‑OCR‑motorn.

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

> **Varför Tess4J?** Det underhålls aktivt, fungerar på flera plattformar och ger dig ett rent Java‑API för **utföra OCR på bild**‑uppgifter.

## Steg 2: Förbered logiken för bildladdning

Nu skriver vi en hjälpfunktion som **laddar bild för OCR**. Metoden använder Javas `ImageIO` för att läsa en PNG till en `BufferedImage`.

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

Observera att metodnamnet tydligt återspeglar avsikten **ladda bild för OCR**, vilket gör koden själv‑dokumenterande.

## Steg 3: Konfigurera OCR‑motorn för att **utföra OCR på bild**

Med bilden i handen skapar vi en `Tesseract`‑instans, aktiverar automatisk språkdetection och anropar `doOCR`. Detta är kärnan i hur vi **utför OCR på bild**‑data.

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

> **Varför aktivera auto‑detect?** Det låter motorn välja den bästa språkmodellen för bilden, vilket är särskilt användbart när du **konverterar bild till text** från källor som blandar engelska och andra skript.

## Steg 4: Sätt ihop allt – Huvudapplikationen

Här är startpunkten som **igenkänner text från PNG**, **extraherar text från bild**, och slutligen skriver ut resultatet. Detta är det kompletta, körbara exemplet.

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

### Förväntad utskrift

Om `hello.png` innehåller frasen “Hello, OCR world!”, kommer konsolen att visa något liknande:

```
=== Recognized Text ===
Hello, OCR world!
```

Det exakta resultatet kan variera något beroende på bildkvalitet, men du bör se den text du placerade i PNG‑filen.

## Steg 5: Hantera vanliga kantfall

### 5.1 Hantera lågupplösta bilder

Om käll‑PNG‑filen är suddig minskar OCR‑noggrannheten. En snabb lösning är att förstora bilden innan den matas in i motorn:

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

Anropa `upscale(image, 2)` innan `engine.recognize(image)` för att förbättra resultatet.

### 5.2 Flerspråkiga dokument

Om du förväntar dig fransk eller tysk text, lägg bara till språk‑koderna i `setLanguage`:

```java
tesseract.setLanguage("eng+fra+deu");
```

Motorn kommer då att försöka **extrahera text från bild** med de kombinerade språkmodellerna.

### 5.3 Hoppa över tomma sidor

Ibland renderas en skannad PDF‑sida som en tom PNG. Att upptäcka en tom bild sparar behandlingstid:

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## Steg 6: Paketering och körning av applikationen

- **Kompilera:** `mvn clean compile`
- **Kör:** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

Se till att `tessdata`‑mappen (som innehåller språkfiler) ligger bredvid den kompilerade JAR‑filen eller ange dess absoluta sökväg i `OcrEngine`.

## Slutsats

Du har nu ett robust, produktionsklart mönster för att **utföra OCR på bild**‑filer med Java. Från **laddar bild för OCR** till **igenkänna text från PNG**, har vi gått igenom hur man **extraherar text från bild**, **konverterar bild till text**, och hanterar knepiga scenarier som lågupplösta skanningar eller flerspråkigt innehåll.

Sedan kan du utforska:

- **Batch‑behandling** – loopa över en katalog med PNG‑filer och skriv varje resultat till en `.txt`‑fil.
- **PDF‑generering** – bädda in den extraherade texten tillbaka i sökbara PDF‑filer.
- **Moln‑OCR‑tjänster** – jämför lokal Tesseract‑prestanda med API:er som Google Vision eller Azure Cognitive Services.

Känn dig fri att experimentera, justera parametrarna och dela dina resultat. Lycka till med kodandet, och må dina bilder alltid förvandlas till ren, sökbar text! 

![Diagram som visar OCR‑arbetsflödet för att utföra OCR på bild](https://example.com/ocr-workflow.png "exempel på att utföra OCR på bild")

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [igenkänna text bild med Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Konvertera bild till text i Java med Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Extrahera text från bild Java med Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}