---
category: general
date: 2026-10-11
description: Aspose.OCR를 사용하여 C#에서 이미지에 대한 OCR을 수행하는 방법을 배우세요. 여기에는 System.Drawing.Common
  설치와 JPG 파일에서 텍스트 추출이 포함됩니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: ko
lastmod: 2026-10-11
og_description: C#에서 Aspose.OCR을 사용하여 이미지에 OCR을 수행합니다. 이 가이드는 System.Drawing.Common을
  설치하고, OCR을 위해 이미지를 로드하며, JPG에서 텍스트를 추출하는 방법을 보여줍니다.
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: C#에서 이미지에 OCR 수행 – 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Aspose.OCR를 사용하여 C#에서 이미지에 OCR 수행하는 방법
url: /ko/net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 Aspose.OCR을 사용하여 이미지에 OCR 수행하는 방법

If you need to **perform OCR on image** files in a .NET application, this guide shows you a complete solution. Using Aspose.OCR you can quickly **recognize text from picture** files such as JPGs and display the result in a console window.

You will learn how to:

* **install System.Drawing.Common package** – `Image` 클래스를 제공하는 라이브러리,
* **load image for OCR** – JPEG 또는 PNG를 메모리로 읽기,
* 언어 모델 구성,
* **perform OCR on image** 그리고 마지막으로,
* **extract text from JPG** 및 출력.

The steps are written for .NET 6+, but they also work with .NET Framework 4.6.1 or later.

---

## 사전 요구 사항

| 요구 사항 | 중요한 이유 |
|-------------|----------------|
| .NET 6 SDK (or .NET Framework 4.6.1+) | C# 콘솔 앱의 런타임을 제공합니다. |
| Visual Studio 2022 (or any IDE) | NuGet 패키지를 추가하고 프로그램을 실행하기 쉽게 해줍니다. |
| Internet connection (first run only) | Aspose.OCR이 언어 모듈을 자동으로 다운로드합니다. |
| A sample image containing Cyrillic or Latin text (e.g., `sample_cyrillic.jpg`) | **extract text from JPG** 를 시연하는 데 사용됩니다. |

---

## 1단계: System.Drawing.Common 패키지 설치

The `System.Drawing.Common` NuGet package supplies the `Image` class that you will **load image for OCR**. Open the Package Manager Console and run:

```powershell
Install-Package System.Drawing.Common
```

> **Pro tip:** Linux/macOS에서 플랫폼‑특정 경고가 발생하면 `net6.0-windows`를 대상으로 설정하거나 프로젝트 파일에 `<UseWindowsForms>true</UseWindowsForms>`를 추가하십시오.

---

## 2단계: Aspose.OCR NuGet 패키지 추가

Aspose.OCR contains the OCR engine and language models. Install it with:

```powershell
Install-Package Aspose.OCR
```

The package is lightweight; the required language data (e.g., Cyrillic) is downloaded the first time you set `OcrEngine.Language`.

---

## 3단계: 이미지 로드 방법 (**load image for OCR**)

Loading the picture is the first concrete step before you can **perform OCR on image**. The `Image.FromFile` method reads any format supported by GDI+, including JPG, PNG, BMP, and TIFF.

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*If the file does not exist, `FileNotFoundException` is thrown – wrap the call in a try/catch block for production code.*

---

## 4단계: 엔진 구성 및 **perform OCR on image**

Create an `OcrEngine` instance, select the language model, assign the loaded image, and call `Recognize()`.

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

The `Recognize()` method returns an `OcrResult` object that holds the extracted text, confidence scores, and bounding boxes. The language module is downloaded automatically on first use, so no extra files are required.

---

## 5단계: **extract text from JPG** 및 표시

Now you can **recognize text from picture** and output the result. The `Text` property of `OcrResult` contains the plain string.

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### 예상 콘솔 출력

```
Recognized text:
Пример текста на кириллице
```

If the source image contains English text, the output will be the English sentence you placed in the picture.

---

## 엣지 케이스 및 모범 사례 팁

| 상황 | 권장 사항 |
|-----------|----------------|
| **Large images ( > 5 MB )** | OCR 전에 가장 긴 변을 ≤ 2000 px로 이미지 크기를 조정하여 메모리 사용량을 줄이고 속도를 향상시킵니다. |
| **Multiple languages in one picture** | `ocrEngine.AddLanguage(OcrLanguage.English)`를 Cyrillic 외에 호출하고, `ocrEngine.Language = OcrLanguage.Multilingual`로 설정합니다. |
| **Low‑contrast scans** | 비트맵을 엔진에 전달하기 전에 `System.Drawing.Graphics`를 사용해 대비를 높입니다. |
| **Running on Linux/macOS** | `libgdiplus` 네이티브 종속성이 설치되어 있는지 확인합니다 (`sudo apt-get install -y libgdiplus`). |
| **Repeated OCR calls** | 같은 `OcrEngine` 인스턴스를 재사용하고 `ocrEngine.Image`만 교체하여 모듈 로드를 반복하지 않도록 합니다. |

---

## 전체 실행 가능한 프로그램

Below is the complete console application that incorporates all previous steps. Copy the code into a new C# console project, replace the image path, and run it.

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Running the program** 은 인식된 문자열을 콘솔에 출력하여 **performed OCR on image** 와 **extracted text from JPG** 를 성공적으로 수행했음을 확인합니다.

---

## 결론

You now know how to **perform OCR on image** files in C# using Aspose.OCR, from installing the required **System.Drawing.Common package** to **load image for OCR**, selecting the appropriate language, and finally **extract text from JPG**. This end‑to‑end example gives you a solid foundation for building more advanced document‑processing pipelines, such as batch‑processing folders of pictures or integrating OCR into a web API.

### 다음 단계는?

* **recognize text from picture** 를 PDF에서 탐색하려면 각 페이지를 먼저 이미지로 변환하세요.
* `OcrEngine` 속성 `Resolution`, `Threshold`, `MaxProcessingTime`을 실험하여 노이즈가 많은 스캔의 정확도를 미세 조정합니다.
* OCR 출력을 자연어 처리 라이브러리와 결합하여 추출된 콘텐츠를 자동으로 분류합니다.

Feel free to adapt the code for other image formats, add error handling, or integrate it into larger applications. Happy coding!

## 다음에 배워야 할 내용은?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [C#에서 이미지 텍스트 추출 – 완전한 Aspose OCR 가이드](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [Aspose.OCR을 사용한 언어 선택으로 C# 이미지 텍스트 추출](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Aspose OCR을 사용한 스트림에서 이미지 텍스트 추출 방법](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}