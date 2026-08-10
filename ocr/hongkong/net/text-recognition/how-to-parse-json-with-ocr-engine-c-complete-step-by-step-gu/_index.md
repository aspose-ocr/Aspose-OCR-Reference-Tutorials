---
category: general
date: 2026-03-17
description: 學習如何在 C# 中解析 OCR 結果的 JSON。此教學涵蓋如何擷取文字、載入影像以進行 OCR、執行 OCR 識別，以及有效使用 C#
  的 OCR 引擎。
draft: false
keywords:
- how to parse json
- how to extract text
- load image for OCR
- run OCR recognition
- use OCR engine C#
language: zh-hant
og_description: 如何在 C# 中解析 OCR 輸出的 JSON。跟隨我們的指南提取文字、載入影像進行 OCR、執行 OCR 識別，以及使用 OCR
  引擎 C#。
og_title: 如何使用 OCR 引擎 C# 解析 JSON – 完整教學
tags:
- C#
- OCR
- JSON
- Image Processing
title: 如何使用 OCR 引擎 C# 解析 JSON – 完整逐步指南
url: /zh-hant/net/text-recognition/how-to-parse-json-with-ocr-engine-c-complete-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 OCR 引擎 C# 解析 JSON – 完整逐步指南

有沒有想過 **how to parse json** 直接從 OCR 引擎產生的 JSON？你並不孤單。大多數開發者都會遇到相同的問題——取得原始 JSON，然後想辦法提取有用的資訊，例如信心分數或實際文字。在本指南中，我們將逐步說明如何載入 OCR 圖片、執行 OCR 辨識，最後以乾淨且易於維護的方式 **how to parse json**。

在本教學結束時，你將能夠：

* 只需幾行程式碼即可載入 OCR 圖片。  
* 使用 C# OCR 引擎執行 OCR 辨識。  
* **How to extract text** 並從 JSON 負載中取得其他中繼資料。  
* 處理常見的邊緣情況（欄位缺失、格式意外）而不會當機。

不需要外部文件說明——所有你需要的資訊都在這裡。

## 前置條件

在開始之前，請確保你已具備：

* .NET 6.0 或更新版本（程式碼亦可在 .NET Framework 4.7+ 上編譯）。  
* 你所使用的 OCR 函式庫參考（範例使用假想的 `OcrEngine` 類別）。  
* 用於 JSON 處理的 `Newtonsoft.Json` NuGet 套件（`Install-Package Newtonsoft.Json`）。  
* 一個圖像檔案（例如 `passport.png`），放置於應用程式可讀取的位置。

> **專業提示：** 若你使用商業 OCR SDK，請確認已啟用 JSON 輸出格式——大多數供應商會透過類似 `ocrEngine.Config.OutputFormat` 的設定屬性來公開此功能。

## 第一步 – 建立並設定 OCR 引擎（主要關鍵字示範）

首先，你需要實例化 OCR 引擎並告訴它回傳 JSON。這就是 **how to parse json** 首次出現在程式碼中的地方，因為引擎會傳回一個 JSON 字串，之後我們會對它進行解析。

```csharp
using System;
using Newtonsoft.Json.Linq;   // For JSON parsing
// Assume OcrEngine, OutputFormat, and ImageStream live in the OCR SDK namespace
using OcrSdk;                  // <-- replace with the real namespace

// Step 1: Create an OCR engine instance and set JSON output
var ocrEngine = new OcrEngine();
ocrEngine.Config.OutputFormat = OutputFormat.Json;
```

**為什麼這很重要：** 將 `OutputFormat` 設為 `Json` 可確保回應同時包含辨識文字 **以及** 如信心分數等有用的中繼資料。若遺漏此步驟，將只得到純文字，**how to parse json** 就變得沒有意義了。

## 第二步 – 載入 OCR 圖片

現在我們載入要分析的圖片。這正是次要關鍵字 **load image for OCR** 發揮作用的地方。

```csharp
// Step 2: Load the image you want to recognize
// Make sure the path points to a real file; otherwise an exception is thrown.
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY\passport.png");
```

> **如果檔案不存在會怎樣？** 請將呼叫包在 `try/catch` 中，並顯示友善的訊息——你的應用程式不會當機，使用者也能知道發生了什麼問題。

## 第三步 – 執行 OCR 辨識

引擎已就緒且圖片已載入，接下來合乎邏輯的步驟就是實際執行辨識程序。這正符合次要關鍵字 **run OCR recognition**。

```csharp
// Step 3: Execute OCR and get the raw result object
var ocrResult = ocrEngine.Recognize();
```

`ocrResult.Text` 屬性現在包含 JSON 字串。若將其印到主控台，會看到類似以下內容：

```json
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}
```

## 第四步 – 從 JSON 中提取文字（以及其他欄位）

這是本教學的核心：從 OCR 負載中 **how to parse json** 以及 **how to extract text**。我們將使用 `Newtonsoft.Json.Linq.JObject` 以獲得彈性。

```csharp
// Step 4: Output the raw JSON (optional, helps debugging)
Console.WriteLine("Raw OCR JSON:");
Console.WriteLine(ocrResult.Text);
Console.WriteLine();

// Step 5: Parse the JSON into a JObject
JObject jsonObject = JObject.Parse(ocrResult.Text);

// Extract the overall confidence score
var overallConfidence = jsonObject["OverallConfidence"]?.Value<double>() ?? 0.0;
Console.WriteLine($"Overall confidence: {overallConfidence:P0}");

// Extract the text from the first page (how to extract text)
string pageText = jsonObject["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
Console.WriteLine("Extracted text:");
Console.WriteLine(pageText);
```

