---
category: general
date: 2026-05-21
description: C#를 사용하여 이미지에서 OCR을 수행합니다. OCR을 위한 이미지 로드 방법, PNG에서 텍스트 추출 방법, 그리고 작은
  코드 샘플을 통해 이미지에서 텍스트를 인식하는 방법을 배웁니다.
draft: false
keywords:
- perform OCR on image
- extract text from PNG
- recognize text from image
- load image for OCR
language: ko
og_description: C#에서 이미지를 빠르게 OCR합니다. 이 가이드는 OCR을 위해 이미지를 로드하는 방법, PNG에서 텍스트를 추출하는
  방법, 레이아웃을 고려한 HTML 출력으로 이미지에서 텍스트를 인식하는 방법을 보여줍니다.
og_title: C#로 이미지 OCR 수행 – 전체 프로그래밍 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  headline: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  name: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  steps:
  - name: Load Image for OCR
    text: The line `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");`
      is where we **load image for OCR**. The `ImageStream` helper abstracts away
      file‑format details, so you can feed JPEG, BMP, or TIFF without changing code.
  - name: Extract Text from PNG
    text: 'Once `engine.Recognize()` finishes, the OCR engine holds the recognized
      text internally. You can pull it out as a string if you only need raw text:'
  - name: Recognize Text from Image
    text: 'The `Recognize()` call does the heavy lifting. Under the hood the engine:'
  - name: Handling Layout‑Aware HTML Output
    text: 'Most developers stop at plain text, but the `HtmlSaveOptions` we used let
      you **perform OCR on image** and keep the visual structure intact. Two flags
      matter:'
  - name: Scaling to Multiple Files
    text: 'If you need to **perform OCR on image** files in a folder, wrap the core
      logic in a simple loop:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Aspose.OCR
title: C#로 이미지 OCR 수행 – 완전 단계별 가이드
url: /ko/net/text-recognition/perform-ocr-on-image-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#로 이미지 OCR 수행 – 완전 단계별 가이드

무거운 GUI 없이 **이미지에서 OCR 수행**하는 방법이 궁금하셨나요? 당신만 그런 것이 아닙니다. 영수증을 디지털화하거나 스캔된 양식에서 데이터를 추출하거나 단순히 PNG를 검색 가능한 텍스트로 바꾸고 싶을 때, 몇 줄의 C# 코드만으로 작업을 마칠 수 있습니다.

이 튜토리얼에서는 OCR을 위해 이미지를 로드하고, 이미지에서 텍스트를 인식한 뒤, PNG에서 깨끗한 HTML로 텍스트를 추출하는 과정을 단계별로 살펴봅니다. 마지막에는 **이미지에서 OCR 수행**하고 원본 레이아웃을 보존하는 콘솔 앱을 바로 실행할 수 있게 됩니다.

## 만들게 될 것

- PNG(또는 지원되는 이미지) 파일을 읽는 최소 콘솔 프로그램  
- OCR 엔진을 사용해 **이미지에서 텍스트 인식**  
- 레이아웃을 보존한 HTML로 결과 저장, 원본 이미지 삽입  
- **OCR을 위한 이미지 로드**, **PNG에서 텍스트 추출**, 일반적인 엣지 케이스 처리 방법 소개  

> **전제 조건**  
> - .NET 6.0 SDK 이상(또는 .NET Framework 4.7+ 대상 가능)  
> - NuGet 호환 OCR 라이브러리 – 예제는 *Aspose.OCR* 사용하지만 유사 API를 제공하는 라이브러리라면 모두 동작합니다  
> - 기본적인 C# 지식(특별한 전제는 없음)  

준비되셨나요? 좋습니다—바로 시작해봅시다.

## 이미지 OCR 수행 – 전체 코드 walkthrough

아래는 **완전하고 실행 가능한** 프로그램입니다. 새 콘솔 프로젝트(`dotnet new console`)에 복사‑붙여넣기하고 **F5**를 눌러 실행하세요.

