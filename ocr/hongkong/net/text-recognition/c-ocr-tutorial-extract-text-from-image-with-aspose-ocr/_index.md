---
category: general
date: 2026-01-01
description: c# OCR 教學示範如何從圖片提取文字，使用 Aspose OCR 對 JPG 檔案執行 OCR。學習載入圖片進行 OCR 並獲得精確結果。
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- perform ocr on jpg
- load image for ocr
language: zh-hant
og_description: c# OCR 教學，逐步指導您從圖像提取文字、對 JPG 進行 OCR，以及使用 Aspose 載入圖像進行 OCR。
og_title: c# OCR 教學 – 使用 Aspose OCR 從圖像提取文字
tags:
- OCR
- C#
- Aspose
title: C# OCR 教學：使用 Aspose OCR 從圖像提取文字
url: /zh-hant/net/text-recognition/c-ocr-tutorial-extract-text-from-image-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR 教學 – 使用 Aspose OCR 從圖像提取文字

在尋找一個實際可用的 **c# ocr tutorial** 嗎？在本指南中，我們將示範如何使用 Aspose.OCR 函式庫 **從圖像提取文字** 以及 **對 JPG 檔案執行 OCR**。無論你是要建立收據掃描器、文件歸檔系統，或只是對從圖片讀取文字感到好奇，以下步驟都能讓你在幾分鐘內從零開始得到可執行的程式碼。

我們會涵蓋所有必需的內容：安裝套件、載入圖像以進行 OCR、設定語言資源、執行辨識引擎，以及處理最常見的陷阱。完成後，你將擁有一個獨立的主控台應用程式，能將辨識出的文字印在螢幕上——不需要任何外部服務。

## 需要的環境

- .NET 6.0 或更新版本（此程式碼亦相容 .NET Framework 4.6+）  
- Visual Studio 2022、VS Code，或任何你偏好的 C# 編輯器  
- 含有俄文（西里爾字母）文字的圖像檔，例如 `receipt_ru.jpg`  
- 首次執行時需要網路連線（Aspose 會自動下載語言資源）  

如果你已經具備上述條件，太好了——讓我們開始吧。

## 步驟 1：安裝 Aspose.OCR 並建立新專案

首先，將 Aspose.OCR NuGet 套件加入你的專案。於解決方案資料夾開啟終端機並執行：

```bash
dotnet add package Aspose.OCR
```

> **小技巧：** 使用 `--version` 參數鎖定最新的穩定版，例如 `Aspose.OCR 23.9.0`。

接著，建立一個簡易的主控台專案（如果你已經有專案可略過此步）：

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

現在你有了一個乾淨的起點，之後可以貼上完整的範例程式碼。

## 步驟 2：載入圖像以進行 OCR

載入圖像是任何 **c# ocr tutorial** 的第一個功能步驟。Aspose.OCR 支援檔案路徑、串流，甚至 `Bitmap`。在本例中，我們直接從磁碟載入：

```csharp
using Aspose.OCR;
using System;

class Program
{
    static void Main()
    {
        // Step 2: Load the image you want to process.
        // Replace the path with the actual location of your JPG file.
        var inputImage = OcrImage.FromFile(@"YOUR_DIRECTORY/receipt_ru.jpg");

        // The rest of the tutorial continues below...
    }
}
```

> **為什麼重要：** 明確載入圖像可讓引擎有清晰的目標，提升辨識精度——尤其在處理多頁 PDF 或混合格式輸入時。

## 步驟 3：設定語言與自動下載資源

Aspose.OCR 隨附可按需下載的語言套件。啟用自動下載可確保引擎在首次執行程式碼時取得俄文語言資料。

```csharp
        // Step 3: Create the OCR engine and configure settings.
        var ocrEngine = new OcrEngine();

        // Enable automatic download of language resources.
        ocrEngine.Settings.AutoDownloadResources = true;

        // Set the language to Russian (Cyrillic). You can change this to OcrLanguage.English, etc.
        ocrEngine.Settings.Language = OcrLanguage.Russian;
```

> **說明：**  
> • `AutoDownloadResources = true` 省去手動取得 `.dat` 檔案的步驟。  
> • 設定 `Language` 告訴引擎預期的字元集，顯著提升辨識速度與精度。

