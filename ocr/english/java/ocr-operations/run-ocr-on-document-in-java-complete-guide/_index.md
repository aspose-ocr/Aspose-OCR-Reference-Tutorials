---
category: general
date: 2026-06-16
description: Run OCR on document using Java in just a few steps. Learn how to configure
  OCR, recognize text from TIFF, and extract text from multi‑page images.
draft: false
keywords:
- run OCR on document
- how to configure OCR
- recognize text from TIFF
- extract text from multi-page
language: en
og_description: Run OCR on document with Java. This guide shows how to configure OCR,
  recognize text from TIFF files, and extract text from multi‑page images.
og_title: Run OCR on Document in Java – Step‑by‑Step Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Run OCR on document using Java in just a few steps. Learn how to configure
    OCR, recognize text from TIFF, and extract text from multi‑page images.
  headline: Run OCR on Document in Java – Complete Guide
  type: TechArticle
- description: Run OCR on document using Java in just a few steps. Learn how to configure
    OCR, recognize text from TIFF, and extract text from multi‑page images.
  name: Run OCR on Document in Java – Complete Guide
  steps:
  - name: '**Streamed processing** – Some OCR SDKs let you feed pages one‑by‑one instead
      of loading the entire TIFF into memory. Look for methods like `engine.setImageStream(...)`
      that accept an `InputStream`.'
    text: '**Streamed processing** – Some OCR SDKs let you feed pages one‑by‑one instead
      of loading the entire TIFF into memory. Look for methods like `engine.setImageStream(...)`
      that accept an `InputStream`.'
  - name: '**Memory limits** – If you hit `OutOfMemoryError`, lower the thread count
      or increase the JVM heap (`-Xmx2g`).'
    text: '**Memory limits** – If you hit `OutOfMemoryError`, lower the thread count
      or increase the JVM heap (`-Xmx2g`).'
  - name: '**Post‑processing** – Use regex or natural‑language libraries to clean
      up line breaks, remove headers/footers, or extract specific fields (e.g., invoice
      numbers).'
    text: '**Post‑processing** – Use regex or natural‑language libraries to clean
      up line breaks, remove headers/footers, or extract specific fields (e.g., invoice
      numbers).'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Run OCR on Document in Java – Complete Guide
url: /java/ocr-operations/run-ocr-on-document-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Run OCR on Document in Java – Complete Guide

Ever needed to **run OCR on document** files but weren’t sure where to start? You’re not alone. Whether you’re digitizing old archives or pulling data from scanned forms, getting reliable text out of images is a common pain point.

In this tutorial we’ll walk through a practical, end‑to‑end example that shows **how to configure OCR**, **recognize text from TIFF**, and **extract text from multi‑page** documents—all with just a handful of lines of Java. No fluff, just a working solution you can drop into your project today.

## What You’ll Learn

- Set up an OCR engine instance in Java  
- Load a multi‑page TIFF image for processing  
- Optimize the engine by configuring thread count (the “how to configure OCR” part)  
- Perform recognition and output the extracted text  
- Handle edge cases like large files and memory limits  

By the end of this guide you’ll be able to **run OCR on document** images confidently, and you’ll have a solid foundation for extending the solution to PDFs, PNGs, or even live camera streams.

## Prerequisites

- Java 17 or newer (the code uses the `var` keyword for brevity)  
- An OCR library that exposes an `OcrEngine` class (e.g., *Aspose.OCR for Java* or *Tesseract‑Java* wrapper).  
- A multi‑page TIFF file named `multi_page.tif` placed in a known directory.  

If you’re missing the OCR library, add it to your `pom.xml` (Maven) or `build.gradle` (Gradle) – the exact coordinates depend on the vendor, but most provide a single JAR you can reference.

---

## Step 1: Initialize the OCR Engine – How to Run OCR on Document

First things first: you need an engine object that will do the heavy lifting. Think of it as the brain behind the operation.

```java
import com.example.ocr.OcrEngine;   // Replace with your actual package
import com.example.ocr.ImageStream;
import com.example.ocr.OcrResult;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();
```

> **Why this matters:** The `OcrEngine` encapsulates all recognition settings, language packs, and hardware utilization options. Creating it once and reusing it for multiple images is more efficient than instantiating it repeatedly.

---

## Step 2: Load the Multi‑Page TIFF – Extract Text from Multi‑Page Images

Now we point the engine at the file we want to process. TIFF is a common format for scanned documents because it can store several pages in a single file.

```java
        // Step 2: Load the multi‑page image to be processed
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page.tif"));
```

