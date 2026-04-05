---
category: general
date: 2026-04-04
description: C# 예제를 사용하여 OCR 엔진으로 TIFF 파일에서 텍스트를 추출하는 방법을 배우세요. JSON 및 XML 출력이 포함된
  단계별 가이드.
draft: false
keywords:
- extract text from tiff
- ocr engine example
- Aspose OCR C#
- multi‑page TIFF OCR
- JSON OCR result
language: ko
og_description: C#에서 OCR 엔진을 사용하여 TIFF 파일에서 텍스트를 추출하는 예제. 자세한 단계, 전체 코드, 그리고 JSON/XML
  출력에 대한 팁.
og_title: Aspose OCR 엔진으로 TIFF에서 텍스트 추출 – 전체 가이드
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Aspose OCR 엔진을 사용하여 TIFF에서 텍스트 추출 – 완전한 예제
url: /ko/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-engine-complete-examp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFF에서 텍스트 추출 – C# 전체 OCR 엔진 예제

멀티‑페이지 파일을 처리할 수 있는 라이브러리를 찾느라 고민했던 적이 있나요? 특히 **TIFF에서 텍스트를 추출**해야 하는데 복잡한 우회 방법이 필요했을 때 말이죠. 여러분만 그런 것이 아닙니다. 많은 레거시 시스템에서는 문서가 멀티‑페이지 TIFF 스캔 형태로 들어오며, 원시 텍스트를 추출하는 기능은 검색, 규정 준수, 데이터 입력 자동화 등에 필수적입니다.

좋은 소식은? Aspose OCR을 사용하면 몇 줄의 코드만으로도 가능하니 저수준 픽셀 버퍼를 직접 다룰 필요가 없습니다. 이 튜토리얼에서는 멀티‑페이지 TIFF를 로드하고, 모든 페이지를 인식한 뒤, 깔끔하게 포맷된 JSON과 선택적인 XML을 출력하는 **전체 OCR 엔진 예제**를 단계별로 안내합니다. 끝까지 따라오면 몇 초 만에 TIFF 파일에서 텍스트를 추출하는 C# 콘솔 앱을 바로 실행할 수 있습니다.

## 배울 내용

- .NET 프로젝트에 Aspose OCR 엔진을 설정하는 방법  
- 멀티‑페이지 TIFF 파일에서 **텍스트를 추출**하는 정확한 코드  
- JSON과 XML 출력 중 어떤 것을 선택해야 하는지, 그리고 두 가지 모두 생성하는 방법  
- 일반적인 문제점(예: 이미지 DPI, 메모리 사용량) 해결 팁  

### 사전 요구 사항

- .NET 6.0 SDK 이상(.NET Core 및 .NET Framework에서도 동작)  
- 유효한 Aspose OCR 라이선스(또는 무료 체험 키)  
- Visual Studio 2022 또는 선호하는 C# 편집기  
- 예제에 사용된 샘플 멀티‑페이지 TIFF 파일(`multi-page.tiff`)  

> **프로 팁:** 예산이 빠듯하다면 무료 체험으로도 월 최대 100페이지까지 텍스트를 추출할 수 있어 테스트에 충분합니다.

---

## Step 1 – OCR 엔진 초기화 (ocr engine example)

**TIFF에서 텍스트를 추출**하려면 먼저 OCR 엔진 인스턴스를 만들어야 합니다. 이 객체는 나중에 조정할 수 있는 모든 설정(언어, 해상도 등)을 보관합니다.

```csharp
using Aspose.OCR;
using System.IO;

// Create a new OCR engine – this is the core of our ocr engine example
var ocrEngine = new OcrEngine();

// Optional: set language if you know the document’s language
// ocrEngine.Language = Language.English;
```

*왜 중요한가:* `OcrEngine` 클래스는 복잡한 작업을 추상화합니다. 엔진을 한 번 인스턴스화하고 여러 이미지에 재사용하면 페이지당 새 엔진을 생성하는 것보다 메모리 효율이 높습니다.

---

