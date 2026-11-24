---
category: general
date: 2026-11-23
description: 下載 OCR 語言並使用 Aspose.OCR 從圖像中提取文字。學習如何在幾個簡單步驟內辨識 PNG 檔案中的西里爾文字。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- download OCR language
- extract text from image
- how to recognize cyrillic
- recognize text from PNG
- recognize Cyrillic text
language: zh-hant
lastmod: 2026-11-23
og_description: 下載 OCR 語言並使用 Aspose.OCR 從圖像中提取文字。按照此步驟教學，從 PNG 檔案中辨識西里爾文字。
og_image_alt: Screenshot of Aspose.OCR engine recognizing Cyrillic text from a PNG
  image
og_title: 下載 OCR 語言並從圖片中提取文字 – Aspose.OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-11-23'
  description: download OCR language and extract text from an image with Aspose.OCR.
    Learn how to recognize Cyrillic text from PNG files in a few easy steps.
  headline: How to download OCR language and extract text from an image
  type: TechArticle
- description: download OCR language and extract text from an image with Aspose.OCR.
    Learn how to recognize Cyrillic text from PNG files in a few easy steps.
  name: How to download OCR language and extract text from an image
  steps:
  - name: '**Multiple languages** – you can load several language modules at once,
      e.g., `engine.LoadLanguage("cyrillic,english");`. The engine will attempt to
      recognize characters from any loaded set.'
    text: '**Multiple languages** – you can load several language modules at once,
      e.g., `engine.LoadLanguage("cyrillic,english");`. The engine will attempt to
      recognize characters from any loaded set.'
  - name: '**Large images** – for high‑resolution files, consider down‑sampling before
      OCR to reduce memory usage.'
    text: '**Large images** – for high‑resolution files, consider down‑sampling before
      OCR to reduce memory usage.'
  - name: '**Batch processing** – wrap the recognition logic in a loop that iterates
      over a directory of PNG files. Remember to re‑assign `engine.Image` for each
      file; the engine can be reused.'
    text: '**Batch processing** – wrap the recognition logic in a loop that iterates
      over a directory of PNG files. Remember to re‑assign `engine.Image` for each
      file; the engine can be reused.'
  type: HowTo
- questions:
  - answer: Download the language module manually from the Aspose download portal,
      place the `.zip` file in the folder you specify with `SetLocalResourcesPath`,
      and the engine will load it without contacting the internet.
    question: What if the download fails because of a firewall?
  - answer: Yes. The OCR engine accepts any format that `System.Drawing.Image` can
      load. Simply change the file extension in `ImageStream.FromFile`.
    question: Can I recognize text from other image formats (e.g., JPEG, BMP)?
  - answer: The underlying API is the same; PNG is just one of many supported formats.
      Mentioning “recognize text from PNG” helps surface the tutorial for users searching
      for that exact phrase.
    question: How does this differ from “recognize text from PNG” vs. “recognize text
      from image”?
  - answer: 'Each `OcrEngine` instance is not thread‑safe. Create a separate instance
      per thread or use a pool pattern if you need high‑throughput processing. ##
      Edge cases and variations 1. **Multiple languages** – you can load several language
      modules at once, e.g., `engine.LoadLanguage("cyrillic,english");`. '
    question: Is the OCR engine thread‑safe?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 如何下載 OCR 語言並從圖片提取文字
url: /zh-hant/net/ocr-configuration/how-to-download-ocr-language-and-extract-text-from-an-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何下載 OCR 語言並從圖像中提取文字

如果您需要 **下載 OCR 語言** 資源並從圖像中提取文字，本指南將向您展示如何使用 Aspose.OCR 完整執行。無論來源是包含西里爾字元的 PNG 或其他支援的格式，您都會得到一個完整且可執行的解決方案。

您將學會如何：

* 按需載入語言模組（即「下載 OCR 語言」步驟）  
* 從 PNG 檔案辨識西里爾文字  
* 可選地將引擎指向本機資料夾以使用預先下載的資源  

完成本教學後，您即可將 OCR 整合至任何 .NET 應用程式，並可靠地 **從圖像中提取文字**。

## 前置條件

在開始之前，請確保您已具備：

* .NET 6.0 SDK 或更新版本已安裝  
* 有效的 Aspose.OCR 授權（免費試用版可用於評估）  
* Visual Studio 2022 或任何相容 C# 的 IDE  
* 一個包含西里爾文字的圖像檔案（`sample_cyrillic.png`）  

程式碼片段使用 C# 10 語言功能，但若有需要，您也可以調整為較早的版本。

## 步驟 1：安裝 Aspose.OCR NuGet 套件

在專案資料夾中開啟終端機並執行以下指令：

```bash
dotnet add package Aspose.OCR
```

## 步驟 2：建立主控台專案並加入 using 指令

建立一個新的主控台應用程式（如果尚未有的話）：

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

開啟 `Program.cs`，在檔案頂部加入所需的命名空間：

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Helpers;   // Provides ImageStream helper methods
```

`Aspose.OCR.Helpers` 命名空間提供方便的方式從磁碟載入圖像。

## 步驟 3：初始化 OCR 引擎並 **下載 OCR 語言** 資源

OCR 引擎預設僅附帶最小資源集。若要辨識西里爾字元，必須載入相應的語言模組。如果本機沒有該模組，Aspose.OCR 會自動下載。

```csharp
// Step 3: Create the OCR engine with default (basic) resources
var engine = new OcrEngine();

// Load the Cyrillic language module; this triggers a download if missing
engine.LoadLanguage("cyrillic");

