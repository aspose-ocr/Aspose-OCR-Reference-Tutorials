---
category: general
date: 2026-01-02
description: 使用 Aspose OCR 於 C# 從圖像提取文字。了解如何快速且可靠地將圖像轉換為 JSONL 格式。
draft: false
keywords:
- extract text from image
- convert image to jsonl
language: zh-hant
og_description: 使用 Aspose OCR 從圖像提取文字並轉換為 JSONL 格式。完整的逐步 C# 教學，適合開發者。
og_title: 從圖片提取文字 – 在 C# 中轉換為 JSONL
tags:
- C#
- OCR
- Aspose
- JSONL
title: 從圖片提取文字並轉換為 JSONL – C# 指南
url: /zh-hant/net/text-recognition/extract-text-from-image-and-convert-to-jsonl-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像提取文字並轉換為 JSONL – 完整 C# 教程

有沒有曾經需要**從圖像提取文字**，卻不確定哪個函式庫能提供乾淨、結構化的輸出？你並不孤單。在許多收據處理或文件數位化專案中，瓶頸往往是將位圖轉換為可搜尋的文字*以及*機器可讀的格式。

好消息是？使用 Aspose OCR，你可以**從圖像提取文字**，只需幾行程式碼，就能**將圖像轉換為 JSONL**，供下游分析使用。本指南將帶你完成整個流程，從載入 PNG 到寫入可串流至資料管線的 JSON‑Lines 檔案。

> **提示：**如果你已經在使用 .NET 6 或更新版本，相同的程式碼即可直接運作，無需額外設定。

## 前置條件 — 你需要的項目

- **.NET 6 SDK**（或任何較新的 .NET 版本）
- **Aspose.OCR** NuGet 套件  
  ```bash
  dotnet add package Aspose.OCR
  ```
- **Newtonsoft.Json** 用於序列化  
  ```bash
  dotnet add package Newtonsoft.Json
  ```
- 範例圖像（例如 `receipt.png`），放在可參考的資料夾中。
- 你選擇的 IDE 或編輯器 — Visual Studio、VS Code、Rider 等。

不需要繁重的設定，也不需要外部服務，只要幾個 NuGet 套件即可。

