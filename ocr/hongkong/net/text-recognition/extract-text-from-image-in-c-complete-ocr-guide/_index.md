---
category: general
date: 2026-04-11
description: 使用 Aspose OCR 於 C# 從圖像提取文字。了解如何載入圖像進行 OCR，並在支援 GPU 的情況下辨識 TIFF 檔案的文字。
draft: false
keywords:
- extract text from image
- load image for OCR
- recognize text from TIFF
- Aspose OCR C#
- GPU OCR processing
- high‑resolution OCR
language: zh-hant
og_description: 使用 Aspose OCR 在 C# 中從圖像擷取文字。本教學示範如何載入圖像進行 OCR，並使用 GPU 加速從 TIFF 識別文字。
og_title: 在 C# 中從圖像提取文字 – 完整 OCR 指南
tags:
- OCR
- C#
- Aspose
- GPU
title: 在 C# 中從圖像提取文字 – 完整 OCR 指南
url: /zh-hant/net/text-recognition/extract-text-from-image-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像中提取文字（C#） – 完整 OCR 指南

曾經需要 **從圖像中提取文字**，卻不確定哪個函式庫能處理巨大的 TIFF 而不會卡住嗎？你並不孤單。在許多實務專案中——例如發票數位化或掃描書籍的存檔——能夠載入圖像進行 OCR，然後從 TIFF 識別文字，往往是成敗關鍵。

在本指南中，我們將手把手示範使用 Aspose OCR for .NET 完成此任務。完成後，你將擁有一個可執行的 C# 主控台應用程式，能載入高解析度掃描檔、啟動 GPU 加速處理（若無 GPU 會自動退回 CPU），並輸出純文字結果。沒有遺漏，沒有「請參考文件」的死胡同。

## 您需要的條件

- **.NET 6 或更新版本**（程式碼可在任何近期 SDK 上編譯）
- **Aspose.OCR for .NET** NuGet 套件  
  `dotnet add package Aspose.OCR`
- 一個 **大型 TIFF** 或任何其他想要 OCR 的影像格式  
  （範例使用 `large_scan.tif`）
- （可選）支援 CUDA 11+ 的 GPU —— 若沒有，函式庫會自動切換至 CPU 模式。

就這樣。讓我們開始吧。

