---
category: general
date: 2026-06-06
description: 使用 C# OCR 識別文字圖像 – 一個一步一步的 C# OCR 範例，可從掃描文件中提取文字，並在數分鐘內將掃描轉換為文字。
draft: false
keywords:
- recognize text image
- c# ocr example
- extract text scan
- convert scan to text
- image to text c#
language: zh-hant
og_description: 使用 C# OCR 識別文字圖像。學習一個實用的 C# OCR 範例，從掃描檔中提取文字，將掃描轉換為文字，並處理真實世界的圖像。
og_title: 在 C# 中辨識文字圖像 – 完整 OCR 教學
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: recognize text image using C# OCR – a step‑by‑step c# ocr example that
    extracts text from scans and convert scan to text in minutes.
  headline: recognize text image in C# – Full OCR Guide
  type: TechArticle
- questions:
  - answer: The `Windows.Media.Ocr` namespace is Windows‑only. On Linux or macOS you’d
      swap it for TesseractSharp or IronOcr—both expose a similar `Engine.Recognize`
      method, so the surrounding code stays virtually unchanged.
    question: Does this work on .NET Core on Linux?
  - answer: Handwriting recognition is still experimental. For best results, stick
      to printed fonts or consider a cloud service like Azure Cognitive Services if
      you need high accuracy.
    question: How accurate is the built‑in OCR for handwritten notes?
  - answer: 'Not out of the box. Convert each PDF page to an image first (using `PdfSharp`
      or `Ghostscript`) and then feed the bitmap to the OCR engine. --- ## Conclusion
      You now have a complete, production‑ready **c# ocr example** that can **recognize
      text image** files, **extract text scan** contents, and **co'
    question: Can I process PDFs directly?
  type: FAQPage
tags:
- OCR
- C#
- Image Processing
title: 在 C# 中辨識文字圖像 – 完整 OCR 指南
url: /zh-hant/net/text-recognition/recognize-text-image-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中辨識文字圖像 – 完整 OCR 教學

有沒有想過如何使用 C# 直接從掃描的相片 **recognize text image**？你並不是唯一有此疑問的人。無論是將舊收據數位化、從名片提取資料，或是把低解析度的掃描檔轉成可編輯的文字，從圖像中抽取文字的能力都是每位開發者工具箱中實用的技巧。

在本指南中，我們將逐步說明一個 **c# ocr example**，它會載入圖片、執行光學字元辨識，並將結果輸出到主控台。完成後，你將能夠 **extract text scan** 檔案、**convert scan to text**，甚至針對噪點圖像進行微調。無需任何高階第三方服務——只需內建的 Windows.Media.Ocr API（或任何相容的 OcrEngine）以及少量程式碼。

## 你將學到什麼

* 如何為 OCR 設定 C# 專案。
* 取得處理 **recognize text image** 檔案的完整程式碼。
* 處理低解析度掃描與多頁文件的技巧。
* 將範例擴充為可重用函式庫，以供自己的應用程式使用的方法。

### 前置條件

* .NET 6.0 或更新版本（此 API 亦支援 .NET 5+）。
* Visual Studio 2022（Community 版亦可）或任何你喜歡的 IDE。
* 一張範例圖片，例如 `lowres_scan.jpg`，放在可參考的資料夾中。
* 具備 async/await 的基本概念——OCR 呼叫在 Windows API 中為非同步。

> **Pro tip:** 如果你在非 Windows 平台，請將 `Windows.Media.Ocr` 命名空間改為跨平台的函式庫，例如 TesseractSharp；其餘邏輯保持不變。

---

## 步驟 1：使用 OCR 引擎設定 **recognize text image**

首先，我們需要一個 OCR 引擎實例。`OcrEngine` 類別是任何 **image to text c#** 操作的入口點。

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Create the OCR engine – default language is English.
        OcrEngine engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));
        if (engine == null)
        {
            Console.WriteLine("Failed to create OcrEngine. Make sure you are on Windows 10 version 1809 or later.");
            return;
        }

        // Continue with the rest of the pipeline...
```

**Why this matters:** 引擎抽象化了模式辨識的繁重工作。透過明確建立它，我們可以控制語言設定，這在之後想要 **extract text scan** 其他語言的文件時尤為重要。

## 步驟 2：載入影像檔案 – **convert scan to text** 的核心

接著，我們從磁碟讀取影像，並將其轉換為 `SoftwareBitmap`，這是 OCR 引擎所期待的格式。

```csharp
        // Load the image file into a SoftwareBitmap.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "lowres_scan.jpg");
        using (FileStream fs = new FileStream(imagePath, FileMode.Open, FileAccess.Read))
        {
            // Decode the image (supports JPEG, PNG, BMP, etc.).
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Optional: upscale low‑resolution images for better accuracy.
            SoftwareBitmap upscaled = SoftwareBitmap.Convert(bitmap, bitmap.BitmapPixelFormat, bitmap.BitmapAlphaMode);
            // Pass the bitmap to OCR.
            await RecognizeAsync(engine, upscaled);
        }
    }
