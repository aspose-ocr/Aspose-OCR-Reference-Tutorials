---
category: general
date: 2026-05-02
description: 在 C# 中對圖像執行 OCR 時限制 GPU 記憶體使用。學習如何啟用 GPU 加速、從收據提取文字，並精通 C# OCR 教學。
draft: false
keywords:
- limit gpu memory usage
- extract text from receipt
- how to enable gpu acceleration
- run OCR on image
- c# ocr tutorial
language: zh-hant
og_description: 在 C# 中對圖像執行 OCR 時限制 GPU 記憶體使用量。本指南示範如何啟用 GPU 加速、從收據提取文字，並精通 C# OCR
  教學。
og_title: 在 C# OCR 中限制 GPU 記憶體使用 – 完整指南
tags:
- Aspose OCR
- C#
- GPU acceleration
title: 在 C# OCR 中限制 GPU 記憶體使用 – 完整指南
url: /zh-hant/net/ocr-optimization/limit-gpu-memory-usage-in-c-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# OCR 中限制 GPU 記憶體使用 – 完整指南

有沒有曾經在處理一批收據時需要**限制 GPU 記憶體使用**？你並非唯一遇到這種情況的人——開發者常因為一次要處理過多影像而觸發記憶體不足錯誤。好消息是 Aspose.OCR 讓你只需一行程式碼就能同時限制記憶體佔用**以及**啟用 GPU 加速。  

在本教學中，我們將逐步示範一個實用的解決方案，說明**如何啟用 GPU 加速**、從範例收據影像擷取文字，並將 GPU 記憶體使用量控制在整潔的 1 GB 以內。完成後，你將擁有一個可直接執行的 C# 主控台應用程式，以及一系列可在任何**run OCR on image**情境中重複使用的技巧。

## 需求環境

- .NET 6.0 SDK 或更新版本（程式碼亦可在 .NET 5+ 上編譯）  
- Aspose.OCR for .NET NuGet 套件 (`Aspose.OCR`) – 使用 `dotnet add package Aspose.OCR` 安裝  
- 支援 CUDA 的 GPU 或相容 DirectML 的 Windows 裝置  
- 範例收據影像 (`receipt.jpg`)，放置於可參考的資料夾中  

就這樣——不需額外的原生函式庫，也不必手動複製 DLL。Aspose 抽象化了 GPU 後端，讓你專注於業務邏輯。

## 步驟 1：安裝 Aspose.OCR NuGet 套件

首先，打開專案資料夾的終端機並執行以下指令：

```bash
dotnet add package Aspose.OCR
```

此指令會取得最新的穩定版（截至 2026 年 5 月為 23.11）。套件同時包含 CPU 與 GPU 的二進位檔，無需手動下載 CUDA 或 DirectML 執行環境——Aspose 會在執行時自動偵測可用的環境。

> **專業提示：** 若你的目標是 CI/CD 流程，請在 `.csproj` 中鎖定版本，以免意外升級。

## 步驟 2：建立 OCR Engine 並**限制 GPU 記憶體使用**

現在我們將建立 `OcrEngine` 實例，並明確指示它的 GPU 記憶體使用量不得超過 1 GB。這正是**限制 GPU 記憶體使用**需求的核心。

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

public class GpuExample
{
    public static void Run()
    {
        // Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU mode – Aspose auto‑detects CUDA or DirectML
        ocrEngine.Settings.Engine = EngineMode.Gpu;

        // 👉 Limit GPU memory usage to 1024 MB (1 GB)
        ocrEngine.Settings.GpuMemoryLimitMb = 1024;

        // Load the receipt image and run OCR
        var result = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/receipt.jpg");

        // Output the plain‑text result
        Console.WriteLine(result.Text);
    }
}
```

請留意註解 `// 👉 Limit GPU memory usage…`——該行正對應主要關鍵字。透過設定 `GpuMemoryLimitMb`，你告訴底層推論引擎最多只分配指定的記憶體量，讓多個同時執行的工作可以共存而不會耗盡 GPU。

## 步驟 3：**如何啟用 GPU 加速**（以及為何重要）

你可能會想，「為什麼不直接使用 CPU？」答案是速度。以現代的 RTX 3080 為例，同一張收據的處理時間不到 200 ms，而在 4 核心 CPU 上則需要 1.2 秒。

啟用 GPU 加速只需要切換 `EngineMode` 列舉即可：

```csharp
ocrEngine.Settings.Engine = EngineMode.Gpu;
```

Aspose 會自動選擇最佳的後端：

