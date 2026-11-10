---
category: general
date: 2026-02-13
description: 如何使用 Aspose OCR 快速讀取收據並以正則表達式提取金額。學習一步一步的收據 OCR 處理流程。
draft: false
keywords:
- how to read receipt
- extract amount using regex
- regex find total
- process receipt with ocr
language: zh-hant
og_description: 如何使用 Aspose OCR 與正則表達式在 C# 中讀取收據。本指南將示範如何使用 OCR 處理收據並提取總金額。
og_title: 如何在 C# 中讀取收據 – 完整的 OCR 與正則表達式教學
tags:
- OCR
- C#
- Regex
- Aspose
title: 如何在 C# 中讀取收據 – OCR + 正則表達式指南
url: /zh-hant/net/text-recognition/how-to-read-receipt-in-c-ocr-regex-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中讀取收據 – OCR + 正則表達式指南

有沒有想過 **如何讀取收據** 圖片而不必手動輸入每一行？在許多小型企業應用程式中，你需要從收據照片中提取總金額，手動操作就失去了自動化的意義。好消息是？使用 Aspose OCR，你可以讓引擎完成繁重的工作，然後透過簡單的正則表達式找出總額。在本教學中，我們將逐步說明 **process receipt with OCR**，使用正則表達式提取金額，最終得到可直接使用的總金額。

你將看到完整、可執行的範例，了解為何收據語言模型很重要，並獲得處理邊緣情況（如不同貨幣符號或缺少 “Total” 標籤）的技巧。無需外部文件——所有需要的資訊都在此。

## 你將學到什麼

- 如何設定 Aspose OCR 以進行收據專屬辨識（`Receipt` 語言模型會自動去除傾斜與雜訊）。  
- 如何套用正則表達式以 **extract amount using regex**，適用於大多數美國式收據的模式。  
- 如何處理常見變化，例如 “TOTAL”、 “Total:” 或 “Grand Total – $12.34”。  
- 如何安全地輸出結果，以及在找不到匹配模式時的處理方式。  

**先決條件**： .NET 6+（或 .NET Framework 4.7+）、有效的 Aspose OCR 授權或試用版，以及本機儲存的收據圖片。就這樣——不需要除 Aspose.OCR 之外的其他 NuGet 套件。

---

## 第一步 – 安裝 Aspose OCR 並準備專案

### 為什麼這很重要

Aspose OCR 提供專為 **process receipt with OCR** 設計的模型，能夠校正皺摺的紙張並忽略背景噪音。使用通用文字模型會產生更多錯誤，尤其在低解析度掃描時更為明顯。

### 程式碼

```csharp
// Install the package via NuGet first:
//   dotnet add package Aspose.OCR
using Aspose.OCR;
using Aspose.OCR.Enums;
using System.Text.RegularExpressions;

// If you have a license file, load it now (optional but removes trial watermark)
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

> **專業提示：** 將授權檔案放在來源控制資料夾之外，以免意外提交。

---

## 第二步 – 為收據辨識設定 OCR 引擎

### 為什麼這很重要

`Receipt` 語言模型內建去傾斜與去雜訊功能，能顯著提升對常常折疊或皺摺的實際收據的辨識準確度。

### 程式碼

```csharp
// Step 2: Create and configure the OCR engine for receipt processing
var ocrEngine = new OcrEngine
{
    // Receipt model is optimized for invoices, grocery receipts, etc.
    Language = OcrLanguage.Receipt
};
```

---

## 第三步 – 從收據圖片辨識文字

### 為什麼這很重要

在套用任何正則表達式之前，你需要先取得原始文字。`RecognizeImage` 方法會回傳一個 `OcrResult`，其中包含完整字串、信賴分數，以及其他你日後可能需要的資訊。

### 程式碼

```csharp
// Step 3: Recognize text from the receipt image
// Replace the path with the actual location of your receipt file.
string receiptPath = @"C:\Receipts\sample-receipt.jpg";

OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

// Quick sanity check – print the whole OCR output (helps debugging)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(receiptResult.Text);
Console.WriteLine("===================\n");
```

**預期的 OCR 輸出（範例）**  
```
Walmart Supercenter
123 Main St.
Anytown, USA
Date: 02/12/2026
Item A   $3.45
Item B   $7.89
Subtotal $11.34
Tax      $0.91
Total:   $12.25
Thank you!
```

---

## 第四步 – 建立正則表達式以 **Extract Amount Using Regex**

### 為什麼這很重要

收據的格式多種多樣，但「Total」這個字（或相近變體）後接金額是一個可靠的錨點。以下模式容許可選的空格、冒號、連字號，以及可選的 `$` 符號。

### 程式碼

```csharp
// Step 4: Use a regular expression to locate the total amount in the recognized text
string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
RegexOptions options = RegexOptions.IgnoreCase;

