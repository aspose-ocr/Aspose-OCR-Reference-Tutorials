---
category: general
date: 2026-02-16
description: 如何在 C# 中使用 OCR 識別圖像文字、從 JPEG 提取文字，並使用 Aspose OCR 將圖像轉換為文字。逐步指南。
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from jpeg
- convert image to text
- how to extract text
language: zh-hant
og_description: 學習如何在 C# 中使用 OCR，從圖像辨識文字、從 JPEG 提取文字，並將圖像轉換為文字。提供完整程式碼與技巧。
og_title: 如何在 C# 中使用 OCR – 從圖像辨識文字
tags:
- C#
- Aspose OCR
- Image Processing
title: 如何在 C# 中使用 OCR – 快速從圖像辨識文字
url: /zh-hant/net/text-recognition/how-to-use-ocr-in-c-recognize-text-from-image-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 快速辨識影像文字

有沒有想過 **如何在 .NET 專案中使用 OCR** 從圖片中提取文字？你並不孤單。許多開發者在需要 *辨識影像文字*（尤其是 JPEG）時會卡住，最後只能四處搜尋一段「神奇」的程式碼片段。

事實上，Aspose OCR 讓整個流程變得輕而易舉。在本教學中，我們會一步步說明如何 **將影像轉換為文字**、從 JPEG 中提取文字，還有——沒錯——在你的主控台上看到完整的輸出。沒有模糊的說明，只有完整可執行的範例。

## 你將學會

- 安裝 Aspose OCR NuGet 套件。
- 以 **online mode** 初始化 OCR 引擎，讓缺少的語言套件自動下載。
- 載入西里爾文語言模型（或任何你需要的語言）。
- 將 JPEG 影像提供給引擎，並 **recognize text from image**。
- 處理常見的問題，例如檔案遺失或不支援的格式。
- 查看完整程式碼，直接複製貼上到 Visual Studio 使用。

> **專業提示：** 若你在處理掃描的 PDF，能先將每頁轉成影像再送入同一個引擎——程式碼不需要任何變更。

## 前置條件

在開始之前，請確保你已具備以下條件：

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0+ (or .NET Framework 4.7.2+) | Aspose OCR 針對現代執行環境。 |
| Visual Studio 2022 (or any IDE you like) | 方便除錯與 IntelliSense。 |
| A JPEG image containing text (e.g., `cyrillic_sample.jpg`) | 我們會在示範中 **extract text from JPEG**。 |
| Internet connection (for the first run) | 引擎會在 **online mode** 下載語言套件。 |

即使缺少上述任一項目，教學仍能編譯通過，但 OCR 引擎在找不到語言模型時可能會拋出例外。

## 步驟 1 – 安裝 Aspose OCR NuGet 套件

首先需要取得此函式庫本身。開啟 **Package Manager Console** 並執行：

```powershell
Install-Package Aspose.OCR
```

或者，你也可以使用 UI，在 NuGet 套件管理員中搜尋 “Aspose.OCR” 並點選 **Install**。此操作會下載所有必需的 DLL，包括核心 OCR 引擎以及可按需取得的語言模型。

> **為什麼這一步很重要：** 若未安裝套件，`OcrEngine` 或 `LanguageModel` 等類別將不存在，程式碼無法編譯。

## 步驟 2 – 初始化 OCR 引擎（主要關鍵字）

現在函式庫已就緒，我們可以透過建立 `OcrEngine` 實例來 **how to use OCR**。使用 `ResourceMode.Online` 會讓 Aspose 自動下載缺少的語言套件，這對快速原型開發非常合適。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Initialize the OCR engine in online mode.
// This will download language packs if they aren’t already present.
OcrEngine ocrEngine = new OcrEngine(ResourceMode.Online);
```

> **底層發生了什麼？** 引擎會連線至 Aspose 的 CDN，檢查你所請求的語言模型，並將必要檔案下載至本機快取。之後的執行即為離線模式，提升處理速度。

## 步驟 3 – 載入所需的語言模型

若處理英文文字，預設即為 `LanguageModel.English`。在本範例中，我們會載入 **Cyrillic**，但你可以改成任何支援的語言。

```csharp
// Load the Cyrillic language model so the engine knows which characters to look for.
ocrEngine.LoadLanguage(LanguageModel.Cyrillic);
```

> **邊緣情況：** 若嘗試載入未支援的語言（例如 `LanguageModel.Klingon`），會拋出 `UnsupportedLanguageException`。若你的 UI 允許使用者即時選擇語言，請將呼叫包在 try‑catch 區塊中。

## 步驟 4 – 提供影像（次要關鍵字：extract text from jpeg）

此處我們將引擎指向包含欲讀取文字的 JPEG 檔案。`ImageStream.FromFile` 能接受 Aspose 可解碼的任何影像格式，但 JPEG 是相片與螢幕截圖最常見的格式。

```csharp
// Replace the path with the actual location of your JPEG image.
string imagePath = @"C:\Images\cyrillic_sample.jpg";