## Step 2 – 멀티‑페이지 TIFF 로드 (extract text from TIFF)

이제 엔진에 소스 파일을 지정합니다. `ImageStream.FromFile`은 TIFF, JPEG, PNG 등 다양한 형식을 지원하지만, 이번 튜토리얼에서는 TIFF에 집중합니다.

```csharp
// Load the multi‑page TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi-page.tiff");
```

> **Note:** `YOUR_DIRECTORY`를 실제 머신의 폴더 경로로 교체하세요.  
> **Tip:** TIFF의 DPI가 낮은 경우(150 이하) OCR 정확도를 높이기 위해 사전 처리하는 것을 고려하세요.

---

## Step 3 – 모든 페이지 인식

`Recognize()`를 호출하면 TIFF의 **모든 페이지**에 대해 OCR 알고리즘이 실행됩니다. 결과 객체에는 원시 텍스트, 신뢰도 점수, 페이지별 구분 정보가 포함됩니다.

```csharp
// Run OCR on the loaded image – this extracts text from all pages
var ocrResult = ocrEngine.Recognize();
```

*돌려받는 내용:* `ocrResult`는 `PageResult` 객체 컬렉션을 보유합니다. 각 페이지 텍스트는 `ocrResult.Pages[i].Text`를 통해 접근할 수 있습니다. 엔진은 또한 신뢰도 수준을 제공하므로 품질 검증에 활용할 수 있습니다.

---

## Step 4 – 결과를 JSON(및 선택적 XML)으로 저장

현대 파이프라인은 대부분 JSON을 선호하지만, 레거시 시스템은 아직도 XML을 사용합니다. 두 형식을 깔끔하게 포맷해서 생성하는 방법은 다음과 같습니다.

```csharp
// Convert the recognition result to pretty‑printed JSON
string jsonResult = ocrResult.ToJson(prettyPrint: true);
File.WriteAllText(@"YOUR_DIRECTORY/result.json", jsonResult);

// Optional: also output XML for older workflows
string xmlResult = ocrResult.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY/result.xml", xmlResult);
```

### 샘플 JSON 출력 (일부만 표시)

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
      "Confidence": 0.97
    },
    {
      "PageNumber": 2,
      "Text": "Itemized List\n1. Widget A – $500.00\n2. Widget B – $750.00",
      "Confidence": 0.95
    }
  ]
}
```

JSON은 사람이 읽기 쉬워 디버깅이 간편합니다. 필요하다면 XML도 동일한 구조로 제공됩니다.

---

## Step 5 – 추출 결과 확인 (extract text from TIFF)

파일이 저장된 뒤 간단한 검증을 통해 문제가 없는지 확인합니다.

```csharp
// Load the JSON back just to confirm it was saved correctly
string loadedJson = File.ReadAllText(@"YOUR_DIRECTORY/result.json");
Console.WriteLine("First 200 characters of JSON output:");
Console.WriteLine(loadedJson.Substring(0, Math.Min(200, loadedJson.Length)));
```

콘솔에 스니펫이 출력되면 **TIFF에서 텍스트를 성공적으로 추출**하고 저장한 것입니다. 이제 JSON을 검색 인덱스, 데이터베이스 또는 기타 다운스트림 서비스에 전달할 수 있습니다.

---

## 왜 Aspose OCR을 사용해 TIFF에서 텍스트를 추출해야 할까?

- **멀티‑페이지 지원 기본 제공** – TIFF를 직접 분할할 필요 없음  
- **고정밀도** – 자체 신경망 모델 덕분에 높은 정확도 제공  
- **크로스‑플랫폼** – Windows, Linux, macOS .NET 런타임 모두에서 동작  
- **다양한 출력 형식**(JSON, XML, plain text)으로 최신 및 레거시 스택 모두에 적합  

아직 고민 중이라면 샘플 문서로 무료 체험을 해보세요. 오픈소스 대안에 비해 속도와 간편함을 직접 체감할 수 있을 것입니다.

---

## 흔히 겪는 문제와 해결 방법

| 문제 | 증상 | 해결 방법 |
|------|------|-----------|
| Low‑resolution TIFF | 문자 누락, 낮은 신뢰도 | OCR 전에 이미지를 ≥150 DPI로 확대 (`ocrEngine.Image = ImageStream.FromFile(...).Resize(150)` ) |
| Wrong language | 특히 비영어 텍스트에서 글자가 깨짐 | `ocrEngine.Language = Language.Spanish`(또는 적절한 언어) 를 `Recognize()` 전에 설정 |
| Out‑of‑memory on huge files | `OutOfMemoryException` | 페이지를 배치 처리: `ocrEngine.Image.Pages`를 순회하며 `RecognizePage(i)` 호출 |
| License not applied | 출력에 “Evaluation” 워터마크 | 라이선스 등록: `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## 전체 작업 예제 (복사‑붙여넣기 바로 사용)

