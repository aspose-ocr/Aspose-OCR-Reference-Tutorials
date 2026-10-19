---
category: general
date: 2026-02-28
description: 如何在 C# 中使用 Aspose OCR 執行 OCR – 學習如何從影像提取文字，將影像轉換為 JSON 或 XML，只需幾個步驟。
draft: false
keywords:
- how to run OCR
- extract text from image
- convert image to json
- convert image to xml
- how to extract text
language: zh-hant
og_description: 如何在 C# 中使用 Aspose OCR 執行光學字符識別 – 探索如何從圖片中提取文字，並將圖片轉換為 JSON 或 XML，並附有即用範例。
og_title: 如何在 C# 中使用 Aspose OCR 執行 OCR – 完整指南
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 如何在 C# 中使用 Aspose OCR 執行 OCR – 完整指南
url: /zh-hant/net/text-recognition/how-to-run-ocr-with-aspose-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose OCR 執行 OCR – 完整指南

如果你想了解 **如何在 C# 中執行 OCR** 以辨識收據影像，來到這裡就對了。在本教學中，我們將一步步說明 **從影像擷取文字**，以及如何使用 Aspose OCR **將影像轉換為 JSON** 或 **將影像轉換為 XML**，全部都在同一個獨立程式中完成。

想像一下，你正在開發一個費用追蹤應用程式，需要從拍攝的收據中抽取每筆項目。手動輸入每筆資料既繁瑣又容易出錯，對吧？完成本指南後，你將擁有一段可重複使用的程式碼，能讀取任意影像、回傳結構化文字，並同時提供 JSON 與 XML 兩種格式，方便後續處理。

## 前置條件

在開始之前，請確保你已具備以下環境：

- .NET 6.0 SDK 或更新版本（此程式碼亦相容於 .NET Framework 4.8）
- Visual Studio 2022（或任何你慣用的編輯器）
- 已安裝 **Aspose.OCR** NuGet 套件（`Install-Package Aspose.OCR`）
- 一張範例影像（例如 `receipt.png`），放在可參照的資料夾內

不需要額外的設定；此函式庫已內建所有必要的 OCR 模型。

![Receipt image for OCR processing – how to run OCR](receipt.png)

> *替代文字：用於 OCR 處理的收據影像 – 如何執行 OCR*

## 步驟說明實作

以下我們將解決方案切分為多個邏輯區塊。每一步都說明 **為什麼** 要這樣做，而不只是 **程式碼長什麼樣**。

### 1️⃣ 初始化 OCR 引擎 – **如何執行 OCR** 的基礎

`OcrEngine` 類別是入口點。建立實例時會載入內部語言模型，並為辨識做好準備。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        // This object holds the OCR model and settings.
        var ocrEngine = new OcrEngine();
```

> **小技巧：** 在多張影像間重複使用同一個 `OcrEngine` 可以減少記憶體開銷，提升批次處理速度。

### 2️⃣ 載入影像 – **從影像擷取文字** 的核心

Aspose OCR 使用自家的 `Image` 包裝類別。使用 `using` 陳述式可確保檔案句柄即時釋放。

```csharp
        // Step 2: Load the image you want to analyze
        // Replace YOUR_DIRECTORY with the actual path on your machine.
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");
```

若影像為其他格式（BMP、TIFF、PDF），相同的 `Load` 方法亦能直接處理，無需額外轉換。

### 3️⃣ 執行 OCR 辨識 – **如何執行 OCR** 的核心

呼叫 `Recognize` 會完成繁重的工作：版面分析、字元切割以及語言特定的分類。

```csharp
        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);
```

回傳的 `OcrResult` 包含原始文字、信心分數，以及可序列化的詳細版面樹狀結構。

### 4️⃣ 影像轉 JSON – **將影像轉換為 json** 的直接方式

JSON 非常適合 Web API 或 NoSQL 資料庫。`ToJson` 方法會回傳格式化好的字串，除錯時相當方便。

```csharp
        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);
