---
category: general
date: 2026-01-10
description: 如何快速執行 OCR 並從圖像中提取阿拉伯文字。了解將圖像轉換為文字、從 PNG 讀取文字，以及如何使用 Aspose OCR 提取文字。
draft: false
keywords:
- how to run OCR
- extract arabic text
- convert image to text
- read text from png
- how to extract text
language: zh-hant
og_description: 如何在 C# 中執行 OCR 並從 PNG 圖像中擷取阿拉伯文字。本指南一步一步示範如何將圖像轉換為文字以及從 PNG 讀取文字。
og_title: 如何在 C# 中執行 OCR – 從 PNG 提取阿拉伯文字
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中執行 OCR – 從 PNG 提取阿拉伯文字
url: /zh-hant/net/text-recognition/how-to-run-ocr-in-c-extract-arabic-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中執行 OCR – 從 PNG 提取阿拉伯文字

有沒有想過 **如何執行 OCR** 在包含阿拉伯字元的圖片上？你並不孤單。許多開發者在需要 **從 PNG 提取阿拉伯文字** 時卡住了，卻不知道哪個函式庫能順利處理從右至左的腳本。

在本教學中，我們將逐步說明使用 Aspose.OCR 在乾淨的 C# 主控台應用程式中 **將影像轉換為文字**、**從 PNG 讀取文字**，以及最終 **如何提取文字** 所需的全部知識。完成後，你將擁有一個可直接執行的程式，會在終端機上印出阿拉伯字串。

## 你將學到

- 安裝並參考 Aspose.OCR NuGet 套件。  
- 為阿拉伯語言支援設定 OCR 引擎。  
- 載入 PNG 影像並執行辨識程序。  
- 取得並顯示提取的文字。  
- 微調設定以提升準確度並處理常見陷阱。

不需要任何 OCR 的先前經驗，只要具備 C# 基礎知識以及 .NET 開發環境（Visual Studio、Rider，或 `dotnet` CLI 都可以）。

---

## 如何執行 OCR – 設定 Aspose OCR

### 步驟 1：加入 Aspose.OCR NuGet 套件

我們首先需要的就是 OCR 函式庫本身。Aspose.OCR 為商業產品，但提供免費試用版，足以用於學習目的。

```bash
# Using the .NET CLI
dotnet add package Aspose.OCR
```

或者，在 Visual Studio 中開啟 **NuGet 套件管理員**，搜尋 **Aspose.OCR**，然後點擊 **Install**。

> **專業提示：** 若你打算在 CI 流程中使用此函式庫，請加入 `-v` 參數以鎖定版本，例如 `dotnet add package Aspose.OCR -v 23.10`。

### 步驟 2：建立新主控台專案（如果尚未有的話）

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
```

現在你已擁有一個全新的 `Program.cs` 檔案，可供我們撰寫程式碼。

---

## 提取阿拉伯文字 – 撰寫 OCR 程式碼

以下是完整且可直接執行的程式。請將其儲存為 `Program.cs`（或取代自動產生的檔案）。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Config;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // Step 2: Choose the language for recognition.
            // Here we use Arabic. You can swap this for
            // OcrLanguage.Korean, OcrLanguage.SerbianCyrillic, etc.
            // -------------------------------------------------
            ocrEngine.Language = OcrLanguage.Arabic;

            // -------------------------------------------------
            // Step 3: Load the image containing the text.
            // Replace the path with the location of your PNG.
            // -------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/arabic_sample.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // Step 4: Run the OCR process.
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 5: Display the extracted text.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Arabic Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### 為何每行程式碼都重要

- **`OcrEngine`**：協調影像載入、語言選擇與辨識的核心類別。  
- **`Language = OcrLanguage.Arabic`**：阿拉伯語使用從右至左的腳本與獨特字形；設定語言可讓引擎套用正確的字元模型。  
- **`ImageStream.FromFile`**：支援 PNG、JPEG、BMP 等多種格式。若需從 `MemoryStream`（例如上傳的檔案）讀取，請相應替換此呼叫。  
- **`Recognize()`**：執行繁重的工作——像素分析、分割與字元分類。  
- **`ocrEngine.Text`**：最終的 Unicode 字串，可供後續處理、儲存或顯示。

### 預期輸出

如果 `arabic_sample.png` 包含短語 “مرحبا بالعالم”（Hello World），主控台將會印出：

```
=== Extracted Arabic Text ===
مرحبا بالعالم
```

如果輸出呈現亂碼，請再次確認影像是否清晰、語言是否設定為 Arabic，以及 OCR 引擎版本是否符合文件說明。

---

## 影像轉文字 – 微調準確度

雖然預設設定適用於大多數乾淨的掃描檔，但實務上的影像常常需要額外的調整。

| Setting | 功能說明 | 使用時機 |
|---------|----------|----------|
| `ocrEngine.Config.Preprocess = true` | 啟用自動二值化與除噪。 | 有陰影的掃描文件。 |
| `ocrEngine.Config.Deskew = true` | 旋轉影像以校正輕微傾斜。 | 角度拍攝的照片。 |
| `ocrEngine.Config.PageSegMode = PageSegMode.SingleBlock` | 將整張影像視為單一文字區塊。 | 簡單說明或單行標籤。 |
| `ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزس شصضطظعغفقكلمنهوية"` | 僅限制辨識阿拉伯字元。 | 減少混合語言頁面的誤判。 |

