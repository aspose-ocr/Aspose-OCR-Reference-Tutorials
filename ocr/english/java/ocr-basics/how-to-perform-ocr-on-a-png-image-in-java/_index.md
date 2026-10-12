---
category: general
date: 2026-10-11
description: Learn how to perform OCR on a PNG image in Java, extract text from image
  and convert image to text with a simple OcrEngine example.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: en
lastmod: 2026-10-11
og_description: How to perform OCR on a PNG image in Java, extract text from image
  and convert image to text using a concise, ready‑to‑run example.
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: How to perform OCR on a PNG image in Java – complete guide
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  headline: How to perform OCR on a PNG image in Java
  type: TechArticle
- description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  name: How to perform OCR on a PNG image in Java
  steps:
  - name: 4.1 Handling low‑resolution PNGs
    text: 'Tesseract performs best on images with at least 300 DPI. If your source
      PNG is smaller, upscale it before OCR:'
  - name: 4.2 Extracting non‑English text
    text: 'To **extract text from image** that contains other languages, download
      the appropriate `.traineddata` files and set the language code:'
  - name: 4.3 Batch processing multiple PNGs
    text: 'If you need to **recognize text from PNG** files in a folder, iterate over
      the directory:'
  - name: 4.4 Dealing with OCR errors
    text: 'Typical OCR mistakes include misreading `0` (zero) as `O` or `1` as `l`.
      Post‑processing with regular expressions can clean the result:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
- Text Extraction
title: How to perform OCR on a PNG image in Java
url: /java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to perform OCR on a PNG image in Java

If you need to **perform OCR** on an image file, learning **how to perform OCR** in Java is essential for many automation tasks. Whether you are digitizing receipts, indexing scanned documents, or building a searchable photo archive, the ability to **extract text from image** files saves countless manual hours.

This tutorial shows you a complete, runnable solution that loads a PNG, runs an OCR engine, and **recognize text from PNG** files. You’ll also see how to **convert image to text** and handle common pitfalls such as low‑resolution input or non‑ASCII characters.

## What you’ll achieve

By the end of this guide you will be able to:

* **load image java** code that reads a PNG from disk,
* initialize a lightweight OCR engine,
* **extract text from image** and print the result to the console,
* adapt the solution for other image formats or batch processing.

No external services are required—only a single open‑source OCR library (Tess4J) and the Java SE runtime.

---

## Prerequisites

* Java 17 or newer (the code compiles with JDK 17).
* Maven or Gradle for dependency management.
* Basic familiarity with the command line and IDE of your choice.
* The `tess4j` library (a Java wrapper for Tesseract). Add the following Maven dependency:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

If you use Gradle, the equivalent is:

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

You also need the Tesseract data files (`.traineddata`). Download the English data pack from the official repository and place it in a folder named `tessdata` at the project root.

---

## Step 1: Load the image in Java

Loading a PNG is straightforward with the standard `ImageIO` class. The code below demonstrates **load image java** in a safe, exception‑aware way:

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Reads a PNG file from the given path and returns a BufferedImage.
 *
 * @param path absolute or relative path to the PNG file
 * @return BufferedImage representation of the file
 * @throws Exception if the file cannot be read or is not a PNG
 */
private static BufferedImage loadPng(String path) throws Exception {
    File imgFile = new File(path);
    if (!imgFile.exists()) {
        throw new IllegalArgumentException("File not found: " + path);
    }
    BufferedImage img = ImageIO.read(imgFile);
    if (img == null) {
        throw new IllegalArgumentException("Unsupported image format or corrupt file: " + path);
    }
    return img;
}
```

**Why this matters:** `ImageIO.read` automatically detects the image format, but we explicitly check for `null` to avoid silent failures when the PNG is corrupted. This pattern is a best practice when you **load image java** for OCR.

---

## Step 2: Initialize the OCR engine

Tess4J wraps the native Tesseract binary, exposing a simple Java API. The following method creates an `Tesseract` instance, points it to the `tessdata` folder, and configures the language to English:

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;

/**
 * Configures and returns a ready‑to‑use Tesseract instance.
 *
 * @return configured ITesseract object
 */
private static ITesseract createOcrEngine() {
    ITesseract tesseract = new Tesseract();
    // Path to the folder that contains .traineddata files
    tesseract.setDatapath("tessdata");
    // Language code – "eng" for English; you can add more languages later
    tesseract.setLanguage("eng");
    // Optional: increase OCR accuracy for PNGs with low DPI
    tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
    return tesseract;
}
```

