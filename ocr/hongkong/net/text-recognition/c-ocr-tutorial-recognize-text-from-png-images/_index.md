---
category: general
date: 2026-01-13
description: C# OCR 教學，示範如何從 PNG 檔案辨識文字、從影像擷取文字，並使用 Aspose.OCR 處理俄文文字。
draft: false
keywords:
- c# ocr tutorial
- recognize text from png
- how to extract text from image
- recognize russian text
- load image for ocr
language: zh-hant
og_description: C# OCR 教學：學習如何從 PNG 檔案辨識文字、從影像擷取文字，並使用 Aspose.OCR 處理俄文文字。
og_title: c# OCR 教學 – 從 PNG 圖像辨識文字
tags:
- OCR
- C#
- Aspose
title: C# OCR 教程：從 PNG 圖片辨識文字
url: /zh-hant/net/text-recognition/c-ocr-tutorial-recognize-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR 教學 – 從 PNG 圖片辨識文字

是否曾需要一個 **c# ocr tutorial**，只用幾行程式碼就能將掃描的發票轉換成可編輯的文字？你並不孤單。無論你是在打造帳單自動化工具，或只是想從螢幕截圖中提取資料，從 PNG 圖片辨識文字都是常見的痛點。在本指南中，我們將逐步說明一個完整、可直接執行的範例，展示 *如何從影像中提取文字*，自動載入西里爾語言模組，並將結果輸出至主控台。

> **Quick hook:** 整個解決方案僅在單一 `Main` 方法內，您可以直接複製貼上、按 F5，即可即時看到俄文字符顯示。

我們也會涵蓋幾個「如果…」情境，例如從串流載入影像或處理缺少語言套件的情況，讓您在完成本教學後能獲得全面的理解。

## 您需要的條件

在深入之前，請確保您具備以下條件：

| 需求 | 原因 |
|------|------|
| .NET 6.0 or later (or .NET Framework 4.7+) | Aspose.OCR 兩者皆支援，但 .NET 6 提供最新的執行時改進。 |
| Visual Studio 2022 (or any C# IDE) | 讓除錯與 NuGet 套件管理變得輕鬆無痛。 |
| Internet connection (first run only) | 第一次使用俄文時，西里爾語言模組會自動下載。 |
| A PNG image of a Russian invoice (or any text‑heavy PNG) | 我們將使用 `russian_invoice.png` 作為示範檔案。 |

如果您已經有專案，則可跳過建立步驟。否則，開啟終端機並執行以下指令：

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

現在您已擁有一個乾淨的主控台專案，可用於 **c# ocr tutorial**。

## 步驟 1：透過 NuGet 安裝 Aspose.OCR

Aspose.OCR 為商業套件，但提供完整功能的免費試用版。使用以下指令將其加入您的專案：

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** 若您位於公司代理伺服器之後，請在執行指令前設定 `http_proxy` 環境變數；否則套件下載可能失敗。

此套件會包含 `Aspose.OCR.dll`、`Aspose.OCR.Common.dll`，以及少量語言資料檔。西里爾語言包（用於俄文）未隨套件一起提供，會在需要時下載，以減少初始體積。

## 步驟 2：載入影像以進行 OCR

**load image for ocr** 步驟出奇地簡單。Aspose.OCR 透過 `OcrImage` 類別抽象化檔案處理，能從檔案路徑、`Stream` 或甚至位元組陣列讀取。以下是最常見的寫法：

```csharp
using Aspose.OCR;

// ...

// Step 2: Load the PNG file you want to process.
// Replace the path with the actual location of your invoice image.
string imagePath = Path.Combine(Environment.CurrentDirectory, "russian_invoice.png");

// OcrImage.FromFile automatically detects the format (PNG, JPEG, etc.).
OcrImage invoiceImage = OcrImage.FromFile(imagePath);
```

如果影像儲存在資料庫 BLOB 中，您可以將 `FromFile` 呼叫改為 `FromStream(new MemoryStream(blobBytes))`。函式庫會將兩種情況視為相同。

## 步驟 3：從 PNG 辨識文字

現在進入 **c# ocr tutorial** 的核心——呼叫 OCR 引擎。`OcrEngine` 類別輕量，您可以重複使用單一實例處理多張影像，或在每次請求時建立新實例以確保隔離。

```csharp
// Step 3: Create the OCR engine.
using var ocrEngine = new OcrEngine();

// Recognize Russian text; the Cyrillic language pack is fetched automatically.
// If you wanted English, you’d pass OcrLanguage.English instead.
OcrResult ocrResult = ocrEngine.Recognize(invoiceImage, OcrLanguage.Russian);
```

在背後，Aspose 會檢查本機是否已有西里爾語言資料檔。若未存在，會從 Aspose 的 CDN 下載，並存放於快取資料夾（Windows 上為 `%USERPROFILE%\.Aspose\OCR`），之後才開始辨識。這也是為何首次執行可能需要數秒，而之後的執行則即時完成。

### 若下載失敗該怎麼辦？

網路偶發問題在所難免。請將呼叫包在 try‑catch 區塊中，並回退至內建語言（例如英文）或拋出友善的錯誤訊息：

```csharp
try
{
    OcrResult ocrResult = ocrEngine.Recognize(invoiceImage, OcrLanguage.Russian);
    // Use ocrResult...
}
catch (Aspose.OCR.Exceptions.OcrLicenseException ex)
{
    Console.WriteLine("Language pack download failed: " + ex.Message);
    // Optionally retry or switch language.
}
```

## 步驟 4：擷取並顯示結果

`OcrResult` 物件包含原始文字、信心分數以及每個單字的邊界框。對於大多數簡單情況，只需使用 `Text` 屬性即可：

```csharp
// Step 4: Output the recognized text.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

### 預期輸出

若 `russian_invoice.png` 包含類似 `Сумма: 1 200,00 ₽` 的行，主控台將會輸出：

```
=== OCR Output ===
Сумма: 1 200,00 ₽
```

請注意正確的西里爾字符以及金額中使用的不換行空格。Aspose.OCR 完全保留影像中的 Unicode 編碼。

## 步驟 5：完整可執行範例

將上述所有步驟整合起來，以下是一個 **完整、獨立** 的程式，您可以直接貼入 `Program.cs`。不需額外參考，也沒有隱藏步驟。

```csharp
using System;
using System.IO;
using Aspose.OCR;

class AutoDownloadDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance.
        using var ocrEngine = new OcrEngine();

        // 2️⃣ Load the PNG image you want to process.
        //    Update the path to point at your own file.
        string imagePath = Path.Combine(Environment.CurrentDirectory, "russian_invoice.png");
        OcrImage invoiceImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Recognize the text, automatically fetching the Russian (Cyrillic) module.
        OcrResult ocrResult;
        try
        {
            ocrResult = ocrEngine.Recognize(invoiceImage, OcrLanguage.Russian);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"⚠️ OCR failed: {ex.Message}");
            return;
        }

        // 4️⃣ Display the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**執行它：**  
