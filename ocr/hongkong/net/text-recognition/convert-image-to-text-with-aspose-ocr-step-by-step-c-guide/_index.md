---
category: general
date: 2026-02-22
description: 使用 Aspose OCR 於 C# 將圖像轉換為文字。了解如何註冊語言模組、載入圖像進行 OCR，並從圖像中擷取文字，支援西里爾字母。
draft: false
keywords:
- convert image to text
- extract text from image
- how to register module
- load image for ocr
- how to recognize cyrillic
language: zh-hant
og_description: 即時將圖像轉換為文字。本指南說明如何註冊模組、載入圖像進行 OCR，並從圖像中提取文字，包括西里爾文字辨識。
og_title: 使用 Aspose OCR 將圖像轉換為文字 – 完整 C# 教程
tags:
- Aspose OCR
- C#
- Image Processing
title: 使用 Aspose OCR 將圖像轉換為文字 – C# 逐步指南
url: /zh-hant/net/text-recognition/convert-image-to-text-with-aspose-ocr-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 將圖像轉換為文字 – 步驟教學 C# 指南

曾經需要 **將圖像轉換為文字**，卻不知從何入手嗎？你並不孤單——許多開發者在圖片包含非拉丁字符（例如西里爾字母）時會卡住。在本教學中，我們將逐步演示一個完整、可直接執行的解決方案，說明如何註冊語言模組、載入 OCR 圖像，最後使用 Aspose OCR for .NET 從圖像中提取文字。

我們將涵蓋從安裝 NuGet 套件到處理缺少語言檔案等邊緣案例的所有內容。完成本指南後，你將能夠僅用幾行 C# **將圖像轉換為文字**，並且了解每一步的 *原因*。

## 你將學到什麼

- 如何 **註冊西里爾語言模組** 以讓 OCR 引擎能理解此文字腳本。  
- 使用 Aspose 的 `Image.Load` 方法正確 **載入 OCR 圖像** 的方式。  
- 如何將引擎設定為 **辨識西里爾字母**，然後 **從圖像中提取文字**。  
- 針對常見問題（如 zip 模組損壞或不支援的圖像格式）提供故障排除技巧。  

### 前置條件

- .NET 6.0 或更新版本（此程式碼亦可在 .NET Framework 4.7+ 上執行）。  
- Visual Studio 2022（或任何支援 C# 的 IDE）。  
- Aspose.OCR NuGet 套件（`Install-Package Aspose.OCR`）。  
- 一個西里爾語言 zip 檔案（`cyrillic.zip`）以及範例圖像（`cyrillic_sample.jpg`）。  

> **專業提示：** 將語言模組放在專用資料夾中（例如 `./ocr-modules/`），以避免與路徑相關的錯誤。

---

## 步驟 1：如何註冊模組 – 新增西里爾語支援

在 OCR 引擎能讀取西里爾字符之前，你必須告訴它語言資料所在的位置。這就是 **如何註冊模組** 的步驟。

```csharp
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

// Path to the Cyrillic language module (ZIP file)
string languageModulePath = Path.Combine("ocr-modules", "cyrillic.zip");

// Read the ZIP file into a byte array
byte[] moduleBytes = File.ReadAllBytes(languageModulePath);

// Register the module with the OCR engine
OcrEngine.RegisterLanguageModule(Language.Cyrillic, moduleBytes);
```

**為何需要註冊？**  
Aspose OCR 內建一組預設的拉丁語系，以保持函式庫輕量。透過註冊西里爾模組，你可以擴充引擎的字典，使其能正確將字形映射至 Unicode 字元。若跳過此步驟，引擎將回退至猜測模式，導致輸出文字雜亂。

> **常見錯誤：** 使用指向錯誤目錄的相對路徑。呼叫 `RegisterLanguageModule` 前，務必使用 `Path.Combine` 建構路徑或以 `File.Exists` 驗證其是否存在。

---

## 步驟 2：載入 OCR 圖像 – 準備輸入

現在語言已就緒，我們需要將圖片載入記憶體。這就是 **載入 OCR 圖像** 的步驟。

```csharp
using Aspose.OCR;

// Ensure the image exists
string imagePath = Path.Combine("ocr-images", "cyrillic_sample.jpg");
if (!File.Exists(imagePath))
{
    Console.WriteLine($"Image not found: {imagePath}");
    return;
}

// Load the image – Aspose automatically detects format (JPEG, PNG, BMP, etc.)
Image inputImage = Image.Load(imagePath);
```

**為何要這樣載入？**  
`Image.Load` 抽象化了格式偵測與色彩空間轉換，無論來源檔案類型為何，都能提供一致的 `Image` 物件。這降低了新手開發者常遇到的 *Unsupported format* 錯誤機率。

> **提示：** 若需對圖像進行前處理（例如去斜或二值化），請在呼叫 `Recognize` 之前完成。Aspose 提供 `ImageProcessor` 工具可協助完成此作業。

---

## 步驟 3：設定語言並將圖像轉換為文字

