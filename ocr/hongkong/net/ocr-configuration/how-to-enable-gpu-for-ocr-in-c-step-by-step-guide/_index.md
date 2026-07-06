---
category: general
date: 2026-04-04
description: 快速在 Aspose OCR 中啟用 GPU。學習如何從圖像提取文字、載入圖像進行 OCR，並使用 C# 識別文字。
draft: false
keywords:
- how to enable gpu
- extract text from image
- how to extract text
- how to recognize text
- load image for ocr
language: zh-hant
og_description: 如何快速在 Aspose OCR 中啟用 GPU。跟隨本教學從圖像提取文字、載入圖像進行 OCR，並使用 C# 識別文字。
og_title: 如何在 C# 中啟用 GPU 進行 OCR – 完整指南
tags:
- Aspose OCR
- C#
- GPU acceleration
title: 如何在 C# 中啟用 GPU 進行 OCR – 步驟指引
url: /zh-hant/net/ocr-configuration/how-to-enable-gpu-for-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中啟用 GPU 進行 OCR – 完整教學

有沒有想過在使用 Aspose OCR 時 **如何啟用 GPU**？也許你在處理數百張收據時遇到了效能瓶頸，CPU 已經跟不上了。好消息是開啟 GPU 加速非常簡單，一旦啟用，你會看到 OCR 引擎在圖像上飛快運行。

在本教學中，我們不僅會打開 GPU 開關，還會示範 **載入圖像以進行 OCR**、**辨識文字**，以及最終 **從圖像中提取文字** 的完整 C# 範例。完成後，你將擁有一個可直接執行的程式，能從任何支援的圖片中抽取純文字——不需要外部服務。

## 您需要的條件

- .NET 6+（或 .NET Framework 4.7.2 及以上）。  
- Aspose.OCR for .NET，版本 24.2.0 或更新（此版本加入了 GPU 旗標）。  
- 具備 GPU 且已安裝相應驅動程式的機器（NVIDIA CUDA 11+ 表現良好）。  
- 您想要處理的圖像檔案——例如掃描的收據、拍攝的發票或手寫筆記。

如果您已具備上述條件，太好了——讓我們開始吧。

## 步驟 1：如何啟用 GPU – 設定 OCR 引擎

您首先需要告訴 Aspose OCR 使用 GPU。這透過在 `OcrEngine` 實例上設定 `UseGpu` 屬性來完成。該屬性預設為 `false`，因此我們需要明確將其開啟。

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // <-- GPU module namespace

// Create the OCR engine and enable GPU acceleration (available from version 24.2.0)
var ocrEngine = new OcrEngine
{
    // Enabling GPU can speed up recognition by 2‑5× on a modern card
    UseGpu = true
};
```

**為什麼這很重要：** 當 `UseGpu` 為 `true` 時，函式庫會將繁重的矩陣計算交給圖形處理器。以一般的 RTX 3060 為例，您會看到每張圖像的延遲從數秒下降到毫秒級。

> **專業提示：** 若您在無頭 CI 環境中執行，請確保已安裝 GPU 驅動程式且服務帳號具備存取裝置的權限。否則引擎會靜默地回退至 CPU 模式。

## 步驟 2：載入圖像以進行 OCR – 指定引擎的檔案來源

接下來我們需要 **載入圖像以進行 OCR**。Aspose OCR 支援 System.Drawing 所能處理的任何圖像格式（PNG、JPEG、BMP、TIFF 等）。`ImageStream.FromFile` 輔助方法會將檔案包裝成所需的串流物件。

```csharp
// Replace the path with the location of your receipt or document
string imagePath = @"C:\MyImages\receipt.jpg";

