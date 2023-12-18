---
title: Recognize Line in OCR Image Recognition
linktitle: Recognize Line in OCR Image Recognition
second_title: Aspose.OCR .NET API
description: 
type: docs
weight: 14
url: /net/image-and-drawing-recognition/recognize-line/
---

## Complete Source Code
```csharp
using System;
using System.IO;
using Aspose.OCR;

namespace Aspose.OCR.Examples.CSharp.PerformingandManagingOCR
{
    public class RecognizeLine
    {
        public static void Run()
        {
            // ExStart:1   
            // The path to the documents directory.
            string dataDir = "Your Document Directory";

            // Initialize an instance of AsposeOcr
            AsposeOcr api = new AsposeOcr();

            // Recognize image
            string result = api.RecognizeLine(dataDir + "sample_line.png");

            // Display the recognized text
            Console.WriteLine(result);
            // ExEnd:1

            Console.WriteLine("RecognizeLine executed successfully");
        }
    }
}

```