## 步驟 4：執行 OCR 並取得辨識文字

現在開始執行繁重的工作。`Recognize` 方法會處理圖像，並回傳包含擷取字串的 `OcrResult` 物件。

```csharp
        // Step 4: Perform OCR on the loaded image.
        var ocrResult = ocrEngine.Recognize(inputImage);

        // Step 5: Output the recognized text to the console.
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
```

執行程式後，你應該會看到類似以下的輸出：

```
Recognized text:
Счет № 12345
Дата: 01/01/2026
Сумма: 1 250,00 ₽
```

> **預期結果：** 具體輸出取決於原始圖像的品質，但 Aspose 基於神經網路的引擎通常能高忠實度處理乾淨的收據與印刷表單。

## 完整可執行範例

以下是結合所有步驟的 **完整、可執行程式碼**。將其複製貼上至 `Program.cs`，將 `YOUR_DIRECTORY` 替換為實際的資料夾路徑，然後執行 `dotnet run`。

```csharp
using Aspose.OCR;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance.
        var ocrEngine = new OcrEngine();

        // Step 2: Enable automatic download of language resources.
        ocrEngine.Settings.AutoDownloadResources = true;

        // Step 3: Set the language to Russian (Cyrillic) for recognition.
        ocrEngine.Settings.Language = OcrLanguage.Russian;

        // Step 4: Load the image containing Russian text.
        var inputImage = OcrImage.FromFile(@"YOUR_DIRECTORY/receipt_ru.jpg");

        // Step 5: Perform OCR on the loaded image.
        var ocrResult = ocrEngine.Recognize(inputImage);

        // Step 6: Output the recognized text.
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **提示：** 若需 **從圖像提取文字** 的檔案類型不是 JPG（如 PNG、BMP、TIFF），只要更改副檔名即可——Aspose 都能處理。

## 步驟 5：常見問題與小技巧

| 問題 | 發生原因 | 解決方式 |
|-------|----------------|-----|
| **雜訊字元** | 低解析度圖像或過度壓縮 | 使用較高品質的來源，或使用 `Bitmap` 進行前處理（例如提升對比度） |
| **語言未被辨識** | 語言套件未下載 | 確保 `AutoDownloadResources` 為 `true`，且首次執行時機器具備網路連線 |
| **`ocrResult.Text` 為 null** | 圖像路徑不正確或檔案遺失 | 驗證路徑，載入前使用 `File.Exists` 檢查 |
| **效能延遲** | 大量圖像依序處理 | 在多次呼叫間重複使用同一個 `OcrEngine` 實例 |

### 加分項目：在迴圈中讀取多個檔案

如果需要對資料夾中的 **JPG 檔案執行 OCR**，可將邏輯包在 `foreach` 迴圈中：

```csharp
string[] files = Directory.GetFiles(@"YOUR_DIRECTORY", "*.jpg");
foreach (var file in files)
{
    var img = OcrImage.FromFile(file);
    var result = ocrEngine.Recognize(img);
    Console.WriteLine($"File: {Path.GetFileName(file)}");
    Console.WriteLine(result.Text);
    Console.WriteLine(new string('-', 40));
}
```

此模式可順利擴展至收據處理流程。

## 結論

你剛完成了一個 **c# ocr tutorial**，示範如何使用 Aspose.OCR **從圖像提取文字**、**對 JPG 執行 OCR**，以及 **載入圖像以進行 OCR**。此範例程式展示了完整流程——從安裝 NuGet 套件到印出辨識出的西里爾文字——讓你可以立即將其複製到任何 .NET 專案中。

準備好進一步了嗎？試著將 `OcrLanguage.Russian` 換成 `OcrLanguage.English` 以辨識英文收據，或嘗試 `OcrEngine.Settings` 的各項設定（例如 `PageSegmentationMode`、`ImagePreprocessing`）來微調精度。你也可以將輸出整合至資料庫、產生 PDF，或送入翻譯 API。

如果遇到任何問題，請參考 Aspose.OCR 文件或在下方留言。祝開發愉快，願你的 OCR 結果永遠清晰如水晶！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}