---
title: Set Threads Count in OCR Image Recognition with Aspose.OCR for .NET
linktitle: Set Threads Count in OCR Image Recognition with Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
description: 
type: docs
weight: 11
url: /net/ocr-settings//ocr-settings/set-threads-count/
---

## Complete Source Code
```csharp
using System;
using System.IO;
using Aspose.OCR;

namespace Aspose.OCR.Examples.CSharp.PerformingandManagingOCR
{
    public class SetThreadsCount
    {
        public static void Run()
        {
            // ExStart:1   
            // The path to the documents directory.
            string dataDir = "Your Document Directory";

            // Initialize an instance of AsposeOcr
            AsposeOcr api = new AsposeOcr();

            // Recognize image
            RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
            {
                ThreadsCount = 2 // O - means auto calculate
            });
            // Display the recognized text
            Console.WriteLine(result.RecognitionText);
            // ExEnd:1

            Console.WriteLine("SetThresholdValue executed successfully");
        }
    }
}

```
