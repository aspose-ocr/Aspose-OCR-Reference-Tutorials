---
category: general
date: 2026-01-10
description: Aspose OCR을 C#에서 사용하여 이미지에서 텍스트를 인식하고, 텍스트 좌표를 추출하며, 영수증을 JSON으로 변환하는
  방법을 배웁니다. 단계별 튜토리얼.
draft: false
keywords:
- recognize text from image
- how to extract text
- extract text coordinates
- convert receipt to json
language: ko
og_description: C#에서 Aspose OCR을 사용하여 이미지에서 텍스트를 인식합니다. 이 가이드는 텍스트를 추출하고 좌표를 얻으며 영수증을
  JSON으로 변환하는 방법을 보여줍니다.
og_title: 이미지에서 텍스트 인식 – 전체 C# OCR 튜토리얼
tags:
- OCR
- C#
- Aspose
title: C#에서 이미지 텍스트 인식 – OCR 및 JSON 완전 가이드
url: /ko/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지에서 텍스트 인식 – 전체 C# OCR 튜토리얼

이미지에서 텍스트를 인식해야 했지만 어떤 라이브러리를 선택해야 할지 몰랐던 적이 있나요? 당신만 그런 것이 아닙니다. 실제 애플리케이션—경비 추적기, 영수증 스캐너, 문서 보관소—에서 텍스트를 신뢰성 있게 추출하는 것이 첫 번째 장벽입니다.  

이 튜토리얼에서는 **how to extract text**를 단계별로 살펴보고, 경계 상자를 추출한 뒤, 마지막으로 Aspose.OCR for .NET을 사용해 **convert receipt to JSON**하는 과정을 보여드립니다. 끝까지 진행하면 영수증 사진을 받아 신뢰도 점수와 좌표가 포함된 깔끔한 JSON 파일을 출력하는 독립형 C# 프로젝트를 얻게 됩니다.

## 필요한 준비물

시작하기 전에, 다음이 머신에 설치되어 있는지 확인하세요:

- **.NET 6.0 SDK** (또는 이후 버전). 이전 프레임워크도 동작하지만, .NET 6이 최신 라이브러리에 가장 적합합니다.
- **Visual Studio 2022** 또는 C# 확장 기능이 포함된 VS Code.
- **Aspose.OCR for .NET** NuGet 패키지(`Aspose.OCR` 및 `Aspose.OCR.Output`). 패키지 관리자 콘솔을 통해 설치할 수 있습니다:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Output
```

- 예시 영수증 이미지(예: `receipt.jpg`)를 나중에 참조할 폴더에 배치합니다.

이것으로 끝입니다—추가 SDK나 네이티브 바이너리 없이 순수 관리 코드만 사용합니다.

## Step 1: 새 콘솔 프로젝트 만들기

먼저, 콘솔 앱을 생성합니다. UI 오버헤드 없이 OCR을 테스트하기 가장 빠른 방법입니다.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later.
        }
    }
}
```

> **Pro tip:** 프로젝트 폴더를 깔끔하게 유지하세요; `Resources`라는 하위 폴더를 만들고 그 안에 `receipt.jpg`를 넣으세요. 경로 처리가 훨씬 쉬워집니다.

## Step 2: 영수증 이미지 로드

이제 실제로 **recognize text from image**를 수행합니다. 첫 번째 단계는 OCR 엔진에 파일을 지정하는 것입니다.

```csharp
// Inside Main()
string imagePath = @"Resources/receipt.jpg";
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    Image = ImageStream.FromFile(imagePath)
};

Console.WriteLine("✅ Image loaded successfully.");
```

로드를 간단한 존재 확인으로 감싸는 이유는 무엇일까요? 실제 운영 환경에서는 누락되었거나 손상된 사용자 업로드 파일을 자주 다루기 때문입니다. 문제를 일찍 포착하면 나중에 발생할 수 있는 모호한 예외를 방지할 수 있습니다.

## Step 3: OCR 수행 – **recognize text from image**

