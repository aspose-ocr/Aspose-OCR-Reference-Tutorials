---
title: Convert Image to Coordinates: Extract Paragraph Rectangles
linktitle: Get Rectangles for Paragraphs in OCR Image Recognition
second_title: Aspose.OCR .NET API
description: Learn how to convert image to coordinates and extract paragraph rectangles using Aspose.OCR for .NET – the go‑to guide for OCR paragraph detection and rectangle extraction.
weight: 11
url: /net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
date: 2026-02-22
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert Image to Coordinates: Extract Paragraph Rectangles

## Introduction

Welcome to our comprehensive guide on **how to convert image to coordinates** and extract rectangles for paragraphs in OCR image recognition with Aspose.OCR for .NET. If you're looking to enhance your document‑processing pipeline, pull out paragraph boundaries, and automate data extraction, you're in the right place. We'll walk through every step—from setting up the environment to printing the rectangle coordinates—so you can start using OCR results immediately.

## Quick Answers
- **What does “extract rectangles” mean?** It returns the bounding boxes (x, y, width, height) of detected text areas.  
- **Which API method provides the rectangles?** `AsposeOcr.GetRectangles` with `AreasType.PARAGRAPHS`.  
- **Do I need a license for development?** A free trial works for testing; a commercial license is required for production.  
- **Can I process multiple images at once?** Yes—loop over your image list and call `GetRectangles` for each file.  
- **What formats are supported?** PNG, JPEG, TIFF, BMP, and many more.

## What is “convert image to coordinates” in OCR?
In OCR terminology, converting an image to coordinates means identifying the geometric boundaries that enclose each paragraph or line of text within an image. These coordinates let you highlight, crop, or further analyze specific sections of a scanned document.

## Why extract paragraph coordinates?
- **Precise post‑processing** – you can feed each rectangle into downstream workflows (e.g., translation, redaction).  
- **Improved UI/UX** – overlay bounding boxes on the original image to show users where text was found.  
- **Batch automation** – quickly locate and isolate paragraphs across large document sets.  

## Prerequisites

- Basic knowledge of C# and .NET development.  
- A development environment with Aspose.OCR for .NET installed – you can download it [here](https://releases.aspose.com/ocr/net/).  
- Familiarity with image processing concepts and why OCR is essential for extracting text from scanned files.

## Import Namespaces

In your C# file, import the required namespaces so the OCR classes are available:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Step 1: Set Up Your Document Directory

Define the folder that contains the images you want to analyze:

```csharp
string dataDir = "Your Document Directory";
```

## Step 2: Initialize AsposeOcr Instance

Create an `AsposeOcr` object – this gives you access to all OCR functions:

```csharp
AsposeOcr api = new AsposeOcr();
```

## Step 3: Specify the Image Path

Point to the exact image file you wish to process:

```csharp
string fullPath = dataDir + "sample.png";
```

## Step 4: Recognize Image and Get Paragraph Rectangles

Call the `GetRectangles` method. Setting `detect_areas` to `true` tells the engine to return **paragraph** rectangles:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## Step 5: Print Results

Output the coordinates so you can see the **extract paragraph coordinates** that were detected:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## How to Extract Rectangles from Images Using Aspose.OCR

Now that you’ve seen the code, let’s break down why each step matters:

1. **Directory setup** ensures your application can locate the source files without hard‑coding absolute paths.  
2. **`AsposeOcr` initialization** loads the OCR engine with default settings; you can later tweak `api.Config` for DPI, language, or preprocessing.  
3. **`GetRectangles`** with `AreasType.PARAGRAPHS` is the core call that performs **ocr paragraph detection** and returns a list of `Rectangle` objects.  
4. **Printing the results** gives you a quick way to verify that the coordinates match the visual layout of the source image.

## Common Issues and Solutions

| Issue | Reason | Fix |
|-------|--------|-----|
| No rectangles returned | Image quality too low or wrong `AreasType` | Ensure the image is clear and use `AreasType.PARAGRAPHS`. |
| Coordinates are off‑by‑one | DPI scaling mismatch | Set the correct DPI when loading the image or use `api.Config.Dpi`. |
| License exception | Running without a valid license in production | Apply a temporary or permanent license via `api.SetLicense`. |

## Frequently Asked Questions

**Q: Is Aspose.OCR compatible with different image formats?**  
A: Yes, Aspose.OCR supports PNG, JPEG, TIFF, BMP, and many other common formats.

**Q: Can I use Aspose.OCR for batch processing of multiple images?**  
A: Absolutely! Loop through a collection of file paths and call `GetRectangles` for each image.

**Q: Is there a free trial available for Aspose.OCR for .NET?**  
A: Yes, you can explore a free trial [here](https://releases.aspose.com/).

**Q: How can I obtain a temporary license for Aspose.OCR?**  
A: You can acquire a temporary license [here](https://purchase.aspose.com/temporary-license/).

**Q: Where can I find additional support and discussions related to Aspose.OCR?**  
A: Head over to the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) for community support and discussions.

## Conclusion

In this tutorial we’ve shown **how to convert image to coordinates** and extract paragraph rectangles using Aspose.OCR for .NET, walked through each code snippet, and explained how to interpret the returned coordinates. By integrating these steps into your application, you can reliably pull out paragraph boundaries, enhance document workflows, and build smarter OCR‑driven solutions.

---

**Last Updated:** 2026-02-22  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}