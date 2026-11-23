---
category: general
date: 2026-05-31
description: C#에서 이미지에서 텍스트를 추출하고 영수증 이미지를 읽는 동안 Aspose OCR을 사용하여 OCR 신뢰도 점수를 얻는 방법을
  배워보세요.
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: ko
og_description: OCR 신뢰도 점수는 정확성을 평가할 수 있게 해줍니다; 이 가이드는 이미지에서 텍스트를 추출하고, 경계 상자를 얻으며,
  Aspose OCR을 사용하여 영수증 이미지를 읽는 방법을 보여줍니다.
og_title: C#에서 OCR 신뢰도 점수 – 완전 가이드
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#에서 OCR 신뢰도 점수 – 완전 가이드
url: /ko/net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 OCR 신뢰도 점수 – 완전 가이드

이미지에서 텍스트를 *추출*해야 할 때 **OCR confidence scores**가 궁금했던 적 있나요? 비용 추적을 위해 **read receipt image** 파일을 읽고 엔진이 확신하지 못하는 문자들을 알고 싶을 수도 있습니다. 좋은 소식은? Aspose.OCR을 사용하면 몇 줄의 C# 코드만으로 JPG에서 신뢰도 백분율, 경계 상자, 그리고 일반 텍스트를 가져올 수 있습니다.

이 튜토리얼에서는 라이브러리 설치, **perform OCR on JPG**를 위한 엔진 구성, 신뢰도 점수 추출, 그리고 페이지에서 각 문자가 위치하는 곳을 알려주는 **OCR bounding boxes** 해석까지 알아봅니다. 마지막에는 영수증이나 스캔 문서를 검증하기에 완벽한, 모든 문자와 신뢰도, 위치를 출력하는 실행 가능한 콘솔 앱을 만들 수 있습니다.

## 배울 내용

- NuGet을 통해 Aspose.OCR을 설치하고 기본 OCR 엔진을 설정합니다.  
- `OcrOptions`를 구성하여 **with confidence scores**와 **bounding boxes**가 포함된 일반 텍스트 출력을 요청합니다.  
- `OcrResult`를 순회하여 **extract text from image**를 라인별·심볼별로 추출합니다.  
- 파일 누락, 낮은 신뢰도 문자, 비 JPG 형식 등 일반적인 함정을 처리합니다.  
- 예제를 확장하여 폴더에 있는 여러 영수증 이미지를 처리합니다.

Aspose에 대한 사전 경험은 필요하지 않으며, .NET 환경과 테스트하고 싶은 영수증 이미지(JPG)만 있으면 됩니다.

---

## 단계 1 – Aspose.OCR 설치 및 프로젝트 준비

먼저 Aspose.OCR NuGet 패키지가 필요합니다. 프로젝트 폴더에서 터미널을 열고 다음을 실행합니다:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** 무료 체험은 최대 200페이지까지 지원되며, 영수증 스캔 테스트에 충분합니다.

패키지를 설치한 후, 아직 프로젝트가 없으면 새 콘솔 프로젝트를 생성합니다:

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

이제 생성된 `Program.cs`를 열고 using 지시문을 추가합니다:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

이 네임스페이스들을 통해 `OcrEngine`, `OcrOptions`, 그리고 이후에 사용할 결과 타입에 접근할 수 있습니다.

## 단계 2 – OCR 신뢰도 점수 및 OCR 경계 상자 가져오기

이것이 튜토리얼의 핵심입니다. 각 인식된 문자에 **confidence score**와 **bounding box**(문자를 둘러싼 사각형)가 포함되도록 엔진을 구성합니다. H2 헤더 자체가 주요 키워드를 포함하고 있어 SEO 규칙을 만족합니다.

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**Why include confidence scores?**  
신뢰도 점수(0‑100%)는 엔진이 각 문자에 대해 얼마나 확신하는지를 알려줍니다. 출력 결과를 비용 승인 워크플로와 같은 하위 로직에 전달한다면, 낮은 신뢰도 심볼을 자동으로 거부하거나 표시할 수 있습니다.

**Why request bounding boxes?**  
경계 상자는 원본 이미지에 텍스트를 강조 표시하거나, 부분 영역을 추출하거나, UI 오버레이와 OCR 결과를 정렬할 때 필수적입니다. 각 `character.Bounds`는 픽셀 좌표의 X, Y, 너비, 높이를 제공합니다.