// Optional: specify a folder for cached language files
// engine.ResourceManager.SetLocalResourcesPath(@"C:\AsposeOCRResources");
```

**此步驟的重要性：**  
*`LoadLanguage("cyrillic")`* 告訴引擎使用哪個字元集。若未呼叫此方法，引擎會回退至預設的拉丁字元集，導致無法辨識西里爾字形。下載僅會執行一次，之後模組會被快取供未來執行使用。

## 步驟 4：載入包含西里爾文字的圖像

Aspose.OCR 可處理 .NET `System.Drawing` 支援的任何圖像格式。此教學使用 PNG 檔案，因為它保留無損品質，可提升辨識準確度。

```csharp
// Step 4: Load the image containing Cyrillic text
engine.Image = ImageStream.FromFile(@"C:\Images\sample_cyrillic.png");
```

如果您偏好使用相對路徑，請將圖像放在專案資料夾內，並使用 `Path.Combine(Directory.GetCurrentDirectory(), "sample_cyrillic.png")`。

## 步驟 5：辨識文字並顯示結果

現在引擎已配置完成且圖像已載入，呼叫 `Recognize()` 並讀取 `Text` 屬性。

```csharp
// Step 5: Perform OCR and output the recognized text
engine.Recognize();

Console.WriteLine("Recognized text:");
Console.WriteLine(engine.Text);
```

**預期輸出**

```
Recognized text:
Привет, мир!
```

實際字串取決於 `sample_cyrillic.png` 的內容，但您應該會在主控台看到西里爾字元。

## 步驟 6：完整、可執行的程式

將上述所有步驟整合起來，以下是完整的原始碼檔案，您可以複製到 `Program.cs` 後執行：

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Helpers;

namespace OcrDemo
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            // Initialize OCR engine
            var engine = new OcrEngine();

            // Load Cyrillic language – downloads if not cached
            engine.LoadLanguage("cyrillic");

            // (Optional) Set a custom folder for language resources
            // engine.ResourceManager.SetLocalResourcesPath(@"C:\AsposeOCRResources");

            // Load the PNG image that contains Cyrillic text
            engine.Image = ImageStream.FromFile(@"C:\Images\sample_cyrillic.png");

            // Run OCR
            engine.Recognize();

            // Output the result
            Console.WriteLine("Recognized text:");
            Console.WriteLine(engine.Text);
        }
    }
}
```

使用以下指令執行程式：

```bash
dotnet run
```

您應該會在主控台看到西里爾語句，證明 **辨識西里爾文字** 操作成功。

## 專業提示：提升噪點 PNG 檔案的辨識準確度

* **預處理圖像** – 在傳遞給 OCR 引擎前，使用 `System.Drawing` 轉為灰階、提升對比度，或套用中值濾波。  
* **設定 `engine.Config` 選項** – 若文字可能旋轉，請啟用 `engine.Config.DetectOrientation = true`。  
* **快取語言模組** – 透過呼叫 `SetLocalResourcesPath` 可避免後續執行時的網路延遲。

## 常見問題解答

**Q: 若因防火牆導致下載失敗，該怎麼辦？**  
A: 手動從 Aspose 下載入口取得語言模組，將 `.zip` 檔案放入您使用 `SetLocalResourcesPath` 指定的資料夾，引擎即可在不連線的情況下載入。

**Q: 我可以辨識其他圖像格式的文字嗎（例如 JPEG、BMP）？**  
A: 可以。OCR 引擎接受任何 `System.Drawing.Image` 能載入的格式，只需在 `ImageStream.FromFile` 中更改檔案副檔名即可。

**Q: 「從 PNG 辨識文字」與「從圖像辨識文字」有何不同？**  
A: 底層 API 相同，PNG 只是眾多支援格式之一。提及「從 PNG 辨識文字」有助於讓搜尋此關鍵字的使用者找到本教學。

**Q: OCR 引擎是否支援執行緒安全？**  
A: 每個 `OcrEngine` 實例並非執行緒安全。若需高吞吐量處理，請為每個執行緒建立獨立實例或使用池化模式。

## 邊緣情況與變體

1. **多語言** – 您可以一次載入多個語言模組，例如 `engine.LoadLanguage("cyrillic,english");`。引擎會嘗試辨識任一已載入集合中的字元。  
2. **大型圖像** – 對於高解析度檔案，建議在 OCR 前先下採樣，以降低記憶體使用量。  
3. **批次處理** – 將辨識邏輯包在迴圈中，遍歷 PNG 檔案目錄。記得為每個檔案重新指派 `engine.Image`；引擎可重複使用。

## 結論

您現在已了解如何 **下載 OCR 語言** 資源、為 Aspose.OCR 設定西里爾語言，並使用簡潔的 C# 主控台應用程式 **從圖像中提取文字**（特別是 PNG 檔案）。此基礎可讓您構建更複雜的解決方案，如文件掃描器、自動資料輸入管線或多語言文字提取服務。

您可以進一步探索以下方向：

* 結合 **從 PNG 辨識文字** 與 **如何辨識西里爾文字**，以處理多語言文件。  
* 將 OCR 流程整合至 ASP.NET Core API，將 OCR 以 Web 服務形式提供。  
* 嘗試其他語言模組（例如 `engine.LoadLanguage("arabic")`），擴大應用程式的覆蓋範圍。

祝開發順利，盡情體驗即時下載 OCR 語言的強大功能！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [如何在 C# 中執行 OCR – 使用 Aspose 辨識西里爾文字](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [如何下載 OCR 資源並在 C# 中辨識圖像文字](/ocr/english/net/text-recognition/how-to-download-ocr-resources-and-recognize-text-from-image/)
- [如何下載 Aspose.OCR 模型並在 C# 中從 PNG 提取文字](/ocr/english/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}