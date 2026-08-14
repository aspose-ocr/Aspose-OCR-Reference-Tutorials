---
category: general
date: 2026-02-20
description: 如何在 C# 中使用 OCR 讀取 PNG 圖片的文字 – 學習將圖片轉換為文字，快速擷取俄文文本。
draft: false
keywords:
- how to use ocr
- read text from png
- convert image to text
- recognize image text
- extract russian text
language: zh-hant
og_description: 在第一句說明了如何在 C# 中使用 OCR——一步一步的指南，教您從 PNG 讀取文字、將圖像轉換為文字，並提取俄文文字。
og_title: 如何在 C# 中使用 OCR – 完整指南
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中使用 OCR – 從 PNG 提取俄文文字
url: /zh-hant/net/text-recognition/how-to-use-ocr-in-c-extract-russian-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 OCR – 從 PNG 提取俄文文字

有沒有想過在 .NET 專案中 **如何使用 OCR**，卻不必花上數週去尋找合適的函式庫？你並不孤單。在許多實務應用中，我們需要 **從 PNG 讀取文字**，將圖片轉換成可搜尋的字串，有時還要提取俄文的西里爾字元以進行俄語處理。

在本教學中，我們將逐步示範一個實作範例，說明如何使用 Aspose.OCR **將影像轉換為文字**，以及 **辨識俄文影像文字**。完成後，你將擁有一個可直接執行的主控台程式，能夠 **從 PNG 檔案中提取俄文文字**，並提供一些日後可能遇到的特殊情況的技巧。

---

## 需要的環境

- .NET 6 SDK 或更新版本（此程式碼亦相容於 .NET Core 3.1+）  
- Visual Studio 2022 或任何你喜歡的編輯器（VS Code 亦可）  
- **Aspose.OCR** NuGet 套件 (`Install-Package Aspose.OCR`)  
- 含有俄文字符的範例 PNG（我們稱之為 `sample_russian.png`）

就這樣——不需要額外的原生 DLL、也不需要外部服務，甚至不需要繁雜的設定檔。準備好了嗎？讓我們開始吧。

---

## 步驟 1 – 初始化 OCR 引擎（how to use ocr）

當你想 **使用 OCR** 時，第一件事就是建立一個引擎實例。Aspose 會為你處理繁重的工作，包括在首次請求時下載西里爾語言套件。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Drawing;

// Create the OCR engine – this also triggers a one‑time download of language data
OcrEngine ocrEngine = new OcrEngine();
```

> **為什麼這很重要：** 引擎保存所有內部狀態（例如語言模型），並提供稍後會呼叫的 `Recognize` 方法。只建立一次並在多張圖片間重複使用，較之於每個檔案都新建物件更有效率。

---

## 步驟 2 – 載入 PNG 影像（read text from png）

引擎就緒後，你需要提供一張影像給它。**從 PNG 讀取文字** 的步驟相當直接，但有幾個需要注意的地方：

1. **檔案路徑** – 確保路徑為絕對路徑或相對於可執行檔的工作目錄。  
2. **資源釋放** – `Image` 實作了 `IDisposable`；請將其包在 `using` 區塊中以避免記憶體泄漏。

```csharp
string imagePath = @"YOUR_DIRECTORY\sample_russian.png";

