---
category: general
date: 2026-03-26
description: c# OCR 教學，示範如何從圖像提取文字、從 JPEG 識別文字以及載入圖像進行 OCR – 包含西里爾字母支援。
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- recognize text from jpeg
- load image for ocr
- recognize cyrillic text
language: zh-hant
og_description: c# OCR 教學，手把手教你載入影像進行 OCR，從 JPEG 識別文字，並提取西里爾文字，簡單幾步即可完成。
og_title: c# OCR 教程 – 使用 Aspose OCR 從圖像提取文字
tags:
- OCR
- C#
- Aspose
- ImageProcessing
title: C# OCR 教學 – 使用 Aspose OCR 從圖像提取文字
url: /zh-hant/net/text-recognition/c-ocr-tutorial-extract-text-from-image-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr 教學 – 使用 Aspose OCR 從圖像提取文字

有沒有需要一個 **c# ocr 教學**，能夠真正把空白 JPEG 轉成可讀的 Unicode 文字？也許你正在開發文件歸檔工具、收據掃描器，或只是想了解如何從圖片中抽取文字。無論哪種情況，你都來對地方了。在本指南中，我們會示範如何 **從圖像檔案提取文字**、**從 jpeg 識別文字**，甚至處理棘手的 **識別西里爾文字** 情境——全部離線，無需雲端呼叫。

我們將使用 Aspose.OCR，這是一個完整離線的函式庫，提供可在磁碟上指向的語言模組。完成本教學後，你會得到一個自包含的 Console 應用程式，能載入圖像進行 OCR、執行引擎，並將結果印到主控台。沒有外部服務、沒有 API 金鑰——純粹的 C#。

## 需要的環境

- .NET 6.0 或更新版本（程式碼同樣支援 .NET Core 與 .NET Framework）
- Visual Studio 2022 或任何你慣用的 IDE
- Aspose.OCR NuGet 套件 (`Aspose.OCR`) 以及對應的 `Aspose.OCR.Resources` 資料夾
- 一張包含西里爾字元的 JPEG 圖片（或任何你想測試的語言）

如果缺少上述任一項，請在套件管理員主控台中安裝 NuGet 套件：

```powershell
Install-Package Aspose.OCR
```

然後從 Aspose 官方網站下載語言資源，解壓縮至類似 `C:\OCR\Aspose.OCR.Resources` 的資料夾。

現在，開始吧。

## 步驟 1：載入 OCR 資源 – load image for ocr

引擎首先需要語言模組的路徑。把它想成告訴 OCR 辭典在哪裡。

```csharp
using Aspose.OCR;
using Aspose.OCR.Resources;

// Point to the folder that contains the language modules
ResourceManager.SetLocalResourcesPath(@"C:\OCR\Aspose.OCR.Resources");
```

> **小技巧：** 開發階段使用絕對路徑。發佈應用程式時，可考慮將資源嵌入或放在執行檔旁邊。

## 步驟 2：選擇語言 – recognize cyrillic text

Aspose 支援數十種語言，但必須自行選擇需要的那一種。對於西里爾文字，我們使用 `OcrLanguage.CyrillicExtended`。若只需要拉丁字元，則改成 `OcrLanguage.English`。

```csharp
// Create the OCR engine and set the language
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.CyrillicExtended   // This enables Cyrillic recognition
};
```

為什麼這麼重要？引擎會載入特定語言的分類器；選錯語言會大幅降低準確度。

## 步驟 3：載入 JPEG – recognize text from jpeg

接著載入要掃描的圖片。Aspose 能讀取常見格式，如 JPEG、PNG、BMP、TIFF。

```csharp
// Load the image file (replace with your own path)
var ocrImage = OcrImage.FromFile(@"C:\OCR\Samples\cyrillic_doc.jpg");
```

如果圖像過大，建議先縮小再送入引擎——這樣可以加快處理速度並減少記憶體使用。

## 步驟 4：執行辨識 – extract text from image

引擎已配置好且圖像已在記憶體中，辨識只需要一行程式碼。

```csharp
// Perform the OCR operation
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);
```

