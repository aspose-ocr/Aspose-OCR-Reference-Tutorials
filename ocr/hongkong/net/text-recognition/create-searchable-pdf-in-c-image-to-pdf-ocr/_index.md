---
category: general
date: 2026-02-28
description: 在 C# 中將多頁 TIFF 轉換為可搜尋的 PDF。本指南示範如何將影像轉換為可搜尋的 PDF，並提供完整的 C# OCR 範例。
draft: false
keywords:
- create searchable pdf
- image to searchable pdf
- convert tiff to pdf
- c# ocr example
- c# image to pdf
language: zh-hant
og_description: 使用 Aspose.OCR 從 TIFF 建立可搜尋的 PDF。跟隨此一步一步的 C# OCR 範例，將圖像轉換為可搜尋的 PDF。
og_title: 在 C# 中建立可搜尋的 PDF – 圖像轉 PDF OCR
tags:
- OCR
- PDF
- C#
- Aspose
title: 在 C# 中建立可搜尋的 PDF – 圖像轉 PDF OCR
url: /zh-hant/net/text-recognition/create-searchable-pdf-in-c-image-to-pdf-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中建立可搜尋的 PDF – 影像轉 PDF OCR

是否曾需要從掃描文件**建立可搜尋的 PDF**，卻不知從何開始？你並非唯一遇到此問題的人。在許多辦公流程中，可搜尋的 PDF 是死檔與可搜尋檔案庫之間的差別。

在本教學中，我們將逐步說明一個完整的**c# ocr example**，將多頁 TIFF 轉換為可搜尋的 PDF，全部使用 Aspose.OCR。完成後，你將清楚知道如何**image to searchable pdf**、如何**convert tiff to pdf**，並擁有一段可直接放入任何 .NET 專案的即用程式碼片段。

## 你將學到

* 如何在 C# 專案中安裝與參考 Aspose.OCR。  
* 載入 TIFF、設定語言並呼叫 `RecognizeToPdf` 的完整步驟。  
* 每個步驟的重要性——從記憶體管理到語言選擇。  
* 處理大型文件的技巧、排除常見 OCR 問題，以及將解決方案擴充至其他影像格式的建議。  

**先決條件** – 最近的 .NET SDK（4.6+ 或 .NET Core 3.1+）、Visual Studio（或你喜愛的 IDE），以及 Aspose.OCR 授權（免費試用版可用於測試）。不需要其他外部函式庫。

---

## 建立可搜尋的 PDF – 概觀

從高層次來看，流程如下：

1. **Initialize** `OcrEngine`。  
2. **Load** 原始影像（此例為 TIFF）。  
3. **Configure** 語言設定以提升準確度。  
4. **Run** OCR 並 **save** 結果直接為可搜尋的 PDF。  

就這樣。Aspose API 會處理繁重的工作，讓你不必自行整合 OCR 與 PDF 函式庫。

---

## 第一步：安裝 Aspose.OCR 並設定專案

首先，加入 Aspose.OCR NuGet 套件：

```bash
dotnet add package Aspose.OCR
```

或者，若你偏好在 Visual Studio 的套件管理員主控台使用：

```powershell
Install-Package Aspose.OCR
```

套件還原完成後，開啟專案檔並確認參考：

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.10.0" />
</ItemGroup>
```

> **專業提示：** 使用最新的穩定版（請至 Aspose 官方網站確認），以取得錯誤修正與最新的語言套件。

---

## 第二步：將 TIFF 轉換為 PDF – 載入影像

現在我們將載入欲轉為可搜尋的 TIFF。Aspose 的 `Image.Load` 方法原生支援多頁 TIFF。

```csharp
using Aspose.OCR;
using System.Drawing;

// Load the multi‑page TIFF. Replace the path with your actual file.
using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");
```

> **為何重要：** 在 `using` 區塊中載入影像可確保未受管理的資源即時釋放——在處理大型文件時尤為關鍵。

---

## 第三步：影像轉可搜尋 PDF – OCR 引擎設定

在執行 OCR 之前，我們會告訴引擎預期的語言。英文適用於大多數情況，但你可以替換為任何 `OcrLanguage` 列舉值。

```csharp
// Create the OCR engine instance
var ocrEngine = new OcrEngine();

