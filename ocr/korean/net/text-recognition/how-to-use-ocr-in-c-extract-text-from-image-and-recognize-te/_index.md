---
category: general
date: 2026-02-13
description: C#에서 OCR을 사용하여 이미지에서 텍스트를 추출하고, 사진이나 JPG에서 텍스트를 인식하며, 인터넷 없이 이미지에서 OCR을
  실행하는 방법.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from photo
- recognize text from jpg
- run OCR on image
language: ko
og_description: C#에서 OCR을 사용하여 이미지에서 텍스트를 추출하고, 사진에서 텍스트를 인식하며, 완전하고 실행 가능한 예제로 이미지에
  OCR을 적용하는 방법.
og_title: C#에서 OCR 사용 방법 – 이미지에서 텍스트 추출
tags:
- OCR
- C#
- Image Processing
title: C#에서 OCR 사용 방법 – 이미지에서 텍스트 추출 및 사진에서 텍스트 인식
url: /ko/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-and-recognize-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 OCR 사용 방법 – 이미지에서 텍스트 추출 및 사진에서 텍스트 인식

스크린샷, 스캔한 영수증, 혹은 휴대폰으로 찍은 임의의 사진에서 단어를 추출하기 위해 **OCR을 어떻게 사용하는지** 궁금해 본 적 있나요? 당신만 그런 것이 아닙니다. 실제 애플리케이션에서는 사진을 검색 가능한 텍스트로 변환해야 할 때가 많으며, 인터넷 연결이 불안정한 상황에서도 로컬에서 처리하려면 퍼즐처럼 느껴질 수 있습니다.

그래서 이 가이드는 C# OCR 엔진을 사용해 **이미지에서 텍스트 추출**하는 단계별 방법을 보여주고, **사진에서 텍스트 인식**, **JPG에서 텍스트 인식**, 그리고 디스크에 바로 있는 **이미지에서 OCR 실행**까지 다룹니다. 끝까지 따라 하면 바로 사용할 수 있는 완전한 복사‑붙여넣기 가능한 프로그램을 얻을 수 있습니다.

## 배울 내용

- Simplified Chinese(간체 중국어) 혹은 원하는 다른 언어에 맞게 OCR 엔진을 설정하는 방법  
- 네트워크 호출 없이 로컬 폴더에서 **리소스 로드**에 필요한 정확한 코드  
- JPEG, PNG, BMP와 같은 **사진 파일에서 텍스트 인식** 방법  
- 모델 파일이 없거나 지원되지 않는 이미지 형식과 같은 일반적인 에지 케이스 처리 팁  
- Visual Studio에 바로 넣어 실행할 수 있는 전체 실행 예제

### 전제 조건

- .NET 6.0 이상 (여기서 사용한 API는 .NET Standard 2.0을 대상으로 하므로 이전 버전에서도 동작합니다)  
- C# 및 Visual Studio(또는 선호하는 IDE)에 대한 기본 지식  
- 사용 중인 OCR 라이브러리(예제에서는 언어 모델과 함께 제공되는 가상의 `OcrEngine` 클래스를 가정)  
- 필요한 언어 모델 파일이 들어 있는 폴더 – 엔진이 한자를 읽는 “두뇌” 역할을 합니다

> **Pro tip:** 아직 중국어 모델 파일이 없다면, 공급업체 사이트에서 한 번 다운로드 받아 `C:\OcrResources`와 같은 폴더에 넣어 두세요. 이후엔 엔진이 다시 온라인에 접속할 필요가 없습니다.

---

![사진에서 OCR 프로세스를 보여주는 다이어그램](path/to/ocr-diagram.png "사진에서 OCR 프로세스를 보여주는 다이어그램")

## OCR 사용 방법: 엔진 설정하기

먼저, 사용하려는 언어에 맞게 구성된 OCR 엔진 인스턴스를 만들어야 합니다. 이 튜토리얼에서는 **Simplified Chinese**를 대상으로 하지만, `OcrLanguage.ChineseSimplified`를 `OcrLanguage.English`(또는 다른 enum 값)으로 바꾸는 것만으로도 한 줄로 전환할 수 있습니다.

