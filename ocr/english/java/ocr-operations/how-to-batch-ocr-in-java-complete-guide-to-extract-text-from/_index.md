---
category: general
date: 2026-02-09
description: Learn how to batch OCR in Java with Aspose OCR. Extract text from images,
  recognize text from PNG, JPG, and TIFF files in a single call.
draft: false
keywords:
- how to batch ocr
- extract text from images
- recognize text from png
- recognize text from jpg
- recognize text from tiff
language: en
og_description: Master how to batch OCR in Java. This tutorial shows you how to extract
  text from PNG, JPG, and TIFF images using Aspose OCR with clear code examples.
og_title: How to Batch OCR in Java – Extract Text from Images Efficiently
tags:
- OCR
- Java
- Aspose
title: How to Batch OCR in Java – Complete Guide to Extract Text from Images
url: /java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Batch OCR in Java – Complete Guide to Extract Text from Images

Ever wondered **how to batch OCR** a handful of pictures without writing a loop for each file? You're not the only one. In many real‑world projects you get a folder full of scans—PNG receipts, JPG screenshots, or even multi‑page TIFFs—and you need the text fast.  

The good news is that Aspose OCR lets you do exactly that: a single method call that recognises text from PNG, JPG, and TIFF files all at once. In this tutorial we’ll walk through the entire process, from setting up the project to printing the results, so you can start extracting text from images today.

## What This Tutorial Covers

* **How to batch OCR** using Aspose’s `OcrBatchProcessor`.
* Ways to **extract text from images** of different formats (PNG, JPG, TIFF).
* Tips for controlling parallelism to keep your app responsive.
* A complete, runnable Java program you can copy‑paste and run immediately.

No prior experience with Aspose is required—just a basic Java installation and an IDE of your choice. By the end, you’ll have a solid foundation for recognising text from PNG, JPG, and TIFF files in bulk.

---

![Diagram illustrating how to batch OCR multiple image files](/images/batch-ocr-diagram.png "how to batch ocr")

*Image alt text: how to batch ocr diagram showing multiple image files processed together.*

## Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| Java 17 or newer | Aspose OCR targets modern JVMs. |
| Maven or Gradle | Simplifies adding the Aspose OCR library. |
| Basic Java knowledge | Needed to understand the code flow. |
| A set of sample images (`.png`, `.jpg`, `.tif`) | To see the extraction in action. |

If you already have these, great—let’s dive in.

## Step 1: Add Aspose OCR to Your Project

The first thing you need is the Aspose OCR JAR. With Maven, drop this into your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

If you prefer Gradle, the equivalent is:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

Adding the dependency pulls in everything required for **recognize text from png**, **recognize text from jpg**, and **recognize text from tiff**. No extra native libraries are needed.

## Step 2: Define the Image Files You Want to Process

Now we’ll tell the OCR engine which files to handle. This is where **how to batch OCR** really shines—just pass a list of paths and let the library do the heavy lifting.

```java
import java.util.Arrays;
import java.util.List;

// Step 2: List your image files (PNG, JPG, TIFF)
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/img1.png",   // PNG file – recognize text from png
        "YOUR_DIRECTORY/img2.jpg",   // JPG file – recognize text from jpg
        "YOUR_DIRECTORY/img3.tif");  // TIFF file – recognize text from tiff
```

> **Pro tip:** Keep your file paths absolute or use `Paths.get(...)` to avoid surprises on different OSes.

## Step 3: Create the Batch Processor and Tune Parallelism

Aspose OCR ships with `OcrBatchProcessor`, which can run several recognitions in parallel. Controlling the thread count prevents your app from hogging CPU when you have dozens of images.

```java
import com.aspose.ocr.OcrBatchProcessor;

// Step 3: Initialise the batch processor
OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();

// Limit to 4 concurrent threads – a sweet spot for most desktops
ocrProcessor.setMaxParallelism(4);
```

Why limit parallelism? If you run too many threads on a modest laptop, you might see a slowdown instead of a speed‑up. Setting `setMaxParallelism` lets you balance speed and stability.

## Step 4: Run the Batch OCR Call

Here’s the core of **how to batch OCR**: a single `recognize` call that returns a list of `RecognitionResult` objects, one per image.

