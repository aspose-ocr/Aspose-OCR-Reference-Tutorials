---
category: general
date: 2026-05-25
description: 如何在 C# 中使用 OCR 從圖像檔案提取文字。只需幾個簡單步驟，即可學會使用 Aspose.OCR 從 JPG 識別中文字符。
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from jpg
- recognize chinese characters
- ocr chinese simplified
language: zh-hant
og_description: 如何在 C# 中使用 OCR 從圖像檔案提取文字。本指南示範如何使用 Aspose.OCR 從 JPG 識別中文字符。
og_title: 如何在 C# 中使用 OCR – 從 JPG 識別中文文字
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: How to use OCR in C# to extract text from image files. Learn to recognize
    Chinese characters from a JPG using Aspose.OCR in a few simple steps.
  headline: How to Use OCR in C# – Recognize Chinese Text from JPG
  type: TechArticle
- description: How to use OCR in C# to extract text from image files. Learn to recognize
    Chinese characters from a JPG using Aspose.OCR in a few simple steps.
  name: How to Use OCR in C# – Recognize Chinese Text from JPG
  steps:
  - name: What’s happening under the hood?
    text: '- **`OcrEngine.Language`** tells Aspose which dictionary to use. By picking
      `ChineseSimplified`, we instruct the engine to look for the Simplified Chinese
      language pack. - **First‑time download**: When `Recognize` runs, the SDK reaches
      out to Aspose’s CDN, pulls the ≈6 MB language file, caches it lo'
  - name: 5.1 Dealing with Low‑Quality Images
    text: 'OCR accuracy drops when the source image is blurry, noisy, or has poor
      lighting. A quick fix is to pre‑process the image:'
  - name: 5.2 Running in a Headless Environment
    text: 'If you’re deploying to a Linux container without a GUI, make sure the `libgdiplus`
      library (required for `System.Drawing`) is installed:'
  - name: 5.3 Caching the Language Pack Manually
    text: You can download the language file once and point Aspose to it via the `License`
      API, which eliminates the one‑time network call. This is handy for offline scenarios.
  - name: Expected Output
    text: 'If the JPG contains the phrase “欢迎光临”, the console will print:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: 如何在 C# 中使用 OCR – 從 JPG 識別中文文字
url: /zh-hant/net/text-recognition/how-to-use-ocr-in-c-recognize-chinese-text-from-jpg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 從 JPG 識別中文文字

有沒有想過 **如何使用 OCR** 從手機拍攝的圖片中提取文字？你並不孤單。在許多實際專案中——例如收據掃描器、翻譯應用程式或自動化資料輸入——你都需要快速且可靠地 **從圖像中提取文字**。

在本教學中，我們將逐步說明一個完整且可執行的範例，該範例 **從 JPG 檔案中識別文字**，甚至能處理使用 **OCR Chinese Simplified** 語言套件的 **中文字符識別**。完成後，你將擁有一個獨立的主控台應用程式，能將偵測到的字串印出到主控台，且不需要額外手動下載。

> **快速說明：** 此程式碼適用於 Aspose.OCR ≥ 23.7，會在首次使用時自動下載語言資源。若使用較舊版本，則需手動加入語言。

## 前置條件

在開始之前，請確保你已具備：

- .NET 6.0 SDK 或更新版本（範例目標為 .NET 6，但 .NET 5 亦可使用）
- 最新版的 Visual Studio 2022 或搭配 C# 擴充功能的 VS Code
- 首次下載語言檔時需要的網際網路連線
- 包含簡體中文文字的 JPG 圖片（此處稱為 `chinese_sign.jpg`）

就這樣——不需要大型 OCR 引擎，也不必處理原生 DLL。只要幾個 NuGet 指令和幾行程式碼即可。

## 第一步：透過 NuGet 安裝 Aspose.OCR

首先，我們需要 OCR 函式庫。於專案資料夾中開啟終端機並執行：

```bash
dotnet add package Aspose.OCR
```

或者，你也可以使用 Visual Studio 介面，於 **Dependencies → Manage NuGet Packages** 右鍵點擊，搜尋 “Aspose.OCR”，然後點選 **Install**。

> **小技巧：** 保持套件為最新版本。每個次要版本都會加入新的語言套件與效能優化。

## 第二步：建立新的主控台專案（如果尚未建立）

如果從頭開始，建立一個全新的主控台應用程式：

```bash
dotnet new console -n OcrChineseDemo
cd OcrChineseDemo
```

現在你已擁有一個 `Program.cs` 檔案，可用於放置 OCR 程式碼。

## 第三步：撰寫 OCR 程式碼 – 從 JPG 識別簡體中文

開啟 `Program.cs`，將其內容替換為下列程式碼。每一行皆有註解，讓你了解 *為何* 這樣做，而不只是 *做了什麼*。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;   // Required for Image.FromFile

namespace OcrChineseDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // --------------------------------------------------------------
            // 1️⃣  Initialise the OCR engine and request the Simplified Chinese
            //     language. This language isn’t bundled in the core package,
            //     so Aspose.OCR will download it the first time you call
            //     Recognize().
            // --------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                // The enum value maps to the language pack name.
                Language = OcrLanguage.ChineseSimplified
            };

            // --------------------------------------------------------------
            // 2️⃣  Load the image you want to process. Replace the path with
            //     the actual location of your JPG file.
            // --------------------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/chinese_sign.jpg";
            using var image = Image.FromFile(imagePath);

            // --------------------------------------------------------------
            // 3️⃣  Perform the recognition. The first call may take a few
            //     seconds because the language resources are being fetched.
            // --------------------------------------------------------------
            string recognizedText = ocrEngine.Recognize(image);

            // --------------------------------------------------------------
            // 4️⃣  Output the result to the console.
            // --------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### 背後的運作原理