using (Image russianImage = Image.FromFile(imagePath))
{
    // The image is now loaded and will be disposed automatically
}
```

> **專業提示：** 若使用串流（例如上傳的檔案），請使用 `Image.FromStream(stream)` 而非 `FromFile`。

---

## 步驟 3 – 選擇西里爾語言套件（extract russian text）

Aspose 內建多種語言套件，但預設為英文。由於我們的目標是 **提取俄文文字**，必須明確告訴引擎使用西里爾模型。

```csharp
ocrEngine.Language = Language.Cyrillic;   // Switches the OCR engine to Cyrillic
```

> **為什麼這很關鍵：** 若未設定 `Language.Cyrillic`，引擎會嘗試將字形解讀為拉丁字符，導致輸出亂碼。首次呼叫時可能需要數秒下載語言資料——之後會本機快取。

---

## 步驟 4 – 辨識並將影像轉換為文字（convert image to text）

這是本教學的核心：將圖片轉換成純文字字串。`Recognize` 方法正是執行此操作。

```csharp
using (Image russianImage = Image.FromFile(imagePath))
{
    // Perform OCR – this returns the detected text as a string
    string recognizedText = ocrEngine.Recognize(russianImage);

    // Show the result in the console
    Console.WriteLine("=== Recognized Russian Text ===");
    Console.WriteLine(recognizedText);
}
```

**預期的主控台輸出**（實際文字會依 PNG 內容而異）：

```
=== Recognized Russian Text ===
Привет, мир! Это пример текста на русском языке.
```

如果看到問號或隨機符號，請再次確認影像解析度足夠且已正確設定 `Language.Cyrillic`。

---

## 步驟 5 – 顯示與驗證辨識文字（recognize image text）

在實際應用中，你可能會將結果寫入資料庫、送入搜尋索引，或傳遞給翻譯 API。對於本教學而言，簡單的 `Console.WriteLine` 已足以證明我們能可靠地 **辨識影像文字**。

```csharp
Console.WriteLine("\nDone! The OCR engine has extracted the Russian text.");
```

> **邊緣情況：** 若 PNG 不含文字（或文字過於模糊），`Recognize` 會回傳空字串。務必做好防護：

```csharp
if (string.IsNullOrWhiteSpace(recognizedText))
{
    Console.WriteLine("No readable text found – try a clearer image or adjust DPI.");
}
```

---

## 完整範例程式

以下是完整程式碼，你可以直接貼到新的主控台專案（`dotnet new console`）中。它包含所有 using 陳述式、正確的資源釋放，以及少量錯誤處理。

```csharp
// ------------------------------------------------------------
// Full OCR example – extract Russian text from a PNG file
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine (downloads Cyrillic pack on first run)
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Path to the PNG that contains Russian text
        string imagePath = @"YOUR_DIRECTORY\sample_russian.png";

        // 3️⃣ Tell the engine to use Cyrillic (necessary for Russian)
        ocrEngine.Language = Language.Cyrillic;

        // 4️⃣ Load the image and run OCR
        using (Image russianImage = Image.FromFile(imagePath))
        {
            string recognizedText = ocrEngine.Recognize(russianImage);

            // 5️⃣ Output the result
            Console.WriteLine("=== Recognized Russian Text ===");
            Console.WriteLine(recognizedText);

            // Simple validation
            if (string.IsNullOrWhiteSpace(recognizedText))
            {
                Console.WriteLine("\n⚠️ No text detected – check image quality or language settings.");
            }
            else
            {
                Console.WriteLine("\n✅ OCR succeeded!");
            }
        }
    }
}
```

儲存檔案後，執行 `dotnet run`，即可在主控台看到嵌入於 PNG 中的俄文句子。 🎉

---

## 實用技巧與常見陷阱

| Situation | What to Do |
|-----------|------------|
| **影像解析度低** | 在 OCR 前提升 DPI（`new Bitmap(image, new Size(width*2, height*2))`）。 |
| **文字旋轉** | 使用 `ocrEngine.RotateImage` 或以 `System.Drawing` 先行處理以校正傾斜。 |
| **單張影像含多種語言** | 設定 `ocrEngine.Language = Language.Cyrillic | Language.English;` 以啟用混合偵測。 |
| **大量檔案批次處理** | 重複使用單一 `OcrEngine` 實例；每次迭代只需釋放 `Image` 物件。 |
| **在 Linux 上執行** | 確保已安裝 `libgdiplus`（`apt-get install -y libgdiplus`），因為 `System.Drawing.Common` 依賴它。 |

---

## 視覺摘要

![在 C# 中使用 OCR 的主控台輸出，顯示提取的俄文文字](ocr_console_output.png "在 C# 中使用 OCR – 範例輸出")

*上圖展示程式執行完畢後的主控台視窗，證明我們已成功 **從 PNG 讀取文字** 並 **將影像轉換為文字**。*

---

## 結論

我們已完整說明了在 C# 中 **如何使用 OCR**：從初始化引擎、載入 PNG、切換至西里爾語言套件、執行辨識，最後顯示提取的俄文句子。這段簡短程式展示了完整的 **將影像轉換為文字** 工作流程，並說明如何可靠地 **辨識影像文字**。

接下來的步驟？  
- 嘗試從多頁 PDF 中提取文字（Aspose.OCR 亦支援）。  
- 試驗其他語言套件（`Language.Arabic`、`Language.ChineseSimplified` 等）。  
- 將輸出接入翻譯服務或搜尋索引，讓你的應用真正支援多語言。

對於處理噪點掃描或將 OCR 整合至 Web API 有任何問題嗎？歡迎留言，祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}