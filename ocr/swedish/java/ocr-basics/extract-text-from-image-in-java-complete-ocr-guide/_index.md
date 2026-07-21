---
category: general
date: 2026-07-21
description: Extrahera text från bild med Java OCR. Lär dig hur du konverterar PNG
  till text, läser text från PNG, laddar bild för OCR och utför OCR på bilden på bara
  några steg.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: sv
lastmod: 2026-07-21
og_description: Extrahera text från bild med Java. Denna guide visar hur du konverterar
  PNG till text, läser text från PNG, laddar bild för OCR och utför OCR på bilden
  effektivt.
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: Extrahera text från bild i Java – Steg‑för‑steg OCR‑handledning
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
title: Extrahera text från bild i Java – Komplett OCR‑guide
url: /sv/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från bild i Java – Komplett OCR‑guide

Har du någonsin behövt **extrahera text från bild** men varit osäker på vilket Java‑bibliotek du ska välja? Du är inte ensam. Oavsett om du digitaliserar kvitton, skannar PDF‑filer eller bygger ett sökbart arkiv, är det en daglig smärta för många utvecklare att dra ut text från en PNG.

I den här handledningen går vi igenom en praktisk lösning som låter dig **konvertera PNG till text**, **läsa text från PNG**, **ladda bild för OCR** och **utföra OCR på bild** — allt med några rader ren Java‑kod. I slutet har du ett körbart program som du kan lägga in i vilket projekt som helst.

## Vad du kommer att bygga

Vi kommer att skapa en liten Java‑konsolapp som:

1. Laddar en PNG‑fil från disk.  
2. Skickar bilden till en OCR‑motor (Tess4J, ett Java‑wrapper för Tesseract).  
3. Skriver ut den igenkända texten till konsolen.

Inga externa tjänster, ingen magi — bara ren Java och en öppen källkods‑OCR‑motor.

## Förutsättningar

- **Java 17** eller senare (koden kompilerar även med äldre versioner, men Java 17 ger dig de senaste språkfunktionerna).  
- **Maven** eller **Gradle** för beroendehantering.  
- En exempel‑PNG med namnet `sample.png` placerad i en mapp du kan referera till (t.ex. `src/main/resources`).  
- Grundläggande kunskap om Javas `main`‑metod och undantagshantering.

Om någon av dessa är obekanta, oroa dig inte — varje steg innehåller en snabb genomgång.

## Steg 1: Ställ in projektet och lägg till OCR‑biblioteket

Först, skapa ett nytt Maven‑projekt (eller Gradle om du föredrar det). Lägg till Tess4J‑beroendet, som automatiskt hämtar Tesseract‑binärerna åt dig.

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

> **Pro tip:** Om du använder Gradle är motsvarande rad `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'`.

Genom att lägga till detta bibliotek får du klassen `Tesseract`, som hanterar den tunga lyften för **utföra OCR på bild**‑data.

## Steg 2: Ladda bild för OCR

Nu behöver vi **ladda bild för OCR**. Tess4J arbetar med `java.awt.image.BufferedImage`, så vi läser PNG‑filen med `ImageIO`.

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

Metoden ovan isolerar tydligt logiken för **ladda bild för OCR**, vilket gör resten av koden enklare att testa. Lägg märke till kommentaren – den speglar originalsnutten men utökas för tydlighet.

## Steg 3: Utföra OCR på bild

Med bilden i minnet kan vi nu **utföra OCR på bild**. `Tesseract`‑instansen är vår motor; vi konfigurerar den att använda standard‑engelska språkdata som följer med Tess4J.

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

Här har vi slagit ihop original‑“Steg 1” och “Steg 4” till en enda metod, eftersom `Tesseract`‑objektet är billigt att skapa och vi vill hålla koden kompakt. Kommentaren refererar fortfarande till de ursprungliga stegen för spårbarhet.

## Steg 4: Sätt ihop allt – Main‑metod

Till sist samlar vi allt i `main`. Här kommer du att **läsa text från PNG** och se resultatet skrivet i konsolen.

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

När du kör `mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"` (eller motsvarande Gradle‑kommando) bör du se något liknande:

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

Detta resultat visar att du framgångsrikt har **extraherat text från bild**, **konverterat PNG till text** och **läst text från PNG** i ett enda, snyggt program.

## Hantera vanliga kantfall

### Lågt bildkvalitet

Om PNG‑filen är suddig eller har låg kontrast minskar OCR‑noggrannheten. En snabb lösning är att förbehandla bilden:

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

### Flerspråkigt stöd

Tess4J kan hantera många språk. Ladda bara ner rätt `.traineddata`‑fil och sätt `tesseract.setLanguage("spa")` för spanska, till exempel.

### Stora PDF‑filer eller flersidiga bilder

Om du behöver **extrahera text från bild**‑filer inuti en PDF, dela först varje sida i PNG‑filer (med PDFBox) och skicka sedan varje PNG till samma OCR‑rutin.

## Fullt fungerande exempel (All kod på ett ställe)

Nedan finns den kompletta, körklara Java‑klassen. Kopiera och klistra in den i `src/main/java/com/example/ocrdemo/OcrDemo.java` så är du klar.

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

När klassen körs skrivs OCR‑resultatet ut, vilket bekräftar att du har lyckats **utföra OCR på bild** och omvandlat din PNG till redigerbar text.

## Sammanfattning & nästa steg

Vi började med att **extrahera text från bild** med en lättviktig Java‑setup. Du vet nu hur du **laddar bild för OCR**, **utför OCR på bild** och **läser text från PNG** — grundläggande byggstenar för alla dokument‑digitaliseringspipelines.

Vill du gå längre? Prova dessa idéer:

- **Batch‑behandling:** Loopa igenom en katalog med PNG‑filer och skriv varje resultat till en `.txt`‑fil.  
- **Integrera med en databas:** Spara extraherade strängar tillsammans med metadata för sökbara arkiv.  
- **Kombinera med NLP:** Skicka OCR‑utdata till en sentiment‑analysmodell för snabba insikter.  

Varje av dessa utökningar bygger på samma kärnkoncept som vi täckt, så du är redo att experimentera.

---

*Happy coding! If you hit any snags

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Extrahera text från bild Java med Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [bild till text java: Konvertera bild till text med Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Hur man OCR‑läser bildtext med språk med Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}