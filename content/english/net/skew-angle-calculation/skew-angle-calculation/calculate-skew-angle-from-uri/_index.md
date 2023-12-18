---
title: Calculate Skew Angle from URI in OCR Image Recognition with Aspose.OCR for .NET
linktitle: Calculate Skew Angle from URI in OCR Image Recognition with Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
description: 
type: docs
weight: 12
url: /net/skew-angle-calculation//skew-angle-calculation/calculate-skew-angle-from-uri/
---

## Complete Source Code
```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models.PreprocessingFilters;

namespace Aspose.OCR.Examples.CSharp.PerformingandManagingOCR
{
    public class CalculateSkewAngleFromUri
    {
        public static void Run()
        {
            // ExStart:1   

            // Initialize an instance of AsposeOcr
            AsposeOcr api = new AsposeOcr();

            // Calculate Angle
            float angle = api.CalculateSkewFromUri("https://i.stack.imgur.com/0A4M9.png");

            // Display the result
            Console.WriteLine(angle);
          
            // ExEnd:1

            Console.WriteLine("CalculateSkewAngleFromUri executed successfully");
        }
    }
}

```
