---
date: 2025-12-21
description: Aspose.OCR for .NET를 사용하여 OCR을 수행하고 이미지에서 텍스트를 추출하는 방법을 배웁니다. 이 단계별 가이드는
  다국어 텍스트 인식 및 언어 선택을 보여줍니다.
linktitle: How to Perform OCR with Language Selection in Aspose.OCR
second_title: Aspose.OCR .NET API
title: Aspose.OCR에서 언어 선택을 통한 OCR 수행 방법
url: /ko/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR에서 언어 선택으로 OCR 수행하는 방법

## Introduction

이미지에서 OCR을 수행하고 .NET 애플리케이션에서 이미지 파일의 텍스트를 추출해야 하는 경우, Aspose.OCR for .NET은 빠르고 정확하며 언어를 인식하는 솔루션을 제공합니다. 이 튜토리얼에서는 언어 선택이 가능한 OCR 이미지 인식을 보여주는 실제 예제를 단계별로 살펴보며, 몇 줄의 코드만으로 사진에서 다국어 텍스트를 추출할 수 있습니다.

## Quick Answers
- **What does Aspose.OCR do?** It recognizes printed and handwritten text in images and returns the extracted text.  
- **Can I choose the language?** Yes – you can specify any supported language such as English, German, Spanish, Chinese, etc.  
- **Do I need a license for development?** A free trial works for evaluation; a license is required for production use.  
- **Which .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Is skew correction automatic?** You can enable `AutoSkew` and fine‑tune the `SkewAngle` setting.

## Why Choose Aspose.OCR for OCR Tasks?

- **High accuracy** across multiple fonts and image qualities.  
- **Built‑in language selection** eliminates the need for external language packs.  
- **Simple API** that integrates cleanly with existing C# projects.  
- **No external dependencies** – everything runs locally, keeping your data secure.

## Prerequisites

Before we dive into the code, make sure you have the following prerequisites in place:

- Aspose.OCR for .NET: Ensure that you have the Aspose.OCR library installed. You can download it from the [Aspose.OCR for .NET download page](https://releases.aspose.com/ocr/net/).

- Development Environment: Set up a working environment with a .NET application. If you haven't done this yet, refer to the [documentation](https://reference.aspose.com/ocr/net/) for detailed instructions.

## Import Namespaces

In your .NET application, start by importing the necessary namespaces:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Step 1: Initialize Aspose.OCR

Begin by initializing an instance of the Aspose.OCR class. This sets the stage for utilizing the OCR capabilities within your application.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Step 2: Specify Image Path

Next, define the path to the image you want to perform OCR on. Ensure the image is accessible from your application.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## Step 3: Recognize Image with Language Selection

Now comes the core OCR operation. Utilize the Aspose.OCR library to recognize text from the specified image. Adjust recognition settings, including language selection.

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Choose the language: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## Step 4: Print and Display Results

After the OCR operation, print and display the results, including recognized text, areas, warnings, and JSON representation.

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

## Common Issues and Tips

- **Incorrect language selection** – If the output looks garbled, double‑check that the `Language` property matches the language of the source image.  
- **Skewed images** – Enable `AutoSkew` or manually adjust `SkewAngle` for better accuracy on tilted scans.  
- **Large files** – Process large images in chunks or reduce resolution before feeding them to `RecognizeImage` to conserve memory.

## Conclusion

Congratulations! You've learned **how to perform OCR** with language selection using Aspose.OCR for .NET. This tutorial showed you how to extract text from image files, customize recognition settings, and handle multilingual content effortlessly.

## FAQ's

### Q1: Is Aspose.OCR suitable for multilingual text recognition?

A1: Yes, Aspose.OCR supports various languages, providing flexibility for multilingual OCR tasks.

### Q2: Can I fine‑tune OCR settings for specific image characteristics?

A2: Absolutely! Adjust parameters like skew angle, line recognition, and area detection to optimize OCR for different scenarios.

### Q3: Where can I find additional support or community discussions?

A3: Visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) for support and discussions with the community.

### Q4: Is there a free trial available?

A4: Yes, explore the [free trial](https://releases.aspose.com/) to experience the capabilities of Aspose.OCR.

### Q5: How can I purchase Aspose.OCR for .NET?

A5: To purchase, visit the [purchase page](https://purchase.aspose.com/buy).

---

**Last Updated:** 2025-12-21  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}