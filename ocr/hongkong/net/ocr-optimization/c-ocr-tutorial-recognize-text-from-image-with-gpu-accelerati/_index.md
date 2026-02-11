---
category: general
date: 2026-01-15
description: C# OCR 教學，示範如何從圖像辨識文字、從發票擷取文字，以及使用 Aspose OCR 在 GPU 上將圖像轉換為文字。
draft: false
keywords:
- c# ocr tutorial
- recognize text from image
- extract text from invoice
- convert image to text
- load image for ocr
language: zh-hant
og_description: c# OCR 教學，教你從圖像識別文字、從發票提取文字，並使用 Aspose OCR 在 GPU 上將圖像轉換為文字。
og_title: c# OCR 教學 – 快速 GPU 加速文字辨識
tags:
- OCR
- C#
- Aspose
- GPU
title: C# OCR 教學 – 使用 GPU 加速辨識圖像文字
url: /zh-hant/net/ocr-optimization/c-ocr-tutorial-recognize-text-from-image-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR 教學 – 使用 GPU 加速辨識圖像文字

是否曾經需要一個**c# OCR 教學**，能真正完成任務而不必無止盡的反覆試驗？也許你正盯著一張高解析度的發票，想知道如何在幾秒鐘內**從發票中擷取文字**。好消息是，你不需要重新發明輪子——Aspose.OCR 為你提供乾淨、GPU 加速的 API，幫你完成繁重的工作。

在本指南中，我們將逐步示範一個完整且可執行的範例，說明如何**從圖像辨識文字**、**將圖像轉換為文字**，以及處理最常見的陷阱。完成後，你將擁有一個獨立的程式，能讀取任何文件的圖片，從收據到掃描合約，並輸出乾淨、可搜尋的文字。

## 你將學會

- 如何安裝並引用 Aspose.OCR NuGet 套件。
- 如何設定 OCR 引擎在 GPU 上執行，以獲得極速效能。
- 使用 `OcrImage.FromFile` 正確**載入 OCR 圖像**的方法。
- 如何以目標語言呼叫 `Recognize` 並取得結果。
- 處理多頁 PDF、低對比掃描以及錯誤處理的技巧。

不需要任何 Aspose 的先前經驗；只要有可運作的 .NET 開發環境（Visual Studio 2022 或 VS Code）以及一張普通的 GPU（即使是整合式 Intel GPU 也足夠）。

---

## 步驟 1 – 安裝 Aspose.OCR 並準備專案

首先，你需要 Aspose.OCR 函式庫。最簡單的方式是透過 NuGet。

```bash
dotnet add package Aspose.OCR
```

> **專業提示：** 若你的目標是 .NET 6 或更高版本，套件會自動下載 Windows、Linux、macOS 的原生 GPU 二進位檔。無需額外複製 DLL。

套件加入後，開啟你的專案檔 (`*.csproj`) 並確認參考設定：

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.12.0" />
</ItemGroup>
```

現在你已具備開始編寫程式的所有必要條件。

## 步驟 2 – 建立 GPU 加速的 OCR 引擎（c# OCR 教學）

**c# OCR 教學** 的核心是 `OcrEngine`。將 `Engine = Engine.Gpu` 設定為 GPU，我們即告訴 Aspose 使用顯示卡而非 CPU。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine with GPU acceleration.
            var ocrEngine = new OcrEngine
            {
                Engine = Engine.Gpu // GPU acceleration is selected; the library auto‑detects the device.
            };

            // The rest of the steps are broken out into separate methods for clarity.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            PerformOcr(ocrEngine, imagePath);
        }
    }
}
```

> **為什麼使用 GPU？** GPU 能平行處理成千上萬的像素，將大型高 DPI 圖像的 OCR 時間從數秒縮短至毫秒等級。

## 步驟 3 – 載入 OCR 圖像（載入圖像以進行 OCR）

正確載入圖像比想像中更重要。`OcrImage.FromFile` 支援 PNG、JPEG、BMP、TIFF，甚至 PDF 頁面。它也會讀取圖像的 DPI，這會影響辨識精度。

```csharp
static void PerformOcr(OcrEngine engine, string filePath)
{
    // Step 3: Load the image you want to recognize.
    // The FromFile method automatically detects the format.
    var image = OcrImage.FromFile(filePath);

    // Optional: Pre‑process the image for better results.
    // For example, you can increase contrast or convert to grayscale.
    image = ImagePreprocessor.AdjustContrast(image, 1.2);
    image = ImagePreprocessor.ConvertToGrayscale(image);
    
    // Continue to recognition...
    RecognizeAndDisplay(engine, image);
}
```

**注意：** 若處理 PDF，你可以將每一頁提取為 `OcrImage`，並逐一送入。

## 步驟 4 – 從圖像辨識文字（辨識圖像文字）

現在魔法發生了。我們請求引擎辨識英文文字，但你也可以傳入 Aspose 支援的任何語言（西班牙文、德文、中文等）。

```csharp
static void RecognizeAndDisplay(OcrEngine engine, OcrImage image)
{
    // Step 4: Perform OCR on the image using the desired language.
    var result = engine.Recognize(image, Language.English);

    // Step 5: Output the recognized text.
    Console.WriteLine("=== OCR RESULT ===");
    Console.WriteLine(result.Text);
}
```

