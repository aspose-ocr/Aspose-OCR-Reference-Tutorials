---
category: general
date: 2026-09-13
description: Aspose OCR을 사용하여 C#에서 스캔한 페이지를 PDF로 변환하는 방법을 배웁니다. 이 가이드는 전처리, 한국어 텍스트
  인식 및 검색 가능한 PDF 생성 과정을 보여줍니다.
keywords:
- scanned page to pdf
- preprocess image for OCR
- generate pdf with text
- convert image to searchable pdf
- gpu accelerated OCR
- recognize Korean text image
lastmod: 2026-09-13
og_description: Aspose OCR과 함께 C#에서 스캔한 페이지를 PDF로 변환하는 방법을 배웁니다. 이 튜토리얼은 이미지 전처리,
  한국어 텍스트를 위한 GPU 가속 OCR, 그리고 몇 분 안에 검색 가능한 PDF를 생성하는 과정을 다룹니다.
og_image_alt: Screenshot of C# console app converting a scanned Korean page to searchable
  PDF using Aspose OCR
og_title: C#와 OCR을 사용하여 스캔한 페이지를 PDF로 변환하는 방법
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  headline: How to turn a scanned page to PDF in C# with OCR
  type: TechArticle
- description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  name: How to turn a scanned page to PDF in C# with OCR
  steps:
  - name: Initialise the OCR engine with GPU support.
    text: Initialise the OCR engine with GPU support.
  - name: Add **preprocess image for OCR** filters such as deskew and denoise.
    text: Add **preprocess image for OCR** filters such as deskew and denoise.
  - name: Download and load the Korean language model (handled automatically).
    text: Download and load the Korean language model (handled automatically).
  - name: Run the OCR on the image.
    text: Run the OCR on the image.
  - name: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
    text: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
  - name: (Optional) Serialize the OCR output to JSON for downstream pipelines.
    text: (Optional) Serialize the OCR output to JSON for downstream pipelines.
  - name: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
    text: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
  - name: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
    text: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
  - name: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
    text: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
  type: HowTo
- questions:
  - answer: 'The exporter embeds the original bitmap at its native resolution. If
      size is a concern, downscale the image *before* recognition:'
    question: My PDF is huge compared to the original image.
  - answer: Verify that the image path is correct and that the file is not corrupted.
      Also, make sure the GPU driver is up‑to‑date; older drivers can cause silent
      failures.
    question: The OCR returns empty strings.
  - answer: Absolutely. Wrap steps 4‑6 in a `foreach (var file in Directory.GetFiles("Resources",
      "*.jpg"))` loop and change the output PDF path accordingly.
    question: Can I process multiple pages in a loop?
  type: FAQPage
tags:
- scanned page to pdf
- OCR
- Aspose
- C#
title: C#와 OCR을 사용하여 스캔한 페이지를 PDF로 변환하는 방법
url: /ko/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 스캔한 페이지를 OCR을 사용하여 C#에서 PDF로 변환하는 방법

스캔한 페이지를 텍스트 검색이 가능하도록 **convert a scanned page to PDF**해야 한다면, 올바른 위치에 오셨습니다. 이 튜토리얼에서는 Aspose OCR을 사용하여 **preprocess image for OCR**, **recognize Korean text image**, 그리고 마지막으로 **create searchable PDF image**를 수행하는 방법을 간단한 C# 콘솔 애플리케이션을 통해 안내합니다.

## 빠른 답변
- **OCR을 처리하는 라이브러리는 무엇인가요?** Aspose.OCR for .NET  
- **GPU를 사용할 수 있나요?** 예 – GPU 가속을 활성화하면 최대 2× 빠른 처리 속도를 얻을 수 있습니다  
- **한국어 언어 팩이 필요합니까?** 첫 사용 시 자동으로 다운로드됩니다  
- **출력이 검색 가능합니까?** 생성된 PDF에는 보이지 않는 텍스트 레이어가 포함됩니다  
- **지원되는 .NET 버전은 무엇인가요?** .NET 6.0 이상 (.NET Core 및 .NET Framework 포함)

