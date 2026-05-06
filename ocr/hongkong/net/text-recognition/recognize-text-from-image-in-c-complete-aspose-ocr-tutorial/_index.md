---
category: general
date: 2026-05-06
description: 學習如何使用 Aspose OCR 於 C# 從圖像辨識文字。從收據提取文字、載入圖像進行 OCR，並查看完整的 Aspose OCR 範例。
draft: false
keywords:
- recognize text from image
- extract text from receipt
- load image for OCR
- Aspose OCR example
language: zh-hant
og_description: 學習使用 Aspose OCR 從圖像識別文字、從收據提取文字，並載入圖像進行 OCR，提供簡明的逐步指南。
og_title: 在 C# 中從圖像辨識文字 – 完整的 Aspose OCR 教程
tags:
- C#
- OCR
- Aspose
title: 在 C# 中從圖片辨識文字 – 完整 Aspose OCR 教程
url: /zh-hant/net/text-recognition/recognize-text-from-image-in-c-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中辨識影像文字 – 完整 Aspose OCR 教學

有沒有曾經需要**辨識影像文字**，卻不確定該選哪個函式庫？你並不是唯一遇到這個問題的人——許多開發者在嘗試從收據上抓取金額或掃描表單時，都會卡在同一個牆壁。好消息是 Aspose OCR 讓整個流程變得輕而易舉，在本教學中，我們將一步步示範一個**完整的 Aspose OCR 範例**，只需幾行 C# 程式碼即可**從收據影像中擷取文字**。

在接下來的幾分鐘內，你將學會如何**載入影像供 OCR 使用**、定義包含總金額的精確區域、執行引擎，最後顯示結果。沒有模糊的外部文件參考，沒有遺漏的步驟——所有可以直接 copy‑paste 並執行的程式碼都在這裡。只要稍作設定、跟隨幾個步驟，你就能即時辨識影像檔案中的文字。

> **你將學到的內容**  
> * 一個可執行的 C# 主控台應用程式，能辨識影像檔案中的文字。  
> * 為何將 OCR 限制在特定矩形區域（提升速度與準確度）的概念。  
> * 處理常見邊緣情況的技巧，例如模糊的收據或旋轉的掃描圖。

---

## 前置條件

在開始之前，請確保你已具備以下項目：

| 前置條件 | 為何重要 |
|-------------|----------------|
| .NET 6.0 SDK（或更新版本） | Aspose OCR 以 .NET Standard 2.0 / .NET 5+ 套件形式提供，任何近期的執行環境皆可使用。 |
| Visual Studio 2022（或 VS Code） | 舒適的 IDE 能加速除錯，但任何能編譯 C# 的編輯器都可以。 |
| **Aspose.OCR for .NET** NuGet 套件 | 這是實際負責從影像辨識文字的核心函式庫。 |
| 一張範例收據影像（`receipt.jpg`） | 我們將使用此檔案示範**從收據擷取文字**。 |

你可以使用以下指令安裝 NuGet 套件：

```bash
dotnet add package Aspose.OCR
```

完成後，即可開始載入影像供 OCR 使用。

---

## 第一步：載入影像供 OCR 使用

首先，你需要將引擎指向要分析的檔案。這也是次要關鍵字**載入影像供 OCR 使用**自然出現的地方。

```csharp
using Aspose.OCR;
using System.Drawing;

// Create the OCR engine instance
var ocrEngine = new OcrEngine();

// Load the receipt image – replace the path with your own file location
ocrEngine.SetImage(@"C:\Images\receipt.jpg");
```

> **小技巧：** 若影像放在專案資料夾內，可使用相對路徑，例如 `ocrEngine.SetImage("receipt.jpg");`。只要確保檔案已複製到輸出目錄（`Copy to Output Directory = PreserveNewest`）。

`SetImage` 方法接受 System.Drawing 能解碼的任何格式（JPEG、PNG、BMP 等），因此不會被單一檔案類型所限制。

---

## 第二步：定義感興趣的區域 – **從收據擷取文字**

掃描整張圖片會浪費 CPU 時間，且可能產生雜訊。透過告訴 Aspose OCR 總金額所在的精確位置，你可以同時提升速度與準確度。這就是**從收據擷取文字**的關鍵步驟。

```csharp
// Define a rectangle that covers the total amount on the receipt
// (x, y, width, height) – adjust these numbers for your own layout
var roi = new Rectangle(150, 500, 300, 80);
ocrEngine.SetRegionOfInterest(roi);
```

> **為何使用矩形？**  
> OCR 引擎在像素格上運作。當你將其限制在特定區域時，會忽略其他所有內容——不會再出現來自店家標誌或標題列的雜散字元。

如果不確定確切座標，可使用任何能顯示像素位置的影像檢視器（例如 Paint.NET）目測數值。

---

## 第三步：執行引擎 – **辨識影像文字**（主要關鍵字）

現在魔法發生了。你告訴 Aspose 真正讀取剛才定義的矩形內的像素。

```csharp
// Perform the recognition
OcrResult result = ocrEngine.Recognize();
```

`OcrResult` 包含原始文字、信心分數，甚至每個單字的邊界框。為了快速示範，我們只會印出純文字。

