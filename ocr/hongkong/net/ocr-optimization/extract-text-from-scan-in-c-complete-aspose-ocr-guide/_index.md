---
category: general
date: 2026-02-19
description: 學習如何使用 Aspose OCR 從掃描圖像提取文字，並對圖像進行預處理以提升 OCR 準確度。一步一步的 C# 教學。
draft: false
keywords:
- extract text from scan
- preprocess image for ocr
language: zh-hant
og_description: 快速從掃描中提取文字。本指南說明如何對圖像進行 OCR 前處理，並使用 Aspose OCR 在 C# 中獲得可靠的結果。
og_title: 從掃描中提取文字 – 完整 C# Aspose OCR 教學
tags:
- OCR
- C#
- Aspose
title: 在 C# 中從掃描圖像提取文字 – 完整 Aspose OCR 指南
url: /zh-hant/net/ocr-optimization/extract-text-from-scan-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從掃描檔案提取文字 – 完整 Aspose OCR 指南

有沒有曾經需要**從掃描檔案提取文字**，卻一直得到亂碼輸出？你並不是唯一遇到這個問題的人。在許多實務專案中——例如發票數位化或舊文件的存檔——從掃描圖像取得乾淨的文字是第一道關卡。好消息是？只要幾行 C# 程式碼加上 Aspose OCR，就能把雜訊 JPEG 轉成可讀的字元，而稍微的前處理則能讓結果從「馬馬虎虎」變成「驚艷」。

在本教學中，我們將逐步說明整個流程：設定 OCR 引擎、**為 OCR 前處理圖像** 以提升品質、執行辨識，最後印出提取的文字。完成後，你將擁有一個可直接執行的 Console 應用程式，能可靠地從任何掃描圖像中抽取文字。

## 需要的環境

在開始之前，請確保你已具備以下條件：

- **.NET 6+**（或 .NET Framework 4.7.2+）已安裝 – API 兩者皆支援。
- **Aspose.OCR** NuGet 套件 (`Install-Package Aspose.OCR`) – 這是唯一的外部相依性。
- 一張範例掃描圖像（例如 `skewed_scan.jpg`），放在可供參考的資料夾中。
- 程式碼編輯器或 IDE – Visual Studio、Rider 或 VS Code 都可使用。

不需要其他函式庫；我們將使用的前處理選項已內建於 Aspose OCR。

## 步驟 1：建立新 Console 專案

首先，建立一個全新的 Console 應用程式，讓你有一個乾淨的測試環境。

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

就這樣——你的專案現在已參考 OCR 函式庫。打開 `Program.cs`，清除預設的 `Hello World` 行，我們將以自己的程式碼取代它。

## 步驟 2：初始化 OCR 引擎 – 提取的核心

要**從掃描檔案提取文字**，你需要建立一個 `OcrEngine` 實例。將語言設定為英文是最常見的情況，但 Aspose 也支援數十種語言，若有需要可自行切換。

```csharp
using Aspose.OCR;
using Aspose.OCR.Preprocessing;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine and tell it we’re dealing with English text
        var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };
```

為什麼要先實例化引擎？引擎會保存所有設定——語言、前處理以及內部快取——提前建立可確保之後的每一次呼叫都使用相同的配置。

## 步驟 3：為 OCR 前處理圖像 – 提升提取前的準確度

掃描圖像很少是完美的。它們可能被旋轉、雜訊過多或對比度不足。Aspose OCR 提供三種實用的前處理選項，能顯著提升結果：

- **Deskew** – 自動校正旋轉的頁面。
- **Denoise** – 平滑斑點與顆粒雜訊。
- **Contrast** – 提亮微弱的字元。

```csharp
        // 2️⃣ Turn on preprocessing to clean up the image
        ocrEngine.Preprocessing = new PreprocessingOptions
        {
            Deskew = DeskewAdvanced.Enable(),      // corrects rotation
            Denoise = DenoiseWavelet.Enable(),    // reduces noise
            Contrast = ContrastBoost.Enable()     // enhances contrast
        };
```

