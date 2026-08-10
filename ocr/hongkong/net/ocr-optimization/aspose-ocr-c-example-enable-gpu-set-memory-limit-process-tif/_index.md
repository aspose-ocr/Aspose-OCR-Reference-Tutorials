---
category: general
date: 2026-06-03
description: Aspose OCR C# 示例，展示如何設定 GPU 記憶體限制、載入影像進行 OCR，並從 TIF 檔案辨識文字，附完整程式碼與技巧。
draft: false
keywords:
- aspose ocr c# example
- set gpu memory limit
- load image for ocr
- recognize text from tif
- gpu acceleration asp ocr
- high‑resolution OCR c#
- asp ocr cuda setup
language: zh-hant
og_description: 學習完整的 Aspose OCR C# 範例：啟用 GPU、設定 GPU 記憶體上限、載入影像進行 OCR，並從 TIF 檔案辨識文字。完整程式碼已提供。
og_title: Aspose OCR C# 範例 – GPU 加速、記憶體限制與 TIF 處理
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Aspose OCR C# example showing how to set GPU memory limit, load image
    for OCR and recognize text from TIF files with full code and tips.
  headline: Aspose OCR C# Example – Enable GPU, Set Memory Limit & Process TIF Images
  type: TechArticle
- description: Aspose OCR C# example showing how to set GPU memory limit, load image
    for OCR and recognize text from TIF files with full code and tips.
  name: Aspose OCR C# Example – Enable GPU, Set Memory Limit & Process TIF Images
  steps:
  - name: Why set a memory limit?
    text: '- **Stability:** Prevents out‑of‑memory crashes when processing gigantic
      images. - **Co‑existence:** Allows other GPU‑heavy apps (e.g., TensorFlow models)
      to run side‑by‑side. - **Predictability:** Makes performance testing repeatable
      because the GPU won’t start swapping.'
  - name: Handling multi‑page TIFFs
    text: If your TIFF contains several pages, Aspose OCR will only read the first
      one by default. To process all pages, you can loop over `image.Pages` (available
      in newer SDK versions) and feed each page to the engine separately.
  - name: Why this works well with TIF
    text: '- **Lossless compression:** TIFF often stores raw pixel data, giving the
      OCR engine the highest fidelity. - **Multiple color spaces:** Aspose can handle
      grayscale, RGB, or even CMYK TIFFs without extra conversion code.'
  - name: Expected output
    text: 'Running the program on a clear, 300 dpi scan of a printed page typically
      yields something like:'
  - name: Quick checklist
    text: '- ✅ **Aspose OCR C# example** compiled without errors. - ✅ **GPU enabled**
      (`Enable = true`). - ✅ **GPU memory limit** set to 2048 MB. - ✅ **Image loaded**
      from a TIF file. - ✅ **Text recognized** and printed.'
  type: HowTo
tags:
- Aspose
- OCR
- C#
- GPU
title: Aspose OCR C# 示例 – 啟用 GPU、設定記憶體上限與處理 TIF 圖像
url: /zh-hant/net/ocr-optimization/aspose-ocr-c-example-enable-gpu-set-memory-limit-process-tif/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR C# 範例 – 啟用 GPU、設定記憶體上限與處理 TIF 圖像

有沒有想過在處理巨量 TIFF 掃描檔時，如何從 **Aspose OCR C# example** 程式碼中擠出最高效能？你並不孤單。在許多實務專案——例如數位化檔案或從高解析度收據中擷取資料——瓶頸往往不是 OCR 演算法本身，而是硬體使用率。

事實上：Aspose OCR 支援 GPU 加速，但你必須明確告訴它可使用多少記憶體、載入正確的影像類型，最後再從 .tif 檔中取出辨識文字。本教學會一步步帶你完成，從安裝 SDK 到微調 GPU 設定，讓你在不耗盡 GPU 記憶體的前提下，以極速執行 OCR。

我們也會加入幾個「如果…」情境，例如處理多頁 TIFF 或在沒有 GPU 時回退至 CPU，讓你得到的是完整且穩健的解決方案，而非一次性的程式碼片段。

## 需要的前置條件

在開始之前，請確保你的機器具備以下項目：

