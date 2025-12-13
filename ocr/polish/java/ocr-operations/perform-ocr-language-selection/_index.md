---
date: 2025-12-13
description: „Dowiedz się, jak wyodrębnić tekst z obrazu przy użyciu Aspose.OCR dla
  Javy z wyborem języka. Ten krok‑po‑kroku samouczek Aspose OCR Java pokazuje precyzyjną
  konfigurację OCR.”
linktitle: How to Extract Text from Image with Language Selection Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Jak wyodrębnić tekst z obrazu z wyborem języka przy użyciu Aspose.OCR
url: /pl/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyodrębnić tekst z obrazu z wyborem języka przy użyciu Aspose.OCR

## Introduction

Wyodrębnianie tekstu z plików graficznych to powszechne wymaganie, niezależnie od tego, czy digitalizujesz zeskanowane dokumenty, przetwarzasz paragony, czy budujesz archiwa przeszukiwalne. Aspose.OCR dla Javy upraszcza to zadanie i daje precyzyjną kontrolę nad wyborem języka, korekcją pochylenia i obszarami rozpoznawania. W tym samouczku przeprowadzimy kompletny, praktyczny przykład, który pokazuje **jak wyodrębnić tekst z obrazu** przy określonym ustawieniu języka, abyś mógł już dziś zintegrować niezawodny OCR w swoich aplikacjach Java.

## Quick Answers
- **What library handles OCR in Java?** Aspose.OCR for Java  
- **Which setting selects the language?** `settings.setLanguage(Language.Eng)` (or any supported language)  
- **Do I need a license for development?** A free evaluation license works for testing; a commercial license is required for production.  
- **Can I limit OCR to a region of the image?** Yes, use `RecognitionSettings.setRecognitionAreas()` with rectangles.  
- **What is the typical runtime?** A few seconds per page on a standard laptop, depending on image size and language complexity.

## What is “extract text from image”?

Wyodrębnianie tekstu z obrazu (OCR) konwertuje wizualną reprezentację znaków na ciągi znaków odczytywalne przez maszynę. Umożliwia to wyszukiwanie, analizy i przepływy pracy związane z ekstrakcją danych, które w przeciwnym razie wymagałyby ręcznej transkrypcji.

## Why use Aspose.OCR with language selection?
- **Multilingual support** – Choose the exact language(s) present in your image to boost accuracy.  
- **Fine‑tuned control** – Adjust skew, define recognition areas, and set auto‑skew behavior.  
- **Pure Java API** – No native dependencies, easy to integrate into any Java project.  
- **Rich result data** – Get plain text, JSON, bounding rectangles, and warnings in one call.

## Prerequisites

Before you start, make sure you have:

- **Java Development Kit (JDK)** installed (JDK 8 or later).  
- **Aspose.OCR for Java** library – download it from the official site [here](https://reference.aspose.com/ocr/java/).  
- An image file that contains the text you want to extract, e.g., `p3.png`.

## Import Packages

In your Java source file, include the required Aspose.OCR classes and standard Java utilities:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Step‑by‑Step Guide

### Step 1: Set up Your Document Directory

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Replace `"Your Document Directory"` with the absolute path where `p3.png` resides.

### Step 2: Define the Image Path

```java
// The image path
String file = dataDir + "p3.png";
```

Make sure the `file` variable points to the exact image you intend to process.

### Step 3: Create Aspose.OCR API Instance

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

The `AsposeOCR` object gives you access to all OCR operations.

### Step 4: Set Recognition Options (Language Selection)

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Here we:

1. Disable auto‑skew because we provide a manual skew value.  
2. Define a rectangular region (`RecognitionAreas`) to limit OCR to the part of the image that actually contains text.  
3. Set the **language** to English (`Language.Eng`). Change this to `Language.Fra`, `Language.Spa`, etc., depending on your source image.

### Step 5: Perform OCR and Retrieve Results

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

The `RecognizePage` call runs the OCR engine using the image and the settings you defined. The outcome is stored in a `RecognitionResult` object.

### Step 6: Print and Utilize Results

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

The console output shows:

- The full extracted text (`recognitionText`).  
- Text for each defined rectangle (`recognitionAreasText`).  
- Bounding rectangle coordinates.  
- A JSON representation for easy downstream processing.  
- Detected skew angle and any warnings.

You can now feed `result.recognitionText` into your business logic—store it, index it, or pass it to another service.

## Common Issues and Solutions

| Issue | Cause | Fix |
|-------|-------|-----|
| **Garbage characters** | Wrong language selected | Set the correct `Language` enum (e.g., `Language.Fra` for French). |
| **No text returned** | Recognition area does not cover the text | Adjust the `Rectangle` coordinates or remove `RecognitionAreas` to process the whole image. |
| **Slow performance** | Very large image or high resolution | Downscale the image before OCR or increase memory allocation for the JVM. |
| **Warnings about unsupported format** | Image format not recognized | Convert the image to PNG, JPEG, or TIFF before processing. |

## Frequently Asked Questions

**Q: Can I recognize multiple languages in a single OCR call?**  
A: Yes. Use `settings.setLanguage(Language.Eng | Language.Fra)` to enable multilingual recognition.

**Q: Which image formats does Aspose.OCR support?**  
A: PNG, JPEG, BMP, TIFF, GIF, and several others. Just provide the correct file path.

**Q: Is there a size limit for the image?**  
A: There’s no hard limit, but very large images increase memory usage and processing time. Consider resizing large files.

**Q: How do I obtain a production license?**  
A: Purchase a license from the Aspose website and apply it via `License` class as shown in the Aspose documentation.

**Q: Can I extract text from a PDF page directly?**  
A: Not directly with Aspose.OCR. Convert the PDF page to an image first (e.g., using Aspose.PDF) and then run OCR.

## Conclusion

You’ve now seen how to **extract text from image** using Aspose.OCR for Java while selecting the appropriate language and limiting the recognition to specific regions. This approach delivers accurate, high‑performance OCR that can be embedded into any Java‑based workflow—from document management systems to data‑capture pipelines.

---

**Last Updated:** 2025-12-13  
**Tested With:** Aspose.OCR 24.11 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}