---
category: general
date: 2026-07-05
description: Compress PDF images while converting PNG to PDF using Java. Learn image
  preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
draft: false
keywords:
- compress pdf images
- convert png to pdf
- image preprocessing for ocr
- recognize text jpg
- batch ocr to pdf
language: en
og_description: Compress PDF images and convert PNG to PDF using Java. This guide
  covers image preprocessing for OCR, recognize text JPG, and batch OCR to PDF.
og_title: Compress PDF Images with Java – Complete Batch OCR Tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  headline: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  type: TechArticle
- description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  name: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints a line for each image, e.g.:'
  - name: What if my server has no GPU?
    text: Just set `gpuSettings.setEnabled(false)`. The rest of the pipeline remains
      unchanged, and you still get multithreaded CPU processing.
  - name: My PDFs are still too large—can I lower the quality further?
    text: Yes. Adjust `options.setImageQuality(70)` or even `50`. Lower values shrink
      size more aggressively but may blur fine glyphs. Test with a representative
      sample.
  - name: How do I handle other image formats (TIFF, BMP)?
    text: 'Add the extensions to the filter lambda:'
  - name: Can I keep the original color images instead of binarizing?
    text: Replace `.addBinarize()` with `.addGrayscale()` in the preprocessor builder
      if you need color retention for downstream analysis.
  type: HowTo
tags:
- ocr
- java
- pdf
- image-processing
title: Compress PDF Images with Java – Full Batch OCR to PDF Guide
url: /java/advanced-ocr-techniques/compress-pdf-images-with-java-full-batch-ocr-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Compress PDF Images with Java – Full Batch OCR to PDF Guide

Ever needed to **compress PDF images** while turning a folder of PNGs into searchable PDFs? You’re not the only one. In many automation pipelines the biggest pain point is juggling image quality, OCR accuracy, and final PDF size—all at once.  

In this tutorial we’ll walk through a practical solution that **converts PNG to PDF**, applies **image preprocessing for OCR**, and finally **compresses PDF images** so the output stays lightweight. By the end you’ll know how to **recognize text JPG** files, set up a **batch OCR to PDF** workflow, and keep your PDFs tidy.

## What You’ll Learn

- Setting up Aspose OCR for Java and applying a license.
- Configuring the engine for multithreading, GPU acceleration, and spell correction.
- Building a reusable **image preprocessing for OCR** pipeline (denoise, contrast, binarize).
- Using **PdfSaveOptions** to **compress PDF images** without sacrificing readability.
- Looping through a directory to **convert PNG to PDF** and **recognize text JPG** in bulk.
- A complete, ready‑to‑run Java program you can drop into any project.

> **Prerequisites**: Java 8+, Maven or Gradle, an Aspose OCR for Java license, and a folder of PNG/JPG images you want to process.

---

## Step 1: Apply the Aspose OCR License (Essential for Production)

Before you can call any OCR APIs you must load a valid license; otherwise you’ll be stuck with trial limitations.

```java
import com.aspose.ocr.*;

public class LicenseSetup {
    public static void loadLicense() throws Exception {
        License license = new License();
        // Point to your license file – keep it out of source control!
        license.setLicense("Aspose.OCR.Java.lic");
    }
}
```

*Why this matters*: A licensed engine unlocks GPU support, higher accuracy, and removes watermarks that would otherwise bloat your PDF files.

---

## Step 2: Configure the OCR Engine – Threads, GPU, and Spell Correction

A fast OCR engine is the backbone of any **batch OCR to PDF** job. We’ll spin up as many threads as the host CPU can handle, enable GPU acceleration (if you have a compatible card), and tighten spell correction to clean up OCR errors.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.GPUSettings;
import com.aspose.ocr.spell.SpellCorrectionOptions;

public class EngineConfig {
    public static OcrEngine createEngine() {
        OcrEngine ocrEngine = new OcrEngine();

        // Use all available logical processors
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Enable GPU – huge speedup for large batches
        GPUSettings gpu = new GPUSettings();
        gpu.setEnabled(true);
        ocrEngine.setGpuSettings(gpu);

        // Light spell correction: fix common typos without over‑correcting
        SpellCorrectionOptions spellOpts = new SpellCorrectionOptions();
        spellOpts.setMaxEditDistance(1);
        ocrEngine.getSpellCorrection().setOptions(spellOpts);

        return ocrEngine;
    }
}
```

*Pro tip*: If you’re running on a headless server without a GPU, just set `gpu.setEnabled(false)` – the code will still work, just a bit slower.

---

## Step 3: Build an Image Preprocessing Pipeline

Raw scans often suffer from noise, low contrast, or uneven lighting. **Image preprocessing for OCR** dramatically improves recognition rates, especially for **recognize text JPG** scenarios.

```java
import com.aspose.ocr.*;

