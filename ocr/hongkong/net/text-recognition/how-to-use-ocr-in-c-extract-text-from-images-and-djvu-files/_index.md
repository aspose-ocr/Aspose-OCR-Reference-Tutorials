---
category: general
date: 2026-04-04
description: 快速且安全地使用 OCR。學習從圖像提取文字、將 DJVU 轉換為文字，並使用 Aspose.OCR 載入圖像進行 OCR。
draft: false
keywords:
- how to use OCR
- extract text from image
- convert djvu to text
- load image for OCR
- extract text from djvu
language: zh-hant
og_description: 如何在 C# 中使用 OCR 從圖像檔案和 DJVU 文件中提取文字。逐步教學，附完整程式碼。
og_title: 如何在 C# 中使用 OCR — 完整指南
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中使用 OCR – 從圖像和 DJVU 檔案中提取文字
url: /zh-hant/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-and-djvu-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 從圖像和 DJVU 檔案提取文字

Ever wondered **如何使用 OCR** to pull words out of a scanned page without manually typing? You're not the only one. In many projects—whether you’re digitizing old books or pulling data from receipts—getting text from an image is a daily pain point. The good news? With Aspose.OCR you can do it in a handful of lines, even when the source is a DJVU file.

In this guide we’ll walk through everything you need to **從圖像提取文字** files, **載入圖像以進行 OCR**, and even **將 DJVU 轉換為文字** using C#. By the end you’ll have a ready‑to‑run console app that prints the recognized text right to the console. No mystery, no extra dependencies, just pure C# and Aspose.

## 您將學習到

- 如何安裝並引用 Aspose.OCR 函式庫。
- 載入圖像以進行 OCR 所需的完整程式碼，無論是 PNG、JPEG 或 DJVU 頁面。
- 如何呼叫引擎並取得結果。
- 處理大型文件與常見陷阱的技巧。
- 完整、可執行的範例，可直接複製貼上至 Visual Studio。

> **先決條件：** .NET 6.0 或更新版本，以及有效的 Aspose.OCR 授權（或免費試用）。如果尚未取得函式庫，請使用 `dotnet add package Aspose.OCR` 從 NuGet 取得。

---

## 如何在 C# 中使用 Aspose 使用 OCR

This is the core step where we actually answer the question **如何使用 OCR** in a C# project. The code below is a full program; you can drop it into a new console app and hit F5.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create the OCR engine instance.
            var ocrEngine = new OcrEngine();

            // Step 2: Load the image (or DJVU page) you want to analyze.
            // Replace the path with your own file location.
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book-page.djvu");

            // Step 3: Run the recognition process.
            OcrResult ocrResult = ocrEngine.Recognize();

            // Step 4: Output the extracted text.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**為什麼這樣可行：**  
- `OcrEngine` 是入口點；它抽象化了影像前處理、語言偵測與字元分類等繁重工作。  
- `ImageStream.FromFile` 能處理多種格式，包括 DJVU，這表示您可以 **將 DJVU 轉換為文字**，無需額外的轉換步驟。  
- `Recognize()` 會回傳 `OcrResult` 物件，內含純文字輸出、信心分數，甚至在需要時的邊界框。

Running the program prints something like:

```
=== OCR Result ===
In the beginning God created the heavens and the earth.
```

That’s it—your first successful **從 DJVU 提取文字** operation.

![如何使用 OCR 範例](/images/ocr-demo.png "顯示如何在 C# 主控台應用程式中使用 OCR 的螢幕截圖")

*替代文字：「如何使用 OCR」主控台輸出螢幕截圖。*

---

## 載入圖像以進行 OCR

Before the engine can read anything, you must **載入圖像以進行 OCR** correctly. Aspose supports most raster formats out‑of‑the‑box, but a few tips can make recognition smoother:

- **將大型圖像調整大小**至長邊最大 2000 像素。過大的檔案會增加記憶體使用並可能減慢引擎速度。  
- **將彩色圖像轉為灰階**，若發現背景雜訊。使用 `ocrEngine.Image = ImageStream.FromFile(path).ConvertToGrayscale();`。  
- **手動設定 DPI** 以應對低解析度掃描（`ocrEngine.Image.DpiX = 300; ocrEngine.Image.DpiY = 300;`）。

