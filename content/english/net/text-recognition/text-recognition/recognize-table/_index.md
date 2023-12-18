---
title: Recognize Table in OCR Image Recognition with Aspose.OCR for .NET
linktitle: Recognize Table in OCR Image Recognition with Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
description: 
type: docs
weight: 15
url: /net/text-recognition//text-recognition/recognize-table/
---

## Complete Source Code
```csharp
using System;
using System.IO;
using Aspose.OCR;

namespace Aspose.OCR.Examples.CSharp.PerformingandManagingOCR
{
    public class RecognizeTable
    {
        public static void Run()
        {
            // ExStart:1   
            // The path to the documents directory.
            string dataDir = "Your Document Directory";

            // Initialize an instance of AsposeOcr
            AsposeOcr api = new AsposeOcr();

            // Recognize image
            RecognitionResult result = api.RecognizeImage(dataDir + "table.png", new RecognitionSettings
            {
                LinesFiltration = true, // if all image is table
                DetectAreas = false
                // or
                // LinesFiltration = false, 
                // DetectAreas = true //- for auto detect areas with table
            });
            // Display the recognized text
            Console.WriteLine(result.RecognitionText);
            // ExEnd:1

            Console.WriteLine("SetThresholdValue executed successfully");
        }
    }
}

```