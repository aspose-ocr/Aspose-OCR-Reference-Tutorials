---
category: general
date: 2026-03-26
description: 如何在 C# 中使用 Aspose OCR 進行阿拉伯文 OCR – 學習快速提取阿拉伯文字、從圖像識別文字，並將圖像轉換為文字。
draft: false
keywords:
- how to ocr arabic
- extract arabic text
- recognize text from image
- convert image to text
- load image for ocr
language: zh-hant
og_description: 如何在 C# 中進行阿拉伯文 OCR？跟隨本指南，使用 Aspose OCR 提取阿拉伯文文字、從圖像識別文字，並將圖像轉換為文字。
og_title: 如何在 C# 中進行阿拉伯文 OCR – 完整程式設計指南
tags:
- OCR
- C#
- Aspose
- Arabic
title: 如何在 C# 中對阿拉伯語進行 OCR – 步驟指南
url: /zh-hant/net/text-recognition/how-to-ocr-arabic-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中 OCR 阿拉伯文 – 完整程式指南

有沒有想過在 .NET 應用程式中 **如何 OCR 阿拉伯文**？在本教學中，我們將逐步說明如何使用 Aspose OCR 從影像 **擷取阿拉伯文字**。無論你是要打造多語言掃描器，或只是需要將阿拉伯標示抓取到資料庫，只要有正確的元件，整個流程相當簡單。

事實上，大多數 OCR 函式庫預設為英文，因此必須告訴引擎你預期的語言。我們將說明 **如何載入影像以進行 OCR**、設定語言，最後 **從影像辨識文字**，讓你只需幾行 C# 程式碼即可 **將影像轉換為文字**。完成後，你將擁有一個可執行的主控台應用程式，會印出偵測到的語言以及擷取出的阿拉伯字串。

## 需求條件

- **.NET 6+**（或任何近期的 .NET 執行環境；API 的使用方式相同）
- **Aspose.OCR for .NET** NuGet 套件 – 使用 `dotnet add package Aspose.OCR` 安裝
- 包含阿拉伯字元的影像檔，例如 `arabic_sign.jpg`
- 程式碼編輯器 — Visual Studio、VS Code 或 Rider 都可

不需要額外的設定檔、外部服務，也沒有隱藏的魔法。只要一個乾淨、獨立的主控台應用程式即可。

## 步驟 1：初始化 OCR 引擎 – 如何 OCR 阿拉伯文

首先，建立 `OcrEngine` 的實例。此物件是函式庫的核心，負責保存所有影響辨識的設定。

```csharp
using System;
using Aspose.OCR;

class LanguageExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **為什麼這很重要：** 建立引擎會分配原生 OCR 資源。如果省略此步驟，程式庫將無法得知預期的語言，結果會出現亂碼。

## 步驟 2：告訴引擎要辨識的語言

現在設定 `Language` 屬性。對於阿拉伯文，我們使用 `OcrLanguage.Arabic`。只要更改這一行，即可切換至其他文字系統（如西里爾文、韓文等）。

```csharp
        // Step 2: Specify the language to recognize (Arabic in this case)
        ocrEngine.Language = OcrLanguage.Arabic;   // alternatives: OcrLanguage.CyrillicExtended, OcrLanguage.Korean
```

> **小技巧：** 若影像包含多種語言，可啟用 `OcrLanguage.Multilingual` 讓引擎自行判斷，但效能會稍微下降。堅持使用單一語言（如阿拉伯文）可保持快速且精確。

## 步驟 3：載入影像以進行 OCR

接下來的步驟是將影像提供給引擎。`OcrImage.FromFile` 會從磁碟讀取檔案，並轉換成 Aspose 可處理的內部位圖。

```csharp
        // Step 3: Load the image that contains the text
        OcrImage inputImage = OcrImage.FromFile("YOUR_DIRECTORY/arabic_sign.jpg");
```

> **如果找不到檔案該怎麼辦？** 將呼叫包在 `try/catch` 中，並顯示友善的訊息。否則引擎會拋出 `FileNotFoundException`。

```csharp
        // Optional: graceful error handling
        try
        {
            OcrImage inputImage = OcrImage.FromFile("YOUR_DIRECTORY/arabic_sign.jpg");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Could not load image: {ex.Message}");
            return;
        }
