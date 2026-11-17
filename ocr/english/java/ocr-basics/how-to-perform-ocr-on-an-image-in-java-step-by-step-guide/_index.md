---
category: general
date: 2026-11-17
description: Learn how to perform OCR on an image in Java and extract text from pictures
  using a simple code example. Includes read image Java tips.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text image
- read image java
- convert image to text
- image to text java
language: en
lastmod: 2026-11-17
og_description: How to perform OCR on an image in Java and extract text quickly. Follow
  this guide to read image Java and convert image to text with a ready‑to‑run example.
og_image_alt: Screenshot showing Java code that performs OCR on an image
og_title: How to perform OCR on an image in Java – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Learn how to perform OCR on an image in Java and extract text from
    pictures using a simple code example. Includes read image Java tips.
  headline: How to perform OCR on an image in Java – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Java
- Image processing
- Text extraction
title: How to perform OCR on an image in Java – step‑by‑step guide
url: /java/ocr-basics/how-to-perform-ocr-on-an-image-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to perform OCR on an image in Java – step‑by‑step guide

If you need to **how to perform OCR** on a picture, this tutorial shows you a complete, runnable solution in Java. You’ll see how to read an image file, configure an OCR engine, and extract the text that the engine recognizes.

Working with scanned documents, receipts, or screenshots often requires converting the visual content into searchable text. This guide walks you through every step, from loading the image to printing the extracted text, and it also covers common pitfalls such as unsupported file formats and null results.

## Prerequisites

Before you start, make sure you have:

* Java Development Kit (JDK) 8 or newer installed.
* A build tool (Maven or Gradle) to pull the OCR library.
* An image file (JPEG, PNG, BMP) that you want to process.

The code uses the **OCR library from the `com.asprise.ocr` package** because it requires only a single JAR and works on all major platforms. Replace it with another provider (Tesseract, Google Vision, etc.) by swapping the import statements and engine‑initialisation code.

## Step 1: Add the OCR dependency

If you use Maven, add the following dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.2.0</version>
</dependency>
```

For Gradle, place this line in `build.gradle`:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.2.0'
```

These lines ensure that the **read image Java** code can compile and that the OCR engine is available at runtime.

## Step 2: Read the image with Java

Reading an image file is the first concrete step in any **extract text image** workflow. Java’s built‑in `ImageIO` class handles most common formats.

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Loads an image from the supplied path.
 *
 * @param path absolute or relative path to the image file
 * @return a BufferedImage instance, or null if the file cannot be read
 */
private static BufferedImage loadImage(String path) {
    try {
        return ImageIO.read(new File(path));
    } catch (Exception e) {
        System.err.println("Failed to read image: " + e.getMessage());
        return null;
    }
}
```

**Why this matters:** `ImageIO.read` returns `null` for unsupported formats or corrupted files. The method above logs the problem and returns `null` so the next step can react gracefully.

## Step 3: Create and configure the OCR engine

The OCR engine must know which language to recognize. Setting the language improves accuracy dramatically, especially for non‑English documents.

```java
import com.asprise.ocr.Ocr;

/**
 * Instantiates an OCR engine configured for English.
 *
 * @return a ready‑to‑use Ocr object
 */
private static Ocr createEngine() {
    Ocr ocrEngine = new Ocr();
    // The first argument is the language; "eng" is the ISO code for English.
    ocrEngine.startEngine("eng", Ocr.SPEED_FAST);
    return ocrEngine;
}
```

**Why this matters:** Starting the engine is a relatively heavy operation, so you should create it once and reuse it for multiple images if your application processes batches.

## Step 4: Perform OCR and convert the image to text

Now that the image is loaded and the engine is ready, you can run the recognition step. This is the core of **how to perform OCR**.

```java
/**
 * Runs OCR on a BufferedImage and returns the recognized text.
 *
 * @param ocrEngine an initialized Ocr instance
 * @param image     the image to process
 * @return the extracted text, or an empty string if nothing is recognized
 */
private static String extractText(Ocr ocrEngine, BufferedImage image) {
    if (image == null) {
        return "";
    }
    // The third parameter (0) tells the engine to return plain text.
    String result = ocrEngine.recognize(image, 0);
    return result != null ? result.trim() : "";
}
```

**Edge‑case handling:** If the image is `null`, the method returns an empty string instead of throwing a `NullPointerException`. This makes the surrounding code more robust when dealing with user‑supplied files.

## Step 5: Display the extracted text

Finally, print the result to the console or forward it to another component (e.g., a database or a UI widget).

```java
/**
 * Demonstrates the full OCR workflow.
 *
 * @param args command‑line arguments (first argument = path to image)
 */
public static void main(String[] args) {
    if (args.length == 0) {
        System.err.println("Usage: java OcrDemo <path-to-image>");
        return;
    }

    String imagePath = args[0];
    BufferedImage image = loadImage(imagePath);
    Ocr ocrEngine = createEngine();

    String text = extractText(ocrEngine, image);
    System.out.println("=== Recognized Text ===");
    System.out.println(text.isEmpty() ? "(no text detected)" : text);

    // Clean up the OCR engine to free native resources.
    ocrEngine.stopEngine();
}
```

When you run the program with `java OcrDemo sample.jpg`, the console shows the recognized characters. This completes the **convert image to text** cycle.

### Expected output

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

If the image contains no readable characters, the program prints `(no text detected)`.

## Common variations and how to adapt them

| Variation | What changes | When to use |
|-----------|--------------|-------------|
| **Different language** | Replace `"eng"` with `"spa"` for Spanish, `"fra"` for French, etc. | Documents written in a language other than English |
| **Batch processing** | Loop over a list of file paths, reuse the same `Ocr` instance. | Large sets of scanned pages |
| **Higher accuracy** | Use `Ocr.SPEED_SLOW` or enable `ocrEngine.setConfig("tessedit_char_whitelist", "0123456789")` for numeric-only scans. | When OCR quality is critical (e.g., invoice numbers) |
| **Tesseract alternative** | Swap the import to `net.sourceforge.tess4j.Tesseract` and adjust the initialization code. | Projects that already depend on Tesseract |

## Pro tips

* **Resize large images** before feeding them to the engine; OCR speed scales with pixel count.
* **Pre‑process** the image (grayscale, contrast boost) using libraries such as OpenCV if the source is noisy.
* **Cache the OCR engine** if you call it many times in a short period—starting and stopping the engine incurs overhead.
* **Validate the result** with regular expressions when you expect a specific format (e.g., dates, phone numbers).

## Conclusion

You now know **how to perform OCR** on an image in Java, from reading the file to displaying the extracted text. The tutorial covered **read image Java**, **extract text image**, **convert image to text**, and **image to text java** techniques, and it provided practical tips for real‑world scenarios.  

From here you can:

* Integrate the OCR step into a web service that receives uploads.
* Combine the output with a search index for full‑text search over scanned documents.
* Explore advanced OCR options such as multi‑language support or custom character sets.

Happy coding, and enjoy turning pictures into searchable text!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Use OCR in Java – Extract Text from Image with Spell Correction](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/)
- [Convert Image to Text in Java Using Aspose OCR – Full Guide](/ocr/english/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/)
- [How to Enable GPU for OCR in Java – Extract Text from Image](/ocr/english/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}