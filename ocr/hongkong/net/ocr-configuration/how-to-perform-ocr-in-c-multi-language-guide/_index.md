---
category: general
date: 2026-04-29
description: 如何在 C# 中使用 Aspose OCR 執行文字辨識 – 提取印地語文字、從 PNG 識別文字，並即時變更 OCR 語言。
draft: false
keywords:
- how to perform OCR
- extract Hindi text
- multi language OCR
- recognize text from PNG
- change OCR language
language: zh-hant
og_description: 如何在 C# 中使用 Aspose OCR 執行文字辨識。學習提取印地語文字、辨識 PNG 檔案中的文字，並動態變更 OCR 語言。
og_title: 如何在 C# 中執行 OCR – 完整多語言教學
tags:
- OCR
- C#
- Aspose
title: 如何在 C# 中執行 OCR – 多語言指南
url: /zh-hant/net/ocr-configuration/how-to-perform-ocr-in-c-multi-language-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中執行 OCR – 多語言指南

有沒有想過 **如何在包含多種語言的圖像** 上執行 OCR？或許你手上同時有一張俄文收據和一張印地文傳單，需要一次取得兩者的文字，而不必切換不同工具。這是處理國際文件的人常見的困擾。

本教學將示範如何使用 Aspose OCR 以乾淨、端對端的方式 **執行 OCR**、擷取印地文文字、辨識 PNG 檔案中的文字，甚至即時 **變更 OCR 語言**。完成後，你將擁有一段可重複使用的程式碼，支援任意組合的支援語言。

## 你將學到什麼

- 如何在 .NET 專案中設定 Aspose OCR 引擎。  
- 靜態語言設定與執行時切換語言的差異。  
- 如何從影像中擷取印地文文字，以及為何此函式庫能自動下載語言套件。  
- 處理 PNG 檔案、應對缺少語言模組以及排除常見問題的技巧。

> **專業提示：** 若你已在單一語言上使用 Aspose OCR，只需調整幾行程式碼，即可將其轉換為 **多語言 OCR** 解決方案。

---

## 前置條件

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6 or later (or .NET Framework 4.7+) | Aspose OCR 針對現代執行環境；較舊版本可能缺少語言套件自動下載功能。 |
| Aspose.OCR NuGet package (`Install-Package Aspose.OCR`) | 提供 `OcrEngine` 類別與語言列舉。 |
| Two sample PNG images (`russian.png` and `hindi.png`) placed in a known folder | 示範 **recognize text from PNG** 與 **extract Hindi text** 的單次執行。 |
| Internet connection (for the first time you request a new language) | 函式庫會依需求即時下載所需的語言模組。 |

不需要額外的 OCR 二進位檔或外部工具——Aspose 已處理所有繁重工作。

---

## 步驟 1 – 安裝 Aspose OCR 並建立引擎

首先，將 Aspose OCR 套件加入專案。開啟 Package Manager Console 並執行：

```powershell
Install-Package Aspose.OCR
```

現在我們可以建立 `OcrEngine` 實例。把引擎想像成可在執行時重新設定的智慧掃描器。

```csharp
using Aspose.OCR;
using System;

class MultiLanguageOcrDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();
```

為什麼只建立一次引擎？重複使用同一個實例可避免多次載入原生 OCR 函式庫的開銷，對於大量批次處理尤為顯著。

---

## 步驟 2 – 辨識俄文文字（第一語言）

在切換到印地文之前，先證明引擎能正確處理已知語言。我們將語言設為俄文，輸入 PNG，並輸出結果。

```csharp
        // Step 2: Configure the engine for Russian and recognize the image
        ocrEngine.Config.Language = OcrLanguage.Russian;
        var russianImagePath = @"YOUR_DIRECTORY/russian.png";
        var russianOcrResult = ocrEngine.Recognize(OcrEngine.LoadImage(russianImagePath));
        Console.WriteLine("Russian: " + russianOcrResult.Text);
```

**底層發生了什麼？**  
`OcrEngine.LoadImage` 會將 PNG 讀入 Aspose 內部的 bitmap 格式。`Config.Language` 屬性告訴 OCR 引擎要使用哪套字典與字元集。呼叫 `Recognize` 時，引擎會執行針對西里爾字元調校的神經網路模型，並回傳包含純文字的 `OcrResult` 物件。

> **預期輸出（範例）**  
> `Russian: Привет, мир! Это тестовое изображение.`

如果看到亂碼，請確認影像未損毀且已安裝俄文語言模組（隨基礎套件一起提供）。

---

## 步驟 3 – 切換至印地文 – 動態 **變更 OCR 語言**

現在進入有趣的部分：在不重新建立引擎的情況下切換語言。第一次請求印地文時，Aspose OCR 會下載相應模組，只需一次網路連線即可。

```csharp
        // Step 3: Switch the engine to Hindi (the language module will be downloaded automatically) and recognize the image
        ocrEngine.Config.Language = OcrLanguage.Hindi;
        var hindiImagePath = @"YOUR_DIRECTORY/hindi.png";
        var hindiOcrResult = ocrEngine.Recognize(OcrEngine.LoadImage(hindiImagePath));
        Console.WriteLine("Hindi: " + hindiOcrResult.Text);
    }
}
```

**為什麼會這樣運作？**  
`Config.Language` 的 setter 會觸發延遲載入機制。若磁碟上沒有請求的語言套件，Aspose 會向 CDN 取得壓縮模組、快取下來，然後繼續辨識。此設計讓你能建立 **多語言 OCR** 流程，於執行時依內容自動調整。

