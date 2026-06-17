---
category: general
date: 2026-03-05
description: 使用 Aspose OCR 在 C# 中提取圖像文字。學習在 C# 讀取圖像檔、將 DJVU 轉換為文字，並快速取得 OCR 圖像轉字串的結果。
draft: false
keywords:
- extract text from image
- read image file c#
- convert djvu to text
- ocr image to string
- recognize text from djvu
language: zh-hant
og_description: 使用 Aspose OCR 在 C# 中從圖像提取文字。本指南示範如何在 C# 讀取圖像檔、將 DJVU 轉換為文字，以及輕鬆將 OCR
  圖像轉為字串。
og_title: 在 C# 中從圖像提取文字 – 完整 Aspose OCR 指南
tags:
- Aspose OCR
- C#
- Image Processing
title: 在 C# 中從圖像提取文字 – Aspose OCR 步驟說明
url: /zh-hant/net/text-recognition/extract-text-from-image-in-c-aspose-ocr-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中從圖像提取文字 – 完整 Aspose OCR 指南

有沒有曾經需要**從圖像提取文字**，卻不確定哪個函式庫能提供可靠的結果？也許你手頭有一批 DJVU 掃描檔，只想要純文字而不想使用第三方工具。本文教學將在幾分鐘內使用 Aspose OCR for .NET 解決這個問題。

我們將一步步說明如何在 C# 中讀取圖像檔案、將 DJVU 文件轉換為文字，以及將任何 OCR 圖像轉為乾淨的字串。最後你會得到一個可直接執行的 Console 應用程式，會把辨識出的文字印到螢幕上。沒有模糊的「請參考文件」連結——只有完整、可直接複製貼上的解決方案。

## 需要的環境

- **.NET 6.0** 或更新版本（程式碼同樣支援 .NET Framework 4.6 以上）。  
- **Aspose.OCR for .NET** NuGet 套件（免費試用授權即可測試）。  
- DJVU 檔案或任何支援的圖像（PNG、JPEG、BMP 等）。  
- Visual Studio、Rider，或你慣用的編輯器。

如果缺少上述任一項，只要安裝 NuGet 套件即可：

```bash
dotnet add package Aspose.OCR
```

設定完成。讓我們開始吧。

## 步驟 1：初始化 OCR 引擎 – 從圖像提取文字

首先建立 `OcrEngine` 的實例。可以把它想像成會閱讀像素並轉換成字元的大腦。

```csharp
using Aspose.OCR;
using System;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine
        var ocrEngine = new OcrEngine();
```

為什麼要在載入檔案之前就實例化引擎？Aspose 的設計將設定（例如授權）與實際圖像資料分離，讓同一個引擎可以重複使用於多個檔案，而不必每次都重新建立物件——這是一個小幅的效能提升。

## 步驟 2：套用 Aspose OCR 授權（非必須但建議）

如果你有商業授權，現在就設定它。跳過此步驟會進入示範模式，輸出會加上浮水印且頁數受限。

```csharp
        // Apply license – remove this line if you’re using the free trial
        ocrEngine.SetLicense("Aspose.OCR.lic");
```

**小技巧：** 將授權檔放在版本控制系統之外（例如使用環境變數），以免不小心提交。

## 步驟 3：載入圖像 – 輕鬆讀取 C# 圖像檔案

Aspose 能讀取多種格式，包括較少見的 DJVU。我們會使用 `ImageStream.FromFile` 輔助方法將檔案載入引擎。

```csharp
        // Load the image (DJVU, PNG, JPEG, etc.)
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.djvu");
```

如果你想使用 `byte[]`（例如圖像來自資料庫），也可以改用 `ImageStream.FromBytes(byteArray)`。在需要從串流而非磁碟讀取圖像時，這個彈性非常好用。

## 步驟 4：執行 OCR – 單次呼叫將圖像轉為字串

現在魔法發生了。呼叫 `Recognize()` 會執行 OCR 引擎，並回傳包含提取文字、信心分數等資訊的 `RecognitionResult`。

```csharp
        // Run OCR and get the result
        var result = ocrEngine.Recognize();

        // Extract plain text
        string recognizedText = result.Text;
```

為什麼不直接呼叫 `Recognize().Text`？將呼叫分開可以讓你在之後檢查 `result.Confidence` 或 `result.Regions`，如果需要更細緻的資料（例如除錯或建立 UI 以標示低信心的單字）就很方便。

## 步驟 5：顯示提取的文字 – 最終輸出

最後，把文字寫到 Console。實際應用中，你可能會寫入檔案、資料庫，或透過 API 傳送。

