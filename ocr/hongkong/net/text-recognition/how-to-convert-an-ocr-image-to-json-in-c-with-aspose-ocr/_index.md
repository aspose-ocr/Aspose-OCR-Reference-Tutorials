---
category: general
date: 2026-09-06
description: 在 C# 中使用 Aspose.OCR 進行 OCR 圖像至 JSON 的轉換——一步一步教你從圖像提取文字並獲得 JSON 輸出。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- ocr image to json
- extract text from image
- convert image to text
- recognize text from photo
- load image for ocr
language: zh-hant
lastmod: 2026-09-06
og_description: 使用 Aspose.OCR 在 C# 中將 OCR 圖像轉換為 JSON。了解如何載入圖像進行 OCR、從相片辨識文字，並將結果轉換為
  JSON。
og_image_alt: Screenshot of C# code that converts an OCR image to JSON using Aspose.OCR
og_title: 在 C# 中將 OCR 圖像轉換為 JSON – 完整 Aspose.OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-09-06'
  description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  headline: How to convert an OCR image to JSON in C# with Aspose.OCR
  type: TechArticle
- description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  name: How to convert an OCR image to JSON in C# with Aspose.OCR
  steps:
  - name: Place an image named `input.jpg` in the project root.
    text: Place an image named `input.jpg` in the project root.
  - name: Execute `dotnet run`.
    text: Execute `dotnet run`.
  - name: Observe the console output and open `output.json` to see the structured
      data.
    text: Observe the console output and open `output.json` to see the structured
      data.
  type: HowTo
- questions:
  - answer: Yes. Use `ocrEngine.SaveJson(Stream)` to write directly to a `MemoryStream`,
      then call `stream.ToArray()`.
    question: Can I get the OCR result as a byte array instead of a file?
  - answer: Aspose.OCR can accept PDF pages converted to images via Aspose.PDF, but
      the OCR engine itself works on raster images. Convert PDFs to images first,
      then **load image for ocr**.
    question: Does the engine support PDF input?
  - answer: 'Set `ocrEngine.Language = OcrLanguage.Arabic`. The JSON includes the
      correct text direction, which you can render in UI frameworks that support RTL.
      ## Conclusion You now have a complete solution for **ocr image to json** in
      C#. By loading an image, configuring the language, running the OCR engine, '
    question: How do I handle right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- Aspose.OCR
- C#
- JSON
- Image processing
title: 如何在 C# 中使用 Aspose.OCR 將 OCR 圖像轉換為 JSON
url: /zh-hant/net/text-recognition/how-to-convert-an-ocr-image-to-json-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.OCR 將 OCR 圖像轉換為 JSON

如果您需要在 .NET 應用程式中 **ocr image to json**，本教學將示範如何使用 Aspose.OCR 完成。 我們會一步步說明如何載入圖像進行 OCR、從照片中辨識文字，並將結果轉換為 JSON，讓您可以在 API 或資料庫中使用這些資料。

從圖像檔案中擷取文字是發票處理、收據掃描與檔案保存等專案的常見需求。 完成本教學後，您將能 **convert image to text**、取得純文字結果，並產生保留版面資訊的結構化 JSON 負載。

## Prerequisites

在開始之前，請確保您已具備：

- 已安裝 .NET 6.0 SDK 或更新版本  
- Visual Studio 2022（或任何支援 .NET 的編輯器）  
- 已於專案中加入 Aspose.OCR NuGet 套件（`Aspose.OCR`）  
- 已將範例圖像（`input.jpg`）放置於程式碼可參考的資料夾中  

您不需要額外的 OCR 引擎；Aspose.OCR 會在內部處理所有繁重工作。

## Step 1: Install the Aspose.OCR NuGet package

在專案資料夾的終端機中執行：

```bash
dotnet add package Aspose.OCR
```

此套件包含 `Aspose.OCR.OcrEngine` 類別，提供 **load image for ocr**、語言選擇與結果匯出的相關方法。

## Step 2: Create a new C# console project

如果尚未有專案，請建立一個：

```bash
dotnet new console -n OcrToJsonDemo
cd OcrToJsonDemo
```

加入您需要的 `using` 指示詞：

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;
```

## Step 3: Load the image and configure the OCR engine

以下程式碼示範如何 **load image for ocr**、設定語言，並為處理做準備。 本例使用西里爾文，您也可以依來源語言改為 `OcrLanguage.English`、`OcrLanguage.French` 等。

```csharp
// Step 3: Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Choose the language that matches the text in the image.
// Replace OcrLanguage.Cyrillic with the language you need.
ocrEngine.Language = OcrLanguage.Cyrillic;

// Load the image file. The ImageStream class abstracts file, stream, or byte[] sources.
string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **為何重要：** 正確設定語言可大幅提升在 **recognize text from photo** 時的準確度。 引擎會使用語言專屬的字典與字元集。

## Step 4: Run the OCR process and retrieve results

現在執行 OCR 引擎。 若處理成功，您可以將 **extract text from image** 以純文字、HTML 或 JSON 形式取得。 Aspose.OCR 提供 `SaveJson` 方法，可將結構化結果寫入檔案。