```csharp
using System;
using YourOcrLibrary;   // Replace with the actual namespace of your OCR SDK

// Step 1: Create and configure the OCR engine for Simplified Chinese
var ocrEngine = new OcrEngine
{
    // Primary keyword appears here naturally
    Language = OcrLanguage.ChineseSimplified,

    // Point to a folder that already contains the Chinese model files
    ResourceFolder = @"C:\OcrResources"
};
```

**왜 중요한가요:**  
`Language` 속성을 설정하면 엔진이 어떤 문자 집합을 기대해야 하는지 알게 됩니다. `ResourceFolder`는 엔진이 신경망 가중치와 언어 사전을 찾는 위치이며, 즉 두뇌의 메모리 뱅크와 같습니다. 잘못된 폴더를 지정하면 엔진이 `FileNotFoundException`을 발생시키고 작업이 중단됩니다.

## 이미지에서 텍스트 추출 – 리소스 로드하기

엔진이 실제로 텍스트를 읽기 전에 모델 파일들을 메모리로 로드해야 합니다. 이 단계는 **매번 이미지 처리 시 네트워크 호출을 피**하기 때문에 매우 중요합니다.

```csharp
// Step 2: Load the language resources from the specified folder (no internet required)
try
{
    ocrEngine.LoadResources();
    Console.WriteLine("Resources loaded successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to load OCR resources: {ex.Message}");
    // In a real app you might fallback to a default language or abort gracefully
}
```

**어떤 문제가 발생할 수 있나요?**  
폴더 경로가 틀리거나 파일이 손상된 경우 `LoadResources()`가 예외를 발생시킵니다. 위의 `try/catch` 블록은 프로덕션 환경에서 자주 필요하게 되는 우아한 오류 처리 방식을 보여줍니다.

## 사진에서 텍스트 인식 – OCR 실행하기

이제 재미있는 부분입니다: 이미지 파일을 엔진에 전달하고 인식된 텍스트를 받아오는 과정입니다. 이는 **이미지에서 OCR 실행** 시나리오의 핵심이며, JPEG, PNG, BMP 등 어떤 형식이든 동일하게 동작합니다.

```csharp
// Step 3: Recognize text from an image file
string imagePath = @"C:\OcrResources\photo.jpg";

try
{
    var recognitionResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(recognitionResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
}
```

`RecognizeImage` 메서드는 일반적으로 다음과 같은 정보를 담은 `RecognitionResult`(또는 SDK에서 정의한 이름)를 반환합니다.

- `Text` – 순수 텍스트 전사  
- `Confidence` – 각 라인에 대한 엔진의 신뢰도 점수(숫자)  
- `BoundingBoxes` – 선택 사항으로, 각 단어가 이미지 내에 위치한 좌표

**Confidence가 왜 중요한가요:**  
데이터 입력 자동화 도구를 만든다면, 신뢰도가 낮은(예: 0.85 이하) 라인에 대해 사용자가 확인하도록 할 수 있습니다. 이렇게 하면 전체 정확도가 크게 향상됩니다.

## JPG에서 텍스트 인식 – 다양한 포맷 처리하기

많은 개발자가 OCR은 PNG 전용이라고 생각하지만, 최신 엔진은 **JPG** 파일도 충분히 처리합니다. 단, JPEG 압축으로 인한 아티팩트가 모델을 혼란스럽게 만들 수 있다는 점만 주의하면 됩니다.

```csharp
// Bonus: Recognize text from a JPG with optional preprocessing
string jpgPath = @"C:\OcrResources\scanned_doc.jpg";

// Optional: use a simple image‑preprocess step to improve accuracy
var preprocessed = ImageHelper.DenoiseAndDeskew(jpgPath); // pseudo‑method
var result = ocrEngine.RecognizeImage(preprocessed);
Console.WriteLine($"Detected text ({result.Confidence:P0} confidence):");
Console.WriteLine(result.Text);
```

`DenoiseAndDeskew` 헬퍼가 없다면 OpenCvSharp 같은 라이브러리에서 해당 기능을 제공하니 활용하세요. 핵심 포인트는 **이미지에서 OCR 실행** 전에 스캐너나 휴대폰 카메라에서 나온 사진을 약간 정리해 주는 것입니다.

