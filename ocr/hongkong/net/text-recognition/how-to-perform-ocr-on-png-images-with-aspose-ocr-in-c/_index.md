---
category: general
date: 2026-11-26
description: 學習如何對 PNG 檔案執行 OCR、將 PNG 轉換為文字，並使用 Aspose.OCR 提取西里爾文字——開發人員的逐步指南。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- convert PNG to text
- recognize text from PNG
- extract Cyrillic text
- load image for OCR
language: zh-hant
lastmod: 2026-11-26
og_description: 如何在 C# 中使用 Aspose.OCR 對 PNG 檔案執行 OCR 並提取西里爾文字。請跟隨本完整教學將 PNG 轉換為文字。
og_image_alt: how to perform OCR on a PNG image using Aspose.OCR
og_title: 如何使用 Aspose.OCR 對 PNG 圖像執行 OCR – C# 指南
schemas:
- author: Aspose
  dateModified: '2026-11-26'
  description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  headline: How to perform OCR on PNG images with Aspose.OCR in C#
  type: TechArticle
- description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  name: How to perform OCR on PNG images with Aspose.OCR in C#
  steps:
  - name: Handling large images
    text: 'If the PNG is larger than 2 MB, consider down‑scaling it before recognition
      to speed up processing:'
  - name: 'Edge case: Missing language module'
    text: 'If the download fails (e.g., offline environment), the engine throws an
      `OcrException`. Catch it to provide a graceful fallback:'
  - name: Expected output
    text: 'If `sample_image.png` contains the Cyrillic phrase “Привет мир”, the console
      will display:'
  - name: How it works
    text: 1. **Engine creation** – prepares the OCR pipeline. 2. **Image loading**
      – supports both raw PNG and down‑scaled versions for performance. 3. **Language
      selection** – demonstrates **extract Cyrillic text** while handling missing
      modules. 4. **Recognition** – the core **recognize text from PNG** call
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
title: 如何在 C# 中使用 Aspose.OCR 對 PNG 圖像執行 OCR
url: /zh-hant/net/text-recognition/how-to-perform-ocr-on-png-images-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.OCR 對 PNG 圖像執行 OCR

如果您需要 **how to perform OCR**（執行 OCR）於 PNG 檔案，本指南將向您展示使用 Aspose.OCR 將 PNG 轉換為文字的完整步驟。無論是從掃描文件中提取西里爾文字，或僅僅從 PNG 截圖中辨識文字，此解決方案即插即用，僅需幾行 C# 程式碼即可。

在本教學中，您將學會：

* **load image for OCR** 從本機資料夾載入，
* 設定引擎以 **extract Cyrillic text**，
* **recognize text from PNG** 並取得乾淨的字串，
* 處理常見問題，例如缺少語言模組和大型圖像。

不需要任何 Aspose.OCR 的先前經驗——只要有 .NET 開發環境以及您想處理的 PNG 圖像即可。

## 前置條件

* .NET 6.0（或更新版本）已安裝。
* 取得 **Aspose.OCR for .NET** 的授權或試用版。您可從 Aspose 官方網站取得免費試用。
* Visual Studio 2022（或任何支援 .NET 的 IDE）。
* 包含欲提取文字的 PNG 檔案（範例使用 `sample_image.png`）。

## 步驟 1：安裝 Aspose.OCR NuGet 套件

在專案資料夾中開啟終端機並執行：

```bash
dotnet add package Aspose.OCR
```

此套件包含核心 OCR 引擎及所有語言模組。當您請求本機未安裝的語言時，Aspose.OCR 會自動下載所需的模組。

## 步驟 2：建立 OCR 引擎實例（how to perform OCR）

任何 OCR 工作流程的第一個可執行步驟是實例化引擎。此物件負責管理後續所有操作，例如載入圖像與執行辨識。

```csharp
using Aspose.OCR;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

**為什麼重要：** `OcrEngine` 類別封裝了 OCR 流程。建立單一實例並在多張圖像間重複使用，可減少記憶體開銷並提升效能。

## 步驟 3：載入 OCR 圖像 – 指定來源 PNG 檔案

載入圖像即是您 **load image for OCR** 的時機。Aspose.OCR 支援多種輸入類型；最直接的是 `ImageStream.FromFile`。

```csharp
// Load the PNG image from disk
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_image.png");
```

> **專業提示：** 使用絕對路徑或 `Path.Combine` 可避免在不同環境下的執行時錯誤。

### 處理大型圖像

如果 PNG 大於 2 MB，建議在辨識前先縮小尺寸，以加快處理速度：

```csharp
using System.Drawing;

// Downscale large images to a maximum width of 1200 pixels
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/sample_image.png");
int maxWidth = 1200;
int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

