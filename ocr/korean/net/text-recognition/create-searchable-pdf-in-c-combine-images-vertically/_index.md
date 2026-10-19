---
category: general
date: 2026-02-28
description: C#에서 이미지를 수직으로 결합하여 검색 가능한 PDF를 만들기. 이미지를 수직으로 쌓는 방법과 Aspose OCR을 사용해
  스캔한 페이지 PDF를 변환하는 방법을 배워보세요.
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: ko
og_description: C#에서 이미지를 수직으로 결합하여 검색 가능한 PDF를 만들기. 이 가이드는 이미지를 수직으로 쌓고 Aspose OCR을
  사용해 스캔한 페이지 PDF를 변환하는 방법을 보여줍니다.
og_title: C#에서 검색 가능한 PDF 만들기 – 이미지를 수직으로 결합
tags:
- Aspose OCR
- C#
- PDF generation
title: C#에서 검색 가능한 PDF 만들기 – 이미지를 수직으로 결합
url: /ko/net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 검색 가능한 PDF 만들기 – 이미지를 수직으로 결합

스캔한 PNG 몇 장으로 **검색 가능한 PDF**를 만들어야 할 때, 어디서 시작해야 할지 몰라 고민한 적 있나요? 당신만 그런 것이 아닙니다. 많은 문서 자동화 프로젝트에서 가장 큰 어려움은 이미지 파일들을 하나의 깔끔하고 검색 가능한 PDF로 변환하여 인덱싱하고 공유할 수 있게 만드는 것입니다.  

이 튜토리얼에서는 **이미지를 수직으로 쌓는 방법**, **이미지를 수직으로 결합하는 방법**, 그리고 마지막으로 Aspose.OCR의 GPU 가속 엔진을 사용해 **스캔한 페이지 PDF를** 단일 검색 가능한 문서로 변환하는 완전한 실행 가능한 예제를 단계별로 살펴보겠습니다. 끝까지 진행하면 .NET 솔루션에 바로 넣어 사용할 수 있는 독립형 프로그램을 얻게 됩니다.

> **배우게 될 내용**
> - GPU 지원 OCR 엔진 초기화.
> - 이미지를 병렬로 처리.
> - **이미지를 수직으로 결합**하여 다중 페이지 스캔을 모방.
> - 검색 가능한 PDF와 상세 JSON 보고서를 내보내어 다운스트림 분석에 활용.

## 사전 요구 사항

- .NET 6+ (코드는 .NET 6, .NET 7, 또는 .NET 8에서 컴파일됩니다)
- Aspose.OCR NuGet 패키지 (`Install-Package Aspose.OCR`)
- `ProcessingMode.Gpu` 설정을 유지하려면 GPU 지원 머신이 필요합니다 (CPU 폴백도 작동합니다)
- 몇 개의 스캔된 PNG/JPEG 파일이 들어 있는 폴더 (데모는 `page1.png`, `page2.png`, `page3.png` 사용)

외부 서비스나 숨겨진 구성 파일 없이 순수 C#만 사용합니다.

## Step 1 – OCR 엔진을 설정하여 **검색 가능한 PDF 만들기**

먼저 `OcrEngine`을 생성하고 GPU 가속을 활성화한 뒤, 언어를 영어로 설정하고 전처리 필터를 몇 개 추가합니다. 이 필터들은 기울어진 페이지를 바로잡는 `DeskewFilter`와 노이즈를 제거하는 `DenoiseFilter`를 통해 정확도를 향상시킵니다.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Collections.Generic;
using System.Drawing;

