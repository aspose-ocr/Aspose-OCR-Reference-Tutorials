---
category: general
date: 2026-06-28
description: 使用 C# 從影像建立可搜尋的 PDF。學習如何將影像轉換成 PDF、從影像擷取文字，並在同一流程中辨識多種語言。
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- how to recognize multiple languages
- how to generate searchable pdf
language: zh-hant
og_description: 使用 C# 建立可搜尋的 PDF。本指南說明如何將影像轉換為 PDF、從影像提取文字，以及以程式方式辨識多種語言。
og_title: 建立可搜尋的 PDF（C#）–一步步教學
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Create searchable PDF from images using C#. Learn how to convert image
    to PDF, extract text from image, and recognize multiple languages in one flow.
  headline: Create Searchable PDF in C# – Complete Guide with Aspose OCR
  type: TechArticle
- description: Create searchable PDF from images using C#. Learn how to convert image
    to PDF, extract text from image, and recognize multiple languages in one flow.
  name: Create Searchable PDF in C# – Complete Guide with Aspose OCR
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 SDK or later (the code compiles with .NET Core as well). - An
      Aspose.OCR license (you can start with a free trial; the API works without a
      license but adds a watermark). - A sample image that contains English, Arabic,
      and Korean text (or any languages you need). - Visual Studio 2022 or yo'
  - name: What If a Language Isn't Recognized?
    text: If you add a language that the engine doesn’t have a model for, it will
      simply ignore it and fall back to the others. To avoid surprises, double‑check
      the supported language list in the Aspose documentation.
  - name: Expected Output
    text: '``` Plain text: Hello World! مرحبا بالعالم! 안녕하세요 세계! Searchable PDF saved.
      ```'
  type: HowTo
tags:
- OCR
- PDF
- C#
- Aspose
title: 在 C# 中建立可搜尋的 PDF – 使用 Aspose OCR 的完整指南
url: /zh-hant/net/text-recognition/create-searchable-pdf-in-c-complete-guide-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中建立可搜尋的 PDF – 使用 Aspose OCR 的完整指南

有沒有想過如何直接在 C# 專案中 **create searchable PDF**，而不必離開程式碼？你並不是唯一有此需求的人。無論是數位化多語言文件，或是開發收據掃描應用程式，將圖片轉換成可搜尋的 PDF 都是一項顛覆性的功能。

在本教學中，我們將逐步說明如何使用 Aspose.OCR **create searchable PDF**，涵蓋從載入圖片到匯出完整可搜尋文件的所有步驟。過程中，我們也會示範如何 **convert image to PDF**、**extract text from image**，以及 **recognize multiple languages**——全部以單一、支援非同步的方式完成。

## 您將學會的內容

- 一個可執行的 C# 主控台應用程式，能讀取圖片、在 GPU 加速模式下執行 OCR，並產生可搜尋的 PDF。
- 了解為何啟用 GPU 會對效能產生影響的洞見。
- 用於下游處理的 **extract text from image** 技術。
- 一個清晰的範例，說明 **how to recognize multiple languages** 的單次處理方式。
- 擴充程式碼以處理其他格式或自訂 OCR 設定的技巧。

### 前置條件

- .NET 6.0 SDK 或更新版本（程式碼同樣可在 .NET Core 上編譯）。
- Aspose.OCR 授權（可先使用免費試用版；未授權時 API 仍可運作，但會加上浮水印）。
- 一張包含英文、阿拉伯文與韓文的範例圖片（或任何您需要的語言）。
- Visual Studio 2022 或您喜愛的 IDE。

全部準備好了嗎？太好了——讓我們開始吧。

---

## 步驟 1：設定專案並安裝 Aspose.OCR

首先，建立一個新的主控台專案：

```bash
dotnet new console -n SearchablePdfDemo
cd SearchablePdfDemo
```

接著加入 Aspose.OCR NuGet 套件：

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** 如果您打算在具備 GPU 的機器上執行 OCR，亦請安裝 `Aspose.OCR.Gpu` 套件。它會自動下載原生 CUDA 函式庫。

## 步驟 2：建立 OCR 引擎並啟用 GPU 加速

此操作的核心是 `OcrEngine`。啟用 GPU 可以為高解析度圖片的處理時間節省數秒。

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// ...

// Step 2: Create an OCR engine and turn on GPU support
var ocrEngine = new OcrEngine();
ocrEngine.Settings.EnableGpu = true;   // ← speeds up large images dramatically
```

為何要啟用 GPU？因為 OCR 本質上是一個大型矩陣乘法問題；GPU 能比 CPU 更有效率地處理這些平行任務。如果您在沒有 GPU 的無頭伺服器上執行，只需將 `EnableGpu` 保持為 `false`——引擎會自動回退至 CPU 處理。

## 步驟 3：非同步載入圖片

非同步 I/O 能讓 UI 保持回應，並防止伺服器情境下執行緒池耗盡。`OcrImage.FromFileAsync` 輔助方法抽象了串流處理的細節。

```csharp
using Aspose.OCR;

// ...

// Step 3: Load the image to be processed (async)
var imagePath = @"C:\Docs\multilingual_sample.jpg";
var image = await OcrImage.FromFileAsync(imagePath);
```

如果之後需要 **convert image to PDF**，請保留此 `OcrImage` 實例；您將直接將它傳遞給 PDF 匯出器。

## 步驟 4：辨識多語言文字

Aspose.OCR 允許您指定以逗號分隔的語言代碼清單。這就是在單次處理中 **how to recognize multiple languages** 的解決方案。

