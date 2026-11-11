---
category: general
date: 2026-05-02
description: C# OCR 教學，示範如何在 C# 中擷取文字影像、辨識 PNG 文字，然後使用 JsonSerializer 寫入縮排的 JSON。一步一步的開發者指南。
draft: false
keywords:
- c# ocr tutorial
- extract text image c#
- recognize png text
- write indented json
- use jsonserializer c#
language: zh-hant
og_description: c# OCR 教學，示範如何使用 C# 從圖像中提取文字並辨識 PNG 圖片文字，然後使用 JsonSerializer 輸出縮排的
  JSON。完整、可執行的範例。
og_title: c# OCR 教學 – 提取文字並匯出為縮排 JSON
tags:
- OCR
- C#
- Aspose
- JSON
title: C# OCR 教學 – 從圖像提取文字並匯出為縮排 JSON
url: /zh-hant/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-as-indent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – 從圖片提取文字並匯出為縮排 JSON

有沒有曾經需要一個 **c# ocr tutorial**，直接從文字圖片轉成格式良好的 JSON 檔案？你並不是唯一的需求者。在許多專案中——例如發票掃描、收據解析，甚至簡單的 meme 文字抽取——最終會得到一個 PNG 檔，卻不知道如何在不自行編寫辨識器的情況下抽出文字。  

本指南提供實作解決方案：我們將使用 Aspose.OCR **extract text image c#**，**recognize png text**，然後使用 C# 中的 `JsonSerializer` **write indented json**。完成後，你將擁有一個可自行部署的主控台應用程式，能直接放入任何 .NET 解決方案。沒有模糊的「請參考文件」連結，只有完整、可直接複製貼上的範例。

## 需要的工具

- **.NET 6**（或任何較新的 .NET 版本）。舊版框架亦可使用，但此範例語法以 .NET 6+ 為目標。
- **Aspose.OCR for .NET** – 透過 NuGet 安裝：`dotnet add package Aspose.OCR`。
- 一個範例 PNG 圖片（`text.png`），內含清晰、機器可讀的文字。
- 你慣用的 IDE 或編輯器 – Visual Studio、VS Code、Rider 等等。

> **Pro tip:** 如果你打算處理大量圖片，建議重複使用同一個 `OcrEngine` 實例，而不是每個檔案都新建一個。這樣可減少開銷並提升吞吐量。

## 步驟 1：建立 c# ocr tutorial 專案

首先，建立一個主控台專案。以下指令會產生專案骨架並加入 OCR 函式庫：

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
dotnet add package Aspose.OCR
```

接著開啟產生的 `Program.cs`。稍後我們會把內容換成完整範例，現在先確保專案能成功編譯：

```bash
dotnet build
```

若未看到錯誤，即可繼續下一步。

## 步驟 2：從圖片辨識 PNG 文字

任何 **c# ocr tutorial** 的核心都是 OCR 引擎本身。Aspose.OCR 抽象化低階細節，提供簡潔的 `OcrEngine` 類別。以下示範建立引擎、指向 PNG 檔，並要求辨識文字。

```csharp
using Aspose.OCR;
using System;
using System.Text.Json;

class JsonExportExample
{
    public static void Run()
    {
        // 1️⃣ Create an OCR engine instance – this is the entry point for all OCR work.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Recognize text from the input image. 
        //    The method automatically detects the language (default is English) and returns an OcrResult.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/text.png");

        // If the image couldn't be read, handle it gracefully.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No text detected – double‑check the file path and image quality.");
            return;
        }

