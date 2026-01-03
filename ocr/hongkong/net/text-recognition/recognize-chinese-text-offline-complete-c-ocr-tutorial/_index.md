---
category: general
date: 2026-01-02
description: 學習如何使用 Aspose.OCR 進行離線文字辨識，識別中文文字並從 PNG 檔案中提取文字。無需網路，只需幾個步驟即可對圖像執行 OCR。
draft: false
keywords:
- recognize chinese text
- extract text from png
- offline text recognition
- perform OCR on image
language: zh-hant
og_description: 在無需網路的情況下辨識中文文字。本教學示範如何使用離線文字辨識從 PNG 中提取文字，並在 C# 中對圖像執行 OCR。
og_title: 離線辨識中文文字 – 步驟式 C# 指南
tags:
- OCR
- C#
- Aspose
title: 離線識別中文文字 – 完整 C# OCR 教程
url: /zh-hant/net/text-recognition/recognize-chinese-text-offline-complete-c-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 離線辨識中文文字 – 完整 C# OCR 教學

是否曾需要從掃描的 PNG 中 **辨識中文文字**，但您的應用程式在沒有網路的機器上執行？您並不孤單。在許多企業情境——例如與外部斷絕連線的伺服器或現場裝置——依賴雲端服務根本不可行。

本指南將逐步說明一個完整的解決方案，讓您能 **從 png 檔案擷取文字**、執行 **離線文字辨識**，以及使用 Aspose.OCR **對影像資產執行 OCR**。完成後，您將擁有一個可直接執行的 C# 主控台程式，將中文字符直接輸出至主控台。

## 前置條件

- .NET 6 SDK（或任何較新的 .NET 版本）已在本機安裝。  
- Visual Studio 2022 或 VS Code——依您喜好選擇。  
- Aspose.OCR for .NET 的 NuGet 套件副本（`Aspose.OCR`）。  
- 英文與簡體中文的語言資源檔（本教學示範如何自動下載）。  
- 一張名為 `chinese_doc.png` 的影像，放置於可參考的資料夾（`YOUR_DIRECTORY` 佔位符）。

不需要額外的服務或 API 金鑰——只需本機 DLL 與幾個資源檔。

---

## 步驟 1 – 下載所需的語言資源（一次）

Aspose.OCR 會將語言套件儲存在磁碟上。首次執行應用程式時，需要下載這些套件。`ResourceManager.DownloadResources` 呼叫正是執行此動作，且因為我們同時傳入英文與簡體中文，之後引擎即可在兩者間切換，且不會產生額外的網路流量。

```csharp
using Aspose.OCR;

// Download English and Simplified Chinese language packs (run once)
ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);
```

> **專業提示：** 若需在多台機器上產生可重現的建置，請將下載的資料夾（`Aspose.OCR.Resources`）納入版本控制。

## 步驟 2 – 以離線模式初始化 OCR 引擎

將 `OfflineMode = true` 設定為真，告訴函式庫避免任何 HTTP 呼叫。這是實現真正 **離線文字辨識** 的關鍵。

```csharp
// Initialise the OCR engine for offline use
var ocrEngine = new OcrEngine()
{
    OfflineMode = true   // Guarantees no network traffic
};
```

> **為何重要：** 某些 OCR 函式庫在缺少語言套件時會回退至雲端服務。強制離線模式可確保效能確定性，並符合資料隱私政策。

## 步驟 3 – 載入欲處理的 PNG

我們將使用 `System.Drawing.Bitmap` 讀取影像。若您的專案在非 Windows 平台上以 .NET 6+ 為目標，可考慮使用 `SkiaSharp` 作為替代方案，但對於大多數以 Windows 為主的部署而言，`Bitmap` 已足夠。

```csharp
using System.Drawing;

// Load the PNG that contains Chinese characters
var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
var image = new Bitmap(imagePath);
```

> **特殊情況：** 若 PNG 檔案非常大（超過 5 MP），您可能需要先將其縮小，以加快辨識速度並減少記憶體使用量：

```csharp
// Optional downscale for huge images
if (image.Width * image.Height > 5_000_000)
{
    var scaled = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
    image.Dispose();
    image = scaled;
}
```

## 步驟 4 – 使用簡體中文語言執行辨識

