---
category: general
date: 2026-05-31
description: 學習如何在 C# 中使用 Aspose OCR 進行圖像文字辨識，包括如何從 TIFF 檔案提取文字以及有效載入圖像以執行 OCR。
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- Aspose OCR C#
- GPU accelerated OCR
language: zh-hant
og_description: 使用 Aspose OCR 從圖像辨識文字的逐步指南，涵蓋從 TIFF 提取以及正確載入圖像以供 OCR。
og_title: 使用 Aspose OCR 在 C# 中辨識圖像文字
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to recognize text from image in C# with Aspose OCR, including
    how to extract text from tiff files and load image for OCR efficiently.
  headline: recognize text from image in C# using Aspose OCR
  type: TechArticle
- questions:
  - answer: Reduce its resolution before feeding it to the engine, or increase `GpuMemoryLimit`
      if you have enough VRAM.
    question: What if the image is huge (over 10 MB)?
  - answer: Absolutely. Just reuse the same `OcrEngine` instance and assign a new
      `ImageStream` each iteration.
    question: Can I process multiple images in a loop?
  - answer: '`OcrEngine` implements `IDisposable`. Wrap it in a `using` block for
      clean resource management, especially when working with GPU resources.'
    question: Do I need to dispose of anything?
  - answer: Set `engine.Language = OcrLanguage.Spanish` (or any supported language)
      before calling `Recognize()`.
    question: What about languages other than English?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: 在 C# 中使用 Aspose OCR 進行圖像文字辨識
url: /zh-hant/net/text-recognition/recognize-text-from-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 在 C# 中辨識影像文字

曾經需要**辨識影像中的文字**，卻不知從何下手嗎？你並不孤單——許多開發者在處理掃描文件或多頁 TIFF 時都會卡關。本文將一步步帶你完成一個完整、可直接執行的範例，使用 Aspose OCR 套件**辨識影像文字**，同時示範如何**從 TIFF 中擷取文字**以及最佳的**載入影像供 OCR**方式，讓你不再抓狂。

我們會從安裝 NuGet 套件說起，說明 GPU 加速的使用方式，並在必要時自動回退至 CPU。完成本教學後，你將擁有一個會在主控台印出辨識文字與處理時間的應用程式——不會缺少任何步驟，也不會有模糊的說明。

## 你將會建立的內容

- 一個簡易的 .NET 主控台應用程式，可載入影像（含多頁 TIFF）  
- 一個已設定 GPU 使用的 OCR 引擎，若無 GPU 時會優雅地回退至 CPU  
- 從影像中擷取純文字，並印出至主控台  
- 時間資訊，讓你能比較 GPU 與 CPU 的效能差異  

**先備條件**

- .NET 6 SDK 或更新版本（此程式碼亦相容 .NET Core 與 .NET Framework）  
- 具備 C# 基礎與命令列操作經驗  
- 能連網以下載 Aspose.OCR NuGet 套件  

如果你已符合上述條件，讓我們開始吧。

![使用 Aspose OCR 辨識影像文字的 C# 程式碼](image.png "使用 Aspose OCR 辨識影像文字的 C# 程式碼")

## 第一步 – 辨識影像文字：設定 OCR 引擎

首先，我們需要建立一個 `OcrEngine` 實例。Aspose OCR 讓你自行選擇處理裝置——GPU 以提升速度，CPU 作為安全網。引擎同時接受記憶體上限提示，對於共用機器相當實用。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Create the OCR engine and request GPU acceleration.
        // If no compatible GPU is found, Aspose silently falls back to CPU.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,      // Try GPU first
            GpuMemoryLimit = 1024        // Optional: cap GPU memory usage (MB)
        };
```

**為什麼這很重要：**  
選擇 `OcrDevice.Gpu` 能在處理大型影像（尤其是多頁 TIFF）時省下數秒。`GpuMemoryLimit` 則可防止應用程式在共用工作站上佔用過多 GPU 記憶體。

## 第二步 – 載入影像供 OCR（支援 TIFF）

接著，我們把影像提供給引擎。Aspose 的 `ImageStream.FromFile` 能接受**任何**該函式庫支援的格式——TIFF、PNG、JPEG，隨你喜好。此步驟直接回應**載入影像供 OCR**的需求。

```csharp
        // Load the image you want to process.
        // Replace the path with the actual location of your TIFF or other image.
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");
```

**小技巧：** 若你處理的是多頁 TIFF，Aspose 會自動將每一頁視為獨立的影格，並依序處理，無需額外程式碼。

## 第三步 – 執行辨識並**從 TIFF 中擷取文字**

引擎已備妥且影像已載入，我們即可啟動 OCR 作業。`Recognize` 方法會回傳 `OcrResult`，其中包含純文字、信心分數與時間細節。

```csharp
        // Perform the OCR operation.
        OcrResult result = engine.Recognize();
