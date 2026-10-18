---
category: general
date: 2026-01-02
description: C#에서 Aspose OCR을 사용하여 이미지에서 텍스트를 추출합니다. 이미지를 JSONL 형식으로 빠르고 안정적으로 변환하는
  방법을 배워보세요.
draft: false
keywords:
- extract text from image
- convert image to jsonl
language: ko
og_description: 이미지에서 텍스트를 추출하고 Aspose OCR을 사용해 JSONL 형식으로 변환합니다. 개발자를 위한 단계별 C# 튜토리얼.
og_title: 이미지에서 텍스트 추출 – C#에서 JSONL로 변환
tags:
- C#
- OCR
- Aspose
- JSONL
title: 이미지에서 텍스트 추출 및 JSONL 변환 – C# 가이드
url: /ko/net/text-recognition/extract-text-from-image-and-convert-to-jsonl-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지에서 텍스트 추출 및 JSONL 변환 – 완전한 C# 튜토리얼

이미 **이미지에서 텍스트를 추출**해야 하는데 어떤 라이브러리가 깔끔하고 구조화된 출력을 제공할지 몰라 고민한 적이 있나요? 당신만 그런 것이 아닙니다. 영수증 처리나 문서 디지털화 프로젝트에서 가장 큰 병목은 비트맵을 검색 가능한 텍스트 *및* 기계가 읽을 수 있는 형식으로 변환하는 것입니다.  

좋은 소식은? Aspose OCR을 사용하면 **이미지에서 텍스트를 추출**하고 몇 줄의 코드만으로 **이미지를 JSONL로 변환**하여 하위 분석에 활용할 수 있습니다. 이 가이드는 PNG를 로드하는 단계부터 데이터 파이프라인으로 스트리밍할 수 있는 JSON‑Lines 파일을 작성하는 전체 과정을 안내합니다.

> **힌트:** .NET 6 이상을 이미 사용 중이라면 추가 설정 없이 동일한 코드를 사용할 수 있습니다.

## 사전 요구 사항 — 필요한 것

- **.NET 6 SDK** (또는 최신 .NET 버전)
- **Aspose.OCR** NuGet 패키지  
  ```bash
  dotnet add package Aspose.OCR
  ```
- **Newtonsoft.Json** 직렬화를 위한 패키지  
  ```bash
  dotnet add package Newtonsoft.Json
  ```
- 샘플 이미지 (예: `receipt.png`)를 참조 가능한 폴더에 배치
- 원하는 IDE 또는 편집기—Visual Studio, VS Code, Rider 등

설정이 복잡하지 않으며 외부 서비스도 필요 없습니다. NuGet 패키지만 있으면 됩니다.

