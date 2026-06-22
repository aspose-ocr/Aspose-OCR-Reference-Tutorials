---
category: general
date: 2026-06-22
description: Create searchable PDF using OCR in Java. Learn how to disable compression
  and convert scanned image PDF to a searchable PDF quickly.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- ocr to searchable pdf
- how to disable compression
- pdf without compression
language: en
og_description: Create searchable PDF using OCR in Java. This guide shows how to disable
  compression, convert scanned image PDF, and generate a PDF without compression.
og_title: Create Searchable PDF with OCR – Complete Java Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  headline: Create Searchable PDF with OCR – Full Guide
  type: TechArticle
- description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  name: Create Searchable PDF with OCR – Full Guide
  steps:
  - name: Set the output format to `PDF_SEARCHABLE`.
    text: Set the output format to `PDF_SEARCHABLE`.
  - name: Turn off PDF compression with `PdfCompression.NONE`.
    text: Turn off PDF compression with `PdfCompression.NONE`.
  - name: Run OCR and capture the `PdfDocument`.
    text: Run OCR and capture the `PdfDocument`.
  - name: Save the file to disk.
    text: Save the file to disk.
  type: HowTo
tags:
- OCR
- PDF
- Java
- Document Processing
title: Create Searchable PDF with OCR – Full Guide
url: /java/ocr-operations/create-searchable-pdf-with-ocr-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Searchable PDF with OCR – Full Guide

Ever needed to **create searchable PDF** from a batch of scanned images but weren’t sure which settings to flip? You’re not the only one—most developers hit the same wall when the output ends up a huge, unreadable blob.  

In this tutorial we’ll walk through a clean, end‑to‑end example that shows you exactly how to **create searchable PDF** using a Java OCR engine, **convert scanned image PDF**, and, crucially, **how to disable compression** so the resulting file stays true to the original dimensions. By the end you’ll have a ready‑to‑run snippet and a solid understanding of why each configuration matters.

## What You’ll Learn

* How to configure the OCR engine to **ocr to searchable pdf**.  
* The reason behind turning off PDF compression and how to get a **pdf without compression**.  
* A complete Java program that takes a scanned image, runs OCR, and saves a **searchable PDF**.  
* Tips for handling edge cases like multi‑page scans or low‑resolution sources.  

**Prerequisites** – Java 8+ installed, a compatible OCR SDK (the code uses the ABBYY FineReader Engine API, but the concepts apply to any library offering `setOutputFormat` and `setPdfCompression`). An IDE such as IntelliJ IDEA or Eclipse will make life easier, but a simple text editor works too.

---

![Create searchable PDF workflow](image-placeholder.png "Diagram showing the create searchable pdf process from scanned images to final PDF")

## Step 1: Set the OCR Engine to **Create Searchable PDF**

The first thing you need to tell the OCR engine is what kind of output you expect. By default many SDKs spit out plain text or a raster PDF, which isn’t searchable. Switching the format does the heavy lifting for you.

```java
// Step 1: Tell the engine we want a searchable PDF
engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);
```

*Why this matters*: The `PDF_SEARCHABLE` flag instructs the engine to embed an invisible text layer beneath the scanned image. Search tools can then index the document, making it behave like any native PDF you’d open in Adobe Reader.

## Step 2: Disable Compression – **How to Disable Compression** Properly

If you skip this step the engine will compress each page to save space, but the compression can blur fine details—especially problematic when you later need to extract high‑resolution images.

```java
// Step 2: Turn off PDF compression to keep original image quality
engine.getConfig().setPdfCompression(PdfCompression.NONE);
```

**Pro tip**: Disabling compression is essential when you plan to archive legal documents or medical scans where every pixel counts. The resulting file may be larger, but you preserve the original dimensions and clarity.

## Step 3: Perform OCR and Get the Resulting Document

Now that the engine knows what to output and how to treat the images, you can run the recognition. The call returns a `PdfDocument` object that’s ready to be saved or further manipulated.

```java
// Step 3: Run OCR and capture the searchable PDF in memory
PdfDocument pdf = engine.recognizeToPdf();
```

*What’s happening under the hood?* The engine processes each input page, runs character recognition, and stitches the hidden text layer onto the image. If you have multiple pages, they’re concatenated automatically.

## Step 4: Save the **Searchable PDF** to Disk

Finally, write the in‑memory PDF to a file. Pick a location you have write permissions for, and give the file a meaningful name.

```java
// Step 4: Persist the searchable PDF on disk
pdf.save("YOUR_DIRECTORY/searchable.pdf");
```

When you open `searchable.pdf` in a viewer, you’ll notice you can select and search the text—even though the visible content is still the original scanned image.

