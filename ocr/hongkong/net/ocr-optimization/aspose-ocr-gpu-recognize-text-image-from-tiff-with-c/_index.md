---
category: general
date: 2026-05-21
description: Aspose OCR GPU 讓您快速辨識文字圖像。了解如何載入圖像進行 OCR，從 TIFF 提取文字並提升效能。
draft: false
keywords:
- aspose ocr gpu
- recognize text image
- ocr tiff image
- load image for ocr
- extract text from tiff
language: zh-hant
og_description: Aspose OCR GPU 加速文字提取。本指南說明如何載入影像進行 OCR、辨識文字影像，並高效從 TIFF 中提取文字。
og_title: Aspose OCR GPU – 在 C# 中從 TIFF 識別文字圖像
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Aspose OCR GPU lets you recognize text image quickly. Learn how to
    load image for OCR, extract text from TIFF and boost performance.
  headline: 'Aspose OCR GPU: Recognize Text Image from TIFF with C#'
  type: TechArticle
- description: Aspose OCR GPU lets you recognize text image quickly. Learn how to
    load image for OCR, extract text from TIFF and boost performance.
  name: 'Aspose OCR GPU: Recognize Text Image from TIFF with C#'
  steps:
  - name: Enables GPU acceleration (optional, with automatic CPU fallback).
    text: Enables GPU acceleration (optional, with automatic CPU fallback).
  - name: Creates an `OcrEngine` configured for English.
    text: Creates an `OcrEngine` configured for English.
  - name: Loads a large **OCR TIFF image** from disk.
    text: Loads a large **OCR TIFF image** from disk.
  - name: Runs the recognition and prints the result.
    text: Runs the recognition and prints the result.
  type: HowTo
tags:
- aspose
- ocr
- csharp
title: Aspose OCR GPU：使用 C# 從 TIFF 識別文字圖像
url: /zh-hant/net/ocr-optimization/aspose-ocr-gpu-recognize-text-image-from-tiff-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR GPU：使用 C# 辨識 TIFF 影像中的文字

有沒有想過在不讓 CPU 卡住的情況下，從巨大的 TIFF 檔案中 **辨識文字影像**？你並不是唯一有這個疑問的人。在許多文件處理流程中，OCR 步驟往往是瓶頸，尤其是當你把數 GB 的掃描頁面交給普通的引擎時。

好消息是 **Aspose OCR GPU** 能讓這個過程加速，而以下程式碼範例正好示範了如何 **載入 OCR 影像**、**從 TIFF 取得文字**，以及在沒有 GPU 時優雅地回退。讓我們一起深入了解。

## 本教學涵蓋內容

我們將一步步說明一個可直接複製貼上的 C# 程式，內容包括：

1. 啟用 GPU 加速（可選，會自動回退至 CPU）。  
2. 建立一個以英文為目標的 `OcrEngine`。  
3. 從磁碟載入大型 **OCR TIFF 影像**。  
4. 執行辨識並印出結果。  

完成後，你將了解每個步驟的 **原因**、如何處理常見的例外情況，並擁有一個可執行的範例，能夠套用到 PDF、多頁 TIFF，甚至即時相機串流。

> **先決條件** – .NET 6+（或 .NET Framework 4.7+）、Aspose.OCR NuGet 套件，以及若想看到加速效果的 GPU 環境。若未偵測到 GPU，程式會自動改用 CPU，無需額外硬體。

---

![Aspose OCR GPU processing diagram showing CPU fallback](/images/aspose-ocr-gpu-diagram.png){: .align-center alt="aspose ocr gpu"}

## 步驟 1：啟用 GPU 加速（可選）

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // adds GPU support

// Enable GPU if a compatible device is present.
// The call is safe – if no GPU is found Aspose falls back to CPU.
OcrEngine.EnableGpu(true);
```

**為什麼重要：**  
GPU 核心在影像前處理（二值化、除噪）與神經網路推論的巨量平行運算上表現卓越。透過 `EnableGpu(true)`，引擎即可將這些工作交給 GPU。若機器缺少相容的 CUDA 顯卡，Aspose 會靜默切換回 CPU，避免程式崩潰。

**小技巧：** 在 Windows 上可能需要安裝最新的 NVIDIA 驅動程式與 CUDA 工具組；在 Linux 上，請確保 `nvidia‑driver` 與 `libcuda.so` 已加入系統的 library path。

## 步驟 2：建立並設定 OCR 引擎

```csharp
// Step 2: Instantiate the OCR engine and set the language.
var ocrEngine = new OcrEngine
{
    // English works for most scanned docs; you can pick other languages here.
    Language = OcrLanguage.English
};
```

**為什麼重要：**  
`OcrEngine` 是 **Aspose OCR GPU** 的核心。設定 `Language` 讓底層神經模型知道要辨識哪種字元集，能大幅提升準確度。你也可以調整 `Resolution`、`PreprocessOptions` 或 `RecognitionMode` 以因應更複雜的文件。

## 步驟 3：載入 OCR 影像

```csharp
// Step 3: Load a large TIFF image from disk.
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/large_doc.tif");
```

**為什麼重要：**  
TIFF 可包含多頁、高解析度與無損壓縮——非常適合保存檔案，但對記憶體負擔較重。`ImageStream.FromFile` 以串流方式讀取檔案，避免一次性載入全部影像，適合處理超大型檔案。

**邊緣案例：** 若需處理多頁 TIFF，可在迴圈中呼叫 `ocrEngine.Image = ImageStream.FromFile(path, pageIndex);`，並持續遞增 `pageIndex`，直到 `ocrEngine.Image.IsNull` 回傳 `true` 為止。

## 步驟 4：執行辨識

```csharp
// Step 4: Run the OCR process.
ocrEngine.Recognize();
```

**為什麼重要：**  
`Recognize()` 完成所有繁重工作：前處理、版面分析、字元分割，最後的神經網路推論。啟用 GPU 時，推論步驟會在 GPU 上執行，常可為大型 TIFF 節省 50‑80 % 的處理時間。

## 步驟 5：輸出結果

```csharp
// Step 5: Show how many characters were extracted and how long it took.
Console.WriteLine($"Recognized {ocrEngine.Text.Length} characters in {ocrEngine.ProcessingTime} ms");

