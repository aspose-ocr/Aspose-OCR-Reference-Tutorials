---
category: general
date: 2026-03-13
description: 使用 Aspose OCR 於 C# 從圖像提取文字。了解如何載入圖像進行 OCR、執行圖像 OCR，並以清晰的逐步程式碼提取西里爾文字。
draft: false
keywords:
- extract text from image
- load image for ocr
- run ocr on image
- extract cyrillic text
- recognize cyrillic text
language: zh-hant
og_description: 使用 Aspose OCR 在 C# 中從圖像提取文字。本教學示範如何載入圖像進行 OCR、執行 OCR，並有效提取西里爾文字。
og_title: 使用 Aspose OCR 從圖像擷取文字 – C# 指南
tags:
- Aspose OCR
- C#
- Image Processing
title: 使用 Aspose OCR 從圖像提取文字 – C# 程式設計指南
url: /zh-hant/net/text-recognition/extract-text-from-image-with-aspose-ocr-c-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 從圖像提取文字 – C# 程式設計指南

是否曾需要**從圖像提取文字**，卻不確定哪個函式庫能順利處理西里爾字元？你並不孤單。在許多專案中——發票掃描、護照驗證或快速筆記——從圖片中取得可靠的文字是必須的。  

在本指南中，我們將逐步說明**載入圖像以供 OCR**、設定 Aspose OCR、**在圖像上執行 OCR**，最後只需幾行 C# 程式碼即可**提取西里爾文字**。完成後，你將擁有一段可直接執行的程式碼片段，會將辨識出的文字印到主控台。

## 您將學習

- 如何安裝與引用 Aspose OCR NuGet 套件。  
- 正確指向語言套件資源的方法。  
- 為何選擇 `Language.Cyrillic` 對非拉丁文字至關重要。  
- 常見陷阱（缺少資源、不支援的圖像格式）以及如何避免。  
- 一個完整、可執行的範例，能直接放入任何 .NET 專案。

不需要先前的 OCR 經驗，但若具備 C# 與 Visual Studio 的基本認識，學習過程會更順暢。

## 前置條件

在開始之前，請確保你已具備以下條件：

1. 已安裝 **.NET 6.0** 或更新版本（此程式碼可在 .NET Core 與 .NET Framework 上執行）。  
2. 已安裝 **Visual Studio 2022**（或任何支援 C# 的編輯器）。  
3. 已取得 **Aspose.OCR** NuGet 套件。可於套件管理員主控台執行以下指令安裝：  

   ```powershell
   Install-Package Aspose.OCR
   ```

4. 一個包含 OCR 語言套件的資料夾（可從 Aspose 官方網站下載）。  
5. 一張圖像檔（範例中為 `cyrillic.png`），內含你想要讀取的西里爾文字。

> **專業小技巧：** 將語言套件資料夾放在專案的 `bin` 目錄旁，可簡化路徑處理。

## 第一步 – 載入圖像以供 OCR

首先必須提供給引擎一個位圖。Aspose OCR 接受 `ImageStream`，可直接從檔案路徑建立。

```csharp
using Aspose.OCR;

// Step 1: Load the image you want to process
string imagePath = @"YOUR_DIRECTORY\cyrillic.png";
ImageStream image = ImageStream.FromFile(imagePath);
```

*為何這很重要：* 先載入圖像可讓你確認檔案是否存在且格式受支援（PNG、JPEG、BMP 等）。若檔案遺失，`FromFile` 會拋出明確例外，避免之後出現難以追蹤的 OCR 錯誤。

## 第二步 – 設定 OCR 引擎與資源

接著，實例化 OCR 引擎並指向存放語言套件的資料夾。若未提供正確資源，引擎將無法辨識西里爾字形。

```csharp
// Step 2: Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Tell Aspose where the language resources live
string resourcesPath = @"YOUR_DIRECTORY\OcrResources";
ocrEngine.SetResourcesPath(resourcesPath);
```

*為何這很重要：* `SetResourcesPath` 方法是程式碼與各語言字形資料檔之間的橋樑。忘記此步驟通常會導致輸出亂碼或拋出 `ResourceNotFoundException`。

## 第三步 – 選擇語言並**在圖像上執行 OCR**

現在設定預期的語言。因本範例處理西里爾文字，我們使用 `Language.Cyrillic`。若需同時辨識多種文字，可使用位元 OR（`|`）運算子結合。

