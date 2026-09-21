---
category: general
date: 2026-01-09
description: C# OCR 教學：從 PNG 讀取文字，將影像轉換為文字，並使用 Aspose OCR 識別收據上的印地語文字。
draft: false
keywords:
- c# ocr tutorial
- read text from png
- convert image to text
- recognize hindi text
- extract text from receipt
language: zh-hant
og_description: C# OCR 教學，教您如何從 PNG 讀取文字、將圖像轉換為文字，並使用 Aspose OCR 識別收據上的印地語文字。
og_title: c# OCR 教學 – 從 PNG 收據中提取印地語文字
tags:
- OCR
- C#
- Aspose
- Image Processing
title: c# OCR 教學 – 從 PNG 收據提取印地語文字
url: /zh-hant/net/text-recognition/c-ocr-tutorial-extract-hindi-text-from-png-receipts/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR 教學 – 從 PNG 收據中提取印地語文字

有沒有想過如何在 C# 應用程式中 **讀取 PNG** 檔案的文字？也許你手頭有一堆印地語收據，需要自動提取金額。這正是本 c# OCR 教學要解決的——只需幾行程式碼即可將影像轉換為可搜尋的文字。

在本指南中，我們將逐步說明如何安裝 Aspose OCR、載入 PNG 收據、辨識印地語字元，最後將擷取的字串印出到主控台。完成後，你將能夠 **將影像轉換為文字**、**辨識印地語文字**，甚至 **從收據影像中提取文字**，且全程不離開 IDE。

> **先決條件說明：** 你需要一個有效的 Aspose OCR 授權（或使用免費試用版），並已安裝 .NET 6 以上版本。如果你是 NuGet 新手，別擔心——我們也會說明。

---

## 需要的工具

- **Visual Studio 2022**（或任何相容 C# 的編輯器）
- **.NET 6 SDK**（或更新版本）
- **Aspose.OCR** NuGet 套件  
  ```bash
  dotnet add package Aspose.OCR
  ```
- 範例收據影像，例如 `hindi-receipt.png`，存放於專案資料夾中。

準備好以上項目後，你就能直接複製貼上最終程式碼，並立即按 **F5** 執行。

---

## 步驟 1：建立專案並匯入命名空間

首先，若尚未有專案，請建立一個 Console 專案：

```bash
dotnet new console -n HindiReceiptOcr
cd HindiReceiptOcr
dotnet add package Aspose.OCR
```

接著開啟 `Program.cs`。在檔案頂部匯入 Aspose OCR 的命名空間，讓編譯器能找到相關類別：

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;
```

> **為什麼重要：** `OcrEngine` 位於 `Aspose.OCR`，而語言相關的列舉則在 `Aspose.OCR.Settings`。若遺漏任一項，將導致編譯時錯誤。

---

## 步驟 2：初始化 OCR 引擎並選擇語言模型

OCR 引擎必須知道要辨識 **哪種語言**。Aspose 提供多種語言套件；指定 `OcrLanguage.Hindi` 即可告訴引擎下載（若尚未存在）並使用印地語模型。

```csharp
// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // The library will auto‑download the model the first time it runs.
    Language = OcrLanguage.Hindi
};
```

> **專業提示：** 若你打算處理多語言收據，可在執行時切換 `Language`，甚至啟用 `MultiLanguage` 模式。

---

## 步驟 3：將 PNG 收據送入引擎

這裡就是 **讀取 PNG 文字** 的地方。提供完整路徑（相對於可執行檔亦可），此方法會回傳一個純文字字串，包含引擎能辨識的所有內容。

```csharp
// Step 3: Perform OCR on the target image file
string imagePath = @"hindi-receipt.png";   // adjust if your file lives elsewhere
string recognizedText = ocrEngine.RecognizeImage(imagePath);
```

若影像解析度高且文字清晰，將得到近乎完美的結果。對於雜訊較多的掃描，可考慮前處理（例如二值化）——Aspose 提供 `PreprocessImage` 方法，日後可進一步探索。

---

## 步驟 4：顯示或儲存擷取的文字

大多數開發者在測試時會直接將結果輸出到主控台。實務上，你可能會寫入資料庫或 CSV 檔案。

```csharp
// Step 4: Show the OCR result
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(recognizedText);
```

執行程式並使用範例收據時，會輸出類似以下內容：

```
=== OCR Output ===
दिनांक: 09/01/2026
बिल no: 12345
रक्कम: ₹ 1,250.00
धन्यवाद!
```

這就是 **將影像轉換為文字** 的實際運作——不需要手動抄寫。

---

## 完整範例（可直接複製貼上）

以下是完整、獨立的程式碼。將其貼入 `Program.cs`，把 `hindi-receipt.png` 放在編譯後的 `.exe` 同目錄，然後按 **Ctrl + F5** 執行。

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace HindiReceiptOcr
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine with Hindi language
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.Hindi
            };

            // 2️⃣ Path to the PNG receipt (adjust if needed)
            string imagePath = @"hindi-receipt.png";

            // 3️⃣ Run OCR – this will download the Hindi model on first run
            string recognizedText = ocrEngine.RecognizeImage(imagePath);

            // 4️⃣ Output the result – you can also write to a file or DB
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### 預期輸出

當收據影像中的印地語字元清晰時，主控台會顯示擷取的行，並保留換行。若 OCR 無法辨識某個字詞，則會出現亂碼片段——提示你需要提升影像品質或調整前處理。

---

## 步驟 5：更進一步 – 程式化擷取收據文字

若你的目標是 **從收據中提取文字**（如日期、總金額、發票號碼），可以使用正規表達式對 OCR 結果字串進行後處理：

```csharp
using System.Text.RegularExpressions;

