---
category: general
date: 2026-06-16
description: OCR bounding box tutorial in Java shows how to extract text from image,
  read text from image, and get OCR confidence score for JPG files.
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: en
og_description: OCR bounding box in Java lets you recognize text from JPG files, extract
  text from image, and view OCR confidence scores—all in a simple code example.
og_title: OCR Bounding Box in Java – Extract Text from Image
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: OCR Bounding Box in Java – Extract Text from Image
url: /java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Bounding Box in Java – Extract Text from Image

Ever wondered how to get the **ocr bounding box** for each piece of text in a Java image? In this tutorial we’ll show you how to **extract text from image** files, **read text from image**, and even see the **ocr confidence score** while you **recognize text from jpg** files. The short answer? A few lines of code using a modern OCR library, plus a bit of explanation about why each call matters.

Below you’ll find a complete, ready‑to‑run example, step‑by‑step breakdown, and a handful of practical tips you can copy straight into your own project. By the end, you’ll be able to output something like:

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## What You’ll Need

- **Java 11** or newer (the syntax below uses the `var` keyword for brevity, but you can drop it for older JDKs).  
- An OCR library that offers a Java API – for this guide we’ll use **[Tesseract4J](https://github.com/nguyenq/tess4j)**, a thin wrapper around the popular Tesseract engine.  
- A JPEG image (`.jpg`) that contains clear, printed text.  
- Your favorite IDE (IntelliJ IDEA, Eclipse, VS Code…) – any will do.

If you’re missing the library, just add this Maven dependency:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Now let’s dive in.

![OCR bounding box example](ocr-bounding-box.png "OCR bounding box example")

## OCR Bounding Box: Setting Up the Engine

The first thing you have to do is create an OCR engine instance. Think of it as turning on the scanner that will later read the pixels.

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**Why this matters:**  
Without setting the `datapath`, Tesseract won’t know where its language packs live, and you’ll get a cryptic “Failed loading language” error. The `setLanguage` call is optional if you only need the default English pack, but being explicit makes the code clearer for future readers.

## Load the Image You Want to Process

Next, feed the engine the JPEG you’d like to analyze. The library accepts a `File` or `BufferedImage`; we’ll use a `File` for simplicity.

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**Pro tip:**  
If your image lives in resources (e.g., inside a JAR), use `getResourceAsStream` and wrap it with `ImageIO.read`. That way the tutorial works both locally and in a packaged app.

## Perform OCR Recognition

Now we actually ask the engine to read the picture. The result is a plain‑text string, but we also want the **ocr confidence score** and the **ocr bounding box** for each line.

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**Why we use `getWords` instead of the plain `doOCR`:**  
`doOCR` gives you the raw string but discards spatial information. By calling `getWords` with `RIL_WORD` (or `RIL_TEXTLINE` if you prefer line‑level boxes), we retrieve a list of `Word` objects that each carry the text, confidence, and bounding rectangle. That’s the heart of the **ocr bounding box** feature.

## Understanding the Output

Running the snippet above against a clean JPEG yields output similar to:

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **Text** – the recognized characters.  
- **Confidence** – a floating‑point value between 0 and 1; higher means the engine is more sure.  
- **Box** – the rectangle that encloses the word in pixel coordinates (x, y, width, height).  

You can now **read text from image** and also know exactly where each snippet lives on the canvas—perfect for highlighting, cropping, or feeding into downstream NLP pipelines.

## Edge Cases & Common Pitfalls

| Situation | What to Watch For | Fix / Work‑around |
|-----------|-------------------|-------------------|
| Image is blurry or low‑contrast | Confidence scores drop dramatically (often below 0.6). | Pre‑process with OpenCV: increase contrast, apply thresholding. |
| JPEG contains rotated text | Bounding boxes appear skewed or missing. | Use `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)` to let Tesseract auto‑detect orientation. |
| Large images cause OutOfMemoryError | Java heap fills up when loading big pictures. | Downscale the image before OCR (`ImageIO.read` → `BufferedImage.getScaledInstance`). |
| You need line‑level boxes instead of word‑level | `RIL_WORD` returns per‑word boxes. | Switch to `ITesseract.PageIteratorLevel.RIL_TEXTLINE`. |
| Non‑English characters appear as � | Language data not loaded. | Download the appropriate `.traineddata` file and point `setDatapath` to its folder. |

Addressing these issues early saves you hours of debugging later.

## Full Working Example (All Steps in One File)

Below is a self‑contained Java class you can copy‑paste into a `src/main/java` folder and run with `mvn exec:java`. It pulls together everything we discussed.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.ITesseract.RenderedFormat;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;
import net.sourceforge.tess4j.Word;

import java.io.File;
import java.util.List;

public class OcrBoundingBoxDemo {

    public static void main(String[] args) {
        // ==== Step 1: Initialize the OCR engine ====
        ITesseract ocrEngine = new Tesseract();
        ocrEngine.setDatapath("tessdata"); // folder containing .traineddata files
        ocrEngine.setLanguage("eng");      // English language pack

        // Optional: improve accuracy for printed text
        ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO);
        ocrEngine.setOcrEngineMode(ITesseract.OEM_TESSERACT_ONLY);

        // ==== Step 2: Load the JPEG you want to read ====
        File imageFile = new File("YOUR_DIRECTORY


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}