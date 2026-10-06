---
category: general
date: 2026-02-13
description: C#에서 OCR을 사용하여 이미지 파일에서 텍스트를 추출하고, GPU 처리를 활성화하며, 스캔을 빠르게 텍스트로 변환하는 방법을
  배워보세요.
draft: false
keywords:
- how to use OCR
- extract text from image
- how to extract text
- convert scan to text
- enable gpu processing
language: ko
og_description: C#에서 OCR을 사용하는 방법은? 이 가이드는 이미지 파일에서 텍스트를 추출하고, GPU 처리를 활성화하며, 스캔을
  텍스트로 변환하는 방법을 보여줍니다.
og_title: C#에서 OCR 사용 방법 – GPU로 이미지에서 텍스트 추출
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: C#에서 OCR 사용 방법 – GPU를 이용한 이미지에서 텍스트 추출
url: /ko/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 OCR 사용 방법 – GPU로 이미지에서 텍스트 추출

스캔한 문서에서 텍스트를 손쉽게 추출하는 **OCR 사용 방법**이 궁금하셨나요? 여러분만 그런 것이 아닙니다—개발자들은 항상 “이미지 파일에서 텍스트를 효율적으로 추출하려면 어떻게 해야 할까?”라고 묻습니다. 좋은 소식은 Aspose.OCR을 사용하면 바로 그 작업을 할 수 있으며, 지원되는 하드웨어에서는 **GPU 처리**를 활성화해 눈에 띄는 속도 향상을 얻을 수도 있다는 점입니다.

이 튜토리얼에서는 **OCR 사용 방법**, **이미지에서 텍스트 추출**, **스캔을 텍스트로 변환**하는 전체 흐름을 단계별로 살펴보고, GPU를 사용할 수 없을 때의 대처 방법도 안내합니다. 최종적으로는 인식된 텍스트를 출력하고 GPU가 실제로 사용됐는지 알려주는 C# 콘솔 앱을 바로 실행할 수 있게 됩니다.

## 준비 사항

- .NET 6 SDK 이상 (코드는 .NET Core에서도 동작)  
- Visual Studio 2022 또는 선호하는 편집기  
- Aspose.OCR for .NET 패키지 (NuGet을 통해 제공)  
- 테스트용 고해상도 이미지 파일 (예: `highres_scan.tif`)  

특별한 설정은 필요 없습니다—몇 개의 NuGet 명령만 실행하면 바로 시작할 수 있습니다.

## 1단계: Aspose.OCR 설치 및 프로젝트 준비

우선 OCR 라이브러리를 프로젝트에 추가해야 합니다. 솔루션 폴더에서 터미널을 열고 다음 명령을 실행하세요:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

위 명령은 **OcrDemo**라는 새 콘솔 프로젝트를 만들고 `Aspose.OCR` NuGet 패키지를 추가합니다. 이 라이브러리에는 우리가 사용할 `OcrEngine` 클래스가 포함되어 있습니다.

> **Pro tip:** 전용 GPU가 장착된 머신을 사용한다면 최신 그래픽 드라이버가 설치되어 있는지 확인하세요. 그렇지 않으면 라이브러리가 자동으로 CPU 모드로 전환됩니다.

## 2단계: 전체 OCR 코드 작성

이제 `Program.cs` 파일을 열고 내용을 아래 코드로 교체합니다. 각 줄마다 주석이 달려 있어 *왜* 그렇게 하는지 이해할 수 있습니다.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create an OCR engine and request GPU processing.
            //    If the GPU isn’t present, Aspose.OCR will silently
            //    switch to CPU mode – no crash, no extra code needed.
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                ProcessingMode = OcrProcessingMode.Gpu
            };

            // -------------------------------------------------
            // 2️⃣  Define the path to the image you want to process.
            //    Replace the placeholder with the actual file location.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/highres_scan.tif";

            // -------------------------------------------------
            // 3️⃣  Perform the recognition. The method returns an
            //    OcrResult object that contains the extracted text,
            //    confidence scores, and more.
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // -------------------------------------------------
            // 4️⃣  Report whether the GPU was really used.
            //    This is handy for debugging performance issues.
            // -------------------------------------------------
            Console.WriteLine($"GPU used: {ocrEngine.IsGpuEnabled}");

            // -------------------------------------------------
            // 5️⃣  Output the recognized text to the console.
            //    In a real app you might write this to a file,
            //    a database, or feed it into another workflow.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### 왜 이렇게 동작하나요?

