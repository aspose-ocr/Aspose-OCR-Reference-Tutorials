---
category: general
date: 2026-04-26
description: C#로 PNG 파일에서 텍스트를 빠르게 추출하세요. 이미지를 텍스트로 변환하고, PNG 파일을 읽으며, 이미지를 순회하고,
  몇 분 안에 배치 OCR을 수행하는 방법을 배워보세요.
draft: false
keywords:
- extract text from png
- convert images to text
- read png files
- loop through images
- batch ocr images
language: ko
og_description: C#로 PNG 파일에서 텍스트를 빠르게 추출하세요. 이 가이드는 이미지를 텍스트로 변환하고, PNG 파일을 읽으며, 이미지를
  순회하고 배치 OCR을 수행하는 방법을 보여줍니다.
og_title: PNG에서 텍스트 추출 – 완전한 C# 배치 OCR 튜토리얼
tags:
- C#
- OCR
- Aspose
title: PNG에서 텍스트 추출 – 완전한 C# 배치 OCR 튜토리얼
url: /ko/net/text-recognition/extract-text-from-png-complete-c-batch-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG에서 텍스트 추출 – 완전한 C# 배치 OCR 튜토리얼

PNG 파일에서 **텍스트를 추출**해야 하는데 어디서 시작해야 할지 몰라 고민한 적 있나요? 혼자가 아닙니다—스크린샷 폴더에 OCR을 처음 적용할 때 많은 개발자들이 이 장벽에 부딪히곤 합니다. 좋은 소식은 몇 줄의 C# 코드와 Aspose OCR만 있으면 이미지를 텍스트로 변환하고, PNG 파일을 읽으며, 이미지를 순회하고, 모든 작업을 한 번에 배치 처리할 수 있다는 점입니다.

이 튜토리얼에서는 바로 실행 가능한 콘솔 앱을 단계별로 살펴보겠습니다. 최종적으로 디렉터리 내 모든 PNG에서 텍스트를 추출하고, 각 이미지 옆에 동일한 이름의 `.txt` 파일을 생성하는 독립형 솔루션을 얻게 됩니다. 별도의 스크립트나 수동 복사‑붙여넣기 없이 순수 코드만으로 구현합니다.

## 필요 사항

- **.NET 6 SDK** (또는 최신 .NET 버전). 무료이고 빠르며 어디서든 동작합니다.
- **Aspose.OCR for .NET** (NuGet 패키지). 호환 GPU가 있으면 GPU 가속을 지원하고, 없을 경우 자동으로 CPU로 전환됩니다.
- 처리하고자 하는 **PNG 이미지**가 들어 있는 폴더.
- 텍스트 편집기 또는 IDE—Visual Studio, VS Code, Rider 등 원하는 도구.

이것만 있으면 준비 완료입니다.

![extract text from png example](image.png "extract text from png demo screenshot")

*이미지 대체 텍스트: “C# 배치 OCR을 사용해 PNG에서 텍스트 추출”*

## 1단계 – 프로젝트 설정 및 Aspose.OCR 설치

먼저 새 콘솔 프로젝트를 만들고 Aspose OCR 패키지를 추가합니다.

```bash
dotnet new console -n PngOcrBatch
cd PngOcrBatch
dotnet add package Aspose.OCR
```

콘솔 앱을 사용하는 이유는 배치 작업에 가장 간단한 호스트이며, 명령줄에서 실행하거나 작업 스케줄러와 연동하기 쉽기 때문입니다. 나중에 UI가 필요하면 핵심 로직을 클래스 라이브러리로 옮기기만 하면 됩니다.

## 2단계 – GPU 가속 OCR 엔진 초기화 (CPU 폴백 포함)

Aspose는 지원되는 GPU를 자동으로 감지하는 `GpuOcrEngine`을 제공합니다. GPU가 없을 경우 자동으로 일반 CPU 엔진으로 전환되므로 별도 코드가 필요 없습니다.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create the OCR engine – GPU if available, otherwise CPU
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;   // Latin covers most Western alphabets

        // The rest of the code lives in a separate method for clarity
        ProcessFolder(ocrEngine, @"C:\MyPngFolder");
    }

    // …
}
```

**팁:** GPU가 없는 헤드리스 서버에서는 `GpuOcrEngine`을 `OcrEngine`으로 교체하면 동일하게 동작합니다.

## 3단계 – 대상 디렉터리의 이미지 순회

**이미지를 순회**하면서 PNG 파일만 선택해야 합니다. `Directory.GetFiles` 메서드가 핵심 역할을 하며, 빈 폴더에 대비한 방어 코드도 포함합니다.

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    if (!Directory.Exists(folderPath))
    {
        Console.WriteLine($"❌ Folder not found: {folderPath}");
        return;
    }

    // Grab every *.png file – this is the “read png files” part
    string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

    if (pngFiles.Length == 0)
    {
        Console.WriteLine("⚠️ No PNG files found. Make sure the folder contains .png images.");
        return;
    }

    foreach (var pngPath in pngFiles)
    {
        Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
        ExtractAndSave(engine, pngPath);
    }
}
```

`SearchOption.TopDirectoryOnly` 사용에 주목하세요. 하위 폴더까지 재귀적으로 탐색하려면 `AllDirectories`로 바꾸면 됩니다. 이 작은 변경만으로 전체 트리의 **이미지를 텍스트로 변환**할 수 있습니다.

