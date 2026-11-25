---
category: general
date: 2026-10-18
description: 在 C# 中快速執行 OCR，學習從 JPG 提取文字、將影像轉換為文字，並使用 Aspose.OCR 讀取影像文字。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- convert image to text
- read text from image
- load image for OCR
language: zh-hant
lastmod: 2026-10-18
og_description: 使用 Aspose.OCR 在 C# 中對圖像執行 OCR。本教學示範如何從 JPG 提取文字、將圖像轉換為文字，並在數分鐘內讀取圖像中的文字。
og_image_alt: Console output displaying recognized Cyrillic text after performing
  OCR on an image
og_title: 在 C# 中對圖像執行 OCR – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Perform OCR on an image in C# quickly. Learn to extract text from JPG,
    convert image to text and read text from image using Aspose.OCR.
  headline: How to perform OCR on an image in C# with Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose.OCR
title: 如何在 C# 中使用 Aspose.OCR 進行圖像光學字符辨識
url: /zh-hant/net/text-recognition/how-to-perform-ocr-on-an-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.OCR 對圖像執行 OCR

如果您需要在 .NET 應用程式中**對圖像執行 OCR**，本指南將為您展示一個完整、可直接執行的解決方案。您將看到如何**載入供 OCR 使用的圖像**、辨識西里爾字元，以及**從 JPG 檔案中提取文字**，而無需編寫任何低階的圖像處理程式碼。

在本教學中，您將會：

* 安裝 Aspose.OCR NuGet 套件。  
* 載入圖像檔案（JPG、PNG、BMP 等）。  
* 執行 OCR 引擎以**將圖像轉換為文字**。  
* **從圖像讀取文字**，並在主控台輸出。  

這些步驟適用於任何 .NET 相容的圖像，因此您可以將其套用於 PDF、掃描收據或螢幕截圖等。

## 前置條件

* .NET 6.0 SDK 或更新版本（此程式碼亦可在 .NET Framework 4.7+ 上執行）。  
* Visual Studio 2022 或您偏好的任何 C# 編輯器。  
* 首次執行時需要網際網路連線 – Aspose.OCR 會自動下載西里爾語言模組。  

> **專業提示：**請保持 NuGet 套件為最新版本；較新版本可提升辨識精度並加入語言套件。

## 步驟 1：安裝 Aspose.OCR

在專案資料夾中開啟終端機並執行以下指令：

```bash
dotnet add package Aspose.OCR
```

此套件包含用於**對圖像執行 OCR**的 `OcrEngine` 類別。指令執行完畢後，套件參考會出現在您的 *.csproj* 檔案中。

## 步驟 2：建立主控台程式骨架

如果尚未有專案，請建立一個新的主控台專案：

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

將產生的 *Program.cs* 替換為下節所示的程式碼。此骨架包含必要的 `using` 指令與驅動 OCR 流程的 `Main` 方法。

## 步驟 3：載入供 OCR 使用的圖像

第一行功能程式碼**載入您想要分析的圖像**。Aspose.OCR 接受任何串流，因此您可以從磁碟、網路 URL 或嵌入式資源載入檔案。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Step 3: Load the image containing Cyrillic text
        // Replace the path with the location of your JPG file.
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);
```

*為什麼這很重要*：使用 `ImageStream.FromFile` 可抽象化格式處理，確保 OCR 引擎收到一致的位圖，無論原始檔案類型為何。由於 `using` 陳述式，串流也會自動釋放。

## 步驟 4：初始化 OCR 引擎並設定語言（可選）

預設情況下，Aspose.OCR 會自動偵測語言。對於西里爾文字，您可以明確要求 `Language.Cyrillic` 模組，這會加速首次下載。

```csharp
        // Step 4: Initialize the OCR engine
        var engine = new OcrEngine();

        // Optional: force Cyrillic language to avoid auto‑detection overhead
        engine.Language = Language.Cyrillic;
