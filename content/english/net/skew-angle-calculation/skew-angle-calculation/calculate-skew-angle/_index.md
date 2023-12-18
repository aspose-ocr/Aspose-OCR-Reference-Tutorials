---
title: Calculate Skew Angle in OCR Image Recognition with Aspose.OCR for .NET
linktitle: Calculate Skew Angle in OCR Image Recognition with Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
description: 
type: docs
weight: 10
url: /net/skew-angle-calculation//skew-angle-calculation/calculate-skew-angle/
---

## Complete Source Code
```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;

namespace Aspose.OCR.Examples.CSharp.PerformingandManagingOCR
{
    public class CalculateSkewAngle
    {
        public static void Run()
        {
            // ExStart:1   
            // The path to the documents directory.
            string dataDir = "Your Document Directory";

            // Initialize an instance of AsposeOcr
            AsposeOcr api = new AsposeOcr();

            // Calculate Angle
            float angle = api.CalculateSkew(dataDir + "skew_image.png");

            // Display the result
            Console.WriteLine(angle);
            // ExEnd:1

            Console.WriteLine("CalculateSkewAngle executed successfully");
        }
    }
}

```
