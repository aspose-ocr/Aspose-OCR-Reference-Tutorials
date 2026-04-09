---
category: general
date: 2026-04-08
description: 學習如何透過將圖像轉換為文字來閱讀西里爾字母。本分步指南展示如何對圖像檔案執行 OCR，並使用 Aspose OCR 提取俄文文字。
draft: false
keywords:
- how to read cyrillic
- convert image to text
- run ocr on image
- how to extract russian
- recognize cyrillic from image
language: zh-hant
og_description: 如何快速閱讀西里爾字母——對圖像執行 OCR，並使用 Aspose OCR 在 C# 中提取俄文文本。
og_title: 如何閱讀西里爾字母：使用 Aspose OCR 將圖像轉換為文字
tags:
- OCR
- C#
- Aspose
title: 如何閱讀西里爾文字：使用 Aspose OCR 將圖像轉換為文字
url: /zh-hant/net/text-recognition/how-to-read-cyrillic-convert-image-to-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何讀取西里爾字母：使用 Aspose OCR 將圖像轉換為文字

有沒有想過直接從螢幕截圖或掃描文件中 **讀取西里爾字母**？你並不是唯一有此需求的人——開發者經常需要從圖像中提取俄文文字，以進行資料輸入、本地化或聊天機器人訓練。好消息是？只要幾行 C# 程式碼加上 Aspose OCR，就能快速 **將圖像轉換為文字**。

在本教學中，我們將逐步說明完整流程：從安裝函式庫、設定俄文（西里爾）引擎，到實際 **在圖像上執行 OCR** 並顯示結果。完成後，你將能在 IDE 中 **提取俄文** 字元，並且看到如何可靠地 **從圖像中辨識西里爾字母**。

## 前置條件 — 開始之前需要的項目

- .NET 6.0 或更新版本（程式碼亦可在 .NET Core 3.1 上執行，但建議使用較新版本）
- Visual Studio 2022（或任何你喜歡的 C# 編輯器）
- Aspose OCR NuGet 套件 (`Aspose.OCR`) – 於套件管理員主控台安裝：
  ```powershell
  Install-Package Aspose.OCR
  ```
- 含有俄文西里爾文字的範例圖像，例如 `russian_sample.png`。  
  *(若沒有，可自行截取任意俄文網頁的螢幕截圖。)*

就這樣——不需要額外的 OCR 引擎，也不必編譯原生 DLL。Aspose 會自動下載語言資料，這也是此範例保持輕量的原因。

## 步驟 1：初始化 OCR 引擎（高效讀取西里爾字母）

我們首先建立一個 `OcrEngine` 實例。預設情況下，它會即時下載所需的語言套件，無需自行管理任何檔案。

```csharp
using Aspose.Ocr;
using System;

namespace CyrillicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – create the OCR engine with default options.
            var ocrEngine = new OcrEngine();   // auto‑download enabled
```

**為什麼重要：** 只初始化一次引擎並在多張圖像間重複使用，可減少額外開銷。自動下載功能會確保俄文語言資料 (`ru`) 已就緒，避免出現「找不到語言」的錯誤。

## 步驟 2：告訴引擎要辨識的語言

Aspose OCR 支援數十種語言，但必須明確設定語言代碼。俄文（西里爾）的 ISO‑639‑1 代碼為 `"ru"`。

```csharp
            // Step 2 – select Russian (Cyrillic) as the target language.
            ocrEngine.Language = "ru";
```

**小技巧：** 若需處理混合語言文件，可傳入逗號分隔的清單，例如 `"ru,en"`，引擎會同時嘗試。純西里爾文字時，使用 `"ru"` 可獲得最佳準確度。

## 步驟 3：在圖像檔案上執行 OCR

現在將圖像路徑傳入 `RecognizeImage`。此方法會回傳一個 `OcrResult` 物件，內含擷取的文字與信心分數。

```csharp
            // Step 3 – run OCR on the chosen image.
            var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/russian_sample.png");
```

**特殊情況：** 若圖像檔案過大（超過 5 MB），建議先調整尺寸；檔案過大會降低 OCR 準確度，且引擎載入時間會變長。

