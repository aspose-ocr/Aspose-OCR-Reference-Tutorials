---
category: general
date: 2026-02-13
description: 使用 Aspose OCR 於 C# 從圖片中提取文字。了解如何從 jpg 讀取文字並對圖片執行 OCR，並提供完整、可執行的範例。
draft: false
keywords:
- extract text from image
- read text from jpg
- run OCR on image
- Aspose OCR C#
- OCR language packs
language: zh-hant
og_description: 使用 Aspose OCR 在 C# 中從圖像提取文字。本指南示範如何從 JPG 讀取文字並對圖像執行 OCR，並提供完整程式碼範例。
og_title: 使用 Aspose OCR 從圖像提取文字 – C# 快速入門
tags:
- C#
- OCR
- Aspose
title: 使用 Aspose OCR 從圖像提取文字 – C# 快速入門
url: /zh-hant/net/text-recognition/extract-text-from-image-with-aspose-ocr-c-quickstart/
---

braces; keep unchanged.

Check tables: keep markdown table syntax.

Check URLs: none present.

Check images: none.

Now produce final output with all translated content and unchanged shortcodes.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 從圖像提取文字 – C# 快速入門

有沒有曾經需要 **從圖像提取文字**，卻不確定該選哪個函式庫？你並不孤單——開發者常常在讀取 jpg 檔案中的文字時掙扎，尤其是內容是非拉丁文字時。好消息是？使用 Aspose OCR，只需幾行 C# 程式碼即可對圖像檔案執行 OCR，且函式庫會自行按需下載語言包。

在本教學中，我們將逐步說明一個完整的端到端範例，展示如何使用 Aspose OCR **從圖像提取文字**、將辨識限制為俄文，並將結果輸出到主控台。完成後，你將能夠讀取 jpg 檔案中的文字、對任何尺寸的圖像資產執行 OCR，並以最小的變更將程式碼套用到其他語言。

> **你將學到**
> * 如何在 .NET 專案中安裝並引用 Aspose OCR。  
> * 執行 **從圖像提取文字** 的完整步驟——初始化引擎、選擇語言，並呼叫 `RecognizeImage`。  
> * 為何你可能想將引擎鎖定於單一語言包（提升速度與準確度）。  
> * 常見的陷阱，例如檔案遺失或不支援的格式，以及如何優雅地處理它們。  

## 前置條件

在深入之前，請確保你的機器上已具備以下項目：

| 需求 | 原因 |
|------|------|
| .NET 6.0 SDK or later | Aspose OCR 目標為 .NET Standard 2.0+，因此 .NET 6 提供最新的執行時功能。 |
| Visual Studio 2022 (or any IDE you like) | 有助於除錯，但非必須。 |
| An image file (`cyrillic_sample.jpg`) that contains Cyrillic text | 我們將使用此檔案示範 **從 jpg 讀取文字**。 |
| Internet connection (first run only) | Aspose OCR 會按需下載語言包。 |

如果缺少上述任何項目，請立即取得——安裝 SDK 後無需重新啟動。

## 步驟 1：安裝 Aspose OCR NuGet 套件

首先需要的是 Aspose OCR 函式庫。於專案資料夾中開啟終端機並執行以下指令：

```bash
dotnet add package Aspose.OCR
```

此指令會取得最新的穩定版（截至 2026 年 2 月為 23.12），並將其加入你的 `.csproj`。此套件包含核心 OCR 引擎與輕量級的語言包下載器，讓你不必將龐大的檔案打包到應用程式中。

> **專業提示：** 若你在企業代理伺服器後工作，請在執行指令前設定 `http_proxy` 環境變數，以避免下載錯誤。

## 步驟 2：建立 Console 應用程式骨架

