---
category: general
date: 2026-02-20
description: C#에서 Aspose.OCR을 사용해 이미지 OCR을 전처리합니다. 중앙값 필터 적용 방법, 이미지 노이즈 감소 및 텍스트
  이미지를 효율적으로 추출하는 방법을 배워보세요.
draft: false
keywords:
- preprocess image OCR
- apply median filter
- extract text image
- reduce image noise
- c# ocr example
language: ko
og_description: Aspose.OCR로 이미지 OCR 전처리하기. 이 튜토리얼에서는 중앙값 필터를 적용하고 이미지 노이즈를 줄이며 C#를
  사용해 텍스트 이미지를 추출하는 방법을 보여줍니다.
og_title: C#에서 이미지 OCR 전처리 – 완전 가이드
tags:
- OCR
- C#
- Image Processing
title: C#에서 이미지 OCR 전처리 – 완전한 단계별 가이드
url: /ko/net/ocr-optimization/preprocess-image-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 이미지 OCR 전처리 – 완전 단계별 가이드

스캔한 사진에서 텍스트가 깨져서 나오는 경우 **이미지 OCR 전처리**가 필요했던 적이 있나요? 당신만 그런 것이 아닙니다. 영수증, 신분증, 손글씨 메모와 같은 실제 프로젝트에서는 원본 이미지가 바로 인식될 준비가 되어 있는 경우는 드뭅니다. 좋은 소식은? 몇 가지 간단한 전처리 단계만으로 정확도를 크게 높일 수 있으며, 이를 모두 C#와 Aspose.OCR로 구현할 수 있다는 것입니다.

이 튜토리얼에서는 **median filter 적용**, **이미지 노이즈 감소**, 그리고 최종적으로 **텍스트 이미지 추출**을 수행하여 깨끗하고 읽기 쉬운 결과를 얻는 실습 예제를 단계별로 살펴보겠습니다. 끝까지 따라오시면 .NET 솔루션에 바로 넣어 사용할 수 있는 완전 실행 가능한 C# 콘솔 앱을 얻게 됩니다. 애매한 설명이 아니라 필요한 코드와 각 라인 뒤에 숨은 “왜”를 제공합니다.

---

## 필요 사항

- **Aspose.OCR for .NET** (작성 시점 최신 버전, 23.12). NuGet을 통해 설치할 수 있습니다: `Install-Package Aspose.OCR`.
- .NET 6.0 이상 (예제는 콘솔 앱을 사용하지만 동일한 로직을 ASP.NET, WPF 등에서도 사용할 수 있습니다).
- 정리할 샘플 이미지—예: `skewed_photo.jpg`.  
- 약간의 C# 경험; 개념은 주니어 개발자도 이해하기 쉬운 수준입니다.

> **Pro tip:** 기업용 컴퓨터를 사용 중이라면 NuGet 피드가 외부 패키지를 허용하도록 설정되어 있는지 확인하세요. 그렇지 않으면 설치가 실패합니다.

## Step 1 – OCR 엔진 인스턴스 생성  

먼저 `OcrEngine`을 생성합니다. 이 객체는 인식 설정을 보관하며 이후 전처리된 비트맵을 처리합니다.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;   // For Image handling
using System;

class PreprocessExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is the core component that will read text.
        OcrEngine ocrEngine = new OcrEngine();

        // ... we’ll continue with loading and preprocessing the image below.
```

**Why?**  
엔진을 한 번 생성하고 여러 이미지에 재사용하면 오버헤드가 감소합니다. 또한 전체 파이프라인을 다시 구축하지 않고도 언어나 인식 모드를 나중에 조정할 수 있습니다.

## Step 2 – 원본 이미지 로드  

`System.Drawing.Image` 객체를 사용해 원본 파일을 가리켜야 합니다. 실제 프로젝트에서는 스트림을 받을 수도 있지만, 여기서는 명확성을 위해 디스크에서 읽어옵니다.

```csharp
        // Load the image that requires preprocessing.
        Image sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_photo.jpg");
