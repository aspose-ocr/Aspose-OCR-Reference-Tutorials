---
category: general
date: 2026-02-11
description: 在 C# 中將 OCR 圖像轉換為 JSON。學習如何從圖像提取文字、在 C# 讀取圖像檔案、格式化 JSON 輸出，以及使用 Aspose.OCR
  以 C# 進行美化列印 JSON。
draft: false
keywords:
- ocr image to json
- extract text from image
- read image file c#
- format json output
- pretty print json c#
language: zh-hant
og_description: 將 OCR 圖像轉換為 JSON（C#）。本指南說明如何從圖像中擷取文字、在 C# 讀取圖像檔案、格式化 JSON 輸出，以及使用
  Aspose.OCR 於 C# 進行 JSON 美化列印。
og_title: C# 中的 OCR 圖像轉 JSON – 完整逐步指南
tags:
- OCR
- C#
- JSON
title: 在 C# 中將 OCR 圖像轉換為 JSON – 完整逐步指南
url: /zh-hant/net/text-recognition/ocr-image-to-json-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# 中的 OCR 圖像轉 JSON – 完整逐步指南

是否曾經需要 **ocr image to json**，卻不確定該選擇哪個函式庫或如何取得格式良好的結果？你並不孤單。在許多實務應用中——收據掃描、身分驗證或簡單的文件歸檔——你會想從圖像中擷取文字，並得到一個乾淨的 JSON 負載，供下游服務使用。

在本教學中，我們將完整走過整個流程：從 C# 讀取圖像檔案、使用 Aspose.OCR 擷取文字、要求引擎輸出結構化的 JSON，最後將 JSON 以易讀的方式 pretty‑print。完成後，你將擁有一段自包含、可直接投入生產環境的程式碼，能夠在任何 .NET 專案中使用。

我們也會提及常見的陷阱（例如缺少語言套件），並示範幾種快速變化方式——例如切換為 XML 輸出或處理多頁 PDF。無需參考外部文件，所有資訊都在此處。

## 需要的條件

- **.NET 6+**（此程式碼亦可於 .NET Framework 4.7+ 執行）
- **Aspose.OCR for .NET** – 透過 NuGet 安裝 (`Install-Package Aspose.OCR`)
- 範例圖像（例如 `receipt.png`），放置於可參考的位置
- 具備基本的 C# 語法概念（只要寫過「Hello World」就足夠）

> *Pro tip:* 若你在 CI 伺服器上執行，請將 `AutomaticResourceDownload = true` 設為 true，讓 Aspose 能即時下載語言資料——不必手動處理 DLL。

## Step 1: Read image file C# and create the OCR engine  

首先，我們從磁碟載入圖像。使用 `System.Drawing.Image` 可讓程式碼保持簡潔，且支援 PNG、JPEG、BMP，甚至多頁 TIFF（引擎預設只取第一頁）。

```csharp
using System.Drawing;          // For Image
using Aspose.OCR;              // Core OCR classes
using Aspose.OCR.Models;       // Language and output enums
using System.Text.Json;        // JSON parsing & pretty‑print

// 1️⃣ Configure the OCR engine – this is where we tell Aspose what language we expect
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // extract text from image in English
    AutomaticResourceDownload = true,        // auto‑download language packs if missing
    OutputFormat = OcrOutputFormat.Json      // ask for JSON rather than plain text
};
```

**為什麼這很重要：**  
- `AutomaticResourceDownload` 可防止在本機缺少英文語言檔時發生執行時錯誤。  
- 將 `OutputFormat` 設為 `Json` 代表引擎已自行將原始 OCR 結果轉換為結構化物件，無需自行解析字串。

## Step 2: Run OCR and obtain JSON output  

接著把已載入的 bitmap 送入引擎。`Recognize` 方法會回傳一個 `OcrResult`，其 `Text` 屬性即為 JSON 字串。

```csharp
// 2️⃣ Load the image you want to process
using (var receiptImage = Image.FromFile(@"C:\Images\receipt.png"))
{
    // 3️⃣ Perform OCR – this call blocks until the engine finishes
    var ocrResult = ocrEngine.Recognize(receiptImage);

    // 4️⃣ The OCR engine gave us JSON straight away
    string rawJson = ocrResult.Text;
    
    // Optional: write the raw JSON to a file for debugging
    System.IO.File.WriteAllText(@"C:\Temp\ocr_raw.json", rawJson);
}
```

**邊緣情況：** 若圖像檔損毀或路徑錯誤，`Image.FromFile` 會拋出 `FileNotFoundException`。若輸入可能不穩定，請將程式碼包在 `try/catch` 中。

## Step 3: Parse and format the JSON – pretty print JSON C#  

OCR 引擎產生的原始 JSON 壓縮且難以閱讀。使用 `System.Text.Json` 我們可以將其反序列化為 `JsonDocument`，再以縮排方式重新序列化。

