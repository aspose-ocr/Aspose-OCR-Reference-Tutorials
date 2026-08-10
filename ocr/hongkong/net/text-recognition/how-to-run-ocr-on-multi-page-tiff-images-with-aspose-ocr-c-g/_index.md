---
category: general
date: 2026-02-11
description: 學習如何在 C# 中使用 Aspose OCR 進行多頁 TIFF 的 OCR。將 TIFF 轉換為文字，從 TIFF 提取文字，快速辨識圖像文字。
draft: false
keywords:
- how to run OCR
- recognize text from image
- convert tiff to text
- extract text from tiff
- perform OCR on image
language: zh-hant
og_description: 如何在 C# 中使用 Aspose OCR 於多頁 TIFF 執行 OCR。一步一步的指南，將 TIFF 轉換為文字、從 TIFF
  提取文字，以及從圖像識別文字。
og_title: 如何對多頁 TIFF 圖像執行 OCR – 完整 C# 教學
tags:
- OCR
- C#
- Aspose
- TIFF
title: 使用 Aspose OCR 在多頁 TIFF 圖像上執行 OCR – C# 指南
url: /zh-hant/net/text-recognition/how-to-run-ocr-on-multi-page-tiff-images-with-aspose-ocr-c-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose OCR 執行多頁 TIFF 圖像的 OCR

有沒有想過 **如何執行 OCR** 在包含多頁的掃描 TIFF 上？你並不孤單——許多開發人員在需要從舊文件中提取可搜尋文字時，都會碰到這個問題。好消息是？使用 Aspose OCR，只需幾行 C# 程式碼即可辨識圖像檔案中的文字，最終會得到可直接用於索引或後續處理的純文字串。

在本教學中，我們將完整說明工作流程：從安裝 Aspose OCR 套件、載入多頁 TIFF、將 TIFF 轉換為文字，最後顯示擷取的內容。完成後，你將能 **從 TIFF 檔案中擷取文字**、**從圖像來源辨識文字**，甚至在批次作業中自動處理數十個檔案。沒有魔法，只有清晰實用的步驟。

## 你將學會

- 如何為英文語言辨識設定 Aspose OCR 引擎。  
- 使用 `OcrEngine` 類別將 **TIFF 轉換為文字** 的完整程式碼。  
- 處理多頁圖像的技巧，確保每一頁正確分離。  
- 常見陷阱（例如缺少原生相依性）以及避免方法。  

**先備條件** – 需要 .NET 6 或更新版本、Visual Studio（或任何 C# 編輯器），以及可連網以下載自動資源的功能。就這些；不需要額外的原生函式庫。

---

## Step 1 – 安裝 Aspose OCR NuGet 套件

在能 **對圖像執行 OCR** 之前，必須先將程式庫加入專案。

```bash
dotnet add package Aspose.OCR
```

> **專業提示：** 若你在 Visual Studio 內工作，也可以右鍵點擊專案 → *Manage NuGet Packages* → 搜尋 “Aspose.OCR” 並點選 *Install*。

此套件已包含所有必需項目，且設定 `AutomaticResourceDownload = true` 後，引擎會即時下載語言套件。

---

## Step 2 – 初始化 OCR 引擎（How to Run OCR）

套件安裝完成後，我們建立並設定 `OcrEngine` 實例。這就是 **how to run OCR** 的核心。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;   // For Image class
using System;

// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // Recognize English text
    AutomaticResourceDownload = true,        // Auto‑download language data
    OutputFormat = OcrOutputFormat.Text      // Get plain concatenated text
};
```

**為什麼重要：** 設定 `Language` 告訴引擎預期的字元集，而 `AutomaticResourceDownload` 讓你免於手動放置語言檔案。將 `OutputFormat` 設為 `Text` 可取得簡單字串——非常適合 **convert TIFF to text** 的流程。

---

## Step 3 – 載入多頁 TIFF（Recognize Text from Image）

TIFF 可以包含多個影格，每個影格代表一頁。`System.Drawing.Image` 類別為我們抽象了這個概念。

```csharp
// Step 3: Load the multi‑page image to be processed
using (var image = Image.FromFile("YOUR_DIRECTORY/multi_page.tiff"))
{
    // Step 4: Run OCR on the image
    var ocrResult = ocrEngine.Recognize(image);

    // Step 5: Display the extracted text
    Console.WriteLine(ocrResult.Text);
}
```

> **如果檔案不在同一資料夾該怎麼辦？** 只要提供完整絕對路徑，或使用 `Path.Combine` 搭配 `AppContext.BaseDirectory`。  
> **記憶體使用量如何？** `using` 陳述式會在處理完畢後釋放影像，避免記憶體洩漏——在批次處理大量大型 TIFF 時尤為關鍵。

`Recognize` 呼叫會自動遍歷 TIFF 中的每一頁，並以換行符號串接結果。因此在列印 `ocrResult.Text` 時，你會看到每頁被分開。

---

## Step 4 – 完整範例（所有步驟於單一檔案）

以下是一個完整、可直接執行的主控台應用程式。將它貼到新的 .NET 主控台專案中，然後按 **F5**。

```csharp
// File: Program.cs
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Configure the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English,
                AutomaticResourceDownload = true,
                OutputFormat = OcrOutputFormat.Text
            };

            // 2️⃣ Load your multi‑page TIFF (replace with your actual path)
            const string tiffPath = @"YOUR_DIRECTORY\multi_page.tiff";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            // 3️⃣ Perform OCR
            using (var image = Image.FromFile(tiffPath))
            {
                var result = ocrEngine.Recognize(image);

                // 4️⃣ Output the extracted text
                Console.WriteLine("=== OCR RESULT ===");
                Console.WriteLine(result.Text);
                Console.WriteLine("==================");
            }

            // Keep console open
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**預期輸出**（為簡潔起見已截斷）：