```csharp
using System;
using Aspose.OCR;               // OCR engine namespace
using Aspose.OCR.Models;        // Save options namespace
using Aspose.OCR.ImageProcessing; // Image loading helpers

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine and set the language
            // -------------------------------------------------
            var engine = new OcrEngine
            {
                Language = OcrLanguage.English   // You can change to French, German, etc.
            };

            // -------------------------------------------------
            // Step 2: Load the image for OCR
            // -------------------------------------------------
            // Replace the path with your actual PNG/JPEG/TIFF file.
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");

            // -------------------------------------------------
            // Step 3: Perform OCR recognition
            // -------------------------------------------------
            engine.Recognize();

            // -------------------------------------------------
            // Step 4: Configure HTML save options – keep layout
            // -------------------------------------------------
            var htmlOptions = new HtmlSaveOptions
            {
                PreserveLayout = true,   // Keep columns, tables, and spacing
                EmbedImages = true       // Embed the original PNG inside the HTML
            };

            // -------------------------------------------------
            // Step 5: Save the recognized content as layout‑aware HTML
            // -------------------------------------------------
            engine.Save("YOUR_DIRECTORY/form.html", htmlOptions);

            Console.WriteLine("HTML with layout saved.");
        }
    }
}
```

> **예상 출력**  
> ```
> HTML with layout saved.
> ```  
> 실행이 끝나면 PNG 옆에 `form.html` 파일이 생성됩니다. 브라우저에서 열면 레이아웃은 그대로이지만 텍스트가 선택 가능하고 검색 가능합니다.

### OCR을 위한 이미지 로드

`engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");` 라인이 **OCR을 위한 이미지 로드** 부분입니다. `ImageStream` 도우미는 파일 형식 세부 정보를 추상화하므로 JPEG, BMP, TIFF 등을 코드 변경 없이 그대로 사용할 수 있습니다.  

**그냥 `Bitmap`을 넘기면 안 될까요?**  
많은 OCR SDK가 DPI 메타데이터를 포함한 스트림을 기대하기 때문입니다. 라이브러리 내장 로더를 사용하면 엔진이 화면에 표시되는 그대로의 이미지를 보게 되어 정확도가 향상됩니다.

#### Pro tip
여러 파일을 처리한다면 로드 단계를 `try/catch` 로 감싸고 `FileNotFoundException`을 로그에 남기세요. 하나의 파일이 없다고 전체 배치가 중단되는 일을 방지할 수 있습니다.

### PNG에서 텍스트 추출

`engine.Recognize()` 가 끝나면 OCR 엔진은 내부에 인식된 텍스트를 보관합니다. 원시 텍스트만 필요하다면 문자열로 바로 꺼낼 수 있습니다:

```csharp
string plainText = engine.Text;   // Returns the whole document as plain text
Console.WriteLine(plainText);
```

레이아웃이 필요 없을 때 **PNG에서 텍스트 추출**하는 가장 빠른 방법입니다. 대부분의 데이터 입력 작업에서는 일반 텍스트면 충분하니, CSV로 가져갈 경우 줄바꿈을 적절히 정리하는 것을 잊지 마세요.

### 이미지에서 텍스트 인식

`Recognize()` 호출이 실제 작업을 수행합니다. 내부적으로 엔진은 다음을 수행합니다.

1. 이미지를 정규화(기울기 보정, 노이즈 제거)  
2. 라인과 단어로 세분화  
3. 수백만 개의 글리프로 학습된 신경망 분류기 실행  

`Language = OcrLanguage.English` 로 설정했기 때문에 영어 전용 사전이 적용되어 오탐이 크게 감소합니다. 다국어가 필요하면 언어 배열을 전달하면 됩니다:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

### 레이아웃 인식 HTML 출력 처리

대부분의 개발자는 평문 텍스트에 머무르지만, 여기서 사용한 `HtmlSaveOptions` 로 **이미지에서 OCR 수행**하면서 시각적 구조를 그대로 유지할 수 있습니다. 중요한 두 플래그는 다음과 같습니다.

