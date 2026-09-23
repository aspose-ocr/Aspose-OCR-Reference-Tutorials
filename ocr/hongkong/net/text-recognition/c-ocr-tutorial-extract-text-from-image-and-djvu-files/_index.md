---
category: general
date: 2026-01-09
description: c# OCR 教學，示範如何從圖像檔案提取文字，並使用 Aspose.OCR 將 DJVU 轉換為文字。分鐘內學會一步步提取。
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- how to extract text
- convert djvu to text
- extract text from djvu
language: zh-hant
og_description: C# OCR 教學，快速示範如何從圖像檔案提取文字，並使用 Aspose.OCR 將 DJVU 轉換為文字。請按照指南獲得可行的解決方案。
og_title: C# OCR 教學 – 從圖像與 DJVU 提取文字
tags:
- OCR
- C#
- Aspose
title: c# OCR 教學：從圖像與 DJVU 檔案提取文字
url: /zh-hant/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-djvu-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR 教學 – 從圖像與 DJVU 檔案提取文字

有沒有想過如何在不抓狂的情況下從圖像檔案中提取文字？在本 **c# OCR 教學** 中，我們將逐步示範一個完整、可直接執行的範例，從一般圖片 *以及* DJVU 文件中提取文字。  

如果你也在尋找快速的 **將 DJVU 轉換為文字** 方法，恭喜你來對地方了——不需要額外的轉換工具，僅使用純 C# 程式碼。

## 你將學到

- 如何在 .NET 專案中設定 Aspose.OCR 函式庫。  
- 取得 **從圖像提取文字** 所需的完整程式碼。  
- 一個簡潔的 **從 DJVU 提取文字** 方法（是的，同一個引擎即可完成）。  
- 常見的陷阱（大型檔案、缺少字型、授權問題）以及避免方式。  

你只需要最新的 .NET SDK 以及網路連線以下載 NuGet 套件。無需任何 OCR 先前經驗。

## 前置條件

在深入之前，請確保你已具備以下條件：

| 需求 | 原因說明 |
|------|----------|
| .NET 6.0 or later | Aspose.OCR 目標為 .NET Standard 2.0，使用 .NET 6 以上可獲得最佳效能。 |
| Visual Studio 2022 (or VS Code) | IDE 可讓套件管理變得輕鬆，但任何編輯器皆可使用。 |
| NuGet package **Aspose.OCR** | 這是實際執行繁重工作的引擎。 |
| A sample image (`sample.png`) and a DJVU file (`sample.djvu`) | 我們將使用它們示範兩種提取情境。 |

你可以使用以下指令安裝套件：

```bash
dotnet add package Aspose.OCR
```

> **小技巧：** 若在 CI 伺服器上，於建置步驟加入 `--no-restore`，並在開始時一次還原，以加快速度。

## 步驟 1：初始化 OCR 引擎 – c# OCR 教學的核心

我們首先要做的是建立 `OcrEngine` 的實例。可以把它想像成在程式中開啟掃描器。

```csharp
using Aspose.OCR;

var ocrEngine = new OcrEngine();
```

為什麼每次都要建立新引擎？因為引擎會保存設定（語言、偵測模式等）。重新建立可避免舊設定在執行間互相影響。

## 步驟 2：載入並辨識圖像 – 如何從圖像提取文字

現在我們將一般位圖（PNG、JPEG、BMP…）輸入引擎。`RecognizeImage` 方法會回傳辨識出的字串。

```csharp
// Path to your image file
string imagePath = @"C:\OCR\sample.png";

// Perform OCR
string imageText = ocrEngine.RecognizeImage(imagePath);

// Show the result
Console.WriteLine("=== Text extracted from image ===");
Console.WriteLine(imageText);
```

* **File existence** – 若路徑錯誤，方法會拋出 `FileNotFoundException`。若預期使用者提供路徑，請以 `try/catch` 包住。  
* **Image quality** – OCR 在 300 dpi 以上的圖像上表現最佳。低解析度的掃描可能產生亂碼。  
* **Language support** – 預設 Aspose.OCR 假設使用英文。若要變更語言，請在 `RecognizeImage` 前設定 `ocrEngine.Language = Language.Spanish;`。

## 步驟 3：辨識 DJVU 文件中的文字 – 將 DJVU 轉換為文字

DJVU 是一種可容納多頁的容器格式。Aspose.OCR 能直接處理，只需指向該檔案即可。

```csharp
// Path to your DJVU file
string djvuPath = @"C:\OCR\sample.djvu";

// Perform OCR on the DJVU file
string djvuText = ocrEngine.RecognizeImage(djvuPath);

// Output the result
Console.WriteLine("\n=== Text extracted from DJVU ===");
Console.WriteLine(djvuText);
```

