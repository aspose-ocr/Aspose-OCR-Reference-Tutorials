---
title: Recognize Line in OCR Image Recognition with Aspose.OCR for .NET
linktitle: Recognize Line in OCR Image Recognition with Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
description: 
type: docs
weight: 18
url: /net/text-recognition//text-recognition/recognize-line/
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
