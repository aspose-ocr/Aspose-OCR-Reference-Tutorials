---
category: general
date: 2026-09-18
description: Learn how to extract text from images in Java using Aspose OCR. Batch
  process PNG, JPG, and TIFF files efficiently in a single call.
images:
- /java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/og-image.png
keywords:
- extract text from images
- convert images to text
- how to batch ocr
- extract text from png
- extract text from jpg
- extract text from tiff
language: en
lastmod: 2026-09-18
og_description: Master how to extract text from images in Java with batch OCR. Use
  Aspose OCR to convert PNG, JPG, and TIFF files in one call.
og_image_alt: Diagram showing multiple image files processed together for batch OCR
og_title: Extract text from images in Java – batch OCR guide
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to extract text from images in Java using Aspose OCR. Batch
    process PNG, JPG, and TIFF files efficiently in a single call.
  headline: How to extract text from images in Java by batch OCR
  type: TechArticle
- questions:
  - answer: Yes, Aspose OCR is pure Java and requires no UI components, so it works
      perfectly on headless environments.
    question: Can I run this on a headless server?
  - answer: A commercial license is needed for production deployments; a free trial
      is available for evaluation.
    question: Is a license required for production use?
  - answer: Any OS that can run Java 17+, including Windows, Linux, and macOS.
    question: Which operating systems are supported?
  - answer: Over 60 languages are supported out of the box, ranging from English and
      Spanish to Arabic and Chinese.
    question: How many languages can Aspose OCR recognise?
  - answer: Individual image files up to 200 MB are supported; larger files should
      be split before processing.
    question: What is the maximum file size Aspose OCR can handle?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: How to extract text from images in Java by batch OCR
url: /java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to extract text from images in Java by batch OCR

If you need to **extract text from images** quickly and without writing a loop for each file, batch OCR is the answer. In many real‑world projects you receive a folder full of scans—PNG receipts, JPG screenshots, or multi‑page TIFFs—and you must turn them into searchable text. Aspose OCR lets you do exactly that with a single method call that processes PNG, JPG, and TIFF files together, saving both development time and CPU cycles.

## Quick answers
- **What does batch OCR do?** It processes multiple image files in one request, returning text for each file.
- **Which formats are supported?** PNG, JPG/JPEG, and multi‑page TIFF are handled out of the box.
- **Do I need a separate native library?** No, the Aspose OCR JAR contains everything you need.
- **Can I control how many threads run?** Yes, use `setMaxParallelism` on the batch processor.
- **What Java version is required?** Java 17 or newer.

## What is Aspose OCR?
Aspose OCR is a Java library that recognises printed and handwritten text in image files without external dependencies. It supports over 60 languages and can process up to 100 images per batch, making it ideal for large‑scale document digitisation.

## What this tutorial covers
Load a list of image paths, create an `OcrBatchProcessor`, tune parallelism, run a single `recognize` call, and print the extracted strings. By the end you’ll have a ready‑to‑run Java program that extracts text from PNG, JPG, and TIFF files in bulk.

- **How to batch OCR** using Aspose’s `OcrBatchProcessor`.
- Ways to **extract text from images** of different formats (PNG, JPG, TIFF).
- Tips for controlling parallelism to keep your app responsive.
- A complete, runnable Java program you can copy‑paste and execute immediately.

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

## Step 1: add Aspose OCR to your project

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

Adding the dependency pulls in everything required for **extract text from png**, **extract text from jpg**, and **extract text from tiff**. No extra native libraries are needed.

## Step 2: define the image files you want to process

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

## Step 3: create the batch processor and tune parallelism

Aspose OCR ships with `OcrBatchProcessor`, which can run several recognitions in parallel. Controlling the thread count prevents your app from hogging CPU when you have dozens of images.

```java
import com.aspose.ocr.OcrBatchProcessor;

// Step 3: Initialise the batch processor
OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();

// Limit to 4 concurrent threads – a sweet spot for most desktops
ocrProcessor.setMaxParallelism(4);
```