在底層，引擎會將每一頁提取為圖像，並使用相同的辨識流程。因此不需要額外的「將 DJVU 轉換為文字」步驟——OCR 引擎會自行完成。

### 處理多頁 DJVU 檔案

若 DJVU 包含多頁，`RecognizeImage` 會依序串接它們。若需要每頁分開取得，可使用回傳 `List<string>` 的重載方法：

```csharp
var pagesText = ocrEngine.RecognizeImage(djvuPath, true); // true = return per‑page list
for (int i = 0; i < pagesText.Count; i++)
{
    Console.WriteLine($"\n--- Page {i + 1} ---");
    Console.WriteLine(pagesText[i]);
}
```

## 步驟 4：微調引擎以提升準確度 – 為什麼這很重要

預設的辨識結果已相當不錯，但透過調整幾個設定仍可進一步提升：

```csharp
ocrEngine.Language = Language.English;      // set detection language
ocrEngine.Dpi = 300;                        // enforce 300 DPI processing
ocrEngine.IsDetectOrientation = true;      // auto‑rotate tilted pages
ocrEngine.IsDetectSkew = true;              // correct slanted text
```

這些旗標在 **如何從先儲存為 DJVU 的掃描 PDF 提取文字** 時特別有用。開啟方向偵測可免除手動旋轉圖像的步驟。

## 步驟 5：處理授權與執行時錯誤

Aspose.OCR 提供免費試用版，會在輸出數頁後加上「Demo」水印。若要移除水印，請加入授權檔案：

```csharp
// Assuming you have a license.xml in the project root
var license = new Aspose.OCR.License();
license.SetLicense("license.xml");
```

若遺漏此步驟，引擎仍會運作，但結果會包含「Demo」字樣。另外，處理大型 DJVU 檔案時要留意 `OutOfMemoryException`——可參考前述逐頁處理的方式。

## 完整、可執行的範例

以下是一個獨立的 Console 程式，將所有步驟整合在一起。直接複製貼上、調整檔案路徑，然後按 **Run** 即可。

```csharp
// Complete c# OCR tutorial – extract text from image and DJVU
using System;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Set up licensing (optional, removes demo watermark)
            // var license = new License();
            // license.SetLicense("license.xml");

            // 2️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = Language.English,
                Dpi = 300,
                IsDetectOrientation = true,
                IsDetectSkew = true
            };

            // 👉 Extract text from a regular image
            string imagePath = @"C:\OCR\sample.png";
            try
            {
                string imageText = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("=== Text extracted from image ===");
                Console.WriteLine(imageText);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Image OCR failed: {ex.Message}");
            }

            // 👉 Extract text from a DJVU file (convert DJVU to text)
            string djvuPath = @"C:\OCR\sample.djvu";
            try
            {
                // Single string for all pages
                string djvuText = ocrEngine.RecognizeImage(djvuPath);
                Console.WriteLine("\n=== Text extracted from DJVU ===");
                Console.WriteLine(djvuText);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"DJVU OCR failed: {ex.Message}");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**預期輸出**（假設檔案內含「Hello World」字串）：

```
=== Text extracted from image ===
Hello World

=== Text extracted from DJVU ===
Hello World
```

若來源檔案有多行文字，將會完整保留原始文件的換行。

## 常見問題與邊緣案例處理

* **如果圖像是黑白的呢？**  
  OCR 仍能正常運作，但可透過 `ocrEngine.ImagePreprocessOptions = ImagePreprocessOptions.Contrast;` 提升對比度。

* **我只能提取數字嗎？**  
  可以——在呼叫 `RecognizeImage` 前設定 `ocrEngine.CharWhitelist = "0123456789";`。

* **檔案大小有上限嗎？**  
  引擎會將整個檔案載入記憶體。對於超過約 100 MB 的檔案，建議改為逐頁處理（參見步驟 3 的 List 重載）。

* **這與 Tesseract 有何不同？**  
  Aspose.OCR 為商業函式庫，內建 DJVU 支援且無需本機相依檔案；而 Tesseract 需要本機二進位檔及額外的 DJVU 轉換工具。

## 結論

你剛完成一個 **c# OCR 教學**，示範如何使用 Aspose.OCR **從圖像檔案提取文字**，以及無縫 **將 DJVU 轉換為文字**。此範例涵蓋從套件安裝到授權、從單頁圖像提取到多頁 DJVU 處理，甚至還提供提升準確度的技巧。

接下來，你可以探索 **如何從 PDF 提取文字**、將 OCR 步驟整合至 Web API，或嘗試語言套件以處理多語言文件。沒有任何限制——只要記住關鍵要點：設定引擎、提供檔案、讀取回傳的字串。

還有其他問題嗎？歡迎留言、在自己的文件上測試程式碼，祝開發愉快！ 

![c# OCR tutorial screenshot showing console output](/images/csharp-ocr-tutorial.png "c# OCR tutorial – console output example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}