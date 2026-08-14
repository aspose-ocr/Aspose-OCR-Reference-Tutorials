---
category: general
date: 2026-02-20
description: 如何在 C# 中對 DjVu 檔案執行 OCR。學習從影像辨識文字，並使用 Aspose OCR 快速將 DjVu 轉換為文字。
draft: false
keywords:
- how to perform OCR
- recognize text from image
- how to read djvu
- extract text from image
- convert djvu to text
language: zh-hant
og_description: 如何在 C# 中對 DjVu 檔案執行 OCR。本教學將示範如何從圖像辨識文字、讀取 DjVu，並使用 Aspose OCR 將 DjVu
  轉換為文字。
og_title: 如何在 C# 中對 DjVu 檔案執行 OCR – 完整指南
tags:
- OCR
- C#
- DjVu
- Aspose
title: 如何在 C# 中對 DjVu 檔案執行 OCR – 逐步指南
url: /zh-hant/net/text-recognition/how-to-perform-ocr-on-djvu-files-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中對 DjVu 檔案執行 OCR – 完整指南

有沒有想過在不抓狂的情況下 **執行 OCR** 於 DjVu 文件？你並非唯一有此困擾的人。許多開發者在需要 **從影像中辨識文字**（這些影像位於 DjVu 容器內）時會卡關。好消息是？只要幾行 C# 程式碼加上 Aspose OCR 函式庫，就能輕鬆擷取隱藏的文字。

在本教學中，我們將一步步說明如何將 DjVu 頁面轉換為純文字。完成後，你將了解 **如何讀取 DjVu**、如何 **從影像物件擷取文字**，甚至 **如何將 DjVu 轉換為文字** 以供後續處理。無需外部服務，無模糊參考——僅提供一個自包含、可執行的範例。

## 前置條件

在深入之前，請確保你已備妥以下項目：

- .NET 6.0 SDK 或更新版本（此程式碼亦相容 .NET Framework 4.8）。
- Visual Studio 2022 或任何支援 C# 的編輯器。
- Aspose OCR for .NET 授權（免費試用版可用於測試）。
- 一個範例 DjVu 檔案（`sample.djvu`），放置於可參考的資料夾中。

事先備妥上述項目，可確保流程順暢——避免之後出現「缺少參考」的驚喜。

## 如何對 DjVu 頁面執行 OCR

核心概念很簡單：將 DjVu 頁面載入為影像，交給 OCR 引擎，然後讀取產生的字串。讓我們一步步拆解。

### 步驟 1：安裝 Aspose OCR

在專案資料夾中開啟終端機，執行以下指令：

```bash
dotnet add package Aspose.OCR
```

此指令會下載最新的 Aspose OCR 二進位檔及其相依性。如果你偏好 NuGet 套件管理員 UI，只要搜尋 **Aspose.OCR** 並點擊 **Install** 即可。

### 步驟 2：初始化 OCR 引擎

建立 `OcrEngine` 實例是執行 **OCR** 時的第一步。可將其視為開啟掃描器的大腦。

```csharp
using Aspose.OCR;

// ...

// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **小技巧**：在多頁面上重複使用同一個 `OcrEngine` 可節省記憶體並加速處理。

### 步驟 3：將 DjVu 頁面載入為影像

大多數影像 API 無法直接支援 DjVu 檔案，但 Aspose 能將每頁視為位圖。此處我們使用 `System.Drawing.Image` 讀取檔案。

```csharp
using System.Drawing;

// ...

// Step 3: Load a DjVu page as an image
string djvuPath = @"C:\Path\To\Your\Directory\sample.djvu";
Image djvuPage = Image.FromFile(djvuPath);
```

> **為什麼這樣可行**：`Image.FromFile` 會自動將 DjVu 串流解碼為 OCR 引擎可理解的點陣格式。如果需要處理多頁 DjVu 中的特定頁面，請先使用 Aspose PDF 或 Aspose Imaging 取得該頁。

### 步驟 4：從影像辨識文字

現在魔法發生了。`Recognize` 方法會掃描位圖，並回傳包含偵測到字元的字串。

```csharp
// Step 4: Perform OCR to extract text from the image
string extractedText = ocrEngine.Recognize(djvuPage);
```

此時，你已 **從影像中辨識文字**，這些資料原本位於 DjVu 容器內。回傳的字串可能包含換行、標點，甚至在來源語言支援時的 Unicode 字元。

### 步驟 5：顯示或儲存結果

為了快速驗證，只需將文字輸出至主控台。在實務應用中，你可能會將其寫入檔案或資料庫。

```csharp
// Step 5: Display the recognized text
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(extractedText);
```

將所有步驟整合起來，以下是完整、可直接執行的程式。

```csharp
// File: DjvuOcrExample.cs
using System;
using System.Drawing;
using Aspose.OCR;

