---
category: general
date: 2026-03-04
description: 使用 Aspose OCR 在 C# 中從圖像提取文字。了解如何載入圖像進行 OCR，並高效辨識 TIFF 檔案中的文字。
draft: false
keywords:
- extract text from image
- load image for ocr
- recognize text from tiff
- Aspose OCR C#
- GPU OCR engine
language: zh-hant
og_description: 使用 Aspose OCR 在 C# 中從圖像提取文字。本指南展示如何載入圖像進行 OCR，並使用 GPU 引擎辨識 TIFF 檔案中的文字。
og_title: 使用 Aspose OCR 從圖像提取文字 – C# 教程
tags:
- OCR
- C#
- Aspose
- GPU
title: 使用 Aspose OCR 從圖片提取文字 – 完整 C# 指南
url: /zh-hant/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從影像提取文字 – Aspose OCR 完整 C# 指南

曾經需要**從影像提取文字**，卻不確定哪個函式庫能同時提供速度與準確度嗎？你並不孤單——許多開發者在處理掃描的 PDF 或 TIFF 檔案時都會碰到這個問題。好消息是，Aspose OCR 結合 GPU 加速引擎，讓整個流程變得輕鬆自如。

在本教學中，我們將示範如何**載入影像以供 OCR**、設定 GPU 引擎，最後**從 TIFF 檔案辨識文字**，只需幾行程式碼。完成後，你將擁有一個可執行的主控台應用程式，將提取的文字輸出到螢幕，並了解每一步背後的「原因」。

## 你將學會

- 如何安裝與參考 Aspose.OCR NuGet 套件。
- 為何 GPU 加速的 `GpuOcrEngine` 能大幅縮短處理時間。
- 使用 `ImageInfo` 正確**載入影像以供 OCR**的方法。
- 如何設定語言與記憶體限制。
- 如何**從 TIFF 辨識文字**並處理常見陷阱。

不需要任何 Aspose 的先前經驗；只要具備 C# 與 .NET 的基本知識即可。讓我們開始吧。

---

## 步驟 1：從影像提取文字 – 初始化 GPU OCR 引擎

我們首先需要一個能真正讀取像素的 OCR 引擎。Aspose 提供的 `GpuOcrEngine` 會將繁重的運算交給顯示卡處理。當你有數十個高解析度 TIFF 等待排程時，這特別有用。

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Create a GPU‑enabled OCR engine.
// Setting GpuMemoryLimit helps avoid out‑of‑memory crashes on modest GPUs.
GpuOcrEngine ocrEngine = new GpuOcrEngine
{
    GpuMemoryLimit = 1024 // limit to 1024 MB
};
```

**為何這很重要：**  
僅使用 CPU 的引擎會逐一掃描每個像素，對於大型影像而言會非常緩慢。透過限制 GPU 記憶體，可保持流程輕量，同時仍獲得效能提升。

> **小技巧：** 若在沒有 GPU 的伺服器上執行，請改用 `OcrEngine`——API 完全相同，只要更換類別名稱即可。

---

## 步驟 2：載入影像以供 OCR – 準備 TIFF 檔案

引擎已就緒後，我們需要**載入影像以供 OCR**。Aspose 的 `ImageInfo.Load` 支援多種格式，包括多頁 TIFF。只要指向你的檔案，剩下的交給函式庫處理。

```csharp
// Replace the path with the location of your TIFF file.
string imagePath = @"YOUR_DIRECTORY/english_page.tif";

// Load the image into an ImageInfo object.
// ImageInfo abstracts away format specifics, giving you a uniform API.
ImageInfo image = ImageInfo.Load(imagePath);
```

**邊緣情況：**  
如果你的 TIFF 包含多頁，可遍歷 `image.Pages` 並逐一處理。對於大多數單頁掃描，上述程式碼已足夠。

---

## 步驟 3：從 TIFF 辨識文字 – 執行 OCR

影像已載入記憶體且引擎已就緒，我們終於可以**從 TIFF 辨識文字**。`Recognize` 方法會回傳 `OcrResult` 物件，內含提取的字串、信心分數，甚至在之後需要時的邊界框。

```csharp
// Set the language you expect in the image.
// English is the default, but you can combine languages like Language.English | Language.Spanish.
ocrEngine.Language = Language.English;

