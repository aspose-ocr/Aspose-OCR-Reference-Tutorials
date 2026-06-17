---
category: general
date: 2026-03-13
description: 如何在 C# 中使用 OCR 從掃描檔提取文字。學習使用 Aspose OCR、GPU 加速將 TIFF 轉換為文字，並提供逐步程式碼示範。
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: zh-hant
og_description: 如何在 C# 中使用 OCR 從掃描檔案提取文字。本指南將示範如何使用 Aspose OCR 及 GPU 加速將 TIFF 轉換為文字。
og_title: 如何在 C# 中使用 OCR – 快速從掃描檔提取文字
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 如何在 C# 中使用 OCR – 快速從掃描檔提取文字
url: /zh-hant/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

.

Continue.

Now the table "What You’ll Need". Translate header and cells.

Now the "Overview of the Solution" heading.

Then bullet list.

Image alt and title.

Step headings.

Code block placeholders.

Edge case note.

Expected Output heading.

Code block placeholder.

Step 4 heading.

Full Working Example heading.

Quick Checklist heading.

Checklist bullet points.

Common Pitfalls & Pro Tips heading and table.

Now ensure we keep markdown formatting.

Let's craft translation.

Note: Use Traditional Chinese characters, Hong Kong style (e.g., "程式" maybe). Keep technical terms in English.

Let's write.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 快速從掃描檔案提取文字

有沒有想過 **如何使用 OCR** 從一堆掃描的 TIFF 檔案中抽取可讀文字？你並不是唯一有此需求的人。在許多實務專案中——例如發票數位化、歷史文件保存，或僅僅是讓 PDF 可搜尋——開發者都需要一個可靠的方式 **從掃描檔案提取文字**，而且不需要費力。

好消息是？只要使用 Aspose OCR 加上幾行 C# 程式碼，就能在數秒內把 TIFF 轉成文字，即使在一般工作站上也能順利執行。以下提供完整、可直接執行的範例，並說明每個選擇的原因，讓你能依需求自行調整工作流程。

## 需要的前置條件

在開始之前，請先確認你已具備以下項目：

| 前置條件 | 為什麼重要 |
|--------------|----------------|
| .NET 6+（或 .NET Framework 4.7+） | Aspose OCR NuGet 套件針對現代 .NET 執行環境。 |
| Visual Studio 2022（或任何你慣用的 IDE） | 提供 IntelliSense 與便利的除錯功能。 |
| 支援 CUDA 的 GPU 與驅動程式（可選） | 開啟 `ocrEngine.UseGpu = true` 後，可在大量批次時顯著提升速度。 |
| 一個放置欲處理 TIFF 圖片的資料夾 | 本教學使用 `*.tif` 檔案，你也可以自行調整搜尋模式。 |
| Aspose.OCR NuGet 套件（`Install-Package Aspose.OCR`） | 核心函式庫，負責所有繁重的 OCR 工作。 |

如果缺少任何項目，請立即取得——否則閱讀完本文後才發現缺少相依性會卡住。

## 解決方案概觀

從宏觀角度看，程式執行三件事：

1. **建立 OCR 引擎**，並視需要開啟 GPU 加速。  
2. **遍歷目錄中的每個 TIFF 檔案**，執行辨識並取得純文字結果。  
3. **將文字寫入與原圖同名的 `.txt` 檔**。

就這樣。程式碼刻意保持簡潔，同時示範了最佳實踐，如明確指定語言、正確釋放資源，以及針對常見例外情況的錯誤處理。

