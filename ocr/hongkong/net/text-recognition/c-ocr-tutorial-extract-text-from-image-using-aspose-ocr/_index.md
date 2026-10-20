---
category: general
date: 2026-02-19
description: c# OCR 教學，示範如何從圖像提取文字、從 JPG 識別文字，並使用 Aspose OCR 函式庫將圖像轉換為文字。
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- recognize text from jpg
- convert image to text
- extract text from jpg
language: zh-hant
og_description: C# OCR 教學，逐步帶領您從圖像提取文字、從 JPG 識別文字，以及使用 Aspose OCR 將圖像轉換為文字。
og_title: C# OCR 教學 – 使用 Aspose OCR 從圖像提取文字
tags:
- OCR
- C#
- Aspose
title: C# OCR 教學 – 使用 Aspose OCR 從圖像擷取文字
url: /zh-hant/net/text-recognition/c-ocr-tutorial-extract-text-from-image-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR 教學 – 使用 Aspose OCR 從圖像提取文字

有沒有想過如何在不抓狂的情況下 **從圖像中提取文字**？在許多實際應用中，你需要讀取掃描的發票、從照片中提取序號，或只是把 JPG 轉換成可搜尋的文字。這篇 **c# ocr 教學** 會一步步示範如何使用 Aspose OCR 函式庫完成，還會說明 *recognize text from jpg* 與 *convert image to text* 之間的細微差異。

本指南將教你如何設定 Aspose OCR NuGet 套件、編寫一個讀取圖片的簡易主控台程式，並處理最常見的陷阱（例如不支援的圖像格式或語言設定）。完成後，你將擁有一段可直接放入任何 .NET 專案的可運作程式碼，並能在數秒內 **從 jpg 檔案提取文字**。

## 需求條件

在開始之前，請確保已備妥以下項目：

| 前置條件 | 重要原因 |
|--------------|----------------|
| .NET 6 SDK (or later) | 現代 C# 功能與更佳效能 |
| Visual Studio 2022 or VS Code | 舒適的編輯體驗 |
| An image file (`sample.jpg`) you want to process | 你想處理的圖像檔案 (`sample.jpg`) |
| Internet access to pull the Aspose.OCR NuGet package | 需要下載 Aspose.OCR NuGet 套件的網路連線 |
| The library isn’t built‑in, we need to download it | 此函式庫未內建，我們必須下載 |

如果上述項目聽起來陌生，別慌——以下步驟會逐一說明，而且即使只使用純文字編輯器加上 `dotnet` CLI，程式碼也能正常執行。

## 步驟 1：安裝 Aspose.OCR NuGet 套件

首先，我們需要將 OCR 引擎加入專案。於專案資料夾開啟終端機並執行以下指令：

```bash
dotnet add package Aspose.OCR
```

> **小技巧：** 若你使用 Visual Studio，也可以右鍵點擊專案 → *管理 NuGet 套件* → 搜尋 “Aspose.OCR” 並點選 *安裝*。

此指令會下載最新的穩定版（截至 2026 年 2 月為 23.3），並將參考加入你的 `.csproj`。不需要額外複製 DLL，所有工作皆由 .NET 執行階段處理。

## 步驟 2：建立簡易主控台應用程式骨架

現在讓我們搭建一個最小的主控台應用程式來承載 OCR 邏輯。建立名為 `Program.cs` 的檔案（或取代現有檔案），貼上以下骨架程式碼：

```csharp
using System;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the OCR routine from here.
            Console.WriteLine("Starting c# OCR tutorial...");
        }
    }
}
```

請注意最上方的 `using System;` ——我們稍後會用於主控台輸出以及處理可能的例外情況。

## 步驟 3：初始化 OCR 引擎並設定語言

Aspose OCR 支援數十種語言，但大多數示範只需英文即可。此引擎輕量，我們可以直接在 `Main` 中實例化。於介紹性的 `Console.WriteLine` 之 **後** 加入以下程式碼：

```csharp
using Aspose.OCR;   // <-- add this using directive at the top of the file

// ...

// Step 3: Create an OCR engine and configure it for English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // you can switch to Language.Spanish, etc.
};
```

為什麼要明確設定語言？因為底層的辨識演算法會使用特定語言的字典來提升準確度。跳過此步驟雖可能仍能運作，但在非英文文字上常會得到亂碼結果。

## 步驟 4：從 JPG 圖像辨識文字

這是本教學的核心——將圖像檔案送入引擎並取得文字結果。於引擎初始化後立即插入以下程式碼：

```csharp
// Step 4: Define the path to the image you want to process
string imagePath = @"YOUR_DIRECTORY/sample.jpg";   // <-- replace with your actual path

try
{
    // Recognize the image. This method returns an OcrResult object.
    OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

    // Display the raw OCR output in the console
    Console.WriteLine("\n--- OCR Output ---");
    Console.WriteLine(ocrResult.Text);
}
catch (Exception ex)
{
    // If something goes wrong (file not found, unsupported format, etc.)
    Console.Error.WriteLine($"Error during OCR: {ex.Message}");
}
```