`result.Text` 屬性包含純文字字串。若需要每個單字的信心分數，可檢查 `result.Regions`。

### 預期輸出

```
=== OCR RESULT ===
Invoice #12345
Date: 2025‑12‑01
Total: $1,234.56
Thank you for your business!
```

若圖像模糊，可能會看到亂碼——這時第 3 步的前處理就派上用場了。

## 步驟 5 – 從發票擷取文字 – 真實案例

假設你有一個資料夾，裡面放滿掃描過的發票，且想抽取總金額。以下是前述程式碼的快速擴充，使用簡單的正規表達式。

```csharp
using System.Text.RegularExpressions;

static void ExtractTotalAmount(string ocrText)
{
    // Look for a pattern like "$1,234.56"
    var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
    if (match.Success)
        Console.WriteLine($"Detected total: {match.Value}");
    else
        Console.WriteLine("Total amount not found.");
}
```

在印出 OCR 結果後，你會呼叫 `ExtractTotalAmount(result.Text);`。這說明只要取得原始字串，**從發票中擷取文字** 是多麼簡單。

## 步驟 6 – 大量將圖像轉換為文字（將圖像轉換為文字）

單一檔案的處理對示範而言足夠，但正式環境常需處理數十或數百張圖像。以下是一段簡潔的迴圈，可處理整個目錄：

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    foreach (var file in Directory.EnumerateFiles(folderPath, "*.*", SearchOption.TopDirectoryOnly)
                                 .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
    {
        Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
        var img = OcrImage.FromFile(file);
        var res = engine.Recognize(img, Language.English);
        Console.WriteLine(res.Text);
        ExtractTotalAmount(res.Text); // optional invoice extraction
    }
}
```

執行 `ProcessFolder(ocrEngine, @"C:\Invoices")` 後，會對資料夾中所有支援的檔案**將圖像轉換為文字**，並利用 GPU 加速。

## 邊緣情況與常見陷阱

| 情況 | 為何發生 | 快速解決方案 |
|-----------|----------------|-----------|
| **低對比掃描** | OCR 難以分辨前景與背景。 | 提高對比度（`ImagePreprocessor.AdjustContrast`）或使用自適應閾值。 |
| **多頁 PDF** | `OcrImage.FromFile` 只會讀取第一頁。 | 使用 `PdfDocument` 將每頁提取為 `OcrImage`，並迴圈處理。 |
| **不支援的語言** | 預設語言為英文。 | 傳入 `Language.Spanish` 或任何支援的列舉值。 |
| **未偵測到 GPU** | 缺少原生二進位檔或驅動程式過舊。 | 確認 GPU 驅動程式為最新；使用 `-runtime` 旗標重新安裝 NuGet 套件。 |
| **大型圖像記憶體不足** | GPU 記憶體有限。 | 降低圖像解析度（`image = ImagePreprocessor.Resize(image, 2000, 0)`）。 |

提前處理這些問題，可為你節省大量除錯時間。

## 完整可執行範例

以下是完整程式碼，你可以直接複製貼上到新的 Console 應用程式中。它包含上述所有輔助方法。

```csharp
using System;
using System.IO;
using System.Linq;
using System.Text.RegularExpressions;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize GPU‑accelerated OCR engine.
            var ocrEngine = new OcrEngine { Engine = Engine.Gpu };

            // 2️⃣ Define the path to a single image or a folder.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            // string folderPath = @"C:\Invoices";

            // Uncomment one of the following lines:
            PerformOcr(ocrEngine, imagePath);
            // ProcessFolder(ocrEngine, folderPath);
        }

        // -------------------------------------------------
        // Load image, preprocess, recognize, and display.
        // -------------------------------------------------
        static void PerformOcr(OcrEngine engine, string filePath)
        {
            var image = OcrImage.FromFile(filePath);
            image = ImagePreprocessor.AdjustContrast(image, 1.2);
            image = ImagePreprocessor.ConvertToGrayscale(image);

            var result = engine.Recognize(image, Language.English);
            Console.WriteLine("=== OCR RESULT ===");
            Console.WriteLine(result.Text);

            ExtractTotalAmount(result.Text);
        }

        // -------------------------------------------------
        // Bulk processing of a folder.
        // -------------------------------------------------
        static void ProcessFolder(OcrEngine engine, string folderPath)
        {
            foreach (var file in Directory.EnumerateFiles(folderPath, "*.*")
                                          .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
            {
                Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
                var img = OcrImage.FromFile(file);
                var res = engine.Recognize(img, Language.English);
                Console.WriteLine(res.Text);
                ExtractTotalAmount(res.Text);
            }
        }

        // -------------------------------------------------
        // Simple regex to pull the total amount from an invoice.
        // -------------------------------------------------
        static void ExtractTotalAmount(string ocrText)
        {
            var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
            if (match.Success)
                Console.WriteLine($"Detected total: {match.Value}");
            else
                Console.WriteLine("Total amount not found.");
        }
    }
}
```

**執行它** (` 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}