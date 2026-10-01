---
category: general
date: 2025-12-29
description: 如何在 C# 中使用 OCR 從圖像提取文字、顯示字元數，並透過 GPU 加速提升效能（使用 Aspose OCR）。
draft: false
keywords:
- how to use OCR
- extract text image
- display character count
- gpu acceleration ocr
- c# ocr aspose
language: zh-hant
og_description: 如何在 C# 中使用 OCR 從圖像提取文字、顯示字元數，並使用 Aspose OCR 透過 GPU 加速處理。
og_title: 如何在 C# 中使用 OCR – 使用 GPU 快速提取文字
tags:
- OCR
- C#
- Aspose
- GPU
title: 如何在 C# 中使用 OCR – 使用 GPU 加速從圖像中提取文字
url: /zh-hant/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 完整指南

有沒有想過在 .NET 專案中 **如何使用 OCR** 而不必寫上千行程式碼？也許你已掃描了一個巨大的 TIFF 檔案，需要快速取得文字，或只是想為報表儀表板計算字元數。無論哪種情況，你都來對地方了。在本教學中，我們將示範如何從影像中擷取文字、顯示字元計數，並以 **GPU 加速 OCR** 讓整個流程更快——全部使用 **C# Aspose OCR** 函式庫。

我們也會順帶提及你可能在尋找的次要主題：**extract text image**、**display character count** 以及 **c# ocr aspose** 小技巧。完成後，你將擁有一個可直接執行的主控台應用程式，能在瞬間處理大型掃描檔。

---

## 你將學會

- 在 C# 專案中設定 Aspose OCR（不需要複雜的 NuGet 操作）。
- 為大型檔案啟用 **GPU 加速 OCR**。
- 載入影像並 **從影像中擷取文字**。
- **顯示字元計數** 與處理時間。
- 處理常見問題，例如缺少 GPU 驅動程式或不支援的影像格式。

> **先決條件：** .NET 6 以上（或 .NET Framework 4.7.2）以及相容的 GPU。若沒有 GPU，程式碼會自動回退至 CPU 模式。

