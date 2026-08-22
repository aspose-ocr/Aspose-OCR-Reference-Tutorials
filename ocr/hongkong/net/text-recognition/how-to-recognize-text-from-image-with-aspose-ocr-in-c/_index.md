---
category: general
date: 2026-08-22
description: 學習使用 Aspose.OCR 從圖像辨識文字。本指南亦涵蓋 OCR 圖像轉文字，並在幾個步驟內從 JPG 提取文字。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- ocr image to text
- extract text from jpg
- convert image to text
- read cyrillic text image
language: zh-hant
lastmod: 2026-08-22
og_description: 使用 Aspose.OCR 於 C# 識別圖像文字。跟隨本教學將圖像 OCR 為文字，從 JPG 提取文字，並讀取西里爾文字圖像。
og_image_alt: Screenshot of C# console output showing recognized Cyrillic text from
  a JPG image
og_title: 使用 Aspose.OCR 從圖像辨識文字 – C# 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-08-22'
  description: Learn to recognize text from image using Aspose.OCR. This guide also
    covers OCR image to text and extract text from jpg in a few steps.
  headline: How to recognize text from image with Aspose.OCR in C#
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中使用 Aspose.OCR 從圖像識別文字
url: /zh-hant/net/text-recognition/how-to-recognize-text-from-image-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.OCR 從圖像辨識文字 – 完整 C# 教程

如果您需要在 .NET 專案中辨識圖像中的文字，本教學將提供一個可直接執行的解決方案。您將會看到如何設定 OCR 引擎、選擇正確的語言模組，以及輸出擷取出的字元。範例亦示範如何將西里爾語圖片的圖像 OCR 成文字，涵蓋了常見的西里爾文字圖檔讀取情境。

除了核心步驟之外，您還會學會如何從 jpg 檔案擷取文字、將圖像轉換為其他格式的文字，並處理需要自動下載語言模組的情況。除了 Aspose.OCR NuGet 套件外，無需任何外部服務。

## 先決條件

在開始之前，請確保您已具備：

- .NET 6.0 SDK 或更新版本已安裝  
- Visual Studio 2022（或任何支援 C# 的編輯器）  
- 首次執行需要網路連線（會即時下載西里爾語語言模組）  
- Aspose.OCR NuGet 套件 (`dotnet add package Aspose.OCR`)  

上述項目讓您能在不額外設定的情況下編譯並執行程式碼。

## 步驟 1：建立新的主控台專案

在終端機中執行以下指令，以產生最小的主控台應用程式：

```bash
dotnet new console -n ImageOcrDemo
cd ImageOcrDemo
dotnet add package Aspose.OCR
```

`dotnet new console` 指令會建立 `Program.cs` 檔案以及一個參考 Aspose.OCR 函式庫的專案檔。加入套件後會解決所有必要的組件。

## 步驟 2：匯入 Aspose.OCR 命名空間

編輯 **Program.cs**，在檔案頂部加入 `using Aspose.OCR;` 指示。這樣即可在不使用完整限定名稱的情況下使用 OCR 類別。

```csharp
using System;
using Aspose.OCR;
```

`using` 陳述式提升可讀性，讓程式碼更專注於 OCR 工作流程。

## 步驟 3：初始化 OCR 引擎

建立 `OcrEngine` 實例。此引擎負責保存語言模組與辨識設定等組態。

```csharp
// Initialise the OCR engine
var ocrEngine = new OcrEngine();
```

在整個應用程式生命週期只建立一次引擎較為有效率，因為底層的原生函式庫僅會載入一次。

## 步驟 4：選擇語言模組

對於西里爾文字，將 `Language` 屬性設為 `Language.Cyrillic`。若系統缺少該模組，Aspose.OCR 會自動下載，因此首次執行可能需要幾秒鐘。

```csharp
// Choose Cyrillic language module – it will be downloaded if absent
ocrEngine.Language = Language.Cyrillic;
```

若日後需要以其他語言（例如 English 或 Arabic）進行圖像 OCR，只需將 `Language.Cyrillic` 替換為相應的列舉值。此彈性讓您能對任何支援的文字系統執行圖像轉文字。

## 步驟 5：從 JPG 檔案辨識文字

呼叫 `RecognizeImage` 並傳入圖像的完整路徑。此方法會回傳包含擷取字串的 `OcrResult`。

