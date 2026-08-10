---
category: general
date: 2026-03-17
description: c# OCR 튜토리얼 – 이미지 파일에서 텍스트를 추출하고, WebP 사진에서 텍스트를 읽으며, 간단한 OcrEngine을
  사용해 이미지를 텍스트로 변환하는 방법을 알아보세요.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: ko
og_description: C# OCR 튜토리얼은 이미지 파일에서 텍스트를 추출하고, WebP 사진에서 텍스트를 읽으며, 몇 줄의 코드로 이미지를
  텍스트로 변환하는 방법을 보여줍니다.
og_title: c# OCR 튜토리얼 – 이미지를 몇 분 안에 텍스트로 추출하기
tags:
- C#
- OCR
- Image Processing
title: 'C# OCR 튜토리얼: 이미지(WebP, 사진)에서 텍스트 추출 – 빠른 가이드'
url: /ko/net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

final output with translated Korean text, preserving markdown.

Let's craft translation.

Be careful with bold and blockquote formatting.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR 튜토리얼 – 이미지에서 텍스트 추출 (WebP, 사진)

이미지 파일에서 **텍스트를 추출**해야 했지만 C#에서 어디서 시작해야 할지 몰랐던 적이 있나요? WebP 스크린샷, 영수증의 JPEG, 혹은 스캔한 PDF 페이지가 있고 그 안의 단어만 원한다면, 이 **c# OCR tutorial**에서는 사진에서 텍스트를 읽고, WebP 및 기타 최신 포맷을 처리하며, 이미지를 일반 텍스트로 변환하는 완전한 실행 가능한 예제를 단계별로 살펴보겠습니다—몇 줄의 코드만으로 가능합니다.

**무엇을 얻을 수 있나요?** 텍스트가 포함된 사진을 검색 가능한 문자열로 변환하고, 데이터베이스에 저장하거나 downstream AI 파이프라인에 전달할 수 있습니다. 마법은 없고, 견고한 OCR 엔진과 몇 가지 .NET API, 그리고 각 단계 뒤에 숨은 “왜”에 대한 명확한 설명만 있으면 됩니다.

## 필요 사항

- **.NET 6 SDK** (또는 그 이후 버전). 아래 코드는 .NET 6+에서 컴파일되며 Windows, Linux, macOS에서 실행됩니다.
- **Visual Studio 2022** 또는 선호하는 편집기 (VS Code도 괜찮습니다).
- **`Microsoft.Windows.SDK.Contracts`** NuGet 패키지 (`Windows.Media.Ocr` 제공). 설치 방법:

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- 처리하고 싶은 이미지 파일 – 이번 튜토리얼에서는 `YOUR_DIRECTORY` 폴더에 위치한 **WebP** 사진 `photo.webp`를 사용합니다.

> Pro tip: 비 Windows 플랫폼을 사용 중이라면 `OcrEngine`을 **Tesseract** 같은 크로스‑플랫폼 라이브러리로 교체할 수 있습니다. 주변 코드는 거의 그대로 유지됩니다.

## 단계 1: C# OCR 튜토리얼 프로젝트 설정

먼저 새 콘솔 앱을 만듭니다. 터미널을 열고 다음을 실행하세요:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

위에서 보여준 대로 필요한 패키지를 추가하고 IDE에서 프로젝트를 엽니다. 이 스캐폴딩은 **c# OCR tutorial**을 위한 깨끗한 시작점을 제공합니다.

## 단계 2: 네임스페이스 가져오기 및 이미지 준비

`OcrEngine`, `SoftwareBitmap`, 이미지 로딩 헬퍼를 찾을 수 있도록 몇 개의 `using` 지시문이 필요합니다.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **왜 이 네임스페이스인가요?**  
> `Windows.Media.Ocr`는 실제 인식을 수행하는 `OcrEngine` 클래스를 포함합니다. `Windows.Graphics.Imaging`은 이미지를 (WebP 포함) `SoftwareBitmap`으로 디코딩해 엔진이 이해할 수 있게 합니다. `System.IO`와 `Windows.Storage.Streams` 헬퍼는 파일 로딩을 간편하게 해줍니다.

이제 이미지를 로드합니다. 내장 디코더는 WebP, HEIF, PNG, JPEG 등을 처리할 수 있어 **WebP에서 텍스트를 읽는** 데 별도 플러그인이 필요 없습니다.

```csharp
// Step 2: Load the image file into a SoftwareBitmap
string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

// Open the file as a random access stream
using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
{
    // Decode the image (auto-detects format)
    BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
    SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();
    
    // Optional: Convert to grayscale for better OCR accuracy
    SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);
    
    // Pass the bitmap to the next step
    await RecognizeTextAsync(grayBitmap);
}
```

> **엣지 케이스:** 이미지가 이미 흑백이라면 변환 단계를 건너뛸 수 있습니다. 그레이스케일 변환은 작은 성능 향상을 제공하고 잡음이 많은 사진의 인식률을 높이는 경우가 많습니다.

## 단계 3: OCR 엔진 실행 – 사진에서 텍스트 인식

여기가 **c# OCR tutorial**의 핵심입니다. `OcrEngine` 인스턴스를 만들고 비트맵을 전달한 뒤 인식된 텍스트를 추출합니다.