```bash
dotnet run
```

您應該會在主控台看到擷取出的俄文文字。若語言包尚未快取，首次執行會下載約 2 MB 的檔案；之後的執行則幾乎即時。

## 常見變形與邊緣案例

| 情境 | 如何調整 |
|------|----------|
| **Image is a JPEG instead of PNG** | 相同的 `OcrImage.FromFile` 呼叫即可使用；函式庫會自動偵測格式。 |
| **You need to process many images in a batch** | 在 `foreach` 迴圈中重複使用同一個 `OcrEngine` 實例；只需更換 `Recognize` 呼叫的影像。 |
| **You only want numbers (e.g., invoice totals)** | OCR 完成後，使用正規表達式（如 `\d[\d\s,]*\d`）過濾 `ocrResult.Text`。 |
| **Running on Linux/macOS** | 確保已安裝 `libgdiplus` 相依套件（`sudo apt-get install -y libgdiplus`）。 |
| **Memory constraints** | 使用完畢後釋放每個 `OcrImage`：`invoiceImage.Dispose();` |

## 專業提示，讓 **c# ocr tutorial** 體驗更順暢

- **手動快取語言包**：若有多台機器在防火牆後，請將 `%USERPROFILE%\.Aspose\OCR` 資料夾複製至每台目標機器。  
- **微調 OCR 引擎**：透過調整 `ocrEngine.Config`（例如將 `PageSegMode = PageSegMode.SingleLine` 設為單行收據）。  
- **記錄信心分數**：`ocrResult.Confidence` 為每個單字提供 0‑1 的分數，可用於標記低信心結果以供人工審核。  
- **結合 PDF 轉換**：Aspose.PDF 可將 PDF 頁面渲染為 PNG，之後再送入相同的 OCR 流程。  

## 結論

您剛完成一個 **c# ocr tutorial**，示範了如何 **recognize text from png** 檔案、**how to extract text from image**，以及使用 Aspose.OCR 自動下載功能 **recognize russian text**。此範例展示了完整流程——從載入影像、呼叫引擎、處理語言包取得，到輸出結果。  

接下來您可以延伸應用：將 OCR 結果寫入資料庫、餵入機器學習模型，或打造即時上傳發票的使用者介面。基礎建構已備妥，您可嘗試不同的影像品質、語言或批次處理策略。  

若遇到任何問題——例如缺少 DLL、下載西里爾模組時網路逾時，或出現非預期字元——請回顧「Common Variations & Edge Cases」表格。當然，Aspose 文件（在程式碼註解中有連結）也是深入客製化的好資源。  

祝開發順利，願您的 OCR 結果永遠清晰如晶！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}