class DjvuExample
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load a DjVu page as an image
        Image djvuPage = Image.FromFile(@"C:\Path\To\Your\Directory\sample.djvu");

        // Perform OCR to extract text from the image
        string extractedText = ocrEngine.Recognize(djvuPage);

        // Display the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

**預期輸出**（為簡潔起見已截斷）：

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
Lorem ipsum dolor sit amet, consectetur...
```

如果看到亂碼，請確認 DjVu 檔案未加密，且已在 `ocrEngine.Language` 中設定正確語言。預設為英語；可透過 `ocrEngine.Language = Language.French;` 等方式切換至法語、德語等。

## 從影像辨識文字 – 常見陷阱

即使有完整範例，開發者仍常在某些邊緣情況上卡住：

| 問題 | 發生原因 | 解決方法 |
|-------|----------------|-----|
| **Blank output** | 圖像解析度太低 (<300 dpi)。 | 在呼叫 `Recognize` 前使用 `ocrEngine.ImageResolution = 300;`。 |
| **Wrong language** | OCR 預設為英語。 | 設定 `ocrEngine.Language = Language.Spanish;`（或任何支援的語言）。 |
| **Memory leak** | 大型 DjVu 頁面在處理後仍佔用記憶體。 | 完成後呼叫 `djvuPage.Dispose();`。 |
| **Multi‑page DjVu** | 只載入了第一頁。 | 使用 Aspose Imaging 的 `DjvuImage` 類別迴圈處理每一頁。 |

提前處理這些問題可為你節省無數除錯時間。

## 如何在 C# 中讀取 DjVu 檔案 – 超越簡易 OCR

如果你的專案需要處理多於單一頁面，必須先將每頁擷取為影像。Aspose Imaging 可輕鬆完成此工作：

```csharp
using Aspose.Imaging;
using Aspose.Imaging.FileFormats.Djvu;

// ...

string djvuPath = @"sample.djvu";
using (DjvuImage djvu = (DjvuImage)Image.Load(djvuPath))
{
    for (int i = 0; i < djvu.Frames.Count; i++)
    {
        using (Image page = djvu.Frames[i].ConvertToRaster())
        {
            // Run OCR on each page
            string pageText = ocrEngine.Recognize(page);
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(pageText);
        }
    }
}
```

## 從影像擷取文字 – 微調準確度

預設的 OCR 設定對於乾淨的掃描檔案已相當不錯，但仍可透過以下方式提升準確度：

```csharp
ocrEngine.ImagePreprocessingOptions = new ImagePreprocessingOptions()
{
    // Binarize the image to improve contrast
    BinarizationMethod = BinarizationMethod.Otsu,
    // Deskew the image if it’s tilted
    Deskew = true,
    // Remove noise
    NoiseRemoval = true
};
```

## 轉換 DjVu 為文字 – 完整端對端範例

以下是一個精簡版範例，將所有步驟整合：載入多頁 DjVu、前處理每頁、執行 OCR，並將結果儲存為 `.txt` 檔案。

```csharp
using System;
using System.IO;
using Aspose.Imaging;
using Aspose.Imaging.FileFormats.Djvu;
using Aspose.OCR;
using Aspose.OCR.Models;

class DjvuToTextConverter
{
    static void Main()
    {
        // Prepare OCR engine with preprocessing
        OcrEngine ocr = new OcrEngine
        {
            ImagePreprocessingOptions = new ImagePreprocessingOptions()
            {
                BinarizationMethod = BinarizationMethod.Otsu,
                Deskew = true,
                NoiseRemoval = true
            }
        };

        string inputPath = @"C:\Docs\sample.djvu";
        string outputPath = @"C:\Docs\sample_extracted.txt";

        using (DjvuImage djvu = (DjvuImage)Image.Load(inputPath))
        using (StreamWriter writer = new StreamWriter(outputPath))
        {
            for (int i = 0; i < djvu.Frames.Count; i++)
            {
                using (var page = djvu.Frames[i].ConvertToRaster())
                {
                    string text = ocr.Recognize(page);
                    writer.WriteLine($"--- Page {i + 1} ---");
                    writer.WriteLine(text);
                }
            }
        }

        Console.WriteLine($"Extraction complete. Text saved to {outputPath}");
    }
}
```

執行此腳本會產生 `sample_extracted.txt`，其中每頁內容皆已整齊分隔。這是將 DjVu **轉換為文字** 用於索引、搜尋或存檔的最快方法。

## 結論

我們已從頭到尾說明了 **如何對 DjVu 檔案執行 OCR**，並探討了 **從影像中辨識文字** 的方法。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}