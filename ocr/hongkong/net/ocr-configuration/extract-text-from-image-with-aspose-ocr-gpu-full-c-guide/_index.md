---
category: general
date: 2026-04-06
description: 使用 Aspose OCR GPU 於 C# 從圖像提取文字。於此一步一步指引中學習如何從檔案載入圖像及設定 GPU 記憶體上限。
draft: false
keywords:
- extract text from image
- load image from file
- set gpu memory limit
- aspose ocr example
- aspose ocr gpu
language: zh-hant
og_description: 使用 Aspose OCR GPU 於 C# 從圖像提取文字。於本分步指南中學習如何從檔案載入圖像及設定 GPU 記憶體上限。
og_title: 使用 Aspose OCR GPU 從圖像提取文字 – 完整 C# 指南
tags:
- Aspose OCR
- C#
- GPU
- OCR
title: 使用 Aspose OCR GPU 從圖像提取文字 – 完整 C# 教程
url: /zh-hant/net/ocr-configuration/extract-text-from-image-with-aspose-ocr-gpu-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR GPU 進行影像文字擷取 – 完整 C# 教學

是否曾需要 **從影像擷取文字**，卻在效能成為瓶頸時卡住？你並不孤單——許多開發者在 OCR 成為瓶頸時都會遇到相同問題。在本教學中，我們將示範如何使用 Aspose OCR 的 GPU 執行環境從檔案載入影像，甚至設定 GPU 記憶體上限以更精細地控制資源。

我們會一步步走過完整、可直接執行的 C# 範例，說明每一行程式碼的意義，並指出可能遭遇的常見陷阱。完成後，你將具備在 GPU 上建置快速、可擴充 OCR 流程的堅實基礎。

## 本指南涵蓋內容

- **先決條件**：.NET 6+（或 .NET Framework 4.6+）、Aspose.OCR NuGet 套件、相容的 GPU 驅動程式。
- **逐步程式碼**：從檔案載入影像、設定 Aspose OCR GPU 引擎、擷取文字。
- **為何** 需要設定 GPU 記憶體上限，以及如何安全地設定。
- **邊緣案例處理**：低解析度影像、缺少 GPU、以及信心分數的除錯。
- **後續步驟**：批次處理、整合至 ASP.NET Core，必要時切換回 CPU。

> **專業小技巧**：若不確定 GPU 是否被使用，可在 OCR 執行時開啟 GPU 活動監測工具（例如 NVIDIA‑SMI）。你會看到記憶體使用量的尖峰與你設定的上限相符。

---

![說明使用 Aspose OCR GPU 引擎從影像擷取文字流程的圖示](extract-text-from-image-aspose-ocr-gpu.png "使用 Aspose OCR GPU 擷取影像文字")

## 步驟 1：為 GPU 處理初始化 Aspose OCR 引擎

首先需要建立一個 `OcrEngine` 實例，讓它知道要在 GPU 上執行。Aspose 提供了乾淨的 `OcrEngineSettings` 物件，可在其中指定執行環境。

```csharp
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

// Create the OCR engine and tell it to use the GPU runtime
var ocrEngine = new OcrEngine(new OcrEngineSettings
{
    Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
});
```

**為何重要**：預設情況下 Aspose OCR 會回退到 CPU，對於小影像還算可接受，但對高解析度照片則會非常慢。明確設定 `Runtime = OcrRuntime.Gpu` 可將繁重的運算交給顯示卡，顯著提升速度。

## 步驟 2：（可選）設定 GPU 記憶體上限

如果你在共用工作站或資源受限的容器中執行，能限制 OCR 引擎使用的記憶體量是很有幫助的。這樣可避免記憶體不足的當機，並讓其他程序保持順暢。

```csharp
// Limit the GPU memory usage to 1024 MB (1 GB)
ocrEngine.Settings.GpuMemoryLimit = 1024;
```

**使用時機**：  
- **多租戶環境**：多個服務共享同一塊 GPU。  
- **CI/CD 流程**：每個工作分配固定的 GPU 記憶體。  

若省略此行，Aspose 會依需求使用全部可用記憶體，這在專屬工作站上通常沒問題。

## 步驟 3：從檔案載入影像

接下來要把圖片載入記憶體。Aspose OCR 使用 `System.Drawing.Image`，因此我們使用 `Image.FromFile`。請確保路徑指向真實檔案，否則會拋出例外。

```csharp
// Replace with the actual path to your high‑resolution image
string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

using (var image = Image.FromFile(imagePath))
{
    // The image is now ready for OCR processing
    // (the next step will happen inside this using block)
}
```

**為何使用檔案載入**：許多開發者會直接傳入位元組陣列，雖然可行但會多一步不必要的轉換。使用 `Image.FromFile` 簡潔直觀，且 `using` 陳述式可確保檔案句柄即時釋放。

