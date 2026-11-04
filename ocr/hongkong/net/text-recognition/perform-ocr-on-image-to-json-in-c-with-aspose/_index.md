---
category: general
date: 2026-04-08
description: 學習如何使用 Aspose OCR 在 C# 中對圖像執行 OCR 並寫入 JSON 檔案。本 Aspose OCR C# 教學示範將 OCR
  圖像轉換為包含置信度值的 JSON。
draft: false
keywords:
- perform OCR on image
- write JSON file C#
- OCR image to JSON
- Aspose OCR C# tutorial
language: zh-hant
og_description: 在 C# 中對圖像執行 OCR 並將結果匯出為 JSON 檔案。本教學涵蓋完整的 Aspose OCR C# 工作流程，包括信心分數。
og_title: 在 C# 中對圖像執行 OCR 並轉換為 JSON – Aspose OCR 指南
tags:
- Aspose
- OCR
- C#
- JSON
title: 在 C# 中使用 Aspose 將圖像 OCR 轉換為 JSON
url: /zh-hant/net/text-recognition/perform-ocr-on-image-to-json-in-c-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中使用 Aspose 執行影像 OCR 並轉成 JSON

是否曾需要 **對影像執行 OCR**，卻不確定如何將結果轉成結構化格式？你並不孤單——開發者常問：「如何把掃描的圖片變成可用的資料？」好消息是 Aspose.OCR 讓這件事變得非常簡單，甚至可以 **write JSON file C#**‑style，並包含信心分數。

在本指南中，我們將一步步說明完整的 **aspose OCR C# tutorial**，從載入影像到將辨識文字匯出為 JSON。完成後，你將擁有一個可執行的 Console 應用程式，能 **perform OCR on image**、將輸出轉成 JSON（含信心值），只需一行程式碼即可儲存。沒有隱藏步驟、沒有外部腳本——純粹的 C#。

## 前置條件

在開始之前，請確保你已具備：

- .NET 6.0 SDK 或更新版本（此程式碼同樣支援 .NET Core 與 .NET Framework）
- Visual Studio 2022（或任何你喜歡的編輯器）
- 有效的 **Aspose.OCR for .NET** 授權或免費暫時授權（免費試用版可用於測試）
- 一張欲處理的影像檔案（`input.png`），支援的常見格式如 PNG、JPG、BMP 等

就這些。如果缺少任何項目，請立即取得；接下來的教學假設這些已就緒。

## 第一步：安裝 Aspose.OCR NuGet 套件

首先，將函式庫加入專案。於專案資料夾開啟終端機，執行：

```bash
dotnet add package Aspose.OCR
```

此指令會下載最新版本（截至 2026 年 4 月為 23.12）並將必要的 DLL 放入 `bin` 資料夾，無需額外設定。

## 第二步：初始化 OCR 引擎（Perform OCR on Image）

接著建立 `OcrEngine` 實例，並指定使用的語言。英語（`"en"`）最常用，你也可以改成 `"fr"`、`"de"` 或其他支援的語言。

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Path to your input image – change as needed
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        // Path where the JSON will be saved
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // Step 2: Initialize the OCR engine – this is where we **perform OCR on image**
        var ocrEngine = new OcrEngine
        {
            Language = "en"               // Set language; you can use ISO‑639‑1 codes
        };

        // Optional: tweak recognition options (speed vs. accuracy)
        // ocrEngine.RecognitionMode = RecognitionMode.LargeText; // Uncomment for large blocks
```

**為什麼在此初始化：** `OcrEngine` 會保存所有辨識所需的設定。提前設定語言可確保引擎使用正確的字元集，顯著提升辨識準確度。

## 第三步：辨識影像並取得信心分數

引擎就緒後，將影像檔案傳入。`RecognizeImage` 方法會回傳 `OcrResult` 物件，內含擷取的文字與每個單字的信心分數。

```csharp
        // Step 3: Perform OCR on the image file
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Verify that the result is not null
        if (ocrResult == null)
        {
            Console.WriteLine("OCR failed – check the file path and format.");
            return;
        }

        // For debugging: print the plain text to the console
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
```

**底層發生了什麼？** Aspose 以神經網路為基礎的辨識器會分析每個像素區塊，對照語言模型，並附加 0‑100 的信心值，告訴你對每個單字的確定程度。

## 第四步：將結果轉成 JSON（OCR Image to JSON）

Aspose 讓轉換變得毫不費力。傳入 `includeConfidence: true` 後，我們會得到如下的 JSON 內容：

```json
{
  "Text": "Hello world",
  "Words": [
    { "Value": "Hello", "Confidence": 97.3 },
    { "Value": "world", "Confidence": 95.8 }
  ]
}
```

產生 JSON 字串的程式碼如下：

```csharp
        // Step 4: Convert OCR result to JSON, including confidence values
        string jsonResult = ocrResult.ToJson(includeConfidence: true);
