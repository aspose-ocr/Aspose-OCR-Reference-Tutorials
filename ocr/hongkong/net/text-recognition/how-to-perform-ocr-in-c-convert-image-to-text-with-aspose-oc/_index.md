---
category: general
date: 2026-05-21
description: 如何在 C# 中使用 Aspose OCR 執行光學字元辨識 – 學習將圖像轉換為文字、從 jpg 讀取文字，以及快速且可靠地載入圖像進行
  OCR。
draft: false
keywords:
- how to perform OCR
- convert image to text
- read text from jpg
- how to extract text from image
- load image for OCR
language: zh-hant
og_description: 如何在 C# 中使用 Aspose OCR 執行文字辨識。本指南將逐步示範如何將影像轉換為文字、從 jpg 讀取文字，以及載入影像進行
  OCR。
og_title: 如何在 C# 中執行 OCR – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: How to perform OCR in C# using Aspose OCR – learn to convert image
    to text, read text from jpg, and load image for OCR quickly and reliably.
  headline: How to Perform OCR in C# – Convert Image to Text with Aspose OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中執行 OCR – 使用 Aspose OCR 將圖像轉換為文字
url: /zh-hant/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-text-with-aspose-oc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中執行 OCR – 完整指南

曾經想過 **如何在 C# 應用程式中執行 OCR**，卻不想與低階影像處理糾纏嗎？你並不孤單。許多開發者都需要一種可靠的方式來 **將影像轉換為文字**，尤其是在處理掃描文件或收據照片時。本教學將一步步說明如何載入影像以供 OCR、執行辨識引擎，最後讀取擷取出的文字——全部使用 Aspose OCR。

我們也會說明如何 **從 jpg 讀取文字**，討論 **如何從影像中擷取文字** 的細節，並提供一張快速備忘錄，說明 **載入影像以供 OCR** 的情境。完成後，你將擁有一個可直接放入任何 .NET 專案的即用範例。

## 前置條件

在開始之前，請確保你具備以下條件：

- .NET 6.0 或更新版本（程式碼同時支援 .NET Core 與 .NET Framework）
- Visual Studio 2022 或你慣用的任何 IDE
- Aspose OCR for .NET 授權檔（可選，但建議使用以取得完整功能）
- 一張範例影像（例如 `sample.jpg`），放置於已知資料夾
- 可連網以取得 NuGet 套件 `Aspose.OCR`

如果上述項目有任何不熟悉的，別擔心——我們會在教學中逐一說明。

## 步驟 1 – 透過 NuGet 安裝 Aspose OCR

首先需要取得 Aspose OCR 函式庫。開啟套件管理員主控台並執行：

```powershell
Install-Package Aspose.OCR
```

或是使用 CLI：

```bash
dotnet add package Aspose.OCR
```

> **小技巧：** 加入套件會自動還原所有相依性，無需手動搜尋其他 DLL。

## 步驟 2 – 載入影像以供 OCR

函式庫安裝完成後，我們需要 **載入影像以供 OCR**。這一步相當重要，因為引擎期待的是 `ImageStream` 物件，而非單純的檔案路徑。

```csharp
using Aspose.OCR;

// Assume the image lives in the same folder as the executable
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "sample.jpg");

// Create an ImageStream from the file
ImageStream imgStream = ImageStream.FromFile(imagePath);
```

請注意我們使用 `AppDomain.CurrentDomain.BaseDirectory` 來組合完整路徑。這樣的寫法在 Visual Studio、主控台或已發佈的 exe 中都能保持穩定。此外，`ImageStream` 類別支援多種格式，你可以輕鬆 **從 jpg、png 或 bmp 讀取文字**。

## 步驟 3 – 在已載入的影像上執行 OCR

以下是本教學的核心——**如何在已載入的影像上執行 OCR**，並將語言設定為英文；如有需要，可將 `OcrLanguage.English` 替換為其他支援語言。

```csharp
// Step 3: Create an OCR engine and specify the language
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,
    Image = imgStream // assign the previously loaded image
};

// Optionally, apply your license to unlock the full feature set
var license = new License();
license.SetLicense(@"YOUR_DIRECTORY\Aspose.OCR.NET.lic");

// Run the recognition process
ocrEngine.Recognize();
```

為什麼要在呼叫 `Recognize()` 之前設定 `Image` 屬性？引擎必須先取得有效的影像來源，否則會拋出 `NullReferenceException`。將步驟 2 中建立的 `ImageStream` 指派給 `Image`，即可確保執行順暢。

## 步驟 4 – 取得並顯示擷取的文字（將影像轉換為文字）

引擎完成辨識後，辨識結果會存放在 `Text` 屬性中。這就是 **將影像轉換為文字** 的魔法所在。

