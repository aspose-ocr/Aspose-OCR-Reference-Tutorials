---
category: general
date: 2025-12-30
description: 使用 Aspose OCR 於 C# 將影像轉換為 PDF。了解如何對影像進行 OCR 前置處理、辨識韓文文字影像，並快速建立可搜尋的 PDF
  影像。
draft: false
keywords:
- convert image to pdf
- preprocess image for ocr
- recognize korean text image
- create searchable pdf image
language: zh-hant
og_description: 將圖像轉換為 PDF（使用 Aspose OCR）。本教學示範如何為 OCR 預處理圖像、辨識韓文文字圖像，並建立可搜尋的 PDF
  圖像。
og_title: 在 C# 中將圖片轉換為 PDF – 完整 OCR 指南
tags:
- C#
- OCR
- Aspose
- PDF
title: 在 C# 中將圖像轉換為 PDF – 完整 OCR 指南
url: /zh-hant/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中將圖像轉換為 PDF – 完整 OCR 指南

是否曾需要 **將圖像轉換為 PDF**，同時希望內部文字可搜尋？你並非唯一遇到此需求的人。許多開發者在處理掃描頁面時，尤其是韓文書籍時，常會卡在這裡。好消息是，使用 Aspose OCR 你可以 **預處理圖像以供 OCR**、**辨識韓文文字圖像**，最後 **建立可搜尋的 PDF 圖像**，只需幾行程式碼。

在本教學中，我們將逐步說明整個流程——從載入韓文書籍頁面的原始 JPEG、清理圖像、擷取文字，最後封裝成可搜尋的 PDF。完成後，你將擁有一個可直接執行的 C# 主控台應用程式，隨時可放入任何 .NET 專案中。

## 需要的條件

- **.NET 6.0 或更新版本**（此程式碼同時適用於 .NET Core 與 .NET Framework）  
- **Aspose.OCR for .NET** NuGet 套件（`Aspose.OCR`）——免費試用金鑰可於 Aspose 官方網站取得。  
- 含有韓文文字的範例圖像（例如 `korean_book_page.jpg`）。  
- 你選擇的開發環境（Visual Studio、VS Code、Rider —— 我使用 VS 2022）。

> **專業提示：** 請將圖像檔案放在專用資料夾，例如 `Resources/`，以確保路徑在不同機器間保持一致。

## 流程概覽

1. **初始化 OCR 引擎**，並啟用 GPU 加速以提升速度。  
2. **加入前處理濾鏡**（去斜、去噪）以提高辨識準確度。  
3. **下載並載入韓文語言模型**——若需要，Aspose 會自動執行此步驟。  
4. **對輸入圖像執行辨識**。  
5. **使用內建匯出器將結果匯出為可搜尋的 PDF**。  
6. **（可選）將結果序列化為 JSON**，以供後續分析或記錄。

以下我們將逐步拆解每個步驟，說明 *為何* 重要，並提供可直接 copy‑paste 的完整程式碼。

---

## ## Convert Image to PDF – 完整工作流程

