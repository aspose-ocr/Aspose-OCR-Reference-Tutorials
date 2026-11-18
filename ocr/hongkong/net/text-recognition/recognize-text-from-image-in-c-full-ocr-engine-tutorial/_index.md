---
category: general
date: 2026-06-06
description: 使用 C# OCR 引擎辨識圖像文字。學習在幾分鐘內將圖像轉換為 JSON、轉換為 XML，並載入圖像進行 OCR。
draft: false
keywords:
- recognize text from image
- convert image to json
- convert image to xml
- ocr engine c#
- load image for ocr
language: zh-hant
og_description: 使用 C# OCR 引擎辨識圖像文字。將結果匯出為 JSON 與 XML，並精通載入圖像進行 OCR。
og_title: 在 C# 中從圖像辨識文字 – 完整 OCR 引擎教學
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Recognize text from image using C# OCR engine. Learn to convert image
    to JSON, convert image to XML, and load image for OCR in minutes.
  headline: Recognize Text from Image in C# – Full OCR Engine Tutorial
  type: TechArticle
tags:
- OCR
- C#
- Image Processing
title: 在 C# 中從圖片辨識文字 – 完整 OCR 引擎教學
url: /zh-hant/net/text-recognition/recognize-text-from-image-in-c-full-ocr-engine-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中從圖像辨識文字 – 完整 OCR 引擎教學

是否曾需要**從圖像辨識文字**，卻不確定該選哪個 C# 函式庫？你並非唯一面臨此問題的開發者——大家常常要把掃描的收據、螢幕截圖或手寫筆記轉換成可搜尋的文字。好消息是？使用現代的**OCR engine C#**，只需幾行程式碼即可完成，之後還能**將圖像轉換為 JSON**或**將圖像轉換為 XML**以供後續處理。

在本指南中，我們會一步步說明：安裝 OCR 套件、載入圖像以進行 OCR、擷取文字，最後將結果匯出為 JSON 與 XML。完成後，你將擁有一個可自行放入任何 .NET 專案的完整主控台應用程式。沒有模糊的參考，只有完整、可執行的解決方案。

## 您將學會的內容

- 清楚了解如何使用流行的 C# OCR 引擎**載入圖像以進行 OCR**。  
- 可執行的程式碼，能**從圖像辨識文字**並回傳豐富的結果物件。  
- 簡單的片段，能**將圖像轉換為 JSON**與**將圖像轉換為 XML**，且不需額外函式庫。  
- 處理多頁 PDF、不同圖像格式，以及低對比掃描等常見陷阱的技巧。

### 前置條件

- .NET 6 SDK 或更新版本（如果你願意，也可以目標 .NET Framework 4.8）。  
- 基本的 C# 知識——不需要高階，只要了解類別與 `async`/`await` 即可。  
- 一個你想要 OCR 的圖像檔（範例中的 `structured.png`）。  

如果你已具備上述條件，讓我們開始吧。

---

## 從圖像辨識文字 – 設定 OCR 引擎

首先，我們需要一個可靠的 OCR 函式庫。本教學將使用 **IronOcr**，這是一款商業級引擎，在 NuGet 上提供免費的社群版。它開箱即支援英文，並提供我們在原始程式碼中看到的 `OcrEngine` 類別。

```bash
dotnet add package IronOcr --version 2024.3.0
```

> **專業提示：** 若預算較緊，亦可改用 `Tesseract` 取代 `IronOcr`——API 稍有不同，但概念完全相同。

現在建立一個新的主控台專案，並加入必要的 `using` 陳述式：

```csharp
using IronOcr;
using System.IO;
```

### 步驟式引擎設定

```csharp
// Step 1: Create and configure the OCR engine
var ocrEngine = new IronTesseract();           // IronOcr’s engine class
ocrEngine.Language = OcrLanguage.English;     // Load English language data
```

*為什麼這很重要：* 只初始化一次引擎並在多張圖像間重複使用，可減少額外開銷。同時，明確設定語言可避免引擎自動偵測的程序，後者往往較慢且精確度較低。

---

## 載入圖像以進行 OCR – 為引擎提供正確資料

引擎期待一個 `OcrInput` 物件。你可以指向檔案路徑、串流，甚至是 `Bitmap`。以下是最簡單的做法：

```csharp
// Step 2: Load the image to be processed
var input = new OcrInput(@"YOUR_DIRECTORY\structured.png");

// Optional: improve accuracy on low‑contrast images
input.Deskew();          // Straighten tilted pages
input.Contrast(10);      // Boost contrast by 10%
```

> **邊緣案例：** 若來源是多頁 PDF，請改用 `input.AddPdf("file.pdf")` 取代 PNG。OCR 引擎會自動將每一頁視為獨立圖像處理。

## 從圖像辨識文字 – 執行 OCR 程序

引擎與輸入準備好後，實際的辨識只需要一行程式碼：

```csharp
// Step 3: Recognize text in the image
using var result = ocrEngine.Read(input);
```

`result` 是一個 `OcrResult` 物件，包含：

- `Text` – 原始擷取的字串。  
- `Lines` – 包含信心分數的 `OcrLine` 物件集合。  
- `Words` – 各個單字的集合，同樣帶有信心分數。  

你可以直接在除錯器中檢視它，但大多數情況下你會想要將資料序列化。

## 將圖像轉換為 JSON – 匯出 OCR 結果

IronOcr 內建透過 `System.Text.Json` 的 JSON 序列化功能。以下程式碼會在原始圖像旁寫入一個整齊的 JSON 檔案：

