---
category: general
date: 2026-01-15
description: C#에서 Aspose OCR을 사용하여 이미지를 JSON으로 변환합니다. 이미지에서 텍스트를 추출하고, JSON 경계 상자를
  얻으며, 영수증 이미지를 인식하는 방법을 배워보세요.
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: ko
og_description: Aspose OCR을 사용하여 C#에서 이미지를 JSON으로 변환합니다. 이미지에서 텍스트를 추출하고, 영수증 이미지를
  인식하며, JSON 경계 상자를 얻는 단계별 가이드.
og_title: Aspose OCR C# 가이드를 사용하여 이미지를 JSON으로 변환
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: Aspose OCR C# 가이드를 사용하여 이미지를 JSON으로 변환
url: /ko/net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert Image to JSON with Aspose OCR C# Guide

이미지를 **JSON으로 변환**해야 하는데 원시 텍스트와 정확한 단어 좌표를 모두 제공해 줄 라이브러리를 찾지 못해 고민한 적이 있나요? 당신만 그런 것이 아닙니다. 많은 개발자들이 이미지 파일(특히 영수증)에서 텍스트를 추출하면서 동시에 다운스트림 처리를 위한 기계가 읽을 수 있는 JSON 페이로드가 필요할 때 이 문제에 부딪힙니다.

이 튜토리얼에서는 **Aspose OCR C# 예제**를 통해 이미지에서 텍스트를 추출하고, 영수증 이미지를 인식하며, 각 단어에 대한 **JSON 바운딩 박스**를 출력하는 전체 과정을 단계별로 살펴봅니다. 최종적으로는 콘솔 앱을 실행해 깔끔하게 포맷된 JSON 문자열을 출력하고, 이를 어떤 API, 데이터베이스, 분석 파이프라인에도 전달할 수 있게 됩니다.

> **What you’ll walk away with**  
> • **이미지를 JSON으로 변환**하는 완전한 C# 프로젝트  
> • `IncludeBoundingBoxes`를 활성화하는 이유(이는 `json bounding boxes`의 핵심)  
> • 다양한 이미지 포맷 및 언어를 처리하기 위한 팁  

시작해봅시다.

---

## What You’ll Need

코드 작성을 시작하기 전에 다음 사전 요구 사항이 설치되어 있는지 확인하세요.

- **.NET 6.0 SDK**(또는 이후 버전) – 코드는 .NET 6을 목표로 하지만 .NET Framework 4.7+에서도 동작합니다.  
- **Aspose.OCR for .NET** NuGet 패키지 – `dotnet add package Aspose.OCR` 명령으로 추가할 수 있습니다.  
- 프로젝트에서 참조할 수 있는 폴더에 위치한 샘플 영수증 이미지(`receipt.jpg`).  
- Visual Studio 2022, VS Code 또는 선호하는 IDE.

다른 외부 서비스는 필요하지 않으며, 모든 작업이 로컬에서 수행됩니다.

---

## Convert Image to JSON – Overview

핵심 아이디어는 간단합니다: 이미지를 로드하고, Aspose OCR에 영어(또는 지원되는 언어)를 인식하도록 지시하고, 바운딩 박스를 포함하도록 요청한 뒤, 최종적으로 **JSON** 형식의 결과를 요청합니다. 라이브러리가 OCR, 레이아웃 분석, JSON 직렬화를 모두 처리해 줍니다.

다음은 흐름을 나타낸 고수준 다이어그램입니다(작은 그림을 상상해 보세요).

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

이 작은 다이어그램이 우리가 구현할 전체 파이프라인을 포괄합니다.

---

## Step 1: Set Up the Project and Install Aspose OCR

먼저 새 콘솔 프로젝트를 만들고 Aspose OCR 패키지를 추가합니다.

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Visual Studio를 사용한다면 프로젝트를 마우스 오른쪽 버튼으로 클릭 → *Manage NuGet Packages* → **Aspose.OCR**을 검색하고 최신 안정 버전(현재 23.12)을 설치하세요.

---

## Step 2: Load the Image You Want to Recognize

`OcrImage.FromFile` 메서드를 사용해 영수증 이미지를 읽습니다. 경로가 실제 파일을 가리키는지 확인하지 않으면 `FileNotFoundException`이 발생합니다.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

이미지가 `.csproj`와 같은 폴더에 있다면 `"receipt.jpg"`만 사용하면 됩니다.

---

## Step 3: Configure OCR Options for JSON Bounding Boxes

