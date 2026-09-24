---
category: general
date: 2025-12-29
description: 學習如何使用 C# OCR 範例從 JPG 辨識文字。從圖像提取文字、將圖像轉換為文字，並在數分鐘內載入圖像進行 OCR。
draft: false
keywords:
- recognize text from jpg
- extract text from image
- c# ocr example
- convert image to text
- load image for ocr
language: zh-hant
og_description: 使用 C# 從 JPG 識別文字。本指南展示如何從圖像提取文字、將圖像轉換為文字，以及載入圖像進行 OCR，並提供完整程式碼範例。
og_title: 在 C# 中從 JPG 辨識文字 – 完整 OCR 教學
tags:
- OCR
- C#
- Image Processing
title: 在 C# 中從 JPG 識別文字 – 完整 OCR 教學
url: /zh-hant/net/text-recognition/recognize-text-from-jpg-in-c-complete-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 JPG 識別文字（C#） – 完整 OCR 教程

是否曾需要 **從 JPG 識別文字**，卻不確定該選擇哪個函式庫？你並不孤單。許多開發者在第一次嘗試從影像檔案（尤其是 JPEG）提取文字時，都會卡在同一個問題上。

在本指南中，我們將一步步示範 **C# OCR 範例**：載入 JPG、執行光學字元辨識，並將結果輸出至主控台。完成後，你將能 **從影像提取文字**、**將影像轉換為文字**，甚至可以將程式碼套用到其他格式。沒有多餘的說明，只有可直接 copy‑paste 的完整解決方案。

## 你將學會

- 如何啟用 Aspose.OCR 的試用模式（或切換至授權金鑰）
- 在 C# 專案中 **載入影像供 OCR 使用** 的完整步驟
- 如何呼叫 OCR 引擎並取得辨識後的字串
- 處理低解析度 JPG 或記憶體洩漏等常見問題的技巧
- 若需要多頁 PDF 或特定語言字典，接下來可以去哪裡

**先備條件**  
你需要 .NET 6+（或 .NET Framework 4.6+）、Visual Studio 2022（或你慣用的 IDE），以及 Aspose.OCR NuGet 套件。若尚未安裝套件，請執行：

```bash
dotnet add package Aspose.OCR
```

基礎建設完成後，讓我們進入程式碼。

![從 JPG 識別文字範例](/images/recognize-text-from-jpg.png "顯示 C# 主控台在辨識 JPG 檔案後的輸出畫面")

## 步驟 1 – 啟用試用模式（或套用授權）

在 OCR 引擎能執行任何操作之前，Aspose 必須先啟用試用模式或載入有效的授權檔。若跳過此步驟，執行時會拋出例外。

```csharp
using Aspose.OCR;

// Enable the free trial – remove this line once you have a license
OcrEngine.EnableTrialMode();
```

*為什麼這很重要*：試用模式會移除「evaluation」浮水印，並在有限期間內解鎖全部功能。日後若加入授權，只需將 `EnableTrialMode` 呼叫改為 `OcrEngine.SetLicense("YourLicenseFile.lic");` 即可。

## 步驟 2 – 建立 OCR 引擎實例

`OcrEngine` 類別是函式庫的核心。通常在整個應用程式中只需要實例化一次，但若需要不同語言設定，也可以建立多個實例。

```csharp
// Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

*小技巧*：若要在迴圈中處理大量影像，請重複使用同一個 `ocrEngine` 物件。這樣可減少開銷，提升批次處理速度。

## 步驟 3 – 載入要處理的 JPG 影像

這一步就是 **載入影像供 OCR 使用**。Aspose.OCR 使用同一命名空間下的 `Image` 類別，無需引用 System.Drawing。

```csharp
// Replace the path with your actual JPG location
var imagePath = @"C:\Images\sample.jpg";
var image = Image.Load(imagePath);
```

*如果檔案不是 JPG 呢？*  
Aspose 也支援 PNG、BMP、TIFF，甚至 PDF 頁面。只要更改檔案副檔名，`Image.Load` 會自動完成相應的載入工作。

## 步驟 4 – 從已載入的影像辨識文字

現在呼叫 `Recognize` 方法。它會回傳一個 `OcrResult` 物件，內含擷取出的字串、信心分數與版面資訊。

```csharp
// Run OCR on the loaded image
var ocrResult = ocrEngine.Recognize(image);
```

*為什麼使用獨立變數*：將結果存入變數後，可稍後檢查 `ocrResult.Confidence` 或 `ocrResult.TextBlocks`，這對除錯或後續處理非常有幫助。

## 步驟 5 – 顯示（或儲存）辨識結果

最後，我們把辨識出的文字輸出到主控台。實際應用中，你可能會將它寫入資料庫、檔案，或透過 API 傳送。

```csharp
// Print the extracted text
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(ocrResult.Text);
```

**預期輸出**

```
=== Recognized Text ===
Hello, world!
This is a sample JPG image.
```

如果輸出呈現亂碼，請嘗試提升影像解析度或套用前置處理濾鏡（例如銳化或二值化）。Aspose.OCR 也提供 `ImagePreprocessor` 供進階調整使用。

## 完整可執行範例

將以下程式碼全部放入同一個檔案，即可編譯執行：

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Enable trial mode (remove when you have a license)
        OcrEngine.EnableTrialMode();

        // 2️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 3️⃣ Load the JPG image
        var imagePath = @"C:\Images\sample.jpg"; // 👉 Change to your file
        var image = Image.Load(imagePath);

        // 4️⃣ Recognize the text
        var ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Show the result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

將程式碼貼到新的 Console App 專案，調整 `imagePath` 後按 **F5**。你應該會在主控台視窗看到擷取出的文字。

## 常見問題與解決方式

| 問題 | 為什麼會發生 | 快速解決方案 |
|------|--------------|--------------|
| **雜訊字元** | 低解析度 JPG 或過度壓縮 | 使用較高解析度的來源，或在辨識前呼叫 `image = ImagePreprocessor.Binarize(image);` |
| **記憶體不足例外** | 在迴圈中處理大量大尺寸影像卻未釋放資源 | 使用 `using` 包裝 `Image.Load` 與 `ocrEngine`，或在每次迭代後呼叫 `image.Dispose();` |
| **語言錯誤** | 預設語言為英文，影像實際為其他語言 | 在 `Recognize` 前設定 `ocrEngine.Language = OcrLanguage.French;`（或任何支援的語言） |
| **效能緩慢** | 單執行緒處理大量檔案 | 使用 `Parallel.ForEach` 並在每個執行緒中重複使用單一 `ocrEngine` 實例 |

## 延伸應用

- **批次處理**：遍歷資料夾內的所有 JPG，收集每個 `ocrResult.Text`，寫入 CSV 檔案。
- **PDF 轉換**：擷取文字後，可將結果交給 PDF 函式庫（如 Aspose.PDF）產生可搜尋的 PDF。
- **語言偵測**：結合 Aspose.OCR 與語言偵測函式庫，自動選擇適當的 OCR 語言。

## 結論

現在你已掌握一個完整的 **C# OCR 範例**，能 **從 JPG 識別文字**、**從影像提取文字**，並以簡短程式碼 **將影像轉換為文字**。只要熟悉 **載入影像供 OCR 使用** 的步驟，就能將此模式套用到任何影像格式，或整合到更大型的文件處理流程中。

準備好接受下一個挑戰了嗎？試著加入影像前置處理以提升準確度，或探索 Aspose 的多語言 OCR 功能。若遇到障礙，請參考官方 Aspose.OCR 文件或在下方留言——祝開發順利！

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}