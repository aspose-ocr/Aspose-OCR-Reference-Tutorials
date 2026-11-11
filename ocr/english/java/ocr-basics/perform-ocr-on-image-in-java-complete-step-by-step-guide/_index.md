---
category: general
date: 2026-06-16
description: Learn how to perform OCR on image files in Java. This tutorial covers
  recognizing text from PNG, extracting text from image, converting image to text,
  and loading image for OCR.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: en
og_description: Perform OCR on image using Java. This guide shows how to recognize
  text from PNG, extract text from image, and convert image to text with a ready‑to‑run
  example.
og_title: Perform OCR on Image in Java – Full Programming Tutorial
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
title: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
url: /java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Perform OCR on Image in Java – Complete Step‑by‑Step Guide

Ever needed to **perform OCR on image** files but weren’t sure which Java library to pick? You’re not alone. Whether you’re building a receipt scanner, a document archiver, or just curious about turning pictures into searchable text, learning how to **perform OCR on image** with Java is a handy skill.

In this tutorial we’ll walk through everything you need to **perform OCR on image** files: loading the image, configuring the engine, recognizing the text, and finally printing the result. By the end you’ll be able to **recognize text from PNG** files, **extract text from image** sources, and **convert image to text** with just a few lines of code.

## Prerequisites

- Java 17 or newer (the code compiles with any recent JDK)
- Maven installed (or your favourite build tool)
- Basic familiarity with Java syntax
- A PNG file you’d like to test (we’ll call it `hello.png`)

> **Pro tip:** If you don’t have a PNG handy, create one by taking a screenshot of any text and saving it as `hello.png` in a folder called `resources`.

## What We’ll Build

A tiny console application named `OcrDemo` that:

1. **Loads image for OCR** – reads a PNG from disk.
2. **Performs OCR on image** – uses the Tesseract engine via Tess4J.
3. **Extracts text from image** – returns a `String` with the recognized content.
4. Prints the result to the console.

Let’s dive in.

## Step 1: Set Up the Project and Add Tess4J

First, create a new Maven project (or Gradle if you prefer). Add the Tess4J dependency, which wraps the popular Tesseract OCR engine.

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

> **Why Tess4J?** It’s actively maintained, works cross‑platform, and gives you a clean Java API for **perform OCR on image** tasks.

## Step 2: Prepare the Image‑Loading Logic

Now we’ll write a helper method that **load image for OCR**. The method uses Java’s `ImageIO` to read a PNG into a `BufferedImage`.

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

Notice the method name clearly reflects the **load image for OCR** intent, making the code self‑documenting.

## Step 3: Configure the OCR Engine to **Perform OCR on Image**

With the image in hand, we create a `Tesseract` instance, enable automatic language detection, and call `doOCR`. This is the core of how we **perform OCR on image** data.

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

> **Why enable auto‑detect?** It lets the engine pick the best language model for the image, which is especially useful when you **convert image to text** from sources that mix English and other scripts.

## Step 4: Put It All Together – The Main Application

Here’s the entry point that **recognize text from PNG**, **extract text from image**, and finally prints the result. This is the complete, runnable example.

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

### Expected Output

If `hello.png` contains the phrase “Hello, OCR world!”, the console will display something like:

```
=== Recognized Text ===
Hello, OCR world!
```

The exact output may vary slightly depending on image quality, but you should see the text you placed in the PNG.

## Step 5: Handling Common Edge Cases

### 5.1 Dealing with Low‑Resolution Images

If the source PNG is blurry, OCR accuracy drops. A quick fix is to upscale the image before feeding it to the engine:

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

Call `upscale(image, 2)` before `engine.recognize(image)` to improve results.

### 5.2 Multi‑Language Documents

If you anticipate French or German text, simply add the language codes to `setLanguage`:

```java
tesseract.setLanguage("eng+fra+deu");
```

The engine will then try to **extract text from image** using the combined language models.

### 5.3 Skipping Empty Pages

Sometimes a scanned PDF page renders as a blank PNG. Detecting an empty image saves processing time:

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## Step 6: Packaging and Running the Application

1. **Compile:** `mvn clean compile`
2. **Run:** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

Make sure the `tessdata` folder (containing language files) sits next to the compiled JAR or specify its absolute path in `OcrEngine`.

## Conclusion

You now have a solid, production‑ready pattern to **perform OCR on image** files using Java. From **loading image for OCR** to **recognize text from PNG**, we covered how to **extract text from image**, **convert image to text**, and handle tricky scenarios like low‑resolution scans or multi‑language content.

Next, you might explore:

- **Batch processing** – loop over a directory of PNGs and write each result to a `.txt` file.
- **PDF generation** – embed the extracted text back into searchable PDFs.
- **Cloud OCR services** – compare local Tesseract performance with APIs like Google Vision or Azure Cognitive Services.

Feel free to experiment, tweak the parameters, and share your findings. Happy coding, and may your images always turn into clean, searchable text! 

![Diagram showing the OCR workflow to perform OCR on image](https://example.com/ocr-workflow.png "perform OCR on image example")


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}