- **`OcrEngine.Language`** 告訴 Aspose 要使用哪個字典。選擇 `ChineseSimplified` 後，引擎會尋找簡體中文語言套件。
- **首次下載**：當呼叫 `Recognize` 時，SDK 會連線至 Aspose 的 CDN，下載約 6 MB 的語言檔案，並在本機快取，之後的辨識即時完成。
- **`Image.FromFile`** 能處理 .NET 可解碼的任何點陣圖格式——JPG、PNG、BMP——因此你可以 **從圖像中提取文字**，不僅限於 JPG。

## 第四步：執行應用程式並驗證輸出

建置並執行：

```bash
dotnet run
```

你應該會看到類似以下的結果：

```
=== Recognized Text ===
欢迎光临
```

如果主控台顯示亂碼或空字串，請再次確認以下項目：

1. 圖片確實包含清晰且高對比度的中文字符。
2. 檔案路徑正確（沒有多餘的空格或遺漏副檔名）。
3. 你的機器能連線至 `https://download.aspose.com` 以下載語言套件。

## 第五步：處理邊緣情況與常見陷阱

### 5.1 處理低品質影像

當來源影像模糊、雜訊多或光線不足時，OCR 的準確度會下降。快速的解決方式是先對影像進行前處理：

```csharp
using System.Drawing.Imaging;

// Convert to grayscale
var gray = new Bitmap(image.Width, image.Height);
using (var g = Graphics.FromImage(gray))
{
    var colorMatrix = new ColorMatrix(
        new float[][]{
            new float[]{0.3f,0.3f,0.3f,0,0},
            new float[]{0.59f,0.59f,0.59f,0,0},
            new float[]{0.11f,0.11f,0.11f,0,0},
            new float[]{0,0,0,1,0},
            new float[]{0,0,0,0,1}
        });
    var attributes = new ImageAttributes();
    attributes.SetColorMatrix(colorMatrix);
    g.DrawImage(image, new Rectangle(0,0,image.Width,image.Height),
                0,0,image.Width,image.Height, GraphicsUnit.Pixel, attributes);
}

// Use the processed bitmap for OCR
string recognizedText = ocrEngine.Recognize(gray);
```

### 5.2 在無頭環境執行

如果你將應用程式部署至沒有圖形介面的 Linux 容器，請確保已安裝 `libgdiplus` 函式庫（`System.Drawing` 所必需）。

```bash
apt-get update && apt-get install -y libgdiplus
```

### 5.3 手動快取語言套件

你可以先下載語言檔，然後透過 `License` API 指向該檔案，這樣就能避免一次性的網路下載，對於離線情境相當方便。

```csharp
// Assuming you have the .dat file downloaded to /opt/ocr/langs/
ocrEngine.SetLicense("Aspose.OCR.lic"); // optional if you have a paid license
ocrEngine.LoadLanguage(@" /opt/ocr/langs/ChineseSimplified.dat");
```

## 完整範例（全功能）

以下是可直接複製貼上至 `Program.cs` 的 *完整* 程式碼。沒有隱藏的部份，也不需要外部腳本。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

namespace OcrChineseDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialise OCR engine with Simplified Chinese language
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified
            };

            // Path to the JPG image containing Chinese text
            string imagePath = @"YOUR_DIRECTORY/chinese_sign.jpg";

            // Load the image (ensure the file exists)
            using var image = Image.FromFile(imagePath);

            // Recognize text – first call may download the language pack
            string recognizedText = ocrEngine.Recognize(image);

            // Display the result
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### 預期輸出

若 JPG 包含「欢迎光临」這句話，主控台將會印出：

```
=== Recognized Text ===
欢迎光临
```

你可以自行更換成其他簡體中文招牌、街道名稱或商品標籤——引擎會盡力辨識。

## 結論

我們剛剛說明了在 C# 中 **如何使用 OCR** 來 **從圖像檔案中提取文字**，特別是處理 **在 JPG 中識別中文字符** 的挑戰。透過 Aspose.OCR 即時下載語言的功能，你可以保持部署的輕量化，同時即時支援 **OCR Chinese Simplified**。

接下來可以試試以下想法：

- **批次處理**：遍歷資料夾中的影像，將每個結果寫入 CSV。
- **結合翻譯 API**：將辨識出的字串送至 Azure Translator，實作即時多語言應用程式。
- **探索其他語言**：將 `OcrLanguage.ChineseSimplified` 換成 `Japanese` 或 `Arabic`，觀察相同程式碼的適應情況。

對效能調校、授權或將 OCR 整合至 Web 服務有任何疑問嗎？歡迎在下方留言——祝開發愉快！ 

---

![Screenshot of console output showing how to use OCR in C# to recognize Chinese text from a JPG image](ocr-chinese-demo.png "how to use OCR console output")

## 相關教學

- [使用 Aspose.OCR 進行語言選擇的 C# 圖像文字提取](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [使用 Aspose OCR 識別多語言圖像文字](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [透過設定矩形在 OCR 中提取圖像文字](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}