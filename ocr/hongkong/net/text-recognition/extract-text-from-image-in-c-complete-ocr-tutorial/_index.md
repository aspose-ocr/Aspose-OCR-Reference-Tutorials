---
category: general
date: 2026-06-06
description: 使用 C# OCR 從圖像提取文字。學習如何載入圖像進行 OCR、辨識掃描文件，並在數分鐘內獲得精確結果。
draft: false
keywords:
- extract text from image
- load image for OCR
- recognize scanned document
- c# OCR tutorial
language: zh-hant
og_description: 使用 C# 從圖像提取文字。本教學示範如何載入圖像進行 OCR、辨識掃描文件，並一步步掌握 C# OCR 教程。
og_title: 在 C# 中從圖像提取文字 – 完整 OCR 指南
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from image using C# OCR. Learn how to load image for OCR,
    recognize scanned document, and get accurate results in minutes.
  headline: Extract Text from Image in C# – Complete OCR Tutorial
  type: TechArticle
- description: Extract text from image using C# OCR. Learn how to load image for OCR,
    recognize scanned document, and get accurate results in minutes.
  name: Extract Text from Image in C# – Complete OCR Tutorial
  steps:
  - name: Save the code as `Program.cs` inside a new console project.
    text: Save the code as `Program.cs` inside a new console project.
  - name: Open a terminal at the project root.
    text: Open a terminal at the project root.
  - name: Run `dotnet add package Aspose.OCR` (if you haven’t already).
    text: Run `dotnet add package Aspose.OCR` (if you haven’t already).
  - name: 'Build and execute:'
    text: 'Build and execute:'
  type: HowTo
- questions:
  - answer: Yes—most OCR libraries let you load a PDF page as an image stream or expose
      a `PdfDocument` API. Convert each page to an image first, then follow the same
      steps.
    question: Can I process PDFs directly?
  - answer: The `ImageStream.FromFile` method supports JPEG, PNG, BMP, and TIFF out
      of the box. No extra conversion required.
    question: What if my image is in PNG format?
  - answer: Handwriting is a tougher nut to crack. Look for a library that offers
      a “handwriting” model, or pre‑process the image with binarization and noise
      removal before feeding it to the engine.
    question: How do I improve accuracy for handwritten notes?
  - answer: 'Absolutely. Most engines expose a `Rect` or `Region` property where you
      can limit OCR to a bounding box—great for forms with fixed fields. --- ## Next
      Steps & Related Topics Now that you’ve mastered the basics of **extract text
      from image** with a **c# OCR tutorial**, consider exploring: - **Batch p'
    question: Is there a way to extract text in a specific region?
  type: FAQPage
tags:
- OCR
- C#
- Image Processing
title: 在 C# 中從圖像提取文字 – 完整 OCR 教學
url: /zh-hant/net/text-recognition/extract-text-from-image-in-c-complete-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從圖像中提取文字（C#） – 完整 OCR 教學

有沒有想過只用幾行 C# 就能 **從圖像中提取文字**？你並不孤單。許多開發者在需要從雜訊多、傾斜的掃描圖中抽取文字時會卡關，而一般的「複製貼上」技巧根本無法解決。  

在本指南中，我們將逐步說明實用的 **c# OCR 教學**，示範如何 **load image for OCR**、啟用智慧前處理，最後 **recognize scanned document** 內容，達到晶瑩剔透的準確度。完成後，你將擁有一個可直接放入任何 .NET 專案的可執行程式。

## 本教學涵蓋內容

- 安裝 Aspose.OCR（或相容）NuGet 套件  
- 建立並設定 OCR 引擎實例  
- **Load image for OCR** – 處理檔案路徑、串流以及常見陷阱  
- 啟用自動前處理以修正傾斜、去噪與對比度問題  
- **Recognize scanned document** – 取得純文字結果  
- 完整的原始程式碼，可直接 copy‑paste 並立即執行  

不需要任何 OCR 前置經驗；只要具備 C# 與 Visual Studio（或你慣用的 IDE） 的基本概念即可。

