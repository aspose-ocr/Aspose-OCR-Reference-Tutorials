---
category: general
date: 2026-01-12
description: C# OCR 教學，示範如何辨識文字影像、以 C# 擷取文字影像，並產生帶有信心分數的影像轉 PDF OCR 檔案。
draft: false
keywords:
- c# ocr tutorial
- image to pdf ocr
- recognize text image
- ocr confidence scores
- extract text image c#
language: zh-hant
og_description: 學習完整的 C# OCR 教學，識別文字圖像、提取文字圖像（C#），並將圖像轉換為 PDF OCR 文件，並顯示信心分數。
og_title: c# OCR 教學 – 將圖像轉換為可搜尋的 PDF
tags:
- OCR
- C#
- PDF
title: c# OCR 教學 – 將圖像轉換為可搜尋的 PDF
url: /zh-hant/net/text-recognition/c-ocr-tutorial-turn-images-into-searchable-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr 教程 – 將圖像轉換為可搜尋的 PDF

有沒有想過如何在 C# 專案中 **recognize text image** 檔案，而不必尋找第三方服務？你並不孤單。在許多實際應用中——例如發票掃描器、收據追蹤器或多語言文件檔案庫——開發人員需要一個可靠、內部部署的 OCR 引擎，且能輸出信心分數。  

本 **c# ocr tutorial** 將一步步帶領你完成所有需求：從載入圖片、選擇語言模型、切換 GPU 加速，到將結果儲存為可搜尋的 PDF。完成後，你將擁有一個即時可執行的程式範例，能提取文字、回報 OCR 信心分數，並可選擇產生 *image to pdf ocr* 檔案——全部在不到一分鐘的編寫時間內完成。

## 你將構建的內容

- 載入多語言圖片（`sample_multi_lang.jpg` 為佔位圖）。  
- 選擇阿拉伯語、印地語和俄語語言模型（可自行新增）。  
- 若機器支援，開啟 GPU 處理。  
- 取得原始 OCR 結果 **with confidence scores**。  
- 將結果序列化為格式化的 JSON **or** 寫入可搜尋的 PDF。  

不使用外部網路服務，也沒有隱藏的魔法——僅使用 Aspose.OCR for .NET、少量 C# 程式碼，並清楚說明每一行 **why** 的意義。

## 前置條件

- .NET 6.0 或更新版本（程式碼可在 .NET Core 與 .NET Framework 上編譯）。  
- Visual Studio 2022（或任何你喜歡的 IDE）。  
- Aspose.OCR for .NET 授權（免費試用版可用於測試）。  
- 可選：若想加速辨識，需具備相容 CUDA 的 GPU。  

> **Pro tip:** 若沒有 GPU，只需將 `UseGpu = false` 設為 false，引擎會自動回退至 CPU，且不需修改程式碼。

## 步驟 1：安裝必要的 NuGet 套件

在 **Package Manager Console** 中開啟並執行以下指令：

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Gpu
Install-Package Newtonsoft.Json
```

## 步驟 2：設定專案結構

建立新的主控台專案（`dotnet new console -n AsposeOcrDemo`），並將產生的 `Program.cs` 替換為以下程式碼。  
所有邏輯皆位於 `Program` 類別中；唯一額外的型別是一個小型擴充方法，用於將 OCR 結果格式化為 JSON。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.Models;
using Newtonsoft.Json;

namespace AsposeOcrDemo
{
    class Program
    {
        // Step 1: Input image and language models
        private const string InputImagePath = @"YOUR_DIRECTORY/sample_multi_lang.jpg";
        private static readonly string[] Languages = { LanguageModel.Arabic, LanguageModel.Hindi, LanguageModel.Russian };

        // Step 2: Processing options (GPU toggle & output format)
        private const bool UseGpu = true;               // set false if no GPU
        private const string OutputFormat = "Json";     // change to "Pdf" for PDF output

        static void Main()
        {
            // Step 3: Initialise the appropriate OCR engine
            IOcrEngine engine = UseGpu ? (IOcrEngine)new GpuOcrEngine() : new OcrEngine();

            // Step 4: Run OCR – language models are auto‑downloaded if missing
            OcrResult result = engine.Recognize(
                InputImagePath,
                new OcrOptions { LanguageModels = Languages, AutoDownloadResources = true });

            // Step 5: Emit the result in the chosen format
            if (OutputFormat.Equals("json", StringComparison.OrdinalIgnoreCase))
            {
                string json = JsonConvert.SerializeObject(
                    result.GetWordsWithConfidence(),
                    Formatting.Indented);
                Console.WriteLine(json);
            }
            else if (OutputFormat.Equals("pdf", StringComparison.OrdinalIgnoreCase))
            {
                string pdfPath = Path.ChangeExtension(InputImagePath, ".pdf");
                File.WriteAllBytes(pdfPath, result.Pdf);
                Console.WriteLine($"PDF saved to: {pdfPath}");
            }
        }
    }

    // Helper that flattens OcrResult into a JSON‑friendly structure
    internal static class OcrResultExtensions
    {
        public static object GetWordsWithConfidence(this OcrResult result)
        {
            var words = new System.Collections.Generic.List<object>();
            foreach (var w in result.Words)
                words.Add(new
                {
                    Text = w.Text,
                    Confidence = w.Confidence,
                    BoundingBox = new { w.Bounds.X, w.Bounds.Y, w.Bounds.Width, w.Bounds.Height }
                });

            return new
            {
                RecognizedText = result.Text,
                LanguageModels = result.UsedLanguageModels,
                Words = words,
                ProcessingTimeMs = result.ProcessingTime.TotalMilliseconds
            };
        }
    }
}
```

