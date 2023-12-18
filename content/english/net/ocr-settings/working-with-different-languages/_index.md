---
title: Working with Different Languages in OCR Image Recognition
linktitle: Working with Different Languages in OCR Image Recognition
second_title: Aspose.OCR .NET API
description: 
type: docs
weight: 15
url: /net/ocr-settings/working-with-different-languages/
---

## Complete Source Code
```csharp
using System.IO;

using Aspose.OCR;
using System;

namespace Aspose.OCR.Examples.CSharp.PerformingandManagingOCR
{
    public class WorkingWithDifferentLanguages
    {
        public static void Run()
        {
            // ExStart:1
            // The path to the documents directory.
            string dataDir = "Your Document Directory";

            // Initialize an instance of AsposeOcr
            AsposeOcr api = new AsposeOcr();

            // Recognize image
            string result = api.RecognizeImage(dataDir + "SpanishOCR.bmp");

            // Display the recognized text
            Console.WriteLine(result);
            // ExEnd:1

            Console.WriteLine("WorkingWithDifferentLanguages executed successfully");
        }
    }
}
```
