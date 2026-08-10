---
category: general
date: 2026-06-06
description: Extract text from scanned image using Aspose OCR for Java. Learn how
  to recognize text from tiff files with parallel processing.
draft: false
keywords:
- extract text from scanned image
- recognize text from tiff
- Aspose OCR Java tutorial
- parallel OCR processing
- Java image recognition
language: en
og_description: Extract text from scanned image with Aspose OCR. This guide shows
  how to recognize text from tiff files efficiently using Java.
og_title: Extract Text from Scanned Image – Aspose OCR Java Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from scanned image using Aspose OCR for Java. Learn how
    to recognize text from tiff files with parallel processing.
  headline: Extract Text from Scanned Image in Java – Complete Aspose OCR Guide
  type: TechArticle
- description: Extract text from scanned image using Aspose OCR for Java. Learn how
    to recognize text from tiff files with parallel processing.
  name: Extract Text from Scanned Image in Java – Complete Aspose OCR Guide
  steps:
  - name: Maven users
    text: 'Add the following dependency to your `pom.xml`:'
  - name: Manual JAR setup
    text: Download the latest `aspose-ocr-xx.jar` from the Aspose website and place
      it on your classpath.
  - name: Expected Output
    text: '``` === Extracted Text === Invoice Number: 12345 Date: 2024‑05‑01 Total:
      $1,250.00 ... ```'
  - name: What’s Next?
    text: '- **Batch processing**: Loop over a directory of TIFFs, store each result
      in its own file. - **Integrate with Elasticsearch**: Index the extracted text
      for fast full‑text search. - **Add language detection**: Use `OcrLanguage.AutoDetect`
      for multi‑lingual documents.'
  type: HowTo
- questions:
  - answer: Absolutely. `OcrInputImage` accepts any format that Java’s ImageIO can
      read. Just replace the file extension in the path.
    question: Does this work with PNG or JPEG files?
  - answer: You could, but remember other services may need CPU cycles. A good rule
      of thumb is “total cores – 1” for dedicated OCR workers.
    question: My server has 8 cores—should I set `setMaxThreads(8)`?
  - answer: 'Check that the image isn’t completely white, that you set the correct
      language, and that the resolution is at least 200 DPI. Low‑quality scans often
      need pre‑processing (deskew, contrast boost) before feeding them to Aspose OCR.
      --- ## Wrap‑Up We’ve just **extracted text from scanned image** files u'
    question: What if the OCR result is empty?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Extract Text from Scanned Image in Java – Complete Aspose OCR Guide
url: /java/advanced-ocr-techniques/extract-text-from-scanned-image-in-java-complete-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract Text from Scanned Image – Complete Aspose OCR Guide

Ever needed to **extract text from scanned image** but felt stuck at the “how?”? You’re not the only one. Whether you’re digitizing old archives, pulling data from invoices, or building a searchable PDF library, getting reliable text out of a TIFF scan can be a pain point.  

Good news: with Aspose OCR for Java you can **recognize text from tiff** files in just a few lines, and even squeeze out extra speed by limiting the engine to a handful of CPU cores. In this tutorial we’ll walk through the whole process—from setting up the library to handling the result—so you can copy‑paste a working example right away.

## What This Tutorial Covers

- Installing Aspose OCR for Java (Maven or manual JAR)
- Loading a large scanned TIFF image
- Configuring the engine to use up to 4 threads (parallel OCR)
- Running the OCR process and printing the extracted text
- Common pitfalls (memory, multi‑page TIFFs) and how to avoid them
- Quick performance tip: when to tune `setMaxThreads`

By the end you’ll be able to **extract text from scanned image** files reliably, and you’ll understand why tweaking the thread count matters when you *recognize text from tiff* in a production pipeline.

---

![extract text from scanned image example](example.png "Screenshot showing extracted text from a scanned TIFF image")

## Prerequisites

Before we dive in, make sure you have:

1. **Java Development Kit (JDK) 8+** – any recent version works.
2. **Maven** (or the ability to add JARs manually) – we’ll use Maven for simplicity.
3. An **Aspose OCR for Java** license (the free evaluation works, but it adds a watermark).  
4. A **large TIFF scan** (e.g., `large_scan.tif`) you want to process.

If any of these sound unfamiliar, don’t worry—each step is explained below.

## Step 1: Add Aspose OCR to Your Project

### Maven users

Add the following dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version on Maven Central -->
</dependency>
```

### Manual JAR setup

Download the latest `aspose-ocr-xx.jar` from the Aspose website and place it on your classpath.  

> **Pro tip:** Keep the JAR in a `libs/` folder and reference it in your IDE’s project settings. This avoids “class not found” surprises later.