이미지를 메모리에 로드한 상태에서 Aspose에 **recognize text from image**를 요청합니다. 이 작업은 동기식이며 풍부한 결과 집합을 반환합니다.

```csharp
// Still inside Main()
try
{
    ocrEngine.Recognize();
    Console.WriteLine("🧠 OCR completed.");
}
catch (Exception ex)
{
    Console.WriteLine($"❗ OCR failed: {ex.Message}");
    return;
}
```

내부적으로 Aspose는 수백만 글자에 대해 학습된 신경망을 실행합니다. 엔진은 `ocrEngine.Text`, `ocrEngine.RecognitionResult` 및 좌표를 보유한 `OcrRegion` 객체 컬렉션을 채웁니다. 이것이 바로 다음 단계에 필요한 내용입니다.

## Step 4: **How to extract text** – 원시 문자열 가져오기

순수 텍스트만 필요하다면(예: 빠른 검색), 엔진에서 바로 가져올 수 있습니다:

```csharp
string plainText = ocrEngine.Text;
Console.WriteLine("\n--- Extracted Text ---");
Console.WriteLine(plainText);
```

OCR이 단락 경계를 감지한 위치에 줄 바꿈이 포함된 것을 볼 수 있습니다. 많은 영수증 스캔 상황에서 원시 문자열만으로도 간단한 정규식을 사용해 총액, 날짜, 상점 이름 등을 추출하기에 충분합니다.

## Step 5: **extract text coordinates** – 각 단어의 경계 상자

이미지에서 특정 텍스트가 위치한 *곳*을 알아야 할 때가 많습니다—예를 들어 UI에서 총액을 강조 표시하려는 경우. Aspose는 `OcrRegion` 객체를 통해 이를 제공합니다.

```csharp
Console.WriteLine("\n--- Text Coordinates (extract text coordinates) ---");
foreach (var region in ocrEngine.RecognitionResult.Regions)
{
    // Each region represents a word or a line depending on the engine settings.
    string word = region.Text;
    var bounds = region.BoundingBox; // X, Y, Width, Height
    Console.WriteLine($"Word: \"{word}\" | Box: X={bounds.X}, Y={bounds.Y}, W={bounds.Width}, H={bounds.Height}");
}
```

우리는 인식된 각 세그먼트에 대해 **extract text coordinates**를 반복하고 있습니다. 좌표는 원본 이미지에 상대적이므로 그래픽 캔버스나 HTML `<canvas>` 요소에 겹쳐 표시할 수 있습니다.

## Step 6: **convert receipt to JSON** – 상세 결과 저장

이제 모든 것을 연결하는 단계가 왔습니다: 텍스트, 신뢰도 점수 및 경계 상자를 포함하는 기계가 읽을 수 있는 구조가 필요합니다. Aspose는 이를 손쉽게 구현할 수 있는 `JsonSaveOptions`를 제공합니다.

```csharp
// Define where the JSON will be saved
string jsonPath = @"Resources/receipt.json";

// Configure JSON options to keep confidence and bounding boxes
JsonSaveOptions jsonOptions = new JsonSaveOptions
{
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};

// Save the OCR result
ocrEngine.Save(jsonPath, jsonOptions);
Console.WriteLine($"\n💾 Detailed OCR results saved to {jsonPath}");
```

생성된 파일은 다음과 같은 형태이며(간결하게 표시):

```json
{
  "Regions": [
    {
      "Text": "Store",
      "Confidence": 0.99,
      "BoundingBox": { "X": 45, "Y": 120, "Width": 80, "Height": 20 }
    },
    {
      "Text": "Total",
      "Confidence": 0.97,
      "BoundingBox": { "X": 300, "Y": 560, "Width": 70, "Height": 22 }
    }
    // ... more regions ...
  ]
}
```

이제 **convert receipt to JSON** 아티팩트를 얻었으며, 이를 비용 보고 API, 분석 파이프라인, 혹은 각 단어 주위에 사각형을 그리는 간단한 UI와 같은 하위 서비스에 전달할 수 있습니다.

## 전체 작업 예제

