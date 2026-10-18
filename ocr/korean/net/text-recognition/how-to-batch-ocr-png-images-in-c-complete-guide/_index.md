---
category: general
date: 2026-03-17
description: C#에서 PNG 이미지를 빠르게 일괄 OCR하는 방법. PNG 파일에서 텍스트를 추출하고, PNG를 텍스트로 변환하며, 간단한
  스크립트로 디렉터리의 이미지를 읽는 방법을 배워보세요.
draft: false
keywords:
- how to batch OCR
- extract text png
- convert png to text
- read images from directory
language: ko
og_description: C#에서 단계별 코드로 PNG 이미지를 일괄 OCR하는 방법. 텍스트 PNG 파일을 추출하고, PNG를 텍스트로 변환하며,
  디렉터리에서 이미지를 손쉽게 읽어옵니다.
og_title: C#에서 PNG 이미지 일괄 OCR하는 방법 – 완전 가이드
tags:
- OCR
- C#
- Image Processing
title: C#에서 PNG 이미지를 일괄 OCR하는 방법 – 완전 가이드
url: /ko/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 PNG 이미지 일괄 OCR 하는 방법 – 완전 가이드

스크린샷이 가득한 폴더를 각각 파일을 수동으로 열지 않고 **일괄 OCR** 하는 방법이 궁금하셨나요? 당신만 그런 것이 아닙니다—개발자들은 특히 다운스트림 분석을 위해 텍스트 PNG 파일을 추출하는 것이 목표일 때, 대량의 PNG 컬렉션을 **일괄 OCR** 하는 방법을 지속적으로 묻습니다.  

이 튜토리얼에서는 **텍스트 PNG 추출**하고, **PNG를 텍스트로 변환**하며, **디렉터리에서 이미지 읽기**의 최적 방법을 보여주는 바로 실행 가능한 C# 예제를 단계별로 살펴보겠습니다. 끝까지 진행하면 모든 이미지 옆에 `.txt` 파일을 자동으로 생성하는 단일 스크립트를 얻게 되어 수시간 걸리던 수동 복사‑붙여넣기를 절약할 수 있습니다.

## 달성 목표

- OCR 엔진을 한 번 초기화하고 전체 배치에 재사용합니다.  
- 루프를 직접 작성하지 않고 지정된 폴더의 모든 `*.png`를 스캔합니다.  
- 각 OCR 결과를 원본 파일 이름을 유지한 채 별도의 텍스트 파일에 기록합니다.  
- 빈 폴더나 이미지가 아닌 파일과 같은 일반적인 엣지 케이스를 우아하게 처리합니다.

### 전제 조건

- .NET 6.0 이상 (코드는 .NET Core 및 .NET Framework에서도 작동합니다).  
- `OcrEngine`, `ImageStream`, `OcrResult` 타입을 제공하는 OCR 라이브러리 (예: 예제에 사용된 가상의 **FastOCR** SDK).  
- 기본적인 C# 지식—고급 패턴은 필요하지 않습니다.

---

## PNG 이미지 일괄 OCR 방법 – 개요

아래는 **완전하고 실행 가능한 프로그램**입니다. 새 콘솔 프로젝트에 복사‑붙여넣기하고, 플레이스홀더 경로를 교체한 뒤 **F5**를 눌러 실행해 보세요.

