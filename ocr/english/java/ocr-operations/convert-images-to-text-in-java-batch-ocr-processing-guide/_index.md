---
category: general
date: 2026-01-02
description: Convert images to text with Java using Aspose OCR. Master batch OCR processing,
  read images from folder, and filter files by extension.
draft: false
keywords:
- convert images to text
- batch ocr processing
- read images from folder
- extract text from png
- filter files by extension
language: en
og_description: Convert images to text quickly with Java. This tutorial covers batch
  OCR processing, reading images from a folder, and filtering files by extension.
og_title: Convert Images to Text in Java – Complete Batch OCR Guide
tags:
- OCR
- Java
- Aspose
title: Convert Images to Text in Java – Batch OCR Processing Guide
url: /java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert Images to Text in Java – Batch OCR Processing Guide

Ever needed to **convert images to text** but weren't sure how to handle dozens of files at once? You're not alone—developers constantly wrestle with pulling data out of PNGs, JPGs, and other scans. The good news? With Aspose OCR you can spin up a batch OCR processing pipeline in minutes, read images from folder structures, and even filter files by extension so you only work on what matters.

In this tutorial we'll build a self‑contained Java program that walks a directory, picks out every `.png` or `.jpg`, sends each picture to Aspose OCR asynchronously, and prints the extracted text in the original order. By the end you'll have a reusable snippet you can drop into any project that needs to **convert images to text** at scale.

---

![Convert images to text example](https://example.com/convert-images-to-text.png "Screenshot of Java console output showing converted text from PNG files")

## What You'll Build

- A single `AsposeOCR` engine shared across threads (efficient and thread‑safe).  
- A `ParallelRecognizer` that runs OCR jobs in parallel, perfect for **batch OCR processing**.  
- Logic that **reads images from folder** using `java.nio.file.Files`.  
- Simple filters to **extract text from PNG** files while still handling JPGs.  
- Clean shutdown of the internal thread pool to avoid resource leaks.

### Prerequisites

- Java 17 (or any recent LTS version).  
- Maven or Gradle to pull the Aspose OCR library.  
- A folder full of PNG/JPG images you want to process.  
- Basic familiarity with Java streams—nothing fancy required.

> **Pro tip:** If you don't have a license yet, Aspose offers a free temporary key you can use for testing.

---

## Step 1 – Set Up the Project and Add Aspose OCR

First, create a new Maven project (or Gradle, your call). Add the Aspose OCR dependency to `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **Why this matters:** Declaring the dependency up front ensures the compiler can see `AsposeOCR`, `ParallelRecognizer`, and related classes. It also guarantees that the same version is used across all machines, which is crucial for reproducible **batch OCR processing**.

Once the build finishes, refresh your IDE and you should see the Aspose packages under `External Libraries`.

---

## Step 2 – Convert Images to Text – Initialize the OCR Engine

We only need **one** OCR engine instance for the whole run. Sharing it across threads saves memory and speeds things up because the engine loads language packs just once.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```

> **Explanation:** `ParallelRecognizer` wraps the engine in a thread‑pool. When you submit many files, each gets its own worker thread, enabling true parallelism on multi‑core CPUs.

---

## Step 3 – Read Images from Folder – Walk the Directory Tree

Now we need to **read images from folder** and collect every PNG or JPG. The `Files.walk` API makes this a one‑liner, but we’ll add a filter to **extract text from PNG** only when needed.

```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```

> **Why we filter here:** Using `filter` lets us **filter files by extension** early, which slashes unnecessary I/O later. It also keeps the code readable—no need for complex regexes.

---

## Step 4 – Batch OCR Processing – Submit Jobs Asynchronously

With the list of files ready, we push each path to the `ParallelRecognizer`. The `recognizeAsync` method returns a `Future<OcrResult>` that we store for later retrieval.

```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```

> **What’s happening under the hood?** Each call enqueues a task into the recognizer’s internal executor service. The tasks run in parallel, so a folder with 100 images can be processed in a fraction of the time a single‑threaded loop would take.

---

## Step 5 – Retrieve Results in Original Order – Preserve File Sequence

Because we stored the futures in the same order as `imagePaths`, we can simply iterate over the list and call `get()`. The call blocks only until that particular image is done, preserving order without extra bookkeeping.

```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**Sample console output** (truncated for brevity):

```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```

> **Edge case handling:** If a particular image throws an exception (corrupt file, unsupported format), we catch it and continue processing the rest—an essential habit for reliable **batch OCR processing** pipelines.

---

## Step 6 – Clean Up – Shut Down the Recognizer

Never forget to shut down the internal thread pool; otherwise your JVM may hang on exit.

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

That’s it! The program will now walk any directory, filter for PNG/JPG files, run OCR in parallel, and print the results.

---

## Full Working Example

Below is the complete, copy‑and‑paste‑ready Java class. Replace `"YOUR_DIRECTORY"` with the path to your images folder and run it from your IDE or command line.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

Run the class, watch the console fill with extracted strings, and celebrate the fact that you just **converted images to text** without writing a single loop that blocks on I/O.

---

## Frequently Asked Questions (FAQs)

**Q: Can I process PDFs or TIFFs as well?**  
A: Absolutely. Aspose OCR supports many formats—just add the appropriate file extensions to the filter in Step 2.

**Q: What if I need a different language, like Spanish?**  
A: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`. Make sure the language pack is installed (Aspose includes most major languages out of the box).

**Q: My folder contains sub‑folders—will they be scanned?**  
A: Yes. `Files.walk` traverses the entire tree recursively, so every nested PNG/J

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}