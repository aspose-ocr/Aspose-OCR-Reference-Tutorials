---
title: Get OCR Line Rectangles for Image Text Lines
linktitle: Get OCR Line Rectangles for Image Text Lines
second_title: Aspose.OCR .NET API
description: Learn how to get OCR line rectangles using Aspose.OCR for .NET to recognize text lines in images and extract line coordinates easily.
weight: 10
url: /net/image-and-drawing-recognition/get-rectangles-for-lines/
date: 2025-12-17
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Get OCR Line Rectangles for Image Text Lines

## Introduction

In this tutorial you'll discover **how to get OCR line rectangles** with Aspose.OCR for .NET. By the end of the guide you’ll be able to **recognize text lines in an image** and **extract line coordinates** for each detected line—perfect for downstream processing such as layout analysis, data extraction, or custom rendering.

## Quick Answers
- **What does “get OCR line rectangles” mean?** It returns the bounding boxes of each text line detected in an image.  
- **Which API method is used?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Do I need a license?** A free trial works for development; a commercial license is required for production.  
- **Supported image formats?** PNG, JPEG, BMP, TIFF, and more.  
- **Can I run this on .NET Core?** Yes, Aspose.OCR fully supports .NET Core and .NET 5/6.

## Prerequisites

Before diving into the tutorial, make sure you have the following prerequisites in place:

- Basic knowledge of C# and .NET development.  
- An integrated development environment (IDE) such as Visual Studio.  
- Aspose.OCR for .NET library installed. You can download it [here](https://releases.aspose.com/ocr/net/).  
- A sample image containing text for OCR recognition.

## Import Namespaces

Ensure you have the necessary namespaces imported to your project. Add the following lines to the top of your C# file:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Now, let's break down the process of getting rectangles for lines in OCR image recognition into easy‑to‑follow steps.

## Step 1: Set Up Your Document Directory

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Replace `"Your Document Directory"` with the actual path to the folder that holds your sample image.

## Step 2: Initialize Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Create an instance of the `AsposeOcr` class to access the OCR functionality.

## Step 3: Specify Image Path

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Define the full path to the image you want to perform OCR on.

## Step 4: Recognize Image and Get Rectangles

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

The `GetRectangles` method returns a list of `Rectangle` objects, each representing the coordinates of a detected text line. This is the core of **getting OCR line rectangles**.

## Step 5: Print Result

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Print the coordinates of the detected areas to the console. You’ll see values that you can later use to **extract line coordinates** for custom processing.

## Why Use Aspose.OCR for Line Rectangles?

- **High accuracy** – Advanced algorithms detect lines even in noisy or skewed images.  
- **Cross‑platform** – Works on .NET Framework, .NET Core, and .NET 5/6.  
- **No external dependencies** – Pure .NET library, no native DLLs to ship.  
- **Rich output** – Apart from line rectangles you can also retrieve words, characters, and confidence scores.

## Common Issues and Solutions

| Issue | Solution |
|-------|----------|
| **No rectangles returned** | Ensure the image contains clear, horizontal text and that `AreasType.LINES` is specified. |
| **Incorrect coordinates** | Verify the image DPI; low‑resolution images may cause inaccurate bounds. |
| **Performance bottleneck on large images** | Resize the image to a reasonable resolution before calling `GetRectangles`. |
| **License exception** | Use a trial license for testing; apply a full license for production to avoid evaluation limits. |

## FAQ's

### Q1: Can I use Aspose.OCR for .NET with any type of image?

A1: Aspose.OCR supports a wide range of image formats, ensuring flexibility in your OCR applications.

### Q2: How accurate is the OCR recognition?

A2: Aspose.OCR leverages advanced algorithms for high accuracy, making it suitable for various text recognition scenarios.

### Q3: Is there a trial version available?

A3: Yes, you can explore the capabilities of Aspose.OCR for .NET with the [free trial](https://releases.aspose.com/).

### Q4: Where can I find comprehensive documentation?

A4: Refer to the [documentation](https://reference.aspose.com/ocr/net/) for detailed information and usage guidelines.

### Q5: Need assistance or have specific questions?

A5: Visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) for community support and discussions.

## Frequently Asked Questions

**Q: Can I extract individual words instead of whole lines?**  
A: Yes, use `AreasType.WORDS` with the same `GetRectangles` method to obtain word‑level bounding boxes.

**Q: Does the API support multi‑page PDFs?**  
A: Convert each PDF page to an image first, then call `GetRectangles` on each image.

**Q: How do I handle rotated text?**  
A: Enable the auto‑rotate option in the OCR settings or pre‑rotate the image before processing.

**Q: Is there a way to get confidence scores for each line?**  
A: After obtaining rectangles, call `api.RecognizeImage(...).Lines` to access line objects that include confidence values.

**Q: What .NET versions are compatible?**  
A: The library works with .NET Framework 4.5+, .NET Core 3.1+, and .NET 5/6.

## Conclusion

Congratulations! You've successfully **got OCR line rectangles** for an image using Aspose.OCR for .NET. With the bounding boxes in hand, you can now feed line coordinates into downstream workflows such as custom rendering, data extraction, or layout analysis.

---

**Last Updated:** 2025-12-17  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}