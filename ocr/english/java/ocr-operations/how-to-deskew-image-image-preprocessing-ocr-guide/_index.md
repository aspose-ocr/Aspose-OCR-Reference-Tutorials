---
category: general
date: 2026-06-22
description: 'How to deskew image for OCR: learn image preprocessing OCR steps, remove
  salt pepper noise, and boost accuracy.'
draft: false
keywords:
- how to deskew image
- image preprocessing ocr
- remove salt pepper
- preprocess images OCR
language: en
og_description: How to deskew image for OCR, remove salt pepper noise, and apply preprocess
  images OCR techniques in a complete Java example.
og_title: How to Deskew Image – Image Preprocessing OCR Guide
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: 'How to deskew image for OCR: learn image preprocessing OCR steps,
    remove salt pepper noise, and boost accuracy.'
  headline: How to Deskew Image – Image Preprocessing OCR Guide
  type: TechArticle
tags:
- OCR
- image-processing
- Java
title: How to Deskew Image – Image Preprocessing OCR Guide
url: /java/ocr-operations/how-to-deskew-image-image-preprocessing-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Deskew Image – Image Preprocessing OCR Guide

Ever wondered **how to deskew image** so your OCR engine actually reads the text? You're not the only one. A tilted scan can turn a perfect document into a garbled mess, and most developers hit that snag at least once.

In this tutorial we’ll walk through a full **image preprocessing OCR** pipeline that not only corrects rotation but also **remove[s] salt pepper** artifacts and boosts contrast—basically everything you need to **preprocess images OCR**‑style before feeding them to the engine. By the end you’ll have a ready‑to‑run Java snippet and a clear mental model of why each step matters.

## How to Deskew Image – Building the Preprocessing Pipeline

The heart of any OCR‑friendly workflow is a **preprocess options** object that strings together a series of filters. Think of it as a conveyor belt: each filter does one job, then passes the image to the next. Below is a minimal but complete example using a hypothetical OCR library that ships with `DeskewFilter`, `DenoiseFilter`, and `ContrastBoostFilter`.

```java
import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.DeskewFilter;
import com.example.ocr.filters.DenoiseFilter;
import com.example.ocr.filters.ContrastBoostFilter;

/**
 * Demonstrates how to deskew image and apply common OCR preprocessing steps.
 */
public class OcrPreprocessDemo {

    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine (replace with your actual implementation)
        Engine engine = new Engine();

        // 2️⃣ Build the preprocessing pipeline
        ImagePreprocessOptions preprocessOptions = new ImagePreprocessOptions();

        // 2a️⃣ Deskew – correct rotation up to ±15°
        preprocessOptions.addFilter(new DeskewFilter(15));

        // 2b️⃣ Denoise – remove salt‑and‑pepper noise
        preprocessOptions.addFilter(new DenoiseFilter());

        // 2c️⃣ Contrast boost – make low‑contrast scans more readable
        preprocessOptions.addFilter(new ContrastBoostFilter(1.5f));

        // 3️⃣ Attach the pipeline to the engine
        engine.setPreprocessOptions(preprocessOptions);

        // 4️⃣ Run OCR on a sample image
        String result = engine.recognizeText("sample-scanned-page.png");

        // 5️⃣ Output the recognized text
        System.out.println("=== OCR RESULT ===");
        System.out.println(result);
    }
}
```

### Why this works

* **DeskewFilter** analyses the image’s dominant text lines, estimates the angle, and rotates the bitmap back to horizontal. Most libraries cap the correction at ±15° because larger angles usually indicate a badly scanned page that needs manual intervention.
* **DenoiseFilter** targets the classic *salt‑and‑pepper* pattern—those isolated black or white pixels that look like static on a TV. Removing them prevents the OCR engine from mistaking noise for characters.
* **ContrastBoostFilter** stretches the histogram, making faint strokes pop. A multiplier of `1.5f` is a safe default; you can bump it up if your scans are especially washed out.

> **Pro tip:** If you know your documents never exceed a 10° tilt, pass that smaller bound to `DeskewFilter`—the algorithm runs faster and is less likely to over‑correct.

## Image Preprocessing OCR: Adding Filters in the Right Order

Order matters. Imagine you denoise *before* deskewing; the noise could throw off the angle detection, leading to a mis‑aligned result. Conversely, applying contrast boost *after* deskew ensures the rotation doesn’t introduce new artifacts.

Below is a quick checklist you can copy‑paste into any project:

| Step | Filter | Reason |
|------|--------|--------|
| 1 | `DeskewFilter` | Aligns text baseline |
| 2 | `DenoiseFilter` | Removes isolated pixel noise |
| 3 | `ContrastBoostFilter` | Enhances legibility for OCR |

