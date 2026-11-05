---
category: general
date: 2026-02-16
description: 使用 Aspose OCR 在 C# 中快速對 PNG 進行 OCR。了解如何擷取文字、讀取文字 PNG 以及辨識文字 PNG，並提供一步一步的教學。
draft: false
keywords:
- run OCR on PNG
- how to extract text
- read text png
- recognize text png
- ocr tutorial c#
language: zh-hant
og_description: 在 C# 中使用 Aspose OCR 進行 PNG 圖片的 OCR。本教學將一步步示範如何擷取文字、讀取 PNG 文字以及辨識 PNG
  文字。
og_title: 在 C# 中對 PNG 執行 OCR – 完整指南
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 在 C# 中對 PNG 進行 OCR – Aspose 完整指南
url: /zh-hant/net/text-recognition/run-ocr-on-png-in-c-complete-guide-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中對 PNG 執行 OCR – 使用 Aspose 的完整指南

是否曾經需要 **在 PNG 上執行 OCR** 卻不知從何下手？你並不孤單——開發者常常詢問 *如何擷取文字*，無論是高解析度的螢幕截圖、收據或掃描圖表。本教學將一步步示範一個實用的端對端解決方案，讓你使用 Aspose.OCR 函式庫在純 C# 中 **在 PNG 上執行 OCR**。

我們會涵蓋從安裝 NuGet 套件、啟用 GPU 加速、載入英文語言模型，到最終將辨識結果印出至主控台的全部流程。完成後，你將清楚知道 **如何擷取文字**、如何 **有效讀取 PNG 文字**，並擁有一段可直接套用於任何專案的 **OCR 教學 C#** 程式碼片段。

## 你將學會

- 安裝與設定 Aspose.OCR for .NET。
- 啟用硬體加速以提升處理速度。
- 載入語言模型並將 PNG 圖片送入引擎。
- 取得並顯示輸出，處理常見的陷阱。
- 將範例延伸至其他語言或影像格式。

**先備條件：** .NET 6 或更新版本、Visual Studio 2022（或你慣用的 IDE），以及若想使用可選的加速功能，需具備相容的 GPU。無需事先具備 OCR 經驗。

---

## 在 PNG 上執行 OCR – 環境設定

在開始撰寫程式碼之前，先確保開發環境已就緒。這一步相當關鍵；缺少套件或執行時版本不符會導致整個教學無法進行。

1. **建立新的主控台專案**  
   ```bash
   dotnet new console -n OcrPngDemo
   cd OcrPngDemo
   ```

2. **加入 Aspose.OCR NuGet 套件**  
   ```bash
   dotnet add package Aspose.OCR
   ```

3. **（可選）驗證 GPU 支援** – 若你的電腦配備支援 CUDA/OpenCL 的 NVIDIA 或 AMD GPU，請安裝相應的驅動程式。設定 `HardwareAcceleration.Gpu` 時，函式庫會自動偵測硬體。

就這樣。現在已有一個全新專案，並加入了 OCR 函式庫，隨時可以 **在 PNG 上執行 OCR**。

## 如何擷取文字 – 初始化 OCR 引擎

第一行正式程式碼會建立一個 `OcrEngine` 實例。把這個引擎想像成整個作業的“大腦”；它負責保存設定、語言模型與硬體選項。

```csharp
using Aspose.OCR;

// Step 1: Initialize the OCR engine (default CPU mode)
OcrEngine ocrEngine = new OcrEngine();
```

為什麼要手動實例化而不是使用靜態輔助方法？  
因為這樣可以完整掌控 **如何擷取文字**——你可以即時切換 GPU、變更語言，或在執行時更換圖像來源。在較大型的應用程式中，通常會將引擎設為 singleton，以避免重複載入模型。

## 使用 GPU 加速讀取 PNG 文字

如果你處理的是高解析度的螢幕截圖，僅使用 CPU 的 OCR 會感覺相當緩慢。啟用 GPU 加速可為每次執行節省數秒時間。

```csharp
// Step 2: Enable GPU acceleration for faster processing (requires compatible GPU)
ocrEngine.HardwareAcceleration = HardwareAcceleration.Gpu;
```

*小技巧：* 若機器沒有相容的 GPU，上述程式碼會自動回退至 CPU 模式，且不會拋出例外，讓你在不同環境下的程式碼保持不變。

## 載入語言模型 – 「English」範例

Aspose 內建英文模型，若需其他語言（法文、德文等）只要一次呼叫即可載入。載入模型是 **辨識 PNG 文字** 的前置條件，否則引擎不會知道要使用哪套字元集。

```csharp
// Step 3: Load the language model you need (English is included by default)
ocrEngine.LoadLanguage(LanguageModel.English);
```

若日後需要 **在其他語言的 PNG 中讀取文字**，只要把 `LanguageModel.English` 換成相對應的列舉值即可。

## 提供圖像 – 從檔案到串流

接下來把 PNG 檔案交給引擎。`ImageStream.FromFile` 輔助方法會將檔案讀入記憶體，支援多種格式，但我們的重點是 PNG。

