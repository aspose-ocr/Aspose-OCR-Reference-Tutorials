---
title: Specify Ignored Characters in OCR Image Recognition
linktitle: Specify Ignored Characters in OCR Image Recognition
second_title: Aspose.OCR .NET API
description: 
type: docs
weight: 14
url: /net/ocr-settings/specify-ignored-characters/
---

## Complete Source Code
```csharp
using System.IO;

using Aspose.OCR;
using System;

namespace Aspose.OCR.Examples.CSharp.PerformingandManagingOCR
{
    public class SpecifyIgnoredCharacters
    {
        public static void Run()
        {
            // ExStart:1
            // The path to the documents directory.
            string dataDir = "Your Document Directory";

            // Initialize an instance of AsposeOcr
            AsposeOcr api = new AsposeOcr();

            // Recognize image
            RecognitionResult result = api.RecognizeImage(dataDir + "SpanishOCR.bmp", new RecognitionSettings
            {
                IgnoredCharacters = "ab1"
            });

            // Display the recognized text
            Console.WriteLine(result.RecognitionText);
            // ExEnd:1

            Console.WriteLine("WorkingWithDifferentLanguages executed successfully");
        }
    }
}
```
