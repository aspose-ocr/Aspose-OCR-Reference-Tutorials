---
category: general
date: 2026-01-02
description: 使用 Aspose OCR 及 GPU 支援，快速在 PNG 圖檔上執行 OCR。了解如何從圖像辨識文字、提取文字，以及設定 GPU 記憶體上限。
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: zh-hant
og_description: 利用 Aspose OCR 與 GPU 加速，高效執行 PNG 圖片的 OCR。此教學示範如何從影像辨識文字、擷取文字以及控制 GPU
  記憶體使用量。
og_title: 使用 GPU 在 PNG 上執行 OCR – 完整 C# 指南
tags:
- OCR
- C#
- GPU
title: 使用 GPU 在 PNG 圖像上執行 OCR – 完整 C# 指南
url: /zh-hant/net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 GPU 上執行 PNG OCR – 完整 C# 指南

曾經需要 **在 PNG 上執行 OCR**，卻因效能瓶頸卡住嗎？你並不孤單。在許多實務工作流程中，一張高解析度的 PNG 會讓只有 CPU 的 OCR 引擎變得緩慢，將本應快速的查詢變成需要等上好幾分鐘的等待。

好消息是，Aspose OCR 提供了 GPU 擴充功能，讓你可以 **從影像中辨識文字**，而耗時僅為原來的極小比例。在本教學中，我們將手把手示範如何使用 C# **在 PNG 上執行 OCR**、如何 **從影像中擷取文字**，以及如何 **設定 GPU 記憶體上限**，讓你在硬體預算內保持最佳效能。

我們也會說明每一步背後的「如何」與「為什麼」，讓你不只是拿到一段可直接貼上的程式碼，而是真正建立起完整的概念模型。

## 你將學到

- 使用 Aspose OCR GPU 支援的前置條件。  
- 如何將 PNG 讀入 `Bitmap` 並送入 OCR 引擎。  
- 如何設定 `GpuDevice` 與 `GpuMemoryLimitMb` 以取得最佳效能。  
- 如何 **從影像中辨識文字** 並取得純文字結果。  
- 處理常見邊緣案例的技巧，例如記憶體不足的 GPU 或多頁 PNG。  

完成本指南後，你將能以 GPU 速度 **在 PNG 上執行 OCR**，並自信地掌控 OCR 工作的記憶體佔用。

![Diagram showing run OCR on PNG with GPU acceleration](run-ocr-on-png-diagram.png "run OCR on PNG example")

## 前置條件

在開始之前，請確保你已具備以下環境：

1. .NET 6.0 或更新版本（此程式碼同樣支援 .NET Core 與 .NET Framework）。  
2. 支援 CUDA 的 NVIDIA GPU（範例預設使用裝置索引 0）。  
3. Aspose.OCR NuGet 套件及其 GPU 擴充 (`Aspose.OCR.Extensions`)。  
4. 一張放在專案可參考資料夾中的範例 PNG（`input.png`）。  

如果上述項目對你來說陌生，別擔心，我們會在相關段落說明替代方案。

---

## 步驟 1 – 安裝 Aspose OCR 與 GPU 擴充

首先，沒有正確的函式庫，後續程式碼將無法編譯。

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

`Aspose.OCR.Extensions` 套件會自動下載執行 GPU 加速所需的原生 CUDA 二進位檔。  
*小技巧*：如果你的機器沒有 GPU，仍然可以編譯專案，只要在稍後將 `PreferGpu = false` 即可。

---

## 步驟 2 – 載入要處理的 PNG

現在我們透過將 PNG 載入 `Bitmap` 來真正 **在 PNG 上執行 OCR**。這一步相當直接，但值得提醒：`Bitmap` 需要檔案路徑，請確保路徑相對於可執行檔是正確的。

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

若 PNG 異常大（例如單邊超過 5000 像素），建議先縮小尺寸，以免耗盡 GPU 記憶體。這時 **設定 GPU 記憶體上限** 的選項就派上用場了。

---

## 步驟 3 – 建立並設定 GPU 使用的 OCR 引擎

以下是本教學的核心：設定 OCR 引擎以 **從影像中辨識文字**，並利用 GPU。兩個屬性是關鍵：

- `GpuDevice` – 指定使用哪一個 CUDA 裝置。  
- `GpuMemoryLimitMb` – 限制引擎可分配的 GPU 記憶體上限。

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**為什麼要設定記憶體上限？** 有些 GPU 需要與顯示器共享記憶體，或同時執行多項工作負載。透過上限可以避免因記憶體不足而發生當機，特別是在平行處理大量 PNG 時。

---

## 步驟 4 – 定義辨識選項（語言與 GPU 偏好）

`RecognitionOptions` 物件告訴引擎要辨識的語言以及是否 **偏好使用 GPU**（即使是小圖）。對大多數英文文件而言已足夠，若需其他語系，只要把 `Language.English` 換成相應的列舉值即可。

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

如果你需要 **從影像中擷取文字** 的語言不是英文，只要更改 `Language` 列舉即可。此函式庫內建支援數十種語言。

---

## 步驟 5 – 執行 OCR 並取得結果

所有設定完成後，最後只需要一行程式碼即可 **在 PNG 上執行 OCR**，並取得豐富的結果物件。

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

`OcrResult` 不僅包含純文字 (`ocrResult.Text`)，還有信心分數、邊界框，甚至是帶有高亮文字的原始影像——若需要除錯或視覺化抽取結果時非常有用。

**預期輸出**（以顯示「Hello World」的範例 PNG 為例）：

```
=== OCR Output ===
Hello World
```

若文字呈現亂碼，請先確認 PNG 是否損毀，並檢查 GPU 記憶體上限是否過低。

---

## 步驟 6 – 處理邊緣案例與最佳實踐

### 記憶體不足的 GPU

若出現 `CudaException: out of memory`，請降低 `GpuMemoryLimitMb`，或在處理前將 PNG 切割成多塊。切割可以使用 `Graphics.DrawImage` 在 `Bitmap` 的副本上完成。

### 批次處理多張 PNG

處理資料夾內多張 PNG 時，建議重複使用同一個 `OcrEngine` 實例——只初始化一次即可減少 GPU 上下文切換。

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### 回退至 CPU

若系統沒有可用的 GPU，只要將 `PreferGpu = false` 即可。引擎會自動回退至 CPU，程式碼不需任何變更。

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## 完整範例程式

以下是可直接貼到新 Console 專案的完整程式碼，包含上述所有步驟與安全檢查。

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

將檔案存為 `Program.cs`，執行 `dotnet run`，即可在主控台看到抽取出的文字。

---

## 結論

我們已示範如何使用 Aspose OCR 的 GPU 擴充，在 **PNG 上執行 OCR**、**從影像中辨識文字**，以及 **設定 GPU 記憶體上限**。透過配置 `GpuDevice` 與 `GpuMemoryLimitMb`，即使在較低階的 GPU 上，也能保持應用程式的高速與穩定。

接下來你可以：

- 嘗試其他語言（`Language.French`、`Language.Spanish`）。  
- 將 OCR 步驟整合到更大的文件處理流水線。  
- 加入後處理，如拼寫檢查或實體抽取，進一步美化原始文字。  

記住，關鍵不只是程式碼本身，而是了解每個設定背後的原因。當你懂得何時 **設定 GPU 記憶體上限**、何時回退至 CPU，就能打造出具備彈性且可擴充的 OCR 解決方案。

對特定 PNG 大小、多頁 TIFF，或 GPU 錯誤排除有疑問嗎？歡迎在下方留言，我們一起討論。祝編程愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}