// (Optional) Specify language for better accuracy
ocrEngine.Language = OcrLanguage.English;
```

> **專家說明：** 正確選擇語言可大幅降低辨識錯誤。若文件包含多種語言，可使用 `|` 運算子結合，例如 `OcrLanguage.English | OcrLanguage.French`。

---

## 第四步：C# OCR 範例 – 辨識並儲存

引擎就緒後，呼叫 `RecognizeToPdf`。此方法會直接將可搜尋的 PDF 寫入磁碟，並在原始影像後嵌入隱形文字層。

```csharp
// Define the output path for the searchable PDF
string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";

// Perform OCR and write the searchable PDF
ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);
```

執行此行程式碼後，`output.pdf` 會包含原始 TIFF 頁面，並附加一層任何 PDF 閱讀器皆可搜尋的隱藏文字。

---

## 第五步：C# 影像轉 PDF – 驗證結果

讓我們確認一切順利。於 Adobe Reader（或任何檢視器）開啟產生的 PDF，並搜尋在原始 TIFF 中確定存在的字詞。

```csharp
Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
```

若搜尋有結果，代表你已成功**create searchable pdf** 從影像。若無，請再次檢查語言設定或原始 TIFF 的品質。

---

## 完整範例

將所有部件組合起來，以下是一個可自行編譯執行的完整主控台應用程式：

```csharp
using Aspose.OCR;
using System.Drawing;

class SearchablePdfDemo
{
    static void Main()
    {
        // Step 1: Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the multi‑page TIFF
        using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");

        // Step 3: (Optional) Set language for better accuracy
        ocrEngine.Language = OcrLanguage.English;

        // Step 4: Convert the image to a searchable PDF
        string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);

        // Step 5: Inform the user
        System.Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
    }
}
```

**預期輸出**（於主控台）：

```
Searchable PDF created at: C:\MyFolder\output.pdf
```

開啟 `output.pdf`，你應該能在檢視器的搜尋框中輸入原始 TIFF 任意字詞，並看到相符的文字被標示。

---

![Create searchable PDF example](placeholder-image.png){: .align-center alt="create searchable pdf example"}

*上圖顯示在檢視器中開啟的可搜尋 PDF，隱藏文字層已啟用。*

---

## 常見問題與邊緣情況

### 如果我的 TIFF 很大（數百頁）？

Aspose.OCR 會一次串流一頁，但仍可能觸及記憶體上限。建議分批處理 TIFF：

```csharp
for (int i = 0; i < tiffImage.PageCount; i++)
{
    using var singlePage = tiffImage.ExtractPage(i);
    ocrEngine.RecognizeToPdf(singlePage, $"page_{i}.pdf");
}
```

之後，可使用 PDF 函式庫（例如 Aspose.PDF）合併每頁的 PDF。

### 我可以輸出為其他格式，例如可搜尋的 DOCX 嗎？

可以——使用 `RecognizeToDocument` 取代 `RecognizeToPdf`。API 與 PDF 方法相同，只需更改目標檔案副檔名。

### 如何處理非英文語言？

將 `OcrLanguage.English` 替換為相應的列舉，例如 `OcrLanguage.Spanish`。也可以結合多種語言：

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.German;
```

### 密碼保護的 PDF 該怎麼處理？

OCR 步驟完成後，你可以使用 Aspose.PDF 開啟產生的 PDF 並套用加密：

```csharp
var pdfDoc = new Aspose.Pdf.Document(outputPdfPath);
pdfDoc.Encrypt("ownerPassword", "userPassword", 
    Aspose.Pdf.Permissions.All, Aspose.Pdf.EncryptionAlgorithms.AES256);
pdfDoc.Save(outputPdfPath);
```

---

## 重點回顧

我們已說明如何使用 C# 從 TIFF 影像**create searchable PDF**。從安裝 Aspose.OCR、載入影像、設定語言、執行 OCR 到最終驗證可搜尋的輸出，你現在擁有一個可套用於其他格式的完整**c# ocr example**。

如果你想更進一步，請嘗試：

* **Convert TIFF to PDF** 用於非搜尋的檔案庫（只需略過 OCR 步驟）。  
* 嘗試 **image to searchable pdf**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}