## Step 2: Create a Simple Java Class

Create a file named `ParallelOcrDemo.java` in your source folder (`src/main/java`). This class will hold the entire OCR workflow.

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Load the scanned TIFF image you want to process
        // Replace the path with the actual location of your image
        ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/large_scan.tif"));

        // Step 2.3: Limit the engine to use up to 4 CPU cores.
        // This is useful on servers where you don't want to hog all cores.
        ocrEngine.getSettings().setMaxThreads(4);

        // Step 2.4: Run the OCR operation
        OcrResult ocrResult = ocrEngine.process();

        // Step 2.5: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

> **Why we limit threads:** By default Aspose OCR will try to use every core, which can starve other services on a shared machine. Setting `setMaxThreads(4)` tells the engine to run up to four parallel workers—enough for a noticeable speed‑up on most modern CPUs without monopolizing resources.

## Step 3: Compile and Run

Open a terminal at the project root and execute:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ParallelOcrDemo"
```

If you’re not using Maven, compile with `javac` and run:

```bash
javac -cp "libs/*" src/main/java/com/example/ocr/ParallelOcrDemo.java
java -cp "libs/*:src/main/java" com.example.ocr.ParallelOcrDemo
```

### Expected Output

```
=== Extracted Text ===
Invoice Number: 12345
Date: 2024‑05‑01
Total: $1,250.00
...
```

The console will display the plain‑text version of whatever was on the scanned page. If the image contains multiple pages, Aspose OCR concatenates them in order.

## Step 4: Handling Multi‑Page TIFFs (Edge Case)

A common scenario is a **multi‑page TIFF**—think of a scanned book. By default `OcrInputImage` reads the first frame only. To process all pages, use `OcrInputImage` with a `FileInputStream` and enable multi‑page support:

```java
import java.io.FileInputStream;
import com.aspose.ocr.*;

FileInputStream fis = new FileInputStream("YOUR_DIRECTORY/multi_page.tif");
ocrEngine.setImage(new OcrInputImage(fis, true)); // 'true' enables multi‑page
```

Now `ocrEngine.process()` will return a single `OcrResult` that contains the concatenated text from every page.

## Step 5: Fine‑Tuning Recognition Accuracy

If you notice **garbled characters** or missing words, try these adjustments:

| Setting | What it does | When to use it |
|---------|--------------|----------------|
| `ocrEngine.getSettings().setLanguage(OcrLanguage.English)` | Forces English language model (faster, more accurate for English scans) | Your document is monolingual English |
| `ocrEngine.getSettings().setResolution(300)` | Upscales low‑resolution images before recognition | Scans below 200 DPI |
| `ocrEngine.getSettings().setNoiseRemoval(true)` | Attempts to clean speckles and artifacts | Scans with heavy noise |

Example snippet:

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setNoiseRemoval(true);
```

## Step 6: Exporting Results to a File

Printing to the console is fine for demos, but production code usually writes the output somewhere useful:

```java
import java.io.FileWriter;
import java.io.IOException;

// After processing
String extractedText = ocrResult.getText();
try (FileWriter writer = new FileWriter("output.txt")) {
    writer.write(extractedText);
}
System.out.println("Text saved to output.txt");
```

Now you have a plain‑text file you can feed into a search index, a database, or a downstream analytics pipeline.

---

## Frequently Asked Questions (FAQ)

**Q: Does this work with PNG or JPEG files?**  
A: Absolutely. `OcrInputImage` accepts any format that Java’s ImageIO can read. Just replace the file extension in the path.

**Q: My server has 8 cores—should I set `setMaxThreads(8)`?**  
A: You could, but remember other services may need CPU cycles. A good rule of thumb is “total cores – 1” for dedicated OCR workers.

**Q: What if the OCR result is empty?**  
A: Check that the image isn’t completely white, that you set the correct language, and that the resolution is at least 200 DPI. Low‑quality scans often need pre‑processing (deskew, contrast boost) before feeding them to Aspose OCR.

---

## Wrap‑Up

We’ve just **extracted text from scanned image** files using Aspose OCR for Java, and you now know how to **recognize text from tiff** efficiently with parallel processing. The complete code lives in the snippets above, and you can copy‑paste it into your own project right away.

### What’s Next?

- **Batch processing**: Loop over a directory of TIFFs, store each result in its own file.  
- **Integrate with Elasticsearch**: Index the extracted text for fast full‑text search.  
- **Add language detection**: Use `OcrLanguage.AutoDetect` for multi‑lingual documents.  

Experiment with those ideas, and you’ll quickly turn a mountain of scanned paperwork into searchable, actionable data.

Happy coding, and feel free to drop a comment if you hit a snag!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to recognize tiff with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}