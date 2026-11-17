---
category: general
date: 2026-03-29
description: 如何使用 Aspose 的 OCR 從 PNG 檔案提取文字並將圖像轉換為文字。學習 C# 中逐步的非同步 OCR。
draft: false
keywords:
- how to use OCR
- extract text from png
- convert images to text
- extract text from images
language: zh-hant
og_description: 如何在 C# 中使用 Aspose 進行 OCR，從 PNG 檔案提取文字。本指南將帶您了解非同步 OCR、程式碼及技巧。
og_title: 如何在 C# 中使用 OCR – 從 PNG 圖像提取文字
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中使用 OCR – 快速從 PNG 圖像提取文字
url: /zh-hant/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-png-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 快速從 PNG 圖像提取文字

有沒有想過 **如何使用 OCR** 從少量 PNG 截圖中提取文字？也許你有掃描的收據、發票或 UI 模型圖，需要將文字轉成可搜尋的格式。好消息是？使用 Aspose.OCR，只需幾行非同步 C# 程式碼即可將圖像轉換為文字。  

在本教學中，我們將完整示範如何從 PNG 檔案提取文字，說明每一步的原因，並提供一個可直接執行的程式，會為每一頁印出辨識出的文字。完成後，你將能 **從圖像提取文字**，不必再翻閱文件。

## 你將學會

- 安裝並參考 Aspose.OCR NuGet 套件。  
- 初始化 OCR 引擎並設定語言（本例為英文）。  
- 將 PNG 檔案陣列傳入 `RecognizeImagesAsync`，實現快速、非阻塞的處理。  
- 迭代 `OcrResult` 物件並輸出提取的字串。  

不需要外部服務，也不需要複雜的回呼——只要乾淨的 async C#，適用於 .NET 6+。

---

## 前置條件

| 需求 | 原因 |
|-------------|--------|
| .NET 6 SDK（或更新版） | 如 `async Main` 等現代語言功能 |
| Visual Studio 2022 或 VS Code | 用來編譯與執行程式的 IDE |
| Aspose.OCR NuGet 套件（`Aspose.OCR`） | 提供範例中使用的 `OcrEngine` 類別 |
| 幾張 PNG 圖片（`page1.png`、`page2.png`，…） | OCR 處理的輸入檔案 |

如果你已經有 .NET 專案，只要執行 `dotnet add package Aspose.OCR` 即可。否則可使用 `dotnet new console -n OcrDemo` 建立全新主控台應用程式。

---

## 第 1 步：安裝 Aspose.OCR 並設定專案

首先，將 OCR 函式庫加入專案：

```bash
dotnet add package Aspose.OCR
```

**為什麼這很重要**：Aspose.OCR 包含原生 OCR 引擎、語言套件以及簡易的 API。透過 NuGet 取得可確保版本相容性與自動更新。

---

## 第 2 步：初始化 OCR 引擎並選擇語言

引擎必須知道要辨識哪種語言。英文最常用，但你也可以改成 `Language.Spanish`、`Language.French` 等。

```csharp
using Aspose.OCR;

// ...

// Step 2: Create the engine and set the language to English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // Change this if you need a different language
};
```

> **專業提示**：務必明確設定語言；使用預設值可能降低準確度並增加處理時間。

---

## 第 3 步：準備 PNG 檔案清單

你可以傳入單一檔案或陣列。傳入陣列可讓引擎以非同步方式批次處理，特別適合少量頁面。

```csharp
// Step 3: Define the image files you want to process
string[] imagePaths = { "page1.png", "page2.png", "page3.png" };
```

如果圖像放在子資料夾，只需在路徑前加上相對路徑（`"images/page1.png"`）。若路徑錯誤，引擎會拋出明確的 `FileNotFoundException`，請務必再次確認檔名。

---

## 第 4 步：對所有圖像執行非同步 OCR

`RecognizeImagesAsync` 方法會回傳 `OcrResult` 陣列。因為是 async，UI（或主控台）在 OCR 背景執行時仍保持回應。

```csharp
// Step 4: Perform async OCR on every image
OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);
```