此處明確告訴引擎使用哪種語言。`RecognitionOptions` 物件亦允許您調整 `DetectOrientation` 或 `PreserveFormatting` 等設定，但預設值已能滿足大多數印刷文件的需求。

```csharp
using Aspose.OCR;

// Perform OCR using Simplified Chinese language pack
var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
{
    Language = Language.ChineseSimplified
});
```

## 步驟 5 – 顯示（或進一步處理）擷取的文字

`OcrResult.Text` 屬性保存純文字表示。您可以將其寫入主控台、檔案，或傳入後續的 NLP 流程。

```csharp
// Output the recognized Chinese text to the console
Console.WriteLine("=== Recognized Chinese Text ===");
Console.WriteLine(ocrResult.Text);
```

### 預期輸出

若 `chinese_doc.png` 包含「你好，世界！」這句話，主控台將顯示：

```
=== Recognized Chinese Text ===
你好，世界！
```

> **注意：** OCR 的準確度取決於影像品質、字體清晰度與對比度。為獲得最佳效果，請使用高解析度掃描（300 dpi 或更高），且確保文字未傾斜。

---

## 完整範例程式

以下是完整、可直接複製貼上的程式碼。將其儲存為 `Program.cs` 放入新建的主控台專案，然後執行 `dotnet run`。所有步驟已串接在一起，您可看到從資源下載到最終輸出的完整流程。

```csharp
// Program.cs
using Aspose.OCR;
using System;
using System.Drawing;

class OfflineExample
{
    static void Main()
    {
        // 1️⃣ Download language resources (only needed once)
        ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);

        // 2️⃣ Initialise OCR engine in offline mode
        var ocrEngine = new OcrEngine()
        {
            OfflineMode = true
        };

        // 3️⃣ Load the PNG image
        var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
        using var image = new Bitmap(imagePath);

        // 4️⃣ Recognise Simplified Chinese text
        var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
        {
            Language = Language.ChineseSimplified
        });

        // 5️⃣ Print the result
        Console.WriteLine("=== Recognized Chinese Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **小技巧：** 若希望在真的無法連線時能優雅地處理，可將 `ResourceManager.DownloadResources` 呼叫包在 `try/catch` 區塊中。否則該方法會拋出 `NetworkException`。

---

## 常見問題 (FAQ)

| Question | Answer |
|----------|--------|
| **我可以辨識繁體中文嗎？** | 可以——將 `Language.ChineseSimplified` 替換為 `Language.ChineseTraditional`，並下載相應的語言套件。 |
| **如果我要從 JPEG 而非 PNG 擷取文字該怎麼辦？** | 相同程式碼即可，只需更改檔案副檔名。`Bitmap` 支援大多數常見的點陣圖格式。 |
| **有沒有辦法取得每個字元的邊界框？** | 將 `RecognitionOptions.DetectRegions = true`。`OcrResult` 便會包含帶座標的 `Region` 物件。 |
| **如何在 Linux 上執行？** | 使用 `System.Drawing.Common` 套件（1.0 以上）。在無頭 Linux 環境下，可能需要 `libgdiplus` 原生相依性。 |
| **我可以批次處理資料夾內的多張影像嗎？** | 當然可以——將辨識邏輯包在 `foreach (var file in Directory.GetFiles(folder, "*.png"))` 迴圈中。 |

## 後續步驟與相關主題

- **提升準確度**：嘗試將 `RecognitionOptions.PreprocessImage = true`，讓引擎自動增強對比度。  
- **結合多語言**：您可以將語言陣列傳給 `ResourceManager.DownloadResources`，讓引擎自動偵測。  
- **整合 UI**：將主控台程式碼放入 WinForms 或 WPF 應用程式，並在文字方塊中顯示 OCR 結果。  
- **探索其他 Aspose 函式庫**：`Aspose.PDF` 用於 PDF 產生，`Aspose.Slides` 用於投影片自動化等。  

如果您有興趣從其他影像格式擷取文字，使用相同的模式即可——只需更換檔案路徑，並視需要調整前處理選項。祝開發愉快！

---

![辨識中文文字範例](/images/recognize-chinese-text.png "顯示辨識中文文字輸出於主控台的螢幕截圖")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}