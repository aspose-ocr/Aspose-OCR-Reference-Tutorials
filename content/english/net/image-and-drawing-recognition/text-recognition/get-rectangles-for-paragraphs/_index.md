---
title: Get Rectangles for Paragraphs in OCR Image Recognition with Aspose.OCR for .NET
linktitle: Get Rectangles for Paragraphs in OCR Image Recognition with Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
description: 
type: docs
weight: 11
url: /net/image-and-drawing-recognition//text-recognition/get-rectangles-for-paragraphs/
---

## Complete Source Code
```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;

namespace Aspose.OCR.Examples.CSharp.PerformingandManagingOCR
{
    public class GetRectanglesParagraphs
    {
        public static void Run()
        {
            // ExStart:1   
            // The path to the documents directory.
            string dataDir = "Your Document Directory";

            // Initialize an instance of AsposeOcr
            AsposeOcr api = new AsposeOcr();

            // Image Path
            string fullPath = dataDir + "sample.png";

            // Recognize image           
            List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);// if you want to get a paragraphs  - don't set detect_areas = false

            // Print result           
            Console.WriteLine("Areas coordinates:");
            rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
            // ExEnd:1

            Console.WriteLine("GetRectanglesParagraphs executed successfully");
        }
    }
}

```