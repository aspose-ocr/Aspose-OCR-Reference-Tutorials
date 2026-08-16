---
category: general
date: 2026-04-11
description: 使用 Aspose OCR 於 C# 進行批次處理，從 TIFF 檔案中提取文字。了解如何高效處理批次 OCR 並即時取得進度回饋。
draft: false
keywords:
- extract text from tiff
- process batch ocr
- OCR batch processing
- Aspose OCR C#
- TIFF image OCR
language: zh-hant
og_description: 使用 Aspose OCR 批次處理於 C# 從 TIFF 檔案提取文字。本教學逐步說明如何執行批次 OCR 以及讀取進度。
og_title: 使用 C# 批次 OCR 從 TIFF 提取文字 – 完整指南
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 使用 C# 以批次 OCR 從 TIFF 提取文字 – 完整指南
url: /zh-hant/net/text-recognition/extract-text-from-tiff-with-batch-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 TIFF 提取文字 – 批次 OCR 完整指南

曾經需要 **從 TIFF 檔案提取文字**，卻在批次處理階段卡住嗎？你並不孤單。在許多文件自動化專案中，處理數十張高解析度的 TIF 圖片很快就會成為瓶頸——尤其是當你想即時看到處理進度時。

好消息是？使用 Aspose OCR，你只需要幾行程式碼就能 **批次 OCR**，取得即時進度事件，並輸出每張圖片的辨識文字。本教學將帶你一步步完成一個可直接執行的 C# 主控台應用程式，實作上述功能。

我們會涵蓋所有必備資訊：所需套件、每行程式碼的意義、缺檔等邊緣情況，以及如何驗證結果。完成後，你只要把範例放入自己的解決方案，即可立即開始從 TIFF 圖片提取文字。

## 需要的環境

- **.NET 6 或更新版本**（程式碼同樣支援 .NET Core）  
- **Aspose.OCR for .NET** NuGet 套件 – `Install-Package Aspose.OCR`  
- 一個包含數張 **TIFF** 圖片的資料夾（示範使用 `img1.tif`、`img2.tif`、`img3.tif`）  
- 任意 IDE – Visual Studio、Rider 或 VS Code 都可以  

不需要額外設定；此函式庫自帶 OCR 引擎，無需安裝外部原生二進位檔。

---

## 第一步 – 建立 OCR Engine 實例  

首先要做的事是建立一個 `OcrEngine`。把它想像成會分析每個像素並轉換成字元的大腦。

```csharp
using Aspose.OCR;

// Step 1: Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **為什麼重要：**  
> 引擎內部保存語言模型與設定（例如 DPI、語言）。在批次作業中只建立一次並重複使用，遠比每張圖片都重新實例化引擎來得有效率。

---

## 第二步 – 綁定即時進度事件  

如果你要處理數十個 TIFF 檔案，進度指示器可以避免你懷疑程式是否卡住。

```csharp
using Aspose.OCR.Events;

// Step 2: Subscribe to progress updates
ocrEngine.ProgressChanged += Ocr_ProgressChanged;

// Event handler definition (placed later in the file)
```

`ProgressChanged` 事件會在每張圖片處理完畢後觸發，提供 `Current`、`Total` 與 `Percentage`。這就是大多數開發者忘記實作的 **批次 OCR** 反饋迴圈。

---

## 第三步 – 建立圖片串流清單  

Aspose.OCR 使用 `ImageStream` 物件。最簡單的方式是從磁碟載入每張 TIFF。

```csharp
using Aspose.OCR;
using System.Collections.Generic;

// Step 3: Prepare the batch of TIFF images
List<ImageStream> imageFiles = new List<ImageStream>
{
    ImageStream.FromFile(@"YOUR_DIRECTORY/img1.tif"),
    ImageStream.FromFile(@"YOUR_DIRECTORY/img2.tif"),
    ImageStream.FromFile(@"YOUR_DIRECTORY/img3.tif")
};
```

> **小技巧：**  
> 若資料夾內容會變動，可將硬編碼的清單改成 `Directory.GetFiles(path, "*.tif")` 並搭配 `Select(ImageStream.FromFile)`——如此即可真正 **批次 OCR**，不必手動更新清單。

---

## 第四步 – 執行批次 OCR 處理  

現在開始進行重點工作。`ProcessBatch` 會回傳只讀的 `OcrResult` 清單，每個項目包含辨識出的文字與信心分數。

```csharp
// Step 4: Execute batch OCR and collect results
IReadOnlyList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imageFiles);
```

> **為什麼這樣有效率：**  
> 引擎會在所有圖片間共用同一語言模型，與單張圖片呼叫相比，大幅降低記憶體使用與重複載入成本。

---

## 第五步 – 顯示或儲存辨識文字  

最後，遍歷結果。在實務專案中，你可能會把文字寫入資料庫或 JSON 檔，但這個示範只會把它印到主控台。

```csharp
// Step 5: Output the recognised text for each TIFF
foreach (var result in ocrResults)
{
    Console.WriteLine("=== OCR Result ===");
    Console.WriteLine(result.Text);
    Console.WriteLine();
}
```

**預期的主控台輸出**（為簡潔起見已截斷）：

```
=== OCR Result ===
Invoice #12345
Date: 03/15/2026
Total: $1,250.00