## 요구 사항

- **.NET 6.0 또는 이후 버전** – .NET Core, .NET Framework 및 .NET 5/6+에서 작동합니다  
- **Aspose.OCR for .NET** NuGet 패키지 (`Aspose.OCR`) – 체험 키는 Aspose 사이트에서 무료로 제공됩니다  
- 예시 이미지(한국어 문자 포함), 예: `korean_book_page.jpg`  
- 선호하는 IDE(Visual Studio 2022, VS Code, Rider 등)

> **Pro tip:** 이미지를 `Resources/` 폴더에 저장하면 기기마다 경로가 일관됩니다.

## 프로세스 개요

1. GPU 지원으로 OCR 엔진을 초기화합니다.  
2. **preprocess image for OCR** 필터(예: deskew, denoise)를 추가합니다.  
3. 한국어 언어 모델을 다운로드하고 로드합니다(자동 처리).  
4. 이미지에 대해 OCR을 실행합니다.  
5. **SearchablePdfExporter**를 사용해 결과를 내보내어 **create searchable PDF image**를 생성합니다.  
6. (선택 사항) OCR 출력을 JSON으로 직렬화하여 다운스트림 파이프라인에 전달합니다.

아래에서는 각 단계를 자세히 설명하고, 왜 중요한지 설명하며, 복사‑붙여넣기 할 수 있는 정확한 코드를 제공합니다.

## 스캔한 페이지를 PDF로 변환하는 방식은?

`OcrEngine`은 이미지에 대한 광학 문자 인식을 수행하는 Aspose.OCR의 주요 클래스입니다.  
`SearchablePdfExporter`는 원본 이미지와 검색을 위한 보이지 않는 텍스트 레이어를 포함하는 PDF를 생성합니다.  
`RecognitionResult`는 OCR 엔진이 반환한 텍스트와 신뢰도 데이터를 보유합니다.

이미지를 `new OcrEngine()`으로 로드하고 `engine.Recognize("korean_book_page.jpg")`를 호출한 뒤, `RecognitionResult`를 `SearchablePdfExporter.Export`에 전달합니다. 이 두 단계 흐름은 비트맵을 읽고 유니코드 텍스트를 추출한 뒤, 텍스트 레이어가 보이지 않지만 검색 가능한 단일 PDF에 두 요소를 모두 삽입합니다. GPU 가속은 인식 시간을 대략 절반으로 줄이며, deskew 및 denoise 필터는 잡음이 많은 스캔에서 정확도를 최대 15 % 향상시킵니다.

## 이미지 → PDF 변환 – 전체 워크플로우