你可以在建立引擎後立即加入以下程式碼：

```csharp
ocrEngine.Config.Preprocess = true;
ocrEngine.Config.Deskew = true;
ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزسشصضطظعغفقكلمنهوية";
```

---

## 從 PNG 讀取文字 – 處理不同的影像來源

有時 PNG 可能儲存在資料庫中或來自網路請求。以下是一個快速範例，從 `byte[]` 讀取：

```csharp
byte[] pngBytes = File.ReadAllBytes("YOUR_DIRECTORY/arabic_sample.png");
using var ms = new MemoryStream(pngBytes);
ocrEngine.Image = ImageStream.FromStream(ms);
ocrEngine.Recognize();
Console.WriteLine(ocrEngine.Text);
```

其餘流程保持相同，這表示 **如何提取文字** 在任何來源下皆一致。

---

## 如何提取文字 – 進階選項與邊緣案例

### 1. 多頁 PDF 或 TIFF

如果需要對多頁文件執行 OCR，請對每頁迴圈處理：

```csharp
var pdfDoc = new Aspose.Pdf.Document("multi_page.pdf");
foreach (var page in pdfDoc.Pages)
{
    using var img = page.ConvertToImage();
    ocrEngine.Image = ImageStream.FromBitmap(img);
    ocrEngine.Recognize();
    Console.WriteLine($"Page {page.Number}: {ocrEngine.Text}");
}
```

> **注意：** 此程式碼片段需要 `Aspose.PDF` 套件。

### 2. 自動偵測語言

Aspose.OCR 亦提供自動偵測功能，但速度較慢。若不確定影像是阿拉伯語或其他腳本，請啟用此功能：

```csharp
ocrEngine.Language = OcrLanguage.AutoDetect;
```

引擎會嘗試每個語言模型，並挑選最相符的結果。

### 3. 效能建議

- **重複使用 `OcrEngine`** 物件以處理多張影像；每次重新建立實例會增加額外負擔。  
- **平行執行** 時，必須為每個執行緒提供獨立的引擎實例——共享同一實例會導致競爭條件。

---

## 結論

我們已從頭到尾說明了在 C# 中 **如何執行 OCR**，示範了 **提取阿拉伯文字**、**影像轉文字**、**從 PNG 讀取文字**，以及在各種情境下 **如何提取文字**。範例程式碼完整、獨立，隨時可貼入任何 .NET 主控台專案中使用。

接下來的步驟？嘗試將 `OcrLanguage.Arabic` 改為 Korean 或 Serbian Cyrillic，體驗函式庫的多語言能力。可實驗前處理旗標以提升噪點掃描的準確度，或將 OCR 程式整合至 Web API，讓使用者上傳影像即時取得文字結果。

祝程式開發順利，願你的 OCR 結果永遠清晰如水晶！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}