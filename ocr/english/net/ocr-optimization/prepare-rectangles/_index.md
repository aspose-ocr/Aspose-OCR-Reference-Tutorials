---
title: "How to Extract Text from Image by Preparing Rectangles in OCR"
linktitle: "Prepare Rectangles in OCR Image Recognition"
second_title: "Aspose.OCR .NET API"
description: "Learn how to extract text from image using Aspose.OCR for .NET. This guide walks you through preparing rectangles for OCR image recognition and boosting accuracy."
weight: 11
url: /net/ocr-optimization/prepare-rectangles/
date: 2025-12-22
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Prepare Rectangles in OCR Image Recognition

## Introduction

Optical Character Recognition (OCR) is essential for converting visual content into searchable, editable text. In this tutorial you’ll **extract text from image** by preparing custom rectangles that focus the OCR engine on specific regions. Using Aspose.OCR for .NET, we’ll walk through every step—from setting up your project to retrieving the recognized text—so you can integrate powerful image‑to‑text functionality into your .NET applications.

## Quick Answers
- **What does “extract text from image” mean?** It means converting the visual characters in a picture into machine‑readable strings.  
- **Which library helps with this in .NET?** Aspose.OCR for .NET.  
- **Do I need a license for development?** A free trial works for testing; a license is required for production.  
- **Can I target specific areas?** Yes, by defining rectangles that limit the OCR scope.  
- **What .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## What is “extract text from image” with rectangles?
When you define rectangular zones on an image, the OCR engine processes only those zones. This improves accuracy, reduces processing time, and lets you ignore noisy backgrounds or irrelevant sections.

## Why prepare rectangles before OCR?
- **Focus on relevant content:** Skip headers, footers, or decorative graphics.  
- **Boost performance:** Smaller regions mean faster recognition.  
- **Improve accuracy:** Less visual noise leads to cleaner results.

## Prerequisites

- Familiarity with C# and .NET development.  
- Aspose.OCR for .NET library installed – you can download it **[here](https://releases.aspose.com/ocr/net/)**.  
- A sample image (e.g., `sample.png`) that contains the text you want to extract.

## Import Namespaces

First, bring the required namespaces into scope:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Step 1: Set Up Your Document Directory

Specify where your image files live and create an instance of the OCR engine.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## How to extract text from image using multiple rectangles

### Step 2: Recognize Image with Multiple Rectangles

#### 2.1 Define the rectangles

Create a list of `Rectangle` objects that outline the areas you want the OCR engine to scan.

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 Perform OCR recognition

Pass the image path and the rectangle list to `RecognizeImage`. The method returns a collection of strings—each entry corresponds to one rectangle.

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### Step 3: Recognize Image with Recognition Settings (Alternative Approach)

If you prefer using `RecognitionSettings`, you can achieve the same result with a slightly different API call.

#### 3.1 Define recognition settings

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 Display recognized text

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Common Issues & Tips

- **Incorrect rectangle coordinates:** Ensure the `X`, `Y`, `Width`, and `Height` values correctly map to the region you want.  
- **Image quality:** Low‑resolution images may yield poor OCR results; consider pre‑processing (e.g., binarization).  
- **Empty results:** Verify that the rectangles actually contain text; otherwise the engine returns empty strings.

## Conclusion

You’ve now learned how to **extract text from image** by preparing custom rectangles with Aspose.OCR for .NET. This technique gives you fine‑grained control over OCR processing, helping you build faster, more accurate text‑extraction features in your applications.

## Frequently Asked Questions

**Q:** Can I use Aspose.OCR for .NET with other .NET frameworks?  
**A:** Yes, Aspose.OCR for .NET is compatible with various .NET frameworks.

**Q:** Is there a free trial available for Aspose.OCR for .NET?  
**A:** Absolutely! You can access the free trial **[here](https://releases.aspose.com/)**.

**Q:** How do I get support for Aspose.OCR for .NET?  
**A:** Visit the **[Aspose.OCR forum](https://forum.aspose.com/c/ocr/16)** for dedicated support.

**Q:** Can I obtain a temporary license for testing purposes?  
**A:** Yes, you can acquire a temporary license **[here](https://purchase.aspose.com/temporary-license/)**.

**Q:** Where can I find the documentation for Aspose.OCR for .NET?  
**A:** The documentation is available **[here](https://reference.aspose.com/ocr/net/)**.

---

**Last Updated:** 2025-12-22  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}