### 為何此程式碼可運作

1. **GPU toggle** – `GpuOcrEngine` 利用 CUDA 核心；三元運算子讓切換變得毫不費力。  
2. **Automatic language download** – `AutoDownloadResources = true` 確保在首次執行應用程式時會下載阿拉伯語、印地語與俄語模型。  
3. **Confidence scores** – `result.Words` 包含每個辨識字詞的 `Confidence`；擴充方法會將其格式化為整潔的 JSON 物件。  
4. **Searchable PDF** – `result.Pdf` 已是完整的可搜尋 PDF，我們只需將位元組陣列寫入磁碟。無需額外函式庫。

## 步驟 6：執行範例

開啟終端機，切換至專案資料夾，執行以下指令：

```bash
dotnet run
```

若選擇 **JSON** 輸出，會看到類似以下內容：

```json
{
  "RecognizedText": "مرحبا Hello Привет",
  "LanguageModels": [
    "Arabic",
    "Hindi",
    "Russian"
  ],
  "Words": [
    {
      "Text": "مرحبا",
      "Confidence": 0.98,
      "BoundingBox": { "X": 45, "Y": 12, "Width": 120, "Height": 30 }
    },
    {
      "Text": "Hello",
      "Confidence": 0.99,
      "BoundingBox": { "X": 180, "Y": 12, "Width": 80, "Height": 30 }
    },
    {
      "Text": "Привет",
      "Confidence": 0.97,
      "BoundingBox": { "X": 280, "Y": 12, "Width": 110, "Height": 30 }
    }
  ],
  "ProcessingTimeMs": 312
}
```

若改為 **PDF**，主控台會印出路徑，且你會在原始圖像旁找到可搜尋的 PDF。

## 常見問題與邊緣情況

- **如果語言模型不可用會怎樣？**  
  OCR 引擎會拋出明確的 `ResourceNotFoundException`。由於我們設定 `AutoDownloadResources = true`，缺少的模型會在首次執行時自動下載，因此在正式環境中很少會看到此例外。

- **我可以一次處理多張影像嗎？**  
  當然可以。將 `engine.Recognize` 呼叫包在遍歷檔案目錄的 `foreach` 迴圈中。相同的 `OcrResultExtensions` 可用於每張影像。

- **GPU 需要授權嗎？**  
  不需要。免費試用版同時支援 CPU 與 GPU。完整授權會移除試用水印並解除頁數限制。

- **信心分數的準確度如何？**  
  分數介於 0.0（毫無信心）至 1.0（完美信心）之間。實務上，超過 0.90 的分數通常足以供後續處理使用；若需要更嚴格的驗證，可過濾低於此門檻的字詞。

## 步驟 7：後續步驟（擴充你的 OCR 工具箱）

1. **新增更多語言** – 只需將 `LanguageModel.French`（或任何支援的模型）加入 `Languages` 陣列。  
2. **結合 OCR 與 PDF/A 轉換** – Aspose.PDF 可將 OCR 層嵌入符合 PDF/A‑2b 標準的文件，以供保存。  
3. **整合 Azure Functions** – 將邏輯封裝為無伺服器端點，即時處理上傳。  
4. **微調信心門檻** – 使用 `result.Words.Where(w => w.Confidence < 0.85)` 來標記不確定的字詞，以便人工審核。

---

### TL;DR

本 **c# ocr tutorial** 示範如何：

- 載入影像並選擇多種語言模型。  
- 使用單一布林旗標開啟 GPU 加速。  
- 取得 OCR 結果 **with confidence scores** 並序列化為 JSON。  
- 可選擇寫入可搜尋的 PDF（**image to pdf ocr**）。  

以上全部僅需幾行程式碼、免費的 Aspose.OCR 試用版，即可完成。試著執行、調整語言清單，你將在數分鐘內擁有可投入生產的 OCR 流程。

![c# ocr 教程範例圖](https://example.com/placeholder-image.jpg "c# ocr 教程範例圖")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}