---
category: general
date: 2026-04-26
description: Aspose.OCR을 사용하여 C#에서 이미지에서 텍스트를 추출하고, 이미지를 JSON 및 XML 형식으로 몇 분 안에 변환하는
  방법을 배워보세요.
draft: false
keywords:
- extract text from image
- convert image to json
- convert image to xml
- Aspose OCR C#
- image to JSON C#
- image to XML C#
language: ko
og_description: Aspose.OCR를 사용하여 C#에서 이미지에서 텍스트를 추출합니다. 결과를 즉시 JSON 및 XML로 변환하는 방법을
  단계별로 배워보세요.
og_title: C#에서 이미지에서 텍스트 추출 – JSON 및 XML로 변환
tags:
- OCR
- C#
- Aspose
- JSON
- XML
title: C#에서 이미지의 텍스트 추출 – JSON 및 XML로 변환
url: /ko/net/text-recognition/extract-text-from-image-in-c-convert-to-json-xml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 이미지에서 텍스트 추출 – JSON 및 XML로 변환

.NET 프로젝트에서 **이미지에서 텍스트를 추출**해야 했지만 “실제로 데이터를 어떻게 가져오지?” 라는 부분에서 막힌 적이 있나요? 당신만 그런 것이 아닙니다. 실제 애플리케이션—예를 들어 청구서 처리, 영수증 스캔, 배지 검증—에서 사진에서 원시 문자를 추출하는 것이 첫 번째이자 중요한 단계입니다.  

좋은 소식은? Aspose.OCR을 사용하면 몇 줄의 코드만으로 이를 수행하고, 즉시 **이미지를 JSON으로 변환**하거나 **이미지를 XML로 변환**하여 하위 시스템에 전달할 수 있습니다. 이 가이드에서는 완전한 실행 가능한 코드를 단계별로 살펴보고, 각 부분이 왜 중요한지 설명하며, 일반적인 함정을 피하는 몇 가지 팁을 보여드립니다.

---

## 필요

- **.NET 6+** (최근 SDK이면 모두 작동합니다; 샘플은 .NET 6을 대상으로 합니다)
- **Aspose.OCR for .NET** NuGet 패키지  
  ```bash
  dotnet add package Aspose.OCR
  ```
- 인쇄 가능한 텍스트가 포함된 이미지 파일(PNG, JPG 등); 예제로 `invoice.png`를 사용합니다.
- 코드 편집기—Visual Studio, VS Code, 또는 Rider—원하는 것을 사용하세요.

그게 전부입니다. 추가 OCR 엔진이나 외부 서비스 없이 단일 NuGet 패키지만 있으면 됩니다.

---

## Step 1: OCR 엔진 설정 – 이미지에서 텍스트 추출 방법

먼저 `OcrEngine` 인스턴스를 생성하고 이미지 파일을 지정합니다. 이 단계가 기반이며, 이미지가 올바르게 로드되지 않으면 엔진이 아무것도 인식할 수 없습니다.

```csharp
using Aspose.OCR;
using System.IO;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process
// Replace YOUR_DIRECTORY with the actual folder path
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/invoice.png");

// Optional: verify the image was loaded
if (ocrEngine.Image == null)
{
    throw new FileNotFoundException("Image not found. Check the path and filename.");
}
```

**Why this matters:**  
- `OcrEngine`은 모든 저수준 이미지 전처리(이진화, 기울기 보정)를 캡슐화합니다.  
- `ImageStream.FromFile`을 통해 이미지를 로드하면 엔진이 정확한 바이트를 읽어 DPI와 색 깊이를 보존합니다—두 요소 모두 인식 정확도에 영향을 줄 수 있습니다.  

> **Pro tip:** 소스 이미지가 스트림에 있는 경우(예: 웹 API를 통해 업로드된 경우) `FromFile` 대신 `ImageStream.FromStream(yourStream)`을 사용하세요.

---

## Step 2: 엔진에 기대하는 언어 지정 – 이미지에서 텍스트를 정확히 추출

Aspose.OCR은 다양한 알파벳을 지원합니다. 올바른 언어를 지정하면 문자 집합이 제한되고 정확도가 향상됩니다.

```csharp
// Set the language; Latin covers English, French, German, etc.
ocrEngine.Language = Language.Latin;
```

**Why:**  
`Language.Latin`을 설정하면 OCR 엔진이 키릴 문자나 아시아 글자를 무시해 오탐을 줄입니다. 이후 다국어 문서를 처리해야 하면 `Language.Multilingual`으로 전환하거나 여러 언어를 조합할 수 있습니다.

---

## Step 3: 인식 프로세스 실행 – 한 번의 호출로 이미지에서 텍스트 추출

이제 실제로 텍스트를 인식합니다. `Recognize` 메서드는 원시 텍스트, 신뢰도 점수, 레이아웃 데이터 등을 포함하는 `RecognitionResult` 객체를 반환합니다.

```csharp
// Perform OCR
RecognitionResult recognitionResult = ocrEngine.Recognize();

// Quick sanity check
if (recognitionResult == null || string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text was detected. Verify the image quality.");
    return;
}

// Print the raw extracted text to the console
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(recognitionResult.Text);
```

**Why:**  
`Recognize`를 한 번 호출하면 충분합니다. 엔진이 내부적으로 전처리, 분할, 문자 분류를 수행하기 때문입니다. `Text` 속성은 순수 문자열 형태를 제공하므로 로깅이나 빠른 검증에 적합합니다.

---

## Step 4: 결과를 JSON으로 변환 – 이미지를 쉽게 JSON으로 변환

