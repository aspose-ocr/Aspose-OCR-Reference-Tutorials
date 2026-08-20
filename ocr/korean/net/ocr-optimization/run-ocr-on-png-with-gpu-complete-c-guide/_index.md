---
category: general
date: 2026-01-02
description: Aspose OCR와 GPU 지원을 사용하여 PNG에서 OCR을 빠르게 실행합니다. 이미지에서 텍스트를 인식하고, 이미지에서
  텍스트를 추출하며, GPU 메모리 제한을 설정하는 방법을 배워보세요.
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: ko
og_description: PNG에서 OCR을 효율적으로 수행하려면 Aspose OCR과 GPU 가속을 활용하십시오. 이 튜토리얼에서는 이미지에서
  텍스트를 인식하고, 이미지에서 텍스트를 추출하며, GPU 메모리 사용량을 제어하는 방법을 보여줍니다.
og_title: GPU로 PNG에서 OCR 실행 – 완전 C# 가이드
tags:
- OCR
- C#
- GPU
title: GPU로 PNG에서 OCR 실행 – 완전한 C# 가이드
url: /ko/net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GPU를 이용한 PNG OCR 실행 – 완전한 C# 가이드

고해상도 PNG 파일에 **OCR을 실행**해야 하는데 성능이 걸리는 경험이 있나요? 여러분만 그런 것이 아닙니다. 실제 파이프라인에서는 단일 고해상도 PNG가 CPU 전용 OCR 엔진을 병목 현상으로 만들고, 빠르게 처리돼야 할 작업이 1분 이상 걸리기도 합니다.  

좋은 소식은 Aspose OCR이 GPU 확장을 제공한다는 점입니다. 이를 통해 **이미지에서 텍스트 인식**을 훨씬 짧은 시간에 수행할 수 있습니다. 이번 튜토리얼에서는 C#으로 **PNG에 OCR을 실행**하는 방법, **이미지에서 텍스트 추출**하는 방법, 그리고 **GPU 메모리 제한을 설정**하는 방법을 단계별로 살펴보겠습니다.

각 단계마다 “어떻게”와 “왜”를 함께 설명하므로, 단순히 복사‑붙여넣기 스니펫이 아니라 탄탄한 개념 모델을 얻을 수 있습니다.

## 배울 내용

- Aspose OCR의 GPU 지원을 사용하기 위한 전제 조건.  
- PNG를 `Bitmap`으로 로드하고 OCR 엔진에 전달하는 방법.  
- 최적 성능을 위한 `GpuDevice`와 `GpuMemoryLimitMb` 구성 방법.  
- **이미지에서 텍스트 인식**하고 평문 결과를 가져오는 방법.  
- 메모리 부족 GPU 또는 다중 페이지 PNG와 같은 일반적인 엣지 케이스 처리 팁.  

이 가이드를 마치면 **GPU 속도로 PNG에 OCR을 실행**하고 OCR 작업의 메모리 사용량을 자신 있게 제어할 수 있게 됩니다.

![GPU 가속을 이용한 PNG OCR 실행을 보여주는 다이어그램](run-ocr-on-png-diagram.png "GPU 가속 PNG OCR 예시")

## 전제 조건

시작하기 전에 다음을 준비하세요:

1. .NET 6.0 이상 (코드는 .NET Core와 .NET Framework에서도 동작합니다).  
2. CUDA를 지원하는 NVIDIA GPU (예제에서는 디바이스 인덱스 0을 사용합니다).  
3. Aspose.OCR NuGet 패키지와 GPU 확장(`Aspose.OCR.Extensions`).  
4. 프로젝트에서 참조할 수 있는 폴더에 위치한 샘플 PNG(`input.png`).  

이 중 익숙하지 않은 부분이 있더라도 걱정 마세요—관련 대안을 별도로 안내합니다.

---

## Step 1 – Aspose OCR 및 GPU 확장 설치

먼저 해야 할 일입니다. 올바른 라이브러리가 없으면 나머지 코드는 컴파일되지 않습니다.

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

`Aspose.OCR.Extensions` 패키지는 GPU 가속에 필요한 네이티브 CUDA 바이너리를 자동으로 포함합니다.  
*팁:* GPU가 없는 머신에서도 프로젝트를 컴파일할 수 있습니다. 나중에 `PreferGpu = false` 로 설정하면 됩니다.

---

## Step 2 – 처리할 PNG 로드

이제 **PNG에 OCR을 실행**하기 위해 `Bitmap`으로 로드합니다. 이 단계는 간단하지만 한 가지 주의할 점이 있습니다: `Bitmap`은 파일 경로를 기대하므로 실행 파일 기준 상대 경로가 올바른지 확인하세요.

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

PNG가 비정상적으로 크다면(예: 한 변이 5000 px 이상) 먼저 다운스케일하여 GPU 메모리 소모를 방지하는 것이 좋습니다. 이때 **GPU 메모리 제한 설정** 옵션이 유용하게 작동합니다.