```csharp
// Step 3: Select the language you want to recognize
ocrEngine.Language = Language.Cyrillic;

// Assign the previously loaded image to the engine
ocrEngine.Image = image;

// Finally, perform the recognition
ocrEngine.Recognize();
```

*為何這很重要：* 指定語言會縮小 OCR 演算法的搜尋空間，顯著提升速度與準確度。使用正確的語言旗標**在圖像上執行 OCR**，即可減少錯誤辨識的情況。

## 第四步 – 取得並使用提取出的西里爾文字

辨識完成後，結果會存於 `Text` 屬性。你現在可以將其顯示、寫入檔案，或傳遞給其他系統。

```csharp
// Step 4: Output the recognized text
string recognizedText = ocrEngine.Text;
Console.WriteLine("=== Extracted Cyrillic Text ===");
Console.WriteLine(recognizedText);
```

典型的主控台輸出如下：

```
=== Extracted Cyrillic Text ===
Привет, мир! Это тестовое изображение.
```

若輸出出現非預期符號，請再次確認語言套件與你安裝的 Aspose OCR 版本相符。

## 完整可執行範例 – 結合所有步驟

以下程式碼可直接貼到新的主控台專案中。將 `YOUR_DIRECTORY` 替換為你機器上的實際路徑。

```csharp
using System;
using Aspose.OCR;

namespace ExtractCyrillicDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the image you want to process
            string imagePath = @"YOUR_DIRECTORY\cyrillic.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // 2️⃣ Initialize OCR engine and point to language resources
            OcrEngine ocrEngine = new OcrEngine();
            string resourcesPath = @"YOUR_DIRECTORY\OcrResources";
            ocrEngine.SetResourcesPath(resourcesPath);

            // 3️⃣ Choose Cyrillic language and run OCR on image
            ocrEngine.Language = Language.Cyrillic;
            ocrEngine.Image = image;
            ocrEngine.Recognize();

            // 4️⃣ Extract and display the text
            string result = ocrEngine.Text;
            Console.WriteLine("=== Extracted Cyrillic Text ===");
            Console.WriteLine(result);
        }
    }
}
```

### 預期結果

執行程式後，應在主控台印出 `cyrillic.png` 中的完整文字。若圖像內的句子為「Привет, мир!」，則會看到相同的行出現在主控台，且不會有額外符號。

## 邊緣情況與故障排除

| 情況 | 檢查項目 | 建議修正 |
|-----------|---------------|---------------|
| **缺少語言套件** | `resourcesPath` 是否指向包含 `.dat` 檔案的資料夾？ | 重新從 Aspose 下載套件，並放置於指定資料夾。 |
| **不支援的圖像格式** | 檔案是否為 PNG、JPEG、BMP 或 TIFF？ | 在呼叫 `FromFile` 前，先將圖像轉換為支援的格式。 |
| **輸出出現雜訊字元** | 是否正確設定 `ocrEngine.Language`？ | 使用 `Language.Cyrillic`（或以位元 OR 結合多語言旗標）。 |
| **大型圖像導致效能下降** | 圖像解析度是否大於 3000 px？ | 在 OCR 前將圖像縮小至合理尺寸（例如寬度 1024 px）。 |

## 相關主題你可能想進一步探索

- 在 PDF 中使用 Aspose PDF + OCR **提取圖像文字**。  
- 從 `Stream` **載入圖像以供 OCR**（適用於圖像來自 Web API 的情況）。  
- 使用平行方式 **在圖像上執行 OCR** 以加速批次處理。  
- 使用 Aspose OCR 手寫模式 **提取西里爾文字** 於手寫筆記。  
- 將結果整合至資料庫，**辨識西里爾文字** 以供搜尋索引。

## 結論

我們剛剛示範了如何使用 Aspose OCR **從圖像提取文字**，涵蓋從載入圖像到印出辨識出的西里爾字元的全部步驟。這段簡短、獨立的程式展示了最小化的程式碼需求，而故障排除表則協助你避免最常見的問題。  

試著在自己的截圖上執行，或將語言套件換成阿拉伯語或中文，看看相同的模式如何在全球範圍內運作。祝編程愉快，願你的 OCR 結果永遠清晰可辨！ 

![從圖像提取文字範例](extract-text-from-image.png "從圖像提取文字範例")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}