---
category: general
date: 2026-04-03
description: 使用 Aspose OCR 於 C# 從圖像提取文字。學習如何轉換掃描圖像、在 C# 載入圖像檔案，並非同步辨識 TIF 文字。
draft: false
keywords:
- extract text from image
- convert scanned image
- how to ocr image
- load image file c#
- recognize text from tif
language: zh-hant
og_description: 使用 Aspose OCR 在 C# 中從圖像提取文字。此指南示範如何轉換掃描圖像、載入圖像檔案（C#），以及使用非同步呼叫從 TIF
  識別文字。
og_title: 在 C# 中從圖像提取文字 – 非同步 OCR 教學
tags:
- OCR
- C#
- Aspose
- Async
title: 在 C# 中從圖片提取文字 – 非同步 OCR 教學
url: /zh-hant/net/text-recognition/extract-text-from-image-in-c-async-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從影像中提取文字（C#）– 非同步 OCR 教程

需要快速 **從影像中提取文字** 嗎？使用 Aspose OCR，您可以在 C# 中透過非同步呼叫完成，整個過程在您還沒喝完咖啡前就結束了。  
如果您同時想知道如何 **convert scanned image** 檔案或在 C# 中載入影像檔而不費吹灰之力，您來對地方了。

在本指南中，我們將逐步說明每個步驟——從磁碟中讀取 TIF 檔案到取得乾淨、可搜尋的文字。完成後，您將能夠 **recognize text from TIF** 檔案，了解載入不同影像格式的細節，並擁有一套可在任何 .NET 專案中重複使用的穩固非同步模式。

## 您將學到

* 如何設定 Aspose OCR 引擎以供非同步使用。  
* 取得以 **load image file C#** 方式載入影像檔的完整程式碼，並包含缺少檔案時的錯誤處理。  
* 將 **convert scanned image** PDF 或 TIFF 轉換為 Aspose 可讀取的位圖的方法。  
* 為何 async OCR (`RecognizeAsync`) 比同步版本更快且具可擴充性。  
* 預期的主控台輸出以及如何驗證提取的文字與來源相符。  

> **專業提示：** 若您一次處理數十頁，請在多次呼叫間保持 OCR 引擎持續運作——每次重新建立實例會增加不必要的開銷。

## 非同步提取影像文字

解決方案的核心在於一個非同步的 `Main` 方法。使用 `await` 可讓 UI 執行緒保持空閒（或在主控台應用程式中釋放執行緒池），同時 OCR 引擎執行繁重的工作。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.Threading.Tasks;

class AsyncDemo
{
    static async Task Main()
    {
        // 1️⃣ Create an instance of the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        Image inputImage = Image.FromFile(@"YOUR_DIRECTORY/input.tif");

        // 3️⃣ Run asynchronous OCR recognition (returns a Task<string>)
        string recognizedText = await ocrEngine.RecognizeAsync(inputImage);

        // 4️⃣ Display the OCR result
        Console.WriteLine("Async OCR result:");
        Console.WriteLine(recognizedText);
    }
}
```

**為何使用非同步？** OCR 操作可能涉及網路 I/O（若引擎使用雲端服務）或密集的 CPU 工作。`RecognizeAsync` 釋放呼叫執行緒，使其他工作（例如處理更多檔案）得以繼續。

### 預期輸出

```
Async OCR result:
The quick brown fox jumps over the lazy dog.
```

如果影像包含多行文字，每行會以換行字元分隔。若需要永久儲存，可使用 `File.WriteAllText("output.txt", recognizedText);` 將結果寫入檔案。

## 將掃描影像轉換為可用格式

有時您會收到掃描的 PDF 或多頁 TIFF。Aspose OCR 最適合使用 `System.Drawing.Image`，因此可能需要先進行轉換。

```csharp
using Aspose.OCR;
using System.Drawing;
using System.Drawing.Imaging;

// Load a multi‑page TIFF and pick the first frame
Image tiff = Image.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
tiff.SelectActiveFrame(FrameDimension.Page, 0); // Grab page 0

