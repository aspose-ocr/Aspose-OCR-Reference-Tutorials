---
category: general
date: 2026-01-13
description: c# OCR 教學，示範如何從圖像提取文字、載入圖像進行 OCR，並使用 Aspose OCR 格式化 JSON 輸出。學習將物件序列化為
  JSON。
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- format json output
- serialize object to json
- load image for ocr
language: zh-hant
og_description: c# OCR 教學，帶你一步步從圖像提取文字、載入圖像進行 OCR，並使用 Aspose OCR 格式化 JSON 輸出。
og_title: c# OCR 教學 – 提取文字與格式化 JSON
tags:
- OCR
- C#
- JSON
title: C# OCR 教學 – 從圖像中提取文字並獲取格式化的 JSON
url: /zh-hant/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-get-formatted-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – 從影像擷取文字並格式化 JSON 輸出

有沒有想過在 C# 專案中**從影像檔案擷取文字**，卻不必與低階像素處理糾纏？這就是這篇 *c# ocr tutorial* 要解決的問題。只要幾分鐘，你就會看到如何**載入影像進行 OCR**、執行 Aspose OCR，並**格式化 JSON 輸出**，讓資料直接供 API 或資料庫使用。

我們會逐行說明程式碼，解釋每個部份的意義，甚至示範你應該得到的完整 JSON。完成後，你將擁有一個可直接執行的 console 應用程式，能把發票 PNG 轉成整齊、縮排的 JSON。沒有多餘說明，只有實用解決方案，隨時可放入任何 .NET 6+ 專案。

## 本 c# ocr tutorial 內容

- 安裝 Aspose.OCR NuGet 套件  
- 載入影像檔案以供 OCR 處理  
- 辨識英文文字（或任何支援語言）  
- **將 OCR 結果序列化為 JSON**，並使用美化印出  
- 在 console 顯示 JSON，必要時亦可儲存  

只需要對 C# 有基本了解以及最近的 .NET SDK。除此之外不需要其他前置條件。如果你想**從影像檔案擷取文字**，無論是發票、收據或掃描表單，請繼續閱讀。

---

## 步驟 1：設定 c# ocr tutorial 開發環境

在撰寫程式碼之前，先確保已安裝以下工具：

1. **.NET 6 SDK 或更新版本** – 可從 Microsoft 官方網站下載。  
2. **Visual Studio 2022**（Community 版亦可）或任何你喜歡的編輯器。  
3. **Aspose.OCR NuGet 套件** – 在專案資料夾執行 `dotnet add package Aspose.OCR`。

> **小技巧：** 若使用 CI pipeline，請將套件參考加入 `.csproj`，讓建置自動還原。

---

## 步驟 2：載入影像以供 OCR

本教學的第一個實作步驟是取得要處理的影像。Aspose OCR 支援 PNG、JPEG、TIFF 等常見格式。

```csharp
using Aspose.OCR;
using System.Text.Json;

// Replace this with the actual path to your invoice image
string imagePath = @"C:\Invoices\invoice.png";

// Create an OcrImage instance from the file system
OcrImage inputImage = OcrImage.FromFile(imagePath);
```

> **為何重要：** 將影像載入為 `OcrImage` 後，OCR 引擎即可取得位圖資料與 DPI 資訊，提升辨識準確度。若省略此步或提供損毀檔案，將拋出執行時例外。

---

## 步驟 3：從影像擷取文字

現在正式執行 OCR 引擎。`Recognize` 方法會回傳包含原始文字、信心分數與版面資訊的 `OcrResult` 物件。

```csharp
// Initialize the OCR engine – no license needed for a trial run
OcrEngine ocrEngine = new OcrEngine();

// Recognize English text (you can change the language enum if needed)
OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);
```

> **邊緣情況：** 若需處理多語言文件，可分別以不同 `OcrLanguage` 呼叫兩次 `Recognize`，再將結果串接。引擎是執行緒安全的，甚至可以平行處理大量批次。

---

## 步驟 4：將物件序列化為 JSON – 格式化 JSON 輸出

`OcrResult` 只是一個普通的 C# 類別，我們可以直接交給 `System.Text.Json`。啟用 `WriteIndented` 後，輸出即為人類可讀的格式。

