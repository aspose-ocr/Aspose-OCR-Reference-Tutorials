---
category: general
date: 2026-02-19
description: Extract text from image using Java OCR. Learn a java ocr example that
  loads an image for OCR and extracts text from invoice files in just a few steps.
draft: false
keywords:
- extract text from image
- java ocr example
- load image for ocr
- extract text from invoice
language: en
og_description: Extract text from image using Java OCR. This guide shows how to load
  image for OCR and pull text from invoices with a simple java ocr example.
og_title: Extract Text from Image in Java – Complete OCR Example
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Extract Text from Image in Java – Complete OCR Example
url: /java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract Text from Image in Java – Complete OCR Example

Ever needed to **extract text from image** but weren’t sure which library to pick? You’re not alone—many developers hit this wall when automating invoice processing or building searchable archives. The good news? With a few lines of Java you can load an image for OCR, define a region of interest, and pull the exact text you need.  

In this tutorial we’ll walk through a **java ocr example** that shows exactly how to **load image for OCR**, set a ROI, and **extract text from invoice** files using Aspose.OCR. By the end you’ll have a runnable program you can drop into any Java project.

## What You’ll Learn

- How to create an `OcrEngine` instance and why it matters.
- The correct way to **load image for OCR** with Aspose’s `ImageStream`.
- Setting a **region of interest (ROI)** so you only process the part of the image that contains the invoice amount.
- Extracting the recognized text and printing it to the console.
- Common pitfalls (e.g., wrong rectangle coordinates) and quick fixes.

**Prerequisites**

- Java 8 or newer installed.
- Maven or Gradle to pull the Aspose.OCR library (`com.aspose:aspose-ocr`).
- A sample invoice image (`invoice.png`) placed in a known directory.

Got all that? Great—let’s dive in.

![Extract text from image using Java OCR](/images/extract-text-from-image-java.png "extract text from image example")

## Extract Text from Image – Step‑by‑Step Java OCR Example

Below is the full source code. Feel free to copy‑paste it into `RoiOcrExample.java` and run it directly.

```java
import com.aspose.ocr.*;

public class RoiOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance.
        // The engine holds all configuration and performs the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image.
        // You can point to any PNG, JPG, or TIFF file. Here we use a sample invoice.
        String imagePath = "YOUR_DIRECTORY/invoice.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 3: Define the region of interest (ROI) you want to recognize.
        // x = 120, y = 340, width = 500, height = 120 – tweak these values for your own layout.
        Rectangle regionOfInterest = new Rectangle(120, 340, 500, 120);
        ocrEngine.setRegionOfInterest(regionOfInterest);

        // Step 4: Perform OCR on the specified ROI and retrieve the text.
        // recognize() returns an OcrResult object; getText() extracts the plain string.
        String extractedText = ocrEngine.recognize().getText();

        // Step 5: Output the recognized text.
        System.out.println("ROI text: " + extractedText);
    }
}
```

### Why Each Step Is Important

1. **Creating the OCR engine** – without an engine there’s no context for image processing. The object also lets you tweak language packs later if you need multi‑language support.  
2. **Loading the image** – `ImageStream.fromFile` abstracts away the file format, ensuring the engine reads the bytes correctly. If you skip this, you’ll get a `NullPointerException`.  
3. **Setting the ROI** – processing the whole page can be wasteful. By narrowing the rectangle to the invoice total area, you speed up recognition and reduce noise.  
4. **Calling `recognize()`** – this is where the magic happens. The method runs the OCR algorithm over the ROI and produces a result object.  
5. **Printing the output** – in real projects you’d probably store the text in a database, but `System.out.println` is perfect for a quick demo.

## Load Image for OCR

If you’re wondering whether the path needs to be absolute or relative, the answer is both work—just make sure the Java process can read the file. On Windows, backslashes must be escaped (`C:\\images\\invoice.png`) or you can use forward slashes (`C:/images/invoice.png`).  

**Pro tip:** If you’re processing many invoices in a loop, reuse the same `OcrEngine` instance; it caches internal resources and improves throughput.

## Define Region of Interest (ROI)

Choosing the right rectangle can be a bit of trial and error. A handy way to find coordinates is to open the image in any graphics editor (like GIMP or Paint.NET) and hover over the area—you’ll see the X/Y values in the status bar.  

Edge case: some invoices have variable layouts. In that scenario you could run a quick pre‑scan on the whole image, locate keywords like “Total:” with a regex, then adjust the ROI dynamically.

## Perform OCR and Get Text

The `recognize()` call is synchronous—your thread blocks until the engine finishes. For large batches you might want to spin up a thread pool and process images in parallel. Just remember that each thread needs its own `OcrEngine` instance; they’re not thread‑safe.

## Run and Verify Output

Compile and run:

```bash
javac -cp "path/to/aspose-ocr.jar" RoiOcrExample.java
java -cp ".:path/to/aspose-ocr.jar" RoiOcrExample
```

You should see something like:

```
ROI text: $1,254.00
```

If the output looks garbled, double‑check the ROI coordinates and ensure the image quality is high (300 dpi or more works best).  

### Common Pitfalls & How to Fix Them

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Empty string | ROI outside image bounds | Verify rectangle values against image dimensions |
| Misspelled words | Low resolution | Use a higher‑resolution source or apply image preprocessing (e.g., binarization) |
| `java.lang.NoClassDefFoundError` | Missing Aspose JAR on classpath | Add `aspose-ocr.jar` to `-cp` or use Maven/Gradle dependency management |

## Conclusion

You now know how to **extract text from image** in Java using a concise **java ocr example**. By loading the image correctly, defining a focused ROI, and calling `recognize()`, you can reliably **extract text from invoice** files and feed that data into downstream systems.

What’s next? Try swapping the ROI for different fields (date, vendor name), experiment with language packs for multilingual invoices, or integrate the OCR step into a Spring Boot microservice. The same pattern works for receipts, passports, or any document where you need precise text extraction.

If you’ve got questions about scaling this solution or handling noisy scans, drop a comment below—happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}