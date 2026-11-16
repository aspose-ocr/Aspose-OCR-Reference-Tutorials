---
category: general
date: 2026-03-07
description: 學習如何從 png 讀取文字，使用 Aspose OCR 提取西里爾文字，將圖像轉換為文字，並下載西里爾語言包。
draft: false
keywords:
- read text from png
- extract cyrillic text
- convert image to text
- load image for ocr
- download cyrillic language pack
language: zh-hant
og_description: 學習如何從 PNG 讀取文字、提取西里爾文字，並使用 Aspose OCR 於 C# 中將圖像轉換為文字。
og_title: 從 PNG 讀取文字 – 使用 Aspose OCR 提取西里爾文字
tags:
- Aspose OCR
- C#
- Image Processing
title: 從 PNG 讀取文字 – 使用 Aspose OCR 提取西里爾文字
url: /zh-hant/net/ocr-configuration/read-text-from-png-extract-cyrillic-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 PNG 讀取文字 – 使用 Aspose OCR 提取西里爾文字

需要 **從 png 讀取文字** 並提取西里爾字元嗎？在本指南中，我們將示範如何使用 Aspose OCR 從 png 讀取文字、提取西里爾文字，並在幾行 C# 程式碼內 **將影像轉換為文字**。

如果你曾經盯著一張俄文發票的螢幕截圖，想知道如何把文字轉成可搜尋的字串，那麼你來對地方了。我們還會說明如何自動 **下載西里爾語言包**，免去手動搜尋額外檔案的麻煩。

## 您將能夠達成的目標

完成本教學後，你將能夠：

* **直接從磁碟或串流載入影像以供 OCR 使用**。  
* 在不需手動下載的情況下，將引擎設定為 **Cyrillic 語言**。  
* 執行辨識，並 **提取 PNG 檔案中的西里爾文字**。  
* 在主控台上看到辨識後的文字 – 純淨的純文字結果，可供資料庫、搜尋索引或其他工作流程使用。

不需要外部服務、雲端金鑰，只要 Aspose OCR NuGet 套件與幾行 C# 程式碼即可。

## 前置條件

* .NET 6.0 或更新版本（程式碼可在 .NET Core、.NET Framework 以及 .NET 5+ 上執行）。  
* Visual Studio 2022 或您喜歡的任何編輯器。  
* Aspose.OCR NuGet 套件（`dotnet add package Aspose.OCR`）。  
* 包含西里爾字元的 PNG 影像，例如放在 `YOUR_DIRECTORY` 資料夾中的 `cyrillic_sample.png`。

> **小技巧**：如果您使用 Visual Studio，右鍵點擊專案 → **Manage NuGet Packages** → 搜尋 “Aspose.OCR” 並安裝最新的穩定版。

---

## Step 1 – Install Aspose OCR and create the engine

首先我們需要建立 OCR 引擎實例。`OcrEngine` 類別是所有操作的入口點。

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Create an OCR engine – this object holds all settings and results
var ocrEngine = new OcrEngine();
```

> **為什麼這很重要**：引擎封裝了語言包、影像資料與辨識選項。只要實例化一次，並在多張影像間重複使用，可提升效能。

---

## Step 2 – **load image for ocr** and set the language

現在告訴引擎要處理哪張影像以及要偵測哪種語言。設定 `Language.Cyrillic` 後，第一次執行時會自動下載所需的語言包。

```csharp
// 1️⃣ Load the PNG that contains Cyrillic text
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_sample.png");

// 2️⃣ Tell Aspose we want to read Cyrillic characters
ocrEngine.Settings.Language = Language.Cyrillic;   // downloads pack if missing
```

> **邊緣情況**：如果你的 PNG 檔案很大（超過 5 MB），建議先縮小尺寸以加速辨識。`Image` 屬性也接受 `Stream`，因此可以從記憶體、網路請求或 Azure Blob 載入，而不必觸及檔案系統。

---

## Step 3 – **convert image to text** with a single call

辨識只需要呼叫 `Recognize()`。呼叫完成後，`Text` 屬性即保存了提取出的字串。

```csharp
// Run the OCR engine – this does the heavy lifting
ocrEngine.Recognize();