```

## 步驟 4：從影像辨識文字並將影像轉換為文字

在引擎設定完成且影像已載入後，我們最後執行辨識。`Recognize` 方法會回傳一個 `OcrResult` 物件，內含擷取的字串以及一些信心指標。

```csharp
        // Step 4: Run the recognition process
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);
```

> **為什麼會有效：** Aspose 的 OCR 引擎會先執行一系列前處理步驟——二值化、去斜、字元分割——再將資料送入針對阿拉伯字形訓練的神經網路。對於高對比度的印刷品，結果通常相當可靠。

## 步驟 5：顯示偵測到的語言與擷取的文字

最後，我們將結果輸出。`Language` 屬性仍保留我們設定的值，證明引擎確實使用了阿拉伯文。`OcrResult` 的 `Text` 屬性則包含 **將影像轉換為文字** 的輸出。

```csharp
        // Step 5: Display the detected language and the extracted text
        Console.WriteLine($"Detected language: {ocrEngine.Language}");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### 預期輸出

```
Detected language: Arabic
مرحبا بكم في عالم البرمجة
```

如果影像模糊或字體裝飾性太強，可能會出現缺字或信心較低的情況。此時可嘗試提升影像解析度，或在傳遞給 `OcrEngine` 前套用前處理濾鏡（例如銳化）。

## 完整範例程式

以下是完整程式碼，你可以直接複製貼上到新的主控台專案中。請記得將 `YOUR_DIRECTORY/arabic_sign.jpg` 替換為實際的阿拉伯影像路徑。

```csharp
using System;
using Aspose.OCR;

class LanguageExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Specify the language to recognize (Arabic in this case)
        ocrEngine.Language = OcrLanguage.Arabic;   // alternatives: OcrLanguage.CyrillicExtended, OcrLanguage.Korean

        // Step 3: Load the image that contains the text
        OcrImage inputImage;
        try
        {
            inputImage = OcrImage.FromFile("YOUR_DIRECTORY/arabic_sign.jpg");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Could not load image: {ex.Message}");
            return;
        }

        // Step 4: Run the recognition process
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);

        // Step 5: Display the detected language and the extracted text
        Console.WriteLine($"Detected language: {ocrEngine.Language}");
        Console.WriteLine(ocrResult.Text);
    }
}
```

使用 `dotnet run` 執行專案。若一切設定正確，將會在主控台看到阿拉伯字串。

## 常見問題與例外情況

### 如果需要 **從影像辨識文字**，但檔案格式不是 JPEG 該怎麼辦？

Aspose OCR 支援 PNG、BMP、TIFF，甚至 PDF 頁面。只要在 `FromFile` 中更改副檔名即可。對於 PDF，你也可以傳入頁碼：`OcrImage.FromPdf("file.pdf", pageNumber: 1)`。

### 當影像低對比度時，如何提升辨識準確度？

在建立 `OcrImage` 前，可使用 `System.Drawing` 或 `ImageSharp` 先行前處理影像，例如提升對比、轉為灰階，或套用銳化濾鏡。範例：

```csharp
using SixLabors.ImageSharp;
using SixLabors.ImageSharp.Processing;

// Load, enhance, then feed to Aspose
using var img = Image.Load("low_contrast.jpg");
img.Mutate(x => x.Contrast(1.5f).Sharpen());
img.Save("enhanced.png");
OcrImage enhanced = OcrImage.FromFile("enhanced.png");
```

### 我可以一次 **擷取多張影像的阿拉伯文字** 嗎？

當然可以。將辨識邏輯包在遍歷目錄檔案的 `foreach` 迴圈中。使用完畢後務必釋放每個 `OcrImage`，以釋放原生記憶體：

```csharp
foreach (var file in Directory.GetFiles("images", "*.jpg"))
{
    using var img = OcrImage.FromFile(file);
    var result = ocrEngine.Recognize(img);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text}");
}
```

## 往後的步驟

現在你已掌握使用 Aspose **如何 OCR 阿拉伯文**，接下來可以考慮：

- **Extract Arabic text** 從 PDF（使用 `OcrImage.FromPdf`）。
- 將結果儲存至資料庫，以便建立可搜尋的檔案庫。
- 結合 OCR 與翻譯 API，自動將阿拉伯文翻譯成英文。
- 嘗試其他語言——只要將 `OcrLanguage.Arabic` 換成 `OcrLanguage.Korean` 或 `OcrLanguage.CyrillicExtended` 即可。

上述主題皆基於相同的核心概念：**載入影像以進行 OCR**、**從影像辨識文字**、以及 **將影像轉換為文字**，因此你已具備探索的能力。

---

*祝程式開發順利！若遇到問題，歡迎在下方留言或參考 Aspose.OCR 文件以取得更深入的設定說明。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}