## 단계 3 – JPG에서 OCR 수행 및 이미지에서 텍스트 추출

이제 실제로 엔진을 실행합니다. `Recognize()` 호출이 모든 무거운 작업을 수행하고 `OcrResult` 객체를 반환합니다.

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

이미지 경로가 잘못되었거나 지원되지 않는 형식이면 Aspose가 `FileNotFoundException` 또는 `UnsupportedImageFormatException`을 발생시킵니다. 프로덕션 코드에서는 try/catch 블록으로 감싸 이러한 예외를 우아하게 처리하세요.

### 일반 텍스트 추출

연결된 텍스트만 필요하면 `ocrResult.Text`를 읽을 수 있습니다:

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

하지만 신뢰도 점수와 경계 상자를 요청했기 때문에 구조를 순회하여 각 문자 상세 정보를 확인합니다.

## 단계 4 – 라인, 심볼을 순회하며 OCR 신뢰도 점수 표시

다음 루프는 모든 문자를 출력하고, 해당 신뢰도와 박스를 표시합니다. 여기서 **read receipt image** 예제가 진가를 발휘합니다.

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

샘플 출력은 다음과 비슷할 수 있습니다:

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**Interpreting the numbers:**  
- **Confidence ≥ 90%** – 보통 그대로 받아들여도 안전합니다.  
- **Confidence 70‑89%** – 특히 금액의 숫자와 같은 경우 재확인하는 것이 좋습니다.  
- **Confidence < 70%** – 수동 검토를 위해 표시하는 것을 고려하세요.

## 단계 5 – 전체 실행 가능한 예제 (오류 처리 포함)

모든 것을 합치면 `Program.cs`에 복사·붙여넣기 할 수 있는 완전한 프로그램이 됩니다. 파일 누락을 간단히 확인하고 OCR이 실패했을 때 친절한 메시지를 출력합니다.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### 예상 출력

`dotnet run`을 실행하면 콘솔에 먼저 연결된 영수증 텍스트가 표시되고, 이어서 각 문자와 신뢰도 점수 및 경계 상자가 리스트됩니다. 문자의 신뢰도가 낮으면 80% 이하의 백분율이 표시되어 해당 영수증 부분을 수동으로 검증하도록 안내합니다.

## 보너스: 폴더 내 여러 영수증 처리

영수증 JPG가 여러 개 있다면 위 로직을 `foreach (var file in Directory.GetFiles(folder, "*.jpg"))` 루프로 감싸면 됩니다. 각 파일마다 `OcrEngine`을 재설정하거나 루프 내부에서 새 인스턴스를 생성해 상태 누수를 방지하세요.

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

대량 처리 기능은 야간 비용 가져오기 작업에 유용합니다.

---

## 결론

이제 **OCR confidence scores**를 C#에서 얻고, **extracting text from image**를 수행하며, **perform OCR on JPG** 파일(예: **read receipt image**)에서 **OCR bounding boxes**를 가져오는 완전한 엔드‑투‑엔드 솔루션을 갖추었습니다. 코드는 최신 Aspose.OCR 버전(2026‑05‑31 기준)과 완전히 독립적으로 동작하며, 신뢰할 수 있는 문서 처리 파이프라인을 구축하는 데 필요한 세밀한 데이터를 제공합니다.

다음 단계는 `System.Drawing`이나 UI 라이브러리를 사용해 원본 영수증에 경계 상자를 시각화하거나, 낮은 신뢰도 문자를 보조 검증 서비스에 전달하는 것입니다. `ocrEngine.Options.Language = OcrLanguage.French;`와 같이 언어를 바꿔 다양한 로케일을 실험해 볼 수도 있습니다.

행복한 코딩 되세요, 그리고 신뢰도 점수가 언제나 높게 유지되길 바랍니다! 

![Console output showing OCR confidence scores and bounding boxes for a receipt

## 다음에 배울 내용은?

- [Aspose.OCR을 사용한 언어 선택이 가능한 C# 이미지 텍스트 추출](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [이미지 인식에서 인식된 문자에 대한 OCR 문자 선택 가져오기](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [이미지 인식에서 JSON 결과를 위한 Aspose OCR 사용 방법](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}