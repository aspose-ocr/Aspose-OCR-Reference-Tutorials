---
category: general
date: 2026-03-17
description: 使用 Aspose OCR 於 C# 從圖像中提取文字。了解如何套用中位數濾波器、載入 OCR 圖像、建立 OCR 引擎，並高效執行 OCR
  識別。
draft: false
keywords:
- extract text from image
- apply median filter
- load image for ocr
- run ocr recognition
- create ocr engine
language: zh-hant
og_description: 快速從影像中提取文字。本指南說明如何建立 OCR 引擎、套用中值濾波、載入影像進行 OCR，以及在 C# 中執行 OCR 識別。
og_title: 使用 Aspose OCR 從圖像提取文字 – 完整 C# 教程
tags:
- OCR
- C#
- Aspose
title: 使用 Aspose OCR 從圖片擷取文字 – 步驟指南
url: /zh-hant/net/text-recognition/extract-text-from-image-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 從圖像提取文字 – 步驟指南

曾經需要 **從圖像提取文字**，卻不確定該選哪個函式庫嗎？在我最近的專案中，我需要從雜訊較多的 JPEG 中抽取手寫筆記，結果 Aspose OCR 成為了可靠的選擇。在本教學中，你將會看到如何 **建立 OCR 引擎**、**載入圖像進行 OCR**、**套用中值濾波**，最後 **執行 OCR 辨識** 取得乾淨的文字輸出。

我們會一步步走過整個流程——從安裝 NuGet 套件到在主控台印出結果——讓你可以直接把完整範例複製貼上到自己的解決方案中。沒有模糊的參考，只有完整、可自行執行的程式碼。

> **快速預覽：** 完成後，你會得到一個 C# 主控台應用程式，讀取 `photo_noisy.jpg`、校正傾斜、使用中值濾波平滑雜訊，最後在螢幕上印出擷取到的字串。

---

## 需要的環境

- **.NET 6+**（或 .NET Core 3.1 – API 相同）
- **Aspose.OCR** NuGet 套件（`Install-Package Aspose.OCR`）
- 一張範例圖像，最好是有雜訊的掃描檔（`photo_noisy.jpg` 效果不錯）
- 任意你喜歡的 IDE——Visual Studio、Rider 或 VS Code

就這些。沒有額外的 DLL、外部服務，也不需要隱藏的設定檔。如果你已經有 .NET 專案，只要加入套件即可開始。

---

## Step 1 – 建立 OCR 引擎（基礎設定）

第一件事就是 **建立 OCR 引擎**。把引擎想像成會解讀像素的“大腦”。沒有它，其他步驟都無從談起。

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

> **為什麼重要：** `OcrEngine` 包含所有預設設定，包括語言偵測與影像前處理。提前實例化可以讓你之後自由客製化。

---

## Step 2 – 套用中值濾波（降雜訊）

雜訊會讓 OCR 卡關。**套用中值濾波** 這一步會在不模糊邊緣的前提下平滑斑點，非常適合文字。

```csharp
// Clear any default filters that Aspose may have added
ocrEngine.Config.Filters.Clear();

// Add a deskew filter to correct any rotation
ocrEngine.Config.Filters.Add(new DeskewFilter());

// Add a median filter with a kernel size of 3
ocrEngine.Config.Filters.Add(new MedianFilter(3));
```

> **小技巧：** 核心大小 `3` 適用大多數顆粒狀照片。若影像非常雜訊，將其調整為 `5`，但要注意可能會失去細小筆畫。

---

## Step 3 – 載入圖像進行 OCR（提供給引擎）

接下來 **載入圖像進行 OCR**。Aspose 提供便利的 `ImageStream.FromFile` 幫手，會把檔案讀成引擎能辨識的格式。

```csharp
// Point to your image file – adjust the path as needed
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/photo_noisy.jpg");
```

> **邊緣情況：** 若圖像位於嵌入式資源中，請改用 `ImageStream.FromStream(yourStream)`。引擎接受任何可解碼成位圖的串流。

---

## Step 4 – 執行 OCR 辨識（取得文字）

引擎已備妥且圖像已載入，現在可以 **執行 OCR 辨識**。這一行程式碼會完成所有重活——前處理、字元分割與語言模型。

```csharp
// Perform the recognition
var ocrResult = ocrEngine.Recognize();

// The Text property holds the extracted string
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrResult.Text);
```

> **你會看到：** 若圖像內含 “Hello World”，主控台會正確輸出該字串，且已去除中值濾波消除的雜訊符號。

---

## Step 5 – 完整範例（可直接複製貼上）

以下是完整程式碼，直接編譯即可。將它存成 `Program.cs` 放在主控台專案內，將 `YOUR_DIRECTORY` 替換成實際資料夾路徑，然後執行 `dotnet run`。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create OCR engine
            var ocrEngine = new OcrEngine();

            // Step 2: Apply filters – deskew + median
            ocrEngine.Config.Filters.Clear();
            ocrEngine.Config.Filters.Add(new DeskewFilter());
            ocrEngine.Config.Filters.Add(new MedianFilter(3));

            // Step 3: Load the image you want to process
            // Make sure the path points to a valid JPEG/PNG/TIFF file
            ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/photo_noisy.jpg");

            // Step 4: Run OCR recognition
            var ocrResult = ocrEngine.Recognize();

            // Step 5: Output the extracted text
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**預期輸出（範例）：**

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

如果圖像完全是空白，`ocrResult.Text` 會是空字串——這只是提醒你檢查圖像路徑或濾波設定。

---

## 常見問題與注意事項

| 問題 | 解答 |
|----------|--------|
| *如果圖像旋轉了 90° 該怎麼辦？* | `DeskewFilter` 會自動偵測並校正小幅旋轉。若角度極端，請在去斜之前自行加入旋轉濾波。 |
| *可以更換語言嗎？* | 可以——在呼叫 `Recognize()` 前設定 `ocrEngine.Config.Language = Language.English;`（或其他支援語言）。 |
| *中值濾波是唯一的降雜訊方式嗎？* | 絕非如此。Aspose 也提供 `GaussianFilter` 與 `BilateralFilter`，可依雜訊類型選擇。 |
| *如何處理多頁 PDF？* | 逐頁迴圈，先將每頁轉成圖像（例如使用 Aspose.PDF），再把每張圖像送入同一個 OCR 引擎。 |
| *如果需要信心分數呢？* | `ocrResult.Confidence` 會回傳 0~1 之間的浮點數，代表整體可信度。 |

---

## 視覺化流程圖

![Extract text from image flow diagram](ocr_flow.png "Extract text from image")

上圖說明了整個流程：**建立 OCR 引擎 → 套用中值濾波 → 載入圖像進行 OCR → 執行 OCR 辨識 → 取得文字**。可作為快速參考，貼在工作桌上。

---

## 結語

我們已完整示範如何在 C# 中使用 Aspose OCR **從圖像提取文字**。透過 **建立 OCR 引擎**、**套用中值濾波**、**載入圖像進行 OCR**，最後 **執行 OCR 辨識**，你現在擁有一套能處理雜訊掃描、收據或手寫筆記的可靠解決方案。

想更進一步的話，可以嘗試：

- 設定 `OcrEngine.Config.Language = Language.Spanish;` 以支援多語言專案。
- 將 `ocrResult.Text` 匯出成 JSON 檔供後續處理。
- 與 `Tesseract` 結合，當 Aspose 在特定字型上表現不佳時採用混合方案。

歡迎自行實驗、調整濾波參數，並在留言區分享你的成果。祝開發順利，圖像永遠可讀！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}