```csharp
using System;
using System.IO;
using System.Linq;
using FastOCR;               // <-- Replace with your actual OCR namespace

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine (language = English)
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.Language = Language.English;

        // -------------------------------------------------
        // Step 2: Locate every PNG file in the input folder
        // -------------------------------------------------
        string inputFolder = @"YOUR_DIRECTORY\images";
        string[] imagePaths = Directory.GetFiles(inputFolder, "*.png");

        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to process.");
            return;
        }

        // -------------------------------------------------
        // Step 3: Convert file paths to ImageStream objects
        // -------------------------------------------------
        var imageStreams = imagePaths
            .Select(path => ImageStream.FromFile(path))
            .ToList();

        // -------------------------------------------------
        // Step 4: Recognize text in the entire batch
        // -------------------------------------------------
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // -------------------------------------------------
        // Step 5: Write each result to a .txt file next to the image
        // -------------------------------------------------
        string outputFolder = @"YOUR_DIRECTORY\output";
        Directory.CreateDirectory(outputFolder); // ensures the folder exists

        for (int i = 0; i < ocrResults.Count; i++)
        {
            string originalFileName = Path.GetFileNameWithoutExtension(imagePaths[i]);
            string outputPath = Path.Combine(outputFolder, $"{originalFileName}.txt");
            File.WriteAllText(outputPath, ocrResults[i].Text);
            Console.WriteLine($"✅ {originalFileName}.txt created");
        }

        Console.WriteLine("All done! Check the output folder for your text files.");
    }
}
```

> **예상 출력:** 각 `image01.png`에 대해 인식된 문자가 들어 있는 `image01.txt` 파일이 생성됩니다. 콘솔에는 파일이 기록될 때마다 해당 파일명이 표시됩니다.

![일괄 OCR 다이어그램](how-to-batch-ocr-diagram.png "C#를 사용한 PNG 이미지 일괄 OCR 방법을 보여주는 다이어그램")

---

## 단계별 설명

### 1. OCR 엔진 초기화 – 프로세스의 핵심  

`var ocrEngine = new OcrEngine();` 라인은 전체 배치에 재사용될 단일 엔진 인스턴스를 생성합니다. 엔진을 재사용하는 것은 **핵심**이며, 대부분의 OCR 라이브러리는 생성 시 무거운 리소스(예: 언어 모델)를 할당하기 때문입니다. 한 번 초기화하면 성능이 크게 향상됩니다—특히 수십에서 수백 개의 PNG를 처리할 때 더욱 그렇습니다.

> **프로 팁:** 영어 외의 언어가 필요하면 `ocrEngine.Config.Language = Language.Spanish;` 와 같이 설정합니다(지원되는 열거형 중 하나).

### 2. 디렉터리에서 이미지 읽기 – 모든 PNG 찾기  

`Directory.GetFiles(@"YOUR_DIRECTORY\images", "*.png")` 은 보조 키워드 *read images from directory* 가 약속하는 바로 그 동작을 수행합니다. 절대 경로 배열을 반환하며, 이를 이후 OCR 엔진에 전달합니다.  

> **`SearchOption.AllDirectories`를 사용하지 않는 이유는?** 이미지가 하위 폴더에 있다면 `GetFiles(path, "*.png", SearchOption.AllDirectories)` 로 전환할 수 있습니다. 다만 깊은 스캔은 원치 않는 파일을 포함할 수 있으니 적절히 필터링하세요.

### 3. 파일 경로를 ImageStream 객체로 변환  

대부분의 OCR SDK는 원시 경로 대신 스트림을 기대합니다. LINQ 표현식 `Select(path => ImageStream.FromFile(path)).ToList()` 은 배치 인식기가 한 번에 사용할 수 있는 **스트림 리스트**를 생성합니다. 이 단계는 파일 핸들을 한 번만 열어 I/O 오버헤드를 줄여줍니다.

> **예외 상황:** 파일이 손상된 경우 `ImageStream.FromFile` 이 예외를 발생시킬 수 있습니다. 복원력이 필요하면 변환을 `try/catch` 로 감싸세요.

### 4. 전체 배치에서 텍스트 인식  

`ocrEngine.RecognizeBatch(imageStreams)` 은 *how to batch OCR* 에 대한 최적 솔루션입니다. 각 이미지를 순회하며 단일 이미지 메서드를 호출하는 대신 전체 컬렉션을 엔진에 전달합니다. 내부적으로 라이브러리는 작업을 병렬화할 수 있어 멀티코어 머신에서 속도가 크게 향상됩니다.