```csharp
static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
{
    // Step 3: Create the OCR engine instance – it automatically picks the best language
    OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

    if (ocrEngine == null)
    {
        Console.WriteLine("❌ No OCR engine available for the current language.");
        return;
    }

    // Perform recognition
    OcrResult ocrResult = await ocrEngine.RecognizeAsync(bitmap);

    // Step 4: Display the extracted text – this is the “convert image to text” part
    Console.WriteLine("📝 Recognized text:");
    Console.WriteLine(ocrResult.Text);
}
```

**무슨 일이 일어나고 있나요?**  
- `TryCreateFromUserProfileLanguages()`는 Windows 사용자 프로필에 설정된 언어를 선택합니다. 일반적으로 영어, 스페인어 등을 포함합니다. 특정 언어가 필요하면 `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))`를 사용하세요.  
- `RecognizeAsync`는 백그라운드 스레드에서 무거운 작업을 수행하고, 원시 문자열, 단어 경계 상자, 신뢰도 점수를 포함한 `OcrResult`를 반환합니다.  
- 마지막으로 `ocrResult.Text`를 출력해 **이미지를 텍스트로 변환**한 결과를 다른 곳에 파이프할 수 있습니다.

## 단계 4: 전체 실행 가능한 예제

모든 코드를 합치면 `Program.cs`에 복사‑붙여넣기 할 수 있는 독립형 프로그램이 됩니다. 컴파일하고 실행하면 `photo.webp`에서 추출한 텍스트가 출력됩니다.

```csharp
// Program.cs – Complete c# OCR tutorial example
using System;
using System.IO;
using System.Threading.Tasks;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Replace with your actual directory and file name
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"❗ Image not found: {imagePath}");
            return;
        }

        // Load and optionally preprocess the image
        using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
        {
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Convert to grayscale – improves OCR accuracy on many photos
            SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);

            // Run OCR
            await RecognizeTextAsync(grayBitmap);
        }
    }

    static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
    {
        // Create OCR engine (auto‑detect language)
        OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

        if (ocrEngine == null)
        {
            Console.WriteLine("❌ Unable to create OCR engine. Ensure language packs are installed.");
            return;
        }

        // Perform recognition
        OcrResult result = await ocrEngine.RecognizeAsync(bitmap);

        // Output the extracted text
        Console.WriteLine("\n--- OCR Output ---");
        Console.WriteLine(result.Text);
        Console.WriteLine("--- End of Output ---\n");
    }
}
```

### 예상 출력

`photo.webp`에 “Hello, world! This is a test.” 라는 문장이 들어 있다면 다음과 비슷한 결과가 표시됩니다:

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

줄 바꿈은 원본 이미지 레이아웃에 따라 달라지지만, **이미지에서 텍스트 추출** 결과는 언제나 추가 가공이 가능한 일반 문자열입니다.

## 일반적인 질문 및 엣지 케이스

### 다른 이미지 포맷에서도 작동하나요?

물론입니다. 사용된 디코더(`BitmapDecoder`)는 JPEG, PNG, BMP, GIF, **WebP**, HEIF 등을 자동 감지합니다. 따라서 코드를 수정하지 않고도 **WebP**, JPEG, 혹은 TIFF에서도 텍스트를 읽을 수 있습니다.

### OCR 엔진이 낮은 신뢰도를 반환하면 어떻게 하나요?

`ocrResult.Lines`와 각 `OcrWord`의 `ConfidenceScore`를 확인하세요. 점수가 임계값(예: 0.6) 이하라면 다음을 고려합니다:

- 이미지 전처리 (대비 증가, 샤프닝, 디스큐)
- 고해상도 원본 이미지 사용
- 다국어 지원이 필요한 경우 **Tesseract** 같은 전용 라이브러리로 전환

### 동일 이미지에서 여러 언어를 처리하려면?

언어별로 별도의 `OcrEngine` 인스턴스를 만들고 순차적으로 실행하거나, 혼합 언어 감지를 지원하는 라이브러리를 사용합니다. 내장 엔진의 경우 `Language` 객체를 전달하면 됩니다:

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### Linux/macOS에서도 실행할 수 있나요?

`Windows.Media.Ocr` API는 Windows 전용입니다. 비 Windows 환경에서는 OCR 부분을 **Tesseract**(`Tesseract.Net.SDK` 사용)로 교체하면 됩니다. 로딩 및 전처리 코드는 동일하게 유지되므로 이 **c# OCR tutorial**의 나머지 부분은 그대로 적용됩니다.

## 정확도 향상을 위한 프로 팁

- 큰 이미지는 긴 쪽을 최대 2000 px로 **리사이즈**하세요 – OCR 엔진이 중간 크기에서 더 빠르게 동작합니다.  
- 사진이 거칠면 간단한 가우시안 블러로 **노이즈 제거**를 수행하세요.  
- 텍스트가 완전히 수평이 아니면 비트맵을 **디스큐**하세요; `SoftwareBitmap`을 회전한 뒤 `OcrEngine`에 전달하면 됩니다.  
- 배치로 많은 이미지를 처리한다면 `OcrEngine` 인스턴스를 **캐시**하세요; 반복 생성은 오버헤드를 증가시킵니다.

## 탐색할 관련 주제

- **Tesseract**를 사용한 **이미지를 텍스트로 변환** – 크로스‑플랫폼 프로젝트용  
- **PDF에서 텍스트 추출** – 각 페이지를 이미지로 렌더링 후 OCR 적용  
- **배치 OCR**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}