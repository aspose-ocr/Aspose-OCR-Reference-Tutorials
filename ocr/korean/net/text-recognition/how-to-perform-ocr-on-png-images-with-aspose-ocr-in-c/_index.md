---
category: general
date: 2026-11-26
description: Aspose.OCR을 사용하여 PNG 파일에서 OCR을 수행하고, PNG를 텍스트로 변환하며, 키릴 문자 텍스트를 추출하는
  방법을 배우세요 – 개발자를 위한 단계별 가이드.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- convert PNG to text
- recognize text from PNG
- extract Cyrillic text
- load image for OCR
language: ko
lastmod: 2026-11-26
og_description: C#에서 Aspose.OCR을 사용하여 PNG 파일에 대한 OCR을 수행하고 키릴 문자 텍스트를 추출하는 방법. PNG를
  텍스트로 변환하는 전체 튜토리얼을 확인하세요.
og_image_alt: how to perform OCR on a PNG image using Aspose.OCR
og_title: Aspose.OCR를 사용하여 PNG 이미지에서 OCR 수행하는 방법 – C# 가이드
schemas:
- author: Aspose
  dateModified: '2026-11-26'
  description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  headline: How to perform OCR on PNG images with Aspose.OCR in C#
  type: TechArticle
- description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  name: How to perform OCR on PNG images with Aspose.OCR in C#
  steps:
  - name: Handling large images
    text: 'If the PNG is larger than 2 MB, consider down‑scaling it before recognition
      to speed up processing:'
  - name: 'Edge case: Missing language module'
    text: 'If the download fails (e.g., offline environment), the engine throws an
      `OcrException`. Catch it to provide a graceful fallback:'
  - name: Expected output
    text: 'If `sample_image.png` contains the Cyrillic phrase “Привет мир”, the console
      will display:'
  - name: How it works
    text: 1. **Engine creation** – prepares the OCR pipeline. 2. **Image loading**
      – supports both raw PNG and down‑scaled versions for performance. 3. **Language
      selection** – demonstrates **extract Cyrillic text** while handling missing
      modules. 4. **Recognition** – the core **recognize text from PNG** call
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
title: C#에서 Aspose.OCR을 사용하여 PNG 이미지에 OCR 수행하는 방법
url: /ko/net/text-recognition/how-to-perform-ocr-on-png-images-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 Aspose.OCR을 사용하여 PNG 이미지에 OCR 수행하는 방법

PNG 파일에 **OCR 수행 방법**이 필요하다면, 이 가이드는 Aspose.OCR을 사용하여 PNG를 텍스트로 변환하는 정확한 단계를 보여줍니다. 스캔한 문서에서 키릴 문자 텍스트를 추출하든 PNG 스크린샷에서 텍스트를 인식하든, 이 솔루션은 바로 사용할 수 있으며 C# 코드 몇 줄만 필요합니다.

이 튜토리얼에서는 다음을 배웁니다:

* **OCR용 이미지 로드** 로컬 폴더에서,
* 엔진을 구성하여 **키릴 문자 텍스트 추출**,
* **PNG에서 텍스트 인식**하고 깨끗한 문자열을 얻습니다,
* 누락된 언어 모듈 및 큰 이미지와 같은 일반적인 함정을 처리합니다.

Aspose.OCR에 대한 사전 경험은 필요하지 않습니다—단지 .NET 개발 환경과 처리하려는 PNG 이미지만 있으면 됩니다.

## 사전 요구 사항

* .NET 6.0(또는 그 이후 버전) 설치
* **Aspose.OCR for .NET**의 라이선스 또는 평가판 사본. Aspose 웹사이트에서 무료 평가판을 받을 수 있습니다.
* Visual Studio 2022(또는 .NET을 지원하는 모든 IDE)
* 추출하려는 텍스트가 포함된 PNG 파일(`sample_image.png` 사용 예시)

## 단계 1: Aspose.OCR NuGet 패키지 설치

프로젝트 폴더에서 터미널을 열고 다음을 실행합니다:

```bash
dotnet add package Aspose.OCR
```

패키지에는 핵심 OCR 엔진과 모든 언어 모듈이 포함됩니다. 로컬에 없는 언어를 요청하면 Aspose.OCR이 자동으로 필요한 모듈을 다운로드합니다.

## 단계 2: OCR 엔진 인스턴스 생성 (OCR 수행 방법)

OCR 워크플로우에서 첫 번째 실행 가능한 단계는 엔진을 인스턴스화하는 것입니다. 이 객체는 이미지 로드 및 인식 수행과 같은 이후 모든 작업을 관리합니다.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

