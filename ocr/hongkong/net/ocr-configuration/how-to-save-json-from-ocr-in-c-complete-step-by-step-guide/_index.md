---
category: general
date: 2026-03-02
description: 學習如何在使用 Aspose OCR 從圖像提取文字的同時儲存 JSON。包括寫入 JSON 檔案的程式碼、載入位圖圖像的技巧，以及完整的
  C# 範例。
draft: false
keywords:
- how to save json
- extract text from image
- write json file
- how to extract text
- load bitmap image
language: zh-hant
og_description: 發掘如何在使用 Aspose OCR 從圖像提取文字時儲存 JSON。完整的 C# 程式碼、寫入 JSON 檔案步驟以及實用技巧。
og_title: 如何在 C# 中從 OCR 保存 JSON – 完整程式教學
tags:
- C#
- OCR
- Aspose
- JSON
title: 如何在 C# 中將 OCR 產生的 JSON 儲存 – 完整逐步指南
url: /zh-hant/net/ocr-configuration/how-to-save-json-from-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中從 OCR 保存 JSON – 完整逐步指南

有沒有想過 **如何保存 JSON**，其中包含剛從圖片中提取的文字？你並不是唯一有此疑問的人。許多開發者在需要 *從圖像中提取文字* 並將資訊以整齊的 JSON 檔案形式持久化時，常會卡關。好消息是？只要有正確的工具，解決方案其實相當簡單。

在本教學中，我們將示範一個真實情境：使用 Aspose.OCR **從圖像中提取文字**，接著 **寫入 JSON 檔案**，最後 **在磁碟上保存 JSON**。同時也會說明如何正確 **載入 bitmap 圖片** 物件，並涵蓋可能遇到的幾個邊緣案例。完成後，你將擁有一個完整的 C# 主控台應用程式，從載入圖片到產生可直接使用的 JSON 文件全都搞定。

## 需要的環境

- .NET 6.0 或更新版本（程式碼同樣支援 .NET Core 與 .NET Framework）
- Aspose.OCR for .NET（可取得免費試用的 NuGet 套件）
- 一張包含英文文字的 PNG 或 JPG 圖片範例
- Visual Studio、VS Code，或任何支援 C# 的 IDE

不需要額外的函式庫——只要使用標準的 `System.Drawing` 命名空間處理 bitmap，及 `System.Text.Json` 進行序列化即可。

---

## Step 1 – 載入 Bitmap 圖片（「load bitmap image」部分）

在執行任何 OCR 之前，你必須先將圖像以 `Bitmap` 形式載入記憶體。這就像在閱讀書本前先打開書本一樣。

```csharp
using System.Drawing;

// Replace the placeholder with the actual path to your image file
string imagePath = @"C:\Images\sample-page.png";

// Load the image – this is the “load bitmap image” step
Bitmap bitmapImage = new Bitmap(imagePath);
```

> **小技巧：** 若圖片檔案過大，建議先縮小尺寸以提升效能。OCR 引擎在 2 MB 以下的圖像上運作較快。

---

## Step 2 – 設定 Aspose OCR 引擎

Bitmap 已就緒後，我們需要建立一個 `OcrEngine`。此物件負責 **從圖像中提取文字**，並可選擇輸出幾何資訊（如邊界框）。

```csharp
using Aspose.OCR;

// Create the OCR engine with English language and enable bounding boxes
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,
    ExportBoundingBoxes = true // adds geometry info to the result
};
```

為什麼要啟用 `ExportBoundingBoxes`？如果你日後需要在 UI 中標示單字，這些座標就非常有用。若不需要，可將此旗標設為 `false`，JSON 會稍微精簡一些。

---

## Step 3 – 執行 OCR 並取得結構化結果

引擎設定完成後，接下來就是實際的 **如何提取文字** 操作。`RecognizeToOcrResult` 方法會回傳一個豐富的物件，內含辨識文字、信心分數，以及可選的版面配置資料。

```csharp
// Run OCR – this is the core “how to extract text” call
var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);
```

此時 `ocrResult` 變數已包含所有必要資訊。若在除錯器中檢視，你會看到 `Page`、`Paragraph`、`Line`、`Word` 等層級結構，每個物件都有自己的 `Text` 屬性。

---

## Step 4 – 序列化結果為格式化的 JSON 字串

這一步就是 **如何保存 JSON** 的核心魔法。我們使用內建且效能佳的 `System.Text.Json`，它預設支援美化輸出（pretty printing）。

```csharp
using System.Text.Json;

// Serialize with indentation for readability
string jsonResult = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true }
);
```

若想使用不同的命名慣例（例如 camelCase），只要在選項中加入 `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` 即可。

