---
category: general
date: 2026-01-07
description: 提升 C# 中使用 Aspose OCR 的辨識準確度。學習如何從 PNG 讀取文字、從圖像提取文字，並有效載入圖像以執行 OCR。
draft: false
keywords:
- improve OCR accuracy
- read text from PNG
- extract text from image
- load image for OCR
- recognize text from stream
language: zh-hant
og_description: 使用 Aspose OCR 在 C# 中提升 OCR 準確度。本指南展示如何從 PNG 讀取文字、從圖像提取文字，以及從串流辨識文字。
og_title: 在 C# 中提升 OCR 準確度 – 完整 Aspose OCR 教程
tags:
- C#
- Aspose
- OCR
- Image Processing
title: 使用 Aspose 提升 C# OCR 準確度 – 步驟指南
url: /zh-hant/net/ocr-optimization/improve-ocr-accuracy-in-c-with-aspose-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中使用 Aspose 提升 OCR 準確度 – 步驟指南

有沒有想過在從掃描文件中提取文字時，如何**提升 OCR 準確度**？你並非唯一面臨此問題的人。在許多實際專案中，OCR 引擎會因雜訊、頁面傾斜或非拉丁字母而感到困惑，最終的結果往往看起來像是亂碼而非有用的資料。

好消息是，只要調整少數設定，就能把這些混亂轉變為乾淨、可搜尋的文字。在本教學中，我們將逐步示範一個完整且可執行的範例，使用 Aspose.OCR for .NET **read text from PNG**、**extract text from image** 以及 **load image for OCR**。完成後，你將擁有穩固的基礎，確保每次都能得到可靠的結果。

## 你將學到的內容

- 如何安裝並引用 Aspose.OCR NuGet 套件。  
- 為何設定 `RecognitionSettings` 是**提升 OCR 準確度**的關鍵。  
- 取得從檔案串流**load image for OCR**所需的完整程式碼。  
- 如何**recognize text from stream**以及處理西里爾字母或其他語言。  
- 進一步調校的技巧，例如去傾斜與去雜訊，以保持高準確率。

此處不提供模糊的「請參考文件」捷徑——只給你一個可自行複製貼上並執行的完整解決方案。

## 前置條件

| 需求 | 原因 |
|-------------|--------|
| .NET 6.0 or later | Aspose.OCR 支援 .NET Standard 2.0+，而 .NET 6 提供最新的效能提升。 |
| Visual Studio 2022 (or any IDE you like) | 方便建立專案與管理 NuGet。 |
| A PNG image containing Cyrillic or any other language you want to test | 我們將**read text from PNG**，並展示語言選擇如何影響準確度。 |
| Internet access to pull the NuGet package | 此函式庫位於 NuGet.org 上。 |

就這樣——沒有什麼特殊需求。

## 步驟 1：安裝 Aspose.OCR 並準備專案

首先，將 Aspose.OCR 套件加入你的專案：

```bash
dotnet add package Aspose.OCR
```

為何這對**提升 OCR 準確度**很重要？此套件內含預訓練的語言模型以及一系列前處理過濾器（去傾斜、去雜訊等），這些對於獲得乾淨的結果至關重要。若省略此步驟，將只能使用預設、較不穩健的引擎。

> **專業提示：** 若你針對特定語言，建議從 Aspose 官方網站下載相應的語言套件；這可將錯誤率降低數個百分點。

## 步驟 2：建立 OCR 引擎並設定 Recognition Settings

現在我們將實例化 `OcrEngine`，並告訴它我們想透過啟用前處理過濾器與選擇正確語言來**提升 OCR 準確度**。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Step 2: Initialize the OCR engine with accuracy‑boosting settings
using var ocrEngine = new OcrEngine();

