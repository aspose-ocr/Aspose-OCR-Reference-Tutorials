---
category: general
date: 2026-03-23
description: 使用 Aspose OCR 從影像建立可搜尋的 PDF。了解如何將 TIFF 轉換為高壓縮的 PDF，並在數分鐘內辨識影像文字。
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- high compression pdf
- recognize image text
- searchable pdf from image
language: zh-hant
og_description: 使用 Aspose OCR 從圖像建立可搜尋的 PDF。本教學示範如何將 TIFF 轉換為 PDF、加入可搜尋的文字層，並套用高壓縮。
og_title: 從圖片建立可搜尋 PDF – 完整 C# 指南
tags:
- Aspose OCR
- C#
- PDF generation
title: 從圖像建立可搜尋的 PDF – 完整 C# 指南
url: /zh-hant/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像建立可搜尋 PDF – 完整 C# 指南

有沒有需要 **建立可搜尋 pdf**，卻不知道從哪裡開始？你並不孤單——許多開發者在將 TIFF 掃描檔轉成可搜尋 PDF 時都卡在同一個問題上。好消息是：使用 Aspose OCR，你可以 **convert tiff to pdf**，在上面加上一層隱藏文字，甚至透過 **high compression pdf** 選項壓縮檔案大小，全部只需幾行 C# 程式碼。

在本教學中，我們將完整示範整個流程：從安裝 NuGet 套件、載入 TIFF 圖像、辨識文字，到最後匯出可搜尋的 PDF。完成後，你會得到一個可執行的 console 應用程式，能 **recognize image text**，並產生一個緊湊、可搜尋的 PDF，隨時可供索引使用。全程不需要額外工具或手動 OCR 步驟——只要乾淨的程式碼加上一點說明即可。

## 前置條件與所需項目

- **.NET 6+**（或 .NET Framework 4.6+）。API 兩者皆支援，但 .NET 6 提供最新的執行時改進。  
- **Visual Studio 2022** 或任何你慣用的 IDE。  
- **Aspose.OCR** 與 **Aspose.OCR.Gpu** NuGet 套件（GPU 套件為可選，能在支援的硬體上加速辨識）。  
- 一個範例 TIFF 檔（例如 `invoice.tif`），放在你可控制的資料夾內。  

如果你已經具備上述項目，直接跳到下一步。若尚未安裝，以下的安裝步驟會一次搞定。

## 第一步：安裝 Aspose OCR 套件

首先，在終端機中切換到專案資料夾，執行：

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

上述指令會同時下載核心 OCR 引擎與 GPU 加速函式庫。GPU 套件並非必須；若找不到相容的 GPU，引擎會自動回退至 CPU 模式。  

> **小技巧：** 在正式環境中，請在 `csproj` 中鎖定套件版本，以避免意外的破壞性變更。

## 第二步：建立專案骨架

建立一個新的 console 應用程式（如果尚未有的話）：

```bash
dotnet new console -n PdfExportDemo
cd PdfExportDemo
```

將自動產生的 `Program.cs` 替換成稍後完整示範的程式碼。此程式將會：

1. 使用 GPU 支援初始化 `OcrEngine`。  
2. 載入 TIFF 圖像。  
3. 執行 OCR，若失敗則優雅地中止。  
4. 設定 **PdfExportOptions** 以產生可搜尋圖層並啟用 **high compression**。  
5. 寫入輸出檔案。

## 第三步：撰寫完整程式碼（完整範例）

以下為 **全部** 原始檔案內容。請直接複製貼上至 `Program.cs`。註解說明了每一行「為什麼」而不只是「做什麼」。

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;

