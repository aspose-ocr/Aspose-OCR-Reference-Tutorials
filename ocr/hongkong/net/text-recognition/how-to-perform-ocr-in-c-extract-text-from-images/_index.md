---
category: general
date: 2026-10-08
description: 學習如何在 C# 中使用 Aspose.OCR 執行 OCR，從圖像檔案中提取文字。本指南將示範如何將圖像轉換為文字，並辨識 JPEG 中的文字。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- recognize text from jpeg
- c# ocr example
language: zh-hant
lastmod: 2026-10-08
og_description: 如何在 C# 中使用 Aspose.OCR 執行 OCR。請跟隨此一步一步的指南，從圖像檔案中提取文字、將圖像轉換為文字，並識別 JPEG
  中的文字。
og_image_alt: Console output displaying Cyrillic text recognized from a JPEG image
  by a C# OCR program
og_title: 如何在 C# 中執行 OCR – 從圖片提取文字
schemas:
- author: Aspose
  dateModified: '2026-10-08'
  description: Learn how to perform OCR in C# using Aspose.OCR to extract text from
    image files. This guide shows you how to convert image to text and recognize text
    from JPEG.
  headline: How to perform OCR in C# – extract text from images
  type: TechArticle
- description: Learn how to perform OCR in C# using Aspose.OCR to extract text from
    image files. This guide shows you how to convert image to text and recognize text
    from JPEG.
  name: How to perform OCR in C# – extract text from images
  steps:
  - name: Why each line matters
    text: '* **`OcrEngine ocrEngine = new OcrEngine();`** – Instantiates the engine
      that orchestrates the whole OCR pipeline. * **`ocrEngine.Language = Language.Cyrillic;`**
      – Selects the language model. Choosing the correct language dramatically improves
      accuracy when you **extract text from image** files tha'
  - name: 4.1 Recognizing English or multilingual text
    text: 'Replace the language assignment with the appropriate enum:'
  - name: 4.2 Processing images from a stream instead of a file
    text: 'If your image arrives via an HTTP response or a database blob, use a `MemoryStream`:'
  - name: 4.3 Handling large or low‑resolution images
    text: 'Large images increase memory consumption. You can downscale before OCR:'
  - name: 4.4 Error handling
    text: 'Wrap the recognition call in a try‑catch block to catch network or file‑access
      errors:'
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
- Image Processing
title: 如何在 C# 中執行 OCR – 從圖像提取文字
url: /zh-hant/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中執行 OCR – 從圖像中擷取文字

如果您需要在 .NET 應用程式中 **how to perform OCR**，本教學提供完整、可直接執行的解決方案。使用 Aspose.OCR，您可以 **extract text from image** 檔案、**convert image to text**，以及 **recognize text from JPEG**，只需幾行程式碼即可完成。

您將看到完整的工作流程——從安裝函式庫到列印辨識後的字串——讓您可以將範例複製到自己的專案中，立即開始處理圖像。

## 您將學到的內容

* 如何為 OCR 任務設定 C# 專案。  
* 如何載入 JPEG（或任何支援的圖像）並執行辨識。  
* 如何取得辨識結果文字並在應用程式中使用。  

唯一的先決條件是最近的 .NET SDK（≥ .NET 6）以及首次下載語言模型時的網際網路連線。

## 步驟 1：設定專案並安裝 Aspose.OCR

1. 建立新的主控台專案：

   ```bash
   dotnet new console -n OcrDemo
   cd OcrDemo
   ```

2. 新增 Aspose.OCR NuGet 套件：

   ```bash
   dotnet add package Aspose.OCR
   ```

   此套件包含 OCR 引擎、語言模型以及執行 **convert image to text** 所需的圖像處理工具。

> **專業提示：** 若您打算對多張圖像執行 OCR，建議將套件加入共用函式庫，以便重複使用同一個引擎實例。

## 步驟 2：撰寫 C# OCR 範例