public class PreprocessorSetup {
    public static ImagePreprocessor createPreprocessor() {
        return new ImagePreprocessor.Builder()
                .addDenoise(0.7)      // Reduce grain while preserving edges
                .addContrast(1.15)    // Boost contrast for clearer glyphs
                .addBinarize()        // Convert to black‑and‑white for OCR
                .build();
    }
}
```

*Why we chain these*: Denoising first prevents the binarizer from amplifying speckles; contrast then ensures characters stand out; finally, binarization gives the OCR engine a clean binary image to work with.

---

## Step 4: Prepare PDF Save Options – **Compress PDF Images** Efficiently

Aspose lets you fine‑tune the PDF output. We’ll turn on image compression and set a quality level that balances size and legibility.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOptions {
    public static PdfSaveOptions createOptions() {
        PdfSaveOptions options = new PdfSaveOptions();
        options.setCompressImages(true);   // This is the key to compress PDF images
        options.setImageQuality(90);       // 90% retains sharp text while shrinking file size
        return options;
    }
}
```

*Result*: Each searchable PDF will be noticeably smaller—ideal for archiving or sending via email.

---

## Step 5: Process the Folder – **Convert PNG to PDF** and **Recognize Text JPG** in One Loop

Now we bring everything together. The loop walks through an input directory, runs OCR on each PNG or JPG, and writes a searchable PDF to an output folder. The PDF name mirrors the source image name.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.PdfSaveOptions;
import java.io.File;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license
        LicenseSetup.loadLicense();

        // 2️⃣ Engine & preprocessing
        OcrEngine ocrEngine = EngineConfig.createEngine();
        ocrEngine.setPreprocessor(PreprocessorSetup.createPreprocessor());

        // 3️⃣ PDF options (compress PDF images)
        PdfSaveOptions pdfOptions = PdfOptions.createOptions();

        // 4️⃣ Define input / output folders
        File inputFolder = new File("YOUR_DIRECTORY/input");
        File outputFolder = new File("YOUR_DIRECTORY/output");
        if (!outputFolder.exists()) outputFolder.mkdirs();

        // 5️⃣ Filter PNG & JPG files
        File[] imageFiles = inputFolder.listFiles((dir, name) ->
                name.toLowerCase().endsWith(".png") || name.toLowerCase().endsWith(".jpg"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG or JPG files found in the input folder.");
            return;
        }

        // 6️⃣ Process each file
        for (File image : imageFiles) {
            // Recognize text – works for both PNG and JPG
            ocrEngine.recognizeImage(image.getAbsolutePath());

            // Build output PDF path (same base name)
            String pdfPath = outputFolder.getAbsolutePath() + File.separator +
                    image.getName().replaceAll("\\.(png|jpg)$", ".pdf");

            // Save as searchable PDF – this step also compresses images
            ocrEngine.saveAsSearchablePdf(pdfPath, pdfOptions);

            System.out.println("✅ Processed: " + image.getName() + " → " + pdfPath);
        }

        System.out.println("🎉 All files have been converted and compressed!");
    }
}
```

### Expected Output

Running the program prints a line for each image, e.g.:

```
✅ Processed: invoice1.png → /output/invoice1.pdf
✅ Processed: receipt23.jpg → /output/receipt23.pdf
🎉 All files have been converted and compressed!
```

Open any resulting PDF in a viewer and you’ll see selectable, searchable text while the file size is typically **30‑50 % smaller** than a non‑compressed counterpart.

---

## Common Questions & Edge Cases

### What if my server has no GPU?
Just set `gpuSettings.setEnabled(false)`. The rest of the pipeline remains unchanged, and you still get multithreaded CPU processing.

### My PDFs are still too large—can I lower the quality further?
Yes. Adjust `options.setImageQuality(70)` or even `50`. Lower values shrink size more aggressively but may blur fine glyphs. Test with a representative sample.

### How do I handle other image formats (TIFF, BMP)?
Add the extensions to the filter lambda:

```java
name.toLowerCase().endsWith(".png") ||
name.toLowerCase().endsWith(".jpg") ||
name.toLowerCase().endsWith(".tif") ||
name.toLowerCase().endsWith(".bmp")
```

The same preprocessing pipeline works for most raster formats.

### Can I keep the original color images instead of binarizing?
Replace `.addBinarize()` with `.addGrayscale()` in the preprocessor builder if you need color retention for downstream analysis.

---

## Pro Tips for Production‑Ready Batch OCR

- **Memory management**: Reuse a single `OcrEngine` instance (as shown) to avoid the overhead of creating/destroying objects per image.
- **Error handling**: Wrap the per‑file block in a `try/catch` to log failures without aborting the whole batch.
- **Logging**: Use a proper logging framework (SLF4J, Log4j) instead of `System.out.println` for scalable solutions.
- **Parallelism**: For massive folders, consider processing sub‑directories in parallel streams, but keep an eye on GPU contention.
- **Security**: Store the license file outside the repository and protect it with file system permissions.

---

## Conclusion

We’ve just demonstrated how to **compress PDF images** while performing a **batch OCR to PDF** conversion that **convert PNG to PDF**, **recognize text JPG**, and applies a robust **image preprocessing for OCR** pipeline. The full Java program is self‑contained, runs on any modern JDK, and produces lightweight searchable PDFs ready for archiving or downstream analysis.

Next steps? Experiment with different pre‑processing parameters, try out OCR languages other than English, or integrate the workflow into a Spring Boot microservice that watches a directory and processes files on the fly. The core concepts—license loading, engine configuration, preprocessing, and PDF compression—stay the same, giving you a solid foundation for any OCR‑driven project.

Got questions or want to share your own tweaks? Drop a comment below, and happy coding!

![Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output](alt="Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output")


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}