---

## Step 3 – GPU 사용을 위한 OCR 엔진 생성 및 구성

튜토리얼의 핵심 부분입니다. OCR 엔진을 **이미지에서 텍스트 인식**하도록 GPU와 함께 구성합니다. 핵심 프로퍼티 두 가지:

- `GpuDevice` – 사용할 CUDA 디바이스 선택.  
- `GpuMemoryLimitMb` – 엔진이 할당할 수 있는 GPU 메모리 상한.

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**메모리 제한을 설정하는 이유**는 일부 GPU가 디스플레이와 메모리를 공유하거나 동시에 여러 작업을 수행하기 때문입니다. 할당량을 제한하면 특히 다수의 PNG를 병렬 처리할 때 메모리 부족 오류를 방지할 수 있습니다.

---

## Step 4 – 인식 옵션 정의 (언어 및 GPU 선호)

`RecognitionOptions` 객체는 엔진에 어떤 언어를 인식할지와 작은 이미지에도 **GPU 선호** 여부를 알려줍니다. 대부분의 영어 문서에는 이 설정만으로 충분하지만, `Language.English`를 다른 지원 언어로 교체하면 됩니다.

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

영어가 아닌 언어에서 **이미지에서 텍스트 추출**이 필요하면 `Language` 열거형을 해당 언어로 바꾸면 됩니다. 라이브러리는 수십 개의 언어를 기본적으로 지원합니다.

---

## Step 5 – OCR 실행 및 결과 가져오기

모든 설정이 끝났다면, 이제 한 줄의 코드로 **PNG에 OCR을 실행**하고 풍부한 결과 객체를 반환합니다.

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

`OcrResult`에는 평문(`ocrResult.Text`)뿐 아니라 신뢰도 점수, 바운딩 박스, 하이라이트된 원본 이미지 등이 포함됩니다—디버깅이나 시각화가 필요할 때 유용합니다.

**예상 출력**(샘플 PNG에 “Hello World”가 적힌 경우):

```
=== OCR Output ===
Hello World
```

텍스트가 깨져 보이면 PNG가 손상됐는지, GPU 메모리 제한이 이미지 크기에 비해 너무 낮지는 않은지 확인하세요.

---

## Step 6 – 엣지 케이스 및 모범 사례 팁

### 메모리 부족 GPU

`CudaException: out of memory`와 같은 예외가 발생하면 `GpuMemoryLimitMb`를 낮추거나 PNG를 타일로 나누어 처리하세요. 타일링은 `Graphics.DrawImage`와 `Bitmap` 복제본을 이용해 구현할 수 있습니다.

### 배치 처리 시 다수 PNG

폴더에 있는 PNG를 일괄 처리할 때는 동일한 `OcrEngine` 인스턴스를 재사용하세요—한 번 초기화하면 GPU 컨텍스트 전환을 줄일 수 있습니다.

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### CPU로 폴백

GPU가 없을 경우 `PreferGpu = false` 로 설정하면 됩니다. 엔진이 자동으로 CPU로 전환되며 코드 변경이 필요 없습니다.

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## 전체 작업 예제

아래는 새 콘솔 프로젝트에 복사‑붙여넣기 할 수 있는 완전한 프로그램입니다. 앞서 설명한 모든 단계와 몇 가지 안전 검증이 포함되어 있습니다.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

파일을 `Program.cs` 로 저장하고 `dotnet run` 을 실행하면 추출된 텍스트가 콘솔에 출력됩니다.

---

## 결론

이번 글에서는 Aspose OCR의 GPU 확장을 활용해 **PNG에 OCR을 실행**하고, **이미지에서 텍스트 인식** 및 **이미지에서 텍스트 추출**을 수행하면서 **GPU 메모리 제한을 설정**하는 방법을 살펴보았습니다. `GpuDevice`와 `GpuMemoryLimitMb`를 적절히 구성하면 저사양 GPU에서도 애플리케이션을 빠르고 안정적으로 운영할 수 있습니다.

다음 단계로 고려해볼 수 있는 내용:

- 다른 언어 실험 (`Language.French`, `Language.Spanish` 등).  
- OCR 단계를 더 큰 문서 처리 파이프라인에 통합.  
- 추출된 텍스트에 맞춤법 검사나 엔터티 추출 같은 후처리 추가.  

코드뿐 아니라 각 설정이 왜 중요한지 이해하는 것이 핵심입니다. **GPU 메모리 제한을 설정**하는 시점과 CPU 폴백 시점을 정확히 알면, 확장 가능한 OCR 솔루션을 만들 수 있습니다.

특정 PNG 크기, 다중 페이지 TIFF, GPU 오류 해결 등에 대한 질문이 있으면 아래 댓글로 남겨 주세요. 즐거운 코딩 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}