많은 최신 서비스가 JSON 페이로드를 선호합니다. Aspose.OCR은 신뢰도 값과 경계 상자를 포함한 전체 `RecognitionResult`를 직렬화하는 편리한 `ToJson` 메서드를 제공합니다.

```csharp
// Serialize the result to JSON
string jsonResult = recognitionResult.ToJson();

// Save the JSON to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonResult);

Console.WriteLine("JSON file saved at YOUR_DIRECTORY/invoice.json");
```

**Why you might want JSON:**  
- **Interoperability:** 프런트엔드 앱(React, Angular)이 JSON을 직접 사용할 수 있습니다.  
- **Debugging:** JSON에 문자별 신뢰도가 포함되어 있어 신뢰도가 낮은 단어를 수동 검토 대상으로 표시할 수 있습니다.  

> **Edge case:** 하위 시스템이 순수 텍스트만 필요하면 `recognitionResult.Text`를 추출해 전체 Aspose 페이로드 대신 사용자 정의 JSON 객체에 넣을 수 있습니다.

---

## Step 5: 결과를 XML로 변환 – 레거시 시스템을 위한 이미지 XML 변환

일부 기업은 여전히 데이터 교환을 위해 XML 스키마에 의존합니다. `ToXml` 메서드는 `ToJson`과 동일하지만 XML을 출력합니다.

```csharp
// Serialize the result to XML
string xmlResult = recognitionResult.ToXml();

// Save the XML to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlResult);

Console.WriteLine("XML file saved at YOUR_DIRECTORY/invoice.xml");
```

**Why XML:**  
- **Schema validation:** Aspose가 생성하는 구조와 일치하는 XSD를 정의해 계약 준수를 보장할 수 있습니다.  
- **Integration:** 오래된 ERP 또는 문서 관리 시스템은 종종 XML을 바로 파싱합니다.

---

## 전체 작업 예제 – 원스톱 코드

아래는 모든 요소를 연결한 완전한 프로그램입니다. 새 콘솔 프로젝트(`dotnet new console`)에 복사·붙여넣기하고 실행하세요.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Initialize OCR engine and load the image
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();
            // Adjust the path to point at your PNG/JPG file
            string imagePath = "YOUR_DIRECTORY/invoice.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            if (ocrEngine.Image == null)
            {
                Console.WriteLine($"Unable to load image at {imagePath}");
                return;
            }

            // -------------------------------------------------
            // Step 2: Specify language (Latin for most European scripts)
            // -------------------------------------------------
            ocrEngine.Language = Language.Latin;

            // -------------------------------------------------
            // Step 3: Run OCR and get the result
            // -------------------------------------------------
            RecognitionResult result = ocrEngine.Recognize();

            if (result == null || string.IsNullOrWhiteSpace(result.Text))
            {
                Console.WriteLine("No text detected – check image quality or language setting.");
                return;
            }

            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();

            // -------------------------------------------------
            // Step 4: Convert to JSON (convert image to json)
            // -------------------------------------------------
            string json = result.ToJson();
            string jsonPath = "YOUR_DIRECTORY/invoice.json";
            File.WriteAllText(jsonPath, json);
            Console.WriteLine($"JSON output written to {jsonPath}");

            // -------------------------------------------------
            // Step 5: Convert to XML (convert image to xml)
            // -------------------------------------------------
            string xml = result.ToXml();
            string xmlPath = "YOUR_DIRECTORY/invoice.xml";
            File.WriteAllText(xmlPath, xml);
            Console.WriteLine($"XML output written to {xmlPath}");
        }
    }
}
```

**예상 출력 (콘솔):**

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

JSON file saved at YOUR_DIRECTORY/invoice.json
XML file saved at YOUR_DIRECTORY/invoice.xml
```

JSON 및 XML 파일은 예를 들어 다음과 같은 풍부한 구조를 포함합니다:

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
  "Confidence": 0.96,
  "Blocks": [
    { "Text": "Invoice #12345", "Confidence": 0.98, "Rectangle": { "X": 12, "Y": 30, "Width": 200, "Height": 20 } },
    ...
  ]
}
```

```xml
<RecognitionResult>
  <Text>Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00</Text>
  <Confidence>0.96</Confidence>
  <Blocks>
    <Block>
      <Text>Invoice #12345</Text>
      <Confidence>0.98</Confidence>
      <Rectangle X="12" Y="30" Width="200" Height="20"/>
    </Block>
    ...
  </Blocks>
</RecognitionResult>
```

---

## 자주 묻는 질문 및 엣지 케이스

### 이미지가 흐리거나 회전된 경우는 어떻게 하나요?

Aspose.OCR은 대부분의 이미지를 자동으로 기울기 보정하지만, 극단적인 경우 `ocrEngine.Image = ImageProcessor.Deskew(ocrEngine.Image)`로 사전 처리할 수 있습니다. 약간의 대비 강화(`ImageProcessor.AdjustContrast`)를 추가하면 신뢰도 점수를 향상시킬 수 있습니다.

### PDF에서 텍스트를 추출할 수 있나요?

예—먼저 각 PDF 페이지를 이미지로 변환하고(예: Aspose.PDF 또는 PDFium 같은 무료 라이브러리 사용) 동일한 OCR 흐름에 이미지를 전달하면 됩니다.

### 하나의 문서에서 여러 언어를 처리하려면 어떻게 해야 하나요?

`ocrEngine.Language = Language.Multilingual;`을 설정하거나 특정 언어를 조합합니다:

```csharp
ocrEngine.Language = Language.English | Language.French | Language.German;
```

보다 넓은 언어 집합은

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}