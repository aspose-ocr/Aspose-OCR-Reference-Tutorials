---
category: general
date: 2026-04-08
description: 使用 GPU 的批次 PDF OCR 可快速從 PDF 檔案中提取文字。了解如何設定 OCR 語言以及在 C# 中使用 GPU 加速的 OCR。
draft: false
keywords:
- batch pdf ocr
- extract text from pdf
- gpu accelerated ocr
- set ocr language
language: zh-hant
og_description: 使用 GPU 的批次 PDF OCR 可讓您快速從 PDF 檔案中提取文字。本教學說明如何設定 OCR 語言並利用 GPU 加速。
og_title: 使用 GPU 的批量 PDF OCR – 快速文字提取指南
tags:
- Aspose.OCR
- C#
- GPU
title: 批量 PDF OCR（GPU）— 快速文字提取指南
url: /zh-hant/net/ocr-optimization/batch-pdf-ocr-with-gpu-fast-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 GPU 進行批次 PDF OCR – 快速文字擷取指南

需要 **使用 GPU 進行批次 PDF OCR** 以加速大量文件處理嗎？本指南將示範如何使用 Aspose.OCR 的 **GPU 加速 OCR** 引擎 **從 PDF 檔案擷取文字**。無論是處理成千上萬張發票，或是掃描法律檔案，設定 OCR 語言並啟用 GPU 都能為你的工作負載節省數分鐘，甚至數小時。

事實上，大多數開發者預設使用僅 CPU 的 OCR，結果常常慢得令人抓狂。完成本教學後，你將了解為什麼 GPU 很重要、如何設定引擎，以及如何在批次作業中從每一頁 PDF 取得乾淨的文字。全程僅使用純 C# 以及少量程式碼，無需額外工具。

## 需要的環境

- .NET 6.0 或更新版本（程式碼同樣可於 .NET Core 編譯）  
- Aspose.OCR for .NET 2024‑R3（或更新）— NuGet 套件 `Aspose.OCR`  
- 至少一張支援 CUDA 11+ 的 NVIDIA GPU（若使用相容的 AMD，需安裝相應驅動程式）  
- 基本的 C# async/await 知識（非必須，但有助於理解）  

如果這些都已備妥，太好了——我們直接開始。如果尚未配置 GPU，**設定 OCR 語言** 步驟仍可在 CPU 上執行，讓你先測試邏輯再連接 GPU。

---

## 批次 PDF OCR – 初始化 GPU 引擎

第一步是建立支援 GPU 的 OCR 引擎並開啟加速器。Aspose 提供 `GpuOcrEngine` 類別，繼承自一般的 `OcrEngine`。只要切換一個旗標即可啟用 GPU。

```csharp
using Aspose.Ocr;
using System;
using System.Collections.Generic;

/// <summary>
/// Demonstrates batch PDF OCR using a GPU‑accelerated engine.
/// </summary>
public static class PdfBatchOcrDemo
{
    public static void BatchPdfWithGpu()
    {
        // 1️⃣ Create a GPU‑aware OCR engine and enable the GPU.
        var ocrEngine = new GpuOcrEngine
        {
            Options = { EnableGpu = true, GpuDeviceId = 0 } // 0 = first GPU in the system
        };
```

**為什麼這很重要：**  
- **EnableGpu = true** 告訴 Aspose 將大量影像處理工作交給顯示卡。  
- **GpuDeviceId = 0** 代表使用第一張 GPU；若有多張卡可自行調整索引。  
- 使用 `GpuOcrEngine` 取代 `OcrEngine`，API 完全相同，但效能提升明顯。

> **專業小技巧：** 若在無介面的伺服器上執行，請確保已全域安裝 NVIDIA 驅動程式與 CUDA 執行環境；否則引擎會悄悄回退至 CPU。

---

## 設定 OCR 語言 (set OCR language)