```java
import com.aspose.ocr.RecognitionResult;
import java.util.List;

// Step 4: Execute batch OCR
List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);
```

The method blocks until every image is processed, then hands you the text. If you need non‑blocking behaviour, you can wrap this in a `CompletableFuture`, but for most scripts the synchronous call keeps the code tidy.

## Step 5: Print the Extracted Text

Finally, iterate over the results and display the recognised strings. This demonstrates that we have successfully **extract text from images** of various formats.

```java
// Step 5: Output the recognized text for each file
for (int i = 0; i < recognitionResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(recognitionResults.get(i).getText());
    System.out.println("---");
}
```

### Expected Output

```
File: YOUR_DIRECTORY/img1.png
The quick brown fox jumps over the lazy dog.
---
File: YOUR_DIRECTORY/img2.jpg
Invoice #12345
Total: $567.89
---
File: YOUR_DIRECTORY/img3.tif
Page 1 of 3
Report generated on 2026-02-09
---
```

If the OCR engine cannot read a file, the `getText()` method returns an empty string, so you can add a simple check to log warnings.

## Full Working Example

Putting everything together, here’s the complete, ready‑to‑run Java class. Copy it into a file named `BatchOcrTutorial.java`, adjust the image paths, and run `javac && java`.

```java
import com.aspose.ocr.*;
import java.util.Arrays;
import java.util.List;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {

        // Step 1: Define the image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/img1.png",
                "YOUR_DIRECTORY/img2.jpg",
                "YOUR_DIRECTORY/img3.tif");

        // Step 2: Create the batch OCR processor and optionally limit parallelism
        OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();
        ocrProcessor.setMaxParallelism(4); // limit to 4 concurrent threads

        // Step 3: Perform OCR on all images in a single batch call
        List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);

        // Step 4: Output the recognized text for each file
        for (int i = 0; i < recognitionResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(recognitionResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

Run it, and you’ll see the console print the extracted text for each PNG, JPG, and TIFF file—exactly what you need when **how to batch OCR** is the question on your mind.

## Common Questions & Edge Cases

### What if I have more than three images?

Just add more entries to the `imageFiles` list. The batch processor will automatically split the work across the threads you configured with `setMaxParallelism`.

### My images are in a sub‑folder—do I need to list each one manually?

You can programmatically collect all files with a specific extension:

```java
try (Stream<Path> paths = Files.walk(Paths.get("YOUR_DIRECTORY"))) {
    List<String> imageFiles = paths
        .filter(Files::isRegularFile)
        .filter(p -> p.toString().matches(".*\\.(png|jpg|tif|tiff)$"))
        .map(Path::toString)
        .collect(Collectors.toList());
}
```

This keeps the code flexible and still respects **how to batch OCR**.

### How do I handle low‑confidence results?

`RecognitionResult` provides a `getConfidence()` method. You can filter out results below a threshold and retry with higher DPI settings:

```java
ocrProcessor.setResolution(300); // increase DPI for better accuracy
```

### Does Aspose OCR support other languages?

Yes—just call `ocrProcessor.setLanguage(OcrLanguage.Spanish)` (or any supported enum) before the `recognize` call. This expands the utility beyond English, making **extract text from images** truly multilingual.

## Performance Tips

* **Batch size matters** – Larger batches reduce overhead, but very large lists may consume more memory. Test with 50–200 images per batch.
* **Parallelism** – On a 4‑core CPU, `setMaxParallelism(4)` usually yields the best throughput. Adjust based on your server’s workload.
* **Image preprocessing** – Converting images to grayscale or increasing contrast before OCR can improve accuracy, especially for noisy scans.

## Conclusion

You now know **how to batch OCR** in Java using Aspose OCR, how to **extract text from images** of various formats, and why controlling parallelism matters. The complete code example demonstrates recognising text from PNG, JPG, and TIFF files in a single, efficient call.

Ready for the next step? Try feeding the OCR output into a search index, a database, or even an AI summarizer. You could also experiment with PDF input (Aspose OCR supports it) or combine this with image‑preprocessing libraries like OpenCV for even higher accuracy.

Happy coding, and remember—batch OCR doesn’t have to be a headache. With the right tools and a clear pattern, you’ll be turning piles of pictures into searchable text in no time.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}