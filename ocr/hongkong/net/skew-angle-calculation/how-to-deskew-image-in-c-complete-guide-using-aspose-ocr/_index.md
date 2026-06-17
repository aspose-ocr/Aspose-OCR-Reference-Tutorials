---
category: general
date: 2026-03-21
description: 學習如何校正圖像文件的傾斜並使用 Aspose OCR 識別文字圖像。只需幾行 C# 程式碼，即可將 jpg 轉換為文字並校正圖像旋轉。
draft: false
keywords:
- how to deskew image
- recognize text image
- convert jpg to text
- correct image rotation
- recognize text jpg
language: zh-hant
og_description: 如何使用 Aspose OCR 校正圖像傾斜並從 JPEG 中提取文字。請參考此一步一步的指南，將 jpg 轉換為文字並校正圖像旋轉。
og_title: 如何在 C# 中校正圖像傾斜 – 快速 Aspose OCR 教程
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中去除圖像傾斜 – 使用 Aspose OCR 的完整指南
url: /zh-hant/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-guide-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中校正圖像傾斜 – 使用 Aspose OCR 的完整指南

有沒有想過 **how to deskew image** 檔案在掃描器掃出時會傾斜？你並不孤單——許多開發者在嘗試從收據、發票或手寫筆記中提取文字時，都會遇到這個問題。好消息是，使用 Aspose OCR，你可以校正圖像旋轉，並只用幾行程式碼就取得乾淨、可搜尋的文字。

在本教學中，我們將逐步說明整個流程：從安裝函式庫、啟用自動校正傾斜、辨識文字圖像，最後將 JPG 轉換為文字。完成後，你將擁有一個可直接執行的主控台應用程式，能 **recognize text jpg** 檔案而無需先手動旋轉。

## 需要的環境

- **.NET 6.0** 或更新版本（此程式碼同時適用於 .NET Core 與 .NET Framework）  
- **Aspose.OCR for .NET** NuGet 套件 – 建議使用 23.12 或更新版本  
- 一個範例 **skewed JPEG**（例如 `skewed_receipt.jpg`），放在應用程式可讀取的位置  
- Visual Studio、VS Code，或任何你偏好的 C# 編輯器  

不需要其他第三方工具。此函式庫內部已處理校正傾斜、OCR 以及語言偵測。

![校正圖像示例](/images/deskew-example.png "使用 Aspose OCR 校正圖像")

## 步驟 1：設定專案並安裝 Aspose.OCR

為了保持整潔，先建立一個全新的主控台專案：

```bash
dotnet new console -n DeskewDemo
cd DeskewDemo
dotnet add package Aspose.OCR --version 23.12.0
```

`dotnet add package` 指令會下載 **Aspose.OCR** 二進位檔及所有原生相依性。若你在 Windows 上，會自動取得原生 DLL；在 Linux/macOS 上，可能需要自行安裝 `libgdiplus` 套件，但這只需安裝一次。

## 步驟 2：啟用自動校正傾斜（修正圖像旋轉）

現在開啟 `Program.cs`，將其內容替換為以下程式碼。此處的關鍵行是 `ocrEngine.Settings.Deskew = true;` —— 這個旗標會告訴引擎自動 **how to deskew image**。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Create an OCR engine (CPU mode is fine for most desktop apps)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------------
            // 2️⃣ Turn on deskewing – this corrects image rotation for us
            // ---------------------------------------------------------------
            ocrEngine.Settings.Deskew = true;   // <-- how to deskew image is handled here

            // ---------------------------------------------------------------
            // 3️⃣ Point the engine at the JPEG you want to process
            // ---------------------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/skewed_receipt.jpg";

            // ---------------------------------------------------------------
            // 4️⃣ Run OCR – the result already contains the corrected text
            // ---------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(imagePath);

            // ---------------------------------------------------------------
            // 5️⃣ Output the text – this is your “convert jpg to text” step
            // ---------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### 為什麼要啟用 Deskew？

當掃描器以角度掃入頁面時，文字基線會傾斜。傳統 OCR 引擎會把每個字元當作傾斜的版本來辨識，導致準確度大幅下降。將 `Deskew = true` 設為開啟後，Aspose OCR 會在底層執行快速的 Hough 變換，將位圖旋轉回水平，然後再進行辨識。其效果等同於你在 Photoshop 手動旋轉圖像——但更快且全自動。

