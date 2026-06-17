---
category: general
date: 2026-04-01
description: GPU 디바이스 ID를 설정하고 Aspose OCR에서 GPU 가속을 활성화하여 PNG 파일에서 텍스트를 빠르게 인식하는 방법을
  배웁니다. 단계별 C# 가이드.
draft: false
keywords:
- recognize text from png
- set gpu device id
- Aspose OCR GPU
- batch OCR C#
- OCR performance tips
language: ko
og_description: GPU 장치 ID를 설정하여 PNG 파일에서 텍스트를 빠르게 인식하세요. Aspose OCR로 GPU 가속을 활성화하는
  전체 C# 가이드를 따라보세요.
og_title: PNG에서 텍스트 인식 – GPU 가속 Aspose OCR 튜토리얼
tags:
- C#
- OCR
- GPU
- Aspose
title: Aspose OCR로 PNG에서 텍스트 인식 – GPU 가속 배치 데모
url: /ko/net/ocr-optimization/recognize-text-from-png-with-aspose-ocr-gpu-accelerated-batc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# png에서 텍스트 인식 – 전체 C# GPU 가속 배치 튜토리얼

png 이미지에서 텍스트를 **인식**해야 했지만 과정이 너무 느리다고 느낀 적이 있나요? 당신만 그런 것이 아닙니다. 대부분의 개발자는 간단한 OCR 호출로 시작하지만, 폴더에 수십 개의 스크린샷이 있으면 콘솔이 달팽이처럼 느리게 움직이는 것을 보게 됩니다.  

좋은 소식은? Aspose OCR이 무거운 작업을 그래픽 카드에 맡길 수 있으며, 몇 줄만으로 **set gpu device id**를 설정해 원하는 GPU를 선택할 수 있습니다. 이 가이드에서는 폴더의 모든 PNG를 가져오고, GPU 가속을 켜며, 첫 번째 GPU를 선택하고, 각 파일의 문자 수를 출력하는 완전한 실행 가능한 예제를 단계별로 살펴보겠습니다.

끝까지 읽으면 .NET 프로젝트에 바로 넣어 사용할 수 있는 독립형 프로그램을 얻게 되며, GPU를 활성화하는 이유, 엣지 케이스를 처리하는 방법, 성능을 더욱 향상시키기 위한 조정 포인트를 이해하게 될 것입니다.

## 필요 사항

- **.NET 6.0** 또는 그 이후 버전 (.NET Core에서도 컴파일됩니다).  
- **Aspose.OCR** NuGet 패키지 – `dotnet add package Aspose.OCR` 명령으로 설치합니다.  
- CUDA 호환 GPU가 장착된 머신 (보통 NVIDIA) 및 적절한 드라이버.  
- 처리하려는 **PNG** 이미지가 들어 있는 폴더.  

위 내용이 익숙하지 않더라도 걱정하지 마세요. 아래 단계에는 필요한 정확한 명령이 포함되어 있으며, GPU가 없을 때의 대처 방법도 설명합니다.

## 단계 1: OCR 엔진 초기화 및 GPU 가속 활성화  

먼저 해야 할 일은 `OcrEngine` 인스턴스를 생성하고 GPU 지원을 켜는 것입니다. 이 플래그는 Aspose에게 내부에서 네이티브 CUDA 라이브러리를 사용하도록 지시합니다.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU acceleration – huge speed boost for large batches
        ocrEngine.UseGpuAcceleration = true;
```

**왜 중요한가:** `UseGpuAcceleration`를 사용하지 않으면 각 이미지를 CPU에서 처리하게 되며, 특히 고해상도 PNG의 경우 속도가 수십 배 느려질 수 있습니다. 이 플래그를 활성화하면 이후에 특정 GPU 디바이스를 지정할 준비도 됩니다.

## 단계 2: GPU 디바이스 ID 설정 (선택 사항이지만 권장됨)  

워크스테이션에 GPU가 여러 대 있는 경우 사용할 GPU를 선택할 수 있습니다. 디바이스 ID는 **0**부터 시작하므로 `0`은 첫 번째 GPU, `1`은 두 번째 GPU를 의미합니다.

```csharp
        // Optional: Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id
```

**프로 팁:** 공유 서버에서 실행할 때 GPU 디바이스 ID를 명시적으로 설정하면 다른 프로세스의 리소스를 빼앗는 일을 방지할 수 있습니다. 이 줄을 생략하면 Aspose가 기본 디바이스를 선택하는데, 단일 GPU 환경에서는 보통 문제되지 않습니다.

## 단계 3: 배치 폴더에서 모든 PNG 파일 수집  

다음으로 OCR을 수행할 모든 PNG 파일을 찾아야 합니다. `Directory.GetFiles` 메서드가 이 작업을 수행합니다.

```csharp
        // Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // <-- replace with your path
            "*.png",                  // only PNG files
            System.IO.SearchOption.TopDirectoryOnly);