![使用 C# 透過 Aspose OCR 從圖像提取文字](https://example.com/assets/ocr-sample.png)

*Alt text: 使用 C# 及 Aspose OCR 從圖像提取文字*

## 步驟 1：載入要處理的圖像  

當你想要**從圖像提取文字**時，首先要做的事就是提供 OCR 引擎一個位圖。使用 `System.Drawing.Bitmap` 簡單直接，且適用於大多數點陣圖格式。

```csharp
using System.Drawing;

// Adjust the path to where your receipt.png lives
string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
Bitmap receiptImage = new Bitmap(imagePath);
```

> **為什麼這很重要：**將圖像以 `Bitmap` 載入，可讓 OCR 引擎直接存取像素，較起以原始位元組串流的方式，提升辨識速度與準確度。

## 步驟 2：為 JSON‑Lines 輸出設定 Aspose OCR  

Aspose OCR 允許你指定語言、輸出格式以及一些效能調整。我們在此請求 **JSON‑Lines**（每行一個 JSON 物件），因為它非常適合之後逐行處理。

```csharp
using Aspose.OCR;

// Create the engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine we’re dealing with English text
RecognitionOptions options = new RecognitionOptions
{
    Language = Language.English,
    OutputFormat = OutputFormat.JsonLines   // This is the key for converting image to JSONL
};
```

**專業提示：**如果需要多語言收據，請設定 `Language = Language.Multilingual` 或傳入 `Language` 陣列。

## 步驟 3：執行 OCR 並取得結果  

現在我們真的**從圖像提取文字**。`Recognize` 方法會回傳一個 `OcrResult` 物件，內含 `OcrLine` 物件集合，每個物件代表一行已辨識的文字及其邊界框。

```csharp
// Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);
```

此時 `ocrResult.Lines` 已包含你所需的全部資訊——原始文字、信心分數與座標。

## 步驟 4：將行序列化為 JSON‑Lines  

我們會將集合轉換為格式化的 JSON 字串。雖然 JSON‑Lines 通常是緊湊的，但加入縮排可讓開發時更易檢查檔案。

```csharp
using Newtonsoft.Json;

// Serialize each line as a separate JSON object
string jsonLines = JsonConvert.SerializeObject(
    ocrResult.Lines,
    Formatting.Indented
);
```

產生的 `jsonLines` 變數大致如下（為簡潔起見已裁剪）：

```json
{
  "Text": "Store XYZ",
  "Confidence": 0.98,
  "BoundingBox": { "X": 10, "Y": 15, "Width": 120, "Height": 20 }
}
{
  "Text": "Date: 01/01/2026",
  "Confidence": 0.95,
  "BoundingBox": { "X": 10, "Y": 45, "Width": 180, "Height": 20 }
}
```

每行皆以換行字元結尾，從而得到真正的 **JSONL**（JSON‑Lines）檔案。

## 步驟 5：將 JSON‑Lines 寫入磁碟  

最後，我們將輸出持久化，讓其他服務（例如 Spark、Logstash，或簡單的 Bash 腳本）能逐行讀取。

```csharp
using System.IO;

// Choose a destination file
string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
File.WriteAllText(outputPath, jsonLines);
```

當你開啟 `receipt.jsonl` 時，會看到每行一個 JSON 物件，已可供串流使用。

## 步驟 6：驗證匯出結果  

快速的合理性檢查能為你節省日後數小時的除錯時間。讓我們讀回前幾行並印到主控台。

```csharp
Console.WriteLine("First three lines of the JSONL output:");
foreach (var line in File.ReadLines(outputPath).Take(3))
{
    Console.WriteLine(line);
}
```

典型的主控台輸出：

```
First three lines of the JSONL output:
{"Text":"Store XYZ","Confidence":0.98,"BoundingBox":{"X":10,"Y":15,"Width":120,"Height":20}}
{"Text":"Date: 01/01/2026","Confidence":0.95,"BoundingBox":{"X":10,"Y":45,"Width":180,"Height":20}}
{"Text":"Total   $23.45","Confidence":0.97,"BoundingBox":{"X":10,"Y":75,"Width":150,"Height":20}}
```

如果看到類似的結果，恭喜你——你已成功**從圖像提取文字**且**將圖像轉換為 JSONL**。

## 常見陷阱與避免方法

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **空白輸出** | 圖像路徑不正確或檔案無法讀取。 | 在建立 bitmap 前先使用 `File.Exists(imagePath)` 檢查檔案是否存在。 |
| **信心分數低** | 圖像模糊或對比度低。 | 對圖像進行前處理（例如 `Bitmap.RotateFlip`、`Graphics.Clear`）或提高 DPI。 |
| **語言設定錯誤** | OCR 預設為英文，但收據使用其他語言。 | 設定 `options.Language = Language.Spanish`（或相應的列舉值）。 |
| **JSONL 顯示為單一 JSON 陣列** | 使用了 `Formatting.None` 卻未處理換行。 | 確保每個序列化的物件以 `Environment.NewLine` 結尾。 |

## 完整範例程式  

以下是完整、可直接執行的程式。將它貼到 Console 專案中，然後按 **F5**。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using Newtonsoft.Json;

namespace OcrToJsonlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the image
            string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }
            Bitmap receiptImage = new Bitmap(imagePath);

            // 2️⃣ Set up OCR options for JSON‑Lines output
            OcrEngine ocrEngine = new OcrEngine();
            RecognitionOptions options = new RecognitionOptions
            {
                Language = Language.English,
                OutputFormat = OutputFormat.JsonLines
            };

            // 3️⃣ Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);

            // 4️⃣ Serialize to JSON‑Lines
            string jsonLines = JsonConvert.SerializeObject(
                ocrResult.Lines,
                Formatting.Indented
            );

            // 5️⃣ Write to file
            string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
            File.WriteAllText(outputPath, jsonLines);
            Console.WriteLine($"✅ JSONL saved to {outputPath}");

            // 6️⃣ Quick verification
            Console.WriteLine("\nFirst three lines of output:");
            foreach (var line in File.ReadLines(outputPath).Take(3))
            {
                Console.WriteLine(line);
            }
        }
    }
}
```

**預期結果：**產生一個 `receipt.jsonl` 檔案，每行包含一個 JSON 物件，內含 `Text`、`Confidence` 與 `BoundingBox` 欄位。你現在可以將此檔案輸入任何消費 JSONL 的分析管線。

## 後續步驟 — 超越基礎 OCR  

- **批次處理：**將上述邏輯包在 `foreach` 迴圈中，以處理整個收據資料夾。  
- **平行處理：**使用 `Parallel.ForEach` 在處理數千張圖像時利用多核心加速。  
- **後處理：**在儲存前剔除信心分數低的行（`Confidence < 0.9`）。  
- **整合：**使用相應的 SDK，直接將 JSONL 推送至 Azure Blob Storage 或 AWS S3。  
- **其他格式：**若下游系統偏好，可將 `OutputFormat` 改為 `PlainText` 或 `Xml`。  

## 結論  

現在你已擁有一套完整、端對端的解決方案，使用 Aspose OCR 在 C# 中**從圖像提取文字**並**將圖像轉換為 JSONL**。本教學涵蓋了從載入 bitmap 到驗證輸出的所有步驟，並提供了多項實用技巧，讓你的管線更具韌性。

使用你自己的收據、發票或掃描表單試試看——觀察 OCR 引擎如何在數秒內將像素轉換為可搜尋、具行結構的資料。若遇到特殊情況（例如傾斜掃描或多語言文字），請重新檢視 *RecognitionOptions* 部分，調整語言或前處理步驟。

祝程式開發愉快，願你的資料管線永遠保持乾淨！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}