```csharp
// Step 4: Export the recognition result to JSON and save it
string jsonResult = System.Text.Json.JsonSerializer.Serialize(result, new System.Text.Json.JsonSerializerOptions
{
    WriteIndented = true
});
File.WriteAllText(@"YOUR_DIRECTORY\result.json", jsonResult);
```

**你會看到的結果：** 一個格式良好的 JSON 文件，內含原始文字、信心分數以及每行與每字的邊界框。此結構非常適合送入下游服務，如 ElasticSearch 或 Azure Cognitive Search。

## 將圖像轉換為 XML – 結構化資料輸出

某些舊有系統仍然需要 XML。IronOcr 的 `ToXml()` 方法可快速完成轉換：

```csharp
// Step 5: Export the recognition result to XML and save it
string xmlResult = result.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY\result.xml", xmlResult);
```

XML 會鏡像 JSON 的層級結構，使用 `<Line>` 與 `<Word>` 元素並帶有 `Confidence` 屬性。若需要自訂 schema，你可以手動將 `result` 投射成 `XDocument`——API 完全支援 LINQ。

## 完整端對端範例程式碼

將所有步驟整合起來，以下是一個可直接執行的 `Program.cs`：

```csharp
using IronOcr;
using System;
using System.IO;
using System.Text.Json;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure the OCR engine
        var ocrEngine = new IronTesseract();
        ocrEngine.Language = OcrLanguage.English;

        // 2️⃣ Load the image (adjust the path to your file)
        var input = new OcrInput(@"YOUR_DIRECTORY\structured.png");
        input.Deskew();
        input.Contrast(10);

        // 3️⃣ Perform recognition
        using var result = ocrEngine.Read(input);
        Console.WriteLine("✅ OCR completed. Extracted text:");
        Console.WriteLine(result.Text);

        // 4️⃣ Convert image to JSON
        string json = JsonSerializer.Serialize(result, new JsonSerializerOptions { WriteIndented = true });
        string jsonPath = @"YOUR_DIRECTORY\result.json";
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"📄 JSON saved to {jsonPath}");

        // 5️⃣ Convert image to XML
        string xml = result.ToXml();
        string xmlPath = @"YOUR_DIRECTORY\result.xml";
        File.WriteAllText(xmlPath, xml);
        Console.WriteLine($"📄 XML saved to {xmlPath}");
    }
}
```

**預期輸出**（為簡潔起見已截斷）：

```
✅ OCR completed. Extracted text:
Invoice #12345
Date: 2024‑04‑01
Total: $1,234.56
...
📄 JSON saved to YOUR_DIRECTORY\result.json
📄 XML saved to YOUR_DIRECTORY\result.xml
```

使用 `dotnet run` 執行程式。若一切配置正確，你會在主控台看到輸出，且在 `YOUR_DIRECTORY` 中出現兩個檔案。

## 常見問題與陷阱

| 問題 | 解答 |
|----------|--------|
| *如果圖像是帶有 EXIF 旋轉資訊的 JPEG 會怎樣？* | 在 `Deskew()` 之前先呼叫 `input.AutoRotate()`。IronOcr 會讀取 EXIF 標籤並校正方向。 |
| *我可以一次處理整個資料夾的圖像嗎？* | 當然可以。將上述邏輯包在 `foreach (var file in Directory.GetFiles(folder, "*.png"))` 迴圈中即可。 |
| *如何提升噪點掃描的辨識準確度？* | 增加 `input.Denoise()`，並考慮使用 `input.BlackWhiteThreshold(120)`。同時，提供與文件語言相符的語言包。 |
| *JSON 格式能否與其他 OCR 函式庫相容？* | 此 schema 足夠通用——`Text`、`Lines`、`Words`——因此可輕鬆映射至 Tesseract 的輸出，僅需最小的轉換工作。 |

## 效能技巧（專業級）

- **重複使用引擎**：在緊密迴圈中不斷實例化 `IronTesseract` 會使吞吐量下降最多 30 %。請在應用程式域中保留單例。  
- **平行化 I/O**：若同時處理數十張圖像，可同時將它們讀入記憶體 (`Task.WhenAll`) 並將每個 `OcrInput` 交給同一個引擎——IronOcr 為執行緒安全。  
- **批次匯出**：不要逐一寫入 JSON/XML 檔案，而是先將結果彙整至單一集合，再一次序列化，這樣可減少磁碟寫入次數。

## 往後步驟與相關主題

既然你已能**從圖像辨識文字**，可以考慮擴充整個流程：

- **搜尋整合** – 將 JSON 推送至 Elasticsearch 以進行全文搜尋。  
- **文件分類** – 將 OCR 輸出餵入輕量級機器學習模型，自動為發票、合約或收據加上標籤。  
- **手寫文字** – 改用 `OcrLanguage.EnglishHandwritten` 語言包（需 IronOcr 付費版）以辨識手寫內容。  

上述每項都建立在你剛完成的基礎上，足以讓你忙上好幾週。

## 結論

我們剛剛說明了如何使用現代的 **OCR engine C#** 來**從圖像辨識文字**，接著**將圖像轉換為 JSON**與**將圖像轉換為 XML**，最後如何**載入圖像以進行 OCR**，且整個流程具備高度的穩定性。完整範例在不到一分鐘內即可執行，且匯出的檔案已可直接供任何下游系統使用。

試著執行程式碼，並依需求進行微調。

## 接下來該學什麼？

以下教學與本指南所示技巧緊密相關，並提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索其他實作方式。

- [如何使用 Aspose OCR 取得圖像辨識的 JSON 結果](/ocr/english/net/text-recognition/get-result-as-json/)
- [使用 Aspose.OCR 以語言選擇擷取圖像文字（C#）](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [將圖像轉換為文字 – 從 URL 執行 OCR](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}