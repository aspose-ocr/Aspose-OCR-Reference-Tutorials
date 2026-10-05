---
category: general
date: 2026-10-05
description: 「Image to PDF OCR」教學示範如何載入影像進行 OCR、套用前處理步驟，並使用 Aspose OCR C# 範例擷取西里爾文字影像。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- image to pdf OCR
- load image for OCR
- ocr image preprocessing steps
- aspose OCR C# example
- extract Cyrillic text image
language: zh-hant
lastmod: 2026-10-05
og_description: 《圖像轉 PDF OCR 指南》將帶領您完成載入圖像進行 OCR、應用前處理步驟，以及使用 Aspose OCR C# 範例提取西里爾文字圖像。
og_image_alt: Developer view of OCR converting an image to PDF with Aspose OCR in
  C#
og_title: 使用 Aspose OCR 在 C# 中將圖片轉換為 PDF 並進行 OCR – 完整範例
schemas:
- author: Aspose
  dateModified: '2026-10-05'
  description: Image to PDF OCR tutorial shows how to load image for OCR, apply preprocessing
    steps, and extract Cyrillic text image using an Aspose OCR C# example.
  headline: 'Image to PDF OCR with Aspose OCR in C#: step‑by‑step guide'
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- PDF
- Image processing
title: 在 C# 中使用 Aspose OCR 將圖像轉為 PDF OCR：逐步指南
url: /zh-hant/net/ocr-optimization/image-to-pdf-ocr-with-aspose-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 於 C# 進行影像轉 PDF OCR：逐步指南

如果您需要在 .NET 應用程式中執行 **image to PDF OCR**，本指南將逐步說明如何載入影像進行 OCR、進行前處理，並將辨識出的文字匯出為可搜尋的 PDF。您將看到完整的 *Aspose OCR C# 範例*，從影像中擷取西里爾文字並將結果儲存為 PDF 檔案。

將掃描文件轉換為可搜尋的 PDF 是檔案保存、合規或資料擷取流程中的常見需求。完成本教學後，您將擁有一個可直接執行的專案，完整執行從影像載入到 PDF 產生的 OCR 工作流程，並正確處理西里爾字元。

## 您將學會

- 如何在 C# 專案中安裝並參考 **Aspose.OCR** 函式庫。  
- 使用 Aspose 的 `Image.Load` 方法正確 **load image for OCR**。  
- 關鍵的 **OCR image preprocessing steps**（旋轉與去斜）以提升辨識準確度。  
- 如何設定引擎以 **extract Cyrillic text image** 並輸出可搜尋的 PDF。  
- 針對常見問題（例如缺少語言模組）提供除錯技巧。

### 前置條件

| 需求 | 原因 |
|------|------|
| .NET 6.0 SDK 或更新版本 | 提供範例中使用的 C# 10 功能所需的執行環境。 |
| Visual Studio 2022（或任何支援 .NET 的 IDE） | 讓專案建立與除錯更為簡便。 |
| 網際網路連線（首次執行時） | 讓 OCR 引擎能自動下載西里爾語言模組。 |
| 包含西里爾文字的範例影像（例如 `sample_cyrillic.jpg`） | 示範 *extract Cyrillic text image* 情境。 |

> **Pro tip:** 如果您在企業代理伺服器後工作，請在首次執行前設定 `Resources.AutoDownload` 屬性以使用您的代理設定。

## 步驟 1：安裝 Aspose.OCR NuGet 套件

在解決方案資料夾中開啟終端機並執行：

```bash
dotnet add package Aspose.OCR
```

此套件包含 `Aspose.Ocr` 命名空間、OCR 引擎，以及多語言辨識所需的語言資源。

## 步驟 2：載入影像進行 OCR

第一個功能步驟是將來源檔案讀入 `Aspose.Ocr.Image` 物件。使用完整路徑可確保引擎不論目前工作目錄為何，都能正確找到檔案。

```csharp
// Load the source image that contains Cyrillic text
var inputImage = Aspose.Ocr.Image.Load(@"C:\OCR\sample_cyrillic.jpg");
```

> **Why this matters:** 早期載入影像可取得其像素資料，這是前處理階段所必需的。`Image.Load` 方法同時會驗證檔案格式，若影像不受支援會拋出明確的例外。

## 步驟 3：設定 OCR 引擎以擷取西里爾文字

Aspose OCR 支援多種語言，但必須明確設定預期的語言。對於西里爾文字，請使用 `Language.Cyrillic` 列舉值。啟用 `Resources.AutoDownload` 可確保首次執行程式碼時自動下載所需的語言模組。

```csharp
using (var ocrEngine = new Aspose.Ocr.OcrEngine())
{
    // Select Cyrillic language to correctly recognize Russian, Ukrainian, etc.
    ocrEngine.Language = Aspose.Ocr.Language.Cyrillic;

    // Automatically download missing language modules (required on first run)
    ocrEngine.Resources.AutoDownload = true;
```

> **Why this matters:** 若未設定語言，引擎會預設為英語，這會大幅降低西里爾字元的辨識精度。

## 步驟 4：套用 OCR 影像前處理步驟

前處理透過校正常見影像問題提升 OCR 品質。範例使用以下兩個最有效的選項：

- **Rotate** – 若頁面以角度掃描，則將其校正為水平。  
- **Deskew** – 移除輕微斜度，避免影響字元分割。

