---
category: general
date: 2026-01-10
description: 學習如何使用 Aspose OCR 在 C# 中辨識圖像文字、擷取文字座標，並將收據轉換為 JSON。逐步教學。
draft: false
keywords:
- recognize text from image
- how to extract text
- extract text coordinates
- convert receipt to json
language: zh-hant
og_description: 使用 Aspose OCR 在 C# 中辨識圖像文字。本指南示範如何擷取文字、取得座標，並將收據轉換為 JSON。
og_title: 從圖像辨識文字 – 完整 C# OCR 教學
tags:
- OCR
- C#
- Aspose
title: 在 C# 中從圖像識別文字 – OCR 與 JSON 完全指南
url: /zh-hant/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像辨識文字 – 完整 C# OCR 教學

是否曾需要從圖像辨識文字卻不確定該選擇哪個函式庫？你並不孤單。在許多實務應用——支出追蹤、收據掃描或文件歸檔——可靠地提取文字是第一道關卡。

在本教學中，我們將一步步說明 **如何提取文字**、取得其邊界框，最後使用 Aspose.OCR for .NET **將收據轉換為 JSON**。完成後，你將擁有一個獨立的 C# 專案，能將收據照片轉換為包含信心分數與座標的整齊 JSON 檔案。

## 需要的環境

- **.NET 6.0 SDK**（或任何更新的版本）。舊版框架亦可使用，但 .NET 6 是現代函式庫的最佳選擇。
- **Visual Studio 2022** 或搭配 C# 擴充功能的 VS Code。
- **Aspose.OCR for .NET** NuGet 套件（`Aspose.OCR` 與 `Aspose.OCR.Output`）。可透過套件管理員主控台安裝：

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Output
```

- 範例收據影像（例如 `receipt.jpg`），放置於稍後會參考的資料夾中。

就這樣——不需要額外的 SDK、也不需要原生二進位檔，僅使用純受管理的程式碼。

## 步驟 1：建立新 Console 專案

首先，建立一個 console 應用程式。這是測試 OCR 而不需 UI 負擔的最快方式。

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later.
        }
    }
}
```

> **小技巧：** 保持專案資料夾整潔；建立名為 `Resources` 的子資料夾，並將 `receipt.jpg` 放入其中。這樣路徑處理就不會麻煩。

## 步驟 2：載入收據影像

現在我們真正開始 **從圖像辨識文字**。第一步是將 OCR 引擎指向該檔案。

```csharp
// Inside Main()
string imagePath = @"Resources/receipt.jpg";
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    Image = ImageStream.FromFile(imagePath)
};

Console.WriteLine("✅ Image loaded successfully.");
```

為什麼要把載入包在簡單的存在性檢查裡？因為在正式環境中，你常會處理可能遺失或損壞的使用者上傳檔案。提前捕捉問題可避免之後出現難以理解的例外。

## 步驟 3：執行 OCR – **從圖像辨識文字**

將影像載入記憶體後，我們請 Aspose **從圖像辨識文字**。此操作為同步，並回傳豐富的結果集合。

```csharp
// Still inside Main()
try
{
    ocrEngine.Recognize();
    Console.WriteLine("🧠 OCR completed.");
}
catch (Exception ex)
{
    Console.WriteLine($"❗ OCR failed: {ex.Message}");
    return;
}
```

在幕後，Aspose 會執行一個已在數百萬字元上訓練的神經網路。引擎會填充 `ocrEngine.Text`、`ocrEngine.RecognitionResult`，以及包含座標的 `OcrRegion` 物件集合。這正是下一步所需的資訊。

## 步驟 4：**如何提取文字** – 取得原始字串

如果你只在乎純文字（例如快速搜尋），可以直接從引擎取得：

```csharp
string plainText = ocrEngine.Text;
Console.WriteLine("\n--- Extracted Text ---");
Console.WriteLine(plainText);
```

你會看到 OCR 偵測到段落邊界的換行符號。在許多收據掃描情境下，原始字串已足以使用簡單的正規表達式抽取總金額、日期或商家名稱。

## 步驟 5：**提取文字座標** – 每個字詞的邊界框

通常你需要知道影像上文字的 *位置*——例如在 UI 中標示總金額。Aspose 透過 `OcrRegion` 物件提供此資訊。

```csharp
Console.WriteLine("\n--- Text Coordinates (extract text coordinates) ---");
foreach (var region in ocrEngine.RecognitionResult.Regions)
{
    // Each region represents a word or a line depending on the engine settings.
    string word = region.Text;
    var bounds = region.BoundingBox; // X, Y, Width, Height
    Console.WriteLine($"Word: \"{word}\" | Box: X={bounds.X}, Y={bounds.Y}, W={bounds.Width}, H={bounds.Height}");
}
```

請注意，我們在每個已辨識的區段上迴圈 **提取文字座標**。座標是相對於原始影像的，因此可在圖形畫布或 HTML `<canvas>` 元素上疊加顯示。