class AllInOneDemo
{
    static void Main()
    {
        // Initialize OCR engine – this is the heart of creating a searchable PDF
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu,   // Switch to CPU if no GPU
            Language = OcrLanguage.English
        };
        // Pre‑processing improves OCR quality
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseFilter());
```

**왜 중요한가:** OCR 엔진은 텍스트 인식이라는 무거운 작업을 수행합니다. `ProcessingMode.Gpu`를 활성화하면 최신 그래픽 카드에서 인식 시간이 절반으로 줄어들고, 필터들은 스캔 시 흔히 발생하는 아티팩트를 감소시켜 왜곡된 출력이 나오는 것을 방지합니다.

## Step 2 – 배치 프로세서를 구성하여 **스캔한 페이지 PDF 변환**을 효율적으로 수행

각 페이지를 하나씩 처리하는 방식은 이미지가 몇 장일 때는 괜찮지만, 실제 프로젝트에서는 수십에서 수백 페이지가 일반적입니다. Aspose.OCR의 `OcrBatchProcessor`를 사용하면 인식을 병렬로 실행할 수 있어 **스캔한 페이지 PDF 변환** 단계가 크게 빨라집니다.

```csharp
        // Set up batch processor – ideal for converting many scanned pages to PDF
        var batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 2,          // Adjust based on CPU/GPU cores
            Language = OcrLanguage.English,
            ProcessingMode = ProcessingMode.Gpu
        };

        // List the image files you want to turn into a searchable PDF
        List<string> imageFiles = new()
        {
            "YOUR_DIRECTORY/page1.png",
            "YOUR_DIRECTORY/page2.png",
            "YOUR_DIRECTORY/page3.png"
        };
