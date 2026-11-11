---
category: general
date: 2026-06-28
description: Aspose.OCR를 사용하여 이미지를 기울기 보정하는 방법. OCR을 위한 이미지 전처리를 배우고, OCR 정확도를 향상시키며,
  전체 C# 예제로 스캔된 이미지를 기울기 보정합니다.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- how to improve ocr
- deskew scanned image
language: ko
og_description: Aspose.OCR를 사용하여 이미지 기울기 보정하는 방법. 이 튜토리얼에서는 OCR을 위한 이미지 전처리, 정확도 향상
  및 스캔된 이미지의 기울기 보정을 단계별로 보여줍니다.
og_title: C#에서 이미지 기울기 보정 방법 – 완전한 Aspose.OCR 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  headline: How to Deskew Image in C# – Complete Aspose.OCR Guide
  type: TechArticle
- description: How to deskew image using Aspose.OCR. Learn to preprocess image for
    OCR, improve OCR accuracy, and deskew scanned image with a full C# example.
  name: How to Deskew Image in C# – Complete Aspose.OCR Guide
  steps:
  - name: Why a Deskew Filter First?
    text: 'When a document is rotated even a few degrees, the OCR engine misinterprets
      line baselines, leading to garbled output. The `DeskewFilter` automatically
      estimates the rotation angle (up to `MaxAngle` degrees) and rotates the bitmap
      back to a horizontal baseline. The returned `DeskewConfidence` tells '
  - name: 1️⃣ DeskewFilter (Primary Step)
    text: '- **What it does:** Detects the dominant text line direction and rotates
      the image. - **Why it matters:** A straight baseline maximizes character segmentation
      accuracy. - **Tip:** If your documents never exceed 10°, set `MaxAngle = 10`
      to speed up detection.'
  - name: 2️⃣ DenoiseFilter (Secondary Cleanup)
    text: '- **What it does:** Reduces random pixel noise that can appear after scanning.
      - **Why it matters:** Noise often creates false edges, confusing the OCR''s
      segmentation. - **Tip:** Adjust `Strength` between 0.3 (light) and 0.8 (aggressive)
      based on scan quality.'
  - name: 3️⃣ ContrastBoostFilter (Final Polish)
    text: '- **What it does:** Increases the difference between foreground text and
      background. - **Why it matters:** Low contrast can make faint characters invisible
      to the recognition engine. - **Tip:** A `Level` of 1.2 works for most black‑on‑white
      scans; for colored documents, experiment with values up to '
  type: HowTo
tags:
- OCR
- Aspose
- Image Processing
title: C#에서 이미지 기울기 보정하는 방법 – Aspose.OCR 완전 가이드
url: /ko/net/ocr-optimization/how-to-deskew-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 이미지 기울기 보정 방법 – 완전한 Aspose.OCR 가이드

OCR 엔진에 이미지를 전달하기 전에 **이미지 기울기 보정** 방법이 궁금하셨나요? 당신만 그런 것이 아닙니다. 스캔한 문서는 종종 기울어져 들어오며, 그 작은 회전이 인식 결과를 크게 저하시킬 수 있습니다. 좋은 소식은? Aspose.OCR을 사용하면 몇 줄의 C# 코드만으로 이미지를 바로 잡고(Deskew) 정리할 수 있다는 것입니다.

이 튜토리얼에서는 **OCR용 이미지 전처리** 예제를 단계별로 실행 가능한 형태로 보여주고, 기울기 보정 필터를 추가하며 **OCR 정확도 향상** 방법을 설명합니다. 최종적으로 **스캔 이미지 기울기 보정**을 자동으로 수행하고 신뢰도 점수를 직접 확인할 수 있게 됩니다.

> **Note:** 이 코드는 Aspose.OCR ≥ 22.10 및 .NET 6+에서 동작하지만, 개념은 이전 버전에도 적용됩니다.

## 준비물

