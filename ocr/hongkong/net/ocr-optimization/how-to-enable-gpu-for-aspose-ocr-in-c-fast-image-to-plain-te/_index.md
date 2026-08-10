---
category: general
date: 2026-02-24
description: 如何在 Aspose OCR C# 範例中啟用 GPU – 快速將圖像轉換為純文字。包括設定 GPU 裝置 ID 以及讀取圖像文字的 C#
  指南。
draft: false
keywords:
- how to enable gpu
- image to plain text
- aspose ocr example
- set gpu device id
- read image text c#
language: zh-hant
og_description: 如何在 Aspose OCR C# 範例中啟用 GPU。學習設定 GPU 裝置 ID 並高效讀取圖像文字（C#）。
og_title: 如何在 C# 中為 Aspose OCR 啟用 GPU – 快速將圖像轉換為純文字
tags:
- Aspose OCR
- C#
- GPU acceleration
title: 如何在 C# 中為 Aspose OCR 啟用 GPU – 快速將圖像轉為純文字
url: /zh-hant/net/ocr-optimization/how-to-enable-gpu-for-aspose-ocr-in-c-fast-image-to-plain-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中啟用 Aspose OCR 的 GPU – 快速將圖像轉換為純文字

有沒有想過在使用 Aspose OCR 將圖片轉換為可編輯文字時，**如何啟用 GPU**？你並不孤單——許多開發人員在處理大型發票或掃描合約時會遇到效能瓶頸。好消息是？只要利用顯示卡，將圖像轉換為純文字就能快如閃電。

在本指南中，我們將逐步示範一個完整的 **Aspose OCR 範例**，說明如何啟用 GPU、設定 GPU 裝置 ID，並以 **C# 讀取圖像文字** 的方式實作。完成後，你將擁有一個可執行的程式，能在 CPU 版所需時間的幾分之一內擷取任何支援圖像的文字。

## 您需要的條件

- .NET 6.0 或更新版本（API 同時支援 .NET Core 與 .NET Framework）
- 支援 CUDA 的 GPU，且已安裝最新驅動程式
- Aspose.OCR for .NET 授權（或可用於開發的免費試用版）
- Visual Studio 2022（或任何你偏好的 C# 編輯器）

不需要額外的 NuGet 套件，除了 `Aspose.OCR` 本身之外，無需其他依賴。

---

## 第一步 – 安裝 Aspose OCR NuGet 套件

首先，將官方的 Aspose OCR 函式庫加入專案。開啟 **Package Manager Console**，執行：

```powershell
Install-Package Aspose.OCR
```

此指令會下載 `Aspose.OCR.dll` 以及所有相依檔案。若你偏好圖形介面，可右鍵點擊專案 → **Manage NuGet Packages** → 搜尋 *Aspose.OCR* 並點選 **Install**。  

*小技巧：* 安裝完成後，請確認 **Solution Explorer** 中的 **Dependencies** 內出現 `Aspose.OCR` 資料夾。

## 第二步 – 建立簡易的 Console 應用程式骨架

我們將建立一個小型的 console 應用程式來示範完整流程。建立新專案：

```bash
dotnet new console -n GpuOcrDemo
cd GpuOcrDemo
```

將產生的 `Program.cs` 替換為稍後提供的完整程式碼。這個骨架提供乾淨的入口點，讓我們專注於 OCR 邏輯。

## 第三步 – 如何啟用 GPU 並設定 GPU 裝置 ID

現在來到重點：**如何在 Aspose OCR 中啟用 GPU**。函式庫提供 `OcrSettings` 物件，可切換 `UseGpu`，並可選擇特定的 CUDA 裝置（透過 `GpuDeviceId`）。以下程式碼片段即是你要嵌入程式中的內容：

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration – this is the crucial “how to enable gpu” step
        ocrEngine.Settings = new OcrSettings()
        {
            UseGpu = true,          // Turn on GPU processing
            GpuDeviceId = 0         // Optional: select the first CUDA‑compatible device
        };

        // 3️⃣ Recognise text from an image (any supported format)
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/large_invoice.png");

        // 4️⃣ Output the plain‑text result to the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

### 為什麼要啟用 GPU？

啟用 GPU 後，像是像素前處理、字元分割與神經網路推論等重度運算都會交給顯示卡處理。在一張中等規格的 GTX 1650 上，與僅使用 CPU 的模式相比，可獲得 **2‑3 倍的速度提升**，尤其面對高解析度文件時更為明顯。

### 選擇裝置 ID