| 前置條件 | 為什麼重要 |
|--------------|----------------|
| **.NET 6 SDK**（或更新版本） | Aspose OCR 目標為 .NET Standard 2.0+，任何較新的 .NET 版本皆可相容。 |
| **Aspose.OCR NuGet 套件** (`Install-Package Aspose.OCR`) | 提供 `OcrEngine`、`GpuSettings` 等核心類別的程式庫。 |
| **CUDA 11+**（NVIDIA）**或 ROCm 5+**（AMD） | GPU 加速的必要條件；SDK 會在執行時檢查相容的驅動程式。 |
| 具備 **至少 2 GB VRAM** 的 **GPU**（本教學以 2048 MB 為上限） | 記憶體不足時，引擎會自動靜默回退至 CPU。 |
| 想要處理的 **高解析度 TIFF** 影像 | Aspose OCR 幾乎支援所有點陣圖格式，TIF 是掃描檔的常見格式。 |
| Visual Studio 2022（或任意你喜歡的編輯器） | 用於建置與除錯 C# 專案。 |

若缺少上述任一項目，程式仍能編譯，但將無法體驗我們所追求的效能提升。

## 步驟 1：建立 Aspose OCR C# Example Engine

每個 **Aspose OCR C# example** 的第一步都是實例化 OCR 引擎。把 `OcrEngine` 想成電影導演——它負責協調從影像載入到文字抽取的所有工作。

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();
```

> **小技巧：** 若要連續處理多張影像，請保持同一個 `OcrEngine` 實例存活。每張影像重新建立引擎會產生額外開銷，往往會超過 OCR 本身的執行時間。

## 步驟 2：設定 GPU 記憶體上限（並啟用加速）

接下來是常讓人卡住的部份：**設定 GPU 記憶體上限**。預設情況下 Aspose OCR 會盡可能使用所有可用的 VRAM，這在共用工作站上可能會導致其他程式資源不足。`GpuSettings` 物件讓你可以限制分配量。

```csharp
        // Step 2: Enable GPU acceleration (requires CUDA 11+ or ROCm 5+)
        ocrEngine.Settings.Gpu = new GpuSettings
        {
            Enable = true,          // Turn on the GPU path
            DeviceId = 0,           // First GPU in the system (change if you have multiple)
            MemoryLimitMb = 2048    // Optional cap – 2 GB in this example
        };
```

### 為什麼要設定記憶體上限？

- **穩定性：** 防止在處理超大型影像時因記憶體不足而當機。  
- **共存性：** 讓其他需要大量 GPU 的應用程式（例如 TensorFlow 模型）能同時執行。  
- **可預測性：** 測試時表現更一致，因為 GPU 不會因為突發的記憶體交換而變慢。

如果省略 `MemoryLimitMb`，Aspose 會自行分配所需的記憶體，這在專用推論伺服器上或許沒問題，但在開發者筆記型電腦上就相當危險。

## 步驟 3：載入影像以供 OCR

正確的檔案格式是下一個關鍵環節。`OcrImage.FromFile` 會自動偵測影像類型，但仍建議先確認檔案是否存在，以及它是否屬於支援的 TIFF 變體（例如 LZW 壓縮或 CCITT‑G4）。

```csharp
        // Step 3: Load the high‑resolution image to be processed
        var imagePath = "YOUR_DIRECTORY/large_photo.tif";

        if (!System.IO.File.Exists(imagePath))
        {
            System.Console.WriteLine($"Error: File not found -> {imagePath}");
            return;
        }

        var image = OcrImage.FromFile(imagePath);
```

### 處理多頁 TIFF

若你的 TIFF 包含多頁，Aspose OCR 預設只會讀取第一頁。若要處理全部頁面，可遍歷 `image.Pages`（較新 SDK 版本提供）並將每頁分別送入引擎。

```csharp
        foreach (var page in image.Pages)
        {
            var result = ocrEngine.Recognize(page);
            System.Console.WriteLine($"--- Page {page.Index + 1} ---");
            System.Console.WriteLine(result.Text);
        }
        return; // Skip the single‑image path below
```

上述程式碼示範了 **載入影像供 OCR** 的通用模式，適用於單頁與多頁檔案。

## 步驟 4：從 TIF（或任何點陣圖）辨識文字

影像已載入記憶體後，我們請 Aspose 執行辨識。`Recognize` 方法會回傳 `OcrResult`，其中包含純文字、信心分數，甚至如果需要的話，還有文字框的座標資訊。

```csharp
        // Step 4: Perform OCR recognition on the image
        var ocrResult = ocrEngine.Recognize(image);