```csharp
    // Preprocess the image: rotate to correct orientation and deskew to flatten text lines
    ocrEngine.PreprocessImage(
        inputImage,
        Aspose.Ocr.PreprocessOptions.Rotate |
        Aspose.Ocr.PreprocessOptions.Deskew);
```

> **How it works:** `PreprocessImage` 會建立供 OCR 引擎使用的內部位圖。位元 OR 可結合多個選項，讓您無需額外程式碼即可串接多個步驟。

## 步驟 5：辨識文字並轉換為 PDF（image to PDF OCR）

現在影像已完成前處理且語言已設定，呼叫 `Recognize`。此方法會回傳 `OcrResult` 物件，您可直接將其儲存為 PDF。產生的 PDF 內含隱藏文字層，因而可搜尋。

```csharp
    // Perform OCR and ask for PDF output format
    var ocrResult = ocrEngine.Recognize(inputImage, Aspose.Ocr.OutputFormat.Pdf);
```

> **Result:** PDF 包含原始點陣圖影像以及與辨識出的西里爾字元相符的文字覆蓋層。搜尋引擎可索引此文字，使用者亦可複製貼上。

## 步驟 6：儲存可搜尋的 PDF

最後，將 PDF 寫入磁碟。請選擇應用程式具有寫入權限的路徑。

```csharp
    // Save the searchable PDF to the desired location
    ocrResult.Save(@"C:\OCR\result.pdf");
}
```

### 預期輸出

當您在任何 PDF 檢視器中開啟 `result.pdf` 時，會看到原始影像，且能選取辨識出的西里爾文字。快速搜尋來源影像中出現的詞彙，即可在 PDF 中突顯相應位置。

![OCR conversion result](/images/ocr-conversion.png){alt="顯示使用 Aspose OCR 於 C# 將影像轉換為 PDF 的 OCR 轉換截圖"}

## 完整可執行範例

以下為完整程式碼，您可將其複製到主控台應用程式中。它包含所有必要的 `using` 指示詞以及適用於正式環境的錯誤處理。

```csharp
// ------------------------------------------------------------
// Image to PDF OCR – Aspose OCR C# example
// ------------------------------------------------------------
using System;
using Aspose.Ocr;

namespace ImageToPdfOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the image that contains Cyrillic text
            const string inputPath = @"C:\OCR\sample_cyrillic.jpg";
            // Destination PDF file
            const string outputPath = @"C:\OCR\result.pdf";

            try
            {
                // Step 1: Load the image for OCR
                var inputImage = Image.Load(inputPath);

                // Step 2: Create and configure the OCR engine
                using (var ocrEngine = new OcrEngine())
                {
                    // Choose Cyrillic language
                    ocrEngine.Language = Language.Cyrillic;
                    // Enable automatic download of language resources
                    ocrEngine.Resources.AutoDownload = true;

                    // Step 3: Apply preprocessing (rotate + deskew)
                    ocrEngine.PreprocessImage(
                        inputImage,
                        PreprocessOptions.Rotate |
                        PreprocessOptions.Deskew);

                    // Step 4: Recognize and export as PDF (image to PDF OCR)
                    var ocrResult = ocrEngine.Recognize(
                        inputImage,
                        OutputFormat.Pdf);

                    // Step 5: Save the searchable PDF
                    ocrResult.Save(outputPath);
                }

                Console.WriteLine($"✅ OCR completed. PDF saved to: {outputPath}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ An error occurred: {ex.Message}");
                // In a real application, consider logging the stack trace.
            }
        }
    }
}
```

執行程式 (`dotnet run`) 並確認 `result.pdf` 已出現在 `C:\OCR`。主控台會顯示成功完成的訊息。

## 常見問題與避免方法

| 現象 | 原因 | 解決方案 |
|------|------|----------|
| **PDF 中無西里爾字元** | 未將語言設定為西里爾語。 | 確保 `ocrEngine.Language = Language.Cyrillic;`。 |
| **PDF 檔案為空** | `Resources.AutoDownload` 已停用且缺少語言模組。 | 保留 `ocrEngine.Resources.AutoDownload = true;`，或自行從 Aspose 官方網站下載西里爾語模組。 |
| **旋轉掃描的辨識效果差** | 未執行前處理步驟。 | 加入 `PreprocessOptions.Rotate`（必要時亦加入 `Deskew`）。 |
| **載入影像時發生 `FileNotFoundException`** | 影像路徑不正確或檔案遺失。 | 使用絕對路徑，或在載入前確認檔案是否存在。 |
| **大型影像導致記憶體不足** | 未縮放即載入超高解析度影像。 | 在 OCR 前縮小影像（`Image.Resize`），或提升程式的記憶體上限。 |

## 擴充範例

- **Multiple languages:** 設定 `ocrEngine.Language = Language.Cyrillic | Language.English;` 以辨識混合文字。  
- **Different output formats:** 將 `OutputFormat.Pdf` 替換為 `OutputFormat.Txt` 或 `OutputFormat.Docx`，以取得純文字或 Word 輸出。  
- **Batch processing:** 將 OCR 邏輯包裝在 `foreach` 迴圈中， 

## 接下來您應該學習什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [使用 Aspose.OCR 於 C# 提取影像文字並選擇語言](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [如何在 C# 中執行 OCR – 使用 Aspose OCR 從影像提取文字](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image-using-aspose/)
- [如何使用 Aspose.OCR for .NET 從影像提取文字](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}