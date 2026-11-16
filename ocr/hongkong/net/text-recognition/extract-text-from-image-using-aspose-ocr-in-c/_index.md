---
category: general
date: 2026-08-09
description: 使用 Aspose OCR 在 C# 中從圖像提取文字。了解如何載入圖像進行 OCR、設定 OCR 語言、處理圖像 OCR，以及高效將圖像轉換為文字。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert image to text
- load image for ocr
- process image ocr
- set ocr language
language: zh-hant
lastmod: 2026-08-09
og_description: 使用 Aspose OCR 於 C# 從圖像提取文字。本教學示範如何載入圖像進行 OCR、設定 OCR 語言、處理圖像 OCR，以及以少量程式碼將圖像轉換為文字。
og_image_alt: Screenshot of C# console output showing extracted text from an image
  using Aspose OCR
og_title: 使用 Aspose OCR 從圖像擷取文字 – C# 指南
schemas:
- author: Aspose
  dateModified: '2026-08-09'
  description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  headline: Extract text from image using Aspose OCR in C#
  type: TechArticle
- description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  name: Extract text from image using Aspose OCR in C#
  steps:
  - name: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
    text: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
  - name: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
    text: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
  - name: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
    text: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
  - name: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
    text: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
  - name: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
    text: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
  - name: Instantiates `OcrEngine`.
    text: Instantiates `OcrEngine`.
  - name: '**Sets OCR language** to Cyrillic (or any language you choose).'
    text: '**Sets OCR language** to Cyrillic (or any language you choose).'
  - name: '**Loads image for OCR** from disk.'
    text: '**Loads image for OCR** from disk.'
  - name: '**Processes image OCR** to obtain the textual result.'
    text: '**Processes image OCR** to obtain the textual result.'
  - name: '**Converts image to text** and prints it.'
    text: '**Converts image to text** and prints it.'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 使用 Aspose OCR 在 C# 中從圖片提取文字
url: /zh-hant/net/text-recognition/extract-text-from-image-using-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像中提取文字（使用 Aspose OCR 於 C#）

如果您需要在 .NET 應用程式中 **從圖像中提取文字**，本指南將帶您完成一個完整、可直接執行的解決方案。您將會看到如何 **載入圖像以進行 OCR**、選擇適當的語言模組、執行 OCR 引擎，最後只需幾行 C# 代碼即可 **將圖像轉換為文字**。

本教學涵蓋使用 Aspose.OCR 獲得可靠結果所需的全部內容，包括不支援的圖像格式及語言特有的細節等常見陷阱。完成後，您將擁有一個自包含的程式，能將辨識出的文字印出到主控台。

## 您將達成的目標

* 將圖像檔載入 Aspose OCR 引擎。  
* **設定 OCR 語言**（範例使用西里爾文，但任何支援的語言皆可）。  
* **處理圖像 OCR** 並取得文字表示。  
* **將圖像轉換為文字** 並顯示，可供後續處理或儲存。  

**先決條件**

* .NET 6.0 或更新版本（此程式碼亦可於 .NET Framework 4.6+ 執行）。  
* Visual Studio 2022（或任何支援 C# 的 IDE）。  
* Aspose.OCR NuGet 套件（`Install-Package Aspose.OCR`）。  

---

## 從圖像提取文字 – 完整程式碼說明

