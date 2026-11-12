---
category: general
date: 2026-09-22
description: 使用 Aspose.OCR 在 C# 中從圖像提取文字。了解如何將圖像轉換為文字、載入圖像進行 OCR，以及高效辨識西里爾文字。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert image to text
- load image for OCR
- recognize text image
- recognize Cyrillic text
language: zh-hant
lastmod: 2026-09-22
og_description: 使用 Aspose.OCR 在 C# 中從圖像提取文字。本教學展示如何將圖像轉換為文字、載入圖像進行 OCR，以及僅用幾行程式碼辨識西里爾文字。
og_image_alt: Diagram showing extract text from image workflow using Aspose.OCR
og_title: 使用 Aspose.OCR 從圖片提取文字 – 逐步 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-09-22'
  description: Extract text from image with Aspose.OCR in C#. Learn how to convert
    image to text, load image for OCR, and recognize Cyrillic text efficiently.
  headline: How to extract text from image using Aspose.OCR in C#
  type: TechArticle
- description: Extract text from image with Aspose.OCR in C#. Learn how to convert
    image to text, load image for OCR, and recognize Cyrillic text efficiently.
  name: How to extract text from image using Aspose.OCR in C#
  steps:
  - name: Install the Aspose.OCR package
    text: 'Open a terminal in your solution folder and run:'
  - name: Create the OCR engine instance
    text: '```csharp using Aspose.OCR; using System.Drawing; // Required for Image
      handling'
  - name: Choose the language to recognize
    text: '```csharp // Step 3: Select Cyrillic as the target language engine.Language
      = OcrLanguage.Cyrillic; ```'
  - name: Load image for OCR
    text: '```csharp // Step 4: Load the image that contains the text engine.Image
      = Image.FromFile(@"YOUR_DIRECTORY\sample_cyrillic.png"); ```'
  - name: Perform the recognition and get the result
    text: '```csharp // Step 5: Run the recognition process string recognizedText
      = engine.Recognize(); ```'
  - name: Output the extracted text
    text: '```csharp // Step 6: Display the extracted text Console.WriteLine("Recognized
      text:"); Console.WriteLine(recognizedText); ```'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image processing
title: 如何在 C# 中使用 Aspose.OCR 從圖像提取文字
url: /zh-hant/net/text-recognition/how-to-extract-text-from-image-using-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.OCR 從圖像提取文字

如果您需要在 .NET 應用程式中 **從圖像提取文字**，本指南將帶您完成一個完整、可直接執行的解決方案。您將看到如何 **將圖像轉換為文字**、載入圖像進行 OCR，並在不需額外設定的情況下處理西里爾字元。

本教學涵蓋您所需的一切：必備的 NuGet 套件、完整的程式碼範例、每一步的說明，以及常見陷阱的提示。完成後，您只需將幾行程式碼貼入專案，即可立即開始辨識文字。

## 您需要的環境

- .NET 6.0 SDK 或更新版本（此程式碼亦可在 .NET Framework 4.7+ 上執行）
- Visual Studio 2022 或任何支援 C# 的 IDE
- 已在專案中安裝 Aspose.OCR NuGet 套件 (`Aspose.OCR`)
- 包含西里爾文字的範例圖像（例如 `sample_cyrillic.png`）

> **小技巧：** 第一次請求未捆綁的語言時，Aspose.OCR 會自動下載所需的模組。此行為即使您能無縫 **辨識西里爾文字**。

## 使用 Aspose.OCR 從圖像提取文字

解決方案的核心是建立 `OcrEngine`、設定語言、載入圖像，並呼叫 `Recognize()`。以下各節將逐步說明每個步驟。

### 步驟 1：安裝 Aspose.OCR 套件

在解決方案資料夾中開啟終端機，執行以下指令：

```bash
dotnet add package Aspose.OCR
```

此指令會將最新穩定版的 Aspose.OCR 加入您的專案檔，確保執行時可使用 OCR 引擎與語言模組。

### 步驟 2：建立 OCR 引擎實例

```csharp
using Aspose.OCR;
using System.Drawing;   // Required for Image handling

// ...

// Step 2: Initialize the OCR engine
OcrEngine engine = new OcrEngine();
```

`OcrEngine` 是所有 OCR 操作的入口點。實例化它會分配圖像分析所需的內部資源。

### 步驟 3：選擇要辨識的語言

```csharp
// Step 3: Select Cyrillic as the target language
engine.Language = OcrLanguage.Cyrillic;
```

設定 `engine.Language` 可告訴 Aspose.OCR 要搜尋哪種字元集。**辨識西里爾文字** 若機器上尚未安裝相應語言包，會自動下載。

### 步驟 4：載入圖像以進行 OCR

```csharp
// Step 4: Load the image that contains the text
engine.Image = Image.FromFile(@"YOUR_DIRECTORY\sample_cyrillic.png");
```

