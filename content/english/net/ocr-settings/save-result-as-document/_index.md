---
title: Save Result as Document in OCR Image Recognition
linktitle: Save Result as Document in OCR Image Recognition
second_title: Aspose.OCR .NET API
description: 
type: docs
weight: 10
url: /net/ocr-settings/save-result-as-document/
---

## Complete Source Code
```csharp
using System;
using System.IO;
using Aspose.OCR;

namespace Aspose.OCR.Examples.CSharp.PerformingandManagingOCR
{
    public class SaveResultAsDocument
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

            // Save the result in your preferred format
            result.Save(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx);
            result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
            result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
            result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
            // ExEnd:1

            Console.WriteLine("SaveResultAsDocument executed successfully");
        }
    }
}

```
