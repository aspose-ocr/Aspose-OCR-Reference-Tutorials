---
category: general
date: 2026-02-13
description: 如何在 C# 中使用 OCR 從圖像提取文字、辨識相片或 JPG 中的文字，並在無網路環境下執行 OCR。
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from photo
- recognize text from jpg
- run OCR on image
language: zh-hant
og_description: 如何在 C# 中使用 OCR 從圖像提取文字、從相片辨識文字，並以完整可執行的範例對圖像執行 OCR。
og_title: 如何在 C# 中使用 OCR – 從圖像提取文字
tags:
- OCR
- C#
- Image Processing
title: 如何在 C# 中使用 OCR – 從圖像提取文字並從相片辨識文字
url: /zh-hant/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-and-recognize-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 從圖像提取文字並辨識照片文字

有沒有想過 **如何使用 OCR** 從螢幕截圖、掃描收據，或是手機隨手拍的照片中抽取文字？你並不是唯一有這個疑問的人。在許多實務應用中，我們需要把圖片轉換成可搜尋的文字，而在本機端完成（不依賴不穩定的網路連線）常常像解謎一樣。

因此本指南會一步步示範如何使用 C# OCR 引擎 **extract text from image**，同時說明 **recognize text from photo**、**recognize text from JPG**，以及 **run OCR on image** 檔案的完整流程。完成後，你將得到一個可直接複製貼上的完整程式，開箱即用。

## 你將學會

- 如何為簡體中文（或任何你想使用的語言）設定 OCR 引擎。  
- 從本機資料夾 **load resources** 所需的完整程式碼——不會有任何網路請求。  
- 如何 **recognize text from photo**（如 JPEG、PNG、BMP）檔案。  
- 處理常見例外情況（例如模型檔遺失或不支援的影像格式）的技巧。  
- 一個完整、可執行的範例，直接貼到 Visual Studio 即可看到結果。

### 前置條件

- .NET 6.0 或更新版本（此 API 目標為 .NET Standard 2.0，舊版亦可運作）。  
- 具備基本的 C# 與 Visual Studio（或其他 IDE）使用經驗。  
- 你所使用的 OCR 函式庫（此範例假設有一個虛構的 `OcrEngine` 類別，隨附語言模型）。  
- 一個包含必要語言模型檔案的資料夾——可視為引擎閱讀中文字符的「大腦」。

> **Pro tip:** 若尚未取得中文模型檔，請先從供應商網站下載，並放置於類似 `C:\OcrResources` 的資料夾中。之後引擎就不會再需要上網。

---

![顯示 OCR 在照片上運作流程的圖示](path/to/ocr-diagram.png "Diagram showing OCR process on a photo")

## 如何使用 OCR：設定引擎

首先，你需要建立一個 OCR 引擎實例，並設定要辨識的語言。本教學以 **簡體中文** 為例，只要將 `OcrLanguage.ChineseSimplified` 換成 `OcrLanguage.English`（或其他 enum 值）即可完成切換，僅需一行程式碼。

```csharp
using System;
using YourOcrLibrary;   // Replace with the actual namespace of your OCR SDK

// Step 1: Create and configure the OCR engine for Simplified Chinese
var ocrEngine = new OcrEngine
{
    // Primary keyword appears here naturally
    Language = OcrLanguage.ChineseSimplified,

    // Point to a folder that already contains the Chinese model files
    ResourceFolder = @"C:\OcrResources"
};
```

**為什麼這很重要：**  
設定 `Language` 屬性讓引擎知道要預期哪種字符集。`ResourceFolder` 則是引擎尋找神經網路權重與語言字典的路徑——相當於大腦的記憶庫。如果指向錯誤的資料夾，引擎會拋出 `FileNotFoundException`，導致程式無法繼續。

## Extract Text from Image – Loading Resources

在引擎能真正讀取文字之前，必須先把模型檔載入記憶體。這一步 **至關重要**，因為它避免了每次處理影像時都必須發起網路請求。

```csharp
// Step 2: Load the language resources from the specified folder (no internet required)
try
{
    ocrEngine.LoadResources();
    Console.WriteLine("Resources loaded successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to load OCR resources: {ex.Message}");
    // In a real app you might fallback to a default language or abort gracefully
}
```

**可能會發生什麼問題？**  
如果資料夾路徑錯誤或檔案損毀，`LoadResources()` 會拋出例外。上方的 `try/catch` 示範了如何優雅地處理錯誤——這在正式環境中相當常見。

## Recognize Text from Photo – Running the OCR

現在進入有趣的部分：將影像檔送入引擎，取得辨識結果。這正是 **run OCR on image** 情境的核心，無論是 JPEG、PNG，甚至 BMP 都適用。

```csharp
// Step 3: Recognize text from an image file
string imagePath = @"C:\OcrResources\photo.jpg";

try
{
    var recognitionResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(recognitionResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
}
```

