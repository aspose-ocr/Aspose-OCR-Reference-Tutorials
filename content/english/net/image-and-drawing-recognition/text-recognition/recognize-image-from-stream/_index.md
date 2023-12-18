---
title: Recognize Image from Stream in OCR Image Recognition with Aspose.OCR for .NET
linktitle: Recognize Image from Stream in OCR Image Recognition with Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
description: 
type: docs
weight: 12
url: /net/image-and-drawing-recognition//text-recognition/recognize-image-from-stream/
---

## Complete Source Code
```csharp
using System;
using System.IO;
using Aspose.OCR;

namespace Aspose.OCR.Examples.CSharp.PerformingandManagingOCR
{
    public class RecognizeImageFromStream
    {
        public static void Run()
        {
            // ExStart:1   
            // The path to the documents directory.
            string dataDir = "Your Document Directory";
            string result = "";

            // Initialize an instance of AsposeOcr
            AsposeOcr api = new AsposeOcr();

            // Recognize image
            using (MemoryStream ms = new MemoryStream())
            using (FileStream file = new FileStream(dataDir + "sample.png", FileMode.Open, FileAccess.Read))
            {
                file.CopyTo(ms);
                result = api.RecognizeImage(ms);
            }

            // Display the recognized text
            Console.WriteLine(result);
            // ExEnd:1

            Console.WriteLine("RecognizeImageFromStream executed successfully");
        }
    }
}

```
