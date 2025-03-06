---
title: Get Rectangles for Paragraphs in OCR Image Recognition
linktitle: Get Rectangles for Paragraphs in OCR Image Recognition
second_title: Aspose.OCR .NET API
description: Unlock advanced OCR capabilities with Aspose.OCR for .NET. Extract paragraph rectangles effortlessly.
weight: 11
url: /net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Get Rectangles for Paragraphs in OCR Image Recognition

## Introduction

Welcome to our comprehensive guide on leveraging Aspose.OCR for .NET to extract paragraph rectangles in OCR image recognition. If you're looking to enhance your document processing capabilities and harness the power of Optical Character Recognition (OCR) in your .NET applications, you're in the right place.

## Prerequisites

Before we dive into the tutorial, make sure you have the following prerequisites in place:

- Basic knowledge of C# and .NET development.
- A development environment set up with Aspose.OCR for .NET. If you haven't already, you can download it [here](https://releases.aspose.com/ocr/net/).
- An understanding of image processing concepts and the importance of OCR in extracting text from images.

## Import Namespaces

In your C# code, ensure you have the necessary namespaces imported to use Aspose.OCR efficiently. Include the following at the top of your file:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Step 1: Set Up Your Document Directory

Begin by initializing the path to your document directory where the images for OCR processing are stored:

```csharp
string dataDir = "Your Document Directory";
```

## Step 2: Initialize AsposeOcr Instance

Create an instance of the AsposeOcr class to gain access to OCR functionalities:

```csharp
AsposeOcr api = new AsposeOcr();
```

## Step 3: Specify the Image Path

Define the full path to the image you want to process:

```csharp
string fullPath = dataDir + "sample.png";
```

## Step 4: Recognize Image and Get Paragraph Rectangles

Invoke the `GetRectangles` method to obtain rectangles for paragraphs in the OCR image. Set `detect_areas` to `true` if you want to extract paragraphs:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## Step 5: Print Results

Print the coordinates of the identified areas:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## Step 6: Conclusion

Congratulations! You've successfully executed the OCR image recognition process to obtain rectangles for paragraphs using Aspose.OCR for .NET.

## Conclusion

In this tutorial, we've explored the fundamental steps to integrate Aspose.OCR for .NET into your applications, allowing you to extract paragraph rectangles from OCR-processed images. Aspose.OCR simplifies the implementation of OCR, making it a valuable tool for document processing and text extraction.

## FAQ's

### Q1: Is Aspose.OCR compatible with different image formats?

A1: Yes, Aspose.OCR supports various image formats, including PNG, JPEG, and TIFF.

### Q2: Can I use Aspose.OCR for batch processing of multiple images?

A2: Absolutely! Aspose.OCR facilitates batch processing to handle multiple images seamlessly.

### Q3: Is there a free trial available for Aspose.OCR for .NET?

A3: Yes, you can explore a free trial [here](https://releases.aspose.com/).

### Q4: How can I obtain a temporary license for Aspose.OCR?

A4: You can acquire a temporary license [here](https://purchase.aspose.com/temporary-license/).

### Q5: Where can I find additional support and discussions related to Aspose.OCR?

A5: Head over to the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) for community support and discussions.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
