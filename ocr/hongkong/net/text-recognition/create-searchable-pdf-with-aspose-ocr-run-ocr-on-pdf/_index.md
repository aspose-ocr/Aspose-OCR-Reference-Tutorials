---
category: general
date: 2026-05-28
description: 使用 Aspose OCR 於 C# 建立可搜尋的 PDF。了解如何對 PDF 執行 OCR、辨識文字 PDF，並將 OCR 掃描的 PDF
  轉換為可搜尋的 PDF。
draft: false
keywords:
- create searchable pdf
- run ocr on pdf
- recognize text pdf
- ocr scanned pdf
- aspose ocr pdf
language: zh-hant
og_description: 使用 Aspose OCR 於 C# 建立可搜尋 PDF。請依照此一步步指南執行 PDF OCR、辨識文字 PDF，並處理 OCR
  掃描的 PDF 檔案。
og_title: 使用 Aspose OCR 建立可搜尋的 PDF – 對 PDF 進行 OCR
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  headline: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  type: TechArticle
- description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  name: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  steps:
  - name: Multiple Languages (OCR Scanned PDF)
    text: 'If your source PDF contains both English and Spanish text, combine languages:'
  - name: Password‑Protected PDFs
    text: 'When dealing with secured PDFs, supply the password before calling `Recognize`:'
  - name: Controlling Image Quality
    text: 'Higher DPI yields better OCR results but consumes more memory. Adjust the
      DPI if you notice garbled characters:'
  - name: License vs. Evaluation Mode
    text: 'In evaluation mode a watermark appears on each page. To remove it, apply
      your license before any OCR call:'
  - name: What’s Next?
    text: '- Explore the **aspose ocr pdf** API further: extract plain text, export
      to DOCX, or generate searchable PDFs in bulk. - Combine the searchable PDF output
      with Aspose.PDF to add bookmarks or watermarks. - Experiment with different
      DPI settings or custom OCR dictionaries for niche fonts.'
  type: HowTo
tags:
- Aspose
- OCR
- PDF
- C#
title: 使用 Aspose OCR 建立可搜尋 PDF – 在 PDF 上執行 OCR
url: /zh-hant/net/text-recognition/create-searchable-pdf-with-aspose-ocr-run-ocr-on-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 建立可搜尋的 PDF – 在 PDF 上執行 OCR

有沒有曾經需要從一堆掃描文件**建立可搜尋的 PDF**檔案？你並不孤單。在許多辦公流程中，阻礙你擁有完整可搜尋檔案的唯一障礙，只是一小段在 PDF 頁面上執行 OCR 的程式碼。  

在本教學中，我們將逐步示範一個完整、可直接執行的範例，說明如何使用 Aspose OCR for .NET 函式庫**建立可搜尋的 PDF**檔案。完成後，你將會知道如何*在 PDF 上執行 OCR*、*辨識文字 PDF*檔案，並將*OCR 掃描的 PDF*轉換成可搜尋的版本，且不需要任何第三方服務。

> **先決條件** – 最近的 .NET SDK（建議 6.0 以上）、有效的 Aspose.OCR for .NET 授權（或臨時評估金鑰），以及一份你想處理的 PDF。

![建立可搜尋 PDF 圖示](alt="說明使用 Aspose OCR 建立可搜尋 PDF 工作流程的圖示")  

---

## 本指南涵蓋內容

- 在 C# 專案中設定 Aspose OCR 函式庫。  
- 載入來源 PDF（任意頁數）。  
- 設定引擎輸出為**可搜尋的 PDF**。  
- 執行 OCR 程序並儲存結果。  
- 處理多頁文件、語言選擇與常見陷阱的技巧。  

只要依照每一步操作，你最終會得到一個可以在 Adobe Reader 中開啟、按下 **Ctrl + F**，即時搜尋原始掃描檔中任何出現過的字詞的檔案。

---

## 步驟 1：安裝 Aspose OCR for .NET

在撰寫任何程式碼之前，先將 NuGet 套件加入你的專案：

```bash
dotnet add package Aspose.OCR
```

> **專業提示：** 使用 `--version` 參數鎖定最新的穩定版（例如 `Aspose.OCR 23.10`），可確保相容於 .NET 6 及更新版本。

---

## 步驟 2：建立 OCR Engine 實例

此程序的核心是 `OcrEngine`。它就像是讀取影像並輸出文字的大腦。初始化非常簡單：

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Instantiate the OCR engine
            var ocrEngine = new OcrEngine();
```

`OcrEngine` 物件會同時保存輸入的影像串流以及告訴 Aspose 你想要的輸出設定。

---

## 步驟 3：載入來源 PDF（在 PDF 上執行 OCR）

Aspose OCR 能直接讀取 PDF；它會在內部將每一頁轉為影像。將佔位路徑替換成你的掃描文件所在位置：

```csharp
            // Step 3: Load the source PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);
```

> **為什麼這樣可行：** `ImageStream.FromFile` 方法會自動偵測 PDF 格式，並為 OCR 準備光柵化的表示。無需額外的轉換步驟。

---

## 步驟 4：設定輸出格式與語言

在這裡告訴 Aspose 我們想要的結果。將 `OutputFormat` 設為 `SearchablePdf`，引擎會在原始頁面影像後嵌入辨識出的文字，產生**可搜尋的 PDF**。你也可以選擇語言以提升準確度——預設為英文，亦可切換成法文、德文等。

```csharp
            // Step 4: Choose output format and language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf; // creates searchable PDF
            ocrEngine.Configuration.Language = Language.English;               // *recognize text PDF* in English