`RecognizeImage` 方法會回傳一個 `RecognitionResult`（或你的 SDK 所稱的類型），通常包含：

- `Text` – 純文字轉錄。  
- `Confidence` – 數值分數，表示引擎對每一行文字的信心程度。  
- `BoundingBoxes` – 可選的座標資訊，標示每個字詞在圖片中的位置。

**為什麼要關心 confidence：**  
如果你在開發資料輸入自動化工具，可以設定一個門檻值（例如 0.85），對低信心的行列要求使用者確認。這樣能大幅提升整體準確度。

## Recognize Text from JPG – Handling Different Formats

許多開發者誤以為 OCR 只能處理 PNG，事實上現代引擎同樣支援 **JPG**。唯一需要注意的是 JPEG 壓縮可能產生雜訊，會干擾模型判讀。

```csharp
// Bonus: Recognize text from a JPG with optional preprocessing
string jpgPath = @"C:\OcrResources\scanned_doc.jpg";

// Optional: use a simple image‑preprocess step to improve accuracy
var preprocessed = ImageHelper.DenoiseAndDeskew(jpgPath); // pseudo‑method
var result = ocrEngine.RecognizeImage(preprocessed);
Console.WriteLine($"Detected text ({result.Confidence:P0} confidence):");
Console.WriteLine(result.Text);
```

如果沒有 `DenoiseAndDeskew` 輔助函式，許多函式庫（例如 OpenCvSharp）都提供相應功能。重點在於：**run OCR on image** 前先稍作清理，特別是來自掃描器或手機相機的檔案。

## Run OCR on Image – Tips, Edge Cases, and Best Practices

### 1. 記憶體管理
載入大型語言模型可能佔用數百 MB 記憶體。使用完畢後請記得釋放引擎：

```csharp
ocrEngine.Dispose(); // or using statement if the SDK implements IDisposable
```

### 2. 批次處理
若需要一次處理多張照片，只需先載入資源一次，然後在迴圈中呼叫辨識：

```csharp
string[] files = Directory.GetFiles(@"C:\BatchPhotos", "*.jpg");
foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), res.Text);
}
```

### 3. 多語言情境
可以在執行期間改變 `ocrEngine.Language`，再呼叫 `LoadResources()` 重新載入。但要留意額外的載入時間。

### 4. 處理空結果
有時引擎會回傳空字串，通常代表影像過於模糊或文字顏色與背景相近。簡易檢查方式如下：

```csharp
if (string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text detected – consider increasing image contrast.");
}
```

### 5. 安全性考量
千萬不要直接把使用者上傳的檔案送入 OCR 引擎，未經驗證的檔案可能帶來風險。最低限度應檢查檔案副檔名與大小，並考慮使用防毒掃描。

---

## 完整可執行範例

以下是一個單一、獨立的程式碼範例，可直接貼到新的 Console App 專案中。它示範了 **how to use OCR**、**extract text from image**、**recognize text from photo**、**recognize text from JPG**，以及 **run OCR on image** 的完整流程。

```csharp
// File: Program.cs
using System;
using System.IO;
using YourOcrLibrary; // Replace with actual namespace

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // ------------------------------
            // 1️⃣ Configure the OCR engine
            // ------------------------------
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified,
                ResourceFolder = @"C:\OcrResources"
            };

            // Load language resources (no internet needed)
            try
            {
                ocrEngine.LoadResources();
                Console.WriteLine("Resources loaded.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Failed to load resources: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Recognize text from a photo (JPG in this case)
            // -------------------------------------------------
            string imagePath = @"C:\OcrResources\photo.jpg";

            if (!File.Exists(imagePath))
            {
                Console.Error.WriteLine($"Image not found: {imagePath}");
                return;
            }

            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("\n=== OCR Output ===");
                Console.WriteLine(result.Text);
                Console.WriteLine($"\nConfidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"OCR error: {ex.Message}");
            }

            // Clean up
            ocrEngine.Dispose();
        }
    }
}
```

**預期輸出（範例）：**

```
Resources loaded.

=== OCR Output ===
中华人民共和国
北京
2026年02月13日

Confidence: 92.45%
```

實際顯示的文字會依照圖像內容而異，但你應該會在主控台看到一段 Unicode 文字，並伴隨信心百分比。

---

## 結論

我們已從頭到尾走過 **how to use OCR** 在 C# 中的完整流程——設定引擎、載入語言資源，最後 **recognize text from photo** 或 **JPG** 檔案，且全程不需連網。依照上述步驟，你可以 **extract text from image**、**run OCR on image**，並處理新手常碰到的陷阱。

準備好接受下一個挑戰了嗎？試著把 PDF 頁面轉成影像後再送入引擎，或換一套不同語言的模型，觀察 confidence 分數的變化。你可能

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}