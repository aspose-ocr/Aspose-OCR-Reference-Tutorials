---
category: general
date: 2026-03-13
description: C#에서 OCR을 사용해 스캔 이미지에서 텍스트를 추출하는 방법. Aspose OCR, GPU 가속 및 단계별 코드를 통해
  TIFF를 텍스트로 변환하는 방법을 배워보세요.
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: ko
og_description: C#에서 OCR을 사용하여 스캔에서 텍스트를 추출하는 방법. 이 가이드는 Aspose OCR과 GPU 가속을 활용해 TIFF를
  텍스트로 변환하는 방법을 보여줍니다.
og_title: C#에서 OCR 사용 방법 – 스캔에서 텍스트를 빠르게 추출하기
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#에서 OCR 사용 방법 – 스캔에서 텍스트를 빠르게 추출하기
url: /ko/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 OCR 사용 방법 – 스캔에서 텍스트 빠르게 추출

스캔된 TIFF 파일 더미에서 읽을 수 있는 텍스트를 추출하는 **OCR를 사용하는 방법**이 궁금했나요? 여러분만 그런 것이 아닙니다. 실제 프로젝트—예를 들어 청구서 디지털화, 역사 문서 보관, 혹은 PDF를 검색 가능하게 만들기—에서 개발자는 **스캔에서 텍스트를 추출**하는 신뢰할 수 있는 방법이 필요합니다.

좋은 소식은? Aspose OCR와 몇 줄의 C# 코드만 있으면 보통 워크스테이션에서도 몇 초 만에 TIFF를 텍스트로 변환할 수 있습니다. 아래에서는 바로 실행 가능한 전체 예제와 각 선택에 대한 이유를 제공하므로 여러분의 워크플로에 맞게 쉽게 적용할 수 있습니다.

## 필요 사항

시작하기 전에 아래 항목을 준비하세요:

| Prerequisite | Why it matters |
|--------------|----------------|
| .NET 6+ (or .NET Framework 4.7+) | Aspose OCR NuGet 패키지는 최신 .NET 런타임을 대상으로 합니다. |
| Visual Studio 2022 (or any IDE you like) | IntelliSense와 쉬운 디버깅을 제공합니다. |
| CUDA‑compatible GPU & driver (optional) | `ocrEngine.UseGpu = true` 를 설정하면 대용량 배치에서 눈에 띄는 속도 향상을 얻을 수 있습니다. |
| 처리하려는 TIFF 이미지가 들어 있는 폴더 | 이 튜토리얼은 `*.tif` 파일을 사용하지만 패턴은 자유롭게 변경할 수 있습니다. |
| Aspose.OCR NuGet package (`Install-Package Aspose.OCR`) | 무거운 작업을 수행하는 핵심 라이브러리입니다. |

위 항목 중 하나라도 없으면 지금 바로 확보하세요—나중에 의존성 오류로 시간을 낭비하고 싶지 않으니까요.

## 솔루션 개요

프로그램은 크게 세 가지 작업을 수행합니다:

1. **OCR 엔진을 생성**하고 필요에 따라 GPU 가속을 켭니다.  
2. **디렉터리의 모든 TIFF 파일을 순회**하면서 인식하고 결과 텍스트를 얻습니다.  
3. **텍스트를 원본 이미지와 같은 위치에 `.txt` 파일**로 저장합니다.

그게 전부입니다. 코드는 의도적으로 작게 유지했지만, 명시적 언어 선택, 적절한 리소스 해제, 일반적인 가장자리 경우에 대한 오류 처리와 같은 모범 사례를 보여줍니다.