- `PreserveLayout = true` – 컬럼, 테이블, 간격을 유지합니다.  
- `EmbedImages = true` – 원본 PNG를 Base64‑인코딩된 `<img>` 요소로 삽입해 HTML이 자체 포함형이 됩니다.

파일 크기를 줄이고 싶다면 `EmbedImages = false` 로 설정하면 HTML이 디스크에 있는 원본 PNG를 참조합니다.

#### 엣지 케이스: 대용량 파일

이미지 크기가 5 MB를 초과하면 임베딩으로 HTML 용량이 급증할 수 있습니다. 이 경우 외부 이미지 참조로 전환하고 `ImageProcessor.Compress` 로 PNG를 미리 압축하는 것을 고려하세요.

## 흔히 마주치는 문제와 Pro Tips

| 증상 | 가능 원인 | 해결 방법 |
|--------|--------------|-----|
| 문자 깨짐 | 잘못된 언어 설정 또는 언어 팩 누락 | 해당 언어 데이터 파일을 설치하고 `engine.Language` 를 올바르게 설정 |
| 출력에 텍스트 없음 | 이미지가 너무 어둡거나 해상도 낮음 | `engine.Image = ImageProcessor.AdjustContrast(engine.Image, 1.2)` 로 전처리 |
| HTML 레이아웃 깨짐 | `PreserveLayout` 이 기본값 `false` 로 남아 있음 | `HtmlSaveOptions` 에서 `PreserveLayout = true` 로 설정 |
| 다수 페이지 처리 시 느림 | 파일당 엔진을 재초기화 | 동일 `OcrEngine` 인스턴스를 재사용하고 루프마다 `engine.Image` 만 교체 |

### 다수 파일에 대한 확장

폴더에 있는 **이미지에서 OCR 수행** 파일들을 처리하려면 핵심 로직을 간단한 루프로 감싸면 됩니다:

```csharp
foreach (var file in Directory.GetFiles("YOUR_DIRECTORY", "*.png"))
{
    engine.Image = ImageStream.FromFile(file);
    engine.Recognize();
    var htmlPath = Path.ChangeExtension(file, ".html");
    engine.Save(htmlPath, htmlOptions);
    Console.WriteLine($"Processed {Path.GetFileName(file)}");
}
```

루프 안에서 **OCR을 위한 이미지 로드**를 수행하지만 `engine` 과 `htmlOptions` 객체는 재사용합니다. 이렇게 하면 메모리 사용량이 줄고 배치 작업 속도가 빨라집니다.

## 한 단계 더: PDF 또는 DOCX로 내보내기

동일 `engine` 으로 다른 포맷도 저장할 수 있습니다:

```csharp
engine.Save("output.pdf", new PdfSaveOptions { PreserveLayout = true });
engine.Save("output.docx", new WordSaveOptions { PreserveLayout = true });
```

다운스트림 시스템이 검색 가능한 PDF를 요구한다면 한 줄만 바꾸면 됩니다—별도의 변환 파이프라인이 필요 없습니다.

## 결론

우리는 C#으로 **이미지에서 OCR 수행**하는 전체 과정을 살펴보았습니다. 이미지 로드부터 **PNG에서 텍스트 추출**, 그리고 레이아웃을 보존한 HTML 파일 생성까지 모든 단계가 포함된 실행 가능한 예제를 제공했습니다. 이제 각 단계의 의미와 언어별 튜닝 방법, 주의해야 할 함정들을 이해했으니 자유롭게 응용해 보세요.

다음 단계로는 영어 대신 다른 로케일을 시도해 보거나 `PreserveLayout = false` 로 가벼운 HTML을 생성해 보세요. 혹은 평문 출력을 데이터베이스에 저장해 검색 가능한 아카이브를 만들 수도 있습니다. 강력한 OCR 엔진과 몇 줄의 C# 코드만 있으면 가능성은 무한합니다.

멀티 페이지 TIFF 처리 방법이 궁금하거나 이를 ASP.NET Core API에 통합하고 싶다면 아래 댓글에 남겨 주세요. 즐거운 코딩 되세요!

## 관련 튜토리얼

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}