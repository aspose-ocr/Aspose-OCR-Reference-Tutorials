---
category: general
date: 2026-03-05
description: Aspose OCR을 사용하여 C#에서 TIFF를 텍스트로 변환—스캔된 이미지 파일에서 텍스트를 빠르게 추출하고 OCR 처리를
  위해 C#에서 이미지 파일을 로드하는 방법을 배워보세요.
draft: false
keywords:
- convert TIFF to text
- extract text scanned image
- load image file C#
language: ko
og_description: Aspose OCR을 사용하여 C#에서 TIFF를 텍스트로 변환합니다. 스캔한 이미지에서 텍스트를 추출하고 이미지 파일을
  효율적으로 로드하는 전체 워크플로우를 배워보세요.
og_title: C#에서 TIFF를 텍스트로 변환 – 스캔된 이미지 텍스트 추출
tags:
- OCR
- C#
- Aspose
title: C#에서 TIFF를 텍스트로 변환 – 스캔된 이미지 텍스트 추출
url: /ko/net/text-recognition/convert-tiff-to-text-in-c-extract-scanned-image-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 TIFF를 텍스트로 변환 – 스캔 이미지 텍스트 추출

**C#에서 TIFF를 텍스트로 변환**해야 하나요? 여러 페이지로 구성된 스캔 이미지가 검색 가능한 문자열로 바뀌지 않아 고민하고 계신 분들께 이 가이드는 완전한 실행 가능한 솔루션을 제공합니다. TIFF 파일을 Aspose OCR에 전달하고 순수 텍스트를 출력합니다—추가 서비스나 숨겨진 마법 없이.

> **Pro tip:** 고해상도 스캔을 다룰 때 GPU 처리를 활성화하면 페이지당 몇 초를 절감할 수 있습니다.

또한 **스캔 이미지 파일에서 텍스트 추출** 방법과 **이미지 파일을 C#에서 로드**하는 최적의 방법을 보여드리니, 오늘 바로 이 로직을 모든 .NET 프로젝트에 삽입할 수 있습니다.

---

## 필요 사항

작업을 시작하기 전에 아래 항목들이 시스템에 준비되어 있는지 확인하세요.

| 요구 사항 | 이유 |
|-----------|------|
| .NET 6.0+ (또는 .NET Framework 4.7.2+) | 최신 런타임, `Span<T>`와 비동기 I/O 지원 |
| Aspose.OCR for .NET (NuGet 패키지 `Aspose.OCR`) | 사용할 OCR 엔진 |
| 유효한 Aspose OCR 라이선스 파일 (`Aspose.OCR.lic`) | 라이선스가 없으면 평가 제한에 걸림 |
| 테스트용 TIFF 파일 (단일·다중 페이지) | 예시 파일: `scanned_multi_page.tif` |
| CUDA 11+ 지원 GPU (선택 사항) | `EngineMode = Gpu` 설정 시 인식 속도 향상 |

위 항목 중 누락된 것이 있다면 지금 바로 NuGet 패키지를 받아 주세요:

```bash
dotnet add package Aspose.OCR
```

---

## Step 1: 프로젝트 설정 및 네임스페이스 가져오기

새 콘솔 앱을 만들거나 기존 프로젝트에 코드를 추가합니다. 먼저 필요한 클래스를 가져옵니다.

```csharp
using System;
using Aspose.OCR;          // Core OCR classes
using Aspose.OCR.Image;   // ImageStream helper
```

> **왜 중요한가:** `Aspose.OCR.Image`를 가져오면 `ImageStream` 팩토리를 사용할 수 있어 TIFF 파일을 디스크나 스트림에서 직접 읽을 수 있습니다. 이 단계를 건너뛰면 컴파일 오류가 발생합니다.

---

## Step 2: OCR 엔진 초기화 및 처리 모드 선택

이미지를 할당하기 **전에** OCR 엔진을 설정해야 합니다. 여기서 CPU와 GPU 중 어느 쪽을 사용할지 결정합니다.

```csharp
// Step 2: Initialize the OCR engine and enable GPU processing (must be set before any OCR work)
OcrEngine ocrEngine = new OcrEngine();

// Choose the processing mode that fits your environment.
// Options: Cpu (default) | Gpu | Auto
ocrEngine.EngineMode = OcrEngineMode.Gpu;   // Switch to Cpu if you don’t have a compatible GPU
```

*그래픽 카드가 없는 헤드리스 서버에서는 `Gpu`를 `Cpu` 또는 `Auto`로 변경하세요.*  
엔진 모드는 메모리 할당과 속도에 영향을 주며, GPU 모드는 대용량·고해상도 TIFF에서 2‑3배 빠를 수 있습니다.

---

## Step 3: Aspose OCR 라이선스 적용