var recognitionSettings = new RecognitionSettings
{
    // Choose the language that matches your image; Cyrillic is used here as an example
    Language = Language.Cyrillic,

    // PreprocessFilters help the engine deal with common image issues
    PreprocessFilters = new[]
    {
        PreprocessFilter.Deskew,   // Straightens tilted text
        PreprocessFilter.Denoise   // Removes background noise
    }
};
```

**為何使用這些過濾器？** 去傾斜可校正文字行的角度，這是導致 OCR 分數低落的主要原因之一。去雜訊則減少引擎可能誤認為字元的斑點。兩者結合可顯著**提升 OCR 準確度**——在噪點掃描上常可提升 10‑15 %。

## 步驟 3：載入 PNG 圖片 – 「Read Text from PNG」

接下來，我們需要**load image for OCR**。Aspose 提供 `ImageStream.FromFile`，可將檔案讀取為引擎可使用的串流。

```csharp
// Step 3: Load the PNG image you want to process
string imagePath = @"YOUR_DIRECTORY/cyrillic_doc.png";
var imageStream = ImageStream.FromFile(imagePath);
```

如果圖片儲存在資料庫或透過 API 接收，你可以將 `FromFile` 改為 `FromBytes` 或 `FromStream`——相同的**recognize text from stream**方法皆可使用。

## 步驟 4：從串流辨識文字

以下是使用先前定義設定，執行**recognize text from stream**的核心呼叫。

```csharp
// Step 4: Perform OCR and capture the result
string ocrResult = ocrEngine.Recognize(imageStream, recognitionSettings);
```

`Recognize` 方法會回傳包含所有偵測到字元的純文字字串。由於我們選擇了 `Language.Cyrillic` 並啟用了去傾斜/去雜訊，引擎已調校為能以更高忠實度**extract text from image**。

## 步驟 5：顯示或處理擷取的文字

最後，讓我們**extract text from image**並在主控台上顯示。於實際應用中，你可能會將輸出寫入資料庫、文字檔，或送入搜尋索引。

```csharp
// Step 5: Output the OCR result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrResult);
```

### 預期輸出

如果 PNG 包含西里爾文句子「Привет мир」（Hello world），你應該會看到類似以下的結果：

```
=== OCR Result ===
Привет мир
```

若結果出現雜亂符號，請再次確認已啟用正確的語言與前處理過濾器——這些是**提升 OCR 準確度**的主要調整點。

## 視覺概覽（可選）

如果你想快速瀏覽流程圖，請參考下方圖片。alt 文字已包含主要關鍵字，以符合 SEO 要求。

![Improve OCR accuracy flow diagram](/images/ocr-accuracy-flow.png "Diagram showing steps to improve OCR accuracy")

## 進階技巧以進一步**提升 OCR 準確度**

1. **調整影像解析度**  
   OCR 引擎在 300 dpi 或更高的解析度下表現最佳。若你的 PNG 解析度較低，請先使用 `ImageProcessor.Resize` 進行放大。

2. **自訂前處理**  
   Aspose 允許堆疊多個過濾器——若影像顏色淡化，可加入 `PreprocessFilter.Contrast`，或在高對比黑白掃描時使用 `PreprocessFilter.Binarize`。

3. **語言備援**  
   若預期混合語言，可設定 `Language = Language.AutoDetect`。雖然速度較慢，但可避免因強制使用錯誤語言模型而產生的誤辨識。

4. **批次處理**  
   將 OCR 呼叫包在迴圈中，並重複使用同一個 `OcrEngine` 實例。這可減少開銷，並確保各頁面的準確度一致。

5. **後處理清理**  
   擷取完成後，執行簡單的正規表達式以移除不需要的字元 (`[^\\p{L}\\p{N}\\s]`)——可清除引擎遺漏的殘餘雜訊。

## 結論

我們剛剛完整示範了一個端對端的範例，說明如何在使用 Aspose.OCR 讀取 PNG 檔案時**提升 OCR 準確度**。透過**load image for OCR**、設定 `RecognitionSettings`，以及**recognize text from stream**，即使面對如西里爾文等具挑戰性的文字，也能可靠地**extract text from image**。

將程式碼套用在自己的影像上，嘗試不同的前處理過濾器，你會快速發現微小調整如何大幅提升準確度。需要處理 PDF、TIFF 或多頁文件嗎？原理相同——只要將相應的串流傳入 `Recognize` 即可。

祝開發順利，願你的 OCR 結果永遠清晰如水晶！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}