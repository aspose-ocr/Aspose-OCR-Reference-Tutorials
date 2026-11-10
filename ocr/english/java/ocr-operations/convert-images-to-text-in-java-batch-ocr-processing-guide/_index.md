---
category: general
date: 2026-08-28
description: Learn how to extract text from png images in Java using Aspose OCR. This
  tutorial covers batch OCR processing, reading images from a folder, and filtering
  files by extension.
draft: false
images:
- /java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/og-image.png
keywords:
- extract text from png
- read images from folder
- filter files by extension
- how to batch ocr
- aspose ocr java tutorial
language: en
lastmod: 2026-08-28
og_description: Learn how to extract text from png images in Java using Aspose OCR.
  This tutorial covers batch OCR processing, reading images from a folder, and filtering
  files by extension.
og_image_alt: 'Developer guide: extract text from png images in Java using Aspose
  OCR'
og_title: How to extract text from png in Java – batch OCR guide
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Learn how to extract text from png images in Java using Aspose OCR.
    This tutorial covers batch OCR processing, reading images from a folder, and filtering
    files by extension.
  headline: How to extract text from png in Java – batch OCR guide
  type: TechArticle
- questions:
  - answer: Absolutely. Aspose OCR supports 30+ formats—including PDF, TIFF, BMP,
      and GIF—so just add the desired extensions to the filter in the directory‑walk
      step.
    question: Can I process PDFs or TIFFs as well?
  - answer: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`
      (or any supported language). The language packs are bundled with the library,
      so no extra download is required.
    question: What if I need a language other than English, such as Spanish?
  - answer: Yes. `Files.walk` traverses the entire tree recursively, so every nested
      PNG/J
    question: My folder contains sub‑folders—will they be scanned?
  - answer: Enable streaming mode by calling `ocrEngine.setUseStreaming(true)`. This
      tells the engine to read the image in chunks, dramatically reducing peak memory
      usage.
    question: How do I handle extremely large images that exceed 200 MB?
  - answer: Yes. When constructing `ParallelRecognizer`, pass the desired maximum
      thread count as the second argument (e.g., `new ParallelRecognizer(ocrEngine,
      4)`).
    question: Is there a way to limit the number of concurrent OCR threads?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: How to extract text from png in Java – batch OCR guide
url: /java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to extract text from png in Java – batch OCR guide

If you’ve ever needed to **extract text from png** files but weren’t sure how to scale the operation beyond a handful of pictures, you’re in the right place. Many developers start with a single‑image OCR call and quickly hit performance walls when the folder grows to dozens or hundreds of files. With Aspose OCR for Java you can spin up a robust batch OCR pipeline that walks a directory, filters only the image types you care about, runs recognition in parallel, and returns the results in the same order as the source files. By the end of this guide you’ll have a ready‑to‑drop Java snippet that handles **batch OCR processing** reliably and efficiently.

![Convert images to text example](https://example.com/convert-images-to-text.png "Screenshot of Java console output showing converted text from PNG files")

## Quick answers
- **What library handles OCR?** Aspose OCR for Java.
- **Can I process PNG and JPG together?** Yes – the sample filters both extensions.
- **Is the OCR engine thread‑safe?** A single shared `AsposeOCR` instance is safe for concurrent use.
- **Do I need a license for testing?** A free temporary key is available from Aspose.
- **Will sub‑folders be scanned automatically?** `Files.walk` traverses the whole tree recursively.

## What is extract text from png?

`extract text from png` refers to the process of applying optical character recognition (OCR) to Portable Network Graphics files so that the visible characters become searchable, editable strings. Aspose OCR’s engine reads pixel data, identifies glyph shapes, and returns Unicode text in a single method call.

## Why use Aspose OCR for Java?

Aspose OCR supports **30+ languages**, processes up to **500 images per minute** on a standard 8‑core server, and can handle files up to **200 MB** without loading the entire image into memory. Those quantified capabilities mean you can reliably run large‑scale batch jobs on commodity hardware without hitting memory limits.

## Prerequisites
- Java 17 (or any recent LTS version).
- Maven or Gradle for dependency management.
- A directory containing PNG/JPG images you wish to process.
- Basic familiarity with Java streams and the `java.nio.file` package.
- (Optional) An Aspose OCR temporary license key for evaluation.

> **Pro tip:** The free temporary key expires after 30 days, but it gives you full API access for testing.

## How does the batch OCR pipeline maintain order?

`Future<OcrResult>` represents a pending OCR result that can be retrieved once processing finishes. The pipeline preserves the original file order by storing the `Future<OcrResult>` objects in a list that mirrors the order of the input `Path` collection. When you later iterate over the futures and call `get()`, each call blocks only for its corresponding image, so the output sequence matches the input sequence without extra sorting logic.

## What is Aspose OCR for Java?

`AsposeOCR` is the core class of the Aspose OCR library that encapsulates all language packs, recognition settings, and internal native resources. It is designed to be instantiated once per application lifetime and safely shared across multiple threads. Because it loads language data only once, reusing the same instance reduces initialization overhead and improves throughput for batch operations.

## How to set up the project and add Aspose OCR

First, create a Maven (or Gradle) project and add the Aspose OCR dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

> **Why this matters:** Declaring the dependency up front ensures the compiler can see `AsposeOCR`, `ParallelRecognizer`, and related classes. It also guarantees that the same version is used across all machines, which is crucial for reproducible **batch OCR processing**.

Refresh your IDE after the build completes; you should now see the Aspose packages under **External Libraries**.

## How to initialise the OCR engine – share a single instance

`AsposeOCR` is the main OCR engine class provided by the Aspose OCR library. We only need **one** OCR engine instance for the whole run. Sharing it across threads saves memory and speeds things up because the engine loads language packs just once.

```java
AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");
```

`AsposeOCR` is thread‑safe, so you can safely hand it to a `ParallelRecognizer` that will manage a pool of worker threads.

> **Explanation:** `ParallelRecognizer` wraps the engine in a thread‑pool. When you submit many files, each gets its own worker thread, enabling true parallelism on multi‑core CPUs.

## How to read images from folder – walk the directory tree

`Files.walk` is a Java NIO method that recursively traverses a file tree and returns a stream of `Path` objects. Now we need to **read images from folder** and collect every PNG or JPG. The `Files.walk` API makes this a one‑liner, but we’ll add a filter to **extract text from png** only when needed.

```java
List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
    .filter(Files::isRegularFile)
    .filter(p -> {
        String lower = p.toString().toLowerCase();
        return lower.endsWith(".png") || lower.endsWith(".jpg");
    })
    .collect(Collectors.toList());