These tweaks are optional but often improve the accuracy when you **從圖像提取文字** files like scanned receipts.

---

## 從圖像提取文字 – 最佳實踐

When you’re dealing with typical image formats (PNG, JPEG, BMP), the steps remain the same, but you can fine‑tune the engine:

```csharp
ocrEngine.Image = ImageStream.FromFile("sample.png");

// Optional: enable language packs for better accuracy.
ocrEngine.Language = Language.English;

// Optional: set recognition mode to auto.
ocrEngine.RecognitionMode = RecognitionMode.Auto;
```

- **語言選擇**很重要。若處理多語言文件，請設定 `ocrEngine.Language = Language.Multilingual;`。  
- **RecognitionMode** 可設為 `Auto`、`Fast` 或 `Accurate`。`Accurate` 提供較高品質但較慢——適用於歸檔任務。

---

## 將 DJVU 轉換為文字 – 處理多頁檔案

DJVU files often contain several pages. Aspose treats each page as a separate image stream, so you can loop through them:

```csharp
using Aspose.OCR;
using System.Collections.Generic;

var ocrEngine = new OcrEngine();
List<string> allPagesText = new List<string>();

int pageCount = ImageStream.GetPageCount("book.djvu");
for (int i = 1; i <= pageCount; i++)
{
    ocrEngine.Image = ImageStream.FromFile("book.djvu", i); // Load page i
    OcrResult result = ocrEngine.Recognize();
    allPagesText.Add(result.Text);
}

// Combine all pages into a single string.
string fullText = string.Join("\n--- Page Break ---\n", allPagesText);
Console.WriteLine(fullText);
```

**為什麼要迴圈？**  
DJVU files are essentially a stack of images. By iterating over each page you **從 DJVU 提取文字** in order, preserving the original document flow.

---

## 常見問題與專業提示

| 問題 | 發生原因 | 解決方法 |
|------|----------|----------|
| **雜訊字元** | 解析度過低或壓縮過度 | 放大圖像，設定 `ocrEngine.Image.DpiX/Y = 300` |
| **處理緩慢** | 在大型檔案上使用 `Accurate` 模式 | 切換至 `Fast` 模式以批量處理 |
| **缺少語言支援** | 預設僅支援英文 | 載入額外語言套件（`ocrEngine.Language = Language.Spanish;`） |
| **記憶體不足錯誤** | 一次載入大量高解析度頁面 | 逐頁處理並釋放資源（`ocrEngine.Dispose();`） |

A quick **專業提示**: always call `ocrEngine.Dispose()` after you’re done with a page. It frees native resources and prevents subtle memory leaks that can crash long‑running services.

---

## 測試您的 OCR 流程

To verify everything works, try these simple checks:

1. **列印已辨識字串的長度**: `Console.WriteLine($"Characters recognized: {ocrResult.Text.Length}");`
2. **與已知文字比較**，若有基準文字可使用簡易 diff 函式庫。
3. **記錄信心分數**（`ocrResult.Confidence`），自動偵測低品質頁面。

If the confidence is consistently below 0.7, revisit the image preprocessing steps mentioned earlier.

---

## 下一步

Now that you know **如何使用 OCR**, consider expanding your workflow:

- **批次處理**：將迴圈包在 `Parallel.ForEach` 中，以加速大量集合。  
- **匯出為 PDF**：使用 Aspose.PDF 將辨識文字嵌入為隱藏層，產生可搜尋的 PDF。  
- **結合 AI**：將提取的字串輸入語言模型，以進行摘要或實體抽取。

All of these builds on the same foundation you’ve just set up, and each step benefits from the same **從圖像提取文字** principles we covered.

---

## 結論

We’ve taken a deep dive into **如何使用 OCR** in C# with Aspose, covering everything from loading an image, **從圖像提取文字**, handling **DJVU** files, and troubleshooting common hiccups. The complete, runnable example above gives you a solid starting point, and the tips scattered throughout should help you adapt the solution to real‑world projects.

Give it a try, tweak the settings for your specific documents, and you’ll be turning scanned pages into searchable text in no time. Got questions or a tricky file that refuses to cooperate? Drop a comment—happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}