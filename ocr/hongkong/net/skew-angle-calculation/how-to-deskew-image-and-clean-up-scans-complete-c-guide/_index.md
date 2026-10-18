---
category: general
date: 2026-03-18
description: 如何校正掃描檔案的影像傾斜並降低噪點。學習從檔案載入影像、從 TIFF 提取文字，以及使用 Aspose OCR 進行影像文字辨識。
draft: false
keywords:
- how to deskew image
- how to reduce noise
- recognize text from image
- load image from file
- extract text from tiff
language: zh-hant
og_description: 如何使用 Aspose OCR 快速校正圖像傾斜。此指南將向您展示如何降低噪點、從檔案載入圖像，以及在 C# 中從 TIFF 提取文字。
og_title: 如何校正影像傾斜 – 完整 C# OCR 教學
tags:
- OCR
- C#
- Image Processing
title: 如何校正影像傾斜與清理掃描檔 – 完整 C# 指南
url: /zh-hant/net/skew-angle-calculation/how-to-deskew-image-and-clean-up-scans-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何校正影像傾斜 – 完整 C# OCR 教學

有沒有想過 **如何校正影像傾斜**，讓看起來像是從晃動的掃描器拍出的檔案變得正確？你並不孤單。大多數開發者在來源 TIFF 稍微歪斜時，都會遇到這個問題，導致 OCR 結果一團糟。好消息是，只要幾行 C# 程式碼，就能把圖片拉直、去除顆粒狀背景，並直接從檔案中擷取乾淨、可搜尋的文字。

在本指南中，我們將逐步說明 **如何降低雜訊**、**從檔案載入影像**，最後 **從影像辨識文字**，全部使用 Aspose OCR。完成後，你就能 **從 tiff 文件擷取文字**，毫不費力。

> **專業小技巧：** 若你已在其他專案中使用 Aspose OCR，只要直接加入這些過濾器，無需額外授權問題。

---

## 需要的環境

- .NET 6 或更新版本（程式碼同樣適用於 .NET Core）  
- Aspose.OCR NuGet 套件（`Install-Package Aspose.OCR`）  
- 一個稍微旋轉或有雜訊的掃描 TIFF（本教學使用 `skewed_scanned_doc.tif` 為例）  
- 文字編輯器或 IDE（Visual Studio、VS Code、Rider – 隨你喜好）

不需要額外的函式庫；我們使用的過濾器皆內建於 Aspose OCR。

---

## 第一步 – 建立 OCR 引擎（如何校正影像傾斜）

首先要建立一個 `OcrEngine`。把它想像成之後會為你讀取字元的大腦。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this object holds all settings
        var ocrEngine = new OcrEngine();
```

為什麼要先建立引擎？這樣可以在同一個位置掛上前處理過濾器、語言套件與輸出選項。如果直接呼叫 `OcrEngine.Recognize`，就失去了先清理影像的機會，而這正是我們需要校正傾斜的原因。

---

## 第二步 – 加入校正與降噪過濾器（如何降低雜訊）

接下來掛上兩個過濾器：

| 過濾器 | 功能說明 | 為什麼重要 |
|--------|----------|------------|
| `AutoDeskewFilter` | 偵測並校正旋轉角度 | 讓文字行變直，OCR 引擎才能正確讀取 |
| `NoiseReductionFilterV2` | 移除斑點與背景顆粒 | 像素更乾淨，誤辨識的機會更低 |

```csharp
        // Add filters to improve OCR accuracy
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // corrects rotation
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduces background noise
```

你也可以改用舊版的 `NoiseReductionFilterV2`，但 v2 演算法對現代掃描器的相容性更好。如果文件本身已經完全平整，校正過濾器只會原樣傳遞影像——不會造成任何傷害。

---

## 第三步 – 從檔案載入影像（從檔案載入影像）

Aspose 提供便利的 `ImageStream.FromFile` 輔助方法，可讀取多種格式，包括 TIFF、JPEG、PNG 與 BMP。以下示範如何將檔案載入記憶體：

```csharp
        // Load the scanned image you want to preprocess
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");
```

將 `YOUR_DIRECTORY` 替換成你機器上的實際路徑。若使用相對路徑，請確保檔案與可執行檔同目錄，或自行設定工作目錄。

---

## 第四步 – 在前處理過的影像上執行 OCR（從影像辨識文字）

過濾器已設定、影像也已載入，現在就請 Aspose 讀取字元：

```csharp
        // Perform OCR – the engine will automatically apply the filters first
        var ocrResult = ocrEngine.Recognize(image);
