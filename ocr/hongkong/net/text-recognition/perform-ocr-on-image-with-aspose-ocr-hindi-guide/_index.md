---
category: general
date: 2026-06-03
description: 使用 Aspose OCR 在 C# 中對圖像執行 OCR。學習如何載入圖像進行 OCR，並離線提取印地語文字圖像，提供逐步程式碼說明。
draft: false
keywords:
- perform OCR on image
- load image for OCR
- extract Hindi text image
language: zh-hant
og_description: 在 C# 中使用 Aspose OCR 進行圖像 OCR。此教學示範如何載入圖像進行 OCR，離線提取印地語文字，並提供可執行的程式碼。
og_title: 對圖像執行 OCR – Aspose OCR 印地語指南
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Perform OCR on image using Aspose OCR in C#. Learn how to load image
    for OCR and extract Hindi text image offline with step‑by‑step code.
  headline: Perform OCR on Image with Aspose OCR – Hindi Guide
  type: TechArticle
- description: Perform OCR on image using Aspose OCR in C#. Learn how to load image
    for OCR and extract Hindi text image offline with step‑by‑step code.
  name: Perform OCR on Image with Aspose OCR – Hindi Guide
  steps:
  - name: Create the OCR Engine Instance
    text: The engine is the heart of Aspose OCR. Instantiating it gives you access
      to all the settings you’ll tweak later.
  - name: Point the Engine to Offline Resources
    text: Aspose ships language packs that you can store locally. Setting `ResourcesFolder`
      tells the engine where to look.
  - name: Force Offline Mode
    text: You might wonder, “Do I really need to disable online lookup?” If you’re
      working behind a firewall or just want deterministic results, set `UseOfflineResources`
      to `true`.
  - name: Select Hindi as the Recognition Language
    text: Here we **extract Hindi text image** by telling the engine which language
      to expect. This dramatically improves accuracy.
  - name: Load Image for OCR
    text: Now we actually **load image for OCR**. The `OcrImage.FromFile` method reads
      the bitmap into a format the engine understands.
  - name: Run the Recognition
    text: With everything set, we finally **perform OCR on image** by calling `Recognize`.
  - name: Output the Recognized Text
    text: The result object contains a `Text` property that holds the extracted string.
      We simply write it to the console.
  type: HowTo
tags:
- Aspose OCR
- C#
- Hindi OCR
title: 使用 Aspose OCR 在圖像上執行 OCR – 印地語指南
url: /zh-hant/net/text-recognition/perform-ocr-on-image-with-aspose-ocr-hindi-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 在圖像上執行 OCR – 印地語指南

有沒有曾經需要**在圖像上執行 OCR**，卻不知道如何取得印地語字元？你並不孤單——許多開發者在首次嘗試讀取非拉丁文字時都會碰到這個問題。好消息是 Aspose OCR 讓這個過程相當簡單，而且甚至可以完全離線執行。

在本指南中，我們將**載入圖像以進行 OCR**，將引擎指向離線語言套件，最後**擷取印地語文字圖像**資料，且全程不需要連線。完成後，你將擁有一個可直接執行的 C# 主控台應用程式，能讀取印地語收據並將文字輸出到主控台。

## 需要的環境

- **.NET 6.0** 或更新版本（程式碼亦相容 .NET Framework 4.7+）
- **Aspose.OCR for .NET** NuGet 套件  
  `dotnet add package Aspose.OCR`
- 包含**離線印地語語言資源**的資料夾（可從 Aspose 入口網站下載）
- 含有印地語文字的圖像檔，例如 `receipt_hindi.png`

就這樣——不需要外部服務、API 金鑰，只有直接的程式碼。

## 在圖像上執行 OCR – 步驟實作

以下我們將流程分為七個清晰步驟。每個步驟都說明**為什麼**它重要，而不僅僅是**要輸入什麼**。

### 步驟 1：建立 OCR 引擎實例

引擎是 Aspose OCR 的核心。實例化它即可取得之後會調整的所有設定。

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class OfflineLanguageDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine instance
        var ocrEngine = new OcrEngine();
```

> **為什麼？**  
> 如果沒有 `OcrEngine`，就沒有物件可以呼叫 `Recognize`。把它想像成稍後會掃描圖片的「相機」。

### 步驟 2：將引擎指向離線資源

Aspose 會提供可本機儲存的語言套件。設定 `ResourcesFolder` 讓引擎知道要去哪裡尋找。

```csharp
        // Step 2: Point the engine to the folder containing offline language data files
        ocrEngine.Settings.ResourcesFolder = @"YOUR_DIRECTORY/Resources";
```

> **提示：**  
> 在開發期間使用絕對路徑，之後在正式環境切換為相對路徑或設定檔設定。

### 步驟 3：強制離線模式

你可能會想，「真的需要停用線上查詢嗎？」如果你在防火牆後或只想要確定的結果，請將 `UseOfflineResources` 設為 `true`。

```csharp
        // Step 3: Instruct the engine to use only the offline resources (no online lookup)
        ocrEngine.Settings.UseOfflineResources = true;