`OutputFormat = OutputFormat.Json` **및** `IncludeBoundingBoxes = true`를 활성화할 때 마법이 일어납니다. 전자는 Aspose가 결과를 JSON으로 직렬화하도록 지시하고, 후자는 각 단어에 `x`, `y`, `width`, `height`를 추가해 **json bounding boxes**에 필요한 정보를 제공합니다.

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

해상도가 더 필요하거나 다른 언어를 사용해야 할 경우 `ocrOptions.Dpi` 또는 `ocrOptions.Language`를 조정할 수도 있습니다.

---

## Step 4: Perform the Recognition – Extract Text from Image

이제 `Recognize`를 호출합니다. 이 메서드는 JSON 문자열, 원시 텍스트 등을 포함하는 `OcrResult` 객체를 반환합니다.

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

다른 언어를 처리하려면 `Language.English`를 `Language.Spanish`, `Language.French` 등으로 교체하면 됩니다. Aspose는 30개가 넘는 언어를 기본적으로 지원합니다.

---

## Step 5: Output the Result – Your JSON Payload

마지막으로 콘솔에 JSON을 출력합니다. 실제 애플리케이션에서는 파일에 저장하거나 서비스로 전송할 가능성이 높습니다.

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

프로그램을 실행하면 아래와 유사한 JSON 문서가 생성됩니다.

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

각 단어마다 **JSON 바운딩 박스**가 포함된 것을 확인할 수 있습니다—UI 오버레이나 다운스트림 파서에 바로 활용하기에 안성맞춤입니다.

---

## Full Working Example

아래는 복사‑붙여넣기만 하면 바로 실행 가능한 전체 프로그램입니다. 숨겨진 부분이나 외부 호출이 없으며 순수 C#만 사용합니다.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **Watch out for:**  
> • **파일 경로 오류** – 이미지 위치를 다시 확인하세요.  
> • **NuGet 패키지 누락** – `Aspose.OCR`이 참조되어 있는지 확인하세요.  
> • **지원되지 않는 이미지 포맷** – 최상의 결과를 위해 JPEG, PNG, BMP 또는 TIFF를 사용하세요.

---

## Common Questions & Edge Cases

### Can I convert a **PDF page** to JSON instead of a JPEG?

네. 먼저 PDF 페이지를 이미지로 변환한 뒤(예: `Aspose.PDF` 사용) 동일한 OCR 파이프라인에 전달하면 됩니다. JSON 출력은 동일합니다. OCR 단계는 래스터 데이터만을 처리하기 때문입니다.

### What if the receipt is blurry?

`ocrOptions`의 DPI를 높여 보세요. 예시:

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

DPI를 높이면 메모리 사용량이 증가하므로 품질과 성능 사이의 균형을 맞추세요.

### I need **multiple languages** on the same receipt (e.g., English + Spanish).

언어 배열을 전달할 수 있습니다:

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

Aspose는 지정된 순서대로 각 언어를 인식하려 시도합니다.

### How do I write the JSON to a file?

`Console.WriteLine` 라인을 다음과 같이 교체하면 됩니다:

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

이제 다른 서비스로 전달할 수 있는 영구 파일이 생성됩니다.

---

## Visual Summary

![convert image to json example](convert-image-to-json.png "convert image to json example")

*콘솔에서 JSON 페이로드가 출력된 스크린샷입니다.*

---

## Conclusion

우리는 **Aspose OCR**을 사용해 C#에서 **이미지를 JSON으로 변환**하는 방법을 살펴보았습니다. `OutputFormat`과 `IncludeBoundingBoxes`를 설정하면 **이미지에서 텍스트를 추출**, **영수증 이미지를 인식**, 그리고 각 단어에 대한 정밀한 **JSON 바운딩 박스**를 얻을 수 있습니다. 위의 완전한 코드 스니펫을 프로젝트에 바로 넣어 실행해 보세요.

다음 단계는 JSON을 활용해 각 단어를 강조 표시하는 프론트‑엔드 뷰어를 만들거나, 영수증 라인 아이템을 분류하는 머신러닝 모델에 데이터를 공급하는 것입니다. 또한 다른 언어, 높은 DPI 설정, 혹은 여러 이미지를 루프 처리하는 배치 작업도 시도해 볼 수 있습니다.

문제가 발생하면 파일 경로, DPI, 언어 배열에 관한 팁을 기억하세요. 댓글이나 GitHub 레포에 이 데모를 위한 이슈를 남겨도 좋습니다. 즐거운 코딩 되시고, 사진을 구조화된 JSON으로 변환하는 재미를 만끽하세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}