```
=== OCR RESULT ===
Page 1: The quick brown fox jumps over the lazy dog.
Page 2: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
...
==================
Press any key to exit...
```

每一頁會各自佔一行，因為 `OcrOutputFormat.Text` 會在影格之間插入換行符號。如果需要不同的分隔符號，可使用 `String.Replace` 後處理 `result.Text`。

---

## Step 5 – 處理常見邊緣情況

### 5.1 大型 TIFF 檔案  
面對 GB 級別的 TIFF 時，將整個檔案載入記憶體可能會出問題。可行的做法是逐影格處理：

```csharp
using (var image = Image.FromFile(tiffPath))
{
    for (int i = 0; i < image.GetFrameCount(FrameDimension.Page); i++)
    {
        image.SelectActiveFrame(FrameDimension.Page, i);
        var pageResult = ocrEngine.Recognize(image);
        Console.WriteLine($"--- Page {i + 1} ---");
        Console.WriteLine(pageResult.Text);
    }
}
```

### 5. 非英文文件  
若需 **recognize text from image** 的語言為西班牙文或法文，只要更改 `Language` 屬性：

```csharp
ocrEngine.Language = OcrLanguage.Spanish; // or OcrLanguage.French
```

Aspose 會自動下載相應的語言資源。

### 5. 儲存輸出  
通常你會想 **convert TIFF to text** 並將結果存成 `.txt` 檔案：

```csharp
System.IO.File.WriteAllText("output.txt", ocrResult.Text);
```

也可以使用 `String.Split(Environment.NewLine)` 將輸出依頁分割，然後分別寫入不同檔案。

---

## Pro Tips & Gotchas

- **AutomaticResourceDownload** 只在第一次執行應用程式時下載資源，之後即可離線使用。  
- 若出現亂碼，請再次確認 `Language` 設定；語言套件不匹配會導致辨識錯誤。  
- 若 PDF 已被轉為 TIFF，建議提升 `ocrEngine.Dpi`（預設 300）以提升準確度。  
- 必須將 `Image.FromFile` 包在 `using` 區塊中，否則檔案會被鎖定，之後無法刪除或搬移。

---

## Frequently Asked Questions

**Q: 這能用於單頁 TIFF 嗎？**  
A: 完全可以。引擎會以相同方式處理單影格 TIFF，只會回傳一行文字。

**Q: 能否同樣方式處理 PNG 或 JPEG 檔案？**  
A: 可以，只要更改檔案副檔名即可。`Recognize` 方法接受任何 `System.Drawing.Image` 支援的格式。

**Q: 若需要 OCR 結果為 PDF 而非純文字該怎麼做？**  
A: 設定 `OutputFormat = OcrOutputFormat.Pdf`，`ocrResult` 便會包含 PDF 的位元組陣列，你可以寫入磁碟。

---

## Conclusion

現在你已擁有一套完整的端對端解決方案，能在 C# 中使用 Aspose OCR **how to run OCR** 多頁 TIFF 檔案。只要配置引擎、載入圖像，並呼叫 `Recognize`，即可 **extract text from TIFF**、**convert TIFF to text**、以及 **recognize text from image**，僅需幾行程式碼。隨時可以調整語言、輸出格式或逐影格處理，以符合自己的批次需求。

準備好下一步了嗎？試著將此方法與資料夾監看服務結合，讓系統在圖像檔案落入指定資料夾時自動 **perform OCR on image**，或將輸出整合至搜尋索引，實現即時全文搜尋。可能性無窮，而你剛看到的程式碼則是堅實的基礎。

如果在實作過程中遇到任何問題，歡迎在下方留言或在 GitHub 上私訊我。祝開發順利，享受將頑固的 TIFF 轉換為可搜尋文字的樂趣！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}