// Optionally, change DPI for better accuracy
var bitmap = new Bitmap(tiff);
bitmap.SetResolution(300, 300); // 300 DPI is a sweet spot for OCR
```

> **為何要變更 DPI？** 較高的解析度能提供 OCR 引擎更多細節，減少模糊掃描的誤辨識。只要不要超過 600 DPI——大多數引擎不會因此提升精度，卻會佔用更多記憶體。

## 載入影像檔案 C# – 處理不同格式

您可能會想硬編碼 `.tif` 路徑，但穩健的工具應接受 **any** 影像類型（`.png`、`.jpg`、`.bmp`）。以下是一個小型輔助函式，將載入邏輯抽象化：

```csharp
static Image LoadImage(string path)
{
    if (!File.Exists(path))
        throw new FileNotFoundException($"Image not found: {path}");

    // Let .NET decide the correct decoder based on file header
    using (var stream = File.OpenRead(path))
    {
        return Image.FromStream(stream);
    }
}
```

使用方式如下：

```csharp
Image img = LoadImage(@"YOUR_DIRECTORY/input.tif");
string text = await ocrEngine.RecognizeAsync(img);
```

現在您已涵蓋 **load image file C#** 的情境，無需擔心具體副檔名。

## 從 TIF 辨識文字 – 必備知識

TIF 檔案常包含多頁或使用某些壓縮方式，會讓部分函式庫感到困惑。以下兩點可協助您取得可靠結果：

1. **Select the correct frame** – 如前所示使用 `SelectActiveFrame`。  
2. **Normalize colors** – 轉換為 24 位元 RGB 位圖可消除異常調色盤。  

```csharp
static Image PrepareTif(string tifPath, int pageIndex = 0)
{
    Image tif = Image.FromFile(tifPath);
    tif.SelectActiveFrame(FrameDimension.Page, pageIndex);
    // Convert to 24‑bit RGB to avoid palette issues
    Bitmap rgb = new Bitmap(tif.Width, tif.Height, PixelFormat.Format24bppRgb);
    using (Graphics g = Graphics.FromImage(rgb))
    {
        g.DrawImage(tif, 0, 0, tif.Width, tif.Height);
    }
    return rgb;
}
```

將回傳的 `Image` 直接傳入 `RecognizeAsync`，即使來源使用 CCITT Group 4 壓縮，您也能可靠地 **recognize text from TIF**。

## 完整端對端範例

將所有內容整合後，您會得到一個可直接放入主控台專案並執行的單一檔案。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.Drawing.Imaging;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        try
        {
            // Step 1 – Initialize OCR engine (reuse if processing many files)
            OcrEngine ocrEngine = new OcrEngine();

            // Step 2 – Load and prepare the image (handles TIF, PNG, JPG, etc.)
            Image img = PrepareImage(@"YOUR_DIRECTORY/input.tif");

            // Step 3 – Run async recognition
            string result = await ocrEngine.RecognizeAsync(img);

            // Step 4 – Output the result
            Console.WriteLine("Async OCR result:");
            Console.WriteLine(result);

            // Optional: Save to a text file
            File.WriteAllText("ocr-output.txt", result);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }

    // Helper that decides how to load based on extension
    static Image PrepareImage(string path)
    {
        string ext = Path.GetExtension(path).ToLowerInvariant();
        return ext switch
        {
            ".tif" or ".tiff" => PrepareTif(path),
            _ => LoadImage(path)
        };
    }

    static Image LoadImage(string path)
    {
        if (!File.Exists(path))
            throw new FileNotFoundException($"Image not found: {path}");

        using var stream = File.OpenRead(path);
        return Image.FromStream(stream);
    }

    static Image PrepareTif(string tifPath, int page = 0)
    {
        Image tif = Image.FromFile(tifPath);
        tif.SelectActiveFrame(FrameDimension.Page, page);
        Bitmap rgb = new Bitmap(tif.Width, tif.Height, PixelFormat.Format24bppRgb);
        using var g = Graphics.FromImage(rgb);
        g.DrawImage(tif, 0, 0, tif.Width, tif.Height);
        return rgb;
    }
}
```

**您應該會看到：** 主控台會印出提取的文字，且在執行檔旁會產生名為 `ocr-output.txt` 的檔案，內含相同的字串。

## 常見問題與邊緣情況

| Question | Answer |
|----------|--------|
| *我可以直接 OCR PDF 嗎？* | Aspose OCR 僅適用於影像，因此您必須先將每頁 PDF 轉換為影像（例如使用 Aspose.PDF 或 `PdfRenderer`）。 |
| *如果影像太大怎麼辦？* | 在 OCR 前將尺寸縮小至最大 2500 px 的寬度/高度；Aspose 會在內部自動調整大小，但您可節省記憶體。 |
| *非同步方法是否執行緒安全？* | 是的，但僅在未同時呼叫 `RecognizeAsync` 時才重複使用同一個 `OcrEngine` 實例。若進行平行處理，請為每個任務建立獨立的引擎。 |
| *我需要授權嗎？* | Aspose OCR 提供帶有浮水印的免費評估版。正式環境請購買授權，並透過 `License license = new License(); license.SetLicense("Aspose.OCR.lic");` 設定。 |

## 結論

您現在已了解如何在 C# 中使用 Aspose OCR 的非同步 API **extract text from image** 檔案。透過處理影像載入、掃描影像的可選轉換以及 TIF 檔案的特殊情況，此解決方案既穩健又可直接投入生產。  

接下來您可以：

* **Convert scanned image** PDF 轉為 PNG 後再進行 OCR，可提升準確度。  
* 探索 **how to ocr image** 直接從 Web API 串流的方式，省去暫存檔案的需求。  
* 在 `Parallel.ForEach` 迴圈中重複使用 `OcrEngine` 實例，以批次處理數十個檔案。  

試試看這些變化，您將快速體會非同步 OCR 為大量文件應用帶來的顛覆性效益。祝開發順利，如有任何問題，歡迎留下評論！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}