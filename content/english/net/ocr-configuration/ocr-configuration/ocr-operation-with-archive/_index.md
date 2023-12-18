---
title: OCROperation with Archive in OCR Image Recognition with Aspose.OCR for .NET
linktitle: OCROperation with Archive in OCR Image Recognition with Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
description: 
type: docs
weight: 10
url: /net/ocr-configuration//ocr-configuration/ocr-operation-with-archive/
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
    public class OCROperationWithArchive
    {
        public static void Run()
        {
            // ExStart:1   
            // The path to the documents directory.
            string dataDir = "Your Document Directory";

            // Initialize an instance of AsposeOcr
            AsposeOcr api = new AsposeOcr();

            // Image Path
            string fullPath = dataDir + "OCR.zip";

            // Recognize image           
            RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
            {
               //default or custom
            });

            // Print result
            for (int i = 0; i < result.Length; i++)
            {
                 Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
            }
           
            // ExEnd:1
            Console.WriteLine("OCROperationWithArchive executed successfully");
        }
    }
}

```
