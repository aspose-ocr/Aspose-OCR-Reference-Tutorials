---
category: general
date: 2026-06-16
description: 在 C# 中的批次 OCR 處理可讓您快速將圖像轉換為文字。了解如何使用 Aspose.OCR 透過一步步的程式碼從圖像中擷取文字。
draft: false
keywords:
- batch OCR processing
- extract text from images
- convert images to text
language: zh-hant
og_description: 在 C# 中的批次 OCR 處理將圖像轉換為文字。按照本指南使用 Aspose.OCR 從圖像中提取文字。
og_title: C# 批次 OCR 處理 – 從圖像提取文字
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Batch OCR processing in C# lets you convert images to text quickly.
    Learn how to extract text from images using Aspose.OCR with step‑by‑step code.
  headline: Batch OCR Processing in C# – Complete Guide to Extract Text from Images
  type: TechArticle
- description: Batch OCR processing in C# lets you convert images to text quickly.
    Learn how to extract text from images using Aspose.OCR with step‑by‑step code.
  name: Batch OCR Processing in C# – Complete Guide to Extract Text from Images
  steps:
  - name: Expected Output
    text: 'Assuming you have three images (`invoice1.png`, `receipt2.jpg`, `form3.tif`)
      in the input folder, the output folder will contain:'
  - name: What if some images fail to process?
    text: '`OcrBatchProcessor` logs errors to the console by default and continues
      with the next file. For production use, you can subscribe to the `OnError` event
      to collect failed filenames and retry later.'
  - name: Can I process PDFs directly?
    text: Yes. Aspose.OCR treats each page of a PDF as an image internally. Just point
      `InputFolder` to a directory containing PDFs, and the processor will extract
      text from every page—effectively **convert images to text** even when the source
      is a PDF.
  - name: How do I handle multi‑language documents?
    text: Set `Language` to `OcrLanguage.Multilingual` or specify a list of languages
      if the library version supports it. The engine will attempt to recognize characters
      from all provided languages, which is handy for international invoices.
  - name: What about memory consumption?
    text: The batch processor streams each image, so memory usage stays low even with
      thousands of files. However, enabling a high `MaxDegreeOfParallelism` on a memory‑constrained
      machine could cause spikes. Monitor your RAM and adjust the thread count accordingly.
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: C# 批次 OCR 處理 – 完整指南：從圖像提取文字
url: /zh-hant/net/text-recognition/batch-ocr-processing-in-c-complete-guide-to-extract-text-fro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# 批次 OCR 處理 – 完整指南：從圖片中擷取文字

有沒有想過如何在 C# 中 **批次 OCR 處理**，而不必為每張圖片寫一個迴圈？你並不是唯一有此疑問的人。當你面對數十甚至數百張掃描收據、發票或手寫筆記時，手動將每個檔案送入 OCR 引擎很快就會變成噩夢。

好消息是？使用 Aspose.OCR，你可以一次性、整齊地 *將圖片轉換為文字*。在本教學中，我們將從安裝函式庫到執行可投入生產的批次工作，完整說明 **從圖片中擷取文字** 並將結果儲存為你需要的格式。

> **你將得到：** 一個可直接執行的主控台應用程式，能處理整個資料夾，將純文字（或 JSON、XML、HTML、PDF）檔案與原始檔案並排寫入，並示範如何調整平行度以獲得最高吞吐量。

## 前置條件

- .NET 6.0 SDK 或更新版本（程式碼同時支援 .NET Core 與 .NET Framework）
- Visual Studio 2022、VS Code，或任何你慣用的 C# 編輯器
- Aspose.OCR NuGet 授權（免費試用版即可評估）
- 一個包含欲 **將圖片轉換為文字** 的影像檔案資料夾（`.png`、`.jpg`、`.tif` 等）

如果上述條件皆已符合，讓我們開始吧。

![說明批次 OCR 處理流程的圖示](batch-ocr-workflow.png "批次 OCR 處理流程")

## 步驟 1：透過 NuGet 安裝 Aspose.OCR

首先，將 Aspose.OCR 套件加入專案。於專案目錄開啟終端機並執行：

```bash
dotnet add package Aspose.OCR
```