**왜 중요한가:** `OcrEngine` 클래스는 OCR 파이프라인을 캡슐화합니다. 단일 인스턴스를 생성하고 여러 이미지에서 재사용하면 메모리 오버헤드가 감소하고 성능이 향상됩니다.

## 단계 3: OCR용 이미지 로드 – 소스 PNG 파일 지정

이미지를 로드하는 단계가 바로 **OCR용 이미지 로드**입니다. Aspose.OCR은 여러 입력 유형을 지원하며, 가장 간단한 방법은 `ImageStream.FromFile`입니다.

```csharp
// Load the PNG image from disk
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_image.png");
```

> **프로 팁:** 다양한 환경에서 런타임 오류를 방지하려면 절대 경로나 `Path.Combine`을 사용하세요.

### 큰 이미지 처리

PNG 파일이 2 MB보다 크면 인식 전에 다운스케일하여 처리 속도를 높이는 것을 고려하세요:

```csharp
using System.Drawing;

// Downscale large images to a maximum width of 1200 pixels
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/sample_image.png");
int maxWidth = 1200;
int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

using (var ms = new MemoryStream())
{
    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
    ocrEngine.Image = ImageStream.FromStream(ms);
}
```

## 단계 4: 언어 구성 – 키릴 문자 텍스트 추출

기본적으로 Aspose.OCR은 영어를 가정합니다. **키릴 문자 텍스트 추출**을 위해 `Language` 속성을 `Language.Cyrillic`으로 설정하세요. 필요한 모듈은 코드를 처음 실행할 때 자동으로 다운로드됩니다.

```csharp
// Set the OCR language to Cyrillic
ocrEngine.Language = Language.Cyrillic;
```

여러 언어(예: 영어와 키릴)를 인식해야 하는 경우, 이를 결합할 수 있습니다:

```csharp
ocrEngine.Language = Language.English | Language.Cyrillic;
```

### 예외 상황: 언어 모듈 누락

다운로드가 실패하면(예: 오프라인 환경) 엔진이 `OcrException`을 발생시킵니다. 이를 잡아 우아한 대체 처리를 제공하세요:

```csharp
try
{
    ocrEngine.Language = Language.Cyrillic;
}
catch (OcrException ex)
{
    Console.WriteLine($"Language module could not be loaded: {ex.Message}");
    // Optionally, fall back to English or abort the process
}
```

## 단계 5: 인식 작업 수행 (PNG에서 텍스트 인식)

이미지와 언어가 설정되었으니 **PNG에서 텍스트 인식**을 수행할 수 있습니다. `Recognize` 메서드는 OCR 파이프라인을 동기적으로 실행합니다.

```csharp
// Run OCR
ocrEngine.Recognize();
```

**왜 작동하는가:** 내부적으로 Aspose.OCR은 선택된 언어에 맞게 조정된 신경망 기반 인식기로 이미지를 전달하기 전에 전처리(이진화, 노이즈 제거)를 적용합니다.

## 단계 6: 인식된 텍스트 가져오기 및 표시 (PNG를 텍스트로 변환)

인식이 끝나면 추출된 문자열은 `Text` 속성을 통해 사용할 수 있습니다. 이것이 **PNG를 텍스트로 변환**의 최종 단계입니다.