接著告訴引擎要辨識哪種語言。Aspose 會在首次請求時自動下載語言套件，無需自行打包大型檔案。

```csharp
        // 2️⃣ Set the language for recognition – “en” for English.
        ocrEngine.Language = "en";
```

你可以將 `"en"` 替換為任意 ISO‑639‑1 代碼（例如 `"fr"`、`"de"`、`"es"` 等）。若需多語言支援，請使用逗號分隔的清單，如 `"en,fr"`。

**為什麼要設定語言：**  
- OCR 引擎會使用語言專屬的字典提升辨識準確度。  
- 若未設定，預設為英文，可能會誤判其他文字系統的字元。  
- 自動下載確保你始終擁有最新模型，免除手動更新的麻煩。

---

## 從 PDF 頁面擷取文字

現在列出要處理的 PDF 檔案。實務上你可能會從目錄或資料庫讀取檔名；此處為了說明直接寫死一小段清單。

```csharp
        // 3️⃣ List the PDF pages to be processed.
        var pdfPagePaths = new List<string>
        {
            @"YOUR_DIRECTORY\page1.pdf",
            @"YOUR_DIRECTORY\page2.pdf",
            @"YOUR_DIRECTORY\page3.pdf"
        };
```

> **注意：** 使用逐字字串 (`@""`) 可避免在 Windows 上必須跳脫反斜線。

清單備妥後，我們逐一遍歷每個檔案、執行 OCR，並輸出字元數量——這是一個快速的 sanity check，確認引擎真的有讀到內容。

```csharp
        // 4️⃣ Recognize each page and output the character count.
        foreach (var pagePath in pdfPagePaths)
        {
            // RecognizePdf returns an OcrResult containing the extracted text.
            var ocrResult = ocrEngine.RecognizePdf(pagePath);
            Console.WriteLine($"Page {pagePath} → {ocrResult.Text.Length} characters");
        }
    }
}
```

**預期輸出（範例）：**

```
Page YOUR_DIRECTORY\page1.pdf → 1284 characters
Page YOUR_DIRECTORY\page2.pdf → 1120 characters
Page YOUR_DIRECTORY\page3.pdf → 1439 characters
```

如果看到 `0 characters`，請再次確認 PDF 是否真的只有可選取的文字或嵌入的影像；Aspose OCR 針對光柵化頁面（掃描 PDF）運作良好，但原生 PDF 若隱藏文字可能需要其他處理方式。

---

## 驗證結果與處理例外情況

在批次作業中執行 OCR 並非總是一帆風順。以下列出常見問題與對策。

| 問題 | 症狀 | 解決方式 |
|------|------|----------|
| **缺少 GPU 驅動程式** | `Aspose.Ocr.Exceptions.OcrException: GPU not available` | 安裝最新的 NVIDIA 驅動程式與 CUDA 工具組。 |
| **大型 PDF 記憶體不足** | 程式在數頁後崩潰 | 增加 `Options.MaxMemoryUsage`，或改用 `RecognizePdfPage` 逐頁處理。 |
| **語言套件未下載** | 文字雜亂或為空 | 確認首次設定 `ocrEngine.Language` 時機器能連上網路。 |
| **PDF 檔案損毀** | `System.IO.IOException: Cannot read file` | 在送入 OCR 前先驗證檔案完整性，例如使用 `PdfDocument.Load`。 |

你也可以將原始 OCR 文字抓下來作後續處理——寫入 `.txt` 檔、送入搜尋索引，或提供給語言模型進行摘要。

```csharp
        // Example: Save each OCR result to a .txt file.
        foreach (var pagePath in pdfPagePaths)
        {
            var ocrResult = ocrEngine.RecognizePdf(pagePath);
            var txtPath = System.IO.Path.ChangeExtension(pagePath, ".txt");
            System.IO.File.WriteAllText(txtPath, ocrResult.Text);
            Console.WriteLine($"Saved OCR text to {txtPath}");
        }
```