```csharp
        // Show the result
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(recognizedText);
    }
}
```

**預期輸出**（為簡潔起見已截斷）：

```
=== OCR Output ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

如果 OCR 引擎無法辨識任何字元，`recognizedText` 會是空字串。此時請再次檢查圖像品質，或嘗試調整引擎的語言設定（例如 `ocrEngine.Language = Language.English;`）。

## 轉換 DJVU 為文字 – 大量辨識 DJVU 文字

你可能有數十個 DJVU 檔需要處理。只要把前面的程式碼包在迴圈裡：

```csharp
string[] files = Directory.GetFiles("YOUR_DIRECTORY", "*.djvu");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    string text = ocrEngine.Recognize().Text;
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), text);
    Console.WriteLine($"Converted {Path.GetFileName(file)} → {Path.GetFileNameWithoutExtension(file)}.txt");
}
```

這段程式碼**自動將 DJVU 轉為文字**，會在每個來源旁產生一個 `.txt` 檔。快速建立可搜尋的舊掃描文件檔案庫。

## 處理邊緣情況 – 圖像噪點太多怎麼辦？

當圖像模糊、對比低或有彩色背景時，OCR 的準確度會下降。Aspose OCR 提供前處理選項：

```csharp
// Example: Binarize the image to improve contrast
ocrEngine.Image = ImageProcessing.Binarize(ocrEngine.Image, threshold: 128);
```

或者，你也可以設定引擎自動偵測語言：

```csharp
ocrEngine.Language = Language.Detect; // Detects language based on content
```

這些微調常能把 60 % 的準確率提升到 95 %。若遇到問題，可嘗試 `Threshold`、`Denoise` 或 `Deskew` 方法。

## 完整範例 – 複製、貼上、執行

以下是完整程式碼，已可直接編譯。將 `"YOUR_DIRECTORY/input.djvu"` 替換為你的檔案路徑，並確保授權檔可被存取。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Apply license (optional)
        // ocrEngine.SetLicense("Aspose.OCR.lic"); // Uncomment if you have a license

        // 3️⃣ Load the image (DJVU, PNG, JPEG, etc.)
        string imagePath = "YOUR_DIRECTORY/input.djvu";
        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // 4️⃣ Perform OCR
        var result = ocrEngine.Recognize();
        string recognizedText = result.Text;

        // 5️⃣ Output the text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(recognizedText);
    }
}
```

使用以下指令執行：

```bash
dotnet run
```

執行後，你應該會在 Console 中看到提取出的文字，與前面的範例完全相同。

## 常見問題與注意事項

- **這能處理 PDF 檔案嗎？**  
  直接不支援。Aspose OCR 只處理點陣圖；若要處理 PDF，需要先把每頁轉成圖像（例如使用 Aspose.PDF），再將圖像送入 OCR 引擎。

- **如果要在伺服器上大量批次處理該怎麼做？**  
  建立**單一**的 `OcrEngine`，在多執行緒間重複使用。引擎對唯讀操作是執行緒安全的，但請避免同時共享同一個 `Image` 實例。

- **能否提取格式化的文字（字型、大小）？**  
  Aspose OCR 只回傳純 Unicode 文字。若需要保留版面配置，需使用更進階的解決方案，例如結合 OCR‑ML 或支援版面保留的 PDF 函式庫。

## 後續步驟 – 擴展工作流程

既然已能**可靠地從圖像提取文字**，可以考慮：

- 將結果儲存至 Elasticsearch，以支援全文搜尋。  
- 把文字送入語言模型進行摘要。  
- 使用 ASP.NET Core 建立簡易 UI，讓使用者上傳檔案並即時檢視 OCR 結果。  

上述所有工作皆以我們剛剛介紹的核心程式碼為基礎，讓你輕鬆擴充解決方案。

---

### 快速回顧

- 我們**初始化**了 `OcrEngine`（Aspose OCR 的核心）。  
- 套用了**授權**以解鎖完整功能。  
- 使用 `ImageStream.FromFile` **載入** DJVU 檔案。  
- 呼叫 `Recognize()` 取得**ocr image to string**結果。  
- 將**提取的文字**印到 Console。  

這就是將任何支援的圖像（包括 DJVU）轉為可搜尋文字的完整作法。

---

隨意嘗試不同的圖像格式、調整前處理設定，或將此程式碼與其他 Aspose 函式庫串接。如果遇到問題，歡迎在下方留言——祝開發順利！

![從圖像提取文字範例](/images/ocr-example.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}