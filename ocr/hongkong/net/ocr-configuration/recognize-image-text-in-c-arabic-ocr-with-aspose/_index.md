---
category: general
date: 2025-12-30
description: 使用 Aspose OCR 辨識阿拉伯收據的圖像文字。學習如何提取阿拉伯文字、下載語言模型，並在 C# OCR 範例中載入阿拉伯語言。
draft: false
keywords:
- recognize image text
- extract arabic text
- download language model
- c# ocr example
- load arabic language
language: zh-hant
og_description: 使用 Aspose OCR 識別阿拉伯語收據的圖像文字。本指南說明如何提取阿拉伯語文字、下載語言模型，以及在 C# OCR 範例中載入阿拉伯語。
og_title: 在 C# 中辨識圖像文字 – 使用 Aspose 的阿拉伯語 OCR
tags:
- OCR
- C#
- Aspose
title: 在 C# 中辨識圖像文字 – 使用 Aspose 的阿拉伯文 OCR
url: /zh-hant/net/ocr-configuration/recognize-image-text-in-c-arabic-ocr-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中辨識影像文字 – 使用 Aspose 的阿拉伯文 OCR

有沒有需要 **辨識影像文字**，例如從一張阿拉伯文收據上擷取文字，但卻不知從何下手？你並不孤單——許多開發者在處理從右至左的文字時都會卡關。在本教學中，我們將一步步示範完整、可直接執行的 C# OCR 範例，能自動下載所需的語言模型，並將結果輸出到主控台。

我們會說明所有可能會問的問題：為什麼必須明確載入阿拉伯語、即時語言模型下載的運作方式，以及當影像品質不佳時該怎麼處理。完成後，你將擁有一段可直接放入任何 .NET 專案的、具備生產環境品質的程式碼片段。

## 你將學會

- **使用 Aspose OCR 在 C# 中辨識影像文字**  
- 從影像檔案 **擷取阿拉伯文文字** 的完整步驟  
- SDK **自動下載語言模型** 的機制（當模型缺失時）  
- 完整的 **c# ocr example**，可直接複製貼上並立即執行  
- 為何以及如何在辨識前 **載入阿拉伯語言** 以獲得最佳準確度  

### 前置條件

- .NET 6.0 或更新版本（此程式碼亦相容 .NET Framework 4.7+）。  
- 有效的 Aspose.OCR NuGet 套件（可使用 `dotnet add package Aspose.OCR` 安裝）。  
- 一張本機保存的阿拉伯文收據影像（以下稱為 `arabic_receipt.jpg`）。  

不需要其他第三方工具；Aspose 會處理從影像解碼到語言模型管理的全部工作。

![辨識影像文字範例](/images/recognize-image-text-arabic-receipt.png "示意圖顯示從阿拉伯收據辨識影像文字")

## 步驟 1：建立專案並安裝 Aspose OCR

首先，建立一個 Console 專案（或使用既有專案），並加入 Aspose OCR 函式庫。

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
dotnet add package Aspose.OCR
```

*小技巧*：如果你使用 Visual Studio，可以透過 NuGet 套件管理員 UI 加入套件——只要搜尋 **Aspose.OCR** 即可。

## 步驟 2：初始化 OCR 引擎

建立 `OcrEngine` 實例是任何 Aspose OCR 工作流程的基礎。此物件負責保存設定、語言模型與執行時參數。

```csharp
using Aspose.OCR;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // The rest of the code will follow...
        }
    }
}
```

為什麼要在載入語言之前先實例化引擎？因為引擎需要先知道有哪些語言模型可用，若之後才載入語言，會觸發第二次內部初始化，這會影響效能。

## 步驟 3：下載並載入阿拉伯語言模型

Aspose OCR 只隨附極小的核心，會在需要時即時下載語言模型。以下程式碼會在本機尚未快取時，自動取得阿拉伯語模型。

```csharp
// Step 3: Load the Arabic language model (downloaded on demand if missing)
ocrEngine.LoadLanguage(LanguageModel.Arabic);
```

第一次執行時，你會在主控台看到一次短暫的網路請求。之後的執行會因模型已快取於磁碟而瞬間完成。此 **download language model** 行為確保應用程式在不需要額外資料時保持輕量。

## 步驟 4：辨識阿拉伯收據影像中的文字

現在把引擎指向影像檔案。Aspose OCR 會自動偵測影像格式、執行前處理，並遵循阿拉伯文的從右至左排序規則。

```csharp
// Step 4: Recognize text from the Arabic receipt image
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/arabic_receipt.jpg");

