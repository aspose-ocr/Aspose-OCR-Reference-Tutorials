---
title: Specify Allowed Characters in OCR Image Recognition
linktitle: Specify Allowed Characters in OCR Image Recognition
second_title: Aspose.OCR .NET API
description: 
type: docs
weight: 13
url: /net/ocr-settings/specify-allowed-characters/
---

## Complete Source Code
```csharp
using System;
using System.IO;
using Aspose.OCR;

namespace Aspose.OCR.Examples.CSharp.PerformingandManagingOCR
{
    public class SpecifyAllowedCharacters
    {
        public static void Run()
        {
            // ExStart:1   
            // The path to the documents directory.
            string dataDir = "Your Document Directory";

            // The first case:
            // Initialize an instance of AsposeOcr with allowed symbols
            AsposeOcr api = new AsposeOcr("0123456789");

            // Recognize image
            string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");

            // Display the recognized text
            Console.WriteLine(result);

            // The second case:
            // Initialize an instance of AsposeOcr with allowed symbols
            AsposeOcr api2 = new AsposeOcr();

            // Recognize image            
            RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
                new RecognitionSettings { 
                    AllowedCharacters = CharactersAllowedType.DIGITS,
                    RecognizeSingleLine = true
                });

            // Display the recognized text
            Console.WriteLine(result2.RecognitionText);
            // ExEnd:1

            Console.WriteLine("SpecifyAllowedCharacters executed successfully");
        }
    }
}

```
