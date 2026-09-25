---
category: general
date: 2026-01-15
description: 使用 Aspose OCR 在 C# 中將圖像轉換為 JSON。了解如何從圖像提取文字、取得 JSON 邊界框，並辨識收據圖像。
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: zh-hant
og_description: 使用 Aspose OCR 在 C# 中將圖像轉換為 JSON。一步一步的指南，從圖像中提取文字，識別收據圖像，並獲取 JSON 邊界框。
og_title: 使用 Aspose OCR C# 指南將圖像轉換為 JSON
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: 使用 Aspose OCR C# 指南將圖像轉換為 JSON
url: /zh-hant/net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR C# 將影像轉換為 JSON 教學

有沒有曾經需要 **將影像轉換為 JSON**，卻不確定哪個函式庫能同時提供原始文字與精確的字詞座標？你並不孤單。許多開發者在嘗試從影像檔（尤其是收據）提取文字，同時需要機器可讀的 JSON 資料以供後續處理時，常會卡在這裡。

在本教學中，我們將逐步說明一個完整的 **Aspose OCR C# 範例**，示範如何從影像中提取文字、辨識收據影像，並為每個字詞輸出 **JSON 邊界框**。完成後，你將擁有一個可直接執行的主控台應用程式，會印出格式化好的 JSON 字串，供任何 API、資料庫或分析管線使用。

> **你將學會**  
> • 一個完整可運作的 C# 專案，能 **將影像轉換為 JSON**  
> • 為何要啟用 `IncludeBoundingBoxes`（這是取得 `json bounding boxes` 的關鍵）之深入了解  
> • 處理不同影像格式與語言的技巧  

讓我們開始吧。

---

## 所需條件

在深入程式碼之前，請確保已安裝以下前置條件：

- **.NET 6.0 SDK**（或更新版本）– 此程式碼以 .NET 6 為目標，但亦可在 .NET Framework 4.7+ 上執行。  
- **Aspose.OCR for .NET** NuGet 套件 – 可使用 `dotnet add package Aspose.OCR` 取得。  
- 一張範例收據影像（`receipt.jpg`），放在專案可參照的資料夾中。  
- Visual Studio 2022、VS Code，或任何你偏好的 IDE。

不需要其他外部服務；所有操作皆在本機執行。

## 影像轉換為 JSON – 概觀

核心概念很簡單：載入影像，指示 Aspose OCR 辨識英文（或任何支援的語言），要求包含邊界框，最後以 **JSON** 格式取得結果。此函式庫負責所有繁重工作——OCR、版面分析與 JSON 序列化。

以下是一個高階流程圖（想像成一張小圖）：

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

這張小圖概括了我們即將實作的完整流程。

## 步驟 1：建立專案並安裝 Aspose OCR

首先，建立一個新的主控台專案，並加入 Aspose OCR 套件。

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **專業提示：** 若使用 Visual Studio，右鍵點擊專案 → *Manage NuGet Packages* → 搜尋 **Aspose.OCR**，然後安裝最新的穩定版（目前為 23.12）。

## 步驟 2：載入欲辨識的影像

我們將使用 `OcrImage.FromFile` 方法讀取收據影像。請確保路徑指向真實檔案，否則會拋出 `FileNotFoundException`。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

如果影像與 `.csproj` 位於同一目錄，只需使用 `"receipt.jpg"` 即可。

## 步驟 3：設定 OCR 選項以取得 JSON 邊界框

當我們啟用 `OutputFormat = OutputFormat.Json` **以及** `IncludeBoundingBoxes = true` 時，魔法就會發生。前者告訴 Aspose 以 JSON 序列化結果，後者則為每個字詞加入 `x`、`y`、`width`、`height`——正是取得 `json bounding boxes` 所需的資訊。

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

若需要更高解析度或不同語言，也可以調整 `ocrOptions.Dpi` 或 `ocrOptions.Language`。

## 步驟 4：執行辨識 – 從影像中提取文字

現在呼叫 `Recognize`。此方法會回傳一個 `OcrResult` 物件，內含 JSON 字串、原始文字等資訊。

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

若需處理其他語言，請將 `Language.English` 替換為 `Language.Spanish`、`Language.French` 等。Aspose 內建支援超過 30 種語言。

## 步驟 5：輸出結果 – 你的 JSON Payload

最後，我們將 JSON 印到主控台。實際應用中，你可能會將其寫入檔案或傳送至服務。

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

執行程式後，應會產生類似下方片段的 JSON 文件。

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

請注意，每個字詞現在都帶有 **JSON 邊界框**——非常適合用於 UI 疊加或後續解析器。

## 完整範例程式碼

以下是完整、可直接複製貼上的程式。沒有隱藏部分，也不會呼叫外部服務——純粹的 C#。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **注意事項：**  
> • **檔案路徑錯誤** – 請再次確認影像位置。  
> • **缺少 NuGet 套件** – 確認已引用 `Aspose.OCR`。  
> • **不支援的影像格式** – 請使用 JPEG、PNG、BMP 或 TIFF，以獲得最佳效果。

## 常見問題與特殊情況

### 我可以將 **PDF 頁面** 轉換為 JSON 而不是 JPEG 嗎？

可以。先將 PDF 頁面轉為影像（例如使用 `Aspose.PDF`），再將該影像送入相同的 OCR 流程。JSON 輸出會相同，因為 OCR 階段只關心點陣資料。

### 如果收據模糊怎麼辦？

在 `ocrOptions` 中提升 DPI。例如：

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

較高的 DPI 可能會增加記憶體使用量，需在品質與效能之間取得平衡。

### 我需要在同一張收據上使用 **多種語言**（例如 English + Spanish）。

可以傳入語言陣列：

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

### 如何將 JSON 寫入檔案？

只需將 `Console.WriteLine` 那一行改為：

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

## 視覺摘要

![將影像轉換為 JSON 範例](convert-image-to-json.png "將影像轉換為 JSON 範例")

*此螢幕截圖顯示執行示範後，主控台輸出的 JSON Payload。*

## 結論

我們剛剛示範了如何使用 Aspose OCR 在 C# 中 **將影像轉換為 JSON**。透過設定 `OutputFormat` 與 `IncludeBoundingBoxes`，即可 **從影像提取文字**、**辨識收據影像**，並為每個字詞取得精確的 **JSON 邊界框**。完整且可執行的程式碼已在上方片段中提供，現在即可直接放入任何 .NET 專案使用。

接下來可以做什麼？試著將 JSON 輸入前端檢視器，以高亮顯示每個字詞，或將資料送入機器學習模型，對收據的項目進行分類。你也可以嘗試其他語言、更高 DPI 設定，或在迴圈中批次處理多張影像。

如果遇到任何問題，請記得檔案路徑、 DPI 與語言陣列的相關提示。歡迎在你為此示範建立的 GitHub 倉庫留下評論或開啟議題。祝開發順利，盡情將圖片轉換為結構化的 JSON！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}