---
category: general
date: 2026-02-17
description: 如何在 C# 中快速執行 OCR 並將圖像轉換為 JSON。跟隨本 C# OCR 教學，從圖像中擷取文字並將版面儲存為 JSON。
draft: false
keywords:
- how to perform OCR
- convert image to json
- c# ocr tutorial
- extract text image c#
- load image file c#
language: zh-hant
og_description: 如何在 C# 中執行 OCR？本指南將示範如何將圖像轉換為 JSON、在 C# 中從圖像提取文字，以及載入圖像檔案進行 OCR。
og_title: 如何在 C# 中執行 OCR – 將圖像轉換為 JSON
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中執行 OCR – 圖片轉 JSON 指南
url: /zh-hant/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-json-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中執行 OCR – 圖像轉 JSON 指南

有沒有想過 **如何在 C# 中執行 OCR** 於收據、發票或任何掃描文件？你並非唯一有此疑問的人。許多開發者在需要提取文字 *並* 保留版面配置時，常會卡住，且不想花上數小時編寫自訂解析器。  

在本教學中，我們將完整示範 **c# ocr tutorial**，說明如何執行 OCR、**convert image to json**，以及將結果儲存以供後續分析。完成後，你將擁有一個可直接執行的 console 應用程式，能在 C# 中載入圖像檔案、提取文字，並寫入包含座標、信心分數與原始文字的詳細 JSON 檔案。

## 前置條件 — 您需要的項目

- .NET 6 SDK 或更新版本（程式碼亦可在 .NET Core 上執行）  
- Visual Studio 2022 或您偏好的任何編輯器  
- Aspose OCR 授權（可先使用免費試用版）  
- 範例圖像，例如 `receipt.png`，放置於可參考的資料夾中  

就這樣——除了 `Aspose.OCR` 之外不需要額外的 NuGet 套件。只要備妥上述項目，即可開始。

## 如何執行 OCR 並取得 JSON 輸出

使用 Aspose 執行 **how to perform OCR** 的核心相當簡單：建立 `OcrEngine`、提供圖像串流、呼叫 `Recognize`，最後將 `OcrResult` 序列化為 JSON。讓我們一步一步拆解說明。

### 步驟 1：安裝 Aspose OCR NuGet 套件

在專案資料夾的終端機中執行：

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** 使用 `--version` 參數鎖定最新的穩定版（例如 `23.9.0`），可確保建置可重現。

### 步驟 2：建立 Console 專案骨架

如果尚未有專案，先建立一個：

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
```

現在你已擁有 `Program.cs` 檔案，可放入 **load image file c#** 的程式碼並啟動 OCR 流程。

### 步驟 3：撰寫完整的 OCR‑to‑JSON 程式碼

以下是完整、可直接執行的程式。將它複製貼上至 `Program.cs`。每一行皆有註解，說明 *為何* 需要此段程式。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonOutput
{
    static void Main()
    {
        // ---------------------------------------------------------
        // 1️⃣  Initialize the OCR engine – this object holds
        //     language settings, recognition options, etc.
        // ---------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------------------------------------------------------
        // 2️⃣  Load the image you want to analyze.
        //     This demonstrates **load image file c#** in a clean way.
        // ---------------------------------------------------------
        // Replace the path with the actual location of your receipt.png
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");
        ImageStream image = ImageStream.FromFile(imagePath);

        // ---------------------------------------------------------
        // 3️⃣  Perform the recognition.
        //     The engine returns an OcrResult containing text,
        //     confidence scores, and layout information.
        // ---------------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // ---------------------------------------------------------
        // 4️⃣  Convert the result to a detailed JSON string.
        //     This is the heart of **convert image to json**.
        // ---------------------------------------------------------
        string jsonResult = ocrResult.ToJson();

        // ---------------------------------------------------------
        // 5️⃣  Save the JSON to disk – you can later import this into
        //     databases, analytics pipelines, or UI components.
        // ---------------------------------------------------------
        string jsonPath = Path.Combine(
            Environment.CurrentDirectory, "receipt.json");
        File.WriteAllText(jsonPath, jsonResult);

        // ---------------------------------------------------------
        // 6️⃣  Let the user know we’re done.
        // ---------------------------------------------------------
        Console.WriteLine("JSON with layout saved to " + jsonPath);
    }
}
```

#### 程式碼功能說明

