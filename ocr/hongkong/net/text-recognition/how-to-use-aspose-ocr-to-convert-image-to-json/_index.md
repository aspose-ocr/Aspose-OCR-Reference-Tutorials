---
category: general
date: 2026-03-15
description: 如何在 C# 中使用 Aspose OCR 從圖像提取文字並將圖像轉換為 JSON。學習從 PNG 識別文字，快速獲得結構化輸出。
draft: false
keywords:
- how to use aspose
- convert image to json
- extract text from image
- recognize text from png
- how to extract ocr
language: zh-hant
og_description: 如何使用 Aspose OCR 從圖像中提取文字，並在 C# 中將圖像轉換為 JSON。本指南將帶領您從 PNG 識別文字並獲取結構化輸出。
og_title: 如何使用 Aspose OCR 將圖片轉換為 JSON
tags:
- Aspose
- OCR
- C#
- JSON
title: 如何使用 Aspose OCR 將圖片轉換為 JSON
url: /zh-hant/net/text-recognition/how-to-use-aspose-ocr-to-convert-image-to-json/
---

Example (Copy‑Paste Ready)

Translate heading: "## 完整範例（可直接複製貼上）"

Code block unchanged.

But there is incomplete code at end: after "throw new InvalidOperationException("OCR". It seems truncated. Keep as is.

After that we have closing shortcodes.

We must ensure we keep all shortcodes and code block placeholders.

Now produce final content with translations.

Let's assemble.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose OCR 將圖像轉換為 JSON

當開發人員需要從圖片中提取文字時，如何使用 Aspose OCR 是一個常見問題。如果您想 **將圖像轉換為 JSON** 或 **從 PNG 識別文字**，本指南將為您提供完整解決方案——不囉嗦，只提供實用的端到端步驟。

接下來的幾分鐘，我們將逐步說明您需要的全部內容：安裝程式庫、設定引擎的 JSON 輸出、載入收據 PNG、執行 OCR，最後將結果寫入 `.json` 檔案。完成後，您只需一次方法呼叫即可 **從圖像中提取文字**，並且了解每一步的重要性。

> **小技巧：** Aspose OCR 支援多種圖像格式（PNG、JPEG、BMP、TIFF）。以下相同程式碼即可處理所有格式，您無需撰寫針對特定格式的程式。

## 您需要的條件

- .NET 6.0 或更新版本（此程式碼亦可於 .NET Framework 4.6+ 執行）  
- 有效的 Aspose.OCR NuGet 套件（免費試用或已授權）  
- 您想要處理的圖像檔案（例如 `receipt.png`）  
- Visual Studio、VS Code，或您偏好的任何 C# 編輯器  

就這樣——無需額外相依套件，亦不需要外部服務。準備好了嗎？讓我們開始吧。

![how to use aspose OCR engine](image-placeholder.png "how to use aspose OCR engine")

## 如何使用 Aspose OCR – 設定 JSON 輸出

當您 **使用 Aspose** 進行 OCR 時，首先要做的事是建立 `OcrEngine` 實例，並告訴它輸出 JSON。這個小小的設定切換可讓您免於之後手動序列化結果。

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that does the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell Aspose to give us JSON instead of plain text.
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Load the image you want to recognize.
        var inputImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");

        // 4️⃣ Run the OCR process.
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Save the JSON payload to disk.
        File.WriteAllText(@"YOUR_DIRECTORY/receipt.json", ocrResult.Text);

        // 6️⃣ Let the developer know we’re done.
        Console.WriteLine("JSON saved.");
    }
}
```

**為什麼這很重要：** 將 `OutputFormat` 設為 `Json` 表示 OCR 引擎已將文字結構化為頁面、行與字的層級。您不必在之後解析原始字串，這讓後續處理（例如將資料寫入資料庫）更加簡潔。

## 使用 Aspose OCR 將圖像轉換為 JSON

現在引擎已完成設定，讓我們更詳細說明 **將圖像轉換為 JSON** 的部分。

1. **載入圖像** – `Image.FromFile` 可用於任何支援的格式。如果您處理的是串流（例如上傳的檔案），可以改用 `Image.FromStream`。  
2. **執行 `Recognize`** – 此方法會回傳 `OcrResult` 物件。因為我們已將輸出設定為 JSON，`ocrResult.Text` 已包含 JSON 字串。  
3. **寫入檔案** – `File.WriteAllText` 是持久化 JSON 最簡單的方式。如果需要將其存入雲端儲存桶，只需將此行換成相應的 SDK 呼叫即可。

### 預期的 JSON 輸出

典型的 JSON 資料如下（為簡潔起見已截斷）：

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Words": [
            { "Text": "Total", "Confidence": 0.99 },
            { "Text": "$12.34", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

現在您可以將此結構輸入任何下游系統——無論是報表工具、機器學習模型，或是簡單的日誌檔案。

## 使用 Aspose OCR 從圖像提取文字

如果您只需要原始字串（即不需要 JSON），只要將輸出格式切換回純文字即可：

```csharp
ocrEngine.Configuration.OutputFormat = OutputFormat.PlainText;
var plainResult = ocrEngine.Recognize(inputImage);
Console.WriteLine(plainResult.Text);
```

**何時選擇純文字？**  
- 快速除錯或在主控台輸出。  
- 需要自行進行後處理的情境（例如正規表達式抽取）。

但請記住，使用 JSON **從圖像中提取文字** 會提供位置資料——這對於在 UI 中高亮文字或與表單欄位對齊非常有用。

## 從 PNG 檔案識別文字

PNG 為無損格式，通常比高度壓縮的 JPEG 能提供更佳的 OCR 準確度。以下是一份快速檢查清單，確保您在 **從 PNG 識別文字** 時取得最佳效果：

| 檢查項目 | 原因說明 |
|----------------|--------------|
| 使用 300 DPI 以上 | 較高解析度提供更多像素供引擎使用。 |
| 保持圖像為灰階 | 降低噪點；Aspose OCR 會自動轉換，但前置處理可加速。 |
| 移除背景雜訊 | 乾淨的背景可提升信心分數。 |

若遇到信心分數偏低，可嘗試提升 DPI 或在送入 Aspose 前套用簡單的閾值過濾。

## 程式化提取 OCR 結果

除了儲存 JSON 之外，您可能還想以程式方式讀取特定欄位——例如收據上的總金額。由於 JSON 包含層級結構，您可以將其反序列化為 C# 物件：

```csharp
using System.Text.Json;

