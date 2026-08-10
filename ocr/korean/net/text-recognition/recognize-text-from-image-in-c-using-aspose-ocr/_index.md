---
category: general
date: 2026-05-31
description: Aspose OCR을 사용해 C#에서 이미지의 텍스트를 인식하는 방법을 배우고, tiff 파일에서 텍스트를 추출하고 OCR을
  효율적으로 수행하기 위해 이미지를 로드하는 방법을 포함합니다.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- Aspose OCR C#
- GPU accelerated OCR
language: ko
og_description: Aspose OCR을 사용하여 이미지에서 텍스트를 인식하는 단계별 가이드로, TIFF에서 추출 및 OCR을 위한 올바른
  이미지 로딩을 다룹니다.
og_title: Aspose OCR을 사용하여 C#에서 이미지의 텍스트 인식
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to recognize text from image in C# with Aspose OCR, including
    how to extract text from tiff files and load image for OCR efficiently.
  headline: recognize text from image in C# using Aspose OCR
  type: TechArticle
- questions:
  - answer: Reduce its resolution before feeding it to the engine, or increase `GpuMemoryLimit`
      if you have enough VRAM.
    question: What if the image is huge (over 10 MB)?
  - answer: Absolutely. Just reuse the same `OcrEngine` instance and assign a new
      `ImageStream` each iteration.
    question: Can I process multiple images in a loop?
  - answer: '`OcrEngine` implements `IDisposable`. Wrap it in a `using` block for
      clean resource management, especially when working with GPU resources.'
    question: Do I need to dispose of anything?
  - answer: Set `engine.Language = OcrLanguage.Spanish` (or any supported language)
      before calling `Recognize()`.
    question: What about languages other than English?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: Aspose OCR을 사용하여 C#에서 이미지의 텍스트 인식
url: /ko/net/text-recognition/recognize-text-from-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 Aspose OCR을 사용하여 이미지에서 텍스트 인식하기

이미지에서 텍스트를 인식해야 했지만 C#에서 어디서 시작해야 할지 몰랐던 적이 있나요? 당신만 그런 것이 아닙니다—많은 개발자들이 스캔 문서나 다중 페이지 TIFF를 다룰 때 이 문제에 부딪힙니다. 이 가이드에서는 Aspose OCR 라이브러리를 사용하여 **recognize text from image**하는 완전한 실행 가능한 예제를 단계별로 안내하고, **extract text from tiff**와 **load image for OCR**하는 최적의 방법도 보여드립니다.

우리는 NuGet 패키지 설치부터 GPU 가속 처리 및 필요 시 CPU로 폴백하는 방법까지 모두 다룰 것입니다. 이 튜토리얼을 마치면 인식된 텍스트와 처리 시간을 출력하는 콘솔 앱을 갖게 됩니다—빠진 부분 없이, 모호한 언급도 없습니다.

## 만들게 될 것

- 이미지(다중 페이지 TIFF 포함)를 로드하는 간단한 .NET 콘솔 애플리케이션  
- GPU 사용으로 구성된 OCR 엔진, 필요 시 부드러운 CPU 폴백 지원  
- 이미지에서 추출한 일반 텍스트를 콘솔에 출력  
- GPU와 CPU 간 성능 차이를 확인할 수 있는 처리 시간 정보  

**필수 조건**

- .NET 6 SDK 이상(.NET Core 및 .NET Framework에서도 동작)  
- C#와 명령줄에 대한 기본 지식  
- Aspose.OCR NuGet 패키지를 가져오기 위한 인터넷 연결  

위 조건을 갖추셨다면, 시작해 봅시다.

![Aspose OCR을 사용하여 이미지에서 텍스트를 인식하는 C# 코드](image.png "Aspose OCR을 사용하여 이미지에서 텍스트를 인식하는 C# 코드")

## Step 1 – 이미지에서 텍스트 인식: OCR 엔진 설정

우선, `OcrEngine` 인스턴스가 필요합니다. Aspose OCR은 처리 장치를 선택할 수 있게 해 줍니다—속도를 위해 GPU, 안전망으로 CPU. 엔진은 메모리 제한 힌트도 받아들여 공유 머신에서 유용합니다.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Create the OCR engine and request GPU acceleration.
        // If no compatible GPU is found, Aspose silently falls back to CPU.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,      // Try GPU first
            GpuMemoryLimit = 1024        // Optional: cap GPU memory usage (MB)
        };
```

**왜 중요한가:**  
`OcrDevice.Gpu`를 선택하면 특히 다중 페이지 TIFF와 같은 큰 이미지의 인식 시간을 몇 초 단축할 수 있습니다. `GpuMemoryLimit`는 공유 워크스테이션에서 앱이 모든 GPU 메모리를 독점하는 것을 방지합니다.

## Step 2 – OCR을 위한 이미지 로드 (TIFF 지원 포함)

이제 엔진에 이미지를 전달합니다. Aspose의 `ImageStream.FromFile`은 라이브러리가 지원하는 **any** 형식—TIFF, PNG, JPEG 등—을 받아들입니다. 이 단계는 **load image for OCR** 요구 사항을 직접 해결합니다.

```csharp
        // Load the image you want to process.
        // Replace the path with the actual location of your TIFF or other image.
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");
```

**Pro tip:** 다중 페이지 TIFF를 다루는 경우, Aspose는 각 페이지를 자동으로 별개의 프레임으로 처리하며 엔진은 순차적으로 처리합니다. 추가 코드가 필요 없습니다.

## Step 3 – 인식 실행 및 **extract text from tiff**

엔진이 준비되고 이미지가 로드되면 OCR 작업을 시작합니다. `Recognize` 메서드는 일반 텍스트, 신뢰도 점수, 타이밍 세부 정보를 포함하는 `OcrResult`를 반환합니다.

```csharp
        // Perform the OCR operation.
        OcrResult result = engine.Recognize();