## 步驟 4：輸出辨識出的西里爾文字

最後，將結果印出至主控台。你也可以寫入檔案、資料庫，或傳遞給其他服務。

```csharp
            // Step 4 – display the recognized Cyrillic text.
            Console.WriteLine("Recognized Cyrillic text:");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

執行程式後，應會看到類似以下的輸出：

```
Recognized Cyrillic text:
Привет, мир! Это пример текста на русском языке.
```

這就是使用 Aspose OCR 完整的 **將圖像轉換為文字** 流程。

![顯示辨識出西里爾文字的主控台輸出截圖](/images/ocr-output.png "如何讀取西里爾字母結果")

## 在實際專案中執行圖像 OCR 的方法

上述程式碼適用於單一圖像，但在正式環境中通常需要處理多個檔案。以下提供一個可直接複製貼上的快速範例：

```csharp
static void ProcessFolder(string folderPath)
{
    var engine = new OcrEngine { Language = "ru" };

    foreach (var file in Directory.GetFiles(folderPath, "*.png"))
    {
        var result = engine.RecognizeImage(file);
        File.WriteAllText(Path.ChangeExtension(file, ".txt"), result.Text);
        Console.WriteLine($"Processed {Path.GetFileName(file)}");
    }
}
```

**為什麼要重複使用引擎？** 為每個檔案建立新的 `OcrEngine` 會重複下載語言資料，浪費 CPU 時間。保留單一實例可顯著提升吞吐量。

## 常見問題與如何精準提取俄文

| 症狀 | 可能原因 | 解決方法 |
|---------|--------------|-----|
| 文字亂碼（例如 `????`） | 語言代碼錯誤（`en` 而非 `ru`） | 設定 `ocrEngine.Language = "ru"` |
| 信心分數低 | 影像模糊或解析度低 | 前處理影像（提升 DPI、銳化） |
| 缺少變音符號 | 預設 OCR 模型不支援該字型 | 使用最新的 Aspose OCR 版本（v23.12+ 包含更好的西里爾支援） |
| 例外 “Unable to download language data” | 首次執行時無法連網 | 手動從 Aspose 入口網站下載語言套件，並透過 `OcrEngine.LanguageDataPath` 指向該路徑 |

解決上述問題即可確保你能高可靠性地 **從圖像中辨識西里爾字母**。

## 擴充範例 – 從主控台到 Web API

如果你在建構接受上傳圖像的 Web 服務，只需更換讀取檔案的部分：

```csharp
[HttpPost("ocr")]
public async Task<IActionResult> Upload(IFormFile image)
{
    using var stream = image.OpenReadStream();
    var engine = new OcrEngine { Language = "ru" };
    var result = engine.RecognizeImage(stream);
    return Ok(new { text = result.Text });
}
```

現在任何客戶端都能 **在圖像上執行 OCR**，即時取得俄文文字——非常適合翻譯流程或內容審核工具。

## 重點回顧 – 本文涵蓋內容

- 透過設定 Aspose OCR 的俄文語言，**如何讀取西里爾字母**。
- 完整可執行的範例，**將圖像轉換為文字** 並印出結果。
- 有關 **在圖像上執行 OCR** 批次處理、錯誤處理與擴展至 Web API 的技巧。
- 提供可靠 **提取俄文** 文字的解答，並說明常見問題。

你剛剛已將靜態 PNG 轉換為可編輯的西里爾字元——不再需要手動複製貼上。  

## 往後步驟與相關主題

- 嘗試使用 `ocrEngine.DetectOrientation` 以自動旋轉傾斜的掃描圖。
- 結合 OCR 與翻譯 API（Google Translate、Azure Translator），一次流程 **將圖像轉換為文字** 並再翻譯成英文。
- 若只需辨識圖像中特定區域的西里爾文字（例如表單欄位），可探索 Aspose 的 `OcrRegion` 功能，實現 **從圖像中辨識西里爾字母**。

如需烏克蘭語可將語言代碼改為 `"uk"`，或改為 `"bg"` 以支援保加利亞語——Aspose OCR 能處理整個西里爾字族。

對於特殊情況或效能調校有任何疑問嗎？歡迎在下方留言，祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}