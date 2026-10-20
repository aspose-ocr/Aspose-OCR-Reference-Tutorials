---
category: general
date: 2026-03-07
description: 使用 C# 從 PNG 檔案中提取文字。學習如何使用 C# 將圖像轉換為文字，並快速讀取掃描圖像中的文字。
draft: false
keywords:
- extract text from png
- convert image to text c#
- read text from scanned images
- how to run ocr on images
language: zh-hant
og_description: 使用 C# 從 PNG 檔案提取文字。本指南示範如何在 C# 中將圖像轉換為文字，以及使用 Aspose OCR 讀取掃描圖像中的文字。
og_title: 在 C# 中從 PNG 提取文字 – 完整 OCR 教程
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 在 C# 中從 PNG 提取文字 – 完整 OCR 教學
url: /zh-hant/net/text-recognition/extract-text-from-png-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 PNG 中提取文字（C#）– 完整 OCR 指南

曾經需要 **extract text from PNG** 檔案，但不知從何入手嗎？你並不孤單——大多數開發者在第一次面對需要轉換為可搜尋文字的掃描圖形或螢幕截圖時，都會卡在這裡。好消息是，只要幾行 C# 程式碼加上 Aspose OCR，就能瞬間把任何 PNG 轉換成可編輯的字串。

在本教學中，我們將完整示範整個流程：從磁碟上定位 PNG、平行啟動 OCR 工作、到顯示每個結果的預覽。完成後，你將了解如何 **convert image to text C#**，能有效 **read text from scanned images**，同時掌握最佳的 **run OCR on images** 方法，避免阻塞 UI 執行緒。

## 需要的環境

- .NET 6.0 或更新版本（程式碼同樣適用於 .NET Core 與 .NET Framework）  
- Aspose.OCR NuGet 套件（`Install-Package Aspose.OCR`）  
- 一個放有 *.png* 檔案的資料夾  
- 任意你喜歡的 IDE（Visual Studio、VS Code、Rider…）

不需要額外設定；此函式庫已內建解碼 PNG、JPEG、TIFF 等所有常見格式的功能。

## 步驟 1：定位所有 PNG 檔案 – 「Extract Text from PNG」開始

首先必須找出所有要執行 OCR 的 PNG。使用 `Directory.GetFiles` 既快速又可靠。

```csharp
// Step 1: Find all PNG images in the input folder
string[] imageFiles = Directory.GetFiles("YOUR_DIRECTORY", "*.png");

// Quick sanity check – throw if nothing was found
if (imageFiles.Length == 0)
    throw new FileNotFoundException("No PNG files found in the specified folder.");
```

*為什麼這很重要：* 只掃描一次目錄即可讓後續流程保持簡潔，且提前檢查可避免之後出現「無輸出」的靜默錯誤，這類問題往往難以除錯。

## 步驟 2：平行啟動 OCR 任務 – 高效 **run OCR on images**

對少量檔案而言，順序執行 OCR 仍可接受，但實務上常會面對數十或數百張圖片。為每張圖片建立一個 `Task`，即可在 CPU 繼續運算的同時讓函式庫處理繁重工作。

```csharp
// Step 2: Prepare a list to hold OCR tasks (one per image)
var ocrTasks = new List<Task<string>>();

// Step 3: Launch a parallel task for each image
foreach (var filePath in imageFiles)
{
    ocrTasks.Add(Task.Run(() =>
    {
        // Load the image and run OCR
        var engine = new OcrEngine();
        engine.Image = ImageStream.FromFile(filePath);
        engine.Recognize();
        return engine.Text;          // This is the extracted string
    }));
}
```

*小技巧：* `Task.Run` 會把工作交給執行緒池，這樣即使有 UI（例如 WinForms/WPF）也能保持回應。如果是在伺服器上執行，同樣的模式可以很好地跨核心擴展。

## 步驟 3：等待所有任務完成 – 收集結果

現在等待每個 OCR 作業結束。`Task.WhenAll` 會回傳一個陣列，順序與原始檔案列表相同，方便把結果對應回檔名。

```csharp
// Step 4: Await all tasks and gather the recognized texts
string[] ocrResults = await Task.WhenAll(ocrTasks);
```

*邊緣情況說明：* 若任一圖片拋出例外（檔案損毀、格式不支援），`WhenAll` 會把例外向上拋出。你可以在內部的 `Task.Run` 加上 try/catch，並在失敗時回傳空字串或診斷訊息，以提升容錯能力。

## 步驟 4：顯示預覽 – 驗證 **convert image to text C#** 輸出

快速的預覽可以讓你在將資料寫入其他地方前，先確認 OCR 是否正確。

```csharp
// Step 5: Show a short preview of each result
for (int i = 0; i < ocrResults.Length; i++)
{
    string fileName = Path.GetFileName(imageFiles[i]);
    string preview = ocrResults[i].Length > 100
        ? ocrResults[i][..100] + "..."
        : ocrResults[i];
    Console.WriteLine($"{fileName}: {preview}");
}
```