```csharp
// 5️⃣ Parse the JSON string into a DOM-like structure
using var jsonDoc = JsonDocument.Parse(rawJson);

// 6️⃣ Pretty‑print with indentation (2 spaces by default)
string prettyJson = JsonSerializer.Serialize(
    jsonDoc.RootElement,
    new JsonSerializerOptions { WriteIndented = true });

// 7️⃣ Output to console – you could also send this to an API or a file
Console.WriteLine(prettyJson);

// 8️⃣ Save the pretty JSON for later use
System.IO.File.WriteAllText(@"C:\Temp\ocr_pretty.json", prettyJson);
```

**你會看到的結果：**  

```json
{
  "Lines": [
    {
      "Text": "Store Name",
      "BoundingBox": { "X": 12, "Y": 5, "Width": 150, "Height": 20 }
    },
    {
      "Text": "Total: $23.45",
      "BoundingBox": { "X": 12, "Y": 200, "Width": 100, "Height": 20 }
    }
  ],
  "Language": "English",
  "Confidence": 0.96
}
```

此 JSON 現在包含逐行文字、邊界框、偵測語言與信心分數——非常適合供下游分析或 UI 元件使用。

## Step 4: Bonus – Switching output format or language  

如果你需要將 **format json output** 轉為 XML，或想辨識西班牙語收據，只要調整引擎設定即可：

```csharp
ocrEngine.Language = OcrLanguage.Spanish;          // extract text from image in Spanish
ocrEngine.OutputFormat = OcrOutputFormat.Xml;     // ask for XML instead of JSON
```

其餘程式碼保持不變；只需要改變反序列化步驟（XML 可使用 `XmlDocument`）。

## Full Working Example  

以下是一個可直接貼到 Console App 的完整單檔範例：

```csharp
// ---------------------------------------------------------------
// ocr_image_to_json_demo.cs
// ---------------------------------------------------------------
using System;
using System.Drawing;
using System.Text.Json;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Configure OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            AutomaticResourceDownload = true,
            OutputFormat = OcrOutputFormat.Json
        };

        // Path to your image – adjust as needed
        string imagePath = @"C:\Images\receipt.png";

        try
        {
            using (var receiptImage = Image.FromFile(imagePath))
            {
                var ocrResult = ocrEngine.Recognize(receiptImage);
                string rawJson = ocrResult.Text;

                // Parse & pretty‑print
                using var jsonDoc = JsonDocument.Parse(rawJson);
                string prettyJson = JsonSerializer.Serialize(
                    jsonDoc.RootElement,
                    new JsonSerializerOptions { WriteIndented = true });

                Console.WriteLine("=== Pretty‑Printed OCR JSON ===");
                Console.WriteLine(prettyJson);

                // Optional: write to file
                System.IO.File.WriteAllText(@"C:\Temp\ocr_pretty.json", prettyJson);
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Error processing image: {ex.Message}");
        }
    }
}
```

執行此程式會在主控台印出排版好的 JSON，並儲存至 `C:\Temp\ocr_pretty.json`。`try/catch` 區塊確保即使圖像無法讀取，也會顯示清晰的錯誤訊息，而不會靜默崩潰。

## Common Questions & Gotchas  

- **如果 OCR 回傳空文字該怎麼辦？**  
  通常表示圖像過於雜訊或語言不匹配。可嘗試提升圖像對比度或將 `Language` 改為 `AutoDetect`。  

- **可以在迴圈中處理多張圖像嗎？**  
  當然可以。將 `using (var img = Image.FromFile(...))` 包在 `foreach (var file in Directory.GetFiles(...))` 迴圈中，將每個 `prettyJson` 收集到清單或寫入不同檔案即可。  

- **JSON 結構是否穩定？**  
  Aspose 保證 `Json` 輸出格式的向後相容性，但若針對特定 API 版本開發，仍建議檢查回應中的 `Version` 屬性。  

- **使用 Aspose.OCR 是否需要授權？**  
  免費評估金鑰可支援至多 100 頁。正式上線時請購買授權，並以 `License license = new License(); license.SetLicense("Aspose.OCR.lic");` 設定授權檔。

## Conclusion  

現在你已掌握 **complete, self‑contained solution to ocr image to json** 的完整流程。只要讀取圖像檔、設定 OCR 引擎、要求 JSON 輸出並進行 pretty‑print，即可在任何 .NET 服務中輕鬆整合文字擷取功能，無需自行撰寫字串處理程式。

未來你可以探索 **extract text from image** 的其他檔案類型（PDF、多頁 TIFF），嘗試不同語言，或將 JSON 匯入 NoSQL 資料庫進行分析。只要妥善處理錯誤、留意授權問題，即可讓 OCR 流程穩定擴展。

祝開發順利，願你的 OCR 管線永遠精準！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}