class PdfExport
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1️⃣ Initialise OCR engine with GPU acceleration.
        //    GpuMode.Enabled tells Aspose to use the GPU if one is present.
        //    If no compatible GPU exists, the engine automatically falls back
        //    to CPU mode—no extra code required.
        // ------------------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine(GpuMode.Enabled))
        {
            // ------------------------------------------------------------
            // 2️⃣ Load the source image.
            //    ImageStream.FromFile supports many formats; here we use TIFF.
            // ------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\invoice.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // ------------------------------------------------------------
            // 3️⃣ Perform OCR recognition.
            //    Recognize() returns false if the engine cannot read the image.
            //    Exiting early prevents us from creating an empty PDF.
            // ------------------------------------------------------------
            if (!ocrEngine.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return;
            }

            // ------------------------------------------------------------
            // 4️⃣ Configure PDF export options.
            //    IncludeTextLayer = true adds an invisible, searchable text layer.
            //    CompressionLevel = High reduces file size dramatically.
            // ------------------------------------------------------------
            PdfExportOptions pdfExportOptions = new PdfExportOptions
            {
                IncludeTextLayer = true,
                CompressionLevel = PdfCompression.High
            };

            // ------------------------------------------------------------
            // 5️⃣ Save the searchable PDF.
            //    The output will be a compact, searchable PDF ready for indexing.
            // ------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\invoice.pdf";
            ocrEngine.Save(outputPath, pdfExportOptions);
            Console.WriteLine($"Searchable PDF saved to: {outputPath}");
        }
    }
}
```

### 為什麼這樣寫會有效

- **GPU 加速** 能將辨識時間從秒級縮短至毫秒級，對大量處理非常有幫助。  
- **IncludeTextLayer** 會把 OCR 產生的文字隱藏嵌入 PDF，讓 PDF 閱讀器能搜尋文件內容，同時不改變圖像的外觀。  
- **High compression** 會對圖像串流使用 Flate（ZIP）壓縮，屬於無損壓縮卻能大幅縮小檔案大小——非常適合大量發票的歸檔。

## 第四步：執行應用程式並驗證輸出

在專案資料夾內的終端機執行：

```bash
dotnet run
```

若一切設定正確，畫面會顯示：

```
Searchable PDF saved to: YOUR_DIRECTORY\invoice.pdf
```

使用任何 PDF 閱讀器（Adobe Acrobat、Edge，或瀏覽器）開啟 `invoice.pdf`。搜尋原始 TIFF 中確定會出現的關鍵字，例如 “Total”。即使文字是圖像的一部份，閱讀器仍會高亮顯示，這正是 **searchable pdf** 的特徵。

### 預期檔案大小

一張約 300 KB 的掃描發票，經過 `PdfCompression.High` 後通常會縮減至 **約 80 KB**。實際大小會受圖像複雜度影響，但明顯的縮減是可以預期的。

## 第五步：常見變化與例外情況

| 情境 | 需要調整的地方 | 原因 |
|-----------|----------------|-----|
| **沒有 GPU 可用** | 將 `new OcrEngine(GpuMode.Enabled)` 改為 `new OcrEngine(GpuMode.Disabled)` | 防止引擎嘗試初始化 GPU，避免短暫延遲。 |
| **多頁（multi‑page TIFF）** | 設定 `ocrEngine.Image = ImageStream.FromFile("multi.tif", PageRange.All);` | 載入所有頁框；Aspose 會逐頁處理並產生多頁 PDF。 |
| **需要非英文的 OCR 語言** | `ocrEngine.Language = Language.French;`（或任何支援的語言） | 提升非英文文件的辨識準確度。 |
| **想要可見的文字覆蓋層而非隱藏層** | `pdfExportOptions.IncludeTextLayer = false;` 並手動加入 `TextFragment` 物件。 | 當你希望 OCR 文字以可選取的形式顯示在圖像上方時使用。 |
| **極小的 PDF** | 結合 `PdfCompression.High` 與在辨識前設定 `ImageResolution = 150` DPI。 | 降低 DPI 減少圖像資料，進一步縮小 PDF 大小，但會犧牲畫質。 |

> **注意：** 在大規模部署前，請先在小樣本上測試各種例外情況。OCR 的準確度會受圖像品質、雜訊與語言等因素影響。

## 第六步：製作上線環境的最佳實踐

1. **錯誤記錄** – 用正式的日誌框架（Serilog、NLog）取代 `Console.WriteLine`，方便除錯。  
2. **批次處理** – 把核心邏輯封裝成接受輸入/輸出路徑的方法，然後遍歷資料夾內的 TIFF 檔。  
3. **非同步 I/O** – 雖然 Aspose OCR 本身是同步的，但檔案的讀寫可以使用 async，以免阻塞 UI 執行緒。  
4. **安全性** – 若透過 Web API 暴露此功能，務必驗證檔案路徑並限制檔案大小，以防濫用。  
5. **版本鎖定** – 使用確切的版本號（`<PackageReference Include="Aspose.OCR" Version="23.12.0" />`）確保不同建置間行為一致。

## 結論

我們剛剛完成了一個 **完整、端對端的解決方案**，能 **create searchable pdf**、**convert tiff to pdf**，同時使用 **high compression pdf** 設定，並且 **recognize image text** 準確無誤。最終產出的 **searchable pdf from image** 輕量、可搜尋，適合後續的索引、歸檔或 e‑discovery 工作流程。

有一堆發票要處理？把這個方法放進迴圈，指向資料夾，讓 Aspose OCR 完全接管。想嘗試不同的壓縮等級或語言套件？程式碼模組化設計，幾秒鐘內即可切換。

---

*想更上一層樓嗎？* 嘗試加入浮水印、嵌入中繼資料，或甚至把多個 OCR 處理過的 PDF 合併。Aspose 系列提供豐富的擴充功能——探索文件、持續前進。祝開發順利！

![Create searchable PDF from image example screenshot](https://example.com/images/create-searchable-pdf.png "create searchable pdf example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}