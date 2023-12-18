---
title: Perform OCR on Image in OCR Image Recognition with Aspose.OCR for .NET
linktitle: Perform OCR on Image in OCR Image Recognition with Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
description: 
type: docs
weight: 14
url: /net/ocr-configuration//ocr-configuration/perform-ocr-on-image/
---

## Complete Source Code
```csharp
using System;
using System.IO;
using Aspose.OCR;

namespace Aspose.OCR.Examples.CSharp.PerformingandManagingOCR
{
    public class PerformOCROnImage
    {
        public static void Run()
        {
            // ExStart:1   
            // The path to the documents directory.
            string dataDir = "Your Document Directory";

            // Initialize an instance of AsposeOcr
            AsposeOcr api = new AsposeOcr();

            // Recognize image
            string result = api.RecognizeImage(dataDir + "sample.png");

            // Display the recognized text
            Console.WriteLine(result);
            // ExEnd:1

            Console.WriteLine("PerformOCROnImage executed successfully");
        }
    }
}

```