다음 스니펫은 *전체* 프로그램입니다. 새 콘솔 프로젝트(`dotnet new console -n OcrPdfDemo`)를 생성하고 자동 생성된 `Program.cs`를 자리표시자에 표시된 코드로 교체하세요.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;
using Aspose.OCR.Result;   // for JsonResult

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialise the OCR engine (GPU enabled, offline mode off)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,          // leverages your graphics card for faster inference
                OfflineMode = false    // allows on‑the‑fly language model download
            };

            // --------------------------------------------------------------
            // Step 2: Add preprocessing filters to improve accuracy
            // --------------------------------------------------------------
            // Deskew corrects slight rotations; MaxAngle = 12° is a safe default.
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 12 });

            // Denoise removes isolated speckles that often appear in scanned books.
            ocrEngine.Filters.Add(new DenoiseFilter());

            // --------------------------------------------------------------
            // Step 3: Load the Korean language model
            // --------------------------------------------------------------
            // Aspose will download the model the first time you run this on a new machine.
            ocrEngine.LoadLanguage(LanguageModel.Korean);

            // --------------------------------------------------------------
            // Step 4: Recognise text from the input image
            // --------------------------------------------------------------
            // Replace the path with your actual image location.
            string imagePath = "Resources/korean_book_page.jpg";
            var recognitionResult = ocrEngine.Recognize(imagePath);

            // --------------------------------------------------------------
            // Step 5: Export the recognised page as a searchable PDF
            // --------------------------------------------------------------
            string pdfPath = "Resources/korean_page.pdf";
            var exporter = new SearchablePdfExporter { OutputPath = pdfPath };
            exporter.Export(ocrEngine, imagePath);

            // --------------------------------------------------------------
            // Step 6: Obtain a structured JSON representation of the result
            // --------------------------------------------------------------
            string json = JsonResult.FromRecognitionResult(recognitionResult).ToString(true);
            Console.WriteLine("=== OCR JSON Result ===");
            Console.WriteLine(json);

            Console.WriteLine("\n✅ Conversion complete!");
            Console.WriteLine($"PDF saved to: {pdfPath}");
        }
    }
}
```

### 이것이 작동하는 이유

- **GPU acceleration**는 CPU 전용 모드에 비해 인식 시간을 대략 절반으로 단축합니다.  
- **Deskew**와 **Denoise**는 고전적인 *preprocess image for OCR* 기법으로, 엔진이 문자를 놓치는 일반적인 스캔 결함을 보정합니다.  
- **Language model loading**은 **recognize Korean text image**에 필수적이며, 한국어 모델이 없으면 엔진은 일반 라틴 알파벳으로 대체되어 의미 없는 결과를 생성합니다.  
- **SearchablePdfExporter**는 원본 비트맵과 보이지 않는 텍스트 오버레이를 결합하여, 어떤 PDF 뷰어에서도 색인할 수 있는 **create searchable pdf image** 결과를 제공합니다.

## 이것이 작동하는 이유

- **GPU acceleration**는 CPU‑only 모드에 비해 인식 시간을 대략 절반으로 단축합니다.  
- **Deskew**와 **Denoise**는 고전적인 *preprocess image for OCR* 기술이며, 엔진이 문자를 놓치는 일반적인 스캔 결함을 수정합니다.  
- **Language model loading**은 **recognize Korean text image**에 필수적이며, 한국어 모델이 없으면 엔진은 일반 라틴 알파벳으로 대체되어 무의미한 결과를 생성합니다.  
- **SearchablePdfExporter**는 원본 비트맵과 보이지 않는 텍스트 오버레이를 결합해, 어떤 PDF 뷰어에서도 색인할 수 있는 **create searchable pdf image** 결과를 제공합니다.

## OCR을 위한 이미지 전처리 – 팁과 요령

`DeskewFilter`는 스캔 페이지의 회전을 보정합니다.  
`ContrastFilter`는 이미지 대비를 조정하여 OCR 정확도를 향상시킵니다.  
`BinarizationFilter`는 임계값을 기준으로 이미지를 흑백으로 변환하여 배경 잡음을 줄입니다.  
`OrientationFilter`는 혼합된 세로/가로 페이지를 감지하고 교정합니다.  

| 문제 | 추가 필터 | 추가 방법 |
|-------|-------------------|------------|
| 낮은 대비 | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| 많은 배경 잡음 | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| 혼합된 방향(세로 및 가로) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Note:** 필터를 너무 많이 추가하면 처리 속도가 느려질 수 있습니다. 확장하기 전에 단일 페이지에서 각 변경 사항을 테스트하세요.

## 한국어 텍스트 이미지 인식 – 일반적인 함정

한국어 스크립트는 시각적으로 밀집된 한글 음절을 포함합니다. 깨진 출력이 보이면:

1. **언어 모델이 완전히 다운로드되었는지 확인** – 콘솔에 “Downloading Korean model…”와 같은 메시지가 표시되는지 확인하세요.  
2. 스캔이 12° 이상 회전된 경우 `DeskewFilter`의 `MaxAngle`을 **증가**하세요.  
3. `ocrEngine.GpuMemoryLimit = 2048;` (MB 단위)로 설정하여 **GPU 메모리를 늘리세요**.  

`LanguageModel.Korean`은 OCR을 위한 한국어 데이터를 로드하여 정확한 한글 인식을 가능하게 합니다.  
이러한 조정은 **recognize Korean text image**의 성공에 직접적인 영향을 줍니다.

## 검색 가능한 PDF 이미지 생성 – 결과 검증

프로그램이 완료되면 `korean_page.pdf`를 任意 PDF 리더(Adobe Acrobat Reader, Foxit, 심지어 Chrome)에서 엽니다. 다음을 수행할 수 있어야 합니다:

- **텍스트 선택**: 마우스로 원본 PDF처럼 텍스트를 선택할 수 있습니다.  
- **검색**: 내장 검색 상자를 사용해 한국어 단어를 찾을 수 있습니다.  

텍스트 레이어가 비어 보이면, `Export` 메서드에 올바른 이미지 경로가 전달되었는지와 OCR 결과에 비어 있지 않은 `RecognitionResult.Text`가 포함되어 있는지 다시 확인하세요.

## 전체 JSON 출력 – 기대되는 내용

콘솔에 깔끔하게 포맷된 JSON 페이로드가 출력됩니다. 축소된 예시는 다음과 같습니다:

```json
{
  "Text": "첫 번째 페이지의 내용...",
  "Blocks": [
    {
      "Text": "첫 번째 페이지의 내용...",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 560, "Height": 780 },
      "Confidence": 0.98
    }
  ],
  "Language": "Korean",
  "ProcessingTimeMs": 842
}
```

## 문제 해결 및 FAQ

**Q: 내 PDF가 원본 이미지에 비해 너무 큽니다.**  
A: Exporter는 원본 비트맵을 원래 해상도로 삽입합니다. 크기가 문제라면 인식하기 *전에* 이미지를 다운스케일하세요:

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q: OCR이 빈 문자열을 반환합니다.**  
A: 이미지 경로가 올바른지, 파일이 손상되지 않았는지 확인하세요. 또한 GPU 드라이버가 최신인지 확인하십시오; 오래된 드라이버는 무음 실패를 일으킬 수 있습니다.

**Q: 여러 페이지를 루프에서 처리할 수 있나요?**  
A: 물론 가능합니다. 단계 4‑6을 `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` 루프에 감싸고 출력 PDF 경로를 적절히 변경하세요.

## 결론

우리는 방금 **converted image to PDF**를 수행했으며, 검색 가능한 텍스트를 보존했습니다. 이는 Aspose OCR의 강력한 파이프라인 덕분입니다. **preprocess image for OCR**를 통해 정확도를 높이고, **recognize Korean text image**로 복잡한 스크립트를 처리하며, **create searchable pdf image**를 통해 휴대 가능하고 색인 가능한 문서를 얻습니다.

코드를 가져가 자신의 스캔에 적용하고 추가 필터나 언어 모델을 실험해 보세요. 동일한 패턴은 중국어, 일본어 또는 라틴 기반 언어에도 적용됩니다—단지 `LanguageModel.Korean`을 해당 열거형으로 교체하면 됩니다.

추가 질문이 있나요? 댓글을 남겨 주세요. 즐거운 코딩 되세요!

---

**마지막 업데이트:** 2026-09-13  
**테스트 환경:** Aspose.OCR 24.11 for .NET  
**작성자:** Aspose

## 관련 튜토리얼

- [Aspose Ocr을 사용하여 스캔 파일에서 검색 가능한 PDF 만들기](/ocr/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/)
- [OCR 전처리 파이프라인: 이미지에서 텍스트 인식하는 방법](/ocr/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)
- [Aspose Ocr으로 이미지에서 텍스트 인식하기 - 완전한 C 가이드](/ocr/net/ocr-configuration/recognize-text-from-image-with-aspose-ocr-complete-c-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}