```

**邊緣案例處理：**  
若 GPU 不可用，`engine.Recognize()` 仍會正常執行，因為引擎會自動切換至 CPU。若需記錄實際使用的裝置，可在辨識後檢查 `engine.Device`。

## 第四步 – 取得辨識出的純文字

擷取文字非常簡單——只要讀取 `Text` 屬性。這就是最終**從 TIFF 中擷取文字**（或任何其他影像）並呈現給使用者的地方。

```csharp
        // Output the plain text that was extracted.
        Console.WriteLine($"Text:\n{result.Text}");
```

你會看到原始字元，且換行會依原始影像的排版保留。若需要更結構化的輸出（例如 JSON 或 CSV），可深入 `result.Regions` 與 `result.Lines`，但對於快速腳本而言，純文字已足夠。

## 第五步 – 測量處理時間並處理 GPU 回退

效能很重要，特別是當你一次處理數十頁時。`ProcessingTime` 屬性會精確告訴你 OCR 花了多久，無論是跑在 GPU 還是 CPU。

```csharp
        // Show how long the recognition took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**為什麼你應該在意：**  
如果發現時間急速上升，可能需要調整 `GpuMemoryLimit`，或明確改為使用 CPU（`Device = OcrDevice.Cpu`）。相反地，若在大型 TIFF 上只花不到一秒，就代表 GPU 加速發揮了效用。

## 完整、可直接執行的範例

將下列程式碼複製到新建的主控台專案（`dotnet new console -n OcrDemo`）中，執行 `dotnet add package Aspose.OCR` 安裝套件。接著把 `YOUR_DIRECTORY/sample_multi_page.tif` 替換成你的影像路徑。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine with GPU preference.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,
            GpuMemoryLimit = 1024
        };

        // Step 2: Load image for OCR (supports TIFF, PNG, JPEG, etc.).
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");

        // Step 3: Run recognition – this will also **extract text from tiff**.
        OcrResult result = engine.Recognize();

        // Step 4: Retrieve and display the recognized plain text.
        Console.WriteLine($"Text:\n{result.Text}");

        // Step 5: Display how long the operation took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**預期輸出（為簡潔起見已截斷）：**

```
Text:
Invoice #12345
Date: 2026-05-01
Total: $1,250.00
...
Time elapsed: 1.42s
```

若你的機器沒有可用的 GPU，耗時可能會多幾秒，但文字仍會正確擷取。

## 常見問題與注意事項

- **如果影像非常大（超過 10 MB）怎麼辦？**  
  在送入引擎前降低解析度，或在有足夠 VRAM 時提升 `GpuMemoryLimit`。  
- **可以在迴圈中處理多張影像嗎？**  
  當然可以。只要在每次迭代時重新指派 `ImageStream`，並重複使用同一個 `OcrEngine` 實例。  
- **需要手動釋放資源嗎？**  
  `OcrEngine` 實作 `IDisposable`。建議使用 `using` 區塊來確保資源（尤其是 GPU 資源）能被正確釋放。  

```csharp
using (OcrEngine engine = new OcrEngine { Device = OcrDevice.Gpu })
{
    // ... same steps as before
}
```

- **支援非英語語系嗎？**  
  在呼叫 `Recognize()` 前設定 `engine.Language = OcrLanguage.Spanish`（或任何支援的語言）。  

## 結論

現在你已擁有一套完整、端到端的解決方案，能在 C# 中使用 Aspose OCR **辨識影像文字**。本教學說明了如何**載入影像供 OCR**、如何**從 TIFF 中擷取文字**，以及如何在衡量效能的同時優雅地處理 GPU 回退。

接下來你可以：

- 嘗試不同的影像格式（BMP、PDF），觀察 Aspose 的處理方式。  
- 深入 `result.Regions` 取得邊界框資料，若需要版面感知的應用。

## 接下來該學什麼？

- [如何在 OCR 影像辨識中使用 Aspose 以串流方式辨識影像](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [使用 Aspose.OCR for .NET 進行影像文字擷取與效能最佳化](/ocr/english/net/ocr-optimization/)
- [使用 Aspose.OCR 辨識影像文字 – 行辨識](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}