- **ProcessingMode = Gpu**는 엔진에게 먼저 GPU를 시도하도록 지시합니다. 라이브러리는 저수준 CUDA/OpenCL 호출을 추상화하므로 직접 디바이스 컨텍스트를 관리할 필요가 없습니다.  
- **IsGpuEnabled**는 GPU 경로가 성공했는지 여부를 확인하는 불리언 값입니다. `false`가 표시되면 엔진이 자동으로 CPU로 전환된 것이므로 걱정하지 않아도 됩니다.  
- **RecognizeImage**는 모든 핵심 작업을 수행합니다: 이미지를 로드하고 OCR 모델을 실행한 뒤 순수 텍스트 결과를 반환합니다. 특별한 전처리(예: 기울기 보정)가 필요하지 않은 한 비트맵을 직접 처리할 필요가 없습니다.

## 3단계: 애플리케이션 실행 및 결과 확인

컴파일하고 실행합니다:

```bash
dotnet run
```

설정이 올바르게 되어 있으면 다음과 같은 출력이 표시됩니다:

```
GPU used: True
=== Extracted Text ===
This is the first line of the scanned document.
Here is the second line, and so on…
```

GPU를 사용할 수 없는 경우 첫 번째 줄에 `GPU used: False`가 표시되지만, 추출된 텍스트는 여전히 나타납니다—우아한 폴백 덕분입니다.

> **Common question:** *이미지가 TIFF가 아니라 JPEG인 경우는 어떻게 하나요?*  
> `RecognizeImage` 메서드는 .NET `System.Drawing`에서 지원하는 모든 형식(JPEG, PNG, BMP 등)을 받아들입니다. `imagePath`의 파일 확장자를 해당 형식으로 바꾸기만 하면 됩니다.

## 4단계: 선택 – 정확도 향상을 위한 설정 조정

Aspose.OCR은 몇 가지 조정 가능한 옵션을 제공합니다:

| 설정 | 기능 설명 | 사용 시점 |
|------|-----------|-----------|
| `ocrEngine.Language` | 특정 언어 강제 지정 (예: `OcrLanguage.English`) | 문서의 언어를 알고 있을 때 |
| `ocrEngine.PageSegMode` | 페이지를 블록으로 나누는 방식 제어 | 다중 컬럼 레이아웃인 경우 |
| `ocrEngine.DetectOrientation` | 텍스트가 수평이 아닐 때 자동 회전 | 뒤집힌 스캔 이미지가 있을 때 |

`RecognizeImage`를 호출하기 전에 이러한 속성을 설정할 수 있습니다. 예시:

```csharp
ocrEngine.Language = OcrLanguage.English;
ocrEngine.DetectOrientation = true;
```

## 5단계: 흐름 시각화 (Alt 텍스트 포함 이미지)

아래는 **OCR 사용 방법**에 GPU 가속을 선택적으로 적용한 흐름을 간단히 나타낸 다이어그램입니다. 코드를 실행하는 데 필수는 아니지만 전체 과정을 한눈에 파악하는 데 도움이 됩니다.

![Diagram showing how to use OCR with GPU processing](/images/ocr-gpu-flow.png)

*Alt text:* *GPU 처리와 필요 시 CPU 폴백을 강조한 OCR 사용 흐름 다이어그램.*

## 엣지 케이스 및 문제 해결

1. **GPU 메모리 부족** – 매우 큰 이미지는 GPU 메모리를 초과할 수 있습니다. 이 경우 라이브러리가 자동으로 CPU로 전환합니다. 메모리 사용량을 낮추려면 이미지를 미리 축소하세요.  
2. **지원되지 않는 이미지 형식** – `RecognizeImage`가 *NotSupportedException*을 발생시키면 파일 확장자를 확인하고 이미지가 손상되지 않았는지 점검하세요. PNG로 변환하면 대부분 해결됩니다.  
3. **낮은 신뢰도 점수** – OCR 결과에 읽을 수 없는 문자가 많이 포함된 경우, 전처리(이진화, 노이즈 제거)를 수행하거나 고해상도 스캔으로 교체해 보세요.  

## 정리: 우리가 이룬 것

우리는 **C# 콘솔 앱에서 OCR 사용 방법**을 다루었고, **이미지 파일에서 텍스트 추출**과 **GPU 처리를 활성화**해 속도를 높이는 방법을 시연했습니다. 이제 **스캔을 텍스트로 변환**하고 GPU 사용 여부를 확인하며, 엣지 케이스에 대비해 몇 가지 설정을 조정할 수 있습니다.

### 다음 단계

- 추출된 텍스트를 **검색 인덱스**(예: Elasticsearch)에 넣어 스캔한 PDF를 검색 가능하게 만들기.  
- **배치 처리**를 실험해 보세요—폴더에 있는 여러 이미지에 대해 반복 실행하고 각 결과를 `.txt` 파일로 저장하기.  
- OCR 결과를 **번역 API**와 결합해 스캔한 외국어 문서를 자동으로 번역하기.  

궁금한 점이 있으면 댓글로 남겨 주세요. 즐거운 코딩 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}