if (!File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Load the image into the OCR engine.
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **為什麼這很重要：** 提供不存在的路徑會拋出 `FileNotFoundException`。上述的防護條件可避免程式崩潰，並向使用者顯示清晰的訊息。

## 步驟 5 – 辨識影像文字並輸出

**how to use OCR** 的核心在於 `Recognize` 方法。它會回傳一個純文字字串，包含所有偵測到的字元，並盡可能保留換行。

```csharp
try
{
    // Perform the OCR operation.
    string recognizedText = ocrEngine.Recognize();

    // Output the extracted text to the console.
    Console.WriteLine("📝 Recognized Text:");
    Console.WriteLine(recognizedText);
}
catch (Exception ex)
{
    Console.WriteLine($"⚠️ OCR failed: {ex.Message}");
}
```

### 預期的主控台輸出

若 JPEG 包含「Привет мир」（俄文的 Hello world）這句話，輸出會類似於：

```
📝 Recognized Text:
Привет мир
```

若影像模糊，輸出可能會出現亂碼——這時前處理（例如提升對比）就能改善，我們稍後會提到。

## 步驟 6 – 完整可執行範例（結合所有步驟）

以下是完整程式碼，你可以直接複製到新的 **Console App** 專案中。它涵蓋從套件安裝到錯誤處理的所有步驟，讓你立刻執行。

```csharp
// ------------------------------------------------------------
// Complete OCR Example – How to use OCR in C#
// ------------------------------------------------------------
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine (online mode auto‑downloads language packs)
            OcrEngine ocrEngine = new OcrEngine(ResourceMode.Online);

            // 2️⃣ Load the language model you need (Cyrillic in this demo)
            try
            {
                ocrEngine.LoadLanguage(LanguageModel.Cyrillic);
            }
            catch (Exception langEx)
            {
                Console.WriteLine($"❌ Language load error: {langEx.Message}");
                return;
            }

            // 3️⃣ Provide the image – this is where we **extract text from jpeg**
            string imagePath = @"YOUR_DIRECTORY\cyrillic_sample.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Cannot find image at {imagePath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Recognize text – the heart of **how to use OCR**
            try
            {
                string recognizedText = ocrEngine.Recognize();

                // 5️⃣ Output – **convert image to text** and display it
                Console.WriteLine("📝 Recognized Text:");
                Console.WriteLine(recognizedText);
            }
            catch (Exception ocrEx)
            {
                Console.WriteLine($"⚠️ OCR operation failed: {ocrEx.Message}");
            }
        }
    }
}
```

> **快速測試：** 將 `YOUR_DIRECTORY\cyrillic_sample.jpg` 替換為實際的、包含清晰文字的 JPEG 路徑。執行專案 (F5) 後，即可在主控台看到抽取出的字串。

## 步驟 7 – 提示、邊緣情況與常見問題

### 如何 **recognize text from image** 非 JPEG 的檔案？

Aspose OCR 支援 PNG、BMP、TIFF，甚至是 PDF 頁面（先將其轉為影像）。只要在 `ImageStream.FromFile` 中更改檔案副檔名即可。程式碼不需額外設定，直接可用。

### 若影像解析度過低該怎麼辦？

OCR 的準確度在低於 300 dpi 時會急劇下降。你可以透過以下方式提升結果：

1. 使用類似 **ImageSharp** 的函式庫將影像放大。  
2. 套用二值化閾值以提升對比度。  
3. 設定 `ocrEngine.Settings.Deskew = true` 以校正傾斜文字。

```csharp
ocrEngine.Settings.Deskew = true; // Auto‑corrects rotated text
```

### 我可以批次 **convert image to text** 嗎？

當然可以。將辨識邏輯包在針對影像資料夾的 `foreach` 迴圈中。請記得重複使用同一個 `OcrEngine` 實例——它會快取語言套件，提升批次處理速度。

```csharp
string[] files = Directory.GetFiles(@"C:\Images", "*.jpg");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    string txt = ocrEngine.Recognize();
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), txt);
}
```

### 這在 Linux/macOS 上能運作嗎？

可以。只要安裝 .NET 執行環境，Aspose OCR 即為跨平台。唯一需要注意的是影像解碼的原生相依性，已隨 NuGet 套件一起打包。

### 如何 **extract text from jpeg** 同時保留版面配置？

將 `ocrEngine.Settings.PreserveFormatting = true` 設為 true。此設定會保留換行與簡易表格，使輸出更易閱讀。

```csharp
ocrEngine.Settings.PreserveFormatting = true;
```

## 結論

透過幾個步驟，我們示範了在 C# 中 **how to use OCR**，以 **recognize text from image**、**extract text from JPEG**，以及 **convert image to text**，全部使用 Aspose OCR。完整範例即開即用，能處理檔案遺失情況，並在主控台即時回饋結果。

從此你可以：

- 將 `LanguageModel.Cyrillic` 換成其他語言（English、Arabic、Chinese 等）。  
- 批次處理影像資料夾，以自動化資料輸入。  
- 結合 OCR 與自然語言處理，為掃描文件建立索引。

現在就試試看吧——執行程式碼、測試不同的影像品質，讓引擎幫你完成繁重的工作。若遇到問題，社群（以及 Aspose 的文件）隨時可供查詢。祝開發愉快！

![如何使用 OCR 範例截圖](placeholder-image.png "C# 中如何使用 OCR 範例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}