// Assuming ocrResult.Text contains the JSON string
var ocrData = JsonSerializer.Deserialize<OcrResponse>(ocrResult.Text);

// Example class definitions (simplified)
public class OcrResponse
{
    public Page[] Pages { get; set; }
}
public class Page
{
    public int PageNumber { get; set; }
    public Line[] Lines { get; set; }
}
public class Line
{
    public Word[] Words { get; set; }
}
public class Word
{
    public string Text { get; set; }
    public double Confidence { get; set; }
}
```

現在您可以使用 LINQ 查詢 `ocrData`：

```csharp
var totalLine = ocrData.Pages
    .SelectMany(p => p.Lines)
    .FirstOrDefault(l => l.Words.Any(w => w.Text.Equals("Total", StringComparison.OrdinalIgnoreCase)));

if (totalLine != null)
{
    var amount = totalLine.Words
        .FirstOrDefault(w => w.Text.StartsWith("$"))
        ?.Text;
    Console.WriteLine($"Extracted amount: {amount}");
}
```

**為什麼這有效：** JSON 已經告訴您每個字在頁面上的位置，即使版面稍有變動，也能可靠地定位欄位。

## 邊緣案例與常見陷阱

- **空結果：** 如果 `ocrEngine.Recognize` 回傳 `null`，可能是圖像不支援或已損毀。務必做好防護：

  ```csharp
  var ocrResult = ocrEngine.Recognize(inputImage);
  if (ocrResult == null) throw new InvalidOperationException("OCR failed – check the image path.");
  ```

- **大型檔案：** 對於多 MB 的圖像，請考慮以串流方式讀取或在 OCR 前調整大小，以避免過度佔用記憶體。

- **授權問題：** 試用版會在輸出中加入浮水印。請確保在程式開始時載入授權：

  ```csharp
  Aspose.OCR.License license = new Aspose.OCR.License();
  license.SetLicense("Aspose.OCR.lic");
  ```

- **非拉丁文字：** Aspose OCR 支援多種語言，但必須相應設定 `Language` 屬性（例如 `ocrEngine.Configuration.Language = Language.English;`）。

## 完整範例（可直接複製貼上）

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Load your Aspose license (optional for trial)
        // var license = new Aspose.OCR.License();
        // license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set output to JSON – this is the key step for convert image to JSON
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Optional: improve accuracy for PNG files
        ocrEngine.Configuration.Dpi = 300; // higher DPI = better results

        // 4️⃣ Load the image you want to process
        var inputImagePath = @"YOUR_DIRECTORY/receipt.png";
        if (!File.Exists(inputImagePath))
            throw new FileNotFoundException($"Image not found: {inputImagePath}");

        var inputImage = Image.FromFile(inputImagePath);

        // 5️⃣ Run OCR – this is where we actually extract text from image
        var ocrResult = ocrEngine.Recognize(inputImage);
        if (ocrResult == null)
            throw new InvalidOperationException("OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}