```csharp
using Aspose.OCR;

// ...

// Step 4: Run OCR with English, Arabic, and Korean support
var ocrResult = await ocrEngine.RecognizeAsync(image, new OcrOptions
{
    Language = "en,ar,ko"   // ← multiple languages, order doesn’t matter
});
```

`ocrResult.Text` 屬性現在保存了 Aspose 能辨識出的純文字內容。這就是 **extract text from image** 的核心。

```csharp
Console.WriteLine("Plain text extracted:");
Console.WriteLine(ocrResult.Text);
```

### 若語言未被辨識會怎樣？

如果您加入的語言在引擎中沒有對應模型，系統會直接忽略該語言，改以其他已支援的語言處理。為避免意外，請再次確認 Aspose 文件中的支援語言清單。

## 步驟 5：直接匯出可搜尋的 PDF

與其手動建立 PDF 再疊加文字，Aspose.OCR 提供一行程式碼即可 **how to generate searchable pdf**。此方法會將 OCR 文字嵌入為隱形圖層，使 PDF 在保留原始影像的同時具備搜尋功能。

```csharp
using Aspose.OCR.Output;

// ...

// Step 5: Export the recognized content as a searchable PDF
await ocrEngine.RecognizeToPdfAsync(image, new PdfExportOptions
{
    Language = "en,ar,ko",               // keep language consistency
    OutputPath = @"C:\Docs\sample_searchable.pdf"
});

Console.WriteLine("Searchable PDF saved at C:\\Docs\\sample_searchable.pdf");
```

在背後，Aspose 會建立一個 PDF 頁面，以原始位圖作為可見背景，並加入與影像座標對應的隱藏文字層。當您在 Adobe Reader 開啟檔案並按 **Ctrl + F** 時，即可搜尋到三種語言的文字。

## 步驟 6：整合全部 – 完整的非同步 `Main`

以下是完整、可直接執行的程式碼。將其貼到 `Program.cs`，替換檔案路徑後，按 **F5** 即可執行。

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Output;

class AllInOne
{
    static async Task Main()
    {
        // Step 2: Create an OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.EnableGpu = true;

        // Step 3: Load the image to be processed (async)
        var image = await OcrImage.FromFileAsync(@"C:\Docs\multilingual_sample.jpg");

        // Step 4: Recognize text in the image using multiple languages
        var ocrResult = await ocrEngine.RecognizeAsync(image, new OcrOptions
        {
            Language = "en,ar,ko"
        });

        Console.WriteLine("Plain text:");
        Console.WriteLine(ocrResult.Text);

        // Step 5: Export the recognized content as a searchable PDF
        await ocrEngine.RecognizeToPdfAsync(image, new PdfExportOptions
        {
            Language = "en,ar,ko",
            OutputPath = @"C:\Docs\sample_searchable.pdf"
        });

        Console.WriteLine("Searchable PDF saved.");
    }
}
```

### 預期輸出

```
Plain text:
Hello World!
مرحبا بالعالم!
안녕하세요 세계!
Searchable PDF saved.
```

當您開啟 `sample_searchable.pdf` 並搜尋 “Hello”、 “العالم” 或 “세계” 時，引擎會找到相應的單字，即使它們是以影像形式呈現。

## 步驟 7：常見問題與解決方法

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| **GPU not detected** | 機器缺少 CUDA 驅動程式或未安裝 `Aspose.OCR.Gpu` 套件。 | 安裝 NVIDIA 驅動程式，確認 CUDA 版本，或將 `EnableGpu = false`。 |
| **Missing language support** | 語言代碼不在內建模型集合中。 | 從 Aspose 下載額外語言套件，或僅使用支援的代碼。 |
| **PDF appears blank** | 輸出路徑無效或程式缺乏寫入權限。 | 使用絕對路徑並確保有適當權限，例如 `C:\Temp\output.pdf`。 |
| **Performance slowdown** | 大型圖片（>5 MP）造成記憶體壓力。 | 在 OCR 前縮小圖片，或提升程式的記憶體上限。 |

## 擴充範例

- **Batch processing:** 將核心邏輯包在 `foreach` 迴圈中，以遍歷資料夾內的多張圖片。
- **Custom OCR settings:** 調整 `ocrEngine.Settings.PageSegMode` 以因應單欄或多欄版面配置。
- **Metadata injection:** 使用 `PdfExportOptions` 將作者、標題或建立日期等資訊嵌入可搜尋的 PDF 中。

---

## 結論

現在您已掌握一套完整、端對端的流程，能使用 C# 直接從影像 **create searchable pdf**。透過上述步驟，您學會了如何 **convert image to pdf**、**extract text from image**，以及 **recognize multiple languages**——同時保持程式碼簡潔且支援非同步。

接下來，您可以嘗試不同的語言套件、加入 OCR 後處理（例如拼字檢查），或將此流程整合至即時提供可搜尋 PDF 的 Web API。沒有任何限制，而您剛寫的程式碼則是任何文件自動化專案的堅實基礎。

對效能調校或授權有任何疑問嗎？歡迎留言，我們一起討論。祝開發愉快！

## 接下來您可以學習什麼？

以下教學涵蓋與本指南密切相關的主題，並以此為基礎延伸。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [使用 Aspose.OCR 於 C# 提取影像文字並選擇語言](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [將影像轉換為 PDF C# – 儲存多頁 OCR 結果](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [如何在 .NET 使用 Aspose.OCR 進行 PDF OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}