在模組已註冊且圖片已載入後，我們終於可以 **將圖像轉換為文字**。此步驟同時說明 **如何辨識西里爾字母**。

```csharp
// Create an OCR engine instance and set its language to Cyrillic
var ocrEngine = new OcrEngine
{
    Language = Language.Cyrillic,
    // Optional: increase accuracy for noisy images
    // Settings = new OcrEngineSettings { EnableNoiseRemoval = true }
};

// Run the recognition process
OcrResult ocrResult = ocrEngine.Recognize(inputImage);
```

**為何要明確設定語言？**  
即使已註冊模組，引擎仍預設使用英文。指定 `Language.Cyrillic` 可讓引擎使用新註冊的字典，顯著提升對斯拉夫文字的辨識準確度。

> **邊緣情況：** 若在未設定語言的情況下嘗試辨識圖像，Aspose 會回退至拉丁語，導致西里爾文字顯示為不可讀的字元。

---

## 步驟 4：從圖像提取文字 – 取得結果

`OcrResult` 物件包含原始字串、信心分數與位置資料。對於大多數情況，你只需要純文字即可。

```csharp
// Display the recognized text in the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);

// Optional: check confidence (0‑100)
// Console.WriteLine($"Confidence: {ocrResult.Confidence}%");
```

**為何要檢查信心分數？**  
信心分數告訴你 OCR 結果的可靠程度。超過 80% 的分數通常可安全用於後續處理，而較低的分數可能需要人工審核或圖像前處理。

> **如果輸出為空該怎麼辦？**  
常見原因包括語言模組不正確、圖像損壞，或圖像對比度過低。可嘗試提升對比度或在辨識前使用 `ImageProcessor.AdjustContrast`。

---

## 完整範例程式

以下是完整、可直接複製貼上的程式，將所有步驟串接起來。將其儲存為 `Program.cs`，並從專案根目錄執行。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Register the Cyrillic language module
        // -------------------------------------------------
        string languageModulePath = Path.Combine("ocr-modules", "cyrillic.zip");
        if (!File.Exists(languageModulePath))
        {
            Console.WriteLine($"Language module not found: {languageModulePath}");
            return;
        }
        OcrEngine.RegisterLanguageModule(Language.Cyrillic, File.ReadAllBytes(languageModulePath));

        // -------------------------------------------------
        // Step 2: Load the image you want to convert
        // -------------------------------------------------
        string imagePath = Path.Combine("ocr-images", "cyrillic_sample.jpg");
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }
        Image inputImage = Image.Load(imagePath);

        // -------------------------------------------------
        // Step 3: Create OCR engine and set language
        // -------------------------------------------------
        var ocrEngine = new OcrEngine { Language = Language.Cyrillic };

        // -------------------------------------------------
        // Step 4: Recognize and extract text
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 5: Output the result
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**預期輸出**

```
=== OCR Result ===
Привет мир! Это пример текста на кириллице.
```

如果看到的不是西里爾文字而是亂碼，請再次確認 `cyrillic.zip` 檔案與你安裝的 Aspose OCR 版本相符，且圖像足夠清晰以供辨識。

## 常見問題 (FAQ)

**Q: 我可以將此方法用於其他語言嗎？**  
A: 當然可以。將 `Language.Cyrillic` 替換為相應的列舉（例如 `Language.Arabic`），並註冊對應的 ZIP 檔案。

**Q: 支援哪些圖像格式？**  
A: JPEG、PNG、BMP、TIFF 與 GIF 均由 `Image.Load` 原生支援。若處理 PDF，需使用 Aspose.PDF，先將頁面轉為圖像再進行 OCR。

**Q: 如何提升低品質掃描的辨識準確度？**  
A: 前處理圖像——使用 `ImageProcessor` 進行二值化、去斜或除噪。亦可提升 `OcrEngineSettings` 中的 `EnableNoiseRemoval` 與 `EnableTextSegmentation` 等設定。

**Q: 有辦法取得每個單字的邊界框嗎？**  
A: 有。`OcrResult` 包含 `Regions` 集合，每個區域都保存 `Location` 資料。遍歷 `ocrResult.Regions` 即可取得座標。

## 結論

我們已示範如何使用 Aspose OCR **將圖像轉換為文字**，涵蓋從 **如何註冊模組**、**載入 OCR 圖像** 到最終 **從圖像提取文字**，同時 **辨識西里爾字符**。上方的完整程式碼已可直接執行，說明則提供每行程式背後的 *原因*，讓你能將此解決方案套用至其他語言或更複雜的工作流程。

準備好下一步了嗎？可嘗試多頁 PDF 轉換、將 OCR 輸出整合至搜尋索引，或與 Azure Cognitive Services 結合進行語言偵測。掌握圖像轉文字的基礎後，想像空間無限。

![將圖像轉換為文字範例](image-placeholder.png "將圖像轉換為文字")

*祝編程愉快！如果遇到任何問題，請在下方留言，我們會一起排除故障。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}