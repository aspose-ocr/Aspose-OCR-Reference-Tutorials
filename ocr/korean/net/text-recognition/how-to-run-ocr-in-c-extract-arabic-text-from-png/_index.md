---
category: general
date: 2026-01-10
description: 이미지에서 OCR을 빠르게 실행하고 아랍어 텍스트를 추출하는 방법. 이미지를 텍스트로 변환하고 PNG에서 텍스트를 읽는 방법을
  배우며, Aspose OCR을 사용해 텍스트를 추출하는 방법을 확인하세요.
draft: false
keywords:
- how to run OCR
- extract arabic text
- convert image to text
- read text from png
- how to extract text
language: ko
og_description: C#에서 OCR을 실행하고 PNG 이미지에서 아랍어 텍스트를 추출하는 방법. 이 가이드는 이미지를 텍스트로 변환하고 PNG에서
  텍스트를 단계별로 읽는 방법을 보여줍니다.
og_title: C#에서 OCR 실행하기 – PNG에서 아랍어 텍스트 추출
tags:
- OCR
- C#
- Aspose
title: C#에서 OCR 실행하기 – PNG에서 아랍어 텍스트 추출
url: /ko/net/text-recognition/how-to-run-ocr-in-c-extract-arabic-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 OCR 실행하기 – PNG에서 아랍어 텍스트 추출

아랍어 문자가 포함된 사진에서 **OCR을 실행하는 방법**을 궁금해 본 적 있나요? 당신만 그런 것이 아닙니다. 많은 개발자들이 PNG에서 **아랍어 텍스트를 추출**해야 할 때, 오른쪽에서 왼쪽으로 쓰는 스크립트를 문제 없이 처리할 라이브러리를 몰라 난관에 부딪히곤 합니다.  

이 튜토리얼에서는 **이미지를 텍스트로 변환**, **PNG에서 텍스트 읽기**, 그리고 최종적으로 Aspose.OCR을 사용해 **텍스트를 추출하는 방법**을 깔끔한 C# 콘솔 앱에서 단계별로 안내합니다. 끝까지 따라오면 아랍어 문자열을 터미널에 바로 출력하는 실행 준비가 된 프로그램을 얻게 됩니다.

## 배울 내용

- Aspose.OCR NuGet 패키지를 설치하고 참조하기.  
- 아랍어 지원을 위해 OCR 엔진을 구성하기.  
- PNG 이미지를 로드하고 인식 프로세스를 실행하기.  
- 추출된 텍스트를 가져와 표시하기.  
- 정확도를 높이기 위해 설정을 조정하고 일반적인 함정을 처리하기.

OCR에 대한 사전 경험은 필요 없으며, C#에 대한 기본 이해와 .NET 개발 환경(Visual Studio, Rider, 혹은 `dotnet` CLI)만 있으면 됩니다.

---

## OCR 실행하기 – Aspose OCR 설정

### 단계 1: Aspose.OCR NuGet 패키지 추가

우선 필요한 것은 OCR 라이브러리 자체입니다. Aspose.OCR은 상용 제품이지만, 학습 목적에 완벽히 사용할 수 있는 무료 체험판을 제공합니다.

```bash
# Using the .NET CLI
dotnet add package Aspose.OCR
```

또는 Visual Studio에서 **NuGet 패키지 관리자**를 열고 **Aspose.OCR**을 검색한 뒤 **설치**를 클릭합니다.

> **Pro tip:** 라이브러리를 CI 파이프라인에서 사용할 계획이라면 버전을 고정하기 위해 `-v` 플래그를 추가하세요. 예: `dotnet add package Aspose.OCR -v 23.10`.