```

> **Note:** `YOUR_DIRECTORY`를 실제 폴더 경로로 교체하세요. 파일을 찾지 못하면 `FileNotFoundException`이 발생합니다—우아한 오류 처리를 원한다면 이를 잡아야 합니다.

## Step 3 – 이미지 기울기 보정 및 회전  

대부분의 스캔 문서는 약간 기울어져 있습니다. `DeskewAndRotate` 필터는 기울기 각도를 자동으로 감지하고 이미지를 바로 세워 회전합니다.

```csharp
        // Correct orientation – crucial for accurate OCR.
        Image processedImage = sourceImage.Apply(Preprocess.DeskewAndRotate());
```

**Why does this matter?**  
OCR 엔진은 텍스트 라인이 수평이라고 가정합니다. 2도 정도의 기울기만 있어도 인식 정확도가 15‑20 % 감소할 수 있습니다. 기울기 보정은 큰 효과를 얻을 수 있는 가장 저렴한 방법입니다.

## Step 4 – 이미지 노이즈 감소를 위한 Median Filter 적용  

노이즈는 특히 저조도 사진에서 점이나 무작위 픽셀 형태로 나타납니다. Median filter는 가장자리를 보존하면서 이러한 노이즈를 부드럽게 제거합니다. 이는 OCR 전에 정확히 필요한 작업입니다.

```csharp
        // Reduce noise – radius of 2 is a good balance for most photos.
        processedImage = processedImage.Apply(Preprocess.MedianFilter(radius: 2));
```

**Why a median filter?**  
평균(Mean) 필터와 달리, median filter는 각 픽셀을 주변 픽셀들의 중앙값으로 교체합니다. 따라서 고립된 노이즈는 제거되면서 텍스트 획은 흐려지지 않습니다—이는 **이미지 노이즈 감소**를 위한 고전적인 기법입니다.

## Step 5 – 스트레칭을 통한 대비 향상  

노이즈를 제거한 뒤 다음 단계는 텍스트와 배경 사이의 차이를 높이는 것입니다. 대비 스트레칭은 픽셀 강도를 0‑255 전체 범위에 걸쳐 퍼뜨립니다.

```csharp
        // Stretch contrast to make dark text pop against a light background.
        processedImage = processedImage.Apply(Preprocess.ContrastStretch());
```

**Why stretch?**  
OCR 엔진은 명확한 전경‑배경 구분에 의존합니다. 이미지가 흐리면 엔진이 텍스트를 배경으로 오인할 수 있습니다. 대비 스트레칭은 수동 임계값 설정 없이 이를 해결합니다.

## Step 6 – 전처리된 이미지에 OCR 수행  

이미지가 바로 서고, 깨끗하며, 고대비가 되었다면 이제 OCR 엔진에 전달합니다.

```csharp
        // Recognize the text from the cleaned image.
        string extractedText = ocrEngine.Recognize(processedImage);
```

**What you get:**  
`extractedText`에는 Aspose.OCR이 감지한 원시 Unicode 문자열이 들어 있습니다. 필요에 따라 추가로 후처리(트림, 정규식 등)할 수 있습니다.

## Step 7 – 인식된 텍스트 출력  

마지막으로 결과를 콘솔이나 파일에 기록합니다—워크플로에 맞는 방법을 선택하세요.

```csharp
        // Show the result in the console.
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

### 예상 출력

`skewed_photo.jpg`에 “Hello World”라는 문구가 포함되어 있다면 다음과 같은 출력이 나타납니다:

```
=== Extracted Text ===
Hello World
```

이미지가 여전히 노이즈가 많다면 깨진 문자들이 보일 수 있습니다—Step 4로 돌아가 median filter 반경을 늘리거나 `GaussianBlur`와 같은 추가 필터를 실험해 보세요.

## 전체 작동 예제 (복사‑붙여넣기 가능)

아래는 전체 프로그램 코드이며 바로 컴파일할 수 있습니다. 누락된 부분은 없으며 파일 경로만 교체하면 됩니다.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;
using System;

class PreprocessExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image that needs preprocessing
        Image sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_photo.jpg");

        // Step 3: Deskew and rotate the image to correct orientation
        Image processedImage = sourceImage.Apply(Preprocess.DeskewAndRotate());

        // Step 4: Reduce noise with a median filter (radius = 2)
        processedImage = processedImage.Apply(Preprocess.MedianFilter(radius: 2));

        // Step 5: Enhance contrast using contrast stretching
        processedImage = processedImage.Apply(Preprocess.ContrastStretch());

        // Step 6: Perform OCR on the preprocessed image
        string extractedText = ocrEngine.Recognize(processedImage);

        // Step 7: Output the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

> **Edge case tip:** 이미지에 컬러 텍스트가 컬러 배경 위에 있는 경우 `ContrastStretch` 적용 전에 그레이스케일로 변환하는 것을 고려하세요. 파이프라인에서 `Preprocess.Grayscale()`을 사용하면 됩니다.

## 일반적인 질문 및 변형  

### 이미지가 뒤집혀 있으면 어떻게 하나요?  
`DeskewAndRotate`는 180도 회전을 자동으로 감지하지만, 기울기 보정 전에 `Preprocess.Rotate(angle: 180)`를 사용해 강제로 회전시킬 수 있습니다.

### median filter를 건너뛸 수 있나요?  
가능하지만 **이미지 노이즈 감소** 효과가 크게 줄어들 가능성이 높습니다. 고해상도 스캔에서는 필터가 필요 없을 수 있지만, 저조도 휴대폰 사진에서는 보통 필수입니다.

### 간단한 `Apply(Preprocess.Binarize())`와는 어떻게 다른가요?  
이진화는 이미지를 순수한 흑백으로 변환해 얇은 글꼴에 거칠게 작용할 수 있습니다. 우리의 접근 방식은 그레이스케일 세부 정보를 유지한 뒤 대비를 스트레칭합니다—다양한 크기의 글꼴에 대해 더 나은 결과를 제공하는 경우가 많습니다.

### **median filter**를 관심 영역에만 적용할 수 있나요?  
Aspose.OCR의 `Apply`는 전체 비트맵에 적용되지만, 먼저 이미지를 잘라내고(`sourceImage.Clone(new Rectangle(...), sourceImage.PixelFormat)`) 해당 서브 이미지에 필터를 적용할 수 있습니다.

## 다음 단계 – 기본 전처리를 넘어  

- **Language Packs:** 프랑스어나 일본어와 같은 문자를 추출해야 한다면 `ocrEngine.Language = Language.French;`와 같이 적절한 언어 모델을 로드하세요.
- **Custom Thresholding:** 매우 낮은 대비 스캔의 경우 median filter 후 `Preprocess.AdaptiveThreshold()`를 실험해 보세요.
- **Batch Processing:** `foreach (string file in Directory.GetFiles(...))` 루프로 전체 단계를 감싸고 각 결과를 `.txt` 파일에 기록합니다.  
- **Performance Tuning:** `OcrEngine` 인스턴스를 하나만 재사용하고 `Bitmap` 버퍼를 미리 할당하여 수천 장의 이미지를 처리할 때 GC 스파이크를 방지합니다.

## 결론  

우리는 C#에서 **이미지 OCR 전처리**를 처음부터 끝까지 수행하는 방법을 보여드렸습니다: 사진 로드, 기울기 보정, **median filter 적용**, 대비 강화, 그리고 마지막으로 Aspose.OCR로 **텍스트 이미지 추출**을 수행합니다. 완전한 코드 스니펫은 어떤 프로젝트에도 바로 삽입할 수 있으며, 각 변환 뒤에 숨은 “왜”를 설명해 주어 자체적인 상황에 맞게 매개변수를 조정할 수 있습니다.

몇 장의 다른 사진으로 실험해 보고, 필터 반경을 조정하면서 인식 정확도가 상승하는 것을 확인해 보세요. 익숙해지면 위에서 언급한 고급 조정을 탐색해 보세요. 그러면 팀 내에서 깨끗한 OCR 파이프라인을 담당하는 핵심 인물이 될 수 있습니다.

코딩 즐겁게 하시고, OCR이 언제나 깨끗하게 읽히길 바랍니다! 

![이미지 OCR 전처리 예시](/images/preprocess-image-ocr.png "이미지 OCR 전처리 – 전후 비교")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}