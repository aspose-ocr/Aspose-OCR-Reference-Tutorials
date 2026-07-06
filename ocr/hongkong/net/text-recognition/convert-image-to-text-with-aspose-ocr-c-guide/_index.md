---
category: general
date: 2026-02-14
description: 使用 Aspose OCR 在 C# 中將圖像轉換為文字。了解如何從圖片中提取阿拉伯文文字、載入圖像進行 OCR，並高效辨識阿拉伯文。
draft: false
keywords:
- convert image to text
- extract text from picture
- how to extract arabic text
- load image for ocr
- how to recognize arabic
language: zh-hant
og_description: 使用 Aspose OCR 在 C# 中將圖像轉換為文字。本教程展示如何從圖片中提取阿拉伯文字、載入圖像進行 OCR，以及識別阿拉伯文字。
og_title: 使用 Aspose OCR 將圖像轉換為文字 – C# 指南
tags:
- OCR
- C#
- Aspose
title: 使用 Aspose OCR 將圖像轉換為文字 – C# 指南
url: /zh-hant/net/text-recognition/convert-image-to-text-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose OCR 轉換影像為文字 – C# 指南

想在 C# 應用程式中 **convert image to text** 嗎？將影像轉換為文字是一項常見任務，尤其當你需要 **extract text from picture** 檔案且其中包含非拉丁文字時。本教學將逐步示範完整、可直接執行的範例，說明 **how to extract Arabic text**、**load image for OCR** 的方式，以及使用 Aspose.OCR 函式庫 **recognize Arabic** 字元的精確步驟。

我們會從安裝 NuGet 套件說起，並處理缺少字型或低解析度掃描等邊緣情況。完成後，你將擁有一個自包含的程式，能在主控台印出辨識出的阿拉伯文字——不需任何外部工具。

## 你將學到

- 如何將 Aspose.OCR 加入 .NET 專案（截至 2026 年的最新版本）
- 完整的 **convert image to text** 程式碼，以及每一行的意義
- 提升阿拉伯字形辨識準確度的技巧
- 如何 **load image for OCR**（從檔案路徑或串流）
- 常見問題的排除方法（例如語言設定錯誤、不支援的影像格式）

> **Pro tip:** 若你的目標是 .NET 6 或更新版本，可使用頂層語句（top‑level statements）讓程式碼更簡潔。以下範例仍採用傳統的 `Program` 類別，以確保相容性最高。

## 前置條件

- .NET 6 SDK（或任何較新的 .NET 版本）
- Visual Studio 2022 或搭配 C# 擴充功能的 VS Code
- NuGet 套件 `Aspose.OCR`（透過 `dotnet add package Aspose.OCR` 安裝）
- 含有阿拉伯文字的影像檔（例如 `arabic_sign.jpg`）

---

## Convert image to text – Step‑by‑step implementation

以下是完整的來源檔案，你可以直接複製貼上到新的主控台專案中。它包含 **所有必要的 `using` 指令**、`Main` 方法，以及說明每個操作背後原因的行內註解。