```

在背後，引擎會先執行校正演算法、平滑雜訊，然後使用神經網路辨識器。結果會包在 `OcrResult` 物件中，提供原始文字、信心分數，甚至如果需要還可以取得文字框座標。

---

## 第五步 – 顯示或儲存擷取的文字（從 TIFF 擷取文字）

為了快速示範，我們直接把文字輸出到主控台，實務上你可以寫入檔案、資料庫，或傳給後續工作流程。

```csharp
        // Show the recognized text in the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

**預期輸出**（範例，實際會依文件不同而異）：

```
Invoice #12345
Date: 2023‑04‑01
Total: $1,250.00
Thank you for your business!
```

如果輸出仍出現亂碼，請再次確認原始 TIFF 的解析度是否足夠（建議最低 300 dpi），以及 `ocrEngine.Settings.Language` 是否正確設定。

---

## 完整範例程式（一次呈現全部步驟）

以下是完整程式碼，你可以直接複製貼上到新的 Console 專案，立即執行。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // deskew image
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduce noise

        // 3️⃣ Load the image file (TIFF, JPEG, etc.)
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");

        // 4️⃣ Recognize text – filters run automatically
        var ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

將檔案存為 `Program.cs`，執行 `dotnet run`，即可在終端機看到已清理的文字。

---

## 常見問題與特殊情況

### 我的 TIFF 有多頁怎麼辦？
Aspose OCR 可透過迴圈 `image.GetPages()`（或 `image.Pages`）處理多頁影像。每一頁都會回傳自己的 `OcrResult`。若需要單一字串，可使用 `StringBuilder` 合併。

### 校正過濾器能處理嚴重旋轉的影像嗎？
它支援約 ±15° 的旋轉角度。若超過此範圍，建議先使用圖形函式庫（例如 `System.Drawing` 或 `SkiaSharp`）手動旋轉，再交給 Aspose。

### 如何提升非英文文字的辨識準確度？
明確設定語言：

```csharp
ocrEngine.Settings.Language = Language.English; // or Language.French, etc.
```

若內建語言套件不支援你的字母表，也可以自行載入自訂語言包。

### 可以在 Linux 上執行嗎？
絕對可以。Aspose OCR 為跨平台套件，只要確保本機有相應的原生相依性（純 .NET 版通常不需要）。使用 `dotnet publish -r linux-x64` 可產生自包含的執行檔。

---

## 加分：視覺化校正後的影像

如果想在 OCR 前先看校正後的結果，可以把影像存回磁碟：

```csharp
// After OCR, the filtered image is stored in ocrEngine.Settings.FiltersResult
var corrected = ocrEngine.Settings.FiltersResult;
corrected.Save(@"output/deskewed_cleaned.tif");
```

![如何校正影像示例](https://example.com/deskew-demo.png "如何校正影像示例")

*圖片替代文字：* **如何校正影像示例** – 顯示一張經 AutoDeskewFilter 校正前後的 TIFF 對比圖。

---

## 結論

我們已說明 **如何校正影像傾斜**、**如何降低雜訊**，以及完整流程：**從影像辨識文字**、**從檔案載入影像**、**從 TIFF 擷取文字**，全部使用 Aspose OCR 於 C# 實作。重點是，只要加入兩個前處理過濾器，就能把晃動、顆粒感的掃描件變成清晰、可搜尋的文件，且不需額外工具。

準備好下一步了嗎？若文件是倒置的，可改用 `AutoRotateFilter`；若印刷品顏色淡薄，可嘗試 `ContrastEnhancementFilter`。相同的模式——引擎 → 過濾器 → 載入 → 辨識——適用於所有 Aspose OCR 情境，讓你輕鬆重用此骨架於 PDF、PNG，甚至相機照片。

祝程式開發順利，OCR 準確度天天提升！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}