或是在 Visual Studio 內，右鍵點選 *Dependencies → Manage NuGet Packages*，搜尋 **Aspose.OCR**，然後點擊 *Install*。這一行指令會把 **批次 OCR 處理** 所需的所有元件都拉下來。

> **小技巧：** 請保持套件版本為最新；截至 2026 年 6 月的最新發行版已支援更多影像格式，且提升了多語言辨識的準確度。

## 步驟 2：建立 Console 骨架

建立一個新的 C# 主控台應用程式（如果尚未建立），然後將產生的 `Program.cs` 替換為以下骨架。請注意最上方的 `using Aspose.OCR;` 指令，這是提供 `OcrBatchProcessor` 類別的命名空間。

```csharp
using Aspose.OCR;
using System;

class BatchDemo
{
    static void Main()
    {
        // We'll fill this in later.
    }
}
```

此時檔案僅是個佔位符，但它為我們的 **批次 OCR 處理** 邏輯提供了乾淨的起點。

## 步驟 3：初始化 OcrBatchProcessor

`OcrBatchProcessor` 是負責掃描資料夾、對每張支援的影像執行 OCR，並寫入輸出的核心。建立它非常簡單：

```csharp
// Step 3: Create an OCR batch processor instance
var ocrBatchProcessor = new OcrBatchProcessor();
```

為什麼要使用批次處理器而非單張影像 API？批次類別會自動處理檔案列舉、錯誤記錄，甚至平行執行，讓你省下寫迴圈的時間，將更多精力放在調校辨識準確度上。

## 步驟 4：指定輸入與輸出資料夾

告訴處理器從哪裡讀取影像、以及將結果寫入哪裡。將佔位路徑替換為你機器上的實際目錄。

```csharp
// Step 4: Configure the input folder containing images to process
ocrBatchProcessor.InputFolder = @"C:\MyProjects\OCRDemo\Images\Batch";

// Step 5: Set the folder where OCR results will be saved
ocrBatchProcessor.OutputFolder = @"C:\MyProjects\OCRDemo\Results\Batch";
```

兩個資料夾必須在執行應用程式前先建立，否則會拋出 `DirectoryNotFoundException`。雖然可以在程式內動態建立，但為了說明清晰，我們保持範例簡潔。

## 步驟 5：選擇輸出格式

Aspose.OCR 能輸出純文字、JSON、XML、HTML，甚至 PDF。對於大多數 **從圖片中擷取文字** 的情境，純文字已足夠；當然，你也可以自行切換。

```csharp
// Step 6: Choose the desired output format (e.g., plain text)
ocrBatchProcessor.OutputFormat = ResultFormat.Text;   // alternatives: Json, Xml, Html, Pdf, etc.
```

如果後續流程需要結構化資料，`ResultFormat.Json` 是不錯的選擇。函式庫會自動將每頁文字包裝成 JSON 物件，並保留版面資訊。

## 步驟 6：設定語言與平行度

OCR 的準確度取決於正確的語言模型。英語適用於大多數西方文件，但你也可以選擇任何支援的語言（阿拉伯語、中文等）。此外，你可以指定要啟動多少執行緒——預設上限為四。

```csharp
// Step 7: Specify the language for OCR recognition
ocrBatchProcessor.Language = OcrLanguage.English;

// Step 8: Define the level of parallelism (up to 4 concurrent threads)
ocrBatchProcessor.MaxDegreeOfParallelism = 4;
```

**為什麼平行度重要：** 若你的 CPU 為四核心，將 `MaxDegreeOfParallelism` 設為 `4` 可將處理時間縮短約 75 %。在雙核心筆記型電腦上，`2` 會較安全。請自行實驗，找出最適合你硬體的設定。

## 步驟 7：執行批次工作

現在正式上工。只要一行程式碼即可啟動整個管線，處理輸入資料夾中的所有影像，並將結果寫入輸出資料夾。

```csharp
// Step 9: Execute the batch processing of all supported image files
ocrBatchProcessor.Execute();

Console.WriteLine("Batch OCR completed.");
```

當主控台顯示 *Batch OCR completed.* 時，你會在每個原始影像旁看到相對應的 `.txt`（或你選擇的格式）檔案。檔名與來源相同，讓對應 OCR 輸出與原始圖片變得非常簡單。

## 完整範例