需要留意的幾點：

* **`RecognizeImage`** 支援大多數常見的點陣圖格式——JPEG、PNG、BMP、TIFF。這也是本教學能在不額外轉換的情況下 *recognize text from jpg* 的原因。
* 此方法會回傳 `OcrResult` 物件，內含 `Text`、`Confidence`，若需要位置資料，還有 `BoundingBoxes`。
* 將呼叫包在 `try/catch` 中可提升程式穩定性——缺少檔案時不會導致整個應用程式崩潰。

## 步驟 5：執行應用程式並驗證輸出

儲存檔案，回到終端機，執行以下指令：

```bash
dotnet run
```

你應該會看到類似以下的輸出：

```
Starting c# OCR tutorial...

--- OCR Output ---
Hello, world!
This is a sample image containing text.
```

如果主控台印出與 `sample.jpg` 中相同的文字，恭喜！你剛剛使用少量 C# 程式碼 **將圖像轉換為文字**。

### 若輸出結果異常該怎麼辦？

* **信心度低：** 嘗試提升圖像解析度或進行前處理（例如銳化、二值化）。Aspose OCR 提供 `PreprocessImage` 方法可供探索。
* **語言錯誤：** 再次確認 `ocrEngine.Language` 與來源圖像的語言相符。
* **不支援的格式：** 確認檔案副檔名真的是 JPEG；有時 PNG 以 `.jpg` 副檔名儲存會讓解析器困惑。

## 步驟 6：打包完整範例以供重複使用

以下是 **完整且可執行的程式**，你可以直接複製貼上到任何新的主控台專案。它包含所有必要的 `using` 陳述式、例外處理，以及說明每行程式碼的註解。

```csharp
// Program.cs
using System;
using Aspose.OCR;   // Aspose OCR library

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("=== c# OCR Tutorial – Extract Text from Image ===");

            // 1️⃣ Create OCR engine and set language (English by default)
            var ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Path to the image you want to process
            string imagePath = @"YOUR_DIRECTORY/sample.jpg"; // <-- update this

            try
            {
                // 3️⃣ Perform OCR – this both *recognizes text from jpg* and *extracts text from image*
                OcrResult result = ocrEngine.RecognizeImage(imagePath);

                // 4️⃣ Output the recognized string – you’ve now *converted image to text*
                Console.WriteLine("\n--- OCR Result ---");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                // Friendly error message – helps when the file is missing or corrupted
                Console.Error.WriteLine($"Oops! Something went wrong: {ex.Message}");
            }

            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

將其儲存為 `Program.cs`，執行 `dotnet run`，即可即時示範 **從 jpg 提取文字** 的效果。

## 加分項：從資料夾中的多張圖像提取文字

通常你需要批次處理整個掃描資料夾。以下是一段快速擴充程式碼，會遍歷資料夾內每個 `.jpg` 檔案，執行 OCR，並將結果寫入同名的 `.txt` 檔案。

```csharp
using System.IO;

// ...

string folderPath = @"YOUR_DIRECTORY"; // folder containing many jpg files

foreach (string file in Directory.GetFiles(folderPath, "*.jpg"))
{
    try
    {
        OcrResult batchResult = ocrEngine.RecognizeImage(file);
        string txtPath = Path.ChangeExtension(file, ".txt");
        File.WriteAllText(txtPath, batchResult.Text);
        Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Failed on {Path.GetFileName(file)}: {ex.Message}");
    }
}
```

此程式碼片段示範了在實務情境中大規模 *extract text from image* 檔案的需求，這是文件管理系統的常見需求。

## 圖片說明（可選）

若你想在文章中加入視覺提示，可嵌入主控台輸出的螢幕截圖：

![c# OCR 教學主控台輸出顯示提取文字](/images/ocr-console.png)

*Alt 文字包含主要關鍵字以符合 SEO 要求。*

## 常見問題與特殊情況

**Q: 這能用於 PDF 嗎？**  
A: 不能直接使用。必須先將每頁 PDF 轉為圖像（例如使用 Aspose.PDF），再將這些圖像送入 OCR 引擎。

**Q: 手寫文字呢？**  
A: Aspose OCR 主要針對印刷文字。若要辨識草寫或手寫筆記，需要使用專門的模型（例如 Azure Cognitive Services 或 Google Vision）。

**Q: 我可以變更輸出編碼嗎？**  
A: `OcrResult.Text` 為 .NET 的 `string`，預設為 UTF‑16，因此你可以使用 `File.WriteAllText(path, text, Encoding.UTF8)` 等方式寫入任意檔案編碼。

**Q: 這個函式庫是免費的嗎？**  
A: Aspose 提供帶有浮水印的完整功能評估模式。正式上線時需購買授權，但 API 使用方式保持不變。

## 結論

你剛剛完成了一個 **c# OCR 教學**，內容涵蓋安裝 Aspose OCR、初始化引擎，以及 **從圖像檔案提取文字**（包括 JPEG），讓你能夠 *convert

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}