![Extract text from image using C#](https://example.com/assets/ocr-sample.png)

*Alt text: Aspose OCR을 사용한 C# 이미지 텍스트 추출*

## 단계 1: 처리할 이미지 로드  

**이미지에서 텍스트를 추출**하려면 먼저 OCR 엔진에 비트맵을 제공해야 합니다. `System.Drawing.Bitmap`을 사용하면 대부분의 래스터 형식에 대해 간단히 처리할 수 있습니다.

```csharp
using System.Drawing;

// Adjust the path to where your receipt.png lives
string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
Bitmap receiptImage = new Bitmap(imagePath);
```

> **왜 중요한가:** 이미지를 `Bitmap`으로 로드하면 OCR 엔진이 픽셀에 직접 접근할 수 있어 원시 바이트 스트리밍보다 인식 속도와 정확도가 향상됩니다.

## 단계 2: JSON‑Lines 출력을 위한 Aspose OCR 구성  

Aspose OCR은 언어, 출력 형식 및 몇 가지 성능 옵션을 지정할 수 있습니다. 여기서는 **JSON‑Lines**(한 줄에 하나의 JSON 객체) 형식을 요청합니다. 이는 이후 라인‑별 처리에 최적입니다.

```csharp
using Aspose.OCR;

// Create the engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine we’re dealing with English text
RecognitionOptions options = new RecognitionOptions
{
    Language = Language.English,
    OutputFormat = OutputFormat.JsonLines   // This is the key for converting image to JSONL
};
```

> **프로 팁:** 다국어 영수증이 필요하면 `Language = Language.Multilingual`을 설정하거나 `Language` 배열을 전달하세요.

## 단계 3: OCR 실행 및 결과 캡처  

이제 실제로 **이미지에서 텍스트를 추출**합니다. `Recognize` 메서드는 `OcrResult` 객체를 반환하며, 여기에는 인식된 텍스트 라인과 해당 경계 상자를 나타내는 `OcrLine` 컬렉션이 포함됩니다.

```csharp
// Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);
```

이 시점에서 `ocrResult.Lines`는 원시 텍스트, 신뢰도 점수, 좌표 등 필요한 모든 정보를 담고 있습니다.

## 단계 4: 라인을 JSON‑Lines로 직렬화  

컬렉션을 보기 좋게 들여쓰기된 JSON 문자열로 변환합니다. JSON‑Lines는 보통 압축된 형태이지만, 들여쓰기를 추가하면 개발 중 파일을 검토하기가 쉬워집니다.

```csharp
using Newtonsoft.Json;

// Serialize each line as a separate JSON object
string jsonLines = JsonConvert.SerializeObject(
    ocrResult.Lines,
    Formatting.Indented
);
```

결과 `jsonLines` 변수는 다음과 같은 형태를 가집니다(예시, 일부만 표시).

```json
{
  "Text": "Store XYZ",
  "Confidence": 0.98,
  "BoundingBox": { "X": 10, "Y": 15, "Width": 120, "Height": 20 }
}
{
  "Text": "Date: 01/01/2026",
  "Confidence": 0.95,
  "BoundingBox": { "X": 10, "Y": 45, "Width": 180, "Height": 20 }
}
```

각 라인은 개행 문자로 끝나므로 진정한 **JSONL**(JSON‑Lines) 파일이 됩니다.

## 단계 5: JSON‑Lines를 디스크에 기록  

마지막으로 출력을 저장해 Spark, Logstash 또는 간단한 Bash 스크립트와 같은 다른 서비스가 라인 단위로 데이터를 읽을 수 있게 합니다.

```csharp
using System.IO;

// Choose a destination file
string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
File.WriteAllText(outputPath, jsonLines);
```

`receipt.jsonl`을 열면 한 줄에 하나의 JSON 객체가 들어 있어 스트리밍 준비가 완료된 것을 확인할 수 있습니다.

## 단계 6: 내보내기 검증  

간단한 검증을 통해 나중에 발생할 디버깅 시간을 크게 절감할 수 있습니다. 처음 몇 줄을 다시 읽어 콘솔에 출력해 보세요.

```csharp
Console.WriteLine("First three lines of the JSONL output:");
foreach (var line in File.ReadLines(outputPath).Take(3))
{
    Console.WriteLine(line);
}
```

전형적인 콘솔 출력:

```
First three lines of the JSONL output:
{"Text":"Store XYZ","Confidence":0.98,"BoundingBox":{"X":10,"Y":15,"Width":120,"Height":20}}
{"Text":"Date: 01/01/2026","Confidence":0.95,"BoundingBox":{"X":10,"Y":45,"Width":180,"Height":20}}
{"Text":"Total   $23.45","Confidence":0.97,"BoundingBox":{"X":10,"Y":75,"Width":150,"Height":20}}
```

비슷한 결과가 보이면 축하합니다—**이미지에서 텍스트를 추출**하고 **이미지를 JSONL로 변환**하는 작업을 성공적으로 마친 것입니다.

## 흔히 발생하는 문제와 해결 방법  

| 문제 | 발생 원인 | 해결 방법 |
|------|----------|----------|
| **빈 출력** | 이미지 경로가 잘못되었거나 파일을 읽을 수 없음 | `File.Exists(imagePath)`를 사용해 비트맵을 만들기 전에 경로를 확인 |
| **낮은 신뢰도 점수** | 이미지가 흐리거나 대비가 낮음 | 이미지 전처리(`Bitmap.RotateFlip`, `Graphics.Clear` 등)하거나 DPI를 높임 |
| **잘못된 언어 설정** | OCR 기본값이 영어이지만 영수증이 다른 언어임 | `options.Language = Language.Spanish`(또는 해당 언어 enum) 설정 |
| **JSONL이 단일 JSON 배열로 보임** | 개행 처리를 하지 않고 `Formatting.None` 사용 | 각 직렬화된 객체 뒤에 `Environment.NewLine`을 추가하도록 보장 |

## 전체 작업 예제  

아래는 완전한 실행 가능한 프로그램입니다. 콘솔 프로젝트에 붙여넣고 **F5**를 눌러 실행하세요.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using Newtonsoft.Json;

namespace OcrToJsonlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the image
            string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }
            Bitmap receiptImage = new Bitmap(imagePath);

            // 2️⃣ Set up OCR options for JSON‑Lines output
            OcrEngine ocrEngine = new OcrEngine();
            RecognitionOptions options = new RecognitionOptions
            {
                Language = Language.English,
                OutputFormat = OutputFormat.JsonLines
            };

            // 3️⃣ Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);

            // 4️⃣ Serialize to JSON‑Lines
            string jsonLines = JsonConvert.SerializeObject(
                ocrResult.Lines,
                Formatting.Indented
            );

            // 5️⃣ Write to file
            string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
            File.WriteAllText(outputPath, jsonLines);
            Console.WriteLine($"✅ JSONL saved to {outputPath}");

            // 6️⃣ Quick verification
            Console.WriteLine("\nFirst three lines of output:");
            foreach (var line in File.ReadLines(outputPath).Take(3))
            {
                Console.WriteLine(line);
            }
        }
    }
}
```

**예상 결과:** `receipt.jsonl` 파일에 한 줄에 하나의 JSON 객체가 저장되며, 각 객체는 `Text`, `Confidence`, `BoundingBox` 필드를 포함합니다. 이제 이 파일을 JSONL을 지원하는 모든 분석 파이프라인에 전달할 수 있습니다.

## 다음 단계 – 기본 OCR을 넘어서는 활용  

- **배치 처리:** 위 로직을 `foreach` 루프로 감싸 영수증 폴더 전체를 처리
- **병렬 처리:** 수천 장의 이미지를 다룰 때 `Parallel.ForEach`를 사용해 멀티코어 가속
- **후처리:** 신뢰도 낮은 라인(`Confidence < 0.9`)을 필터링 후 저장
- **통합:** Azure Blob Storage 또는 AWS S3 SDK를 사용해 JSONL을 직접 업로드
- **대체 형식:** 다운스트림 시스템이 필요로 하면 `OutputFormat`을 `PlainText` 또는 `Xml`로 전환

## 결론  

Aspose OCR과 C#을 이용해 **이미지에서 텍스트를 추출**하고 **이미지를 JSONL로 변환**하는 완전한 엔드‑투‑엔드 솔루션을 이제 갖추었습니다. 이 튜토리얼은 비트맵 로드부터 출력 검증까지 모든 과정을 다루었으며, 파이프라인을 견고하게 유지하기 위한 실용적인 팁도 포함했습니다.

자신만의 영수증, 청구서 또는 스캔된 양식으로 직접 실행해 보세요—OCR 엔진이 픽셀을 몇 초 만에 검색 가능하고 라인‑구조화된 데이터로 변환하는 모습을 확인할 수 있습니다. 스캔이 기울어졌거나 다국어 텍스트가 포함된 경우 *RecognitionOptions* 섹션을 다시 검토하고 언어 또는 전처리 단계를 조정하면 됩니다.

행복한 코딩 되시길, 그리고 데이터 파이프라인이 언제나 깨끗하게 유지되길 바랍니다!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}