```

### 為什麼 TIF 特別適合

- **無損壓縮：** TIFF 常保存原始像素資料，提供 OCR 引擎最高的細節還原度。  
- **多種色彩空間：** Aspose 能直接處理灰階、RGB，甚至 CMYK 的 TIFF，無需額外轉換程式碼。

若要切換語言套件（例如法文或日文），請在呼叫 `Recognize` 前設定 `ocrEngine.Settings.Language = "fr"`。

## 步驟 5：顯示辨識結果

最後，我們把文字輸出到主控台。實際應用中，你可能會寫入資料庫、JSON 檔，或將字串傳給下游的 NLP 流程。

```csharp
        // Step 5: Display the recognized text
        System.Console.WriteLine("=== OCR Output ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### 預期輸出

在 300 dpi、清晰的列印頁面掃描上執行程式，通常會得到類似以下的結果：

```
=== OCR Output ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
...
```

若影像模糊或 GPU 記憶體上限設定過低，可能會出現亂碼或結果被截斷。將 `MemoryLimitMb` 設得低於影像實際佔用的記憶體（6000×8000 像素的 TIFF 大約需要 1 GB）時，引擎會自動回退至 CPU。

## 完整範例程式

以下是可直接執行的完整程式碼。將它貼到新的 Console App 專案中，將 `YOUR_DIRECTORY/large_photo.tif` 替換成你的 TIFF 路徑，然後按 **F5** 執行。

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration and set a memory cap
        ocrEngine.Settings.Gpu = new GpuSettings
        {
            Enable = true,
            DeviceId = 0,
            MemoryLimitMb = 2048 // 2 GB limit – adjust to your GPU size
        };

        // Step 3: Load the image (ensure the file exists)
        var imagePath = "YOUR_DIRECTORY/large_photo.tif";

        if (!System.IO.File.Exists(imagePath))
        {
            System.Console.WriteLine($"Error: File not found -> {imagePath}");
            return;
        }

        var image = OcrImage.FromFile(imagePath);

        // Step 4: Perform OCR on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 5: Output the recognized text
        System.Console.WriteLine("=== OCR Output ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### 快速檢查清單

- ✅ **Aspose OCR C# example** 已成功編譯。  
- ✅ **GPU 已啟用**（`Enable = true`）。  
- ✅ **GPU 記憶體上限** 設為 2048 MB。  
- ✅ **影像已從 TIF 檔載入**。  
- ✅ **文字已辨識並列印**。

## 常見問題與避免方式

| 症狀 | 可能原因 | 解決方法 |
|---------|--------------|-----|
| `System.DllNotFoundException: cudart64_110.dll` | 未安裝 CUDA 執行時或版本不符。 | 安裝與驅動相容的 CUDA 11.x（或 12.x）。 |
| OCR 回傳空字串 | 影像過暗或 DPI 低於 150。 | 使用 `image.AdjustContrast()` 前處理，或將解析度重採樣至 300 dpi。 |
| GPU 記憶體不足當機 | `MemoryLimitMb` 設定過低。 | 提高上限或使用 `image.Crop` 將影像切割成多塊。 |
| `Unsupported image format` 錯誤 | TIFF 使用了罕見壓縮（例如 JPEG‑2000）。 | 先用 ImageMagick 轉換成支援的格式再進行 OCR。 |

## 延伸示範

既然已掌握 **aspose ocr c# example** 的核心流程，你可以進一步探索：

- **批次處理：** 迴圈讀取資料夾內所有 TIF，將每個結果寫入 `.txt` 檔。  
- **語言套件：** `ocrEngine.Settings.Language = "es"` 以支援西班牙文，或載入自訂字典。  
- **文字框座標：** 使用 `ocrResult.Regions` 取得每個單字的座標，適合做遮蔽工具。  
- **CPU 回退機制：** 將 GPU 區塊包在 try/catch 中；若失敗，設定 `ocrEngine.Settings.Gpu.Enable = false` 後重新嘗試。

這些延伸保持了核心模式不變，同時為特定需求提供更多價值。

## 接下來該學什麼？

以下教學與本篇內容密切相關，能進一步擴充你的技巧與 API 應用範圍，每篇皆附完整可執行的程式碼與步驟說明。

- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}