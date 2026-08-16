---
category: general
date: 2026-03-29
description: Aspose를 사용하여 PNG 파일에서 텍스트를 추출하고 이미지를 텍스트로 변환하는 방법. C#에서 단계별 비동기 OCR을
  배워보세요.
draft: false
keywords:
- how to use OCR
- extract text from png
- convert images to text
- extract text from images
language: ko
og_description: C#에서 Aspose를 사용해 PNG 파일의 텍스트를 추출하는 OCR 사용 방법. 이 가이드는 비동기 OCR, 코드 및
  팁을 안내합니다.
og_title: C#에서 OCR 사용 방법 – PNG 이미지에서 텍스트 추출
tags:
- OCR
- C#
- Aspose
title: C#에서 OCR 사용 방법 – PNG 이미지에서 텍스트를 빠르게 추출하기
url: /ko/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-png-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 OCR 사용 방법 – PNG 이미지에서 텍스트를 빠르게 추출하기

몇 장의 PNG 스크린샷에서 **OCR을 사용해 텍스트를 추출**하는 방법이 궁금하신가요? 스캔한 영수증, 청구서, UI 목업 등이 있고 이를 검색 가능한 형식으로 변환해야 할 때가 있죠. 좋은 소식은 Aspose.OCR을 사용하면 비동기 C# 코드 몇 줄만으로 이미지를 텍스트로 변환할 수 있다는 것입니다.  

이 튜토리얼에서는 PNG 파일에서 텍스트를 추출하는 정확한 방법을 보여주고, 각 단계가 왜 중요한지 설명하며, 모든 페이지에 대해 인식된 텍스트를 출력하는 실행 가능한 프로그램을 제공합니다. 끝까지 읽으면 **이미지에서 텍스트를 추출**하는 방법을 문서 찾아 헤매지 않고 바로 사용할 수 있게 됩니다.

## 배울 내용

- Aspose.OCR NuGet 패키지를 설치하고 참조하기.  
- OCR 엔진을 초기화하고 언어를 설정하기 (예제에서는 English).  
- `RecognizeImagesAsync`에 PNG 파일 배열을 전달해 빠르고 논블로킹 방식으로 처리하기.  
- `OcrResult` 객체들을 순회하며 추출된 문자열을 출력하기.  

외부 서비스 없이, 복잡한 콜백 없이—.NET 6+에서 동작하는 깔끔한 async C# 코드만 있으면 됩니다.

---

## 사전 요구 사항

| Requirement | Reason |
|-------------|--------|
| .NET 6 SDK (or later) | `async Main` 같은 최신 언어 기능 사용 가능. |
| Visual Studio 2022 or VS Code | 코드를 컴파일하고 실행할 IDE. |
| Aspose.OCR NuGet package (`Aspose.OCR`) | 샘플에서 사용하는 `OcrEngine` 클래스를 제공. |
| A few PNG images (`page1.png`, `page2.png`, …) | OCR 프로세스에 사용할 입력 파일. |

이미 .NET 프로젝트가 있다면 `dotnet add package Aspose.OCR`만 실행하면 됩니다. 그렇지 않다면 `dotnet new console -n OcrDemo`로 새 콘솔 앱을 만들고 진행하세요.

---

## Step 1: Install Aspose.OCR and Set Up the Project

First, add the OCR library to your project:

```bash
dotnet add package Aspose.OCR
```

Why this matters: Aspose.OCR bundles the native OCR engine, language packs, and a simple API. By pulling it via NuGet you guarantee version compatibility and automatic updates.

---

## Step 2: Initialize the OCR Engine and Choose a Language

The engine needs to know which language to look for. English is the most common, but you can swap `Language.Spanish`, `Language.French`, etc.

```csharp
using Aspose.OCR;

// ...

// Step 2: Create the engine and set the language to English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // Change this if you need a different language
};
```

> **Pro tip:** Always set the language explicitly; leaving it at the default can degrade accuracy and increase processing time.

---

## Step 3: Prepare the List of PNG Files

You can feed a single file or an array. Supplying an array lets the engine batch‑process them asynchronously, which is ideal for a handful of pages.

```csharp
// Step 3: Define the image files you want to process
string[] imagePaths = { "page1.png", "page2.png", "page3.png" };
```

