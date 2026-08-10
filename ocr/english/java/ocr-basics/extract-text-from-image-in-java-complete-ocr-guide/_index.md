---
category: general
date: 2026-07-21
description: Extract text from image using Java OCR. Learn how to convert PNG to text,
  read text from PNG, load image for OCR, and perform OCR on image in just a few steps.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: en
lastmod: 2026-07-21
og_description: Extract text from image with Java. This guide shows you how to convert
  PNG to text, read text from PNG, load image for OCR, and perform OCR on image efficiently.
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: Extract Text from Image in Java – Step‑by‑Step OCR Tutorial
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
title: Extract Text from Image in Java – Complete OCR Guide
url: /java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract Text from Image in Java – Complete OCR Guide

Ever needed to **extract text from image** but weren’t sure which Java library to pick? You’re not alone. Whether you’re digitizing receipts, scanning PDFs, or building a searchable archive, pulling text out of a PNG is a daily pain point for many developers.

In this tutorial we’ll walk through a hands‑on solution that lets you **convert PNG to text**, **read text from PNG**, **load image for OCR**, and **perform OCR on image**—all with a few lines of clean Java code. By the end you’ll have a runnable program you can drop into any project.

## What You’ll Build

We’ll create a small Java console app that:

1. Loads a PNG file from disk.  
2. Sends the image to an OCR engine (Tess4J, a Java wrapper for Tesseract).  
3. Prints the recognized text to the console.

No external services, no magic—just pure Java and an open‑source OCR engine.

## Prerequisites

- **Java 17** or later (the code compiles with older versions, but Java 17 gives you the latest language goodies).  
- **Maven** or **Gradle** for dependency management.  
- A sample PNG named `sample.png` placed in a folder you can reference (e.g., `src/main/resources`).  
- Basic familiarity with Java’s `main` method and exception handling.

If any of those sound unfamiliar, don’t worry—each step includes a quick recap.

## Step 1: Set Up the Project and Add the OCR Library

First, create a new Maven project (or Gradle if you prefer). Add the Tess4J dependency, which brings in Tesseract binaries for you.

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

> **Pro tip:** If you’re using Gradle, the equivalent line is `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'`.

Adding this library gives you the `Tesseract` class, which handles the heavy lifting of **performing OCR on image** data.

## Step 2: Load Image for OCR

Now we need to **load image for OCR**. Tess4J works with `java.awt.image.BufferedImage`, so we’ll read the PNG using `ImageIO`.

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

The method above cleanly isolates the **load image for OCR** logic, making the rest of the code easier to test. Notice the comment – it mirrors the original snippet while expanding it for clarity.

## Step 3: Perform OCR on Image

With the image in memory, we can now **perform OCR on image**. The `Tesseract` instance is our engine; we’ll configure it to use the default English language data that ships with Tess4J.

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

Here we’ve merged the original “Step 1” and “Step 4” into a single method, because the `Tesseract` object is cheap to create and we want the code to stay compact. The comment still references the original steps for traceability.

## Step 4: Put It All Together – Main Method

Finally, we bring everything together in `main`. This is where you’ll **read text from PNG** and see the result printed to the console.

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

When you run `mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"` (or the Gradle equivalent), you should see something like:

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

That output proves you’ve successfully **extract text from image**, **convert PNG to text**, and **read text from PNG** in a single, tidy program.

## Handling Common Edge Cases

### Low‑Quality Images

If the PNG is blurry or has low contrast, OCR accuracy drops. A quick fix is to pre‑process the image:

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

### Multi‑Language Support

Tess4J can handle many languages. Just download the appropriate `.traineddata` file and point `tesseract.setLanguage("spa")` for Spanish, for example.

### Large PDFs or Multi‑Page Images

If you need to **extract text from image** files inside a PDF, split each page into PNGs first (using PDFBox) and then feed each PNG to the same OCR routine.

## Full Working Example (All Code in One Place)

Below is the complete, ready‑to‑run Java class. Copy‑paste it into `src/main/java/com/example/ocrdemo/OcrDemo.java` and you’re good to go.

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

Running the class prints the OCR result, confirming you have successfully **performed OCR on image** and turned your PNG into editable text.

## Recap & Next Steps

We started by **extracting text from image** using a lightweight Java setup. You now know how to **load image for OCR**, **perform OCR on image**, and **read text from PNG**—essential building blocks for any document‑digitization pipeline.

Want to go further? Try these ideas:

- **Batch processing:** Loop over a directory of PNGs and write each result to a `.txt` file.  
- **Integrate with a database:** Store extracted strings alongside metadata for searchable archives.  
- **Combine with NLP:** Feed the OCR output into a sentiment‑analysis model for quick insights.  

Each of those extensions builds on the same core concepts we covered, so you’re ready to experiment.

---

*Happy coding! If you hit any snags


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [image to text java: Convert Image to Text with Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}