## 步驟 4：執行 OCR 並取得結果

引擎已配置完成且影像已載入，現在可以正式擷取文字。`Recognize` 方法會回傳 `OcrResult`，其中包含原始文字與信心分數。

```csharp
using (var image = Image.FromFile(imagePath))
{
    // Perform OCR on the loaded image
    var ocrResult = ocrEngine.Recognize(image);

    // Display the confidence and the extracted text
    Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(ocrResult.Text);
}
```

**了解輸出內容**：  
- `Confidence` 為 0~1 之間的值。0.95（即 95 %）通常代表 OCR 結果相當精準。  
- `Text` 會保留影像中的換行，對後續處理相當方便。

## 步驟 5：驗證輸出並處理邊緣案例

### 檢查信心分數

若信心低於 80 % 左右，可能需要回退至 CPU 處理或先做影像前處理（例如二值化）。

```csharp
if (ocrResult.Confidence < 0.80)
{
    Console.WriteLine("Low confidence detected – consider preprocessing or CPU fallback.");
    // Example fallback: switch to CPU runtime temporarily
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
    Console.WriteLine(cpuResult.Text);
}
```

### 處理缺少 GPU 的情況

並非每台機器都有相容的 GPU。若無法初始化 GPU 執行環境，Aspose 會拋出 `OcrException`。

```csharp
try
{
    var ocrResult = ocrEngine.Recognize(image);
    // Normal processing...
}
catch (OcrException ex) when (ex.Message.Contains("GPU"))
{
    Console.WriteLine("GPU not available – falling back to CPU.");
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine(cpuResult.Text);
}
```

### 高解析度影像

極大尺寸的影像（例如寬度 > 4000 px）會佔用大量 GPU 記憶體。若觸發先前設定的上限，Aspose 會中止處理。此時可先將影像縮小：

```csharp
using (var original = Image.FromFile(imagePath))
{
    int maxWidth = 2000;
    var resized = new Bitmap(original, new Size(maxWidth, original.Height * maxWidth / original.Width));
    var ocrResult = ocrEngine.Recognize(resized);
    // Continue as before
}
```

## 完整可執行範例

以下程式碼可直接貼到新的 Console 專案中執行，包含所有步驟、錯誤處理與可選的回退邏輯。

```csharp
// Program.cs
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Initialize OCR engine to use GPU
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
        });

        // Step 2: (Optional) Limit GPU memory usage to 1 GB
        ocrEngine.Settings.GpuMemoryLimit = 1024;

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

        // Step 3: Load image from file
        using (var image = Image.FromFile(imagePath))
        {
            try
            {
                // Step 4: Run OCR on the image
                var ocrResult = ocrEngine.Recognize(image);

                // Step 5: Output confidence and extracted text
                Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
                Console.WriteLine("Extracted text:");
                Console.WriteLine(ocrResult.Text);

                // Edge‑case: low confidence handling
                if (ocrResult.Confidence < 0.80)
                {
                    Console.WriteLine("\nLow confidence detected – trying CPU fallback...");
                    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                    var cpuResult = ocrEngine.Recognize(image);
                    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                    Console.WriteLine(cpuResult.Text);
                }
            }
            catch (OcrException ex) when (ex.Message.Contains("GPU"))
            {
                Console.WriteLine("GPU not available – falling back to CPU runtime.");
                ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                var cpuResult = ocrEngine.Recognize(image);
                Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                Console.WriteLine(cpuResult.Text);
            }
        }
    }
}
```

### 預期輸出

```
GPU OCR confidence: 96.45%
Extracted text:
This is the text that was
found in the high‑resolution
image you supplied.

```

若信心低於門檻，會看到額外的 CPU 回退訊息。

---

## 結論

現在你已掌握 **使用 Aspose OCR GPU 引擎從影像擷取文字**、**從檔案載入影像**，以及 **為生產環境設定 GPU 記憶體上限** 的方法。上面的範例是一個完整、可直接引用的解決方案，適用於任何 .NET 專案。

接下來可以考慮：

- **批次處理**：遍歷資料夾中的多張影像，將結果寫入 CSV。  
- **ASP.NET Core 整合**：提供接受上傳影像並回傳 OCR 文字的 API 端點。  
- **效能調校**：嘗試不同的 `GpuMemoryLimit` 數值，並監測 GPU 使用率以找出最佳設定。

歡迎依需求自行調整程式碼，無論是建置文件數位化管線、即時翻譯應用，或是發票掃描服務，核心步驟皆相同：初始化 GPU 引擎、聰明管理記憶體、並始終驗證信心分數。

有任何問題或遇到困難，請在下方留言，我們一起除錯。祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}