```csharp
// Step 4: Provide the image to be processed
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/high_res_image.png");
```

務必確認路徑指向真實的 PNG，否則會拋出 `FileNotFoundException`。測試時，只要把一張列印發票的螢幕截圖放到資料夾內，並在此處引用即可。

## 辨識 PNG 文字 – 執行 OCR 操作

所有設定完成後，真正的 OCR 呼叫只需要一個方法。此方法會回傳一個字串，內含所有擷取出的字元，並盡可能保留換行。

```csharp
// Step 5: Run the OCR operation and capture the recognized text
string recognizedText = ocrEngine.Recognize();
```

為什麼只要這一行就能工作？  
在背後，引擎會依序執行前處理（去噪、二值化）、分割（切割成行與字元），最後使用深度學習模型進行分類。所有繁重的步驟都已被封裝，讓 API 看起來相當輕量。

## 顯示結果 – 驗證輸出

最後，我們把結果印到主控台。實務上，你可能會寫入資料庫、送入搜尋索引，或傳給其他服務。

```csharp
// Step 6: Display the OCR result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

執行程式後，你應該會看到類似以下的輸出：

```
=== OCR Result ===
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
Thank you for your business!
```

若輸出呈現亂碼，請再次檢查圖像品質（對比、方向），並考慮啟用 `ocrEngine.PreprocessOptions` 進行額外調整。

## 完整 OCR 教學 C# – 可執行範例

以下是 **完整、可執行** 的程式碼，將所有步驟整合在一起。直接貼到 `Program.cs`，替換圖像路徑後按 **F5** 即可執行。

```csharp
using System;
using Aspose.OCR;

namespace OcrPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize the OCR engine (CPU by default)
            OcrEngine ocrEngine = new OcrEngine();

            // Enable GPU acceleration if a compatible GPU is present
            ocrEngine.HardwareAcceleration = HardwareAcceleration.Gpu;

            // Load the English language model (default)
            ocrEngine.LoadLanguage(LanguageModel.English);

            // Specify the PNG image to process
            string imagePath = "YOUR_DIRECTORY/high_res_image.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR and retrieve the recognized text
            string recognizedText = ocrEngine.Recognize();

            // Output the result to the console
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

**預期輸出：** 主控台會列印出 PNG 中找到的全部字元，並保留換行。若圖像僅包含數字，則會看到一串數字；若混合多語言，則會得到相應的 Unicode 字元。

> **注意：** 上述程式可處理任何 PNG、JPEG 或 BMP，只要檔案路徑正確。若要 **從串流讀取 PNG 文字**（例如來自 Web API），請將 `ImageStream.FromFile` 改為 `ImageStream.FromBytes(byteArray)`。

---

## 常見問題與邊緣案例

### 我的 PNG 旋轉了怎麼辦？

Aspose.OCR 能自動旋轉圖像。加入以下程式碼：

```csharp
ocrEngine.Image = ImageStream.FromFile(imagePath);
ocrEngine.ImageOrientation = ImageOrientation.AutoDetect;
```

### 如何處理大量批次？

將引擎放在 `using` 區塊中，並在多個檔案間重複使用：

```csharp
using (var engine = new OcrEngine())
{
    engine.LoadLanguage(LanguageModel.English);
    foreach (var file in Directory.GetFiles(folder, "*.png"))
    {
        engine.Image = ImageStream.FromFile(file);
        string text = engine.Recognize();
        // Process text...
    }
}
```

### 能從低對比度的圖像擷取文字嗎？

啟用前處理：

```csharp
ocrEngine.PreprocessOptions = PreprocessOptions.EnhanceContrast | PreprocessOptions.Denoise;
```

### 有辦法取得信心分數嗎？

有的——`ocrEngine.RecognizeWithDetails()` 會回傳 `OcrResult` 集合，每個物件都包含 `Confidence` 屬性。

---

## 視覺範例

<img src="https://example.com/ocr-output.png" alt="Run OCR on PNG example output showing extracted invoice text">

*Alt 文字已包含主要關鍵字，以符合 SEO 需求。*

---

## 結論

現在你已掌握一套 **在 PNG 上執行 OCR** 的完整工作流程，使用 Aspose.OCR 即可開箱即用。透過本 **OCR 教學 C#**，你能 **如何擷取文字**、**讀取 PNG 文字**，以及 **辨識 PNG 文字**，只需幾行程式碼。引擎的 GPU 支援、語言載入與簡潔 API，使其成為任何 .NET 開發者將影像轉換為可搜尋文字的首選方案。

接下來可以嘗試將 `LanguageModel.English` 換成其他語言、使用 `PreprocessOptions` 處理噪點掃描，或將結果整合至全文搜尋索引。可能性無限，而你剛寫好的程式碼則是所有後續冒險的可重用基礎。

若遇到任何問題，歡迎在下方留言或參考 Aspose 官方文件取得更深入的設定說明。祝開發順利，玩得開心，讓那些頑固的 PNG 變成可編輯的文字吧！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}