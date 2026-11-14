---
category: general
date: 2026-11-14
description: 學習如何使用 Aspose OCR 在 C# 中將圖像辨識為文字。此一步一步的指南亦涵蓋如何從 JPG 提取文字並高效地將圖像轉換為文字。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize image to text
- extract text from jpg
- perform OCR on image
- convert image to text
- recognize text from image
language: zh-hant
lastmod: 2026-11-14
og_description: 使用 Aspose OCR 在 C# 中將圖像識別為文字。請跟隨本完整教學，從 jpg 提取文字、對圖像執行 OCR，並將圖像轉換為文字。
og_image_alt: Screenshot of C# code that recognize image to text using Aspose OCR
og_title: 使用 Aspose OCR 將圖片辨識為文字 – C# 指南
schemas:
- author: Aspose
  dateModified: '2026-11-14'
  description: Learn how to recognize image to text using Aspose OCR in C#. This step‑by‑step
    guide also covers how to extract text from jpg and convert image to text efficiently.
  headline: How to recognize image to text with Aspose OCR in C#
  type: TechArticle
- description: Learn how to recognize image to text using Aspose OCR in C#. This step‑by‑step
    guide also covers how to extract text from jpg and convert image to text efficiently.
  name: How to recognize image to text with Aspose OCR in C#
  steps:
  - name: Large images
    text: Large files increase memory usage and processing time. Resize the image
      to a maximum of 2000 px on the longest side before calling `RecognizeImage`.
  - name: Missing language model
    text: If the required language pack cannot be downloaded (e.g., offline environment),
      the engine throws `IOException`. Wrap the call in a try‑catch block and provide
      a fallback language.
  - name: Asynchronous processing
    text: For UI applications, avoid blocking the UI thread. Wrap the recognition
      call in `Task.Run`.
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 如何在 C# 中使用 Aspose OCR 將圖像辨識為文字
url: /zh-hant/net/text-recognition/how-to-recognize-image-to-text-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose OCR 在 C# 中將圖像辨識為文字

如果您需要在 .NET 應用程式中將圖像辨識為文字，本教學會展示完整的步驟。您將會看到如何從 jpg 檔案擷取文字、對圖像資料執行 OCR，以及以最少程式碼將圖像轉換為文字。

本教學涵蓋從安裝 Aspose.OCR NuGet 套件到安全處理 OCR 結果的所有內容。無需任何外部服務，程式碼可在 .NET 6 或更高版本上執行。

## 安裝 Aspose OCR 套件

在撰寫任何程式碼之前，先將 Aspose.OCR 函式庫加入您的專案。此套件包含所有語言模型，並會在執行期間自動下載所需檔案。

```bash
dotnet add package Aspose.OCR
```

此指令會將最新的穩定版 **Aspose.OCR** 加入您的 `csproj`。此步驟確保您可以直接呼叫 `OcrEngine`，無需手動管理 DLL。

## 建立並設定 OCR 引擎

建立 OCR 引擎是您必須執行的第一個程式化動作。引擎負責圖像載入、語言選擇與辨識。

```csharp
using Aspose.OCR;

// Step 1: Instantiate the OCR engine (required modules are downloaded automatically)
OcrEngine ocrEngine = new OcrEngine();
```

`OcrEngine` 是執行繁重工作的核心類別。實例化它會觸發輕量化的初始化；函式庫僅在您選擇語言時才下載相應的語言包。

## 選擇語言模型（從 jpg 擷取文字）

正確的語言模型會影響辨識準確度。若要辨識西里爾文字，請指定 `OcrLanguage.Cyrillic`。第一次設定尚未快取於本機的語言時，Aspose 會在背景下載該模型。

```csharp
// Step 2: Choose the language model – triggers download if needed
ocrEngine.Language = OcrLanguage.Cyrillic;
```

如果您處理的是拉丁文字，請將 `Cyrillic` 改為 `English` 或其他列舉值。相同的程式路徑 **perform OCR on image** 皆適用於任何語言。

## 從 JPG 檔案辨識文字（將圖像轉換為文字）

現在您可以將圖像檔案傳入引擎。`RecognizeImage` 方法接受檔案路徑、串流或 `Bitmap`。此處使用 JPEG，因為它是掃描文件的常見格式。

```csharp
// Step 3: Recognize text from the image file
OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/cyrillic-sample.jpg");
```

此方法會回傳一個 `OcrResult` 物件，內含原始字串、信心分數以及可選的版面資訊。此呼叫 **recognize text from image** 只需一行程式碼。

## 顯示 OCR 結果（從 jpg 擷取文字）

辨識完成後，將偵測到的文字輸出至主控台，或傳遞給其他元件。

```csharp
// Step 4: Display the recognized text
Console.WriteLine(ocrResult.Text);
```

典型的主控台輸出如下：

```
Пример текста на кириллице
```

