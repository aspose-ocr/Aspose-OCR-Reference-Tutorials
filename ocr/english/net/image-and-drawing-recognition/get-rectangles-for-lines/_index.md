---
title: Get Rectangles for Lines in OCR Image Recognition
linktitle: Get Rectangles for Lines in OCR Image Recognition
second_title: Aspose.OCR .NET API
description: Explore Aspose.OCR for .NET your key to precise OCR image recognition. Unleash the power of text extraction effortlessly.
weight: 10
url: /net/image-and-drawing-recognition/get-rectangles-for-lines/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Get Rectangles for Lines in OCR Image Recognition

## Introduction

Welcome to the world of Aspose.OCR for .NET, a powerful tool that allows you to harness the potential of Optical Character Recognition (OCR) in your .NET applications. Whether you're a seasoned developer or a curious enthusiast, this guide will walk you through the process of getting rectangles for lines in OCR image recognition using Aspose.OCR.

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

Now, let's break down the process of getting rectangles for lines in OCR image recognition into easy-to-follow steps.

## Step 1: Set Up Your Document Directory

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Replace `"Your Document Directory"` with the actual path to your document directory.

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

Utilize the `GetRectangles` method to retrieve rectangles for lines in the specified image.

## Step 5: Print Result

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Print the coordinates of the detected areas to the console.

## Conclusion

Congratulations! You've successfully obtained rectangles for lines in OCR image recognition using Aspose.OCR for .NET. This versatile tool opens up a world of possibilities for text extraction in your applications.

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

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