```

**Edge case handling:**  
GPU를 사용할 수 없는 경우에도 `engine.Recognize()`는 엔진이 조용히 CPU로 전환하기 때문에 작동합니다. 실제 사용된 장치를 기록해야 한다면 인식 후 `engine.Device`를 확인할 수 있습니다.

## Step 4 – 인식된 일반 텍스트 가져오기

텍스트 추출은 간단합니다—`Text` 속성을 읽기만 하면 됩니다. 여기서 **extract text from tiff**(또는 다른 이미지) 작업을 최종적으로 수행하고 사용자에게 보여줍니다.

```csharp
        // Output the plain text that was extracted.
        Console.WriteLine($"Text:\n{result.Text}");
```

원본 이미지에 나타난 대로 원시 문자와 줄 바꿈이 보존됩니다. JSON이나 CSV와 같은 더 구조화된 출력이 필요하면 `result.Regions`와 `result.Lines`를 살펴볼 수 있지만, 일반 텍스트만으로도 대부분의 간단한 스크립트에 충분합니다.

## Step 5 – 처리 시간 측정 및 GPU 폴백 처리

성능은 특히 수십 페이지를 처리할 때 중요합니다. `ProcessingTime` 속성은 GPU든 CPU든 OCR에 걸린 시간을 정확히 알려줍니다.

```csharp
        // Show how long the recognition took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Why you should care:**  
시간이 급격히 늘어나는 것을 발견하면 `GpuMemoryLimit`를 조정하거나 CPU로 명시적으로 전환(`Device = OcrDevice.Cpu`)할 수 있습니다. 반대로 큰 TIFF에서 1초 미만의 결과가 나오면 GPU 가속이 제대로 작동하고 있다는 의미입니다.

## 전체 실행 가능한 예제

아래 코드를 새 콘솔 프로젝트(`dotnet new console -n OcrDemo`)에 복사하고 `dotnet add package Aspose.OCR`를 실행하세요. 그런 다음 `YOUR_DIRECTORY/sample_multi_page.tif`를 이미지 경로로 교체합니다.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine with GPU preference.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,
            GpuMemoryLimit = 1024
        };

        // Step 2: Load image for OCR (supports TIFF, PNG, JPEG, etc.).
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");

        // Step 3: Run recognition – this will also **extract text from tiff**.
        OcrResult result = engine.Recognize();

        // Step 4: Retrieve and display the recognized plain text.
        Console.WriteLine($"Text:\n{result.Text}");

        // Step 5: Display how long the operation took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**예상 출력 (간략히 표시):**

```
Text:
Invoice #12345
Date: 2026-05-01
Total: $1,250.00
...
Time elapsed: 1.42s
```

머신에 적절한 GPU가 없으면 경과 시간이 몇 초 더 길어질 수 있지만, 텍스트는 여전히 올바르게 추출됩니다.

## 일반적인 질문 및 주의 사항

- **이미지가 너무 큰 경우(10 MB 초과)**  
  엔진에 전달하기 전에 해상도를 낮추거나 VRAM이 충분하면 `GpuMemoryLimit`를 늘리세요.  
- **여러 이미지를 루프에서 처리할 수 있나요?**  
  가능합니다. 동일한 `OcrEngine` 인스턴스를 재사용하고 각 반복마다 새로운 `ImageStream`을 할당하면 됩니다.  
- **특별히 해제해야 할 것이 있나요?**  
  `OcrEngine`은 `IDisposable`을 구현합니다. 특히 GPU 리소스를 사용할 때는 `using` 블록으로 감싸서 자원을 깔끔히 관리하세요.  

```csharp
using (OcrEngine engine = new OcrEngine { Device = OcrDevice.Gpu })
{
    // ... same steps as before
}
```

- **영어 외 다른 언어는 어떻게 하나요?**  
  `Recognize()` 호출 전에 `engine.Language = OcrLanguage.Spanish`(또는 지원되는 다른 언어)로 설정하세요.  

## 결론

이제 Aspose OCR을 사용하여 C#에서 **recognize text from image**하는 완전한 엔드‑투‑엔드 솔루션을 갖추었습니다. 이 튜토리얼에서는 **load image for OCR**, **extract text from tiff** 방법과 성능을 측정하고 GPU 폴백을 우아하게 처리하는 방법을 다루었습니다.

다음 단계로는 다음을 시도해 볼 수 있습니다:
- 다양한 이미지 형식(BMP, PDF)으로 실험하여 Aspose가 어떻게 처리하는지 확인하세요.
- `result.Regions`를 살펴보아 레이아웃을 인식하는 바운딩 박스 데이터를 얻을 수 있습니다.

## 다음에 배울 내용은?

- [스트림에서 이미지 인식을 위한 Aspose 사용 방법 (OCR 이미지 인식)](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [이미지에서 텍스트 추출 – .NET용 Aspose.OCR OCR 최적화](/ocr/english/net/ocr-optimization/)
- [이미지에서 텍스트 추출 – Aspose.OCR로 라인 인식](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}