## 4단계 – OCR 수행 및 결과 저장

이제 **배치 OCR 이미지** 워크플로우의 핵심 단계입니다. 각 PNG를 로드하고 `Recognize()`를 실행한 뒤, 추출된 문자열을 동일한 기본 이름을 가진 `.txt` 파일에 기록합니다.

```csharp
static void ExtractAndSave(OcrEngine engine, string imagePath)
{
    try
    {
        // Load the PNG into the engine
        engine.Image = ImageStream.FromFile(imagePath);

        // Run recognition – this returns a RecognitionResult object
        RecognitionResult result = engine.Recognize();

        // Build the output path (same name, .txt extension)
        string txtPath = Path.ChangeExtension(imagePath, ".txt");

        // Write the OCR text to disk
        File.WriteAllText(txtPath, result.Text);

        Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        // Edge case: corrupted PNG or unsupported format
        Console.WriteLine($"❗ Error processing {Path.GetFileName(imagePath)}: {ex.Message}");
    }
}
```

**왜 try/catch로 감싸는가?** 실제 이미지 배치에는 손상된 파일이나 특수 색상 프로파일을 사용하는 PNG가 포함될 수 있습니다. 예외를 잡아두면 전체 실행이 중단되지 않고 나머지 파일을 계속 처리할 수 있습니다.

## 5단계 – 애플리케이션 실행 및 출력 확인

앱을 빌드하고 실행합니다:

```bash
dotnet run
```

콘솔에 다음과 유사한 로그가 표시됩니다:

```
🔎 Processing: invoice1.png
✅ Saved: invoice1.txt
🔎 Processing: screenshot_2024.png
✅ Saved: screenshot_2024.txt
...
```

생성된 `.txt` 파일을 열어보면 추출된 텍스트를 확인할 수 있습니다. 파일이 비어 있다면 이미지 품질을 다시 점검하세요; OCR은 선명하고 고대비 텍스트에서 가장 잘 동작합니다.

### 빠른 검증 스크립트 (선택 사항)

모든 PNG에 대응하는 텍스트 파일이 생성됐는지 확인하려면 다음 PowerShell 한 줄 명령을 실행합니다:

```powershell
Get-ChildItem -Path "C:\MyPngFolder" -Filter *.png |
  ForEach-Object { 
    $txt = $_.BaseName + ".txt"
    if (-Not (Test-Path $txt)) { Write-Host "Missing: $txt" }
  }
```

## 일반적인 변형 및 엣지 케이스

| 상황 | 변경 내용 |
|-----------|----------------|
| **비라틴 언어** (예: Cyrillic) | `ocrEngine.Language = Language.Cyrillic;` |
| **대규모 이미지 집합 (>10 000 파일)** | `Parallel.ForEach`를 사용해 처리 속도를 높이되 GPU 메모리 사용량을 모니터링합니다. |
| **원본 이미지 순서를 유지해야 할 경우** | `foreach` 전에 `pngFiles`를 정렬합니다 (`Array.Sort(pngFiles);`). |
| **GPU가 없는 CI 서버에서 실행** | `GpuOcrEngine`을 `OcrEngine`으로 교체해 GPU 초기화 오류를 방지합니다. |
| **특정 키워드가 포함된 파일만 처리하고 싶을 때** | `result.Text`를 얻은 뒤 `result.Text.Contains("Invoice")`를 검사하여 파일을 기록합니다. |

이러한 조정으로 **이미지를 텍스트로 변환** 파이프라인을 거의 모든 시나리오에 맞게 확장할 수 있습니다.

## 전체 소스 코드 (복사‑붙여넣기 가능)

```csharp
// ------------------------------------------------------------
// Extract Text from PNG – Batch OCR using Aspose.OCR (C#)
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine (GPU if possible)
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;

        // 2️⃣ Define the folder that holds your PNG files
        string targetFolder = @"C:\MyPngFolder";   // <-- change to your path

        // 3️⃣ Process every PNG in the folder
        ProcessFolder(ocrEngine, targetFolder);
    }

    static void ProcessFolder(OcrEngine engine, string folderPath)
    {
        if (!Directory.Exists(folderPath))
        {
            Console.WriteLine($"❌ Folder not found: {folderPath}");
            return;
        }

        string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

        if (pngFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No PNG files found.");
            return;
        }

        foreach (var pngPath in pngFiles)
        {
            Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
            ExtractAndSave(engine, pngPath);
        }
    }

    static void ExtractAndSave(OcrEngine engine, string imagePath)
    {
        try
        {
            engine.Image = ImageStream.FromFile(imagePath);
            RecognitionResult result = engine.Recognize();

            string txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, result.Text);

            Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❗ Error on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

`Program.cs`로 저장하고 `dotnet run`을 실행하면 마법이 펼쳐집니다.

## 결론

이제 C#을 사용해 **PNG 파일에서 텍스트를 추출**하는 완전하고 프로덕션 수준의 방법을 갖추었습니다. 튜토리얼에서는 프로젝트 설정, GPU 가속 OCR 엔진 초기화, **이미지를 순회**, **배치 OCR 이미지** 수행 및 결과를 텍스트 파일로 저장하는 전 과정을 다루었습니다.

다음 단계가 궁금하다면 시도해 보세요:

- **다른 포맷** (JPG, BMP 등)에서도 **이미지를 텍스트로 변환**하기

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}