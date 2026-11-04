---
category: general
date: 2026-01-12
description: 텍스트 이미지를 인식하고, C#으로 텍스트 이미지를 추출하며, 신뢰도 점수가 포함된 이미지‑PDF OCR 파일을 생성하는 방법을
  보여주는 C# OCR 튜토리얼.
draft: false
keywords:
- c# ocr tutorial
- image to pdf ocr
- recognize text image
- ocr confidence scores
- extract text image c#
language: ko
og_description: 텍스트 이미지를 인식하고, C#으로 텍스트 이미지를 추출하며, 신뢰도 점수가 포함된 이미지‑PDF OCR 문서를 만드는
  완전한 C# OCR 튜토리얼을 배워보세요.
og_title: c# OCR 튜토리얼 – 이미지를 검색 가능한 PDF로 변환
tags:
- OCR
- C#
- PDF
title: c# OCR 튜토리얼 – 이미지를 검색 가능한 PDF로 변환
url: /ko/net/text-recognition/c-ocr-tutorial-turn-images-into-searchable-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – 이미지 를 검색 가능한 PDF 로 변환

서드파티 서비스를 찾지 않고 C# 프로젝트에서 **텍스트 이미지** 파일을 인식하는 방법을 궁금해 본 적 있나요? 당신만 그런 것이 아닙니다. 실제 애플리케이션—예를 들어 청구서 스캐너, 영수증 트래커, 다국어 문서 아카이브 등—에서 개발자는 신뢰할 수 있는 온프레미스 OCR 엔진이 필요하며, 이 엔진은 신뢰도 점수도 제공해야 합니다.  

이 **c# ocr tutorial**에서는 이미지 로드, 언어 모델 선택, GPU 가속 전환, 결과를 검색 가능한 PDF로 저장하는 전체 과정을 단계별로 안내합니다. 최종적으로 텍스트를 추출하고 OCR 신뢰도를 보고하며, 필요에 따라 *image to pdf ocr* 파일을 생성하는 실행 가능한 코드 샘플을 1분 이내에 만들 수 있습니다.

## 만들게 될 것

- 다중 언어 이미지(`sample_multi_lang.jpg`를 플레이스홀더로 사용)를 로드합니다.  
- 아랍어, 힌디어, 러시아어 언어 모델을 선택합니다(추가 가능).  
- 머신이 지원한다면 GPU 처리를 켭니다.  
- 신뢰도 점수가 포함된 원시 OCR 결과를 가져옵니다.  
- 결과를 보기 좋은 JSON으로 직렬화 **또는** 검색 가능한 PDF로 저장합니다.  

외부 웹 서비스 없이, 숨겨진 마법 없이—단지 Aspose.OCR for .NET, 몇 줄의 C#, 그리고 각 줄이 왜 중요한지에 대한 명확한 설명만 있습니다.

## 전제 조건

- .NET 6.0 이상(코드는 .NET Core와 .NET Framework에서도 컴파일됩니다).  
- Visual Studio 2022(또는 원하는 IDE).  
- Aspose.OCR for .NET 라이선스(무료 체험판으로 테스트 가능).  
- 선택 사항: 인식 속도를 높이고 싶다면 CUDA 호환 GPU.  

> **Pro tip:** GPU가 없으면 `UseGpu = false`로 설정하면 엔진이 코드 변경 없이 CPU로 자동 전환됩니다.

## Step 1: 필요한 NuGet 패키지 설치

**Package Manager Console**을 열고 다음을 실행합니다:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Gpu
Install-Package Newtonsoft.Json
```

이 세 패키지는 OCR 엔진, GPU 가속, 그리고 신뢰도 출력을 위한 깔끔한 JSON 직렬화기를 제공합니다.

## Step 2: 프로젝트 구조 설정

새 콘솔 프로젝트(`dotnet new console -n AsposeOcrDemo`)를 만들고 생성된 `Program.cs`를 아래 코드로 교체합니다. 모든 로직은 `Program` 클래스 안에 있으며, 추가된 타입은 OCR 결과를 JSON으로 포맷하는 작은 확장 메서드뿐입니다.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.Models;
using Newtonsoft.Json;

namespace AsposeOcrDemo
{
    class Program
    {
        // Step 1: Input image and language models
        private const string InputImagePath = @"YOUR_DIRECTORY/sample_multi_lang.jpg";
        private static readonly string[] Languages = { LanguageModel.Arabic, LanguageModel.Hindi, LanguageModel.Russian };

        // Step 2: Processing options (GPU toggle & output format)
        private const bool UseGpu = true;               // set false if no GPU
        private const string OutputFormat = "Json";     // change to "Pdf" for PDF output

        static void Main()
        {
            // Step 3: Initialise the appropriate OCR engine
            IOcrEngine engine = UseGpu ? (IOcrEngine)new GpuOcrEngine() : new OcrEngine();

            // Step 4: Run OCR – language models are auto‑downloaded if missing
            OcrResult result = engine.Recognize(
                InputImagePath,
                new OcrOptions { LanguageModels = Languages, AutoDownloadResources = true });

            // Step 5: Emit the result in the chosen format
            if (OutputFormat.Equals("json", StringComparison.OrdinalIgnoreCase))
            {
                string json = JsonConvert.SerializeObject(
                    result.GetWordsWithConfidence(),
                    Formatting.Indented);
                Console.WriteLine(json);
            }
            else if (OutputFormat.Equals("pdf", StringComparison.OrdinalIgnoreCase))
            {
                string pdfPath = Path.ChangeExtension(InputImagePath, ".pdf");
                File.WriteAllBytes(pdfPath, result.Pdf);
                Console.WriteLine($"PDF saved to: {pdfPath}");
            }
        }
    }

    // Helper that flattens OcrResult into a JSON‑friendly structure
    internal static class OcrResultExtensions
    {
        public static object GetWordsWithConfidence(this OcrResult result)
        {
            var words = new System.Collections.Generic.List<object>();
            foreach (var w in result.Words)
                words.Add(new
                {
                    Text = w.Text,
                    Confidence = w.Confidence,
                    BoundingBox = new { w.Bounds.X, w.Bounds.Y, w.Bounds.Width, w.Bounds.Height }
                });

            return new
            {
                RecognizedText = result.Text,
                LanguageModels = result.UsedLanguageModels,
                Words = words,
                ProcessingTimeMs = result.ProcessingTime.TotalMilliseconds
            };
        }
    }
}
```

