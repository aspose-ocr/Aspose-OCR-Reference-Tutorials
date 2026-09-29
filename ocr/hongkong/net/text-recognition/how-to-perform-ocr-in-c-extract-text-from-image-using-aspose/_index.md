---
category: general
date: 2026-02-16
description: 如何在 C# 中快速執行 OCR – 只需幾個簡單步驟，即可學會使用 Aspose OCR 函式庫從圖像提取文字。
draft: false
keywords:
- how to perform OCR
- extract text from image
- Aspose OCR C#
- OCR JSON output
- image text extraction
language: zh-hant
og_description: 如何在 C# 中執行 OCR？跟隨此逐步教學，使用 Aspose OCR 從圖像提取文字並取得 JSON 結果。
og_title: 如何在 C# 中執行 OCR – 快速指南
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 如何在 C# 中執行 OCR – 使用 Aspose OCR 從圖像提取文字
url: /zh-hant/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image-using-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中執行 OCR – 使用 Aspose OCR 從圖像提取文字

有沒有想過在 C# 中 **如何執行 OCR** 而不讓自己抓狂？你並不孤單。許多開發人員在需要從掃描的表格、收據或手寫筆記中提取文字時會卡關。好消息是？使用 Aspose OCR，你只需幾行程式碼就能 **從圖像提取文字**。

在本教學中，我們將逐步示範一個完整、可直接執行的範例，說明如何載入語言模型、提供圖像、執行辨識引擎，並將結果序列化為 JSON。完成後，你將擁有一段可重複使用的程式碼片段，能直接嵌入任何 .NET 專案，並附上實務情境的實用技巧。

## 你需要的條件

- .NET 6.0 或更新版本（程式碼同樣適用於 .NET Framework，但建議使用 .NET 6 以上）
- 有效的 Aspose.OCR NuGet 套件（`Install-Package Aspose.OCR`）
- 包含欲讀取文字的圖像檔案（JPEG、PNG、BMP 等）
- 基本的 C# 開發環境（Visual Studio、Rider 或 VS Code）

就這樣——不需要額外的 OCR 引擎、也不需要原生 DLL，僅使用乾淨的受管理程式庫。

## 步驟 1：建立 OCR 引擎實例 – 如何執行 OCR

首先需要建立一個 `OcrEngine` 物件。可以把它想像成負責繁重運算的大腦。

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **為什麼這一步很重要：** `OcrEngine` 包含所有設定選項。沒有它，你無法告訴函式庫使用哪種語言或從哪裡取得圖像。

## 步驟 2：載入語言模型 – 從圖像提取文字

Aspose OCR 內建多種語言套件。對於大多數英文文件，你會載入內建的 English 模型。

```csharp
// Load the English language model
ocrEngine.LoadLanguage(LanguageModel.English);
```

> **專業提示：** 若需辨識法文、德文或自訂語言，請將 `LanguageModel.English` 替換為相應的列舉值，或載入自訂模型檔案。

## 步驟 3：提供要處理的圖像 – 如何執行 OCR

現在將引擎指向你想要讀取的檔案。`ImageStream.FromFile` 輔助方法會將圖像讀取為 OCR 引擎可理解的格式。

```csharp
// Supply the image (replace the path with your own file location)
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.jpg");
```

> **特殊情況：** 大尺寸圖像（>5 MB）會降低處理速度。建議在送入引擎前先調整大小或壓縮。

## 步驟 4：執行辨識 – 從圖像提取文字

所有設定完成後，即可執行 OCR 操作。`Recognize` 方法會回傳一個 `OcrResult` 物件，內含文字、邊界框與信心分數。

```csharp
// Perform OCR and capture the result
OcrResult ocrResult = ocrEngine.Recognize();
```

> **底層發生了什麼？** 引擎執行一個已在數百萬字元上訓練的神經網路，然後將每個偵測到的字形映射為 Unicode 文字。

## 步驟 5：將結果轉換為 JSON – 如何執行 OCR

