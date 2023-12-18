---
title: Get Result as JSON in OCR Image Recognition
linktitle: Get Result as JSON in OCR Image Recognition
second_title: Aspose.OCR .NET API
description: 
type: docs
weight: 12
url: /net/text-recognition/get-result-as-json/
---

## Complete Source Code
```csharp
using System;
using System.IO;
using Aspose.OCR;

namespace Aspose.OCR.Examples.CSharp.PerformingandManagingOCR
{
    public class GetResultAsJson
    {
        public static void Run()
        {
            // ExStart:1   
            // The path to the documents directory.
            string dataDir = "Your Document Directory";

            // Initialize an instance of AsposeOcr
            AsposeOcr api = new AsposeOcr();

            // Recognize image
            RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });

            // Display the recognition result in JSON format
            Console.WriteLine(result.GetJson());
            // ExEnd:1

            Console.WriteLine("GetResultAsJson executed successfully");
        }
    }
}

```