> **Pro tip:** If your TIFF lives on a network share, use `ImageStream.fromUrl(...)` instead. This avoids copying the whole file into memory before OCR begins.

---

## Step 3: How to Configure OCR for Maximum Throughput

Out‑of‑the‑box OCR libraries often run on a single thread, which can be a bottleneck on modern multi‑core machines. Here’s where we answer the “**how to configure OCR**” part of the puzzle.

```java
        // Step 3: Configure the engine to use all available CPU cores
        int availableCores = Runtime.getRuntime().availableProcessors();
        engine.getRecognitionSettings().setThreadCount(availableCores);
```

> **Why this works:** By matching the thread count to the number of logical processors, the OCR engine can process different pages in parallel. For a 4‑core laptop you’ll see roughly a 3‑4× speed boost when dealing with multi‑page documents.

> **Edge case:** Some environments (e.g., Docker containers with limited CPU quotas) report more cores than they’re allowed to use. In such cases, cap the thread count manually: `engine.getRecognitionSettings().setThreadCount(Math.min(availableCores, 2));`

---

## Step 4: Recognize Text from TIFF – The Core OCR Call

With everything wired up, it’s time to actually run the recognition. This single call will iterate over each page of the TIFF, apply the language models, and return a composite result.

```java
        // Step 4: Perform the OCR recognition
        OcrResult result = engine.recognize();
```

> **What’s happening under the hood?** The engine splits the TIFF into individual raster images, feeds each to the OCR neural net, and stitches the textual output together. If you need per‑page granularity, `result.getPages()` will give you a list of `OcrPageResult` objects.

---

## Step 5: Output the Recognized Text – Verify the Extraction

Finally, we print the extracted text to the console. In a real‑world app you’d probably write it to a database or a JSON file.

```java
        // Step 5: Output the recognized text
        System.out.println(result.getText());
    }
}
```

**Expected output (truncated):**

```
Page 1:
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00

Page 2:
Terms and Conditions...
```

If you see gibberish instead of clean characters, double‑check that the correct language packs are installed and that the image isn’t too noisy. Pre‑processing steps like deskewing or binarization can dramatically improve accuracy.

---

## Handling Large Multi‑Page Files – Tips for Extraction

Even though we’ve already shown the basic flow, real‑world documents can be massive. Here are a few extra considerations:

1. **Streamed processing** – Some OCR SDKs let you feed pages one‑by‑one instead of loading the entire TIFF into memory. Look for methods like `engine.setImageStream(...)` that accept an `InputStream`.
2. **Memory limits** – If you hit `OutOfMemoryError`, lower the thread count or increase the JVM heap (`-Xmx2g`).
3. **Post‑processing** – Use regex or natural‑language libraries to clean up line breaks, remove headers/footers, or extract specific fields (e.g., invoice numbers).

---

## Full Working Example (All Steps Combined)

Below is the complete, ready‑to‑run Java class. Paste it into your IDE, adjust the package/imports, and run it.

```java
package com.example.ocrdemo;

import com.example.ocr.OcrEngine;
import com.example.ocr.ImageStream;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to run OCR on document images, configure the engine,
 * recognize text from TIFF files, and extract text from multi‑page documents.
 */
public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Create the OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Load the multi‑page TIFF image
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page.tif"));

        // Configure the engine to use all CPU cores (how to configure OCR)
        int cores = Runtime.getRuntime().availableProcessors();
        engine.getRecognitionSettings().setThreadCount(cores);

        // Perform recognition (recognize text from TIFF)
        OcrResult result = engine.recognize();

        // Output the extracted text (extract text from multi‑page)
        System.out.println(result.getText());
    }
}
```

> **Pro tip:** Wrap the `recognize()` call in a `try‑catch` block to handle `OcrException` gracefully, especially when dealing with corrupted image files.

---

## Conclusion

We’ve just shown you how to **run OCR on document** images using Java, covering everything from engine initialization to multi‑page text extraction. By understanding **how to configure OCR**, you can squeeze out every ounce of performance from modern CPUs, while the steps for **recognize text from TIFF** and **extract text from multi‑page** files give you a solid baseline for any document‑digitization project.

What’s next? Try swapping the TIFF for a PDF, experiment with custom language models, or pipe the output into a search index. The sky’s the limit once you have this foundation under your belt.

If you hit any snags—maybe the OCR library you chose uses a different API—drop a comment below. Happy coding, and enjoy turning those scanned pages into searchable text!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to recognize tiff with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}