此行使用 `System.Drawing.Image` **載入 OCR 圖像**。將 `YOUR_DIRECTORY` 替換為 PNG 或 JPEG 檔案的實際路徑。引擎現在已持有可供分析的位圖。

### 步驟 5：執行辨識並取得結果

```csharp
// Step 5: Run the recognition process
string recognizedText = engine.Recognize();
```

`Recognize()` 會掃描位圖，套用語言特定模型，並回傳擷取的字串。若圖像清晰且語言設定正確，該方法會返回高準確度的結果。

### 步驟 6：輸出擷取的文字

```csharp
// Step 6: Display the extracted text
Console.WriteLine("Recognized text:");
Console.WriteLine(recognizedText);
```

將結果印到主控台可讓您驗證 **從圖像提取文字** 是否如預期運作。您亦可將文字寫入檔案、資料庫，或傳遞給其他服務。

## 完整、可執行的範例

以下是一個獨立的程式，包含上述所有步驟。將程式碼複製到新的主控台專案 (`dotnet new console`) 中並執行。

```csharp
using System;
using System.Drawing;          // Provides Image class
using Aspose.OCR;              // Aspose OCR namespace

namespace ImageToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            OcrEngine engine = new OcrEngine();

            // Select the language – Cyrillic triggers module download if needed
            engine.Language = OcrLanguage.Cyrillic;

            // Load the image file (adjust the path to your environment)
            string imagePath = @"YOUR_DIRECTORY\sample_cyrillic.png";
            engine.Image = Image.FromFile(imagePath);

            // Perform recognition
            string recognizedText = engine.Recognize();

            // Output the result
            Console.WriteLine("Recognized text:");
            Console.WriteLine(recognizedText);
        }
    }
}
```

**預期輸出**

```
Recognized text:
Пример текста на кириллице
```

若範例圖像包含短語 “Пример текста на кириллице”，主控台將如圖所示精確顯示。字型、尺寸或雜訊的變化可能影響準確度，但 Aspose.OCR 內建的前處理能處理大多數常見情況。

## 處理常見的邊緣情況

| Scenario | What to do | Why it matters |
|----------|------------|----------------|
| 找不到圖像 | 將 `Image.FromFile` 包裹在 `try / catch (FileNotFoundException)` 區塊中，並顯示友善的訊息。 | 防止應用程式當機，並協助使用者找到正確的檔案。 |
| 低對比度圖像 | 將 `engine.ImagePreprocessingOptions` 設為 `ImagePreprocessingOptions.Auto`，或在辨識前手動調整亮度/對比度。 | 在來源圖像較暗時提升 OCR 準確度。 |
| 需要辨識多種語言 | 設定 `engine.Language = OcrLanguage.Multilingual;`，並可選擇加入 `engine.AdditionalLanguages.Add(OcrLanguage.English);`。 | 可偵測混合文字文件（例如西里爾與拉丁混合）。 |
| 大量圖像批次處理 | 重複使用單一 `OcrEngine` 實例，於迴圈中呼叫 `engine.Recognize()`。處理完畢後釋放引擎。 | 減少記憶體分配並加快處理速度。 |

## 可靠 OCR 的最佳實踐

- **使用無損圖像格式**（PNG 或 TIFF）為佳；JPEG 壓縮可能產生干擾辨識器的雜訊。
- **保持圖像解析度** 在 300 dpi 或以上（列印文字），較低解析度可能遺漏小字元。
- **在載入圖像前裁剪不必要的邊框**；多餘的空白會增加處理時間卻無實質價值。
- **驗證輸出**，檢查是否為空字串或出現非預期字元，特別是在處理帶有雜訊的掃描文件時。

## 往後的步驟

既然您已能 **從圖像提取文字**，可以考慮擴充此解決方案：

- **批次將圖像轉換為文字**：讀取圖像目錄，逐一處理檔案，並將結果寫入 CSV 檔案。
- **整合雲端儲存**：從 Azure Blob Storage 或 Amazon S3 取得圖像，執行 OCR，並將擷取的文字儲存回雲端。
- **結合翻譯 API**：在辨識西里爾文字後，呼叫 Azure Translator 或 Google Cloud Translation 產生英文輸出。
- **探索進階版面分析**：Aspose.OCR 提供 `OcrPage` 物件，可取得文字座標，對於重新生成 PDF 或可搜尋文件非常有用。

依照本教學的步驟操作後，您已為任何需要 **將圖像轉換為文字** 或 **辨識文字圖像**（支援多語言）的專案奠定堅實基礎。

---

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並以此技術為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索其他實作方式。

- [如何使用 Aspose.OCR for .NET 從圖像提取文字](/ocr/english/net/text-recognition/get-recognition-result/)
- [使用 Aspose.OCR 以語言選擇提取圖像文字 (C#)](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [使用 Aspose OCR 從圖像提取文字 – C# 快速入門](/ocr/english/net/text-recognition/extract-text-from-image-with-aspose-ocr-c-quickstart/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}