---
category: general
date: 2026-03-05
description: 使用 Aspose OCR 在 C# 中將 TIFF 轉換為文字——快速擷取掃描圖像檔的文字，並學習如何在 C# 中載入圖像檔進行 OCR
  處理。
draft: false
keywords:
- convert TIFF to text
- extract text scanned image
- load image file C#
language: zh-hant
og_description: 使用 Aspose OCR 在 C# 中將 TIFF 轉換為文字。了解從掃描圖像提取文字及高效載入圖像檔案的完整工作流程。
og_title: 在 C# 中將 TIFF 轉換為文字 – 擷取掃描圖像文字
tags:
- OCR
- C#
- Aspose
title: 在 C# 中將 TIFF 轉換為文字 – 提取掃描圖像文字
url: /zh-hant/net/text-recognition/convert-tiff-to-text-in-c-extract-scanned-image-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將 TIFF 轉換為文字（C#） – 擷取掃描圖像文字

需要 **convert TIFF to text in C#** 嗎？你並不是唯一在與多頁掃描圖像奮戰、而這些圖像頑固地不願變成可搜尋的字串的人。  
在本指南中，我們將逐步說明一個完整、可直接執行的解決方案，將 TIFF 檔案送入 Aspose OCR，並輸出純文字——不需額外服務，也沒有隱藏的魔法。

> **Pro tip:** 如果你在處理高解析度掃描，啟用 GPU 處理可以為每頁節省數秒。

我們還會示範如何 **extract text scanned image** 檔案，以及將 **load image file C#** 載入 OCR 引擎的最佳方式，讓你今天就能將此邏輯嵌入任何 .NET 專案。

---

## 您需要的條件

在開始之前，請確保您的機器上已具備以下項目：

| 需求 | 原因 |
|-------------|--------|
| .NET 6.0+ (or .NET Framework 4.7.2+) | 現代執行環境，支援 `Span<T>` 與非同步 I/O |
| Aspose.OCR for .NET (NuGet package `Aspose.OCR`) | 我們將使用的 OCR 引擎 |
| A valid Aspose OCR license file (`Aspose.OCR.lic`) | 若未提供，將受到評估版限制 |
| A TIFF file (single‑or multi‑page) to test | 使用範例：`scanned_multi_page.tif` |
| GPU with CUDA 11+ (optional) | 在 `EngineMode = Gpu` 時可加速辨識 |

如果缺少上述任一項，請立即取得 NuGet 套件：

```bash
dotnet add package Aspose.OCR
```

---

## 步驟 1：設定專案並匯入命名空間

建立一個新的主控台應用程式（或將程式碼加入現有專案）。我們首先要匯入所需的類別。

```csharp
using System;
using Aspose.OCR;          // Core OCR classes
using Aspose.OCR.Image;   // ImageStream helper
```

> **Why this matters:** 匯入 `Aspose.OCR.Image` 可取得 `ImageStream` 工廠，能直接從磁碟或串流讀取 TIFF 檔案。跳過此步驟會導致編譯時錯誤。

---

## 步驟 2：初始化 OCR 引擎並選擇處理模式

必須在指派任何圖像之前先設定 OCR 引擎的**前置條件**。在此決定是使用 CPU 還是啟用 GPU。

```csharp
// Step 2: Initialize the OCR engine and enable GPU processing (must be set before any OCR work)
OcrEngine ocrEngine = new OcrEngine();

// Choose the processing mode that fits your environment.
// Options: Cpu (default) | Gpu | Auto
ocrEngine.EngineMode = OcrEngineMode.Gpu;   // Switch to Cpu if you don’t have a compatible GPU
```

*如果你在沒有顯示卡的無頭伺服器上，請將 `Gpu` 改為 `Cpu` 或 `Auto`。*  
引擎模式會影響記憶體配置與速度；在大型、高解析度 TIFF 上，GPU 模式可快 2‑3 倍。

---

## 步驟 3：套用您的 Aspose OCR 授權

