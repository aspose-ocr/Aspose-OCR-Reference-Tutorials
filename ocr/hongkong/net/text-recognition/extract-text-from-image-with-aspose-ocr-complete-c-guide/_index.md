---
category: general
date: 2026-05-28
description: 使用 Aspose OCR 於 C# 從圖像提取文字。了解如何提取 OCR 文字、載入圖像進行 OCR，以及快速辨識 TIF 檔案的文字。
draft: false
keywords:
- extract text from image
- how to extract ocr text
- load image for ocr
- recognize text from tif
language: zh-hant
og_description: 使用 Aspose OCR 於 C# 從圖像提取文字。本教學示範如何提取 OCR 文字、載入圖像進行 OCR，以及辨識 TIF 檔案中的文字。
og_title: 使用 Aspose OCR 從圖像提取文字 – 完整 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Extract text from image using Aspose OCR in C#. Learn how to extract
    OCR text, load image for OCR, and recognize text from TIF files quickly.
  headline: Extract Text from Image with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Extract text from image using Aspose OCR in C#. Learn how to extract
    OCR text, load image for OCR, and recognize text from TIF files quickly.
  name: Extract Text from Image with Aspose OCR – Complete C# Guide
  steps:
  - name: '**Wrong file path** – A typo leads to a `FileNotFoundException`. Double‑check
      the path or use `Path.Combine` for cross‑platform safety.'
    text: '**Wrong file path** – A typo leads to a `FileNotFoundException`. Double‑check
      the path or use `Path.Combine` for cross‑platform safety.'
  - name: '**Unsupported format** – Aspose OCR supports PNG, JPEG, BMP, and TIFF.
      Trying a PDF directly will throw an `UnsupportedFormatException`. Convert first
      if needed.'
    text: '**Unsupported format** – Aspose OCR supports PNG, JPEG, BMP, and TIFF.
      Trying a PDF directly will throw an `UnsupportedFormatException`. Convert first
      if needed.'
  - name: '**Large image size** – Very high‑resolution TIFFs can consume memory. Consider
      down‑scaling with `engine.Options.Dpi = 300` before recognition.'
    text: '**Large image size** – Very high‑resolution TIFFs can consume memory. Consider
      down‑scaling with `engine.Options.Dpi = 300` before recognition.'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 使用 Aspose OCR 從圖像提取文字 – 完整 C# 指南
url: /zh-hant/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 從圖像提取文字 – 完整 C# 指南

從圖像提取文字是當你需要將掃描的文件、收據，甚至白板照片數位化時常見的障礙。如果你在尋找在 .NET 專案中 **如何提取 OCR 文字**，你來對地方了——本指南將帶你完整走過整個流程，從載入圖片到從 TIF 檔案中提取已辨識的字元。

我們會涵蓋所有你需要知道的內容：建立 OCR 引擎、載入圖像以進行 OCR、執行非同步辨識，最後將提取的文字印出到主控台。完成後，你將擁有一段可直接執行的程式碼，能處理任何 TIFF（或其他支援格式），同時也能清楚了解每個步驟的意義。

## 您需要的條件

- .NET 6 或更新版本（程式碼亦可在 .NET Core 3.1+ 上編譯）
- 已在專案中安裝 Aspose.OCR NuGet 套件（`Aspose.OCR`）
- 放置於可參考位置的範例 TIFF 圖片（`page1.tif`）
- 任一程式碼編輯器或 IDE（Visual Studio、VS Code、Rider… 隨你喜好）

不需要額外的設定檔，也不必在本機安裝龐大的 OCR 引擎——Aspose 會為你處理所有繁重的工作。

---

## 從圖像提取文字 – 步驟 1：初始化 OCR 引擎