// Optional: print the extracted text (be careful with huge strings!)
Console.WriteLine("--- Extracted Text Start ---");
Console.WriteLine(ocrEngine.Text);
Console.WriteLine("--- Extracted Text End ---");
```

**為什麼重要：**  
`ocrEngine.Text` 包含影像中全部串接好的文字，而 `ProcessingTime` 則提供一個快速的基準，讓你比較 CPU 與 GPU 的執行時間。將結果印到主控台方便除錯；在正式環境中，你可能會把文字寫入資料庫或檔案。

**預期輸出（以 2 頁發票為例）：**

```
Recognized 1342 characters in 842 ms
--- Extracted Text Start ---
Invoice #12345
Date: 2026‑04‑30
...
Total: $1,234.56
--- Extracted Text End ---
```

若未偵測到 GPU，相同硬體上執行時間可能會升至約 1800 ms，清楚顯示 **aspose ocr gpu** 的效益。

---

## 常見問題處理

| 情境 | 需要注意的地方 | 解決方式 |
|-----------|-------------------|------------|
| **未偵測到 GPU** | `EnableGpu(true)` 會靜默回退，但你可能誤以為仍在使用 GPU。 | 在呼叫後檢查 `OcrEngine.IsGpuEnabled`，並記錄結果。 |
| **巨型 TIFF 記憶體不足** | 載入 10 000 × 10 000 像素的影像可能超出 RAM。 | 使用 `ImageStream.FromFile(path, pageIndex, maxResolution: 300)` 於載入時降解析度。 |
| **語言設定錯誤** | 使用英文模型辨識法文文件會產生雜訊。 | 設定 `Language = OcrLanguage.French` 或開啟多語言模式。 |
| **多頁 TIFF** | 只處理了第一頁。 | 在迴圈中使用 `ImageStream.FromFile(path, pageNumber)` 逐頁處理。 |

---

## 完整範例程式

以下程式碼即為可直接貼入 Console 應用程式的完整範例，內含錯誤處理、GPU 狀態記錄，以及簡易計時器供自行做效能測試。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // adds GPU support

namespace AsposeOcrGpuDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Enable GPU acceleration (if available)
            OcrEngine.EnableGpu(true);
            Console.WriteLine($"GPU enabled: {OcrEngine.IsGpuEnabled}");

            // 2️⃣ Create the OCR engine and set language
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English
            };

            // 3️⃣ Load the TIFF image (replace with your actual path)
            string imagePath = @"YOUR_DIRECTORY\large_doc.tif";
            try
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Failed to load image: {ex.Message}");
                return;
            }

            // 4️⃣ Perform recognition
            try
            {
                ocrEngine.Recognize();
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Recognition error: {ex.Message}");
                return;
            }

            // 5️⃣ Output results
            Console.WriteLine($"Recognized {ocrEngine.Text.Length} characters in {ocrEngine.ProcessingTime} ms");
            Console.WriteLine("--- Extracted Text Start ---");
            Console.WriteLine(ocrEngine.Text);
            Console.WriteLine("--- Extracted Text End ---");
        }
    }
}
```

複製、貼上、按 **F5**，即可在主控台看到字元數與擷取出的文字。若需 **辨識文字影像** 的其他語言，只要把 `OcrLanguage.English` 換成 Aspose 支援的其他語言即可。

---

## 重點回顧與後續建議

我們剛剛說明了如何使用 **aspose ocr gpu** 來 **辨識文字影像**，從 **OCR TIFF 影像** 中 **載入影像**、**擷取文字**，且效率極佳。啟用 GPU、設定語言、串流 TIFF、讀取結果的核心概念，同樣適用於 JPEG、PNG 等其他格式。

### 接下來可以嘗試的方向

- **批次處理**：遍歷資料夾內的 TIFF，將每個 `ocrEngine.Text` 寫入 `.txt` 檔。  
- **多頁處理**：在 `while` 迴圈中使用 `ImageStream.FromFile(path, pageIndex)` 逐頁辨識多頁文件。  
- **自訂前處理**：調整 `ocrEngine.PreprocessOptions`（如 `Denoise`、`Deskew`）以因應噪點較多的掃描件。  
- **GPU 效能基準**：在同一台機器上分別記錄 `ProcessingTime`（有/無 `EnableGpu(true)`）以量化加速幅度。

盡情實驗吧——GPU 加速在高解析度、多頁 TIFF 上最能發揮威力，即使是一般的 1080 Ti 也能顯著縮短辨識時間。

若對特定文件類型有疑問，或需要將輸出整合至資料庫，歡迎在下方留言，我們會盡力協助。祝開發順利！

## 相關教學

- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}