```csharp
// Get the recognized text
string recognizedText = ocrEngine.Text;

// Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

### 예상 출력

`sample_image.png`에 키릴 구문 “Привет мир”가 포함되어 있으면 콘솔에 다음과 같이 표시됩니다:

```
=== OCR Result ===
Привет мир
```

출력에는 이미지에 나타난 대로 줄 바꿈 및 구두점이 포함될 수 있습니다. 필요에 따라 `String.Trim()`, `Regex` 또는 기타 텍스트 정리 유틸리티로 문자열을 후처리할 수 있습니다.

## 단계 7: 선택 사항 – 결과를 파일에 저장

OCR 결과를 저장하면 후속 처리(예: 인덱싱, 번역)가 가능합니다. 텍스트를 UTF‑8 파일에 쓰는 간단한 방법은 다음과 같습니다:

```csharp
File.WriteAllText(@"YOUR_DIRECTORY/ocr_output.txt", recognizedText, Encoding.UTF8);
Console.WriteLine("OCR text saved to ocr_output.txt");
```

## 일반적인 함정 및 회피 방법

| 문제 | 증상 | 해결 방법 |
|-------|----------|-----|
| **언어 모듈 누락** | `Language = Language.Cyrillic`에서 `OcrException` | 첫 실행 시 인터넷 연결을 확인하거나 Aspose 오프라인 패키지를 통해 모듈을 미리 다운로드하세요. |
| **흐리거나 저대비 이미지** | 정확도 저하, 많은 “?” 문자 | 이미지를 전처리하세요: 대비를 높이고, 샤프닝을 적용하거나 엔진에 전달하기 전에 그레이스케일로 변환합니다. |
| **매우 큰 PNG** | 처리 시간 증가, `OutOfMemoryException` 발생 가능 | Step 3에서와 같이 다운스케일하거나 다중 페이지 이미지를 개별 타일로 분할하세요. |
| **UTF‑8이 아닌 문자** | 깨진 출력 | 콘솔이나 파일 작성기가 UTF‑8 인코딩(`Encoding.UTF8`)을 사용하는지 확인하세요. |

## 전체 실행 가능한 예제

아래는 위의 모든 단계를 포함한 완전한 프로그램입니다. 새 콘솔 프로젝트에 복사하고 파일 경로를 조정한 뒤 실행하세요.

```csharp
using System;
using System.Drawing;
using System.IO;
using System.Text;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1. Create OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2. Load PNG image (with optional down‑scaling for large files)
            string imagePath = @"YOUR_DIRECTORY/sample_image.png";
            Bitmap original = new Bitmap(imagePath);
            const int maxWidth = 1200;

            if (original.Width > maxWidth)
            {
                int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
                Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

                using (var ms = new MemoryStream())
                {
                    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    ocrEngine.Image = ImageStream.FromStream(ms);
                }
            }
            else
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }

            // 3. Set language to Cyrillic (fallback to English if needed)
            try
            {
                ocrEngine.Language = Language.Cyrillic;
            }
            catch (OcrException ex)
            {
                Console.WriteLine($"Failed to load Cyrillic module: {ex.Message}");
                Console.WriteLine("Falling back to English.");
                ocrEngine.Language = Language.English;
            }

            // 4. Recognize text
            ocrEngine.Recognize();

            // 5. Retrieve and display the text (convert PNG to text)
            string recognizedText = ocrEngine.Text;
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);

            // 6. Save result to a UTF‑8 file
            string outputPath = @"YOUR_DIRECTORY/ocr_output.txt";
            File.WriteAllText(outputPath, recognizedText, Encoding.UTF8);
            Console.WriteLine($"OCR text saved to {outputPath}");
        }
    }
}
```

### 작동 방식

1. **엔진 생성** – OCR 파이프라인을 준비합니다.  
2. **이미지 로드** – 성능을 위해 원본 PNG와 다운스케일 버전을 모두 지원합니다.  
3. **언어 선택** – 누락된 모듈을 처리하면서 **키릴 문자 텍스트 추출**을 보여줍니다.  
4. **인식** – 핵심 **PNG에서 텍스트 인식** 호출입니다.  
5. **결과 처리** – **PNG를 텍스트로 변환**을 보여주고 파일에 출력합니다.

`dotnet run`으로 프로그램을 실행하세요. 모든 설정이 올바르면 인식된 텍스트가 콘솔에 출력되고 `ocr_output.txt`에 저장됩니다.

## 결론

이 튜토리얼에서는 Aspose.OCR for .NET을 사용하여 PNG 파일에 **OCR 수행 방법**을 배웠으며, **OCR용 이미지 로드**부터 **키릴 문자 텍스트 추출** 및 **PNG를 텍스트로 변환**까지 모든 과정을 다루었습니다. 완전한 실행 가능한 예제는 표준 워크플로우, 일반적인 예외 상황 및 OCR 파이프라인을 안정적으로 유지하는 실용적인 팁을 보여줍니다.

**다음 단계**

* 추가 언어(아랍어, 중국어)를 `Language` 플래그를 결합하여 **PNG에서 텍스트 인식**을 탐색하세요.  
* 검색 가능한 문서 아카이브를 위해 OCR 결과를 Azure Cognitive Search와 통합하세요.  
* `Resolution`과 같은 Aspose.OCR의 `OcrEngine` 설정을 실험해 보세요.

## 다음에 배울 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료에는 단계별 설명과 함께 완전한 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [C#에서 Aspose.OCR 모델을 다운로드하고 PNG에서 텍스트 추출하는 방법](/ocr/english/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/)
- [C#에서 OCR 수행 – Aspose로 키릴 텍스트 인식하는 방법](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [C#에서 배치 OCR – PNG 파일에서 텍스트를 빠르게 추출하는 방법](/ocr/english/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}