---
category: general
date: 2026-02-28
description: 在 C# 中透過垂直合併圖像建立可搜尋的 PDF。了解如何垂直堆疊圖像，並使用 Aspose OCR 轉換掃描頁面的 PDF。
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: zh-hant
og_description: 在 C# 中透過垂直合併圖像來建立可搜尋的 PDF。本指南示範如何垂直堆疊圖像，並使用 Aspose OCR 將掃描頁面轉換為 PDF。
og_title: 使用 C# 建立可搜尋的 PDF – 垂直合併圖片
tags:
- Aspose OCR
- C#
- PDF generation
title: 在 C# 中建立可搜尋的 PDF – 垂直合併圖像
url: /zh-hant/net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中建立可搜尋的 PDF – 垂直合併影像

是否曾需要從少量掃描的 PNG 建立 **可搜尋的 PDF**，卻不知從何下手？您並不孤單。在許多文件自動化專案中，最大痛點往往是將一堆影像檔案轉換成一個整齊、可搜尋的 PDF，方便索引與分享。

在本教學中，我們將逐步示範一個完整、可直接執行的範例，說明如何 **垂直堆疊影像**、**垂直合併影像**，以及最終使用 Aspose.OCR 的 GPU 加速引擎將 **掃描頁面 PDF** 轉換為單一可搜尋的文件。完成後，您將擁有一個可自行嵌入任何 .NET 解決方案的獨立程式。

> **您將學會**
> - 使用 GPU 支援初始化 OCR 引擎。
> - 並行處理一批影像。
> - **垂直合併影像** 以模擬多頁掃描。
> - 匯出可搜尋的 PDF 以及供後續分析使用的詳細 JSON 報告。

- .NET 6+（程式碼可在 .NET 6、.NET 7 或 .NET 8 上編譯）
- Aspose.OCR NuGet 套件（`Install-Package Aspose.OCR`）
- 若想保留 `ProcessingMode.Gpu` 設定，需具備支援 GPU 的機器（亦可使用 CPU 回退）
- 一個包含數個掃描 PNG/JPEG 檔案的資料夾（示範使用 `page1.png`、`page2.png`、`page3.png`）

不需要外部服務，也沒有隱藏的設定檔——純粹的 C#。

## 步驟 1 – 設定 OCR 引擎以 **建立可搜尋的 PDF**

首先，我們建立 `OcrEngine`，啟用 GPU 加速，選擇英語作為語言，並加入兩個前置處理過濾器。這些過濾器可透過校正傾斜頁面（`DeskewFilter`）與去除雜訊（`DenoiseFilter`）來提升辨識準確度。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Collections.Generic;
using System.Drawing;

class AllInOneDemo
{
    static void Main()
    {
        // Initialize OCR engine – this is the heart of creating a searchable PDF
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu,   // Switch to CPU if no GPU
            Language = OcrLanguage.English
        };
        // Pre‑processing improves OCR quality
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseFilter());
```

**為何重要**：OCR 引擎負責文字辨識的繁重工作。啟用 `ProcessingMode.Gpu` 可在現代顯示卡上將辨識時間減半，而過濾器則可減少常見的掃描雜訊，避免產生亂碼輸出。

## 步驟 2 – 設定批次處理器以高效 **轉換掃描頁面 PDF**

逐頁處理對於少量影像尚可，但實務專案常涉及數十或數百頁。Aspose.OCR 的 `OcrBatchProcessor` 允許我們平行執行辨識，顯著加速 **轉換掃描頁面 pdf** 的步驟。

```csharp
        // Set up batch processor – ideal for converting many scanned pages to PDF
        var batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 2,          // Adjust based on CPU/GPU cores
            Language = OcrLanguage.English,
            ProcessingMode = ProcessingMode.Gpu
        };

        // List the image files you want to turn into a searchable PDF
        List<string> imageFiles = new()
        {
            "YOUR_DIRECTORY/page1.png",
            "YOUR_DIRECTORY/page2.png",
            "YOUR_DIRECTORY/page3.png"
        };