If your images live in a subfolder, just prepend the relative path (`"images/page1.png"`). The engine will throw a clear `FileNotFoundException` if a path is wrong—so double‑check the filenames.

---

## Step 4: Run Asynchronous OCR on All Images

The `RecognizeImagesAsync` method returns an array of `OcrResult`. Because it’s async, your UI (or console) stays responsive while the OCR runs in the background.

```csharp
// Step 4: Perform async OCR on every image
OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);
```

**Why async?**  
If you’re integrating OCR into a web API or a desktop app, you don’t want the thread to block while the engine scans each pixel. `await` releases the thread back to the thread pool, improving scalability.

---

## Step 5: Display the Extracted Text for Each Page

Now that we have the results, iterate through them and print the recognized text. The `Text` property contains the plain‑text output, ready for further processing (e.g., saving to a database).

```csharp
// Step 5: Output the recognized text for every page
for (int i = 0; i < ocrResults.Length; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

### Expected Output

Assuming `page1.png` contains “Invoice #12345” and `page2.png` holds “Total: $89.99”, you’ll see something like:

```
--- Page 1 ---
Invoice #12345
Date: 03/28/2026
--- Page 2 ---
Total: $89.99
Paid by: Credit Card
```

If the OCR fails to locate any text, the `Text` property will be an empty string—handle that case in production code by checking `string.IsNullOrWhiteSpace`.

---

## Full Working Example

Below is the complete program you can copy‑paste into `Program.cs`. It includes all the using directives, async `Main`, and comments that clarify each step.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    // Async Main is supported from C# 7.1 onward
    static async Task Main()
    {
        // Step 1: Initialize the OCR engine and set the language to English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Step 2: Define the image files to be processed
        string[] imagePaths = { "page1.png", "page2.png", "page3.png" };

        // Step 3: Perform asynchronous OCR on all images
        OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);

        // Step 4: Output the recognized text for each page
        for (int i = 0; i < ocrResults.Length; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].Text);
        }
    }
}
```

Save the file, place your PNGs next to the executable (or adjust the paths), and run:

```bash
dotnet run
```

You should see the extracted text printed to the console, confirming that you’ve successfully **converted images to text**.

---

## Handling Common Edge Cases

| Situation | What to Do |
|-----------|------------|
| **Low‑resolution PNG** | Increase `ocrEngine.ImageProcessingOptions.Dpi` before recognition. |
| **Multiple languages** | Set `ocrEngine.Language = Language.English \| Language.Spanish;` (bitwise OR). |
| **Large batch (hundreds of files)** | Process in chunks (e.g., 20 files per `RecognizeImagesAsync` call) to avoid memory spikes. |
| **Need the confidence score** | Use `ocrResults[i].Confidence` (a float between 0 and 1) to filter low‑quality results. |

These tweaks keep your OCR pipeline robust, especially when you move from a demo to production.

---

## Bonus: Saving the Results to a Text File

If you prefer a persistent copy rather than console output, add a tiny helper:

```csharp
using System.IO;

// After the for‑loop:
File.WriteAllLines("OcrOutput.txt", ocrResults.Select(r => r.Text));
Console.WriteLine("All pages saved to OcrOutput.txt");
```

Now you have a single file that **extracts text from images** for downstream processing—perfect for indexing, searching, or feeding into a language model.

---

## Conclusion

We’ve walked through **how to use OCR** in C# with Aspose to **extract text from PNG** files and **convert images to text** efficiently. The async approach ensures your application stays responsive, while the straightforward API keeps the code readable and maintainable.  

Give it a spin with your own documents, experiment with different languages, and maybe even chain the output into a search index or a summarization service. The sky’s the limit when you can reliably turn pictures into searchable strings.

---

### Next Steps & Related Topics

- **Extract text from images** in other formats (JPEG, TIFF) – just change the file extensions.  
- **Batch processing with Parallel.ForEach** for massive workloads.  
- **Post‑OCR cleanup** using regular expressions to normalize dates, amounts, or IDs.  
- **Integrate with Azure Cognitive Services** if you need cloud‑based OCR with additional features.  

Feel free to drop a comment if you hit any snags, or share how you’ve extended this basic flow. Happy coding!   (Image: ![OCR result screenshot showing extracted text](/images/ocr-result.png){.align-center alt="how to use OCR example output"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}