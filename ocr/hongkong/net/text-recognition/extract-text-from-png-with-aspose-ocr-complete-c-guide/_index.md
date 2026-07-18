---
category: general
date: 2026-07-18
description: 使用 Aspose OCR 於 C# 從 PNG 提取文字。了解如何將影像轉換為文字、對影像執行 OCR，並快速辨識西里爾文字。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from png
- convert image to text
- perform ocr on image
- recognize cyrillic text
- ocr cyrillic image
language: zh-hant
lastmod: 2026-07-18
og_description: 使用 Aspose OCR 從 PNG 提取文字。本指南示範如何將圖像轉換為文字、對圖像執行 OCR，以及僅用幾行 C# 程式碼識別西里爾文字。
og_image_alt: Screenshot showing C# console output after extracting text from a PNG
  image
og_title: 使用 Aspose OCR 從 PNG 中提取文字 – 完整 C# 教程
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Extract text from PNG using Aspose OCR in C#. Learn how to convert
    image to text, perform OCR on image and recognize Cyrillic text quickly.
  headline: Extract Text from PNG with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Extract text from PNG using Aspose OCR in C#. Learn how to convert
    image to text, perform OCR on image and recognize Cyrillic text quickly.
  name: Extract Text from PNG with Aspose OCR – Complete C# Guide
  steps:
  - name: Why Each Piece Matters
    text: '* **`var ocrEngine = new OcrEngine();`** – This creates the engine object
      that holds all OCR settings. Think of it as the “brain” that will analyze the
      pixels. * **`ocrEngine.Language = OcrLanguage.Cyrillic;`** – By explicitly setting
      the language, you tell the engine which character set to expect. '
  - name: 4.1 Dealing with Low‑Resolution PNGs
    text: 'OCR accuracy drops when the source image is under 300 dpi. You can pre‑process
      the image using `System.Drawing` or `ImageSharp` to upscale it:'
  - name: 4.2 Recognizing Multiple Languages
    text: 'If you need to **perform OCR on image** files that contain both Latin and
      Cyrillic characters, set a composite language:'
  - name: 4.3 Saving the Result to a File
    text: 'Instead of printing to the console, you might want a persistent text file:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: 使用 Aspose OCR 從 PNG 提取文字 – 完整 C# 教學
url: /zh-hant/net/text-recognition/extract-text-from-png-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 PNG 提取文字（使用 Aspose OCR） – 完整 C# 指南

有沒有曾經需要 **從 PNG 提取文字**，但不確定哪個函式庫能直接支援西里爾字元？你並不孤單。在許多專案中——例如自動收據處理或多語言文件歸檔——能夠 **將影像轉換為文字** 是每日的痛點。  

好消息是？使用 Aspose.OCR，你只需幾行程式碼即可 **對影像執行 OCR**，而且函式庫會自動下載所需的語言模組。以下示範如何在 PNG 中 **辨識西里爾文字**，並取得乾淨的字串，供後續處理使用。

## 本教學涵蓋內容

我們將一步步說明讓你快速上手所需的一切：

* 安裝 Aspose.OCR NuGet 套件  
* 在 C# 中初始化 OCR 引擎  
* 選擇 **Cyrillic** 語言模型（讓你能 **辨識西里爾文字**）  
* 將 PNG 檔案提供給引擎，讓它自動 **對影像執行 OCR**  
* 將結果輸出至主控台或檔案  

不需要外部工具，也不需要手動下載語言檔案——只要純粹的 C# 程式碼，即可放入任何 .NET 專案中。

---

![OCR 工作流程圖 – 從 PNG 提取文字](/images/ocr-workflow.png "說明 PNG 圖片如何被處理並使用 Aspose OCR 轉換為文字的圖示")

*Image alt text: “說明使用 Aspose OCR 在 C# 中從 PNG 提取文字的流程圖”。*

## 前置條件

在深入之前，請確保你具備以下條件：

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 SDK 或更新版本（此程式碼亦可於 .NET Framework 4.7.2+ 上執行） | 現代執行環境提供最新的語言功能。 |
| Visual Studio 2022（或任何你偏好的編輯器） | 方便加入 NuGet 套件並執行主控台應用程式。 |
| 包含西里爾字元的 PNG 圖片（例如 `sample_cyrillic.png`） | 這是我們將提供給 OCR 引擎的檔案。 |
| 網際網路連線（首次執行時會下載西里爾語言模組） | Aspose.OCR 會依需求取得語言套件。 |

就這樣——不需要額外的 DLL，也不需要外部服務。準備好了嗎？讓我們開始吧。

## 步驟 1：透過 NuGet 安裝 Aspose.OCR

為了保持整潔，我們將建立一個全新的主控台專案，並加入 OCR 函式庫。

```bash
dotnet new console -n OcrCyrillicDemo
cd OcrCyrillicDemo
dotnet add package Aspose.OCR
```

執行 `dotnet add package` 指令會從 NuGet 取得最新的穩定版 Aspose.OCR，其中包含核心 OCR 引擎，但 **不** 包含語言套件——當你設定語言時，系統會自動下載。

> **專業提示：** 若你目標是 .NET Framework，請在 Visual Studio 開啟 NuGet 套件管理員，搜尋 “Aspose.OCR”。同一套件可在各執行環境中使用。

## 步驟 2：建立最小化的 C# 程式