![如何在 C# 中使用 OCR 的範例](/images/how-to-use-ocr-csharp.png "說明如何在 C# 中使用 OCR 從掃描檔案提取文字")

## 步驟 1：初始化 OCR 引擎（How to Use OCR）

首先需要建立 `OcrEngine` 實例。這個物件是所有 Aspose OCR 功能的入口。預設情況下它在 CPU 上執行，但將 `UseGpu = true` 設為 true 後，若系統安裝了相容的 CUDA 驅動，便會把大量矩陣運算交給顯示卡處理。

```csharp
using Aspose.OCR;
using System.IO;

// Initialise the engine ----------------------------------------------------
OcrEngine ocrEngine = new OcrEngine
{
    // Enable GPU acceleration if a compatible card is present.
    // If you don’t have a GPU, just leave this as false – the code will still run.
    UseGpu = true,

    // Choose English as the recognition language. Change this if you need
    // another language pack (e.g., Language.French, Language.Spanish, etc.).
    Language = Language.English
};
```

**為什麼這很重要：**  
- **GPU 加速** 能在高解析度掃描時將處理時間縮短最多 70 %。  
- **明確指定語言** 可避免引擎自行猜測，提高非拉丁文字的辨識準確度。

## 步驟 2：指向掃描檔所在的資料夾（Convert TIFF to Text）

接著告訴程式要去哪裡找圖檔。使用 `Directory.GetFiles` 搭配 `*.tif` 篩選條件，讓邏輯保持簡單，且不會誤抓到 `.jpg`、`.png` 等不相關檔案。

```csharp
// Define the folder that contains the scanned TIFF images -----------------
string inputFolder = @"C:\ScannedDocs"; // <-- replace with your actual path

// Verify the folder exists before we start looping
if (!Directory.Exists(inputFolder))
{
    Console.WriteLine($"❌ Folder not found: {inputFolder}");
    return;
}
```

**邊緣案例說明：** 若資料夾是空的，下面的迴圈根本不會執行，這是完全正常的情況。稍後會看到友善的「找不到檔案」訊息。

## 步驟 3：處理每一個 TIFF 檔（Extract Text from Scans）

現在進入程式的核心：載入每張圖、執行 OCR，並把結果寫出。`ImageStream.FromFile` 會直接把檔案串流至記憶體，比先載入 `Bitmap` 更有效率。

```csharp
// Step 3: Iterate over every .tif file in the folder --------------------
string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

if (tiffFiles.Length == 0)
{
    Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
}
else
{
    foreach (var imagePath in tiffFiles)
    {
        try
        {
            // Load the current image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR on the image
            ocrEngine.Recognize();

            // Build the output .txt file path (same name, different extension)
            string textPath = Path.ChangeExtension(imagePath, ".txt");

            // Save the extracted text
            File.WriteAllText(textPath, ocrEngine.Text);

            Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
        }
        catch (Exception ex)
        {
            // Log the error but continue with the next file
            Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

**為什麼每次迭代都要包在 `try/catch` 中：**  
批次處理文件時常會遇到損毀的 TIFF 或記憶體不足的情況，這些錯誤不應該讓整個執行中斷。catch 區塊會記錄問題並繼續處理，確保管線的韌性。

### 預期輸出

對每個 `example.tif`，會在同一目錄產生 `example.txt`，內容類似：

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

如果 OCR 引擎無法辨識某行，會留下空白行或是亂碼——程式不會當機。

## 步驟 4：清理與釋放（Best Practice）

`OcrEngine` 實作了 `IDisposable`，因此在使用完畢後釋放本機資源是禮貌的作法。雖然在簡短的 Console App 中可以依賴 GC，但養成顯式釋放的習慣仍值得推崇。

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## 完整可執行範例（Copy‑Paste Ready）

以下程式碼可直接貼到新的 Console App 專案中。只要已安裝 Aspose.OCR NuGet 套件，即可直接編譯執行。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // Step 1: Initialise the OCR engine (how to use OCR)
        // --------------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            UseGpu = true,               // Enable GPU if available
            Language = Language.English  // Set language for recognition
        };

        // --------------------------------------------------------------------
        // Step 2: Define the folder containing TIFF scans (convert TIFF to text)
        // --------------------------------------------------------------------
        string inputFolder = @"C:\ScannedDocs"; // <-- adjust this path

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"❌ Folder not found: {inputFolder}");
            return;
        }

        // --------------------------------------------------------------------
        // Step 3: Process each TIFF file (extract text from scans)
        // --------------------------------------------------------------------
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

        if (tiffFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
        }
        else
        {
            foreach (var imagePath in tiffFiles)
            {
                try
                {
                    // Load image
                    ocrEngine.Image = ImageStream.FromFile(imagePath);

                    // Run OCR
                    ocrEngine.Recognize();

                    // Save result next to source image
                    string textPath = Path.ChangeExtension(imagePath, ".txt");
                    File.WriteAllText(textPath, ocrEngine.Text);

                    Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }
        }

        // --------------------------------------------------------------------
        // Step 4: Clean‑up (c# OCR tutorial best practice)
        // --------------------------------------------------------------------
        ocrEngine.Dispose();
        Console.WriteLine("🎉 All done! OCR engine released.");
    }
}
```

### 快速檢查清單

- **GPU 旗標** – 若沒有 CUDA 驅動，請移除或設為 `false`。  
- **語言** – 如需其他語言，將 `Language.English` 換成相對應的語言。  
- **檔案模式** – 若掃描檔是其他格式，將 `"*.tif"` 改成 `"*.png"` 或 `"*.*"`。

## 常見陷阱與進階技巧（c# OCR tutorial）

| 陷阱 | 如何避免 |
|---------|-----------------|
| **大量批次導致記憶體不足** | 將檔案分批處理，或在每處理 50 個檔案後呼叫 `GC.Collect()`（通常不需要）。 |
| **GPU 未被偵測** 但 `UseGpu = true` | 引擎會自動回退到 CPU，你可以在建構後檢查 `ocrEngine.IsGpuAvailable`。 |
| **語言包選錯** 造成輸出雜亂 | 必須明確設定 `ocrEngine.Language`；預設可能是 `Language.Unknown`。 |
| **檔案路徑含 Unicode 字元** | 使用 `Path.GetFullPath` 正規化，或在 Windows 上以 `@"\\?\"` 前綴處理超長路徑。 |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}