Why limit parallelism? If you run too many threads on a modest laptop, you might see a slowdown instead of a speed‑up. Setting `setMaxParallelism` lets you balance speed and stability.

## Step 4: run the batch OCR call

Here’s the core of **how to batch OCR**: a single `recognize` call that returns a list of `RecognitionResult` objects, one per image.  
`recognize` processes the supplied images and returns a list of `RecognitionResult` objects, each containing the extracted text.

```java
import com.aspose.ocr.RecognitionResult;
import java.util.List;

// Step 4: Execute batch OCR
List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);
```

The method blocks until every image is processed, then hands you the text. If you need non‑blocking behaviour, you can wrap this in a `CompletableFuture`, but for most scripts the synchronous call keeps the code tidy.

## Step 5: print the extracted text

Finally, iterate over the results and display the recognised strings. This demonstrates that we have successfully **extract text from images** of various formats.  
`RecognitionResult` holds the OCR output for a single image, including the extracted text and confidence score.

```java
// Step 5: Output the recognized text for each file
for (int i = 0; i < recognitionResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(recognitionResults.get(i).getText());
    System.out.println("---");
}
```

### Expected output

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

## Full working example

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

## Common questions & edge cases

### What if I have more than three images?
Just add more entries to the `imageFiles` list. The batch processor will automatically split the work across the threads you configured with `setMaxParallelism`.

### My images are in a sub‑folder—do I need to list each one manually?
`Files.list` returns a lazily populated stream of paths in a directory.

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
`getConfidence()` returns a numeric confidence value indicating how likely the recognized text is correct.

```java
ocrProcessor.setResolution(300); // increase DPI for better accuracy
```

### Does Aspose OCR support other languages?
Yes—call `ocrProcessor.setLanguage(OcrLanguage.Spanish)` (or any supported enum) before the `recognize` call. This expands the utility beyond English, making **extract text from images** truly multilingual.

## Performance tips

* **Batch size matters** – Larger batches reduce overhead, but very large lists may consume more memory. Test with 50–200 images per batch.
* **Parallelism** – On a 4‑core CPU, `setMaxParallelism(4)` usually yields the best throughput. Adjust based on your server’s workload.
* **Image preprocessing** – Converting images to grayscale or increasing contrast before OCR can improve accuracy, especially for noisy scans.

## Conclusion

You now know **how to batch OCR** in Java using Aspose OCR, how to **extract text from images** of various formats, and why controlling parallelism matters. The complete code example demonstrates recognising text from PNG, JPG, and TIFF files in a single, efficient call.

Ready for the next step? Feed the OCR output into a search index, a database, or an AI summariser. You could also experiment with PDF input (Aspose OCR supports it) or combine this with image‑preprocessing libraries like OpenCV for even higher accuracy.

Happy coding, and remember—batch OCR doesn’t have to be a headache. With the right tools and a clear pattern, you’ll be turning piles of pictures into searchable text in no time.

## Frequently asked questions

**Q: Can I run this on a headless server?**  
A: Yes, Aspose OCR is pure Java and requires no UI components, so it works perfectly on headless environments.

**Q: Is a license required for production use?**  
A: A commercial license is needed for production deployments; a free trial is available for evaluation.

**Q: Which operating systems are supported?**  
A: Any OS that can run Java 17+, including Windows, Linux, and macOS.

**Q: How many languages can Aspose OCR recognise?**  
A: Over 60 languages are supported out of the box, ranging from English and Spanish to Arabic and Chinese.

**Q: What is the maximum file size Aspose OCR can handle?**  
A: Individual image files up to 200 MB are supported; larger files should be split before processing.

---

**Last Updated:** 2026-09-18  
**Tested with:** Aspose OCR 24.9 for Java  
**Author:** Aspose

## Related Tutorials

- [Extract Text from Images – OCR Basics for Java](/ocr/java/ocr-basics/)
- [How To Batch Ocr In Java Complete Guide To Extract Text From](/ocr/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/)
- [Preprocess Image Ocr In Java Boost Accuracy Extract Text](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}