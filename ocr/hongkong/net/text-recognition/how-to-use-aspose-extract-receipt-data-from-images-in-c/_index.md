---
category: general
date: 2026-04-04
description: 學習如何使用 Aspose 提取收據資料、載入收據影像並對收據影像進行 OCR，並附有完整的 C# 範例。為開發人員提供逐步指南。
draft: false
keywords:
- how to use aspose
- extract receipt data
- how to extract receipt
- load receipt image
- ocr receipt image
language: zh-hant
og_description: 如何使用 Aspose 從掃描的收據圖像中提取收據資料。完整 C# 程式碼、說明與 OCR 收據圖像處理技巧。
og_title: 如何使用 Aspose – 從圖像中提取收據資料
tags:
- Aspose
- OCR
- C#
- Receipt Processing
title: 如何使用 Aspose – 從圖像中提取收據資料（C#）
url: /zh-hant/net/text-recognition/how-to-use-aspose-extract-receipt-data-from-images-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose – 從圖像中提取收據資料（C#）

有沒有想過 **如何使用 Aspose** 從收據照片中提取結構化資訊？你並不是唯一有此疑問的人。無論你是在開發費用追蹤應用程式或是自動化發票錄入，痛點都是相同的：手上只有一張 PNG 或 JPEG 圖片，而你需要商家名稱、日期與總金額，卻不想手動輸入。

事實上，Aspose.OCR 讓整個流程變得輕而易舉。在本教學中，我們將示範如何載入收據圖像、執行 OCR，最後以幾行 C# 程式碼抽取收據資料。完成後，你將擁有一個可執行的主控台程式，直接在螢幕上印出商家、日期與總金額。

> **快速上手：** 若只需要程式碼，直接跳至底部的「完整可執行範例」章節，複製貼上即可。

## 需要的環境

- **.NET 6.0 或更新版本**（此 API 支援 .NET Core 與 .NET Framework）
- **Aspose.OCR for .NET** NuGet 套件（`Install-Package Aspose.OCR`）
- 本機儲存的範例收據圖像（PNG、JPG 或 BMP）
- Visual Studio 2022 或任何支援 C# 專案的編輯器

不需要其他第三方函式庫。唯一的前置條件是對 C# 主控台應用程式有基本認識——只要寫過「Hello World」就可以開始。

## 步驟 1 – 安裝與參考 Aspose.OCR

要 **如何使用 Aspose**，首先需要在專案中加入此函式庫。開啟套件管理員主控台並執行以下指令：

```powershell
Install-Package Aspose.OCR
```

或者使用 NuGet UI 搜尋「Aspose.OCR」並安裝。安裝完成後，於檔案頂部加入所需的命名空間：

```csharp
using Aspose.OCR;
using Aspose.OCR.Structured;
```

> **專業提示：** 請保持 NuGet 套件為最新版本。以今天（2026 年 4 月）為例，最新的穩定版為 23.11.0，已針對高解析度收據的 OCR 效能進行優化。

## 步驟 2 – 載入收據圖像

在 **載入收據圖像** 時，常見的來源有兩種：本機路徑或來自網路請求的串流。此教學中，我們簡化為直接從磁碟讀取：

```csharp
// Step 2: Load the receipt image to be processed
var ocrEngine = new OcrEngine
{
    Language = Language.English // set language for better accuracy
};

ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.png");
```

將 `YOUR_DIRECTORY/receipt.png` 替換為實際的收據檔案路徑。若處理使用者上傳的檔案，可將 `MemoryStream` 傳入 `ImageStream.FromStream`。

> **為什麼重要：** 指定語言（English）可告訴 OCR 引擎預期的字元集，降低誤辨識的機率——在 **ocr receipt image**（即 OCR 收據圖像）中包含數字與符號時尤為關鍵。

## 步驟 3 – 執行 OCR 並擷取版面資訊

OCR 步驟不僅會輸出原始文字，還會擷取版面資訊，這對之後的結構化抽取至關重要。

```csharp
// Step 3: Run OCR to generate text and layout information (required for structured extraction)
ocrEngine.Recognize();
```

`Recognize()` 完成後，`ocrEngine` 會同時保存純文字與每個單字的位置資料。這是下一步的基礎，我們將請 Aspose 自動「**如何抽取收據**」欄位。

## 步驟 4 – 初始化版面辨識器

Aspose 提供 `LayoutRecognizer` 類別，能了解收據通常的排版（商家名稱在上方、日期行、總金額在底部）。只需將先前設定好的 OCR 引擎傳入即可：

```csharp
// Step 4: Initialize the layout recognizer with the OCR engine
var layoutRecognizer = new LayoutRecognizer(ocrEngine);
```

在底層，辨識器會套用一系列啟發式規則——例如搜尋貨幣符號或日期模式——將原始文字映射為語意欄位。

## 步驟 5 – 抽取結構化收據資料

現在到最精彩的部分：**抽取收據資料**。只需一個方法呼叫即可完成繁重工作：

```csharp
// Step 5: Extract structured receipt data (merchant, date, total amount)
var receiptData = layoutRecognizer.ExtractReceiptData();
```

`receiptData` 是 `ReceiptData` 類型的物件（定義於 `Aspose.OCR.Structured`），它包含三個主要屬性：