```csharp
// Step 4: Execute the OCR process
if (ocrEngine.Process())
{
    // Plain‑text output
    string plainText = ocrEngine.Text;
    Console.WriteLine("=== Plain Text ===");
    Console.WriteLine(plainText);

    // JSON output – includes bounding boxes, confidence scores, and line information
    string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
    ocrEngine.SaveJson(jsonPath);
    Console.WriteLine($"\nJSON result saved to: {jsonPath}");
}
else
{
    Console.WriteLine("OCR processing failed. Check the image path and format.");
}
```

### Expected JSON structure

典型的 `output.json` 內容如下（為了易讀已做格式化）：

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Пример текста",
          "Confidence": 0.96,
          "Rect": { "X": 45, "Y": 120, "Width": 210, "Height": 30 }
        },
        {
          "Text": "Еще одна строка",
          "Confidence": 0.93,
          "Rect": { "X": 45, "Y": 160, "Width": 230, "Height": 28 }
        }
      ]
    }
  ]
}
```

此 JSON 負載包含每一行的文字、信心分數，以及在原始照片中包圍該行的矩形。 這讓您能輕鬆將 OCR 結果對映回 UI 元件或資料庫欄位。

## Step 5: Full source code for the demo

以下是完整、可直接執行的程式碼，實作 **ocr image to json** 工作流程。 複製至 `Program.cs` 後執行 `dotnet run`。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrToJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Select the language (Cyrillic in this example)
            ocrEngine.Language = OcrLanguage.Cyrillic;

            // 3️⃣ Load the image you want to process
            string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found: {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Run the OCR process
            if (ocrEngine.Process())
            {
                // 5️⃣ Retrieve plain text (optional)
                string plainText = ocrEngine.Text;
                Console.WriteLine("=== Plain Text ===");
                Console.WriteLine(plainText);

                // 6️⃣ Save the result as JSON
                string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
                ocrEngine.SaveJson(jsonPath);
                Console.WriteLine($"\nJSON result saved to: {jsonPath}");
            }
            else
            {
                Console.WriteLine("OCR processing failed. Verify the image format and language settings.");
            }
        }
    }
}
```

### Running the example

1. 在專案根目錄放置一張名為 `input.jpg` 的圖像。  
2. 執行 `dotnet run`。  
3. 觀察主控台輸出，並開啟 `output.json` 以檢視結構化資料。

## Pro tips and common pitfalls

| Situation | Recommendation |
|-----------|----------------|
| **Low‑resolution photos** | 在處理前提升 DPI，或使用 `ocrEngine.Image = ImageStream.FromFile(path, 300)` 強制 300 DPI。 |
| **Mixed languages** | 設定 `ocrEngine.Language = OcrLanguage.Multilingual`，並可透過 `ocrEngine.Language = new[] { OcrLanguage.English, OcrLanguage.Cyrillic }` 提供語言清單。 |
| **Large documents** | 一次處理單頁以降低記憶體使用量；引擎支援多頁 TIFF。 |
| **Incorrect characters** | 確認已選擇正確的 `OcrLanguage`；使用錯誤語言會降低 **convert image to text** 的準確度。 |
| **JSON missing fields** | 請確保使用 Aspose.OCR 23.6 以上版本；較舊版本未提供 `SaveJson` 方法。 |

## Frequently asked questions

**Q: Can I get the OCR result as a byte array instead of a file?**  
A: 可以。使用 `ocrEngine.SaveJson(Stream)` 直接寫入 `MemoryStream`，之後呼叫 `stream.ToArray()`。

**Q: Does the engine support PDF input?**  
A: Aspose.OCR 可接受透過 Aspose.PDF 轉換成圖像的 PDF 頁面，但 OCR 引擎本身僅處理點陣圖。 請先將 PDF 轉為圖像，再 **load image for ocr**。

**Q: How do I handle right‑to‑left scripts like Arabic?**  
A: 設定 `ocrEngine.Language = OcrLanguage.Arabic`。JSON 會包含正確的文字方向，您可在支援 RTL 的 UI 框架中正確呈現。

## Conclusion

現在您已掌握在 C# 中實作 **ocr image to json** 的完整解決方案。 只要載入圖像、設定語言、執行 OCR 引擎，並將結果匯出為 JSON，即可 **extract text from image**、**convert image to text**、以及 **recognize text from photo**，完成一條流暢的工作流程。

接下來您可以探索：

- 將 JSON 輸出整合至 Web API（`ASP.NET Core`）  
- 將結果儲存至 MongoDB 等 NoSQL 資料庫  
- 加入後處理以校正常見 OCR 錯誤  

歡迎嘗試不同語言、圖像格式與輸出選項，以符合您的專案需求。 Happy coding!

## What Should You Learn Next?

以下教學與本指南緊密相關，能進一步擴展您的技巧。 每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，並探索替代實作方式。

- [recognize text from image in C# – Complete Guide to OCR and JSON](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/)
- [Convert Image to Text in C# with Aspose OCR – Step‑by‑Step Guide](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}