---
category: general
date: 2026-03-17
description: C#에서 Aspose OCR을 사용하여 PNG에서 텍스트를 추출합니다. 이미지에서 텍스트를 읽는 방법, 영수증 OCR을 처리하는
  방법, GPU 가속을 이용한 OCR 엔진을 만드는 방법을 배웁니다.
draft: false
keywords:
- extract text from png
- read text from image
- ocr receipt image
- process receipt ocr
- create ocr engine
language: ko
og_description: Aspose OCR을 사용하여 PNG에서 텍스트를 추출합니다. 이 가이드는 이미지에서 텍스트를 읽고, 영수증 OCR을
  처리하며, OCR 엔진을 효율적으로 만드는 방법을 보여줍니다.
og_title: PNG에서 텍스트 추출 – OCR로 이미지에서 텍스트 읽기
tags:
- OCR
- CSharp
- Aspose
title: PNG에서 텍스트 추출 – OCR로 이미지에서 텍스트 읽기
url: /ko/net/text-recognition/extract-text-from-png-read-text-from-image-with-ocr/
---

translate column headers and content.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG에서 텍스트 추출 – 이미지에서 텍스트 읽기 (OCR)

PNG에서 **텍스트를 추출**해야 했지만 어떤 라이브러리가 신뢰할 수 있는 결과를 제공할지 몰랐던 적이 있나요? 여러분만 그런 것이 아닙니다—개발자들은 “영수증 같은 이미지 파일에서 커스텀 신경망을 만들지 않고 텍스트를 어떻게 읽을 수 있나요?” 라는 질문을 끊임없이 합니다. 좋은 소식은 Aspose OCR이 무거운 작업을 대신 해 주며, GPU를 활용해 속도를 높일 수도 있다는 점입니다.

이 튜토리얼에서는 **영수증 OCR 처리**에 필요한 모든 과정을 단계별로 살펴봅니다. NuGet 패키지 설치부터 PNG 파일을 이해하는 OCR 엔진 생성까지. 최종적으로는 영수증 이미지를 읽고 인식된 텍스트를 출력하는 독립 실행형 콘솔 앱을 만들고, 다양한 시나리오에 맞게 엔진을 조정하는 방법도 알려드립니다. 외부 문서는 없으며 순수 코드와 명확한 설명만 제공합니다.

## Prerequisites

- .NET 6.0 SDK (또는 최신 .NET 버전)  
- Visual Studio 2022 또는 C# 확장 기능이 설치된 VS Code  
- 최신 드라이버가 설치된 지원되는 NVIDIA GPU (선택 사항이지만 GPU 모드에 권장)  
- **Aspose.OCR** NuGet 패키지 (`dotnet add package Aspose.OCR`)  

GPU가 없더라도 CPU 모드에서 예제를 실행할 수 있습니다—GPU 설정 라인만 건너뛰면 됩니다.

## Step 1: Install Aspose.OCR and Set Up the Project

First, create a new console project and bring in the Aspose OCR library.

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Why this matters: the `Aspose.OCR` package bundles the OCR engine, image loaders, and optional GPU support. Adding it via NuGet ensures you get the latest stable version (as of March 2026 it’s 23.10).

## Step 2: Import Namespaces and Create the OCR Engine

Now open **Program.cs** and add the required `using` directives. Then instantiate the engine.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Optional: Enable GPU acceleration if a compatible GPU is present
            // This dramatically speeds up processing of high‑resolution PNGs
            ocrEngine.Config.EngineMode = EngineMode.Gpu;   // <-- primary way to "process receipt ocr" fast
            ocrEngine.Config.GpuDeviceId = 0; // selects the first GPU in the system

            // The rest of the code follows...
```

**Pro tip:** If you run into `System.DllNotFoundException` on machines without a GPU, simply comment out the two lines that set `EngineMode` and `GpuDeviceId`. The engine will fall back to CPU automatically.

## Step 3: Load the PNG Image You Want to Extract Text From

Aspose OCR can read images directly from a file path, a stream, or even a byte array. For this demo we’ll load a local receipt image.

```csharp
            // Step 3: Load the image (replace the path with your own PNG file)
            string imagePath = @"C:\Images\receipt.png";

            // Validate the file exists to avoid runtime surprises
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }

            // Load the image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Notice how we guard against a missing file. In real‑world apps you’d probably surface a friendly UI message instead of just exiting.