// Step 5: Display the recognized text (RTL ordering is handled automatically)
Console.WriteLine("=== Recognized Arabic Text ===");
Console.WriteLine(ocrResult.Text);
```

`Recognize` 方法會回傳一個 `OcrResult` 物件，內含純文字、信心分數，甚至還有若需後續標註時使用的邊框資訊。對於簡單的 **c# ocr example**，只需要取用 `Text` 屬性即可。

### 預期輸出

若收據影像內容類似：

```
المجموع: 120.00 ريال
التاريخ: 30/12/2025
```

主控台將會印出完全相同的阿拉伯文字行，且正確由右至左排列：

```
=== Recognized Arabic Text ===
المجموع: 120.00 ريال
التاريخ: 30/12/2025
```

## 步驟 5：完整可執行範例

把前面的程式碼整合起來，即成為以下完整程式，你可以立即編譯並執行。

```csharp
using Aspose.OCR;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Load (and download if needed) the Arabic language model
            ocrEngine.LoadLanguage(LanguageModel.Arabic);

            // Path to your Arabic receipt image – adjust as needed
            string imagePath = @"YOUR_DIRECTORY/arabic_receipt.jpg";

            // Perform OCR
            var ocrResult = ocrEngine.Recognize(imagePath);

            // Output the recognized Arabic text
            Console.WriteLine("=== Recognized Arabic Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

將此檔案存為 `Program.cs`，執行 `dotnet run`，即可在主控台看到阿拉伯文字。如果出現「model not found」錯誤，請再次確認網路連線——SDK 必須在第一次執行時 **download language model**。

## 常見問題與特殊情境

### 影像模糊該怎麼辦？

Aspose OCR 內建影像增強濾鏡。你可以在呼叫 `Recognize` 前啟用：

```csharp
ocrEngine.ImagePreprocessingOptions = ImagePreprocessingOptions.Auto;
```

這通常能提升低解析度收據的辨識準確度。

### 可以在迴圈中處理多張影像嗎？

絕對可以。首次載入模型後，引擎相當輕量，故可重複使用同一個 `ocrEngine` 實例：

```csharp
foreach (var file in Directory.GetFiles(@"YOUR_DIRECTORY", "*.jpg"))
{
    var result = ocrEngine.Recognize(file);
    Console.WriteLine($"--- {Path.GetFileName(file)} ---");
    Console.WriteLine(result.Text);
}
```

### 使用 Aspose OCR 需要授權嗎？

免費評估授權足以支援開發與測試。正式上線時需購買授權，否則輸出會在超過一定字元數後被截斷。

### **load arabic language** 會影響效能嗎？

首次載入阿拉伯模型會使部署大小增加約 5 MB，並在首次執行時下載一次（在一般寬頻下約 2 秒）。之後的辨識皆以原生速度執行，對每張影像不會產生額外開銷。

## 取得最佳結果的技巧

- **裁切收據**，去除多餘雜訊；OCR 引擎只會處理你提供的區域。  
- **盡量使用 PNG** 而非 JPEG；無損壓縮能保留阿拉伯字形所需的銳利邊緣。  
- **設定正確的 DPI**（300 dpi 為安全預設），若是程式產生影像時請務必如此。  
- 若需過濾低信心文字，請檢查 `ocrResult.Confidence`。

## 結論

現在你已掌握如何使用 Aspose OCR 在 C# 中 **辨識影像文字**，並以完整的 **c# ocr example** 從阿拉伯收據中 **擷取阿拉伯文字**。只要先載入阿拉伯語言模型，讓 SDK 在需要時 **download language model**，再呼叫 `Recognize`，即可可靠地從任何影像中抽取阿拉伯文字。

接下來你可以探索：

- 將辨識出的文字寫入資料庫，以作為費用追蹤。  
- 使用 Aspose 的版面分析功能，抽取關鍵值對（例如總金額、日期）。  
- 將解決方案延伸至其他從右至左語言，如希伯來文或波斯文。

試著跑跑看，調整前處理參數，讓 OCR 為你完成繁重的工作。祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}