using (var ms = new MemoryStream())
{
    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
    ocrEngine.Image = ImageStream.FromStream(ms);
}
```

## 步驟 4：設定語言 – extract Cyrillic text

預設情況下，Aspose.OCR 假設使用英語。若要 **extract Cyrillic text**，請將 `Language` 屬性設為 `Language.Cyrillic`。首次執行程式碼時，所需模組會自動下載。

```csharp
// Set the OCR language to Cyrillic
ocrEngine.Language = Language.Cyrillic;
```

如果需要辨識多種語言（例如英語與西里爾文），可以將它們結合起來：

```csharp
ocrEngine.Language = Language.English | Language.Cyrillic;
```

### 邊緣情況：缺少語言模組

若下載失敗（例如離線環境），引擎會拋出 `OcrException`。請捕捉此例外以提供優雅的備援方案：

```csharp
try
{
    ocrEngine.Language = Language.Cyrillic;
}
catch (OcrException ex)
{
    Console.WriteLine($"Language module could not be loaded: {ex.Message}");
    // Optionally, fall back to English or abort the process
}
```

## 步驟 5：執行辨識操作（recognize text from PNG）

現在圖像與語言皆已設定，您可以 **recognize text from PNG**。`Recognize` 方法同步執行 OCR 流程。

```csharp
// Run OCR
ocrEngine.Recognize();
```

**為什麼有效：** 在內部，Aspose.OCR 會先進行前處理（二值化、去噪），再將圖像送入針對所選語言調校的神經網路辨識器。

## 步驟 6：取得並顯示辨識文字（convert PNG to text）

辨識完成後，可透過 `Text` 屬性取得提取的字串。這就是 **convert PNG to text** 的最後一步。

```csharp
// Get the recognized text
string recognizedText = ocrEngine.Text;

// Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

### 預期輸出

若 `sample_image.png` 包含西里爾語句子 “Привет мир”，控制台將顯示：

```
=== OCR Result ===
Привет мир
```

輸出可能會保留圖像中出現的換行與標點符號。若有需要，您可以使用 `String.Trim()`、`Regex` 或其他文字清理工具進行後處理。

## 步驟 7：選用 – 將結果儲存至檔案

將 OCR 結果儲存可供後續處理（例如索引、翻譯）。以下是一個快速將文字寫入 UTF‑8 檔案的方法：

```csharp
File.WriteAllText(@"YOUR_DIRECTORY/ocr_output.txt", recognizedText, Encoding.UTF8);
Console.WriteLine("OCR text saved to ocr_output.txt");
```

## 常見問題與避免方法

| Issue | Symptom | Fix |
|-------|----------|-----|
| **缺少語言模組** | ``OcrException`` 發生於 `Language = Language.Cyrillic` | 確保首次執行時具備網路連線，或透過 Aspose 的離線套件預先下載模組。 |
| **模糊或低對比度圖像** | 辨識精度差，出現大量 “?” 字元 | 前處理圖像：提升對比度、套用銳化，或轉為灰階後再送入引擎。 |
| **非常大的 PNG** | 處理時間過長，可能拋出 `OutOfMemoryException` | 如步驟 3 所示進行縮小，或將多頁圖像切割成獨立區塊。 |
| **非 UTF‑8 字元** | 輸出亂碼 | 確認控制台或檔案寫入器使用 UTF‑8 編碼（`Encoding.UTF8`）。 |

## 完整、可執行範例

以下為結合上述所有步驟的完整程式碼。將其複製到新的 Console 專案中，並在調整檔案路徑後執行。

```csharp
using System;
using System.Drawing;
using System.IO;
using System.Text;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1. Create OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2. Load PNG image (with optional down‑scaling for large files)
            string imagePath = @"YOUR_DIRECTORY/sample_image.png";
            Bitmap original = new Bitmap(imagePath);
            const int maxWidth = 1200;

            if (original.Width > maxWidth)
            {
                int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
                Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

                using (var ms = new MemoryStream())
                {
                    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    ocrEngine.Image = ImageStream.FromStream(ms);
                }
            }
            else
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }

            // 3. Set language to Cyrillic (fallback to English if needed)
            try
            {
                ocrEngine.Language = Language.Cyrillic;
            }
            catch (OcrException ex)
            {
                Console.WriteLine($"Failed to load Cyrillic module: {ex.Message}");
                Console.WriteLine("Falling back to English.");
                ocrEngine.Language = Language.English;
            }

            // 4. Recognize text
            ocrEngine.Recognize();

            // 5. Retrieve and display the text (convert PNG to text)
            string recognizedText = ocrEngine.Text;
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);

            // 6. Save result to a UTF‑8 file
            string outputPath = @"YOUR_DIRECTORY/ocr_output.txt";
            File.WriteAllText(outputPath, recognizedText, Encoding.UTF8);
            Console.WriteLine($"OCR text saved to {outputPath}");
        }
    }
}
```

### 工作原理

1. **Engine creation** – 準備 OCR 流程。  
2. **Image loading** – 同時支援原始 PNG 與縮小版本，以提升效能。  
3. **Language selection** – 示範 **extract Cyrillic text** 並處理缺少模組的情況。  
4. **Recognition** – 核心 **recognize text from PNG** 呼叫。  
5. **Result handling** – 展示 **convert PNG to text** 並將結果寫入檔案。

使用 `dotnet run` 執行程式。若環境設定正確，您將在控制台看到辨識文字，且會儲存至 `ocr_output.txt`。

## 結論

在本教學中，您學會了使用 Aspose.OCR for .NET **how to perform OCR** PNG 檔案，涵蓋從 **load image for OCR** 到 **extract Cyrillic text** 以及 **convert PNG to text** 的完整流程。完整、可執行的範例展示了標準工作流程、常見邊緣情況與實用技巧，確保您的 OCR 流程可靠。

**下一步**

- 探索結合 `Language` 標誌的其他語言（阿拉伯語、中文）以 **recognize text from PNG**。  
- 將 OCR 結果整合至 Azure Cognitive Search，以建立可搜尋的文件檔案庫。  
- 嘗試 Aspose.OCR 的 `OcrEngine` 設定，例如 `Resolution`

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [How to Download Aspose.OCR Model and Extract Text from PNG in C#](/ocr/english/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/)
- [How to Perform OCR in C# – Recognize Cyrillic Text with Aspose](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [How to Batch OCR in C# – Fast Way to Extract Text PNG Files](/ocr/english/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}