### Full Working Example

Below is a self‑contained Java class that puts all four steps together. Feel free to copy‑paste, adjust the input path, and run it as‑is.

```java
import com.abbyy.ocrsdk.Engine;
import com.abbyy.ocrsdk.OcrOutputFormat;
import com.abbyy.ocrsdk.PdfCompression;
import com.abbyy.ocrsdk.PdfDocument;

/**
 * Demonstrates how to create searchable PDF from scanned images.
 * This example uses the ABBYY FineReader Engine Java API.
 */
public class SearchablePdfCreator {

    public static void main(String[] args) {
        // ---- 1. Initialize the OCR engine -------------------------------------------------
        Engine engine = new Engine();
        // (Assume license activation and engine initialization are handled elsewhere)

        // ---- 2. Configure output to be a searchable PDF ----------------------------------
        engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);

        // ---- 3. Disable compression for a PDF without compression -------------------------
        engine.getConfig().setPdfCompression(PdfCompression.NONE);

        // ---- 4. Load the scanned image(s) --------------------------------------------------
        // For simplicity, we let the engine auto‑detect images in the working folder.
        // You could also call engine.addImage("path/to/image.tif") for explicit control.
        engine.addImage("YOUR_DIRECTORY/scanned-page.tif");

        // ---- 5. Perform OCR and retrieve the PDF -----------------------------------------
        PdfDocument pdf = engine.recognizeToPdf();

        // ---- 6. Save the result -----------------------------------------------------------
        pdf.save("YOUR_DIRECTORY/searchable.pdf");

        System.out.println("✅ Searchable PDF created successfully at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

**Expected output** – After running the program you’ll see the console message above, and the file `searchable.pdf` will appear in `YOUR_DIRECTORY`. Opening it in any PDF reader should let you:

* Highlight text.
* Use the built‑in search (Ctrl + F) to locate words.
* Export the hidden text layer if needed.

---

## Why Disable Compression? Understanding **PDF Without Compression**

You might wonder, “Isn’t compression always a good idea?” The answer is nuanced:

| Situation | Keep Compression (`NORMAL`) | Disable Compression (`NONE`) |
|-----------|-----------------------------|------------------------------|
| Archival of legal contracts | ❌ May alter pixel fidelity | ✅ Guarantees original look |
| Large batch of low‑resolution scans | ✅ Saves storage | ❌ Increases size without benefit |
| Need for OCR accuracy on tiny fonts | ❌ Blurs fine details | ✅ Preserves every stroke |

In short, **how to disable compression** is a trade‑off between storage and fidelity. For most searchable PDF workflows where you intend to search the text rather than re‑print the images, turning compression off is the safest bet.

## Converting a **Scanned Image PDF** Directly

Sometimes you already have a PDF that contains scanned images (a “image‑only PDF”). To **convert scanned image pdf** into a searchable version, you can feed the whole PDF to the engine instead of individual images:

```java
engine.addPdf("YOUR_DIRECTORY/scanned-image-only.pdf");
PdfDocument searchable = engine.recognizeToPdf();
searchable.save("YOUR_DIRECTORY/searchable-from-pdf.pdf");
```

The same configuration flags (`PDF_SEARCHABLE` and `PdfCompression.NONE`) apply, so you get a **pdf without compression** even when starting from a PDF container.

## Common Pitfalls & How to Avoid Them

* **Forgot to set the output format** – The engine defaults to raster PDF, which isn’t searchable. Always call `setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE)` before `recognizeToPdf()`.
* **Running out of memory on large batches** – Load and process pages in chunks, or use the streaming API if your SDK provides one.
* **Incorrect file paths** – Use absolute paths or ensure your working directory is set correctly; otherwise `pdf.save()` throws an `IOException`.
* **License not activated** – Most commercial OCR SDKs require a valid license; the engine will throw a runtime exception if it’s missing.

---

## Conclusion

You now have a complete, ready‑to‑run solution that shows **how to create searchable PDF** files from scanned images, how to **convert scanned image PDF**, and exactly **how to disable compression** to produce a **pdf without compression**. The key steps are:

1. Set the output format to `PDF_SEARCHABLE`.  
2. Turn off PDF compression with `PdfCompression.NONE`.  
3. Run OCR and capture the `PdfDocument`.  
4. Save the file to disk.

From here you can experiment with fonts, add watermarks, or batch‑process entire folders. If you’re curious about adding OCR language packs, handling multi‑page TIFFs, or integrating this workflow into a web service, check out our upcoming tutorials on “OCR language selection in Java” and “Streaming OCR for large document sets”.

Got questions, or spotted a snag? Drop a comment below—happy coding, and enjoy your newly searchable PDFs!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}