> **팁:** OCR 라이브러리에 배치 메서드가 없더라도 단일 이미지 `Recognize` 호출을 `Parallel.ForEach` 로 감싸면 유사한 성능을 얻을 수 있습니다.

### 5. 각 OCR 결과 쓰기 – PNG를 텍스트로 변환  

마지막 `for` 루프는 `ocrResults[i].Text` 를 원본 PNG와 동일한 이름을 가진 `.txt` 파일에 기록합니다. 이는 보조 키워드 *convert PNG to text* 가 설명하는 바로 그 동작입니다. `Path.Combine` 호출은 출력 폴더가 존재함을 보장하고 경로 탐색 버그를 방지합니다.

> **흔한 실수:** 출력 디렉터리를 먼저 생성하지 않으면 `DirectoryNotFoundException` 이 발생합니다. `Directory.CreateDirectory(outputFolder);` 라인이 이를 사전에 해결합니다.

---

## 실제 상황 대응

| Situation | What to Change | Why |
|-----------|----------------|-----|
| **입력 폴더가 비어 있음** | 초기 `if (imagePaths.Length == 0)` 가드를 유지 | 불필요한 OCR 호출을 방지하고 친절한 메시지를 제공합니다 |
| **혼합 파일 유형** | `Directory.EnumerateFiles(..., "*.*", SearchOption.TopDirectoryOnly).Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase))` 사용 | PNG만 처리하도록 보장하여 *extract text png* 를 오류 없이 수행합니다 |
| **대용량 이미지 ( > 5 MB )** | OCR에 전달하기 전에 다운스케일: `ImageStream.FromFile(path).Resize(1920, 1080)` (API가 지원하는 경우) | 메모리 부담을 줄이고 인식 정확도를 향상시킬 수 있습니다 |
| **다른 OCR 언어** | `ocrEngine.Config.Language = Language.French;` 설정 | 엔진을 원본 이미지의 언어와 일치시킵니다 |

---

## 자주 묻는 질문 (FAQ)

**Q: JPEG 또는 TIFF 파일에서도 작동하나요?**  
A: 핵심 로직은 동일합니다; 검색 패턴을 `"*.jpg"` 또는 `"*.tif"` 로 바꾸고 OCR 라이브러리가 해당 형식을 디코딩할 수 있는지 확인하면 됩니다.

**Q: 메모리 부족 없이 수천 개의 이미지를 처리하려면 어떻게 해야 하나요?**  
A: 배치 호출을 스트리밍 방식으로 교체합니다—예를 들어 한 번에 50장씩 처리하고 다음 청크를 로드하기 전에 스트림을 해제합니다.

**Q: OCR 신뢰도 점수가 필요합니다. 어디서 확인할 수 있나요?**  
A: 대부분의 `OcrResult` 객체는 `Confidence` 속성을 제공합니다. 기록 단계에 다음과 같이 확장할 수 있습니다:

```csharp
var result = ocrResults[i];
string content = $"Confidence: {result.Confidence:P2}\n{result.Text}";
File.WriteAllText(outputPath, content);
```

---

## 마무리

우리는 이제 C#에서 PNG 이미지를 **일괄 OCR** 하는 전체 과정을 다루었습니다. 단일 엔진을 초기화하고, 디렉터리에서 이미지를 읽으며, 스트림으로 변환하고, 전체 배치를 인식한 뒤, 각 결과를 텍스트 파일에 기록함으로써 **텍스트 PNG 추출**, **PNG를 텍스트로 변환**, **디렉터리에서 이미지 읽기** 작업을 위한 견고하고 프로덕션 준비된 패턴을 갖추게 되었습니다.

다음은? OCR 제공자를 교체하거나, 멀티스레드 후처리(예: 맞춤법 검사)를 추가하거나, `.txt` 파일을 검색 인덱스로 공급해 보세요. 배치 워크플로우를 마스터하면 가능성은 무한합니다.

특별한 팁이 있나요? 댓글로 공유해 주세요. 즐거운 코딩 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}