典型的主控台輸出如下：

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
```

如果預覽出現亂碼，請檢查影像品質或考慮前置處理（例如二值化）——但對於大多數乾淨的 PNG，Aspose OCR 通常能一次就正確辨識。

## 可選：將結果寫入 CSV – 真實案例

大多數專案都需要把抽取出的文字以結構化格式保存。以下是一個簡易輔助程式，會把檔名與完整 OCR 文字寫入 CSV。

```csharp
string csvPath = Path.Combine("YOUR_DIRECTORY", "ocr-results.csv");
using var writer = new StreamWriter(csvPath);
writer.WriteLine("FileName,ExtractedText");

for (int i = 0; i < imageFiles.Length; i++)
{
    string escaped = ocrResults[i].Replace("\"", "\"\"");
    writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
}
Console.WriteLine($"All results saved to {csvPath}");
```

之後即可將 CSV 匯入 Excel、Power BI，或任何需要 **read text from scanned images** 的下游系統。

## 常見問答

**如果我的 PNG 很大（超過 5 MB）怎麼辦？**  
Aspose OCR 會自動對大型影像做降採樣，以維持記憶體使用量合理；若需要自行調整，可使用 `engine.Image = ImageStream.FromFile(filePath).Resize(2000, 0);` 將寬度限制在 2000 px，並保持長寬比。

**可以在 Linux 上執行嗎？**  
可以。Aspose OCR 為跨平台套件，只要安裝相應的原生相依（例如部分發行版的 `libgdiplus`）即可。

**OCR 語言預設是英文嗎？**  
是的。若需其他語言，可在呼叫 `Recognize()` 前設定 `engine.Language = OcrLanguage.French;`（或任何支援的列舉值）。

**要如何處理包含 PNG 的受密碼保護 PDF？**  
先將 PDF 頁面轉成影像（可使用 Aspose PDF 或其他函式庫），再把產生的 PNG 交給相同的管線。**how to run OCR on images** 的原則不變。

## 完整範例（Async Main）

以下是一個可直接貼到 Console 專案的完整程式碼，包含前述所有步驟，以及一個小幫手用來驗證輸入資料夾。

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // -------------------------------------------------
        // 1️⃣ Locate PNGs – the heart of “extract text from png”
        // -------------------------------------------------
        const string folder = @"YOUR_DIRECTORY";   // <-- change this
        if (!Directory.Exists(folder))
        {
            Console.WriteLine($"Folder not found: {folder}");
            return;
        }

        string[] imageFiles = Directory.GetFiles(folder, "*.png");
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to do.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Fire off OCR tasks – best way to “run OCR on images”
        // -------------------------------------------------
        var ocrTasks = new List<Task<string>>();
        foreach (var filePath in imageFiles)
        {
            ocrTasks.Add(Task.Run(() =>
            {
                var engine = new OcrEngine();
                engine.Image = ImageStream.FromFile(filePath);
                engine.Recognize();
                return engine.Text;
            }));
        }

        // -------------------------------------------------
        // 3️⃣ Await results
        // -------------------------------------------------
        string[] ocrResults = await Task.WhenAll(ocrTasks);

        // -------------------------------------------------
        // 4️⃣ Show previews
        // -------------------------------------------------
        for (int i = 0; i < ocrResults.Length; i++)
        {
            string fileName = Path.GetFileName(imageFiles[i]);
            string preview = ocrResults[i].Length > 100
                ? ocrResults[i][..100] + "..."
                : ocrResults[i];
            Console.WriteLine($"{fileName}: {preview}");
        }

        // -------------------------------------------------
        // 5️⃣ Optional: write CSV – perfect for “read text from scanned images”
        // -------------------------------------------------
        string csvPath = Path.Combine(folder, "ocr-results.csv");
        using var writer = new StreamWriter(csvPath);
        writer.WriteLine("FileName,ExtractedText");
        for (int i = 0; i < imageFiles.Length; i++)
        {
            string escaped = ocrResults[i].Replace("\"", "\"\"");
            writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
        }

        Console.WriteLine($"✅ OCR complete – results saved to {csvPath}");
    }
}
```

**預期輸出**（兩個 PNG 為例）：

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
✅ OCR complete – results saved to C:\MyImages\ocr-results.csv
```

## 小結

我們已完整說明如何使用 C# **extract text from PNG** 檔案。從定位檔案、平行執行 OCR、預覽文字，到將結果寫入 CSV，這份指南提供了可直接投入生產環境的 **convert image to text C#** 範式。

如果你已準備好進一步嘗試，請將相同管線套用到 JPEG 或 TIFF，測試不同的 OCR 語言，或將結果串接至搜尋索引，讓 **read text from scanned images** 能即時被搜尋。

對於邊緣案例、效能調校或授權問題有任何疑問，歡迎留言或在 Aspose 社群發問——祝開發順利！

![從 PNG 中提取文字範例](extract-text-png.png "使用 Aspose OCR 從 PNG 提取文字")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}