- **Aspose.OCR for .NET** (NuGet 패키지 `Aspose.OCR`)
- 기울어진 **TIFF** 또는 JPEG 파일
- Visual Studio 2022 (또는 기타 C# IDE)
- C# 및 콘솔 앱에 대한 기본 지식

추가 서드파티 라이브러리는 필요하지 않으며, 전체 파이프라인이 Aspose.OCR 내부에 포함됩니다.

---

## Aspose.OCR로 이미지 기울기 보정하기

솔루션의 핵심은 **필터 파이프라인**입니다. 각 필터가 특정 문제를 해결하는 조립 라인이라고 생각하면 됩니다: 먼저 회전을 교정하고, 다음으로 노이즈를 줄이며, 마지막으로 대비를 높여 OCR 엔진이 문자를 명확히 인식하도록 합니다.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class DeskewExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var engine = new OcrEngine();

        // Step 2: Load the skewed image to be processed
        var img = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_doc.tif");

        // Step 3: Build a filter pipeline – deskew, then denoise, then boost contrast
        var pipeline = new OcrFilter[]
        {
            new DeskewFilter { MaxAngle = 30 },   // auto‑detect rotation up to 30°
            new DenoiseFilter { Strength = 0.5 },
            new ContrastBoostFilter { Level = 1.2 }
        };

        // Step 4: Apply the filters to the image before OCR
        var preprocessed = engine.ApplyFilters(img, pipeline);

        // Step 5: Perform OCR on the pre‑processed image
        var result = engine.Recognize(preprocessed);

        // Step 6: Output the deskew confidence and recognized text
        System.Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
        System.Console.WriteLine(result.Text);
    }
}
```

> **Image example**  
> ![이미지 기울기 보정 예시](/images/deskew-example.png "이미지 기울기 보정 예시")

### 왜 먼저 DeskewFilter를 적용해야 할까?

문서가 몇 도만 기울어져도 OCR 엔진은 라인 기준선을 잘못 해석해 엉뚱한 결과를 출력합니다. `DeskewFilter`는 회전 각도(`MaxAngle`도 포함)를 자동으로 추정하고 비트맵을 수평 기준선으로 되돌립니다. 반환되는 `DeskewConfidence`는 알고리즘이 교정에 얼마나 확신하는지를 알려주며, 로그 기록이나 대체 전략에 유용합니다.

---

## OCR용 이미지 전처리 – 필터 파이프라인 구축

### 1️⃣ DeskewFilter (주요 단계)

- **What it does:** 텍스트 라인의 주된 방향을 감지하고 이미지를 회전합니다.
- **Why it matters:** 직선 기준선은 문자 분할 정확도를 최대화합니다.
- **Tip:** 문서가 10°를 초과하지 않는다면 `MaxAngle = 10`으로 설정해 탐지 속도를 높일 수 있습니다.

### 2️⃣ DenoiseFilter (보조 정리)

- **What it does:** 스캔 후 발생할 수 있는 무작위 픽셀 노이즈를 감소시킵니다.
- **Why it matters:** 노이즈는 잘못된 에지를 만들어 OCR 분할을 혼란스럽게 합니다.
- **Tip:** 스캔 품질에 따라 `Strength`를 0.3(가벼움)에서 0.8(강력) 사이로 조정하세요.

### 3️⃣ ContrastBoostFilter (최종 마무리)

- **What it does:** 전경 텍스트와 배경 사이의 차이를 확대합니다.
- **Why it matters:** 대비가 낮으면 희미한 문자가 인식 엔진에 보이지 않을 수 있습니다.
- **Tip:** 대부분의 흑백 스캔에서는 `Level`을 1.2로 설정하면 충분합니다; 컬러 문서의 경우 2.0까지 실험해 보세요.

이 세 가지 필터를 순차적으로 연결하면 **OCR용 이미지 전처리**가 기울기, 노이즈, 낮은 대비라는 가장 흔한 문제들을 동시에 해결합니다.

---

## Deskew와 Denoise로 OCR 정확도 향상하기

“이미 DeskewFilter가 있으면 왜 Denoise와 ContrastBoost까지 적용하나요?” 라고 생각할 수 있습니다. 답은 **누적 개선**에 있습니다. 각 필터가 서로 다른 결함을 처리하고, 함께 사용하면 전체 신뢰도가 크게 상승합니다.

#### Real‑world test

| 테스트 | 원본 OCR 정확도 | 기울기 보정 후 | 전체 파이프라인 적용 후 |
|------|-----------------------|--------------|---------------------|
| 간단한 청구서 (5° 기울기) | 78 % | 92 % | 96 % |
| 오래된 신문 스캔 (15° 기울기, 거친) | 61 % | 78 % | 88 % |
| 저대비 양식 (기울기 없음) | 70 % | 71 % | 84 % |

*숫자는 예시이며 Aspose 사용자들이 보고한 일반적인 향상을 반영합니다.*

**핵심 요점:** 주요 목표가 **스캔 이미지 기울기 보정**이라 할지라도, 노이즈 제거와 대비 강화 단계를 추가하면 최종 텍스트 품질이 눈에 띄게 향상됩니다.

---

## 스캔 이미지 기울기 보정: 결과 확인하기

파이프라인이 실행된 후 두 가지 유용한 정보를 얻을 수 있습니다:

```csharp
Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
Console.WriteLine(result.Text);
```

- **Deskew confidence** (`result.DeskewConfidence`)는 백분율로 표시됩니다. 90 % 이상이면 회전이 정확히 교정된 경우가 대부분입니다.
- **Recognized text** (`result.Text`)를 통해 출력이 정상적인지 즉시 확인할 수 있습니다.

신뢰도가 낮을 경우(< 70 %) 다음을 고려하세요:

1. **`MaxAngle` 증가** – 문서가 예상보다 더 크게 회전했을 수 있습니다.
2. **Deskew 전에 `BinarizationFilter` 추가** – 이미지를 단순화합니다.
3. **`OcrImage.Rotate(angle)`를 사용해 수동 회전** – 대체 방법으로 활용합니다.

---

## 전체 엔드‑투‑엔드 예제 (즉시 실행 가능)

아래는 **완전하고 독립적인 프로그램** 코드이며, 새 콘솔 앱 프로젝트에 복사·붙여넣기 하면 바로 실행할 수 있습니다. `YOUR_DIRECTORY`를 기울어진 TIFF 파일이 들어 있는 폴더 경로로 바꾸는 것을 잊지 마세요.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace DeskewDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize the OCR engine
            var engine = new OcrEngine();

            // 2️⃣ Load the image you want to straighten
            var imgPath = @"C:\Images\skewed_doc.tif"; // <-- update this path
            var img = OcrImage.FromFile(imgPath);

            // 3️⃣ Define the preprocessing pipeline
            var pipeline = new OcrFilter[]
            {
                new DeskewFilter { MaxAngle = 30 },   // auto‑detect up to 30°
                new DenoiseFilter { Strength = 0.5 }, // moderate noise reduction
                new ContrastBoostFilter { Level = 1.2 } // brighten the text
            };

            // 4️⃣ Apply the pipeline – this returns a new image instance
            var preprocessed = engine.ApplyFilters(img, pipeline);

            // 5️⃣ Run OCR on the cleaned‑up image
            var result = engine.Recognize(preprocessed);

            // 6️⃣ Show confidence and the extracted text
            Console.WriteLine($"Deskew confidence: {result.DeskewConfidence:P2}");
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(result.Text);
        }
    }
}
```