라이선스 없이 실행하면 몇 페이지만 처리되고 워터마크가 삽입됩니다. 라이선스를 미리 로드하면 이후 모든 작업이 제한 없이 수행됩니다.

```csharp
// Step 3: Apply the Aspose OCR license (replace with your own license file if needed)
ocrEngine.SetLicense("Aspose.OCR.lic");
```

> **흔한 실수:** `SetLicense`를 `Recognize()` **후**에 호출하면 해당 호출은 평가 모드로 돌아갑니다.

---

## Step 4: TIFF 파일 로드 – 단일 및 다중 페이지 이미지 처리

Aspose OCR은 다중 페이지 TIFF를 기본적으로 지원하지만, 올바른 스트림을 전달해야 합니다. 아래 패턴은 두 경우 모두 작동합니다.

```csharp
// Step 4: Load the image to be recognized
string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

using (var imageStream = ImageStream.FromFile(tiffPath))
{
    // Step 5: Assign the image to the engine
    ocrEngine.Image = imageStream;

    // Step 6: Perform the OCR operation
    OcrResult ocrResult = ocrEngine.Recognize();

    // Step 7: Output the recognized text
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
```

### `ImageStream.FromFile`을 사용하는 이유

- 내부적으로 `FileStream`을 추상화해 TIFF 페이지 열거를 자동으로 처리합니다.  
- `MemoryStream`도 지원하므로 데이터베이스나 웹 API에서 파일 시스템을 거치지 않고 이미지를 로드할 수 있습니다.

### 엣지 케이스: 매우 큰 TIFF

TIFF 파일 크기가 200 MB를 초과하면 페이지별로 로드하여 메모리 부족 예외를 방지하세요:

```csharp
int pageCount = ImageInfo.GetPageCount(tiffPath);
for (int i = 0; i < pageCount; i++)
{
    using var pageStream = ImageStream.FromFile(tiffPath, i);
    ocrEngine.Image = pageStream;
    var pageResult = ocrEngine.Recognize();
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

---

## Step 5: 출력 확인

프로그램을 실행하면 다음과 같은 결과가 표시됩니다:

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
Thank you for your business!
```

텍스트가 깨져 보인다면 다음을 재확인하세요:

1. **해상도** – OCR은 300 dpi 이상에서 가장 잘 작동합니다.  
2. **EngineMode** – GPU 드라이버가 오래됐으면 `Cpu`로 전환하세요.  
3. **라이선스** – 라이선스 파일 경로가 정확하고 파일에 접근 가능한지 확인합니다.

---

## Frequently Asked Questions (FAQ)

### 다른 이미지 포맷도 지원하나요?

네. `ImageStream.FromFile`은 JPEG, PNG, BMP는 물론 PDF(Aspose.PDF 사용)도 지원합니다. 파일 확장자를 교체하기만 하면 됩니다.

### 데이터베이스에 저장된 이미지를 처리하려면?

BLOB을 `MemoryStream`으로 읽은 뒤 `ImageStream.FromStream(memoryStream)`에 전달하면 됩니다. OCR 엔진은 파일 기반 스트림과 동일하게 취급합니다.

### Linux에서도 실행할 수 있나요?

가능합니다—Aspose OCR은 크로스 플랫폼을 지원합니다. 적절한 .NET 런타임을 설치하고, GPU를 사용할 경우 필요한 네이티브 라이브러리가 존재하는지 확인하세요.

---

## Full Working Example (Copy‑Paste Ready)

아래는 전체 프로그램 코드이며, 바로 컴파일할 수 있습니다. `YOUR_DIRECTORY`와 라이선스 파일 경로를 실제 위치로 교체하세요.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace TiffToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Choose processing mode: Gpu, Cpu, or Auto
            ocrEngine.EngineMode = OcrEngineMode.Gpu; // Change to Cpu if no GPU

            // Apply license (skip if you only need a trial)
            ocrEngine.SetLicense("Aspose.OCR.lic");

            // Path to the TIFF file
            string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

            // Load the TIFF (handles multi‑page automatically)
            using (var imageStream = ImageStream.FromFile(tiffPath))
            {
                // Assign image to engine
                ocrEngine.Image = imageStream;

                // Run OCR
                OcrResult result = ocrEngine.Recognize();

                // Display result
                Console.WriteLine("=== OCR Output ===");
                Console.WriteLine(result.Text);
            }

            // Optional: Process each page individually for huge files
            // int pages = ImageInfo.GetPageCount(tiffPath);
            // for (int i = 0; i < pages; i++) { ... }
        }
    }
}
```

`Program.cs`로 저장하고 `dotnet run`을 실행하면 텍스트가 출력되는 것을 확인할 수 있습니다.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}