아래는 새 콘솔 프로젝트에 바로 넣을 수 있는 완전한 프로그램입니다. 초기화, 로드, 인식, 저장까지 논의한 모든 부분이 포함되어 있습니다.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialize the OCR engine (ocr engine example)
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // Optional: set license if you have one
            // var license = new License();
            // license.SetLicense("Aspose.OCR.lic");

            // -------------------------------------------------
            // 2️⃣  Load the multi‑page TIFF (extract text from TIFF)
            // -------------------------------------------------
            string tiffPath = @"YOUR_DIRECTORY/multi-page.tiff";
            if (!File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -------------------------------------------------
            // 3️⃣  Recognize every page
            // -------------------------------------------------
            var ocrResult = ocrEngine.Recognize();

            // -------------------------------------------------
            // 4️⃣  Save JSON (pretty) and optional XML
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/result.json";
            string jsonResult = ocrResult.ToJson(prettyPrint: true);
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"JSON saved to {jsonPath}");

            // Optional XML output
            string xmlPath = @"YOUR_DIRECTORY/result.xml";
            string xmlResult = ocrResult.ToXml();
            File.WriteAllText(xmlPath, xmlResult);
            Console.WriteLine($"XML saved to {xmlPath}");

            // -------------------------------------------------
            // 5️⃣  Quick verification (extract text from TIFF)
            // -------------------------------------------------
            string preview = jsonResult.Length > 200 ? jsonResult.Substring(0, 200) + "..." : jsonResult;
            Console.WriteLine("\nPreview of JSON output:");
            Console.WriteLine(preview);
        }
    }
}
```

파일을 `Program.cs`로 저장하고 `dotnet run`을 실행하면 콘솔에 JSON과 XML이 저장된 경로가 표시됩니다. 이제 **OCR 엔진 예제**를 완료하고 TIFF에서 텍스트를 추출한 것입니다.

---

## 다음 단계 및 관련 주제

- **배치 처리:** 위 로직을 `foreach` 루프로 감싸서 수십 개의 TIFF 파일을 자동으로 처리  
- **검색 연동:** JSON을 Elasticsearch 또는 Azure Cognitive Search에 푸시해 스캔 문서에 대한 전체 텍스트 검색 구현  
- **이미지 사전 처리:** Aspose `ImageProcessing` API를 활용해 기울기 보정, 잡음 제거, 대비 조정 등 OCR 전처리 수행  
- **대체 출력:** 메타데이터가 필요 없을 경우 `ocrResult.ToPlainText()`를 사용해 순수 문자열만 얻기  

다른 이미지 형식이 궁금하다면 동일한 패턴을 PDF(소스 파일만 교체)나 PNG에도 적용할 수 있습니다. 핵심은 엔진을 한 번 설정하면 이후 과정은 반복 가능한 파이프라인이 된다는 점입니다.

---

## 결론

우리는 Aspose OCR을 사용해 **TIFF에서 텍스트를 추출**하고, 깔끔한 JSON 및 선택적인 XML을 출력하는 **전체 OCR 엔진 예제**를 단계별로 살펴보았습니다. 코드는 독립형이며, 각 단계 뒤에 “왜”라는 설명을 포함해 이해를 돕습니다.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}