```

> **Why we filter here:** Using `filter` lets us **filter files by extension** early, which slashes unnecessary I/O later. It also keeps the code readable—no need for complex regexes.

## How to submit OCR jobs asynchronously

`recognizeAsync` submits an image to the OCR engine for asynchronous processing and returns a `Future<OcrResult>` representing the pending result. With the list of files ready, we push each path to the `ParallelRecognizer`. The `recognizeAsync` method returns a `Future<OcrResult>` that we store for later retrieval.

```java
ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine, Runtime.getRuntime().availableProcessors());
List<Future<OcrResult>> futures = new ArrayList<>();

for (Path imagePath : imagePaths) {
    futures.add(recognizer.recognizeAsync(imagePath));
}
```

> **What’s happening under the hood?** Each call enqueues a task into the recognizer’s internal executor service. The tasks run in parallel, so a folder with 100 images can be processed in a fraction of the time a single‑threaded loop would take.

## How to retrieve results while preserving file sequence

`Future<OcrResult>` holds the result of an asynchronous OCR task and provides a `get()` method to obtain the recognized text. Because we stored the futures in the same order as `imagePaths`, we can simply iterate over the list and call `get()`. The call blocks only until that particular image is done, preserving order without extra bookkeeping.

```java
for (int i = 0; i < futures.size(); i++) {
    try {
        OcrResult result = futures.get(i).get();
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println("Text: " + result.getText());
    } catch (Exception e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**Sample console output** (truncated for brevity):

```
File: invoice1.png
Text: Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...
```

> **Edge case handling:** If a particular image throws an exception (corrupt file, unsupported format), we catch it and continue processing the rest—an essential habit for reliable **batch OCR processing** pipelines.

## How to clean up resources – shut down the recognizer

`ParallelRecognizer.shutdown()` stops the internal thread pool, ensuring all OCR tasks complete before the application exits. Never forget to shut down the internal thread pool; otherwise your JVM may hang on exit.

```java
recognizer.shutdown();
```

That’s it! The program now walks any directory, filters for PNG/JPG files, runs OCR in parallel, and prints the results in the original order.

---

## Full working example (copy‑and‑paste)

Below is the complete, ready‑to‑run Java class. Replace `"YOUR_DIRECTORY"` with the path to your images folder and run it from your IDE or the command line.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

public class BatchOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine (single shared instance)
        AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");

        // Create a parallel recognizer that uses a thread pool
        ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine,
                Runtime.getRuntime().availableProcessors());

        // Walk the directory and collect PNG/JPG files
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(Files::isRegularFile)
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        // Submit OCR jobs asynchronously
        List<Future<OcrResult>> futures = new ArrayList<>();
        for (Path imagePath : imagePaths) {
            futures.add(recognizer.recognizeAsync(imagePath));
        }

        // Retrieve results in the original order
        for (int i = 0; i < futures.size(); i++) {
            try {
                OcrResult result = futures.get(i).get();
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println("Text: " + result.getText());
            } catch (Exception e) {
                System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Clean up the recognizer's thread pool
        recognizer.shutdown();
    }
}
```

Run the class, watch the console fill with extracted strings, and celebrate the fact that you just **converted images to text** without writing a single loop that blocks on I/O.

---

## Frequently asked questions (FAQs)

**Q: Can I process PDFs or TIFFs as well?**  
A: Absolutely. Aspose OCR supports 30+ formats—including PDF, TIFF, BMP, and GIF—so just add the desired extensions to the filter in the directory‑walk step.

**Q: What if I need a language other than English, such as Spanish?**  
A: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH` (or any supported language). The language packs are bundled with the library, so no extra download is required.

**Q: My folder contains sub‑folders—will they be scanned?**  
A: Yes. `Files.walk` traverses the entire tree recursively, so every nested PNG/J

**Q: How do I handle extremely large images that exceed 200 MB?**  
A: Enable streaming mode by calling `ocrEngine.setUseStreaming(true)`. This tells the engine to read the image in chunks, dramatically reducing peak memory usage.

**Q: Is there a way to limit the number of concurrent OCR threads?**  
A: Yes. When constructing `ParallelRecognizer`, pass the desired maximum thread count as the second argument (e.g., `new ParallelRecognizer(ocrEngine, 4)`).

---

---

**Last Updated:** 2026-08-28  
**Tested with:** Aspose OCR for Java 24.10  
**Author:** Aspose  






```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

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

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

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

## Related Tutorials

- [Convert Images To Text In Java Batch Ocr Processing Guide](/ocr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/)
- [Read Text From Image In Java Complete Aspose Ocr Guide](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Extract Text from Images Using Aspose.OCR – Allowed Characters](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}