把這一步想像成在把照片交給 OCR 引擎前，先給掃描器做一次快速拋光。跳過它就像要閱讀一張被塗抹的明信片——雖然可能，但會非常挫折。

## 步驟 4：辨識文字 – 真正的提取

現在把已清理過的圖像餵給引擎。將 `YOUR_DIRECTORY` 替換為實際存放 `skewed_scan.jpg` 的路徑。

```csharp
        // 3️⃣ Run OCR on the preprocessed image
        var ocrResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/skewed_scan.jpg");
```

`RecognizeImage` 方法會回傳一個 `OcrResult` 物件，裡面包含原始文字、信心分數，甚至在需要時的邊界框資訊。

## 步驟 5：顯示（或儲存）提取的文字

最後，讓我們看看得到的結果。在真實專案中，你可能會把它寫入資料庫或檔案；此處先直接印到主控台。

```csharp
        // 4️⃣ Output the extracted text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

執行程式 (`dotnet run`) 後，你應該會看到類似以下的輸出：

```
=== Extracted Text ===
Invoice #12345
Date: 01/02/2026
Total: $1,234.56
Thank you for your business!
```

如果輸出仍是亂碼，請再次確認圖像路徑是否正確，以及前處理選項是否已啟用。通常是細微的旋轉或過重的雜訊造成問題。

![extract text from scan example](/images/ocr-example.png)

*Alt text: 使用 Aspose OCR 在 C# 中提取掃描文字的螢幕截圖*

## 常見陷阱與避免方法

- **錯誤的檔案路徑** – 相對路徑是相對於專案根目錄，而非二進位檔案夾。若不確定，請使用絕對路徑。
- **不支援的影像格式** – Aspose OCR 支援 JPEG、PNG、BMP、TIFF。若有 PDF，請先轉成影像。
- **缺少語言資料** – 若使用非英語，可能需要從 Aspose 官網下載額外語言套件。
- **過度前處理** – 在已相當乾淨的影像上同時使用去雜訊與對比度提升，可能會把微弱字元洗掉。請分別測試每個選項的開關。

小技巧：如果只需要校正（大多數掃描僅是旋轉），可以省略其他兩個選項，以節省幾毫秒的處理時間。

## 擴充解決方案 – 若需要更多功能？

### 從多張掃描提取文字

將辨識程式碼包在 `foreach` 迴圈中，遍歷資料夾內的所有影像：

```csharp
string[] files = Directory.GetFiles(@"YOUR_DIRECTORY", "*.jpg");
foreach (var file in files)
{
    var result = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"--- {Path.GetFileName(file)} ---");
    Console.WriteLine(result.Text);
}
```

### 取得信心分數

若需要過濾低信心的結果：

```csharp
if (ocrResult.Confidence < 0.75)
{
    Console.WriteLine("Warning: Low confidence, consider manual review.");
}
```

### 在 Web API 中使用 OCR

透過 ASP.NET Core 端點公開提取邏輯。核心程式碼保持不變，只需將引擎以 singleton 服務注入即可。

## 重點回顧

我們已說明如何使用 Aspose OCR 在 C# 中**從掃描圖像提取文字**。從建立專案開始，我們：

1. 使用英語初始化 OCR 引擎。
2. **為 OCR 前處理圖像**，使用校正、去雜訊與對比度提升。
3. 在範例 JPEG 上執行辨識。
4. 將乾淨的文字印出至主控台。

有了這些組件，你現在可以把 OCR 整合到發票處理器、文件存檔系統，或任何需要將紙本轉為可搜尋資料的應用程式中。

## 接下來可以做什麼？

- 嘗試其他前處理組合（例如針對黑白文件的 `Binarize`）。
- 嘗試不同語言或多語言偵測。
- 結合 OCR 輸出與自然語言處理，自動抽取關鍵欄位。

如果在使用過程中遇到問題或發現巧妙的調整，歡迎留下評論。祝開發順利，願你的掃描永遠清晰如水晶！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}