開啟 `Program.cs`，將其內容取代為以下完整範例。此程式碼片段完成所有工作：初始化引擎、選擇西里爾模型、讀取 PNG，並印出辨識出的文字。

```csharp
using System;
using Aspose.OCR;

namespace OcrCyrillicDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // ---------------------------------------------------------
            // Step 2.1: Instantiate the OCR engine – the heart of the process
            // ---------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------
            // Step 2.2: Choose the Cyrillic language model.
            // Aspose will download the necessary module on first use.
            // ---------------------------------------------------------
            ocrEngine.Language = OcrLanguage.Cyrillic;

            // ---------------------------------------------------------
            // Step 2.3: Define the path to the PNG you want to convert.
            // You can also accept this as a command‑line argument.
            // ---------------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY\sample_cyrillic.png";

            // ---------------------------------------------------------
            // Step 2.4: Perform OCR on the image.
            // RecognizeImage returns a string with the extracted text.
            // ---------------------------------------------------------
            string recognizedText = ocrEngine.RecognizeImage(imagePath);

            // ---------------------------------------------------------
            // Step 2.5: Output the result – you could write to a file instead.
            // ---------------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### 為何每個部分都很重要

* **`var ocrEngine = new OcrEngine();`** – 這會建立一個保存所有 OCR 設定的引擎物件。可將其視為分析像素的「大腦」。
* **`ocrEngine.Language = OcrLanguage.Cyrillic;`** – 透過明確設定語言，你告訴引擎預期的字元集。這會大幅提升西里爾文字的辨識準確度，且會自動下載語言套件（無需手動步驟）。
* **`RecognizeImage(imagePath)`** – 此方法讀取 PNG 檔案，執行 OCR 演算法，並回傳純文字字串。這就是核心的 **將影像轉換為文字** 操作。
* **`Console.WriteLine`** – 簡單的方式來驗證提取是否成功。在實務應用中，你可能會將字串儲存至資料庫或傳給翻譯服務。

## 步驟 3：執行應用程式

在終端機中執行以下指令：

```bash
dotnet run
```

首次執行時會顯示短暫的進度條，期間 Aspose 會下載西里爾語言模組（通常只有幾 MB）。之後，你會看到類似以下的輸出：

```
=== Extracted Text ===
Пример текста на кириллице.
```

如果輸出呈現亂碼，請再次確認圖片確實包含清晰的西里爾字元，且檔案路徑正確。

## 步驟 4：處理常見的邊緣情況

### 4.1 處理低解析度 PNG

當來源影像低於 300 dpi 時，OCR 準確度會下降。你可以使用 `System.Drawing` 或 `ImageSharp` 先行處理影像，將其放大。

```csharp
using System.Drawing;
using System.Drawing.Drawing2D;
using System.Drawing.Imaging;

// Load, upscale, and save a temporary higher‑resolution copy.
using (var original = new Bitmap(imagePath))
{
    var upscale = new Bitmap(original.Width * 2, original.Height * 2);
    using (var g = Graphics.FromImage(upscale))
    {
        g.InterpolationMode = InterpolationMode.HighQualityBicubic;
        g.DrawImage(original, 0, 0, upscale.Width, upscale.Height);
    }
    upscale.Save("temp_upscaled.png", ImageFormat.Png);
    recognizedText = ocrEngine.RecognizeImage("temp_upscaled.png");
}
```

### 4.2 辨識多種語言

如果需要 **對影像執行 OCR**，且檔案同時包含拉丁與西里爾字元，請設定複合語言：

```csharp
ocrEngine.Language = OcrLanguage.Cyrillic | OcrLanguage.English;
```

引擎會自動嘗試偵測每種文字腳本。

### 4.3 將結果儲存至檔案

若不想印到主控台，可能會想將結果寫入永久的文字檔：

```csharp
System.IO.File.WriteAllText("extracted_text.txt", recognizedText);
Console.WriteLine("Text saved to extracted_text.txt");
```

## 步驟 5：製作上線就緒的 OCR 提示

* **快取語言模組** – 首次下載後，檔案會存放於使用者的暫存資料夾。於伺服器環境中，請將它們複製到永久位置，並將 `OcrEngine.LanguageFolder` 指向該位置。  
* **設定 `ocrEngine.Config`** – 你可以微調降噪、二值化與旋轉偵測，以提升掃描文件的辨識效果。  
* **批次處理** – 將辨識呼叫包在 `foreach` 迴圈中，以處理數十張 PNG。記得重複使用同一個 `OcrEngine` 實例，以避免重複載入模組。

---

## 結論

現在你已擁有一個可直接運作的端對端範例，使用 Aspose OCR 在 C# 中 **從 PNG 提取文字**。依照上述步驟，你可以 **將影像轉換為文字**、**對影像執行 OCR**，並可靠地 **辨識西里爾文字**——同時讓函式庫自行管理語言模組。

接下來，你可以考慮擴充此解決方案：加入 PDF 輸出、與 Azure Functions 整合以實作無伺服器處理，或將程式碼封裝成可重用的類別庫。其可能性與你將會遇到的各種文字腳本同樣廣闊。

對於處理其他字母、調整效能或與 UI 整合有任何問題嗎？歡迎留言，祝編程愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南技術密切相關的主題。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [使用 Aspose.OCR 進行語言選擇的 C# 圖像文字提取](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [如何透過設定矩形於 OCR 中提取圖像文字](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [將影像轉換為文字 – 從 URL 執行 OCR](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}