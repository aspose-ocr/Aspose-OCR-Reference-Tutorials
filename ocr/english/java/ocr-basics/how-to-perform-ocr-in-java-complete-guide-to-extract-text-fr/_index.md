---
category: general
date: 2026-06-06
description: how to perform OCR in Java – quickly extract text from image, convert
  image to text, and read text from jpg using a simple code example.
draft: false
keywords:
- how to perform OCR
- ocr in java
- extract text from image
- convert image to text
- read text from jpg
language: en
og_description: how to perform OCR in Java – learn how to extract text from image,
  convert image to text, and read text from jpg with a ready‑to‑run example.
og_title: How to Perform OCR in Java – Step‑by‑Step Guide
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  headline: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  type: TechArticle
- description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  name: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  steps:
  - name: What You’ll Learn
    text: '- Install an OCR library (yes, **ocr in java** is easier than you think).
      - Create and configure an OCR engine instance. - Load a JPG (or any image) and
      set the language. - Process the image and **extract text from image** files.
      - Print the recognized string to the console.'
  - name: Expected Output
    text: 'If `input.jpg` contains the Mongolian phrase “Сайн байна уу?” the console
      will show:'
  - name: 'Pro Tip: Batch Processing'
    text: 'If you need to **extract text from image** files in bulk, wrap the core
      logic in a loop:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: How to Perform OCR in Java – Complete Guide to Extract Text from Images
url: /java/ocr-basics/how-to-perform-ocr-in-java-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Perform OCR in Java – Complete Guide to Extract Text from Images

Ever wondered **how to perform OCR** on a picture you snapped on your phone? You're not the only one. Whether you're building a receipt‑scanning app or just need to pull text out of a scanned PDF, **how to perform OCR** in Java is a skill that pays off quickly. In this tutorial we’ll walk through a practical example that **extracts text from image** files, **converts image to text**, and even shows you how to **read text from jpg** with just a few lines of code.

> *Pro tip:* The same approach works for PNG, BMP, or any format the OCR engine supports—just swap the file name.

## How to Perform OCR in Java – Overview

Optical Character Recognition (OCR) is the technology that turns pictures of letters into actual, searchable text. In the Java ecosystem there are several libraries—Tesseract, Asprise, and commercial SDKs—all exposing a similar workflow: load an image, tell the engine what language to expect, run the recognition, and grab the result. Below we’ll use a generic `OcrEngine` class to keep the example clear, but you can replace it with any concrete implementation that follows the same pattern.

### What You’ll Learn

- Install an OCR library (yes, **ocr in java** is easier than you think).
- Create and configure an OCR engine instance.
- Load a JPG (or any image) and set the language.
- Process the image and **extract text from image** files.
- Print the recognized string to the console.

By the end you’ll have a self‑contained Java program you can drop into any project and run instantly.

![how to perform OCR example](ocr-example.png "how to perform OCR in Java illustration")

## Step 1 – Install and Import an OCR Library (ocr in java)

Before you write a single line of Java, you need a library that actually does the heavy lifting. If you’re using Maven, add a dependency like this (replace `com.example.ocr` with the real group ID of your chosen SDK):

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>ocr-sdk</artifactId>
    <version>1.4.2</version>
</dependency>
```

If you prefer Gradle:

```gradle
implementation 'com.example:ocr-sdk:1.4.2'
```

Once the JAR is on your classpath, import the classes you’ll need:

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;
```

> **Why this matters:** Importing the right classes prevents “cannot find symbol” errors and makes your IDE happy—nothing more frustrating than a missing import when you’re trying to **convert image to text**.

## Step 2 – Create the OCR Engine Instance (how to perform OCR)

Now that the library is ready, spin up the engine. Think of the engine as the brain that will look at the pixels and guess the letters.

```java
// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

Creating the engine is usually cheap; most SDKs allocate internal buffers lazily, so you can safely reuse the same instance across many images if you’re processing a batch.

## Step 3 – Load the Image and Set the Language (extract text from image)

The next step is to give the engine something to read. Here we load a JPEG from disk and tell the OCR engine that the text is in Mongolian (ISO 639‑2 code “mon”). You can change the path or language code to match your use‑case.

```java
// Step 3: Load the image you want to recognize
ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/input.jpg"));