![Extract text from image using Aspose OCR in C#](image-placeholder.png "Extract text from image using Aspose OCR in C#")

## 步驟 1：提取文字 – 初始化 OCR 引擎

在處理任何影像之前，你需要建立一個 `OcrEngine` 實例。此引擎保存所有控制辨識執行方式的設定。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // Initialise the OCR engine and request GPU processing.
        // ProcessingMode.Auto tells Aspose to fall back to CPU if a GPU isn’t detected.
        var ocrEngine = new OcrEngine
        {
            Settings = { ProcessingMode = ProcessingMode.Gpu }
        };

        // Optional: cap GPU memory usage to avoid OOM on shared machines.
        ocrEngine.Settings.GpuMemoryLimit = 1024; // MB
```

**為什麼這很重要：**  
`ProcessingMode.Gpu` 能在現代顯示卡上為辨識時間削減數秒，但將 `ProcessingMode.Auto`（或保留預設）設定為較安全，因為在沒有 GPU 的環境中不會出錯。`GpuMemoryLimit` 的限制是一個實用技巧——若不設此限制，巨大的影像可能會佔用全部 VRAM，導致其他應用程式崩潰。

## 步驟 2：載入影像供 OCR 使用 – 把 TIFF 讀入記憶體

引擎已就緒後，我們需要將要分析的圖片傳入。Aspose 提供的 `ImageStream.FromFile` 會抽象化格式處理。

```csharp
        // Load the high‑resolution TIFF you want to OCR.
        // Replace the path with the location of your own file.
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/large_scan.tif");
```

**底層發生了什麼？**  
`ImageStream.FromFile` 會將檔案讀入串流，並自動偵測影像格式（TIFF、PNG、JPEG 等）。若你處理的是多頁 TIFF，Aspose 會將每一頁視為獨立的框格；之後如有需要可自行迭代。

## 步驟 3：辨識 TIFF 文字 – 執行 OCR 引擎

影像載入後，重活就開始了。`Recognize` 方法會回傳一個 `OcrResult` 物件，內含提取的文字以及一些實用的中繼資料欄位。

```csharp
        // Perform the OCR operation.
        var ocrResult = ocrEngine.Recognize(image);
```

**為什麼只呼叫一次 `Recognize`？**  
因為引擎在第一次執行後會快取內部結構，對大多數情境而言一次呼叫已足夠。若需處理多頁，請重複使用同一個 `OcrEngine` 實例——這樣可避免重新初始化 GPU 上下文的開銷。

## 步驟 4：顯示結果 – 展示提取的文字

最後，我們將辨識出的字串輸出到主控台。實際應用中，你可能會把它寫入資料庫或檔案。

```csharp
        // Show the extracted plain text.
        Console.WriteLine(ocrResult.Text);
    }
}
```

**預期輸出：**  
如果 `large_scan.tif` 包含一張印刷發票，你會看到類似以下的內容：

```
Invoice #12345
Date: 2024‑03‑15
Total: $1,234.56
...
```

具體版面會依原始影像而異，但重點是你現在已取得 **extract text from image** 的結果，準備進行後續處理。

## 步驟 5：故障排除與特殊情況

### GPU 未偵測到？

如果在沒有相容 GPU 的機器上執行範例，使用 `ProcessingMode.Auto` 時引擎會靜默退回 CPU。若想明確強制使用 CPU，請將先前的程式碼行改為：

```csharp
ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
```

### 記憶體需求高的 TIFF

極大尺寸的掃描（例如 10 000 × 10 000 px）仍可能超過我們設定的 1 GB GPU 上限。此時，可提升 `GpuMemoryLimit`（前提是有剩餘 VRAM），或在送入引擎前先縮小影像：

```csharp
var resized = image.Resize(4000, 4000); // keep aspect ratio as needed
var ocrResult = ocrEngine.Recognize(resized);
```

### 多頁文件

若你的 TIFF 包含多頁，請使用迴圈逐頁處理：

```csharp
for (int i = 0; i < image.PageCount; i++)
{
    var pageStream = image.GetPage(i);
    var result = ocrEngine.Recognize(pageStream);
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(result.Text);
}
```

### 語言與字型支援

Aspose OCR 會自動偵測拉丁系文字，但若要辨識西里爾文、阿拉伯文或自訂字型，可能需要額外提供語言套件：

```csharp
ocrEngine.Settings.Language = Language.Russian; // example
```

## 專業提示與最佳實踐

- **重複使用引擎**：每張影像都重新建立 `OcrEngine` 會增加明顯的延遲。
- **批次處理**：處理數十張 TIFF 時，可將它們排入佇列並以平行執行緒處理——但要留意 GPU 記憶體的競爭情形。
- **驗證輸出**：OCR 並非完美；可對 `ocrResult.Text` 執行簡易拼寫檢查或正規表達式驗證，以捕捉明顯的錯誤辨識。
- **記錄效能**：在 `Recognize` 前後使用 `Stopwatch` 計算耗時，判斷在你的環境中 GPU 加速是否值得額外的設定成本。

## 結論

你現在擁有一個完整、端對端的範例，能使用 Aspose OCR 在 C# 中 **extract text from image** 檔案。透過載入影像、呼叫引擎辨識 TIFF 文字，並處理 GPU 與 CPU 兩種情境，本教學為你提供了可直接投入生產環境的基礎，無論是發票、護照或任何掃描文件皆可套用。

接下來要做什麼？可以嘗試將 TIFF 換成多頁 PDF、實驗自訂語言套件，或將輸出串接至自然語言處理管線，以自動化資料抽取。可能性無限——祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}