未套用授權時，會受到頁數與浮水印的限制。請盡早載入授權檔，以確保之後的所有操作皆不受限制。

```csharp
// Step 3: Apply the Aspose OCR license (replace with your own license file if needed)
ocrEngine.SetLicense("Aspose.OCR.lic");
```

> **Common pitfall:** 若在 `Recognize()` 之後才呼叫 `SetLicense`，引擎將回退至試用模式。

---

## 步驟 4：載入 TIFF 檔案 – 處理單頁與多頁圖像

Aspose OCR 內建支援讀取多頁 TIFF，但必須提供正確的串流。以下是一個適用於兩種情況的穩健範例。

```csharp
// Step 4: Load the image to be recognized
string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

using (var imageStream = ImageStream.FromFile(tiffPath))
{
    // Step 5: Assign the image to the engine
    ocrEngine.Image = imageStream;

    // Step 6: Perform the OCR operation
    OcrResult ocrResult = ocrEngine.Recognize();

    // Step 7: Output the recognized text
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
```

### 為何使用 `ImageStream.FromFile`？

- 它抽象化底層的 `FileStream`，在內部處理 TIFF 頁面的列舉。  
- 同樣支援 `MemoryStream`，因此可直接從資料庫或 Web API 載入圖像，無需觸及檔案系統。

### 邊緣情況：超大型 TIFF

若 TIFF 超過 200 MB，建議逐頁載入以避免記憶體不足的例外：

```csharp
int pageCount = ImageInfo.GetPageCount(tiffPath);
for (int i = 0; i < pageCount; i++)
{
    using var pageStream = ImageStream.FromFile(tiffPath, i);
    ocrEngine.Image = pageStream;
    var pageResult = ocrEngine.Recognize();
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

---

## 步驟 5：驗證輸出

執行程式後，您應該會看到類似以下的結果：

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
Thank you for your business!
```

如果文字顯示亂碼，請再次確認：

1. **Resolution** – OCR 在 300 dpi 或更高時效果最佳。  
2. **EngineMode** – 若 GPU 驅動過舊，請切換至 `Cpu`。  
3. **License** – 確認授權檔路徑正確且檔案可讀取。

---

## 常見問題 (FAQ)

### 這能適用於其他圖像格式嗎？

當然可以。`ImageStream.FromFile` 支援 JPEG、PNG、BMP，甚至 PDF（透過 Aspose.PDF）。只要更換檔案副檔名即可。

### 若需處理儲存在資料庫中的圖像該怎麼辦？

將 BLOB 讀入 `MemoryStream`，再傳入 `ImageStream.FromStream(memoryStream)`。OCR 引擎會將其視為檔案串流處理。

### 我可以在 Linux 上執行嗎？

可以——Aspose OCR 為跨平台套件。安裝相應的 .NET 執行環境，並確保 GPU（若使用）所需的原生函式庫已就緒。

---

## 完整可執行範例（可直接複製貼上）

以下為完整程式碼，已可直接編譯。請將 `YOUR_DIRECTORY` 以及授權檔路徑替換為實際位置。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace TiffToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Choose processing mode: Gpu, Cpu, or Auto
            ocrEngine.EngineMode = OcrEngineMode.Gpu; // Change to Cpu if no GPU

            // Apply license (skip if you only need a trial)
            ocrEngine.SetLicense("Aspose.OCR.lic");

            // Path to the TIFF file
            string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

            // Load the TIFF (handles multi‑page automatically)
            using (var imageStream = ImageStream.FromFile(tiffPath))
            {
                // Assign image to engine
                ocrEngine.Image = imageStream;

                // Run OCR
                OcrResult result = ocrEngine.Recognize();

                // Display result
                Console.WriteLine("=== OCR Output ===");
                Console.WriteLine(result.Text);
            }

            // Optional: Process each page individually for huge files
            // int pages = ImageInfo.GetPageCount(tiffPath);
            // for (int i = 0; i < pages; i++) { ... }
        }
    }
}
```

將此檔案儲存為 `Program.cs`，執行 `dotnet run`，即可看到文字輸出

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}