讓我們建立一個最小的 console 應用程式來容納 OCR 邏輯。開啟 `Program.cs`（或建立新檔案），並貼上以下骨架程式碼。請注意頂部的 `using` 指令——它們會將 Aspose OCR 命名空間匯入作用域。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in in the next steps.
        }
    }
}
```

此時專案已能編譯，但尚未執行任何功能。接下來的章節將完善 **在圖像上執行 OCR** 的工作流程。

## 步驟 3：初始化 OCR 引擎（從圖像提取文字）

要 **從圖像提取文字**，首先需要建立 `OcrEngine` 實例。Aspose OCR 會在首次需要時延遲下載語言資源，從而保持初始二進位檔案體積小。

```csharp
// Step 3: Initialize the OCR engine (resources are downloaded on demand)
var ocrEngine = new OcrEngine();
```

為何在此初始化而非使用靜態欄位？在 `Main` 內部進行可確保任何例外（例如缺少原生相依性）能及早拋出，讓除錯更為簡便。

## 步驟 4：限制辨識語言（從 JPG 讀取文字）

如果你知道要掃描的文字語言——例如俄文——可透過設定 `Language` 屬性提升速度與準確度。當你 **從 jpg 讀取文字** 且檔案包含西里爾字元時，這特別有用。

```csharp
// Step 4: Limit recognition to the Russian language pack (ISO code "ru")
ocrEngine.Language = OcrLanguage.Russian;
```

在背後，Aspose OCR 會在首次執行此行程式碼時下載俄文語言包。之後的執行會重複使用快取的語言包，故首次下載後不再有網路開銷。

> **為何鎖定語言？**  
> * **效能：** 引擎會跳過非所選字母表的字元掃描。  
> * **準確度：** 會套用語言特定的啟發式（例如常見詞頻），降低誤辨識。

若需支援多種語言，可傳入逗號分隔的列表，例如 `OcrLanguage.English | OcrLanguage.Russian`。

## 步驟 5：對目標 JPG 執行 OCR（在圖像上執行 OCR）

現在我們真的要 **在圖像上執行 OCR**。提供 JPG 檔案的完整路徑——Aspose OCR 支援多種格式（`.png`、`.bmp`、`.tif` 等），但此示範僅使用 `.jpg`。

```csharp
// Step 5: Perform OCR on the image containing Cyrillic text
string imagePath = @"YOUR_DIRECTORY/cyrillic_sample.jpg";
var recognizedResult = ocrEngine.RecognizeImage(imagePath);
```

若找不到檔案，`RecognizeImage` 會拋出 `FileNotFoundException`。為使教學更健全，請將呼叫包在 try‑catch 區塊中：

```csharp
try
{
    var recognizedResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("✅ OCR succeeded!");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(recognizedResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"❌ Error during OCR: {ex.Message}");
}
```

`RecognizeImage` 方法會回傳 `OcrResult` 物件，其 `Text` 屬性包含純文字提取結果。若日後需要版面資訊，也可存取 `Boxes` 取得邊框資料。

## 步驟 6：驗證輸出

執行程式 (`dotnet run`) 後，應會看到類似以下的輸出：

```
✅ OCR succeeded!
Extracted text:
Пример текста на кириллице
```

若輸出呈現亂碼，請再次確認圖像是否清晰且已選擇正確語言。模糊或低對比度的圖像是導致 OCR 效果不佳的主要原因。

### 邊緣案例與常見問題

| 情況 | 處理方式 |
|------|----------|
| **圖像包含多種語言** | 將 `ocrEngine.Language` 設為組合，例如 `OcrLanguage.English | OcrLanguage.Russian`。 |
| **大量圖像批次** | 在多個檔案間重複使用相同的 `OcrEngine` 實例；它會快取語言資料。 |
| **在無頭伺服器上執行** | 不需要 UI——Aspose OCR 在 Docker 或 Azure Functions 中亦能正常運作。 |
| **需要更高準確度** | 調整 `ocrEngine.Options`（例如 `ocrEngine.Options.Denoise = true`）。 |
| **不支援的檔案格式** | 在呼叫 `RecognizeImage` 前，先將圖像轉換為支援的格式（PNG 或 JPG）。 |

## 完整範例程式

以下是完整、可直接複製貼上的程式碼，已整合上述所有步驟。將其儲存為 `Program.cs`，並於命令列執行。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine (downloads language packs on first use)
            var ocrEngine = new OcrEngine();

            // 2️⃣ Restrict recognition to Russian – speeds up processing and boosts accuracy
            ocrEngine.Language = OcrLanguage.Russian;

            // 3️⃣ Path to the JPG you want to read text from
            string imagePath = @"YOUR_DIRECTORY/cyrillic_sample.jpg";

            // 4️⃣ Perform OCR and handle possible errors
            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("✅ OCR completed successfully.");
                Console.WriteLine("🖼️ Extracted text:");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Failed to extract text from image: {ex.Message}");
            }
        }
    }
}
```

**預期的主控台輸出**（假設範例圖像包含文字 “Пример текста на кириллице”）：

```
✅ OCR completed successfully.
🖼️ Extracted text:
Пример текста на кириллице
```

若將圖像換成英文照片並將 `ocrEngine.Language = OcrLanguage.English;`，相同程式碼即可 **從 jpg 讀取文字**（英文），且不需其他變更。

## 加分項目：對多個檔案執行 OCR

通常你會需要對 **在圖像上執行 OCR** 的集合進行處理。以下是一段快速程式碼，會遍歷資料夾中的檔案：

```csharp
string folder = @"YOUR_DIRECTORY";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    try
    {
        var result = ocrEngine.RecognizeImage(file);
        Console.WriteLine($"[{System.IO.Path.GetFileName(file)}] => {result.Text}");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error processing {file}: {ex.Message}");
    }
}
```

引擎會重複使用先前下載的語言包，因而批次執行效率高。

## 結論

現在你已掌握使用 Aspose OCR 於 C# 中 **從圖像提取文字** 的完整、可投入生產的模式。教學涵蓋了從安裝 NuGet 套件、處理錯誤到擴展至多檔案的全部內容。無論是 **從 jpg 讀取文字** 資產、掃描 PDF，或建構文件自動化流程，都可套用相同方法——只需更換語言包或微調 OCR 選項。

準備好進一步了嗎？試試看：

* 嘗試其他語言（例如 `OcrLanguage.ChineseSimplified`）。  
* 透過 `recognizedResult.Boxes` 抽取版面資訊。  
* 將 OCR 流程整合至 ASP.NET Core API，讓其他服務可即時請求文字提取。

祝程式開發順利，願你的圖像永遠足夠清晰，以獲得完美的 OCR 效果！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}