以下是可直接貼到 `Program.cs` 並立即執行的完整程式碼：

```csharp
using Aspose.OCR;
using System;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create an OCR batch processor instance
        var ocrBatchProcessor = new OcrBatchProcessor();

        // Step 2: Configure the input folder containing images to process
        ocrBatchProcessor.InputFolder = @"C:\MyProjects\OCRDemo\Images\Batch";

        // Step 3: Set the folder where OCR results will be saved
        ocrBatchProcessor.OutputFolder = @"C:\MyProjects\OCRDemo\Results\Batch";

        // Step 4: Choose the desired output format (plain text is default)
        ocrBatchProcessor.OutputFormat = ResultFormat.Text; // alternatives: Json, Xml, Html, Pdf, etc.

        // Step 5: Specify the language for OCR recognition
        ocrBatchProcessor.Language = OcrLanguage.English;

        // Step 6: Define the level of parallelism (up to 4 concurrent threads)
        ocrBatchProcessor.MaxDegreeOfParallelism = 4;

        // Step 7: Execute the batch processing of all supported image files
        ocrBatchProcessor.Execute();

        Console.WriteLine("Batch OCR completed.");
    }
}
```

### 預期輸出

假設輸入資料夾內有三張影像（`invoice1.png`、`receipt2.jpg`、`form3.tif`），則輸出資料夾會包含：

```
invoice1.txt
receipt2.txt
form3.txt
```

每個 `.txt` 檔案都存放對應影像所擷取的原始字元。使用 Notepad 開啟任一檔案，即可看到原始掃描的純文字內容。

## 常見問題與邊緣案例

### 若有部分影像處理失敗該怎麼辦？

`OcrBatchProcessor` 會預設將錯誤寫到主控台，並繼續處理下一個檔案。若要在正式環境收集失敗的檔名並稍後重試，可訂閱 `OnError` 事件。

```csharp
ocrBatchProcessor.OnError += (sender, args) =>
{
    Console.WriteLine($"Failed on {args.FileName}: {args.Exception.Message}");
};
```

### 能直接處理 PDF 嗎？

可以。Aspose.OCR 會將 PDF 的每一頁視為影像來處理。只要把 `InputFolder` 指向包含 PDF 的資料夾，處理器就會從每一頁抽取文字——即使來源是 PDF，也能 **將圖片轉換為文字**。

### 如何處理多語言文件？

將 `Language` 設為 `OcrLanguage.Multilingual`，或在函式庫支援的情況下指定語言清單。引擎會嘗試辨識所有提供的語言，對於國際發票特別有用。

### 記憶體使用情況如何？

批次處理器會以串流方式讀取每張影像，即使處理上千檔案，記憶體使用仍保持在低水平。但在記憶體受限的機器上啟用過高的 `MaxDegreeOfParallelism` 可能會造成記憶體峰值。請監控 RAM 使用情形，並依需求調整執行緒數。

## 提升準確度的技巧

- **前置處理影像**：在 OCR 前先除噪、去斜、轉為灰階。Aspose.OCR 提供 `ImagePreprocessOptions` 可附加至 `ocrBatchProcessor`。
- **選擇適當格式**：若需保留版面，`ResultFormat.Html` 或 `Pdf` 會保留換行與基本樣式。
- **驗證結果**：實作簡易的後處理步驟，檢查是否有空的輸出檔案——空檔通常代表辨識失敗。

## 後續步驟

現在你已掌握 **批次 OCR 處理** 以及 **從圖片中擷取文字** 的技巧，接下來可以考慮：

- **整合資料庫** – 將每筆 OCR 結果與中繼資料一起存入，以便搜尋。
- **加入 UI** – 建立小型 WPF 或 WinForms 前端，讓使用者拖放資料夾。
- **擴展規模** – 在 Azure Functions 或 AWS Lambda 上執行批次工作，實現雲端原生處理。

上述主題皆以本教學的核心概念為基礎，你已做好擴充解決方案的準備。

---

**祝開發順利！** 若在實作過程中遇到問題或有改進想法，歡迎在下方留言討論。讓我們一起持續優化 OCR 自動化流程。

## 接下來該學什麼？

以下教學與本指南的技術緊密相關，提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，或在專案中探索其他實作方式。

- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}