> **為何在乎？** 自動化文字提取可應用於發票處理、可搜尋的 PDF、減少資料輸入，甚至打造 AI 可用的資料集。

![使用 C# OCR 從圖像提取文字](/images/extract-text-from-image-csharp.png "從圖像提取文字")

## 前置條件

- .NET 6.0 SDK 或更新版本（此程式碼亦支援 .NET Framework 4.8）  
- Visual Studio 2022（Community 版亦可使用）  
- NuGet 套件 `Aspose.OCR`（或任何提供 `OcrEngine`、`OcrResult` 等的函式庫）  

如果尚未安裝套件，請執行以下指令：

```bash
dotnet add package Aspose.OCR
```

此單一指令會下載所有執行高效能 OCR 所需的原生二進位檔案。

---

## 步驟 1：建立 OCR 引擎實例

首先要啟動負責繁重運算的引擎。把 `OcrEngine` 想成整個流程的核心——啟動後即可餵入圖像並請求文字。

```csharp
using Aspose.OCR;          // Namespace for OCR classes
using Aspose.OCR.Image;    // For ImageStream helper

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **專業提示：** 若一次批次處理大量圖像，請將引擎設為 singleton；它會重複使用內部資源，提升效能。

## 步驟 2：啟用自動前處理

實務上的掃描圖很少完美，常有傾斜、雜訊或對比度不足。啟用 `AutoPreprocess` 後，引擎會在辨識字元前自動校正傾斜、去除雜訊並調整對比度。

```csharp
// Step 2: Enable automatic preprocessing (deskew, denoise, contrast adjustment)
ocrEngine.Config.AutoPreprocess = true;
```

為何這麼重要？若未經前處理，OCR 引擎可能把「8」誤讀為「B」或完全漏掉某行。自動化步驟可免除自行撰寫影像清理程式的麻煩。

## 步驟 3：設定辨識語言

大多數 OCR 函式庫皆附帶語言套件。此處設定為英文，但可依文件需求切換至 `OcrLanguage.French`、`OcrLanguage.Spanish` 等。

```csharp
// Step 3: Set the language for recognition
ocrEngine.Language = OcrLanguage.English;
```

若掃描文件包含多種語言，可將引擎執行兩次或使用多語言模型——這是之後可深入探討的方向。

## 步驟 4：載入圖像以供 OCR

現在我們 **load image for OCR**。`ImageStream.FromFile` 輔助方法會將檔案讀入引擎可辨識的格式。請確認路徑指向真實檔案；在專案資料夾執行時相對路徑亦可使用。

```csharp
// Step 4: Load the image to be processed
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **常見錯誤：** 路徑含空格卻未加引號會導致 `FileNotFoundException`。在將檔案交給引擎前，務必使用 `File.Exists` 確認檔案是否存在。

## 步驟 5：執行 OCR 辨識

完成所有設定後，我們終於 **recognize scanned document** 內容。`Recognize` 方法負責主要運算，並回傳包含擷取文字與信心分數的 `OcrResult` 物件。

```csharp
// Step 5: Perform OCR recognition
OcrResult ocrResult = ocrEngine.Recognize();
```

若需取得每行的信心等級，可檢查 `ocrResult.Confidence`（介於 0 到 1 的浮點數）。信心過低？請考慮調整前處理參數或提供更高解析度的圖像。

## 步驟 6：輸出辨識文字

驗證成功最簡單的方式是將文字輸出至主控台。實際應用中，你可能會寫入檔案、資料庫，或傳遞給其他服務。

```csharp
// Step 6: Output the recognized text
Console.WriteLine(ocrResult.Text);
```

執行程式後應會印出類似以下內容：

```
The quick brown fox jumps over the lazy dog.
```

即使原始圖像稍有傾斜或雜訊，自動前處理也應已將其清理至足以產生乾淨的輸出。

---

## 完整原始程式碼 – 可直接執行範例

以下為完整程式碼，可直接複製到新建的主控台專案（`dotnet new console`）中。它包含上述所有步驟，並加入少量錯誤處理，使教學更健全。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace ExtractTextFromImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Validate input argument
            if (args.Length == 0)
            {
                Console.WriteLine("Usage: dotnet run <image-path>");
                return;
            }

            string imagePath = args[0];

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found at '{imagePath}'");
                return;
            }

            try
            {
                // Step 1: Create OCR engine
                OcrEngine ocrEngine = new OcrEngine();

                // Step 2: Enable auto‑preprocess (deskew, denoise, contrast)
                ocrEngine.Config.AutoPreprocess = true;

                // Step 3: Choose language (English in this case)
                ocrEngine.Language = OcrLanguage.English;

                // Step 4: Load image for OCR
                ocrEngine.Image = ImageStream.FromFile(imagePath);

                // Step 5: Recognize scanned document
                OcrResult result = ocrEngine.Recognize();

                // Step 6: Output the extracted text
                Console.WriteLine("\n--- Extracted Text ---\n");
                Console.WriteLine(result.Text);
                Console.WriteLine("\n--- End of Output ---\n");

                // Optional: Show confidence if you need it
                Console.WriteLine($"Overall confidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### 執行方式

1. 將程式碼儲存為 `Program.cs`，放入新建的主控台專案中。  
2. 在專案根目錄開啟終端機。  
3. 執行 `dotnet add package Aspose.OCR`（若尚未安裝）。  
4. 建置並執行：  

   ```bash
   dotnet run "C:\Images\invoice_scanned.jpg"
   ```

你應該會在主控台看到擷取的文字，以及整體的信心百分比。

---

## 常見問題 (FAQs)

**Q: 可以直接處理 PDF 嗎？**  
A: 可以——大多數 OCR 函式庫允許將 PDF 頁面載入為影像串流，或提供 `PdfDocument` API。先將每頁轉為影像，再依照相同步驟處理。

**Q: 如果我的圖像是 PNG 格式呢？**  
A: `ImageStream.FromFile` 方法本身支援 JPEG、PNG、BMP 與 TIFF，無需額外轉換。

**Q: 如何提升手寫筆記的辨識精度？**  
A: 手寫文字較難辨識。可尋找提供「handwriting」模型的函式庫，或在送入引擎前先以二值化與去噪方式前處理影像。

**Q: 有辦法只擷取特定區域的文字嗎？**  
A: 當然可以。大多數引擎提供 `Rect` 或 `Region` 屬性，讓你限制 OCR 於某個矩形範圍——非常適合固定欄位的表單。

---

## 往後步驟與相關主題

既然你已掌握 **extract text from image** 的 **c# OCR 教學** 基礎，接下來可探索以下主題：

- **批次處理** – 迭代目錄中的圖像，將每個結果寫入 CSV 檔。  
- **PDF 產生** – 結合擷取文字與 PDF 函式庫，產生可搜尋的 PDF。  
- **機器學習後處理** – 使用拼寫檢查或語言模型清理 OCR 錯誤。  

上述每項皆以我們先前討論的核心概念為基礎：載入圖像以供 OCR、設定引擎、以及辨識掃描文件。

---

## 結論

我們剛剛完整示範了一個端對端的範例，說明如何在 C# 中 **extract text from image**。從建立 `OcrEngine` 到輸出最終字串，每一行程式碼皆有說明且可直接執行。

只要依照步驟操作，即可在數秒內將雜訊掃描、收據或手寫筆記轉換為可搜尋、可編輯的文字。持續嘗試——調整前處理參數、切換語言，或一次處理多個檔案。自動化文件處理的世界等你探索。

有更多問題或想分享有趣的使用案例嗎？在下方留言吧，祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以示範的技術為基礎。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索不同的實作方式。

- [使用 Aspose.OCR .NET 從圖像提取文字](/ocr/english/net/image-and-drawing-recognition/)
- [使用 Aspose.OCR 的語言選擇功能在 C# 中提取圖像文字](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [從圖像提取文字 – 使用 Aspose.OCR for .NET 進行 OCR 最佳化](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}