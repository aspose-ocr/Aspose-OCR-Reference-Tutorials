---
category: general
date: 2026-01-07
description: 如何在 C# 中使用 Aspose OCR 執行光學字符識別並從圖片中提取文字。學習如何從圖片讀取文字、辨識印地語文字，並取得完整程式碼範例。
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from image
- recognize hindi text
- how to extract text from image
language: zh-hant
og_description: 如何在 C# 中執行 OCR 從圖像提取文字。本教學示範如何從圖像讀取文字、辨識印地語文字，以及使用 Aspose OCR 從圖像提取文字。
og_title: 如何在 C# 中執行 OCR – 完整指南
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中執行 OCR – 使用 Aspose OCR 從圖像提取文字
url: /zh-hant/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中執行 OCR – 使用 Aspose OCR 從圖像提取文字

有沒有想過 **如何執行 OCR** 在掃描的發票或招牌照片上？你並不是唯一有此需求的人。在許多實務專案中，你需要 **從圖像提取文字**，無論是收據、護照掃描件，或是手寫筆記。好消息是？使用 Aspose.OCR 只需幾行 C# 程式碼，就能完成，而且還能學會 **辨識印地語文字**。

在本教學中，我們將逐步說明一個完整、可直接執行的範例，該範例 **從圖像讀取文字**，示範如何使用 Aspose OCR 引擎 **從圖像提取文字**，並說明每一步背後的「原因」。不會有模糊的外部文件參考——只提供一個可直接複製貼上並立即執行的獨立解決方案。

## 需要的環境

- .NET 6.0 或更新版本（程式碼亦可編譯於 .NET Standard 2.0）
- Visual Studio 2022（或任何你偏好的 IDE）
- Aspose.OCR NuGet 套件（`Install-Package Aspose.OCR`）
- 包含印地語文字的圖像檔（例如 `hindi_invoice.jpg`）
- 隨 Aspose 提供的 OCR 語言資源資料夾（從 Aspose 官方網站下載）

> **專業提示：** 請將 OCR 資源資料夾放在專案旁邊，以便輕鬆處理路徑。

## 步驟實作說明

以下我們將流程分為六個邏輯步驟。每個步驟都有自己的 H2 標題（方便搜尋引擎與 AI 模型快速定位資訊），以及自然包含次要關鍵字的 H3 子標題。

### Step 1 – 設定 OCR 資源路徑  
**為何重要：** Aspose.OCR 依賴語言套件（字型、字典與模型檔）存放於你指定的資料夾。若路徑錯誤，引擎會拋出 `FileNotFoundException`，且無法從圖像取得任何文字。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Tell the OCR engine where to find language resources
OcrEngine.SetResourcesPath(@"C:\MyProject\OcrResources");
```

### Step 2 – 建立 OCR 引擎實例  
**為何重要：** `OcrEngine` 是佔用大量記憶體的物件，用於在記憶體中保存辨識模型。將其放入 `using` 區塊可確保正確釋放，這在批次處理大量圖像時尤為重要。

```csharp
// Instantiate the OCR engine inside a using block
using (var ocrEngine = new OcrEngine())
{
    // Subsequent steps go here...
}
```

### Step 3 – 設定辨識參數（選擇印地語）  
**為何重要：** 預設情況下 Aspose 會嘗試自動偵測語言，但明確設定 `Language.Hindi` 可提升對天城文（Devanagari）腳本的準確度，並加快處理速度。

```csharp
    // Configure the engine to recognize Hindi text
    var recognitionSettings = new RecognitionSettings
    {
        Language = Language.Hindi   // Recognize Hindi characters
    };
```

### Step 4 – 載入欲辨識的圖像  
**為何重要：** `ImageStream.FromFile` 抽象化底層位圖處理，並有效率地串流資料。若圖像來自網路請求，也可使用 `MemoryStream`。

```csharp
    // Load the target image (replace with your own path)
    var imageStream = ImageStream.FromFile(@"C:\MyProject\Images\hindi_invoice.jpg");
```

### Step 5 – 執行 OCR 程序  
**為何重要：** `Recognize` 方法負責繁重的工作——前處理、分割、字元分類，最後組合成文字。它回傳純文字字串，你可以儲存、顯示或進一步處理。

```csharp
    // Execute OCR and capture the recognized text
    string recognizedText = ocrEngine.Recognize(imageStream, recognitionSettings);