## 이미지에서 OCR 실행 – 팁, 에지 케이스, 모범 사례

### 1. 메모리 관리
대형 언어 모델을 로드하면 수백 메가바이트가 사용될 수 있습니다. 작업이 끝난 뒤에는 엔진을 반드시 Dispose하세요.

```csharp
ocrEngine.Dispose(); // or using statement if the SDK implements IDisposable
```

### 2. 배치 처리
수십 장의 사진을 처리해야 한다면, 리소스를 한 번만 로드하고 루프를 돌면 됩니다.

```csharp
string[] files = Directory.GetFiles(@"C:\BatchPhotos", "*.jpg");
foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), res.Text);
}
```

### 3. 다국어 시나리오
`ocrEngine.Language`를 재할당하고 `LoadResources()`를 다시 호출하면 언어를 즉시 전환할 수 있습니다. 다만 로드 시간이 추가로 소요된다는 점을 유념하세요.

### 4. 빈 결과 처리
엔진이 빈 문자열을 반환하는 경우가 있습니다. 이는 보통 이미지가 너무 흐리거나 텍스트 색상이 배경과 섞였을 때 발생합니다. 간단히 확인하는 방법:

```csharp
if (string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text detected – consider increasing image contrast.");
}
```

### 5. 보안 고려 사항
사용자가 업로드한 파일을 바로 OCR 엔진에 전달하면 안 됩니다. 최소한 파일 확장자와 크기를 검증하고, 악성코드 검사를 수행하는 것이 좋습니다.

---

## 전체 동작 예제

아래 코드는 새 콘솔 앱 프로젝트에 복사해 넣을 수 있는 단일 파일 프로그램입니다. **OCR 사용 방법**, **이미지에서 텍스트 추출**, **사진에서 텍스트 인식**, **JPG에서 텍스트 인식**, 그리고 **이미지에서 OCR 실행**을 한 번에 보여줍니다.

```csharp
// File: Program.cs
using System;
using System.IO;
using YourOcrLibrary; // Replace with actual namespace

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // ------------------------------
            // 1️⃣ Configure the OCR engine
            // ------------------------------
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified,
                ResourceFolder = @"C:\OcrResources"
            };

            // Load language resources (no internet needed)
            try
            {
                ocrEngine.LoadResources();
                Console.WriteLine("Resources loaded.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Failed to load resources: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Recognize text from a photo (JPG in this case)
            // -------------------------------------------------
            string imagePath = @"C:\OcrResources\photo.jpg";

            if (!File.Exists(imagePath))
            {
                Console.Error.WriteLine($"Image not found: {imagePath}");
                return;
            }

            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("\n=== OCR Output ===");
                Console.WriteLine(result.Text);
                Console.WriteLine($"\nConfidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"OCR error: {ex.Message}");
            }

            // Clean up
            ocrEngine.Dispose();
        }
    }
}
```

**예상 출력(예시):**

```
Resources loaded.

=== OCR Output ===
中华人民共和国
北京
2026年02月13日

Confidence: 92.45%
```

실제 출력은 이미지 내용에 따라 달라지지만, 콘솔에 유니코드 문자 블록과 함께 신뢰도 퍼센트가 표시될 것입니다.

---

## 결론

C#에서 **OCR을 어떻게 사용하는지**를 처음부터 끝까지 살펴보았습니다—엔진 설정, 언어 리소스 로드, 그리고 인터넷에 전혀 연결하지 않고 **사진**이나 **JPG** 파일에서 **텍스트 인식**까지. 위 단계를 따라 하면 **이미지에서 텍스트 추출**하고 **이미지에서 OCR 실행**하는 완전한 프로그램을 만들 수 있으며, 초보자가 흔히 마주하는 함정도 피할 수 있습니다.

다음 도전 과제가 준비됐나요? 엔진에 PDF 페이지를 이미지로 변환해 넣어 보거나, 다른 언어 팩을 사용해 보면서 신뢰도 점수가 어떻게 변하는지 실험해 보세요. 여러분은

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}