---

## Step 5 – 寫入 JSON 檔案至磁碟（「write json file」步驟）

最後，我們真正 **寫入 JSON 檔案** 到檔案系統。這就是在 C# 環境中 **如何保存 JSON** 的具體答案。

```csharp
using System.IO;

// Choose where you want the JSON output
string jsonPath = @"C:\Images\sample-page.json";

// Save the JSON string – this completes the “how to save json” workflow
File.WriteAllText(jsonPath, jsonResult);
```

執行完此行程式碼後，你會在原始圖片旁看到一個排版整齊的 `sample-page.json`。用任何文字編輯器開啟，或傳給其他服務——你的 OCR 資料已可隨處使用。

---

## Step 6 – 驗證輸出（會看到什麼？）

執行程式時，應會在主控台印出簡短的確認訊息：

```csharp
Console.WriteLine("OCR result saved as JSON.");
```

打開產生的 JSON 檔案，你會看到類似以下的內容：

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello, world!",
          "Words": [
            { "Text": "Hello,", "Confidence": 0.99 },
            { "Text": "world!", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

如果 `ExportBoundingBoxes` 為 `true`，每個單字還會包含 `Rectangle` 座標，對於後續的 UI 開發相當便利。

---

## 常見問題與邊緣案例

### 圖片路徑無效該怎麼辦？

將 bitmap 載入包在 `try/catch` 區塊中，並拋出清晰的錯誤訊息：

```csharp
try
{
    Bitmap bitmapImage = new Bitmap(imagePath);
}
catch (FileNotFoundException)
{
    Console.Error.WriteLine($"Image not found: {imagePath}");
    return;
}
```

### 如何處理非英文語言？

只要更改 `Language` 屬性即可：

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Aspose 支援超過 50 種語言，挑選與來源文字相符的即可。

### 必須手動釋放 `Bitmap` 物件嗎？

必須。`Bitmap` 實作 `IDisposable`，請使用 `using` 陳述式以即時釋放原生資源。

```csharp
using (Bitmap bitmapImage = new Bitmap(imagePath))
{
    // OCR code here
}
```

### 想要產生不含縮排的緊湊 JSON 該怎麼做？

替換 `JsonSerializerOptions` 為：

```csharp
new JsonSerializerOptions { WriteIndented = false }
```

這樣可以減少檔案大小，適合頻寬受限的情境。

---

## 完整範例（直接複製貼上）

以下是結合所有步驟、錯誤處理與最佳實踐的完整程式碼。存成 `Program.cs` 後，即可在命令列或 IDE 中執行。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1 – Load the bitmap image (load bitmap image)
        // -------------------------------------------------
        string imagePath = @"C:\Images\page.png";
        string jsonPath  = @"C:\Images\page.json";

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"Error: Image file not found at {imagePath}");
            return;
        }

        using Bitmap bitmapImage = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2 – Configure the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ExportBoundingBoxes = true // optional, adds geometry info
        };

        // -------------------------------------------------
        // Step 3 – Perform OCR (how to extract text)
        // -------------------------------------------------
        var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);

        // -------------------------------------------------
        // Step 4 – Serialize to JSON (how to save json)
        // -------------------------------------------------
        string jsonResult = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true }
        );

        // -------------------------------------------------
        // Step 5 – Write JSON file (write json file)
        // -------------------------------------------------
        try
        {
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"OCR result saved as JSON at {jsonPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to write JSON file: {ex.Message}");
        }
    }
}
```

**程式功能說明：**  
1. 檢查圖片是否存在。  
2. 使用 `using` 區塊安全載入圖片。  
3. 執行 OCR 以 **從圖像中提取文字**。  
4. 將結果序列化為排版整齊的 JSON 字串。  
5. 將字串寫入磁碟，回答核心問題 **如何保存 JSON**。

執行 `dotnet run`（或在 Visual Studio 按 F5）後，檔案寫入成功時會顯示確認訊息。

---

## 結論

現在你已掌握一套完整、可投入生產環境的 **如何保存 JSON** 解決方案，從載入 bitmap 圖片到寫出乾淨的 JSON 檔案，每一步都說明了背後的「為什麼」，讓你能輕鬆套用到自己的專案中。

如果想探索下一步，可以考慮：

- **從 PDF 提取文字**：先將每頁轉為圖像再執行 OCR。  
- 使用邊界框資料在 WPF 或 WinForms UI 中標示單字。  
- 直接將 JSON 串流傳送至 Web API（使用 `HttpClient`），而非寫入檔案。

試試看、調整參數，讓 OCR 資料為你的應用程式提供動力。有任何問題歡迎留言，祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}