```csharp
// Step 4: Get the recognized text
string extractedText = ocrEngine.Text;

// Display it in the console
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(extractedText);
```

典型的輸出可能如下所示：

```
=== OCR Result ===
Invoice #12345
Date: 2026-04-30
Total: $1,250.00
Thank you for your business!
```

如果影像模糊或字型複雜，可能會出現亂碼。此時可考慮調整引擎的 `Resolution` 屬性，或在送入 OCR 前先對影像做前處理（例如二值化）。

## 步驟 5 – 進階：使用自訂設定從影像中擷取文字

有時預設設定不足以應付需求。以下提供幾項調整，協助解決 **如何從影像中擷取文字** 時的困難。

```csharp
// Increase DPI for better accuracy on low‑resolution images
ocrEngine.Image = ImageStream.FromFile(imagePath);
ocrEngine.Image.DpiX = 300;
ocrEngine.Image.DpiY = 300;

// Enable auto‑rotate if the image might be skewed
ocrEngine.AutoRotate = true;

// Restrict recognition to a specific character set (e.g., digits only)
ocrEngine.RecognitionSettings.Characters = "0123456789.-";
```

這些微調在處理收據、表單或掃描表格時，往往能顯著提升辨識效果。請記住，**如何執行 OCR** 並非一刀切；你需要根據來源素材不斷嘗試不同設定。

## 步驟 6 – 讀取 JPG 檔案文字時的常見陷阱

即使使用功能完整的函式庫，開發者仍會遇到各種障礙。以下列出在 **從 jpg 讀取文字** 時可能遭遇的問題與快速解法：

| 問題 | 為何會發生 | 快速解決方案 |
|------|------------|--------------|
| **對比度低** | JPG 壓縮會平坦顏色，使文字與背景難以區分。 | 使用對比度增強濾鏡前處理影像（如 `ImageSharp` 或 `System.Drawing`）。 |
| **方向錯誤** | 手機有時只儲存方向資訊，未實際旋轉像素。 | 設定 `ocrEngine.AutoRotate = true` 或在 OCR 前手動旋轉影像。 |
| **檔案過大** | 超高解析度的 JPG 佔用記憶體，導致辨識緩慢。 | 在載入前將影像縮小至合理 DPI（例如 300 DPI）。 |

將上述要點記在心中，能在日後 **載入影像以供 OCR** 於正式環境時，為你省下大量除錯時間。

## 步驟 7 – 完整程式碼：單一檔案範例

以下提供完整、可直接執行的程式碼範例。將它貼到新的 Console 專案中，按 **F5** 即可執行。

```csharp
using System;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣  Set up license (optional but recommended)
        // -------------------------------------------------
        var license = new License();
        // Replace with your actual license path or comment out for trial mode
        license.SetLicense(@"YOUR_DIRECTORY\Aspose.OCR.NET.lic");

        // -------------------------------------------------
        // 2️⃣  Load the image you want to process
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "sample.jpg");
        ImageStream imgStream = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // 3️⃣  Create OCR engine – this is where we **perform OCR**
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            Image = imgStream,
            AutoRotate = true   // helpful for photos taken at odd angles
        };

        // -------------------------------------------------
        // 4️⃣  Run recognition
        // -------------------------------------------------
        ocrEngine.Recognize();

        // -------------------------------------------------
        // 5️⃣  Retrieve and display the result – **convert image to text**
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

**預期輸出**（假設 `sample.jpg` 包含清晰的英文文字）：

```
=== OCR Result ===
Hello, world!
This is a sample image for OCR testing.
```

若輸出為空白，請再次確認影像路徑是否正確，且檔案未損毀。

## 結論

現在你已掌握 **如何在 C# 中執行 OCR**，從安裝套件、**載入影像以供 OCR**、執行辨識引擎，到最後 **將影像轉換為文字** 的完整流程。本文亦提供了 **從 jpg 讀取文字** 的實用技巧，並解答了 **如何從影像中擷取文字** 的常見疑問。

接下來可以嘗試先將 PDF 轉為影像再進行 OCR、實驗多語言辨識，或將 OCR 步驟整合至更大的文件處理流水線。可能性無窮，而你已具備堅實的基礎，能夠應對任何文字擷取挑戰。

如有任何問題或發現好用的技巧，歡迎留言分享——祝開發順利！

![How to perform OCR example](/images/ocr-example.png "How to perform OCR in C# – visual overview")


## 相關教學

- [使用 Aspose.OCR 於 C# 進行語言選擇的影像文字擷取](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [將影像轉換為文字 – 從 URL 執行 OCR](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [如何 OCR 影像 – 在 OCR 影像辨識中執行 OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}