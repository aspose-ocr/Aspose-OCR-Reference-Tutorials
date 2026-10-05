---
category: general
date: 2026-02-22
description: 使用 Aspose OCR 產生可搜尋的 PDF 並從圖像中擷取文字。了解如何在單一教學中將圖像轉換為 PDF 並輸出純文字。
draft: false
keywords:
- generate searchable pdf
- extract text from image
- convert image to pdf
- output plain text
- convert scanned image pdf
language: zh-hant
og_description: 使用 Aspose OCR 從掃描圖像生成可搜尋的 PDF。本指南說明如何從圖像擷取文字、輸出純文字，以及將圖像轉換為 PDF。
og_title: 從圖像產生可搜尋的 PDF – 完整 C# 教學
tags:
- C#
- OCR
- PDF generation
- Aspose
title: 在 C# 中從圖像生成可搜尋 PDF – 步驟指南
url: /zh-hant/net/text-recognition/generate-searchable-pdf-from-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從影像產生可搜尋 PDF（C#） – 完整教學

是否曾需要從掃描圖片**產生可搜尋 PDF**，卻不知從何下手？你並不孤單——大多數開發者在首次接觸 OCR 時都會卡住。好消息是？使用 Aspose OCR，你只需幾行 C# 程式碼即可**從影像擷取文字**、**輸出純文字**，以及**將影像轉換為 PDF**。

在本教學中，我們將完整示範從載入 PNG 檔案到儲存可搜尋 PDF 以及純文字檔的整個流程。完成後，你將擁有一段可直接放入任何 .NET 專案的可重用程式碼。沒有多餘的說明，只有真正能完成工作的內容。

## 你將學會

- 如何在 .NET 主控台應用程式中設定 **Aspose.OCR**。  
- **輸出純文字** 與 **可搜尋 PDF** 兩種模式的差異。  
- 如何**從影像擷取文字**並寫入 `.txt` 檔案。  
- 如何**將影像轉換為 PDF**，在保留原始點陣圖的同時加入隱藏文字層。  
- 處理大量批次、常見陷阱，以及在何處微調設定以提升辨識準確度的技巧。

> **先決條件** – 需要 .NET 6+（或 .NET Framework 4.7+）、Visual Studio 2022（或任意編輯器），以及 Aspose OCR 授權（或免費試用版）。不需要其他第三方函式庫。

![generate searchable pdf example](image-placeholder.png "Example of a generated searchable PDF")

## 步驟 1：安裝 Aspose OCR 並建立引擎

首先，將 NuGet 套件加入專案：

```bash
dotnet add package Aspose.OCR
```

接著即可啟動 OCR 引擎，並告訴它要辨識的語言。預設為英文，你也可以改成法文、西班牙文等，只要更改 `Language` 列舉即可。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine for English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };
```

**為什麼這很重要：** 引擎會保存所有設定——語言、輸出格式以及可選的前處理旗標。只設定一次並重複使用，可避免每次處理檔案時重新建立實例的額外開銷。

## 步驟 2：擷取文字並儲存為純文字

如果只需要原始字元，將引擎切換為 `OutputFormat.Text`。這會指示 Aspose OCR 完全跳過 PDF 產生，直接回傳字串。

```csharp
        // Tell the engine to return plain text
        ocrEngine.OutputFormat = OutputFormat.Text;

        // Path to your source image (PNG, JPEG, BMP, etc.)
        string inputImagePath = @"YOUR_DIRECTORY/input.png";

        // Perform recognition – the result contains the extracted string
        OcrResult plainTextResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Write the text to a .txt file
        string textOutputPath = @"YOUR_DIRECTORY/output.txt";
        File.WriteAllText(textOutputPath, plainTextResult.Text);
```

**小技巧：** `plainTextResult.Text` 已自動去除屬於 OCR 版面的換行。如果需要保留原始間距，可改為檢查 `plainTextResult.TextBlocks`。

### 預期結果

開啟 `output.txt`，應該會看到類似以下內容：

```
Hello, world!
This is a sample scanned document.
```

這就是本教學的**輸出純文字**部分——快速、輕量，且非常適合後續處理（例如建立索引）。

## 步驟 3：切換為可搜尋 PDF 模式

現在來建立**可搜尋 PDF**。引擎會把原始點陣圖嵌入，同時在底層加入 OCR 產生的文字層，使文件在任何 PDF 檢視器中皆可搜尋。

```csharp
        // Change the output format to searchable PDF
        ocrEngine.OutputFormat = OutputFormat.SearchablePdf;

        // Recognize the same image again – this time we get PDF bytes
        OcrResult pdfResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Save the PDF bytes to a file
        string pdfOutputPath = @"YOUR_DIRECTORY/output.pdf";
        File.WriteAllBytes(pdfOutputPath, pdfResult.RawData);
    }
}
```

**為什麼要重新辨識：** OCR 引擎會快取最後一次的影像，但輸出格式決定它回傳的資料類型。切換格式會強制重新執行一次辨識，以產生隱藏文字層。

### PDF 內容長什麼樣

在 Adobe Reader 或任意檢視器中開啟 `output.pdf`，嘗試選取文字。你會發現即使畫面仍是原始點陣圖，仍能複製、搜尋與標記文字。這正是**將掃描影像轉換為 PDF**的特徵。

## 步驟 4：處理多個檔案（可選）

實務上很少只處理單一影像。以下示範一個快速迴圈，會處理資料夾內所有 PNG，產生對應的 `.txt` 與 `.pdf` 檔案。

```csharp
        string folder = @"YOUR_DIRECTORY";
        foreach (var file in Directory.GetFiles(folder, "*.png"))
        {
            // Plain‑text extraction
            ocrEngine.OutputFormat = OutputFormat.Text;
            var txtResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllText(Path.ChangeExtension(file, ".txt"), txtResult.Text);

            // Searchable PDF generation
            ocrEngine.OutputFormat = OutputFormat.SearchablePdf;
            var pdfResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllBytes(Path.ChangeExtension(file, ".pdf"), pdfResult.RawData);
        }