在背後，引擎會先執行一系列前處理（去噪、二值化），再將視覺模式與選定的語言模型比對。

## 步驟 5：顯示結果 – extract text from image

最後，我們把辨識出的字串輸出。實務上，你可能會把它寫入檔案、資料庫，或送入搜尋索引。

```csharp
// Print the extracted text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**預期輸出**（假設範例圖像包含「Привет мир!」）：

```
=== OCR Output ===
Привет мир!
```

如果看到亂碼，請再次確認已選擇正確的語言，且圖像沒有過於雜訊。

## 完整範例程式

以下是可直接複製貼上的完整程式。將它存為 `Program.cs`，放入新建的 Console 專案後執行。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Resources;

class OfflineOcrDemo
{
    static void Main()
    {
        // Step 1: Point the OCR engine to the folder that contains the language modules
        ResourceManager.SetLocalResourcesPath(@"C:\OCR\Aspose.OCR.Resources");

        // Step 2: Create the OCR engine and select the required language (Cyrillic Extended)
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.CyrillicExtended
        };

        // Step 3: Load the image that contains the text to be recognized
        var ocrImage = OcrImage.FromFile(@"C:\OCR\Samples\cyrillic_doc.jpg");

        // Step 4: Perform the recognition operation
        OcrResult ocrResult = ocrEngine.Recognize(ocrImage);

        // Step 5: Display the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **注意：** 請將路徑替換成你機器上的實際位置。程式在離線環境下即可運作，無需網路連線，只要資源已備妥。

## 常見問題與特殊情況

### 我的圖像是 PNG 而不是 JPEG，該怎麼辦？
Aspose.OCR 會把 PNG 視為與 JPEG 相同的處理方式。只要在 `FromFile` 中改成相應的副檔名即可。**recognize text from jpeg** 步驟同樣適用於所有支援的格式。

### 如何提升低品質掃描的準確度？
- 使用 `ocrImage.AdjustContrast(1.2)` 或類似方法對圖像做前處理（提升對比、去斜）。
- 在呼叫 `Recognize` 前先執行 `OcrEngine.PreprocessImage`。
- 選擇與文字腳本相符的語言；若同時包含拉丁與西里爾，可設定 `Language = OcrLanguage.Multilingual`。

### 能只抽取數字或日期嗎？
可以。取得 `ocrResult.Text` 後，使用正規表達式過濾所需部分。OCR 本身只回傳原始字串，後續的解析由你自行處理。

### 能在 Linux 上執行嗎？
當然可以。Aspose.OCR 是跨平台的。只要在 Linux 主機上安裝 .NET 執行環境，並將 `SetLocalResourcesPath` 指向正確的資料夾即可。

## 生產環境小技巧

- **快取 OcrEngine**：每次請求都新建引擎會增加開銷。若大量處理圖像，建議使用單例。
- **執行緒安全**：預設情況下引擎不是執行緒安全的。可在 `Recognize` 前加鎖，或為每個執行緒建立獨立的引擎實例。
- **記憶體管理**：使用完 `OcrImage` 後務必呼叫 `ocrImage.Dispose()`，釋放原生緩衝區。
- **日誌記錄**：捕捉 `ocrResult.Confidence`（若有）以偵測低信心的掃描，並觸發備援機制。

## 結論

現在你已掌握一套 **c# ocr 教學**，完整說明如何 **load image for ocr**、**recognize text from jpeg**、**extract text from image**，以及 **recognize cyrillic text**，全程使用 Aspose.OCR。範例程式已可直接執行，說明也闡述了每行程式碼背後的原因——不只是「怎麼做」。

接下來，你可以嘗試其他語言、將 OCR 整合至 Web API，或把抽出的字串餵入搜尋引擎。可能性與你提供的圖像一樣無限。

若在實作過程中遇到問題，歡迎在下方留言或查閱 Aspose 官方文件以取得更深入的設定說明。祝開發順利，願你的圖像永遠清晰可辨！

![c# ocr tutorial screenshot showing console output of extracted text](/images/ocr-demo.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}