```

典型的 JSON 輸出如下（為簡潔起見已截斷）：

```json
{
  "Text": "Total 12.34",
  "Blocks": [
    {
      "Text": "Total",
      "Confidence": 0.98,
      "Bounds": { "X": 10, "Y": 150, "Width": 45, "Height": 15 }
    },
    {
      "Text": "12.34",
      "Confidence": 0.97,
      "Bounds": { "X": 60, "Y": 150, "Width": 30, "Height": 15 }
    }
  ]
}
```

現在你可以直接將此 JSON 送到 REST 端點，或儲存至 Azure Cosmos DB。

### 5️⃣ 影像轉 XML – 需要 **將影像轉換為 xml** 時的做法

某些舊有系統仍以 XML 為主。Aspose 提供 `ToXml` 方法，可產生符合 schema 的乾淨表示。

```csharp
        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

XML 範例片段：

```xml
<OcrResult>
  <Text>Total 12.34</Text>
  <Blocks>
    <Block>
      <Text>Total</Text>
      <Confidence>0.98</Confidence>
      <Bounds X="10" Y="150" Width="45" Height="15" />
    </Block>
    <Block>
      <Text>12.34</Text>
      <Confidence>0.97</Confidence>
      <Bounds X="60" Y="150" Width="30" Height="15" />
    </Block>
  </Blocks>
</OcrResult>
```

兩種格式保留相同的階層資料，你可以依下游流程的需求自行選擇。

## 常見問題與可靠擷取文字的技巧

即使使用功能強大的函式庫，實務影像仍會出現各種挑戰。以下列出三種常見問題與對應解決方案。

### 📏 低解析度影像

**為何重要：** 小字體容易合併，導致信心分數下降。  
**解決方法：** 先前處理影像——使用 `Image.Resize` 放大，或在辨識前套用銳化濾鏡。

```csharp
using var highRes = image.Resize(2.0, InterpolationMode.HighQualityBicubic);
var result = ocrEngine.Recognize(highRes);
```

### 🌈 低對比度

**為何重要：** 亮文字搭配暗背景會干擾分割演算法。  
**解決方法：** 反轉顏色或透過 `Image.AdjustBrightnessContrast` 調整亮度/對比度。

```csharp
image.AdjustBrightnessContrast(brightness: 30, contrast: 40);
```

### 📄 多語言文件

**為何重要：** 預設語言模型為英文，混合語言會產生雜訊。  
**解決方法：** 在辨識前設定 `ocrEngine.Language = OcrLanguage.Multilingual;`

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

處理好這些邊緣情況後，**如何從任何影像擷取文字** 就能變成可靠的常規作業，而非賭博。

## 完整範例（可直接複製貼上）

以下是完整程式碼，已備妥可直接編譯執行。只要把 `YOUR_DIRECTORY` 替換成影像所在路徑，然後按 F5 即可。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Optional: improve accuracy for low‑contrast images
        // ocrEngine.Language = OcrLanguage.Multilingual;

        // Step 2: Load the image you want to analyze
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");

        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);

        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

**預期的主控台輸出**（為易讀性已排版）會同時顯示 JSON 與 XML 結構，內含擷取的文字與邊框座標。

## 重點回顧

- **如何在 C# 中使用 Aspose OCR 執行 OCR**
- 步驟式流程 **從影像擷取文字**
- 兩種序列化方式：**將影像轉換為 json** 與 **將影像轉換為 xml**
- 處理低解析度、低對比度與多語言情境的技巧
- 完整、可直接貼上的程式碼範例，適用於任何 .NET 專案

## 接下來可以做什麼？

現在你已能 **從影像擷取文字** 並取得結構化資料，以下是幾個後續應用想法：

- 將 JSON 送入 Azure Function，將收據儲存至 Cosmos DB。
- 使用 XML 輸出填充既有的 SOAP 會計系統。
- 結合 Aspose OCR 與機器學習模型，自動分類費用類型。

盡情實驗吧——把 `receipt.png` 換成發票、名片或手寫筆記。相同的模式可跨各種影像類型使用。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}