// Step 3b: Specify the language (e.g., English = "eng", Mongolian = "mon")
ocrEngine.getSettings().setLanguage("mon");
```

> **Side note:** If you don’t set a language, the engine defaults to English, which can drastically lower accuracy when the text is actually Cyrillic or another script. Always specify the correct language when you can.

## Step 4 – Process the Image and Get the Result (convert image to text)

With the image and language in place, ask the engine to do its magic. The `process()` call runs the OCR algorithm and returns an `OcrResult` object containing the recognized string and confidence scores.

```java
// Step 4: Process the image and obtain the recognition result
OcrResult ocrResult = ocrEngine.process();
```

Behind the scenes, the engine may perform preprocessing—deskewing, binarization, noise reduction—so you don’t have to write those steps yourself. That’s why most modern OCR libraries are a joy to use for **convert image to text** tasks.

## Step 5 – Output the Extracted Text (read text from jpg)

Finally, pull the plain‑text out of the result and do something useful with it. For this demo we simply print it to the console, but you could write it to a file, feed it into a search index, or pass it to another service.

```java
// Step 5: Output the extracted text
System.out.println(ocrResult.getText());
```

That line alone proves you’ve successfully **read text from jpg** (or any supported format). If the output looks garbled, double‑check the language code and image quality.

## Full Working Example (All Steps Combined)

Below is a complete, ready‑to‑run Java class that ties every piece together. Copy it into a file named `OcrDemo.java`, adjust the image path and language, then run `javac OcrDemo.java && java OcrDemo`.

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to perform OCR in Java using a generic OCR SDK.
 * This example loads a JPG, sets the language to Mongolian, and prints
 * the recognized text to the console.
 *
 * Replace the import package with the actual library you are using.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Validate command‑line arguments
        if (args.length < 2) {
            System.err.println("Usage: java OcrDemo <image-path> <language-code>");
            System.exit(1);
        }

        String imagePath = args[0];   // e.g., "input.jpg"
        String language = args[1];    // e.g., "mon" for Mongolian

        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image
        ocrEngine.setImage(new OcrInputImage(imagePath));

        // Step 3: Set the language (ISO‑639‑2)
        ocrEngine.getSettings().setLanguage(language);

        // Step 4: Run the recognition
        OcrResult result = ocrEngine.process();

        // Step 5: Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### Expected Output

If `input.jpg` contains the Mongolian phrase “Сайн байна уу?” the console will show:

```
=== Recognized Text ===
Сайн байна уу?
```

If the image is blurry or the language code is wrong, you’ll see garbled characters or an empty string—common pitfalls that we’ll discuss next.

## Common Pitfalls and How to Fix Them

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Garbled Cyrillic characters | Wrong language code (defaulting to English) | Set `ocrEngine.getSettings().setLanguage("mon")` or the appropriate code. |
| No output at all | Image path incorrect or file unreadable | Verify the path, ensure the file exists, and that the process has read permissions. |
| Low accuracy (<70 %) | Image is low‑contrast or rotated | Pre‑process the image: increase contrast, deskew, or convert to grayscale before feeding it to the engine. |
| `OutOfMemoryError` on large PDFs | Loading many high‑resolution pages at once | Process pages one at a time, or downscale images before OCR. |

### Pro Tip: Batch Processing

If you need to **extract text from image** files in bulk, wrap the core logic in a loop:

```java
for (File img : new File("batchFolder").listFiles()) {
    ocrEngine.setImage(new OcrInputImage(img.getAbsolutePath()));
    OcrResult r = ocrEngine.process();
    System.out.println(r.getText());
}
```

That snippet demonstrates how easy it is to scale from a single JPG to an entire folder of scans.

## Going Further – What to Explore Next?

- **Language Packs:** Most OCR SDKs let you download additional language data files. Adding a new pack lets you **convert image to text** for languages beyond English and Mongolian.
- **PDF OCR:** Combine this code with Apache PDFBox to


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}