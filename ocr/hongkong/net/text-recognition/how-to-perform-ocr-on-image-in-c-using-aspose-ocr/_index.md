---
category: general
date: 2026-10-11
description: 學習如何在 C# 中使用 Aspose.OCR 進行圖像 OCR，包括安裝 System.Drawing.Common 以及從 JPG 檔案提取文字。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: zh-hant
lastmod: 2026-10-11
og_description: 在 C# 中使用 Aspose.OCR 執行圖像 OCR。本指南示範如何安裝 System.Drawing.Common、載入圖像進行
  OCR，並從 JPG 提取文字。
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: 在 C# 中對圖像執行 OCR – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中使用 Aspose.OCR 進行圖像 OCR
url: /zh-hant/net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.OCR 執行影像 OCR

如果您需要在 .NET 應用程式中 **執行影像 OCR**，本指南將為您展示完整解決方案。使用 Aspose.OCR，您可以快速 **從圖片辨識文字**（如 JPG）並在主控台視窗中顯示結果。

您將學會：

* **install System.Drawing.Common package** – 提供 `Image` 類別的函式庫，
* **load image for OCR** – 將 JPEG 或 PNG 讀入記憶體，
* 設定語言模型，
* **perform OCR on image**，最後，
* **extract text from JPG** 並輸出。

這些步驟以 .NET 6+ 為基礎撰寫，但同樣適用於 .NET Framework 4.6.1 以上的版本。

---

## 前置條件

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6 SDK (or .NET Framework 4.6.1+) | 提供 C# 主控台應用程式的執行環境。 |
| Visual Studio 2022 (or any IDE) | 方便加入 NuGet 套件並執行程式。 |
| Internet connection (first run only) | Aspose.OCR 會自動下載語言模組。 |
| A sample image containing Cyrillic or Latin text (e.g., `sample_cyrillic.jpg`) | 用於示範 **extract text from JPG**。 |

---

## 步驟 1：安裝 System.Drawing.Common 套件

`System.Drawing.Common` NuGet 套件提供 `Image` 類別，您將使用它 **load image for OCR**。開啟套件管理員主控台並執行以下指令：

```powershell
Install-Package System.Drawing.Common
```

> **專業提示：** 若在 Linux/macOS 上遇到平台特定的警告，請將目標設定為 `net6.0-windows`，或在專案檔中加入 `<UseWindowsForms>true</UseWindowsForms>`。

---

## 步驟 2：加入 Aspose.OCR NuGet 套件

Aspose.OCR 包含 OCR 引擎與語言模型。使用以下指令安裝：

```powershell
Install-Package Aspose.OCR
```

此套件體積輕盈；所需的語言資料（例如西里爾文）會在您首次設定 `OcrEngine.Language` 時自動下載。

---

## 步驟 3：如何載入影像以供 OCR

載入圖片是執行 **perform OCR on image** 前的第一個具體步驟。`Image.FromFile` 方法可讀取 GDI+ 支援的任何格式，包括 JPG、PNG、BMP 與 TIFF。

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*如果檔案不存在，會拋出 `FileNotFoundException` —— 在正式環境中請將呼叫包在 try/catch 區塊內。*

---

## 步驟 4：設定引擎並 **perform OCR on image**

建立 `OcrEngine` 實例，選取語言模型，指派已載入的影像，然後呼叫 `Recognize()`。

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

`Recognize()` 方法會回傳 `OcrResult` 物件，其中包含擷取的文字、信心分數與邊界框。語言模組會在首次使用時自動下載，無需額外檔案。

---

## 步驟 5：**Extract text from JPG** 並顯示

現在您可以 **recognize text from picture** 並輸出結果。`OcrResult` 的 `Text` 屬性包含純文字字串。

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### 預期的主控台輸出

```
Recognized text:
Пример текста на кириллице
```

如果來源影像包含英文文字，輸出將會是您在圖片中放置的英文句子。

---

## 邊緣情況與最佳實踐提示

| Situation | Recommendation |
|-----------|----------------|
| **Large images ( > 5 MB )** | 在 OCR 前將影像長邊縮小至 ≤ 2000 px，以降低記憶體使用量並提升速度。 |
| **Multiple languages in one picture** | 除了西里爾文外，呼叫 `ocrEngine.AddLanguage(OcrLanguage.English)`，然後將 `ocrEngine.Language = OcrLanguage.Multilingual`。 |
| **Low‑contrast scans** | 在將位圖傳遞給引擎之前，使用 `System.Drawing.Graphics` 提高對比度。 |
| **Running on Linux/macOS** | 確保已安裝 `libgdiplus` 原生相依性（`sudo apt-get install -y libgdiplus`）。 |
| **Repeated OCR calls** | 重複使用同一個 `OcrEngine` 實例，僅更換 `ocrEngine.Image`，以避免重複載入模組。 |

---

## 完整、可執行的程式

以下是結合所有前述步驟的完整主控台應用程式。將程式碼複製到新的 C# 主控台專案，替換影像路徑後執行。

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**執行程式** 會在主控台印出辨識出的字串，證明您已成功 **performed OCR on image** 並 **extracted text from JPG**。

---

## 結論

現在您已了解如何在 C# 中使用 Aspose.OCR **perform OCR on image**，從安裝必要的 **System.Drawing.Common package**、**loading image for OCR**、選擇適當的語言，最後 **extracting text from JPG**。此端對端範例為您建立更進階的文件處理管線奠定堅實基礎，例如批次處理圖片資料夾或將 OCR 整合至 Web API。

### 接下來做什麼？

* 探索在 PDF 中 **recognize text from picture**，方法是先將每頁轉為影像。
* 試驗 `OcrEngine` 的屬性 `Resolution`、`Threshold` 與 `MaxProcessingTime`，以微調噪點掃描的準確度。
* 將 OCR 輸出與自然語言處理函式庫結合，自動為擷取的內容分類。

歡迎將程式碼套用於其他影像格式、加入錯誤處理，或整合至更大型的應用程式。祝開發順利！

## 接下來應該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索替代實作方式。

- [Extract Text from Image in C# – Complete Aspose OCR Guide](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}