## 步驟 3：辨識文字圖像並將 JPG 轉換為文字

`Recognize` 呼叫同時執行兩件事：

1. **Deskews** 圖像（因為我們已開啟此旗標）。  
2. **Extracts** 文字內容，並以 `OcrResult` 物件回傳。

你可以將 `ocrResult.Text` 視為普通字串，寫入檔案，或傳入後續的處理流程。若需要每個詞的原始信心分數，可使用 `ocrResult.Words`，它會提供包含 `Confidence` 值的集合。

### 範例輸出

假設 `skewed_receipt.jpg` 為一張簡單的收據，你可能會看到類似以下的輸出：

```
=== Recognized Text ===
Store: Coffee Corner
Date: 2026-03-20
Item   Qty   Price
Latte   2    5.00
Bagel   1    2.50
Total          12.50
```

請注意，儘管原始圖像旋轉了約 7°，數字仍能整齊對齊。這就是內建於函式庫的 **correct image rotation** 魔法。

## 步驟 4：執行範例並驗證結果

編譯並執行：

```bash
dotnet run
```

如果一切設定正確，你會在主控台看到擷取出的文字。若出現 `FileNotFoundException` 等例外，請再次確認 JPEG 的路徑，並確保檔案可讀取。

### 常見陷阱與專業提示

- **Large Images** – OCR 記憶體使用量會隨圖像尺寸增長。請在送入引擎前將過大的檔案（例如寬度 > 3000 px）重新調整大小。  
- **Non‑Latin Scripts** – 預設情況下引擎假設使用英語。若需在其他字母系統中 **recognize text image**，請設定 `ocrEngine.Settings.Language = OcrLanguage.French;`（或任何支援的語言）。  
- **Batch Processing** – 處理大量檔案時，請重複使用同一個 `OcrEngine` 實例；為每個檔案建立新引擎會產生不必要的開銷。  
- **Quality Check** – 校正傾斜後，你可以透過 `ocrEngine.Settings.DeskewedImage.Save("corrected.jpg");` 匯出校正後的位圖，以目視驗證旋轉修正。

## 完整可執行範例（全部整合）

以下是完整、獨立的程式，你可以直接複製貼上到 `Program.cs`。它包含註解、錯誤處理，以及可選的儲存校正後圖像步驟。

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the input JPEG – change this to your actual file location
            string inputPath = @"YOUR_DIRECTORY\skewed_receipt.jpg";

            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: File not found – {inputPath}");
                return;
            }

            try
            {
                // 1️⃣ Create OCR engine (CPU mode is sufficient for most scenarios)
                var ocrEngine = new OcrEngine();

                // 2️⃣ Enable automatic deskewing – this is the core of how to deskew image
                ocrEngine.Settings.Deskew = true;

                // Optional: Save the corrected image to verify the rotation fix
                // ocrEngine.Settings.DeskewedImagePath = "corrected.jpg";

                // 3️⃣ Perform OCR – this simultaneously deskews and extracts text
                OcrResult result = ocrEngine.Recognize(inputPath);

                // 4️⃣ Output the recognized text – effectively convert jpg to text
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.WriteLine("An unexpected error occurred:");
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

執行此程式將 **recognize text jpg** 檔案，自動校正任何傾斜，並將乾淨、可搜尋的文字印出至主控台。

## 結語

現在你已擁有一段穩固、可投入生產環境的程式碼片段，示範如何使用 Aspose OCR **how to deskew image** 檔案並擷取其內容。此方法適用於收據、發票、掃描合約，或任何文字未完全水平的 JPEG。

你可以進一步探索以下方向：

- **Batch processing** 處理 JPEG 資料夾，並將每個結果寫入 `.txt` 檔（與 *convert jpg to text* 相關）。  
- 將 OCR 步驟整合至 ASP.NET Core API，讓客戶端上傳圖像並取得 JSON 格式的文字。  
- 嘗試不同的 OCR 設定，如 `ocrEngine.Settings.Language` 或 `ocrEngine.Settings.RecognitionMode`，以提升非英語文件的準確度。  

試試看，微調設定，讓引擎幫你完成繁重的工作。和往常一樣，若遇到問題或有巧妙的優化想分享，歡迎在下方留言。祝編程愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}