以下是完整且可執行的程式。將其複製到新的主控台專案中，並將 `YOUR_DIRECTORY/sample_cyrillic.jpg` 替換為您自己的圖像路徑。

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create an OCR engine instance.
            // The using block ensures the engine is disposed correctly.
            using (var engine = new OcrEngine())
            {
                // Step 2: Set OCR language.
                // Change OcrLanguage.Cyrillic to any other supported language,
                // e.g., OcrLanguage.English, OcrLanguage.Chinese, OcrLanguage.Hindi.
                engine.Language = OcrLanguage.Cyrillic;

                // Step 3: Load image for OCR.
                // ImageStream.FromFile reads the image from disk.
                // Supported formats: JPEG, PNG, BMP, TIFF, GIF.
                engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/sample_cyrillic.jpg");

                // Step 4: Process image OCR.
                // The Process method runs the recognition engine and returns an OcrResult.
                var result = engine.Process();

                // Step 5: Convert image to text.
                // The recognized text is available via result.Text.
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

### 為何每一步都很重要

1. **建立 OCR 引擎實例** – `OcrEngine` 封裝了所有 OCR 功能。及時釋放它可釋放原生資源，對長時間執行的服務至關重要。  
2. **設定 OCR 語言** – 選擇正確的語言模組可大幅提升準確度。Aspose 提供超過 30 種語言包；預設為英文。此範例使用西里爾文以示範非拉丁文字。  
3. **載入圖像以進行 OCR** – 引擎使用 `ImageStream`。提供高解析度圖像（≥300 dpi）可減少誤辨，尤其是複雜文字。  
4. **處理圖像 OCR** – 這是執行繁重工作的階段。此方法回傳包含提取文字、信心分數以及可選版面資料的 `OcrResult`。  
5. **將圖像轉換為文字** – `result.Text` 為純文字 `string`。您可以將其寫入檔案、送入搜尋索引，或傳遞給下游的 NLP 流程。  

---

## 載入圖像以進行 OCR

`ImageStream.FromFile` 方法支援常見的點陣圖格式。如果您以位元組陣列（例如來自 Web API）取得圖像，請改用 `ImageStream.FromBytes(byte[])`：

```csharp
byte[] imageBytes = File.ReadAllBytes("path/to/image.png");
engine.Image = ImageStream.FromBytes(imageBytes);
```

**專業提示：** 在將圖像傳遞給引擎之前，務必確認圖像未損壞。快速的 `try { Image.FromFile(...); } catch { ... }` 防護可避免執行時例外。

---

## 設定 OCR 語言

Aspose.OCR 附帶可於執行時啟用的語言包。列出所有可用語言：

```csharp
foreach (var lang in Enum.GetValues(typeof(OcrLanguage)))
{
    Console.WriteLine(lang);
}
```

如果需要在同一文件中辨識多種語言，可使用位元 OR 運算子將它們結合：

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Russian;
```

**邊緣情況：** 將從右至左（RTL）語言（例如阿拉伯文）與從左至右腳本混合使用時，可能需要額外的版面處理。Aspose 會自動偵測方向，但您可透過 `engine.PageSegmentationMode` 進行微調。

---

## 處理圖像 OCR

`Process` 呼叫為同步執行，會阻塞直至引擎完成。對於大量批次或 UI 應用程式，可考慮使用非同步重載：

```csharp
var task = engine.ProcessAsync();
OcrResult result = await task;
```

**常見陷阱：** 在呼叫 `Process` 前忘記設定 `engine.Image` 會拋出 `InvalidOperationException`。請務必先指派圖像。

---

## 將圖像轉換為文字

提取的字串可像其他 .NET `string` 一樣操作。例如，將輸出寫入檔案：

```csharp
File.WriteAllText("output.txt", result.Text);
```

如果需要保留圖像中出現的換行，請直接使用 `result.Text`。若要進行後處理（例如移除多餘空白），可套用標準字串方法：

```csharp
string cleaned = result.Text
    .Replace("\r\n", "\n")
    .Trim();
```

---

## 完整範例回顧

將所有步驟結合，程式會：

1. 建立 `OcrEngine` 實例。  
2. **設定 OCR 語言** 為西里爾文（或您選擇的任何語言）。  
3. **載入圖像以進行 OCR** 從磁碟。  
4. **處理圖像 OCR** 以取得文字結果。  
5. **將圖像轉換為文字** 並印出。

執行帶有清晰西里爾文字的範例會產生類似以下的輸出：

```
=== Recognized Text ===
Пример текста на кириллице
```

如果圖像包含英文文字，只需將 `engine.Language = OcrLanguage.English;` 改為英文，相同程式碼即可正確 **從圖像中提取文字**。

---

## 結論

您現在已了解如何使用 Aspose OCR 於 C# **從圖像中提取文字**。本教學說明了載入圖像、選擇適當語言、執行 OCR 流程，以及 **將圖像轉換為文字** 以供後續使用。

接下來您可以：

* 嘗試其他語言（`載入圖像以進行 OCR` → `設定 OCR 語言` → `處理圖像 OCR`）。  
* 將 OCR 步驟整合到更大的管線中（例如文件匯入、可搜尋的 PDF）。  
* 透過批次處理圖像或使用非同步 API 來優化效能。

歡迎探索 Aspose.OCR 文件，了解自訂字典、版面分割模式與 OCR 準確度調校等進階功能。祝開發順利！

## 接下來您應該學習什麼？

以下教學涵蓋與本指南技術緊密相關的主題，並提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，並在專案中探索其他實作方式。

- [使用 Aspose.OCR 於 C# 進行圖像文字提取與語言選擇](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [圖像文字提取 – 使用 Aspose.OCR 於 .NET 的 OCR 優化](/ocr/english/net/ocr-optimization/)
- [如何使用 Aspose OCR 從串流執行圖像文字提取](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}