以下程式碼片段是 *完整* 程式。你可以建立一個新的主控台專案（`dotnet new console -n OcrPdfDemo`），並將自動產生的 `Program.cs` 替換為此程式碼。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;
using Aspose.OCR.Result;   // for JsonResult

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialise the OCR engine (GPU enabled, offline mode off)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,          // leverages your graphics card for faster inference
                OfflineMode = false    // allows on‑the‑fly language model download
            };

            // --------------------------------------------------------------
            // Step 2: Add preprocessing filters to improve accuracy
            // --------------------------------------------------------------
            // Deskew corrects slight rotations; MaxAngle = 12° is a safe default.
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 12 });

            // Denoise removes isolated speckles that often appear in scanned books.
            ocrEngine.Filters.Add(new DenoiseFilter());

            // --------------------------------------------------------------
            // Step 3: Load the Korean language model
            // --------------------------------------------------------------
            // Aspose will download the model the first time you run this on a new machine.
            ocrEngine.LoadLanguage(LanguageModel.Korean);

            // --------------------------------------------------------------
            // Step 4: Recognise text from the input image
            // --------------------------------------------------------------
            // Replace the path with your actual image location.
            string imagePath = "Resources/korean_book_page.jpg";
            var recognitionResult = ocrEngine.Recognize(imagePath);

            // --------------------------------------------------------------
            // Step 5: Export the recognised page as a searchable PDF
            // --------------------------------------------------------------
            string pdfPath = "Resources/korean_page.pdf";
            var exporter = new SearchablePdfExporter { OutputPath = pdfPath };
            exporter.Export(ocrEngine, imagePath);

            // --------------------------------------------------------------
            // Step 6: Obtain a structured JSON representation of the result
            // --------------------------------------------------------------
            string json = JsonResult.FromRecognitionResult(recognitionResult).ToString(true);
            Console.WriteLine("=== OCR JSON Result ===");
            Console.WriteLine(json);

            Console.WriteLine("\n✅ Conversion complete!");
            Console.WriteLine($"PDF saved to: {pdfPath}");
        }
    }
}
```

### 為何這樣有效

- **GPU acceleration** 可將辨識時間大幅縮短約一半，相較於僅使用 CPU 的模式。  
- **Deskew** 與 **Denoise** 是經典的 *preprocess image for OCR* 技術；它們可校正常見的掃描缺陷，否則會導致引擎遺漏字元。  
- **Language model loading** 對於 **recognize Korean text image** 至關重要——若未載入韓文模型，引擎會退回使用通用的拉丁字母，結果會變成亂碼。  
- **SearchablePdfExporter** 會將原始點陣圖與隱形文字層合併，為你提供 **create searchable pdf image** 的結果，讓任何 PDF 檢視器都能索引。

---

## ## Preprocess Image for OCR – 小技巧與建議

雖然我們加入的兩個濾鏡通常已足夠，但你可能仍會遇到頑固的圖像。以下提供幾個可嘗試的額外步驟：

| 問題 | 額外濾鏡 | 加入方式 |
|-------|-------------------|------------|
| 對比度低 | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| 背景噪點嚴重 | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| 混合方向（直向與橫向） | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **注意：** 加入過多濾鏡會降低處理速度。請先在單頁測試每項變更，再進行大規模處理。

---

## ## Recognize Korean Text Image – 常見陷阱

韓文文字由視覺上密集的 Hangul 音節組成。若發現輸出雜亂：

1. **確保語言模型已完整下載**——於主控台檢查是否出現類似 “Downloading Korean model…” 的訊息。  
2. 若掃描圖像旋轉角度超過 12°，請在 `DeskewFilter` 中 **提升 `MaxAngle`**。  
3. 透過設定 `ocrEngine.GpuMemoryLimit = 2048;`（單位為 MB）來 **增加 GPU 記憶體**。

這些調整會直接影響 **recognize Korean text image** 的成功率。

---

## ## Create Searchable PDF Image – 驗證結果

程式執行完畢後，於任意 PDF 閱讀器（Adobe Acrobat Reader、Foxit，甚至 Chrome）開啟 `korean_page.pdf`。你應該能夠：

- 使用滑鼠 **選取文字**，就像在原生 PDF 中一樣。  
- 使用內建搜尋框 **搜尋** 韓文詞彙。

若文字層顯示為空白，請再次確認 `Export` 方法傳入的圖像路徑正確，且 OCR 結果的 `RecognitionResult.Text` 非空。

---

## ## Full JSON Output – 預期結果

主控台會印出格式良好的 JSON 資料。以下是一個簡化的範例：

```json
{
  "Text": "첫 번째 페이지의 내용...",
  "Blocks": [
    {
      "Text": "첫 번째 페이지의 내용...",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 560, "Height": 780 },
      "Confidence": 0.98
    }
  ],
  "Language": "Korean",
  "ProcessingTimeMs": 842
}
```

---

## ## 故障排除與 FAQ

**Q: 我的 PDF 相較於原始圖像過大。**  
A: 匯出器會以原始解析度嵌入位圖。若檔案大小是考量，請在辨識前先將圖像縮小：

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q: OCR 回傳空字串。**  
A: 請確認圖像路徑正確且檔案未損毀。同時，確保 GPU 驅動程式為最新版本；舊版驅動可能導致靜默失敗。

**Q: 能否在迴圈中處理多頁？**  
A: 當然可以。將第 4‑6 步驟包在 `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` 迴圈中，並依需求調整輸出 PDF 的路徑。

---

## ## 結論

我們剛剛 **將圖像轉換為 PDF**，同時保留可搜尋的文字，這全賴 Aspose OCR 強大的流程。透過 **preprocess image for OCR** 提升準確度；透過 **recognize Korean text image** 處理複雜文字；再透過 **create searchable pdf image** 取得可攜帶且可索引的文件。

取得程式碼，指向你自己的掃描檔，並嘗試額外的濾鏡或語言模型。相同的模式同樣適用於中文、日文或任何拉丁語系——只需將 `LanguageModel.Korean` 換成相應的列舉即可。

還有其他問題嗎？歡迎留言，祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}