```csharp
// Serialize the OCR result with pretty printing
string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
{
    WriteIndented = true
});
```

> **你會得到：** 一段排版整齊的 JSON 字串，內含辨識文字、信心分數與頁面版面資訊。非常適合用於日誌、傳送至 Web 服務，或儲存於 NoSQL 資料庫。

---

## 步驟 5：顯示並（可選）儲存格式化的 JSON

最後，我們把 JSON 輸出到 console。若需要，也可以使用 `File.WriteAllText` 寫入檔案。

```csharp
// Show the JSON in the console
Console.WriteLine(json);

// Optional: Save to a .json file next to the image
string jsonPath = Path.ChangeExtension(imagePath, ".json");
File.WriteAllText(jsonPath, json);
Console.WriteLine($"\nJSON saved to: {jsonPath}");
```

**預期的 console 輸出（為簡潔起見已截斷）：**

```json
{
  "Text": "Invoice #12345\nDate: 2025‑12‑01\nTotal: $250.00",
  "Confidence": 0.97,
  "Pages": [
    {
      "PageNumber": 1,
      "Blocks": [
        {
          "Text": "Invoice #12345",
          "Confidence": 0.99,
          "Rectangle": { "X": 50, "Y": 30, "Width": 200, "Height": 30 }
        }
        // …more blocks…
      ]
    }
  ]
}
```

如果 OCR 引擎找不到任何文字，`Text` 欄位會是空字串，`Confidence` 會是 `0`。這時請檢查影像品質。

---

## 步驟 6：完整可執行範例

將所有程式碼整合如下，直接貼到新的 console 應用程式即可執行：

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonResultDemo
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the source image (replace with your own path)
        string imagePath = @"C:\Invoices\invoice.png";
        OcrImage inputImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Recognize text – this is the core of our c# ocr tutorial
        OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);

        // 4️⃣ Serialize the result with pretty formatting
        string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
        {
            WriteIndented = true
        });

        // 5️⃣ Output to console and optionally write to a file
        Console.WriteLine(json);
        string jsonPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"\nJSON saved to: {jsonPath}");
    }
}
```

在專案資料夾執行 `dotnet run`，即可在 console 看到掃描發票的漂亮 JSON 表示。

---

## 常見問題與技巧（c# ocr tutorial 進階）

| 問題 | 發生原因 | 解決方法 |
|------|----------|----------|
| **空白 `Text` 欄位** | 影像對比度低或旋轉。 | 前置處理影像（提升對比、去斜）或使用 `OcrEngine.ImagePreprocess`。 |
| **`System.DllNotFoundException`** | 缺少 Aspose OCR 原生二進位檔。 | 確認 NuGet 套件已正確還原，且執行環境的架構 (x64/x86) 與 OS 相符。 |
| **大型 PDF 效能下降** | OCR 逐頁順序處理。 | 為每頁建立獨立的 `OcrEngine` 實例並行處理（引擎是執行緒安全的）。 |
| **JSON 過大** | 序列化了所有細節，包括 bounding box。 | 在序列化前先建立只包含 `Text` 與 `Confidence` 的 DTO。 |

> **記得：** 本教學的目標是展示一個乾淨、端到端的流程。之後你可以自行裁剪 JSON 或加入更多中繼資料。

---

## 結論

你剛完成一個**c# ocr tutorial**，從載入影像、**從影像擷取文字**，再到**格式化 JSON 輸出**，最後**將物件序列化為 JSON**。步驟簡單、程式碼即可執行，且 JSON 已完美縮排，方便下游使用。

接下來可以嘗試將 `OcrLanguage.English` 換成 `OcrLanguage.French`，或把收據資料夾以迴圈方式批次處理。也可以探索直接把 JSON 儲存至 Azure Blob Storage，或送入機器學習模型。

若遇到問題，請再次確認影像路徑正確，且已在呼叫 `Recognize` 前載入 Aspose OCR 授權（若有）。祝開發順利，願你的 OCR 結果永遠清晰！ 

*Image illustrating the OCR flow (alt text: "c# ocr tutorial diagram showing load image, recognize text, serialize to JSON")*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}