```

> **專業提示：**  
> 若將此旗標保留為 `false`，引擎可能會下載額外資料，導致延遲，甚至違反安全政策。

### 步驟 4：選擇印地語作為辨識語言

在此我們透過告訴引擎預期的語言來**擷取印地語文字圖像**。這會大幅提升準確度。

```csharp
        // Step 4: Select the desired language for recognition (Hindi in this case)
        ocrEngine.Settings.Language = OcrLanguage.Hindi;
```

> **為什麼有效：**  
> OCR 引擎使用特定語言的字元模型。鎖定印地語後，可避免引擎在數十種文字間猜測。

### 步驟 5：載入圖像以進行 OCR

現在我們真正**載入圖像以進行 OCR**。`OcrImage.FromFile` 方法會將位圖讀取成引擎可理解的格式。

```csharp
        // Step 5: Load the image that contains the text to be recognized
        var image = OcrImage.FromFile(@"YOUR_DIRECTORY/Images/receipt_hindi.png");
```

> **常見陷阱：**  
> 在 Windows 上使用正斜線路徑仍可運作，但使用 `Path.Combine` 可讓程式碼跨平台。

### 步驟 6：執行辨識

在所有設定完成後，我們最終透過呼叫 `Recognize` **在圖像上執行 OCR**。

```csharp
        // Step 6: Perform OCR on the image
        var result = ocrEngine.Recognize(image);
```

> **發生了什麼？**  
> 引擎會掃描每個像素，將圖樣與印地語字形資料庫比對，並組合成 Unicode 字元字串。

### 步驟 7：輸出辨識文字

結果物件包含 `Text` 屬性，內含擷取的字串。我們只需將它寫入主控台。

```csharp
        // Step 7: Output the recognized text
        System.Console.WriteLine(result.Text);
    }
}
```

> **預期輸出：**  
> 如果 `receipt_hindi.png` 包含「भुगतान सफल」，主控台會精確列印該行，保留變音符號。

## 載入圖像以進行 OCR – 準備資源

如果你在想是否可以改用串流而非檔案提供給引擎，答案是可以。將 `OcrImage.FromFile` 替換為：

```csharp
using (var stream = File.OpenRead(@"YOUR_DIRECTORY/Images/receipt_hindi.png"))
{
    var image = OcrImage.FromStream(stream);
    var result = ocrEngine.Recognize(image);
    Console.WriteLine(result.Text);
}
```

> **為什麼使用串流？**  
> 串流讓你能處理儲存在資料庫、雲端 Blob 或嵌入式資源的圖像——非常適合可擴充的服務。

## 擷取印地語文字圖像 – 處理邊緣案例

1. **缺少語言套件** – 若找不到印地語套件，`Recognize` 會拋出例外。請將呼叫包在 try/catch 中，並記錄友善訊息。  
2. **低解析度圖像** – OCR 準確度在低於 300 dpi 時會下降。載入前先對圖像做前處理（調整大小、銳化）。  
3. **混合語言文件** – 你可以啟用多語言：  
   `ocrEngine.Settings.Language = OcrLanguage.Hindi | OcrLanguage.English;`

這些調整可確保你的**在圖像上執行 OCR**流程在正式環境中保持穩定。

## 執行完整範例

將以下程式碼儲存為 `Program.cs`，替換佔位路徑後執行：

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;
using System;
using System.IO;

class OfflineLanguageDemo
{
    static void Main()
    {
        // Initialize engine
        var ocrEngine = new OcrEngine();

        // Offline resources folder
        ocrEngine.Settings.ResourcesFolder = @"C:\OCRResources";

        // Force offline mode
        ocrEngine.Settings.UseOfflineResources = true;

        // Hindi language only
        ocrEngine.Settings.Language = OcrLanguage.Hindi;

        // Load image for OCR
        var imagePath = @"C:\OCRResources\Images\receipt_hindi.png";
        var image = OcrImage.FromFile(imagePath);

        // Perform OCR on image
        var result = ocrEngine.Recognize(image);

        // Output extracted Hindi text image
        Console.WriteLine("Recognized text:");
        Console.WriteLine(result.Text);
    }
}
```

執行 `dotnet run` 後，應會看到類似以下的輸出：

```
Recognized text:
भुगतान सफल
धन्यवाद
```

若得到空字串，請再次確認 **ResourcesFolder** 指向包含 `Hindi.traineddata` 的資料夾，且圖像足夠清晰。

## 結論

我們已說明如何使用 Aspose OCR **在圖像上執行 OCR**，從 **載入圖像以進行 OCR** 到 **擷取印地語文字圖像**，全部在離線環境下完成。上方完整可執行的程式碼提供了堅實的基礎，而關於串流、錯誤處理與多語言支援的技巧，將協助你將此解決方案套用到實務專案。

準備好下一步了嗎？試著將語言切換為 **OcrLanguage.Tamil**，或從 Azure Blob 儲存體提供圖像。你也可以嘗試 `ImagePreprocessing` 設定，以提升噪點收據的辨識準確度。

有任何問題或遇到卡關嗎？留下評論吧——祝開發愉快！ 

![Perform OCR on image example

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在本篇示範的技術之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [使用 Aspose.OCR 於 C# 進行圖像文字擷取與語言選擇](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [使用 Aspose OCR 進行多語言圖像文字辨識](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [從圖像擷取文字 – 使用 Aspose.OCR for .NET 進行 OCR 最佳化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}