```

**小技巧**：若使用僅有 CPU 的機器，請將 `ProcessingMode = ProcessingMode.Cpu`。批次處理器仍會遵守 `MaxDegreeOfParallelism`，您可調整此參數以免過度負載機器。

## 步驟 3 – 在批次上執行 OCR 並收集結果

現在正式進行文字辨識。`Recognize` 方法會回傳 `OcrResult` 物件的清單，每個物件皆包含原始影像與擷取出的文字。

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

此時您已擁有建立 **可搜尋的 PDF** 所需的一切：影像（仍在記憶體中）以及對應的文字層。

## 步驟 4 – **垂直合併影像** 並產生可搜尋的 PDF

大多數掃描文件都是多頁 PDF，因此我們需要將各頁影像拼接成一張高長的影像，以模擬實體堆疊。Aspose.OCR 提供 `Image.CombineVertical` 正好可用於此目的。

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

產生的檔案（`combined_searchable.pdf`）在每頁影像下方包含可選取、可搜尋的文字——正是從掃描來源 **建立可搜尋的 PDF** 所需的功能。

![建立可搜尋的 PDF 範例](/images/create-searchable-pdf.png "建立可搜尋的 PDF 範例")

*圖片說明：建立可搜尋的 PDF 範例，顯示合併後的 PDF 內含可搜尋的文字。*

**為何使用垂直堆疊？** 許多 OCR 函式庫會將每張影像視為獨立頁面。透過堆疊，我們能保持 PDF 的頁序不變，同時只需一次 OCR 即可處理整份文件。

## 步驟 5 – 為第一頁匯出詳細 JSON（適用於後續工作流程）

有時候您需要的不止 PDF；或許想將 OCR 資料寫入資料庫或機器學習管線。Aspose.OCR 允許您將每個 `OcrResult` 序列化為 JSON，保留邊界框、信心分數等資訊。

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**預期的 JSON 片段（已截斷）：**

```json
{
  "Text": "Sample scanned text …",
  "Confidence": 0.97,
  "Blocks": [
    {
      "Text": "Header",
      "BoundingBox": { "X": 15, "Y": 10, "Width": 480, "Height": 30 }
    }
    // …
  ]
}
```

現在您可以將此 JSON 輸入任何後續系統——無論是將文字索引至 Elasticsearch，或是送入自訂分析儀表板。

---

## 如何 **垂直堆疊影像** – 快速回顧

如果您在想 **如何在不使用 Aspose 的情況下垂直堆疊影像**，可以使用 `System.Drawing` 建立新位圖，依序繪製每頁。然而，Aspose 內建的 `Image.CombineVertical` 會自動處理 DPI、像素格式與記憶體管理，是正式環境中最可靠的選擇。

### 替代方案：使用 `System.Drawing`（僅供好奇）

```csharp
int totalHeight = 0;
int maxWidth = 0;
foreach (var img in ocrResults)
{
    totalHeight += img.Image.Height;
    maxWidth = Math.Max(maxWidth, img.Image.Width);
}
var canvas = new Bitmap(maxWidth, totalHeight);
using var g = Graphics.FromImage(canvas);
int offset = 0;
foreach (var img in ocrResults)
{
    g.DrawImage(img.Image, 0, offset);
    offset += img.Image.Height;
}
canvas.Save("combined_manual.png");
```

手動方式可行，但會失去自動 DPI 處理的便利性，以及直接將結果回傳給 `RecognizeToPdf` 的能力。除非有非常特殊的需求，否則建議仍使用 `CombineVertical`。

## 常見陷阱與避免方法

| 問題 | 為何會發生 | 解決方式 |
|-------|----------------|-----|
| **記憶體不足錯誤** 在處理數十張高解析度掃描時 | 每張影像會保留在記憶體中，直至 PDF 寫入完成 | 在使用完畢後立即釋放 `Image` 物件（使用 `using` 區塊），或在合併前先縮小影像尺寸 |
| **文字雜訊** OCR 後 | 掃描傾斜或對比度低 | 保留 `DeskewFilter` 與 `DenoiseFilter`；如有需要，可加入 `ContrastFilter` |
| **缺少可搜尋層** | 使用了 `Recognize` 而非 `RecognizeToPdf` | 確保對合併後的影像呼叫 `ocrEngine.RecognizeToPdf` |
| **GPU 回退失敗** 在沒有適當驅動程式的機器上 | `ProcessingMode.Gpu` 會拋出例外 | 將引擎建立包在 try/catch 中，若失敗則回退至 `ProcessingMode.Cpu` |

## 往後步驟 – 擴充工作流程

既然您已了解如何 **建立可搜尋的 PDF**，接下來可能想要：

- 使用 `Directory.GetFiles` 搭配 `foreach` 迴圈 **批次處理整個資料夾**。
- 在合併前為每頁 **加入浮水印**（使用 Aspose.Imaging 的 `ImageProcessor`）。
- 若日後需要單頁 PDF，**將可搜尋的 PDF 拆分回個別頁面**（使用 Aspose.PDF 的 `PdfDocument.Split`）。
- **整合 Azure Blob Storage**，從雲端取得影像並上傳最終 PDF。

所有這些擴充皆基於相同的核心概念：OCR 設定、影像處理與 PDF 匯出。

---

## 結論

我們已說明如何在 C# 中從一系列掃描影像 **建立可搜尋的 PDF**。透過初始化支援 GPU 的 `OcrEngine`、使用 `OcrBatchProcessor` 進行平行批次處理、**垂直合併影像**，最後呼叫 `RecognizeToPdf`，即可得到整齊、可搜尋的文件，適合歸檔或索引。額外的 JSON 匯出則提供完整的 OCR 結果資訊，為分析或自訂工作流程開啟可能性。

試著執行看看，實驗不同的過濾器，您會發現文件自動化流程變得更順暢。若遇到任何問題，歡迎留言——祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}