// Grab the result; it’s plain Unicode text
string extractedText = ocrEngine.Text;
```

> **底層發生了什麼**：Aspose 以神經網路分類器（訓練自數百萬個西里爾字形）執行辨識。程式庫將所有複雜度抽象化，讓你直接取得乾淨的 Unicode 文字。

---

## Step 4 – Output the result (or pipe it elsewhere)

示範用途我們會把文字印到主控台，但你也可以輕鬆寫入檔案、資料庫，或傳給搜尋索引。

```csharp
// Show the OCR result in the console
Console.WriteLine("=== Recognized Cyrillic Text ===");
Console.WriteLine(extractedText);
```

**預期輸出**（假設 `cyrillic_sample.png` 包含短語 “Привет мир”）：

```
=== Recognized Cyrillic Text ===
Привет мир
```

如果輸出看起來亂碼，請再次確認影像清晰且已設定 `Language.Cyrillic`。引擎預設使用英文，會將西里爾字元視為未知符號。

---

## Step 5 – Full, runnable example

把所有步驟整合起來，以下是一個可直接貼到新 Console 專案的完整程式碼。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // 2️⃣ Load the PNG and select Cyrillic language
        // -------------------------------------------------
        // Replace the path with the location of your PNG
        ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_sample.png");
        ocrEngine.Settings.Language = Language.Cyrillic; // auto‑downloads pack

        // -------------------------------------------------
        // 3️⃣ Perform recognition
        // -------------------------------------------------
        ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== Recognized Cyrillic Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

將檔案儲存為 `Program.cs`，執行 `dotnet run`，即可在主控台看到西里爾文字。

---

## 常見問題與除錯

| 問題 | 回答 |
|----------|--------|
| **如果語言包無法下載該怎麼辦？** | 確認機器能連上網路。語言包會快取於 `%USERPROFILE%\.Aspose\OCR\Languages`。刪除該資料夾即可強制重新下載。 |
| **我可以讀取除西里爾之外的其他語言嗎？** | 當然可以 – 只要把 `Language.Cyrillic` 換成 `Language.English`、`Language.Arabic` 等，同樣會自動下載相應語言包。 |
| **我的 PNG 噪點太多，辨識效果差，該怎麼辦？** | 先前處理影像：提升對比、轉成灰階，或套用中值濾波。Aspose OCR 也提供 `Settings.ImagePreprocess` 選項。 |
| **有辦法取得每個單字的邊界框嗎？** | 可以，呼叫 `Recognize()` 後檢查 `ocrEngine.Regions`，它會回傳每個偵測到的單字的矩形區域。 |
| **正式環境需要授權嗎？** | 免費評估版支援最多 100 頁。商業專案請購買授權，授權會移除評估浮水印並解鎖高速批次處理功能。 |

---

## 下一步 – 擴充解決方案

* **批次處理**：遍歷 PNG 資料夾，將所有文字收集到 CSV 檔案中。  
* **整合 Azure Cognitive Search**：將提取的西里爾字串建立索引，以便快速查詢。  
* **結合 PDF 轉換**：先使用 Aspose.PDF 將掃描的 PDF 轉為 PNG，然後執行相同的 OCR 流程。  

上述情境皆可重複使用我們剛剛學到的核心模式：**載入影像 → 設定語言 → 辨識 → 使用文字**。

---

## 結論

現在你已掌握如何 **從 png 讀取文字**、**提取西里爾文字**，以及使用 Aspose OCR 在 C# 中 **將影像轉換為文字**。關鍵步驟包括建立引擎、載入影像、選擇正確語言（會自動 **下載西里爾語言包**），最後呼叫 `Recognize()`。

試著用不同的影像來練習，玩玩 `Settings` 選項，讓你的應用程式變得可搜尋、多語言且更聰明。

祝程式開發順利，若遇到任何問題，歡迎留下評論！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}