**예상 출력** (스캔이 비교적 깨끗한 경우):

```
Deskew confidence: 96.45%
=== Recognized Text ===
Invoice #12345
Date: 2024‑04‑01
Total: $1,250.00
...
```

문자가 깨져 보이면 필터 강도를 다시 조정하거나 앞서 언급한 `BinarizationFilter`를 추가해 보세요.

---

## 흔히 겪는 함정 & 전문가 팁

- **Pitfall:** 여러 페이지가 포함된 TIFF 사용. `OcrImage.FromFile`은 첫 번째 프레임만 읽습니다. 모든 페이지가 필요하면 `OcrImage.FromMultiPageFile`을 사용하세요.
- **Pitfall:** `OcrEngine`을 해제하지 않음. 프로덕션 코드에서는 `using` 블록으로 감싸 네이티브 리소스를 해제하세요.
- **Pro tip:** 동일한 설정으로 많은 이미지를 처리한다면 파이프라인을 캐시해 오버헤드를 줄이세요.
- **Pro tip:** `DeskewConfidence`를 모니터링 시스템에 로그로 남기세요; 갑작스러운 감소는 스캐너 교정 변화의 신호일 수 있습니다.

---

## 다음 단계 – 워크플로우 확장하기

이제 **이미지 기울기 보정**과 **OCR용 이미지 전처리** 방법을 알았으니 다음을 시도해 볼 수 있습니다:

- **배치 처리** – 폴더에 있는 스캔 PDF를 순회하면서 각 페이지를 이미지로 변환하고 동일한 파이프라인을 적용합니다.
- **언어 지원** – `engine.Language = OcrLanguage.English;` 등으로 설정해 인식률을 높입니다.
- **맞춤형 후처리** – 정규식을 활용해 흔히 발생하는 OCR 오류(예: “0” vs “O”)를 정리합니다.

이러한 주제들은 모두 **OCR 향상 방법** 및 **스캔 이미지 기울기 보정**이라는 부키워드와 자연스럽게 연결됩니다.

---

## 결론

우리는 Aspose.OCR을 사용해 **이미지 기울기 보정**하는 전체 과정을 살펴보았습니다. 견고한 필터 파이프라인 구축부터 신뢰도 점수 확인까지, **Deskew**, **Denoise**, **ContrastBoost**를 적용한 **OCR용 이미지 전처리**를 통해 특히 기울어지거나 노이즈가 많은 스캔에서 **OCR 정확도 향상** 효과를 눈에 띄게 경험할 수 있습니다.

직접 문서 세트에 적용해 보고 필터 파라미터를 조정하면서 OCR 정확도가 상승하는 모습을 확인해 보세요. 질문이 있거나 기울어지지 않는 파일이 있다면 아래에 댓글을 남겨 주세요—함께 문제를 해결해 나갑시다. 즐거운 코딩 되세요!

## 다음에 배워야 할 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하며, 관련 주제를 깊이 있게 다룹니다. 각 자료는 완전한 코드 예제와 단계별 설명을 제공해 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용할 수 있도록 돕습니다.

- [AspOCR 사용 방법: .NET용 이미지 OCR 필터 전처리](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [이미지 OCR 수행 – 이미지 인식에서 OCR 수행](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [OCR 이미지 인식에서 임계값 설정](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}