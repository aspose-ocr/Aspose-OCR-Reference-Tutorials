---
title: Recognize Image without Text Area Detection in OCR Image Recognition
linktitle: Recognize Image without Text Area Detection in OCR Image Recognition
second_title: Aspose.OCR .NET API
description: 
type: docs
weight: 17
url: /net/text-recognition/recognize-image-without-text-area-detection/
---

## Complete Source Code
```csharp
using System;
using System.IO;
using Aspose.OCR;

namespace Aspose.OCR.Examples.CSharp.PerformingandManagingOCR
{
    public class RecognizeImageWithoutTextAreaDetection
    {
        public static void Run()
        {
            // ExStart:1   
            // The path to the documents directory.
            string dataDir = "Your Document Directory";

            // Initialize an instance of AsposeOcr
            AsposeOcr api = new AsposeOcr();

            // Recognize image
            string result = api.RecognizeImage(dataDir + "sample.png", false);

            // Display the recognized text
            Console.WriteLine(result);
            // ExEnd:1

            Console.WriteLine("RecognizeImageWithoutTextAreaDetection executed successfully");
        }
    }
}

```