| 偵測到的後端 | 功能說明 |
|------------------|--------------|
| CUDA (NVIDIA)    | 使用 cuDNN 核心進行 OCR，適用於搭配 NVIDIA 顯示卡的 Windows/Linux |
| DirectML (Windows) | 利用 DirectX 12，於 AMD/Intel GPU 上亦可運作，無需額外驅動 |
| None (fallback)  | 回退至最佳化的 CPU 路徑 |

若系統同時缺少 CUDA 與 DirectML，引擎會靜默回退至 CPU——不會當機，只是效能較慢。

## 步驟 4：**Run OCR on image** 與 **extract text from receipt**

引擎配置完成後，輸入影像相當簡單。`RecognizeImage` 方法接受檔案路徑、`Stream`，甚至是 `Bitmap`。以下是最簡化的呼叫方式：

```csharp
var result = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/receipt.jpg");
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(result.Text);
```

假設收據內容如下：

```
Store XYZ
Date: 2026-04-30
Total: $23.45
```

你應該會看到類似以下的輸出：

```
=== OCR Output ===
Store XYZ
Date: 2026-04-30
Total: $23.45
```

若文字顯示為亂碼，請確認影像具備高對比度且方向正確——OCR 最適合乾淨的掃描檔。

## 步驟 5：驗證記憶體限制並處理例外情況

首次執行後，你可以查詢引擎實際使用了多少 GPU 記憶體：

```csharp
Console.WriteLine($"GPU memory used: {ocrEngine.Settings.GpuMemoryUsedMb} MB");
```

若你打算平行處理數十張收據，或許會想將限制降至 512 MB，並同時執行多個 engine 實例。只要記得每個實例都遵守同一全域上限；函式庫會自動節流分配。

> **常見陷阱：** 將限制設定過低（例如 100 MB）可能導致引擎在執行過程中回退至 CPU，造成效能不一致。請在鎖定數值前，以實際工作負載測試。

## 完整範例程式

以下是一個完整、可直接複製貼上的主控台程式。將 `YOUR_DIRECTORY` 替換為收據影像的實際路徑。

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrGpuDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step‑by‑step demo
            GpuExample.Run();

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }

    class GpuExample
    {
        public static void Run()
        {
            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable GPU acceleration (auto‑detects CUDA or DirectML)
            ocrEngine.Settings.Engine = EngineMode.Gpu;

            // 3️⃣ Limit GPU memory usage to 1 GB for concurrent jobs
            ocrEngine.Settings.GpuMemoryLimitMb = 1024;

            // 4️⃣ Load the image and run OCR
            var recognitionResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/receipt.jpg");

            // 5️⃣ Output the recognized plain‑text
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognitionResult.Text);

            // 6️⃣ Optional: Show how much GPU memory was actually used
            Console.WriteLine($"\nGPU memory used: {ocrEngine.Settings.GpuMemoryUsedMb} MB");
        }
    }
}
```

儲存檔案後，執行 `dotnet run`，你應該會在主控台看到擷取出的收據文字，同時顯示 GPU 記憶體使用的簡短報告。

## 疑難排解與常見問答

**Q: 我的 GPU 為何未被偵測？**  
A: 確認已安裝最新的 NVIDIA 驅動程式（用於 CUDA）或 Windows 10 1809 以上（用於 DirectML）。同時檢查 `Aspose.OCR` DLL 是否與你的執行程序架構相符（建議使用 x64）。

**Q: 輸出為空白。**  
A: 檢查影像品質——模糊或旋轉的收據通常需要前處理（去斜、二值化）。Aspose 提供 `ImagePreprocessor`，可在 `RecognizeImage` 前使用。

**Q: 可以在 Linux 上執行嗎？**  
A: 可以，只要你的系統配備支援 CUDA 11+ 的 NVIDIA GPU。程式碼不需任何變更即可執行。

## 結論

我們已說明如何在 C# 中使用 Aspose.OCR **限制 GPU 記憶體使用** 同時 **run OCR on image**。從安裝 NuGet 套件、配置 engine、啟用 GPU 加速，到最終 **extract text from receipt**，本指南提供一個即時可用、記憶體友善且極速的解決方案。

接下來，你可以探索更進階的 **c# OCR tutorial** 主題——例如批次處理、自訂語言套件，或將結果整合至資料庫。嘗試不同的 `GpuMemoryLimitMb` 設定，以找出最適合你的工作負載的平衡點，並留意 memory‑used 診斷資訊，以免發生意外。

祝開發順利，願你的 GPU 保持涼爽，OCR 表現依舊銳利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}