**為什麼使用 async？**  
如果你將 OCR 整合到 Web API 或桌面應用程式，不希望執行緒在掃描每個像素時被阻塞。`await` 會將執行緒釋放回執行緒池，提升可擴充性。

---

## 第 5 步：顯示每頁的提取文字

取得結果後，遍歷它們並印出辨識出的文字。`Text` 屬性包含純文字輸出，可進一步處理（例如寫入資料庫）。

```csharp
// Step 5: Output the recognized text for every page
for (int i = 0; i < ocrResults.Length; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

### 預期輸出

假設 `page1.png` 內含 “Invoice #12345”，`page2.png` 內含 “Total: $89.99”，你會看到類似以下的結果：

```
--- Page 1 ---
Invoice #12345
Date: 03/28/2026
--- Page 2 ---
Total: $89.99
Paid by: Credit Card
```

如果 OCR 無法找到任何文字，`Text` 屬性會是空字串——在正式程式碼中請使用 `string.IsNullOrWhiteSpace` 進行檢查。

---

## 完整範例程式

以下是可直接貼到 `Program.cs` 的完整程式碼，包含所有 using 指令、async `Main`，以及說明每一步的註解。

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    // Async Main is supported from C# 7.1 onward
    static async Task Main()
    {
        // Step 1: Initialize the OCR engine and set the language to English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Step 2: Define the image files to be processed
        string[] imagePaths = { "page1.png", "page2.png", "page3.png" };

        // Step 3: Perform asynchronous OCR on all images
        OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);

        // Step 4: Output the recognized text for each page
        for (int i = 0; i < ocrResults.Length; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].Text);
        }
    }
}
```

儲存檔案、將 PNG 放在執行檔旁（或調整路徑），然後執行：

```bash
dotnet run
```

你應該會在主控台看到提取的文字，證明已成功 **將圖像轉換為文字**。

---

## 處理常見邊緣案例

| 情況 | 處理方式 |
|-----------|------------|
| **低解析度 PNG** | 在辨識前提升 `ocrEngine.ImageProcessingOptions.Dpi` |
| **多語言** | 設定 `ocrEngine.Language = Language.English | Language.Spanish;`（位元 OR） |
| **大量批次（數百檔）** | 分批處理（例如每次 `RecognizeImagesAsync` 呼叫 20 個檔案），以避免記憶體激增 |
| **需要信心分數** | 使用 `ocrResults[i].Confidence`（0 到 1 之間的浮點數）來過濾低品質結果 |

這些調整可讓你的 OCR 流程在從示範走向正式環境時保持穩定。

---

## 加分：將結果儲存為文字檔

如果想要永久保存而非只在主控台輸出，可加入以下小幫手：

```csharp
using System.IO;

// After the for‑loop:
File.WriteAllLines("OcrOutput.txt", ocrResults.Select(r => r.Text));
Console.WriteLine("All pages saved to OcrOutput.txt");
```

現在你擁有一個單一檔案，**從圖像提取文字**，可供下游處理——非常適合建立索引、搜尋或餵入語言模型。

---

## 結論

我們已逐步說明 **如何在 C# 中使用 OCR**，以 Aspose **從 PNG 檔案提取文字** 並 **將圖像轉換為文字**。非同步方式確保應用程式保持回應，簡潔的 API 讓程式碼易於閱讀與維護。  

試著用自己的文件跑一遍，實驗不同語言，甚至把輸出串接到搜尋索引或摘要服務。只要能可靠地把圖片變成可搜尋的字串，未來的可能性無限。

---

### 後續步驟與相關主題

- **從其他格式（JPEG、TIFF）提取文字** – 只需更改檔案副檔名。  
- **使用 Parallel.ForEach 進行批次處理**，適用於大量工作負載。  
- **OCR 後清理**，使用正規表達式正規化日期、金額或 ID。  
- **結合 Azure Cognitive Services**，若需要雲端 OCR 及額外功能。  

有任何問題或想分享你擴充的方式，歡迎留言。祝編程愉快！   ![OCR 結果螢幕截圖顯示提取的文字](/images/ocr-result.png){.align-center alt="如何使用 OCR 示例輸出"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}