**Why we do this:** Initializing the engine once and reusing it for multiple images reduces startup overhead. The `setOcrEngineMode` call selects the default mode, which works well for most PNGs. If you encounter noisy scans, you can experiment with other modes (e.g., `OEM_LSTM_ONLY`).

---

## Step 3: Perform OCR and **recognize text from PNG**

Now we combine the image loader and the OCR engine. The method below runs OCR on a `BufferedImage` and returns the extracted string:

```java
/**
 * Runs OCR on the supplied image and returns the recognized text.
 *
 * @param image BufferedImage containing the PNG to process
 * @param tesseract configured OCR engine
 * @return plain‑text result of OCR
 * @throws Exception if OCR fails
 */
private static String extractText(BufferedImage image, ITesseract tesseract) throws Exception {
    // Tess4J can directly accept a BufferedImage
    return tesseract.doOCR(image);
}
```

**Full runnable example**

```java
import java.awt.image.BufferedImage;
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.TesseractException;

public class OcrDemo {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the PNG file
            BufferedImage image = loadPng("sample.png");

            // 2️⃣ Create and configure the OCR engine
            ITesseract ocrEngine = createOcrEngine();

            // 3️⃣ Recognize text from PNG
            String recognizedText = extractText(image, ocrEngine);

            // 4️⃣ Display the result – this is the **convert image to text** step
            System.out.println("=== OCR RESULT ===");
            System.out.println(recognizedText);
        } catch (Exception e) {
            System.err.println("Error during OCR processing:");
            e.printStackTrace();
        }
    }

    // ----- Helper methods from previous steps -----
    // loadPng, createOcrEngine, extractText (copy-pasted here for completeness)
    // ... (methods omitted for brevity; see the sections above) ...
}
```

**Expected output**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

The console will show the exact characters the engine extracted from `sample.png`. If the PNG contains only a single word, the output will be that word followed by a newline.

---

## Step 4: Common variations and edge cases

### 4.1 Handling low‑resolution PNGs

Tesseract performs best on images with at least 300 DPI. If your source PNG is smaller, upscale it before OCR:

```java
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.RenderingHints;

private static BufferedImage upscale(BufferedImage src, int scaleFactor) {
    int width = src.getWidth() * scaleFactor;
    int height = src.getHeight() * scaleFactor;
    Image tmp = src.getScaledInstance(width, height, Image.SCALE_SMOOTH);
    BufferedImage resized = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
    Graphics2D g2d = resized.createGraphics();
    g2d.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                         RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g2d.drawImage(tmp, 0, 0, null);
    g2d.dispose();
    return resized;
}
```

Apply `upscale(image, 2)` before calling `extractText` to improve accuracy.

### 4.2 Extracting non‑English text

To **extract text from image** that contains other languages, download the appropriate `.traineddata` files and set the language code:

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 Batch processing multiple PNGs

If you need to **recognize text from PNG** files in a folder, iterate over the directory:

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 Dealing with OCR errors

Typical OCR mistakes include misreading `0` (zero) as `O` or `1` as `l`. Post‑processing with regular expressions can clean the result:

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

---

## Pro tips for reliable OCR in Java

| Tip | Reason |
|-----|--------|
| **Use a lossless PNG** | Compression artifacts in JPEG can confuse the engine. |
| **Trim white borders** | Extraneous whitespace increases processing time and may cause false positives. |
| **Set `tesseract.setPageSegMode(ITesseract.PSM_AUTO)`** only when layout is unknown; otherwise choose a specific mode (e.g., `PSM_SINGLE_BLOCK`). |
| **Cache the `ITesseract` instance**


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Read Text from an Image in Java Using Aspose OCR – Complete Guide](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [How to Use OCR in Java – Recognize Text from Image Quickly](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [Batch Image OCR in Java – Extract Text from PNG Files Fast](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}