// Run the OCR process.
OcrResult ocrResult = ocrEngine.Recognize(image);
```

**為何語言設定重要：**  
指定正確的語言能顯著提升準確度，因為引擎會套用特定語言的字典與字元模型。

---

## 步驟 4：輸出提取的文字

最後一步很簡單——只要將結果寫入主控台、檔案或資料庫。本範例保持簡潔，直接在螢幕上顯示文字。

```csharp
// Print the recognized text.
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrResult.Text);
```

**預期輸出：**  
如果 `english_page.tif` 包含印刷段落，將會看到類似以下內容：

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

若 OCR 表現不佳，文字可能出現異常字元；調整 `GpuMemoryLimit` 或提供更高解析度的原始影像通常能改善。

---

## 完整可執行範例

以下是完整、獨立的程式碼，你可以直接複製貼上到新的 Console App 專案中。它可在 .NET 6 或更新版本編譯。

```csharp
// ------------------------------------------------------------
// Complete C# program to extract text from image using Aspose OCR.
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize GPU OCR engine with a memory cap.
        GpuOcrEngine ocrEngine = new GpuOcrEngine
        {
            GpuMemoryLimit = 1024 // MB
        };

        // 2️⃣ Choose the language for recognition.
        ocrEngine.Language = Language.English;

        // 3️⃣ Load the image you want to process.
        // Make sure the path points to a valid TIFF file.
        string imagePath = @"YOUR_DIRECTORY/english_page.tif";
        ImageInfo image = ImageInfo.Load(imagePath);

        // 4️⃣ Perform OCR – this returns the recognized text.
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Display the result.
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);

        // Keep the console window open when debugging.
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

儲存檔案後，執行 `dotnet run`，即可在主控台看到提取的內容。簡單吧？

---

## 常見問題與邊緣情況

**如果我的影像是 PNG 或 JPEG 而非 TIFF 該怎麼辦？**  
`ImageInfo.Load` 幾乎支援所有點陣圖格式，你只要更換副檔名，其他程式碼保持不變。無需額外修改。

**我的 OCR 回傳亂碼——我該檢查什麼？**  
1. 確認影像解析度（理想為 300 dpi 或更高）。  
2. 確保設定正確的 `Language`；語言不符會降低字典支援。  
3. 若影像非常大，請提升 `GpuMemoryLimit`；引擎可能因資源受限而降速。

**我能批次處理多個檔案嗎？**  
當然可以。將載入與辨識步驟包在 `foreach (var file in Directory.GetFiles(...))` 迴圈中。若處理數百個檔案，請記得釋放每個 `ImageInfo` 以釋放原生資源。

**執行此程式碼需要 GPU 嗎？**  
不需要。若沒有相容的 GPU，只需將 `GpuOcrEngine` 換成一般的 `OcrEngine`。API 呼叫（`Recognize`、`Language` 等）保持不變。

---

## 效能技巧 – 讓 GPU OCR 發揮最大效益

- **重複使用引擎：** 為每張影像建立新的 `GpuOcrEngine` 會產生額外開銷。請只實例化一次，於多個檔案間重複使用。  
- **批次處理：** 先將多張影像載入記憶體，再依序呼叫 `Recognize`；GPU 保持熱態，處理速度更快。  
- **調整記憶體限制：** 在 4 GB VRAM 的機器上，設定 1024 MB 限制較安全；高階工作站可提升至 4096 MB，以處理更大的批次。

---

## 結論

你剛剛學會了如何使用 Aspose OCR 的 GPU 引擎**從影像提取文字**、正確**載入影像以供 OCR**，以及在乾淨、可投入生產的 C# 主控台應用程式中**從 TIFF 辨識文字**。程式碼可直接執行，說明同時涵蓋「如何」與「為何」，讓你具備堅實基礎，能應對更複雜的 OCR 情境——例如多語言文件或即時相機影像。

準備好迎接下一個挑戰了嗎？試著將範例擴充為輸出至 CSV，或利用 `BoundingBox` 資料在原始影像上標示辨識出的文字。可能性無窮，而 GPU 加速帶來的效能提升將讓你的工作流程更敏捷。

如果你覺得本指南對你有幫助，請在 GitHub 上給予星標，與同事分享，或在下方留言分享你的技巧。祝開發愉快！  

![使用 Aspose OCR 從影像提取文字](placeholder.png){alt="使用 Aspose OCR 從影像提取文字"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}