如果圖像中沒有可讀取的字元，`ocrResult.Text` 會是空字串。請務必在後續處理前先檢查此情況。

## 處理常見邊緣案例

### 大尺寸圖像

大型檔案會增加記憶體使用量與處理時間。呼叫 `RecognizeImage` 前，請先將圖像的最長邊縮放至不超過 2000 px。

```csharp
using System.Drawing;

// Load, resize, then recognize
using (Bitmap original = new Bitmap("YOUR_DIRECTORY/large-sample.jpg"))
{
    int maxDim = 2000;
    int width = original.Width;
    int height = original.Height;

    if (width > maxDim || height > maxDim)
    {
        float scale = Math.Min((float)maxDim / width, (float)maxDim / height);
        int newWidth = (int)(width * scale);
        int newHeight = (int)(height * scale);
        using (Bitmap resized = new Bitmap(original, newWidth, newHeight))
        {
            OcrResult result = ocrEngine.RecognizeImage(resized);
            Console.WriteLine(result.Text);
        }
    }
    else
    {
        OcrResult result = ocrEngine.RecognizeImage(original);
        Console.WriteLine(result.Text);
    }
}
```

### 缺少語言模型

若無法下載所需的語言包（例如離線環境），引擎會拋出 `IOException`。請將呼叫包在 try‑catch 區塊中，並提供備援語言。

```csharp
try
{
    ocrEngine.Language = OcrLanguage.Cyrillic;
    OcrResult result = ocrEngine.RecognizeImage("sample.jpg");
    Console.WriteLine(result.Text);
}
catch (IOException ex)
{
    Console.WriteLine($"Language model download failed: {ex.Message}");
    // Fallback to English
    ocrEngine.Language = OcrLanguage.English;
    OcrResult fallback = ocrEngine.RecognizeImage("sample.jpg");
    Console.WriteLine(fallback.Text);
}
```

### 非同步處理

對於 UI 應用程式，請避免阻塞 UI 執行緒。將辨識呼叫包在 `Task.Run` 中執行。

```csharp
await Task.Run(() =>
{
    OcrResult asyncResult = ocrEngine.RecognizeImage("sample.jpg");
    Console.WriteLine(asyncResult.Text);
});
```

## 提升 OCR 穩定性的實用技巧

- **前置處理圖像**：在光線不足的情況下，先執行灰階轉換與對比度增強，可提升 **perform OCR on image** 的準確度。  
- **選擇正確語言**：在辨識前務必設定 `ocrEngine.Language`。預設為英文，對西里爾或亞洲文字的辨識準確度會較低。  
- **驗證輸出**：使用正規表達式確認辨識文字符合預期模式（例如日期、身分證號）後再儲存。  
- **快取語言包**：首次下載可能需要數秒。若需即時啟動，請將必要的語言包隨應用程式一起部署。

## 完整範例

以下是一個獨立的程式，示範從套件安裝到顯示 OCR 結果的完整工作流程。

```csharp
// -----------------------------------------------------------
// Recognize image to text with Aspose OCR – complete example
// -----------------------------------------------------------
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1. Create the OCR engine (modules are downloaded automatically)
        OcrEngine ocrEngine = new OcrEngine();

        // 2. Select the language model – triggers download if missing
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // 3. Recognize text from a JPG file (convert image to text)
        OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/cyrillic-sample.jpg");

        // 4. Output the recognized string (extract text from jpg)
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**預期的主控台輸出**

```
Recognized text:
Пример текста на кириллице
```

將程式執行於不同圖像（例如英文發票）時，只需更改 `Language` 列舉與檔案路徑。相同程式碼 **recognize text from image** 即可無需修改。

## 結論

現在您已掌握如何在 C# 中使用 Aspose OCR 將圖像辨識為文字。教學說明了安裝函式庫、建立與設定 OCR 引擎、將圖像轉換為文字，以及處理常見的邊緣案例。憑藉此基礎，您可以 **extract text from jpg**、**perform OCR on image** 任意大小的資料，並將結果整合至更大的 .NET 工作流程中。

接下來，您可以探索以下進階功能：

- **多頁 PDF OCR**（使用 `PdfInput` 取代 JPG）  
- **自訂字元白名單**，提升數字代碼的辨識精度  
- **將 OCR 結果儲存為可搜尋的 PDF**，使用 `OcrEngine.Save`

嘗試不同的語言模型與圖像前置處理技術，以在您的特定領域中取得最佳的辨識率。祝開發順利！

## 接下來該學什麼？

以下教學與本指南的技術緊密相關，能進一步深化您的技巧。每個資源都提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，並在自己的專案中探索替代實作方式。

- [recognize text from image in C# – step‑by‑step Aspose OCR guide](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-step-by-step-aspose-ocr-guide/)
- [recognize text from image with Aspose OCR – Complete C# Async Guide](/ocr/english/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-async-g/)
- [recognize text from image in C# – Complete Aspose OCR Tutorial](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-aspose-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}