```csharp
// Path to the source image – replace with your own file
string imagePath = @"YOUR_DIRECTORY/sample_image.jpg";

// Perform OCR – this extracts text from the JPG file
OcrResult result = ocrEngine.RecognizeImage(imagePath);
```

此呼叫支援 Aspose.OCR 所支援的任何點陣圖格式（JPG、PNG、BMP、TIFF）。使用 JPG 可直接從 jpg 檔案擷取文字，無需額外轉換步驟。

## 步驟 6：輸出辨識結果文字

最後，將辨識出的文字寫入主控台。此範例示範了讀取西里爾文字圖像並顯示的簡易方式。

```csharp
// Show the recognised text in the console
Console.WriteLine("Recognised text:");
Console.WriteLine(result.Text);
```

執行程式後，您應該會看到西里爾字元以與原圖完全相同的方式列印出來。

## 完整範例程式

以下是完整的 **Program.cs** 檔案，您可以直接複製、貼上並立即執行。

```csharp
using System;
using Aspose.OCR;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Step 2: Choose the language module required for recognition (Cyrillic in this case)
            // The language module will be downloaded automatically if not present
            ocrEngine.Language = Language.Cyrillic;

            // Step 3: Provide the path to the image you want to process
            // You can replace the file name with any JPG, PNG, BMP, or TIFF image
            string imagePath = @"YOUR_DIRECTORY/sample_image.jpg";

            // Step 4: Recognise text from the image file
            OcrResult result = ocrEngine.RecognizeImage(imagePath);

            // Step 5: Output the recognised text
            Console.WriteLine("Recognised text:");
            Console.WriteLine(result.Text);
        }
    }
}
```

### 預期輸出

```
Recognised text:
Пример текста на кириллице
```

實際輸出取決於 `sample_image.jpg` 的內容。如果圖像包含英文文字，只要將 `ocrEngine.Language = Language.English;`，相同程式碼就會回傳英文字串。

## 處理常見問題

| 問題 | 發生原因 | 解決方法 |
|------|----------|----------|
| 語言模組找不到 | 首次執行時嘗試下載模組，但因防火牆限制導致失敗。 | 確保機器能連線至 `https://downloads.aspose.com/ocr`，或自行從 Aspose 入口網站下載模組，並放置於預設資料夾（`%APPDATA%\Aspose\OCR\`）。 |
| 噪點圖像的辨識精度低 | OCR 引擎需要文字與背景之間有明顯的對比度。 | 在呼叫 `RecognizeImage` 前先對圖像進行前處理（例如提升對比度、轉為灰階）。Aspose.OCR 提供 `ImagePreprocessing` 選項可供探索。 |
| 非 JPG 格式 | 部分開發者誤以為程式只能處理 JPG 檔案。 | API 同樣支援 PNG、BMP 與 TIFF。只需在 `imagePath` 中更改檔案副檔名即可。 |
| 大檔案導致處理時間過長 | 較大的圖像需要更多記憶體與 CPU 時間。 | 在辨識前將圖像調整至合理的解析度（例如 1500 × 1500）。 |

以上技巧可協助您在各種情境下可靠地將圖像轉為文字。

## 擴充解決方案

一旦能夠從圖像辨識文字，您可能想要：

- **將結果儲存至檔案** – 將 `result.Text` 寫入 `.txt` 或 `.docx` 文件。  
- **批次處理資料夾** – 迭代目錄中的所有檔案，套用相同的 OCR 邏輯。  
- **結合正規表達式** – 從辨識出的字串中抽取電話號碼、日期或其他模式。  

所有這些擴充皆使用相同的核心程式碼，保持實作簡潔。

## 結論

您現在已掌握使用 Aspose.OCR 在 C# 中從圖像辨識文字的完整指南。教學說明了如何建立專案、初始化 OCR 引擎、選取西里爾語言模組，以及從 JPG 檔案擷取文字。依照這些步驟，您亦可為其他語言、jpg 檔案或任何 .NET 應用程式執行圖像轉文字。

歡迎嘗試其他語言、較大的批次或後處理邏輯。如果需要在不同情境（例如 Web API 或 Windows 服務）中讀取西里爾文字圖像，使用相同模式即可。祝開發順利！

## 接下來該學什麼？

以下教學與本指南所示技術密切相關，並可作為進一步學習的資源。每篇文章皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [使用 Aspose.OCR 以語言選擇提取圖像文字 (C#)](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [使用 Aspose OCR 辨識多語言圖像文字](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [OCR 前處理管線 – 如何在 C# 中從圖像辨識文字](/ocr/english/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}