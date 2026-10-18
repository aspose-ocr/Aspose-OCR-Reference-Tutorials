---
category: general
date: 2026-03-21
description: 如何在 C# 中使用 OCR 識別圖像檔案中的文字。學習從 JPG 中提取阿拉伯文字並將其轉換為純文字。
draft: false
keywords:
- how to use OCR
- extract arabic text
- recognize text from image
- image to text c#
- convert jpg to text
language: zh-hant
og_description: 如何在 C# 中使用 OCR 識別圖像檔案中的文字。本指南展示如何從 JPG 中提取阿拉伯文並將其轉換為可編輯的文字。
og_title: 如何在 C# 中使用 OCR – 從 JPG 提取阿拉伯文字
tags:
- OCR
- C#
- Aspose
- Arabic
title: 如何在 C# 中使用 OCR – 從 JPG 提取阿拉伯文字
url: /zh-hant/net/text-recognition/how-to-use-ocr-in-c-extract-arabic-text-from-jpg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 從 JPG 提取阿拉伯文字

有沒有想過 **如何使用 OCR**，當你手頭上有一張存放在硬碟上的阿拉伯文字圖片？你並不是唯一有此困惑的人。許多開發者都遇到同樣的問題：他們有 JPEG，需要裡面的文字，但又不想從頭自行編寫神經網路。  

好消息是？只要幾行 C# 程式碼，你就可以 **recognize text from image** 檔案，抽取每一個阿拉伯字元，得到一個乾淨的字串，方便儲存、搜尋或顯示。在本教學中，我們會一步步說明完整流程——安裝函式庫、設定語言模型、執行掃描，最後印出結果。完成後，你將能在幾秒鐘內 **convert JPG to text**。

## 你將學會

- 安裝 Aspose.OCR NuGet 套件（適用於 .NET）。
- 以 CPU 模式初始化 OCR 引擎（適合小型任務）。
- 自動載入阿拉伯語言模型。
- 在 JPEG 圖片上執行 OCR，取得辨識出的文字。
- 處理常見問題，如大型檔案或缺少語言資料。

不需要任何 OCR 先前經驗；只要具備基本的 C# 與 Visual Studio 知識即可。準備好了嗎？讓我們開始吧。

## 為 .NET 安裝 Aspose OCR

在撰寫任何程式碼之前，你必須先取得 Aspose.OCR 函式庫。它以 NuGet 套件的形式提供，只要執行一條指令即可安裝：

```bash
dotnet add package Aspose.OCR
```

或者，如果你偏好使用 Visual Studio 介面，請開啟 **Tools → NuGet Package Manager → Manage NuGet Packages for Solution**，搜尋 **Aspose.OCR**，然後點選 **Install**。此套件會把所有必需的檔案一起帶入，包括首次使用時引擎會下載的語言資料檔。

> **Pro tip:** 請將專案目標設定為 .NET 6 或更新版本；舊版框架仍可運作，但會錯失效能提升。

## 初始化 OCR 引擎