![C#에서 OCR 사용 예시](/images/how-to-use-ocr-csharp.png "C#에서 OCR을 사용해 스캔에서 텍스트를 추출하는 방법")

## 단계 1: OCR 엔진 초기화 (How to Use OCR)

먼저 `OcrEngine` 인스턴스를 만들어야 합니다. 이 객체가 Aspose OCR 모든 기능에 접근하는 관문입니다. 기본적으로 CPU에서 동작하지만 `UseGpu = true` 로 설정하면 CUDA‑compatible 드라이버가 설치된 경우 무거운 행렬 연산을 그래픽 카드로 오프로드합니다.

```csharp
using Aspose.OCR;
using System.IO;

// Initialise the engine ----------------------------------------------------
OcrEngine ocrEngine = new OcrEngine
{
    // Enable GPU acceleration if a compatible card is present.
    // If you don’t have a GPU, just leave this as false – the code will still run.
    UseGpu = true,

    // Choose English as the recognition language. Change this if you need
    // another language pack (e.g., Language.French, Language.Spanish, etc.).
    Language = Language.English
};
```

**왜 중요한가:**  
- **GPU 가속**은 고해상도 스캔의 경우 처리 시간을 최대 70 %까지 단축할 수 있습니다.  
- **명시적 언어 선택**은 엔진이 추측하는 것을 방지하고, 특히 비라틴 문자에 대한 정확도를 높여줍니다.

## 단계 2: 엔진에 스캔 파일 지정 (Convert TIFF to Text)

다음으로 프로그램이 이미지들을 찾을 위치를 알려줍니다. `Directory.GetFiles`에 `*.tif` 필터를 사용하면 로직이 간단해지고 `.jpg`나 `.png` 같은 무관한 파일이 포함되지 않습니다.

```csharp
// Define the folder that contains the scanned TIFF images -----------------
string inputFolder = @"C:\ScannedDocs"; // <-- replace with your actual path

// Verify the folder exists before we start looping
if (!Directory.Exists(inputFolder))
{
    Console.WriteLine($"❌ Folder not found: {inputFolder}");
    return;
}
```

**가장자리 경우 주의:** 디렉터리가 비어 있으면 아래 루프가 전혀 실행되지 않으며, 이는 전혀 문제가 되지 않습니다. 이후에 친절한 “파일을 찾을 수 없습니다” 메시지가 표시됩니다.

## 단계 3: 각 TIFF 파일 처리 (Extract Text from Scans)

이제 프로그램의 핵심: 각 이미지를 로드하고 OCR을 실행한 뒤 결과를 저장합니다. `ImageStream.FromFile` 도우미는 파일을 바로 메모리 스트림으로 전달하므로 `Bitmap`을 먼저 로드하는 것보다 효율적입니다.

```csharp
// Step 3: Iterate over every .tif file in the folder --------------------
string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

if (tiffFiles.Length == 0)
{
    Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
}
else
{
    foreach (var imagePath in tiffFiles)
    {
        try
        {
            // Load the current image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR on the image
            ocrEngine.Recognize();

            // Build the output .txt file path (same name, different extension)
            string textPath = Path.ChangeExtension(imagePath, ".txt");

            // Save the extracted text
            File.WriteAllText(textPath, ocrEngine.Text);

            Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
        }
        catch (Exception ex)
        {
            // Log the error but continue with the next file
            Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

**`try/catch` 로 각 반복을 감싸는 이유:**  
문서 배치를 스캔하는 과정은 언제든지 문제가 발생할 수 있습니다. 손상된 TIFF 파일이나 메모리 부족 오류가 전체 실행을 중단하지 않도록, catch 블록에서 문제를 기록하고 다음 파일로 넘어가 파이프라인의 견고함을 유지합니다.

### 예상 출력

각 `example.tif`에 대해 같은 위치에 `example.txt` 파일이 생성되며 내용은 다음과 비슷합니다:

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

OCR 엔진이 라인을 읽지 못하면 빈 줄이나 깨진 문자로 남게 되며, 프로그램이 중단되지는 않습니다.

## 단계 4: 정리 및 해제 (Best Practice)

`OcrEngine`은 `IDisposable`을 구현하므로 사용이 끝난 뒤 네이티브 리소스를 해제하는 것이 예의입니다. 짧은 콘솔 앱에서는 GC에 맡길 수 있지만, 명시적 해제는 습관화할 가치가 있습니다.

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## 전체 작동 예제 (Copy‑Paste Ready)

아래는 새 콘솔 앱 프로젝트에 그대로 붙여넣을 수 있는 완전한 프로그램입니다. Aspose.OCR NuGet 패키지만 추가하면 바로 컴파일됩니다.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // Step 1: Initialise the OCR engine (how to use OCR)
        // --------------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            UseGpu = true,               // Enable GPU if available
            Language = Language.English  // Set language for recognition
        };

        // --------------------------------------------------------------------
        // Step 2: Define the folder containing TIFF scans (convert TIFF to text)
        // --------------------------------------------------------------------
        string inputFolder = @"C:\ScannedDocs"; // <-- adjust this path

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"❌ Folder not found: {inputFolder}");
            return;
        }

        // --------------------------------------------------------------------
        // Step 3: Process each TIFF file (extract text from scans)
        // --------------------------------------------------------------------
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

        if (tiffFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
        }
        else
        {
            foreach (var imagePath in tiffFiles)
            {
                try
                {
                    // Load image
                    ocrEngine.Image = ImageStream.FromFile(imagePath);

                    // Run OCR
                    ocrEngine.Recognize();

                    // Save result next to source image
                    string textPath = Path.ChangeExtension(imagePath, ".txt");
                    File.WriteAllText(textPath, ocrEngine.Text);

                    Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }
        }

        // --------------------------------------------------------------------
        // Step 4: Clean‑up (c# OCR tutorial best practice)
        // --------------------------------------------------------------------
        ocrEngine.Dispose();
        Console.WriteLine("🎉 All done! OCR engine released.");
    }
}
```

### 빠른 체크리스트

- **GPU 플래그** – CUDA 드라이버가 없으면 `false` 로 변경하거나 제거하세요.  
- **언어** – `Language.English` 를 다른 지원 언어로 교체하세요.  
- **파일 패턴** – 스캔 파일이 다른 형식이면 `"*.tif"` 를 `"*.png"` 혹은 `"*.*"` 로 바꾸세요.  

## 흔히 겪는 문제와 전문가 팁 (c# OCR tutorial)

| Pitfall | How to avoid it |
|---------|-----------------|
| **Out‑of‑memory errors** on huge batches | 파일을 더 작은 청크로 나누어 처리하거나 50개 파일마다 `GC.Collect()` 를 호출하세요 (드물게 필요). |
| **GPU not detected** but `UseGpu = true` | 엔진은 자동으로 CPU로 폴백하지만, 생성 후 `ocrEngine.IsGpuAvailable` 로 확인할 수 있습니다. |
| **Wrong language pack** leads to garbled output | 항상 `ocrEngine.Language` 를 명시적으로 설정하세요; 기본값은 `Language.Unknown` 일 수 있습니다. |
| **File path contains Unicode characters** | `Path.GetFullPath` 로 정규화하거나, Windows에서 경로 길이가 길 경우 `@"\\?\"` 를 앞에 붙이세요. |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}