// Example: pull the amount (₹) from the OCR result
var amountMatch = Regex.Match(recognizedText, @"रक्कम:\s*₹\s*([\d,]+\.\d{2})");
if (amountMatch.Success)
{
    Console.WriteLine($"Detected amount: {amountMatch.Groups[1].Value}");
}
```

---

## 常見問題與避免方法

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **空白輸出** | 影像路徑錯誤或檔案未複製至輸出資料夾。 | 使用 `Path.GetFullPath`，並確認檔案存在 (`File.Exists`)。 |
| **雜訊字元** | PNG 解析度低或顏色被壓縮。 | 將影像放大，將 DPI 設為 300 以上，或使用 `ocrEngine.ImagePreprocessor`。 |
| **語言模型未下載** | 首次執行時無網路連線。 | 透過 Aspose 入口網站預先下載印地語模型，或自行在本機部署。 |
| **效能延遲** | 在迴圈中處理大量頁面卻未釋放資源。 | 將 `OcrEngine` 包於 `using` 區塊，或重複使用同一個實例。 |

---

## 圖片說明

![c# OCR 教學：從 PNG 收據讀取印地語文字](https://example.com/placeholder-image.png "c# OCR 教學 – 從 PNG 收據讀取文字")

*此截圖顯示印地語收據在 OCR 轉換前後的樣子。*

---

## 重點回顧：我們學了什麼

- 建立 C# Console 應用程式並加入 Aspose OCR NuGet 套件。  
- 使用 **recognize hindi text** 語言模型初始化 `OcrEngine`。  
- **Read text from PNG** 使用 `RecognizeImage`。  
- **Convert image to text** 並印出結果。  
- 示範簡單的模式以 **extract text from receipt** 欄位。  

---

## 往後步驟與相關主題

1. **Batch processing** – 迴圈處理資料夾中的收據影像，並將結果儲存為 CSV。  
2. **Pre‑processing** – 探索 `ocrEngine.ImagePreprocessor` 以進行噪點移除、傾斜校正或對比度增強。  
3. **Multi‑language OCR** – 啟用 `OcrLanguage.Multilingual` 以處理同時包含印地語與英文的收據。  
4. **Integration** – 將擷取的資料寫入 Entity Framework Core 模型，以實現永久儲存。  

如果你對上述任一主題感興趣，可參考我們關於 **convert image to text in C#** 與 **extract structured data from OCR results** 的教學。

### 祝開發順利！

如果遇到問題，歡迎留下評論，或分享你在專案中如何擴充此 **c# OCR 教學**。請記住，OCR 只是第一步——乾淨的資料才是關鍵。🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}