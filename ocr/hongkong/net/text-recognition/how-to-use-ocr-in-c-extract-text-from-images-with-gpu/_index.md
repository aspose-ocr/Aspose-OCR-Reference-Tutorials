---
category: general
date: 2026-02-13
description: 學習如何在 C# 中使用 OCR 從圖像檔案提取文字、啟用 GPU 處理，並快速將掃描檔轉換為文字。
draft: false
keywords:
- how to use OCR
- extract text from image
- how to extract text
- convert scan to text
- enable gpu processing
language: zh-hant
og_description: 如何在 C# 中使用 OCR？本指南將向您展示如何從圖像檔案中提取文字、啟用 GPU 處理，以及將掃描檔轉換為文字。
og_title: 如何在 C# 中使用 OCR – 使用 GPU 從圖像提取文字
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: 如何在 C# 中使用 OCR – 使用 GPU 從圖像中提取文字
url: /zh-hant/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 從圖片中擷取文字並啟用 GPU

有沒有想過 **如何使用 OCR** 從掃描文件中提取文字而不費吹灰之力？你並不是唯一有此疑問的人——開發者常會問：「如何有效率地從影像檔案中擷取文字？」好消息是，使用 Aspose.OCR 就能做到這一點，甚至可以 **啟用 GPU 處理**，在支援的硬件上顯著提升速度。

在本教學中，我們將一步步示範完整的端到端範例，說明 **如何使用 OCR**、**如何從影像擷取文字**、**如何將掃描檔轉換成文字**，以及當 GPU 不可用時的處理方式。完成後，你將擁有一個可直接執行的 C# 主控台應用程式，會印出辨識出的文字並告知是否真的使用了 GPU。

## 你需要的環境

- .NET 6 SDK 或更新版本（程式碼同樣適用於 .NET Core）  
- Visual Studio 2022 或任何你慣用的編輯器  
- Aspose.OCR for .NET 套件（可透過 NuGet 取得）  
- 一張高解析度的影像檔（例如 `highres_scan.tif`）作為測試用  

不需要複雜的設定——只要執行幾個 NuGet 指令即可開始。

## 步驟 1：安裝 Aspose.OCR 並建立專案

首先，你必須把 OCR 函式庫加入專案。於解決方案資料夾開啟終端機，執行：

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

此指令會建立一個名為 **OcrDemo** 的全新主控台專案，並加入 `Aspose.OCR` NuGet 套件。函式庫內含我們將使用的 `OcrEngine` 類別。

> **小技巧：** 若你的機器配備獨立顯示卡，請確保已安裝最新的顯示卡驅動程式；否則函式庫會自動回退至 CPU 模式。

## 步驟 2：撰寫完整的 OCR 程式碼

接著開啟 `Program.cs`，將內容全部替換成下列程式碼。每一行都有註解，說明 *為什麼* 這麼寫。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create an OCR engine and request GPU processing.
            //    If the GPU isn’t present, Aspose.OCR will silently
            //    switch to CPU mode – no crash, no extra code needed.
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                ProcessingMode = OcrProcessingMode.Gpu
            };

            // -------------------------------------------------
            // 2️⃣  Define the path to the image you want to process.
            //    Replace the placeholder with the actual file location.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/highres_scan.tif";

            // -------------------------------------------------
            // 3️⃣  Perform the recognition. The method returns an
            //    OcrResult object that contains the extracted text,
            //    confidence scores, and more.
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // -------------------------------------------------
            // 4️⃣  Report whether the GPU was really used.
            //    This is handy for debugging performance issues.
            // -------------------------------------------------
            Console.WriteLine($"GPU used: {ocrEngine.IsGpuEnabled}");

            // -------------------------------------------------
            // 5️⃣  Output the recognized text to the console.
            //    In a real app you might write this to a file,
            //    a database, or feed it into another workflow.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### 為什麼這樣寫會有效