現在函式庫已就緒，我們可以建立 `OcrEngine` 的實例。對於大多數小規模任務，預設的 CPU 模式已足夠——它會使用主機的處理器，且不需要額外的 GPU 設定。

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialise the OCR engine (CPU mode is sufficient for small jobs)
var ocrEngine = new OcrEngine();
```

為什麼每次都要建立新引擎？`OcrEngine` 物件會保存語言、DPI、輸出格式等設定。將它的生命週期限制在單一操作內，可確保狀態乾淨，避免不同語言模型之間的交叉影響。

## 載入阿拉伯語言模型

Aspose 會按需下載語言套件。第一次指派 `Language.Arabic` 時，函式庫會將約 30 MB 的資料下載至本機快取資料夾。這一次性的下載讓之後的執行速度快如閃電。

```csharp
// Choose the language model to load.
// The first assignment triggers an automatic download of the language data (~30 MB).
ocrEngine.Settings.Language = Language.Arabic;
```

如果日後需要支援其他文字（例如 English 或 Hindi），只要更改列舉值即可——不需要額外程式碼。引擎會為每種語言分別快取。

## 在 JPG 圖片上執行 OCR

引擎與阿拉伯模型都已就緒，現在只要指向欲處理的圖片即可。路徑可以是絕對或相對，只要確保檔案存在且可讀取。

```csharp
// Run OCR on the input image.
var recognitionResult = ocrEngine.Recognize(@"YOUR_DIRECTORY/arabic_doc.jpg");
```

**Edge case:** 若你的 JPEG 檔案過大（超過 5 MB），建議先將其縮小。大型圖片會佔用較多記憶體，且可能拖慢辨識速度。使用 `System.Drawing` 或 `ImageSharp` 進行快速預縮放，可顯著縮短處理時間。

## 取得並顯示辨識出的文字

`Recognize` 方法會回傳一個 `OcrResult` 物件。其 `Text` 屬性即為引擎能讀取的純文字內容。

```csharp
// Retrieve the recognised text and output it.
string extractedText = recognitionResult.Text;
Console.WriteLine(extractedText);
```

執行程式後，你應該會在主控台看到阿拉伯字元，且保留原始的順序與換行。如果想把文字寫入檔案，只要使用 `File.WriteAllText` 即可。

### 完整可執行範例

將上述所有步驟整合，以下是一個完整、可直接執行的 Console 應用程式範例：

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine (CPU mode works fine for most cases)
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the Arabic language pack – triggers a one‑time download (~30 MB)
        ocrEngine.Settings.Language = Language.Arabic;

        // 3️⃣ Specify the image path – replace with your actual file location
        string imagePath = @"YOUR_DIRECTORY/arabic_doc.jpg";

        // 4️⃣ Run OCR and capture the result
        var result = ocrEngine.Recognize(imagePath);

        // 5️⃣ Extract the text and display it
        string extractedText = result.Text;
        Console.WriteLine("=== Extracted Arabic Text ===");
        Console.WriteLine(extractedText);
    }
}
```

**Expected output (example):**

```
=== Extracted Arabic Text ===
هذا نص تجريبي باللغة العربية
تم استخراج هذا النص بنجاح
```

如果輸出呈現亂碼，請再次確認圖片是否清晰、語言是否正確設定為 `Arabic`。模糊的掃描或旋轉的頁面是 OCR 常見的失敗原因。

## 常見問題與技巧

- **如果圖片同時包含阿拉伯文與英文該怎麼辦？**  
  設定 `ocrEngine.Settings.Language = Language.Multilingual;` 讓 Aspose 自動偵測多種文字。

- **可以使用 GPU 加速處理嗎？**  
  可以——如果你的電腦配備相容的顯示卡且已安裝 CUDA 執行環境，將預設引擎換成 `new OcrEngine(OcrEngineMode.Gpu)` 即可。

- **如何在 UI 中處理從右至左的排版？**  
  原始字串為 Unicode；大多數現代 UI 框架（WinForms、WPF、ASP.NET）在設定適當的 `FlowDirection` 後會自動支援 RTL 版面配置。

- **圖片大小有上限嗎？**  
  技術上沒有上限，但解析度越高記憶體消耗越大。對於極大檔案（例如整本掃描書籍），建議一次只處理一頁。

## 視覺概覽

以下是一張簡易圖示，說明從圖片檔案到文字抽取的流程：

![使用 OCR 流程圖 – 圖片轉文字轉換](/images/ocr-flow.png)

*Alt text:* *使用 OCR 流程圖顯示在 C# 中將圖片轉換為文字的過程*。

## 往後步驟

現在你已掌握 **如何使用 OCR** 來從阿拉伯語 JPEG 中 **extract Arabic text**，接下來可以擴充此解決方案：

- **批次處理：** 迴圈遍歷資料夾內的所有圖片，將每個結果寫入獨立的 `.txt` 檔案。
- **後處理：** 使用正規表達式清除多餘的標點或換行。
- **整合應用：** 將抽取出的字串導入搜尋索引（例如 Azure Cognitive Search），以實現對掃描文件的全文檢索。

如果你想嘗試其他語言，只要更換 `Language` 列舉值即可。想要抽取表格或手寫筆記？Aspose.OCR 也提供 `LayoutAnalysis` 功能，可在辨識前先分割區塊。

---

### 簡要重點

你現在已了解 **如何在 C# 中使用 OCR** 來 **extract Arabic text** 從 JPEG，亦能 **recognize text from image** 檔案並 **convert JPG to text**。上方的完整可執行範例示範了從安裝 NuGet 套件到印出最終字串的每一步。挑選一張範例圖片、貼上程式碼，即可見證魔法發生——不需任何外部服務。祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}