```csharp
// ------------------------------------------------------------
// Program.cs – Complete example to convert image to text
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine – this object holds the core logic.
            var ocrEngine = new Engine();

            // 2️⃣ Configure OCR options.
            //    We set the language to Arabic because the picture contains Arabic script.
            //    You can replace Language.Arabic with any other supported language.
            var ocrOptions = new OcrOptions
            {
                Language = Language.Arabic
            };

            // 3️⃣ Load the image you want to process.
            //    ImageStream.FromFile reads the file into a stream that Aspose can handle.
            //    If your image is in a different folder, adjust the path accordingly.
            var inputImage = ImageStream.FromFile("YOUR_DIRECTORY/arabic_sign.jpg");

            // 4️⃣ Run OCR – the Recognize method returns an OcrResult object.
            var ocrResult = ocrEngine.Recognize(inputImage, ocrOptions);

            // 5️⃣ Output the recognized text to the console.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### 預期輸出

如果 `arabic_sign.jpg` 內的文字為 **"مطار دولي"**（意即「International Airport」），主控台會顯示類似以下內容：

```
=== OCR Result ===
مطار دولي
```

實際拼寫可能因影像品質略有差異，但你應該會看到阿拉伯字元，而非亂碼。

---

## How to extract Arabic text – configuring language

為什麼必須明確設定 `Language = Language.Arabic`？Aspose.OCR 支援數十種語言，但預設為英文。阿拉伯文採用從右至左的書寫方向，且字形會根據上下文變形。告訴引擎正確的語言後，你即可獲得：

- **Ligature detection** – 例如「لا」這類連字的辨識
- **Right‑to‑left ordering** – 輸出字串會正確排列
- **Improved dictionary checks** – 引擎可參照阿拉伯詞彙表提升準確度

若需 **extract text from picture** 檔案且包含多種語言，可將多個 `Language` 列舉傳入 `OcrOptions.Language`（例如 `new[] { Language.Arabic, Language.English }`）。

---

## Load image for OCR – reading the picture

`ImageStream.FromFile(...)` 是 **load image for OCR** 最直接的方式。然而，你可能會遇到以下情況：

- 影像儲存在資料庫 BLOB 中
- 透過 HTTP 請求取得圖片
- 檔案為非標準格式（例如多頁 TIFF）

在這些情況下，你可以從 `MemoryStream` 建立 `ImageStream`：

```csharp
byte[] bytes = System.IO.File.ReadAllBytes("path/to/image.png");
using var memStream = new System.IO.MemoryStream(bytes);
var inputImage = ImageStream.FromStream(memStream);
```

兩種方式最終都會將相同的內部表示傳遞給引擎，因此 OCR 品質不會受到影響。

---

## How to recognize Arabic – running the engine

呼叫 `ocrEngine.Recognize(inputImage, ocrOptions)` 時，引擎會經過以下幾個內部階段：

1. **Pre‑processing** – 降噪、二值化與去斜。
2. **Segmentation** – 將影像切分為行、詞與字元。
3. **Classification** – 將每個切片對應至已知的阿拉伯字形。
4. **Post‑processing** – 套用語言規則與信心門檻。

若發現信心分數偏低，可考慮：

- **Increasing image resolution**（建議最低 300 dpi 才能有效辨識阿拉伯文）
- **Adjusting contrast**（在送入 OCR 前使用簡易影像處理函式庫，如 `System.Drawing` 或 `ImageSharp` 調整對比度）
- **Enabling `ocrOptions.UseLanguageDictionary = true`**（啟用更嚴格的字典檢查）

---

## Common pitfalls & how to avoid them

| 症狀 | 可能原因 | 解決方式 |
|---------|--------------|-----|
| 輸出為空白 | 檔案路徑錯誤或不支援的格式 | 核對路徑、使用 `File.Exists`，確保影像為 PNG/JPEG/BMP |
| 文字亂碼 | 未將語言設定為 Arabic | 在 `OcrOptions` 中設定 `Language = Language.Arabic` |
| 準確度低 | 影像模糊或解析度不足 | 使用更高解析度的來源，或套用銳化濾鏡 |
| 例外 `ArgumentNullException` | `inputImage` 為 null | 確認檔案存在且串流正確開啟 |

---

## Full working example (copy‑paste ready)

如果你偏好單一檔案且不使用命名空間，以下提供一個緊湊版，同時仍遵循最佳實踐：

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class ConvertImageToText
{
    static void Main()
    {
        // Engine creation
        var engine = new Engine();

        // Set OCR options – Arabic language
        var options = new OcrOptions { Language = Language.Arabic };

        // Load image – change the path to your actual file
        var image = ImageStream.FromFile("YOUR_DIRECTORY/arabic_sign.jpg");

        // Perform recognition
        var result = engine.Recognize(image, options);

        // Show result
        Console.WriteLine("=== Recognized Arabic Text ===");
        Console.WriteLine(result.Text);
    }
}
```

使用 `dotnet run` 執行程式，即可在主控台看到阿拉伯文字的輸出。

---

## Visual recap

以下是一張示意圖，展示主控台的 OCR 結果。**alt 文字** 已包含主要關鍵字以符合 SEO 規範。

![轉換影像為文字範例 – 顯示阿拉伯文 OCR 結果的主控台](convert-image-to-text-example.png)

---

## Conclusion

我們剛剛示範了如何在 C# 中使用 Aspose OCR **convert image to text**。本教學涵蓋了從安裝函式庫、設定語言以 **how to extract Arabic text**、載入圖片、以及最終 **how to recognize Arabic** 字元的完整流程。

掌握這些技巧後，你即可將 OCR 整合至任何 .NET 專案——無論是桌面工具、Web API，或是批次處理掃描文件的背景服務。

### 接下來該做什麼？

- 變更 `Language.Arabic` 為 `Language.French`、`Language.ChineseSimplified` 等，試驗其他語言
- 結合 **extract text from picture** 工作流程，將結果寫入資料庫
- 利用 `ocrResult.Confidence` 屬性過濾低信心的行，再進行持久化

對於邊緣案例或效能調校有任何疑問？歡迎在討論串留下評論或提問。祝開發順利，願你的影像總能產生乾淨、可搜尋的文字！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}