```

### Step 6 – 顯示擷取的文字  
**為何重要：** 為了快速除錯，通常會將結果寫入主控台或日誌檔案。於正式環境中，你可能會將其儲存至資料庫，或傳遞至後續工作流程。

```csharp
    // Output the result to the console
    Console.WriteLine("=== OCR Result ===");
    Console.WriteLine(recognizedText);
}
```

## 完整可執行範例

將上述所有步驟整合起來，以下是可直接放入 Console 應用程式專案的完整程式碼。請務必將佔位路徑替換為實際的目錄。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Set the folder that contains language resources
        OcrEngine.SetResourcesPath(@"C:\MyProject\OcrResources");

        // 2️⃣ Create the OCR engine (auto‑disposed)
        using (var ocrEngine = new OcrEngine())
        {
            // 3️⃣ Tell the engine to look for Hindi characters
            var recognitionSettings = new RecognitionSettings
            {
                Language = Language.Hindi
            };

            // 4️⃣ Load the image you want to read
            var imageStream = ImageStream.FromFile(@"C:\MyProject\Images\hindi_invoice.jpg");

            // 5️⃣ Perform OCR
            string recognizedText = ocrEngine.Recognize(imageStream, recognitionSettings);

            // 6️⃣ Show the extracted text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);
        }

        // Keep console open (useful when running from VS)
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**預期輸出**（為簡潔起見已截斷）：

```
=== OCR Result ===
Invoice No: 12345
Date: 01/01/2024
Amount: ₹ 15,000
धन्यवाद
```

如果看到的是亂碼而非印地語字元，請再次確認資源資料夾指向正確版本的 Hindi 語言套件。

## 常見問題與解決方法

| 問題 | 發生原因 | 快速解決方案 |
|------|----------|--------------|
| **亂碼** | 語言資源錯誤或缺失 | 確認 `SetResourcesPath` 指向包含 `Hindi.cognates` 及相關檔案的資料夾 |
| **記憶體不足錯誤** | 載入過大的圖像未進行縮放 | 使用 `ImageStream.FromFile(..., maxWidth: 2000)` 即時縮小圖像 |
| **效能緩慢** | 自動偵測模式掃描多種語言 | 明確設定 `Language = Language.Hindi`（或其他目標語言） |
| **完全沒有輸出** | 圖像全白或模糊 | 在送入 OCR 前先對圖像進行前處理（對比度、二值化） |

## 擴充解決方案：其他語言與情境

如果需要 **從圖像讀取文字**（如英文、西班牙文或其他語言），只要更改 `Language` 列舉即可：

```csharp
recognitionSettings.Language = Language.English;   // or Language.Spanish, etc.
```

也可以同時結合多種語言：

```csharp
recognitionSettings.Language = Language.English | Language.Hindi;
```

若要批次處理，可將 `using (var ocrEngine = new OcrEngine())` 區塊包覆在遍歷圖像資料夾的 `foreach` 迴圈中。引擎會重複使用已載入的模型，顯著降低初始化開銷。

## 測試 OCR 準確度

1. 使用已知測試圖像執行程式（可使用任何圖形編輯器製作含印地語文字的簡易 PNG）。  
2. 將主控台輸出與原始文字比較。  
3. 若錯誤率超過 5 %，請考慮調整圖像品質（將 DPI 提升至 300 dpi）或加入前處理步驟，例如 `imageStream = imageStream.ApplyGaussianBlur(1.5)`（Aspose 提供基本濾鏡）。

## 結論

我們已示範如何在 C# 中使用 Aspose.OCR **執行 OCR**，展示如何 **從圖像提取文字**，並以實務範例說明 **辨識印地語文字**。透過六個步驟——設定資源路徑、建立引擎、設定語言、載入圖像、執行辨識、顯示結果——你現在擁有一個可靠的建構模組，可應用於任何文件數位化專案。

接下來，嘗試將 `Language.Hindi` 換成其他語言，或將 OCR 輸出送入自然語言處理管線，自動分類發票。可能性無窮無盡，而核心模式不變：**從圖像讀取文字**，然後依應用需求處理該文字。

對於邊緣案例、效能調校或授權有任何疑問？歡迎在下方留言，祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}