**為什麼要儲存：**  
- 將繁重的 OCR 步驟與後續分析解耦，只需一次擷取即可無限次使用純文字檔。  
- 相較於 PDF，文字檔體積極小，適合放入版本控制或做 diff。

---

## 完整範例程式

以下是一個完整的主控台應用程式範例，直接貼到新建的 `.csproj` 專案即可執行。將 `YOUR_DIRECTORY` 替換成實際存放 PDF 的路徑。

```csharp
using Aspose.Ocr;
using System;
using System.Collections.Generic;

namespace BatchPdfOcrGpuDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            BatchPdfWithGpu();
        }

        /// <summary>
        /// Executes batch PDF OCR using a GPU‑accelerated engine.
        /// </summary>
        public static void BatchPdfWithGpu()
        {
            // Step 1 – Initialize GPU engine.
            var ocrEngine = new GpuOcrEngine
            {
                Options = { EnableGpu = true, GpuDeviceId = 0 }
            };

            // Step 2 – Set the OCR language (auto‑download enabled).
            ocrEngine.Language = "en";

            // Step 3 – Define the PDFs to process.
            var pdfPagePaths = new List<string>
            {
                @"YOUR_DIRECTORY\page1.pdf",
                @"YOUR_DIRECTORY\page2.pdf",
                @"YOUR_DIRECTORY\page3.pdf"
            };

            // Step 4 – Run OCR on each file and write results.
            foreach (var pagePath in pdfPagePaths)
            {
                var ocrResult = ocrEngine.RecognizePdf(pagePath);
                Console.WriteLine($"Page {pagePath} → {ocrResult.Text.Length} characters");

                // Optional: persist the extracted text.
                var txtPath = System.IO.Path.ChangeExtension(pagePath, ".txt");
                System.IO.File.WriteAllText(txtPath, ocrResult.Text);
                Console.WriteLine($"Saved OCR text to {txtPath}");
            }
        }
    }
}
```

編譯指令：

```bash
dotnet build
dotnet run
```

執行後，你會看到每個 PDF 的字元統計，且相對應的 `.txt` 檔會出現在同一目錄下。

---

![Batch PDF OCR GPU processing diagram](https://example.com/image.png "Batch PDF OCR with GPU")

*圖片說明：**使用 GPU 進行批次 PDF OCR** 流程圖，顯示 PDF → GPU OCR → 文字輸出。*

---

## 後續步驟與相關主題

- **GPU 加速 vs. 僅 CPU 效能比較：** 執行 100 頁的快速基準測試，觀察耗時差異。現代 GPU 可望提升 2‑5 倍。  
- **多語言批次處理：** 設定 `ocrEngine.Language = "en,fr,es"`，一次辨識多種語言文件。  
- **串流大型 PDF：** 使用 `RecognizePdfPage` 逐頁 OCR，降低記憶體壓力。  
- **整合至 Azure Functions 或 AWS Lambda：** 將批次作業搬到雲端，利用支援 GPU 的執行個體彈性擴充。  
- **搜尋索引：** 把擷取的文字送入 Elasticsearch 或 Azure Cognitive Search，實現快速文件檢索。

---

## 結論

你已掌握 **使用 GPU 進行批次 PDF OCR** 的全套技巧，學會如何 **從 PDF 檔案高效擷取文字**，以及正確 **設定 OCR 語言** 以獲得最佳辨識率。啟用 GPU 後，處理時間會大幅縮短；而 Aspose 簡潔的 API 讓你免除繁雜的 OCR 前置工作。

現在就把它套用到自己的資料集吧——調整語言清單、嘗試不同 GPU 裝置，或將邏輯封裝成背景服務。結合高效能 OCR 與現代 .NET 工具，未來的可能性無限。

有任何問題，或遇到本文未涵蓋的例外情況？歡迎在 Aspose 論壇留言或開啟 Issue。祝開發順利，願你的 OCR 作業快速且零錯誤！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}