建立或取代 `Program.cs`，內容如下。此程式碼示範一個 **c# ocr example**，可支援 Aspose.OCR 所支援的任何圖像格式（JPEG、PNG、BMP 等）。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // ---------------------------------------------------------
        // Step 2.1: Create an OCR engine instance
        // ---------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------------------------------------------------------
        // Step 2.2: Choose the language model.
        // The example uses Cyrillic; replace with Language.English,
        // Language.French, etc., to match your source image.
        // ---------------------------------------------------------
        ocrEngine.Language = Language.Cyrillic; // <-- change as needed

        // ---------------------------------------------------------
        // Step 2.3: Load the image you want to process.
        // ImageStream.FromFile automatically reads JPEG, PNG, BMP…
        // ---------------------------------------------------------
        ocrEngine.Image = ImageStream.FromFile("sample_cyrillic.jpg");

        // ---------------------------------------------------------
        // Step 2.4: Run the recognition process.
        // This call downloads the required language model the first
        // time it is used, then performs the OCR.
        // ---------------------------------------------------------
        ocrEngine.Recognize();

        // ---------------------------------------------------------
        // Step 2.5: Retrieve the recognized text.
        // The Text property holds the result of the OCR engine.
        // ---------------------------------------------------------
        string recognizedText = ocrEngine.Text;

        // ---------------------------------------------------------
        // Step 2.6: Display the output.
        // This is where you can further process the string,
        // e.g., save to a database, feed to a search index, etc.
        // ---------------------------------------------------------
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

### 為何每一行都很重要

* **`OcrEngine ocrEngine = new OcrEngine();`** – 建立負責協調整個 OCR 流程的引擎實例。  
* **`ocrEngine.Language = Language.Cyrillic;`** – 設定語言模型。選擇正確的語言能在 **extract text from image** 包含非拉丁字元的檔案時大幅提升準確度。  
* **`ocrEngine.Image = ImageStream.FromFile(...);`** – 載入來源 JPEG（或其他支援的圖像）。此步驟對於 **recognize text from jpeg** 至關重要。  
* **`ocrEngine.Recognize();`** – 執行核心 OCR 演算法。此方法會阻塞，直至引擎完成處理。  
* **`ocrEngine.Text;`** – 回傳純文字結果，您現在可以將其 **convert image to text** 用於後續邏輯。

## 步驟 3：執行程式並驗證輸出

編譯並執行：

```bash
dotnet run
```

如果圖像 `sample_cyrillic.jpg` 包含西里爾文短語 “Привет мир”，控制台將會顯示：

```
=== Recognized Text ===
Привет мир
```

此輸出證明您已成功學會使用 C# **how to perform OCR** 與 **extract text from image**。

## 步驟 4：常見變化與邊緣情況

### 4.1 辨識英文或多語言文字

將語言設定替換為相應的列舉值：

```csharp
ocrEngine.Language = Language.English;           // English only
ocrEngine.Language = Language.Multilingual;      // Detects many languages automatically
```

### 4.2 從串流而非檔案處理圖像

若圖像透過 HTTP 回應或資料庫 BLOB 取得，請使用 `MemoryStream`：

```csharp
using (var ms = new MemoryStream(imageBytes))
{
    ocrEngine.Image = ImageStream.FromStream(ms);
    ocrEngine.Recognize();
}
```

### 4.3 處理大型或低解析度圖像

大型圖像會增加記憶體使用量。您可以在 OCR 前先縮小圖像：

```csharp
ocrEngine.Config.ImagePreprocessOptions.ScaleFactor = 0.5; // Reduce size by 50%
```

### 4.4 錯誤處理

將辨識呼叫包在 try‑catch 區塊中，以捕捉網路或檔案存取錯誤：

```csharp
try
{
    ocrEngine.Recognize();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"OCR failed: {ex.Message}");
}
```

## 步驟 5：後續步驟 – 擴充您的 OCR 工作流程

* **批次處理：** 迭代目錄中的檔案，對每個 JPEG 執行 **convert image to text**。  
* **後處理：** 使用正規表達式清理辨識出的字串，當您需要 **extract text from image** 表單或發票時非常有用。  
* **整合 Azure Cognitive Services：** 將 Aspose.OCR 結果與雲端 OCR 進行比較，以提升複雜版面之準確度。  
* **儲存結果：** 將擷取的文字插入 SQL 資料庫或 ElasticSearch 索引，以供文件搜尋。

---

## 結論

您現在已了解如何使用 Aspose.OCR 在 C# 中 **how to perform OCR**，從安裝套件到顯示辨識字串。這個完整的 **c# ocr example** 讓您能在幾行程式碼內 **extract text from image**、**convert image to text**，以及 **recognize text from JPEG**。請嘗試不同的語言模型、圖像來源與後處理技術，以符合您的特定使用情境。

---

## 接下來您應該學習什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在此處示範的技術之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [How to Use OCR in C# – Extract Text from Image Files](/ocr/english/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-files/)
- [Convert Image to Text in C# with Aspose OCR – Step‑by‑Step Guide](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [How to Perform OCR in C# – Extract Text and Write JSON](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}