### 이 코드가 작동하는 이유

1. **GPU 토글** – `GpuOcrEngine`은 CUDA 코어를 활용합니다; 삼항 연산자를 사용해 전환이 간편합니다.  
2. **자동 언어 다운로드** – `AutoDownloadResources = true`는 처음 실행 시 아랍어, 힌디어, 러시아어 모델을 자동으로 가져옵니다.  
3. **신뢰도 점수** – `result.Words`에는 인식된 각 단어에 대한 `Confidence`가 포함되어 있으며, 확장 메서드가 이를 깔끔한 JSON 객체로 포맷합니다.  
4. **검색 가능한 PDF** – `result.Pdf`는 이미 완전한 검색 가능한 PDF이므로 바이트 배열을 디스크에 쓰기만 하면 됩니다. 추가 라이브러리는 필요 없습니다.

## Step 6: 샘플 실행

터미널을 열고 프로젝트 폴더로 이동한 뒤 다음을 실행합니다:

```bash
dotnet run
```

**JSON** 출력을 선택하면 다음과 같은 결과가 표시됩니다:

```json
{
  "RecognizedText": "مرحبا Hello Привет",
  "LanguageModels": [
    "Arabic",
    "Hindi",
    "Russian"
  ],
  "Words": [
    {
      "Text": "مرحبا",
      "Confidence": 0.98,
      "BoundingBox": { "X": 45, "Y": 12, "Width": 120, "Height": 30 }
    },
    {
      "Text": "Hello",
      "Confidence": 0.99,
      "BoundingBox": { "X": 180, "Y": 12, "Width": 80, "Height": 30 }
    },
    {
      "Text": "Привет",
      "Confidence": 0.97,
      "BoundingBox": { "X": 280, "Y": 12, "Width": 110, "Height": 30 }
    }
  ],
  "ProcessingTimeMs": 312
}
```

**PDF** 로 전환하면 콘솔에 경로가 출력되고 원본 이미지 옆에 검색 가능한 PDF가 생성됩니다.

## 일반적인 질문 및 엣지 케이스

- **언어 모델이 없으면 어떻게 되나요?**  
  OCR 엔진은 명확한 `ResourceNotFoundException`을 발생시킵니다. `AutoDownloadResources = true`로 설정했기 때문에 누락된 모델은 처음 실행 시 자동으로 다운로드되며, 실제 운영 환경에서는 이 예외가 거의 발생하지 않습니다.

- **이미지 배치를 처리할 수 있나요?**  
  가능합니다. `engine.Recognize` 호출을 파일 디렉터리를 순회하는 `foreach` 루프에 감싸면 됩니다. 동일한 `OcrResultExtensions`가 각 이미지에 적용됩니다.

- **GPU 사용에 라이선스가 필요합니까?**  
  필요 없습니다. 무료 체험판은 CPU와 GPU 모두에서 동작합니다. 정식 라이선스는 워터마크를 제거하고 페이지 제한을 해제합니다.

- **신뢰도 점수는 얼마나 정확한가요?**  
  점수는 0.0(전혀 신뢰 없음)부터 1.0(완전 신뢰)까지이며, 실제로는 0.90 이상이면 후속 처리에 충분히 신뢰할 수 있습니다. 더 엄격한 검증이 필요하면 낮은 신뢰도 단어를 필터링하면 됩니다.

## Step 7: 다음 단계 (OCR 툴킷 확장)

1. **언어 추가** – `Languages` 배열에 `LanguageModel.French`(또는 지원되는 모델)를 추가하면 됩니다.  
2. **OCR와 PDF/A 변환 결합** – Aspose.PDF를 사용해 OCR 레이어를 PDF/A‑2b 호환 문서에 삽입해 보관할 수 있습니다.  
3. **Azure Functions와 통합** – 로직을 서버리스 엔드포인트로 래핑해 업로드를 실시간으로 처리합니다.  
4. **신뢰도 임계값 미세 조정** – `result.Words.Where(w => w.Confidence < 0.85)`를 사용해 불확실한 단어를 수동 검토 대상으로 표시합니다.

---

### TL;DR

이 **c# ocr tutorial**에서는 다음을 수행하는 방법을 보여줍니다:

- 이미지를 로드하고 여러 언어 모델을 선택합니다.  
- 단일 불리언 플래그로 GPU 가속을 켭니다.  
- OCR 결과를 **신뢰도 점수와 함께** 가져와 JSON으로 직렬화합니다.  
- 필요에 따라 검색 가능한 PDF(**image to pdf ocr**)를 작성합니다.  

이 모든 작업은 몇 줄의 코드와 무료 Aspose.OCR 체험판만으로 가능합니다. 직접 실행해 보고 언어 목록을 조정하면 몇 분 안에 프로덕션 수준의 OCR 파이프라인을 구축할 수 있습니다.

---

![c# ocr tutorial example image](https://example.com/placeholder-image.jpg "c# ocr tutorial example image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}