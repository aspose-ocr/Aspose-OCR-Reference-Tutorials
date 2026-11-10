---
category: general
date: 2026-05-25
description: 최소한의 ASP.NET Core API로 이미지에서 텍스트를 추출하는 방법을 배웁니다. POST로 이미지를 업로드하고, 멀티파트
  폼 데이터를 읽어 이미지에 OCR을 수행합니다.
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: ko
og_description: 최소한의 ASP.NET Core API를 사용하여 이미지에서 텍스트를 추출합니다. 이 가이드는 POST로 이미지를 업로드하고,
  멀티파트 폼 데이터를 읽으며, 이미지에 OCR을 수행하는 방법을 보여줍니다.
og_title: ASP.NET Core에서 이미지 텍스트 추출 – 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  headline: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  type: TechArticle
- description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  name: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  steps:
  - name: Breaking Down the Logic
    text: '| Step | What Happens | Why It Matters | |------|--------------|----------------|
      | **ReadFormAsync** | Parses the incoming *multipart/form-data* request. | Without
      this, you can’t access the uploaded files. | | **form.Files["image"]** | Retrieves
      the file whose form‑field name is `image`. | Guarant'
  - name: 1. Large Files
    text: 'The default request body limit is 30 MB. For larger scans you might need
      to adjust:'
  - name: 2. Asynchronous OCR
    text: Some OCR libraries expose async methods (`RecognizeAsync`). If yours does,
      replace `ocr.Recognize(img)` with `await ocr.RecognizeAsync(img)` and mark the
      lambda as `async`.
  - name: 3. Security Considerations
    text: '- **Validate file size** before loading it into memory. - **Sanitize the
      filename** if you ever write it to disk. - **Rate‑limit** the endpoint to avoid
      denial‑of‑service attacks.'
  - name: 4. GPU Acceleration
    text: If you uncomment the `engine.GpuDevice = new GpuDevice(0);` line and your
      hardware supports CUDA or DirectML, you’ll see a noticeable speed boost, especially
      on high‑resolution images.
  type: HowTo
tags:
- ASP.NET Core
- OCR
- Minimal API
title: ASP.NET Core Minimal API에서 이미지 텍스트 추출 – 완전 가이드
url: /ko/net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ASP.NET Core Minimal API에서 이미지에서 텍스트 추출 – 완전 가이드

무거운 프레임워크 없이 **이미지에서 텍스트를 추출**하는 방법이 궁금하셨나요? 당신만 그런 것이 아닙니다. 영수증을 스캔하거나 손글씨 메모를 디지털화하거나 검색 인덱스를 구축할 때, 사용자가 사진을 올리고 원시 문자를 바로 받아볼 수 있는 간단한 방법이 필요합니다.

이 튜토리얼에서는 **POST로 이미지 업로드**를 처리하고 *multipart/form‑data* 페이로드를 파싱한 뒤, 싱글톤 `OcrEngine`을 사용해 **이미지에 OCR 수행**하는 작은 ASP.NET Core Minimal API를 만들어 보겠습니다. 최종적으로 .NET 8 프로젝트에 바로 넣어 실행할 수 있는 완전한 앱을 얻을 수 있습니다.

## 만들게 될 내용

- `/ocr` 경로에서 동작하는 최소 웹 앱
- `multipart/form-data` POST 요청으로 전송된 이미지 파일을 받는 엔드포인트
- 업로드된 파일을 읽어 OCR 엔진에 전달하고 평문 텍스트 결과를 반환하는 로직
- 호환 가능한 GPU가 있을 경우 사용할 수 있는 (주석 처리된) GPU 가속 코드 스니펫

**전제 조건**  
- .NET 8 SDK(이상)  
- C#와 커맨드 라인에 대한 기본 지식  
- `OcrEngine` 클래스를 제공하는 OCR 라이브러리(예시에서는 가상의 NuGet 패키지를 가정)  