```

**Why we do this:** 直接將原始檔案串流餵入 OCR 常會得到不佳的結果，尤其是低解析度的掃描。轉換成 `SoftwareBitmap` 後，我們可以在辨識前調整 DPI、色深，甚至套用濾鏡。

## 步驟 3：執行 **recognize text image** 操作

現在我們終於呼叫引擎的 `RecognizeAsync` 方法。這就是魔法發生的地方。

```csharp
    private static async Task RecognizeAsync(OcrEngine engine, SoftwareBitmap bitmap)
    {
        // Run OCR – this returns an OcrResult object.
        OcrResult result = await engine.RecognizeAsync(bitmap);

        // The Result contains a collection of lines and words.
        Console.WriteLine("=== OCR Output ===");
        foreach (var line in result.Lines)
        {
            Console.WriteLine(line.Text);
        }

        // For a quick **image to text c#** check, also output the raw string.
        Console.WriteLine("\nFull Text:\n" + result.Text);
    }
}
```

**What you’ll see:** 若 `lowres_scan.jpg` 包含「Hello World」這句話，主控台將會印出：

```
=== OCR Output ===
Hello World

Full Text:
Hello World
```

這就是完整的 **c# ocr example** 實作——僅四個邏輯步驟，卻涵蓋了從檔案載入到最終輸出的全部。

## 步驟 4：處理邊緣情況 – 當掃描不完美時

實際的影像未必總是清晰。以下是幾項可在不重寫整個程式的情況下調整的方式：

| 問題 | 快速解決方案 |
|-------|-----------|
| **Very low DPI (≤ 72)** | 在辨識前使用 `BitmapTransform` 將位圖放大。 |
| **Skewed text** | 套用旋轉變換 (`SoftwareBitmap.Rotate`) 以校正頁面。 |
| **Multiple languages** | 建立 `OcrEngine.TryCreateFromLanguage(new OcrLanguage("en-fr"))` 並相應設定 `engine.Language`。 |
| **Large files** | 將影像分割成區塊 (`engine.RecognizeAsync(tileBitmap)`) 處理，然後串接結果。 |

這些微調可確保你的 **extract text scan** 程序在處理噪點收據或斜拍照片時仍保持可靠。

## 步驟 5：將範例轉換為可重用的輔助程式（可選）

如果你打算在應用程式的多個部分 **convert scan to text**，可以將邏輯封裝在一個小型工具類別中：

```csharp
public static class OcrHelper
{
    private static readonly OcrEngine _engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));

    public static async Task<string> ImageToTextAsync(string filePath)
    {
        using var fs = new FileStream(filePath, FileMode.Open, FileAccess.Read);
        var decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
        var bitmap = await decoder.GetSoftwareBitmapAsync();

        var result = await _engine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

現在只要呼叫：

```csharp
string text = await OcrHelper.ImageToTextAsync("YOUR_DIRECTORY/lowres_scan.jpg");
Console.WriteLine(text);
```

**Why you’ll love this:** 這個輔助程式將 OCR 的底層實作隔離，讓你專注於業務邏輯——非常適合在多個專案中重用的 **c# ocr example**。

---

![recognize text image example](https://example.com/ocr-demo.png "Screenshot of OCR console output showing recognize text image result")

*替代文字:* **recognize text image** output from a C# OCR console application.

---

## 常見問題

**Q: 這在 Linux 上的 .NET Core 能運作嗎？**  
A: `Windows.Media.Ocr` 命名空間僅限 Windows。於 Linux 或 macOS 上，你可以改用 TesseractSharp 或 IronOcr——兩者皆提供類似的 `Engine.Recognize` 方法，因而周邊程式碼基本保持不變。

**Q: 內建的 OCR 對手寫筆記的準確度如何？**  
A: 手寫辨識仍屬實驗性。若要取得最佳效果，建議使用印刷字體，或在需要高準確度時考慮使用 Azure Cognitive Services 等雲端服務。

**Q: 能直接處理 PDF 嗎？**  
A: 直接支援尚未提供。必須先將每頁 PDF 轉為影像（使用 `PdfSharp` 或 `Ghostscript`），再將位圖餵入 OCR 引擎。

## 結論

現在你已擁有一個完整、可投入生產環境的 **c# ocr example**，它能夠 **recognize text image** 檔案、**extract text scan** 內容，並 **convert scan to text**，僅需幾行程式碼。透過了解整個流程——引擎建立、影像載入、非同步辨識與結果處理——你可以將此模式套用到任何需要將圖片轉為可搜尋字串的 C# 專案。

準備好進一步了嗎？試著使用 WinForms 或 WPF 加入簡易 UI、實驗不同語言，或將輸出接入資料庫以建立可搜尋的檔案庫。當你掌握 **image to text c#** 技術時，無所不能。

祝編程愉快，願你的掃描檔永遠清晰！

## 接下來該學什麼？

以下教學涵蓋與本指南技術密切相關的主題，並以完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [使用 Aspose.OCR 進行語言選擇的 C# 影像文字抽取](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [將影像轉換為文字 – 從 URL 執行 OCR](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [如何透過在 OCR 中準備矩形來抽取影像文字](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}