![How to use OCR with GPU acceleration in C#](ocr-gpu.png "how to use OCR example showing GPU usage")

*Image alt text: 使用 GPU 加速的 OCR 示意圖*

---

## 步驟 1：安裝 Aspose OCR 並準備專案

### 為什麼這很重要

在 **使用 OCR** 之前，必須先參考此函式庫。Aspose OCR 以單一 NuGet 套件提供，內含 CPU 與 GPU 的原生二進位檔，讓你不必手動搜尋 DLL。

```csharp
// In your terminal or Package Manager Console
dotnet add package Aspose.OCR
```

> **小技巧：** 若目標為 .NET Framework，請使用 Visual Studio 內的 NuGet UI，以避免版本衝突。

### 完整專案骨架

建立一個新的主控台應用程式，並貼上以下 `Program.cs`。它已包含所有必要的 `using` 陳述式，讓你不必猜測要匯入什麼。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.ImageProcessing; // optional, for advanced pre‑processing

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Call the helper that does the heavy lifting
            RunOcr(@"YOUR_DIRECTORY/large_scanned_page.tif");
        }

        static void RunOcr(string imagePath)
        {
            // Step 2: Create and configure the OCR engine (see next section)
        }
    }
}
```

儲存檔案、還原套件，即可進入下一步。

---

## 步驟 2：使用 GPU 加速的 OCR 引擎

### 為什麼要啟用 GPU？

在 CPU 上處理多百萬像素的 TIFF 可能需要數秒甚至數分鐘。**GPU 加速 OCR** 會將像素層面的運算交給顯示卡，大幅縮短時間——往往只剩原本的一小部分。

```csharp
static void RunOcr(string imagePath)
{
    // Create an OCR engine instance
    var ocrEngine = new OcrEngine();

    // Enable GPU acceleration – if a compatible device is found
    ocrEngine.UseGpu = true;
    ocrEngine.GpuDeviceId = 0; // 0 = first GPU; change if you have multiple

    // Optional sanity check – fall back to CPU if GPU init fails
    try
    {
        // This call forces the engine to initialize GPU resources
        ocrEngine.InitializeGpu();
        Console.WriteLine("✅ GPU acceleration enabled.");
    }
    catch (Exception ex)
    {
        Console.WriteLine($"⚠️ GPU init failed ({ex.Message}), switching to CPU.");
        ocrEngine.UseGpu = false;
    }

    // Load the image (this also validates format)
    var inputImage = Image.Load(imagePath);
    
    // Perform OCR – the heavy lifting happens here
    var ocrResult = ocrEngine.Recognize(inputImage);

    // Step 3: Display results (character count & processing time)
    DisplayResult(ocrResult);
}
```

> **為什麼有效：** `UseGpu` 會切換內部管線。`InitializeGpu()` 會提前驗證，讓你在耗時的 `Recognize` 呼叫前捕捉到驅動程式問題。

---

## 步驟 3：擷取文字影像並顯示字元計數

現在引擎已經運作，我們來 **從影像中擷取文字**，並顯示辨識出的字元數量。這是大多數開發者會略過的步驟，但對於驗證與後續分析至關重要。

```csharp
static void DisplayResult(OcrResult ocrResult)
{
    // The raw OCR text
    string extractedText = ocrResult.Text;

    // Character count – includes spaces and line breaks
    int charCount = extractedText.Length;

    // Processing time in milliseconds (provided by Aspose)
    long processingMs = ocrResult.ProcessingTime;

    // Output to console – easy to pipe to a file or logger
    Console.WriteLine($"🖋️ Extracted {charCount} characters in {processingMs} ms");
    Console.WriteLine("----- Begin OCR Text -----");
    Console.WriteLine(extractedText);
    Console.WriteLine("------ End OCR Text ------");
}
```

**預期輸出**（2 頁掃描的範例）：

```
✅ GPU acceleration enabled.
🖋️ Extracted 12,345 characters in 842 ms
----- Begin OCR Text -----
Lorem ipsum dolor sit amet, consectetur...
... (rest of the page) ...
------ End OCR Text ------
```

若 GPU 不可用，會顯示警告，結果相同，只是較慢。

---

## 步驟 4：處理大型檔案與邊緣情況

### 如果影像非常大怎麼辦？

Aspose OCR 能串流頁面，但仍需足夠的記憶體。建議在辨識前先將非必要的 DPI 降低：

```csharp
// Optional pre‑processing: downscale to 300 DPI if original > 600 DPI
if (inputImage.DpiX > 600 || inputImage.DpiY > 600)
{
    inputImage = inputImage.Resize(0.5, 0.5); // 50% reduction
    Console.WriteLine("🔎 Image downscaled for faster OCR.");
}
```

### 缺少 GPU 驅動程式？

`InitializeGpu()` 周圍的 `try/catch` 已能捕捉大多數問題，但你也可以查詢可用的裝置：

```csharp
var gpuInfo = GpuDeviceManager.GetDevices();
if (gpuInfo.Count == 0)
{
    Console.WriteLine("⚡ No GPU detected – defaulting to CPU.");
    ocrEngine.UseGpu = false;
}
```

### 不支援的影像格式？

Aspose 支援 TIFF、PNG、JPEG、BMP 以及少數特殊格式。若收到 `UnsupportedFormatException`，請先使用 ImageMagick 等工具或內建的 `Image.Save` 方法將檔案轉為 PNG。

---

## 步驟 5：總結 – 完整可執行範例

將以下完整程式碼複製貼上至 `Program.cs`。這是一個獨立的示範，可立即執行（只需更換路徑）。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.ImageProcessing;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust the path to point at your scanned TIFF or JPEG
            RunOcr(@"YOUR_DIRECTORY/large_scanned_page.tif");
        }

        static void RunOcr(string imagePath)
        {
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,
                GpuDeviceId = 0
            };

            try
            {
                ocrEngine.InitializeGpu();
                Console.WriteLine("✅ GPU acceleration enabled.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ GPU init failed ({ex.Message}), switching to CPU.");
                ocrEngine.UseGpu = false;
            }

            var inputImage = Image.Load(imagePath);

            // Optional downscale for gigantic files
            if (inputImage.DpiX > 600 || inputImage.DpiY > 600)
            {
                inputImage = inputImage.Resize(0.5, 0.5);
                Console.WriteLine("🔎 Image downscaled for faster OCR.");
            }

            var ocrResult = ocrEngine.Recognize(inputImage);
            DisplayResult(ocrResult);
        }

        static void DisplayResult(OcrResult ocrResult)
        {
            string extractedText = ocrResult.Text;
            int charCount = extractedText.Length;
            long processingMs = ocrResult.ProcessingTime;

            Console.WriteLine($"🖋️ Extracted {charCount} characters in {processingMs} ms");
            Console.WriteLine("----- Begin OCR Text -----");
            Console.WriteLine(extractedText);
            Console.WriteLine("------ End OCR Text ------");
        }
    }
}
```

使用 `dotnet run` 執行，觀察主控台輸出 **字元計數** 與 OCR 文字。這就是完整的 **如何使用 OCR** 流程，從頭到尾。

---

## 結論

我們剛剛說明了在 C# 中 **如何使用 OCR** 來 **從影像擷取文字**、**顯示字元計數**，並使用 **c# ocr aspose** 函式庫的 **GPU 加速 OCR** 來提升整個管線。重點如下：

1. 透過 NuGet 安裝 Aspose OCR 並引用正確的命名空間。  
2. 開啟 GPU，但必須保留 CPU 後備方案。  
3. 載入影像，視需要降尺度，然後呼叫 `Recognize`。  
4. 取得 `ocrResult.Text` 與 `ocrResult.ProcessingTime`，以 **顯示字元計數** 及效能指標。  

從此你可以延伸應用——將文字存入資料庫、送入搜尋索引，或對擷取的字串執行語言偵測。若需處理 PDF，只要將每頁轉為影像即可，程式碼同樣適用。

**接下來可以探索的步驟：**

- 使用 `PdfConverter` 從多頁 PDF 中 **extract text image**。  
- 調整 OCR 設定（語言套件、降噪）以提升準確度。  
- 在 Azure Functions 或 AWS Lambda 上使用支援 GPU 的執行個體來擴展解決方案。  

試試看、找出問題再改進。這就是實務 OCR 專案的建置方式。祝開發順利，願你的掃描檔永遠清晰可讀！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}