- `Merchant` – 商店名稱
- `Date` – 購買日期，型別為 `DateTime`（若偵測到）
- `TotalAmount` – 總金額，型別為 `decimal`

若引擎找不到某個欄位，對應屬性會是 `null` 或 `0`。必要時可加入備援邏輯（例如提示使用者確認）。

## 步驟 6 – 顯示抽取的資訊

最後，將結果輸出至主控台。這裡就是看到成果的地方：

```csharp
// Step 6: Display the extracted information
Console.WriteLine($"Merchant: {receiptData.Merchant}");
Console.WriteLine($"Date:     {receiptData.Date:d}");
Console.WriteLine($"Total:    {receiptData.TotalAmount:C}");
```

格式字串（`:d` 與 `:C`）分別產生短日期與貨幣字串，使輸出易於閱讀。

### 預期輸出

假設收據屬於「Coffee Corner」，日期為 2025‑12‑01，總金額為 $4.75，主控台會顯示：

```
Merchant: Coffee Corner
Date:     12/1/2025
Total:    $4.75
```

若有欄位缺失，會顯示空行或預設值——非常適合除錯。

## 邊緣情況與常見陷阱

### 1. 低解析度圖像

若收據圖像模糊或低於 150 dpi，OCR 的準確度會大幅下降。可在送入 Aspose 前使用簡單的雙線性濾波器將圖像放大，以提升結果。

```csharp
ocrEngine.Image = ImageStream.FromFile("receipt.png")
    .Resize(2.0, InterpolationMode.Bilinear);
```

### 2. 非英文收據

主要範例使用 `Language.English`。若處理多語言收據，請將 `Language` 設為相應的列舉（例如 `Language.French`），或在不確定時使用 `Language.AutoDetect`。

### 3. 單張圖像中有多張收據

Aspose 的版面辨識器預期每張圖像僅有一張收據。若照片中有多張收據並排，需先行前處理——將每張收據裁切成獨立檔案再執行 OCR。

### 4. 缺少貨幣符號

有時總金額會缺少 `$` 符號。辨識器仍會抓取數字，但可能需要在後處理時調整小數點位置以確保正確。

```csharp
if (receiptData.TotalAmount == 0 && rawText.Contains("Total"))
{
    // fallback parsing logic here
}
```

## 生產環境的專業提示

- **快取 OCR 引擎**：若批次處理大量收據，重複使用同一實例可減少記憶體配置開銷。
- **記錄原始 OCR 文字**（`ocrEngine.Text`）以作審計追蹤。當欄位抽取失敗時此資訊相當有用。
- **將整個流程包在 try/catch** 中，並回傳友善的錯誤訊息（例如「無法讀取收據，請上傳更清晰的圖像」）。

## 完整可執行範例

以下是一個獨立的主控台應用程式範例，可直接編譯執行。只要將圖像路徑替換即可使用：

```csharp
// ------------------------------------------------------------
// How to Use Aspose – Extract Receipt Data from Images (C#)
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Structured;

namespace ReceiptExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create and configure the OCR engine for English language
            var ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the receipt image you want to process
            // 👉 Make sure the file exists; otherwise an exception will be thrown.
            const string imagePath = "YOUR_DIRECTORY/receipt.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Run OCR – this also captures layout information
            ocrEngine.Recognize();

            // 4️⃣ Initialize the layout recognizer with the OCR engine
            var layoutRecognizer = new LayoutRecognizer(ocrEngine);

            // 5️⃣ Extract structured receipt data (merchant, date, total amount)
            var receiptData = layoutRecognizer.ExtractReceiptData();

            // 6️⃣ Display the extracted information
            Console.WriteLine($"Merchant: {receiptData.Merchant ?? "Not detected"}");
            Console.WriteLine($"Date:     {(receiptData.Date == DateTime.MinValue ? "Not detected" : receiptData.Date.ToShortDateString())}");
            Console.WriteLine($"Total:    {(receiptData.TotalAmount == 0 ? "Not detected" : receiptData.TotalAmount.ToString("C"))}");

            // Keep the console window open when debugging
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**執行程式**

1. 建立新的 .NET 主控台專案（`dotnet new console -n ReceiptExtractor`）。
2. 加入 Aspose.OCR 套件（`dotnet add package Aspose.OCR`）。
3. 用上述程式碼取代產生的 `Program.cs`。
4. 將收據圖像放置於先前指定的路徑。
5. 編譯並執行（`dotnet run`）。

你應該會看到商家、日期與總金額，正如前述範例所示。

## 總結

本指南說明了 **如何使用 Aspose** 來 **載入收據圖像**、執行 **ocr receipt image**，最後以少量程式碼 **抽取收據資料**。重點在於 Aspose.OCR 已完成繁重的工作——只要配置好 OCR 引擎，`LayoutRecognizer` 就能將原始文字轉換為可信賴的結構化物件。

接下來的步驟？可將抽取的值寫入資料庫、產生 PDF 收據摘要，甚至送入機器學習模型進行費用分類。也可嘗試其他結構化文件類型，如發票或運送標籤——Aspose 的 `ExtractInvoiceData` 也有類似的運作方式。

對於邊緣情況有疑問，或想了解如何處理多頁 PDF？歡迎留言或參考官方 Aspose.OCR 文件的進階範例。祝開發順利，盡情體驗 **如何使用 Aspose** 於收據自動化的簡易性！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}