| Step | 為何重要 |
|------|----------|
| **Initialize OcrEngine** | 設定預設語言（英文）並準備內部模型。 |
| **Load image file** | 使用 `ImageStream.FromFile` 可確保圖像以 Aspose 所期望的格式讀取。 |
| **Recognize** | 執行核心工作——像素分析、字元分割與字典查詢。 |
| **ToJson** | 產生包含邊界框、信心分數與原始文字的結構化輸出。 |
| **WriteAllText** | 將 JSON 寫入檔案，以便與其他服務共享。 |
| **Console.WriteLine** | 提供即時回饋——在終端機執行時相當方便。 |

> **Watch out:** 若圖像尺寸過大，建議先行縮小以提升速度與記憶體使用率。Aspose 提供可於 `ImageStream` 上呼叫的 `Resize` 方法。

### 步驟 4：執行應用程式並驗證輸出

在終端機中執行：

```bash
dotnet run
```

你應該會看到：

```
JSON with layout saved to C:\Path\To\OcrJsonDemo\receipt.json
```

在任意編輯器中開啟 `receipt.json`，會看到類似以下內容：

```json
{
  "Pages": [
    {
      "Blocks": [
        {
          "Text": "Total: $12.34",
          "Confidence": 0.98,
          "BoundingBox": { "X": 120, "Y": 340, "Width": 150, "Height": 30 }
        }
      ]
    }
  ]
}
```

此 JSON 捕捉了 **extract text image c#** 以及版面配置的中繼資料，十分適合後續處理。

## 圖像轉 JSON – 進階應用

既然已了解 **how to perform OCR**，接下來探討在實務專案中可能需要的幾種變化。

### 處理多頁文件

若來源是多頁 PDF 或 TIFF，只需對每一頁迴圈處理：

```csharp
foreach (var pageStream in multiPageImageStreams)
{
    OcrResult result = ocrEngine.Recognize(pageStream);
    // Append each page's JSON to a master list
}
```

### 自訂語言與精度

Aspose 支援超過 40 種語言。若要切換至西班牙語：

```csharp
ocrEngine.Language = Language.Spanish;
```

你也可以調整 `ocrEngine.Settings`，啟用 **auto‑rotate**、**noise removal** 或 **dictionary‑based correction**——這些都能提升取得的 JSON 品質。

### 以易讀格式儲存 JSON

若偏好縮排的 JSON 以提升可讀性：

```csharp
string prettyJson = ocrResult.ToJson(true); // true = formatted
File.WriteAllText(jsonPath, prettyJson);
```

## 載入圖像檔案 C# – 常見陷阱與技巧

當你 **load image file c#** 時，可能會遇到：

- **File not found** – 確認路徑為絕對路徑，或使用 `Path.Combine` 搭配 `Environment.CurrentDirectory`。  
- **Unsupported format** – Aspose 支援 PNG、JPEG、BMP、TIFF 與 PDF。若為 RAW 格式，請先轉換。  
- **Large file memory pressure** – 使用 `ImageStream.FromFile(path, maxSizeInKB)` 於載入時即縮小尺寸。

提前處理這些問題，可避免在 OCR 流程後期遭遇難以理解的例外。

## 提取文字圖像 C# – 驗證結果

取得 JSON 後，若只需要純文字：

```csharp
var ocrResult = ocrEngine.Recognize(image);
string plainText = ocrResult.Text; // Simple string with line breaks
Console.WriteLine(plainText);
```

此片段示範 **extract text image c#**，不含版面細節，適合快速搜尋或記錄。

![展示 OCR 工作流程 – 如何執行 OCR、圖像轉 JSON 以及提取文字圖像 C#](/images/ocr-workflow.png "如何執行 OCR 工作流程")

*圖片說明：「如何執行 OCR 工作流程圖，說明圖像轉 JSON 以及提取文字圖像 C#」*  
*(此圖為佔位圖，發佈時請替換為實際流程圖。)*

## 結論

我們已從頭到尾說明 **how to perform OCR** 在 C# 中的完整流程，示範如何 **convert image to JSON**，並闡述 **load image file c#** 與 **extract text image c#** 的細節。完整程式碼可直接嵌入任何 .NET 專案，且 JSON 輸出同時提供原始文字與精確的版面資料，方便後續分析。

接下來可以嘗試將 JSON 匯入資料庫、在 UI 上視覺化邊界框，或串接多次 OCR 以進行批次處理。亦可探索 Aspose 其他功能，如手寫辨識或條碼偵測，皆能自然融入同一條流水線。

若遇到任何問題，請回顧「Load Image File C#」章節的除錯技巧，或參考 Aspose 完備的文件以取得進階設定。祝開發順利，享受將圖像轉換為結構化資料的樂趣！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}