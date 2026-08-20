---
title: "How to Use OCR – Extract Text from Images with Aspose.OCR"
linktitle: Specifying Allowed Characters in Aspose.OCR
second_title: Aspose.OCR Java API
description: "Discover how to use OCR with Aspose.OCR for Java, extract text from images, set allowed characters, and apply a temporary license in minutes."
weight: 15
url: /java/advanced-ocr-techniques/specify-allowed-characters/
date: 2026-05-24
keywords:
- how to use OCR
- extract text from images
- how to apply license
- how to set characters
schemas:
- type: TechArticle
  headline: How to Use OCR – Extract Text from Images with Aspose.OCR
  description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  dateModified: '2026-05-24'
  author: Aspose
- type: HowTo
  name: How to Use OCR – Extract Text from Images with Aspose.OCR
  description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  steps:
  - name: Set Your Document Directory
    text: Choose a folder where OCR results and temporary files will be stored. This
      path is later used to locate the image you want to process.
  - name: Specify the Image Path
    text: Provide the full file system path or a class‑path resource location that
      points to the image you wish to analyse.
  - name: Create an Aspose.OCR Instance
    text: '`AsposeOCR` is the core engine that performs optical character recognition.
      Instantiate it with either a temporary or permanent license string.'
  - name: Perform OCR Recognition
    text: '`RecognizeLine` extracts a single line of text from the supplied image
      and returns it as a plain Java `String`. You can call this method repeatedly
      for multi‑line documents. > **Pro tip:** If you need to restrict the output
      to digits only (e.g., for invoice numbers), call `setAllowedCharacters("0123'
- type: FAQPage
  questions:
  - question: How can I obtain a temporary license for Aspose.OCR?
    answer: Visit the [temporary license page](https://purchase.aspose.com/temporary-license/)
      to request a trial key that removes evaluation watermarks.
  - question: Where can I find support for Aspose.OCR?
    answer: Join the community at the [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16)
      for help and discussions.
  - question: Can I specify allowed characters in Aspose.OCR?
    answer: Yes, use the `setAllowedCharacters` API to define a custom whitelist of
      characters. This is ideal for numeric‑only fields.
  - question: Is Aspose.OCR compatible with the latest JDK versions?
    answer: Absolutely—Aspose.OCR is regularly updated to stay compatible with the
      newest Java releases.
  - question: Are there additional OCR features beyond line recognition?
    answer: The library also supports block, paragraph, and full‑page recognition,
      language packs, and advanced image preprocessing.
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use OCR – Extract Text from Images with Aspose.OCR

In modern Java applications, **how to use OCR** is a frequent question, especially when you need to turn scanned invoices, receipts, or printed forms into searchable text. This tutorial walks you through a complete **Aspose.OCR for Java** example: extracting text from images, restricting the output to a custom character set, and applying a temporary license for quick evaluation.

## Quick Answers
- **What does Aspose.OCR do?** It extracts text from images with high accuracy and lets you limit recognized characters.  
- **Do I need a license?** A temporary or permanent license is required for production use; the temporary key removes watermarks.  
- **Which JDK version is supported?** The library works with the latest JDK releases (JDK 17, 19, 21).  
- **Can I limit recognized characters?** Yes—use the `setAllowedCharacters` method to restrict output.  
- **How long does the setup take?** Roughly 10‑15 minutes for a basic end‑to‑end implementation.

## What is “extract text from images”?
Extracting text from images, also known as optical character recognition (OCR), converts visual characters—whether printed, handwritten, or typed—into machine‑readable strings. This transformation enables applications to search, index, edit, and analyze the content programmatically, supporting workflows such as invoice processing, document archiving, and data entry automation.

## Why Use Aspose.OCR for Java?
Aspose.OCR supports **60+ languages**, can process images up to **10 MB** without loading the entire file into memory, and delivers **>95 % accuracy** on clean scans. The library is self‑contained, requiring no external OCR engines, which simplifies deployment and reduces licensing overhead.

## Prerequisites

### Java Development Kit (JDK)

Make sure you have the latest Java Development Kit installed. You can download it from [here](https://www.oracle.com/java/technologies/javase-downloads.html).

### Aspose.OCR for Java Library

Download and install the Aspose.OCR for Java library from the [download link](https://releases.aspose.com/ocr/java/).

### Aspose.OCR License

To unlock full functionality, obtain a license. You can purchase one from [here](https://purchase.aspose.com/buy) or request a [temporary license](https://purchase.aspose.com/temporary-license/) for trial purposes.

## How to Use OCR with Aspose.OCR for Java?

Load your image, configure the OCR engine, and call the recognition method—all in a few straightforward lines. This direct‑answer paragraph tells you exactly what to do: create an `AsposeOCR` instance with your license string, set any allowed characters, and invoke `RecognizeLine` on the target image to receive the extracted text. The API handles image preprocessing internally, so you get clean results without extra code.

### Import Packages

The `AsposeOCR` class lives in the `com.aspose.ocr` package. Import the required classes before you start coding.

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## Step‑by‑Step Guide

### Step 1: Set Your Document Directory

Choose a folder where OCR results and temporary files will be stored. This path is later used to locate the image you want to process.

```java
String dataDir = "Your Document Directory";
```

### Step 2: Specify the Image Path

Provide the full file system path or a class‑path resource location that points to the image you wish to analyse.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### Step 3: Create an Aspose.OCR Instance

`AsposeOCR` is the core engine that performs optical character recognition. Instantiate it with either a temporary or permanent license string.

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### Step 4: Perform OCR Recognition

`RecognizeLine` extracts a single line of text from the supplied image and returns it as a plain Java `String`. You can call this method repeatedly for multi‑line documents.

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Pro tip:** If you need to restrict the output to digits only (e.g., for invoice numbers), call `setAllowedCharacters("0123456789")` on the `AsposeOCR` instance before invoking `RecognizeLine`. This forces the engine to ignore any non‑numeric symbols.  
> `setAllowedCharacters` is a method of `AsposeOCR` that restricts the OCR output to a specified whitelist of characters.

## Common Issues and Solutions

| Issue | Reason | Fix |
|-------|--------|-----|
| **No output or empty string** | Incorrect image path or unsupported format | Verify `imagePath` and use a supported format (JPEG, PNG, BMP) |
| **Recognition errors** | Low‑resolution image or noisy background | Pre‑process the image (increase contrast, binarize) before OCR |
| **License not applied** | Missing or invalid license key | Ensure the license string is correct and passed to the `AsposeOCR` constructor |

## Frequently Asked Questions

**Q: How can I obtain a temporary license for Aspose.OCR?**  
A: Visit the [temporary license page](https://purchase.aspose.com/temporary-license/) to request a trial key that removes evaluation watermarks.

**Q: Where can I find support for Aspose.OCR?**  
A: Join the community at the [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16) for help and discussions.

**Q: Can I specify allowed characters in Aspose.OCR?**  
A: Yes, use the `setAllowedCharacters` API to define a custom whitelist of characters. This is ideal for numeric‑only fields.

**Q: Is Aspose.OCR compatible with the latest JDK versions?**  
A: Absolutely—Aspose.OCR is regularly updated to stay compatible with the newest Java releases.

**Q: Are there additional OCR features beyond line recognition?**  
A: The library also supports block, paragraph, and full‑page recognition, language packs, and advanced image preprocessing.

## Conclusion

By following this **Aspose OCR Java tutorial**, you now know **how to use OCR** to extract text from images, limit the character set, and apply a temporary license for rapid testing. Dive deeper into the full [documentation](https://reference.aspose.com/ocr/java/) to explore multi‑language support, batch processing, and custom preprocessing pipelines.

---

**Last Updated:** 2026-05-24  
**Tested With:** Aspose.OCR for Java 24.11  
**Author:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Related Tutorials

- [How to Set License and Verify Aspose.OCR License in Java](/ocr/java/ocr-basics/set-license/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Aspose OCR Java Example – Recognizing Lines in Images](/ocr/java/advanced-ocr-techniques/recognize-lines/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}