```csharp
Console.WriteLine("Total amount detected: " + result.Text);
```

執行程式後，你應該會看到類似以下的輸出：

```
Total amount detected: $23.45
```

如果輸出看起來亂碼，請再次檢查 ROI 座標，或嘗試提升影像解析度。

---

## 第四步：處理結果 – 完善 **Aspose OCR 範例**

一個健全的解決方案不會只把字串直接丟到主控台。以下是一個小幫手，會去除多餘空白、刪除雜散換行，並驗證擷取的值是否看起來像金額。

```csharp
static string CleanAmount(string raw)
{
    // Remove any non‑numeric characters except dot and comma
    var cleaned = new string(raw
        .Where(c => char.IsDigit(c) || c == '.' || c == ',')
        .ToArray());

    // Normalize decimal separator to dot
    cleaned = cleaned.Replace(',', '.');

    // If we end up with an empty string, return a friendly message
    return string.IsNullOrWhiteSpace(cleaned) ? "N/A" : cleaned;
}

// ...

string amount = CleanAmount(result.Text);
Console.WriteLine($"Parsed amount: ${amount}");
```

此幫手示範了一個可直接套用於任何大型開票系統的實務**Aspose OCR 範例**。

---

## 第五步：完整可執行程式 – 終極 **從收據擷取文字** 示範

將所有程式碼整合在一起，即得到一個可直接 copy‑paste 的檔案。將其存為 `Program.cs`，然後執行 `dotnet run`。

```csharp
// Program.cs
using Aspose.OCR;
using System;
using System.Drawing;
using System.Linq;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the image for OCR
        var ocrEngine = new OcrEngine();
        ocrEngine.SetImage(@"C:\Images\receipt.jpg");   // <-- adjust path

        // 2️⃣ Define the region that holds the total amount
        var roi = new Rectangle(150, 500, 300, 80);
        ocrEngine.SetRegionOfInterest(roi);

        // 3️⃣ Run the engine – recognize text from image
        OcrResult result = ocrEngine.Recognize();

        // 4️⃣ Clean up the output
        string amount = CleanAmount(result.Text);
        Console.WriteLine($"Total amount detected: ${amount}");
    }

    // Helper that sanitises the OCR output
    static string CleanAmount(string raw)
    {
        var cleaned = new string(raw
            .Where(c => char.IsDigit(c) || c == '.' || c == ',')
            .ToArray());

        cleaned = cleaned.Replace(',', '.');
        return string.IsNullOrWhiteSpace(cleaned) ? "N/A" : cleaned;
    }
}
```

**預期輸出**

```
Total amount detected: $23.45
```

若收據影像較暗或文字傾斜，可能會看到類似 `Total amount detected: 23,45` 的結果。`CleanAmount` 方法會將其正規化為標準的十進位格式。

---

## 常見陷阱：當你**辨識影像文字**時

### 1. ROI 座標錯誤
矩形太小會導致字元被裁切；太大則會重新引入雜訊。建議使用視覺工具微調數值，或利用簡易影像處理函式庫（例如 OpenCV）程式化偵測收據邊界。

### 2. 低解析度掃描
解析度低於 150 dpi 時 OCR 準確度會急劇下降。若能掌控掃描流程，請至少設定為 300 dpi。若只能使用低解析度檔案，可在呼叫 `Recognize()` 前加入 `ocrEngine.SetResolution(300);`。

### 3. 收據傾斜或旋轉
Aspose OCR 支援自動旋轉，但必須先啟用：

```csharp
ocrEngine.SetAutoRotate(true);
```

### 4. 語言設定
預設語言為英文。若收據包含其他字母表，請明確設定語言：

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
```

---

## 邊緣案例與變化 – 擴充 **Aspose OCR 範例**

* **多欄位擷取：** 想同時抓取日期與稅額嗎？只需再新增一個 ROI 矩形，重新呼叫 `Recognize()`（或在重設 ROI 後重用同一個引擎）。  
* **批次處理：** 將邏輯包在 `foreach (var file in Directory.GetFiles(@"C:\Receipts"))` 迴圈中，即可自動處理數十筆檔案。  
* **非同步執行：** `Recognize` 方法是同步的，但若你在開發 UI 應用程式，可使用 `Task.Run` 將其搬到背景執行緒。

---

## 視覺參考

![辨識影像文字範例](/images/ocr-demo.png "螢幕截圖顯示 Aspose OCR 結果 – 辨識影像文字")

*此螢幕截圖示範執行完整程式後的主控台輸出。*

---

## 結論

我們剛剛使用 Aspose OCR **辨識影像文字**，示範了如何**載入影像供 OCR 使用**，並建立了一個實用的**從收據擷取文字**工作流程，任何 .NET 專案都能直接套用。完整的 **Aspose OCR 範例** 只需幾行程式碼，卻涵蓋了最常見的情境：ROI 選取、結果清理，以及典型陷阱的處理。

接下來的步驟是什麼？可以嘗試將矩形改為動態偵測機制、實驗不同語言，或將輸出整合至資料庫以自動化費用追蹤。只要有了現在的基礎，擴充功能將變得輕而易舉。

有任何問題或遇到「不合作」的收據嗎？

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}