Match totalMatch = Regex.Match(receiptResult.Text, pattern, options);
```

**模式說明**

| Part | Meaning |
|------|---------|
| `Total` | 尋找「Total」這個字（不分大小寫）。 |
| `\s*[:\-]?` | 允許任意空白，接著可選的冒號或連字號。 |
| `\s*\$?` | 可選的空白與可選的美元符號。 |
| `(\d+(\.\d{2})?)` | 捕獲一個或多個數字，後面可選擇性地跟著小數點與兩位分（即分錢）。 |

---

## 第五步 – 輸出擷取的總額或處理缺失資料

### 為什麼這很重要

即使是最優秀的 OCR 也可能遺漏文字，特別是在模糊的收據上。提供優雅的備援機制可防止程式崩潰，並讓你有機會加入自訂邏輯（例如請使用者確認）。

### 程式碼

```csharp
// Step 5: Output the extracted total, or indicate it wasn't found
if (totalMatch.Success)
{
    string amount = totalMatch.Groups[1].Value;
    Console.WriteLine($"Total: ${amount}");
}
else
{
    Console.WriteLine("Total amount not found. Consider reviewing the OCR output manually.");
}
```

**範例主控台輸出**

```
Total: $12.25
```

---

## 完整可執行範例 – 所有步驟於單一檔案

以下是一個單一、獨立的程式，你可以直接複製貼上到主控台專案中。它包含註解、錯誤處理，以及可選的授權載入。

```csharp
// ---------------------------------------------------------------
// How to Read Receipt in C# – OCR + Regex (Complete Example)
// ---------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Enums;
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 0️⃣ Optional: Load your Aspose OCR license (remove trial watermark)
        try
        {
            var license = new Aspose.OCR.License();
            license.SetLicense("Aspose.OCR.lic"); // path to .lic file
        }
        catch (Exception ex)
        {
            Console.WriteLine("License not found – running in trial mode.");
        }

        // 1️⃣ Configure the OCR engine for receipt processing
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Receipt // receipt model = de‑skew + de‑noise
        };

        // 2️⃣ Path to the receipt image (change to your file)
        string receiptPath = @"YOUR_DIRECTORY/receipt.jpg";

        // 3️⃣ Perform OCR
        OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

        // 4️⃣ Debug: show full OCR text (helps when regex fails)
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(receiptResult.Text);
        Console.WriteLine("===================\n");

        // 5️⃣ Regex to **extract amount using regex** (find the total)
        string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
        Match totalMatch = Regex.Match(receiptResult.Text, pattern,
                                        RegexOptions.IgnoreCase);

        // 6️⃣ Output
        if (totalMatch.Success)
        {
            string amount = totalMatch.Groups[1].Value;
            Console.WriteLine($"Total: ${amount}");
        }
        else
        {
            Console.WriteLine("Total amount not found. You might need to adjust the regex or improve image quality.");
        }
    }
}
```

**執行程式**

1. 建立一個新的主控台專案 (`dotnet new console -n ReceiptReader`)。  
2. 加入 Aspose.OCR NuGet 套件 (`dotnet add package Aspose.OCR`)。  
3. 將 `YOUR_DIRECTORY/receipt.jpg` 替換為實際的收據圖片路徑。  
4. 建置並執行 (`dotnet run`)。  

如果一切順利，你會看到 OCR 輸出，接著顯示 `Total: $xx.xx`。

---

## 處理邊緣情況與常見變化

### 1. 不同的貨幣符號

如果你處理歐元 (€) 或英鎊 (£)，可以擴充模式：

```csharp
string pattern = @"Total\s*[:\-]?\s*[$€£]?\s*(\d+(\.\d{2})?)";
```

### 2. 缺少 “Total” 標籤

有些收據只顯示 “Grand Total”。加入交替選項：

```csharp
string pattern = @"(?:Total|Grand\s*Total)\s*[:\-]?\s*[$]?\s*(\d+(\.\d{2})?)";
```

### 3. 多個總額（例如 “Subtotal” 與 “Total”）

如果正則表達式匹配到第一個出現，你可能想要取得 **最後** 一個匹配：

```csharp
MatchCollection matches = Regex.Matches(receiptResult.Text, pattern,
                                         RegexOptions.IgnoreCase);
Match last = matches.Count > 0 ? matches[matches.Count - 1] : null;
```

### 4. 低解析度圖片

- 掃描時提高 DPI（`300 DPI` 為理想值）。  
- 在送入 Aspose 前，先以簡單的降噪模糊濾鏡前處理圖片（本指南未涵蓋，但值得探索）。

---

## 實務專案的專業提示

- **Cache the OCR result**：如果需要擷取多個欄位（稅金、項目等），只需執行一次 OCR，即可節省成本。  
- **Log the raw OCR text**：將原始 OCR 文字記錄到資料庫；在有爭議的費用上，它成為有價值的稽核追蹤。  
- 在建置 Web API 時，**run OCR in a background worker**；雖然 OCR 可能需要數百毫秒，非同步執行是可接受的，但對同步請求而言並非最佳。  
- **Validate the extracted amount**：在儲存前，根據業務規則驗證擷取的金額（例如金額必須大於 0）。

---

## 結論

我們已說明如何在 C# 中使用 Aspose OCR 讀取收據圖片，接著 **extract amount using regex** 可靠地找出總金額行。透過 `Receipt` 語言模型，你可以取得去傾斜、去雜訊的文字，而簡潔的正則表達式能處理大多數格式異常。上方完整的程式碼片段可直接嵌入任何 .NET 主控台或服務專案，且額外的邊緣情況建議為生產環境提供堅實基礎。

準備好進一步了嗎？試著擴充解決方案以擷取單項明細、自動計算稅金，或整合至費用追蹤 API。若遇到無法匹配的收據，請記得 **regex find total** 只是一個起點——你隨時可以調整模式以符合特定地區。

祝程式開發順利，願你的收據處理快速、精確且全自動！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}