## Step 4: Perform the OCR Recognition

The actual text extraction happens with a single method call. The engine returns an `OcrResult` object that contains the raw string, confidence scores, and layout information.

```csharp
            // Step 4: Run the OCR process
            OcrResult ocrResult = ocrEngine.Recognize();

            // Check if the engine succeeded
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }
```

Why we check `ocrResult.Text`: sometimes a low‑quality PNG yields an empty string, and it’s better to let the user know than to output nothing silently.

## Step 5: Output the Recognized Text

Finally, print the extracted string to the console. You can also write it to a file, a database, or feed it into another service.

```csharp
            // Step 5: Display the recognized text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

When you run the program (`dotnet run`), you should see something like:

```
=== Extracted Text from PNG ===
Store: Coffee Corner
Date: 03/15/2026
Item      Qty   Price
Latte      2    $5.40
Muffin     1    $2.30
Total            $7.70
=== End of Output ===
```

That’s the **complete solution to extract text from PNG** files with Aspose OCR, and you’ve just learned how to **read text from image** files that look like receipts.

## Optional: Fine‑Tuning the OCR Engine (Advanced)

If you need higher accuracy for specific fonts or noisy backgrounds, consider adjusting these settings:

```csharp
// Enable language detection (default is English)
ocrEngine.Config.Language = Language.English;

// Turn on automatic image preprocessing (deskew, binarization)
ocrEngine.Config.EnableImagePreprocessing = true;

// Set a confidence threshold if you only want high‑certainty results
ocrEngine.Config.ConfidenceThreshold = 0.75f;
```

These tweaks are especially useful when you **process receipt OCR** in batch jobs where some scans are less than perfect.

## Common Pitfalls & How to Avoid Them

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **GPU driver missing** | The engine tries to load CUDA but can’t find the DLL. | Install the latest NVIDIA driver or switch to CPU mode by removing the `EngineMode.Gpu` line. |
| **Incorrect image path** | `ImageStream.FromFile` throws if the file isn’t found. | Always validate the path (see Step 3) or use `Path.Combine` for cross‑platform safety. |
| **Low confidence on blurry receipts** | The OCR engine can’t differentiate characters. | Enable `EnableImagePreprocessing` and optionally increase image DPI before feeding it to the engine. |
| **Memory leak in long‑running services** | Each `OcrEngine` holds unmanaged resources. | Dispose of the engine after use: `using var ocrEngine = new OcrEngine();` |

## Full Working Example (Copy‑Paste)

Below is the **entire program** you can drop into `Program.cs`. It includes all the optional tweaks commented out for easy activation.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            using var ocrEngine = new OcrEngine();

            // Enable GPU acceleration if you have a supported card
            ocrEngine.Config.EngineMode = EngineMode.Gpu;
            ocrEngine.Config.GpuDeviceId = 0;

            // Optional fine‑tuning (uncomment as needed)
            //ocrEngine.Config.Language = Language.English;
            //ocrEngine.Config.EnableImagePreprocessing = true;
            //ocrEngine.Config.ConfidenceThreshold = 0.75f;

            // Load PNG image
            string imagePath = @"C:\Images\receipt.png";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize();

            // Verify result
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }

            // Output the extracted text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Save, run `dotnet run`, and you’ll see the receipt’s contents printed to the console.

![extract text from png example](receipt.png "extract text from png example")

*The image above shows a sample receipt PNG that the code can process.*

## Recap

We’ve covered how to **extract text from PNG** files using Aspose OCR, demonstrated how to **read text from image** files, and walked through a complete **process receipt OCR** pipeline that includes optional GPU acceleration. By **creating an OCR engine** yourself, you gain full control over configuration, performance, and error handling.

## What to Explore Next?

- **Batch processing**: Loop over a directory of PNG receipts and write each result to a CSV file.  
- **Integration with Azure Functions**: Turn this console app into a serverless endpoint that accepts image uploads.  
- **Multi‑language support**: Swap `Language.English` for `Language.Spanish` or add custom dictionaries.  
- **Post‑processing**: Use regular expressions to extract fields like total amount, date, or tax ID from the raw OCR string.

Feel free to experiment—OCR is a surprisingly flexible tool once you know the right knobs to turn. If you hit any snags, drop a comment below or check the Aspose OCR API reference for deeper dives.

Happy coding, and enjoy turning those stubborn PNG receipts into searchable text!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}