```

**為什麼要包含信心分數？** 若你打算將資料送入後續流程（例如驗證、UI 高亮），了解哪些單字較不確定，可決定是否向使用者請求確認。

## 第五步：以 C# 風格寫入 JSON 檔案

現在正式 **write JSON file C#**。`File.WriteAllText` 方法具備原子性且跨平台，十分適合 Console 應用程式使用。

```csharp
        // Step 5: Save the JSON output to a file
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

以上即完成整個工作流程——五個簡潔步驟即可 **perform OCR on image**、將輸出轉成 JSON，並持久化儲存。

## 完整範例程式

以下程式碼可直接複製貼上至 `Program.cs`。請確保 `input.png` 與編譯後的執行檔位於同一目錄，或自行調整路徑。

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------------
        // 1️⃣ Set up file locations (feel free to change paths)
        // -------------------------------------------------------
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // -------------------------------------------------------
        // 2️⃣ Initialize the OCR engine – this is where we **perform OCR on image**
        // -------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = "en" // English – replace with "fr", "es", etc. as needed
        };

        // -------------------------------------------------------
        // 3️⃣ Recognize the image and obtain confidence values
        // -------------------------------------------------------
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        if (ocrResult == null)
        {
            Console.WriteLine("❌ OCR failed – verify the image path and format.");
            return;
        }

        // Show plain text (optional)
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine();

        // -------------------------------------------------------
        // 4️⃣ Convert the result to JSON – **OCR image to JSON**
        // -------------------------------------------------------
        string jsonResult = ocrResult.ToJson(includeConfidence: true);

        // -------------------------------------------------------
        // 5️⃣ Write the JSON file – **write JSON file C#** style
        // -------------------------------------------------------
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

### 預期輸出

執行程式（`dotnet run`）後，畫面會顯示類似以下內容：

```
=== Extracted Text ===
Hello world

✅ JSON with confidence saved to: C:\YourProject\output.json
```

而 `output.json` 則會包含前面示範的結構化 JSON，內含每個單字的信心百分比。

## 專業技巧與邊緣情況

- **檔案不存在處理：** 若路徑可能是動態的，請將 `RecognizeImage` 包在 `try/catch`，捕捉 `FileNotFoundException`。
- **不同語言：** 設定 `ocrEngine.Language = "fr"` 以使用法語，或透過 `ocrEngine.LoadLanguage("custom.lang")` 載入自訂語言包。
- **大型文件：** 若處理多頁 PDF，先使用 `Aspose.PDF` 將每頁轉成影像，再逐頁執行 OCR。
- **效能調校：** 若只需快速結果，可切換至 `RecognitionMode.Fast`——會犧牲少許準確度換取速度。
- **JSON 格式化：** 想要美化輸出嗎？在反序列化 Aspose 產生的 JSON 後，使用 Newtonsoft 的 `JsonConvert.SerializeObject` 並加上 `Formatting.Indented`。

## 常見問題

**Q: 這能在 .NET Framework 上執行嗎？**  
A: 當然可以。相同的 NuGet 套件支援 .NET Standard 2.0，因而可在 .NET Framework 4.6.1 以上版本引用。

**Q: 若我需要整份文件的總體信心分數，而不是每個單字的，該怎麼做？**  
A: `OcrResult` 也提供 `OverallConfidence` 屬性。你可以手動將它加入 JSON：

```csharp
var customObj = new
{
    Text = ocrResult.Text,
    OverallConfidence = ocrResult.OverallConfidence,
    Words = ocrResult.Words
};
string json = JsonConvert.SerializeObject(customObj, Formatting.Indented);
```

**Q: 能直接把 JSON 串流傳送到 Web API 嗎？**  
A: 可以。將 `File.WriteAllText` 換成 `HttpClient` 的 POST，將 `jsonResult

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}