ocrEngine.Image = ImageStream.FromFile(imagePath);
```

如果您想從 `byte[]` 載入（例如圖像來自資料庫），也可以改用 `ImageStream.FromBytes(byteArray)`——結果相同，只是來源不同。

## 步驟 3：辨識文字 – 執行 OCR 程序

現在引擎已設定完成且圖像已載入，是時候 **辨識文字** 了。`Recognize` 方法負責所有繁重的工作，並回傳一個 `OcrResult` 物件，內含純文字、信心分數，甚至在需要時的邊界框資訊。

```csharp
// Run the recognition process (English is the default language)
OcrResult ocrResult = ocrEngine.Recognize();
```

您也可以在呼叫 `Recognize()` 前設定 `ocrEngine.Language = OcrLanguage.French;` 以變更語言。GPU 加速不受所載入語言套件的影響。

## 步驟 4：從圖像中提取文字 – 輸出結果

最後，我們透過讀取結果物件的 `Text` 屬性來 **從圖像中提取文字**。示範時我們僅將其輸出至主控台，您亦可寫入檔案、資料庫，或傳遞給其他服務。

```csharp
// Output the extracted plain‑text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(ocrResult.Text);
```

**預期輸出**（實際文字會依圖像而異）：

```
=== OCR RESULT ===
Store: Coffee Corner
Date: 03/28/2026
Item          Qty   Price
Latte          2    $5.00
Muffin         1    $2.50
Total                 $12.50
```

如果您需要原始的信心值，可遍歷 `ocrResult.Regions`，檢查每個 `Region.Confidence`。

## 完整範例 – 單一檔案，即可執行

以下為完整程式碼。將其複製貼上至新的主控台專案，還原 Aspose.OCR NuGet 套件，然後按 **F5** 執行。

```csharp
// ------------------------------------------------------------
// How to enable gpu for OCR in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU module namespace

class Program
{
    static void Main()
    {
        // -------- Step 1: Enable GPU ----------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true   // <-- crucial for acceleration
        };

        // -------- Step 2: Load image ----------
        // Make sure the file exists; otherwise an exception is thrown.
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------- Step 3: Recognize text -------
        OcrResult ocrResult = ocrEngine.Recognize();

        // -------- Step 4: Extract text ----------
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **注意：** 請將 `YOUR_DIRECTORY/receipt.jpg` 替換為實際的圖像路徑。若程式拋出 `FileNotFoundException`，請再次確認路徑與檔案權限。

## 常見問題與邊緣情況

### 如果偵測不到 GPU 會怎樣？

Aspose OCR 會自動回退至 CPU 模式並記錄警告。若要確認目前使用哪種模式，可在建構後檢查 `ocrEngine.IsGpuEnabled`——僅在 GPU 驅動成功載入時回傳 `true`。

### 我可以在迴圈中處理多張圖像嗎？

當然可以。只需將 `ocrEngine.Image = …` 那行移到 `foreach (var file in files)` 迴圈內。保留同一個 `OcrEngine` 實例；重複使用可避免反覆分配 GPU 資源的開銷。

```csharp
foreach (var file in Directory.GetFiles(@"C:\MyImages", "*.jpg"))
{
    ocrEngine.Image = ImageStream.FromFile(file);
    var result = ocrEngine.Recognize();
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Length} characters");
}
```

### 如何處理非英語語系？

在呼叫 `Recognize()` 前設定語言：

```csharp
ocrEngine.Language = OcrLanguage.Spanish;   // or any supported language enum
```

GPU 加速的運作方式相同，僅語言模型會更換。

### 大尺寸、高解析度照片該怎麼辦？

若遭遇記憶體不足錯誤，請先縮小圖像。Aspose OCR 提供 `ImageHelper.Resize`，可快速縮減尺寸而不會失去太多細節。

```csharp
ocrEngine.Image = ImageHelper.Resize(
    ImageStream.FromFile(imagePath), 
    maxWidth: 2000, 
    maxHeight: 2000);
```

## 結論

我們已說明了 **如何啟用 GPU** 於 Aspose OCR，示範了 **載入圖像以進行 OCR**、**辨識文字**，以及 **從圖像中提取文字** 的完整流程，並提供一個簡潔、可直接投入生產的 C# 程式。只要切換 `UseGpu` 旗標，即可獲得顯著的速度提升，特別是在批次處理收據、發票或任何高流量文件時。

準備好進一步了嗎？試著將此 OCR 流程與資料庫結合，儲存提取出的收據，或將純文字輸入自然語言處理模型以進行費用分類。您也可以探索 `OcrResult.Regions` 集合，取得邊界框座標，並建立 UI 在原圖上標示每個單字。

祝程式開發順利，盡情體驗 GPU 加速為您的 OCR 工作負載帶來的額外效能！

---

![如何啟用 GPU 示意圖](gpu-ocr-diagram.png "如何啟用 GPU 示意圖")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}