위 조건을 갖췄다면 바로 시작해 보세요.

## 1단계: 프로젝트 설정 및 OCR 패키지 추가

먼저 새 웹 프로젝트를 만들고 OCR 라이브러리를 가져옵니다.

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **Pro tip:** 의존성을 최신 상태로 유지하세요. 최신 버전은 특히 GPU 가속 추론에서 성능 향상을 제공하는 경우가 많습니다.

## 2단계: 싱글톤 OCR 엔진 등록 (주 서비스)

앱 전체에서 하나의 `OcrEngine` 인스턴스만 사용하도록 합니다—요청마다 새 엔진을 만들 필요가 없습니다. 빌더의 서비스 컨테이너에 등록합니다.

```csharp
using Awesome.Ocr;               // <-- the OCR library namespace
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using System.Drawing;            // System.Drawing.Common for Image handling

var builder = WebApplication.CreateBuilder(args);

// Register a singleton OCR engine (English language)
// Uncomment the GPU line if you have a compatible GPU and the library supports it.
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU acceleration
    return engine;
});
```

**왜 싱글톤인가요?**  
OCR 엔진을 초기화하는 데는 신경망 가중치를 메모리에 로드하는 등 비용이 많이 듭니다. 동일 인스턴스를 재사용하면 CPU 사이클과 RAM을 모두 절약할 수 있어 `/ocr` 호출마다 응답 속도가 빨라집니다.

## 3단계: 애플리케이션 빌드

이제 `WebApplication` 객체를 구체화합니다.

```csharp
var app = builder.Build();
```

이 한 줄은 마법처럼 보이지만, 내부에서는 라우팅, 미들웨어, 그리고 방금 구성한 DI 컨테이너를 연결합니다.

## 4단계: POST 엔드포인트 정의 – “POST로 이미지 업로드”

튜토리얼의 핵심 부분입니다. **POST로 이미지 업로드**를 받고 multipart 페이로드를 파싱한 뒤 OCR 엔진에 전달합니다.

```csharp
app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    // Step 5: Read multipart form data and extract the uploaded image
    var form = await request.ReadFormAsync();               // <-- read multipart/form-data
    var file = form.Files["image"];                         // expects a field named "image"

    if (file is null || file.Length == 0)
    {
        return Results.BadRequest("No image file provided.");
    }

    // Guard against unsupported content types
    if (!file.ContentType.StartsWith("image/"))
    {
        return Results.BadRequest("Uploaded file is not an image.");
    }

    // Load the image into a System.Drawing.Image
    using var img = Image.FromStream(file.OpenReadStream());

    // Step 6: Perform OCR on the image
    string text = ocr.Recognize(img);                       // <-- perform OCR on image

    // Step 7: Return the extracted text as plain‑text
    return Results.Text(text);
});
```

### 로직 상세 분석

| 단계 | 수행 내용 | 이유 |
|------|-----------|------|
| **ReadFormAsync** | 들어오는 *multipart/form-data* 요청을 파싱합니다. | 파일에 접근하려면 반드시 필요합니다. |
| **form.Files["image"]** | 폼 필드 이름이 `image`인 파일을 가져옵니다. | 호출자와의 계약을 명확히 합니다. |
| **Content‑type check** | 파일이 이미지인지 확인합니다(e.g., `image/png`). | OCR 엔진이 비이미지 데이터를 처리하는 것을 방지합니다. |
| **Image.FromStream** | 원시 스트림을 `System.Drawing.Image` 객체로 변환합니다. | OCR 라이브러리는 `Image` 객체를 요구합니다, 바이트 배열이 아니라. |
| **ocr.Recognize(img)** | OCR 엔진을 **이미지에서 텍스트 인식**하도록 호출합니다. | 바로 **이미지에 OCR 수행**하는 핵심 단계입니다. |
| **Results.Text** | 평문 텍스트 응답을 반환합니다. | 다운스트림 서비스가 쉽게 소비할 수 있는 형식입니다. |