If you need to insert additional steps—say, a **binarization** filter for binary OCR—you would slot it **after** contrast boosting, because a clean, high‑contrast image binarizes more accurately.

## Remove Salt Pepper Noise with DenoiseFilter

Salt‑and‑pepper noise is notorious in low‑quality scans, especially those coming from cheap phone cameras. The `DenoiseFilter` in our library implements a median‑filter kernel, which replaces each pixel with the median of its surrounding neighborhood. The effect? Those specks disappear without blurring the actual characters.

```java
// Example: customizing the median kernel size (default is 3x3)
preprocessOptions.addFilter(new DenoiseFilter(5)); // 5x5 kernel for heavy noise
```

*When to increase the kernel size?* If your source images are riddled with large specks, a bigger kernel will clean them up, but beware: too large and you might start erasing fine strokes in tiny fonts.

## Preprocess Images OCR – Applying the Pipeline

Once you’ve assembled the filter chain, attaching it to the engine is a one‑liner (`engine.setPreprocessOptions`). From that moment on, every call to `recognizeText` automatically runs through the pipeline. No need to manually invoke each filter—your code stays tidy, and future changes (adding a new filter, tweaking parameters) are centralized.

Here’s what a successful run looks like with a sample scan that originally had a 12° tilt and noticeable pepper noise:

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Notice how the text is clean, correctly oriented, and free of stray characters that would have otherwise appeared as “I n v o i c e” or “$‑‑‑”.

## Edge Cases & Common Pitfalls

| Situation | What to watch for | Suggested fix |
|-----------|-------------------|---------------|
| Rotation > 15° | DeskewFilter may give up | Pre‑rotate manually or use a higher‑range filter |
| Extremely low resolution ( < 100 dpi ) | Contrast boost can’t recover details | Resample the image first (e.g., `ResampleFilter`) |
| Mixed noise (Gaussian + salt‑pepper) | DenoiseFilter alone isn’t enough | Chain a `GaussianBlurFilter` before `DenoiseFilter` |
| Color scans with colored text | Grayscale conversion needed | Insert `GrayscaleFilter` before contrast boost |

By anticipating these scenarios you save yourself hours of debugging later.

## Full Working Example (All‑in‑One)

Below is a self‑contained Java class you can drop into any Maven or Gradle project that includes the `com.example.ocr` dependency. It demonstrates **how to deskew image**, **remove salt pepper** noise, and **preprocess images OCR**‑style.

```java
package com.myapp.demo;

import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.*;

public class CompleteOcrPipeline {

    public static void main(String[] args) {
        // -------------------------------------------------
        // 1️⃣ Initialise OCR engine (replace with your own)
        // -------------------------------------------------
        Engine engine = new Engine();

        // -------------------------------------------------
        // 2️⃣ Configure preprocessing pipeline
        // -------------------------------------------------
        ImagePreprocessOptions options = new ImagePreprocessOptions();

        // Deskew up to ±15° – the core of "how to deskew image"
        options.addFilter(new DeskewFilter(15));

        // Remove salt‑and‑pepper artifacts
        options.addFilter(new DenoiseFilter());

        // Boost contrast by 1.5× to aid OCR recognition
        options.addFilter(new ContrastBoostFilter(1.5f));

        // (Optional) Convert to grayscale – often improves OCR accuracy
        options.addFilter(new GrayscaleFilter());

        // Attach the pipeline
        engine.setPreprocessOptions(options);

        // -------------------------------------------------
        // 3️⃣ Perform OCR on a test file
        // -------------------------------------------------
        String imagePath = "src/main/resources/scanned-document.png";
        String text = engine.recognizeText(imagePath);

        // -------------------------------------------------
        // 4️⃣ Show the result
        // -------------------------------------------------
        System.out.println("=== OCR RESULT ===");
        System.out.println(text);
    }
}
```

**Expected output** (assuming `scanned-document.png` contains a clear invoice):

```
=== OCR RESULT ===
Invoice #98765
Date: 2024‑02‑28
Amount Due: $2,340.75
Please remit payment within 30 days.
```

If you swap out the image for one that’s already perfectly aligned, you’ll notice the pipeline still runs—nothing breaks, and the OCR accuracy stays high.

## Conclusion

You now have a solid grasp of **how to deskew image** and why each preprocessing step—**image preprocessing OCR**, **remove salt pepper**, and **preprocess images OCR**—plays a crucial role in delivering clean, searchable text. The example above is a complete,


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Calculate Skew Angle for OCR Image Preprocessing](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}