모든 요소를 합치면, 프로젝트에 복사‑붙여넣기 할 수 있는 완전한 `Program.cs`는 다음과 같습니다:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image
            // -------------------------------------------------
            string imagePath = @"Resources/receipt.jpg";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            OcrEngine ocrEngine = new OcrEngine
            {
                Image = ImageStream.FromFile(imagePath)
            };
            Console.WriteLine("✅ Image loaded.");

            // -------------------------------------------------
            // 2️⃣ Run OCR – recognize text from image
            // -------------------------------------------------
            try
            {
                ocrEngine.Recognize();
                Console.WriteLine("🧠 OCR completed.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❗ OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 3️⃣ Extract plain text (how to extract text)
            // -------------------------------------------------
            Console.WriteLine("\n--- Extracted Text ---");
            Console.WriteLine(ocrEngine.Text);

            // -------------------------------------------------
            // 4️⃣ Get coordinates (extract text coordinates)
            // -------------------------------------------------
            Console.WriteLine("\n--- Text Coordinates ---");
            foreach (var region in ocrEngine.RecognitionResult.Regions)
            {
                var box = region.BoundingBox;
                Console.WriteLine($"Word: \"{region.Text}\" | Box: X={box.X}, Y={box.Y}, W={box.Width}, H={box.Height}");
            }

            // -------------------------------------------------
            // 5️⃣ Save detailed JSON (convert receipt to json)
            // -------------------------------------------------
            string jsonPath = @"Resources/receipt.json";
            JsonSaveOptions jsonOptions = new JsonSaveOptions
            {
                IncludeConfidence = true,
                IncludeBoundingBoxes = true
            };
            ocrEngine.Save(jsonPath, jsonOptions);
            Console.WriteLine($"\n💾 JSON saved at {jsonPath}");
        }
    }
}
```

프로그램을 실행(`dotnet run`)하고 콘솔 출력을 확인하세요. `Resources/receipt.json`를 열어 구조를 검증합니다.

## 자주 묻는 질문 및 엣지 케이스

- **What if the image is blurry?**  
  Aspose OCR은 300 dpi 이상에서 가장 잘 작동합니다. 신뢰도 점수가 낮게 나오면 엔진에 이미지를 전달하기 전에 선명도 필터를 적용해 보세요.

- **Can I recognize multiple languages?**  
  가능합니다. `Recognize()`를 호출하기 전에 `ocrEngine.Language = Language.English | Language.Spanish;`와 같이 설정하세요.

- **How do I limit output to only numbers (e.g., totals)?**  
  순수 텍스트를 얻은 뒤 `ocrEngine.Text`에 `\\d+\\.\\d{2}`와 같은 정규식을 적용하세요. 이미 좌표가 있으므로 매치된 문자열을 해당 영역에 매핑해 시각적으로 강조할 수 있습니다.

- **Is the JSON format customizable?**  
  `JsonSaveOptions` 클래스는 여러 플래그를 제공합니다. 완전히 커스텀 스키마가 필요하면 `ocrEngine.RecognitionResult.Regions`를 순회하고 `System.Text.Json`을 사용해 직접 직렬화하면 됩니다.

## 결론

우리는 C#에서 Aspose.OCR을 사용해 **recognize text from image**를 수행하고, **how to extract text**를 보여주며, **extract text coordinates**를 추출하고, 마지막으로 **convert receipt to JSON**을 구현했습니다. 전체 흐름은 단일 콘솔 앱에 담겨 있어 프로토타입이나 대규모 시스템의 구성 요소로 사용하기에 적합합니다.

다음 단계는? JSON을 경계 상자를 그리는 프론트엔드에 전달하거나, 비용 보고 서비스에 연결해 보세요. 또한 다양한 이미지 포맷(PNG, TIFF)이나 영수증 폴더를 일괄 처리하는 실험도 가능합니다.

OCR, Aspose, JSON 처리에 대해 더 궁금한 점이 있나요? 아래에 댓글을 남겨 주세요. 즐거운 코딩 되세요! 

![Receipt image example for recognize text from image](receipt.jpg "Receipt image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}