**為什麼使用 `JObject`？** 它讓你在不必定義完整 C# 模型類別的情況下安全地遍歷 JSON 樹。若 OCR 引擎遺漏欄位，空值條件運算子 (`?.`) 可防止 `NullReferenceException`。

### 處理邊緣情況

* **缺少欄位：** `?.Value<T>() ?? default` 模式會回傳合理的預設值。  
* **多頁面：** 若預期有多於一頁，請對 `jsonObject["Pages"]` 進行迴圈。  
* **非數值型信心分數：** 若 SDK 有時回傳字串，請使用 `double.TryParse`。

## 第五步 – 封裝成可重複使用的方法

為避免重複貼上相同的樣板程式碼，請將整個流程封裝成輔助方法。這同時示範了 **use OCR engine C#** 以乾淨且可重複使用的方式。

```csharp
public static void RunOcrAndParseJson(string imagePath)
{
    // 1️⃣ Create engine & set JSON output
    var engine = new OcrEngine();
    engine.Config.OutputFormat = OutputFormat.Json;

    // 2️⃣ Load image (load image for OCR)
    engine.Image = ImageStream.FromFile(imagePath);

    // 3️⃣ Run OCR (run OCR recognition)
    var result = engine.Recognize();

    // 4️⃣ Show raw JSON (optional)
    Console.WriteLine("=== Raw JSON ===");
    Console.WriteLine(result.Text);
    Console.WriteLine();

    // 5️⃣ Parse JSON (how to parse json)
    JObject obj = JObject.Parse(result.Text);

    // 6️⃣ Extract useful data (how to extract text)
    double confidence = obj["OverallConfidence"]?.Value<double>() ?? 0.0;
    string text = obj["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;

    Console.WriteLine($"Overall confidence: {confidence:P0}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(text);
}
```

現在你可以在 `Main` 或應用程式的其他位置呼叫 `RunOcrAndParseJson(@"C:\Images\passport.png");`。

## 完整範例程式

以下是一個完整、獨立的主控台程式，你可以直接複製貼上到新的 `.csproj` 中。它包含了我們討論的所有部份，並加入少量錯誤處理。

```csharp
// File: Program.cs
using System;
using Newtonsoft.Json.Linq;
using OcrSdk;               // Replace with the actual namespace of your OCR library

class Program
{
    static void Main()
    {
        try
        {
            // Adjust the path to point at a real image on your machine
            string imagePath = @"YOUR_DIRECTORY\passport.png";

            RunOcrAndParseJson(imagePath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Unexpected error: {ex.Message}");
        }
    }

    /// <summary>
    /// Demonstrates how to parse JSON returned by an OCR engine,
    /// and how to extract text, confidence, and other metadata.
    /// </summary>
    /// <param name="imagePath">Full path to the image file.</param>
    public static void RunOcrAndParseJson(string imagePath)
    {
        // 1️⃣ Initialize OCR engine (use OCR engine C#)
        var engine = new OcrEngine();
        engine.Config.OutputFormat = OutputFormat.Json;

        // 2️⃣ Load image for OCR
        engine.Image = ImageStream.FromFile(imagePath);

        // 3️⃣ Run OCR recognition
        var result = engine.Recognize();

        // 4️⃣ Print raw JSON (helps debugging)
        Console.WriteLine("=== Raw OCR JSON ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // 5️⃣ Parse JSON (how to parse json)
        JObject json = JObject.Parse(result.Text);

        // 6️⃣ Extract overall confidence
        double overallConf = json["OverallConfidence"]?.Value<double>() ?? 0.0;
        Console.WriteLine($"Overall confidence: {overallConf:P0}");

        // 7️⃣ Extract text from first page (how to extract text)
        string firstPageText = json["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(firstPageText);
    }
}
```

**預期輸出**（假設 OCR 成功）：

```
=== Raw OCR JSON ===
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}

Overall confidence: 92%
=== Extracted Text ===
John Doe
Passport No: 123456789
```

如果無法讀取圖片，SDK 會拋出例外，我們在 `Main` 中捕捉，並印出友善的錯誤訊息，而不是當機。

## 常見問題 (FAQs)

**Q: 如果 OCR 引擎回傳頁面陣列會怎樣？**  
A: 對 `json["Pages"]` 進行迴圈，將每個 `["Text"]` 值串接起來，或依使用情境個別處理。

**Q: 我可以將 JSON 反序列化為具型別的 C# 類別嗎？**  
A: 當然可以。定義與 JSON 結構相符的類別，並使用 `JsonConvert.DeserializeObject<YourRootClass>(result.Text)`。這樣可提供編譯時安全性，但需確保模型與 SDK 的輸出保持同步。

**Q: 這能用於非同步 OCR API 嗎？**  
A: 可以。將 `engine.Recognize()` 改為 `await engine.RecognizeAsync()`，並將 `RunOcrAndParseJson` 設為 `async Task`。JSON 解析部分保持不變。

**Q: 我要如何將 JSON 儲存成檔案以供日後分析？**  
A: 取得 `result.Text` 後，呼叫 `File.WriteAllText(@"output.json", result.Text);`。之後可使用 `JObject.Parse(File.ReadAllText(...))` 重新載入。

## 下一步

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}