## 5단계: API 실행

마지막으로 웹 서버를 시작합니다.

```csharp
app.Run();
```

`dotnet run`을 실행하면 API가 `http://localhost:5000`(또는 지정한 포트)에서 대기합니다. `curl`로 테스트해 보세요:

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**예상 출력:** 콘솔에 인식된 문자들이 출력됩니다. 예시:

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

이미지가 흐리거나 지원되지 않는 언어인 경우 OCR 엔진은 빈 문자열이나 오류 메시지를 반환합니다—실제 서비스에서는 이러한 경우를 적절히 처리해야 합니다.

## 엣지 케이스 및 모범 사례

### 1. 대용량 파일

기본 요청 본문 제한은 30 MB입니다. 더 큰 스캔 파일이 필요하면 다음과 같이 조정합니다:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. 비동기 OCR

일부 OCR 라이브러리는 비동기 메서드(`RecognizeAsync`)를 제공합니다. 해당 메서드가 있다면 `ocr.Recognize(img)`를 `await ocr.RecognizeAsync(img)`로 교체하고 람다를 `async`로 표시하세요.

### 3. 보안 고려 사항

- 메모리로 로드하기 전에 **파일 크기 검증**을 수행합니다.  
- 파일을 디스크에 저장한다면 **파일명 정화**를 합니다.  
- **Rate‑limit**을 적용해 서비스 거부 공격을 방지합니다.

### 4. GPU 가속

`engine.GpuDevice = new GpuDevice(0);` 라인의 주석을 해제하고 하드웨어가 CUDA 또는 DirectML을 지원한다면, 특히 고해상도 이미지에서 눈에 띄는 속도 향상을 경험할 수 있습니다.

## 전체 작동 예제

아래는 새 Minimal API 프로젝트에 그대로 복사해 넣을 수 있는 완전한 `Program.cs`입니다.

```csharp
using Awesome.Ocr;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Http.Features;
using System.Drawing;

var builder = WebApplication.CreateBuilder(args);

// Optional: increase multipart limit for big images
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});

// Register the OCR engine as a singleton
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU if available
    return engine;
});

var app = builder.Build();

app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    var form = await request.ReadFormAsync();
    var file = form.Files["image"];

    if (file is null || file.Length == 0)
        return Results.BadRequest("No image file provided.");

    if (!file.ContentType.StartsWith("image/"))
        return Results.BadRequest("Uploaded file is not an image.");

    using var img = Image.FromStream(file.OpenReadStream());

    // Core OCR operation
    string text = ocr.Recognize(img);

    return Results.Text(text);
});

app.Run();
```

저장하고 `dotnet run`을 실행하면 **이미지에서 텍스트 추출**을 즉시 사용할 수 있습니다.

## 결론

ASP.NET Core Minimal API를 활용해 **이미지에서 텍스트를 추출**하는 **완전한 엔드‑투‑엔드 솔루션**을 살펴보았습니다. 프로젝트 스캐폴딩부터 **싱글톤 OCR 엔진 등록**, **POST로 이미지 업로드** 엔드포인트 구현, **multipart/form-data 읽기**, 그리고 **이미지에 OCR 수행**까지 전 과정을 다루었습니다.

다음 단계로 할 수 있는 일:

- richer한 응답을 위한 JSON 래퍼 추가  
- 추출된 텍스트를 저장할 데이터베이스 연동  
- 다국어 지원 확대 (`OcrLanguage.Spanish` 등)

이 패턴은 마이크로서비스에 그대로 끼워 넣거나 API 게이트웨이 뒤에 배치해도 잘 확장됩니다.

PDF 처리, 배치 작업, GPU 튜닝 등에 대한 질문이 있으면 댓글로 남겨 주세요. 즐거운 코딩 되세요!

## 관련 튜토리얼

- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}