```

如果省略語言設定，引擎會在您首次呼叫 `Recognize` 時下載所需模組。下載透過 HTTPS 進行，且會本機快取，以供後續執行使用。

## 步驟 5：執行 OCR 並將圖像轉換為文字

現在您真正**對圖像執行 OCR**，並取得純文字字串。`Recognize` 方法負責所有繁重工作：前處理、版面分析與字元分類。

```csharp
        // Step 5: Perform OCR – convert image to text
        engine.Image = image;
        string recognizedText = engine.Recognize();
```

回傳的 `recognizedText` 包含與原始版面相符的換行符號，方便後續處理或儲存至資料庫。

## 步驟 6：顯示結果 – 從圖像讀取文字

最後，透過將結果寫入主控台**從圖像讀取文字**。此步驟可驗證 OCR 是否成功，並顯示實際提取的內容。

```csharp
        // Step 6: Display the recognized text – read text from image
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

執行程式 (`dotnet run`) 後，您應該會看到類似以下的輸出：

```
=== OCR Result ===
Пример текста на кириллице
```

> **注意：**實際輸出取決於來源 JPG 的品質。清晰且高解析度的圖像可產生最佳結果。

## 完整、可執行的原始程式碼

以下為完整程式，您可以直接複製貼上至 *Program.cs*，並在不做其他修改（除圖像路徑外）的情況下執行。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Load the image containing Cyrillic text
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);

        // Initialize the OCR engine
        var engine = new OcrEngine
        {
            // Force Cyrillic language; optional but speeds up first run
            Language = Language.Cyrillic,
            Image = image
        };

        // Recognize the text – this converts the image to text
        string recognizedText = engine.Recognize();

        // Display the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

執行程式會將提取的字元印至主控台，證明您已成功**從 JPG 提取文字**且**將圖像轉換為文字**。

## 處理常見變化

| Scenario | Adjustment |
|----------|------------|
| **不同語言** | 設定 `engine.Language = Language.English;` 或其他支援的列舉值。 |
| **多頁 PDF** | 將每一頁轉換為圖像（例如使用 `Aspose.PDF`），然後對每張圖像呼叫 OCR 迴圈。 |
| **大量批次** | 將 OCR 呼叫包裹在 `Parallel.ForEach` 迴圈中；重複使用單一 `OcrEngine` 實例以減少記憶體開銷。 |
| **低解析度圖像** | 在辨識前使用 `engine.Image = ImageProcessing.Filters.GaussianBlur(image, 1.5);` 進行前處理，以降低噪點。 |

這些變化讓您能夠**從 JPG 檔案提取文字**，無論其語言、大小或品質為何。

## 效能技巧

* **快取語言模組** – 首次下載可能需要數秒；之後的執行則即時完成。 |
* **重複使用 `OcrEngine`** 實例以處理多張圖像，避免重複初始化的成本。 |
* **限制圖像大小** – 極大的照片會增加記憶體使用量。請在送入引擎前將寬度調整至最高 2000 px。

## 結論

現在您已了解如何在 C# 中使用 Aspose.OCR **對圖像執行 OCR**。只要載入圖像、設定引擎，並呼叫 `Recognize`，即可僅用幾行程式碼**從 JPG 提取文字**、**將圖像轉換為文字**，以及**從圖像讀取文字**。  

從此您可以探索：

* 將 OCR 結果儲存至資料庫，以建立可搜尋的檔案庫。  
* 將工作流程整合至接受上傳圖像的 Web API。  
* 使用其他語言模組（阿拉伯語、印地語等），擴大應用程式的覆蓋範圍。  

歡迎嘗試不同的圖像格式、語言與批次處理策略。核心模式—**載入供 OCR 的圖像 → 辨識 → 處理純文字輸出**—保持不變，為任何文字提取專案提供堅實基礎。

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [使用 Aspose.OCR 以語言選擇方式提取圖像文字 C#](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [將圖像轉換為文字 – 從 URL 執行 OCR](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [如何使用 Aspose.OCR for .NET 從圖像提取文字](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}