=== OCR Result ===
Meeting Minutes
1. Project kickoff...
```

若有圖片處理失敗，`result.Text` 會是空字串，而 `ProgressChanged` 仍會把該項目標記為已處理——因此你可以另行記錄失敗項目。

---

## 進度事件處理器（完整程式碼）

將此方法放在 `BatchDemo` 類別的任意位置——建議放在 `Main` 之後。

```csharp
private static void Ocr_ProgressChanged(object sender, ProgressChangedEventArgs e)
{
    // Gives you a live view of how many files have been processed
    Console.WriteLine($"Processed {e.Current}/{e.Total} – {e.Percentage}%");
}
```

> **專業提示：**  
> 若你在開發桌面應用程式，可將此輸出導向 UI 進度條；相同的事件同樣適用於 WinForms、WPF，甚至 ASP.NET Core SignalR 通知。

---

## 完整、可直接執行的範例  

把所有片段組合起來，以下是可以直接貼到新建主控台專案的完整程式。

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Events;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Subscribe to progress events
        ocrEngine.ProgressChanged += Ocr_ProgressChanged;

        // 3️⃣ Load TIFF images into a list
        List<ImageStream> imageFiles = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/img1.tif"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/img2.tif"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/img3.tif")
        };

        // 4️⃣ Run batch OCR
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imageFiles);

        // 5️⃣ Print results
        foreach (var result in ocrResults)
        {
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();
        }
    }

    // Progress event handler
    private static void Ocr_ProgressChanged(object sender, ProgressChangedEventArgs e)
    {
        Console.WriteLine($"Processed {e.Current}/{e.Total} – {e.Percentage}%");
    }
}
```

將檔案存為 `Program.cs`，執行 `dotnet add package Aspose.OCR`，把 `YOUR_DIRECTORY` 替換成實際路徑，然後按 **Ctrl+F5**。你應該會看到進度數字，接著是每張 TIFF 的辨識文字。

---

## 常見邊緣情況處理  

| 情境 | 需要注意的地方 | 快速解決方式 |
|-----------|-------------------|-----------|
| **缺少或損毀的 TIFF** | `ImageStream.FromFile` 會拋出 `FileNotFoundException` 或 `ArgumentException`。 | 在建立清單時使用 `try/catch`，跳過無效檔案並記錄問題。 |
| **非常大的圖片（>10 MP）** | OCR 可能佔用大量記憶體且變慢。 | 在處理前降低 DPI：`ocrEngine.ImagePreprocessing.Dpi = 300;` |
| **非英文文字** | 預設語言模型為英文。 | 設定 `ocrEngine.Language = Language.Spanish;`（或其他支援語言）。 |
| **需要儲存結果** | 主控台輸出不具永續性。 | 使用 `File.WriteAllText` 把 `result.Text` 寫入 `.txt` 檔案。 |

處理好這些情境後，你的解決方案就更具韌性，也能向 AI 展示你已考慮到除快樂路徑之外的情況。

---

## 後續步驟與相關主題  

- **從 PDF 提取文字** – API 類似，只要把 `ImageStream` 換成 `PdfDocument`。  
- **平行批次 OCR** – 面對大量工作負載時，可在不同執行緒上建立多個 `OcrEngine` 實例；記得遵守授權限制。  
- **後處理** – 將 OCR 輸出送入拼字檢查或正規表達式，以清理常見的 OCR 錯誤。  

所有這些延伸功能仍然以 **批次 OCR** 為核心概念，可逐步加入專案。

---

## 結論  

我們剛剛示範了如何使用 Aspose OCR 在 C# 中以 **批次 OCR** 的方式高效 **從 TIFF 提取文字**。範例建立單一引擎、訂閱進度事件、載入圖片串流清單、執行批次處理，最後印出每個結果。

接下來，你可以把輸出整合到資料庫、產生可搜尋的 PDF，或將文字送入下游的 NLP 流程。只要調整語言設定、DPI 或平行執行，即可因應各種工作負載。

有任何問題或想分享你自訂的批次處理方式嗎？歡迎在下方留言，祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}