```

**팁:** CPU 전용 머신이라면 `ProcessingMode = ProcessingMode.Cpu`로 설정하세요. 배치 프로세서는 여전히 `MaxDegreeOfParallelism`을 적용하므로 머신 과부하를 방지하도록 조정할 수 있습니다.

## Step 3 – 배치에 대해 OCR을 실행하고 결과 수집

이제 실제로 텍스트를 인식합니다. `Recognize` 메서드는 원본 이미지와 추출된 텍스트를 모두 포함하는 `OcrResult` 객체 리스트를 반환합니다.

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

이 시점에서 **검색 가능한 PDF 만들기**에 필요한 모든 것, 즉 메모리에 남아 있는 이미지와 해당 텍스트 레이어를 확보한 것입니다.

## Step 4 – **이미지를 수직으로 결합**하고 검색 가능한 PDF 생성

대부분의 스캔 문서는 다중 페이지 PDF이므로 개별 페이지 이미지를 물리적인 스택처럼 하나의 긴 이미지로 이어붙여야 합니다. Aspose.OCR는 이를 위해 `Image.CombineVertical`을 제공합니다.

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

결과 파일(`combined_searchable.pdf`)은 각 페이지 이미지 아래에 선택 가능하고 검색 가능한 텍스트를 포함합니다—스캔된 소스로부터 **검색 가능한 PDF 만들기**에 정확히 필요한 형태입니다.

![검색 가능한 PDF 예시](/images/create-searchable-pdf.png "검색 가능한 PDF 예시")

*이미지 대체 텍스트: 검색 가능한 PDF 예시로, 검색 가능한 텍스트가 포함된 결합된 PDF를 보여줍니다.*

**왜 수직 스택인가?** 많은 OCR 라이브러리는 각 이미지를 별개의 페이지로 처리합니다. 이미지를 스택하면 PDF 페이지 순서를 유지하면서 전체 문서에 대해 단일 OCR 처리를 활용할 수 있습니다.

## Step 5 – 첫 페이지에 대한 상세 JSON 내보내기 (다운스트림 워크플로에 유용)

때때로 PDF만으로는 부족합니다; OCR 데이터를 데이터베이스나 머신러닝 파이프라인에 전달하고 싶을 수도 있습니다. Aspose.OCR는 각 `OcrResult`를 JSON으로 직렬화하여 경계 상자, 신뢰도 점수 등을 보존합니다.

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**예상 JSON 스니펫 (축약):**

```json
{
  "Text": "Sample scanned text …",
  "Confidence": 0.97,
  "Blocks": [
    {
      "Text": "Header",
      "BoundingBox": { "X": 15, "Y": 10, "Width": 480, "Height": 30 }
    }
    // …
  ]
}
```

이제 이 JSON을 Elasticsearch에 텍스트를 색인하거나 맞춤형 분석 대시보드에 전달하는 등 모든 다운스트림 시스템에 활용할 수 있습니다.

---

## **이미지를 수직으로 스택**하는 방법 – 빠른 요약

Aspose 없이 **이미지를 수직으로 스택**하는 방법이 궁금하다면 `System.Drawing`을 사용해 새 비트맵을 만들고 각 페이지를 순차적으로 그릴 수 있습니다. 하지만 Aspose의 내장 `Image.CombineVertical`은 DPI, 픽셀 포맷, 메모리 관리를 자동으로 처리해 생산 코드에 가장 신뢰할 수 있는 선택입니다.

### 대안: `System.Drawing` 사용 (단순 호기심용)

```csharp
int totalHeight = 0;
int maxWidth = 0;
foreach (var img in ocrResults)
{
    totalHeight += img.Image.Height;
    maxWidth = Math.Max(maxWidth, img.Image.Width);
}
var canvas = new Bitmap(maxWidth, totalHeight);
using var g = Graphics.FromImage(canvas);
int offset = 0;
foreach (var img in ocrResults)
{
    g.DrawImage(img.Image, 0, offset);
    offset += img.Image.Height;
}
canvas.Save("combined_manual.png");
```

수동 방식도 동작하지만 자동 DPI 처리와 결과를 바로 `RecognizeToPdf`에 전달하는 편리함을 잃게 됩니다. 매우 특수한 요구 사항이 아니라면 `CombineVertical`을 사용하세요.

## 흔히 발생하는 문제와 해결 방법

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Out‑of‑memory errors** (수십 개의 고해상도 스캔 처리 시) | 각 이미지가 PDF가 작성될 때까지 메모리에 유지됩니다 | `Image` 객체를 사용이 끝나는 즉시(`using` 블록) 해제하거나 결합하기 전에 이미지를 다운스케일하세요 |
| **Garbage text** (OCR 후) | 스캔이 기울었거나 대비가 낮음 | `DeskewFilter`와 `DenoiseFilter`를 유지하고, 필요하면 `ContrastFilter` 추가를 고려하세요 |
| **Missing searchable layer** | `RecognizeToPdf` 대신 `Recognize`를 사용함 | 결합된 이미지에 대해 `ocrEngine.RecognizeToPdf`를 호출했는지 확인하세요 |
| **GPU fallback fails** (적절한 드라이버가 없는 머신) | `ProcessingMode.Gpu`가 예외를 발생시킴 | 엔진 생성 코드를 try/catch로 감싸고 `ProcessingMode.Cpu`로 폴백하도록 하세요 |

## 다음 단계 – 워크플로 확장

이제 **검색 가능한 PDF 만들기** 방법을 알았으니, 다음과 같은 작업을 고려할 수 있습니다:

- `Directory.GetFiles`와 `foreach` 루프를 사용해 **전체 폴더를 배치 처리**합니다.
- 결합하기 전에 각 페이지에 **워터마크 추가** (Aspose.Imaging의 `ImageProcessor` 사용).
- 나중에 페이지별 PDF가 필요하면 **검색 가능한 PDF를 개별 페이지로 분할** (`PdfDocument.Split` from Aspose.PDF 사용).
- **Azure Blob Storage와 통합**하여 클라우드에서 이미지를 가져오고 최종 PDF를 다시 업로드합니다.

이 모든 확장은 본질적으로 동일한 핵심 개념인 OCR 설정, 이미지 처리, PDF 내보내기를 포함합니다.

## 결론

C#에서 스캔 이미지 컬렉션을 사용해 **검색 가능한 PDF 만들기**에 필요한 모든 내용을 다루었습니다. GPU 지원 `OcrEngine`을 초기화하고 `OcrBatchProcessor`로 병렬 배치를 실행한 뒤 **이미지를 수직으로 결합**하고 마지막으로 `RecognizeToPdf`를 호출하면 보관이나 인덱싱에 적합한 깔끔한 검색 가능한 문서를 얻을 수 있습니다. 추가적인 JSON 내보내기를 통해 OCR 결과를 완전히 파악할 수 있어 분석이나 맞춤형 워크플로에 활용할 수 있습니다.

한 번 실행해 보고 다양한 필터를 실험해 보세요. 그러면 문서 자동화 파이프라인이 훨씬 매끄러워지는 것을 느낄 수 있습니다. 문제가 발생하면 댓글을 남겨 주세요—코딩 즐겁게!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}