```

**邊緣案例說明：** 大尺寸影像可能耗盡記憶體。若遭遇 `OutOfMemoryException`，可在辨識前使用 `Image.Resize` 降低解析度，或將檔案分批處理。

## 步驟 5：微調 OCR 準確度

Aspose OCR 提供了幾個可調整的參數：

| 設定 | 功能說明 | 使用時機 |
|------|----------|----------|
| `ocrEngine.PageSegmentationMode` | 控制引擎如何將影像切割成文字區塊。 | 多欄位版面時特別有用。 |
| `ocrEngine.Deskew` | 自動校正略為傾斜的頁面。 | 掃描文件未完全對齊時。 |
| `ocrEngine.RemoveNoise` | 嘗試清除雜訊與背景雜點。 | 低品質掃描或傳真頁面。 |

範例：

```csharp
ocrEngine.Deskew = true;
ocrEngine.RemoveNoise = true;
```

啟用這些選項可能會延長處理時間，但在**從影像擷取文字**品質上的提升通常值得。

## 步驟 6：以程式方式驗證輸出

有時需要在自動化測試中斷言 PDF 確實包含可搜尋文字。最簡單的檢查方式是確認 PDF 位元組陣列非空，且 `RawData` 長度大於影像檔大小。

```csharp
if (pdfResult.RawData.Length > Image.Load(inputImagePath).Data.Length)
{
    Console.WriteLine("Searchable PDF generated successfully!");
}
else
{
    Console.WriteLine("Warning: PDF may not contain hidden text.");
}
```

若需更深入的驗證，可使用 PDF 函式庫（如 iTextSharp）抽取文字串流，並與 `plainTextResult.Text` 進行比對。

## 常見陷阱與避免方式

- **授權遺失** – 若未提供有效的 Aspose 授權，函式庫會以評估模式執行，並在 PDF 上加上浮水印。請盡早註冊授權 (`License license = new License(); license.SetLicense("Aspose.OCR.lic");`)。  
- **路徑錯誤** – 硬寫絕對路徑只能在你的機器上運作，搬移後會失效。建議使用 `Path.Combine` 搭配 `AppDomain.CurrentDomain.BaseDirectory` 以提升可移植性。  
- **不支援的影像格式** – GIF 與多頁 TIFF 需要特別處理 (`Image.LoadMultiPage`)。若只需要第一頁，可先轉為 PNG/JPEG。  
- **效能瓶頸** – 在迴圈內重建 `OcrEngine` 代價高昂。請保留單一實例，僅在需要時切換 `OutputFormat`。

## 重點回顧

我們已完整說明如何使用 Aspose OCR 從掃描影像**產生可搜尋 PDF**：

1. 安裝 NuGet 套件並建立 `OcrEngine`。  
2. 設定 `OutputFormat.Text` 以**輸出純文字**，寫入 `.txt` 檔。  
3. 切換至 `OutputFormat.SearchablePdf` 以**將影像轉換為 PDF**，並加入隱藏文字層。  
4. 儲存 PDF 位元組，必要時以迴圈處理整個目錄以完成批次作業。  
5. 透過去斜、去雜訊與版面分割等選項微調辨識準確度。  

以上程式碼可直接複製貼上至 Visual Studio，形成一個自包含的範例。

## 接下來可以嘗試什麼？

- **批次處理** 搭配 UI 前端（WinForms 或 WPF），讓使用者可以拖放檔案。  
- **語言偵測** – Aspose OCR 能自動偵測語言，試試 `ocrEngine.Language = Language.AutoDetect`。  
- **後處理** – 將擷取的文字送入搜尋索引（ElasticSearch、Azure Cognitive Search），即時取得文件。  
- **其他輸出格式** – 使用 `OutputFormat.Hocr` 取得 HTML 版 OCR 結果，適合網頁預覽。

盡情嘗試不同的影像解析度、色彩模式與 OCR 設定。玩得越多，你就越能掌握速度與準確度之間的取捨。

---

**開心寫程式！** 若遇到任何問題，歡迎在下方留言或查閱 Aspose OCR 文件以獲得更深入的說明。你的下一個專案——無論是發票、檔案歸檔，或是建置可搜尋的知識庫——都將變得更簡單。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}