## 步驟 6：**將收據轉換為 JSON** – 儲存詳細結果

現在進入將所有結果結合的步驟：我們需要一個機器可讀的結構，包含文字、信心分數與邊界框。Aspose 提供的 `JsonSaveOptions` 讓此工作變得輕鬆。

```csharp
// Define where the JSON will be saved
string jsonPath = @"Resources/receipt.json";

// Configure JSON options to keep confidence and bounding boxes
JsonSaveOptions jsonOptions = new JsonSaveOptions
{
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};

// Save the OCR result
ocrEngine.Save(jsonPath, jsonOptions);
Console.WriteLine($"\n💾 Detailed OCR results saved to {jsonPath}");
```

產生的檔案大致如下（為簡潔起見已裁剪）：

```json
{
  "Regions": [
    {
      "Text": "Store",
      "Confidence": 0.99,
      "BoundingBox": { "X": 45, "Y": 120, "Width": 80, "Height": 20 }
    },
    {
      "Text": "Total",
      "Confidence": 0.97,
      "BoundingBox": { "X": 300, "Y": 560, "Width": 70, "Height": 22 }
    }
    // ... more regions ...
  ]
}
```

現在你已擁有一個 **將收據轉換為 JSON** 的產物，可供下游服務使用——例如費用報告 API、分析管線，或是簡易的 UI 來在每個字詞周圍繪製矩形。

## 完整範例程式

將所有步驟組合起來，以下是完整的 `Program.cs`，可直接複製貼上至你的專案：

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image
            // -------------------------------------------------
            string imagePath = @"Resources/receipt.jpg";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            OcrEngine ocrEngine = new OcrEngine
            {
                Image = ImageStream.FromFile(imagePath)
            };
            Console.WriteLine("✅ Image loaded.");

            // -------------------------------------------------
            // 2️⃣ Run OCR – recognize text from image
            // -------------------------------------------------
            try
            {
                ocrEngine.Recognize();
                Console.WriteLine("🧠 OCR completed.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❗ OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 3️⃣ Extract plain text (how to extract text)
            // -------------------------------------------------
            Console.WriteLine("\n--- Extracted Text ---");
            Console.WriteLine(ocrEngine.Text);

            // -------------------------------------------------
            // 4️⃣ Get coordinates (extract text coordinates)
            // -------------------------------------------------
            Console.WriteLine("\n--- Text Coordinates ---");
            foreach (var region in ocrEngine.RecognitionResult.Regions)
            {
                var box = region.BoundingBox;
                Console.WriteLine($"Word: \"{region.Text}\" | Box: X={box.X}, Y={box.Y}, W={box.Width}, H={box.Height}");
            }

            // -------------------------------------------------
            // 5️⃣ Save detailed JSON (convert receipt to json)
            // -------------------------------------------------
            string jsonPath = @"Resources/receipt.json";
            JsonSaveOptions jsonOptions = new JsonSaveOptions
            {
                IncludeConfidence = true,
                IncludeBoundingBoxes = true
            };
            ocrEngine.Save(jsonPath, jsonOptions);
            Console.WriteLine($"\n💾 JSON saved at {jsonPath}");
        }
    }
}
```

執行程式（`dotnet run`）並觀察主控台輸出。開啟 `Resources/receipt.json` 以驗證結構。

## 常見問題與邊緣情況

- **如果影像模糊怎麼辦？**  
  Aspose OCR 在 300 dpi 或以上的解析度下表現最佳。若信心分數偏低，可在送入引擎前先套用銳化濾鏡。

- **我可以辨識多種語言嗎？**  
  可以。於呼叫 `Recognize()` 前設定 `ocrEngine.Language = Language.English | Language.Spanish;`。

- **如何只輸出數字（例如總金額）？**  
  取得純文字後，可對 `ocrEngine.Text` 使用正規表達式如 `\d+\.\d{2}`。因為已擁有座標，能將匹配的字串映射回其區域以進行視覺標示。

- **JSON 格式可以自訂嗎？**  
  `JsonSaveOptions` 類別提供多個旗標可設定。若需完全自訂的結構，可遍歷 `ocrEngine.RecognitionResult.Regions`，並使用 `System.Text.Json` 自行序列化物件。

## 結論

我們剛剛示範了如何在 C# 中使用 Aspose.OCR **從圖像辨識文字**、**提取文字**、取得 **提取文字座標**，最後 **將收據轉換為 JSON**。整個流程皆在一個易於執行的 console 應用程式中完成，非常適合作為原型或大型系統的建構模組。

接下來的步驟？可將 JSON 輸入前端以繪製邊界框，或將輸出接入費用報告服務。你也可以嘗試不同的影像格式（PNG、TIFF）或批次處理整個收據資料夾。

對 OCR、Aspose 或 JSON 處理還有其他問題嗎？在下方留下評論，我們祝你編程愉快！ 

![從圖像辨識文字的收據範例圖](receipt.jpg "收據圖示範例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}