```

如果需要處理雙語文件，可使用 `Language` 列舉的旗標結合多種語言。

---

## 步驟 5：執行 OCR 程序 – 辨識文字 PDF

現在開始進行重量級工作。`Recognize` 方法會掃描每一頁、提取字形，並建立內部的 PDF 串流，該串流同時包含原始影像與隱形文字層。這一步即是*辨識文字 PDF*。

```csharp
            // Step 5: Execute OCR – this *recognizes text PDF* and builds the searchable stream
            ocrEngine.Recognize();
```

> **常見問題：** *如果 PDF 有 200 頁怎麼辦？*  
> 引擎會依序處理頁面並串流結果，因此記憶體使用量保持在可接受範圍。若檔案極大，建議調高 `ocrEngine.Configuration` 中的 `MemoryLimit` 設定。

---

## 步驟 6：儲存可搜尋的 PDF

最後，將結果寫入磁碟。`Save` 方法會把內部串流寫成新檔，你可以使用任何 PDF 檢視器開啟。

```csharp
            // Step 6: Save the searchable PDF to disk
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

執行程式（`dotnet run`），並在主控台看到檔案建立的確認訊息。開啟 `handbook_searchable.pdf`，試著搜尋原始掃描中確定存在的字詞——應該會立即顯示匹配結果。

---

## 處理例外情況與進階情境

### 多語言（OCR 掃描的 PDF）

如果來源 PDF 同時包含英文與西班牙文，請結合語言：

```csharp
ocrEngine.Configuration.Language = Language.English | Language.Spanish;
```

Aspose OCR 會即時切換字典，提升混合語言文件的辨識精度。

### 密碼保護的 PDF

處理受保護的 PDF 時，請在呼叫 `Recognize` 前提供密碼：

```csharp
ocrEngine.Image = ImageStream.FromFile(inputPath, "MySecretPassword");
```

若密碼錯誤，`Recognize` 會拋出 `InvalidPasswordException`；捕捉此例外即可提示使用者重新輸入正確密碼。

### 控制影像品質

較高的 DPI 能產生更佳的 OCR 結果，但會佔用更多記憶體。若發現字元雜亂，可調整 DPI：

```csharp
ocrEngine.Configuration.Dpi = 300; // default is 200
```

### 授權與評估模式

在評估模式下，每頁會出現浮水印。若要移除浮水印，請在任何 OCR 呼叫之前先套用授權：

```csharp
var license = new License();
license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");
```

---

## 生產環境的專業提示

- **批次處理：** 將核心邏輯包在 `foreach` 迴圈中，遍歷 PDF 清單。每處理完一個檔案後，記得釋放 `OcrEngine` 以釋放原生資源。  
- **日誌記錄：** 使用 `ocrEngine.Configuration.Logger` 捕捉詳細的 OCR 統計資訊（例如每秒辨識的字元數），對於排除低準確度問題相當有幫助。  
- **效能調校：** 在多核心伺服器上，可為每個執行緒建立獨立的 `OcrEngine` 實例；只要每個實例彼此隔離，函式庫即為執行緒安全。  
- **錯誤處理：** 請務必在 `Recognize` 與 `Save` 周圍使用 `try/catch`。常見例外包括 `FileNotFoundException`、`OutOfMemoryException` 與 `UnsupportedFormatException`。

---

## 完整可執行範例（直接複製貼上）

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Apply license (optional – removes evaluation watermark)
            // var license = new License();
            // license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");

            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Load PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Configure output as searchable PDF and set language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
            ocrEngine.Configuration.Language = Language.English;

            // 4️⃣ Run OCR – *recognize text PDF*
            ocrEngine.Recognize();

            // 5️⃣ Save the searchable PDF
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**預期輸出**（主控台）：

```
Searchable PDF created at: C:\Docs\handbook_searchable.pdf
```

執行後開啟產生的檔案，按下 **Ctrl + F**，即可快速定位原始掃描頁面中出現的任何字詞。這就是將*OCR 掃描的 PDF*轉換成**可搜尋的 PDF**的魔法。

---

## 結論

我們剛剛示範了如何使用 Aspose OCR for .NET **建立可搜尋的 PDF**，涵蓋了從安裝套件到處理多語言與密碼保護 PDF 的完整流程。依照這些步驟，你可以可靠地*在 PDF 上執行 OCR*、*辨識文字 PDF*，並將任何*OCR 掃描的 PDF*轉換為完整可搜尋的資產。

### 接下來該做什麼？

- 深入探索 **aspose ocr pdf** API：提取純文字、匯出為 DOCX，或批次產生可搜尋的 PDF。  
- 結合 Aspose.PDF，為可搜尋的 PDF 加入書籤或浮水印。  
- 嘗試不同的 DPI 設定或自訂 OCR 字典，以因應特殊字型需求。

歡迎自行調整範例、整合至文件管理流程，或在留言區提出問題。祝開發順利，讓那些無法閱讀的掃描檔變成可搜尋的金礦！

## 相關教學

- [如何在 .NET 使用 Aspose.OCR 進行 PDF OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [如何在 .NET 使用 Aspose.OCR 進行 PDF OCR（西班牙語）](/ocr/spanish/net/text-recognition/recognize-pdf/)
- [如何在 .NET 使用 Aspose.OCR 進行 PDF OCR（阿拉伯語）](/ocr/arabic/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}