- **ProcessingMode = Gpu** 會讓引擎優先嘗試使用 GPU。函式庫已將底層的 CUDA/OpenCL 呼叫抽象化，你不需要自行管理裝置上下文。  
- **IsGpuEnabled** 為布林值，會確認 GPU 路徑是否成功。如果顯示 `false`，表示引擎已自動回退至 CPU——不必驚慌。  
- **RecognizeImage** 負責所有重度運算：載入影像、執行 OCR 模型，並回傳純文字結果。除非有特殊需求（例如去斜），否則不必自行前處理位圖。

## 步驟 3：執行應用程式並驗證輸出

編譯並執行：

```bash
dotnet run
```

若環境設定正確，畫面會顯示類似以下內容：

```
GPU used: True
=== Extracted Text ===
This is the first line of the scanned document.
Here is the second line, and so on…
```

如果 GPU 不可用，第一行會顯示 `GPU used: False`，但仍會出現擷取到的文字——因為已優雅地回退至 CPU。

> **常見問題：** *如果我的影像是 JPEG 而不是 TIFF，該怎麼辦？*  
> `RecognizeImage` 方法接受 .NET `System.Drawing` 支援的任何格式（JPEG、PNG、BMP 等），只要把 `imagePath` 的副檔名改成相應的即可。

## 步驟 4：可選 – 調整設定以提升準確度

Aspose.OCR 提供了幾個可調整的參數：

| 設定 | 功能說明 | 使用時機 |
|------|----------|----------|
| `ocrEngine.Language` | 強制使用特定語言（例如 `OcrLanguage.English`） | 已知文件語言時 |
| `ocrEngine.PageSegMode` | 控制引擎如何將頁面切分成區塊 | 多欄位版面時 |
| `ocrEngine.DetectOrientation` | 自動旋轉非直立的文字 | 可能倒置的掃描件 |

你可以在呼叫 `RecognizeImage` 之前設定這些屬性。例如：

```csharp
ocrEngine.Language = OcrLanguage.English;
ocrEngine.DetectOrientation = true;
```

## 步驟 5：視覺化流程（含替代文字的圖片）

以下是一張簡易圖示，說明 **如何使用 OCR** 並可選擇 GPU 加速。圖示本身不會影響程式執行，但有助於了解整體流程。

![Diagram showing how to use OCR with GPU processing](/images/ocr-gpu-flow.png)

*替代文字：* *圖示說明如何使用 OCR 進行 GPU 處理，並在需要時回退至 CPU。*

## 邊緣案例與故障排除

1. **GPU 記憶體不足** – 超大影像可能超出 GPU 記憶體上限。此時函式庫會自動切換回 CPU。可先將影像縮小以降低記憶體需求。  
2. **不支援的影像格式** – 若 `RecognizeImage` 拋出 *NotSupportedException*，請檢查副檔名並確認影像未損毀。轉成 PNG 通常能解決問題。  
3. **信心分數低** – 若 OCR 結果出現大量無法辨識的字元，建議先做前處理（二值化、除噪）或使用更高解析度的掃描檔。

## 小結：我們完成了什麼

我們已示範 **如何在 C# 主控台應用程式中使用 OCR**，說明了 **如何從影像檔案擷取文字**，並展示了 **如何啟用 GPU 處理** 以加速結果。現在你知道如何 **將掃描檔轉換成文字**、如何驗證 GPU 是否真的被使用，以及在特殊情況下如何微調設定。

### 往後的步驟

- 嘗試將輸出寫入 **搜尋索引**（例如 Elasticsearch），讓掃描的 PDF 變得可搜尋。  
- 實作 **批次處理**——遍歷資料夾中的多張影像，將每個結果寫入 `.txt` 檔案。  
- 結合 OCR 與 **翻譯 API**，自動翻譯掃描的外文文件。  

有其他問題嗎？歡迎留言討論，祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}