        // Continue to serialization...
```

### 為什麼這樣可行

- **`RecognizeImage`** 支援多種格式（PNG、JPEG、BMP）。我們特別 **recognize png text**，因為 PNG 保留無損細節，最適合 OCR。
- 回傳的 `OcrResult` 不僅包含純文字，還有每個字形的信心分數，若日後需要過濾低信心字元時相當有用。

## 步驟 3：使用 JsonSerializer c# 寫入縮排 JSON

既然已取得 `ocrResult`，在我們的 **c# ocr tutorial** 中接下來的合理步驟就是將該物件轉成可讀的 JSON。內建的 `System.Text.Json` 序列化器即可完成，我們會將其設定為 **write indented json** 以提升可讀性。

```csharp
        // 3️⃣ Serialize the OCR result (including confidence per glyph) to indented JSON.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // This makes the output pretty‑printed.
        };

        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 4️⃣ Display the JSON result – you could also write it to a file if you prefer.
        Console.WriteLine(jsonOutput);
    }
}
```

### 正確使用 `JsonSerializer`

- `WriteIndented` 旗標是 **write indented json** 最簡單的方式，且不需額外第三方函式庫。
- 若需要使用 camel‑case 屬性名稱，可在選項中加入 `PropertyNamingPolicy = JsonNamingPolicy.CamelCase`。
- `jsonOutput` 字串可透過 `File.WriteAllText("result.json", jsonOutput);` 儲存——這在實務流程中相當方便。

## 步驟 4：執行並驗證輸出

Compile and run the program:

```bash
dotnet run
```

假設 `text.png` 內含字串 *“Hello, OCR World!”*，執行後應會看到類似以下內容：

```json
{
  "Text": "Hello, OCR World!",
  "Confidence": 0.9875,
  "Lines": [
    {
      "Text": "Hello, OCR World!",
      "Confidence": 0.9875,
      "Words": [
        {
          "Text": "Hello,",
          "Confidence": 0.9921,
          "BoundingBox": { "X": 12, "Y": 34, "Width": 58, "Height": 20 }
        },
        {
          "Text": "OCR",
          "Confidence": 0.9812,
          "BoundingBox": { "X": 78, "Y": 34, "Width": 34, "Height": 20 }
        },
        {
          "Text": "World!",
          "Confidence": 0.9890,
          "BoundingBox": { "X": 118, "Y": 34, "Width": 62, "Height": 20 }
        }
      ]
    }
  ]
}
```

那個 JSON 已 **indented**，便於在日誌中閱讀或交給下游服務。

### 邊緣情況與技巧

| 情況 | 處理方式 |
|-----------|------------|
| **圖片模糊** | 在呼叫 `RecognizeImage` 前，提高 `ocrEngine.Config.Dpi`（例如 `ocrEngine.Config.Dpi = 300`）。 |
| **非英語語言** | 設定 `ocrEngine.Config.Language = OcrLanguage.German`（或任何支援的語言）。 |
| **大量檔案批次** | 遍歷目錄，重複使用同一個 `OcrEngine` 實例；將每個 JSON 結果以唯一檔名儲存。 |
| **僅需高信心文字** | 在序列化前，過濾 `ocrResult.Lines`，僅保留 `Confidence` ≥ 0.95 的項目。 |

## 完整可執行範例（直接複製貼上）

以下是 *完整* 程式碼，可直接放入 `Program.cs`。它包含所有步驟、錯誤處理與說明註解，使程式碼易於理解。

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    public static void Main()
    {
        // 👉 Step 1: Initialize the OCR engine.
        var ocrEngine = new OcrEngine();

        // 👉 Step 2: Path to the PNG image you want to process.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "text.png");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found at {imagePath}");
            return;
        }

        // 👉 Step 3: Perform OCR – this is where we **recognize png text**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 👉 Step 4: Validate the result.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No recognizable text found. Try a clearer image or adjust DPI settings.");
            return;
        }

        // 👉 Step 5: Configure JsonSerializer to **write indented json**.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // Pretty‑print the JSON.
        };

        // 👉 Step 6: Serialize the OCR result – this demonstrates **use jsonserializer c#**.
        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 👉 Step 7: Output to console (or write to a file).
        Console.WriteLine(jsonOutput);

        // Optional: Save to disk.
        string outputPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(outputPath, jsonOutput);
        Console.WriteLine($"JSON saved to {outputPath}");
    }
}
```

執行程式，檢查主控台或產生的 `.json` 檔，即可看到提取的文字與信心分數，全部以 **indented** 方式整齊呈現。

## 結論

現在你已擁有一個完整的 **c# ocr tutorial**，示範如何使用 `JsonSerializer` 進行 **extract text image c#**、**recognize png text** 與 **write indented json**。此範例完整、可執行，且提供實務情境的實用技巧。  

接下來的步驟是什麼？可以嘗試將 Aspose.OCR 換成其他引擎（例如 Tesseract），觀察 `OcrResult` 結構的變化，或將 JSON 送入下游 API，將 OCR 資料寫入資料庫。你也可以試驗 **use jsonserializer c#** 的選項，如自訂轉換器以處理日期格式或列舉型別。

祝編程愉快，願你的 OCR 流程永遠精準！  

---  

![c# ocr tutorial diagram](image.png "Diagram illustrating OCR flow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}