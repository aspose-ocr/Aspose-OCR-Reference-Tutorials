---
category: general
date: 2026-02-14
description: 如何在 C# 中使用 Aspose.OCR 進行 OCR – 學習從圖像提取文字、從檔案載入圖像，並快速執行 OCR。
draft: false
keywords:
- how to perform OCR
- extract text from image
- load image from file
- recognize text from jpg
- run OCR on image
language: zh-hant
og_description: 如何在 C# 中使用 Aspose.OCR 執行 OCR。本指南將示範如何從圖像中提取文字、從檔案載入圖像，以及高效地對圖像執行 OCR。
og_title: 如何在 C# 中執行 OCR – 完整程式設計教學
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 如何在 C# 中執行 OCR – 逐步指南
url: /zh-hant/net/text-recognition/how-to-perform-ocr-in-c-step-by-step-guide/
---

placeholders and formatting.

Let's assemble.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中執行 OCR – 完整程式教學

有沒有想過 **how to perform OCR** 在你剛用手機拍的照片上？也許你需要從 JPEG 中提取街道標誌文字以供導航應用程式使用，或是手頭有一批掃描過的合約想要轉成可搜尋的文字。簡而言之，你想要 *extract text from image* 而不將任何資料傳到雲端。

好消息是，你可以使用 Aspose.OCR for .NET 在本機完成所有這些操作。在本教學中，我們將逐步說明如何從檔案載入影像、從 JPG 識別文字，最後 **run OCR on image** 完全離線。完成後，你將擁有一段可直接執行的程式碼片段，會在主控台印出辨識出的阿拉伯文字。

> **你將獲得：** 一個自包含、可執行的 C# 程式、每行程式碼意義的說明，以及處理常見邊緣情況（如資源遺失或不支援的語言）的技巧。

## 前置條件

在深入之前，請確保你已具備以下項目：

| Requirement | Reason |
|-------------|--------|
| .NET 6.0 或更新版本（或 .NET Framework 4.7+） | Aspose.OCR 目標為 .NET Standard 2.0，任何現代執行環境皆可運作。 |
| Visual Studio 2022（或搭配 C# 擴充功能的 VS Code） | IDE 能方便管理 NuGet 套件並執行 console 應用程式。 |
| Aspose.OCR NuGet 套件 (`Aspose.OCR`) | 這是實際執行 OCR 工作的函式庫。 |
| 包含離線 OCR 資源的資料夾（從 Aspose 下載） | 離線資源可避免辨識過程中的任何 HTTP 呼叫。 |
| 影像檔案（例如 `arabic_sign.jpg`） | 我們會使用包含阿拉伯文字的 JPEG，但任何語言皆可。 |

如果缺少上述任何項目，請立即取得——在教學開始後才發現缺少相依性是沒意義的。

## 步驟 1：安裝 Aspose.OCR 並準備資源

首先，將 Aspose.OCR 套件加入你的專案：

```bash
dotnet add package Aspose.OCR
```

套件安裝完成後，從 Aspose 官方網站下載 **offline OCR resource bundle**，並解壓縮到本機的資料夾，例如：

```
C:\OCRResources\
```

> **為什麼這很重要：** 在啟動時載入資源一次，可消除網路延遲，且因為資料不會離開機器，使你的解決方案符合 GDPR 要求。

## 步驟 2：建立 OCR Engine 並指向資源資料夾

現在我們將實例化 `Engine` 類別，並告訴它資源所在的位置。這就是本機 **how to perform OCR** 的核心。

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Step 2: Initialize the OCR engine with the offline resource folder
Engine ocrEngine = new Engine
{
    // Replace with the path you used in the previous step
    ResourceFolder = @"C:\OCRResources"
};