### 단계 2: 새 콘솔 프로젝트 만들기 (프로젝트가 없을 경우)

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
```

이제 코드를 넣을 새 `Program.cs` 파일이 준비되었습니다.

---

## 아랍어 텍스트 추출 – OCR 코드 작성

아래는 완전한 실행 가능한 프로그램입니다. `Program.cs`로 저장하거나 자동 생성된 파일을 교체하세요.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Config;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // Step 2: Choose the language for recognition.
            // Here we use Arabic. You can swap this for
            // OcrLanguage.Korean, OcrLanguage.SerbianCyrillic, etc.
            // -------------------------------------------------
            ocrEngine.Language = OcrLanguage.Arabic;

            // -------------------------------------------------
            // Step 3: Load the image containing the text.
            // Replace the path with the location of your PNG.
            // -------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/arabic_sample.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // Step 4: Run the OCR process.
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 5: Display the extracted text.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Arabic Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### 각 라인이 중요한 이유

- **`OcrEngine`**: 이미지 로드, 언어 선택, 인식을 조정하는 핵심 클래스입니다.  
- **`Language = OcrLanguage.Arabic`**: 아랍어는 오른쪽에서 왼쪽으로 쓰이며 고유한 글리프를 사용합니다; 언어를 설정하면 엔진이 올바른 문자 모델을 적용합니다.  
- **`ImageStream.FromFile`**: PNG, JPEG, BMP 등 다양한 포맷을 처리합니다. `MemoryStream`(예: 업로드된 파일)에서 읽어야 할 경우 이 호출을 교체하면 됩니다.  
- **`Recognize()`**: 픽셀 분석, 분할, 문자 분류 등 무거운 작업을 수행합니다.  
- **`ocrEngine.Text`**: 최종 Unicode 문자열로, 추가 처리, 저장 또는 표시가 가능합니다.

### 예상 출력

`arabic_sample.png`에 “مرحبا بالعالم”(Hello World) 문구가 포함되어 있으면, 콘솔에 다음과 같이 출력됩니다:

```
=== Extracted Arabic Text ===
مرحبا بالعالم
```

출력이 깨져 보이면, 이미지가 선명한지, 언어가 아랍어로 설정되었는지, OCR 엔진 버전이 문서와 일치하는지 다시 확인하세요.

---

## 이미지에서 텍스트로 변환 – 정확도 조정

기본 설정은 대부분의 깨끗한 스캔에 잘 작동하지만, 실제 이미지에서는 추가적인 조정이 필요할 때가 많습니다.

| Setting | What It Does | When to Use |
|---------|--------------|-------------|
| `ocrEngine.Config.Preprocess = true` | 자동 이진화와 노이즈 제거를 활성화합니다. | 그림자 있는 스캔 문서. |
| `ocrEngine.Config.Deskew = true` | 약간 기울어진 이미지를 회전시켜 교정합니다. | 각도 잡힌 사진. |
| `ocrEngine.Config.PageSegMode = PageSegMode.SingleBlock` | 전체 이미지를 하나의 텍스트 블록으로 처리합니다. | 간단한 캡션이나 한 줄 라벨. |
| `ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزس شصضطظعغفقكلمنهوية"` | 아랍어 문자만 인식하도록 제한합니다. | 혼합 언어 페이지에서 오탐을 줄일 때. |

엔진을 만든 직후에 다음 라인을 추가할 수 있습니다:

```csharp
ocrEngine.Config.Preprocess = true;
ocrEngine.Config.Deskew = true;
ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزسشصضطظعغفقكلمنهوية";
```

---

## PNG에서 텍스트 읽기 – 다양한 이미지 소스 처리

때때로 PNG가 데이터베이스에 저장되어 있거나 웹 요청으로 들어올 수 있습니다. `byte[]`에서 읽는 간단한 예시는 다음과 같습니다:

```csharp
byte[] pngBytes = File.ReadAllBytes("YOUR_DIRECTORY/arabic_sample.png");
using var ms = new MemoryStream(pngBytes);
ocrEngine.Image = ImageStream.FromStream(ms);
ocrEngine.Recognize();
Console.WriteLine(ocrEngine.Text);
```

나머지 흐름은 동일하게 유지되므로, **텍스트를 추출하는 방법**은 소스에 관계없이 일관됩니다.

---

## 텍스트 추출 방법 – 고급 옵션 및 엣지 케이스

### 1. 다중 페이지 PDF 또는 TIFF

다중 페이지 문서를 OCR해야 한다면, 각 페이지를 반복하면 됩니다:

```csharp
var pdfDoc = new Aspose.Pdf.Document("multi_page.pdf");
foreach (var page in pdfDoc.Pages)
{
    using var img = page.ConvertToImage();
    ocrEngine.Image = ImageStream.FromBitmap(img);
    ocrEngine.Recognize();
    Console.WriteLine($"Page {page.Number}: {ocrEngine.Text}");
}
```

> **Note:** 이 스니펫을 사용하려면 `Aspose.PDF` 패키지가 필요합니다.

### 2. 언어 자동 감지

Aspose.OCR은 자동 감지도 제공하지만 속도가 느립니다. 이미지에 아랍어 또는 다른 스크립트가 포함되어 있는지 확신이 서지 않을 경우 이를 활성화하세요:

```csharp
ocrEngine.Language = OcrLanguage.AutoDetect;
```

엔진은 각 언어 모델을 시도해 가장 적합한 것을 선택합니다.

### 3. 성능 팁

- **`OcrEngine`** 객체를 여러 이미지에 재사용하세요; 매번 새 인스턴스를 만들면 오버헤드가 발생합니다.  
- **병렬 실행**은 스레드당 별도의 엔진 인스턴스가 있을 때만 수행하세요—하나의 인스턴스를 공유하면 레이스 컨디션이 발생합니다.

---

## 결론

우리는 C#에서 **OCR을 실행하는 방법**을 처음부터 끝까지 다루었으며, **아랍어 텍스트 추출**, **이미지를 텍스트로 변환**, **PNG에서 텍스트 읽기**, 그리고 다양한 상황에서 **텍스트를 추출하는 방법**을 보여주었습니다. 샘플 코드는 완전하고 독립적이며, 어떤 .NET 콘솔 프로젝트에든 붙여넣을 준비가 되어 있습니다.

다음 단계는? `OcrLanguage.Arabic`을 한국어나 세르비아어 키릴 문자 등으로 바꿔서 라이브러리의 다국어 기능을 확인해 보세요. 전처리 플래그를 실험해 노이즈가 많은 스캔의 정확도를 높이거나, OCR 루틴을 웹 API에 통합해 사용자가 이미지를 업로드하고 즉시 텍스트 결과를 받을 수 있도록 해보세요.

코딩을 즐기세요, 그리고 OCR 결과가 언제나 선명하기를 바랍니다!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}