```

**엣지 케이스:** 폴더가 비어 있으면 `imageFiles`는 빈 배열이 됩니다. 이후 친절한 메시지로 처리할 것입니다.

## 단계 4: 각 이미지 처리 및 인식된 문자 수 출력  

이제 핵심 루프입니다. 각 PNG에 대해 `Recognize`를 호출하고, 파일 이름과 추출된 텍스트의 길이를 출력합니다.

```csharp
        // Verify we actually found files
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

**출력 예시:**  
```
invoice1.png → 342 chars
receipt_2023.png → 127 chars
screenshot.png → 0 chars
```

이미지에 텍스트가 없으면 카운트는 `0`이 됩니다. 순수 그래픽 스크린샷에서는 이것이 정상입니다.

## 단계 5: 프로그램 실행 및 GPU 사용 확인  

`dotnet build`로 파일을 컴파일하고 `dotnet run`으로 실행합니다. 콘솔이 스크롤되는 동안 GPU 모니터링 도구(NVIDIA Smi 등)를 열어 각 이미지마다 GPU 사용량이 짧게 급증하는지 확인할 수 있습니다. 활동이 보이지 않으면 다음을 다시 확인하세요:

1. CUDA 드라이버가 설치되어 있는지.  
2. `UseGpuAcceleration`가 `true`로 설정되어 있는지.  
3. 올바른 `GpuDeviceId`가 실제 GPU와 일치하는지.  

GPU를 사용할 수 없으면 Aspose가 자동으로 CPU로 전환하지만, 속도 이점을 잃게 됩니다.

## 일반적인 변형 및 팁

| Situation | What to Change |
|-----------|----------------|
| **다른 이미지 형식** (예: JPEG) | 검색 패턴을 `*.jpg` 또는 `*.*` 로 변경하면 Aspose가 여전히 텍스트를 인식합니다. |
| **배치 크기가 매우 큼** (수천 개 파일) | 메모리 압박을 피하기 위해 청크 단위로 처리합니다: `imageFiles`를 작은 배열로 나눕니다. |
| **텍스트 자체가 필요하고 길이만은 원하지 않을 때** | `WriteLine`에서 `ocrResult.Text.Length`를 `ocrResult.Text` 로 교체합니다. |
| **헤드리스 서버에서 실행** | 서버에 GPU 드라이버가 설치되어 있는지 확인하고, 없으면 `UseGpuAcceleration = false` 로 설정해 불필요한 오류를 방지합니다. |
| **GPU가 여러 대 있어 부하를 분산하고 싶을 때** | `foreach` 내부에서 `ocrEngine.GpuDeviceId = i % gpuCount` 로 루프를 돌려 디바이스를 순환시킵니다. |

## 예상 출력 및 검증  

모든 것이 정상적으로 동작하면 콘솔에 각 파일 이름과 문자 수가 앞서 보여진 대로 출력됩니다. 실제 OCR 결과를 다시 확인하려면 텍스트를 일시적으로 출력할 수 있습니다:

```csharp
Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text}");
```

대량 배치에서는 해당 줄을 제거하거나 주석 처리하는 것을 기억하세요; 수천 줄을 출력하면 터미널이 넘칠 수 있습니다.

## 전체 작업 예제 (복사‑붙여넣기 준비)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpuAcceleration = true;

        // Step 2: (Optional) Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id

        // Step 3: Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // replace with your folder path
            "*.png",
            System.IO.SearchOption.TopDirectoryOnly);

        // Guard clause if no files are found
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Step 4: Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

`GpuBatchDemo.cs` 파일로 저장하고 `dotnet add package Aspose.OCR`를 실행한 뒤 `dotnet run`을 실행하세요. GPU 가속 덕분에 각 PNG에 대한 문자 수가 거의 즉시 표시될 것입니다.

## 결론  

이제 GPU 가속을 활성화하고 Aspose OCR에서 **set gpu device id**를 명시적으로 설정하여 **png 파일에서 텍스트를 인식**하는 효율적인 방법을 알게 되었습니다. 완전한 복사‑붙여넣기 프로그램은 폴더 탐색, 엣지 케이스 검사 등을 처리하고 OCR 성능에 대한 즉각적인 피드백을 제공합니다.

다음 단계는? 비동기 처리가 필요하면 `Recognize` 호출을 `ocrEngine.RecognizeAsync` 로 교체해 보세요. 또는 Aspose가 제공하는 다양한 이미지 전처리 옵션(예: 이진화)을 실험해 볼 수 있습니다. OCR 결과를 데이터베이스나 검색 인덱스로 파이프하여 전체 텍스트 검색 솔루션을 구축할 수도 있습니다.

다중 페이지 PDF 처리에 대한 질문이 있거나 Aspose OCR을 Tesseract와 비교하고 싶으신가요? 댓글을 남기거나 **batch OCR C#**, **OCR performance tips**, **GPU‑driven image processing**에 관한 다른 튜토리얼을 확인해 보세요. 즐거운 코딩 되세요!  

![GPU 가속을 사용한 png에서 텍스트 인식 – PNG 파일의 인식된 문자 수를 보여주는 콘솔 출력](image-placeholder.png "png 텍스트 인식 출력 예시")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}