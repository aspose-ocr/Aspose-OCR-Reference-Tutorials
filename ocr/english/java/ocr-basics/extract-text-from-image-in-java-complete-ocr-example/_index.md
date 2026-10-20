---
category: general
date: 2026-01-12
description: Extract text from image using Aspose OCR in Java. Learn how to extract
  text from an invoice image with a java ocr example and get the output OCR text.
draft: false
keywords:
- extract text from image
- how to extract text
- java ocr example
- process invoice image
- output ocr text
language: en
og_description: Extract text from image using Aspose OCR in Java. This guide shows
  how to extract text from an invoice image, includes a java ocr example, and outputs
  OCR text.
og_title: Extract Text from Image in Java – Complete OCR Example
tags:
- OCR
- Java
- Aspose
title: Extract Text from Image in Java – Complete OCR Example
url: /java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract Text from Image in Java – Complete OCR Example

Ever wondered how to **extract text from image** files without pulling your hair out? Maybe you have a stack of scanned invoices and you need the numbers fast. In my experience, the easiest way is to let a dedicated OCR library do the heavy lifting. This tutorial shows *how to extract text* from a typical invoice image using Aspose OCR for Java, and it even demonstrates a **java ocr example** that outputs the OCR text you can pipe into your downstream system.

We'll walk through everything you need to know: from setting up the project, defining the region of interest (ROI) that focuses on the header and total amount, to finally printing the extracted text. By the end, you’ll be able to **process invoice image** files automatically and retrieve clean, searchable text.

> **What you’ll get:** a ready‑to‑run Java program, clear explanations of each step, and practical tips for handling real‑world invoices.

---

## Prerequisites

Before we dive in, make sure you have the following:

- Java Development Kit (JDK) 8 or newer installed.
- Maven or Gradle for dependency management (Maven example shown).
- An Aspose OCR for Java license (the free trial works for testing).
- An invoice image (`invoice.png`) placed in a known directory.

If any of these sound unfamiliar, don’t worry—most of them are just a download away, and the code will still compile with the community edition.

---

## Step 1: Set Up Your Maven Project

First, create a new Maven project (or add to an existing one). In your `pom.xml`, add the Aspose OCR dependency:

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Use the latest version available -->
    </dependency>
</dependencies>
```

> **Pro tip:** Keep the version number up‑to‑date; newer releases often improve accuracy for tricky fonts found on invoices.

After saving the file, run `mvn clean install` to pull the library into your local repository.

---

## Step 2: Load the Invoice Image

Now that the library is ready, let’s write a small Java class. The first thing we do is create an `OcrEngine` instance and point it at the image you want to read.

```java
import com.aspose.ocr.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png"); // <-- replace with your path
```

Why do we create the engine **before** loading the image? The engine holds configuration such as language, DPI, and ROI. Setting the image early ensures those settings apply to the exact file you’re about to process.

---

## Step 3: Define Regions of Interest (ROI)

Invoices often contain a lot of noise—tables, logos, and fine print. By narrowing the OCR to just the header and the total amount, you dramatically boost both speed and accuracy. Aspose lets you describe these zones with rectangles.

```java
        // Step 3: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Apply ROI to the engine
        engine.setRegion(region);
```

The coordinates are in pixels (`x`, `y`, `width`, `height`). If your invoices vary in size, you can calculate these values dynamically—perhaps by checking image dimensions first. That’s a nice extension if you need a **process invoice image** solution that works on batches.

---

## Step 4: Run OCR on the Specified Regions

With the ROI in place, the OCR engine can focus its attention where it matters most. The `recognize()` method returns an `OcrResult` containing the extracted text.

```java
        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();
```

Behind the scenes, Aspose performs several preprocessing steps: binarization, noise removal, and character segmentation. You don’t have to call those manually—just let `recognize()` do its thing.

---

## Step 5: Output the Extracted Text

Finally, we print the text to the console. In a real application you might store it in a database, feed it into a downstream analytics pipeline, or even generate a searchable PDF.

```java
        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

When you run the program, you should see something like:

```
ROI text:
Acme Corp.
Invoice #12345
Date: 2025-12-31
Total Amount: $1,250.00
```

If the output looks garbled, double‑check the rectangle coordinates or increase the image resolution. OCR engines love crisp, high‑DPI scans.

---

## Full Working Example

Below is the complete, self‑contained Java file you can copy‑paste into `src/main/java/RoiExample.java`. No external snippets required—everything you need is right here.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.region.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png");

        // Step 2: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Step 3: Apply the ROI configuration to the engine
        engine.setRegion(region);

        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

> **Note:** Replace `YOUR_DIRECTORY` with the absolute path to your invoice image. If you’re using a relative path, make sure the working directory matches where you run the `java` command.

---

## Common Questions & Edge Cases

### What if the invoice size changes?

You can compute ROI dynamically:

```java
int imgWidth = engine.getImage().getWidth();
int imgHeight = engine.getImage().getHeight();

int headerHeight = imgHeight / 10;
int totalHeight = imgHeight / 8;

OcrRegion region = OcrRegion.builder()
        .addRectangle(0, 0, imgWidth, headerHeight)
        .addRectangle(0, imgHeight - totalHeight, imgWidth, totalHeight)
        .build();
```

### How do I handle multiple languages?

Aspose OCR supports language packs. Just set the language before calling `recognize()`:

```java
engine.setLanguage(OcrLanguage.Spanish); // or OcrLanguage.English, etc.
```

### What if the OCR returns empty strings?

Typical culprits are:

- Low image resolution (< 300 DPI). Upscale or request higher‑quality scans.
- Overly dark or light backgrounds. Apply a simple contrast‑enhancement filter before OCR.
- Incorrect ROI coordinates that miss the text entirely.

---

## Tips for Production‑Ready OCR

1. **Batch Processing:** Wrap the logic in a loop that iterates over a directory of invoice files. Log each result for auditability.
2. **Error Handling:** Catch `OcrException` to gracefully skip corrupted images without halting the whole job.
3. **Performance:** Reuse a single `OcrEngine` instance across multiple images; creating a new engine per file adds unnecessary overhead.
4. **Validation:** After extraction, run a regex check on the total amount (`\$\d{1,3}(,\d{3})*(\.\d{2})?`) to ensure the number looks realistic.

Implementing these suggestions turns a simple **java ocr example** into a robust, scalable solution for any business that needs to **process invoice image** files nightly.

---

## Conclusion

We’ve just covered how to **extract text from image** files in Java using Aspose OCR, focusing on a practical invoice‑processing scenario. By defining a region of interest, running the OCR engine, and printing the **output OCR text**, you now have a solid foundation for building automated data‑capture pipelines.

Next steps? Try expanding the ROI to include line‑item tables, experiment with different language settings, or feed the extracted strings into a PDF‑generation library for searchable documents. The sky’s the limit when you combine OCR with modern Java tooling.

Got more questions about **how to extract text** from other document types, or need help tweaking the ROI for unusual layouts? Drop a comment below—happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}