> **範例印地文輸出**  
> `Hindi: नमस्ते दुनिया! यह एक परीक्षण छवि है।`

請留意同一個 `ocrEngine` 物件能無縫處理西里爾與天城文（Devanagari）腳本。這就是即時 **變更 OCR 語言** 的威力。

---

## 步驟 4 – 高效處理 PNG 檔案

上述兩個範例皆使用 PNG 圖片，這是螢幕截圖與掃描文件常見的格式。PNG 為無損格式，像素資料保持完整——非常適合 OCR。然而，大尺寸 PNG 可能佔用大量記憶體。以下提供幾個快速建議：

1. **必要時調整大小** – 若影像寬度超過 2000 px，使用 `System.Drawing.Image` 縮小後再交給 Aspose。  
2. **設定 DPI** – 部分 OCR 引擎在 300 DPI 下表現較佳。可透過接受自訂解析度 `Bitmap` 的 `OcrEngine.LoadImage` 重載來嵌入。

```csharp
using System.Drawing;

// Example of downscaling a huge PNG
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/large.png");
int maxWidth = 2000;
if (original.Width > maxWidth)
{
    int newHeight = (int)((double)original.Height / original.Width * maxWidth);
    Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));
    original.Dispose(); // free original memory
    original = resized;
}
var result = ocrEngine.Recognize(OcrEngine.LoadImage(original));
```

這些調整可降低記憶體使用，且常提升辨識準確度，因為 OCR 引擎處理的是較易管理的像素格線。

---

## 步驟 5 – 整合完整範例 – 完整可執行程式

以下為完整、可直接執行的程式碼，示範 **如何執行 OCR**、**擷取印地文文字**、**辨識 PNG 文字**，以及在不重新啟動引擎的情況下 **變更 OCR 語言**。

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class MultiLanguageOcrDemo
{
    static void Main()
    {
        // Create a single OCR engine instance (re‑use it for all languages)
        var ocrEngine = new OcrEngine();

        // ----------- Russian ----------
        ocrEngine.Config.Language = OcrLanguage.Russian;
        var russianPath = @"YOUR_DIRECTORY/russian.png";
        var russianResult = ocrEngine.Recognize(OcrEngine.LoadImage(russianPath));
        Console.WriteLine("Russian: " + russianResult.Text);

        // ----------- Hindi ------------
        // The first time this runs, the Hindi language pack will be downloaded automatically.
        ocrEngine.Config.Language = OcrLanguage.Hindi;
        var hindiPath = @"YOUR_DIRECTORY/hindi.png";
        var hindiResult = ocrEngine.Recognize(OcrEngine.LoadImage(hindiPath));
        Console.WriteLine("Hindi: " + hindiResult.Text);

        // ----------- Optional PNG optimization ----------
        // If you have very large PNGs, resize them before recognition (example shown earlier).
        // This block is optional and can be removed if your images are already sized appropriately.
    }
}
```

**執行程式** 後會輸出類似以下內容：

```
Russian: Привет, мир! Это тестовое изображение.
Hindi: नमस्ते दुनिया! यह एक परीक्षण छवि है।
```

若看到上述訊息，恭喜你——已成功建立一個 **多語言 OCR** 解決方案，能以單一引擎 **擷取印地文文字** 並 **辨識 PNG 檔案**。

---

## 常見問題 (FAQ)

| Question | Answer |
|----------|--------|
| *我需要 Aspose OCR 的授權嗎？* | 免費評估金鑰可用於測試，但正式使用需購買商業授權。 |
| *我可以在同一張影像中辨識超過兩種語言嗎？* | 可以。將 `Config.Language` 設為 `OcrLanguage.Multiple`，並傳入以逗號分隔的語言清單（例如 `Russian, Hindi`）。 |
| *如果語言模組下載失敗該怎麼辦？* | 請檢查防火牆或代理伺服器設定。也可以先從 Aspose 入口網站下載模組，放置於 `Data` 資料夾中。 |
| *PNG 是唯一支援的格式嗎？* | 不是。Aspose OCR 亦支援 JPEG、BMP、TIFF 以及 PDF（作為影像）。PNG 只是因其無損品質而常被選用。 |

---

## 往後步驟與相關主題

- **批次處理** – 迭代 PNG 目錄並將結果寫入 CSV 檔案。  
- **PDF 抽取** – 使用 `OcrEngine.RecognizePdf` 從掃描 PDF 中取得文字。  
- **自訂字典** – 以使用者提供的詞彙表擴充內建語言套件，適用於特定領域詞彙。  
- **效能調校** – 在處理大量影像時，使用 `Parallel.ForEach` 平行呼叫。

探索這些領域將深化你在各種情境下 **執行 OCR** 的掌握程度。

---

## 結論

你剛剛學會了如何在 C# 使用 Aspose OCR **執行 OCR**、即時切換語言，並成功從 PNG 圖片 **擷取印地文文字**。重點是單一的 `OcrEngine` 實例即可成為多功能的 **多語言 OCR** 工作馬——只要設定 `Config.Language`，其餘交由函式庫處理。

試跑程式碼，將範例圖片換成自己的，並嘗試其他語言。Aspose OCR 的彈性讓你能從快速原型輕鬆擴展至正式等級的文件處理流水線，只需極少的調整。

祝程式開發順利，文字擷取之旅無錯誤！ 

![how to perform OCR example](/images/ocr-demo.png "how to perform OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}