若你的機器有多張 GPU，`GpuDeviceId` 讓你指定使用哪一張。`0` 代表第一張裝置，`1` 代表第二張，以此類推。你可以使用 NVIDIA 的 `nvidia-smi` 工具或 Aspose 的 `GpuInfo` 類別（此處未示範）來查詢可用的 ID。

## 第四步 – 完整可執行範例（直接貼上即可）

以下是完整、可直接執行的程式。將它貼到 `Program.cs`，將圖像路徑換成磁碟上實際的檔案，然後按 **F5** 執行。

```csharp
// Program.cs – Complete Aspose OCR GPU example
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Validate the input argument (optional but handy)
            if (args.Length == 0)
            {
                Console.WriteLine("Usage: dotnet run <image_path>");
                return;
            }

            string imagePath = args[0];

            // Initialise the OCR engine
            var ocrEngine = new OcrEngine();

            // -------------------- How to Enable GPU --------------------
            // Turn on GPU acceleration and optionally pick a device
            ocrEngine.Settings = new OcrSettings()
            {
                UseGpu = true,          // Enables GPU processing
                GpuDeviceId = 0         // Selects the first CUDA‑compatible GPU
            };
            // ---------------------------------------------------------

            try
            {
                // Recognise the image – this is the “image to plain text” core
                var ocrResult = ocrEngine.RecognizeImage(imagePath);

                // Display the extracted text
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
            }
            catch (Exception ex)
            {
                // Graceful error handling – helpful when the GPU is unavailable
                Console.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

### 預期輸出

若提供的圖像內含文字 *“Invoice #12345 – Total $1,250.00”*，控制台會印出：

```
=== Extracted Text ===
Invoice #12345 – Total $1,250.00
```

結果為純文字，可進一步處理（例如寫入資料庫或交給自然語言解析器）。

## 第五步 – 驗證 GPU 使用情況（可選）

為確保真的使用了 GPU，執行程式時開啟你的 GPU 監控工具（如 **NVIDIA‑Smi** 或 **GPU‑Z**）。你應該會看到所選裝置的運算使用率出現尖峰。若只看到 CPU 活動，請再次檢查：

- GPU 驅動程式是否為最新版本。
- `UseGpu` 旗標是否已設為 `true`。
- 圖像格式是否受支援（PNG、JPEG、TIFF 等）。

## 常見問題與解決方法

| 問題 | 為何會發生 | 快速解決方案 |
|------|------------|--------------|
| **GPU 未偵測到** | 驅動程式過舊或缺少 CUDA 執行環境 | 安裝最新的 NVIDIA 驅動程式與 CUDA 工具組 |
| **`Aspose.OCR` 拋出「GPU not supported」** | 使用非 CUDA GPU（例如較舊的 AMD） | 設定 `UseGpu = false` 或改用相容的 GPU |
| **圖像路徑錯誤** | 相對路徑指向錯誤的資料夾 | 使用絕對路徑或將路徑作為命令列參數傳入 |
| **授權未套用** | 評估模式可能限制 GPU 使用 | 以 `License license = new License(); license.SetLicense("Aspose.OCR.lic");` 註冊授權 |

## 延伸範例：使用 GPU 進行批次處理

若需一次處理數十張發票，可將辨識呼叫包在迴圈中。因為 GPU 會保持熱態，後續的圖像可受益於 **warm‑up caching**，進一步減少每次執行的毫秒數。

```csharp
string[] files = Directory.GetFiles(@"C:\Invoices\", "*.png");
foreach (var file in files)
{
    var result = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Trim()}");
}
```

請務必保留同一個 `OcrEngine` 實例——若每張檔案都重新建立引擎，會重新初始化 GPU 上下文，嚴重影響效能。

## 結論

現在你已擁有一個完整、端到端的 **Aspose OCR 範例**，示範 **如何啟用 GPU**、**設定 GPU 裝置 ID**，以及 **以 C# 讀取圖像文字** 的做法。只要切換 `UseGpu` 並指向正確的裝置，就能把緩慢的 CPU‑bound OCR 工作轉變為高吞吐量的流水線，輕鬆處理大量發票、收據或任何掃描文件。

歡迎自行嘗試：更換不同的圖像格式、在多 GPU 環境調整 `GpuDeviceId`，或結合其他 Aspose 函式庫產生 PDF。只要 GPU 上線，可能性無限。

<img src="gpu-ocr.png" alt="如何在 C# 中使用 Aspose OCR 啟用 GPU – 快速將圖像轉換為純文字">

*祝程式開發順利！若遇到任何問題，歡迎在下方留言或前往 Aspose 官方論壇深入討論。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}