// Load the resources into memory – this prevents any hidden HTTP calls
ocrEngine.LoadResources();
```

> **專業提示：** 若預期資料夾路徑可能錯誤，請將 `LoadResources` 呼叫包在 try‑catch 區塊中。例外訊息會精確指出缺少哪個檔案。

## 步驟 3：從檔案載入影像

接下來，我們需要 **load image from file**，讓引擎能分析它。Aspose.OCR 使用自訂的 `ImageStream` 包裝類別。

```csharp
// Step 3: Load the JPEG you want to recognize
ImageStream image = ImageStream.FromFile(@"C:\OCRResources\arabic_sign.jpg");
```

如果影像位於其他位置，只需更改路徑即可。`ImageStream` 類別抽象化底層的 bitmap 處理，讓你不必擔心 GDI+ 相容性。

## 步驟 4：使用語言設定辨識 JPG 文字

現在進入 **how to perform OCR** 的核心——實際辨識字元。我們將請求阿拉伯文辨識，但你可以將 `Language.Arabic` 換成其他支援的語言。

```csharp
// Step 4: Run OCR specifying the desired language (Arabic in this example)
OcrResult ocrResult = ocrEngine.Recognize(
    image,
    new OcrOptions { Language = Language.Arabic }
);
```

> **為什麼要指定語言？** OCR 引擎會使用特定語言的字典與字元模型。提供正確的語言可大幅提升準確度，尤其是像阿拉伯文這類形狀複雜的文字。

## 步驟 5：顯示擷取的文字

最後，讓我們 **extract text from image** 並將結果印出。這是驗證 OCR 成功的最簡單方式。

```csharp
// Step 5: Output the recognized text to the console
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrResult.Text);
```

執行程式後，應該會在主控台看到標誌上的阿拉伯語句子。如果輸出出現亂碼，請再次確認已選擇正確的語言，且資源資料夾內有阿拉伯語的資料檔案。

## 完整範例程式

以下是完整、可直接編譯的程式碼，將所有步驟串接起來。將它複製貼上到新的 console 專案（`dotnet new console`），然後按 **F5** 執行。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Configure the OCR engine with offline resources
            // -------------------------------------------------
            Engine ocrEngine = new Engine
            {
                ResourceFolder = @"C:\OCRResources" // <-- change to your folder
            };
            ocrEngine.LoadResources(); // Loads language packs, fonts, etc.

            // -------------------------------------------------
            // Step 2: Load the image you want to process
            // -------------------------------------------------
            ImageStream image = ImageStream.FromFile(@"C:\OCRResources\arabic_sign.jpg");

            // -------------------------------------------------
            // Step 3: Recognize text – specify language to improve accuracy
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(
                image,
                new OcrOptions { Language = Language.Arabic } // Change as needed
            );

            // -------------------------------------------------
            // Step 4: Output the result
            // -------------------------------------------------
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**預期輸出（範例）：**

```
=== OCR Result ===
مطار القاهره الدولي
```

如果將影像換成英文標誌並設定 `Language.English`，相同程式碼會輸出英文文字。這展示了 **run OCR on image** 的彈性。

## 從影像擷取文字 – 處理常見情境

### 1. 多頁或多影格影像

某些影像格式（如 TIFF）可能包含多個頁面。若要在此情況下 **extract text from image**，請對每個影格進行迴圈：

```csharp
for (int i = 0; i < image.FramesCount; i++)
{
    image.CurrentFrame = i;
    OcrResult pageResult = ocrEngine.Recognize(image, new OcrOptions { Language = Language.English });
    Console.WriteLine($"Page {i + 1}: {pageResult.Text}");
}
```

### 2. 低解析度影像

當解析度低於 70 dpi 時，OCR 準確度會急劇下降。若出現模糊結果，請先將影像放大：

```csharp
using System.Drawing;
using System.Drawing.Drawing2D;

// Load as Bitmap, resize, then wrap back into ImageStream
Bitmap bmp = new Bitmap(@"C:\OCRResources\lowres.jpg");
Bitmap highRes = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
ImageStream highResStream = ImageStream.FromBitmap(highRes);
```

### 3. 缺少語言套件

若出現類似 *“Language data not found”* 的例外，請再次確認相應的 `.dat` 檔案是否存在於你的 `ResourceFolder` 中。Aspose 為每種語言提供獨立的 zip 檔案。

## 執行影像 OCR – 效能建議

- **Cache the Engine:** 為每張影像建立新的 `Engine` 會增加額外開銷。請保留單一實例以供批次處理使用。
- **Parallelize Safely:** 在 `LoadResources` 後，`Engine` 對唯讀操作是 thread‑safe 的。你可以啟動多個任務，分別對不同影像呼叫 `Recognize`。
- **Dispose When Done:** 雖然 `Engine` 實作 `IDisposable`，.NET GC 最終會回收。但在 `using` 區塊中明確呼叫 `ocrEngine.Dispose()` 是個好習慣。

```csharp
using (Engine ocrEngine = new Engine { ResourceFolder = @"C:\OCRResources" })
{
    ocrEngine.LoadResources();
    // run recognitions here
}
```

## 從 JPG 辨識文字 – 需留意的邊緣情況

| Situation | What to Check | Fix |
|-----------|---------------|-----|
| **損毀的 JPEG** | `ImageStream.FromFile` 會拋出 `FileNotFoundException` 或 `ArgumentException`。 | 驗證檔案完整性，必要時使用圖形編輯器重新儲存影像。 |
| **不支援的語言** | `Language` 列舉未包含你的目標語言。 | 更新 Aspose.OCR 至最新版本；新語言會定期加入。 |
| **混合文字影像**（例如 English + Arabic） | 單一語言設定可能會遺漏次要文字。 | 分別以不同語言設定執行兩次 OCR，然後將結果串接起來。 |

## 小結 – 你現在已掌握如何在 C# 中執行 OCR

本指南說明了使用 Aspose.OCR 的 **how to perform OCR**，從安裝 NuGet 套件到印出辨識文字。你學會了 **load image from file**、**extract text from image**、**recognize text from jpg**，以及以可投入生產的方式安全 **run OCR on image**。

### 接下來？

- **嘗試其他檔案格式**（如 PNG 或 BMP）——只需更改檔案副檔名。
- **整合資料庫**，將 OCR 結果儲存以供可搜尋的檔案庫使用。
- **結合電腦視覺**（例如在 OCR 前偵測文字區域）以提升速度。

隨意調整語言設定、批次處理資料夾，或將輸出接入 Web API。OCR 是基礎元件；當你將它編織進更大的工作流程時，才能發揮真正的威力。

祝開發愉快，願你的影像永遠清晰如水晶！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}