在處理任何圖像之前，你必須先建立一個 `OcrEngine` 實例。把這個引擎想像成能閱讀字元的大腦；沒有它，整個流程就無法運作。

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static async Task Main()
    {
        // Step 1: Create an OCR engine instance
        var engine = new OcrEngine();
```

> **為什麼這很重要：** `OcrEngine` 包含了辨識演算法與語言套件。每次操作只實例化一次即可降低記憶體使用，且提供一個乾淨的切入點，之後可調整設定（例如語言、DPI）。

---

## 如何提取 OCR 文字 – 步驟 2：載入圖像以進行 OCR

引擎已就緒後，我們需要指向要讀取的圖片。Aspose 提供 `ImageStream.FromFile`，可在不將整張位圖載入記憶體的情況下串流檔案，對大型 TIFF 檔案而言效能更佳。

```csharp
        // Step 2: Load the image to be recognized
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/page1.tif");
```

> **小技巧：** 將 `YOUR_DIRECTORY` 替換為圖像的絕對或相對路徑。若從專案資料夾執行程式，`@"./page1.tif"` 就能順利運作。  
> **邊緣情況：** TIFF 檔案可能包含多頁。`ImageStream.FromFile` 預設讀取第一頁；若需其他頁面，可使用 `ImageStream.FromFile(path, pageNumber)`。

---

## 從 TIF 辨識文字 – 步驟 3：執行非同步 OCR

在 OCR 引擎運作時阻塞呼叫執行緒會讓 UI 應用程式卡住，或浪費伺服器資源。使用 `RecognizeAsync` 可讓辨識在背景執行，回傳 `Task<string>`，最終解析為提取的文字。

```csharp
        // Step 3: Perform OCR asynchronously (does not block the calling thread)
        string extractedText = await engine.RecognizeAsync();
```

> **為什麼要使用 async？** 在 Web API 或桌面應用程式中，你希望執行緒池保持回應。`await` 會在 OCR 完成前交還控制權給呼叫端，讓 UI 保持流暢或讓請求執行緒可用於其他工作。

---

## 輸出提取的文字 – 步驟 4：列印或儲存

最後，我們只需將結果寫入主控台。實務上，你可能會寫入資料庫、檔案，或將字串傳遞給其他服務。

```csharp
        // Step 4: Output the recognized text
        Console.WriteLine(extractedText);
    }
}
```

### 預期輸出

若 `page1.tif` 包含文字 *“Hello, Aspose OCR!”*，主控台會顯示：

```
Hello, Aspose OCR!
```

若圖像雜訊較多，可能會出現額外的換行或辨識錯誤的字元——可調整引擎的 `Options`（例如 `engine.Options.DetectLanguage = true`）以提升準確度。

---

## 載入圖像進行 OCR 時的常見陷阱

1. **檔案路徑錯誤** – 打錯字會拋出 `FileNotFoundException`。請再次確認路徑，或使用 `Path.Combine` 以確保跨平台安全。  
2. **不支援的格式** – Aspose OCR 支援 PNG、JPEG、BMP 與 TIFF。直接使用 PDF 會拋出 `UnsupportedFormatException`，如有需要請先轉換。  
3. **圖像尺寸過大** – 超高解析度的 TIFF 可能佔用大量記憶體。辨識前可考慮使用 `engine.Options.Dpi = 300` 進行降解析度處理。

---

## 更進一步：調整辨識設定

Aspose.OCR 附帶多項可調整的選項：

```csharp
engine.Options.Language = Language.English;      // Force English if you know the language
engine.Options.Dpi = 200;                       // Reduce DPI for faster processing
engine.Options.IsAutoRotate = true;            // Auto‑rotate skewed pages
```

試著調整這些設定，以在速度與準確度之間取得平衡。

---

## 完整、可執行範例（直接貼上使用）

以下是可直接放入全新 Console 專案的完整程式碼，已包含前述的可選設定。

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static async Task Main()
    {
        // Create the OCR engine
        var engine = new OcrEngine();

        // Optional: fine‑tune recognition
        engine.Options.Language = Language.English;
        engine.Options.Dpi = 200;
        engine.Options.IsAutoRotate = true;

        // Load the image (replace with your actual path)
        engine.Image = ImageStream.FromFile(@"./page1.tif");

        // Run OCR asynchronously
        string extractedText = await engine.RecognizeAsync();

        // Show the result
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

將檔案儲存為 `Program.cs`，執行 `dotnet add package Aspose.OCR`，再執行 `dotnet run`。你應該會在主控台看到提取的文字。

---

## 重點回顧

我們剛剛示範了 **如何使用 Aspose OCR 在 C# 中從 TIFF 圖像提取文字**。步驟包括：初始化引擎、載入圖像、以非同步方式辨識 TIF 文字，最後輸出結果——完整覆蓋了從圖像檔案提取文字的全流程。  

如果你想超越純文字，請探索 Aspose 的 `PdfConverter`，將 OCR 輸出嵌入可搜尋的 PDF，或使用 `engine.Options` 處理多語言文件。

---

## 接下來可以做什麼？

- **批次處理：** 迴圈遍歷資料夾內的 TIFF，將每筆結果寫入資料庫。  
- **圖像前處理：** 使用 `System.Drawing` 或 `ImageSharp` 在送入 OCR 引擎前清理雜訊掃描。  
- **整合至 ASP.NET Core：** 建立一個端點，接受上傳的圖像並以 JSON 回傳辨識文字。

盡情實驗、嘗試不同組合，然後再回來閱讀本指南作為參考。若遇到任何問題，Aspose OCR 文件是很好的伴侶，但核心模式始終如一：**從圖像提取文字**、**載入圖像以進行 OCR**、**從 TIF 辨識文字**，最後處理結果。

祝程式開發順利，願你的圖像永遠清晰如水晶！

## 相關教學

- [使用 Aspose.OCR 以語言選擇提取圖像文字 C#](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [提取圖像文字 – 使用 Aspose.OCR 於 .NET 的 OCR 最佳化](/ocr/english/net/ocr-optimization/)
- [透過在 OCR 中準備矩形來提取圖像文字](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}