大多數現代 API 皆接受 JSON，因此我們將結果序列化。`ToJson` 擴充方法會產生格式良好的字串。

```csharp
// Serialize the OCR result to JSON
string jsonResult = ocrResult.ToJson();
```

典型的 JSON 負載如下（為簡潔起見已截斷）：

```json
{
  "Text": "Invoice #12345\nDate: 01/02/2026\nTotal: $250.00",
  "Words": [
    {
      "Value": "Invoice",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 80, "Height": 20 },
      "Confidence": 0.98
    },
    // ... more words ...
  ]
}
```

> **為什麼使用 JSON？** 它與語言無關、易於記錄，且非常適合傳送至下游服務，如 Elasticsearch 或 REST API。

## 步驟 6：輸出 JSON – 從圖像提取文字

最後，將 JSON 輸出至主控台（或檔案、或資料庫——由你決定）。

```csharp
// Print the JSON result to the console
Console.WriteLine(jsonResult);
```

執行程式後應會顯示完整的 JSON 結構，證明你已成功 **從圖像提取文字**。

## 完整可執行範例

以下是完整程式碼，你可以直接複製貼上至新的 Console 專案。沒有遺漏任何部份——所有所需內容都在此。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create an OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Step 2: Load the English language model for recognition
            ocrEngine.LoadLanguage(LanguageModel.English);

            // Step 3: Provide the image to be processed
            // Replace the path with the actual location of your image file
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.jpg");

            // Step 4: Perform OCR on the image
            OcrResult ocrResult = ocrEngine.Recognize();

            // Step 5: Convert the recognition result to JSON (includes text, bounding boxes, confidence scores)
            string jsonResult = ocrResult.ToJson();

            // Step 6: Output the JSON result
            Console.WriteLine(jsonResult);
        }
    }
}
```

> **預期輸出：** 包含辨識文字、每個單字的邊界框與信心值的 JSON 字串。若圖像清晰且語言模型相符，信心分數通常會高於 0.90。

## 常見問題與注意事項

- **如果圖像被旋轉了怎麼辦？**  
  Aspose OCR 能自動偵測方向，但為取得最佳效果，建議在傳入引擎前使用 `System.Drawing` 或 `ImageSharp` 先行旋轉圖像。

- **可以直接處理 PDF 嗎？**  
  目前不支援。請先將每頁 PDF 轉為圖像（例如使用 Aspose.PDF），再將這些圖像送入 OCR 引擎。

- **如何處理多頁表單？**  
  逐一迭代每頁圖像，執行相同步驟，並將 JSON 結果彙總至單一集合。

- **有沒有方法只輸出純文字？**  
  有——若只需要合併後的字串，可使用 `ocrResult.Text` 屬性取代 `ToJson()`。

## 生產環境 OCR 專業技巧

1. **快取語言模型** – 載入模型成本不高，但若每秒處理上百張圖像，建議保留單一 `OcrEngine` 實例，而非每次都重新建立。  
2. **調整信心門檻** – 篩除 `Confidence < 0.80` 的單字，以降低噪聲。  
3. **批次處理** – 面對大量工作負載時，可將圖像路徑排入佇列，並使用 `Task.Run` 非同步處理。  
4. **日誌記錄** – 將原始 JSON 與原始圖像一起保存以作稽核追蹤；在除錯辨識錯誤時相當有價值。

## 結論

現在你已掌握使用 Aspose OCR 函式庫在 C# 中 **執行 OCR** 並 **從圖像檔案提取文字** 的完整端對端解決方案。此範例一步步說明了引擎建立、語言載入、圖像輸入、辨識、JSON 序列化與輸出——全部在一個可執行的程式中完成。

接下來要做什麼？試著將 English 模型換成其他語言、測試不同的圖像格式，或將 JSON 負載整合至搜尋索引。只要有這些基礎，你就能應對任何文字提取的挑戰。

祝程式開發順利，願你的 OCR 結果永遠精準！ 

![說明如何在 C# 中使用 Aspose OCR 函式庫執行 OCR 的示意圖](https://example.com/ocr-diagram.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}